
## Package and System Updates

### Why It's Important

Regular updates patch security vulnerabilities, fix bugs, and ensure system stability. In production environments, uncontrolled updates can cause downtime, so they must be managed carefully.

```
# Debian/Ubuntu systems
sudo apt update                 # Refresh package list
sudo apt upgrade               # Upgrade all packages
sudo apt dist-upgrade          # Upgrade with dependency handling
sudo apt autoremove            # Remove unused packages

# RHEL/CentOS systems
sudo yum check-update          # Check for updates
sudo yum update                # Apply updates
sudo yum autoremove            # Remove unused packages

# For critical security updates only (Debian/Ubuntu)
sudo unattended-upgrade --dry-run  # Test security updates
```
### Best Practices / Gotchas

- **Test updates in staging first** - Never apply updates directly to production
    
- **Use maintenance windows** - Schedule updates during low-traffic periods
    
- **Keep kernel versions consistent** across similar servers for compatibility
    
- **Always have a rollback plan** - snapshot VMs or use LVM snapshots before major updates
    
- **Monitor after updates** - some services may need restarting
----

## User and Group Management

### Why It's Important

Proper user management ensures principle of least privilege, enhances security, and provides accountability through audit trails.

### Common Commands
```
# User management
sudo useradd -m -s /bin/bash username    # Create user with home directory
sudo passwd username                     # Set/change password
sudo usermod -aG groupname username      # Add user to group
sudo userdel -r username                 # Delete user and home directory

# Group management
sudo groupadd groupname                  # Create new group
sudo groupdel groupname                  # Delete group
sudo gpasswd -a username groupname       # Add user to group
sudo gpasswd -d username groupname       # Remove user from group

# Permission management
sudo chown user:file.txt                 # Change ownership
sudo chmod 640 file.txt                  # Set permissions (rw-r-----)
sudo setfacl -m u:username:rwx file.txt  # Set ACLs

# Check user information
id username                             # Show user IDs and groups
last                                    # Show last logins
who                                     # Show logged in users
```
---


### Best Practices / Gotchas

- **Use SSH keys instead of passwords** for system accounts
    
- **Regularly audit user accounts** and remove unused ones
    
- **Implement password policies** with `chage` and `/etc/login.defs`
    
- **Use groups for permission management** rather than individual user permissions
    
- **Avoid using root directly** - use sudo with limited privileges

---
## Service Management with systemd

### Why It's Important

systemd is the init system for most modern Linux distributions. Proper service management ensures critical services are always running and configured correctly.

### Common Commands
```
# Basic service management
sudo systemctl start servicename        # Start service
sudo systemctl stop servicename         # Stop service
sudo systemctl restart servicename      # Restart service
sudo systemctl reload servicename       # Reload config without full restart
sudo systemctl status servicename       # Check service status

# Service configuration
sudo systemctl enable servicename       # Enable service at boot
sudo systemctl disable servicename      # Disable service at boot
sudo systemctl daemon-reload            # Reload systemd after config changes

# System overview
sudo systemctl list-units --type=service  # List all services
sudo systemctl list-unit-files           # List all unit files
sudo systemctl --failed                  # Show failed services

# Log viewing for services
sudo journalctl -u servicename          # View logs for specific service
sudo journalctl -u servicename -f       # Follow logs in real-time
sudo journalctl --since "2023-01-01" --until "2023-01-02"  # Time-based filtering
```


### Best Practices / Gotchas

- **Create custom systemd services** for applications rather than using init scripts
    
- **Use `Type=forking` correctly** - know when your service daemonizes
    
- **Set proper restart policies** with `Restart=on-failure` and `RestartSec`
    
- **Implement resource limits** with `MemoryLimit`, `CPUShares` in service files
    
- **Use `journalctl` effectively** with filters like `-p` for priority, `-S` for since
---
## Networking and Firewall Configuration

### Why It's Important

Proper network configuration ensures reliable connectivity, security through controlled access, and optimal performance.

