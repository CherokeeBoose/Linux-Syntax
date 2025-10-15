Linux Syntax
Top 5 Must-Know Commands

1. Getting Help with man

    # man - manual pages system
# Usage: man [options] command_name
# -k: search manual pages for a keyword
# number: specify manual section (1-9)

man command_name     # Display manual page for command
man -k keyword       # Search manuals containing keyword
man man             # Display manual about man itself
# Alternative help commands
command --help      # Show command's built-in help
command -h          # Brief help (if supported)
info command        # GNU info documentation


2. Identity & System Information

  # whoami - print effective user name
# hostname - show or set system hostname
# id - print user and group information
# uname - print system information
# -a: all information
# -n: node/network name
# -r: kernel release
whoami              # Display current username
hostname            # Show system name
hostname -f         # Show fully qualified domain name (FQDN)
id                  # Show user and group IDs
uname -a            # Show all system information
# Expected Output Example:
# $ whoami
# ec2-user
# $ hostname
# ip-172-31-16-210.ec2.internal


3. Directory Navigation

    # pwd - print working directory
# cd - change directory
# ls - list directory contents
# -l: long format
# -a: show all (including hidden)
# -h: human readable sizes
# -R: recursive
pwd                 # Show current directory path
cd /path/to/dir     # Change to specified directory
cd ..               # Move up one directory
cd ~                # Go to home directory
# List directory contents with different options
ls                  # Basic file listing
ls -l               # Long format (permissions, size, date)
ls -la              # Include hidden files
ls -lh              # Show sizes in human readable format
# Expected Output:
# $ ls -l
# total 32
# drwxr-xr-x 2 ec2-user ec2-user 4096 Oct 15 14:23 directory
# -rw-r--r-- 1 ec2-user ec2-user  123 Oct 15 14:22 file.txt



Essential Linux Commands for AWS Cloud Developer's Guide

Part 1: Core Commands and File System

1. Directory Structure Visualization with tree

    # tree - list contents of directories in a tree-like format
# Installation required on most systems:
# Amazon Linux/RHEL: sudo yum install -y tree
# Ubuntu: sudo apt install -y tree
# Options:
# -L n: limit display to n levels deep
# -d: directories only
# -f: full path prefix
# -h: human readable sizes
# --du: report directory sizes
# Basic usage
tree                # Show all files and directories
tree -L 2          # Limit to two levels deep
tree -d            # Show only directories
tree -h --du       # Show sizes of files and directories
# Expected Output:
# .
# ├── app/
# │   ├── config/
# │   │   └── settings.json
# │   └── logs/
# └── data/
#     └── backup/


2. File Operations

    # touch - create empty file or update timestamp
# mkdir - make directories
# cp - copy files and directories
# mv - move (rename) files
# rm - remove files or directories
# Create files and directories
touch file.txt      # Create empty file or update timestamp
mkdir directory     # Create single directory
mkdir -p a/b/c      # Create parent directories as needed (-p)
# Copy operations
# -r: recursive (for directories)
# -p: preserve attributes
# -v: verbose output
cp file1.txt file2.txt         # Copy single file
cp -r source_dir/ dest_dt_dir/    # Copy directory and contents
# Move/Rename operations
mv old.txt new.txt             # Rename file
mv file.txt /path/to/dir/      # Move file to directory
# Remove operations
# -r: recursive
# -f: force (no confirmation)
# -i: interactive (ask before removal)
rm file.txt                    # Remove single file
rm -r directory/              # Remove directory and contents
rm -rf directory/             # Force remove without confirmation
# Expected Output Examples:
# $ mkdir -p project/src/main
# $ ls -R project/
# project/:
# src
# project/src:
# main


3. File Viewing and Monitoring

    # cat - concatenate and display file contents
# less - view file contents page by page
# head - output first part of files
# tail - output last part of files
# Options:
# -n: number of lines
# -f: follow file growth
# View file contents
cat file.txt        # Display entire file
cat -n file.txt     # Display with line numbers
# Paged viewing
less file.txt       # View with forward/backward scrolling
# less navigation:
# space: next page
# b: previous page
# /pattern: search forward
# q: quit
# Partial file viewing
head -n 5 file.txt  # Show first 5 lines
tail -n 10 file.txt # Show last 10 lines
tail -f log.txt     # Follow file updates in real-time
# Common AWS Usage:
tail -f /var/log/cloud-init-output.log  # Monitor EC2 instance initialization


4. File Search and Filters

