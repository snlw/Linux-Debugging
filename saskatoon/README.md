# Description
There's a web server access log file at `/home/admin/access.log`. The file consists of one line per HTTP request, with the requester's IP address at the beginning of each line.

Find what's the IP address that has the most requests in this file (there's no tie; the IP is unique). Write the solution into a file `/home/admin/highestip.txt`.

# Command
```bash
awk '{print $1}' /home/admin/access.log |
sort |
uniq -c |
sort -nr |
head -1 |
awk '{print $2}' >
/home/admin/highestip.txt
```
1. Parse the IP string from each line in the logs
2. Sort the strings to ensure duplicate IPs are adjacent
3. Filter number of occurrences of unique IPs. `-c` flag is for `--count`
4. Sort the output to have the largest count and the corresponding IP at the top.
    - `-n` flag is for numeric sort
    - `-r` flag is for reverse order
5. Get the top result
6. Print the corresponding IP in to the designated file.
