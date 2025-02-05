# Battery Health

The purpose of this Extension Attribute is to display the health of the battery.
 
## Extension Attribute:
```
#!/bin/bash

# Check battery permanent failure status
battery_status=$(ioreg -r -c "AppleSmartBattery" | grep "PermanentFailureStatus" | awk '{print $3}' | sed s/\"//g)

# Translate numeric status to human-readable result
if [ "$battery_status" == "1" ]; then
    result="Failure"
elif [ "$battery_status" == "0" ]; then
    result="OK"
else
    result="Unknown"
fi

# Output result in XML format
echo "<result>$result</result>"
```
## Fleet query:
```SELECT * FROM battery;```

Compatible with: ✅ macOS ✅ Windows 🚫 Linux 🚫 ChromeOS