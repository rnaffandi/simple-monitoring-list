# simple-monitoring-list
Monitoring-List
Edit the Script: Modify the script to append device details without user interaction.
Here’s a modified version of the Bash script for automation:

bash
Copy code
#!/bin/bash

# Define the file where monitoring list will be saved
MONITORING_FILE="monitoring_list.txt"

# Predefined devices (Add more as needed)
devices=(
    "00:1A:2B:3C:4D:5E|Office Printer"
    "11:22:33:44:55:66|John's Laptop"
    "AA:BB:CC:DD:EE:FF|Conference Room AP"
)

# Function to append devices to the monitoring list
append_devices() {
    for device in "${devices[@]}"; do
        local mac_address=$(echo "$device" | cut -d'|' -f1)
        local device_name=$(echo "$device" | cut -d'|' -f2)
        local current_time=$(date '+%Y-%m-%d %H:%M:%S')

        # Append the entry to the monitoring file
        echo "$current_time | MAC: $mac_address | Name: $device_name" >> "$MONITORING_FILE"
    done
    echo "Devices logged successfully."
}

# Call the function
append_devices
Set Up the Cron Job: To run this script automatically at regular intervals, schedule it in the crontab.
Steps to Schedule a Cron Job:
Open the cron editor:

bash
Copy code
crontab -e
Add an entry to schedule the script. For example:

bash
Copy code
0 9 * * * /path/to/monitor_devices.sh
This will run the script every day at 9:00 AM.

Save and exit.

Explanation of Cron Syntax:
0 9 * * * – Run at 9:00 AM every day.
/path/to/monitor_devices.sh – Full path to the script.
Verify Cron Job:
To check scheduled cron jobs:

bash
Copy code
crontab -l
Logs:
You can redirect the script’s output to a log file for monitoring:

bash
Copy code
0 9 * * * /path/to/monitor_devices.sh >> /path/to/monitor_log.txt 2>&1
This way, you automate the task of logging predefined devices at specific intervals.
