# Description
A developer created a testing program that is continuously writing to a log file `/var/log/bad.log` and filling up disk. 
This program is no longer needed. Find it and terminate it.

# Debug Process 
1. Find the user who is using the file (either READ or WRITE). This would return the PID.
`fuser /var/log/bad.log`
2. Verify that the PID corresponds to the execution of the file
`ps aux | grep $PID` --> `... python3 badlog.py`
3. Terminate the process
`kill -9 $PID`

Another way is to use `lsof` to list open files and do a filter on it `grep badlog.py`.