# find - search for files in directory hierarchy
# grep - search text patterns in files
# Options for find:
# -name: search by name
# -type: f (files) or d (directories)
# -mtime: modified time
# Find files
find . -name "*.log"          # Find all .log files in current directory
find /path -type f -mtime -7  # Find files modified in last 7 days
# Text search
# grep options:
# -i: ignore case
# -r: recursive
# -l: list matching files
# -n: show line numbers
# -v: invert match
grep "error" file.txt         # Search for "error" in file
grep -i "WARNING" *.log       # Case-insensitive search in all .log files
grep -r "TODO" .              # Search recursively in current directory
# Common AWS Examples:
grep -i "error" /var/log/cloud-init.log  # Search EC2 initialization errors
find /var/log -name "*.log" -mtime -1    # Find today's log files
# Expected Output:
# $ grep -n "error" app.log
# 15:ERROR: Connection failed
# 23:error: timeout occurred

Part 3: Network Operations in AWS

1. Network Configuration and Status

    # ip - show/manipulate network configuration
# Options:
# addr: show addresses
# link: show network devices
# route: show routing table
# Show network interfaces
ip addr show
# Expected Output:
# 1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536
#     inet 127.0.0.1/8 scope host lo
# 2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 9001
#     inet *********/20 brd *********.255 scope global eth0
# Show routing
ip route show
# Expected Output:
# default via *********  dev eth0
# *********/20 dev eth0 proto kernel scope link src *********


2. Network Testing and Connectivity

    # ping - test network connectivity
# -c: count of packets
# -w: timeout in seconds
# Test connectivity
ping -c 4 *********      # Test internal endpoint
ping -c 4 public_ip      # Test external endpoint
# Expected Output:
# PING ********* (*********) 56(84) bytes of data.
# 64 bytes from **********: icmp_seq=1 ttl=64 time=0.080 ms
# 64 bytes from **********: icmp_seq=2 ttl=64 time=0.074 ms
# Trace route to destination
traceroute *********
# Expected Output:
# traceroute to ********* (*********), 30 hops max
#  1  ********* (*********) 0.501 ms 0.495 ms 0.487 ms
#  2  ********* (*********) 0.884 ms 0.880 ms 0.870 ms


3. Network Service Status

    # netstat/ss - show network connections
# Options:
# -t: TCP connections
# -u: UDP connections
# -l: listening sockets
# -n: show numbers instead of names
# -p: show process using socket
# Show listening ports
netstat -tulpn
# Expected Output:
# Proto Recv-Q Send-Q Local Address           Foreign Address         State
# tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN
# tcp        0      0 0.0.0.0:80              0.0.0.0:*               LISLISTEN
# Show established connections
ss -tan state established
# Expected Output:
# State      Recv-Q Send-Q    Local Address:Port     Peer Address:Port
# ESTAB      0      0         *********:22           *********:54321


4. AWS-Specific Network Commands

    # Test EC2 instance metadata service
curl http://169.254.169.254/latest/meta-data/local-ipv4
# Expected Output:
# *********
# Check VPC connectivity
ping -c 2 *********     # Ping another instance in VPC
# Test load balancer health check
curl -I http://localhost/health
# Expected Output:
# HTTP/1.1 200 OK
# Content-Type: text/plain
# Date: Wed, 15 Oct 2025 14:23:45 GMT


5. Network Troubleshooting

    # Check DNS resolution
nslookup internal-service.*********
# Expected Output:
# Server:    *********.2
# Address:   *********.2#53
# Name:      internal-service.*********
# Address:   *********
# Test web server access
curl -v http://*********
# Check network interface status
ethtool eth0
# Expected Output:
# Settings for eth0:
#         Supported ports: [ TP ]
#         Speed: 10000Mb/s
#         Duplex: Full


6. Security Groups and Network Access

    # Test specific port accessibility
nc -zv ********* 80
# Expected Output:
# Connection to ********* port 80 succeeded!
# Scan for open ports (if allowed)
nmap -p 22,80,443 *********
# Expected Output:
# PORT    STATE    SERVICE
# 22/tcp  open     ssh
# 80/tcp  open     http
# 443/tcp filtered https


Part 4: Basic AWS Network Operations

1. Checking Your Instance's Network Information

    # Display instance IP address
# Shows private IP address of EC2 instance
hostname -i
# Expected Output:
*********
# Show all network interfaces
ip addr show
# Expected Output:
1: lo: <LOOPBACK,UP,LOWER_UP>
    inet 127.0.0.1/8
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP>
    inet *********/20

    