### Common Commands
```
# Network configuration
ip addr show                           # Show IP addresses
ip route show                         # Show routing table
ss -tulpn                             # Show listening ports
ping example.com                      # Test connectivity
traceroute example.com                # Trace network path

# DNS troubleshooting
dig example.com                       # DNS lookup
nslookup example.com                  # Alternative DNS lookup
cat /etc/resolv.conf                  # Check DNS resolver config

# Firewall management (UFW - simpler)
sudo ufw status                       # Show firewall status
sudo ufw allow 22/tcp                 # Allow SSH
sudo ufw enable                       # Enable firewall

# Firewall management (iptables/nftables - advanced)
sudo iptables -L -n -v                # List iptables rules
sudo nft list ruleset                 # List nftables rules

# Network testing
curl -I http://example.com            # Test HTTP connectivity
nc -zv hostname port                  # Test port connectivity
mtr hostname                          # Network diagnostic tool
```

### Best Practices / Gotchas

- **Use firewall whitelisting** rather than blacklisting approach
    
- **Document all firewall changes** - they can be difficult to reverse engineer
    
- **Test network changes in non-production first** - a mistake can cause complete loss of access
    
- **Use persistent firewall rules** - iptables rules don't survive reboot without saving
    
- **Monitor network traffic** with tools like iftop, nethogs

---
## Storage and Filesystem Management

### Why It's Important

Proper storage management prevents data loss, ensures performance, and helps avoid service interruptions due to full filesystems.

### Common Commands

```
# Disk usage analysis
df -h                                  # Show disk space usage
du -sh /path/to/directory             # Show directory size
ncdu /path/to/directory               # Interactive disk usage analysis

# Filesystem management
lsblk                                  # List block devices
sudo fdisk -l                         # Show partition tables
sudo mkfs.ext4 /dev/sdb1              # Create filesystem
sudo mount /dev/sdb1 /mnt             # Mount filesystem
sudo umount /mnt                      # Unmount filesystem

# LVM management
sudo pvdisplay                        # Show physical volumes
sudo vgdisplay                        # Show volume groups
sudo lvdisplay                        # Show logical volumes
sudo lvextend -L +10G /dev/vg0/lv0    # Extend logical volume
sudo resize2fs /dev/vg0/lv0           # Resize filesystem

# SMART monitoring
sudo smartctl -a /dev/sda             # Check disk health
```
### Best Practices / Gotchas

- **Use LVM for flexibility** even with single disks
    
- **Implement monitoring for disk space** - 80% usage should trigger alerts
    
- **Regularly check filesystem integrity** with `fsck` (on unmounted filesystems)
    
- **Use noatime option** in /etc/fstab for better performance on frequently accessed files
    
- **RAID is not backup** - implement proper backup strategies alongside RAID
---
## Process and Resource Monitoring

### Why It's Important

Monitoring processes and resources helps identify performance bottlenecks, prevent system crashes, and optimize resource utilization.

### Common Commands
```
# Process monitoring
ps aux                               # Show all processes
top                                  # Interactive process viewer
htop                                 # Enhanced top (install if needed)
pidof processname                    # Find PID of process

# Resource monitoring
free -h                              # Memory usage
vmstat 1 10                          # Virtual memory statistics
iostat -x 1 10                       # I/O statistics
mpstat -P ALL 1 10                   # CPU statistics

# Process management
kill -9 PID                          # Force kill process
pkill processname                    # Kill by process name
renice -n 10 -p PID                  # Change process priority
nice -n 10 command                   # Start command with specific priority

# Advanced monitoring
lsof -i :80                          # List processes using port 80
lsof -u username                     # List files opened by user
strace -p PID                        # Trace system calls of process
```

### Best Practices / Gotchas

- **Don't overuse kill -9** - it doesn't allow graceful shutdown
    
- **Monitor zombie processes** - they indicate issues with parent processes
    
- **Use `nohup` or `screen`** for long-running processes to prevent termination on logout
    
- **Set process limits** with `/etc/security/limits.conf` to prevent resource exhaustion
    
