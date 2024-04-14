#root #fakelocation
### 前提准备
1. 支持解锁bootload的手机
	- 目前支持的机子有小米、红米、三星、摩托罗拉、一加，以及OPPO和真我的部分机子
	- 小米解锁需要考试，极难，且会掉主板之类的保修，但作者实测，仍可以保修期间免费更换烧了的屏幕，请自己注意。
	- 其他厂商可能存在熔断、拒保的问题，请自行查看自己机子情况。
2. 系统在A14以前，但不要太老
	- 作者在A14上无法使用。
	- 太老的系统无法保证能有效，建议在A10或A9左右。
3. sim卡能用的手机（或者支持esim，esim请自行办理）。
4. windows/mac/linux电脑
### 具体步骤
#### 1.解bl锁（已解锁可跳过，以小米为例）
前往小米社区->底栏\[官方\]->内侧申请->BL解锁申请    
![[1713014436250.jpg]]
![[1713014436256.jpg]]
通过后，前往设置->我的设备->全部参数->疯狂点击OS/MIUI版本，直到提示“您现在处于开发者模式！”
![[1713014436244.jpg]]
随后前往，更多设置->开发者选项->设备解锁状态->绑定账号和设备，根据提示绑定账号和设备,回到开发者选项，打开usb调试。
前往绑定页面小米提供的[网址](https://unlock.update.miui.com),点击立即解锁->解锁工具下载。
![[Pasted image 20240413213139.png]]
下载后解压，打开\[miflash_unlock],登录。
手机关机，按住下音量和关机键，，进入fastboot模式，此时手机上会有fast boot的英文，老机型会有上图的米兔干安卓机器人标志。找根数据线，连接电脑，点击解锁，一路确定，切忌断开连接。等待自动完成重启即可，如重启时屏幕上方带有解锁标志即为成功。
##### 注意
1. 解锁会清除数据，请自行备份。
2. 小米的答题很麻烦。
3. 其他品牌机型请自行查找方法。
4. 回退版本和线刷可以用小米线刷工具，[系统包和线刷工具在这](https://xiaomirom.com/)。
5. 当然，也有其他办法，强行解锁，自行探索。
#### 2.刷入root管理器（magisk为例，已获取root的可跳过）
##### 方法1：提取boot安装（不推荐）
下载自己机型当前系统版本的系统包，解压后，部分机型可以看到boot镜像文件。如果没有，请自行搜索如何提取，本文不再讲解。
安装magiks[官方连接](https://github.com/topjohnwu/Magisk/releases)下载最新版，我个人推荐alpha版，但此文章不提供连接。安装此应用，打开，如图，点击安装，选择修补一个文件，选择所提取的boot文件，等待修补完成后，关机，进入fastboot。
![[f536570faaca55ab1eb675ec2424ba98.jpg]]
连接电脑，使用fastboot命令或者可视化工具刷入，具体请自行搜素。
##### 方法2：刷入rec后刷入
###### 1.刷入rec
建议在twrp[官网]([TeamWin - TWRP](https://twrp.me/)),橙狐[官网]([OrangeFox Recovery Downloads](https://orangefox.download/zh-CN))，以及酷安找自己机型和系统的rec。
手机进入fastboot模式，用数据线连接电脑。将rec刷入，这里要注意是否为ab设备，以及手机是否有REC分区。
1. 有rec分区或onlyA设备
```adb
fastboot flash recovery recovery.img
```
2. AB设备且无rec分区
没刷过，我不会，建议看[酷安教程](https://www.coolapk.com/feed/38141442?shareKey=NmQ2Mjk2MGViN2Y1NjYxYWE4ZWU~&shareUid=3381997&shareFrom=com.coolapk.market_14.1.0)

当然，你也可以使用可视工具刷入，如搞机助手。
输入后按住上音量键+关机，即可进入rec。
进入rec后，会有密码，密码是你锁屏密码，twrp需要右滑块进入。
将rec文件拷到手机中，选择安装->找到文件刷入（如果是镜像img文件，可能需要点击镜像刷入，才能找到刷入），或者高级->刷入当前rec。之后回到主界面，重启，选择重启到rec。
###### 2.安装magisk
之后将下下来的面具的安装包拷到手机上，rec中点击安装，找到并刷入，apk格式，选择系统包，是可以刷入的，如果找不到，请重命名后缀改为zip。刷完后重启系统。
进入系统后，找到面具的apk安装包，点击安装。之后就能找到一个面具图标的软件。
![[Pasted image 20240414000204.png]]
点进去，提示你要修复，确定，直接安装，安装完直接重启即可。
![[3fcf5f8ef3ecee029774756772b3f9ee_720.jpg]]
##### 注意
- 由于考虑到设备较老，本篇只讲magisk，如果您有能力，且设备较新，建议使用kernel su[官方]([tiann/KernelSU: A Kernel based root solution for Android (github.com)](https://github.com/tiann/KernelSU))的方式。更有效。
#### 3.隐藏ROOT
- 由于闪动校园会检测，故需要隐藏root。
##### 需要用到的文件
LSP[官方]([LSPosed/LSPosed: LSPosed Framework (github.com)](https://github.com/LSPosed/LSPosed))，请注意下载Zygisk版
Shamiko[官方]([Releases · LSPosed/LSPosed.github.io](https://github.com/LSPosed/LSPosed.github.io/releases))
ZygestNext[官方]()
##### ksu的隐藏
- 如果您使用的是kernel su，点击底栏\[模块]->安装，请安装以下模块(下载的zip文件)，重启即可。
![[Pasted image 20240414111357.png]]
##### magisk隐藏
- 如果您使用的是面具，请使用此方案。 
进入magisk，点击右上角的齿轮，点击隐藏magisk，默认的名字，确认即可。随后面具会退出，桌面上会多一个，和你定的名字同一个的软件，且封面为小机器人。
![[0c1590497298922227ea264195fc7cba.jpg]]
点击进入，随后点击右上角的齿轮，将Zygisk打开，重启。
重启后，再次进入Magisk，点击底栏\[模块]->从本地安装，安装如下模块(下载的zip文件)，重启。
![[d9034ebc15179fb8352777714780c0ec.jpg]]
重启后，再次进入Magisk，点击右上角的齿轮->配置排除列表->搜索[闪动校园]->全部开启。
![[Pasted image 20240414121109.png]]
![[Pasted image 20240414121251.png]]
#### 开始跑步吧
##### 准备如下
- 以上步骤已完成
- 手机插上卡（或者eSim），可联网。
- 安装Fake Location [官方]([Lerist/FakeLocation: Fake Location (github.com)](https://github.com/Lerist/FakeLocation))
##### 1.打开Fake Location，测试是否成功
点击左上角，打开菜单，登录账号，购买会员(一个月就9块，BTM买不起)。
会员到账后，回到主页，点击图示内容，选择一个地方，启动模拟。
![[Pasted image 20240414122213.png]]
选择启动方式为root模式，点击确定，出现授权root弹框，点确定即可，如果无法授权，进入magisk/kernel->底栏[超级用户]->找到Fake Location，ksu需要点击进去，打开超级用户，magisk直接打开即可。
![[Pasted image 20240414122510.png]]
![[Pasted image 20240414123346.png]]
![[Pasted image 20240414123530.png]]
![[1713069284401.jpg]]
此时重新点击选择一个地方，点击启动模拟
![[Pasted image 20240414124108.png]]
成功后会有如下提示，且按钮会变为\[停止模拟]。
![[Pasted image 20240414124013.png]]
然后开启缺德地图等地图软件，查看是否模拟成功。
![[Pasted image 20240414124220.png]]
##### 2.模拟跑步
正常打开闪动校园，开始跑步，先暂停。
打开Fake Location，点击左上角菜单，点击加号，按照闪动校园的要求设计路线。
![[Pasted image 20240414124700.png]]
![[Pasted image 20240414124708.png]]
###### 功能键作用介绍（上到下）：
- 切换地图背景，卫星图还是路线图，建议卫星。
- 撤销，万一规划错了，回到上一步。
- 点击第一次地图出现同符号标志，即可开始规划路线（注意是直线，别当超人穿墙和房子）。
- 定位你当前的位置
- 确认你的设置路线。
设计完路线，回到原页面，设置好速频，建议3.5，开启步频模拟和速度浮动。启动模拟。
回到闪动校园，继续跑步。
跑步要求的点位可能会变化，点击此处，继续延长线路即可。
![[Pasted image 20240414125627.png]]

### 完结
- xiangyu编写。
- 感谢相关开发人员