2. Basic Connectivity Tests

    # Test internal network connectivity
# Useful for testing connections between EC2 instances
ping -c 3 *********
# Expected Output:
PING ********* (*********) 56(84) bytes of data.
64 bytes from *********: icmp_seq=1 ttl=64 time=0.5 ms
64 bytes from *********: icmp_seq=2 ttl=64 time=0.5 ms
64 bytes from *********: icmp_seq=3 ttl=64 time=0.5 ms
# Check if a port is accessible
# Common ports: 22 (SSH), 80 (HTTP), 443 (HTTPS)
nc -zv ********* 80
# Expected Output:
Connection to ********* port 80 succeeded!

    

3. Viewinwing Network Connections

    # Show listening ports
# Useful for verifying your application is listening
netstat -tulpn | grep LISTEN
# Expected Output:
tcp   0   0   0.0.0.0:80    0.0.0.0:*    LISTEN   1234/httpd
tcp   0   0   0.0.0.0:22       0.0.0.0:*    LISTEN   5678/sshd

    

4. Web Server Testing

    # Test local web server
# Useful for checking if your application is responding
curl -I http://localhost
# Expected Output:
HTTP/1.1 200 OK
Server: nginx/1.20.0
Date: Wed, 15 Oct 2025 14:23:45 GMT

    

5. DNS Resolution

    # Test DNS resolution
# Useful for troubleshooting service connectivity
nslookup example.com
# Expected Output:
Server: *********.2
Address: *********.2#53
Non-authoritative answer:
Name: example.com
Address: *********



6. Checking Instance Network Configuration

    # Display IP address of your EC2 instance
hostname -i
# What this does:
# - Shows the private IP address assigned to your EC2 instance
# - Useful for confirming your instance's identity in the VPC
# - Important for debugging connectivity issues
# Expected Output:
*********  # Your instance's private IP
# Show all network interfaces in detail
ip addr show
# What this does:
# - Lists all network interfaces (NICs) on your instance
# - Shows both IPv4 and IPv6 addresses if configured
# - Displays network interface status (UP/DOWN)
# - Shows network mask and broadcast address
# Expected Output:
1: lo: <LOOPBACK,UP,LOWER_UP>  # Loopback interface
    inet 127.0.0.1/8           # Local loopback address
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP>  # Main network interface
    inet *********/20          # Your instance's IP with subnet mask


7. Network Connectivity Testing

    # Test network connectivity to another instance
ping -c 3 *********
# Detailed explanation:
# ping: Sends ICMP echo requests to verify network connectivity
# -c 3: Sends exactly 3 packets (good practice instead of infinite pings)
# Common uses:
# - Verify network connectivity between instances
# - Check if security groups allow ICMP traffic
# - Measure basic network latency
# - Troubleshoot VPC networking issues
# Expected Output:
PING ********* (*********) 56(84) bytes of data.
64 bytes from *********: icmp_seq=1 ttl=64 time=0.5 ms
64 bytes from *********: icmp_seq=2 ttl=64 time=0.5 ms
64 bytes from *********: icmp_seq=3 ttl=64 time=0.5 ms
# Understanding the output:
# - 56(84) bytes: 56 bytes of data + 28 bytes of ICMP header
# - icmp_seq: Sequence number of the packet
# - ttl: Time To Live value (number of network hops allowed)
# - time: Round-trip time in milliseconds


8. Port Connectivity Testing

    # Check if specific port is accessible
nc -zv ********* 80
# Detailed explanation:
# nc (netcat): Swiss army knife for TCP/IP connections
# -z: Zero-I/O mode (just scan for listening daemons)
# -v: Verbose output
# Common ports to test:
# - 22: SSH
# - 80: HTTP
# - 443: HTTPS
# - 3306: MySQL
# - 5432: PostgreSQL
# Expected Output:
Connection to ********* port 80 succeeded!
# Common issues and what they mean:
# - Connection refused: Port is not open or service not running
# - Connection timed out: Security group/NACL blocking or no route
# - No route to host: Network configuration/routing issue


9. Active Network Connections

    # View all listening ports and established connections
