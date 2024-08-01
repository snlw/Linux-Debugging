# Description
Alice the spy has hidden a secret number combination, find it using these instructions:

1) Find the number of lines with occurrences of the string Alice (case sensitive) in the *.txt files in the /home/admin directory
2) There's a file where Alice appears exactly once. In that file, in the line after that "Alice" occurrence there's a number.
Write both numbers consecutively

# Process
1. Find the number of occurrences of "Alice" in the txt files using `grep "Alice" A.txt -c`. Total is 411
```
A.txt: 398
B.txt: 0
C.txt: 1
D.txt: 12
```
2. In "C.txt", enter vim mode and search for "Alice". Number after match is 156
    - `vim C.txt`
    - `/Alice`

Another method for #1 is to call grep recursively using `grep -rc Alice .txt`
