---
title: Typora+picgo+oss快速搭建hexo博客图床
tags:
  - 踩过的坑
  - typora
  - picgo
  - oss
categories:
  - Tutorial/Error/Fix
abbrlink: d9ee7cbb
date: 2022-10-07 08:41:43
---





### 目录

>准备工作
>
>* Picgo下载
>* OSS对象储存服务开通
>
>图床配置
>
>* Typora配置
>* Picgo配置
>
>测试上传情况

很长一段时间没有更新博客了，听说Typora收费了，幸好我的版本从来没更新过哈哈哈哈

![image-20221007103457780](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007103457780.png)

------------------

但是呢，这次又遇到了一个问题，之前搭建的smms图床不能用了，怎么调试都没办法，之前崩了之后只要更新下API  key 就行了，这次怎么更新都没有用，可能是smms也开始收费了。

当你上传时候出现这个问题的时候，那就说明你的图床崩了。

![image-20221007085519282](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007085519282.png)

打开`文件`—`偏好设置`-`图片`，我们会看到这个选项。

![image-20221007090126052](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007090126052.png)

点击`验证个图片上传选项`，验证一下图片上传。

```shell
[PicGo INFO]: Before transform
[PicGo INFO]: Transforming...
[PicGo INFO]: Before upload
[PicGo INFO]: Uploading...
[PicGo WARN]: failed
[PicGo ERROR]: RequestError: Error: connect ECONNREFUSED 104.21.83.45:443
```

恩。。确实是崩了。

接下来我们就利用picgo+oss搭建一个图床供typora使用。



### 准备工作



#### picgo下载

首先我们前往Github主页下载picgo最新版本  

[Picgo](https://github.com/Molunerfinn/PicGo/releases)

![image-20221007104038135](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007104038135.png)



如果不会科学上网的这里还有一个腾讯COS的下载链接

[Picgo-TecentCOS](https://picgo-1251750343.cos.ap-chengdu.myqcloud.com/2.3.1-beta.6/PicGo-2.3.1-beta.6.AppImage)



下载好之后执行以下指令

```shell
sudo chmod a+x PicGo-2.3.1-beta.6.AppImage   #权限
sudo mv PicGo-2.3.1-beta.6.AppImage picgo#重命名
sudo mv picgo /usr/bin #该目录已包含于环境变量，可直接通过picgo指令打开
```



打开之后它是这样的

![image-20221007104113254](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007104113254.png)

你得右键打开主界面

![image-20221007104134513](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007104134513.png)



#### OSS云对象储存服务

**打开阿里云** 

[阿里云]: https://cn.aliyun.com



**搜索对象储存oss**

![image-20221007104246741](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007104246741.png)



**切换至概况一栏**

![image-20221007104334529](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007104334529.png)

**点击建立bucket**

![image-20221007104441930](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007104441930.png)

**# 上图源自CSDN，本人懒**



**切换至bucket概览，记录下你的地域节点** 

![image-20221007104523311](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007104523311.png)我这里是广州，所以是`oss-cn-guangzhou`



**右上角点击你的头像选择AccessKey管理**

![image-20221007104545235](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007104545235.png)

这个不用管他，继续使用

![image-20221007101544965](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007101544965.png)



**创建一个新的Access key，然后记住你的ID和Secret**

![image-20221007101612928](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007101612928.png)



到这里oss服务就配置完成了，接下来我们就可以开始在本级搭建图床了。



### 图床配置



#### Picgo配置

**打开picgo主界面，点击`图床设置 `- `阿里云oss`**

![image-20221007102114993](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007102114993.png)

这里的keyID和keySecret填写刚才我们建立AccessKey时候得到的两串代码，Bucket填写你建立的bucket名字，储存区域就填写刚才的地域节点，储存路径这个，随便写一个就行了。



#### Typora配置

同样，打开`文件`-`偏好设置`-`图片`

![image-20221007102515260](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007102515260.png)

将上传服务由Picgo-commandline改为Picgo-app，而后Picgo路径填写我们刚刚移动Picgo

到达的位置`/usr/bin/picgo`



### 测试上传情况

点击验证图片上传情况

```shell
{"success":true,"result":["https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/typora-icon2.png","https://xxx.oss-cn-guangzhou.aliyuncs.com/image/typora-icon.png"]}
```

成功。