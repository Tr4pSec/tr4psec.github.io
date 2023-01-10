# Linux Notes

Compromise assessment Cheat Sheet:
https://sandflysecurity.com/linux-compromise-detection-command-cheatsheet.pdf

Checking for active network connections
```
netstat -all
```

List all ports listening:
```
sudo lsof -i -P -n | grep LISTEN
```

Checking running services:
```
ps aux
```

See details of PID:
```
cat /proc/type_PID_here/status
```
```
ps -p $PID -o pid,vsz=MEMORY -o user,group=GROUP -o comm,args=ARGS
```

Parsing logs:
```
find . -name "*.log" | xargs grep -E 'fatal|error|critical|failure|warning|'
```
```
egrep -r "string1|string2" pathname
```
```
journalctl | grep string
```
Parsing .gz logs:
```
zcat *.gz
```

Parsing Audit log:
```
cat audit.log | egrep EXECVE
```

```
sudo aureport -x -if audit.log | cut -d " " -f 4
```

```
sudo aureport -x -if audit.log | cut -d " " -f 4 | sort -u
```
```
sudo aureport  --tty -if audit.log
```