- **Understand the difference between RAM and swap usage** - high swap usage indicates memory pressure
---
## Logs and Troubleshooting

### Why It's Important

Logs are the primary source of truth for system behavior. Effective log analysis is crucial for troubleshooting and security incident response.

### Common Commands

```
# Basic log viewing
tail -f /var/log/syslog             # Follow system log (Debian/Ubuntu)
tail -f /var/log/messages           # Follow system log (RHEL/CentOS)
less /var/log/auth.log              # View authentication log

# Journalctl (systemd systems)
journalctl -f                       # Follow journal logs
journalctl --since "1 hour ago"     # Show logs from last hour
journalctl -p err..emerg            # Show error and emergency messages
journalctl -u nginx.service         # Show logs for specific service

# Log analysis tools
grep "error" /var/log/syslog        # Search for errors
awk '/pattern/ {print $1}' file.log # Extract specific data
sed -n '5,10p' file.log             # Show lines 5-10

# Log rotation
sudo logrotate -f /etc/logrotate.conf  # Force log rotation
```

### Best Practices / Gotchas

- **Implement centralized logging** for multiple servers using rsyslog or Loki
    
- **Rotate logs regularly** to prevent disk space issues
    
- **Use log levels appropriately** - debug in development, warning/error in production
    
- **Correlate timestamps across systems** - ensure time synchronization with NTP
    
- **Don't ignore repeated warnings** - they often precede failures
---
## Backup and Recovery Strategies

### Why It's Important

Backups are the last line of defense against data loss. A robust backup strategy is non-negotiable for any production system.

### Common Commands
```
# Basic backup commands
tar -czvf backup.tar.gz /path/to/backup  # Create compressed tar archive
rsync -avz --delete source/ dest/        # Synchronize directories
dd if=/dev/sda of=/backup/sda.img bs=4M  # Disk image backup

# Database backups (MySQL example)
mysqldump -u root -p --all-databases > full_backup.sql  # Full MySQL backup
pg_dumpall -U postgres > full_backup.sql               # Full PostgreSQL backup

# Backup verification
tar -tzvf backup.tar.gz                 # List tar contents without extracting
md5sum backup.tar.gz                    # Generate checksum for verification

# Restore procedures
tar -xzvf backup.tar.gz -C /restore/path  # Extract tar archive
rsync -avz backup/ /restore/path         # Restore with rsync
mysql -u root -p < full_backup.sql       # Restore MySQL database
```

### Best Practices / Gotchas

- **Follow the 3-2-1 rule**: 3 copies, 2 different media, 1 offsite
    
- **Test restore procedures regularly** - backups are useless if they can't be restored
    
- **Encrypt sensitive backups** - especially for offsite storage
    
- **Monitor backup jobs** - failed backups should trigger alerts
    
- **Consider application-consistent backups** for databases rather than filesystem-only backups
---
## Cron Jobs and Automation

### Why It's Important

Automation reduces human error, ensures consistency, and frees up time for more valuable tasks.

### Common Commands
```
# Cron management
crontab -e                          # Edit user's cron jobs
crontab -l                          # List cron jobs
crontab -r                          # Remove all cron jobs

# System cron jobs
sudo nano /etc/crontab              # System-wide crontab
sudo ls /etc/cron.d/                # Additional cron directories

# Example cron entries
# m h dom mon dow command
0 2 * * * /path/to/backup.sh        # Daily at 2 AM
*/5 * * * * /path/to/monitor.sh     # Every 5 minutes
0 0 * * 0 /path/to/weekly.sh        # Weekly on Sunday

# Alternative schedulers
systemctl list-timers               # List systemd timers
```

### Best Practices / Gotchas

- **Always use full paths** in cron jobs - cron has a minimal PATH
    
- **Capture output** with `> /path/to/log 2>&1` or redirect to /dev/null if not needed
    
- **Test cron commands manually** first to ensure they work
    
- **Consider using systemd timers** for more complex scheduling needs
    
