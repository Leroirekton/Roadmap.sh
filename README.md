# Server Stats Analyzer

A simple Bash script to analyze and report basic server performance statistics. This script can be run on any Linux server to provide a quick overview of its health and resource utilization.

## Features

- **Total CPU Usage**: Displays the current percentage of CPU being used.
- **Total Memory Usage**: Shows used and free memory, including percentages.
- **Total Disk Usage**: Provides used and free disk space for all mounted filesystems, including percentages.
- **Top Processes by CPU**: Lists the top 5 processes consuming the most CPU.
- **Top Processes by Memory**: Lists the top 5 processes consuming the most memory.

### Stretch Goals (Additional Stats)

- **OS Version**: Displays the operating system name and version.
- **System Uptime**: Shows how long the system has been running.
- **Load Average**: Prints the system's 1, 5, and 15-minute load averages.
- **Logged-in Users**: Lists users currently logged into the system.
- **Recent Failed Login Attempts**: Shows the last 5 failed login attempts from `auth.log`.

## Requirements

- A Linux-based operating system (Ubuntu, CentOS, Debian, etc.).
- A Bash shell environment.
- Standard Linux command-line utilities: `top`, `free`, `df`, `ps`, `uname`, `uptime`, `who`, `grep`, `awk`, `sed`, `bc`, `tail`.

## Installation

1.  Clone the repository or download the script file:
    ```bash
    wget https://raw.githubusercontent.com/your-repo/server-stats.sh
    ```
    *(Replace the URL with the actual link to your script)*

2.  Make the script executable:
    ```bash
    chmod +x server-stats.sh
    ```

## Usage

Run the script from your terminal. You may need to use `sudo` if you want to ensure all commands (like checking some system logs) run without permission errors.

```bash
./server-stats.sh
```

or with `sudo`:

```bash
sudo ./server-stats.sh
```

### Example Output

```
========================================
      Server Performance Report
========================================
OS Version: Ubuntu 22.04.3 LTS
System Uptime: 10 days, 5:32
Load Average: 0.15, 0.20, 0.10
Logged-in Users: user1 pts/0 (2023-10-27 10:00)
----------------------------------------
Total CPU Usage: 12.5%
----------------------------------------
Total Memory Usage:
               total        used        free      shared  buff/cache   available
Mem:           7.8G        2.1G        4.2G        1.0M        1.5G        5.5G
Swap:          2.0G          0B        2.0G
----------------------------------------
Total Disk Usage:
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        50G   15G   33G  32% /
/dev/sdb1       200G  180G   10G  95% /data
----------------------------------------
Top 5 Processes by CPU Usage:
%CPU  COMMAND
15.0  chrome
10.5  node
8.0   systemd
2.5   kworker/0:1
1.0   bash
----------------------------------------
Top 5 Processes by Memory Usage:
%MEM  COMMAND
12.5  chrome
8.0   node
3.5   systemd-journald
1.5   dockerd
1.0   bash
----------------------------------------
Recent Failed Login Attempts:
Oct 27 11:15 sshd[1234]: Failed password for root from 192.168.1.100 port 22 ssh2
Oct 27 10:05 sshd[1122]: Failed password for admin from 10.0.0.5 port 22 ssh2
Oct 26 22:30 sshd[1010]: Failed password for user from 172.16.0.2 port 22 ssh2
========================================
      End of Report
========================================
```

## Script Breakdown

The script is organized into functions for clarity:

- `get_cpu_usage()`: Uses `top` and `awk` to calculate the used CPU percentage.
- `get_memory_usage()`: Uses the `free` command to get a human-readable report on memory.
- `get_disk_usage()`: Uses `df` to show disk space for all filesystems.
- `get_top_cpu_processes()`: Uses `ps` to sort and display the top 5 CPU-intensive processes.
- `get_top_memory_processes()`: Uses `ps` to sort and display the top 5 memory-intensive processes.
- `get_os_info()`: Uses `uname` to get OS details.
- `get_uptime()`: Uses the `uptime` command.
- `get_load_average()`: Extracts the load average from the `uptime` command output.
- `get_logged_in_users()`: Uses the `who` command.
- `get_failed_logins()`: Greps the system's `auth.log` for failed login attempts.

## License

This project is open-source and available under the [MIT License](LICENSE).
