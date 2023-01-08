# Linux Notes

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


