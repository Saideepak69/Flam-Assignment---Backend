"# Flam-Assignment---Backend(QueueCTL)" 

# queuectl — CLI-Based Background Job Queue System

> A Python-based background job queue system.  
> It manages background jobs using worker processes, supports automatic retries with exponential backoff, and includes a Dead Letter Queue (DLQ) for permanently failed jobs — all through an intuitive CLI.

---

## Demo Video
 **Watch the Full Demo Here:**  
[https://drive.google.com/file/d/1Eiz7GD2bJCbzXHfA1Pze6eIAf6sWUWyO/view?usp=sharing](https://drive.google.com/file/d/1Eiz7GD2bJCbzXHfA1Pze6eIAf6sWUWyO/view?usp=sharing)

---

## Features
-  Enqueue and manage background jobs  
-  Run multiple worker processes concurrently  
-  Automatic retry with exponential backoff  
-  Dead Letter Queue (DLQ) for failed jobs  
-  Persistent SQLite storage (no data loss)  
-  Configurable retry limit and backoff base  
-  Simple, modular, and easy-to-use CLI  

---

## Tech Stack
| Component | Technology |
|------------|-------------|
| **Language** | Python 3.8+ |
| **Database** | SQLite |
| **Concurrency** | Multiprocessing |
| **CLI Parser** | argparse |
| **Logging** | Python `logging` module |

---

## Job Schema
```json
{
  "id": "unique-job-id",
  "command": "echo 'Hello World'",
  "state": "pending",
  "attempts": 0,
  "max_retries": 3,
  "created_at": "2025-11-08T10:00:00Z",
  "updated_at": "2025-11-08T10:00:00Z"
}

```
## How to run a demo:
  # Step 1: Install Dependencies
    pip install -r requirements.txt
  
  # Step 2: Verify Python Version
    python --version
  
  # Step 3: Initialize the System
    python queuectl.py status
  
  # Step 4: Enqueue Jobs
    python queuectl.py enqueue "{\"id\":\"job1\",\"command\":\"echo Hello Deepak\"}"
    python queuectl.py enqueue "{\"id\":\"job2\",\"command\":\"echo Task 2 Running...\"}"
    python queuectl.py enqueue "{\"id\":\"job3\",\"command\":\"timeout 3\"}"
    python queuectl.py enqueue "{\"id\":\"job4\",\"command\":\"notarealcommand\"}"   # To test retry & DLQ

  # Step 5: List Jobs
    python queuectl.py list
    python queuectl.py list --state pending

  # Step 6: Start Workers
    start python queuectl.py worker start --count 2

  # Step 7: Monitor Status
    python queuectl.py status

  # Step 8: Check the Dead Letter Queue (DLQ)
    python queuectl.py dlq list

  # Step 9: Retry DLQ Jobs
    python queuectl.py dlq retry job4

  # Step 10: Update Configuration
    python queuectl.py config show
    python queuectl.py config set max_retries 5
    python queuectl.py config set backoff_base 3

  # Step 11: Delete Jobs
    Step 12 — Delete Jobs

  # Step 12: Stop Workers
    python queuectl.py worker stop

  # Step 14 — Check Logs
    notepad queuectl.log