- **Document the purpose** of each cron job - they often become forgotten "tribal knowledge"
---
## Security Hardening Best Practices

### Why It's Important

Security hardening protects systems from unauthorized access, data breaches, and other security threats.

### Common Commands
```
# SSH security
sudo nano /etc/ssh/sshd_config      # Configure SSH security settings

# Firewall setup
sudo ufw enable                     # Enable Uncomplicated Firewall
sudo ufw default deny incoming      # Deny all incoming by default
sudo ufw allow from 192.168.1.0/24 to any port 22  # Allow SSH from specific network

# Audit logging
sudo auditctl -l                    # List audit rules
sudo ausearch -k key                # Search audit logs by key

# Security scanning
sudo lynis audit system             # System security audit
sudo chkrootkit                     # Check for rootkits
sudo rkhunter --check               # Rootkit hunter

# File integrity checking
sudo aide --check                   # Check file integrity
sudo tripwire --check               # Alternative file integrity check
```

### Best Practices / Gotchas

- **Disable root SSH login** and use sudo instead
    
- **Use key-based authentication** for SSH instead of passwords
    
- **Keep systems updated** with security patches
    
- **Implement fail2ban** to protect against brute force attacks
    
- **Regularly review user accounts** and remove unnecessary ones
    
- **Use AppArmor or SELinux** for mandatory access control
    
- **Encrypt sensitive data** both at rest and in transit
---
## System Health Monitoring

### Why It's Important

Proactive monitoring helps identify issues before they become critical, ensuring system availability and performance.

### Common Commands
```
# System health checks
uptime                              # System uptime and load
dmesg | tail -20                    # Recent kernel messages
sudo smartctl -H /dev/sda           # Disk health status

# Performance monitoring
sar -u 1 3                         # CPU usage sampling
sar -r 1 3                         # Memory usage sampling
sar -b 1 3                         # I/O statistics

# Temperature monitoring
sensors                             # Show hardware temperatures

# Memory checking
free -m                             # Memory usage in MB
vmstat 1 5                          # Virtual memory statistics

# Advanced monitoring tools
# (May require installation)
nmon                                # Interactive system monitoring
glances                             # Comprehensive system monitoring
```
### Best Practices / Gotchas

- **Monitor key metrics**: CPU, memory, disk I/O, network I/O, disk space
    
- **Set appropriate thresholds** for alerts - avoid alert fatigue
    
- **Establish baselines** for normal operation to identify anomalies
    
- **Use dedicated monitoring systems** like Prometheus, Zabbix, or Nagios
    
- **Monitor application-specific metrics** in addition to system metrics
---
## Shutdown and Reboot Procedures

### Why It's Important

Proper shutdown procedures prevent data corruption, ensure graceful service termination, and maintain system integrity.

### Common Commands
```
# Graceful shutdown
sudo shutdown -h now                # Shutdown immediately
sudo shutdown -h +10 "System maintenance"  # Shutdown in 10 minutes with message

# Reboot commands
sudo reboot                         # Reboot immediately
sudo shutdown -r now                # Reboot immediately
sudo shutdown -r +10 "Kernel update"  # Reboot in 10 minutes

# Canceling shutdown
sudo shutdown -c                    # Cancel scheduled shutdown

# Emergency procedures
echo o > /proc/sysrq-trigger        # Shutdown (if system is unresponsive)
echo b > /proc/sysrq-trigger        # Reboot (if system is unresponsive)

# Maintenance mode
sudo systemctl isolate rescue.target  # Boot into rescue mode
sudo systemctl isolate multi-user.target  # Boot into multi-user mode
```
### Best Practices / Gotchas

- **Always warn users** before shutdowns or reboots
    
- **Schedule maintenance windows** during low-usage periods
    
- **Stop critical services gracefully** before shutdown
    
- **Use maintenance mode** to prevent users from connecting during maintenance
    
- **Have a backout plan** if the reboot doesn't go as expected
    
- **Document the reason** for each reboot for change management purposes
---
