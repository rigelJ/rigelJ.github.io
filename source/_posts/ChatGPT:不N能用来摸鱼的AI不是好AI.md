---
title: 'ChatGPT:不能用来摸鱼的AI不是好AI'
tags:
  - ChatGPT
  - Markdown
  - PPT
categories:
  - Talk
cover: img/myimage/ChatGPT_buneng.png
abbrlink: 2f0634a9
date: 2023-04-27 20:13:08
---

# ChatGPT: 不能用来摸鱼的AI不是好AI


最近ChatGPT的大火，使得很多的行业面临大洗牌，很多人都说要被GPT优化了，本来咱这个职业吧，跟ChatGPT可以说是八竿子打不着，无非也就是当个电子宠物玩玩。

不过最近在少数派看了篇文章，说可以用chatGPT直接生成markdown文档，再把markdown文档转为PPT演示文稿.....

诶这我就来兴趣了。

这多好的摸鱼工具阿，以后什么政治教育，双争教育，爱国主义教育，直接一步到位，还费心思写什么稿子，做什么ppt，这好哇，这可太好了。

但同时我也对其实现的可能性存在一定的质疑，主要在两方面：

> 1. chatGPT真的能实现一篇逻辑清晰，层次分明的文章么？
> 2. Markdown文件转为PPT的可行性有多少?

于是我分别就这两个问题进行了探究。



## ChatGPT实现文章撰写



### chatGPT的部署与使用

网络上有很多种方式可以部署chatGPT，有些是客户端，有些是网站部署，这里推荐Github上两个最主流的项目

> ChatGPT-Next-Web   ChatGPT Desktop Application



#### ChatGPT-Next-Web 

