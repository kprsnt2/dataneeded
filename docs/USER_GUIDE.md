# JobAgents — User Guide

**Document:** JobAgents User Guide
**Date:** 2026-10-05
**Language:** ASD-STE100 Simplified Technical English

---

## 1. About this guide

This guide tells you how to use JobAgents. It has these parts:

- Part A tells you how to start the system.
- Part B tells you the daily steps.
- Part C tells you how to set the automatic time.
- Part D tells you how to repair problems.

Read Part A first. Then do Part B each day.

---

## 2. What JobAgents does

JobAgents finds jobs for you. It does five steps:

1. **Source.** It collects jobs from job boards.
2. **Match.** It gives each job a score. The score tells you if the job is good for you.
3. **Tailor.** It writes a resume for each good job.
4. **Draft.** It writes a message for each good job.
5. **Review.** It checks the messages for errors.

**Important:** JobAgents never sends a message. You must send each message yourself.

---

## 3. Words in this guide

| Word | Meaning |
|---|---|
| Pipeline | All five steps together |
| Run | One full pipeline operation |
| Window | The time limit for jobs. Example: the last 24 hours |
| Track | One group of job titles. There are three tracks |
| Score | A number from 0 to 100. A high number is good |
| Draft | A message that is not sent |

---

# PART A — START THE SYSTEM

## 4. Before you start

You need these items:

- A computer with Windows.
- Python version 3.10 or higher.
- The `omp` tool.
- The `agy` tool.
- The `pi` tool.
- A Fireworks API key.

## 5. Step 1: Open the terminal

1. Push the Windows key.
2. Type `PowerShell`.
3. Push Enter.

## 6. Step 2: Go to the JobAgents folder

Type this command:

```powershell
cd D:\JobAgents
```

Push Enter.

## 7. Step 3: Do the doctor check

The doctor check finds bad tools. Type this command:

```powershell
python -m jobagents doctor
```

Push Enter. Wait 30 seconds.

**Good result:** You see three lines. Each line starts with `OK`.

```
[OK  ] omp   fireworks/deepseek-v4.1-flash      OMP_OK
[OK  ] agy   gemini-3.8-flash-low               AGY_OK
[OK  ] pi    accounts/fireworks/models/...      PI_OK
```

**Bad result:** You see `FAIL`. Go to Part D, section 20.

---

# PART B — DAILY STEPS

## 8. Step 4: Do the first run

The first run collects jobs from the last 7 days. Type this command:

```powershell
python -m jobagents run --since 7d --linkedin --search
```

Push Enter. Wait 15 to 25 minutes.

**Note:** The first run is slow. Later runs are faster.

## 9. Step 5: Look at the results

Type this command:

```powershell
python -m jobagents summary --pretty
```

Push Enter. You see a report. Read these numbers:

| Number | Meaning |
|---|---|
| `jobs_total` | All jobs in the database |
| `jobs_last_24h` | Jobs from the last day |
| `matches_above_threshold` | Good jobs for you |
| `resumes_written` | New resumes |
| `drafts_pending` | Messages that wait for you |

## 10. Step 6: Open the dashboard

1. Type this command:

```powershell
python -m jobagents web --port 8787
```

2. Push Enter.
3. Open your browser.
4. Go to `http://127.0.0.1:8787`.

The dashboard has five tabs:

| Tab | What you do here |
|---|---|
| Analytics | Look at numbers and charts |
| Jobs | Look at all jobs. Filter by score |
| Resume Studio | Change your profile and keywords |
| Review Queue | Approve or reject messages |
| Runs | Look at past runs |

**Note:** To stop the dashboard, push `Ctrl` and `C` together.

## 11. Step 7: Read your resumes

Your new resumes are in this folder:

```
D:\JobAgents\generated\
```

Each file has this name:

```
company__job_title__job_number.md
```

Open a file. Read it. Check these items:

- The facts are correct.
- The numbers are correct.
- The job title is correct.

**If a fact is wrong:** Do not use the file. Go to Part D, section 21.

## 12. Step 8: Send your messages

1. Go to the Review Queue tab.
2. Read each message.
3. Push **Approve** or **Reject**.
4. Copy the approved message.
5. Send the message yourself.

**Warning:** JobAgents cannot send messages. This is correct. It prevents account problems.

## 13. Step 9: Do the daily run

After the first run, do this command each day:

```powershell
python -m jobagents run --since 24h
```

This command finds jobs from the last 24 hours only. It is fast.

**Note:** You do not need the `--linkedin` and `--search` flags each day. Use them two times each week.

---

# PART C — AUTOMATIC OPERATION

## 14. Step 10: Set the automatic time

You can make JobAgents run by itself each day at 09:00.

1. Open PowerShell as Administrator. To do this:
   - Push the Windows key.
   - Type `PowerShell`.
   - Push the right mouse button on **Windows PowerShell**.
   - Push **Run as administrator**.
2. Type this command:

```powershell
cd D:\JobAgents
powershell -ExecutionPolicy Bypass -File scripts\install_schedule.ps1
```

3. Push Enter.

**Good result:** You see this text:

```
Registered 'JobAgents-Daily'.
  time        : 09:00 daily
  wake PC     : yes
```

## 15. What the automatic run does

| Item | Value |
|---|---|
| Time | 09:00 each day |
| Wake the computer | Yes |
| Start if the computer was off | Yes |
| First run | Collects 7 days |
| Later runs | Collects 24 hours |

