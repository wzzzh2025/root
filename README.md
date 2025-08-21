# root
### 开始前的准备

1.打开设置->我的设备->全部参数和信息->连续点击os版本多次，直到提示“你现在已处于开发者模式”

2.接着来到更多设置->开发者选项，找到usb调试和usb安装 并打开

<img width="1406" height="112" alt="image" src="https://github.com/user-attachments/assets/78dd0109-c53b-4889-88da-3c6330454953" />

### 绑定

`miui`系统

`miui`系统直接绑定即可，操作起来不是很麻烦

#### 澎湃系统

1.首先，需要将旧版设置安装到设备中

```bash
adb install setting.apk  
```

<img width="1280" height="1993" alt="image" src="https://github.com/user-attachments/assets/06c0431f-20b7-4cc8-afc9-d8255e4a0520" />


2.接着打开`bypass.cmd`（`windows`环境），会跳转到绑定账号的界面，点击绑定即可，这里手机中会提醒让去小米社区升级什么的，不用管，只需要看`bypass.cmd`打开的`cmd`，里面只要提示绑定成功了就行

<img width="795" height="1272" alt="image" src="https://github.com/user-attachments/assets/a12ccee5-16d8-4067-9937-69ed1a9a8ca2" />


<img width="1730" height="924" alt="image" src="https://github.com/user-attachments/assets/52f69df3-9ba1-4e08-8b48-5058e79768d7" />


3.然后可以打开小米解锁工具，登录本机的小米账号（这一步的步骤都是在验证是否绑定成功了，正常上面两个步骤就已经能够绑定成功了，具体的操作可参考下面的解锁部分）

之后会提醒让进入到`bootloader`中去，用下面这个命令

```bash
adb reboot bootloader
```

等待连接上之后，尝试解锁，如果出现"设备与账号绑定时间不足。。小时"则表明绑定成功

### 解锁

绑定满七天之后就可以解锁了

这里澎湃和`miui`系统的操作都是一样的

1.打开小米解锁工具并登录

<img width="1230" height="840" alt="image" src="https://github.com/user-attachments/assets/9c25c7b4-7041-4668-8fba-684c0de0bfb4" />




2.登录进来是这样一个界面，提示让进入`bootloader`模式后再连接手机，我们可以按照他的提示去手动操作，也可以直接在终端输入这句命令

```bash
adb reboot bootloader
```

<img width="1230" height="840" alt="image" src="https://github.com/user-attachments/assets/84d152a7-00a4-4346-8397-2a30a5458168" />


3.直接点击解锁即可<img width="1230" height="840" alt="image" src="https://github.com/user-attachments/assets/4542241f-5354-402c-9b52-2e7b0f8fd3cf" />


4.这里出现解锁成功说明就已经成功了，设备会自动重启

<img width="1230" height="840" alt="image" src="https://github.com/user-attachments/assets/bc8d18d6-0082-4e68-9e2c-55dbec7a4991" />


解锁这一步相当于给系统刷机了，所以小米账号等等....都需要重新去登录

包括usb调试也需要重新去打开（参考开始前的准备）

### `Root`

如果已经有修补过的镜像了，那么2、3这三部就不需要了，这里澎湃1.10刷1.06的镜像也是没有任何问题的、甚至说刷miui的镜像都没问题（所以刷错了也没关系，真不行了就再刷一遍正常的回去就行了），所以2 、3步是可以跳过的



1.将`root apk magisk` 安装到手机中去

```bash
adb install magisk.apk
```

2.到 https://xiaomirom.com/rom/redmi-pad-se-xun-china-fastboot-recovery-rom/ 这个网站寻找对应`os`版本的镜像包，下载解压是一个文件夹

`->images->init_boot.img`

`push`到手机中去

```bash
adb push init_boot.img /sdcard
```

3.在`magisk` 中修补之前的`init_boot.img` 镜像

点击`magisk` 附近的安装，一步一步跟进去即可，最后选择之前的`init_boot.img`，开始修补，会产生一个修补后的镜像，大概是在`/sdcard/download`这个路径下，先`pull`到电脑中去

```bash
adb pull /sdcard/download/mag....img
```



4.开始`root`  **(如果已经有修补过了的镜像的话前2、3部可以省略)**

先进入到`bootloader`

```bash
adb reboot bootloader
```

接着刷入之前`pull`到电脑上的镜像或者是已经准备好了的镜像

```bash
fastboot flash init_boot mag.....img
```

5.刷入成功后用以下命令重启设备

```bash
fastboot reboot
```

<img width="1552" height="230" alt="image" src="https://github.com/user-attachments/assets/723ccad4-2b8c-4a65-8194-fc57c1b069fb" />


### 安装`losped`

1.先把`losped` push到手机中去

```bash
adb push losped.zip  /sdcard
```

<img width="1680" height="63" alt="image" src="https://github.com/user-attachments/assets/7caac17d-387e-4271-bf03-3a50e41e23f8" />


2.进入到`magisk`中，如果是直接刷的镜像的话，可能会有下面的提示，点击确定即可

<img width="795" height="1272" alt="image" src="https://github.com/user-attachments/assets/8758a1aa-8dac-4606-8d9a-4a2a249c1760" />


3.先在主页的设置中找到`zygisk`并打开，打开后会提示重启后生效，我们先不去重启，我们先把所有需要的东西都加载进来之后再去重启，这样节省一点时间

<img width="795" height="1272" alt="image" src="https://github.com/user-attachments/assets/ad0076b3-2e0d-4f72-8193-1069345040e2" />




4.接着点击底部最右边的 模块->从本地安装，点进去后将`push`进来的`losped`加载进来，然后右下角会有重启按钮，点击重启

<img width="795" height="1272" alt="image" src="https://github.com/user-attachments/assets/e30d7a22-aa69-47a8-9027-118a7da56495" />


<img width="795" height="1272" alt="image" src="https://github.com/user-attachments/assets/44591eeb-ce32-43d2-84c7-c5770be835fe" />


5.为`lspoed`创建快捷方式 （这一步只是为了方便，这样桌面就会有losped的快捷方式了，不然每次都需要去状态栏打开）

向下滑来到状态栏，点击这里打开lsposed

<img width="795" height="1272" alt="image" src="https://github.com/user-attachments/assets/aae0070f-54a5-43e1-9f99-8f1f63d23d23" />


进去后会有一个弹窗提示创建快捷方式，点一下

如果手快了没点到，可以到设置中去手动打开

<img width="795" height="1272" alt="image" src="https://github.com/user-attachments/assets/00f378a2-efd9-40e4-85f3-4ed69ece0088" />


### 安装监听工具

```bash
adb install 摸鱼社区.apk
```

安装进来之后顶部大概率就会弹出来一个框，说模块未激活，点进去激活模块，给小红书权限即可

<img width="795" height="1272" alt="image" src="https://github.com/user-attachments/assets/d9490f2f-8bfe-4264-8e47-c98dc1d2b78b" />


### 给工具`root`权限

打开小红书登录账号后用其他设备往账号中发送一条私信，当设备第一次接收到信息时会弹出来一个框让给小红书`root`权限(默认10秒后自动拒绝)，这里允许一下。

如果没来的及给的话，打开`magisk` ，点击底部第二个超级用户，把小红书的权限打开就可以了
