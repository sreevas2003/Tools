**What is GDB?**

GDB (GNU Debugger) lets you:

  Pause a running program
  
  Inspect variables & memory
  
  Step through code line by line
  
  Find crashes (segfaults 💥)
  
  Debug embedded + Linux apps like a pro

**firstly check**

```
gcc --version
gdb --version
```
If gdb not installed:
```
sudo apt install gdb
```
```
gcc -g hello.c -o hello
```
Run Program Inside GDB
```
run or r
GDB stopped exactly where the error happened 
```

Find the Exact Line (MOST IMPORTANT)
```
bt or backtrace
```
See the Source Code
```
list or l
```
Inspect Variables
```
print var_name
```
Exit GDB
```
quit or q
```

