# DNS Servers

This attribute lists all DNS servers set on the active network connection.
 
## Extension Attribute:
```
#!/bin/bash

# Get macOS version (first 4 characters)
OS=$(/usr/bin/sw_vers -productVersion | /usr/bin/colrm 5)

# Check if OS version is less than 10.5
if [[ "$OS" < "10.5" ]]; then
    # For older macOS versions
    if [ -f /System/Library/CoreServices/RemoteManagement/ARDAgent.app/Contents/Support/networksetup ]; then
        # Find network interface for default route
        NetworkInterface=$(
            /System/Library/CoreServices/RemoteManagement/ARDAgent.app/Contents/Support/networksetup -listnetworkserviceorder 2>&1 | 
            grep $(/usr/sbin/netstat -rn 2>&1 | /usr/bin/grep -m 1 'default' | /usr/bin/awk '{ print $6 }') | 
            sed -e "s/.*Port: //g" -e "s/,.*//g"
        )
        
        # Get DNS servers for the interface
        echo "<result>$(/System/Library/CoreServices/RemoteManagement/ARDAgent.app/Contents/Support/networksetup -getd
```
## Fleet query:
```SELECT * FROM dns_resolvers```

Compatible with: ✅ macOS 🚫 Windows 🚫 Linux 🚫 ChromeOS