## 16. Step 11: Check the automatic run

Type this command:

```powershell
schtasks /Query /TN "JobAgents-Daily" /V /FO LIST
```

Push Enter. Look for `Next Run Time`.

## 17. Step 12: Start the automatic run now

You do not need to wait until 09:00. Type this command:

```powershell
schtasks /Run /TN "JobAgents-Daily"
```

Push Enter.

## 18. Step 13: Read the log files

The log files are in this folder:

```
D:\JobAgents\logs\
```

| File | What it has |
|---|---|
| `daily-YYYY-MM-DD.log` | All text from one run |
| `daily-history.csv` | One line for each run |
| `last-run.json` | The last run in computer format |

To read the last run, type this command:

```powershell
Get-Content logs\last-run.json | ConvertFrom-Json | Format-List
```

## 19. Step 14: Stop the automatic run

Type this command:

```powershell
schtasks /Delete /TN "JobAgents-Daily" /F
```

Push Enter.

---

# PART D — REPAIR PROBLEMS

## 20. Problem: The doctor check shows FAIL

**Cause:** A tool is missing or the model name is wrong.

**Action:**

1. Type this command:

```powershell
python -m jobagents doctor
```

2. Read the `FAIL` line. It tells you which tool is bad.
3. Make sure the tool is on your PATH. Type this command:

```powershell
Get-Command omp, agy, pi
```

4. If a tool is missing, install it again.

## 21. Problem: A resume has a wrong fact

**Cause:** The model wrote a fact that is not true.

**Action:**

1. Open this file:

```
D:\JobAgents\config\profile.md
```

2. Find the wrong fact.
3. If the fact is true, add it to the file.
4. If the fact is false, do nothing. The check system must stop it.
5. Do a new run.

**Note:** JobAgents checks each resume before it writes the file. The system rejects a resume with a false fact. You can see the rejected resumes in the `rejected` number of the run report.

## 22. Problem: No new jobs

**Cause:** The window is too small. Or the job boards have no new jobs.

**Action:**

1. Make the window larger. Type this command:

```powershell
python -m jobagents run --since 7d
```

2. If you still have no jobs, do the source step only:

```powershell
python -m jobagents source
```

## 23. Problem: The dashboard does not open

**Cause:** The port is in use. Or the program stopped.

**Action:**

1. Make sure the command is still active in the terminal.
2. Use a different port. Type this command:

```powershell
python -m jobagents web --port 8899
```

3. Go to `http://127.0.0.1:8899`.

## 24. Problem: The automatic run did not start

**Cause:** The computer was off. Or the automatic task is disabled.

**Action:**

1. Type this command:

```powershell
schtasks /Query /TN "JobAgents-Daily" /V /FO LIST
```

2. Look at `Status`. If the status is `Disabled`, type this command:

```powershell
schtasks /Change /TN "JobAgents-Daily" /ENABLE
```

3. Look at `Last Run Time` and `Last Result`.
4. If `Last Result` is not `0`, read the log file.

**Note:** The computer can be off at 09:00. Then the run starts when you turn the computer on. You do not lose jobs.

## 25. Problem: The run is very slow

**Cause:** The `--linkedin` and `--search` flags make the run slow.

**Action:** Do not use these flags each day. Use them two times each week. Type this command:

```powershell
python -m jobagents run --since 24h
```

---

## 26. Command list

| Command | What it does |
|---|---|
| `python -m jobagents doctor` | Checks the tools |
| `python -m jobagents source` | Collects jobs only |
| `python -m jobagents match` | Scores jobs only |
| `python -m jobagents tailor --limit 5` | Writes resumes only |
| `python -m jobagents outreach` | Writes messages only |
| `python -m jobagents review` | Checks messages only |
| `python -m jobagents run` | Does all five steps |
| `python -m jobagents run --dry-run` | Shows the plan. No cost. No changes |
| `python -m jobagents summary --pretty` | Shows a report |
| `python -m jobagents web` | Starts the dashboard |
| `python -m jobagents stats` | Shows database numbers |

## 27. Run flags

| Flag | What it does |
|---|---|
| `--since 7d` | Jobs from the last 7 days |
| `--since 24h` | Jobs from the last 24 hours |
| `--since 90m` | Jobs from the last 90 minutes |
| `--linkedin` | Also uses LinkedIn. Slow |
| `--search` | Also uses web search. Uses model calls |
| `--tailor-limit 10` | Writes 10 resumes |
| `--draft-limit 10` | Writes 10 messages |
| `--dry-run` | Shows the plan. No changes |
| `--stages match,tailor` | Does two steps only |

---

## 28. Safety rules

Obey these rules:

1. **Do not** let JobAgents send messages. Send them yourself.
2. **Do not** open the dashboard to other computers. Use `127.0.0.1` only.
3. **Do not** put your API key in a file in this folder.
4. **Do not** put your resume in the git repository.
5. **Do not** tell other people about the BugAgents findings. The reports are not public.

---

## 29. Files you can change

| File | What it controls |
|---|---|
| `config\profile.md` | Your facts. Your skills. Your numbers |
| `config\keywords.md` | Job titles. Keywords. Score limits |

**Important:** These two files control all agents. Change them with care.

Before you change a file, make a copy:

```powershell
Copy-Item config\profile.md config\profile.backup.md
```

---

*End of guide.*
