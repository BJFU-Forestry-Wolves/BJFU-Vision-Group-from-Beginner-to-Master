<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/229176129233157162.svg" alt="229176129233157162" style="zoom:150%;" />

<div STYLE="page-break-after: always;"></div>

$$
\Huge \textbf{Contributor}
$$

------------------------------

> Update: 2026/02/07

（按贡献时间先后顺序排序）

叶睿聪（[CCongCirno](https://github.com/CCongCirno)）、刘明楷（[milchstrasse565](https://github.com/milchstrasse565)）、洪佳（[Xiancaijiang](https://github.com/Xiancaijiang)）、杜雨蒙、邱万理、程英杰（[cheng-lao](https://github.com/cheng-lao)）、胡彦祺（[huer512](https://github.com/huer512)）、唐锦梁（[VaporTang](https://github.com/VaporTang)）、赵桐瑶（[LZYZofficial-cyber](https://github.com/LZYZofficial-cyber)）

<div STYLE="page-break-after: always;"></div>

$$
\Huge \textbf{目录}
$$

------------------


[TOC]

<div STYLE="page-break-after: always;"></div>

# 1 基础环境配置

## 1.1 前言

**\"工欲善其事，必先利其器。\"**

在深入探索 RoboMaster 复杂的机器人算法之前，拥有一个稳定、高效且易于调试的开发环境是所有工作的基石。初入视觉组，环境配置往往是入门的第一道槛。面对陌生的 Linux 命令行、缺失的驱动以及各种报错，很容易让人在写下第一行代码前就感到挫败。

本章的设计初衷，正是为了总结经验，帮助你完成开发环境的配置。

鉴于视觉组的绝大部分算法代码最终都需运行在 Ubuntu 系统上，本章将详细介绍如何在你的计算机上部署 Ubuntu 环境。针对不同的硬件条件和使用需求，我们提供了三种主流方案供你选择（详细流程请见参见 1.2）：

- **方案A：Ubuntu 双系统（详见 1.2.1）**
  - **简介：**也就是在电脑上同时安装 Windows 和 Ubuntu 两个独立的操作系统。
  - **优点：**性能最强，能够完整发挥硬件算力。
  - **缺点：**无法同时使用 Windows 软件，切换系统需要重启电脑。
- **方案 B：WSL2 (Windows Subsystem for Linux 2)（详见 1.2.2）**
  - **简介：**微软在 Windows 10/11 中提供的原生 Linux 运行环境。
  - **优点：**相比虚拟机性能更好，且能与 Windows 无缝同时使用，文件交互方便。
  - **缺点：**硬件访问受限（对 GPU、USB 设备、串口的支持尚不完善），且跨文件系统读写性能较差。
- **方案 C：虚拟机（详见 1.2.3）**
  - **简介：**使用 VMware 或 VirtualBox 等软件模拟一台虚拟电脑。
  - **优点：**拥有完整的 Linux 内核，相比 WSL2 对 USB / 串口等的支持相对完善；有快照和回滚功能，系统崩溃可一键复原，试错和分发成本低。
  - **缺点：**性能损耗较大。若使用的是轻薄本或内存仅有 16GB，可能会感到明显卡顿。同时可能会遇到显示 / 渲染等问题。

## 1.2 操作系统安装

### 1.2.1 Ubuntu 双系统 / 单系统安装

> Contributors: 叶睿聪 (dgsyrc@github)、唐锦梁

> 安装双系统时，若操作不当可能会导致电脑数据被清除，请按照指引谨慎操作。

####  1.2.1.1 空间预留

纯Ubuntu安装可跳过空间预留步骤

方法一：如果电脑有多的硬盘插槽，可以直接买新的固态硬盘装上电脑直接跳过本步骤，硬盘的安装可以自己搜（过程很简单），怕弄坏可以拿硬盘找官方保修点装

方法二：直接将某个盘下的文件全部移动到另一个盘，如果该盘下装有软件，请先卸载再安装到另一个盘

盘的容量不一定要200G左右，可以比这个大，后面多的空间可以单独再分出来存东西

![image-20230713153049184](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20230713153049184-1699090495506-20.webp)

右键，此电脑->管理

![image-20230713153304347](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20230713153304347-1699090555520-22.webp)

进入存储->磁盘管理，右键删除刚才清理出来的盘

![image-20230713153531600](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20230713153531600-1699090580234-24.webp)

删完后会变成这样

![image-20230713153609066](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20230713153609066-1699090595617-26.webp)

其它方法：例如用 Diskgenius 等工具，方法很多，只要能不丢失原有数据分出空闲分区即可

####  1.2.1.2 系统安装盘

[Ventoy（用于制作安装系统的启动盘）](https://www.ventoy.net/cn/download.html)

插U盘

要求：一个8G以上的协议至少为 **USB3.0** 的U盘（不能用SD卡，后面安装大概率装不上，USB3.0以上协议的特征是USB口是**蓝色**的），且U盘为空（后面需要格式化），如果没有U盘可以用移动硬盘（doge

**解压**下好的Ventoy，打开

![image-20230713152631709](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20230713152631709-1699090648360-28.webp)

选择你的U盘，点击安装

![image-20230713154300474](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20230713154300474-1699090719320-33.webp)

下载Ubuntu 22.04.5 的安装镜像，可以选择从清华镜像站下载或北林云盘下载（校园网不消耗流量）

[Ubuntu 22.04.5 iso 清华镜像站](https://mirrors.tuna.tsinghua.edu.cn/ubuntu-releases/22.04/ubuntu-22.04.5-desktop-amd64.iso)

[Ubuntu 22.04.5 iso 北林云盘](https://yunpan.bjfu.edu.cn:443/link/F0B97E8905700A4CC8D397EE791219C8)

安装好后会看到电脑里有个叫 Ventoy 的盘，把下好的 Ubuntu 22.04 镜像放进去

![image-20230713154523447](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20230713154523447-1699090731798-35.webp)

*上图示例为 22.04.2，下载链接为 22.04.5，安装 22.04.5 的即可*

####  1.2.1.3 Ubuntu安装

> 参考资料：
>
> [13] [关于重装电脑碰到的BUG及其修复教程_verification failed:(0x1a)-CSDN博客 - https://blog.csdn.net/](https://blog.csdn.net/Sco_ohhG/article/details/135394506)

若无法进入 BIOS（不显示按F几进入setup或者boot之类的字样且按对应按键无反应）

若为已有Ubuntu进行重装，进入Ubuntu，终端输入以下指令重启即可进入BIOS更改引导顺序（Boot -> Boot Priority）

```
sudo systemctl reboot --firmware-setup
```

若为格式化后的空盘（或新的硬盘无预装系统），显示找不到启动盘且无法进入 BIOS

插入制作的 Ventoy 启动盘后显示：

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/e9d0256177cdae101e9ed14fd12d2549.webp" alt="img" style="zoom:50%;" />

选择 OK 后选择 Enroll Key

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20250215014657546.webp" alt="image-20250215014657546" style="zoom:50%;" />

回车

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20250215014747223.webp" alt="image-20250215014747223" style="zoom:50%;" />

选择 `.cer` 即可，确认后 reboot 即可进入 ventoy

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20250215014712038.webp" alt="image-20250215014712038" style="zoom:50%;" />

#####  1.2.1.3.1 双系统 Ubuntu 安装

重启电脑，但不要进windows

这里需要自己查询自己的电脑开机时按哪个键更改启动盘，或者进BIOS更改启动顺序

常见的有 `F2` `F9` `F12`

如果键盘上的这些键是小字，功能图标是大字，那在按的的时候要跟 `Fn` 一起按

然后选择带USB的那个启动（假如提示无法通过该盘启动，可能是没关安全启动（Secure Boot），需要到BIOS里面关掉）

进入下图后回车即可

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/992d6035218781a390a1584b98bda98-1699090847110-37.webp" alt="992d6035218781a390a1584b98bda98" style="zoom: 25%;" />

选择第一个然后回车

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/1c6ef2bb427842de9e35b6955bd28bc-1699090876871-39.webp" alt="1c6ef2bb427842de9e35b6955bd28bc" style="zoom: 50%;" />

等待进入Ubuntu的安装界面

如果在这一步出现白字刷屏报错，显示Live CD启动失败及无法打开某个block则需要换个U盘做启动盘（一般是因为U盘不是USB3.0或者使用存储卡+读卡器安装）

别的错误自行使用 bing 搜索解决（

进入Ubuntu安装界面，点击Install

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/2d540ce7b97ed2c8fa821bc9d056c83-1699103425924-41.webp" alt="2d540ce7b97ed2c8fa821bc9d056c83" style="zoom: 30%;" />

语言选**English**，因为中文下自动生成的中文路径在后面使用过程中容易出问题

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/056956bafba0f412f4c2af4f56106ed-1699103485274-43.webp" alt="056956bafba0f412f4c2af4f56106ed" style="zoom:30%;" />

连接wifi，后面需要联网自动安装驱动（不要使用需要网页登录的wifi，如学校的，这里没法登录）

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/67a62d677cec452208b7273afc192df-1699103523013-45.webp" alt="67a62d677cec452208b7273afc192df" style="zoom:30%;" />

把 `Install third-party` 勾上，这个是自动安装驱动

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/50b36f817644504fed935c43d12a4dc-1699103538149-47.webp" alt="50b36f817644504fed935c43d12a4dc" style="zoom:30%;" />

这一步很**重要**，别选错了，选错你的电脑数据就没了

选择 `Something else`

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20230713160924192-1699103582809-49.webp" alt="image-20230713160924192" style="zoom:40%;" />

接着找到前面步骤中预留的空间（显示 `free space` 字样的）

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20230713161200118-1699103616156-51.webp" alt="image-20230713161200118" style="zoom:40%;" />

点击 `+` 

先新建 `swap` 分区

空间按 16G = 16384MB 分

选择逻辑分区

下面 `Use as` 选择 `swap area`

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20230713161326158-1699103634546-53.webp" alt="image-20230713161326158" style="zoom:50%;" />

确定后再新建 `boot` 分区

空间分 4G=4096MB

选择逻辑分区

下面 `Use as` 选择 ` Ext4 journaling file system`

 `Mount Point` 选择 `/boot`

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20230713162017982-1699103844672-55.webp" alt="image-20230713162017982" style="zoom:50%;" />

确定后再新建 `/` 分区

空间分 100G = 102400MB（如空间不足，分配40G左右也可）

选择逻辑分区

下面 `Use as` 选择 ` Ext4 journaling file system`

 `Mount Point` 选择 `/`

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20230713162816368.webp" alt="image-20230713162816368" style="zoom:50%;" />

确定后再新建 `/home` 分区

空间按需即可，如果是前面单独分出来的空间，直接把剩下的部分都分到这个分区（推荐最少40G）

选择主分区

下面 `Use as` 选择 ` Ext4 journaling file system`

 `Mount Point` 选择 `/home`

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20230713163328631-1699104129254-59.webp" alt="image-20230713163328631" style="zoom: 50%;" />

下面的 `Device for boot loader installation` 选择 `/boot` 所在的 `Device`

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20230713163419499-1699104140456-61.webp" alt="image-20230713163419499" style="zoom:60%;" />

接着点 `Install Now`

位置选 `Shanghai`，这个是用来确定时区的

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20230713163617658-1699104169521-63.webp" alt="image-20230713163617658" style="zoom:50%;" />

下一步要填写用户名与密码，如果不想每次登录输密码把 `Log in automatically` 选上

等待安装完成即可，可能比较慢，取决于网络环境

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20230713163727691-1699104185993-65.webp" alt="image-20230713163727691" style="zoom:40%;" />

安装完成后会提示重启，后面还会提示拔U盘，拔掉U盘回车即可

如果没重启，手动开机就行

开机的时候会进去Grub界面，可以通过键盘上下键更改选择（如果没得选择，仅显示grub命令行界面，请参看2.1.4部分）

在 `Ubuntu` 那一行回车进入 `Ubuntu`

在 `Windows Boot Manager` 那一行回车进入 `Windows`

#####  1.2.1.3.2 单系统 Ubuntu 安装

前步骤同 1.2.1.3.1 节中，至选择 `Something else` 步骤

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20230713160924192-1699103582809-49.webp" alt="image-20230713160924192" style="zoom:40%;" />

但进入后删除目标安装硬盘（例nvme02）中的所有原有分区（除了efi），不要删错删成U盘的或别的硬盘

后续步骤同2.1.3.1节的分盘及往后步骤

#### 1.2.1.4 输入法安装

> 可选

> Contributors: 洪佳、叶睿聪

> 参考资料：
>
> [8] [ubuntu安装搜狗输入法，图文详解+踩坑解决-CSDN博客 - https://blog.csdn.net/](https://blog.csdn.net/qq_42257666/article/details/129098009)
>
> [9] [ubuntu系统安装好搜狗输入法后只能输入英文，无法输入中文的解决方案_ubuntu搜狗输入法无法输入中文-CSDN博客 - https://blog.csdn.net/](https://blog.csdn.net/qq_39779233/article/details/128086129?csdn_share_tail={"type"%3A"blog"%2C"rType"%3A"article"%2C"rId"%3A"128086129"%2C"source"%3A"Hong_J_0826"}&fromshare=blogdetail)
>
> [15] [Ubuntu22.04 系统添加中文输入法 - zensi - 博客园 - https://www.cnblogs.com/](https://www.cnblogs.com/zensi/p/17725119.html?_refluxos=a10)

##### 1.2.1.4.1 添加中文语言支持

系统设置—>区域和语言—>管理已安装的语言—>在“语言”tab下—>点击“添加或删除语言”

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20240124183255432.webp" alt="image-20240124183255432" style="zoom:33%;" />

弹出“已安装语言”窗口，勾选中文（简体），点击应用

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20240124183315544.webp" alt="image-20240124183315544" style="zoom:33%;" />

以下两节（2.9.2/2.9.3）二选一即可

##### 1.2.1.4.2 ibus-Pinyin 安装

终端执行命令安装

```
sudo apt-get install ibus-pinyin
```

安装完成后，重启

重启前往 `Setting->Keyboard`

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/Screenshot from 2025-03-03 19-52-35.webp" alt="Screenshot from 2025-03-03 19-52-35" style="zoom:50%;" />

点击 `+` 号

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/Screenshot from 2025-03-03 19-53-19.webp" alt="Screenshot from 2025-03-03 19-53-19" style="zoom:50%;" />

选择 `Chinses`

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/Screenshot from 2025-03-03 19-53-35.webp" alt="Screenshot from 2025-03-03 19-53-35" style="zoom: 80%;" />

选择 `Intelligenc Pinyin` 即可

##### 1.2.1.4.3 搜狗输入法安装

###### 1.2.1.4.3.1 输入法系统安装

回到“语言支持”窗口，在键盘输入法系统中，选择`fcitx`

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20240124183327528.webp" alt="image-20240124183327528" style="zoom:33%;" />

如果你没有`fcitx`选项，先打开终端手动安装`fcitx`，等安装成功之后再执行上述步骤：

```
sudo apt-get install fcitx
```


点击“应用到整个系统”，会输入密码进行验证，然后关闭窗口，重启电脑

然后设置`fcitx`为开机自启动

```
sudo cp /usr/share/applications/fcitx.desktop /etc/xdg/autostart/
```

###### 1.2.1.4.3.2 下载安装包

打开终端输入`uname -a` 查看系统架构
进入[搜狗输入法`linux`下载页面](https://shurufa.sogou.com/linux)，选择适合你ubuntu架构的版本download

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20240124183346251.webp" alt="image-20240124183346251" style="zoom:33%;" />

###### 1.2.1.4.3.3 安装输入法和依赖

①安装输入法

```
cd 安装包目录
sudo dpkg -i sogoupinyin_版本号.deb
```

②安装所需依赖，完成后重启电脑。

```
sudo apt install libqt5qml5 libqt5quick5 libqt5quickwidgets5 qml-module-qtquick2
sudo apt install libgsettings-qt1
```

###### 1.2.1.4.3.4 配置输入法

①查看桌面右上角的键盘图标，看到列表中出现了搜狗，需要配置一下才能使用

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20240124183358842.webp" alt="image-20240124183358842" style="zoom:33%;" />

②点击配置当前输入法，进入输入法配置界面，我的和原作者一样是直接自动添加好了（如果你也是看完3和4点再来尝试），正常来说这里是没有添加搜狗输入法的

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20240124183413892.webp" alt="image-20240124183413892" style="zoom:33%;" />

如果你点配置，出现以下报错，就是缺少图形界面的依赖，需要安装一下`fcitx-config-gtk`

```
sudo apt install fcitx-config-gtk
```

③点击+号，然后弹出“添加输入法”的窗口，这里一定要把下面的“仅显示当前语言”取消勾选，然后在下面的搜索框中输入`sogou`，再选择搜狗输入法，点击确认添加进来

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20240124183426547.webp" alt="image-20240124183426547" style="zoom:33%;" />

4)如果在2步是自动添加好的搜狗输入法，选中搜狗输入法点`-`取消掉，然后再执行第3步，不然你永远也调不出来搜狗输入法或者输入中文。

###### 1.2.1.4.3.5 其他

①上面步骤做完后可以使用搜狗输入法但是只能输入英文，这可能是缺少包导致的，你可以去官网重新下载deb安装包进行尝试

也可以尝试一下下载以下两个包

```
sudo apt-get install libqt5qml5 libqt5quick5 libqt5quickwidgets5 qml-module-qtquick2
sudo apt install libgsettings-qt1
```

②设置输入法的快捷键，你既可以在系统提供的配置窗口设置，显示高级选项会有更多的设置；

也可以点击搜狗输入法的悬浮窗上的设置按钮，进行直接设置。


####  1.2.1.5 常见问题

**① U盘安装时进不去Ubuntu安装界面，卡在黑屏白字页，内容显示某个block error且刷屏**

**触发原因：**U盘问题

**解决方式：**换个U盘，请保证U盘为USB3.0以上（蓝色插头），换了就行

**②Ubuntu安装好后重启卡在Grub命令行界面，找不到选项进入Ubuntu和Windows Boot Manager**

> 参考资料：
>
> [4] [重装Ubuntu后开机停在Grub命令行的解决办法_ubuntu开机卡在命令行-CSDN博客 - https://blog.csdn.net/](https://blog.csdn.net/weixin_44481159/article/details/109240338)

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20231203161811736.webp" alt="image-20231203161811736" style="zoom: 50%;" />

**触发原因：**未知

**解决方式：**

依次输入如下命令

先查看硬盘信息

```
ls
```

寻找boot分区

```
ls (hd0,gptX)/
```

注意上面的 `hd0,gptX` 为前面查看硬盘分区信息时列出的编号，一个个查即可，如果此时列出的的文件信息包含grub文件夹，那么这个编号对应的就是boot分区

接着是关联grub（以 `hd0,gpt5` 为例）

依次输入这三行命令

```
set root=(hd0,gpt5)
set prefix=(hd0,gpt5)/grub
normal
```

输完后即可进入grub的引导选择页面，直接进Ubuntu

进入Ubuntu后，打开终端，先更新grub

```
sudo update-grub
```

接着下载别人做好的修复工具（记得联网）

```
sudo add-apt-repository ppa:yannubuntu/boot-repair && sudo apt-get update
sudo apt-get install -y boot-repair && boot-repair
```

接着修复工具会自动启动，修复方式选择推荐修复（recommend），期间会要求你复制它显示的一些命令到终端，新开一个终端复制进去执行即可

还有Yes/No的选择页面，都选Yes就行

按工具提示执行完所有步骤后，重启就能够自动进入grub的启动选择页面了

**③ Ubuntu与Windows双系统切换后Windows系统时间异常（通常相差8小时）**

**触发原因：**Linux 默认将主板硬件时钟（RTC）视为 UTC 时间（世界协调时间）。其在显示时间时，会根据设置的时区（如中国 CST +8）自动加上偏移量。Windows 默认将主板硬件时钟视为 Local Time（本地时间）

**冲突过程：**Ubuntu 将 RTC 设置为 UTC 时间（例如 0:00），界面显示为北京时间 8:00。重启进入 Windows，Windows 读取 RTC 为 0:00，直接当作本地时间显示，因此 Windows 显示时间为 0:00（慢了 8 小时）。如果在 Windows 中修正了时间为 8:00，RTC 也会被改为 8:00。重启回 Ubuntu，Ubuntu 读取 RTC 为 8:00（认为是 UTC），再加 8 小时时区，界面显示为 16:00（快了 8 小时）。

**解决方式：**为了解决冲突，我们需要统一两个系统对待硬件时钟的标准。最简单且推荐的方法是修改 Ubuntu 的设置，使其顺应 Windows 的习惯（使用本地时间）。

方式一：修改 Ubuntu 设置（推荐）

进入 Ubuntu 系统。打开终端，输入以下命令并回车：

```
timedatectl set-local-rtc 1 --adjust-system-clock
```
验证设置，终端输入以下命令
```
timedatectl
```
如果输出中包含 `RTC in local TZ: yes`，说明设置成功
重启电脑进入 Windows，进入"设置"→"时间和语言"→"日期和时间"→"自动设置时间"，将"自动设置时间"开关从开拨到关，然后再从关拨到开（可能需要等待一段时间）

方式二：修改 Windows 注册表（仅供参考）（如选择方法一操作后无需再进行方法二操作!!!）

改动 Windows 注册表有风险，谨慎操作!!!

此方法在技术上更“正确”，但操作稍微繁琐，并且可能由于操作不当造成一些风险。

进入 Windows 系统，按下 `Win + R`，输入 `regedit` 并回车，打开注册表编辑器

定位到以下路径：`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\TimeZoneInformation`

在右侧空白处右键，选择 新建 (New) -> DWORD (32-bit) Value

![image-20230713165504671](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/双系统时间错乱修复-方式二-修改Windows注册表截图.webp)

将其命名为 `RealTimeIsUniversal`，双击该项，将其数值数据（Value data）修改为 `1`

重启电脑进入 Ubuntu，确保时间正确。再次回到 Windows，时间应当已自动同步正常

**后话：**虽然更推荐使用方式一来解决双系统时间冲突问题，虽然方式一是解决双系统时间冲突最简单的方法，但在技术原理上，其实是一种"不完美"的妥协。Linux 社区和系统开发者通常强烈建议使用 UTC，这是因为 Local Time 在某些场景（夏令时切换、跨时区旅行、双系统同时尝试调整夏令时）下会导致逻辑错误或系统故障。那既然问题这么多，为什么我还是推荐方式一呢? 因为作为一个中国大陆的居民，中国早已废除夏令时，所以只要不频繁跨时区出差/旅行，使用 Local Time 没有任何感知上的副作用。也推荐对 Windows 注册表有一定了解的用户使用方式二进行操作，从技术的角度上说，方式二更稳健、更规范

**④ Ubuntu缺少无线网卡驱动**
若安装Ubuntu后，设置中找不到wifi连接，参考以下步骤解决（适用于Intel的无线网卡）

打开终端，输入以下指令确定无线网卡属于intel

```
lspci -nn
```

若有显示 `Network controller [0280]: Intel Corporation Device`，说明为Intel无线网卡

先使用USB连接手机网络以便下载环境

USB共享网络打开方式（路径仅供参考，因具体系统而异）：`热点->更多共享设置->USB共享网络`

注意要接好线再打开，否则可能不显示USB共享网络选项

编译环境安装

```
sudo apt-get install make bison flex git
```

下载以下包：

```
git clone https://github.com/intel/backport-iwlwifi.git
git clone git://git.kernel.org/pub/scm/linux/kernel/git/firmware/linux-firmware.git
```

进入 `backport-iwlwifi` 下的 `iwlwifi-stack-dev` 文件夹打开终端并编译

```
sudo make defconfig-iwlwifi-public
sudo make
sudo make install
```

进入 `linux-firmware` 文件夹打开终端复制ucode驱动文件

```
sudo cp iwlwifi-* /lib/firmware
```

重启完成安装

### 1.2.2 WSL2

> Contributors: 叶睿聪 (dgsyrc@github)、唐锦梁

**WSL2支持Win11系统和较新的 Win10（版本 2004 及以上）**

#### 1.2.2.1 默认安装部分

打开Windows Powershell，执行命令

```bat
wsl --install
```

提示安装完成后重启电脑（若提示失败，检查控制面板/程序和功能/启用或关闭Windows功能是否如下图配置）

![image-20231101015646685](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20231101015646685.webp)
打开Powershell，输入一下命令查看支持的版本

```bat
wsl --list --online
```

![image-20231101015843375](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20231101015843375.webp)

输入以下命令设置版本为22.04

```
wsl --install Ubuntu-22.04 -n
```

安装完成后，右键Powershell标题栏

![image-20231101210913942](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20231101210913942.webp)

点击属性，选择终端选择卡，将默认终端应用程序改为 **Windows 终端**

![image-20231101210955130](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20231101210955130.webp)

关掉Powershell重新打开**（不要使用管理员模式）**

在最上面的下拉菜单选择Ubuntu 22.04.2打开

![image-20231101020428285](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20231101020428285.webp)

打开后会提示设置用户名和密码，正常设置即可

进入系统后，输入以下命令更新包

```
sudo apt update && sudo apt upgrade
```

更新完成后，回到Powershell，输入下列命令查看正在运行的子系统

```
wsl -l -v
```

![image-20231101020824525](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20231101020824525.webp)
#### 1.2.2.2 迁移系统

> 可选，硬盘空间充裕无需迁移

由于WSL2默认将子系统装在系统盘，会占用系统盘空间不便于管理，故需要迁移

首先输入以下命令停止子系统运行（Powershell）

```
wsl --shutdown
```

输入以下命令导出系统

```
wsl --export <NAME> <File>
```

其中，NAME为上面查看运行的子系统中显示的NAME，注意该命令输入时要去掉`<>` （File同理）

Flie为导出路径，例如：

```
H:\Ubuntu\Ubuntu.tar
```

如果NAME为`Ubuntu`，则完整导出命令为

```
wsl --export Ubuntu H:\Ubuntu\Ubuntu.tar
```

注意，导出路径的 `.tar` 是必要的，**否则导出失败**

导出完成后，输入以下命令删除原来的子系统

```
wsl --unregister Ubuntu
```

此处Ubuntu为你的子系统显示的NAME，以配置时实际为准

接着导入刚才导出的子系统

```
wsl --import Ubuntu H:\Ubuntu\ H:\Ubuntu\ubuntu.tar --version 2
```

其中 `Ubuntu` 为你要设置的NAME

 `H:\Ubuntu\` 为子系统将要安装的位置

`H:\Ubuntu\ubuntu.tar` 为前面导出的子系统

导入完成即可，重新打开Powershell即可在下拉菜单找到迁移后的子系统（一般图标为🐧）

#### 1.2.2.3 常见问题

- 0x80070422报错

  如下图所示情况

  <img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20240122235506269.webp" alt="image-20240122235506269" style="zoom:67%;" />

  <img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/61953d47e124f7eb9207043c8191e24.webp" alt="61953d47e124f7eb9207043c8191e24" style="zoom:67%;" />

  解决方式：

  `win+R` 打开运行，进入服务管理界面

  <img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20240122235656272.webp" alt="image-20240122235656272" style="zoom:67%;" />

  找到`WSL Service`项，将其启动即可

  <img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20240122235746522.webp" alt="image-20240122235746522" style="zoom:50%;" />

  其中启动类型设置为自动

  <img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20240122235801991.webp" alt="image-20240122235801991" style="zoom:50%;" />

  重启命令行即可修复以上问题

### 1.2.3 虚拟机

>  Contributors: 唐锦梁

Windows 上常用的虚拟化软件有 VMware 和 VirtualBox，VirtualBox 是一个开源软件，VMware是一个成熟的商业软件，但自 2024 年博通调整策略后，VMware Workstation Pro 已经对个人用户完全免费。

VMware 相比 VirtualBox 通常有更好的 3D 图形和磁盘 I/O 性能，界面相对更现代流畅，故现在更推荐使用 VMware。

VMware 的安装包下载流程相当繁琐，需要注册博通账号等一系列流程，故本文直接提供安装包的北林云盘链接供下载。如想自行前往官网下载，可以访问 [Fusion and Workstation | VMware](https://www.vmware.com/products/desktop-hypervisor/workstation-and-fusion) 自行探索。

北林云盘链接如下：[虚拟机及镜像](https://yunpan.bjfu.edu.cn:443/link/595B89CD83E3A059E95F21202673007B)

链接内包含 Ubuntu22.04.5 的系统镜像（下图红框所示），和 17.6.4 版本和 25H2 版本的 VMware，VMware任选一个版本即可，17.6.4 版本相对更稳定，25H2 版本对更新的 Intel 的支持更好，但也存在一些渲染相关的 bug，自行决定下载的版本即可。

![2026-01-23 13-47-52](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/2026-01-23%2013-47-52.webp)

下载后双击 VMware 的安装包安装

安装完成后点击创建虚拟机

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/2026-01-23 13-53-12.webp" alt="18699e1ea2ee028460c4f58b1745654" style="zoom: 33%;" />

选择 custom 模式

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/2026-01-23 14-00-54.webp" style="zoom: 50%;" />

点击 Next，再点击 Next，选择之前下载的 Ubuntu 镜像文件的位置

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/2026-01-23 14-05-28.webp" style="zoom: 50%;" />

点击 Next，输入用户名和密码，用户名只能全小写字母

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/2026-01-23 14-06-56.webp" style="zoom: 50%;" />

再点击 Next，按需选择虚拟机的存放位置，默认放在 C 盘，可自行选择虚拟机文件的存放位置

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/2026-01-23 14-08-57.webp" style="zoom: 50%;" />

建议给个 8 核，4核也可以

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/2026-01-23 14-10-01.webp" style="zoom: 50%;" />

建议 8GB 内存起步

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/2026-01-23 14-10-59.webp" style="zoom: 50%;" />

之后一路 Next，直到这一步，建议至少给 100GB，这里分配 100GB 虚拟机不会立刻占用，而是随着虚拟机的使用过程而不断增大

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/2026-01-23 14-12-17.webp" style="zoom: 50%;" />

接着一路 Next，最后点击 Finish即可

启动虚拟机，首次启动需要安装 Ubuntu 系统

选择 Install Ubuntu，语言选择 **English**

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/2026-01-23 14-17-52.webp" style="zoom: 33%;" />

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/2026-01-23 14-54-20.webp" style="zoom: 33%;" />

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/2026-01-23 14-55-26.webp" style="zoom: 33%;" />

时区选到上海即可（Shanghai，国际时区中，我国大陆的时区是用 Asia/Shanghai 来标定，而不是北京）

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/2026-01-23 14-57-56.webp" style="zoom: 33%;" />

等待安装进度条完成后会提示需要重启虚拟机，点击重启即可

第一次启动虚拟机会显示引导界面，点击右上角 "Skip"

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/2026-01-23 14-59-56.webp" style="zoom: 33%;" />

## 1.3 基础开发工具安装

### 1.3.1 VSCode 安装与配置

> Contributors: 叶睿聪 (dgsyrc@github)

#### 1.3.1.1 安装

##### 1.3.1.1.1 Ubuntu

下载好的 VSCode 的.deb安装包放到桌面

在桌面打开终端，输入以下指令

```bash
sudo apt install ./<VSCode安装包文件名>.deb
```

安装包名字可以右键安装包重命名 `Rename`  , `Ctrl + C` 复制，在终端中 `Ctrl + Shift + V` 粘贴

注：通过上述 `apt` 命令安装好 VSCode 的 `.deb` 包后，通常会自动将微软的官方源添加到你的系统中，这意味着，后续如果VSCode有更新，你不需要再傻傻的去微软的官网下 VSCode 的安装包，而是运行下面的系统更新命令即可自动更新 VSCode

```bash
sudo apt update && sudo apt upgrade
```

安装完成后在终端输入以下指令回车执行

```bash
code
```

即可打开VSCode

##### 1.3.1.1.2 Windows

下载安装即可

[Visual Studio Code - Code Editing. Redefined - https://code.visualstudio.com/](https://code.visualstudio.com/)

#### 1.3.1.2 语言包配置

打开VScode

点击

![image-20230713170625032](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20230713170625032.webp)

进入插件安装页面

在搜索栏上输入 `Chinese` 安装这个语言包

![image-20230713170734097](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20230713170734097.webp)

#### 1.3.1.3 OpenCV环境配置

安装这四个包即可

![image-20230713170802080](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20230713170802080.webp)

![image-20230713170825135](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20230713170825135.webp)

#### 1.3.1.4 Tensorflow

> 本节内容为 Tensorflow，配置环境可跳过

打开扩展管理

![image-20231101235220694](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20231101235220694.webp)

安装以下扩展包

![image-20231101235254880](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20231101235254880.webp)

![image-20231101235308585](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20231101235308585.webp)

安装完成后，在左侧菜单打开远程资源管理器

![image-20231101235415760](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20231101235415760.webp)

选择你装好环境的WSL

![image-20231101235751368](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20231101235751368.webp)

选择打开文件夹，此时会提示要打开的目录，推荐 `/home/用户名` （用户名为前面设置的username）

![image-20231102000102727](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20231102000102727.webp)

安装这两个扩展，注意是安装在WSL内，即点击这种按钮

![image-20231102000417948](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20231102000417948.webp)

**例程训练**

> 参考资料：
>
> [2] [人工智能实践：Tensorflow笔记\_北京大学\_中国大学MOOC(慕课) - https://www.icourse163.org/](https://www.icourse163.org/course/PKU-1002536002)

下载如下代码包：

```
链接：https://pan.baidu.com/s/127QAuHTod9f96L9bLb1dgw 
提取码：rm24 
```

将文件在windows下解压后，将整个class5文件夹拖进vscode的资源管理器中，即

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20231102001018674.webp" alt="image-20231102001018674" style="zoom:30%;" />

打开 `class5/CIFAR10_CNN/p46_cifar10_resnet18.py` 

![image-20231102001124426](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20231102001124426.webp)

此时会提示找不到tensorflow库的位置，鼠标移到标黄线处选择快速修复

![image-20231102001920637](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20231102001920637.webp)

选择选择其他解释器

![image-20231102002019857](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20231102002019857.webp)

选择 `Python 3.9.18('tf')`

由于版本的问题，此时代码依然会报错，修改以下代码

```
import tensorflow as tf
import os
import numpy as np
from matplotlib import pyplot as plt
from tensorflow.keras.layers import Conv2D, BatchNormalization, Activation, MaxPool2D, Dropout, Flatten, Dense
from tensorflow.keras import Model
```

为

```
import tensorflow as tf
import os
import numpy as np
from matplotlib import pyplot as plt
from tensorflow.python.keras.layers import Conv2D, Activation, MaxPool2D, Dropout, Flatten, Dense
from tensorflow.python.keras import Model
from keras.layers import BatchNormalization
```

点击VSCode右上角的运行按钮![image-20231102003925399](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20231102003925399.webp)

训练模型（第一次跑时会先自动下载训练数据）

![image-20231102001255781](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20231102001255781.webp)

注意，训练完成后需要等待一段时间才会显示图表

跑出该图即可（不一定一样）

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20231102004837869.webp" alt="image-20231102004837869" style="zoom: 40%;" />

尝试修改代码中的参数使得 Validation Accuracy 达到0.9以上

### 1.3.2 CMake

> Contributor: 叶睿聪 (dgsyrc@github)、CMake

#### 1.3.2.1 一般安装

> 不推荐本方法，更建议使按照 1.3.2.2 安装更新版本的 CMake

使用以下命令安装即可

```
sudo apt-get install cmake
```

#### 1.3.2.2 更新版本

考虑到部分库的编译对cmake的版本要求较高，在 `1.3.2.1` 中提到的方式安装的版本不能满足要求

因此需要下载cmake的新版本源码手动编译安装

链接 ：https://cmake.org/files/

下载对应Linux版本的 `.tar.gz` 压缩包即可

推荐版本范围：3.22~3.28 之间，4.x 版本编译某些仓库后续可能会遇到一些警告

往下翻，找到对应的系统版本对应的 CPU 架构对应的文件，下图中标识的是 Linux 系统 X86 架构的文件

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/2026-01-23 15-33-20.webp" alt="image-20231102004837869" style="zoom: 33%;" />

下载后使用以下命令解压（若同一目录下只有一个 `.tar.gz` 格式压缩包，可以不输入完整压缩包名称解压）

```
tar -xzvf ***.tar.gz
```

解压完成后，依次执行以下命令安装依赖以及编译安装（要在cmake目录下）

```
sudo apt-get install g++
sudo apt-get install libssl-dev
sudo apt-get install make
./configure
make -j8
sudo make install
```

检查安装后的版本

```
cmake --version
```

举例：

![image-20240221203222526](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20240221203222526.webp)

### 1.3.3 NoMachine

> Contributors: 洪佳、唐锦梁

#### 1.3.3.1 基本介绍

**NoMachine** 是一款跨平台的远程桌面软件，广泛适用于 Linux、Windows、Android 以及 ARM 架构设备等几乎所有主流操作系统。虽然市面上还有向日葵、ToDesk 等常见的远程工具，但 **NoMachine** 开源极其跨平台性，成为了本项目的首选方案。

#### 1.3.3.2 安装NoMachine

- 官网下载地址：[NoMachine - Download Free Remote Desktop Access](https://downloads.nomachine.com/) 

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/2026-01-22 21-14-11.webp" alt="image-20240125010159271" style="zoom:33%;" />

按照系统类型选择下载的安装包

Windows 下载：

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/2026-01-22 21-16-29.webp" alt="image-20240125010301693" style="zoom:33%;" />

Ubuntu 下载，根据系统架构选择 `NoMachine for Linux DEB（amd64）`：

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/2026-01-22 21-20-33.webp" alt="image-20240125010301693" style="zoom:33%;" />

点击download，注意安装目录，下载完双击打开即可，进行安装

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20240125010552041.webp" alt="image-20240125010552041" style="zoom:33%;" />

安装完成后有服务端和客户端，打开客户端

客户端成功打开如上图，第一次进入有官方使用说明，点ok不断继续即可

#### 1.3.3.3 网络连接

控制端和被控端需要处在同一个局域网内，可以通过连接同一个 WiFi(如手机热点)或有线连接，**建议被控插入一个 HDMI 欺骗器**

**注意事项：**

处在同一个局域网也可能因为防火墙设置导致无法连接。

分两种情况：

1. Windows 上 WiFi 连接
   1. 需要设置为 "专用网络"
   
      <img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/2026-01-22 21-58-06.webp" alt="image-20240125010654198" style="zoom:33%;" />

2. Windows 上 有线连接（网线）

   1. 因为无法上网，无法手动设置为专用网络，需要自行配置防火墙，进入 "高级安全 Windows Defender 防火墙"

      <img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/2026-01-22 22-13-13.webp" alt="image-20240125010654198" style="zoom:33%;" />

   2. 点击 "入站规则"，选中如下两项，右键选择 "启动规则" 即可，启用该项可解决 `ping` 不通的问题

      <img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/2026-01-22 22-17-14.webp" alt="image-20240125010654198" style="zoom:33%;" />

   3. 两台设备之间有线连接需要手动配置网段

      1. 对于 Windows 设备，打开控制面板，进入 "网络和 Internet"  → "网络和共享中心" → "更改适配器设置"（位于左侧小字） → 选中你的有限网络设备，通常命名为 "以太网 n"，下图所示的 "以太网 2" 即为有线网卡，选中后右键选择属性，双击 "Internet 协议版本 4（TCP/IPv4）" → 选中 "使用下面的 IP 地址" → IP 地址设置为 192.168.1.x（x是指一个 1-255之间的任意整数，推荐在 50~200 之间选择，注意两台电脑的 IP 地址不能完全相同） → 子网掩码设置为 255.255.255.0 →点击 "确定" → 点击 "确定"

      <img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/nomachine-修改ipv4-windows.webp" alt="image-20240125010654198" style="zoom:33%;" />
   
      2. 对于 Ubuntu 设备，"设置" → "网络" → "齿轮图标" → "IPv4" → "手动" → "地址" 填入 192.168.1.x（x是指一个 1-255之间的任意整数，推荐在 50~200 之间选择，注意两台电脑的 IP 地址不能完全相同），""子网掩码" 填入 255.255.255.0 → "应用"
   
      <img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/nomachine-修改ipv4-ubuntu.webp" alt="image-20240125010654198" style="zoom:33%;" />



#### 1.3.3.4 使用介绍

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20240125010654198.webp" alt="image-20240125010654198" style="zoom:33%;" />

通常当两个系统处在同一个局域网的情况下，会自动显示局域网内的设备列表

>  注意：控制端至少应该下载NoMachine的服务端，才能顺利连接

#### 1.3.3.5 显示优化

> 以下操作在 Windows 控制端进行

如果 Windows 的屏幕分辨率较高，需要调整 NoMachine 的缩放设置，右键属性 → "更改高 DPI 设置" → 勾选 "替代高 DPI 缩放行为" → 选中 "应用程序" → 点击"确认"

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/2026-01-23 00-36-58.webp" alt="image-20240125010654198" style="zoom:33%;" />

按下快捷键 `Ctrl + Alt + 0`，点击 Display，选中 "Resize remote display" 和 "Fullscreen"，再点击 "Change settings"，有线连接建议 "Quality" 直接拖到 `Best quality`，分辨率根据被控端的分辨率动态调整。

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/2026-01-23 00-42-19.webp" alt="image-20240125010654198" style="zoom:33%;" />

再回到软件的主界面，点击 "Settings"

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/2026-01-23 00-43-16.webp" alt="image-20240125010654198" style="zoom:50%;" />

再进入 "Performance"，按照下图配置

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/2026-01-23 00-44-33.webp" alt="image-20240125010654198" style="zoom:50%;" />

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/2026-01-23 00-45-33.webp" alt="image-20240125010654198" style="zoom:33%;" />

#### 1.3.3.6 输入优化

可能会遇到输入大小写不同步的问题，可以进入 "设置" → "辅助功能" → "重复键" 设置为关

同时建议登出后点击右下角齿轮，设置为 `Ubuntu on Xorg`，可解决相关问题

### 1.3.4 终端工具

> 可选

> Contributors: 唐锦梁

命令行（SSH）是上位机交互的基石。相比图形化界面，它几乎不占用系统带宽和算力，是代码编译、进程监控和文件管理的最佳方式。

#### 1.3.4.1 服务端配置（上位机端）

> 通常语境下，服务端就是指你的 Ubuntu 系统或视觉组算法最终部署运行的 MiniPC

```bash
# 1. 更新软件源
sudo apt update

# 2. 安装 OpenSSH Server
sudo apt install openssh-server

# 3. 确认服务状态（应显示 active (running)）
sudo systemctl status ssh

# 4. 允许防火墙通过 SSH
sudo ufw allow ssh
```

#### 1.3.4.2 客户端软件

##### 1.3.4.2.1 MobaXterm (Windows 首选)

MobaXterm 被称为远程计算的“瑞士军刀”。对于视觉组而言，它最大的优势在于自带 X Server。这意味着当你无法连接显示器时，依然可以通过 SSH 隧道将 OpenCV 等的图像窗口回传显示在你的笔记本上，这对调试代码至关重要。

**主要特性：**

- **X11 Forwarding**：原生支持远程图形界面显示
- **SFTP 侧边栏**：连接 SSH 时自动挂载文件系统，方便通过拖拽上传/下载视频和日志文件
- **多协议支持**：集成 SSH, VNC, FTP, 串口（Serial）等多种协议

**安装教程：**

1. **下载**：访问 [MobaXterm 官网](https://mobaxterm.mobatek.net/download.html)，选择 <b>Home Edition (Free)</b>。
   - *Installer edition*：传统安装版
   - *Portable edition*：免安装版，解压即用（可放入 U 盘）
2. **连接配置**：
   - 点击左上角 `Session` -> `SSH`。
   - **Remote host**: 输入上位机 IP 地址（例如 `192.168.1.100`）
   - **Specify username**: 输入上位机用户名（例如 `piesia-01`）
   - 点击 `OK`，输入密码即可连接

> **注意**：初次连接时，若想启用图形回传，请确保设置中 `X11-Forwarding` 处于勾选状态（默认已勾选）

##### 1.3.4.2.2 Tabby (跨平台/高颜值)

> 颜值即正义 (

如果你希望在 Windows 上追求更现代化的 UI 体验或者你正在使用 macOS，Tabby (原 Terminus) 是更好的选择。它是基于 Web 技术构建的终端，界面极度舒适，且配置可同步

**主要特性：**

- **跨平台**：完美支持 Windows, macOS 和 Linux
- **SFTP 支持**：拥有独立的 SFTP 面板
- **高度可定制**：支持各种配色方案、字体连字（Ligatures）和快捷键映射
- **智能补全**：内置部分命令提示功能

**安装教程：**

1. **下载**：访问 [Tabby GitHub Release](https://github.com/Eugeny/tabby/releases) 页面
   - **Windows**: 下载 `tabby-x.x.x-setup-x64.exe `
   - **macOS**: 下载 `tabby-x.x.x-macos-arm64.dmg` (M芯片) 或 `x86_64` (Intel芯片)
2. **配置**：
   - 启动软件，点击右上角齿轮图标进入 `Settings`
   - 选择 `Profiles & connections` -> `New profile`
   - 选择 `SSH connection`
   - 填入 `Name` (任意命名), `Host` (IP地址), `Username` (用户名)
   - 保存后，点击播放键图标即可连接

> **提示**：Tabby 默认不支持 X11 Forwarding。如果使用 Tabby 且需要查看远程图像，通常需要配合单独安装 XServer 软件（如 VcXsrv 或 XQuartz）

##### 1.3.4.2.3 VSCode Remote 开发配置

> 如习惯使用 VSCode，则强烈推荐此方案

传统的开发模式是：“本地写代码 -> 传输文件到上位机 -> 终端编译运行”。 **VSCode Remote 模式**是：“直接编辑上位机文件 -> 自动同步保存 -> 集成终端直接编译”

VSCode 配合 **Remote - SSH** 插件，允许我们将本地的 VSCode 界面作为“前端”，而将 MiniPC（上位机）作为“后端”运行编译环境。这意味着你可以在舒适的 Windows/macOS 界面下写代码，而实际的编译和运行环境完全是在 Linux 上

###### 1.3.4.2.3.1 安装与连接

1. **安装插件**：
   - 打开 VSCode，点击左侧侧边栏的扩展图标（Extensions）
   - 搜索 `Remote - SSH` 并安装（由 Microsoft 官方发布）
2. **配置主机**：
   - 安装完成后，点击左下角的绿色图标 `><`（Open a Remote Window）
   - 选择 `Connect to Host...` -> `Configure SSH Hosts...`
   - 选择第一个配置文件（通常是 `C:\Users\你的用户名\.ssh\config` 或 `~/.ssh/config`）
   - 在文件中按以下格式添加你的上位机信息：

代码段

```
Host RM-MiniPC
    HostName 192.168.1.100  # 替换为上位机实际 IP
    User piesia-01          # 替换为上位机用户名
    Port 22
```

1. **发起连接**：
   - 保存文件后再次点击左下角绿色图标
   - 选择 `Connect to Host...`，现在你应该能看到 `piesia-01` 出现在列表中
   - 点击连接，选择 `Linux` 作为目标平台，输入密码即可
   - 连接成功后，左下角会显示 `SSH: piesia-01`

###### 1.3.4.2.3.2 远程环境配置（关键）

连接成功并不代表配置结束。在 Remote 模式下，**插件是分两处安装的**：

1. **UI 类插件**（如主题、图标）：安装在本地
2. **功能类插件**（如 C++、Python、CMake）：**必须安装在远程服务端（MiniPC）上**

**必装的远程插件：** 请在连接 SSH 状态下，打开扩展面板，你会看到 `SSH: piesia-01 - INSTALLED` 分组。请确保在此处安装以下插件，见本文 1.3.1 VSCode 部分安装的相关插件

###### 1.3.4.2.3.3 免密登录配置

在调试比赛代码时，如果每次连接或重连都要输入密码会非常浪费时间。我们需要配置 **SSH Key** 实现免密登录。

**Windows终端执行以下命令**

```bash
# 在本地生成密钥对（一路回车即可）
ssh-keygen -t rsa
```



1. **复制本机公钥：**

- 在电脑文件夹地址栏输入 `%USERPROFILE%\.ssh` 并回车。

- 用记事本打开 `id_rsa.pub` 文件，全选并复制里面的内容（通常是以 ssh-rsa 开头的一长串字符）。

2. **连接上位机：**

- 使用 VS Code 连接到远程主机（此时还需要输入密码）。

3. **修改远程文件：**

- 在 VS Code 中，点击 `文件` -> `打开文件...`。

- 在顶部的路径栏输入：`/home/piesia-01/.ssh/authorized_keys` (如果提示找不到文件，就先只打开 `/home/piesia-01/`，然后新建文件夹 `.ssh` 和文件 `authorized_keys`)。

- 将刚才复制的公钥内容粘贴到这个文件的最后一行。

- 保存 (`Ctrl + S`)。

配置完成后，再次使用 VS Code 连接或使用终端登录时，将不再询问密码。

# 2 核心算法环境配置

## 2.1传统视觉环境	

### 2.1.1OpenCV 安装

> Contributors: 叶睿聪 (dgsyrc@github)

*方法适用于Ubuntu 20.04/22.04 以及WSL中的Ubuntu 20.04/22.04*

#### 2.1.1.1安装步骤

先安装一些环境依赖

在桌面右键打开终端 `Terminal`

依次执行以下指令

```
sudo apt update
sudo apt-get install build-essential
sudo apt-get install cmake git libgtk2.0-dev pkg-config libavcodec-dev
sudo apt-get install libavformat-dev libswscale-dev
sudo apt install -y make
```

`sudo` 指令需要输入前面设置的密码

如果提示[Y/n]，输入 Y 回车即可

如果执行 `sudo apt-get install build-essential` 时遇到

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20241125192633780.webp" alt="image-20241125192633780" style="zoom:33%;" />

请先执行以下指令即可解决

```
sudo apt-get update
```

下载 OpenCV 4.5.5 的源码和 OpenCV_Contrib 4.5.5 的源码至桌面

[OpenCV 4.5.5 的源码（Source Code）](https://github.com/opencv/opencv/releases)

[OpenCV_Contrib 4.5.5 的源码（Source Code）](https://github.com/opencv/opencv_contrib/tags)

将 OpenCV 4.5.5 源码包解压到桌面，并把 OpenCV_Contrib 解压到 OpenCV 4.5.5 所在的文件夹内

即下图：

![image-20230713165504671](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20230713165504671-1699104265052-67.webp)

在上面这个文件夹内右键打开终端 `Terminal`

输入 `mkdir build` 新建 `build` 文件夹

输入 `cd build` 打开 `build` 文件夹

然后输入以下指令

```
cmake ..
```

注意，执行 `cmake ..` 时可能会提示ippicv库/ade库的文件下载失败（务必要向上检查一遍刚才终端的输出信息【黄色字体】，这个报错信息不会在输出信息末尾提示），黄色字体中CMP0148相关错误可忽略，其它详细报错和解决方式见 `2.2.2 常见问题`

若没有报错，继续执行以下指令

```
sudo make -j8
sudo make install
```

其中第一个指令的执行时间较长，这是因为在编译OpenCV库

安装完成后，在终端中打开`opencv-4.5.5/sample/cpp/example_cmake`

新建文件夹 `build`，在终端打开后执行：

```
cmake ..
make -j8
./opencv_example
```

若出现 `Hello OpenCV` 则说明配置成功

#### 2.1.1.2 常见问题

- 提示ippicv库下载失败

  **报错信息：**

  报错信息类似下一个错误（ade库下载失败）

  **解决方案：**

  提前下好这个包

  备用链接：https://pan.baidu.com/s/1oxF0PY8Jhhr9jZ1f6xqTQg 提取码：rm24 

  此时需要提前准备好这个包并放在桌面: `ippicv_2020_lnx_intel64_20191018_general.tgz`

  重新在opencv-4.5.5文件夹内开启终端（在文件夹内右键选择`Terminal`)

  输入

  ```3
  gedit ./3rdparty/ippicv/ippicv.cmake
  ```

  此时会打开文本编辑器

  <img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20231104165159479.webp" alt="image-20231104165159479" style="zoom:50%;" />

  前文提到将 `ippicv_2020_lnx_intel64_20191018_general.tgz` 放在了桌面，故将框出的这行改为桌面的目录（原本是一个网址）

  【注意：上图的路径地址仅为示例，放在桌面的路径以下面为准】

  ```
  file:///home/你的用户名/Desktop/
  ```

  然后再次执行以下命令即可

  ```
  cmake ..
  ```

- 提示ade库下载失败

  **报错信息：**

  <img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/Screenshot from 2024-01-24 23-57-29.webp" alt="Screenshot from 2024-01-24 23-57-29" style="zoom:67%;" />

  **解决方案：**

  提前下载好这个ade包：

  官方链接：https://github.com/opencv/ade/archive/v0.1.1f.zip

  备用链接：https://pan.baidu.com/s/1PUOKD5rw2v2qqG1GuCBqxQ 提取码：rm24

  下好之后放在桌面，注意如果是官方链接下载的需要重新命名这个包为下面这个名字

  <img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/Screenshot from 2024-01-25 00-07-56.webp" alt="Screenshot from 2024-01-25 00-07-56" style="zoom: 50%;" />

  打开`opencv-4.5.5/modules/gapi/cmake/DownloadADE.cmake`

  <img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/Screenshot from 2024-01-25 00-00-23.webp" alt="Screenshot from 2024-01-25 00-00-23" style="zoom: 50%;" />

  将github那行的链接改为（保留引号）

  ```
  file:///home/你的用户名/Desktop/
  ```

  然后再次执行以下命令即可

  ```
  cmake ..
  ```
  
- opencv_contrib编译失败

  >Contributors: 胡彦祺

  WSL下使用make命令编译发生冲突

  <img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/1.webp" style="zoom: 33%;" />

  opencv_crontrib中的插件无法编译，检查$PATH发现存在大量Windows系统下共享的环境变量

  <img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/2.webp" style="zoom: 25%;" />

  关闭该功能，修改文件`/etc/wsl.conf`
  
  ```bash
  sudo vim /etc/wsl.conf
  ```
  
  ```ini
  # 不加载Windows中的PATH内容
  [interop]
  appendWindowsPath = false
  
  # 不自动挂载Windows系统所有磁盘分区
  [automount]
  enabled = false
  ```

  退出WSL，并重启该容器。*注：退出后必须重启，否则修改不会生效*
  
  ```bash
  wsl --list #查看WSL列表
  ```
  
  ```bash
  wsl --terminate Ubuntu-18.04 #改为你自己WSL的名字
  ```
  
  重新cmake、make编译即可
  
- ippicv库Assertation failed: DL_DESTINATION_DIR

  **报错信息：**

  <img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20250121210719167.webp" alt="image-20250121210719167" style="zoom: 50%;" />

  **解决方案：**

  参考前文ippicv库下载失败，在 `ippicv.cmake` 中修改目录的下一行补上（原文件已有，但可能在改目录时删多了）

  ```
  DESTINATION_DIR "${THE_ROOT}"
  ```

## 2.2机器人操作系统
###  2.2.1ROS 安装与配置


> Contributors: 刘明楷（milchstrasse565@github）

####  2.2.1.1 创建工作空间

终端输入

`mkdir -p ~/test_ws/src`

一般工作空间名为xxx_ws，ws也可写在前面，看个人习惯

#### 2.2.1.2 创建功能包

进入工作空间的src目录

`cd ~/test_ws/src`

创建功能包

`catkin_create_pkg hello_test std_msgs roscpp rospy`

#### 2.2.1.3创建ros节点程序

进入hello_test包的src目录写helloworld程序：

![helloworld](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/2023-08-14_16-59.webp)

```cpp
#include "ros/ros.h"

int main(int argc, char *argv[])
{
    //执行 ros 节点初始化
    ros::init(argc,argv,"hello");
    //创建 ros 节点句柄(非必须)
    ros::NodeHandle n;
    //控制台输出 hello world
    ROS_INFO("hello world!");

    return 0;
}
```

进入hello_test功能包目录下的CMakeLists.txt,一般只修改以下两项即可：

`add_executable(${PROJECT_NAME} src/hello.cpp)
target_link_libraries(${PROJECT_NAME}  ${catkin_LIBRARIES})`

add_executable生成的可执行文件名一般就是包名，即${PROJECT_NAME}，也就是hello_test ，如果有多个节点，则定义为其他名字

然后target_link_libraries，将可执行文件连接到库

最后进入到工作空间目录下编译即可：

`cd ~/test_ws`

 ` catkin_make`

每次编译后，都要配置好环境变量：

`source ~/test_ws/devel/setup.bash`

也可在将这句话加在.bashrc文件中，就不用每次配置环境变量了

然后在终端启动ros：

`roscore`

`rosrun hello_test hello_test `

rosrun后面跟包名+可执行文件名

![helloworld](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/p2.webp)

#### 2.2.1.4 创建发布者

创建新的节点test_pub.cpp：  

```cpp
/*
    需求: 实现基本的话题通信，一方发布数据，一方接收数据，
         实现的关键点:
         1.发送方
         2.接收方
         3.数据(此处为普通文本)

         PS: 二者需要设置相同的话题


    消息发布方:
        循环发布信息:HelloWorld 后缀数字编号

    实现流程:
        1.包含头文件 
        2.初始化 ROS 节点:命名(唯一)
        3.实例化 ROS 句柄
        4.实例化 发布者 对象
        5.组织被发布的数据，并编写逻辑发布数据

*/
// 1.包含头文件 
#include "ros/ros.h"
#include "std_msgs/String.h" //普通文本类型的消息
#include <sstream>

int main(int argc, char  *argv[])
{   
    //设置编码
    setlocale(LC_ALL,"");

    //2.初始化 ROS 节点:命名(唯一)
    // 参数1和参数2 后期为节点传值会使用
    // 参数3 是节点名称，是一个标识符，需要保证运行后，在 ROS 网络拓扑中唯一
    ros::init(argc,argv,"talker");
    //3.实例化 ROS 句柄
    ros::NodeHandle nh;//该类封装了 ROS 中的一些常用功能

    //4.实例化 发布者 对象
    //泛型: 发布的消息类型
    //参数1: 要发布到的话题
    //参数2: 队列中最大保存的消息数，超出此阀值时，先进的先销毁(时间早的先销毁)
    ros::Publisher pub = nh.advertise<std_msgs::String>("chatter",10);

    //5.组织被发布的数据，并编写逻辑发布数据
    //数据(动态组织)
    std_msgs::String msg;
    // msg.data = "你好啊！！！";
    std::string msg_front = "Hello 你好！"; //消息前缀
    int count = 0; //消息计数器

    //逻辑(一秒10次)
    ros::Rate loop_rate(10);

    //节点不死
    while (ros::ok())
    {
        //使用 stringstream 拼接字符串与编号
        std::stringstream ss;
        ss << msg_front << count;
        msg.data = ss.str();
        //发布消息
        pub.publish(msg);
        //加入调试，打印发送的消息
        ROS_INFO("发送的消息:%s",msg.data.c_str());

        //根据前面制定的发送贫频率自动休眠 休眠时间 = 1/频率；
        loop_rate.sleep();
        count++;//循环结束前，让 count 自增
    }
    return 0;
}
```

发送频率设置为10HZ

#### 2.2.1.5 创建订阅者

创建新的节点test_sub.cpp：  

```cpp
/*
    需求: 实现基本的话题通信，一方发布数据，一方接收数据，
         实现的关键点:
         1.发送方
         2.接收方
         3.数据(此处为普通文本)


    消息订阅方:
        订阅话题并打印接收到的消息

    实现流程:
        1.包含头文件 
        2.初始化 ROS 节点:命名(唯一)
        3.实例化 ROS 句柄
        4.实例化 订阅者 对象
        5.处理订阅的消息(回调函数)
        6.设置循环调用回调函数

*/
// 1.包含头文件 
#include "ros/ros.h"
#include "std_msgs/String.h"

void doMsg(const std_msgs::String::ConstPtr& msg_p){
    ROS_INFO("我听见:%s",msg_p->data.c_str());
    // ROS_INFO("我听见:%s",(*msg_p).data.c_str());
}
int main(int argc, char  *argv[])
{
    setlocale(LC_ALL,"");//
    //2.初始化 ROS 节点:命名(唯一)
    ros::init(argc,argv,"listener");
    //3.实例化 ROS 句柄
    ros::NodeHandle nh;

    //4.实例化 订阅者 对象
    ros::Subscriber sub = nh.subscribe<std_msgs::String>("chatter",10,doMsg);
    //5.处理订阅的消息(回调函数)
    ros::Rate loop_rate(5);//频率为５hz
    while (ros::ok())
    {
        ros::spinOnce();
        loop_rate.sleep(); //配合执行频率，sleep一段时间，然后进入下一个循环。
    }
    return 0;
}
```

回调函数名为doMsg，传入的参数为常量指针，因为有时候自定义消息类型数据量会比较大，另外注意这里配合spinOnce()实现接收频率的控制，如果是spin()函数，它就不会返回了，也不继续往后执行了，相当于它在自己的函数里面死循环了。

配置cmakelist文件：

在1.3的基础上添加：

```cmake
add_executable(${PROJECT_NAME} src/hello.cpp)
add_executable(test_pub
  src/test_pub.cpp
)
add_executable(test_sub
  src/test_sub.cpp
)
target_link_libraries(${PROJECT_NAME} ${catkin_LIBRARIES})
target_link_libraries(test_pub ${catkin_LIBRARIES})
target_link_libraries(test_sub ${catkin_LIBRARIES})
```

重新catkin_make编译后，source环境变量后在终端运行发送和接收节点

```
rosrun hello_test test_pub
rosrun hello_test test_sub
```

将分别看到：

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/p3.webp" alt="helloworld" style="zoom:60%;" />

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/p4.webp" alt="helloworld" style="zoom:60%;" />


#### 2.2.1.6 安装turtlebot3仿真需要其他的功能包 

```
sudo apt install ros-noetic-gazebo-ros-pkgs 
sudo apt install ros-noetic-gazebo-ros-control
sudo apt-get install ros-noetic-rviz
sudo apt-get install ros-noetic-map-server
sudo apt install ros-noetic-gmapping
sudo apt install ros-noetic-navigation
sudo apt install ros-noetic-move-base
```

#### 2.2.1.7 安装turtlebot3仿真和导航包

```
mkdir -p ~/catkin_turtlebot3/src
cd ~/catkin_turtlebot3/src
git clone https://github.com/ROBOTIS-GIT/turtlebot3.git
git clone https://github.com/ROBOTIS-GIT/turtlebot3_simulations.git
cd ..
catkin_make
```

添加模型申明，用以设定打开后模型的样子

`echo "export TURTLEBOT3_MODEL=waffle" >> ~/.bashrc`

对环境变量进行设置

`echo "source ~/catkin_turtlebot3/devel/setup.bash" >> ~/.bashrc`

#### 2.2.1.8 运行导航仿真例程

以上环境配置成功后，后续2.3和2.4的仿真例程运行可参考(https://blog.csdn.net/weixin_51015707/article/details/121522342)

 打开新终端，输入命令启动Gazabo，是通过roslaunch命令启动src文件夹中特定节点

`roslaunch turtlebot3_gazebo turtlebot3_world.launch`

打开新终端，启动SLAM进行建图，该命令是在可视化工具rviz中打开并进行SLAM

`roslaunch turtlebot3_slam turtlebot3_slam.launch slam_methods:=gmapping`

打开新终端，输入键盘控制的命令 (注意：该键盘控制是依靠按“W A D X”键增加速度，按S停止进行控制)

`roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch`

 打开新终端，输入命令保存地图

`rosrun map_server map_saver -f ~/map `

地图被保存至主目录中，包含2个文件

```
map.pgn：地图图片
map.yaml：地图信息
```

#### 2.2.1.9 仿真实现自主导航

 运动Gazabo 

`roslaunch turtlebot3_gazebo turtlebot3_world.launch`

读取地图并运行导航程序

`roslaunch turtlebot3_navigation turtlebot3_navigation.launch map_file:=$HOME/map.yaml`

点击上方红色箭头按钮：2D Nav Goal

 随后在地图上任意地点点击设定导航目标位置，小车便开始自主规划移动
## 2.3深度学习环境	
###  2.3.1显卡驱动与 CUDA/cuDNN
#### 2.3.1.1 Nvidia 驱动

**安装的是宿主机（Win11）的GPU驱动**

安装电脑GPU对应的Nvidia驱动（查询请在 此电脑-管理-设备管理器-显示适配器 查看）

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20231116135651422.webp" alt="image-20231116135651422" style="zoom:33%;" />

[Official Drivers | NVIDIA - https://www.nvidia.com/](https://www.nvidia.com/Download/index.aspx)

![image-20231031230258617](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20231031230258617.webp)

下载安装即可

#### 2.3.1.2CUDA Toolkit 安装

```
wget https://developer.download.nvidia.com/compute/cuda/repos/wsl-ubuntu/x86_64/cuda-wsl-ubuntu.pin
sudo mv cuda-wsl-ubuntu.pin /etc/apt/preferences.d/cuda-repository-pin-600
wget https://developer.download.nvidia.com/compute/cuda/12.1.0/local_installers/cuda-repo-wsl-ubuntu-12-1-local_12.1.0-1_amd64.deb
sudo dpkg -i cuda-repo-wsl-ubuntu-12-1-local_12.1.0-1_amd64.deb
sudo cp /var/cuda-repo-wsl-ubuntu-12-1-local/cuda-*-keyring.gpg /usr/share/keyrings/
sudo apt-get update
sudo apt-get -y install cuda
```

分别执行上述命令，直接等待其下载安装完成即可，若提示 `yes/no` 一律 `yes` ，对于各命令执行后的执行信息可以看后面

下述特殊情况处理对于整个环境安装过程均适用，不止对于CUDA Toolkit

留意其是否报错，若下载卡住请按 `ctrl+C` 终止下载并重新执行

**若终止下载，请先删除原有没下好的包**

若终止的是这步

```
wget https://developer.download.nvidia.com/compute/cuda/12.1.0/local_installers/cuda-repo-wsl-ubuntu-12-1-local_12.1.0-1_amd64.deb
```

则使用下列命令删除

```
rm ./cuda-repo-wsl-ubuntu-12-1-local_12.1.0-1_amd64.deb
```

其余同理

图例：

![image-20231101002600073](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20231101002600073.webp)

**命令执行信息**

```
wget https://developer.download.nvidia.com/compute/cuda/repos/wsl-ubuntu/x86_64/cuda-wsl-ubuntu.pin
```

![image-20231101002103546](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20231101002103546.webp)

-------------------------

```
sudo mv cuda-wsl-ubuntu.pin /etc/apt/preferences.d/cuda-repository-pin-600
```

无执行信息

-----------------------------------------------------

```
wget https://developer.download.nvidia.com/compute/cuda/12.1.0/local_installers/cuda-repo-wsl-ubuntu-12-1-local_12.1.0-1_amd64.deb
```

![image-20231101004635263](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20231101004635263.webp)

--------------------------------------

```
sudo dpkg -i cuda-repo-wsl-ubuntu-12-1-local_12.1.0-1_amd64.deb
```

![image-20231101004808455](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20231101004808455.webp)

-----------------------------

```
sudo cp /var/cuda-repo-wsl-ubuntu-12-1-local/cuda-*-keyring.gpg /usr/share/keyrings/
```

无执行信息

-----------------------

```
sudo apt-get update
```

前面Get/Hit的部分留意有没有Ign，如果有请在该命令执行完毕后重新执行一次命令，若依然存在Ign提示请尝试更换网络环境（一般挂了梯子就没这个问题，有的话换条线），后面所有涉及该类提示的同理

![image-20231101005156793](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20231101005156793.webp)

-----------------------------

```
sudo apt-get -y install cuda
```

内容过多，执行信息就不全部展示了（仅展示头尾），后面的一些执行信息同理

注意有无报错即可

![image-20231101012446989](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20231101012446989.webp)

![image-20231101012632938](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20231101012632938.webp)

--------------------------------

#### 2.3.1.3 CUDA安装

CUDA官方地址：[CUDA Toolkit Archive | NVIDIA Developer](https://developer.nvidia.com/cuda-toolkit-archive)

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20250204153127184.webp" alt="image-20250204153127184" style="zoom: 33%;" />

安装CUDA

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20250204153150013.webp" alt="image-20250204153150013" style="zoom:50%;" />

选择精简安装，安装完成后打开cmd检查安装情况

```
nvcc -V
```

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20250204153206530.webp" alt="image-20250204153206530" style="zoom:50%;" />

#### 2.3.1.4 cuDNN安装

cuDNN官方地址：[cuDNN Archive | NVIDIA Developer](https://developer.nvidia.com/rdp/cudnn-archive)

版本对应CUDA的安装版本

下载后，压缩包中三个文件夹解压到该目录下

```
C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v12.6
```

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20250204153217917.webp" alt="image-20250204153217917" style="zoom:50%;" />

验证cudnn是否安装成功

cmd进入目录（在该目录下资源管理器的目录框中输入cmd回车即可）

```
C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.3\extras\demo_suite
```

输入

```
deviceQuery.exe
```

检查安装

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20250204153237425.webp" alt="image-20250204153237425" style="zoom:50%;" />

### 2.3.2Miniconda&Anaconda
#### 2.3.2.1 Miniconda 安装

分别执行下列命令

```
curl https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -o Miniconda3-latest-Linux-x86_64.sh
```

![image-20231101011050897](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20231101011050897.webp)

--------------

```
bash Miniconda3-latest-Linux-x86_64.sh
```

![image-20231101011118050](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20231101011118050.webp)

需要按多次回车，直至

![image-20231101011318770](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20231101011318770.webp)

输入 `yes` 回车

![image-20231101011357841](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20231101011357841.webp)

再次回车确认conda安装位置

![image-20231101011457893](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20231101011457893.webp)

这一步同样输入 `yes` 回车即可

![image-20231101011530449](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20231101011530449.webp)

----------------

```
source ~/.bashrc
```

该命令执行后conda就开始运行了

![image-20231101011614973](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20231101011614973.webp)

---------------

#### 2.3.2.2 anaconda

官方地址（最新版）：[Download Now | Anaconda](https://www.anaconda.com/download/success)

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20250204153055921.webp" alt="image-20250204153055921" style="zoom:50%;" />

安装完成，开始菜单进入anaconda prompt

创建虚拟环境（建议版本3.9以上）

```
conda create -n  自己取的环境名字  python=版本号
```

激活环境

```
conda activate 环境名字
```

查看存在环境

```
conda env list
```

进入命令提示符cmd

查看CUDA版本

```
nvidia-smi
```

![image-20250204153112021](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20250204153112021.webp)

即12.6，安装对应CUDA工具包，版本小于等于上图版本号

### 2.3.3TensorFlow

> Contributors: 叶睿聪 (dgsyrc@github)

> 关于此步的注意事项：请先在windows端自行挂好梯子，否则部分包的下载可能会很慢或者直接失败（也可以尝试更换下载源）
>
> 关于梯子的安装（另附文档）

> 参考资料：
>
> [1] [TensorFlow GPU不可用，WSL2安装\_tensorflow wsl2\_坠星不坠的博客-CSDN博客 - https://blog.csdn.net/](https://blog.csdn.net/qq_40016005/article/details/130203903)





#### 2.3.3.1 Conda 环境配置

分别执行下列命令

```
conda create --name tf python=3.9
```

![image-20231101011743882](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20231101011743882.webp)

输入 `y` 回车

![image-20231101011829268](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20231101011829268.webp)

-------------------

```
conda activate tf
```

前面环境的提示信息变为了tf

![image-20231101012703132](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20231101012703132.webp)

-----------------

#### 2.3.3.2 GPU 配置

> Contributors: 叶睿聪 (dgsyrc@github)、杜雨蒙

如果没有梯子，下的很慢，可以尝试使用豆瓣源，将库名换进来即可

```
pip install （库名） -i http://pypi.douban.com/simple --trusted-host pypi.douban.com
```

分别执行下列命令

```
nvidia-smi
```

![image-20231101012822931](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20231101012822931.webp)

看下显卡型号与本机是否一致，本人电脑此处显示为 `NVIDIA GeForce RTX 3060 Laptop` 

--------------------

```
conda install -c conda-forge cudatoolkit=11.8.0
```

![image-20231101013136871](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20231101013136871.webp)![image-20231101013057366](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20231101013057366.webp)

输入 `y` 回车

![image-20231101013847296](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20231101013847296.webp)

--------------------

```
pip install nvidia-cudnn-cu11==8.6.0.163
```

![image-20231101014305276](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20231101014305276.webp)

若提示

![image-20231101014326659](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20231101014326659.webp)

可以直接跳过，不影响后面配置

-------------------

#### 2.3.3.3 环境变量配置

输入

```
mkdir -p $CONDA_PREFIX/etc/conda/activate.d
cd $CONDA_PREFIX/etc/conda/activate.d
gedit env_vars.sh
```

在弹出的编辑器中输入

```
CUDNN_PATH=$(dirname $(python -c "import nvidia.cudnn;print(nvidia.cudnn.__file__)"))
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$CONDA_PREFIX/lib/:$CUDNN_PATH/lib
export LD_LIBRARY_PATH=/usr/local/cuda-12.1/lib64/stubs/:/usr/local/cuda-12.1/lib64:/usr/local/cuda-12.1/cudnn/lib:$LD_LIBRARY_PATH
```

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20231102003627389.webp" alt="image-20231102003627389" style="zoom:50%;" />

**注意**，第三条指令的12.1为CUDA版本，请输入 `nvidia-smi` 查看本机的CUDA Version根据实际情况填写，不要直接复制粘贴

----------------------

#### 2.3.3.4Tensorflow 安装
如果没有梯子，下的很慢，可以尝试使用豆瓣源，将库名换进来即可

```
pip install （库名） -i http://pypi.douban.com/simple --trusted-host pypi.douban.com
```

执行下列命令

```
pip install --upgrade pip
```

![image-20231101014617429](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20231101014617429.webp)

---------------

```
pip install tensorflow==2.12.0
```

![image-20231101014828621](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20231101014828621.webp)

中间信息省略

![image-20231101014849642](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20231101014849642.webp)

------------------

#### 2.3.3.5 验证安装结果

**CPU 验证**

```
python3 -c "import tensorflow as tf; print(tf.reduce_sum(tf.random.normal([1000, 1000])))"
```

![image-20231101015018100](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20231101015018100.webp)

**GPU 验证**

```
python3 -c "import tensorflow as tf; print(tf.config.list_physical_devices('GPU'))"
```

![image-20231101015041196](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20231101015041196.webp)

若没有上述的信息，输入下面的配置到终端或者关闭终端重新打开再试（要进入tf环境）

```
CUDNN_PATH=$(dirname $(python -c "import nvidia.cudnn;print(nvidia.cudnn.__file__)"))
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$CONDA_PREFIX/lib/:$CUDNN_PATH/lib
```

重新执行GPU验证，若依然无法解决，请从前面GPU配置开始重做一次

**至此，环境配置完成**
### 2.3.4Pytorch
#### 2.3.4.1 安装PyTorch

官方地址：[PyTorch](https://pytorch.org/)

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20250204153247322.webp" alt="image-20250204153247322" style="zoom:50%;" />

将pip命令粘贴到anaconda的已配置好的虚拟环境中

安装完成后，输入以下指令检查是否安装成功

```
pip list
```

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20250204153300299.webp" alt="image-20250204153300299" style="zoom:50%;" />

打开vscode，进入工作目录

按下 `ctrl+shift+P` ,选择 `Python: Select Interpreter`

选中刚才创建的虚拟环境即可

运行以下代码检验PyTorch安装结果

```python
import torch
print(torch.__version__)

x = torch.rand(5, 3)

if torch.cuda.is_available():
    x = x.to("cuda")
    print(x)
else:
    print("CUDA is not available")
```

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20250204153322387.webp" alt="image-20250204153322387" style="zoom:50%;" />

#### 2.3.4.2 测试例：mnist手写数字识别

安装 `matplotlib` 包（在虚拟环境下安装）

```
pip install matplotlib
```

代码

```python
import torch
import torch.nn as nn
import torch.optim as optim
import torchvision
from torchvision import datasets, transforms
import torch.utils.data as data
import matplotlib.pyplot as plt

BATCH_SIZE = 128

# 设置设备
device = torch.device('cuda' if torch.cuda.is_available() else 'cpu')

# 数据加载和预处理
transform = transforms.Compose([
    transforms.ToTensor(),
    transforms.Normalize((0.5,), (0.5,))  # 将像素值归一化为 -1 到 1
])

# download and load the data
train_dataset = torchvision.datasets.MNIST(root='./mnist/', train=True, transform=transform, download=True)
test_dataset = torchvision.datasets.MNIST(root='./mnist/', train=False, transform=transform, download=False)

# encapsulate them into dataloader form
train_loader = data.DataLoader(train_dataset, batch_size=BATCH_SIZE, shuffle=True, drop_last=True)
test_loader = data.DataLoader(test_dataset, batch_size=BATCH_SIZE, shuffle=False, drop_last=True)

# 定义模型
class MNISTModel(nn.Module):
    def __init__(self):
        super(MNISTModel, self).__init__()
        self.model = nn.Sequential(
            nn.Flatten(),
            nn.Linear(28 * 28, 128),
            nn.ReLU(),
            nn.Linear(128, 64),
            nn.ReLU(),
            nn.Linear(64, 10)
        )
    
    def forward(self, x):
        return self.model(x)

# 实例化模型
model = MNISTModel().to(device)

# 定义损失函数和优化器
criterion = nn.CrossEntropyLoss()
optimizer = optim.Adam(model.parameters(), lr=0.001)

# 训练模型
def train_model(model, train_loader, criterion, optimizer, epochs=5):
    model.train()
    for epoch in range(epochs):
        total_loss = 0
        for images, labels in train_loader:
            images, labels = images.to(device), labels.to(device)
            
            # 前向传播
            outputs = model(images)
            loss = criterion(outputs, labels)
            
            # 反向传播和优化
            optimizer.zero_grad()
            loss.backward()
            optimizer.step()
            
            total_loss += loss.item()
        
        print(f"Epoch [{epoch+1}/{epochs}], Loss: {total_loss / len(train_loader):.4f}")

# 测试模型
def test_model(model, test_loader):
    model.eval()
    correct = 0
    total = 0
    with torch.no_grad():
        for images, labels in test_loader:
            images, labels = images.to(device), labels.to(device)
            outputs = model(images)
            _, predicted = torch.max(outputs, 1)
            total += labels.size(0)
            correct += (predicted == labels).sum().item()
    
    print(f"Accuracy: {100 * correct / total:.2f}%")

# 可视化识别结果
def show_predictions(model, test_loader, num_images=10):
    model.eval()
    images_shown = 0
    plt.figure(figsize=(12, 6))

    with torch.no_grad():
        for images, labels in test_loader:
            images, labels = images.to(device), labels.to(device)
            outputs = model(images)
            _, predicted = torch.max(outputs, 1)
            
            for i in range(images.size(0)):
                if images_shown >= num_images:
                    break
                
                image = images[i].cpu().numpy().squeeze()  # 转为二维图像
                label = labels[i].item()
                pred = predicted[i].item()
                
                plt.subplot(2, (num_images + 1) // 2, images_shown + 1)
                plt.imshow(image, cmap='gray')
                plt.title(f"True: {label}, Pred: {pred}", 
                          color="green" if label == pred else "red")
                plt.axis('off')
                images_shown += 1
            
            if images_shown >= num_images:
                break
    
    plt.tight_layout()
    plt.show()


# 执行训练和测试
train_model(model, train_loader, criterion, optimizer, epochs=5)
test_model(model, test_loader)

# 显示部分识别结果
show_predictions(model, test_loader, num_images=10)
```

运行以上代码

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20250204153521410.webp" alt="image-20250204153521410" style="zoom:50%;" />

![image-20250204153533872](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20250204153533872.webp)

若mnist数据集下载失败，`shift+右键` MNIST

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20250204153546080.webp" alt="image-20250204153546080" style="zoom:50%;" />

交换mirrors中两个链接的位置，交换后为

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20250204153556588.webp" alt="image-20250204153556588" style="zoom:50%;" />


<div STYLE="page-break-after: always;"></div>

### 2.3.5 onnxruntime

> Contributor: 叶睿聪 (dgsyrc@github)

git安装

```
sudo apt-get install git
```

下载源码（源码较大，请确保网络通畅，不建议使用梯子，可能会报错）

```
git clone --recursive https://github.com/Microsoft/onnxruntime
```

> **报错1**
>
> error: RPC failed; curl 16 Error in the HTTP2 framing layer
>
> 使用以下指令解决
>
> ```
> git config --global http.postBuffer 5242880000
> git config --global https.postBuffer 5242880000
> ```

安装必要环境

```
sudo apt-get install python-dev-is-python3
sudo apt-get install python3-numpy-dev
sudo apt-get install python3-packaging
sudo apt-get install python3-setuptools
sudo apt-get install python3-wheel
```

在 `onnxruntime` 文件夹下编译

```
sudo ./build.sh --config RelWithDebInfo --build_shared_lib --parallel --allow_running_as_root
```

此时可能会提示cmake版本过低，请根据 `2.10` 内容升级cmake

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20240222190207012.webp" alt="image-20240222190207012" style="zoom: 67%;" />

升级完成后重新执行上述命令即可成功编译（编译时间较长）

**可以用以下方式节省编译时间**

> 如加--skip_tests参数，或者：
>
> 在看到开始编译时（如下图）
>
> <img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20240222185820853.webp" alt="image-20240222185820853" style="zoom: 50%;" />
>
> 按下 `Ctrl+C` 终止编译
>
> 在 `onnxruntime/build/Linux/RelWithDebInfo` 目录下使用以下命令（nuc02替换为实际的用户名）
> 
> ```
>sudo cmake --build /home/nuc02/Desktop/onnxruntime/build/Linux/RelWithDebInfo --config RelWithDebInfo -j8
> ```
>
> 注意编译时是否有报错
>
> **报错1**
>
> <img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20240222191128295.webp" alt="image-20240222191128295" style="zoom: 67%;" />
>
> 缺少python环境
>
> 此时应输入以下指令安装环境
> 
> ```
>sudo apt-get install python-dev-is-python3
> ```
>
> **报错2**
>
> <img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20240222191704374.webp" alt="image-20240222191704374" style="zoom:67%;" />
>
> 缺少 `numpy` 库
>
> 输入以下指令安装环境
> 
> ```
>sudo apt-get install python3-numpy-dev
> ```
>
> 安装完成后再重新编译
>
> 使用加速编译最后需要回到onnxruntime目录下打开终端重新执行一次原本正常编译的指令检查
> 
> ```
>sudo ./build.sh --config RelWithDebInfo --build_shared_lib --parallel --allow_running_as_root
> ```
>

编译完成后

在 `onnxruntime/build/Linux/RelWithDebInfo` 或 `onnxruntime/build/Linux/Release` 下执行以下命令安装（上面加速的步骤可能会导致编译的文件无法转移至 `Release`  )

```
sudo make install
```


---




# 3.硬件

> Contributors: 叶睿聪 (dgsyrc@github)、唐锦梁

## 3.1计算平台

### 3.1.1 MiniPC（NUC 11  / NUC 12 / Piesia U5-125H）

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/08a5392ef1d3008638ac2a90dda4d21.webp" alt="08a5392ef1d3008638ac2a90dda4d21" style="zoom:45%;" />

#### 3.1.1.1 参数（以 NUC 11 为例）

| 属性                | 参数                 |
| ------------------- | -------------------- |
| CPU                 | Intel Core i5-1135G7 |
| GPU                 | 集显 Intel Xe        |
| RAM                 | 16G DDR4             |
| 硬盘                | PCIe4.0 NVMe 512G    |
| 无线网卡            | 有                   |
| USB 3.1 接口        | 3个                  |
| 雷电3接口（Type-C） | 2个                  |

### 3.1.2 各种接口/硬件位置

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/1d1e8cd56f0fd7f411cd46dc9643828.webp" alt="1d1e8cd56f0fd7f411cd46dc9643828" style="zoom:45%;" />

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/8cb5270681e05c9287e16a10d7f0e2a.webp" alt="8cb5270681e05c9287e16a10d7f0e2a" style="zoom:45%;" />

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/e782867fa49bf6f60d4899e76ac426f.webp" alt="e782867fa49bf6f60d4899e76ac426f" style="zoom:45%;" />

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/99019c63fdd45189d07e09be77347de.webp" alt="99019c63fdd45189d07e09be77347de" style="zoom:45%;" />

### 3.1.3外置MiniPC完整装机展示

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/b45c596c6c32b25fc59b4dd740a779a-1699090162011-17.webp" alt="b45c596c6c32b25fc59b4dd740a779a" style="zoom:45%;" />

<div STYLE="page-break-after: always;"></div>

## 3.2传感器

### 3.2.1 工业相机

#### 3.2.1.1 参数

制造商：迈德威视（MindVision）

型号：MV-SUA134GC-T

镜头：6mm焦距 F2.0光圈 1/1.8″靶面

#### 3.2.1.2 接口

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/0cdadb03833111a5741565dff2caa2e.webp" alt="0cdadb03833111a5741565dff2caa2e" style="zoom:45%;" />

### 3.2.2激光雷达

#### 3.2.2.1 参数（以 [Livox Mid-360](https://www.livoxtech.com/cn/mid-360) 为例）

| 参数                    | 说明                                   |
| ----------------------- | -------------------------------------- |
| **激光波长**            | 905 nm                                 |
| **人眼安全级别¹**       | Class 1 (IEC60825-1:2014) 人眼安全     |
| **量程 (@ 100 klx)**    | 40 m @ 10% 反射率<br>70 m @ 80% 反射率 |
| **近处盲区²**           | 0.1 m                                  |
| **FOV**                 | 水平 360°, 竖直 -7°~52°                |
| **测距随机误差³ (1σ)**  | ≤ 2 cm ⁴ (@ 10m)<br>≤ 3 cm ⁵ (@ 0.2m)  |
| **角度随机误差（1σ）**  | < 0.15º                                |
| **点云输出**            | 200,000 点/秒 (可配置第一回波)         |
| **点云帧率**            | 10 Hz (典型值)                         |
| **数据网口**            | 100 BASE-TX 以太网                     |
| **数据同步方式**        | IEEE 1588-2008 (PTPv2), GPS            |
| **抗串扰功能**          | 有                                     |
| **虚警率 (@ 100 klx)⁶** | < 0.01%                                |
| **IMU**                 | 内置 IMU 型号：ICM40609                |
| **工作环境温度⁷**       | -20℃ 至 55℃                            |
| **防护等级**            | IP67                                   |
| **功率⁸**               | 6.5 W                                  |
| **供电电压范围**        | 9 ~ 27 V DC                            |
| **尺寸**                | 65×65×60 mm                            |
| **重量**                | 265 g                                  |

#### 3.2.2.2官方文档与手册

[Downloads - Mid-360 激光雷达 - Livox](https://www.livoxtech.com/cn/mid-360/downloads) （包含 Mid-360 3D模型）

#### 3.2.2.3 配置

**硬件连接：**使用航插一分二线连接 Mid-360 与 MiniPC (RJ 45 网口)、XT30 供电

**IP 设置：**为确保通讯正常，需将 PC（MiniPC）与雷达置于同一网段。请手动修改 PC 的 IPv4 设置：

- **IP 地址：** 推荐设置为 `192.168.1.50`（或 `192.168.1.x` 网段下的其他空闲地址）。

- **子网掩码：** `255.255.255.0`

> 切勿将 PC 的 IP 地址设置为与雷达 IP（如 `192.168.1.153`）完全相同，否则会导致 **IP 冲突**，无法连接

#### 3.2.2.4SDK

***placeholder，update later by VaporTang***

***compile sdk、ip config、Livox Viewer2、pb_rm_nav environment config and more.***

### 3.2.3 USB-Camera

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/933e30e4a2df9666cdfb1555044c951.webp" alt="933e30e4a2df9666cdfb1555044c951" style="zoom:45%;" />

## 3.3电源与通信

### 3.3.1电源与电池管理

#### 3.3.1.1 电池架

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/f602d63510250d8df700e72b8e18b27.webp" alt="f602d63510250d8df700e72b8e18b27" style="zoom:45%;" />

电源接口采用黄色 **XT60 公头**，用于连接分电板侧的 XT60 母座。分电板侧面设有船型开关，开关状态取决于按下的一侧：

- 符号 |（竖线）：代表 <b>开启 (ON)</b>。

- 符号 O（圆圈）：代表 <b>关闭 (OFF)</b>。

> **操作建议：** 在与电控组进行联合调试时，**请勿直接切断整车电源**。正确的断电顺序为：先将 MiniPC 关机操作，待其完全关闭后，再断开电池电源（或关闭总开关）。

#### 3.3.1.2 电池

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/ee686cae28e617f72c13250f16f13dd.webp" alt="ee686cae28e617f72c13250f16f13dd" style="zoom:45%;" />

电池开关机：圆形按钮为开关，短按一次再长按（约2s）打开（关闭同理）

电量查看：关机状态下短按一次，LED 指示灯将显示当前电量

旧款电池型号为大疆 TB47/48 之智能飞行电池。新款电池型号为大疆 Matrice 4D 。另附哈尔滨工程大学同学对大疆智能电池的使用手册 [【分享帖】RM-大疆智能电池使用手册](https://bbs.robomaster.com/article/9289)

> 若发现**外壳鼓包**、**变形**或接口处有黑色烧蚀痕迹，**绝对禁止上电**。若发现电池温度烫手，应静置冷却；若充电时异常发热，请立即断电。

> 请不要低估这块电池内蕴含的能量，使用电池时请保持敬畏

### 3.3.2 分电板与变压器

#### 3.3.2.1 分电板

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/18699e1ea2ee028460c4f58b1745654.webp" alt="18699e1ea2ee028460c4f58b1745654" style="zoom:45%;" />

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/IMG_20251217_003506.webp" alt="18699e1ea2ee028460c4f58b1745654" style="zoom:45%;" />

图一所示分电板：黄色接头为XT60母头，分电板上有四个XT30公头，四个2Pin母头（白色方形），一个8Pin母头

图二所示分电板：RM标志上方为XT60母头，分电板上有七个XT30公头，一个2Pin CAN1(in)、一个4Pin CAN2(in)，六个2Pin CAN(out)


#### 3.3.2.2 DC-DC（24V-19V）降压模块

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/39ad3e5dfeabc94585db165b306ff72.webp" alt="39ad3e5dfeabc94585db165b306ff72" style="zoom:45%;" />

黄色接头为XT30母头（接分电板XT30公头），黑色为DC5525（接迷你PC电源）

### 3.3.3 USB转TTL与线缆

#### 3.3.3.1 USB-Camera

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/933e30e4a2df9666cdfb1555044c951.webp" alt="933e30e4a2df9666cdfb1555044c951" style="zoom:45%;" />

#### 3.3.3.2 RJ45 网线

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/2f466c0c655938d4d5c702e4f1fbab6.webp" alt="2f466c0c655938d4d5c702e4f1fbab6" style="zoom:45%;" />

#### 3.3.3.3 HDMI-HDMI

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/80f5ba37c6e61304e75df6b1f33f020.webp" alt="80f5ba37c6e61304e75df6b1f33f020" style="zoom:45%;" />

#### 3.3.3.4 USB to TTL

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/b90b6f486a7c52c8164661e95f615ac.webp" alt="b90b6f486a7c52c8164661e95f615ac" style="zoom:45%;" />

##### 3.3.3.4.1 接口

| 接口 | 用法          |
| ---- | ------------- |
| VCC  | 5V            |
| TXD  | 接另一端的RXD |
| RXD  | 接另一端的TXD |
| GND  | 接GND（地线） |

## 3.4 调试工具

### 3.4.1 手持装甲板调试模块

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/151b52ccd467ac9988ac2c418025d3c.webp" alt="151b52ccd467ac9988ac2c418025d3c" style="zoom:45%;" />

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/62aed7e72d7f0bdbc0e1b6a25fb92d0.webp" alt="62aed7e72d7f0bdbc0e1b6a25fb92d0" style="zoom:45%;" />

#### 3.4.1.1 参数

| 颜色 | 状态 |
| ---- | ---- |
| 红色 | 红方 |
| 蓝色 | 蓝方 |
| 紫色 | 离线 |

#### 3.4.1.2 拆解

装甲板的内部结构设计相对简单。四个角分别安装有压力传感器模块，两侧则分布着LED灯条。经过拆解分析可知，灯条部分的小板模块采用4Pin供电输入方式，灯条上的11块小板在电气上为并联结构。

通过逆向分析，每颗LED灯珠型号为SMD3528红蓝双色反极贴片式发光二极管。经比对，目前确认其规格与型号 **XL-3528SURUBC-FJ** 一致。

灯珠详细原理及规格图如下：

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/2025-12-17 10.25.57.webp" alt="b45c596c6c32b25fc59b4dd740a779a" style="zoom:40%;" />

##### 驱动方式：

**注意：绝对禁止直接将 LED 接在恒压电源上而不加电阻，这会导致 LED 烧毁**

每个灯珠内部实际包含两个极性相反、相互独立的LED芯片，分别发出红光和蓝光。因此，在驱动红光和蓝光时，可采用一块 3.7 V 软包电池，通过 5 V USB 充放电管理模块进行电能管理。从充放电管理模块输出 5 V 电压，并分为两路：

- 红光 LED 支路串联 **150 Ω** 限流电阻；
- 蓝光 LED 支路串联 **100 Ω** 限流电阻。

推荐从充放电管理模块获取 5 V 电源的原因在于，其输出电压较为稳定。然而，也可以考虑直接使用电池作为输出电源。在这种情况下：

- 红光 LED 支路应串联 **110 Ω** 限流电阻；
- 蓝光 LED 支路应串联 **55 Ω** 限流电阻。

### 3.4.2 裁判系统服务器

> Contributor: 邱万理

#### 3.4.2.1 前期准备

硬件：路由器（以小米路由器为例）、网线

软件：mysql(实际使用感觉非必要）、RoboMaster_Server(很多版本会闪退，自己多换几个赛季的试试，这里以2020年版本为例)

#### 3.4.2.2. 配置路由器

##### 3.4.2.2.1 连接方式

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20240121233742010.webp" alt="image-20240121233742010" style="zoom: 25%;" />

注意网线和电脑连接时接2号的LAN口，而不是接3号的WAN口

##### 3.4.2.2.2 开始配置

首先安装上述连接方式连接，Wifi连上Xiaomi并打开小米路由器设置网页http://miwifi.com/

第一次进入会提示设置密码，设置为12345678

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/1280X1280.webp" alt="1280X1280" style="zoom: 33%;" />

进入后到常用设置的WIFI设置中

SSID也就是名称(如图中的Xiaomi_C952)自己定义，但是最好是字母加数字

加密方式设置为WPA2，所以可以设置为强加密

密码必须设置为12345678

其余可以使用默认设置

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/1280X1280 (1).webp" alt="1280X1280 (1)" style="zoom: 33%;" />

进入常用设置的局域网设置中

将局域网IP地址设置为192.168.1.１

开启DHCP服务，并且设置开始IP为2(因为作为服务器主机的电脑将要设置为192.168.1.2,所以需要确保可以使用此IP)，结束IP则无严格要求

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/1280X1280 (2).webp" alt="1280X1280 (2)" style="zoom: 33%;" />

进入高级设置中的DHCP静态IP分配

添加绑定的设备，设备为作为服务器主机的电脑，IP设置为192.168.1.2

(如果配置不成功可以尝试拔掉网线重新连接)

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/3338de21-5add-4c64-9ff1-999e05808fe2.webp" alt="3338de21-5add-4c64-9ff1-999e05808fe2" style="zoom: 33%;" />

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/9df7eb37-1132-4aca-9c85-59224fb7aff7.webp" alt="9df7eb37-1132-4aca-9c85-59224fb7aff7" style="zoom: 33%;" />

如果还未成功，设置－＞网络和Internet－＞高级网络设置－＞更改适配器选项

进入WLAN的属性中，点击Internet协议版本４(TCP／IPv4)，打开其属性

改为使用下面的IP地址，并且设置IP地址为192.168.1.2，设置子网掩码为255.255.255.0

（注意关闭防火墙）

确定后关机重启

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/5a1f7495-3cd0-4e8c-b2b9-1ed5fa52c944.webp" alt="5a1f7495-3cd0-4e8c-b2b9-1ed5fa52c944" style="zoom: 33%;" />

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/d92ede77-0048-4ced-9dd9-6e4cda0100cb.webp" alt="d92ede77-0048-4ced-9dd9-6e4cda0100cb" style="zoom: 33%;" />

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/aff9fc9a-52ec-4d6f-b2db-fb696be2c7d7.webp" alt="aff9fc9a-52ec-4d6f-b2db-fb696be2c7d7" style="zoom: 33%;" />

#### 3.4.2.3 软件安装

##### 3.4.2.3.1 MySQL

①进入官网下载MySQL，版本可以选择低一些，mysql-8.0.31-win64.zip

https://dev.mysql.com/downloads/mysql/

②解压缩zip文件，放置在一个简短并且没有中文的文件路径下（如放在`D:\mysql-8.0.31-winx64`)

然后配置一下环境变量(不清楚在哪里自己在设置中搜索环境变量）

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/8b8a6f13-5ea5-4c86-82a0-9aa06042969b.webp" alt="8b8a6f13-5ea5-4c86-82a0-9aa06042969b" style="zoom:33%;" />

系统属性界面右下角的环境变量中，在系统变量找到`Path`

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/d62674cc-d8f4-4162-8eba-e4f5387e6952.webp" alt="d62674cc-d8f4-4162-8eba-e4f5387e6952" style="zoom:33%;" />

点击编辑，新建一个环境变量名称为刚刚安装的路径再加上`/bin`

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/ea802741-5189-4b5e-987c-7cbb7f54c150.webp" alt="ea802741-5189-4b5e-987c-7cbb7f54c150" style="zoom:33%;" />

③在刚刚的bin文件的同一位置新建一个`data`文件夹和一个`mysql.ini`文件

![5ba868a2-8e93-4690-898e-6b2b0ec24a51](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/5ba868a2-8e93-4690-898e-6b2b0ec24a51.webp)

`mysql.ini`文件先创建一个`.txt`文件，加入以下内容后再修改后缀名变更为`.ini`文件

其中第12行和第15行请自行修改为自己安装的实际位置

```ini
[mysql]

# 设置mysql客户端默认字符集
default-character-set=utf8 

[mysqld]

#设置3306端口
port = 3306 

# 设置mysql的安装目录
basedir=F:\mysql\mysql-5.7.24-winx64\mysql-5.7.24-winx64

# 设置mysql数据库的数据的存放目录
datadir=F:\mysql\mysql-5.7.24-winx64\mysql-5.7.24-winx64\data

# 允许最大连接数
max_connections=200

# 服务端使用的字符集默认为8比特编码的latin1字符集
character-set-server=utf8

# 创建新表时将使用的默认存储引擎
default-storage-engine=INNODB
```

④打开cmd(Win+R）

首先安装mysql，执行以下命令行

```
mysqld install
```

安装成功后启动mysql服务

```
net start mysql
```

服务器启动后，需要输入密码登录（第一次登录没有密码，直接回车即可）

```
mysqladmin -u root -p password
```

修改密码，u后面为用户名（一般都设置为root）,password建议设置为123456或者12345678,忘记密码没有找回方式

```
mysqladmin -u root -p password
```

⑤设置中搜索服务

找到MySQL，设置其为手动启动，避免每次开机自启

后续启动可以cmd输入

```
net start mysql
```

或者再次打开服务界面，右键点击启动也可

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/72d90abc-034e-403d-9564-fb58e2498213.webp" alt="72d90abc-034e-403d-9564-fb58e2498213" style="zoom:33%;" />

##### 3.4.2.3.2 大疆官方服务器

前往RoboMaster官网下载服务器客户端(RoboMaster产品->裁判系统->软件产品）

各赛季的版本不一定都出来了，并且有些版本的会闪退，自己根据电脑情况多尝试几个版本即可，这里使用的是2020年的服务器客户端

https://www.robomaster.com/zh-CN/products/components/detail/2518

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/0e5d6040-a014-4b9c-9e91-c7eb86a37b42.webp" alt="0e5d6040-a014-4b9c-9e91-c7eb86a37b42" style="zoom:33%;" />

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/2ff831b2-b26c-4607-88e7-0e59d7789b9b.webp" alt="2ff831b2-b26c-4607-88e7-0e59d7789b9b" style="zoom:33%;" />

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/1e4ce0be-abaf-4f0e-8df7-9b74f38bee76.webp" alt="1e4ce0be-abaf-4f0e-8df7-9b74f38bee76" style="zoom:33%;" />

2020赛季的服务器RoboMaster Server里面文件如下图，打开RMServerStart.exe文件，直接点击最下面的StartAll，进入后Play能够打开以下界面即可。

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/2befb81e-b765-4d33-8ed4-525afc8437be.webp" alt="2befb81e-b765-4d33-8ed4-525afc8437be" style="zoom:33%;" />

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/c343c74f-d9b2-489b-b209-b0ec09972dbc.webp" alt="c343c74f-d9b2-489b-b209-b0ec09972dbc" style="zoom: 50%;" />

最终效果图

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/62fe3d5b-ddda-40f3-ac83-a2506ec3d61b.webp" alt="62fe3d5b-ddda-40f3-ac83-a2506ec3d61b" style="zoom:33%;" />

#### 3.4.2.4 完整流程

当以上3步都能大致实现之后，可以开始使用我们的服务器

①首先连接将路由器与电脑连接，电脑Wifi选择Xiaomi(后面字母和数字为用户自己编号，各不相同就不列举)

并且将电脑的IP地址设置为192.168.1.2,子网掩码设置为255.255.255.0(这一步如果静态DHCP分配设置成功不一定需要，如果配置失败请尝试自己手动修改配置）

②打开MySQL服务

③启动RoboMaster Server软件

④机器人主控模块中点击Wifi设置，扫描

扫描到路由器的Wifi后，长按确定（连接并且记忆该Wifi）

连接成功后可以通过主页面左上角感叹号是否消失判断

#### 3.4.2.5 可能遇到的问题

- 主控右上角显示连接上Wifi，但是左上角感叹号仍存在？

仅仅是连接上了路由器的Wifi，但是主机并未正确设置为要求的192.168.1.2

目前找到的许多教程中都是在网络设置中设置IP地址和子网掩码来实现，但是实际使用发现并没有设置为预想的IP。

这时请尝试在MiWifi路由器设置网页中，在高级设置中的DHCP静态IP分配里重新为作为服务器主机的电脑分配IP：192.168.1.2

- 路由器不能正常打开配置页面？

电脑注意是使用LAN口，而不是使用WAN口（如果不确定，请都试一遍）

- 下载的服务器客户端打开后闪退？

不清楚是官方问题还是自己电脑问题，遇到此问题只能自己多找几个赛季的软件都试试，一般前期只是用于测试功率等简单功能，不一定需要使用最新赛季的服务器软件

# 4 视觉知识

## 4.1 OpenCV 开发基础

OpenCV环境配置：见2.1 OpenCV

VSCode插件配置：见1.3.1 OpenCV环境配置

### 4.1.1 CMake 配置与 VSCode 运行

#### 4.1.1.1 cmake配置

查看cmake版本

```
cmake --version
```

`CMakeLists.txt` 文件配置

```cmake
# cmake编译所需最低版本（新项目则设为当前cmake版本）
cmake_minimum_required(VERSION 3.10.0)
# 项目名称demo
project(demo)
# 指定C++版本
set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED True)
# 导入OpenCV库
find_package(OpenCV REQUIRED)
include_directories(${OpenCV_INCLUDE_DIRS})
link_libraries(${OpenCV_LIBS})
# 将项目目录作为项目include包含的目录（加入到列表EXTRA_INCLUDES）
list(APPEND EXTRA_INCLUDES ${PROJECT_SOURCE_DIR})
# 将列表EXTRA_INCLUDES的所有目录作为项目include包含的目录
include_directories(${EXTRA_INCLUDES})
# 指定使用demo.cpp生成可执行文件
add_executable(Demo demo.cpp)
# 链接相关的libraries
target_link_libraries(Demo
    PUBLIC
    ${OpenCV_LIBS}
    PRIVATE
)

# 编译文件连接优化开关
set_target_properties(Demo PROPERTIES INTERPROCEDURAL_OPTIMIZATION True)
# 设置可执行文件输出目录
set(EXECUTABLE_OUTPUT_PATH "${PROJECT_BINARY_DIR}/bin")
# 设置编译的库文件输出目录
set(LIBRARY_OUTPUT_PATH "${PROJECT_BINARY_DIR}/lib")
```

#### 4.1.1.2 VSCode配置

新建一个项目文件夹**（不要中文！写任何代码都不要在任何中文路径下编译，文件名也不要使用中文）**

示例代码如下：

`demo.cpp`

```c++
#include<demo.h>

using namespace cv;

int main()
{
    Mat a;
    return 0;
}
```

`demo.h`

```c++
#pragma once
#include <opencv2/core.hpp>
#include <opencv2/highgui.hpp>
#include <opencv2/opencv.hpp>
```

第一次输入opencv相关头文件时，由于C++扩展没有引入opencv库的目录，会弹出报错，按以下方式解决

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20241116232941180.webp" alt="image-20241116232941180" style="zoom: 50%;" />

选择

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20241116232948457.webp" alt="image-20241116232948457" style="zoom:50%;" />

选择第一个即可

在项目文件夹目录下，打开终端

输入以下指令创建build文件夹

```
mkdir build
```

进入 `build` 文件夹分别输入以下两个指令编译

```
cmake ..
make -j8
```

编译完成后，输入以下指令执行程序

```
./bin/Demo
```

若无报错，则配置完成

### 4.1.2  图像与视频处理基础

#### 4.1.2.1 图像的读写

**imread()和imwrite()**

```c++
Mat img; // 新建一个Mat类型变量
img = imread("读取路径"); // 读取指定路径的图像
imwrite("保存路径", img);  // 保存图像到指定路径
```

imread可在路径后加参数，缺省值为1

下面的语句等价

```c++
img = imread("读取路径", IMREAD_COLOR);
img = imread("读取路径", 1);
img = imread("读取路径");
```

imread()参数的功能

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20241117124316116.webp" alt="image-20241117124316116" style="zoom:33%;" />

#### 4.1.2.2 图像的展示

**imshow()**

```c++
imshow("窗口名字", img); // 在指定窗口中显示图像
waitKey(0); // 必须要在imshow后加，或者在程序结束前加，否则运行到程序结束窗口会自动关闭
```

**destroyWindow()和destroyAllWindows()**

```c++
destroyWindow("窗口名字"); // 关闭指定窗口
destroyAllWindows(); // 关闭所有窗口
```

**namedWindow()**

```c++
namedWindow("窗口名字", 窗口类型); // 窗口类型值缺省为1
```

窗口类型有以下两种常用类型

| 窗口类型        | 作用                                               | 值  |
| --------------- | -------------------------------------------------- | --- |
| WINDOW_NORMAL   | 可通过代码改变窗口大小，图像默认等比例缩放         | 0   |
| WINDOW_AUTOSIZE | 不可通过代码改变窗口大小，窗口大小根据图像大小确定 | 1   |

其它功能用的较少，这里暂不给出

**resizeWindow()**

```c++
resizeWindow("窗口名字", Size(cols, rows)); // cols控制横向大小，即列数，rows控制纵向大小，即行数，单位均为像素，值只能是正整数
```

#### 4.1.2.3 视频的读取

**VideoCapture**

读取视频文件

```c++
VideoCapture cap("视频路径"); // 声明一个cap变量，使用指定视频初始化
Mat img;
if (!cap.isOpened())
{
    std::cerr << "Error: Could not open video" << std::endl;
    return -1;
}
double fps = cap.get(CAP_PROP_FPS); // 获取帧率
while (true)
{
	cap.read(img); // 按顺序将视频的每一帧存入img
    if (!img.empty())
    {
        imshow("窗口名称", img);
        waitKey(1000 / fps); // 播放时的帧率与原视频一致
    }
    else
    {
    	break;
    }
}
```

读取相机

```c++
VideoCapture cap = VideoCapture(0); // 调用相机，默认第一个相机编号是0
Mat img;
if (!cap.isOpened()) // 是否成功打开相机
{
    std::cerr << "Error: Could not open camera" << std::endl; // 输出错误信息
    return -1;
}
double fps = cap.get(CAP_PROP_FPS); // 获取帧率
while (true)
{
	cap.read(img); // 按顺序将视频的每一帧存入img
	if (!img.empty()) // 视频没读完，此时img不为空
	{
    	imshow("窗口名字", img);
        waitKey(1000 / fps); // 播放时的帧率与相机一致 或者用固定值30
    }
    else
    {
        break;
    }
}
```

get() 方法的详细功能

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20241117125136873.webp" alt="image-20241117125136873" style="zoom:33%;" />

录制视频

```c++
VideoCapture cap = VideoCapture(0); // 调用相机，默认第一个相机编号是0
Mat img;
if (!cap.isOpened()) // 是否成功打开相机
{
    std::cerr << "Error: Could not open camera" << std::endl; // 输出错误信息
    return -1;
}
double fps = cap.get(CAP_PROP_FPS); // 获取帧率
VideoWriter writer; // 保存视频用VideoWriter类
int codec = VideoWriter::fourcc('M', 'J', 'P', 'G'); // 编码格式
std::string filename = "save.avi"; // 视频名称
bool isWriterOpen = false;
bool isColor; // 是否为彩色视频
while (true)
{
	cap.read(img); // 按顺序将视频的每一帧存入img
	if (!img.empty()) // 视频没读完，此时img不为空
	{
        if (!isWriterOpen)
        {
            isColor = (img.type() == CV_8UC3); // 彩色视频判断
            writer.open(filename, codec, fps, img.size(), isColor); // 初始化录制
            isWriterOpen = true;
        }
        writer.write(img); // 将画面存入录制器
    	imshow("窗口名字", img);
        waitKey(1000 / fps); // 播放时的帧率与相机一致 或者用固定值30
    }
    else
    {
        break;
    }
}
```

保存的文件在终端当前打开的目录，不是可执行文件所在目录

#### 4.1.2.3 Mat的初始化与数据类型

Mat类型本质是个矩阵

**初始化**

```c++
Mat img(200, 400, CV_8UC3, Scalar(0, 0, 0)); // 创建一个高200px 宽400px 的8位3通道彩色图像 初始化值为0 Scalar(0, 0, 0)可以缺省
```

其中，图像的宽度高度初始化可以使用Size(cols, rows)

以下方式与前面等价

```c++
Mat img(Size(400, 200), CV_8UC3, Scalar(0, 0, 0)); // 注意宽高位置相反
```

此外，可以使用已有矩阵构造

```c++
Mat img1;
Mat img2(img1);
Mat img3=img1;
```

但这种方式实际上只复制了img1的矩阵头，因此两者的修改会相互影响（理解为起了个别名，类比函数的传址调用）

如果希望复制一个一样的矩阵，应使用clone()或copyTo()

```
Mat img1;
Mat img2=img1.clone();
Mat img3=img1.copyTo();
```

**数据类型**

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20241117111755022.webp" alt="image-20241117111755022" style="zoom:33%;" />

若定义单通道图像，可不写 `C1` ，3通道图像写 `C3`。例如 `CV_8UC3` 表示数据为8位无符号整数的三通道图像

最多只有四个通道

**颜色定义**

Scalar()定义颜色，可以理解为一个向量，有几个通道向量就有几个分量

其中，三通道彩色图像中，OpenCV的存储顺序是BGR而不是RGB，例如 `Scalar(20,40,60)` 中20为蓝色通道分量，40为绿色通道分量，60为红色通道分量

#### 4.1.2.4 Mat的赋值

构造时的赋值参考前面的初始化，通过Scalar()可以给每个元素赋相同初值

循环赋值

```c++
// 单通道
Mat img1(128, 128, CV_8U);
for (int i = 0; i < img1.cols; i++)
{
	for (int j = 0; j < img1.rows; j++)
    {
    	img1.at<uchar>(i, j) = i + j; // uchar对应8U（8位无符号整数）
    }
}
// 多通道
Mat img2(128, 128, CV_8UC3);
for (int i = 0; i < img2.cols; i++)
{
    for (int j = 0; j < img2.rows; j++)
    {
        Vec3b elem = img2.at<Vec3b>(i, j); // Vec3b 是3通道uchar向量
        elem.val[0] = i + j;
        elem.val[1] = (i > j) ? 127 + i : 127 + j;
        elem.val[2] = 255 - (i + j);
        img2.at<Vec3b>(i, j) = elem;
    }
}
```

对于多通道矩阵，建议先用向量读出，修改向量后再写回，给出三通道下的对应关系

| 图像类型 | 单个数值类型 | 向量类型 | 单个数值长度（位） |
| -------- | ------------ | -------- | ------------------ |
| CV_8UC3  | uchar        | Vec3b    | 8                  |
| CV_16SC3 | short        | Vec3s    | 16                 |
| CV_16UC3 | ushort       | Vec3w    | 16                 |
| CV_32SC3 | int          | Vec3i    | 32                 |
| CV_32FC3 | float        | Vec3f    | 32                 |
| CV_64FC3 | double       | Vec3d    | 64                 |

读取同理

#### 4.1.2.5 Mat的运算

Mat支持加减乘除四则运算，加法减法都是矩阵对应元素相加减

两个矩阵相乘是矩阵乘法，要求必须A的列数等于B的行数

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20241117121741373.webp" alt="image-20241117121741373" style="zoom:33%;" />

矩阵乘常数是对应每个元素乘该常数，如果要两个矩阵的对应元素相乘作为结果矩阵的值，则

```c++
m = a.mul(b); // a,b,m均为Mat矩阵，大小相同
```

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20241117122150712.webp" alt="image-20241117122150712" style="zoom:33%;" />

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20241117122158378.webp" alt="image-20241117122158378" style="zoom:33%;" />

矩阵点乘

```c++
m = a.dot(b); // a,b均为Mat矩阵，大小相同，m为一个数
```

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20241117122133982.webp" alt="image-20241117122133982" style="zoom:33%;" />

矩阵除法不论是除常数还是除矩阵均为被除矩阵对应位置元素除除数（若为常数，则除常数，为矩阵则除对应位置的元素值）

#### 4.1.2.6 Mat的属性

参考下表

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20241117122626148.webp" alt="image-20241117122626148" style="zoom:33%;" />

访问方式示例：

```c++
Mat img;
int i = img.cols;
int j = img.rows;
int ch = img.channels();
```

#### 4.1.2.7 颜色模型转换

转换Mat的颜色模型使用cvtColor()函数

```
cvtColor(src, dst, code, dstCn = 0); // 依次为原始图像、目标图像、颜色转换标志、目标图像通道数（缺省值为0，与src一致）
```

颜色转换标志

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20241117132501256.webp" alt="image-20241117132501256" style="zoom:33%;" />

示例：

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20241117133535765.webp" alt="image-20241117133535765" style="zoom:33%;" />

从左到右从上到下分别是BGR、GRAY、YUV、HSV、Lab

#### 4.1.2.8 常见错误

- 路径正确，视频无法读取且无法保存录制的视频

  **原因：**ffmpeg未安装

  **解决方案：** 检查以下依赖是否安装

  ```
  sudo apt-get install libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev
  ```

  安装完成后重新编译安装 OpenCV 即可

  注意在执行 `cmake ..` 后终端的输出信息，如 `ffmpeg` 部分提示为 `YES` 即可继续编译安装

  <img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20240322134426787.webp" alt="image-20240322134426787" style="zoom: 33%;" />

- 视频可读取，但相机录制视频无法保存

  <img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20240322135316813.webp" alt="image-20240322135316813" style="zoom:33%;" />

  **原因：** fps, frameSize 参数错误（一般表现为0）

  **解决方案：** fps与frameSize手动设置即可，不使用 `cv::videoCapture` 的成员函数读取

## 4.2 深度学习理论

### 4.2.1 yolov8

> Contributor: 程英杰

#### 4.2.1.1 目标检测与语义分割的区别

##### 4.2.1.1.1 语义分割的目标

语义分割的任务是对输入的图像进行逐像素的分类，标记出像素级别的物体。

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/图像逐像素的分类-1708443883528-1.webp" alt="图像逐像素的分类" style="zoom:33%;" />

如上图，图1中把猫、天空、树、草地进行了逐像素的分类；图2中把牛、天空、树、草地进行了逐像素的分类。

##### 4.2.1.1.2 目标检测的目标

目标检测的任务是对输入的图像进行物体检测，标注物体在图像上的位置，以及该位置上物体属于哪个分类。

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/模型位置标注和做出分类-1708443893034-3.webp" alt="模型位置标注和做出分类" style="zoom:33%;" />

如上图，模型把图中的人、狗、马分别进行了位置标注，并且也给出了对应的分类类别。

##### 4.2.1.2.3 小结

蕴含信息都包含分类信息和位置信息。

但是语义分割所标记的物体是像素级别的颗粒度的，而目标检测标记的物体是其外切框。

#### 4.2.1.2 训练

##### 4.2.1.2.1 安装

Pytorch环境安装省略

```bash
pip install ultralytics
```

##### 4.2.1.2.2 准备数据集

Yolo团队为模型设计了专用数据集格式"YOLO"，要训练yolov8，必须确认数据集为yolo格式。

yolo直接采用txt文件保存模型的labels标签，如下图，每一行都代表着该图像中的一个标签GT

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/yolo数据集格式-1708443900929-5.webp" alt="yolo数据集格式" style="zoom: 50%;" />

目前大部分数据集的保存都是以voc格式，如果你拿到了voc格式的数据集，需要进行转换。

相关链接：[https://blog.csdn.net/kuabiku/article/details/132088402]()

本次使用西南大学 已标注数据集链接： https://pan.baidu.com/s/1oMtdgmBN5xQZTbv2bSLtog?pwd=z3gc

该数据集的标签数据已经是yolo格式

**处理数据集并调整配置文件**

模型训练配置文件(config.yaml)示例：

```yaml
path: data_xn # dataset root dir
train: images/train # ./data_xn/images/train
val: images/test # ./data_xn/images/test
test: # test images (optional)

# Classes
names:
  0: person
  1: bicycle
  2: car
# ...
```

其中  `path`  是数据集相对于`config.yaml`所在目录的路径，也可以填写绝对路径

`train`和`val`分别是训练集和评估集，该字段中的路径将会与`path`中的路径相拼接

`names`是模型分类数据的信息，从`0`开始，分类数量应不小于训练数据中所标注的类别标签的数量。`西南大学 已标注数据集`的最大类别为35，因此`names`中的分类应该从`0`-`34`.

`西南大学 已标注数据集`数据集文件夹`data_xn`的存放格式应该更改为：

```bash
data_xn
    ├─images
    │  ├─test
    │  └─train
    ├─labels
    │  ├─test
    │  └─train
```

其中，`images`下每个子目录中直接存放了图片；`labels`下每个子目录中存放了对应的标注数据(txt文件)

> *训练前，ultralytics会自动读取这写文件夹下的每张图片和标注，并生成* **缓存** *以便于下次训练直接复用。因此如果对数据集进行了改动，再次训练时应将缓存文件* `data_xn/labels/train.cache`和`data_xn/labels/test.cache` *删去以应用更改*

##### 4.2.1.2.3 训练

**准备预训练模型**

对于不同任务，Yolov8准备了不同的预训练模型，具有不同的输出格式。目标检测是Yolov8的主任务，因此所有模型均可使用。

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/yolov8预训练模型-1708443909325-7.webp" alt="yolov8预训练模型" style="zoom:33%;" />

下载地址：[Releases · ultralytics/assets · GitHub](https://github.com/ultralytics/assets/releases) 提供了ultralytics库提供的所有预训练模型的下载，此处下载最小的默认模型

下载命令：

```bash
wget https://github.com/ultralytics/assets/releases/download/v8.1.0/yolov8n.pt
```

**编写训练代码**

在项目根目录创建`datasets`，并将准备好的数据集`data_xn`剪切进去。

将下载好的预训练模型文件`yolov8n.pt`放入项目根目录

在项目根目录创建`train.py`:

```python
from ultralytics import YOLO
if __name__ == "__main__":

    # 加载预训练数据集
    model = YOLO('yolov8n.pt')
    
    # 按照配置文件的定义开始训练，训练3个epochs
    results = model.train(data='config.yaml', epochs=3,lr0=1E-2)

    # model.val()
    # train方法在训练完成后自动对模型进行评估， 因此不需要调用 model.val()

    #导出模型为ONNX格式
    model.export(format='onnx', dynamic=True)
```

> 由于Windows下处理数据集需要创建多个workers，因此，需要将接口调用写在__main__下以防止`Freeze_support Error`
>
> <img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/Freeze_support_Error提示报错-1708443920532-9.webp" alt="Freeze_support_Error提示报错" style="zoom: 50%;" />

**然后运行train.py就可以开始训练了**

**查看训练结果**

训练结果保存在项目根目录`runs`文件夹下，`runs/detect`存放了`目标检测`任务的训练模型和评估结果

关于评估指标的解释，见：[https://blog.csdn.net/java1314777/article/details/134154676]()

模型(权重)文件存放在相应模型文件夹中的`weights`文件夹

#### 4.2.1.3 使用ONNX调用

[生成ONNX文件参考资料](https://docs.ultralytics.com/modes/export/)

ONNX Runtime提供了跨平台调用模型的统一接口

生成并使用ONNX文件的步骤如下:

1. 生成ONNX文件:
   从下面的文件结构开始,通过上面的步骤已经得到了训练过程当中综合准确率最好的模型`best.pt`和模型最后的训练结果`last.pt`
2. <img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/weights权重文件展示图-1708443930529-11.webp" alt="weights权重文件展示图" style="zoom:33%;" />

然后是在pycharm控制台打开之前下载了 `ultralytics`的anaconda环境，然后在控制台输入下面的指令

~~~bash
yolo export model=runs/detect/train6/weights/best.pt format=onnx  int8=true simplify=true dynamic=true
~~~

在`best.pt`所在的文件夹当中得到了`best.onnx`。

>参数解释
>前两个命令 yolo export 指的是使用yolo的相关命令 做导出任务
>model后面跟的参数是训练得到的模型文件路径
>format后面是模型导出的格式 [(yolo官网上模型导出的格式)](https://docs.ultralytics.com/zh/modes/export/#arguments)
>后面的参数也是官网上的相关介绍
>
><img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/yolo官网文件导出参数的介绍-1708443946517-13.webp" alt="yolo官网文件导出参数的介绍" style="zoom: 40%;" />
>
>这里我使用了 int8 simplify dynamic 用来简化模型加快计算速度


当然根据官网也可以使用python将模型文件导出 下面是相关的代码

~~~python
from ultralytics import YOLO
# Load a model
model = YOLO('runs/detect/train6/weights/best.pt')  # load a custom trained model
# Export the model
model.export(format='onnx', int8=True, dynamic=True, simplify=True)
~~~


2. 编写python调用ONNX文件
   [调用ONNX文件参考资料](https://zhuanlan.zhihu.com/p/670622368)

首先先import这些库文件

~~~python 
import onnxruntime as ort
import cv2
import numpy as np
~~~

然后加载ONNX文件

~~~python
import onnxruntime as ort
session = ort.InferenceSession("yolov8m-seg.onnx", providers=["CPUExecutionProvider"]) # 使用CPU加载计算模型
~~~

后续的代码和相关的解释都在注释当中写的比较详细,这里就直接贴代码了

~~~python
# %%
import onnxruntime as ort
import cv2
import numpy as np

# 这个函数是将图片数据转换为模型输入格式 (预处理函数)
def prepare_input(bgr_image, width, height):
    image = cv2.cvtColor(bgr_image, cv2.COLOR_BGR2RGB)  # 将图片从BGR格式转换为RGB格式
    # cv2.imshow(bgr_image)
    image = cv2.resize(image, (width, height)).astype(np.float32) # 将图片resize到模型输入尺寸640x640
    image = image / 255.0  #归一化
    image = np.transpose(image, (2, 0, 1)) # 将图像数据的通道顺序由HWC调整为CHW
    input_tensor = np.expand_dims(image, axis=0) # 扩展数据维度，将数据的维度调整为NCHW
    #axis=0表示在第0维增加一个维度
    #经过预处理后，输入数据input_tensor的维度变为[1, 3, 640, 640]，与模型的输入尺寸一致。
    return input_tensor
# 计算两个方框之间的IOU值的大小 计算方式是 两个方框交集面积/并集面积
# 参考资料 http://t.csdnimg.cn/zTN73
def iou(rec_1,rec_2):
        '''
        rec_1:左上角(rec_1[0],rec_1[1])    右下角：(rec_1[2],rec_1[3])
        rec_2:左上角(rec_2[0],rec_2[1])    右下角：(rec_2[2],rec_2[3])
        （rec_1）
        1--------1
        1   1----1------1
        1---1----1      1
            1           1
            1-----------1 （rec_2）
        '''
        s_rec1=(rec_1[2]-rec_1[0])*(rec_1[3]-rec_1[1])   #第一个bbox面积 = 长×宽
        s_rec2=(rec_2[2]-rec_2[0])*(rec_2[3]-rec_2[1])   #第二个bbox面积 = 长×宽
        sum_s=s_rec1+s_rec2                              #总面积
        left=max(rec_1[0],rec_2[0])                      #交集左上角顶点横坐标
        right=min(rec_1[2],rec_2[2])                     #交集右下角顶点横坐标
        bottom=max(rec_1[1],rec_2[1])                    #交集左上角顶点纵坐标
        top=min(rec_1[3],rec_2[3])                       #交集右下角顶点纵坐标
        if left >= right or top <= bottom:               #不存在交集的情况
            return 0
        else:
            inter=(right-left)*(top-bottom)              #求交集面积
            iou=(inter/(sum_s-inter))*1.0                #计算IOU
            return iou
session = ort.InferenceSession(
     "D:\\ProgramFiles\\ultralytics-main\\runs\\detect\\train6\\weights\\best.onnx", # 模型文件路径 
     providers=["CPUExecutionProvider"])  # 模型路径 还有使用CPU计算
video = cv2.VideoCapture("D:\\opencv_image\\video_zhuangjiaban.mp4") # 读取视频文件
# %%
# 1. 把OpenCV读取的BGR格式的图片转换为RGB格式；
# 2. 把图片resize到模型输入尺寸640x640；
# 3. 对像素值除以255做归一化操作；
# 4. 把图像数据的通道顺序由HWC调整为CHW；
# 5. 扩展数据维度，将数据的维度调整为NCHW。
while True:
    model_width = 640
    model_height = 640
    ret, image = video.read()
    if(ret==False):
       continue      
    image_height, image_width, _ = image.shape
    input_tensor = prepare_input(image, model_width, model_height)
    outputs = session.run(None, {session.get_inputs()[0].name: input_tensor})
    # %%
    #squeeze函数是用于删除shape中为1的维度，对output0做transpose操作是为了方便后续操作
    # print(outputs[0].shape)
    output0 = np.squeeze(outputs[0]).transpose()
    # print("outputs[0].shape shape:", outputs[0].shape)
    # print("output0 shape:", output0.shape)
    # %%
    boxes = output0
    # print(boxes.shape) # 输出结果是 (8400,40)
    # 这里的boxes是一个二维数组，第一维是目标框的数量，第二维是目标框的属性，包括目标框的坐标和类别概率等信息。
    # 咱们细说第二维的属性：前4个元素是目标框的坐标信息，分别是目标框的中心坐标(x,y)和宽高(w,h)，后36个元素是目标框的类别概率信息，每个类别的概率占4个元素。
    # 所以[8400,40] 就代表着 8400个目标框，每个目标框有40个属性
    # boxes shape: (8400, 84)
    # masks shape: (8400, 32)
    # %%
    objects = []
    for row in boxes:
        prob = row[4:40].max()
        if prob < 0.2:
            continue
        class_id = row[4:40].argmax()
        label = class_id
        xc, yc, w, h = row[:4]
        # // 把x1, y1, x2, y2的坐标恢复到原始图像坐标
        x1 = (xc - w / 2) / model_width * image_width
        y1 = (yc - h / 2) / model_height * image_height
        x2 = (xc + w / 2) / model_width * image_width
        y2 = (yc + h / 2) / model_height * image_height
        # // 获取实例分割mask
        # mask = get_mask(row[84:25684], (x1, y1, x2, y2), image_width, image_height)
        # // 从mask中提取轮廓
        # polygon = get_polygon(mask, x1, y1)
        objects.append([x1, y1, x2, y2, label, prob])
    # %%
    objects.sort(key=lambda x: x[5], reverse=True)
    # %%
    # objects.sort(key=lambda x: x[5], reverse=True)
    # // NMS
    results = []
    while len(objects) > 0:
        print(objects[0])
        results.append(objects[0]) # 我们想要与第一个框进行比较 所以不能让第一个框和自己作比较
        # 如果 iou过大(超过了0.5)的话 就删除这个object 保留iou小的object
        objects = [object for object in objects if iou([object[0],object[1],object[2],object[3]], 
                                                    [objects[0][0],objects[0][1],objects[0][2],objects[0][3]]) < 0.5]
        # 这里就是将 objects中和第一个object的iou大于0.5的object删除掉
    # %%
    # 定义矩形的左上角和右下角坐标
    # 设置矩形颜色为红色（BGR格式）
    color = (0, 0, 255)
    thickness = 1 # 若想要填充矩形则将此值改为-1或者大于等于0的数字
    # 在图像上绘制矩形
    for result in results:
        print(result)
        start_point = (int(result[0]), int(result[1]))
        end_point = (int(result[2]), int(result[3]))
        cv2.rectangle(image, start_point, end_point, color, thickness)
    cv2.imshow('window name',image)
    if cv2.waitKey(10) & 0xFF == ord('q'):
            break
cv2.destroyAllWindows()
~~~


<div STYLE="page-break-after: always;"></div>

## 4.3ROS与导航（SLAM）

### 4.3.1 ROS与导航

#### 4.3.1.1 实操学习

> Contributor: 刘明楷（milchstrasse565@github）

- 屏蔽导航包里的速度发布语句

- 自己的ros程序替代导航包控制机器人

  - 订阅里程计/odom，发布速度/cmd_vel，让机器人直线运动1m停止（熟悉订阅/发布/坐标系/消息格式）

- 取消订阅里程计话题获取定位，改为监听map坐标系与机器人本体坐标系的TF获取定位（熟悉TF与TF树）

- 以上一步的定位为基础，进一步订阅导航包生成的局部轨迹，以任意方式实现机器人沿着轨迹进行运动，如使用恒定线速度，用PID的P控制角速度（进一步夯实）

- 慢慢逐步替换开源导航包的规划、控制、定位、建图等所有或某个模块、再进行优化

- 其他必学
  - 各种消息格式
  
  - rviz可视化调试 
  
  - TF坐标变换
  
  - TF监听与广播
  
  - launch文件与参数配置
  
  - cmake编译规则设置
  
  - rosbag数据记录、回放
  


### 4.3.2Catkin 编译系统详解

> Contributor: 洪佳

> 参考资料：
>
> [11] [ROS从入门到精通系列（五）catkin详解与catkin_make编译-CSDN博客 - https://blog.csdn.net/](https://blog.csdn.net/hhaowang/article/details/101691986)

一定要搞明白`make/makefile/catkin_make/cmake/Cmakelist`的关系,本质是链接文件去生成可执行文件

系统学习大家还是要自己学，主要给大家提供思路，学习大纲还有遇到的一些问题的解决方法，少走弯路

#### 4.3.2.1 catkin编译系统

对于源代码包，我们只有编译才能在系统上运行。而Linux下的编译器有``gcc、g++``，随着源文件的增加，直接用``gcc/g++``命令的方式显得效率低下，人们开始用`Makefile`来进行编译。然而随着工程体量的增大，`Makefile`也不能满足需求，于是便出现了`Cmake`工具。`CMake`是对make工具的生成器，是更高层的工具，它简化了编译构建过程，能够管理大型项目，具有良好的扩展性。对于ROS这样大体量的平台来说，就采用的是`CMake`，并且ROS对`CMake`进行了扩展，于是便有了Catkin编译系统。

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20240129164912808.webp" alt="image-20240129164912808" style="zoom:33%;" />

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20240129164930341.webp" alt="image-20240129164930341" style="zoom:33%;" />

其实早期是`rosbuild`，目前还支持使用，但是`ros`的核心软件包都已经被转换为Catkin

#### 4.3.2.2 catkin_make 结构和特点

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20240129165146937.webp" alt="image-20240129165146937" style="zoom:33%;" />

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20240129165635113.webp" alt="image-20240129165635113" style="zoom:33%;" />

#### 4.3.2.3 catkin_make编译流程

- 建立工作空间

  <img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20240129165753173.webp" alt="image-20240129165753173" style="zoom:50%;" />

- 编译

  <img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20240129165829990.webp" alt="image-20240129165829990" style="zoom:50%;" />

source用来配置环境，不然`roslaunch`找不到对应的包

#### 4.3.2.4 catkin_make文件系统

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hoYW93YW5n,size_16,color_FFFFFF,t_70.webp" alt="img" style="zoom: 33%;" />

#### 4.3.2.5 package

package也是ROS源代码存放的地方，任何ROS的代码无论是C++还是Python都要放到package中，这样才能正常的编译和运行。

一个package可以编译出来多个目标文件（ROS可执行程序、动态静态库、头文件等等）。

**package结构**

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hoYW93YW5n,size_16,color_FFFFFF,t_70-1706519610932-6.webp" alt="img" style="zoom:33%;" />

**package指令**

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hoYW93YW5n,size_16,color_FFFFFF,t_70-1706519738476-12.webp" alt="img" style="zoom:33%;" />

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20240129171704680.webp" alt="image-20240129171704680" style="zoom:33%;" />

#### 4.3.2.6 常见问题

点进源代码包后，把`build/devel`两个包删了，在当前路径下进入终端

```
catkin_make
```

如果没有error，记得source配置环境，编译成功‘

以下是一些问题现象和解决方案

**问题①**

```
CMake Error at /opt/ros/noetic/share/catkin/cmake/catkinConfig.cmake:83 (find_package): Could not find a package configuration file provided by "catkin_virtualenv" with any of the following names:

    catkin_virtualenvConfig.cmake
    catkin_virtualenv-config.cmake
  Invoking "make cmake_check_build_system" failed
```

这是由于缺少包导致的

**解决方案：**

在终端输入：

```
sudo apt-get install ros-noetic-catkin-virtualenv
```

注意：

1.error里面”_”下划线在解决代码里面用“-”分割符号

2.Ubuntu20.04是noetic        Ubuntu18.04是melodic

3.有可能缺少好几个包，catkin_make多编译几次再下载几次包

**问题②**

在下载的时候

```
E:无法定位到软件包
```

原因很多，网络连接问题、`ros`软件源、apt源过期等问题

**解决方案：**

查一遍list,这个很麻烦需要耐心，我没试过谨慎试

换源镜像

http://t.csdnimg.cn/o9dce

### 4.3.3 运动学与传感器融合

#### 4.3.3.1 麦轮底盘运动学解算

> Contributor: 洪佳

> 参考资料：
>
> [10] [ROS机器人学习——麦克纳姆轮运动学解算-CSDN博客 - https://blog.csdn.net/](https://blog.csdn.net/oXiaoLingTong/article/details/120198677)

##### 4.3.3.1.1 麦轮概述

RM战车所用的轮子均为麦克纳姆轮，这种轮子安装方式与普通轮子无异，可安装于平行轴上，但是麦克纳姆轮可以实现全向移动，即前后运动、水平移动、绕中心自转。正因为以上优点，许多工业上的全向移动平台都会应用这种轮子。缺点也有，就是不耐磨，需要定期更换。

（全向轮与麦克纳姆轮的共同点在于他们都由两大部分组成：轮毂和辊子（roller）。轮毂是整个轮子的主体支架，辊子则是安装在轮毂上的鼓状物。全向轮的轮毂轴与辊子转轴相互垂直，而麦克纳姆轮的轮毂轴与辊子转轴呈 45° 角。理论上，这个夹角可以是任意值，根据不同的夹角可以制作出不同的轮子，但最常用的还是这两种。）

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20240126010416033.webp" alt="image-20240126010416033" style="zoom:33%;" />

##### 4.3.3.1.2 麦轮安装

同轴安装，分为左旋和右旋两种

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20240126015014818.webp" alt="image-20240126015014818" style="zoom:33%;" />

安装方式如下图，分别为：**X-正方形（X-square）、X-长方形（X-rectangle）、O-正方形（O-square）、O-长方形（O-rectangle）**

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20240126015110765.webp" alt="image-20240126015110765" style="zoom:33%;" />

- X-正方形：轮子转动产生的力矩会经过同一个点，所以 yaw 轴无法主动旋转，也无法主动保持 yaw 轴的角度。
- X-长方形：轮子转动可以产生 yaw 轴转动力矩，但转动力矩的力臂一般会比较短。
- O-正方形：四个轮子位于正方形的四个顶点，平移和旋转都没有任何问题。
- O-长方形：轮子转动可以产生 yaw 轴转动力矩，而且转动力矩的力臂也比较长。是最常见的安装方式。

##### 4.3.3.1.3 运动学模型

**基础知识**

坐标系统

使用右手定义,对于ROS机器人，如果以它为坐标系的原点，那么

|  轴   | 方位  |
| :---: | :---: |
|  x轴  | 前方  |
|  y轴  | 左方  |
|  z轴  | 上方  |

旋转运动

使用右手定义：

围绕 z轴正旋转 是 逆时针旋转

测量单位

ROS使用公制 ：

线速度：m/s

角速度：rad/s

底盘运动学解算

以下以**O-长方型**安装方式进行解算

- 底盘中心

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20240126013124388.webp" alt="image-20240126013124388" style="zoom:33%;" />

- 麦轮轴心（取右上角麦轮即一号轮子分析）

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20240126013249796.webp" alt="image-20240126013249796" style="zoom:33%;" />



逆运动学解算

逆运动学模型（inverse kinematic model）得到的公式可以根据底盘的运动状态解算出四个轮子的速度

①轮子轴心速度

![image-20240126013514833](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20240126013514833.webp)

②辊子方向的速度分量v1∥

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20240126013654586.webp" alt="image-20240126013654586" style="zoom:33%;" />

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20240126013846204.webp" alt="image-20240126013846204" style="zoom: 67%;" />

③轮子转速

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20240126014229717.webp" alt="image-20240126014229717" style="zoom:33%;" />

![image-20240126014243401](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20240126014243401.webp)

④整合得出底盘四个轮子转速，即底盘运动学模型

![image-20240126014625107](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20240126014625107.webp)



正运动学解算

正运动学模型（forward kinematic model）让我们可以通过四个轮子的速度，计算出底盘的运动状态。可以直接根据逆运动学模型中的三个方程解出来。

转换为底盘坐标系下对时间求积分即为里程计变化量

##### 4.3.3.1.4 代码实现

代码参考：http://t.csdnimg.cn/ldXqr

#### 4.3.3.2 IMU与里程计融合

> Contributor: 洪佳

> 参考资料：
>
> [5] [IMU和里程计融合_轮式里程计和imu融合-CSDN博客 - https://blog.csdn.net/](https://blog.csdn.net/baimei4833953/article/details/80768762)
>
> [6] [什么是IMU？-CSDN博客 - https://blog.csdn.net/](https://blog.csdn.net/su_fei_ma_su/article/details/125947605)
>
> [7] [一文了解IMU原理、误差模型、标定、惯性传感器选型以及IMU产品调研(含IMU、AHRS、VRU和INS区别)_imu寄存器值计算重力-CSDN博客 - https://blog.csdn.net/](https://blog.csdn.net/QLeelq/article/details/112985306?csdn_share_tail={"type"%3A"blog"%2C"rType"%3A"article"%2C"rId"%3A"112985306"%2C"source"%3A"Hong_J_0826"}&fromshare=blogdetail)

##### 4.3.3.2.1 概述

实际使用小车的过程中，光有麦轮的里程计计算是不够的，因为实际使用过程中经常会出现轮子打滑和数据出现累计误差的情况，所以我们可以从使用IMU和里程计融合的角度来对系统“升级4.3.1.2.1 IMU

**简述**

IMU 一般指6轴传感器，内部包含了3轴陀螺仪和3轴加速度计，3轴就是表示 XYZ 平面下的3个坐标轴。

3轴陀螺仪测量的是每个轴上面的角速度，精度一般为 °/s ，也就是按照这个趋势旋转，每秒钟能走过的度数。

3轴加速度计测量的是每个轴所受的重力加速度，比如传感器水平放置水平地面时，理论上只受到z轴负向的重力加速度，大小为 9.8 m/s<sup>2</sup>

**原理**

详细了解：

[一文了解IMU原理、误差模型、标定、惯性传感器选型以及IMU产品调研(含IMU、AHRS、VRU和INS区别)_imu寄存器值计算重力-CSDN博客 - https://blog.csdn.net/](https://blog.csdn.net/QLeelq/article/details/112985306?csdn_share_tail={"type"%3A"blog"%2C"rType"%3A"article"%2C"rId"%3A"112985306"%2C"source"%3A"Hong_J_0826"}&fromshare=blogdetail)

##### 4.2.3.2.2 IMU数据获取

**数据接口**

数据接口，通过配置可以输出原始 `ros_imu topic`

还有更多方法

**滤波**

ROS提供的相关包`imu_tools`进行滤波

可以看到`complementary_filter_gain_node`会订阅该`topic`，即该`topic`作为输入滤波得到最终数据(发布`/imu/data` `topic` 类型同样为`sensor_msgs/Imu`)

##### 4.2.3.2.3 融合方法

**直接融合**

从`imu`得到的数据为一个相对角度(主要使用`yaw`，`roll`和`pitch` 后面不会使用到)，使用该角度来替代由编码器计算得到的角度。
这个方法较为简单，出现打滑时候因`yaw`不会受到影响，即使你抬起机器人转动一定的角度，得到的里程也能正确反映出来

**卡尔曼滤波**

- 概述

官方卡尔曼滤波的包[`robot_pose_ekf`](http://wiki.ros.org/robot_pose_ekf)，`robot_pose_ekf`开启扩展卡尔曼滤波器生成机器人姿态，支持

`odom`（编码器）

`imu_data`（IMU）

`vo`（视觉里程计）

还可以支持 [GPS](http://wiki.ros.org/robot_pose_ekf/Tutorials/AddingGpsSensor)

- 配置

可以在 `robot_pose_ekf` 包目录中找到 EKF 节点的默认启动文件。启动文件包含许多可配置的参数：

`freq`：过滤器的更新和发布频率。请注意，随着时间的推移，更高的频率会为您提供更多的机器人姿势，但不会提高每个估计的机器人姿势的准确性。

`sensor_timeout`：当传感器停止向过滤器发送信息时，过滤器应该等待多长时间才能在没有该传感器的情况下继续工作。

`odom_used`、`imu_used vo_used`：启用或禁用输入。

可以在启动文件中修改配置，如下所示：

![image-20231129141340231](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20231129141340231.webp)

**运行**

创建程序包：

```
 $ rosdep install robot_pose_ekf
 $ roscd robot_pose_ekf
 $ rosmake
```

**Run** the `robot pose ekf`

```
 $ roslaunch robot_pose_ekf.launch
```

**相关节点**

①robot_pose_ekf

`robot_pose_ekf`实现了一个扩展的卡尔曼滤波器，用于确定机器人姿态。

②Subscribed Topics

`Odom` （[`nav_msgs/里程计`](http://docs.ros.org/en/api/nav_msgs/html/msg/Odometry.html))

- **2D** pose（由车轮里程计使用）：2D 姿势包含机器人在地平面上的位置和方向以及该姿势的协方差。发送此 2D 姿势的消息实际上表示 3D 姿势，但 z、滚动和俯仰被简单地忽略。

`imu_data` （[`sensor_msgs/Imu`](http://docs.ros.org/en/api/sensor_msgs/html/msg/Imu.html))

- 3D orientation（由 IMU 使用）：**3D 方向**提供有关机器人底架相对于世界参考系的滚动角、俯仰角和偏航角的信息。横滚角和俯仰角被解释为绝对角度（因为 IMU 传感器具有重力参考），偏航角被解释为相对角度。协方差矩阵指定了方向测量的不确定度。`robot_pose_ekf` 在仅接收有关此主题的消息时不会启动;它还需要有关“VO”或“Odom”主题的消息。

`vo`（[`nav_msgs/`里程计](http://docs.ros.org/en/api/nav_msgs/html/msg/Odometry.html))

- **3D** pose（由视觉里程计使用）：3D pose表示机器人的完整位置和方向以及该pose的协方差。当传感器仅测量 3D 姿势的一部分时（例如，车轮里程计仅测量 2D 姿势），只需在未实际测量的 3D pose部分上指定较大的协方差即可。

`robot_pose_ekf`节点不要求所有三个传感器源始终可用。每个源都给出了pose估计值和协方差。这些源以不同的速率和不同的延迟运行。源可以随时间推移出现和消失，节点将自动检测并使用可用的传感器。若要添加自己的传感器输入，请查看[添加 GPS 传感器教程](http://wiki.ros.org/robot_pose_ekf/Tutorials/AddingGpsSensor)

③Published Topics

`robot_pose_ekf/odom_combined` （[geometry_msgs/PoseWithCovarianceStamped](http://docs.ros.org/en/api/geometry_msgs/html/msg/PoseWithCovarianceStamped.html))

- 过滤器的输出（估计的 3Drobot pose）

④提供的` tf` 转换

```
odom_combined`→`base_footprint
```

**工作原理**

Poes解释

所有向滤波器节点发送信息的传感器源都可以有自己的世界参考系，并且每个*世界*参考系都可以随时间任意漂移。因此，不同传感器发送的**absolute Pose**无法相互比较。该节点使用每个传感器的**relative pose differences**来更新扩展的卡尔曼滤波器。

协方差解释(Covariance interpretation)

随着机器人四处移动，其在世界参考中pose的不确定性越来越大。随着时间的流逝，协方差将无限增长。因此，发布pose本身的协方差是没有用的，相反，传感器源会发布协方差如何随时间变化，即速度上的协方差。*请注意，使用对世界的观察（例如，测量到已知墙壁的距离）将减少机器人姿势的不确定性;然而，这是定位，而不是里程计。*

Timing

想象一下，机器人姿势过滤器上次更新的时间是t_0。在*到达每个*传感器的至少一次测量值且时间戳晚于 t_0 之前，节点不会更新机器人姿势过滤器。例如，当在时间戳t_1 > t_0的 `odom` 主题和时间戳t_2 > t_1 > t_0的 `imu_data` 主题上收到消息时，过滤器现在将更新到有关所有传感器的信息可用的最新时间，在本例中为时间t_1。直接给出t_1处的 `odom` 位姿，通过对 t_1 和 t_0 之间的 `imu` 位姿进行线性插值得到 t_2 处的 `imu `位姿。机器人姿势过滤器使用` odom `和` imu `的相对姿势进行更新，介于 t_0 和 t_1 之间。

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/robot_pose_ekfaction=AttachFile&do=get&target=robot_pose_ekf.webp" alt="robot_pose_ekf.webp" style="zoom:50%;" />

上图显示了PR2机器人从给定的初始位置（绿点）开始，驱动并返回初始位置时的实验结果。完美的里程计 x-y 图应显示精确的闭环。蓝线表示车轮里程计的输入，蓝点表示估计的结束位置。红线表示`robot_pose_ekf`的输出，它结合了车轮里程计和`imu`的信息，红点是估计的结束位置。

包裹状态

①稳定性

这个包的代码库已经过很好的测试，并且已经稳定了很长时间。然而，随着消息类型的演变，ROS API 一直在变化。在未来的版本中，ROS API 可能会再次更改为简化的单主题界面（请参阅下面的路线图）。

②路线图

- 该滤波器目前设计用于我们在 PR2 机器人上使用的三个传感器信号（车轮里程计、`imu` 和 `vo`）。我们计划使这个包更加通用：未来的版本将能够监听“n”个传感器源，所有源都发布（[`nav_msgs/`里程计](http://docs.ros.org/en/api/nav_msgs/html/msg/Odometry.html)）消息。每个源都将在里程计消息中设置 3D 姿势的协方差，以指定它实际测量的 3D 姿势的哪一部分。
- 我们想将速度添加到扩展卡尔曼滤波器的状态中。


### 4.3.4 SLAM四种算法建图对比

> Contributor: 洪佳

> 参考资料：
>
> [12] [2D激光slam四种算法建图效果对比_slam建图算法-CSDN博客 - https://blog.csdn.net/](https://blog.csdn.net/m0_73791170/article/details/127339058?csdn_share_tail={"type"%3A"blog"%2C"rType"%3A"article"%2C"rId"%3A"127339058"%2C"source"%3A"Hong_J_0826"}&fromshare=blogdetail)

SLAM——同步定位与建图（Simultaneous Localization and Mapping，SLAM）是在上世纪80年代被提出的，起初发展的算法皆采用激光雷达作为定位与建图的工具，随着稀疏性问题的解决，相机也被引入SLAM领域，如今SLAM技术在向多传感器融合的方向发展，激光雷达、深度相机、IMU惯导等正成为SLAM技术的常见解决方案。

####  4.3.4.1 Gmapping

一种用于建立**二维地图的概率算法**，它基于激光雷达数据和机器人的运动信息，通过**蒙特卡洛方法**进行粒子滤波定位和地图构建。

这个部分写得详细一点，因为我们比赛建图使用的就是`Gmapping`算法,从理论到实际

（后面三种实际操作暂无，为了统一，参考构建地图都来自一篇文章）

**概述**

其算法框架是基于RBPF粒子滤波算法，先进行定位再进行建图

RBPF：http://t.csdnimg.cn/h4PfS，对于建图而言，简单来说就是通过算法迭代，在粒子群中选出最优粒子，使用激光雷达数据和所关联的历史轨迹来绘制地图。其**定位和建图是分离的**，每个粒子都携带它们自身的地图（不适合大场地建图，但是我们比赛场地面积用`Gmapping`建图问题不大）。

|           RBPF问题           |            `Gmapping`改进            |
| :--------------------------: | :----------------------------------: |
| 粒子多——计算量大、内存消耗大 | 改进提议分布（考虑里程计、观测信息） |
|      频繁执行——粒子退化      |       选择性重采样（设定阈值）       |

**优缺点**

- 优点

`Gmapping`可以实时构建室内地图，在构建小场景地图所需的计算量较小且精度较高。相比Hector SLAM对激光雷达频率要求低、鲁棒性高.

而相比Cartographer在构建小场景地图时，`Gmapping`不需要太多的粒子并且没有回环检测因此计算量小于Cartographer而精度并没有差太多。`Gmapping`有效利用了车轮里程计信息，这也是`Gmapping`对激光雷达频率要求低的原因：里程计可以提供机器人的位姿先验。而Hector和Cartographer的设计初衷不是为了解决平面移动机器人定位和建图，Hector主要用于救灾等地面不平坦的情况，因此无法使用里程计。而Cartographer是用于手持激光雷达完成SLAM过程，也就没有里程计可以用。

- 缺点

随着场景增大所需的粒子增加，因为每个粒子都携带一幅地图，因此在构建大地图时所需内存和计算量都会增加。因此不适合构建大场景地图。

没有**回环检测**(http://t.csdnimg.cn/8Vh3X)，因此在回环闭合时可能会造成地图错位，虽然增加粒子数目可以使地图闭合但是以增加计算量和内存为代价。所以不能像Cartographer那样构建大的地图。

`Gmapping`和Cartographer一个是基于滤波框架SLAM另一个是基于优化框架的SLAM，两种算法都涉及到时间复杂度和空间复杂度的权衡。`Gmapping`牺牲空间复杂度保证时间复杂度，这就造成`mapping`不适合构建大场景地图。翻看Cartographer算法，优化相当于地图中只用一个粒子，因此存储空间比较`Gmapping`会小很多倍，但计算量大;优化图需要复杂的矩阵运算。

**建图实操**

1)软硬件准备：

`rplidar`及其驱动；navigation和`gmapping`等package;`tf`变换关系

很多开源的相关功能包，这是SLAM导航核心技术的内容，随便查

编译功能包，使系统识别ROS工作空间

下载`gmapping`·是为了能够在自己的小车运行，因此必须按照小车的实际情`gmapping`算法中的**参数进行配置**

```
touch gmapping_robot.launch
```

2)笔记本和主控板连接

这个步骤看情况，直接接显示屏或者看小屏也可以

可以`ssh`远程操控，使用`Nomachine`等工具

3)操作指令

```
roslaunch turn_on_什么机器人 mapping.launch  //建图命令
rviz     //可视化
roslaunch  机器人 keyboard_teleop.launch   //控制命令
roslaunch turn_on_什么机器人 map_saver.launch   //保存地图
```

**注意：在单独启动rviz时，需要先启动master节点：`roscore`，然后另启一终端运行：`rosrun rviz rviz`。但是对.launch文件，运行之后，若master节点没有启动会自动去启动它，因此在第二步运行rviz时，master节点已经被启动了，无需再次运行`roscore`。
每次打开rviz都要重新配置很麻烦，可以使用ctrl+s命令保存当前配置，保存到路径`opt/ros/melodic/share/rviz/default.rviz`，若提示无法写入该文件，则是当前文件权限为“only read”，启动一个终端，输入并运行命令`sudo chmod 777 /opt/ros/melodic/share/rviz/default.rviz`，然后再此尝试`ctrl+s`保存即可成功**

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20240127172132705.webp" alt="image-20240127172132705" style="zoom:67%;" />

4)灰度地图和代价地图

建图得到**灰度地图**，其数值范围为[-1,100]，其中“-1”代表未知区域，基本是`rviz`的背景色，“0“代表自由区域，为白色，”100“代表完全占用，为黑色，实际上在建图时只有”-1“、”0“、”100“三种情况，因为建图过程中雷达探测到了障碍物一般就是确定的，不会取0-100之间的数值。

到了执行导航功能时，系统的地图又有所不同，此时使用的并不完全是使用建图的地图，而是使用代价地图。代价地图的取值范围是[0,254]，数值越大，表示占用程度越高，导航时小车越要远离。

代价地图的生成过程可以参考此文章：https://blog.csdn.net/qq_35635374/article/details/120874817（到了导航部分再细说），总而言之就是对之前建好的静态层地图和雷达运行探测到的障碍层地图按照膨胀规则进行膨胀和合并，生成数值在[0,254]之间的代价地图，导航时按照地图方格中的数值进行路径规划

#### 4.3.4.2 Hector

`Hector`算法框架是基于高斯牛顿
（Hector 在机器人快速转向时很容易发生错误匹配，建出的地图发生错位，原因主要是优化算法容易陷入局部最小值）

优点：不需要里程计，适应于空中或者路面不平坦的环境

缺点：旋转过快易发生漂移，无回环检测

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20240127172707169.webp" alt="image-20240127172707169" style="zoom: 50%;" />

#### 4.3.4.3 Karto

`Karto`算法框架是基于图优化

优点：这是首个基于图优化的开源算法，利用高度优化和非迭代平方根法分解从而进行稀疏化解耦求解

缺点：无法实时构建子图，耗费时间

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20240127172725405.webp" alt="image-20240127172725405" style="zoom:50%;" />

#### 4.3.4.4 Cartographer

`Cartographer`算法框架是基于图优化cartographer在不同环境下，调整参数和传感器配置，就能工作
大部分数据集，cartographer表现更优。ActiveSubmaps2D类中的submaps_列表实际最多只两个submap，一个认为是old_map，另一个认为是new_map，类似于滑窗操作。

当new_map插入激光scan的个数达到阈值时，则会将old_map进行结束，并且不再增加新的scan。同时将old_map进行删除，将new_map作为`oldmap`，然后重新初始化一个新的submap作为`newmap`。其具体实现可看代码注解，较为简单。首先回环优化，我们需要检测到回环，再进行优化。如何检测回环呢，前文也提到过，如果当前的scan和所有已创建完成的submap中的某个laser scan的位姿在距离上足够近，那么通过某种 scan match策略就会找到该闭环。

这里为了减少计算量，提高实时回环检测的效率，Cartographer应用了branch and bound(分支定界)优化方法进行优化搜索，如果得到一个足够好的匹配，到此处，回环检测部分已经结束了，已经检测到了回环得存在。接下来要根据当前scan的位姿和匹配到得最接近的submap中的某一个位姿来对所有的submap中的位姿进行优化，即使残差E最小。

优点：适应于低成本激光雷达，加速回环检测，实时性强

缺点：在几何对称环境中，易回环出错

![image-20240127172736432](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20240127172736432.webp)

### 4.3.5 pgm 转 posegraph

> Contributor: 唐锦梁

#### 4.3.5.1 精修编辑 pgm 地图

> 参考资料：
>
> [14] [ROS—PGM地图文件的编辑 | 闫金钢的Blog - https://yanjingang.com/](https://yanjingang.com/blog/?p=8597)

根据需求添加或删除围挡。最重要的是将障碍物完全涂黑，障碍物内部不要保留任何白色区域！

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/Pasted image 20250214091419.webp" style="zoom: 25%;" />

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20250217152911916.webp" alt="image-20250217152911916" style="zoom: 25%;" />

#### 4.3.5.2 使用 Ogm2Pgbm 获取带有点云和位姿的 rosbag

安装过程如下

```bash
sudo apt update
sudo apt upgrade -y

sudo apt install -y apt-transport-https ca-certificates curl software-properties-common

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update

sudo apt install -y docker-ce docker-ce-cli containerd.io
```

可以运行以下命令验证Docker是否安装成功

```bash
sudo docker run hello-world
```

(可选)(强烈建议) 添加当前用户到 `docker` 组, 这样就无需每次使用 `sudo` 来运行docker命令

```bash
sudo usermod -aG docker $USER

# 运行完成后注销登录或重启即可生效(建议立刻重启)
```

(可选) 安装Docker Compose

```bash
sudo curl -L "https://github.com/docker/compose/releases/download/$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep -Po '"tag_name": "\K.*?(?=")')/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose

# 验证安装情况
docker-compose --version
```

**使用 Docker 获取功能包**

获取镜像, 该镜像体积较大, 拉取和解压过程较长

```bash
sudo docker pull lihanchen2004/ogm2pgbm:latest
```

克隆仓库，仓库中 `/Ogm2Pgbm/workspace/map/` 将会被映射到 Docker 容器中，方便替换地图

```bash
git clone https://github.com/LihanChen2004/Ogm2Pgbm
cd Ogm2Pgbm
```

安装 `nvidia-container-toolkit` , 注意需要提前在NVIDIA官网下载并安装驱动 [NVIDIA Drivers for Linux](https://www.nvidia.com/en-us/drivers/)

```bash
curl -fsSL https://nvidia.github.io/libnvidia-container/gpgkey | sudo gpg --dearmor -o /usr/share/keyrings/nvidia-container-toolkit-keyring.gpg \
  && curl -s -L https://nvidia.github.io/libnvidia-container/stable/deb/nvidia-container-toolkit.list | \
    sed 's#deb https://#deb [signed-by=/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg] https://#g' | \
    sudo tee /etc/apt/sources.list.d/nvidia-container-toolkit.list
```

```bash
sudo apt-get update
sudo apt-get install -y nvidia-container-toolkit
```

(建议) 开启独显直连, 按下图完成后重启生效
![[Pasted image 20250214104010.webp]]

基于 `lihanchen2004/ogm2pgbm:latest` 创建容器

```bash
# 注意如果到现在为止还没重启过, 建议先重启一次在运行以下命令 :)
sudo ./autorun.sh
```

**启动功能包**

将你需要转换的 `.pgm` 和 `.yaml` 文件复制到宿主机的 `Ogm2Pgbm/workspace/map/` 目录中

> 以下操作均在 Docker容器中完成

请确保当前终端已经进入 Docker container 中
进入终端后会出现一个绿色的→箭头, 如下图
<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/Pasted image 20250214105219.webp" style="zoom: 33%;" />

```bash
MAP_NAME=rmuc_2025

roslaunch ogm2pgbm ogm2pgbm.launch map_file:=/root/workspace/map/$MAP_NAME.yaml record:=true
```

> 命令行可能会输出一大堆类似 `# QXcbConnection: XCB error: 2 (BadValue)` 的报错, 此现象疑似由Qt框架引起, 所以建议不要拖动弹出的RVIZ窗口, 不过貌似影响不大而且触发具有偶然性, 多运行几次就好了

运行上述命令后会启动RVIZ
<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/Pasted image 20250214105348-1739778855212-7.webp" style="zoom: 25%;" />
等待3~4分钟, 程序执行完毕后会在终端输出 `done!`
<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/Pasted image 20250214105744.webp" style="zoom:50%;" />
随后 `Ctrl + C` 终止程序, 程序将自动把 rosbag 保存至 `/root/.ros/ogm2pgbm_sensordata.bag` (容器内部路径)

**将 rosbag 下载到宿主机**

> 以下操作均在宿主机中进行

1. 查看 `CONTAINER_ID` , 运行 `autorun.sh` 确保容器还在运行

   ```bash
   docker ps
   ```

2. 保存 rosbag 到宿主机

   1. 注意修改 `CONTAINER_ID` !!!
   2. 以下命令将容器的 `rosbag` 保存到宿主机的 `Download` 目录

   ```bash
   CONTAINER_ID=abcdef123456
   CONTAINER_PATH=/root/.ros/ogm2pgbm_sensordata.bag
   DST_PATH=~/Downloads/
   
   docker cp $CONTAINER_ID:$CONTAINER_PATH $DST_PATH
   ```

#### 4.3.5.3 将 .bag 转换为 .db3

> 以下操作均在宿主机中进行

在 ROS1 中，rosbag 的文件后缀是 .bag，它是一种基于二进制的 ROS 消息存储格式。ROS2 对 rosbag 格式进行了一些改进和扩展，采用了一种基于 SQLite 的数据库格式，包括一个 .db3 数据库和一个 .yaml 文件
[ternaris | rosbags](https://gitlab.com/ternaris/rosbags)

安装转换包

```bash
sudo pip install rosbags
```

```bash
rosbags-convert --src ogm2pgbm_sensordata.bag \
  --dst RMUC.db3 \
  --src-typestore empty \
  --dst-typestore ros2_humble \
  --exclude-topic /rosout /robot/map /rosout_agg
```

#### 4.3.5.4 播放 rosbag 并制图

> 以下操作均在宿主机中进行

**准备**

下载 rviz 配置文件，便于可视化![[ogm2pgbm.rviz]]

**启动**

1. 启动 `slam_toolbox` 准备建图

   ```bash
   ros2 run slam_toolbox async_slam_toolbox_node --ros-args \
     -p use_sim_time:=True \
     -p odom_frame:=robot_odom \
     -p base_frame:=robot_base_link \
     -p map_frame:=robot_map \
     -p do_loop_closing:=False \
     -p max_laser_range:=10.0
   ```

2. 播放 `rosbag`

   ```bash
   ros2 bag play RMUC.db3
   ```

3. 启动 rviz2 可视化

   1. 注意修改 rviz2 配置文件路径

      ```bash
      rviz2 -d ~/Downloads/ogm2pgbm.rviz 
      ```

**保存 .posegraph 地图**

待 rosbag 播放完毕，在 rviz2 界面左侧 `SlamToolBoxPlugin` 中设置好文件名，点击 `Serialize Map` 即可保存 `.posegraph+.data` 地图；点击 `Save Map` 可保存 `.pgm+.yaml` 地图 (保存在 `Downloads` 目录下)

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/Pasted image 20250214170405.webp" style="zoom: 25%;" />

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/Pasted image 20250214170427.webp" style="zoom:33%;" />

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20250217153213246.webp" alt="image-20250217153213246" style="zoom: 25%;" />

### 4.3.6 cmake进阶

cmake主要是用来方便管理c++工程文件，链接所需要的库依赖，再编译生成可执行文件

控制从源码到可执行文件的整个构建流程，包括编译、链接、测试等步骤。它还支持分布式编译，加速大项目的编译速度。

#### 4.3.6.1 常见问题

1.`target_compile_definitions` 的宏定义内容在VSCode编辑器中中无法识别

**解决方案**

在 `.vscode/c_cpp_properties.json` 中新增下列参数

参考自 [Stack Overflow](https://stackoverflow.com/questions/74397633/vscode-intellisense-cannot-understand-cmake-add-definitions)

```json
{
    "configurations": [
        {
            "compileCommands": "${workspaceFolder}/build/compile_commands.json"
        }
    ],
}
```

#### 4.3.6.2 直接编译C++工程文件

* example：

``` cmake
set(CMAKE_CXX_STANDARD 20)

Project(ApproximateDRAMandSRAM)

find_package(OpenCV REQUIRED)

message(STATUS "Open library status: ")
message(STATUS "> version: ${OpenCV_VERSION} ")
message(STATUS "libraries: ${OpenCV_LIBS} ")
message(STATUS "> include: ${OpenCV_INCLUDE_DIRS}  ")

find_package(FMT REQUIRED)



include_directories(${OpenCV_INCLUDE_DIRS}) 

aux_source_directory(. ALL_SRCS)
add_executable(main ${ALL_SRCS})

target_link_libraries(main
PUBLIC 
${OpenCV_LIBS}
fmt::fmt
)
```

* 把所有的cpp、hpp文件都放在当前目录下，直接生成一个可执行文件main即可

#### 4.3.6.3 ROS1平台上编译

##### 4.3.6.3.1 需求：编译一个rm__common功能包，作为动态链接库给其他功能包使用

* add_definitions(-Wall -Werror -Wno-enum-compare)  

  * **确保warning不会被省略**

 * find_package(Eigen3 REQUIRED)  

   * **寻找外部库**

* find_package(catkin REQUIRED
      COMPONENTS
      roscpp
      tf) 

  * **寻找ROS的组件**

* catkin_package(

  * INCLUDE_DIRS  

    * **使得其他依赖于该包的包能够找到并使用这个包的资源**

  * include  

    *  **当前的包路径**

  * ${EIGEN3_INCLUDE_DIR}  

    * **外部库的路径**

  * CATKIN_DEPENDS  

    * **ROS包的组件**
      tf
      rm_msg

    * DEPENDS  

      ***外部库**

      Eigen3

      LIBRARIES

      ***LIBRARIES 参数是用来声明当前包编译出来的库，供其他包使用**

      rm_common  

      ）

* include_directories( 

          include
            
          ${catkin_INCLUDE_DIRS}
            
          ${EIGEN3_INCLUDE_DIR})

  *  **设置编译器的头文件搜索路径，编译该包需要的头文件**        

* file(GLOB_RECURSE sources "src/*.cpp" "src/decision/*.cpp" "src/filter/*.cpp")

* add_library(rm_common SHARED ${sources})  

  * **编译生成动态链接库**

* add_executable(test_kalman test/test_kalman_filter.cpp)

* target_link_libraries(rm_common ${catkin_LIBRARIES})

  * **将 rm_common 库与 Catkin 的库依赖链接起来**

* target_link_libraries(test_kalman rm_common ${catkin_LIBRARIES})

  * **之前通过 add_library 命令定义的 rm_common 库**

* add_dependencies(rm_common rm_msgs_generate_messages_cpp)

  * **确保在 rm_common 库编译之前，rm_msgs_generate_messages_cpp 目标必须先完成**

* **汇总：**

``` cmake
project(rm_common)

## Use C++14
set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

## By adding -Wall and -Werror, the compiler does not ignore warnings anymore,
## enforcing cleaner code.
add_definitions(-Wall -Werror -Wno-enum-compare)

find_package(Eigen3 REQUIRED)

find_package(catkin REQUIRED
        COMPONENTS
        roscpp
        tf
        rm_msgs
        geometry_msgs
        control_msgs
        controller_manager_msgs
        imu_complementary_filter
        imu_filter_madgwick
        realtime_tools
        dynamic_reconfigure
        )

catkin_package(
        INCLUDE_DIRS   ##使得其他依赖于该包的包能够找到并使用这个包的资源
        include
        ${EIGEN3_INCLUDE_DIR}
        CATKIN_DEPENDS
        tf
        rm_msgs
        geometry_msgs
        control_msgs
        controller_manager_msgs
        imu_complementary_filter
        imu_filter_madgwick
        roscpp
        dynamic_reconfigure
        DEPENDS
        LIBRARIES
        rm_common
)

include_directories(  ##设置编译器的头文件搜索路径
        include
        ${catkin_INCLUDE_DIRS}
        ${EIGEN3_INCLUDE_DIR}
)

file(GLOB_RECURSE sources "src/*.cpp" "src/decision/*.cpp" "src/filter/*.cpp")

add_library(rm_common SHARED ${sources})
#add_executable(test_traj test/test_traj.cpp)
add_executable(test_kalman test/test_kalman_filter.cpp)

target_link_libraries(rm_common ${catkin_LIBRARIES})
#target_link_libraries(test_traj rm_common ${catkin_LIBRARIES})
target_link_libraries(test_kalman rm_common ${catkin_LIBRARIES})

# Fix rm_msgs generation problem
# See https://answers.ros.org/question/73048
add_dependencies(rm_common rm_msgs_generate_messages_cpp)

#############
## Install ##
#############

# Mark executables and/or libraries for installation
install(
        TARGETS ${PROJECT_NAME}
        ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
        LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
        RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

# Mark cpp header files for installation
install(
        DIRECTORY include/${PROJECT_NAME}/
        DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
        FILES_MATCHING PATTERN "*.h"
)

# Mark other files for installation
#install(
#        DIRECTORY doc
#        DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
#)

#############
## Testing ##
#############

if (${CATKIN_ENABLE_TESTING})
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -pthread")
    ## Add gtest based cpp test target and link libraries
    catkin_add_gtest(lqr_test
            test/unit_test_lqr.cpp
            test/LqrTest.cpp)
    target_link_libraries(lqr_test rm_common)
endif ()```
```

* package.xml:

``` xml
<package format="2">
    <name>rm_common</name>
    <version>0.1.20</version>
    <description>The rm_common package</description>

    <maintainer email="liaoqiayuan@gmail.com">qiayuan</maintainer>

    <license>BSD</license>

    <buildtool_depend>catkin</buildtool_depend>
    <depend>roscpp</depend>

    <depend>tf</depend>
    <depend>geometry_msgs</depend>
    <depend>realtime_tools</depend>
    <depend>rm_msgs</depend>
    <depend>imu_complementary_filter</depend>
    <depend>imu_filter_madgwick</depend>
    <depend>dynamic_reconfigure</depend>
    <depend>eigen</depend>
    <depend>control_msgs</depend>
    <depend>controller_manager_msgs</depend>

    <!-- The export tag contains other, unspecified, tags -->
    <export>
        <!-- Other tools can request additional information be placed here -->

    </export>
</package>
```

##### 4.3.6.3.2 ROS1上生成自定义消息类型

* 在package.xml添加两项：

```xml
<build_depend>message_generation</build_depend>
<exec_depend>message_runtime</exec_depend>
```

* 在cmakelists里添加以下内容：

```cmake
find_package(catkin REQUIRED COMPONENTS
  roscpp
  std_msgs
  message_generation
)
add_message_files(
  FILES
  MyCustomMsg.msg
)
generate_messages(
  DEPENDENCIES
  std_msgs
)
catkin_package(
  CATKIN_DEPENDS message_runtime
)

```

#### 4.3.6.4 ROS2 平台上编译

##### 4.3.6.4.1 需求：编译一个rm__common功能包，作为动态链接库给其他功能包使用（对比ROS1，大同小异）

* example：

```cmake
project(rm_common)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# # Find dependencies
find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(std_msgs REQUIRED)
find_package(rm_msgs REQUIRED)
find_package(builtin_interfaces REQUIRED)
include_directories(
  include
)
# Define the sources for the rm_common library
file(GLOB_RECURSE sources "src/*.cpp" )

# Create the rm_common shared library
add_library(rm_common SHARED ${sources})
# 链接生成rm_common动态链接库所需要的库
ament_target_dependencies(rm_common
  rclcpp
  std_msgs
  rm_msgs
  builtin_interfaces
)
# 这里导出库文件以便其他包能够链接到 rm_common 库
ament_export_targets(export_rm_common HAS_LIBRARY_TARGET)
install(
  TARGETS rm_common
  EXPORT export_rm_common
  ARCHIVE DESTINATION lib
  LIBRARY DESTINATION lib
  RUNTIME DESTINATION bin
)
#导出目标: ament_export_targets 告诉构建系统将 rm_common 库导出，以便其他包可以通过 find_package() 使用该库。
#安装规则: install() 定义了如何将 rm_common 库的各类文件（如静态库、动态库、可执行文件）安装到系统中指定的目录。
install(
  DIRECTORY include/${PROJECT_NAME}/
  DESTINATION include/${PROJECT_NAME}/
  FILES_MATCHING PATTERN "*.h"
)
#这一部分的安装操作是针对头文件的安装。它将 include/${PROJECT_NAME}/ 目录下的所有匹配 *.h 的头文件复制到目标安装位置。
if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  # the following line skips the linter which checks for copyrights
  # comment the line when a copyright and license is added to all source files
  set(ament_cmake_copyright_FOUND TRUE)
  # the following line skips cpplint (only works in a git repo)
  # comment the line when this package is in a git repo and when
  # a copyright and license is added to all source files
  set(ament_cmake_cpplint_FOUND TRUE)
  ament_lint_auto_find_test_dependencies()
endif()
ament_export_include_directories(include)
ament_export_dependencies(rclcpp std_msgs rm_msgs builtin_interfaces)#除了ament_cmake，其他的都导出
# Export package dependencies
ament_package()
```

* package.xml:

```xml
<?xml version="1.0"?>
<?xml-model href="http://download.ros.org/schema/package_format3.xsd" schematypens="http://www.w3.org/2001/XMLSchema"?>
<package format="3">
  <name>rm_common</name>
  <version>0.0.0</version>
  <description>TODO: Package description</description>
  <maintainer email="1779252249@qq.com">minipc01</maintainer>
  <license>TODO: License declaration</license>
  <!-- Build dependencies -->
  <buildtool_depend>ament_cmake</buildtool_depend>
  <buildtool_depend>rosidl_default_generators</buildtool_depend>

  <depend>rclcpp</depend>
  <depend>std_msgs</depend>
  <depend>rm_msgs</depend>
  <depend>builtin_interfaces</depend>

  <test_depend>ament_lint_auto</test_depend>
  <test_depend>ament_lint_common</test_depend>

  <export>
    <build_type>ament_cmake</build_type>
  </export>
</package>
```

##### 4.3.6.4.2 其他功能包要使用rm_common包

* example

```cmake
project(rm_hw)
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# find dependencies
find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(std_msgs REQUIRED)
find_package(rm_msgs REQUIRED)
find_package(builtin_interfaces REQUIRED)
find_package(rm_common REQUIRED)
find_package(Eigen3 REQUIRED)
find_package(geometry_msgs REQUIRED)
# 添加include路径
include_directories(include
${rm_common_INCLUDE_DIRS}  # 添加这一行
${EIGEN3_INCLUDE_DIR}
)

# 将源文件添加到可执行目标
add_executable(rm_robot_hw_node
  src/hardware_interface.cpp  # 你的源文件
  src/socketcan.cpp
  src/can_bus.cpp
)

# 链接需要的库
ament_target_dependencies(rm_robot_hw_node
  rclcpp
  std_msgs
  rm_msgs  
  builtin_interfaces
  rm_common
  Eigen3
  geometry_msgs
)

# 安装可执行文件
install(TARGETS rm_robot_hw_node
  DESTINATION lib/${PROJECT_NAME}
)

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  # the following line skips the linter which checks for copyrights
  # comment the line when a copyright and license is added to all source files
  set(ament_cmake_copyright_FOUND TRUE)
  # the following line skips cpplint (only works in a git repo)
  # comment the line when this package is in a git repo and when
  # a copyright and license is added to all source files
  set(ament_cmake_cpplint_FOUND TRUE)
  ament_lint_auto_find_test_dependencies()
endif()

ament_package()
```

* package.xml

```xml
<?xml version="1.0"?>
<?xml-model href="http://download.ros.org/schema/package_format3.xsd" schematypens="http://www.w3.org/2001/XMLSchema"?>
<package format="3">
  <name>rm_hw</name>
  <version>0.0.0</version>
  <description>TODO: Package description</description>
  <maintainer email="1779252249@qq.com">minipc01</maintainer>
  <license>TODO: License declaration</license>

  <buildtool_depend>ament_cmake</buildtool_depend>
  <buildtool_depend>rosidl_default_generators</buildtool_depend>
  <depend>eigen</depend>
  <depend>rclcpp</depend>
  <depend>std_msgs</depend>
  <depend>geometry_msgs</depend>
  <depend>rm_msgs</depend>
  <depend>rm_common</depend>
  <depend>builtin_interfaces</depend>
  <test_depend>ament_lint_auto</test_depend>
  <test_depend>ament_lint_common</test_depend>

  <export>
    <build_type>ament_cmake</build_type>
  </export>
</package>
```

##### 4.3.6.4.3 在ROS2中如果要生成自定义消息类型

* example

```cmake
cmake_minimum_required(VERSION 3.8)
project(rm_msgs)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# find dependencies
find_package(ament_cmake REQUIRED)
find_package(builtin_interfaces REQUIRED)
find_package(rosidl_default_generators REQUIRED)
find_package(std_msgs REQUIRED)
# 生成自定义消息接口
rosidl_generate_interfaces(${PROJECT_NAME}
  "msg/ActuatorState.msg"
  "msg/LpData.msg"
  DEPENDENCIES builtin_interfaces std_msgs
)

# 导出运行时依赖
ament_export_include_directories(include)
ament_export_dependencies(rosidl_default_runtime std_msgs builtin_interfaces)


# 安装消息文件以便其他包使用
install(
  DIRECTORY msg
  DESTINATION share/${PROJECT_NAME}
)

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  # the following line skips the linter which checks for copyrights
  # comment the line when a copyright and license is added to all source files
  set(ament_cmake_copyright_FOUND TRUE)
  # the following line skips cpplint (only works in a git repo)
  # comment the line when this package is in a git repo and when
  # a copyright and license is added to all source files
  set(ament_cmake_cpplint_FOUND TRUE)
  ament_lint_auto_find_test_dependencies()
endif()

ament_package()
```

* package.xml

```xml
<?xml version="1.0"?>
<?xml-model href="http://download.ros.org/schema/package_format3.xsd" schematypens="http://www.w3.org/2001/XMLSchema"?>
<package format="3">
  <name>rm_msgs</name>
  <version>0.0.0</version>
  <description>TODO: Package description</description>
  <maintainer email="1779252249@qq.com">minipc01</maintainer>
  <license>TODO: License declaration</license>

  <buildtool_depend>ament_cmake</buildtool_depend>

  <buildtool_depend>rosidl_default_generators</buildtool_depend>

  <depend>std_msgs</depend>
  <exec_depend>rosidl_default_runtime</exec_depend>
  <depend>builtin_interfaces</depend>

  <test_depend>ament_lint_auto</test_depend>
  <test_depend>ament_lint_common</test_depend>
  <member_of_group>rosidl_interface_packages</member_of_group>
  <export>
    <build_type>ament_cmake</build_type>
  </export>
</package>
```



# 5.项目与兵种开发

## 5.0 前置要求

确保MiniPC在车上，并正确连接**电源线**、**摄像头**、**C板串口**（若需要整车测试）。

使用*USB转TTL连接线*连接C板UART2与MiniPC上USB接口，串口引脚顺序按官方C板文档相应定义进行接线：

<img src=".\北京林业大学RoboMaster机甲大师视觉组从入门到精通\image-20250912221435614.webp" alt="image-20240123150219314" style="zoom: 65%;" />

**注意**：MiniPC启动时必须连接摄像头，否则可能遇到无法启动的情况；使用完毕后，先使用`poweroff`关闭MiniPC，再下电。

## 5.1  视觉工程部署

### 5.1.1 部署与编译

#### 5.1.1.1源代码仓库

源代码仓库：[dgsyrc/MiracleVision: A robot vision project for RoboMaster - https://github.com/](https://github.com/dgsyrc/MiracleVision)

### 5.1.2 必要环境依赖

OpenCV（安装参考 `2.1.1` 内容）

[fmt]([fmtlib/fmt: A modern formatting library - https://github.com/](https://github.com/fmtlib/fmt))

[mindvision 工业相机 SDK](https://pan.baidu.com/s/1CHb8mEZtElr9zUweLXUcmA) 提取码 rm24

onnxruntime（安装参考 `2.3.5` 内容）

### 5.1.3 安装

先按照  `2.1.1` 内容安装好OpenCV 4.5.5

以及按照 `2.3.5` 内容安装好onnxruntime

使用下列命令下载项目源码

```
git clone https://github.com/dgsyrc/MiracleVision.git
```

接着在 `MiracleVision/3rdparty` 下执行下列命令下载 `fmt` 库源码

```
git clone https://github.com/fmtlib/fmt.git
```

将下载好的工业相机SDK解压，在SDK文件夹下使用以下命令安装

```
sudo bash ./install.sh
```

在项目文件夹 `MiracleVision` 下新建文件夹 `build` 

可使用以下命令（在 `MiracleVision` 下使用）

```
mkdir build
```

执行下列命令编译源码

```
cmake ..
make -j4
```

其中 `-j4` 参数可选填，加了更快，但不建议大于4（NUC 11为4核8线程，线程过高可能导致死机或编译报错）

执行完成后，在 `build` 文件夹下执行以下命令运行

```
sudo ./bin/MiracleVision
```

### 5.1.2 配置文件详解

#### 5.1.2.1 angle_solve

`angle_solve_config.xml`

```xml
<?xml version="1.0"?>
<opencv_storage>
<ARMOR_HEIGHT>8.3</ARMOR_HEIGHT>
<ARMOR_LENGHT>10.6</ARMOR_LENGHT>
<PIC_ARMOR_HEIGHT>1024</PIC_ARMOR_HEIGHT>
<PIC_ARMOR_LENGHT>1280</PIC_ARMOR_LENGHT>
<PIC_DISTANCE>980</PIC_DISTANCE>
<ARMOR_DISTANCE>8.0</ARMOR_DISTANCE>
<SPEED_ARG>0.90</SPEED_ARG>
</opencv_storage>
```

| 项               | 含义                 | 类型  | 单位 |
| ---------------- | -------------------- | ----- | ---- |
| ARMOR_HEIGHT     | 装甲板宽度           | float | cm   |
| ARMOR_LENGHT     | 装甲板长度           | float | cm   |
| PIC_ARMOR_HEIGHT | 装甲板宽度           | float | px   |
| PIC_ARMOR_LENGHT | 装甲板长度           | float | px   |
| PIC_DISTANCE     | 标定时装甲板图像距离 | float | px   |
| ARMOR_DISTANCE   | 标定时装甲板实际距离 | float | cm   |
| SPEED_ARG        | 子弹速度系数         | float | -    |

#### 5.1.2.2 armor

`basic_armor_config.xml`

```xml
<?xml version="1.0"?>
<opencv_storage>
<!--
  DEBUG_MODE - display all windows
  - 1 Enable
  - 0 Disable
-->
<DEBUG_MODE>0</DEBUG_MODE>
<!--
  WINDOW_SCALE - windows size
  - 0 Small
  - 1 Medium
  - 2 Big
-->
<WINDOW_SCALE>0</WINDOW_SCALE>
<!--
  GRAY_EDIT - 是否调整灰度图参数
  - 1 Enable
  - 0 Disable
-->
<GRAY_EDIT>0</GRAY_EDIT>
<!--
  COLOR_EDIT - 是否调整颜色参数
  - 1 Enable
  - 0 Disable
-->
<COLOR_EDIT>0</COLOR_EDIT>
<!--
  METHOD - 图像预处理方式
  - 1 HSV
  - 0 BGR
-->
<METHOD>0</METHOD>
<!--
  RED_ARMOR_GRAY_TH   - 红色灰度参数 
  RED_ARMOR_COLOR_TH  - BGR 红色参数
  BLUE_ARMOR_GRAY_TH  - 蓝色灰度参数
  BLUE_ARMOR_COLOR_TH - GBR 蓝色参数
  GREEN_ARMOR_COLOR_TH- 绿色参数
  WHILE_ARMOR_COLOR_TH- 白色参数
-->
<RED_ARMOR_GRAY_TH>32</RED_ARMOR_GRAY_TH>
<RED_ARMOR_COLOR_TH>132</RED_ARMOR_COLOR_TH>
<BLUE_ARMOR_GRAY_TH>33</BLUE_ARMOR_GRAY_TH>
<BLUE_ARMOR_COLOR_TH>140</BLUE_ARMOR_COLOR_TH>
<GREEN_ARMOR_COLOR_TH>10</GREEN_ARMOR_COLOR_TH>
<WHILE_ARMOR_COLOR_TH>240</WHILE_ARMOR_COLOR_TH>
<!--
  - HSV 红色参数
-->
<H_RED_MIN>0</H_RED_MIN>
<H_RED_MAX>255</H_RED_MAX>
<S_RED_MIN>140</S_RED_MIN>
<S_RED_MAX>255</S_RED_MAX>
<V_RED_MIN>37</V_RED_MIN>
<V_RED_MAX>255</V_RED_MAX>
<!--
  - HSV 蓝色参数
-->
<H_BLUE_MIN>90</H_BLUE_MIN>
<H_BLUE_MAX>160</H_BLUE_MAX>
<S_BLUE_MIN>130</S_BLUE_MIN>
<S_BLUE_MAX>255</S_BLUE_MAX>
<V_BLUE_MIN>30</V_BLUE_MIN>
<V_BLUE_MAX>255</V_BLUE_MAX>
<!--
  - Red BGR threshold
-->
<B_RED_MIN>10</B_RED_MIN>
<B_RED_MAX>100</B_RED_MAX>
<G_RED_MIN>10</G_RED_MIN>
<G_RED_MAX>100</G_RED_MAX>
<R_RED_MIN>100</R_RED_MIN>
<R_RED_MAX>200</R_RED_MAX>
<!--
  - Blue BGR threshold
-->
<B_BLUE_MIN>70</B_BLUE_MIN>
<B_BLUE_MAX>230</B_BLUE_MAX>
<G_BLUE_MIN>10</G_BLUE_MIN>
<G_BLUE_MAX>160</G_BLUE_MAX>
<R_BLUE_MIN>0</R_BLUE_MIN>
<R_BLUE_MAX>50</R_BLUE_MAX>
<!--
  LIGHT_EDTI - 是否调整灯条形态参数
  - 1 Enable
  - 0 Disable
-->
<LIGHT_EDTI>0</LIGHT_EDTI>
<!--
  LIGHT_DRAW - 是否绘制灯条
  - 1 Enable
  - 0 Disable
-->
<LIGHT_DRAW>1</LIGHT_DRAW>
<!--
  LIGHT_RATIO_W_H_MIN - 灯条高宽比最小值
  LIGHT_RATIO_W_H_MAX - 灯条高宽比最大值
-->
<LIGHT_RATIO_W_H_MIN>10</LIGHT_RATIO_W_H_MIN>
<LIGHT_RATIO_W_H_MAX>150</LIGHT_RATIO_W_H_MAX>

<!--
  LIGHT_ANGLE_MIN - 灯条角度最小值
  LIGHT_ANGLE_MAX - 灯条角度最大值
  -90~90
-->
<LIGHT_ANGLE_MIN>-30</LIGHT_ANGLE_MIN>
<LIGHT_ANGLE_MAX>30</LIGHT_ANGLE_MAX>
<!--
  LIGHT_PERIMETER_MIN - 灯条周长最小值
  LIGHT_PERIMETER_MAX - 灯条周长最大值
-->
<LIGHT_PERIMETER_MIN>16</LIGHT_PERIMETER_MIN>
<LIGHT_PERIMETER_MAX>1000</LIGHT_PERIMETER_MAX>
<!--
  ARMOR_FORECAST - 是否调整预测模型
  - 1 Enable
  - 0 Disable
-->
<ARMOR_FORECAST>1</ARMOR_FORECAST>
<!--
  ARMOR_EDIT - 是否调整装甲板参数
  - 1 Enable
  - 0 Disable
-->
<ARMOR_EDIT>0</ARMOR_EDIT>
<!--
  ARMOR_DRAW - 是否绘制装甲板
  - 1 Enable
  - 0 Disable
-->
<ARMOR_DRAW>1</ARMOR_DRAW>
<!--
  ARMOR_HEIGHT_RATIO_MIN - 装甲板左右灯条高度比最小值
  ARMOR_HEIGHT_RATIO_MAX - 装甲板左右灯条高度比最大值
-->
<ARMOR_HEIGHT_RATIO_MIN>5</ARMOR_HEIGHT_RATIO_MIN>
<ARMOR_HEIGHT_RATIO_MAX>15</ARMOR_HEIGHT_RATIO_MAX>
<!--
  ARMOR_WIDTH_RATIO_MIN - 装甲板左右灯条宽度比最小值
  ARMOR_WIDTH_RATIO_MAX - 装甲板左右灯条宽度比最大值
-->
<ARMOR_WIDTH_RATIO_MIN>5</ARMOR_WIDTH_RATIO_MIN>
<ARMOR_WIDTH_RATIO_MAX>15</ARMOR_WIDTH_RATIO_MAX>
<!--
  ARMOR_Y_DIFFERENT - 左右灯条y的差值不超过灯条平均高度的倍数
-->
<ARMOR_Y_DIFFERENT>10</ARMOR_Y_DIFFERENT>
<!--
  ARMOR_HEIGHT_DIFFERENT - 左右灯条高度差值不超过灯条平均高度的倍数
-->
<ARMOR_HEIGHT_DIFFERENT>10</ARMOR_HEIGHT_DIFFERENT>
<!--
  ARMOR_ANGLE_DIFFERENT - 左右灯条角度差
-->
<ARMOR_ANGLE_DIFFERENT>200</ARMOR_ANGLE_DIFFERENT>
<!--
  ARMOR_SMALL_ASPECT_MIN - 装甲板最小宽高比
  ARMOR_TYPE_TH          - 大小装甲板分界宽高比
  ARMOR_BIG_ASPECT_MAX   - 装甲板最大宽高比
-->
<ARMOR_SMALL_ASPECT_MIN>11</ARMOR_SMALL_ASPECT_MIN>
<ARMOR_TYPE_TH>22</ARMOR_TYPE_TH>
<ARMOR_BIG_ASPECT_MAX>35</ARMOR_BIG_ASPECT_MAX>
</opencv_storage>
```

| 项                     | 含义                                     | 类型 | 值/单位                        |
| ---------------------- | ---------------------------------------- | ---- | ------------------------------ |
| DEBUG_MODE             | 调试模式（显示图形窗口）                 | bool | Disable (0), Enable (1)        |
| WINDOW_SCALE           | 窗口大小                                 | int  | Small (0), Medium (1), Big (2) |
| GRAY_EDIT              | 调整灰度图参数（显示参数滑动条）         | bool | Disable (0), Enable (1)        |
| COLOR_EDIT             | 调整颜色参数（显示参数滑动条）           | bool | Disable (0), Enable (1)        |
| METHOD                 | 图像预处理方式                           | bool | BGR (0), HSV (1)               |
| RED_ARMOR_GRAY_TH      | 红色灰度参数                             | int  | 0~255                          |
| RED_ARMOR_COLOR_TH     | BGR 红色参数                             | int  | 0~255                          |
| BLUE_ARMOR_GRAY_TH     | 蓝色灰度参数                             | int  | 0~255                          |
| BLUE_ARMOR_COLOR_TH    | BGR 蓝色参数                             | int  | 0~255                          |
| GREEN_ARMOR_COLOR_TH   | BGR 绿色参数                             | int  | 0~255                          |
| WHITE_ARMOR_COLOR_TH   | 白色参数                                 | int  | 0~255                          |
| H_RED_MIN              | HSV 红色识别参数（H 通道最小值）         | int  | 0~255                          |
| H_RED_MAX              | HSV 红色识别参数（H 通道最大值）         | int  | 0~255                          |
| S_RED_MIN              | HSV 红色识别参数（S 通道最小值）         | int  | 0~255                          |
| S_RED_MAX              | HSV 红色识别参数（S 通道最大值）         | int  | 0~255                          |
| V_RED_MIN              | HSV 红色识别参数（V 通道最小值）         | int  | 0~255                          |
| V_RED_MAX              | HSV 红色识别参数（V 通道最大值）         | int  | 0~255                          |
| H_BLUE_MIN             | HSV 蓝色识别参数（H 通道最小值）         | int  | 0~255                          |
| H_BLUE_MAX             | HSV 蓝色识别参数（H 通道最大值）         | int  | 0~255                          |
| S_BLUE_MIN             | HSV 蓝色识别参数（S 通道最小值）         | int  | 0~255                          |
| S_BLUE_MAX             | HSV 蓝色识别参数（S 通道最大值）         | int  | 0~255                          |
| V_BLUE_MIN             | HSV 蓝色识别参数（V 通道最小值）         | int  | 0~255                          |
| V_BLUE_MAX             | HSV 蓝色识别参数（V 通道最大值）         | int  | 0~255                          |
| B_RED_MIN              | 红色灯条 ROI 区域 B 通道均值最小值       | int  | 0~255                          |
| B_RED_MAX              | 红色灯条 ROI 区域 B 通道均值最大值       | int  | 0~255                          |
| G_RED_MIN              | 红色灯条 ROI 区域 G 通道均值最小值       | int  | 0~255                          |
| G_RED_MAX              | 红色灯条 ROI 区域 G 通道均值最大值       | int  | 0~255                          |
| R_RED_MIN              | 红色灯条 ROI 区域 R 通道均值最小值       | int  | 0~255                          |
| R_RED_MAX              | 红色灯条 ROI 区域 R 通道均值最大值       | int  | 0~255                          |
| B_BLUE_MIN             | 蓝色灯条 ROI 区域 B 通道均值最小值       | int  | 0~255                          |
| B_BLUE_MAX             | 蓝色灯条 ROI 区域 B 通道均值最大值       | int  | 0~255                          |
| G_BLUE_MIN             | 蓝色灯条 ROI 区域 G 通道均值最小值       | int  | 0~255                          |
| G_BLUE_MAX             | 蓝色灯条 ROI 区域 G 通道均值最大值       | int  | 0~255                          |
| R_BLUE_MIN             | 蓝色灯条 ROI 区域 R 通道均值最小值       | int  | 0~255                          |
| R_BLUE_MAX             | 蓝色灯条 ROI 区域 R 通道均值最大值       | int  | 0~255                          |
| LIGHT_EDTI             | 调整灯条形态参数（显示参数滑动条）       | bool | Disable (0), Enable (1)        |
| LIGHT_DRAW             | 绘制灯条                                 | bool | Disable (0), Enable (1)        |
| LIGHT_RATIO_W_H_MIN    | 灯条高宽比最小值                         | int  | 0.1                            |
| LIGHT_RATIO_W_H_MAX    | 灯条高宽比最大值                         | int  | 0.1                            |
| LIGHT_ANGLE_MIN        | 灯条角度最小值                           | int  | -90°~90°                       |
| LIGHT_ANGLE_MAX        | 灯条角度最大值                           | int  | -90°~90°                       |
| LIGHT_PERIMETER_MIN    | 灯条周长最小值                           | int  | px                             |
| LIGHT_PERIMETER_MAX    | 灯条周长最大值                           | int  | px                             |
| ARMOR_FORECAST         | 调整预测模型（显示参数滑动条）           | bool | Disable (0), Enable (1)        |
| ARMOR_EDIT             | 调整装甲板参数（显示参数滑动条）         | bool | Disable (0), Enable (1)        |
| ARMOR_DRAW             | 绘制装甲板                               | bool | Disable (0), Enable (1)        |
| ARMOR_HEIGHT_RATIO_MIN | 装甲板左右灯条高度比最小值               | int  | 0.1                            |
| ARMOR_HEIGHT_RATIO_MAX | 装甲板左右灯条高度比最大值               | int  | 0.1                            |
| ARMOR_WIDTH_RATIO_MIN  | 装甲板左右灯条宽度比最小值               | int  | 0.1                            |
| ARMOR_WIDTH_RATIO_MAX  | 装甲板左右灯条宽度比最大值               | int  | 0.1                            |
| ARMOR_Y_DIFFERENT      | 左右灯条y的差值不超过灯条平均高度的倍数  | int  | 0.1                            |
| ARMOR_HEIGHT_DIFFERENT | 左右灯条高度差值不超过灯条平均高度的倍数 | int  | 0.1                            |
| ARMOR_ANGLE_DIFFERENT  | 左右灯条角度差                           | int  | 0.1°                           |
| ARMOR_SMALL_ASPECT_MIN | 装甲板最小宽高比                         | int  | 0.1                            |
| ARMOR_TYPE_TH          | 大小装甲板分界宽高比                     | int  | 0.1                            |
| ARMOR_BIG_ASPECT_MAX   | 装甲板最大宽高比                         | int  | 0.1                            |

#### 5.2.2.3 serial

`uart_serial_config.xml`

```xml
<?xml version="1.0"?>
<opencv_storage>
<!-- PREFERRED_DEVICE - set preferred serial device path -->
<PREFERRED_DEVICE>/dev/ttyUSB0</PREFERRED_DEVICE>
<!-- 
  SET_BAUDRATE - default baudrate for serial
  - 1  B115200
  - 10 B921600
 -->
<SET_BAUDRATE>1</SET_BAUDRATE>
<!-- 
  SHOW_SERIAL_INFORMATION - wheather print serial inforation
  - 0 Disable
  - 1 Enable
 -->
<SHOW_SERIAL_INFORMATION>1</SHOW_SERIAL_INFORMATION>
</opencv_storage>
```

| 项                      | 含义               | 类型   | 值                        |
| ----------------------- | ------------------ | ------ | ------------------------- |
| PREFERRED_DEVICE        | 默认串口           | string | /dev/{device_name}        |
| SET_BAUDRATE            | 波特率             | int    | B115200 (1), B921600 (10) |
| SHOW_SERIAL_INFORMATION | 控制台串口信息输出 | bool   | Disable (0), Enable (1)   |

### 5.1.3 调试与自启动

打开调试模式，启动自瞄程序

#### 5.1.3.1调试

##### 5.1.3.1.1 阈值

对代码进行以下修改，使之实时显示摄像头效果。

1. 进入`base/MiracleVision.cpp`注释掉`#define RELEASE`

![微信图片_20250912224255](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/微信图片_20250912224255.webp)

2. 将`switch (serial_.returnReceiveMode())`改为`switch (uart::AUTO_AIM)`

![微信图片_20250912224303](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/微信图片_20250912224303.webp)

3. 在`configs/armor/basic_armor_config.xml`中，将`DEBUG_MODE`改为`1`

![微信图片_20250912224154](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/微信图片_20250912224154.webp)

4. 可以按需要调整的参数设置EDIT参数，若要调整灰度阈值，则将`GRAY_EDIT`设为1，程序启动后将弹出滑块窗口。

![微信图片_20250912224518](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/微信图片_20250912224518.webp)

##### 5.1.3.1.2 串口

查看控制台是否有 `[rec_info]` 串口解码信息输出，检查获取的各个参数是否正常

例如：yaw，pitch，color，bullet_velocity 等

云台运动 yaw/pitch 值要变化

发射弹丸弹速变化

颜色与我方装甲板颜色相同

无信息输出则串口掉线，重新插拔，重启程序

无法解决则更换串口模块 【注意：模块的芯片应为 `CP2102` （串口名称 `/dev/USB01` ）或模块使用STLink-V2.1（串口名称 `/dev/ACM01` ）】

##### 5.1.3.1.3 装甲板跟随

使用手持装甲板模块测试识别是否正常（远近，左右）

**注意：装甲板灯条应尽量与地面垂直，有条件可直接使用其它车辆作为目标进行测试**

装甲板未被框选的以下可能：

- 串口掉线，检查是否有串口输出信息
- 获取的颜色错误，找电控的查读裁判系统的代码是否出错
- 相机光圈过小/过大，尝试调整工业相机光圈
- 目标装甲板角度过大
- 目标装甲板颜色错误，离线模式（紫色）或为我方颜色

识别装甲板但云台不动：

- 串口掉线，重新插拔串口并重启程序
- 相机卡顿，在 UI 以及控制台可见卡顿现象，插拔相机以及重启程序，若不能解决，尝试更换相机在minipc的插入接口（换C口/反面USB口）【一般是相机供电不足引起】
- 电控方面接收问题，找电控开调试查

##### 5.1.3.1.4 弹道补偿调整

确认跟随正常后，开始调整弹速系数，改变装甲板远近/左右（固定靶），机器人开火

多次尝试均命中即可

弹道过高：`config/angle_solve/angle_solve_config.xml` 中将 `SPEED_ARG` 改大

弹道过低：`config/angle_solve/angle_solve_config.xml` 中将 `SPEED_ARG` 改小

修改幅度不要超过 `0.2`，多次调试确定最佳参数

#### 5.1.3.2 自启动

##### 5.1.3.2.1 配置脚本

放在目录 `MiracleVision/` 下，命名为 `start.sh`

**需要修改路径的用户名**

```
#!/bin/bash
cd /home/username/Desktop/MiracleVision/build
./bin/MiracleVision

exit 0
```

##### 5.1.3.2.2 配置服务

打开目录 `/etc/systemd/system/`

输入以下指令新建服务

```
sudo gedit autoaim.service
```

在 `autoaim.service` 中输入以下配置

**需要修改路径的用户名**

```
[Unit]
Description=AUTO AIM Service
After=network.target

[Service]
ExecStart=/home/username/Desktop/MiracleVision/start.sh

[Install]
WantedBy=multi-user.target
```

 输入以下命令启动

```
sudo systemctl daemon-reload
sudo systemctl start autoaim.service
sudo systemctl enable autoaim.service
```

用以下指令查看运行状态

```
sudo systemctl status autoaim.service
```

#### 5.1.3.3 录制终端会话到文件

**启动录制**

```bash
script my_session.log
```

执行上述命令后，系统会提示 Script started, file is my_session.log。此时，你在终端做的任何操作（包括 Vim 编辑、由命令产生的输出等）都会被实时写入 my_session.log 文件中。

**停止录制**

当操作完成需要结束录制时，可以使用以下任意一种方法：

- **输入命令：** `exit`
- **快捷键：** `Ctrl` + `D`

系统会提示 `Script done, file is my_session.log`，表示录制结束并已保存文件。

### 5.1.4 串口协议

#### 5.1.4.1 接收数据


| 数据位 | 内容                      | 解释                                                                                          |
| :----- | :------------------------ | :-------------------------------------------------------------------------------------------- |
| 0      | 头帧                      | ‘S’ (0x53)                                                                                    |
| 1      | 颜色                      | ALL (0), RED (1), BLUE (2)                                                                    |
| 2      | 模式                      | 0~9 (见表格后注释)                                                                            |
| 3      | 机器人 ID                 | 英雄 HERO (0), 无人机 UAV (1), 工程机器人 ENGINEERING (2), 步兵 INFANTRY (3), 哨兵 SENTRY (4) |
| 4      | yaw轴陀螺仪低八位         | 二进制数 (换算见注释)，单位：角度                                                             |
| 5      | yaw轴陀螺仪数据高八位     | 二进制数 (换算见注释)，单位：角度                                                             |
| 6      | pitch轴陀螺仪低八位       | 二进制数 (换算见注释)，单位：角度                                                             |
| 7      | pitch轴陀螺仪数据高八位   | 二进制数 (换算见注释)，单位：角度                                                             |
| 8      | yaw轴陀螺仪加速度低八位   | 二进制数 (换算见注释)，单位：角度                                                             |
| 9      | yaw轴陀螺仪加速度高八位   | 二进制数 (换算见注释)，单位：角度                                                             |
| 10     | pitch轴陀螺仪加速度低八位 | 二进制数 (换算见注释)，单位：角度                                                             |
| 11     | pitch轴陀螺仪加速度高八位 | 二进制数 (换算见注释)，单位：角度                                                             |
| 12     | 子弹速度                  | 二进制数 (换算见注释)，单位：m/s                                                              |
| 13     | 尾帧                      | ‘E’ (0x45)                                                                                    |

**模式**

| 参数 | 枚举类型标识符           | 模式                     |
| ---- | ------------------------ | ------------------------ |
| 0    | DEFAULT_MODE             | 默认模式（基础自瞄模式） |
| 1    | AUTO_AIM                 | 基础自瞄模式             |
| 2    | ENERGY_BUFF              | 能量机关模式             |
| 3    | SENTINEL_AUTONOMOUS_MODE | 哨兵模式                 |
| 4    | CAMERA_CALIBRATION       | 相机标定模式             |

**二进制数换算**

| 完整数据总位数 | 接收换算                                                   |
| -------------- | ---------------------------------------------------------- |
| 16             | 合并高低八位接收为short (int16_t)类型转换为float类型后/100 |
| 8              | 接收为unsigned char (u_int8_t)类型转换为float类型/10       |

#### 5.1.4.2 发送数据


| 数据位 | 内容                                  | 解释                                                             |
| :----- | :------------------------------------ | :--------------------------------------------------------------- |
| 0      | 头帧                                  | ‘S’ (0x53)                                                       |
| 1      | 装甲板数量 / 是否识别到能量机关装甲板 | 识别到的机器人装甲板数量 / 能量机关：未发现目标 (0) 发现目标 (1) |
| 2      | 开火命令                              | 不开火(0) 开火 (1)                                               |
| 3      | yaw 轴增加量低八位                    | 二进制数 (换算见注释)，单位：角度                                |
| 4      | yaw 轴增加量低高八位                  | 二进制数 (换算见注释)，单位：角度                                |
| 5      | pitch 轴增加量低低八位                | 二进制数 (换算见注释)，单位：角度                                |
| 6      | pitch 轴增加量低高八位                | 二进制数 (换算见注释)，单位：角度                                |
| 7      | 预测坐标x低八位                       | 二进制数 (换算见注释)，单位：像素                                |
| 8      | 预测坐标x高八位                       | 二进制数 (换算见注释)，单位：像素                                |
| 9      | 预测坐标y低八位                       | 二进制数 (换算见注释)，单位：像素                                |
| 10     | 预测坐标y高八位                       | 二进制数 (换算见注释)，单位：像素                                |
| 11     | 深度低八位                            | 二进制数 (换算见注释)                                            |
| 12     | 深度高八位                            | 二进制数 (换算见注释)                                            |
| 13     | CRC 校验位                            | CRC8                                                             |
| 14     | 尾帧                                  | ‘E’ (0x45)                                                       |

**二进制数换算**

| 完整数据总位数       | 发送换算                                                |
| -------------------- | ------------------------------------------------------- |
| 16 (raw & pitch)     | 原始数据*100去尾转换为short (int16_t)类型再拆分高低八位 |
| 16 (预测坐标 & 深度) | 直接拆分高低8位即可                                     |
| 8                    | 原始数据*10去尾转换为unsigned char (u_int8_t)类型       |

<div STYLE="page-break-after: always;"></div>

## 5.2 特定兵种开发

### 5.2.1 哨兵

> Contributor: 洪佳

#### 5.2.1.1 装置和线

| 设备             | 输入   | 其他   |
| ---------------- | ------ | ------ |
| 分电板           | CAN线  | 其他线 |
| 4个全向轮        | 信号线 | 电源线 |
| 拨弹电机         | 信号线 | 电源线 |
| 2个摩擦轮        | 信号线 | 电源线 |
| 荧光弹丸充能装置 | /      | 电源线 |
| YAW轴电机        | 信号线 | 电源线 |
| PITCH轴电机      | 信号线 | 电源线 |

#### 5.2.1.2 对应实物和示意模型

**分电板**

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20240123145741592.webp" alt="image-20240123145741592" style="zoom: 25%;" />



<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20240123145852713.webp" alt="image-20240123145852713" style="zoom:25%;" />

#### 5.2.1.3 接线

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/image-20240123150219314.webp" alt="image-20240123150219314" style="zoom: 15%;" />

<div STYLE="page-break-after: always;"></div>

## 5.3 上位机选型与性能评估

> Contributors: 唐锦梁

### 5.3.1 远程控制软件

在车载机器人的实际调试过程中，若依赖物理外设进行交互，往往需要携带一套繁琐的硬件设备：

- 显示设备：便携屏 × 1、HDMI转miniHDMI线 × 1、屏幕供电线 × 1
- 输入设备：键盘 × 1、鼠标 × 1
- 其他配件：充电宝 × 1（为屏幕供电）、拓展坞 × 1（解决接口不足）

这显然是非常不便且非常不优雅的。同时上位机在车载环境下通常无法连接物理显示器，因此建议使用远程桌面或 SSH 协议进行代码部署、调试与监控。

在远程控制软件选型与配置时，必须遵循以下原则以保障视觉组相关算法的运行效率：

- 资源占用低： 远程软件不应占用过多的 CPU 和 GPU 资源，避免抢占宝贵的上位机算力
- 低延迟： 为满足基本的调试和开发需要，画面应相对清晰且不卡顿
- 局域网优先： 不依赖外网转发服务器的局域网方案相对而言泛用性更强且不受三方软件的收费服务制约

#### 5.3.1.1 图形化远程控制

> ⚠️ **性能警示：** Jetson Orin Nano 等部分嵌入式平台 阉割了 NVENC 硬件编码器。这意味着图形化远程桌面的画面压缩将完全依赖 CPU 软解/软编，这会对系统负载产生显著影响，甚至导致系统卡顿。在此类平台上，建议优先使用 5.3.1.2 章节的命令行方案，仅在必要时开启图形界面

- NoMachine
  - 局域网、在图形化的远程控制方案中对 CPU资源的占用相对较小、支持共享剪贴板（可传输文件）、延迟低、画质高

#### 5.3.1.2 命令行远程控制

针对代码编译、脚本执行、文件管理及系统监控等任务，SSH (Secure Shell) 是高效、稳定且资源占用极低的解决方案。正如本文 1.3.4 节所述，现有三种主流客户端可供选择：VSCode 在开发集成方面表现优异，MobaXterm 以功能丰富全面著称，Tabby 则拥有现代化的美观界面。建议根据具体应用场景及个人操作习惯择优选取。

### 5.3.2 上位机选型

在 RM 比赛中，受限于成本和尺寸等因素，有以下常见的上位机选型方案

- X86 架构

  - Intel NUC 系列（如 NUC 11、NUC 10、NUC 8）

    - 特点：通常没有独立显卡，但是包含核显

      > 队内目前有 3 台 NUC 11

  - 派勤工控机 系列

    - 特点：NUC 的国产替代方案，形态与接口布局类似，性价比较高

      > 队内目前有 4 台派勤的工控机，其中 2 台 CPU 为 i7-1260P，2台为 U5-125H

  - 雷神 MIX-G 系列

    - 特点：高性能方案。该系列最大的优势在于搭载了 RTX 4060 等独立显卡，但相对而言体积重量较大且价格昂贵

      > 队内暂无，后期可尝试采购该系列
  
- ARM 架构

  - Jetson Orin Nano
    - 特点：典型的强 GPU 弱 CPU 平台
      - GPU 强悍：搭载 NVIDIA Ampere 架构 GPU，CUDA 生态，TensorRT 加速效果极佳
      - CPU 瓶颈明显：搭载的 ARM CPU 单核性能较弱
      - **工程痛点：** 编译大型 C++ 工程（如复杂的 ROS 包）速度极慢（20~30min，这在赛场上显然是无法接受的），且运行高频的导航规划时可能会因 CPU 满载导致延迟和漂移问题
    
  - RK3588 开发板（如 Orange Pi 5 / 5 Plus）
    - 特点：均衡性能： 8核 CPU（4大核+4小核）性能尚可，优于 Jetson Nano 系列；内置 6TOPS 算力的 NPU（但是调用较繁琐），性价比高
      - **开发门槛：** NPU 使用需依赖瑞芯微的 RKNN 框架，模型转换和部署比 NVIDIA TensorRT 麻烦，且对 ROS 的支持需要自行折腾系统环境

### 5.3.3 上位机性能测试软件

> 可考虑使用 GParted 硬盘克隆方便测试不同的机器

#### 5.3.3.1 CPU 性能测试

Sysbench 是一个模块化的、跨平台的多线程性能测试工具，主要用于评估 CPU 的整数计算能力和多线程并发处理能力

**安装：**

```bash
sudo apt install sysbench
```

**单核性能测试**（评估单线程逻辑处理能力，如复杂的路径规划算法）：

```bash
# 关注输出中的 "events per second" (数值越大越好)
sysbench cpu --cpu-max-prime=20000 --threads=1 run
```

**多核性能测试**（评估并行处理能力，如编译代码、多节点 ROS 通信）：

```bash
# threads设置为CPU核心数
sysbench cpu --cpu-max-prime=20000 --threads=$(nproc) run
```



#### 5.3.3.2 GPU 性能测试

glmark2

**安装：**

```bash
sudo apt install glmark2
```

**测试：**

```bash
glmark2
```

#### 5.3.3.3 磁盘 I/O 性能测试

在比赛中，录制高带宽的 rosbag（如点云+相机流）对磁盘写入速度要求极高。

- **测试** (测试 4K 随机写入，模拟日志记录场景)：

  ```bash
  sysbench fileio --file-total-size=5G --file-test-mode=rndwr prepare
  sysbench fileio --file-total-size=5G --file-test-mode=rndwr run
  sysbench fileio --file-total-size=5G --file-test-mode=rndwr cleanup
  ```

### 5.3.4 系统稳定性与压力测试

机器人是在相对封闭、振动且可能高温的环境下运行的，**散热**对其性能有极大影响

#### 5.3.4.1 烤机测试

**Stress-ng** 用于模拟 CPU 满载，检测系统是否会因过热而降频或死机

**安装**：

```bash
sudo apt install stress-ng
```

**测试**：

```bash
stress-ng --cpu $(nproc) --timeout 600s
```

**验收标准**： 在运行期间，配合监控软件观察 CPU 频率是否大幅下降。若出现严重降频，说明散热存在问题，需改进风道或更换硅脂。

### 5.3.5 实时性能监控工具

在代码调试和比赛运行期间，我们需要轻量级的工具来监控资源

#### 5.3.5.1 通用系统监控

- **Htop**：
  - **安装：**`sudo apt install htop`
  - **运行：**`htop`
  - 经典工具，查看各 CPU 核心负载、内存占用及僵尸进程
- **Btop** (推荐)：
  - **安装：**`sudo apt install btop`
  - **运行：**`btop`
  - 界面更现代，自带网络上传/下载速率监控和磁盘 I/O 图表，信息密度比 htop 更高
  - **btop 的一大特点是支持鼠标操作**。你可以直接点击界面上的按钮、进程或菜单

## 5.4 导航相关

> Contributors: 唐锦梁

### 5.4.1 激光雷达

经验之谈：

- 激光雷达散热几乎不影响精度（但这并不意味着不需要考虑雷达的散热），导致定位大幅度漂移大概率是上位机性能不足
  - 注意：激光雷达的散热主要影响激光雷达的使用寿命

- 激光雷达的光学罩（Livox Mid-360 的那个深色光学罩）是激光雷达整个光学系统的一部分，如果沾染指纹或者积灰，激光束在发射和接收时会发生散射或折射。
  - 这可能会导致两种后果：一是有效探测距离变短；二是产生噪点
  - 清理应当先使用气吹或者压缩空气，吹除表面的硬质灰尘颗粒，再用无纺布蘸取异丙醇擦拭
- 点云数量和点云质量也影响定位性能
- IMU 与激光雷达的同步
  - 目前主要的激光 SLAM 都是 LIO，高度依赖 IMU 来去除激光雷达在运动中的畸变
    - 硬同步：通过硬件信号线让激光雷达和 IMU 的时间戳物理对齐，精度极高（微秒级），效果最好
    - 软同步：依赖软件估算时间差，容易受系统负载和传输延迟影响，导致在剧烈运动或旋转时，定位发生漂移

## 5.5 强化学习

> Contributors: 唐锦梁

### 5.5.1 Isaac Lab 与 Isaac Sim 性能优化

#### 5.5.1.1 运行模式优化

在强化学习（RL）训练任务中，图形渲染会占用大量 GPU 显存和 CUDA Core 资源。对于不需要实时观察的训练过程，建议剥离渲染管线

**原理：** 禁用 USD Stage 的视口渲染，仅保留物理引擎计算（PhysX）和 Tensor 数据流

**预期收益：** 训练 FPS (Frames Per Second) 提升 <b>5% ~ 10%</b>，显存占用降低约 1-2 GB

**实施方法：** 在运行 Python 训练脚本时，根据 Isaac Lab 的启动参数添加 `--headless` 标志

```bash
# 示例：运行一个强化学习环境
./isaaclab.sh -p source/standalone/workflows/rsl_rl/train.py --task Isaac-Ant-v0 --headless
```

- 注意：如果代码中使用了 `AppLauncher` 类，请确保传递了 `headless=True` 参数配置

#### 5.5.1.2 硬件性能调度

##### 5.5.1.2.1 CPU 优化

Linux 默认的电源策略通常为 `powersave` 或 `ondemand`，这会导致 CPU 在处理突发物理计算时频繁变频，增加延迟

**实施方法：** 使用 `cpupower` 工具将所有核心锁定在最高频率

```bash
# 1. 安装工具
sudo apt update
sudo apt install linux-tools-common linux-tools-generic

# 2. 查看当前模式
cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_governor

# 3. 设置为性能模式 (Performance) (重启后会回到默认的模式)
sudo cpupower frequency-set -g performance
```

##### 5.5.1.2.2 GPU 优化

长时间训练会导致显存（VRAM）和核心温度飙升，触发 NVIDIA 驱动的**热节流**，导致训练速度突然下降

**实施方法：**

1. **启用风扇手动控制：** 打开 `NVIDIA X Server Settings` -> `Thermal Settings` -> 勾选 `Enable GPU Fan Control` -> 手动拉至 <b>85% - 100%</b>。 *(注：若无法调整，可能需要修改 `/etc/X11/xorg.conf` 添加 `Coolbits` 选项)*

2. **监控命令：**

   ```bash
   watch -n 1 nvidia-smi
   ```

   关注 `Pwr:Usage/Cap` 是否稳定，以及 `Temp` 是否超过 80°C

#### 5.5.1.3 资产管理与网络环境

**本地化资产缓存**
Isaac Sim 严重依赖 NVIDIA Nucleus 服务器提供的 USD 资产（环境、材质、机器人模型）

- 问题现象： 加载场景时进度条卡在 `Connecting to Nucleus...` 或训练中途报错 `Failed to resolve path`

优化方案：

- 下载 Omniverse Cache： 在 Omniverse Launcher 中安装 "Cache" 应用，并在设置中分配足够的磁盘空间（建议 SSD 50GB+）

- 预下载资产： 对于常用的 `Isaac/Environments` 或 `Isaac/Robots`，建议通过 Nucleus Navigator 手动下载到本地盘符（Localhost），并在代码中将资产路径指向本地路径而非云端路径

**网络连接**
由于 NVIDIA 的资产服务器位于海外，国内直连丢包率极高

关键问题：

- 材质缺失： 仿真环境全是灰模或粉色棋盘格

- 训练崩溃： 物理引擎初始化时因无法下载材质贴图而触发 `Segmentation Fault`

建议： 必须配置系统级或终端级代理（Proxy）

```bash
# 在运行 Isaac Lab 前的终端设置代理 (示例端口7890)
export http_proxy=http://127.0.0.1:7890
export https_proxy=http://127.0.0.1:7890
export no_proxy=localhost,127.0.0.1,::1
```

> 提示： 确保你的代理软件开启了 TUN 模式 或正确接管了终端流量

### 5.5.2 强化学习与仿真硬件平台

#### 5.5.2.1 CPU

> 原则：单核与多核性能需均衡，拒绝“洋垃圾”

**避雷对象：**

- **洋垃圾 E5 平台**：架构老旧，虽然核心数多但单核性能极差
- **低单核性能 CPU**：仿真环境通常高度依赖单核主频
- **低多核性能 CPU**：虽然单核重要，但多核性能过低会导致处理并发环境时出现瓶颈

**性能瓶颈：**

- **仿真卡顿**：物理引擎解算慢，导致交互采样率低
- **GPU 利用率低**：CPU 无法及时提供数据，导致显卡空转等待
- **IO 效率低**：模型导出和加载速度显著变慢

#### 5.5.2.2 GPU

> 原则：架构与算力优先，盲目追求大显存无意义

**避雷对象：**

- <b>魔改版 RTX 2080Ti (22G)</b>：稳定性差，且架构较老。实测训练速度相较于新架构入门卡（如 RTX 4060）并无显著优势
- <b>多卡交火 (SLI/Crossfire)</b>：深度学习训练依赖的是数据并行或模型并行，传统游戏领域的交火技术对训练加速“聊胜于无”，且配置复杂

**选购建议：**

- 在强化学习任务中，极大的显存（VRAM）往往利用率不高（除非涉及巨型图像输入的视觉 RL），优先考虑 CUDA 核心数和新架构带来的算力提升

**实际体验：**

> 电子产品价格波动大，价格仅供参考

- Tesla V100（16G/32G）
  - **价格**：超低预算计算卡，咸鱼半年质保价格 900 元左右
  - 软件兼容性
    - **可用**：Isaac Gym、常规深度学习训练
    - **不可用**：Isaac Lab（不支持）、Isaac Sim（光追功能无法开启）
  - **总结**：适合仅需跑旧版 Isaac Gym 或常规 CUDA 训练任务的用户，不支持依赖 RTX/光追特性的新一代仿真环境
- RTX 3080（10G）
  - **价格**：高兼容性卡，能买到的基本都是翻新/矿卡，价格约 2200 元
- RTX 3080 Ti
  - **价格**：高性能卡，价格约 3200 元
  - **性能对比**：
    - 性能仅落后 RTX 3090 约 5%
    - 训练性能实测略强于 RTX 5070 Ti
  - **总结**：在 3000 元价位段提供了接近旗舰级的算力，相比 3090 性价比更高
- RTX 5080（及 50 系现状）
  - **价格**：旗舰级新品，价格接近万元
  - **实测问题**：
    - **利用率低**：在强化学习及 YOLO 训练中，GPU 占用虽然显示 90%，但功耗被限制在 170W 左右跑不满
    - **性能提升有限**：实测仅比 RTX 3080 快 20%，与其巨大的价格差（4-5倍）不成正比
    - **生态不成熟**：50 系驱动目前存在兼容性问题，导致性能无法完全释放（类似的问题也出现在 4090 上，功耗仅能跑一半）
  - **总结**：当前阶段 50 系不建议用于强化学习环境。由于驱动和软件适配滞后，高昂的硬件成本无法转化为实际的训练效率

#### 5.5.2.3 存储

> 原则：避免由于 IO 造成训练瓶颈

**避雷对象：**

- **低速硬盘**：SATA 接口固态硬盘或任何读写速度低于 **1000MB/s** 的存储设备

**推荐标准：**

- 使用 **NVMe M.2 SSD**。RL 训练涉及大量的数据 Log 写入、Replay Buffer 读取以及模型 Checkpoint 保存，低速硬盘会显著拖慢整体训练流程

#### 5.5.2.4 RAM

> 原则：内存容量达标即可，不必过度追求参数

**配置标准：**

- **容量**：**32GB** 对于大多数一般用途的强化学习与仿真任务已经绰绰有余
- **性能影响**：内存的频率和时序好坏对 RL 训练性能的影响并不敏感，优先保证容量满足需求即可，无需在此投入过多预算

#### 5.5.2.5 捡垃圾心得

> 捡垃圾前，请确保自己有一颗愿意折腾的心，因此本节内容仅适合预算极其有限且具备调试能力的玩家

##### 5.5.2.5.1 CPU & 主板

**策略：采用非正规渠道的特殊硬件**

- **方案选择**：优先选择 **ES版（工程样品）CPU** 或 **MODT（魔改移动端CPU上台式机）板U套装**
- **优势**：相比正规零售版（盒装/散片），价格通常能便宜 **50%以上**
- **注意**：ES版需确认步进版本（水比较深），MODT需注意BIOS兼容性

##### 5.5.2.5.2 GPU

**策略：注重售后的核心二手卡**

- **方案选择**：购买带有 **3年店保** 的核心二手显卡（主要现在 30 系能买到的基本都是矿）
- **优势**：价格低廉，且通过店铺保修规避“矿卡”或老化带来的烧毁风险（烧了能修/换）（当然也不排除店铺跑路的可能性）

##### 5.5.2.5.3 电源

**策略：二手大牌，金牌认证**

- **方案选择**：寻找二手的大品牌、大瓦数、**80 Plus金牌认证**且成色较新的电源，如果买个二手杂牌的那还真不如整一个全新的国产电源
- **警告**：劣质电源内部电容可能老化，电源炸机可能把你的主板和显卡一波带走，所以虽然电源不直接影响服务器的性能，但其实**并不建议省电源的钱**
- **优势**：相比全新电源，成本可节省约 <b>40%</b>，同时大瓦数金牌能保证高负载下的供电稳定性

##### 5.5.2.5.4 散热

**策略：实用主义，风量至上**

- **机箱风扇**：
  - **选型**：使用**暴力风扇**（高转速工业扇）（需权衡噪音）
  - **连接**：**不要**直接连接主板针脚（避免电流过大烧毁主板），建议直接由电源供电或使用独立集线器
  - **优势**：比普通品牌消费级风扇便宜，风量巨大，能确保显卡、主板供电模组（VRM）等组件保持凉爽
- **CPU散热器**：
  - **选型**：使用**二手风冷散热器**
  - **优势**：风冷结构简单耐造，不易损坏，相比全新可节省 <b>60%</b> 的预算

> 笔记本可以考虑使用一个压风式散热器（约 200 ~ 300 元），但是长期使用有一定损伤笔记本散热风扇的风险，并且会导致键盘温度升高

##### 5.5.2.5.5 RAM & SSD

**策略：打包购买与损耗评估**

- **购买渠道**：尝试寻找与板U（CPU+主板）**打包出售**的内存和硬盘，通常组合购买价格更低
- <b>内存 (RAM) </b>：二手与全新体质差别不大，非常耐造，二手性价比极高
- <b>硬盘 (SSD/HDD) </b>：建议选择<b>年份较新</b>的盘，虽然可以是二手，但需关注健康度（写入量），避免数据丢失风险（注意有一些硬盘的读写数据是可以刷，可以清零的，这点最好提前搞清楚）

# 6. 文档规范与维护


> Contributors: 叶睿聪 (dgsyrc@github)、洪佳、唐锦梁

> 参考资料：
>
> [3] [【Typora 教程】手把手教你如何用Typora撰写笔记](https://www.bilibili.com/video/BV1h84y1Y7nn/?vd_source=436470546f64e53b7d4516956091ffd7)

软件：Typora

以Typora编辑器以及Mardown+latex语法为例

## 6.1 Markdown 与 Typora 教程

### 6.1.1 标题

>语法：# (一级标题)  ## (二级标题)  ### (三级标题) ......

>代码：
>
>```text
># 这是一级标题
>## 这是二级标题
>```

>效果:
>\# 这是一级标题
>\#\# 这是二级标题

>快捷键:
>
>* Ctrl+数字1~6可以快速将选中的文本调成对应级别的标题
>* Ctrl+0可以快速将选中的文本调成普通文本
>* Ctrl+加号/减号对标题级别进行加减

### 6.1.2 分割线

>语法:  ---或者***+回车

>代码:
>
>```text
>---或者***
>```

>效果:

-----

注意：*会自动补全另一个，字体显示不一致*；减号三个即可

### 6.1.3 文字显示

#### 6.1.3.1 字体

>语法:
>
>* 粗体:  用一对双星号包裹
>* 删除线:  用一对双飘号包裹
>* 下划线:  用一对u标签包裹
>* 斜体:  用一对单星号包裹
>* 高亮:  用一对双等号包裹

>代码:
>
>```text
>**这是粗体**
>~~这是删除线~~
><u>这是下划线</u>
>*这是斜体*
>==这是高亮==
>```

>效果:
**这是粗体**
~~这是删除线~~
<u>这是下划线</u>
*这是斜体*
==这是高亮==

>快捷键:
>
>* 加粗:  Ctrl+B
>* 删除线:  Shift+Alt+5
>* 下划线:  Ctrl+U
>* 斜体:  Ctrl+I

#### 6.1.3.2 上下标

>代码:
>
>```text
>x^{2}
>H_{2}O
>```

>效果:
>$x^{2}$
>$H_{2}O$

### 6.1.4 列表

#### 6.1.4.1 无序列表

>代码:
>
>```text
>*/-/+ +空格
>```

>效果:
>1.只有同一级别:
>
>* 苹果
>* 香蕉
>* 橘子
>
>2.子集类:
>
>* 一级分类
>  * 二级分类 
>    * 三级分类

>快捷键:  Ctrl+Shift+]

#### 6.1.4.2 有序列表

>代码:
>
>```text
>数字+.+空格
>```

>效果:
>1. 第一个标题
>2. 第二个标题
>3. 第三个标题
>
>   * 子内容1
>     * 子内容2
>4. 第四个标题

>快捷键:  Ctrl+Shift+[

#### 6.1.4.3 任务列表

>代码:
>
>```text
>- [ ] 吃早餐
>- [x] 背单词
>```

>效果:
>- [ ] 吃早餐
>- [x] 背单词

### 6.1.5 区块显示

>代码:
>
>```text
>>+回车
>```

>效果:
>>这是最外层区块
>
>>>这是内层区块
>
>>>>这是最内层区块

### 6.1.6 代码显示

#### 6.1.6.1 行内代码

代码：

```
`sudo rm -rf /*`
```

`sudo rm -rf /*`

>快捷键:  Ctrl+Shift+`

#### 6.1.6.2 代码块

点击代码块可以选择代码语言（要输入才会显示有什么选择），选择后会有代码高亮（也可以把语言标识写在第一行的三个点旁边以设置语言）

如：cpp（即C++）、python、cmake等

~~~markdown
```
代码块
```
~~~

例如C++代码：

````markdown
```cpp
代码块
```
````

代码高亮效果：

```cpp
#include<iostream>
using namespace std;

int main()
{
    cout << "Hello World!" << endl;
    return 0;
}
```

>快捷键:  Ctrl+Shift+K

### 6.1.7 链接

>代码:
>
>```text
>www.baidu.com
>[百度一下](https://www.baidu.com)
>[百度一下](https://www.baidu.com "https://www.baidu.com")
>```

>效果:
>www.baidu.com
>[百度一下](https://www.baidu.com)
>[百度一下](https://www.baidu.com "https://www.baidu.com")

>快捷键:  Ctrl+K

### 6.1.8 脚注

>说明:  对文本进行解释说明。

>代码: 
>
>```text
>[^文本]
>[^文本]:解释说明
>```

>应用:
>这是一个技术\[^①\]
>
>\[^①\]: 这是一个非常好用的框架。

实际效果为在文本后显示^后的文本

点击该文本后会跳转至文档最末尾并列出`[^①]:` 后内容

### 6.1.9 图片插入

```markdown
![描述](图片链接或本地路径)
```

如：

```markdown
![5](./Sirius 战队2023视觉组培训20231029/5.webp)
```

![5](./北京林业大学RoboMaster机甲大师视觉组从入门到精通/5.webp)

>快捷键:  Ctrl+Shift+I

### 6.1.10 表格

>代码:
>```text
>|  1   |  2   |  3   |
>| :--- | :--: | ---: |
>|  4   |  5   |  6   |
>|  7   |  8   |  9   |
>|  10  |  11  |  12  |
>```

>效果:

| 1   |   2   |    3 |
| --- | :---: | ---: |
| 4   |   5   |    6 |
| 7   |   8   |    9 |
| 10  |  11   |   12 |

>快捷键:  Ctrl+T

### 6.1.11 流程图

#### 6.1.11.1 横向流程图

> 代码:
>
> ````text
> ```mermaid
> graph LR
> A[方形]==>B(圆角)
> B==>C{条件a}
> C-->|a=1|D[结果1]
> C-->|a=2|E[结果2]
> F[横向流程图]
> ```
> ````

>效果:
>```mermaid
>graph LR
>A[方形]==>B(圆角)
>B==>C{条件a}
>C-->|a=1|D[结果1]
>C-->|a=2|E[结果2]
>F[横向流程图]
>```

#### 6.1.11.2 竖向流程图

> 代码:
>
> ````text
> ```mermaid
> graph TD
> A[方形]==>B(圆角)
> B==>C{条件a}
> C-->|a=1|D[结果1]
> C-->|a=2|E[结果2]
> F[竖向流程图]
> ```
> ````

>效果:
>```mermaid
>graph TD
>A[方形]==>B(圆角)
>B==>C{条件a}
>C-->|a=1|D[结果1]
>C-->|a=2|E[结果2]
>F[竖向流程图]
>```

### 6.1.12 表情符号

>代码:
>```text
>:happy:、:cry:、:man:
>```

>效果:
:happy:、 :cry:、 :man:

### 6.1.13 数学公式（Latex）

#### 6.1.13.1 公式的插入

**①行中公式**

>代码:
>
>```text
$公式$
>```

>效果:
$公式$

**②独立公式**

>代码:
>
>```text
>$$
>公式
>$$
>```

>效果:
$$
公式
$$

#### 6.1.13.2 上下标

>代码:
>
>```text
>$x^{y^z}=(1+e^x)^{-2xy^w}$
>$\sideset{^1_2}{^3_4}{\underset{6}\bigotimes}$
>```

效果:

$x^{y^z}=(1+e^x)^{-2xy^w}$

$\sideset{^1_2}{^3_4}{\underset{6}\bigotimes}$

#### 6.1.13.3 括号和分隔符

>代码:
>
>```text
>$\langle\quad\rangle\quad\lceil\quad\rceil\quad\lfloor\quad\rfloor\quad\lbrace\quad\rbrace\quad\lVert\quad\rVert$
>$f(x,y,z)=3y^2z\left(3+\dfrac{7x+5}{1+y^2}\right)$
>$\left.\dfrac{\mathrm{d}u}{\mathrm{d}x}\right|_{x=0}$
>```

>效果:
$\langle\quad\rangle\quad\lceil\quad\rceil\quad\lfloor\quad\rfloor\quad\lbrace\quad\rbrace\quad\lVert\quad\rVert$
$f(x,y,z)=3y^2z\left(3+\dfrac{7x+5}{1+y^2}\right)$
$\left.\dfrac{\mathrm{d}u}{\mathrm{d}x}\right|_{x=0}$

#### 6.1.13.4 分数

>代码:
>
>```text
>$\frac{a}{b}\quad\dfrac{a}{b}\quad {a\over b}$
>```

>效果:
$\frac{a}{b}\quad\dfrac{a}{b}\quad {a\over b}$

#### 6.1.13.5 开方

>代码:
>
>```text
>$\sqrt[根指数,省略时为2]{被开方数}$
>```

>效果:
$\sqrt{2}\quad\sqrt[3]{2}$

#### 6.1.13.6 省略号

>代码:
>
>```text
>$\cdots\quad\ldots\quad\vdots\quad\ddots$
>```

>效果:
$\cdots\quad\ldots\quad\vdots\quad\ddots$

#### 6.1.13.7 矢量和均值

>代码:
>
>```text
>$\overrightarrow{E(\vec{r})}\quad\overleftarrow{E(\vec{r})}\quad\overleftrightarrow{E(\vec{r})}\quad\underrightarrow{E(\vec{r})}\quad\underleftarrow{E(\vec{r})}\quad\underleftrightarrow{E(\vec{r})}\quad\overline{v}=\bar{v}\quad\underline{v}$
>```

>效果:
$\overrightarrow{E(\vec{r})}\quad\overleftarrow{E(\vec{r})}\quad\overleftrightarrow{E(\vec{r})}\quad\underrightarrow{E(\vec{r})}\quad\underleftarrow{E(\vec{r})}\quad\underleftrightarrow{E(\vec{r})}\quad\overline{v}=\bar{v}\quad\underline{v}$

#### 6.1.13.8 积分

>代码:
>
>```text
>$$
>\iint\limits_D\left(\dfrac{\partial Q}{\partial x}-\dfrac{\partial P}{\partial y}\right){\rm d}x{\rm d}y=\oint\limits_LP{\rm d}x+Q{\rm d}y
>$$
>```

>效果:
$$
\iint\limits_D\left(\dfrac{\partial Q}{\partial x}-\dfrac{\partial P}{\partial y}\right){\rm d}x{\rm d}y=\oint\limits_LP{\rm d}x+Q{\rm d}y
$$

#### 6.1.13.9 极限

>代码:
>
>```text
>$\lim\limits_{n\to\infin}(1+\dfrac{1}{n})^n=e$
>```

>效果:
$\lim\limits_{n\to\infin}(1+\dfrac{1}{n})^n=e$

#### 6.1.13.10 累加、累乘及交集、并集

>```text
>$\sum\limits_{i=1}^n\dfrac{1}{n^2}\quad and\quad\prod\limits_{i=1}^n\dfrac{1}{n^2}\quad and\quad\bigcup\limits_{i=1}^n\dfrac{1}{n^2}\quad and\quad\bigcap\limits_{i=1}^n\dfrac{1}{n^2}$
>```

>效果:
$\sum\limits_{i=1}^n\dfrac{1}{n^2}\quad and\quad\prod\limits_{i=1}^n\dfrac{1}{n^2}\quad and\quad\bigcup\limits_{i=1}^n\dfrac{1}{n^2}\quad and\quad\bigcap\limits_{i=1}^n\dfrac{1}{n^2}$

#### 6.1.13.11 希腊字母

| 语法                          | 字母                            | 语法                    | 字母                      | 语法               | 字母                 |
| :---------------------------- | ------------------------------- | ----------------------- | ------------------------- | ------------------ | -------------------- |
| \Alpha(\alpha)                | $\Alpha(\alpha)$                | \Beta(\beta)            | $\Beta(\beta)$            | \Gamma(\gamma)     | $\Gamma(\gamma)$     |
| \Epsilon(\epsilon)\varepsilon | $\Epsilon(\epsilon)\varepsilon$ | \Zeta(\zeta)            | $\Zeta(\zeta)$            | \Eta(\eta)         | $\Eta(\eta)$         |
| \Iota(\iota)                  | $\Iota(\iota)$                  | \Kappa(\kappa)\varkappa | $\Kappa(\kappa)\varkappa$ | \Lambda(\lambda)   | $\Lambda(\lambda)$   |
| \Nu(\nu)                      | $\Nu(\nu)$                      | \Xi(\xi)                | $\Xi(\xi)$                | \Omicron(\omicron) | $\Omicron(\omicron)$ |
| \Rho(\rho)\varrho             | $\Rho(\rho)\varrho$             | \Sigma(\sigma)\varsigma | $\Sigma(\sigma)\varsigma$ | \Tau(\tau)         | $\Tau(\tau)$         |
| \Phi(\phi)\varphi             | $\Phi(\phi)\varphi$             | \Chi(\chi)              | $\Chi(\chi)$              | \Psi(\psi)         | $\Psi(\psi)$         |
| \Delta(\delta)                | $\Delta(\delta)$                | \Theta(\theta)\vartheta | $\Theta(\theta)\vartheta$ | \Mu(\mu)           | $\Mu(\mu)$           |
| \Pi(\pi)\varpi                | $\Pi(\pi)\varpi$                | \Omega(\omega)          | $\Omega(\omega)$          | \upsilon           | $\upsilon$           |
| \ell                          | $\ell$                          | \eth                    | $\eth$                    | \hbar              | $\hbar$              |
| \hslash                       | $\hslash$                       | \mho                    | $\mho$                    | \partial           | $\partial$           |

#### 6.1.13.12 特殊字符

**①说明**

>可以在字符前使用`\large`或`\small`以显示更大或更小的字符。${\LARGE A}{\Large A}{\large A}A{\small A}$

**②关系运算符**

| 输入      | 显示        | 输入              | 显示                | 输入         | 显示         |
| --------- | ----------- | ----------------- | ------------------- | ------------ | ------------ |
| \pm(\mp)  | $\pm(\mp)$  | \times            | $\times$            | \div         | $\div$       |
| \nmid     | $\nmid$     | \cdot             | $\cdot$             | \mid         | $\mid$       |
| \bigodot  | $\bigodot$  | \bigotimes        | $\bigotimes$        | \bigoplus    | $\bigoplus$  |
| \ge       | $\ge$       | \le               | $\le$               | \ll          | $\ll$        |
| \geqslant | $\geqslant$ | \leqslant         | $\leqslant$         | \neq         | $\neq$       |
| \approx   | $\approx$   | \xlongequal{文本} | $\xlongequal{文本}$ | \triangleq   | $\triangleq$ |
| \sim      | $\sim$      | \doteq            | $\doteq$            | \equiv       | $\equiv$     |
| \cong     | $\cong$     | \propto           | $\propto$           | \parallel(\\ | )            |
| \prec     | $\prec$     | \pmod{2}          | $\pmod{2}$          | \bmod        | $\bmod{2}$   |

**③集合运算符**

| 输入      | 显示        | 输入        | 显示          | 输入       | 显示         |
| --------- | ----------- | ----------- | ------------- | ---------- | ------------ |
| \emptyset | $\emptyset$ | \varnothing | $\varnothing$ |            |              |
| \subset   | $\subset$   | \subseteq   | $\subseteq$   | \subsetneq | $\subsetneq$ |
| \supset   | $\supset$   | \supseteq   | $\supseteq$   | \supsetneq | $\supsetneq$ |
| \bigcap   | $\bigcap$   | \bigcup     | $\bigcup$     | \setminus  | $\setminus$  |
| \bigvee   | $\bigvee$   | \bigwedge   | $\bigwedge$   |            |              |
| \in       | $\in$       | \notin      | $\notin$      | \ni        | $\ni$        |

**④三角运算符**

| 输入    | 显示      | 输入 | 显示   | 输入   | 显示     |
| ------- | --------- | ---- | ------ | ------ | -------- |
| \circ   | $\circ$   | \bot | $\bot$ | \angle | $\angle$ |
| \degree | $\degree$ |      |        |        |          |

**⑤微积分运算符**

| 输入  | 显示    | 输入   | 显示     | 输入      | 显示     |
| ----- | ------- | ------ | -------- | --------- | -------- |
| \int  | $\int$  | \iint  | $\iint$  | \iiint    | $\iiint$ |
| \oint | $\oint$ | \oiint | $\oiint$ | \prime(‘) | $\prime$ |
| \lim  | $\lim$  | \infin | $\infin$ | \nabla    | $\nabla$ |

**⑥逻辑运算符**

| 输入     | 显示       | 输入       | 显示         | 输入   | 显示     |
| -------- | ---------- | ---------- | ------------ | ------ | -------- |
| \because | $\because$ | \therefore | $\therefore$ |        |          |
| \forall  | $\forall$  | \exist     | $\exist$     |        |          |
| \not>    | $\not>$    | \not<      | $\not<$      |        |          |
| \land    | $\land$    | \lor       | $\lor$       | \lnot  | $\lnot$  |
| \top     | $\top$     | \vdash     | $\vdash$     | \vDash | $\vDash$ |

**⑦带帽符号**

| 输入       | 显示         | 输入            | 显示              |
| ---------- | ------------ | --------------- | ----------------- |
| \hat{xy}   | $\hat{xy}$   | \widehat{xyz}   | $\widehat{xyz}$   |
| \tilde{xy} | $\tilde{xy}$ | \widetilde{xyz} | $\widetilde{xyz}$ |
| \check{x}  | $\check{x}$  | \breve{y}       | $\breve{y}$       |
| \grave{x}  | $\grave{x}$  | \acute{y}       | $\acute{y}$       |
| \dot{x}    | $\dot{x}$    | \ddot{x}        | $\ddot{x}$        |


**⑧选取符号**

| 输入                           | 显示                             | 输入                            | 显示                              |
| ------------------------------ | -------------------------------- | ------------------------------- | --------------------------------- |
| \fbox{a+b+c+d}                 | $\fbox{a+b+c+d}$                 |                                 |                                   |
| \overbrace{xx\cdots x}^{10个x} | $\overbrace{xx\cdots x}^{10个x}$ | \underbrace{xx\cdots x}_{10个x} | $\underbrace{xx\cdots x}_{10个x}$ |

**⑨箭头符号**

| 输入           | 显示             | 输入              | 显示                | 输入                | 显示                  |
| -------------- | ---------------- | ----------------- | ------------------- | ------------------- | --------------------- |
| \leftarrow     | $\leftarrow$     | \rightarrow       | $\rightarrow$       | \leftrightarrow     | $\leftrightarrow$     |
| \longleftarrow | $\longleftarrow$ | \longrightarrow   | $\longrightarrow$   | \longleftrightarrow | $\longleftrightarrow$ |
| \Leftarrow     | $\Leftarrow$     | \Rightarrow       | $\Rightarrow$       | \Leftrightarrow     | $\Leftrightarrow$     |
| \Longleftarrow | $\Longleftarrow$ | \Longrightarrow   | $\Longrightarrow$   | \Longleftrightarrow | $\Longleftrightarrow$ |
| \uparrow       | $\uparrow$       | \downarrow        | $\downarrow$        | \updownarrow        | $\updownarrow$        |
| \Uparrow       | $\Uparrow$       | \Downarrow        | $\Downarrow$        | \Updownarrow        | $\Updownarrow$        |
| \to            | $\to$            | \swarrow          | $\swarrow$          | \nearrow            | $\nearrow$            |
| \gets          | $\gets$          | \searrow          | $\searrow$          | \nwarrow            | $\nwarrow$            |
| \mapsto        | $\mapsto$        | \rightrightarrows | $\rightrightarrows$ |                     |                       |

**⑩空格**

| 输入 | 效果 | 输入 | 效果 | 输入    | 效果 |
| ---- | ---- | ---- | ---- | ------- | ---- |
| \\!  | $    | \!   | $    | 默认    | $    |    | $ | \quad  | $ | \quad  | $ |
| \,   | $    | \,   | $    | \;(\\ ) | $    | \; | $ | \qquad | $ | \qquad | $ |

#### 6.1.13.13 字体

> 代码:
>
> ```text
> ${\字体{需要转换的字符}}$
> ```

| 输入 | 说明     | 显示            | 输入  | 说明       | 显示                 |
| ---- | -------- | --------------- | ----- | ---------- | -------------------- |
| \rm  | 罗马体   | ${\rm{Sample}}$ | \cal  | 花体       | ${\cal{Sample}}$     |
| \it  | 意大利体 | ${\it{Sample}}$ | \Bbb  | 黑板粗体   | ${\Bbb{Sample}}$     |
| \bf  | 粗体     | ${\bf{Sample}}$ | \mit  | 数学斜体   | ${\mathit{Sample}}$  |
| \sf  | 等线体   | ${\sf{Sample}}$ | \scr  | 手写体     | ${\mathscr{Sample}}$ |
| \tt  | 打字机体 | ${\tt{Sample}}$ | \frak | 旧德式字体 | ${\frak{Sample}}$    |

#### 6.1.13.14 大括号和行标

>说明:  使用`\left`和`\right`来创建自动匹配高度的`()`、`[]`、`{}`、`.`。在每个公式末尾使用`\tag{行标}`来实现行标。

>代码:
>
>```text
>$$
>f\left(
>\left[
>\dfrac{1+\{x,y\}}{\left(\dfrac{x}{y}+\dfrac{y}{x}\right)(u+1)}+a
>\right]
>^{\dfrac{3}{2}}
>\right)
>\tag{行标}
>$$
>```

>效果:
$$
f\left(\left[\dfrac{1+\{x,y\}}{\left(\dfrac{x}{y}+\dfrac{y}{x}\right)(u+1)}+a\right]^{\dfrac{3}{2}}\right)\tag{行标}
$$

>说明:如果你想将行内显示的分隔符也变大,也可以使用`\middle`命令

>代码:
>
>```text
>$$
>\left\langle q\middle\|\dfrac{\dfrac{x}{y}}{\dfrac{u}{v}}\middle|p\right\rangle
>$$
>```

>效果:
$$
\left\langle q\middle\|\dfrac{\dfrac{x}{y}}{\dfrac{u}{v}}\middle|p\right\rangle
$$

#### 6.1.13.15 其他命令

**①注释文字**

>代码:
>
>```text
>$\text{文字}$
>```

>效果:
$$
f(n)=\begin{cases}n/2,&\text{if $n$ is even}\\3n+1,&\text{if $n$ is odd}\end{cases}
$$

**③文字颜色**

>* 适用新旧浏览器
>  代码:
>
>```text
>$\color{颜色}{文字}$
>```

| 输入    | 显示                     | 输入   | 显示                    | 输入   | 显示                    |
| ------- | ------------------------ | ------ | ----------------------- | ------ | ----------------------- |
| black   | $\color{black}{color}$   | grey   | $\color{grey}{color}$   | silver | $\color{silver}{color}$ |
| white   | $\color{white}{color}$   | maroon | $\color{maroon}{color}$ | red    | $\color{red}{color}$    |
| yellow  | $\color{yellow}{color}$  | lime   | $\color{lime}{color}$   | olive  | $\color{olive}{color}$  |
| green   | $\color{green}{color}$   | teal   | $\color{teal}{color}$   | auqa   | $\color{auqa}{color}$   |
| blue    | $\color{blue}{color}$    | navy   | $\color{navy}{color}$   | purple | $\color{purple}{color}$ |
| fuchsia | $\color{fuchsia}{color}$ |        |                         |        |                         |

>* 适用新版浏览器
>  代码:
>
>```text
>$\color{#rgb}{文字}$    (注:其中r、g、b可以输入0~9和a~f来分别表示红色、绿色和蓝色的纯度)
>```

| 输入 | 输出                  | 输入 | 输出                  | 输入 | 输出                  | 输入 | 输出                  |
| ---- | --------------------- | ---- | --------------------- | ---- | --------------------- | ---- | --------------------- |
| #000 | $\color{#000}{color}$ | #005 | $\color{#005}{color}$ | #00A | $\color{#00A}{color}$ | #00F | $\color{#00F}{color}$ |
| #500 | $\color{#500}{color}$ | #505 | $\color{#505}{color}$ | #50A | $\color{#50A}{color}$ | #50F | $\color{#50F}{color}$ |
| #A00 | $\color{#A00}{color}$ | #A05 | $\color{#A05}{color}$ | #A0A | $\color{#A0A}{color}$ | #A0F | $\color{#A0F}{color}$ |
| #F00 | $\color{#F00}{color}$ | #F05 | $\color{#F05}{color}$ | #F0A | $\color{#F0A}{color}$ | #F0F | $\color{#F0F}{color}$ |
| #050 | $\color{#050}{color}$ | #055 | $\color{#055}{color}$ | #05A | $\color{#05A}{color}$ | #05F | $\color{#05F}{color}$ |
| #550 | $\color{#550}{color}$ | #555 | $\color{#555}{color}$ | #55A | $\color{#55A}{color}$ | #55F | $\color{#55F}{color}$ |
| #A50 | $\color{#A50}{color}$ | #A55 | $\color{#A55}{color}$ | #A5A | $\color{#A5A}{color}$ | #A5F | $\color{#A5F}{color}$ |
| #F50 | $\color{#F50}{color}$ | #F55 | $\color{#F55}{color}$ | #F5A | $\color{#F5A}{color}$ | #F5F | $\color{#F5F}{color}$ |
| #0A0 | $\color{#0A0}{color}$ | #0A5 | $\color{#0A5}{color}$ | #0AA | $\color{#0AA}{color}$ | #0AF | $\color{#0AF}{color}$ |
| #5A0 | $\color{#5A0}{color}$ | #5A5 | $\color{#5A5}{color}$ | #5AA | $\color{#5AA}{color}$ | #5AF | $\color{#5AF}{color}$ |
| #AA0 | $\color{#AA0}{color}$ | #AA5 | $\color{#AA5}{color}$ | #AAA | $\color{#AAA}{color}$ | #AAF | $\color{#AAF}{color}$ |
| #FA0 | $\color{#FA0}{color}$ | #FA5 | $\color{#FA5}{color}$ | #FAA | $\color{#FAA}{color}$ | #FAF | $\color{#FAF}{color}$ |
| #0F0 | $\color{#0F0}{color}$ | #0F5 | $\color{#0F5}{color}$ | #0FA | $\color{#0FA}{color}$ | #0FF | $\color{#0FF}{color}$ |
| #5F0 | $\color{#5F0}{color}$ | #5F5 | $\color{#5F5}{color}$ | #5FA | $\color{#5FA}{color}$ | #5FF | $\color{#5FF}{color}$ |
| #AF0 | $\color{#AF0}{color}$ | #AF5 | $\color{#AF5}{color}$ | #AFA | $\color{#AFA}{color}$ | #AFF | $\color{#AFF}{color}$ |
| #FF0 | $\color{#FF0}{color}$ | #FF5 | $\color{#FF5}{color}$ | #FFA | $\color{#FFA}{color}$ | #FFF | $\color{#FFF}{color}$ |

**③删除线**

>说明:  使用`\require{cancle}`声明，再使用`\cancle{字符}`、`\bcancle{字符}`、`\xcancle{字符}`、`\cancleto{字符}{字符}`来实现各种**片段删除线**效果。

>代码:
>
>```text
>$$
>\require{cancel}\begin{array}{r1}
>\verb|y+\cancel{x}|&y+\cancel{x}\\
>\verb|y+\cancel{y+x}|&y+\cancel{y+x}\\
>\verb|y+\bcancel{x}|&y+\bcancel{x}\\
>\verb|y+\xcancel{x}|&y+\xcancel{x}\\
>\verb|y+\cancelto{0}{x}|&y+\cancelto{0}{x}\\
>\verb+\frac{1\cancel9}{\cancel95}=\frac15+&\frac{1\cancel9}{\cancel95}=\frac15\\
>\end{array}
>$$
>```

>效果:
$$
\require{cancel}
\begin{array}{ll}
\verb|y+\cancel{x}| & y+\cancel{x} \\
\verb|y+\cancel{y+x}| & y+\cancel{y+x} \\
\verb|y+\bcancel{x}| & y+\bcancel{x} \\
\verb|y+\xcancel{x}| & y+\xcancel{x} \\
\verb|y+\cancelto{0}{x}| & y+\cancelto{0}{x} \\
\verb|\frac{1\cancel9}{\cancel95}=\frac15| & \frac{1\cancel9}{\cancel95}=\frac15 \\
\end{array}
$$


>说明:  使用`\require{enclose}`来允许**整段删除线**的显示，再使用`\enclose{删除线效果}{字符}`来使用各种整段删除线效果。其中，删除线效果有`horizontalstrike`、`verticalstrike`、`updiagonalstrike`和`downdiagonalstrike`,可以叠加使用。

>代码:
>
>```text
>$$
>\require{enclose}\begin{array}{r1}
>\verb|\enclose{horizontalstrike}{x+y}|&\enclose{horizontalstrike}{x+y}\\
>\verb|\enclose{verticalstrike}{\frac xy}|&\enclose{verticalstrike}{\frac xy}\\
>\verb|\enclose{updiagonalstrike}{x+y}|&\enclose{updiagonalstrike}{x+y}\\
>\verb|\enclose{downdiagonalstrike}{x+y}|&\enclose{downdiagonalstrike}{x+y}\\
>\verb|\enclose{horizontalstrike,updiagonalstrike}{x+y}|&\enclose{horizontalstrike,updiagonalstrike}{x+y}\\
>\end{array}
>$$
>```

>效果:
$$
\require{enclose}\begin{array}{rl}
\verb|\enclose{horizontalstrike}{x+y}|&\enclose{horizontalstrike}{x+y}\\
\verb|\enclose{verticalstrike}{\frac xy}|&\enclose{verticalstrike}{\frac xy}\\
\verb|\enclose{updiagonalstrike}{x+y}|&\enclose{updiagonalstrike}{x+y}\\
\verb|\enclose{downdiagonalstrike}{x+y}|&\enclose{downdiagonalstrike}{x+y}\\
\verb|\enclose{horizontalstrike,updiagonalstrike}{x+y}|&\enclose{horizontalstrike,updiagonalstrike}{x+y}\\
\end{array}
$$

#### 6.1.13.16 矩阵

**①无框矩阵**

>代码:
>
>```text
>$$
>\begin{matrix}
>1&x&x^2\\
>1&y&y^2\\
>1&z&z^2\\
>\end{matrix}
>$$
>```

>效果:
$$
\begin{matrix}
1&x&x^2\\
1&y&y^2\\
1&z&z^2\\
\end{matrix}
$$

**②边框矩阵**

>说明:  在开头将`matrix`替换为`pmatrix`、`bmatrix`、`Bmatrix`、`vmatrix`、`Vmatrix`。

| matrix                               | pmatrix                                | bmatrix                                | Bmatrix                                | vmatrix                                | Vmatrix                                |
| ------------------------------------ | -------------------------------------- | -------------------------------------- | -------------------------------------- | -------------------------------------- | -------------------------------------- |
| $\begin{matrix}1&2\\3&4\end{matrix}$ | $\begin{pmatrix}1&2\\3&4\end{pmatrix}$ | $\begin{bmatrix}1&2\\3&4\end{bmatrix}$ | $\begin{Bmatrix}1&2\\3&4\end{Bmatrix}$ | $\begin{vmatrix}1&2\\3&4\end{vmatrix}$ | $\begin{Vmatrix}1&2\\3&4\end{Vmatrix}$ |

**③带分割线的矩阵**

>说明:  可以使用`cc|c`来在一个三列矩阵中插入分割线。

>代码:
>
>```text
>$$
>\left[
>\begin{array}{cc|c}
>1&2&3\\
>4&5&6
>\end{array}
>\right]
>$$
>```

>效果:
$$
\left[
\begin{array}{cc|c}
1&2&3\\
4&5&6
\end{array}
\right]
$$

**④行中矩阵**

>代码:
>
>```text
>$\bigl(\begin{smallmatrix}a&b\\c&d\end{smallmatrix}\bigr)$
>```

>效果:
$\bigl(\begin{smallmatrix}a&b\\c&d\end{smallmatrix}\bigr)$

#### 6.1.13.17 方程式序列

>说明:  可以使用`\begin{align}...\end{align}`来创建一列整齐且默认右对齐的方程式序列。请注意`{align}`是**自动编号**的，使用`{align*}`来声明停止自动编号，也可以使用`\notag`来取消特定行的自动编号。在需要的时候，你可以使用`\begin{equation}...\end{equation}`来强制表达式自动编号。

>代码:
>$$
>\begin{align}
>f(x)&=1+1\\
>&=2
>\end{align}
>$$
>
>$$
>\begin{equation}
>\left[
>\begin{array}{cc|c}
>1&2&3\\
>4&5&6
>\end{array}
>\right]
>\end{equation}
>$$
>
>
>
>```text
>$$
>\begin{align}
>\sqrt{37}=\sqrt{\dfrac{73^2-1}{12^2}}\\
>&=\sqrt{\dfrac{73^2}{12^2}\cdot\dfrac{73^2-1}{73^2}}\\
>&=\sqrt{\dfrac{73^2}{12^2}}\sqrt{\dfrac{73^2-1}{73^2}}\notag\\
>&=\dfrac{73}{12}\sqrt{1-\dfrac{1}{73^2}}\\
>\approx\dfrac{73}{12}\left(1-\dfrac{1}{2\cdot73^2}\right)\label{A}
>\end{align}
>$$
>***
>
>$$
>\begin{align*}
>v+m&=0&\text{Given}\tag1\\
>-w&=-w+0&\text{additive identity}\tag2\\
>-w+0&=-w+(v+w)&\text{equations $(1)$ and $(2)$}
>\end{align*}
>$$
>```

>效果:
$$
\begin{align}
\sqrt{37}&=\sqrt{\dfrac{73^2-1}{12^2}}\\
&=\sqrt{\dfrac{73^2}{12^2}\cdot\dfrac{73^2-1}{73^2}}\\
&=\sqrt{\dfrac{73^2}{12^2}}\sqrt{\dfrac{73^2-1}{73^2}}\notag\\
&=\dfrac{73}{12}\sqrt{1-\dfrac{1}{73^2}}\\
&\approx\dfrac{73}{12}\left(1-\dfrac{1}{2\cdot73^2}\right)\label{A}
\end{align}
$$

***

$$
\begin{align*}
v+m&=0&\text{Given}\tag1\\
-w&=-w+0&\text{additive identity}\tag2\\
-w+0&=-w+(v+w)&\text{equations $(1)$ and $(2)$}
\end{align*}
$$

你可以使用`\label{标签}`来创建一个标签，就如上面的方程式序列中展示的那样，之后使用`\eqref{标签}`引用你想引用的公式，效果为：$\eqref{A}$。如果不想要括号，可以输入`\ref{标签}`，效果为：公式 $\ref{A}$。

公式1和2的不同列之间存在间隔，如果你不想要，可以通过将`align`替换为`alignat{1}`来去除列间隔。

#### 6.1.13.18 条件表达式

>说明:  使用`\begin{cases}`来创造一组默认左对齐的条件表达式,在每一行插入`&`来指定需要对齐的内容,并在每一行结尾处使用`\\`,以`\end{cases}`结尾。

>代码:
>
>```text
>$$
>f(n)=
>\begin{cases}
>n/2,&\text{if $n$ is even}\\
>3n+1,&\text{if $n$ is odd}
>\end{cases}
>$$
>```

>效果:
$$
f(n)=
\begin{cases}
n/2,&\text{if $n$ is even}\\
3n+1,&\text{if $n$ is odd}
\end{cases}
$$

#### 6.1.13.19 配置行高

>说明:  可以使用`\\[2ex]`语句替代该行末尾的`\\`来让编译器适配 , 其中`[ex]`指一个"X-Height" , 即x字母高度 , 也可以使用`[3ex]`或`[4ex]`等。

>代码:
>
>```text
>$$
>f(n)=
>\begin{cases}
>\dfrac n2,&\text{if $n$ is even}\\[2ex]
>3n+1,&\text{if $n$ is odd}
>\end{cases}\tag{适配[2ex]}
>$$
>***
>
>$$
>f(n)=
>\begin{cases}
>\dfrac n2,&\text{if $n$ is even}\\
>3n+1,&\text{if $n$ is odd}
>\end{cases}\tag{不适配[2ex]}
>$$
>```

>效果:
$$
f(n)=
\begin{cases}
\dfrac n2,&\text{if $n$ is even}\\[2ex]
3n+1,&\text{if $n$ is odd}
\end{cases}\tag{适配[2ex]}
$$

***

$$
f(n)=
\begin{cases}
\dfrac n2,&\text{if $n$ is even}\\
3n+1,&\text{if $n$ is odd}
\end{cases}\tag{不适配[2ex]}
$$

#### 6.1.13.20 数组与表格

>说明:  数组与表格均以`\begin{array}`开头,并在其后定义列数及每一列的文本对齐方式,`c` `l` `r`分别代表居中、左对齐及右对齐。若要插入垂直分割线，在定义中插入`|`，若要插入水平分割线，在定义中加入`\hline`。

>代码:
>
>```text
>$$
>\begin{array}{c|lcr}
>n&\text{左对齐}&\text{居中对齐}&\text{右对齐}\\
>\hline
>1&0.24&1&125\\
>2&-1&189&-8\\
>3&-20&2000&1+10i
>\end{array}
>$$
>```

>效果:
$$
\begin{array}{c|lcr}
n&\text{左对齐}&\text{居中对齐}&\text{右对齐}\\
\hline
1&0.24&1&125\\
2&-1&189&-8\\
3&-20&2000&1+10i
\end{array}
$$

#### 6.1.13.21 嵌套表格或数组

>代码:
>
>```text
>$$
>% outer vertical array of arrays 外层垂直表格
>\begin{array}{c}
>% inner horizontal array of arrays 内层水平表格
>\begin{array}{cc}
>% inner array of minimum values 内层"最小值"数组
>\begin{array}{c|cccc}
>\text{min}&0&1&2&3\\
>\hline
>0&0&0&0&0\\
>1&0&1&1&1\\
>2&0&1&2&2\\
>3&0&1&2&3\\
>\end{array}
>&
>% inner array of maximum values 内层"最大值"数组
>\begin{array}{c|cccc}
>\text{max}&0&1&2&3\\
>\hline
>0&0&1&2&3\\
>1&1&1&2&3\\
>2&2&2&2&3\\
>3&3&3&3&3
>\end{array}
>\end{array}
>% 内层第一行表格组结束
>\\
>% inner array of delta values 内层第二行Delta值数组
>\begin{array}{c|cccc}
>\Delta&0&1&2&3\\
>\hline
>0&0&1&2&3\\
>1&1&0&1&2\\
>2&2&1&0&1\\
>3&3&2&1&0
>\end{array}
>% 内层第二行表格组结束
>\end{array}
>$$
>```

>效果:
>$$
>% outer vertical array of arrays 外层垂直表格
>\begin{array}{c}
>% inner horizontal array of arrays 内层水平表格
>\begin{array}{cc}
>% inner array of minimum values 内层"最小值"数组
>\begin{array}{c|cccc}
>\text{min}&0&1&2&3\\
>\hline
>0&0&0&0&0\\
>1&0&1&1&1\\
>2&0&1&2&2\\
>3&0&1&2&3\\
>\end{array}
>&
>% inner array of maximum values 内层"最大值"数组
>\begin{array}{c|cccc}
>\text{max}&0&1&2&3\\
>\hline
>0&0&1&2&3\\
>1&1&1&2&3\\
>2&2&2&2&3\\
>3&3&3&3&3
>\end{array}
>\end{array}
>% 内层第一行表格组结束
>\\
>% inner array of delta values 内层第二行Delta值数组
>\begin{array}{c|cccc}
>\Delta&0&1&2&3\\
>\hline
>0&0&1&2&3\\
>1&1&0&1&2\\
>2&2&1&0&1\\
>3&3&2&1&0
>\end{array}
>% 内层第二行表格组结束
>\end{array}
>$$

#### 6.1.13.22 方程组

>说明:  使用`\begin{array}...\end{array}`和`\left\{...\right.`来创建一个方程组,或者你也可以使用条件表达式组`\begin{cases}...\end{cases}`来实现相同效果。

>代码:
>
>```text
>$$
>\left\{
>\begin{array}{l}
>a_1x+b_1y+c_1z=d_1\\
>a_2x+b_2y+c_2z=d_2\\
>a_3x+b_3y+c_1z=d_3
>\end{array}
>\right.
>\quad\text{或者}\quad
>\begin{cases}
>a_1x+b_1y+c_1z=d_1\\
>a_2x+b_2y+c_2z=d_2\\
>a_3x+b_3y+c_1z=d_3
>\end{cases}
>$$
>```

>效果:
>$$
>\left\{
>\begin{array}{l}
>a_1x+b_1y+c_1z=d_1\\
>a_2x+b_2y+c_2z=d_2\\
>a_3x+b_3y+c_1z=d_3
>\end{array}
>\right.
>\quad\text{或者}\quad
>\begin{cases}
>a_1x+b_1y+c_1z=d_1\\
>a_2x+b_2y+c_2z=d_2\\
>a_3x+b_3y+c_1z=d_3
>\end{cases}
>$$

#### 6.1.13.23 连分式

>说明:  就像`\frac`一样,使用`\cfrac`或`\dfrac`来创建一个连分式,不要使用普通的`\frac`或`\over`来创建,否则看起来会**很恶心**。

>代码:
>
>```text
>$$
>x=a_0+\cfrac{1^2}{a_1+\cfrac{2^2}{a_2+\cfrac{3^2}{a_3+\cfrac{4^2}{a_4+\cdots}}}}
>$$
>```

>效果:
>$$
>x=a_0+\cfrac{1^2}{a_1+\cfrac{2^2}{a_2+\cfrac{3^2}{a_3+\cfrac{4^2}{a_4+\cdots}}}}
>$$

>反例:
>
>```text
>x=a_0+\frac{1^2}{a_1+\frac{2^2}{a_2+\frac{3^2}{a_3+\frac{4^2}{a_4+\cdots}}}}
>```

>效果:
>$$
>x=a_0+\frac{1^2}{a_1+\frac{2^2}{a_2+\frac{3^2}{a_3+\frac{4^2}{a_4+\cdots}}}}
>$$

>补充:  当然,你可以使用`\frac`来表达连分数的**紧缩记法**。

>代码:
>
>```text
>$$
>x=a_0+\frac{1^2}{a_1+}\frac{2^2}{a_2+}\frac{3^2}{a_3+}\frac{4^2}{a_4+}\cdots
>$$
>```

>效果:
>$$
>x=a_0+\frac{1^2}{a_1+}\frac{2^2}{a_2+}\frac{3^2}{a_3+}\frac{4^2}{a_4+}\cdots
>$$

#### 6.1.13.24 交换图表

>说明:  使用一行`$\require{AMScd}$`语句来允许交换图表的显示,并通过在开头使用`\begin{CD}`,结尾使用`\end{CD}`来创建。

>代码:
>
>```text
>$$
>\require{AMScd}
>\begin{CD}
>A@>a>>B\\
>@VbVV\# @VcVV\\
>C @>>d> D
>\end{CD}
>$$
>```

>效果:
$$
\begin{CD}
A@>a>>B\\
@V b V V\# @VV c V\\
C @>>d> D
\end{CD}
$$

>补充:  其中,`@>>>`代表右箭头、`@<<<`代表左箭头、`@VVV`代表下箭头、`@AAA`代表上箭头、`@=`代表水平双实线、`@|`代表竖直双实线、`@.`代表没有箭头。在`@>>>`的`>>>`之间任意插入文字即代表该箭头的注释文字。

>代码:
>
>```text
>$$
>\begin{CD}
>A@>>>B@>{\text{very long label}}>>C\\
>@.@AAA@|\\
>D@=E@<<<F
>\end{CD}
>$$
>```

>效果:
$$
\begin{CD}
A@>>>B@>{\text{very long label}}>>C\\
@.@AAA@|\\
D@=E@<<<F
\end{CD}
$$

#### 6.1.13.25 其他

>* 搜索$\LaTeX$

### 6.1.14 支持的HTML元素

#### 6.1.14.1 文本居中

>代码
>
>```text
><center>内容</center>
>```

>效果
>
><center>内容</center>

#### 6.1.14.2 快捷键显示

>代码:
>
>```text
><kbd>内容</kbd>
>```

>效果:
<kbd>内容</kbd>

#### 6.1.14.3 加粗

>代码:
>
>```text
><b>加粗</b>
>```

>效果:
<b>加粗</b>

#### 6.1.14.4 倾斜

>代码:
>
>```text
><i>倾斜</i>
>```

>效果:
<i>倾斜</i>

#### 6.1.14.5 上下标

>代码:
>
>```text
>开始<sup>123hi你好</sup>
>开始<sub>321hi你好</sub>
>```

>效果:
开始<sup>123hi你好</sup>
开始<sub>321hi你好</sub>

#### 6.1.14.6 填充的黑色箭头

> 代码：
>
> ```text
> &#x27A4;
> ```

> 效果：
> &#x27A4;

#### 6.1.14.7 分页符

代码：

```html
<div STYLE="page-break-after: always;"></div>
```

效果为生成pdf时遇到分页符则新开一页再放分页符后内容

<div STYLE="page-break-after: always;"></div>

## 6.2 文档在线部署
> Contributor: 唐锦梁

### 6.2.1 前言

视觉组虽然保留了一份可用的文档，但长期面临系统性维护缺失的问题。原有的 PDF 发行版更新滞后，而直接访问 GitHub 仓库又常受网络环境影响，导致文档利用率低下。虽然曾尝试迁移至飞书，但鉴于飞书对文件插入的限制以及对 Markdown 和 LaTeX 语法的支持不足，最终决定继续以 GitHub 为主要托管平台，以保障文档的格式兼容性与版本管理。

为解决 GitHub 直接阅读体验不佳的问题，我们采用 **Cloudflare Pages** 功能，将文档仓库部署为 Serverless 的静态在线网站。这不仅保证了访问速度，也实现了文档内容的自动化同步更新。

文档的在线版本基于 Cloudflare 的 pages 功能，实现 serverless 的在线文档部署。

> 注意：以下流程用作记录部署原理和复现步骤，现 Docsify 环境已部署完毕，仓库内容的任何变动均会自动触发构建并同步至在线文档

### 6.2.2 Github 仓库配置流程

在 GitHub 仓库根目录添加 `index.html` 文件，配置 Docsify 框架

**关键配置说明：** 由于使用 Typora 编辑的 Markdown 文件常采用非标准的 CSS 语法 `style="zoom:50%;"` 来缩放图片，Docsify 默认无法解析该属性。因此，我们在配置中通过正则表达式插件，在渲染前将 `style="zoom:..."` 自动替换为标准的 `style="width:..."`，以确保图片显示正常。

`index.html` 完整内容如下：

```html
<!DOCTYPE html>
<html lang="zh-cn">

<head>
    <meta charset="UTF-8">
    <title>北林 RoboMaster 视觉组文档</title>
    <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />
    <meta name="description" content="从入门到精通">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, minimum-scale=1.0">

    <link rel="stylesheet" href="//cdn.jsdelivr.net/npm/docsify@4/lib/themes/vue.css">
    <link rel="stylesheet" href="//cdn.jsdelivr.net/npm/katex@latest/dist/katex.min.css" />

    <style>
        /* 移动端优化 */
        .markdown-section img {
            max-width: 100%;
        }

        /* 修复 KaTeX 公式可能出现的滚动条问题 */
        .katex-display {
            overflow-x: auto;
            overflow-y: hidden;
        }
    </style>
</head>

<body>
    <div id="app">加载中...</div>

    <script>
        window.$docsify = {
            name: '北林视觉组教程',
            homepage: '北京林业大学RoboMaster机甲大师视觉组从入门到精通.md',
            loadSidebar: false,
            subMaxLevel: 3,
            auto2top: true,
            coverpage: false,

            // docsify-latex 配置 (通常默认即可，这里显式配置以防万一)
            latex: {
                inlineOpen: '$',
                inlineClose: '$',
                blockOpen: '$$',
                blockClose: '$$',
                kramed: false, // 禁用 kramed 兼容模式，使用默认 marked
                customOptions: {} // 这里可以透传 KaTeX 的原生配置
            },

            plugins: [
                function (hook, vm) {
                    hook.beforeEach(function (html) {
                        // 将 style="zoom:..." 替换为 style="width:..."
                        return html.replace(/style="zoom:\s*([^;"]+)(;?)"/g, 'style="width: $1$2; max-width: 100%;"');
                    });
                }
            ]
        }
    </script>

    <script src="//cdn.jsdelivr.net/npm/docsify@4/lib/docsify.min.js"></script>

    <script src="//cdn.jsdelivr.net/npm/katex@latest/dist/katex.min.js"></script>

    <script src="//cdn.jsdelivr.net/npm/docsify-latex@0"></script>

    <script src="//cdn.jsdelivr.net/npm/docsify-copy-code/dist/docsify-copy-code.min.js"></script>
    <script src="//cdn.jsdelivr.net/npm/docsify@4/lib/plugins/zoom-image.min.js"></script>

</body>

</html>
```

### 6.2.3 Cloudflare 部署流程

登录 Cloudflare 控制面板，点击 "计算和AI" 栏目下的 "Workers 和  Pages"

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/2026-01-22 20-00-15.webp" alt="image-20260122195736676" style="zoom:50%;" />

进入 "Workers 和  Pages" 后，点击 "创建应用程序"，点击下方小字 `开始使用` （因为我们要使用 pages，默认是 workers）

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/2026-01-22 20-03-17.webp" alt="image-20260122195736676" style="zoom:50%;" />

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/2026-01-22 20-05-23.webp" alt="image-20260122195736676" style="zoom:50%;" />

选择 "导入现有 Git 存储库" 后 `开始使用`，在随后的页面选择你 fork 的 `BJFU-Vision-Group-from-Beginner-to-Master` 仓库（需要将你的 GitHub 连接至 Cloudflare ），再点击 `开始设置`。进入下一个页面后无需改动，直接点击 `保存并部署即可`

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/2026-01-22 20-06-53.webp" alt="image-20260122195736676" style="zoom:50%;" />

### 6.2.4 自动更新机制

部署完成后，Cloudflare Pages 会与 GitHub 仓库建立 Webhook 连接。每当仓库（或指定的 Fork 分支）有新代码 Push 时，Cloudflare 会自动触发构建。通常等待约 30 秒后刷新网页，即可看到最新的文档内容。

## 6.3 文档图片维护

### 6.3.1 统一分辨率

由于文档中的图片来源混杂（设备拍照、高分屏截图等），分辨率差异巨大。过大的图片不仅增加仓库体积，还可能导致在 Typora 或在线文档中显示比例失调。

为此，我们提供了一个 Python 脚本，用于**批量处理高分辨率且体积过大**的图片。

**脚本逻辑：** 脚本会遍历指定目录，仅对同时满足以下条件的图片进行处理，防止误伤长截图或流程图：

- **宽度** > `width_threshold` (默认 2500px)
- **文件体积** > `size_threshold_mb` (默认 1.5MB)

处理动作为将其缩放至 `target_width` (默认 2000px) 并保存至 `resized_output` 子目录。

**依赖安装：** 需确保安装 Pillow 库：`pip install Pillow`

```python
import os
import sys
import argparse
from PIL import Image


def resize_images(input_dir, width_threshold=2500, size_threshold_mb=1.5, target_width=2000):
    """
    1. 遍历 input_dir
    2. 条件：宽度 > 2500 且 文件体积 > 1.5MB
    3. 动作：缩放到 2000 宽，保存到 resized_output 子文件夹
    """

    # 1. 基础校验
    if not os.path.exists(input_dir):
        print(f"错误：找不到路径 '{input_dir}'")
        return

    # 2. 计算字节阈值 (1.5MB = 1.5 * 1024 * 1024 字节)
    size_threshold_bytes = size_threshold_mb * 1024 * 1024

    # 3. 创建输出目录
    output_dir = os.path.join(input_dir, "resized_output")
    if not os.path.exists(output_dir):
        os.makedirs(output_dir)

    supported_formats = ('.jpg', '.jpeg', '.webp', '.bmp', '.tiff', '.webp')
    count = 0

    print("-" * 50)
    print(f"扫描目录: {input_dir}")
    print(f"过滤条件: 宽度 > {width_threshold}px 且 体积 > {size_threshold_mb}MB")
    print("-" * 50)

    files = os.listdir(input_dir)

    for filename in files:
        if filename.lower().endswith(supported_formats):
            file_path = os.path.join(input_dir, filename)

            try:
                # 获取文件大小 (字节)
                file_size_bytes = os.path.getsize(file_path)
                # 换算成 MB 用于显示
                file_size_mb = file_size_bytes / (1024 * 1024)

                # 优化：如果文件本身很小，直接跳过，不用打开图片读取像素，节省性能
                # (如果你希望严格打印所有图片的尺寸，可以去掉这个预判断)
                if file_size_bytes <= size_threshold_bytes:
                    continue

                with Image.open(file_path) as img:
                    width, height = img.size

                    # 核心判断逻辑：宽度超标 AND 体积超标
                    if width > width_threshold and file_size_bytes > size_threshold_bytes:

                        # 计算新尺寸
                        ratio = target_width / width
                        new_height = int(height * ratio)

                        # 执行缩放
                        resized_img = img.resize((target_width, new_height), Image.Resampling.LANCZOS)

                        # 保存
                        save_path = os.path.join(output_dir, filename)
                        resized_img.save(save_path)

                        print(f"[处理] {filename}")
                        print(f"      - 原参数: 宽{width}px | 体积 {file_size_mb:.2f}MB")
                        print(f"      - 新参数: 宽{target_width}px -> 保存至子目录")
                        count += 1
                    else:
                        # 虽然体积够大，但宽度不够，所以不处理
                        pass

            except Exception as e:
                print(f"[错误] 无法读取 {filename}: {e}")

    print("-" * 50)
    if count == 0:
        print("未发现满足条件的图片（同时满足宽>2500且体积>1.5MB）。")
        # 清理空目录
        if os.path.exists(output_dir) and not os.listdir(output_dir):
            os.rmdir(output_dir)
    else:
        print(f"任务完成！共压缩 {count} 张图片。")
        print(f"输出路径: {output_dir}")


def get_path_from_user():
    """获取动态路径输入"""
    parser = argparse.ArgumentParser(description="图片压缩脚本")
    parser.add_argument("path", nargs="?", help="图片文件夹路径")
    args = parser.parse_args()

    if args.path:
        return args.path

    while True:
        path = input("请输入图片文件夹路径 (输入 q 退出): ").strip()
        path = path.strip('"').strip("'")  # 去除可能的引号

        if path.lower() == 'q':
            sys.exit()

        if os.path.isdir(path):
            return path
        else:
            print("路径无效，请重新输入。")


if __name__ == "__main__":
    target_path = get_path_from_user()
    resize_images(target_path)
```

### 6.3.2 统一图片格式(WebP)

WebP 是一种由 **Google** 推出的现代图像格式，旨在在保证画质的同时，大幅减小图片文件体积，适用于网页和移动端应用。

具有高压缩率、支持有损与无损压缩、支持透明通道、支持动画、支持元数据等特性。

可以提高加载速度，减少网页流量，提高用户体验并节省带宽与存储空间。WebP 一个格式即可覆盖 JPEG、PNG、GIF 的主要使用场景。

现代浏览器对 WebP 都有良好的支持。

以下是一个使用 `libwebp` 库的批量 JPEG/PNG 转WebP 的简易 python 示例（多进程批量处理）

> 注意：使用前需确保系统内已配置 `libwebp`，Windows中可下载 Google 官方的预编译版本 [下载并安装 WebP  | Google for Developers](https://developers.google.com/speed/webp/download?hl=zh-cn)，选择对应的系统和处理器架构，将解压出来的文件夹下的 `bin` 目录添加至系统环境变量并重启计算机。

<img src="./北京林业大学RoboMaster机甲大师视觉组从入门到精通/2026-01-22 20-43-57.webp" alt="image-20260122195736676" style="zoom:50%;" />

该脚本的主要功能为对传入文件夹下的 `.jpg` `.jpeg` `.png` 格式的图片转换为 WebP，转换 `.png` 默认使用无损模式；由于 `.jpg` `.jpeg` 自身即为有损压缩，故可能出现转换后的 WebP 文件大于源文件的情况，故脚本中还加入了是否保留大体积文件的功能。

```python
import os
import subprocess
import multiprocessing
import argparse
import sys
from pathlib import Path


def convert_to_webp(file_info):
    # 解包参数：新增 keep_larger (是否保留大体积文件)
    file_path, quality_jpg, keep_original, source_root, output_root, keep_larger = file_info
    file_path = Path(file_path)

    # --- 计算输出路径 ---
    if output_root:
        try:
            rel_path = file_path.relative_to(source_root)
        except ValueError:
            rel_path = Path(file_path.name)
        output_path = output_root / rel_path.with_suffix('.webp')
        try:
            output_path.parent.mkdir(parents=True, exist_ok=True)
        except FileExistsError:
            pass
    else:
        output_path = file_path.with_suffix('.webp')
    # ------------------

    ext = file_path.suffix.lower()

    if ext == '.png':
        cmd = ["cwebp", "-lossless", str(file_path), "-o", str(output_path)]
    elif ext in ['.jpg', '.jpeg']:
        cmd = ["cwebp", "-q", str(quality_jpg), "-m", "6", "-sharp_yuv", str(file_path), "-o", str(output_path)]
    else:
        return

    try:
        subprocess.run(cmd, stdout=subprocess.DEVNULL, stderr=subprocess.DEVNULL, check=True)

        if output_path.exists():
            orig_size = file_path.stat().st_size
            webp_size = output_path.stat().st_size

            is_smaller = webp_size < orig_size

            # 逻辑判断：
            # 1. 如果体积变小 -> 总是保留
            # 2. 如果体积变大 且 用户允许保留(keep_larger) -> 保留
            # 3. 如果体积变大 且 用户不允许 -> 删除 WebP

            if not is_smaller and not keep_larger:
                print(f"[-] 忽略 {file_path.name}: 转换后体积变大 ({orig_size // 1024}KB -> {webp_size // 1024}KB)")
                output_path.unlink()  # 删除生成的 webp
            else:
                # 确定提示前缀
                prefix = "[+]" if is_smaller else "[!]"
                status_msg = "优化" if is_smaller else "保留(体积增大)"

                print(f"{prefix} {status_msg}: {file_path.name} ({orig_size // 1024}KB -> {webp_size // 1024}KB)")

                # 只有在决定保留 WebP 的情况下，才检查是否需要删除原图
                if not keep_original:
                    file_path.unlink()

    except Exception as e:
        print(f"[!] 错误 {file_path.name}: {e}")


def main():
    parser = argparse.ArgumentParser(description="图片批量转 WebP 脚本")
    parser.add_argument("path", nargs="?", help="源文件夹路径")
    parser.add_argument("-o", "--output", help="输出文件夹名称或路径")
    parser.add_argument("-q", "--quality", type=int, default=90, help="JPG 质量 (默认 90)")
    parser.add_argument("--delete", action="store_true", help="转换成功后删除原图")
    # 新增命令行参数
    parser.add_argument("--keep-larger", action="store_true", help="即使 WebP 体积大于原图也保留")

    args = parser.parse_args()

    source_path = args.path
    output_input = args.output
    keep_larger = args.keep_larger

    # --- 1. 获取源路径 ---
    if not source_path:
        print(">>> 提示：你可以直接将文件夹拖入此窗口")
        source_path = input("1. 请输入[图片源文件夹]路径: ").strip()
        source_path = source_path.replace('"', '').replace("'", "")

    source_dir = Path(source_path).resolve()

    if not source_dir.is_dir():
        print(f"❌ 错误: '{source_path}' 不是一个有效的文件夹。")
        sys.exit(1)

    # --- 2. 获取输出路径 ---
    if not output_input:
        print(f"\n>>> (可选) 请输入输出文件夹名称 (默认为原目录)")
        output_input = input("2. 请输入[输出文件夹]名称/路径: ").strip()
        output_input = output_input.replace('"', '').replace("'", "")

    output_dir = None
    if output_input:
        p_out = Path(output_input)
        if p_out.is_absolute():
            output_dir = p_out
        else:
            output_dir = source_dir / p_out

    # --- 3. 询问是否保留大文件 (仅在没有通过命令行指定时询问) ---
    if not args.path and not keep_larger:
        print("\n>>> (可选) 默认情况下，如果 WebP 比原图大，脚本会忽略该文件")
        k_input = input("3. 是否强制保留体积变大的 WebP? (输入 y 保留，直接回车不保留): ").strip().lower()
        if k_input == 'y':
            keep_larger = True

    # 扫描任务
    extensions = ['*.png', '*.jpg', '*.jpeg']
    files_to_process = []

    print("\n🔍 正在扫描文件...")
    for ext in extensions:
        for p in source_dir.rglob(ext):
            if output_dir and output_dir in p.parents:
                continue
            # 将 keep_larger 传入参数元组
            files_to_process.append((p, args.quality, not args.delete, source_dir, output_dir, keep_larger))

    if not files_to_process:
        print("⚠️ 未发现可转换的图片文件。")
        return

    target_msg = f" -> {output_dir}" if output_dir else " (原目录)"
    keep_msg = "是 (强制格式统一)" if keep_larger else "否 (体积优先)"

    print(f"\n🚀 开始处理: {len(files_to_process)} 张图片")
    print(f"📂 来源: {source_dir}")
    print(f"📂 目标:{target_msg}")
    print(f"💾 强制保留大文件: {keep_msg}")
    print("-" * 30)

    with multiprocessing.Pool(processes=multiprocessing.cpu_count()) as pool:
        pool.map(convert_to_webp, files_to_process)

    print("-" * 30)
    print("✅ 所有任务已完成！")

    if not args.path:
        input("\n按回车键退出...")


if __name__ == "__main__":
    main()
```


# 7 参考资料

> [1] [TensorFlow GPU不可用，WSL2安装\_tensorflow wsl2\_坠星不坠的博客-CSDN博客 - https://blog.csdn.net/](https://blog.csdn.net/qq_40016005/article/details/130203903)
>
> [2] [人工智能实践：Tensorflow笔记\_北京大学\_中国大学MOOC(慕课) - https://www.icourse163.org/](https://www.icourse163.org/course/PKU-1002536002)
>
> [3]  [【Typora 教程】手把手教你如何用Typora撰写笔记 - https://www.bilibili.com/](https://www.bilibili.com/video/BV1h84y1Y7nn/?vd_source=436470546f64e53b7d4516956091ffd7)
>
> [4] [重装Ubuntu后开机停在Grub命令行的解决办法_ubuntu开机卡在命令行-CSDN博客 - https://blog.csdn.net/](https://blog.csdn.net/weixin_44481159/article/details/109240338)
>
> [5] [IMU和里程计融合_轮式里程计和imu融合-CSDN博客 - https://blog.csdn.net/](https://blog.csdn.net/baimei4833953/article/details/80768762)
>
> [6] [什么是IMU？-CSDN博客 - https://blog.csdn.net/](https://blog.csdn.net/su_fei_ma_su/article/details/125947605)
>
> [7] [一文了解IMU原理、误差模型、标定、惯性传感器选型以及IMU产品调研(含IMU、AHRS、VRU和INS区别)_imu寄存器值计算重力-CSDN博客 - https://blog.csdn.net/](https://blog.csdn.net/QLeelq/article/details/112985306?csdn_share_tail={"type"%3A"blog"%2C"rType"%3A"article"%2C"rId"%3A"112985306"%2C"source"%3A"Hong_J_0826"}&fromshare=blogdetail)
>
> [8] [ubuntu安装搜狗输入法，图文详解+踩坑解决-CSDN博客 - https://blog.csdn.net/](https://blog.csdn.net/qq_42257666/article/details/129098009)
>
> [9] [ubuntu系统安装好搜狗输入法后只能输入英文，无法输入中文的解决方案_ubuntu搜狗输入法无法输入中文-CSDN博客 - https://blog.csdn.net/](https://blog.csdn.net/qq_39779233/article/details/128086129?csdn_share_tail={"type"%3A"blog"%2C"rType"%3A"article"%2C"rId"%3A"128086129"%2C"source"%3A"Hong_J_0826"}&fromshare=blogdetail)
>
> [10] [ROS机器人学习——麦克纳姆轮运动学解算-CSDN博客 - https://blog.csdn.net/](https://blog.csdn.net/oXiaoLingTong/article/details/120198677)
>
> [11] [ROS从入门到精通系列（五）catkin详解与catkin_make编译-CSDN博客 - https://blog.csdn.net/](https://blog.csdn.net/hhaowang/article/details/101691986)
>
> [12] [2D激光slam四种算法建图效果对比_slam建图算法-CSDN博客 - https://blog.csdn.net/](https://blog.csdn.net/m0_73791170/article/details/127339058?csdn_share_tail={"type"%3A"blog"%2C"rType"%3A"article"%2C"rId"%3A"127339058"%2C"source"%3A"Hong_J_0826"}&fromshare=blogdetail)
>
> [13] [关于重装电脑碰到的BUG及其修复教程_verification failed:(0x1a)-CSDN博客 - https://blog.csdn.net/](https://blog.csdn.net/Sco_ohhG/article/details/135394506)
>
> [14] [ROS—PGM地图文件的编辑 | 闫金钢的Blog - https://yanjingang.com/](https://yanjingang.com/blog/?p=8597)
>
> [15] [Ubuntu22.04 系统添加中文输入法 - zensi - 博客园 - https://www.cnblogs.com/](https://www.cnblogs.com/zensi/p/17725119.html?_refluxos=a10)
