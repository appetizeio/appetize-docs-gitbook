# ADB tunnel

The ADB tunnel feature allows you to create an SSH tunnel to a running Android session. Then, the Appetize virtual Android device will appear with `adb devices`, as if it were a device plugged into your computer via USB. You can run apps on this device via Android Studio, or interact with it using standard `adb` protocol. 

One common practice is to use the ADB tunnel to connect to an Android "standalone" device, without any specific app installed. You can do this after logging into your account from [http://appetize.io/standalone](http://appetize.io/standalone). 

