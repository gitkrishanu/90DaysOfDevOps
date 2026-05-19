# Day 04 – Linux Practice: Processes and Services

## Process Checks

### 1. Check running processes
```bash
ps aux | head

USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.0  0.1 169000 12000 ?        Ss   08:00   0:01 /sbin/init
root       512  0.0  0.3  54000 25000 ?        Ss   08:01   0:00 systemd-journald
ubuntu    1200  0.1  0.5 120000 45000 ?        Ssl  08:05   0:02 sshd

2. Find process by name
pgrep sshd

Service Checks
3. Check SSH service status
systemctl status ssh

● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/lib/systemd/system/ssh.service)
     Active: active (running)

4. List active services
systemctl list-units --type=service --state=running

cron.service        loaded active running Regular background program processing daemon
ssh.service         loaded active running OpenBSD Secure Shell server
networkd.service    loaded active running Network Configuration


Log Checks
5. View SSH service logs
journalctl -u ssh --since "1 hour ago"

May 19 09:10:01 server sshd[1200]: Server listening on port 22
May 19 09:15:22 server sshd[1350]: Accepted password for ubuntu

6. Monitor system log
tail -n 20 /var/log/syslog

