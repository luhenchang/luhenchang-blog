## 一、wifi-adb调试

Android 10以上的可以连接同一网段AndroidStudio进行调试debug。

```
1、查找设备
   adb devices查看设备是否USB连接
2、设置端口
   adb tcpip 5555
3、连接 
   ip地址可以在android设备的无线网里面进行查看
   adb connect 192.168.137.196:5555
     
```

## 二、屏幕相关

#### 1、获取屏幕

```
$ adb shell wm
usage: wm [subcommand] [options]
       wm size [reset|WxH]
       wm density [reset|DENSITY]
       wm overscan [reset|LEFT,TOP,RIGHT,BOTTOM]
```

#### 2、获取apk正在运行的路径

```
adb shell pm path com.zui.deskclock

```
##### 2.1、通过包名获取对于版本号

```
adb shell pm dump  com.zui.deskclock | grep version
```

#### 3、获取目前系统屏幕window情况

```
adb shell dumpsys window windows
```

#### 3.1 查看堆栈信息


```
 adb shell dumpsys activity activities | grep deskclock
```


#### 4、查看Lenovo信息

```
1、adb shell
2、getprop　
3、getprop | grep ro.enovo.tablet
4、adb devices List of devices attached
```
#### 5、查看系统版本信息

```
cat /system/etc/version.conf
```

#### 6、这个来查询权限 

```
adb shell dumpsys package com.zui.recorder | grep permisson.
```

#### 7、查询生命周期流程

```
adb logcat -b events | grep wm_
```
#啊
#### 8、查询应用程序各个模块的PID并且杀掉进程
```
adb shell top
adb shell kill pid
```
#### 9、日志相关操作
```
//常规日志
adb logcat > 文件路径/name.txt
//日志过滤
[mac Linux用grep,windows用 find]
adb logcat |grep > 文件路径/name.txt
//清楚就日志
adb logcat -c
//结束抓日志
ctrl+c
//audio相关的日志
adb shell dumpsys audio> /Users/wangfeiwangfei/Desktop/logcat/shaloqg.txt
//查看媒体音量
adb shell settings get system volume_music_speaker
//查看听筒音量
adb shell settings get system volume_music_earpiece


```
#### 10、屏幕亮屏相关log

```
2022-06-17 10:43:44.255 3173-20223/com.android.systemui D/KeyguardViewMediator: notifyScreenTurnedOn
2022-06-17 10:43:44.255 3173-20223/com.android.systemui D/KeyguardViewMediator: startAntiWhenScreenOn


2022-06-17 10:43:44.255 1173-1862/system_process I/DreamManagerService: Gently waking up from dream.
2022-06-17 10:43:44.255 3173-20223/com.android.systemui D/KeyguardViewMediator: onScreenTurnedOn: mShowing = true mOccluded = false
2022-06-17 10:43:44.255 3173-3173/com.android.systemui D/KeyguardViewMediator: handleNotifyScreenTurnedOn

2022-06-17 10:43:44.255 3173-3173/com.android.systemui D/misoperation: keyguardScreenOnChange screenOn = true
```



3、其他设置

```
1）getprop

在Android系统中，使用getprop命令可以从系统中读取一些设备信息，属性的文件例如：

init.rc
default.prop
/system/build.prop
查询Android设备的所有配置信息：

adb shell getprop
在Android终端上运行上面命令就会列出所有的配置信息，如下所示：



在所有列出的配置当中，以ro开头的是只读属性。

查看Android设备的单个配置信息：

adb shell getprop <prop-name>
例如，查看单板的信息，可以使用下面命令：

adb shell getprop ro.product.board


此外，还能和管道命令符|结合使用进行配置输出的过滤：

查看有关于虚拟机dalvik的相关配置信息，可以使用下面的命令：

adb shell getprop | grep dalvik


 

（2）setprop

在Android设备终端上使用setprop可以对设备的一些配置进行设置，但是前提下，这些配置是可以写的，而不是ro类型，设置配置的命令如下：

setprop <prop-name> <value>
例如，修改进程默认分配的可以使用堆内存大小：

adb shell setprop dalvik.vm.heapgrowthlimit 128m


 

（3）watchprops

在Android系统中，使用watchprops命令来监听系统属性的变化，在此期间，如果系统的属性发生变化则将变化的值显示出来，如下：

adb shell watchprops
```