netstat -tulpn | grep LISTEN
# Detailed explanation of options:
# -t: Show TCP connections
# -u: Show UDP connections
# -l: Show only listening sockets
# -p: Show process name/PID
# -n: Don't resolve names (faster, shows numeric values)
# Common use cases:
# - Verify application is listening on expected port
# - Debug port conflicts
# - Audit active network services
# - Troubleshoot connection issues
# Expected Output:
Proto Recv-Q Send-Q Local Address     Foreign Address   State    PID/Program name
tcp        0      0 0.0.0.0:80       0.0.0.0:*        LISTEN   1234/httpd
tcp        0      0 0.0.0.0:22       0.0.0.0:*        LISTEN   5678/sshd
# Understanding the output:
# - Proto: Protocol (tcp/udp)
# - Recv-Q/Send-Q: Data queued for receive/send
# - Local Address: Local IP:port
# - Foreign Address: Remote IP:port
# - State: Connection state (LISTEN/ESTABLISHED/etc.)
# - PID/Program: Process ID and name using this port


Part 5: System Monitoring and Logging in AWS

1. System Resource Monitoring

    # View system load and uptime
uptime
# Detailed explanation:
# Shows:
# - Current time
# - System uptime
# - Number of logged-in users
# - Load averages for 1, 5, and 15 minutes
# Load average > number of CPU cores indicates potential performance issues
# Expected Output:
14:23:45 up 7 days, 2:34, 2 users, load average: 0.08, 0.12, 0.15

    

2. Memory Usage

    # Display memory utilization
free -h
# Detailed explanation:
# -h: Human-readable format (GB/MB instead of bytes)
# Important metrics:
# - total: Total installed memory
# - used: Currently used memory
# - free: Completely unused memory
# - available: Memory available for new applications
# - buff/cache: Memory used by system buffers (can be reclaimed if needed)
# Expected Output:
              total        used        free      shared  buff/cache   available
Mem:          15Gi       2.3Gi        10Gi       1.0Gi       3.2Gi        11Gi
Swap:          0B          0B          0B

    

3. Disk Usage Monitoring

    # Check disk space usage
df -h
# Detailed explanation:
# df: Disk Free command
# -h: Human-readable sizes
# Critical thresholds:
# - >85% full requires attention
# - >95% full is critical
# Common AWS mount points:
# - /: Root volume
# - /dev/xvda1: Primary EBS volume
# - /dev/nvme0n1: Nitro-based instance volumes
# Expected Output:
Filesystem      Size  Used  Avail  Use%  Mounted on
/dev/xvda1      8.0G  4.2G   3.8G   53%  /
tmpfs           7.5G     0   7.5G    0%  /dev/shm

    

4. Real-time Process Monitoring

    # Monitor processes in real time
top
# Detailed explanation:
# Key information displayed:
# - System load averages
# - Tasks and their states
# - CPU usage per process
# - Memory usage per process
# 
# Interactive commands:
# k - kill process
# r - renice process
# M - sort by memory usage
# P - sort by CPU usage
# q - quit
# Expected Output:
top - 14:23:45 up 7 days, 2 users, load average: 0.15, 0.12, 0.08
Tasks: 180 total,   1 running, 179 sleeping,   0 stopped,   0 zombie
%Cpu(s):  2.3 us,  1.2 sy,  0.0 ni, 96.3 id,  0.2 wa,  0.0 hi
MiB Mem :  15890.7 total,  10235.8 free,   2340.5 used,   3314.4 buff/cache

    

5. System Logs Monitoring

    # View system messages
tail -f /var/log/messages
# Detailed explanation:
# tail -f: Follow log file in real-time
# Important log files in AWS:
# - /var/log/messages: General system messages
# - /var/log/cloud-init-output.log: EC2 initialization logs
# - /var/log/secure: Security and authentication logs
# Common log patterns to watch for:
# - ERROR: System errors
# - WARNING: Potential issues
# - Failed password: Security concerns
# Expected Output:
Oct 15 14:23:45 ip-********* systemd: Started Apache web server.
Oct 15 14:23:46 ip-********* sshd[1234]: Accepted publickey for ec2-user

    

Part 5: System Monitoring and Logging in AWS (Continued)

6. Application Monitoring

    # Monitor web server status and access
sudo systemctl status httpdtail -f /var/log/httpd/access_log
# Detailed explanation:
# systemctl status shows:
# - Service state (active/inactive)
# - Last log entries
# - Process ID and resource usage
# - Service dependencies
#
# access_log shows:
# - Client IP addresses
# - Request timestamps
# - HTTP methods and URLs
# - Response codes
# - Response sizes
# Expected Output:
● httpd.service - The Apache HTTP Server
   Loaded: loaded (/usr/lib/systemd/system/httpd.service; enabled; vendor preset: disabled)
   Active: active (running) since Wed 2025-10-15 14:23:45 UTC; 2h ago
   Main PID: 1234 (httpd)
   Status: "Total requests: 1234; Current requests/sec: 5; Current traffic: 2MB/sec"
