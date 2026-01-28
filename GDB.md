**What is GDB?**

GDB (GNU Debugger) lets you:

  Pause a running program
  
  Inspect variables & memory
  
  Step through code line by line
  
  Find crashes (segfaults 💥)
  
  Debug embedded + Linux apps like a pro

------

  <img width="1692" height="1200" alt="image" src="https://github.com/user-attachments/assets/66b3b9f0-bc3c-4f25-a2ac-4adc1b45ad3b" />

---------------------


<img width="1024" height="1536" alt="image" src="https://github.com/user-attachments/assets/a630cbca-138e-4766-a02c-e04a2e938cf5" />

---------------------

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