```
下载地址:
build2
build3
Unlock Device

MTK TULIP
adb reboot bootloader
fastboot flashing unlock
看屏幕信息用音量键选择


OEM解锁
执行adb disable-verity提示：Device is locked. Please unlock the device first 解决方法：
(1)进入开发者模式，打开OEM 解锁
(2)adb reboot bootloader进入fastboot模式
(3)执行
fastboot flashing unlock
fastboot getvar unlocked
会提示Finished. Total time: 0.025s
(4)如果机器没有自动重启，则执行
fastboot reboot
重启手机.在运行过程中我的机器会自动重启所以省略了这一步
(5)开机之后，
依次
adb root
adb disable-verity
adb reboot
即可，此时查看OEM 解锁项是灰

     
刷机先运行
adb reboot edl


特殊情况请尝试
Power off-> hold volume + -> plug USB cable -> wait few time

Hold volume -  and power button to reboot



Tulip操作
1、打开开发者中的OEM
2、adb reboot bootloader
3、fastboot flashing unlock
4、根据屏幕提示，按音量下键
5、根据提示重启即可

```
11、进入data的快捷命令>run-as package_name
```
adb shell
halo:/ $ run-as com.zui.recorder
halo:/data/user/0/com.zui.recorder $ ls
cache  code_cache  databases  no_backup  shared_prefs
```


12、数据库

```
1、数据库日志命令:
adb shell setprop log.tag.SQLiteLog V && adb shell setprop log.tag.SQLiteStatements V && adb shell setprop log.tag.SQLiteQueryBuilder 

2、进入到应用数据库目录
adb shell
cd /data/user_de/0/com.zui.zhealthy/databases/
3、sqlite3 zh
4、sqlite3 zhealthy.db
5、sqlite> pragma user_version;
```





limen guohonghua
p11_pro_plush:bihan
p11_5G_WIFI:chenyong




```
#TODO: write a build template file to do this, and/or fold into multi_prebuilt.

LOCAL_PATH := $(my-dir)
###############################################################################
include $(CLEAR_VARS)

LOCAL_MODULE := XuiRecorder
LOCAL_MODULE_TAGS := optional
LOCAL_SRC_FILES := $(LOCAL_MODULE).apk
LOCAL_OVERRIDES_PACKAGES := SoundRecorder
LOCAL_MODULE_CLASS := APPS
LOCAL_MODULE_SUFFIX := $(COMMON_ANDROID_PACKAGE_SUFFIX)
LOCAL_PRIVILEGED_MODULE := false
LOCAL_CERTIFICATE := PRESIGNED
LOCAL_OVERRIDES_PACKAGES := QtiSoundRecorder
ifneq (,$(findstring $(LOCAL_MODULE),$(NO_DEX_PACKAGES)))
LOCAL_DEX_PREOPT := false
endif
#如果是非海外版可以卸载，其他不处理
ifneq ($(ZUI_TARGET_REGION),ROW)
LOCAL_MODULE_PATH := $(PREINSTALL_FOLDER)
endif
# V2 signature should set LOCAL_REPLACE_PREBUILT_APK_INSTALLED
LOCAL_REPLACE_PREBUILT_APK_INSTALLED := $(LOCAL_PATH)/$(LOCAL_MODULE).apk

include $(BUILD_PREBUILT)

# Allow background intents for XuiRecorder
include $(CLEAR_VARS)
LOCAL_MODULE := com.zui.recorder.bgintents.xml
LOCAL_MODULE_TAGS := optional
LOCAL_MODULE_CLASS := ETC
LOCAL_MODULE_PATH := $(TARGET_OUT_ETC)/motorola/bgintents
LOCAL_SRC_FILES := $(LOCAL_MODULE)
include $(BUILD_PREBUILT)

###############################################################################
# call sub-makefiles
include $(call all-makefiles-under,$(LOCAL_PATH))

```
repo相关命令
1、同步切换到对应的具体项目
```
repo sync -c lenvo/dev/CR_commit
```
2、每次提交之前需要进行更新本地为最新

```
repo sync -c .
```
3、查看项目信息

```
repo info 
```
4、提交内容
git push star HEAD:refs/for/bs_mtk8798_inception_dev
```
git push start
```
