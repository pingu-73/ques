# Question 2:
You are an admin on a server with multiple users. You find an unknown process running. You don’t want to kill it yet. How do you determine what exactly the process is doing and whether it is malicious?

## Answer:
- to gather the info about the process we can use `lsof` to open network connections and files associated with that process. to get idea of what resources the process is accessing and using `strace` we could trace system calls  made by that process.
- using `ps -efww` adn filtering out the process with required pid we could a better idea of process.
- We can then inspect the script that the process is running. comparing it with known malware hashes. 
- Monitor processes filesystem activities using `auditd`, network activity and connections using `lsof`. Analyze process's memory using `gcore` or `memmap`.
</br>
Hence, make decision wheather the process is malicious or not.