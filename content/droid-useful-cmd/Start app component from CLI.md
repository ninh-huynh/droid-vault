
Start activity/service from command line

```sh
# Activity
adb shell am start -n package_name/.activity_name

# Service
adb shell am start-service -n package_name/.service_name
```

Other useful options
1. Start with an action

```sh
adb shell am start -a android.intent.action.VIEW -d "https://www.google.com"
```

2. Start with extra data:

```sh
# Activity
adb shell am start -n com.example.app/.MainActivity --es "key" "value"

# Service
adb shell am start-service -n com.example.app/.MyService --es "key" "value"

```
