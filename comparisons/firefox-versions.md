# Firefox Versions

This attribute reports on version of Firefox.
 
## Extension Attribute:
```
#!/bin/bash

# Get Firefox version
FFV=$(/Applications/Firefox.app/Contents/MacOS/firefox --version | awk '{ print $3 }')

echo "<result>$FFV</result>"
```
## Fleet query:
```SELECT bundle_short_version FROM apps WHERE name = 'Firefox.app';```

Compatible with: ✅ macOS 🚫 Windows 🚫 Linux 🚫 ChromeOS