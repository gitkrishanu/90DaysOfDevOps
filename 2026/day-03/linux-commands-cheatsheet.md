# Day 03 – Linux Commands Cheat Sheet

## Process Management Commands

| Command | Usage |
|---|---|
| `ps aux` | Display all running processes |
| `top` | Real-time system and process monitoring |
| `htop` | Interactive process viewer |
| `kill PID` | Terminate a process by PID |
| `kill -9 PID` | Force kill a process |
| `pkill process_name` | Kill process by name |
| `pgrep process_name` | Find PID by process name |
| `jobs` | Show background jobs |
| `bg` | Resume a job in background |
| `fg` | Bring background job to foreground |
| `nohup command &` | Run command after logout |
| `systemctl status service` | Check service status |
| `systemctl restart service` | Restart a service |
| `journalctl -u service` | View logs for a service |

---

## File System Commands

| Command | Usage |
|---|---|
| `pwd` | Show current directory |
| `ls -la` | List files with details |
| `cd /path` | Change directory |
| `mkdir dir_name` | Create directory |
| `rm -rf dir_name` | Remove directory recursively |
| `cp source dest` | Copy files/directories |
| `mv source dest` | Move or rename files |
| `touch file.txt` | Create empty file |
| `cat file.txt` | View file contents |
| `less file.txt` | Read file page by page |
| `head file.txt` | Show first 10 lines |
| `tail -f logfile.log` | Monitor log file live |
| `find / -name file.txt` | Search for files |
| `grep "text" file.txt` | Search text in file |
| `df -h` | Check disk space |
| `du -sh folder` | Check folder size |
| `chmod +x script.sh` | Add execute permission |
| `chown user:user file` | Change file ownership |

---

## Networking Troubleshooting Commands

| Command | Usage |
|---|---|
| `ping google.com` | Test network connectivity |
| `ip addr` | Show IP addresses |
| `curl https://example.com` | Test HTTP connectivity |
| `dig google.com` | DNS lookup |
| `nslookup google.com` | Query DNS records |
| `netstat -tulnp` | Show listening ports |
| `ss -tulnp` | Display socket statistics |
| `traceroute google.com` | Trace packet route |
| `hostname -I` | Show system IP |
| `wget URL` | Download files from internet |

---

## Useful Log & Monitoring Commands

| Command | Usage |
|---|---|
| `dmesg` | View kernel logs |
| `free -m` | Check memory usage |
| `uptime` | Show system uptime/load |
| `whoami` | Display current user |
| `history` | Show command history |

---

# Favorite Troubleshooting Commands

- `tail -f /var/log/syslog` → Monitor logs in real time
- `ss -tulnp` → Check open ports and services
- `journalctl -xe` → Investigate system errors quickly
