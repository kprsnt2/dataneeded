# JobAgents — Daily automation (Windows Task Scheduler)

Runs the full pipeline every day at **09:00 IST**, waking the machine if it is
asleep, then reports the result.

---

## Install

Run once, from an **elevated** PowerShell (needed to set "wake the computer"):

```powershell
cd D:\JobAgents
powershell -ExecutionPolicy Bypass -File scripts\install_schedule.ps1
```

That registers a task named **`JobAgents-Daily`** with these properties:

| Setting | Value |
|---|---|
| Trigger | Daily at **09:00** local time |
| Wake the computer | **Yes** (`-WakeToRun`) |
| Run whether user is logged on | Yes |
| Start when available | Yes (catches up if the machine was off) |
| Execution limit | 2 hours |
| Retry on failure | 3 attempts, 15 min apart |
| First run window | `--since 7d` (backfill) |
| Subsequent runs | `--since 24h` (automatic) |

The window is automatic: the orchestrator checks the last successful run and
picks up from there, so you do not manage it by hand.

---

## Manual control

```powershell
# Run the pipeline now, exactly as the scheduled task would
powershell -ExecutionPolicy Bypass -File scripts\run_daily.ps1

# See the task definition
schtasks /Query /TN "JobAgents-Daily" /V /FO LIST

# Run the scheduled task immediately (uses the same settings as 9am)
schtasks /Run /TN "JobAgents-Daily"

# Disable / re-enable without deleting
schtasks /Change /TN "JobAgents-Daily" /DISABLE
schtasks /Change /TN "JobAgents-Daily" /ENABLE

# Remove entirely
schtasks /Delete /TN "JobAgents-Daily" /F
```

---

## Logs

```
logs/
  daily-YYYY-MM-DD.log      full stdout/stderr of each run
  daily-history.csv         one row per run: date, status, counts, duration
  last-run.json             machine-readable summary of the most recent run
```

Check the last run at a glance:

```powershell
Get-Content logs\last-run.json | ConvertFrom-Json | Format-List
Import-Csv logs\daily-history.csv | Select-Object -Last 10 | Format-Table
```

---

## If the machine was off at 9am

"Start when available" makes the task run as soon as the machine is next on.
Because the window is derived from the last successful run, the catch-up run
covers everything missed rather than only the last 24 hours — no jobs are lost.

To confirm a catch-up happened:

```powershell
Import-Csv logs\daily-history.csv |
  Where-Object { $_.window -ne '1.00:00:00' } |
  Select-Object -Last 5 | Format-Table
```

---

## Laptop-specific notes

**On battery:** Task Scheduler will not wake a machine that is hibernating on
battery by default. Either keep it plugged in overnight, or set:

```powershell
# Allow wake on battery for this task
$t = Get-ScheduledTask -TaskName "JobAgents-Daily"
$t.Settings.DisallowStartIfOnBatteries = $false
$t.Settings.StopIfGoingOnBatteries = $false
Set-ScheduledTask -TaskName "JobAgents-Daily" -Settings $t.Settings
```

**If the lid is closed:** waking is unreliable. "Start when available" still
catches up once the lid opens.

---

## Verifying it works without waiting for 9am

```powershell
# 1. Dry run — proves the pipeline wires up, costs nothing, writes nothing
python -m jobagents run --dry-run

# 2. Run the wrapper script directly
powershell -ExecutionPolicy Bypass -File scripts\run_daily.ps1

# 3. Force the scheduled task now and check the log
schtasks /Run /TN "JobAgents-Daily"
Start-Sleep -Seconds 30
Get-Content logs\last-run.json
```

---

## Why the task runs a script instead of `python` directly

`scripts/run_daily.ps1` exists to make the scheduled run robust and observable:

- resolves the repo root regardless of the task's working directory
- injects `FIREWORKS_API_KEY` from `~/.pi/agent/auth.json` (so no secret is
  stored in the task definition)
- writes dated logs and appends a CSV history row
- converts failures into a non-zero exit code so Task Scheduler records them
- never leaves a half-written `last-run.json` (writes to a temp file, then moves)
