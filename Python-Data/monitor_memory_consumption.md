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
