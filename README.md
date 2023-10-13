This projects includes hardware-specific overlay changes, and an app which selects it dynamically

Here are the list of changes:
- Set Telephony:config_enabled_lte to true on all 4G devices, so the user can select 4G network type in the settings
- Enable Night Mode on devices where appropriate
- Enable Navigation Bar on devices not setting qemu.hw.keys (HTC U11+)
- On Essential PH-1,extends Status Bar to cover the camera notch


Build overlays
--------------
Just execute following commands:
Code:
```
chmod u+x build/build.sh
build/build.sh
```

If You get this, Do what it said:
Code:
```
Please install aapt (apt install aapt should do)
```
Or if you get this:
Code:
OpenJDK Server VM warning: You have loaded library /root/overlay/vendor_hardware_overlay/build/signapk/libconscrypt_openjdk_jni.so which might have disabled stack guard. The VM will try to fix the stack guard now.
It's highly recommended that you fix the library with 'execstack -c <libfile>', or link it with '-z noexecstack'.
Exception in thread "main" java.lang.UnsatisfiedLinkError: org.conscrypt.NativeCrypto.get_cipher_names(Ljava/lang/String;)[Ljava/lang/String;
        at org.conscrypt.NativeCrypto.get_cipher_names(Native Method)
        at org.conscrypt.NativeCrypto.<clinit>(NativeCrypto.java:764)
        at org.conscrypt.OpenSSLProvider.<init>(OpenSSLProvider.java:56)
        at org.conscrypt.OpenSSLProvider.<init>(OpenSSLProvider.java:49)
        at com.android.signapk.SignApk.main(SignApk.java:942)
I have no solution, either. Try to build on another computer.

11. Test overlay with tests.sh and yourself
For general checks (symtax, etc.), just execute following command:
Code:
```
chmod u+x [Path of repository]/tests/tests.sh
[Path of repository]/tests/tests.sh
```
You should fix errors what reported for your device, and then restart from step 10.
If it reported errors but not for your device, just ignore it.
When check passed, you can find overlay file on <Path of repository>/build/treble-overlay-<Manufacturer of your device>-<Name of your device>.apk, just copy it into your phone's /system/overlay/, and set permission to rw-r--r-- / 0644.
And then reboot your phone to test your overlay.

13. If it works for your device, don't forget to perform a pull request for phhusson/vendor_hardware_overlay, to support his awesome works.
