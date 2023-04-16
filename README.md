# kvmBarrierNote

键鼠跨屏方案，我在个人开发过程中非常常用，常用的方案是barrier，当然这里我也会推荐其他方案。
虚拟软件kvm：
barrier:  https://github.com/debauchee/barrier

synergy(收费):  https://symless.com/synergy

sharemouse: https://www.sharemouse.com/

inputDirector: https://alternativeto.net/software/input-director/about/

multiplicity: https://alternativeto.net/software/multiplicity/about/

论坛网站：https://alternativeto.net/software/mouse-without-borders2/

硬件跨屏：
键盘鼠标，多模切换功能。以logi举例，它们还支持软件级别的跨屏logitech flow。
kvm硬件切换器，一套键鼠，通过控制器的按钮进行切换。

## barrier使用方式
这里我们以barrier举例，使用mac和windows进行键鼠跨屏配置。

### 安装下载
![](Pasted%20image%2020230416141504.png)
![](Pasted%20image%2020230416142106.png)
下载完毕后，在你需要共享的mac和windows上同时安装。

导出



### 配置
如果你的工作环境不是家庭内网，推荐使用ssl配置，保护您的桌面安全。 

#### 自动配置
windows客户端配置，键鼠不在这里。
![](Pasted%20image%2020230416164159.png)
![](Pasted%20image%2020230416164401.png)
macos配置服务端：
![](Pasted%20image%2020230416165315.png)
![](Pasted%20image%2020230416165515.png)
自动配置服务端时，记得把忽略自动配置客户端关闭。
不然自动配置的客户端找不到服务器。
![](Pasted%20image%2020230416165805.png)
如果你需要windows做服务端，mac做客户端，则操作方法类似。不做多余赘述。

#### ssl配置

⭐️
**其中只需要客户端生成ssl证书即可，服务端不需要。**

windows安装后，在barrier中自带openssl工具，记的放入环境变量中。
![](Pasted%20image%2020230416152454.png)
macos自带openssl
![](Pasted%20image%2020230416163352.png)
win32: 
openssl不会用？
https://github.com/LeroyK111/opensslNode

req：证书类
-x509: 自签名证书
-nodes：不加密
-days：有效期
-subj：证书信息
-newkey：指定密钥类型和长度
-keyout：密钥名称
-out：输出文件地址

生成证书到指定位置。
```shell
# 打开文件夹
cd C:\Users\USERNAME\AppData\Local\Barrier\SSL
# 在这里，生成证书
openssl req -x509 -nodes -days 999 -subj /CN=Barrier -newkey rsa:4096 -keyout Barrier.pem -out Barrier.pem
```

macos:
生成证书到指定位置。
```shell
# 打开文件夹
cd /Users/USERNAME/Library/Application Support/barrier/SSL
# 调用openssl，在该位置生成 .pem file
openssl req -x509 -nodes -days 999 -subj /CN=Barrier -newkey rsa:4096 -keyout Barrier.pem -out Barrier.pem
```

重新启动barrier，然后就能看到这一栏ssl指纹。
![](Pasted%20image%2020230416171014.png)
### 启动
ssl配置，自动配置，区别仅在于多了一层ssl鉴权。
![](Pasted%20image%2020230416171307.png)

启动client，启动service，链接成功，即可跨屏。

鼠标贴边or用你的快捷键。



