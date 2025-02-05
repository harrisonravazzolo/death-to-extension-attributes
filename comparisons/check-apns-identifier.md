# Check APNs Certificate Identifier

The purpose of this Extension Attribute is to check the identifier of your Apple Push Notification Service certificate.
 
## Extension Attribute:
```
#!/bin/bash

APNS_certificate=`/usr/sbin/system_profiler SPConfigurationProfileDataType | awk '/com.apple.mgmt/{ print $NF }' | sed 's/[";]//g'`

if [[ "$APNS_certificate" = "" ]]; then
      result="NA"
else
      result="$APNS_certificate"
fi

/bin/echo "<result>$result</result>"
```
## Fleet query:
```SELECT topic FROM mdm```

Compatible with: ✅ macOS 🚫 Windows 🚫 Linux 🚫 ChromeOS
