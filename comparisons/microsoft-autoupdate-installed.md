# Microsoft AutoUpdate Installed

The purpose of this Extension Attribute is to check if Microsoft AutoUpdate is installed.
 
## Extension Attribute:
```
#!/bin/bash

# 0 = Microsoft AutoUpdate is not installed
# 1 = Microsoft AutoUpdate is installed

if [[ -x "/Library/Application Support/Microsoft/MAU2.0/Microsoft AutoUpdate.app" ]]; then
    echo "<result>1</result>"
else
    echo "<result>0</result>"
fi

exit 0
```
## Fleet query:
```SELECT 1 FROM apps WHERE name = "Microsoft AutoUpdate.app";```

Compatible with: ✅ macOS 🚫 Windows 🚫 Linux 🚫 ChromeOS
