# Description
There's a file /home/admin/scores.txt with two columns (imagine the first number is a counter and the second one is a test score for example).

Find the average (more precisely; the arithmetic mean: sum of numbers divided by how many numbers are there) of the numbers in the second column (find the average score)

## Process
Use `awk` for processing the score file.
1. COUNT is incremented for each line
2. SUM is increased for each score in position 2 `$2`
3. Once the loop END, output the score in 2 decimal places
4. Pipe it into the solution file
```
awk 
'{COUNT+=1;SUM+=$2}END{printf "%.2f", SUM/COUNT}' /home/admin/scores.txt > /home/admin/solution
```