# Access Log Example:
********* - - [15/Oct/2025:14:23:45 +0000] "GET /index.html HTTP/1.1" 200 2326

    

7. CloudWatch Integration

    # Check CloudWatch agent status
sudo systemctl status amazon-cloudwatch-agent
# View CloudWatch agent configuration
cat /opt/aws/amazon-cloudwatch-agent/etc/amazon-cloudwatch-agent.json
# Detailed explanation:
# CloudWatch agent collects:
# - System metrics (CPU, memory, disk)
# - Custom metrics
# - Log files
# Common configurations:
# - Memory utilization
# - Disk space usage
# - Custom application logs
# - System logs
# Expected Output:
● amazon-cloudwatch-agent.service - Amazon CloudWatch Agent
   Loaded: loaded (/etc/systemd/system/amazon-cloudwatch-agent.service; enabled)
   Activeive: active (running) since Wed 2025-10-15 14:23:45 UTC; 2h ago

    

8. Resource Usage Analysis

    # Check process resource usage
ps aux --sort=-%mem | head -n 5
# Detailed explanation:
# ps aux shows:
# - All processes (a)
# - In user-oriented format (u)
# - Processes without controlling terminals (x)
# --sort=-%mem: Sort by memory usage (descending)
# Common sorting options:
# -%cpu: CPU usage
# -%mem: Memory usage
# -pid: Process ID
# Expected Output:
USER       PID  %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
mysql     1234   2.5  8.4 827232 321844 ?       Ssl  Oct14   5:23 mysqld
httpd     5678   1.2  4.2 423012 162544 ?       Ss   Oct14   2:14 httpd
java      9012   3.1  3.8 912344 145232 ?       Sl   Oct14   8:45 java
nodejs    3456   0.8  2.1 324568  81232 ?       Sl   Oct14   1:12 node

    

9. Custom Monitoring

    # Create a simple monitoring script
cat << 'EOF' > monitor.sh#!/bin/bash
# Monitor key system metrics
echo "=== System Status Report ==="
date
echo "---Memory Usage---"
free -hecho "---Disk Usage---"
df -hecho "---Load Average---"
uptime
echo "---Top 5 CPU Processes---"
ps aux --sort=-%cpu | head -n 6
EOF
chmod +x monitor.sh
# Detailed explanation:
# Script provides:
# - Timestamp for each check
# - Memory status
# - Disk usage
# - System load
# - Top CPU-consuming processes
# 
# Usage:
# ./monitor.sh
# Or schedule with cron:
# */5 * * * * /path/to/monitor.sh >> /var/log/system_monitor.log


10. Log Analysis Techniques

    # Search for errors in logs
grep -i error /var/log/messages
# Count HTTP response codes
awk '{print $9}' /var/log/httpd/access_log | sort | uniq -c
# Detailed explanation:
# Common log analysis patterns:
# - Error tracking
# - Response code distribution
# - Traffic patterns
# - Security incidents
#
# Useful commands:
# grep: Search for patterns
# awk: Process log fields
# sort/uniq: Aggregate data
# sed: Transform log format
# Expected Output:
# HTTP Response Codes:
  12345 200    # Successful requests
    234 304    # Not modified
     45 404    # Not found
      2 500    # Server errors

Part 6: Package Management and Software Installation in AWS

1. Package Manager Basics (YUM/DNF)

    # Update package list and show available updates
sudo yum check-update
# Detailed explanation:
# - Contacts configured repositories
# - Downloads latest package lists
# - Compares with installed versions
# - Shows packages that can be updated
# Common repositories:
# - Amazon Linux base repository
# - EPEL (Extra Packages for Enterprise Linux)
# - Custom repositories (if configured)
# Expected Output:
LastCheck: Thu Oct 15 14:23:45 2025
PackageName      Version         Repository     Size
httpd            2.4.54-1        amzn2         2.3 M
mysql           8.0.31-1        amzn2         25 M

    

2. Installing and Updating Software

    # Install a package
sudo yum install httpd -y
# Detailed explanation:
# sudo: Elevated privileges required for package management
# yum: Package manager
# install: Command to install new packages
# -y: Automatically answer yes to prompts
# Common flags:
# --nogpgcheck: Skip signature verification (not recommended)
# --enablerepo: Enable specific repository
# --security: Only security updates
# Expected Output:
Dependencies resolved.
================================================================================
 Package        Arch   Version         Repository                           Size
