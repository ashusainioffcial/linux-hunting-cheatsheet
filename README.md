# 🐧 Linux Incident Response & System Threat Hunting Cheat Sheet

This reference document catalogs essential native terminal command structures and log-slicing pipelines utilized by L1/L2 Security Analysts to inspect compromised infrastructure endpoints, audit connections, and count risk vectors.

---

## 🌐 1. Live Socket & Network Infrastructure Inspection
Use these commands to trace active network exposure pathways and detect rogue backdoor channels.

- `netstat -ano | head -n 20` — Monitors the first 20 active network sockets, tracking external connections, listening states, and corresponding system Process IDs (PIDs) on Windows-based terminal environments.
- `ss -tulpn` — Native Linux command to display running network services, listening ports, and owning system processes dynamically.
- `netstat -tuln` — Views all active TCP and UDP listening channels without DNS resolution overhead to keep triage high-speed.

---

## 📂 2. High-Velocity Log Filtering Pipelines (`awk`)
Use text processing pipelines to aggregate unstructured string logs and isolate core targets.

- `awk -F ' - ' '{print $3}' auth_log.txt | sort | uniq -c | sort -nr`
  - `-F ' - '` — Establishes space-hyphen-space as the custom delimiter boundary.
  - `print $3` — Pinpoints the third column sector containing target account variables.
  - `sort | uniq -c | sort -nr` — Stitches sorting algorithms and unique counters to render a descending threat metrics list.

---

## 📊 3. Live System Asset Triage
Monitor local user profiles and operating footprints to map administrative changes.

- `cat /etc/passwd` — Audits all local system account architectures to look for hidden accounts added by intruders.
- `last -f /var/log/wtmp` — Views historical logs of user authentication sessions to isolate time stamps of unauthorized access.
- `ps aux | grep root` — Audits every single running processor stack owned by high-clearance privileges to stop live memory injection vectors.