> [ChatGPT-Next-Web](https://github.com/Yidadaa/ChatGPT-Next-Web) 这个项目是利用使用 Vercel 一键部署的Next.js项目，可以直接fork原项目后，将自己仓库的rep部署到vercel，简便可靠。

部署主要有以下几个步骤。

首先，我们要登录openai网站获取OpenAI API key



**第一步**：挂上梯子，这里推荐[灯塔 Cloud ](https://dt666.xyz)，可选择的线路比较多，可及时更换。
![image-20230427201916557](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20230427201916557.png)



**第二步**：注册账号，并登录openAI官网，看似很简单，实则到处都是坑。

> ！如果注册输入邮箱后，出现这个提示，说明这个邮箱被OpenAI拒绝注册了，目前QQ邮箱,foxmail邮箱，163邮箱，网易邮箱yeah.net，126邮箱，新浪邮箱，Outlook、hotmail邮箱，eud.cn邮箱以及其他以.cn结尾的邮箱全部都不能注册了 ，最好的办法就是注册一个Google账号，直接快捷登录。
>
> ![image-20230427202043393](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20230427202043393.png)

> ！如果输入跳转后提示 OpenAI’s services are not available in your country 说明你所在的地区不被允许登录，目前香港和台湾代理用不了的，最好用韩国或者北美的线路。
>
> ![image-20230427201947140](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20230427201947140.png)

> ！登录的时候，又有一个手机号验证的过程，看了崔大的博客找到一个方法，可以花一块钱到[sms-active](https://sms-activate.org)买一个手机号接收验证码。
>
> ![image-20230427202001048](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20230427202001048.png)
>
>
> 把手机号输入进去，就能通过手机验证了。



**第三步** 获取openAI api key

登录API keys - [OpenAI API](https://platform.openai.com/account/api-keys)，点击`View api key`查看账号Api key，自己新建一个然后保存。
![image-20230427202157143](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20230427202157143.png)



**第四步** 将项目部署到Vercel上

参考ChatGPT-Next-Web(https://github.com/Yidadaa/ChatGPT-Next-Web)项目自带的中文说明，大概就是创建一个项目，然后输入API Key 和 配置密码code，点击部署，完成。

![image-20230427202207102](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20230427202207102.png)

然后打开项目就可以使用了。

![image-20230427202216433](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20230427202216433.png)

说实话UI界面做的还挺好看的。



**补充** 给网站挂上域名

由于versel生成的地址太复杂而且很难记，为了简便使用我们可以给它挂个域名。

（域名最近出了点问题，自己看教程吧）



#### ChatGPT Desktop Application
> [ChatGPT Desktop Application](https://github.com/lencx/ChatGPT) 这个项目是一个多平台的客户端，可以实现很多网页浏览器不能实现的功能，直接下载使用。

下载就完事了，注意一下版本不要下错了，windows 是msi文件，linux是deb文件,以windows为例，登录后界面是这样的

![image-20230427202236458](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20230427202236458.png)

### chatgpt功能测试

作为一个经常需要做PPT(hu nong ling dao)的小排，我就直奔主题了，这次，我们来看看chatGPT能不能给我直接实现一篇markdown的教案。

话不多说，开搞。

首先我问了他这样一个问题。
![image-20230427202249271](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20230427202249271.png)

他的回答是这样的
![image-20230427202254794](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20230427202254794.png)

还行，但是感觉这个分点有点乱，正常我们上个教育一般都是分三个大点，然后每个大点里面再分三四个小点，这种层次的布局会更适合授课。

于是我调整了一下思路，给他设定了一下范围，并且给出了每个大点围绕的具体内容。

这是GPT的回答。
![image-20230427202312249](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20230427202312249.png)

我简直可以拍手叫绝了，这个结构完完全全已经符合授课的要求了，如果能够再润色一下语言，那么这绝对是一篇牛逼的稿子。

总的来说，ChatGPT虽然不能直接给出一篇优秀的稿子，但是可以给我们的写作提供思路，比如如果你想写一篇关于挫折的文章，你就可以这样来收集信息

![image-20230427202320460](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20230427202320460.png)

![image-20230427202323843](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20230427202323843.png)

如果临时进行演讲，这将成为一个极其高效的工具。



## 实现Markdown-PPT转换



### Mindshow.fun

简单看了下Mindshow这个软件，号称可以直接将markdown转换为ppt，于是我就先拿这个软件来开刀了。

这个软件覆盖的平台还蛮多的，从MacOS到Linux都覆盖了，开发者也是野心相当的大，还几乎处于测试阶段就全覆盖平台。

为了方便，我下了个windows的用，因为一般干工作上的活都是用的windows，写代码才开linux。

打开界面如下，导入的话可以选额md，word还有幕布格式。

![image-20230427202339958](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20230427202339958.png)

我们选择md格式，稍微调整了一下位置，我们把他下载下来看看效果。

> ！第一个问题：兼容性不太好，wps显示数字就会乱码
>
> ![image-20230427202347507](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20230427202347507.png)

我们再来看看布局和页面有没有问题，看了一下效果，觉得还是比较满意的，每个插入的模块不管是图片还是文字都是可以拖动更改的而不是图片，这点做的很不错。

> !但是有个问题就在于，每个页面没有把最大的标题加上，这样看起来显得逻辑性不好，而且也不便于讲解者理清思路，他给出的模型是这样的
>
> ![image-20230427202354321](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20230427202354321.png)
>
> 这里有几个问题，我标记出来了
>
> ![image-20230427202402376](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20230427202402376.png)
>
> > 第一个问题，不需要数字标记的小点符号
> > 第二个问题：正常我们每个页面除了本级的小标题还应该有个上级的大标题，这里如果没加上会显得东一句西一句，逻辑很乱。
> > 第三个问题：每个小点只能对应一张幻灯片，如果需要一个小点讲两张片子，就不行了，这个问题可以解决一下。

总的来说，Mindshow可以实现从Markdown转PPT的操作，但是还有一些小的细节需要打磨一下，这样的话就更加符合正常ppt使用的习惯，就分页这点来说，我觉得可以借鉴一下Marp的做法。

![image-20230427202417087](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20230427202417087.png)

像这样用分割线来表示分页我觉得是一个很不错的想法，只要每次分割还保留本级和上级标题就可以实现我们正常使用的功能了。

## 总结

ChatGPT---Markdown---PPT 这个工作流虽然还存在一些技术性问题需要修改，但是不得不说这无形之中给未来的公职人员提出了更高的要求，如果只是会做毫无建树，毫无创新的工作，迟早有天会被AI所优化的。

总结，摸鱼很好用，躺着收课件指日可待。