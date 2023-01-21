# matebook-x-pro-2020-hackintosh
matebook x pro 2020 hackintosh

English version wait me free

原链接如下：https://github.com/RepoWeaver/MateBook-X-Pro-2020-OpenCore  作者已经删除这个仓库，可惜了

此EFI同时支持Big Sur，Monterey和Ventura。

最新的oc0.8.8。根据源代码，精简编译了蓝牙，wifi以及声卡，只支持本机使用，如果你在使用中有wifi，蓝牙以及声卡的问题，可以下载原版驱动替换

⚠️注意：已删除内置smbios信息，使用前请注入自己的smbios信息，smbios机型选择MacBookPro16,2

不支持三星pm981/a，必须更换

文件夹内有个config-lockCFG.plist是没解锁cfg和dvmt使用的，默认是已解锁cfg和dvmt，解锁教程看下方


Intel(R) UHD 620显卡

Intel(R) Wireless-AC & Intel(R) 蓝牙

支持 HWP（Intel Speed Shift 和 Intel SpeedStep）的电源管理- 电池寿命改进 - 取决于您的 CPUFriendFriend.kext 文件

睡眠和唤醒（支持原生 macOS hibernatemode3）

休眠hibernatemode25（支持原生 macOS HibernationFixup.kext）

电池支持，更好的内存访问和[电池信息补充和涡轮增压禁用（应用程序）的集成

自动背光控制（未测试）

修复启动时黑屏（不再需要关闭和打开盖子&#127881;)

从睡眠中唤醒后的正确电源管理

我注意到，通过集线器插入显示器时，您可能需要插入两次（这种情况总是发生，只是指出一些事情）

背光快捷键（F1 [降低亮度] - F2 [提高亮度]）

音量快捷键（F4 [静音] - F5 [降低音频电平] - F6 [提高音频电平]）

Realtek ALC256卡的音频（通过AppleALC.kext和layout-id 97）

扬声器（4 声道）和内置麦克风

耳机插孔 [2 合 1]（通过ALCPlugFix）

HDMI 2.0最多两个 4K @60 Hz 显示器（通过 LSPCON）

显示 3K 的本机颜色配置文件

触控板和原生 macOS 手势

触摸屏（禁用）

PCI 设备延迟支持和系统信息应用程序的完整描述

具有适当功率级别的USB 端口映射（Type-A:1 和 Type-C:2）

Thunderbolt 端口（有限支持）

高清摄像机

NVRAM 原生支持



bios设置
禁用安全启动、禁用 TPM
备注
英特尔蓝牙无法支持某些蓝牙设备
默认情况下禁用触摸屏支持（电池改进）

关于解锁cfg和dvmt，网上的工具进去之后发现找不到数值，可以使用以下软件，
InsydeH2OUVE_x86_WINx64_200.00.01.00.zip
链接: https://pan.baidu.com/s/1F6cT6D26Nmd2re45bkBAAg 提取码: 1121⚠️注意：改完cfg重启后验证无误再改dmvt，个人测试同时修改的时候第二个不会保存
解压后打开，左上角file-load runtime,左侧栏双击Variable，
找到cpusetup双击，竖排找0030，横排找0E，原始数值01，把它改成00，然后在cpusetup前打勾，点击左上角紫色的保存图标即可，重启后验证数值是否还是00，cfg解锁成功

解锁dmvt，左上角file-load runtime,左侧栏双击Variable，
找到SaSetup双击，竖排找0100，横排找07，原始数值01，把它改成02。再竖排找0100，横排找08，原始数值02，把它改成03，然后在Sasetup前打勾，点击左上角紫色保存图标即可，重启后验证数值是否是02和03，dmvt解锁成功


安装后设置：有些朋友引导win系统有问题，在matebook上非常不建议oc引导win，哪怕注入本机uuid也不推荐
设置efi/refind/refind_x64.efi为第一引导，就可以用refind正常启动win和oc，免去oc引导win10的问题和每次开机按f12选择启动项。用refind之后，在oc里按Ctrl+回车键把mac启动项设为默认，再把等待时间改为0，refind选择mac就可以直接启动黑苹果

睡眠设置：
解锁cfg后，

设置/节能中的电源or电池里的硬盘睡眠不要勾选，

电源小憩不压迫勾选，

网络唤醒不要勾选，
设置/蓝牙中的高级/蓝牙唤醒不要勾选

powernap会不时唤醒系统以检查邮件、进行 Time Machine 备份等...

proximitywake可以在 iDevice 靠近时唤醒您的机器。

tcpkeepalive已解决设置 iCloud 后的周期性唤醒事件。

womp在局域网上醒来。

综上，终端按需输入，数字0为关闭，一行一回车：

sudo pmset -a powernap 0

sudo pmset -a proximitywake 0

sudo pmset -a tcpkeepalive 0

sudo pmset -a womp 0



