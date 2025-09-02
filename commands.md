```bash
# grep command use
grep "Hello" file.txt
grep -i "Hello" file.txt  # ignores the case
grep -r "Hello" /path/to/project/ # recursive search in files and folders and sub files and folders
```

```bash

# Sort command: to sort lines of text files
sort file.txt  # arranges lines in ascending alphabetical order
sort -r file.txt # sort in a reverse order
sort -n file.txt # sort in numerically 
sort -k2 -n file.txt # -k2 sorts by second column, -n ensures numeric sorting only
sort -u file.txt # -u removes duplicates lines while sorting
```

```bash
# Tail command
tail file.txt # display the last part of lines (bydefault last 10 lines)
tail -n 5 file.txt  # display last 5 lines

nohup kubectl logs pod_name -n pod_namespace &  # By default nohup writes all output to 'nohup.out' in the current directory but It collects only current logs and exists
nohup kubectl logs -f pod_name -n pod_namespace &  # By default nohup writes all output to 'nohup.out' in the current directory and It collects logs continuously and logs keep updating in 'nohup.out' as new entries appear. Safe to logout, process keeps running in the background.

nohup tail -f path_to_logfile &
tail -f nohup.out  # -f continuously displays and any new lines added to the file , & means run in the background
tail -n 100 -f nohup.out

# command to collect logs
nohup tail -f path_to_logfile & > /../.../collected_logs.txt 2>&1 &
tail -f /../.../collected_logs.txt
```
```bash
# Head command

head file.txt # display the first part of lines (bydefault last 10 lines)
head -n 5 file.txt # display first 5 lines
```

