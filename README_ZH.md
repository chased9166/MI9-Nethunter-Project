# MI9-Nethunter-Project
<br> 警告：该内核仅在用于黑客技术的学习和交流，禁止非法使用，期间发生和导致的任何责任问题都与本人无关！ [For English](https://github.com/shandongtlb/MI9-Nethunter-Project)

<br> 该内核基于高通官方CAF-SM8150源码合并小米内核树并进行修改，适用于MIUI_Q,基本上实现了Nethunter官网支持手机的全部功能并且已解决已知的所有问题
<br> 开源源码地址（并没有打Nethunter补丁，可以自行用我提供的patch合并,当然你还需要自己配置defconfig） [kernel source](https://github.com/shandongtlb/msm-4.14)

<br> Nethunter补丁，理论上支持所有4.14.x内核版本的手机 [Nethunter kernel patch](https://github.com/shandongtlb/MI9-Nethunter-Project/blob/master/MI9-nethunter-4.14.patch)
<br> 小米9 Nethunter内核下载地址 [here](https://github.com/shandongtlb/MI9-Nethunter-Project/releases) 
<br> The last version: V8 20200404 4.14.175
## 内核功能
### 内核Nethunter功能 (可以使用我提供的补丁来实现 WIFI inject和HID,当然你还需要自己配置defconfig [patch](https://github.com/shandongtlb/MI9-Nethunter-Project/blob/master/MI9-nethunter-4.14.patch))
<br>  WiFi 网卡监听注入 支持2.4GHZ和5GHZ频段
<br>  支持otg外接网卡 rt3070l ar9170 rtl8187/8等等
<br>  加入新的RTL88xxAU网卡驱动！具体使用方法请看：https://github.com/aircrack-ng/rtl8812au
<br>  HID模拟键盘鼠标攻击，完美支持DuckyHID
<br>  SYSVIPC支持 (现在你可以开启PostgreSQL数据库)
<br>  DriveDroid支持
<br>  USB RNDIS 模拟网卡
<br>  RTL-SDR, AirSpy, Hackrf 支持
<br>  USB RTL8150/2/3 based 有线网卡支持
<br>  USB serial (目前支持CH341和pl2303接口)
<br>  无线扩展兼容性 (现在你可以通过使用"iwconfig"命令开启监听模式)
<br>  支持高通内置网卡开启监听, 现在你可以使用手机自身的"wlan0"网卡来开启监听模式了(暂不支持注入)
### 内核自身功能
<br>  Update to 4.14.175
<br>  添加 BBRv2 and set default
<br>  添加 830mhz gpu freq
<br>  添加 klapse5.0
<br>  添加 Audio control
<br>  添加 zen i/o调度器并设为默认
<br>  添加 dynamic fsync 并且默认关闭
<br>  设置 ddr 2133MHZ
<br>  添加 simple LMK
<br>  添加 exfat
<br>  添加 ntfs
<br>  添加 devfreq_boost
<br>  添加 ext4
<br>  添加 Network File Systems
<br>  添加 vdso32
<br>  添加一些HID驱动 (包括 Steam Controller, Nintendo switch Controller 和 XBox 游戏手柄)
<br>  添加 Shadow Call Stack(SCS) 并且默认关闭
<br>  升级 qcacld3 wlan driver 到最新
<br>  添加 andreno boost 并且默认关闭
<br>  设置 selinux 为 Permissive
<br>  高通触摸升频
<br>  实现0模块，将所有东西都编译进内核，增强通刷性
<br>  升级 wireguard 到最新
<br>  优化 f2fs
<br>  Zram: 默认lz4压缩算法
<br>  开启 target TTL 接口
<br>  use power efficient workingqueues
<br>  LLD link and ThinLTO support
<br>  使用基于高通的CAF编译，最新的驱动，更流畅更省电
<br>  .........
  
## 如何安装和使用
<br>  第一步首先在已经去除data分区强制加密的前提下在twrp备份你的boot.img和dtbo.img，然后刷入面具，最后刷入内核包，重启
<br>  第二步进入到你的系统，用mt管理器打开内核包，找到tools/ppp，将init.nethunter.rc中的所有内容全部复制到系统文件/init.usb.configfs.rc里面（打开init.usb.configfs.rc之后拉到最下面空一行粘贴就好），然后把剩下的那俩bin文件全部复制到系统根目录`/`
<br>  最后一步，重启系统并安装chroot
<br>  如果你想开启HID，你需要到终端模拟器以root身份键入以下命令 `setprop sys.usb.config win,hid`

<br>  如果你想开启手机内置网卡wlan0的监听功能, [请看这里](https://github.com/kimocoder/qualcomm_android_monitor_mode) 

<br>  由于新增rtl8812au网卡的特殊性无法直接用airmon-ng直接开启监听模式，可以通过下列命令运行:
<br>  小米手机的话要操作的应该使wlan2而不是wlan1
<br>  `ip link wlan2 down`
<br>  `iw dev wlan2 set type monitor`
<br>  `ip link wlan2 up`

<br>  建议各位使用官改MIUI，并且使用最新稳定版11.0.5，如果刷了开发版或者MIUI_eu11.0.7的话会导致指纹不可用，，这不是我的问题好吗，完全是小米指纹源码树的锅。。。有尝试修过指纹，但开发版基本每升级一次，上一次修好的指纹就不能用了，懒得再去搞，，我早就提交过 [issue](https://github.com/MiCode/Xiaomi_Kernel_OpenSource/issues/1213) 但一直没有回应，所以还是安心用11.0.5的稳定包吧，国内eu都可。。。

## 已知问题
请告诉我哦

## 感谢名单 (排名不分先后)
<br> Thanks [CAF-SM8150](https://source.codeaurora.org/quic/la/kernel/msm-4.14/) for kernel source
<br> Thanks [kimocoder](https://github.com/kimocoder) for rtl88xxau driver and any help 
<br> Thanks [johanlike](https://github.com/johanlike) for Enable Qcom WiFi monitor mode and any help
<br> Thanks [simonpunk](https://forum.xda-developers.com/oneplus-5/development/burgerhunter-t3638810) for HID patch
<br> Thanks [Evirakernel](https://github.com/evirakernel) for some help
<br> Thanks [acai66](https://github.com/acai66) for any help
<br> Thanks [h1jacker](https://github.com/h1jacker) for any help
<br> Thanks [Bcap03](https://github.com/Bcap03) for any help
<br> Thanks [osm0sis](https://github.com/osm0sis/AnyKernel3) for busybox and anykernel3