# 创建Mixin机器人

因为隐私原因，有些场景最好是用户自己创建一个机器人去获取一些信息，比如获取自己的所有转账记录，获取多签地址余额等，这是一篇创建一个Mixin机器人的保姆教程，帮助缺少一些计算机知识的朋友创建一个Mixin机器人。

这是一篇文章，有可能的话如果内容不适用了，会持续更新，作为一篇基础文章可以方便被大家引用。

里面的内容不能帮助您搞懂是什么？为什么？能帮助您实现Mixin机器人运行起来。

文章以Windows为例，其他操作系统类似。

------

[TOC]

------

## 需要使用到的工具

* VSCode
* Nodejs

## 1.工具准备

### 1.1.安装VSCode

VSCode是一个写代码的工具，我们需要在这个软件中，编写代码。

在VSCode[官方网站](https://code.visualstudio.com/)下载VSCode安装包，点击下图中的”Download for Windows“按钮开始下载。

![image-20230130150035125](C:\Users\vwumumu\Desktop\coding\初始化Mixin机器人.assets\image-20230130150035125.png)

下载后，双击打开安装包，一路点击下一步，按照默认选项安装。

### 1.2.安装Nodejs

在Nodejs[官方网站](https://nodejs.org/zh-cn/)下载安装包，点击下图中绿色按钮，如”18.13.0长期维护版“开始下载。

![image-20230130150518160](C:\Users\vwumumu\Desktop\coding\初始化Mixin机器人.assets\image-20230130150518160.png)

双击打开下载后的安装包，一路点击下一步，完成安装。

## 2.准备Mixin机器人
### 2.1.登录Mixin开发者后台

首先，我们需要登录开发者后台。

通过浏览器，访问：https://developers.mixin.one/dashboard，会弹出如下页面。

![image-20230130143553857](C:\Users\vwumumu\Desktop\coding\初始化Mixin机器人.assets\image-20230130143553857.png)

用Mixin Messenger扫描网页中的二维码，就可以进入到下面的页面：开发者后台。

页面中，左侧我的应用列表中显示的就是您的Mixin账号的Mixin机器人，点击某个具体的机器人，就可以开始配置。

![image-20230130143643963](C:\Users\vwumumu\Desktop\coding\初始化Mixin机器人.assets\image-20230130143643963.png)

### 2.2.填写Mixin机器人信息

如下图，点击”我的应用“列表中的机器人，默认就会进入机器人的”信息“标签页，需要填写一些基本信息，可以下面的信息，填写完成后，点击页面底部的保存按钮，**记下来您的机器人Mixin ID**，在Mixin Messenger中添加这个机器人。

![image-20230130144528327](C:\Users\vwumumu\Desktop\coding\初始化Mixin机器人.assets\image-20230130144528327.png)

### 2.3.获取Mixin机器人密钥

要想能利用机器人去做事情，需要拿到机器人的控制权，拥有机器人密钥的人，就拥有机器人的控制权。

如下图，点击”密钥“标签页，然后点击蓝色的”Ed25519私钥“按钮，生成该机器人的私钥信息

![image-20230130145139696](C:\Users\vwumumu\Desktop\coding\初始化Mixin机器人.assets\image-20230130145139696.png)

接下来，点击弹出窗口的”是的“按钮，重置（生成）机器人的私钥信息：

![image-20230130145206387](C:\Users\vwumumu\Desktop\coding\初始化Mixin机器人.assets\image-20230130145206387.png)

然后，如下图，点击复制按钮将生成的私钥信息复制并保存下来，或直接点击下载按钮，下载一个文件名后缀为json的文件，这些信息我们后面会用到。

![image-20230130145315190](C:\Users\vwumumu\Desktop\coding\初始化Mixin机器人.assets\image-20230130145315190.png)

再次强调，只要拥有了机器人的私钥信息，就拥有了机器人的控制权，只要再生成一次新的私钥信息，旧的私钥信息就失效了。

## 3.初始化机器人

打开Windows PowerShell，按 键盘上的`Win`+`R`组合键，然后在弹出的运行窗口中，输入`powershell`后回车

![image-20230130153914963](C:\Users\vwumumu\Desktop\coding\初始化Mixin机器人.assets\image-20230130153914963.png)

然后打开如下的窗口，`PS C:\Users\vwumumu>`为我们当前所在的目录，就像在我的电脑中打开某个文件夹是一样的，命令行通过这种新式，显示了我们当前处于哪个文件夹：

![image-20230130153940374](C:\Users\vwumumu\Desktop\coding\初始化Mixin机器人.assets\image-20230130153940374.png)

> Windows PowerShell是Windows平台的命令行工具

### 3.1.创建目录并初始化

如下图，通过`mkdir multisig`命令，在当前目录（`PS C:\Users\vwumumu`）下面创建一个名为`multsig`的文件夹，然后通过`cd multisig`命令，将命令行切换到`multsig`目录：

![image-20230130154022834](C:\Users\vwumumu\Desktop\coding\初始化Mixin机器人.assets\image-20230130154022834.png)

执行`npm init -y`，初始化这个目录，我们后面就开始在这个目录下面写代码了

![image-20230130153844173](C:\Users\vwumumu\Desktop\coding\初始化Mixin机器人.assets\image-20230130153844173.png)

### 3.2.安装 mixin-node-sdk

执行`npm install mixin-node-sdk`，安装`mixin-node-sdk`:

![image-20230130154330607](C:\Users\vwumumu\Desktop\coding\初始化Mixin机器人.assets\image-20230130154330607.png)

执行`code .`用`vscode`打开当前目录，可以看到里面有一个名为`node_modules`的文件和名为`package-lock.json`和`package.json`的两个文件：

![image-20230130154610387](C:\Users\vwumumu\Desktop\coding\初始化Mixin机器人.assets\image-20230130154610387.png)

### 3.3.初始化Mixin机器人

点击新建文件图标，创建一个名为`index.js`的文件：

![image-20230130155011620](C:\Users\vwumumu\Desktop\coding\初始化Mixin机器人.assets\image-20230130155011620.png)

将下面的内容复制粘贴到`index.js`文件内，其中`new BlazeClient({xxx},{parse: true, syncAck: true });`是前面生成的机器人私钥，如果找不到了，再去开发者页面生成一份即可，至此，机器人就准备好了。

```js
const { BlazeClient } = require("mixin-node-sdk");
const client = new BlazeClient(
  {
    pin: "975262",
    client_id: "b339c419-305a-492d-af4e-85a127305f85",
    session_id: "431e9d82-2a7e-4a88-ae62-fdef10bac0fc",
    pin_token: "slt8tiFJSPpvNyqD1oDgtKErBxiduls85Nag1_3XcQ8",
    private_key:
      "r5qH3113MubFdUwZWyYkj6j7jkwaeBdNFX-abahbwi7RgkBarUz8Rd2_hXYlHj3KglFItT-qpfTRAhhyvZS6Sg",
  },
  // 上面{ }内的信息替换成您自己Mixin机器人的私钥信息
  { parse: true, syncAck: true }
);

client.loopBlaze({
  onMessage(msg) {
    client.sendMessageText(msg.user_id,"我的第一个Mixin机器人")
  },
});
```

## 4.让机器人动起来

在命令行中执行`node index.js`，光标会呈现一个闪烁的状态：

![image-20230130155845114](C:\Users\vwumumu\Desktop\coding\初始化Mixin机器人.assets\image-20230130155845114.png)

跟您的机器人打个招呼：

![image-20230130160018873](C:\Users\vwumumu\Desktop\coding\初始化Mixin机器人.assets\image-20230130160018873.png)

至此，您的机器人就运行起来了，给它发任何消息，它都会回您这句话：“我的第一个Mixin机器人”。

希望对您有帮助，如果有任何问题，可以来我的小密圈交流：7000104210
