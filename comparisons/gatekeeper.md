# Gatekeeper Status

The purpose of this Extension Attribute is to display the current status of Gatekeeper.
 
## Extension Attribute:
```
#!/bin/sh

TESTFILE="/usr/sbin/jamf/"
CMD=$(spctl -v -a "$TESTFILE" 2>&1)

case "$CMD" in
   *rejected*)
       STATUS="Mac App Store"
   ;;    
   *override=security*)
       STATUS="Anywhere"
   ;;
   *)
       STATUS="Mac App Store and identified developers"    
   ;;
esac
echo "<result>$STATUS</result>"

```
## Fleet query:
```SELECT 1 FROM gatekeeper WHERE assessments_enabled = 1;```

Compatible with: ✅ macOS 🚫 Windows 🚫 Linux 🚫 ChromeOS
