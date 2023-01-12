# 如何完成本文档的协作

### Fork 仓库到你自己的Github账号



### 将 项目 克隆到你的本地

``` bash
git clone git@github.com:xxx/mixchat-docs.git
```

xxx是你的Github账号

### 编辑文档

打开克隆到本地的文件夹，在目录docs下，可以看到网站上显示的文件。

编辑其中的md文件，每个md文件都已下面的内容开始，后面就是文档的正文部分，使用markdown语法即可。
下面的内容对应着文档在网站侧边栏显示的顺序，`1`就是排在第一个显示，`2`就是排在第二个显示，以此类推。

``` bash
---
sidebar_position: 1
---
```

文件夹通过`_category_.json`文件控制文件夹在侧边栏显示的顺序，比如`en`是英文文档，其`position`的值为`2`，则排在侧边栏第2个显示。

文件夹内的每个文档同理，决定该文档在文件夹内的排序。

### 本地查看

在本地的命令行中，mixchat-docs目录下，执行下面的命令，会通过本地浏览器打开网站，预览合适后就可以提交至Github中。

``` bash

yarn run start

```

### 上传到Github

``` bash
git add .
git commit -m 'update'
git push
```

### 将更新提交给Mumu Wu

