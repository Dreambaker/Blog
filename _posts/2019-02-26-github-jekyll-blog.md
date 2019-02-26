---
layout: post
title:  "使用树莓派将有线打印机共享为网络打印机（惠普p1108）"
date:   2019-02-26 21:41:45 +0800
categories: share
---

#### 1.下载驱动

&#8195;&#8195;打开树莓派的控制台，输入：  

&#8195;&#8195;&#8195;&#8195;`sudo apt-get install hplip`  

&#8195;&#8195;之后还需要安装plugin,输入：  

&#8195;&#8195;&#8195;&#8195;`sudo hp-plugin`

#### 2.安装cups
&#8195;&#8195;安装和启动步骤如下
```  
$ sudo apt-get install cups

更改配置文件部分参数如下：

$ vi /etc/cups/cupsd.conf
.... listen localhost 改成 0.0.0.0 ....


# Restrict access to the server…

<Location />

Order allow,deny

Allow @Local    //添加此项

</Location>

 

# Restrict access to the admin pages…

<Location /admin>

Order allow,deny

Allow @Local

</Location>

 

# Restrict access to configuration files…

<Location /admin/conf>

AuthType Default

Require user @SYSTEM

Order allow,deny

Allow @Local

</Location>
```
 

保存，退出cupsd.conf。  

重新启动cups服务：  

$ sudo service cups restart

#### 3. 使用 cups
访问 https://树莓派IP:631 正常的话可以看到 cups 服务页面

接下来点击 Manage Printers 查看是否已经存在一个打印机了（因为之前我们按照了 hplip 驱动）

如果没有的话可以在之前的页面点击 Add Printer 添加一个（选择带有usb字符的那个），具体添加步骤很简单就不赘述了

点击已有的打印机，选择 Modify Printer

如果 Sharing 没有勾上的话，勾一下，一点要保证打印机是处于分享状态的就 ok 了


你可以在这个网页上多探索一下，这里可以管理和配置你的打印机。
#### 4.无线打印
掏出手机随意选择一张照片，点击 打印
选择打印机时会看到局域网上的这台 HP_DeskJet1110，完成打印



