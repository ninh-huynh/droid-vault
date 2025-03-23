
Using ndk-stack

```sh

ndk-stack -sym <path_to_symbols> -dump <logcat_output.txt>
# or
adb logcat | ndk-stack -sym <path_to_symbols>

```

Using addr2line

```sh
arm-linux-androideabi-addr2line -C -f -e libnative-lib.so 0x1a234
```

