# Bash Scripting

## How to write a loop in one line:
```bash
count=0
ls_dir="directory"
for i in $(seq 10 61); do array=($(ls "${ls_dir}/$i")); ((count+="${#array[*]}")); done
```
