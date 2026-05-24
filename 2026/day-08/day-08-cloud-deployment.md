# Day 08 – Cloud Server Setup: Docker, Nginx & Web Deployment

## Objective

Deploy a cloud server, connect via SSH, install Docker and Nginx, configure network access, verify web access from the internet, and collect Nginx logs.

---

# Cloud Instance Details

| Item | Value |
|--------|--------|
| Cloud Provider | AWS EC2 / Utho |
| OS | Ubuntu 24.04 LTS |
| Instance Type | t2.micro |
| Public IP | <YOUR_PUBLIC_IP> |
| SSH User | ubuntu |
| Region | <YOUR_REGION> |

---

# Part 1: Launch Cloud Instance & SSH Access

## Connect via SSH

### Command

```bash
ssh -i my-key.pem ubuntu@<YOUR_PUBLIC_IP>
```

### Verification

```bash
hostname
whoami
```

### Output

```text
ip-172-31-xx-xx
ubuntu
```

### Observation

Successfully connected to the cloud server using SSH.

---

# Part 2: Install Docker & Nginx

## Update System

```bash
sudo apt update
sudo apt upgrade -y
```

### Observation

System packages updated successfully.

---

## Install Docker

```bash
sudo apt install docker.io -y
```

### Verify Docker

```bash
sudo systemctl status docker
docker --version
```

### Output

```text
Docker version 28.x.x
```

### Observation

Docker service is active and running.

---

## Install Nginx

```bash
sudo apt install nginx -y
```

### Verify Nginx

```bash
sudo systemctl status nginx
```

### Output

```text
Active: active (running)
```

### Observation

Nginx installed and started successfully.

---

# Part 3: Security Group Configuration

## AWS Security Group Rules

| Type | Protocol | Port | Source |
|--------|----------|------|--------|
| SSH | TCP | 22 | My IP |
| HTTP | TCP | 80 | 0.0.0.0/0 |

### Verification

Open browser:

```text
http://<YOUR_PUBLIC_IP>
```

### Result

Nginx Welcome Page displayed successfully.

📸 Screenshot Saved:
- nginx-webpage.png

### Observation

Web server is publicly accessible over HTTP.

---

# Part 4: Extract Nginx Logs

## View Access Logs

```bash
sudo tail -20 /var/log/nginx/access.log
```

### Observation

Browser requests are visible in access logs.

---

## Save Logs to File

```bash
sudo cp /var/log/nginx/access.log ~/nginx-logs.txt
```

or

```bash
sudo tail -100 /var/log/nginx/access.log > ~/nginx-logs.txt
```

### Verify

```bash
cat ~/nginx-logs.txt
```

### Observation

Logs successfully exported.

---

## Download Log File

On local machine:

```bash
scp -i my-key.pem ubuntu@<YOUR_PUBLIC_IP>:~/nginx-logs.txt .
```

### Observation

Log file downloaded successfully.

---

# Additional Verification

## Check Listening Ports

```bash
sudo ss -tulpn
```

### Output

```text
LISTEN 0 511 *:80
LISTEN 0 128 *:22
```

### Observation

SSH and HTTP ports are active.

---

## Check Disk Usage

```bash
df -h
```

### Observation

Sufficient disk space available.

---

## Check Running Containers

```bash
docker ps
```

### Output

```text
CONTAINER ID   IMAGE   COMMAND   STATUS
```

### Observation

Docker engine operational.

---

# Screenshots Collected

1. ssh-connection.png
2. nginx-webpage.png
3. docker-nginx.png

---

# Commands Used

```bash
ssh -i my-key.pem ubuntu@<IP>

sudo apt update
sudo apt upgrade -y

sudo apt install docker.io -y
docker --version

sudo apt install nginx -y

sudo systemctl status nginx
sudo systemctl status docker

sudo ss -tulpn

sudo tail -20 /var/log/nginx/access.log

sudo cp /var/log/nginx/access.log ~/nginx-logs.txt

scp -i my-key.pem ubuntu@<IP>:~/nginx-logs.txt .
```

---

# Challenges Faced

### Challenge 1
Unable to access the Nginx webpage initially.

### Resolution
Added inbound HTTP (port 80) rule in AWS Security Group.

---

### Challenge 2
Permission denied while reading log files.

### Resolution
Used sudo to access `/var/log/nginx/access.log`.

---

# What I Learned

- How to launch and manage a cloud VM.
- How SSH authentication works using key pairs.
- How to install and manage services using systemctl.
- How Nginx serves web content on port 80.
- How to view and export application logs.
- Importance of security groups and firewall rules.

---

# Conclusion

Successfully launched a cloud server, connected through SSH, installed Docker and Nginx, configured HTTP access, verified public web access, and collected Nginx logs for troubleshooting and monitoring.
