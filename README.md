
## 本地Ubuntu一键编译脚本,全程无脑操作,只要梯子质量过关就好了

- ### 说明：
- 《[Telegram聊天吹水群](https://t.me/heiheiheio)》- 《[Telegram中文设置方法](https://github.com/danshui-git/shuoming/blob/master/tele.md)》
- 此一键编译脚本基本同步我的《[云编译脚本](https://github.com/281677160/build-actions)》，包含常用插件
- github已筑墙,所以国内用户编译全程都需要梯子,请准备好梯子,使用大陆白名单或全局模式
- 请使用服务器版本的 Ubuntu 18.04 LTS 或 Ubuntu 20.04 LTS （不支持windons子系统，windons请用hyper-v安装ubuntu）
- 编译openwrt两个常用的工具下载地址《[PuTTY(SSH)工具](https://github.com/danshui-git/shuoming/blob/master/Putty%E5%B7%A5%E5%85%B7%E4%B8%8B%E8%BD%BD.md)》《[WinSCP文件管理](https://github.com/danshui-git/shuoming/blob/master/WinSCP.md)》
- 使用非root用户登录您的ubuntu系统,执行以下代码即可:

---
- 为防止个别系统没安装curl，使用一键编译命令之前选执行一次安装curl命令:
```sh
sudo apt-get update && sudo apt-get install -y curl
```
- 一键编译openwrt命令:
```sh
bash <(curl -fsSL git.io/pile.sh)
```
---

- N1和晶晨系列编译成功后的一键打包命令，内核组合一定要在《[更多说明](https://github.com/danshui-git/shuoming/blob/master/Amlogic.md)》查看获取
```
cd openwrt && sudo ./make -d -b s905x3_s905x2_s905x_s905d_s922x_s912 -k 5.10.70_5.4.150
```
---

问：进入一键本地编译系统后叫我选择编译源码，我该任何选择？<br />
答：我[这里](https://github.com/danshui-git/shuoming/blob/master/%E7%AE%80%E5%8D%95%E4%BB%8B%E7%BB%8D%E6%96%B0%E8%84%9A%E6%9C%AC.md)作了简单介绍，当然本地编译是不支持自建文件夹来增加机型的，云编译你们拉取了我仓库后可以随便自建。<br />
#

问：设置openwrt的IP地址是什么意思？<br />
答：这个地址就是用来登录你openwrt用的，需要什么IP是根据你个人需要，固件编译完成，你安装好固件后，在浏览器输入此IP就可以登录openwrt了，默认帐号是root，默认密码为空。<br />
#

问：询问我是否需要选择机型和增删插件，是什么意思？<br />
答：在我设置里面每个源码默认编译都是x86-64的机型固件，不适合所有人的，这个就是进入设置界面，如果你有设置需要就输入‘大小写的Y都可以，按回车确认’，等脚本运行到此步骤就自动弹出窗口，如果不需要就直接按回车就跳过了，《[youtube大神的固件配置视频教程](https://www.youtube.com/watch?v=jEE_J6-4E3Y)》视频跟不上源码的节奏的，你也不能按视频操作，就看看在那里修改机型，那里增加减少插件，增加主题就好了。
#

问：为什么我的配置文件有时候会改变了，不是保存我需要的？<br />
答：因为你个人原因或者网络问题多次发生中途错误，特别是没下载到插件包的情况下，配置就会改变，我的脚本默认是每次都读取前面保存配置，然后经过选择机型和增删插件之后又保存回去的，如果发生你没下载完整插件包，又到了保存配置的步骤，你的配置就发生改变了，因为你源码里面少了插件，下次就会再用你这个少了插件的配置，其实要防止这个也可以的，跟云编译一样弄，可以弄一份配置文件在ubuntu的指定位置，每次只读不写入就可以了，当你发生了配置改变的话，就自己复制新配置粘贴到指定文件就可以，不过有点麻烦，我就没弄了。

#
问：询问我是否把定时更新插件编译进固件，是什么意思？<br />
答：这个在本地编译增加就是个娱乐的，因为我云编译程序是会自动把固件传送到指定位置，安装好固件后就能检测了，本地编译想用的话，只能编译好又手动传到指定位置，就给闲的蛋痛的人玩的，怎么在本地编译又能自动传github的指定位置，这个我不会啊，有懂的可以把代码贡献一下的，谢谢！
#

问：再次编译的时候询问我是否更换源码，是什么意思？<br />
答：就字面上的意思，比如你首次编译的时候选择的是Lede_source源码，你玩腻了，想换其他源码编译就可以换呗。
#

问：再次编译的时间需要那么长呢？人家都几分钟，几十分钟就可以，我还是要3-4个小时？<br />
答：因为我这是跟云编译一样操作，每次编译都是下载最新源码跟插件的，这样比较不容易出现错误，我测试了几十次二次编译，很容易出现build_dir和staging_dir错误，要清除了这些文件再编译才成功，清除了这些其实就是又回到了首次编译的操作，一样要3-4个小时来编译，还不如每次都重新拉取源码跟插件了，只保存你的配置不变，其他都删除了。<br />

编译时间长短是根据插件多跟少，还有CPU线程数有关的，同样插件的情况下，单线程编译需要3个小时左右，双线程就缩短30分钟左右，四线程就缩短1小时左右，八线程就缩短1.5小时左右，十二线程就缩短2小时左右，我的脚本默认是你的CPU多少线程或者核就用多少线程编译的。<br />

同样线程的情况下，不同型号的CPU也有分别的，性能越好的CPU编译速度越快，最明显的对比就是用云编译的时候了，在云编译的时候分配到的服务器CPU越好编译速度越快，他的服务器都是限制了2核2线程的，你们可以用我云编译脚本测试看看，在编译信息里面可以看到服务器的CPU情况。
#

问：为什么编译N1或晶晨系列CPU的盒子需要那么多流量？<br />
答：因为这个多了一个内核文件夹，打包的时候用到的，一个内核文件夹包含很多内核，我测试了一下，就从下载源码到下载完内核文件夹算，都用了差不多4G的流量，当然每个机场计算方式不一样，我的这个机场写的是1倍计算方式，完整编译完成一个N1的固件可能大概需要5G流量左右吧。<br />
#

问：使用什么梯子编译比较好？<br />
答：这个我真没啥好建议啊，我就说说我测试用的几个机场为例吧。<br />

<1> 第一个机场18元一个月，此机场看4K，打开网页都杠杠的，速度很快，但是用来编译的时候只有50%概率能成功，因为下载DL步骤很经常下载不完整，在这个步骤下载不完整就不需要进行编译了，DL下载不完整会自动退出编译程序。<br />

<2> 第二个机场9元一个月的，这个机场100%编译不成功，下载源码都经常下载不了，别说下载DL的时候了，100%下载不完整。<br />

<3> 第三个机场6.66元买的一个月，这个机场可以编译成功，就是下载DL的时候需要30分钟时间，太久了，下载源码也慢，所以我去买了第四个机场，这个机场第三天回来看看的时候居然跑路了，握草。<br />

<4> 第四个机场2.99元买的一个月，这个机场99%编译成功，下载速度快，用着舒服，虽然限速150M，量也才50G，我用这机场测试了3天，量就用完了，所以本地编译也需要很大成本滴。<br />

<5> 第四个机场4.99元买的一个月，这个机场很诡异的，下载源码的时候经常少文件夹的，比如源码里面一起是10个文件夹它经常就下到5-6个，下载我插件包的时候也是这样，下载不完整，不是少这就是少那的，用这个机场来搞本地编译你会疯的，因为我做了判断下载错误就停止，但是这个机场节点下载文件是少了，判断又判断他是成功下载了，所以你会误认为你机场节点很好，但是一编译就100%错误的，呵呵。<br />

<6> 还有一些机场节点有问题，显示编译成功，但是又没固件的。<br />

<7> 本人前后差不多用了10个机场来测试本地编译，真正可以舒服编译的只有2个，所以我真不推荐本地编译，云编译多省事。<br />
#
#
#
---
#
- <img src="https://github.com/danshui-git/shuoming/blob/master/doc/bendi5.png" />
#
- <img src="https://github.com/danshui-git/shuoming/blob/master/doc/bendi1.png" />
#
- <img src="https://github.com/danshui-git/shuoming/blob/master/doc/bendi2.png" />
#
- <img src="https://github.com/danshui-git/shuoming/blob/master/doc/bendi3.png" />
#
- <img src="https://github.com/danshui-git/shuoming/blob/master/doc/bendi4.png" />
---
#
- # 捐赠
- 如果你觉得此项目对你有帮助，请请我喝一杯82年的凉白开，感谢！

-微信-
# <img src="https://github.com/danshui-git/shuoming/blob/master/doc/weixin4.png" />
