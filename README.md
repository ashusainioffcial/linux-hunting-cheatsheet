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

---

## 🔒 4. Linux Host Hardening & SSH Infrastructure Security
Proactive terminal configuration steps to close system attack surfaces and block automated brute-force scripts.

- File Location: `/etc/ssh/sshd_config` (The master control blueprint for remote access rules).
- `PermitRootLogin no` — Explicitly bars the high-clearance default administrative root profile from logging in remotely, breaking botnet target assumptions.
- `PasswordAuthentication no` — Disables text-based entry fields entirely, forcing the network adapter to demand secure, multi-bit cryptographic SSH key verification files.

---

## 🎣 5. Adversary Persistence Mechanics (Reverse Shells & Listeners)
How automated scheduled cron-jobs maintain infrastructure access post-disconnection:
- **Reverse Shell (Outbound Call):** The local cron script initiates an outbound network connection targeting the adversary's command node. This pipes the host system terminal shell directly out to the internet, bypassing standard firewall configurations.
- **Rogue Listener (Secret Door):** The automated script commands the local network card to open unmonitored ports (e.g., Port 54321) into a `LISTENING` state, creating a temporary entrance window for external infiltration sweeps.
- **Forensic Triage:** Detected by auditing outbound data metrics inside Splunk or running `netstat -ano` inside the native terminal to look for unauthorized outbound hooks or active listening sockets.
