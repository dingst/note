### 如何添加广播权限限制

发送广播时，除了通过 Action 筛选 Receiver，还可以 **限制只有具有某种权限的应用才能接收**。

1. 自定义接收需要的权限，发送广播时携带该权限参数，以筛选 Receiver 应用

   ```xml
   <!--Manifest.xml-->
   <permission android:name="com.gaoxiang.permission.receive"/>
   12
   ```

   ```java
   //MainActivity.java
   val intent = Intent(ACTION)
   //FLAG_RECEIVER_INCLUDE_BACKGROUND, to send to static receiver
   intent.addFlags(0x01000000)
   //Receiver must have permission
   sendBroadcast(intent, Constants.RECEIVER_PERMISSION)
   123456
   ```

2. Receiver应用装备该权限

   ```xml
   <!--Manifest.xml-->
   <uses-permission android:name="com.gaoxiang.permission.receive"/>
   12
   ```

对于广播接收者而言，除了通过 Action 筛选广播，还可以 **限制只接收具有某种权限的应用发送的广播**。

1. 接收方，自定义发送者应该具备的权限，接收广播时检查该权限，以筛选发送广播的应用

   ```xml
    <!--Manifest.xml-->
    <permission android:name="com.gaoxiang.permission.receive"/>
   		...
   		<receiver
               android:name=".StaticReceiver"
               android:enabled="true"
               android:exported="true"
               android:permission="com.gaoxiang.permission.send">
               <intent-filter>
                   <action android:name="com.gaoxiang.broacast.one"/>
               </intent-filter>
           </receiver>
   123456789101112
   ```

   ```java
   //MainActivity.java
   //Sender must have permission
   registerReceiver(registeredReceiver, IntentFilter(Constants.BROADCAST_ACTION),
               Constants.SENDER_PERMISSION, null)
   1234
   ```

2. 发送广播的应用装备该权限

   ```xml
   <!--Manifest.xml-->
   <uses-permission android:name="com.gaoxiang.permission.send" />
   12
   ```

### 开发者的视角

1. 发送广播时，使用带权限的 sendBroadcast 方法（需要目标 Receiver 应用的开发者在应用中使用该权限）
2. 为了接收广播，在应用清单文件中声明使用某项权限

参考：https://blog.csdn.net/weixin_40255793/article/details/103443124
