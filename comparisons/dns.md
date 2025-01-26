# DNS Servers

This attribute lists all DNS servers set on the active network connection.
 
## Extension Attribute:
```
#!/bin/sh
NetworkInterface=`/usr/sbin/networksetup -listnetworkserviceorder 2>&1 | grep $(/usr/sbin/netstat -rn 2>&1 | /usr/bin/grep -m 1 'default' | /usr/bin/awk '{ print $6 }') | sed -e "s/.*Port: //g" -e "s/,.*//g"`
echo "<result>`/usr/sbin/networksetup -getdnsservers "$NetworkInterface" 2>&1`</result>"
```
## Fleet query:
```SELECT * FROM dns_resolvers```

Compatible with: ✅ macOS 🚫 Windows 🚫 Linux 🚫 ChromeOS
