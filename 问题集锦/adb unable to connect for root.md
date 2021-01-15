
ubuntu系统使用adb时报如下错误：

adb: unable to connect for root: insufficient permissions for device: user fuying is not in the plug

解决方案：

/etc/udev/rules.d

sudo gedit 51-android.rules

SUBSYSTEM=="usb", ENV{DEVTYPE}=="usb_device", MODE="0666"
