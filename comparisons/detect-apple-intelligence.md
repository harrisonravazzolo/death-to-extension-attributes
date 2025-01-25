# Detect Apple Intelligence

This Extension Attribute was written to detect if Apple Intelligence is enabled on a macOS device.

## Extension Attribute
```
#!/usr/bin/env zsh
autoload is-at-least
RESULT="Not Configured"
osVersion=$( sw_vers -productVersion )
if is-at-least 15.1 $osVersion; then
    lastUser=$( defaults read /Library/Preferences/com.apple.loginwindow.plist lastUserName )
    testFile="/Users/${lastUser}/Library/Preferences/com.apple.CloudSubscriptionFeatures.optIn.plist"
    if [[ -f "${testFile}" ]] ; then
        mobileMeAccountID=$( /usr/libexec/PlistBuddy -c "print Accounts:0:AccountDSID" "/Users/$lastUser/Library/Preferences/MobileMeAccounts.plist" 2>/dev/null )
        if [[ "${mobileMeAccountID}" == *"File Doesn't Exist"* ]]; then
            value=$( /usr/bin/defaults read "/Users/$lastUser/Library/Preferences/com.apple.CloudSubscriptionFeatures.optIn.plist" device 2>/dev/null )
            if [[ "${value}" == "1" ]]; then
                RESULT="Enabled (no Apple Account)"
            else
                RESULT="Disabled"
            fi
        else
        
            value=$( /usr/bin/defaults read "/Users/$lastUser/Library/Preferences/com.apple.CloudSubscriptionFeatures.optIn.plist" "$mobileMeAccountID" 2>/dev/null )
            if [[ "${value}" == "1" ]]; then
                RESULT="Apple Account Enabled"
            else
                RESULT="Disabled"
            fi
        fi
    fi
else
    RESULT="Not Applicable; macOS ${osVersion}"
fi
/bin/echo "<result>$RESULT</result>"
```
## Fleet query:
```SELECT 1 FROM plist WHERE path LIKE '/Users/%/Library/Preferences/com.apple.CloudSubscriptionFeatures.optIn.plist' AND value = 1;```

Compatible with: ✅ macOS 🚫 Windows 🚫 Linux 🚫 ChromeOS