================================================================================
Installing:
 httpd          x86_64 2.4.54-1       amzn2-core                          1.3 M
Installing dependencies:
 httpd-tools    x86_64 2.4.54-1       amzn2-core                          0.2 M

    

3. System Updates

    # Update all installed packages
sudo yum update -y
# Detailed explanation:
# yum update:
# - Checks for updates
# - Resolves dependencies
# - Downloads new packages
# - Installs updates
# Best practices:
# - Schedule updates during maintenance windows
# - Test updates in non-production first
# - Keep snapshots/AMIs before major updates
# Expected Output:
Updating:
 kernel                 x86_64    4.14.301-224.520      amzn2    22 M
 system-libs           x86_64    2.28-164.amzn2        amzn2    8.4 M
Transaction Summary
================================================================================
Install     2 Packages
Upgrade    15 Packages

    

4. Repository Management

    # List configured repositories
yum repolist
# Add a new repository
sudo yum-config-manager --add-repo repository_url
# Detailed explanation:
# Repository types:
# - Base repositories (Amazon Linux)
# - EPEL (Extra Packages)
# - Custom/Third-party repos
# Important considerations:
# - Repository priority
# - Security/trust
# - Package compatibility
# Expected Output:
repo id             repo name                            status
amzn2-core         Amazon Linux 2 core repository       enabled
amzn2extra-docker  Amazon Extras repo for docker        enabled
epel               Extra Packages for Enterprise Linux   enabled

    

5. Package Information and Verification

    # Get information about a package
yum info httpd
# Check installed packages
yum list installed | grep httpd
# Detailed explanation:
# Package information shows:
# - Version details
# - Dependencies
# - Installation size
# - Package description
# - Repository source
# Expected Output:
Name        : httpd
Version     : 2.4.54
Release     : 1.amzn2
Size        : 1.3 M
Repo        : amzn2-core
Summary     : Apache HTTP Server
URL         : http://httpd.apache.org/
License     : Apache License, Version 2.0
Description : The Apache HTTP Server is a powerful, efficient,
             and extensible web server.



1. Understanding File Permissions
Files and folders in Linux have permissions that control who can read, write, or execute them. This is important for keeping your data safe.
Let's look at a file:

    ls -l myfile.txt

    

You might see something like this:

    -rw-r--r-- 1 ec2-user ec2-user 123 Oct 15 14:23 myfile.txt

    

Let's break this down:

* The first - means it's a regular file (d would mean directory)
* rw- : The owner (you) can read and write
* r-- : Your group can only read
* r-- : Everyone else can only read

This is important because:

* It keeps your files safe from accidental changes
* It prevents unauthorized access to sensitive information

2. Changing File Permissions

You can change these permissions with the chmod command. Here's a simple example:

    chmod 644 myfile.txt

    

This sets the permissions to:

* 6 (rw-) for the owner
* 4 (r--) for the group
* 4 (r--) for others

Why is this useful?

* For scripts, you might need to make them executable: chmod 755 myscript.sh
* For sensitive files, you might want only you to read them: chmod 600 mysecrets.txt

Always think: "Who needs to do what with this file?"

3. Understanding Users and Groups

In the cloud, multiple people might need access to your server. Linux uses users and groups to manage this.
To see what user you are:

    whoami


To see what groups you're in:

    groups


Why is this important?

* Different users can have different permissions
* You can group users (like 'developers' or 'admins') to manage permissions easily

4. Password Security

If you're using passwords (though AWS often uses keys), here are some tips:

1. Use strong passwords
2. Don't share passwords
3. Change passwords regularly

To change your password:

    passwd

    

Remember: In AWS, you often use key pairs instead of passwords for EC2 instances.

5. Basic SSH Security

SSH is how you connect to your cloud server. Here are some basic safety tips:

1. Keep your private key file (like mykey.pem) secret and safe
2. Never share your private key
3. Set the correct permissions on your key file:

    chmod 400 mykey.pem

    

This makes the key readable only by you, which is required for SSH to work properly.

6. Updating Your System

Keeping your system updated is crucial for security. On Amazon Linux, you can update like this:

    sudo yum update -y

    

This:

* Checks for any security updates
* Installs them automatically
* Helps protect against known vulnerabilities

Run this regularly to keep your system safe!

7. Checking Running Services

It's good to know what's running on your server:

    sudo systemctl list-units --type=service --state=running

    

This shows all running services. Why is this important?

* You can identify any services you don't need and stop them

Fewer running services mean fewer potential security risks

