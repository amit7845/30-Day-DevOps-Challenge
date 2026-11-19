# Day 3 – Linux Process Management and Production Troubleshooting

## Objective
Practise Linux process monitoring, system resource monitoring, Nginx service management and log investigation.

## 1. Process Management

Commands practised:
- `ps -ef` – display running processes.
- `pgrep -a` – find processes by name.
- `top` – monitor CPU and memory usage.
- `kill -15 PID` – request graceful process termination.
- `nice` – check process scheduling priority.

## 2. System Monitoring

Commands practised:
- `free -h` – check RAM and swap usage.
- `df -h` – check filesystem disk usage.
- `du -sh ~` – check directory storage usage.
- `uptime` – check system uptime and load average.

## 3. Nginx Service Management

Installed and started Nginx.

Commands practised:
- `systemctl status nginx` – check service status.
- `systemctl is-active nginx` – check whether service is active.
- `systemctl reload nginx` – reload configuration.
- `nginx -t` – validate Nginx configuration.
- `journalctl -u nginx` – inspect service logs.

## 4. HTTP Health Check

Command:

```bash
curl -I http://localhost
```

Result: HTTP 200 OK.

## 5. Log Investigation

- `/var/log/nginx/access.log` – records HTTP requests and responses.
- `/var/log/nginx/error.log` – records server errors, warnings and diagnostic events.

## Key Learnings

- Identified running processes using PID and PPID.
- Monitored CPU, RAM and disk usage.
- Practised graceful process termination.
- Managed the Nginx web server using systemctl.
- Validated configuration before reloading.
- Investigated Nginx logs.

## Result

Successfully completed practical Linux process management, system monitoring and Nginx production troubleshooting exercises.
