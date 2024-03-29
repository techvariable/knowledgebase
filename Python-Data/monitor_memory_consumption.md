## Script to Monitor Memory Consumption
The following script helps to keep track of memory consumed by a particular process in a Linux machine whose PID is known:

```
#!/bin/bash

# Store the pid in a variable
pid=$1

# Set the interval to 30 seconds
interval=10

# Create a file to store the results
touch memory_usage.txt

# Continuously run the 'ps' command with the pid and sum the memory usage
while true; do
    mem=$(ps -p $pid -o %mem | awk '{s+=$1} END {print s}')
    echo "Total memory consumed by PID $pid: $mem% at $(date)" >> memory_usage.txt
    sleep $interval
done
```
### Instruction for running the script:
1. Copy the code and save it in a file "memory_monitor.sh"
2. Run the following command:
```
bash ./memory_monitor.sh <pid>
```
The code will create a file "memory_usage.txt" and store the percentage of RAM consumed by the process after every 10 seconds
