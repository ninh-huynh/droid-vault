# Access emulator from WSL2

## Require

Start adb server in window host

```Powershell
adb -a server nodaemon
```

Start emulator

```Powershell
emulator -list-avds
emulator -avd Pixel_6a_API_34
```
## Don't use AS, using terminal only

Use environment variable `ADB_SERVER_SOCKET` in WSL2 with the Window host IP

Run the following command from WSL2

```bash
# https://learn.microsoft.com/en-us/windows/wsl/networking#accessing-windows-networking-apps-from-linux-host-ip

ip route show | grep -i default | awk '{ print $3}'
```

Saving the result in `.bashrc`

```bash
export ADB_SERVER_SOCKET=tcp:$(ip route show | grep -i default | awk '{ print $3}'):5037
```

## Use AS to debug, logcat
Unfortunately, the above method (using ADB_SERVER_SOCKET) not working with IntelliJ IDE (see [#4692](https://github.com/microsoft/WSL/discussions/4692#discussioncomment-5740928))

The solution is use `socat` to forward Windows 5037 port to Linux 5037 port. Run the below command in a separate process before starting up IntelliJ/Android Studio
```bash
export WSL_HOST_IP="$(ip route show | grep -i default | awk '{ print $3}')"
socat TCP-LISTEN:5037,reuseaddr,fork TCP:$WSL_HOST_IP:5037
```