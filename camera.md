# Camera小组

```text
熟悉 Camera 的工作原理，Camera 器件组成部分
搜集 MTK/SPRD Camera 相关 FAQ 和 DOC，仔细研读相关资料
每周开个例会分享一下工作学习心得(安排人轮流讲解一下其他人改的bug，简单的可以不用讲，主要讲一下分析思路和过程，一起讨论一下有没有更好的解决方案)
整理Camera资料（脚本，工具，Snippet，编译方式）
整理常见 camera 相关 log
整理常见名词缩写
有机会可以去了解一下 Tuning/Driver 的工作
分辨哪些是 驱动的问题/tuning的问题/HAL的问题/app的问题？
风险评估能力
开发周期评估能力

疑问墙 : 问题描述  问题出处  问题解答，将已解答的问题进行归类
模块问题收集，模板编写
相机问题难易等级分类，哪些问题可以项目组自己解决，哪些问题需要Camera组解决

划分模块，对各个模块的功能做一个详细的介绍，每个模块主要涉及到哪几个文件
HDR/MFNR/3DNR/Portrait/Blur/Bokeh/Beauty/Body/FaceDetection/MicroLens/Panorama/广角自拍Selfie/TIMELAPSE/大光圈/专业/连拍/滤镜/二维码/夜景/Sticker/有声照片/超级防抖/超像素/GIF 动画/Live shot/流光快门/ZSD/ZSL/SecurityCamera/QuickCamera/二维码/水印/
整理 ProjectConfig.mk 中 Camera 相关的宏
Camera第三方算法集成
学习OpenGL相关知识
设计一套 Camera 的 UI(参考Tecno/TCL/小米等)
解读 MTK Camera2/DreamCamera2/Magic Camera/OpenCamera/GeekCamera2 的代码，分析其架构思想，看一下有哪些可以学习和借鉴的地方
学习研究HAL的代码，需要C/C++相关知识 vendor/mediatek/proprietary/mtkcam3
代码提交commit规范/注释规范
对代码关键节点打上 SageReal 相关 TAG
Camera Monkey问题分析/性能问题分析+优化/功耗/CTS相关问题分析
学习如何分析trace,在关键代码周围加上trace
学习分析log

提 eService/CQ 的模板，参考《000_Camera入门必读和eService提交规范.pdf》
如何提高开发效率？快速分析，快速定位，精准定位，代码健壮程度
如何快速添加一种模式？
抽离一些通用代码做成 工具类(Log)/so库/jar包
开发一个 CameraToolApk 方便调试（打开dump, 设置prop, 设置 camera log level,）
Camera Log分析工具？
开发 Camera压力测试工具(脚本/apk)
开发 raw/YUV/exif/metadata 查看工具

买几本 Camera/图像处理 相关书籍
```

## 小组任务

```text
1.梳理每个模式的流程，整理成文档
    a.Photo
    b.video
2.自定义一个VendorTag，从app下发看是否能接收到
3.梳理Camera Tag，了解每个TAG的作用
    tags
4.对之前遇到的Bug进行整理分类，UI相关/framework/HAL相关/第三方相关/驱动相关/MTK相关/其他
```# 学习资料

## MTK QuickStart培训教程

```text
https://online.mediatek.com/QuickStart/QS00033#QSS00249

https://online.mediatek.com/Pages/eCourse.aspx?001=002&002=002002&003=002002004&vurl=https%3A%2F%2Fonline.mediatek.com%2F_layouts%2F15%2Fmol%2FeCourse%2Fext%2FExteCourseDetail.aspx%3FitemId%3D959%26csId%3D%25257B433B9EC7-CC31-43C3-938C-6DFD42CF3B57%25257D%252540%25257BAD907AF8-9A88-484A-B020-EA10437DADF8%25257D%26RootUrl%3D%252fPages%252feCourse.aspx
```## GeekCamera2

```text
git clone https://e.coding.net/deepinout/camera/GeekCamera2.git

https://github.com/android/camera-samples
```## 学习camera的小目标

```text
使用 Camera1 开发一个相机应用
使用 Camera2 开发一个相机应用
使用 CameraX + Kotlin 开发一个应用

通过高通或者联发科（MTK）官网上的文档，进行相机架构与HAL层的学习。
初步了解算法集成的基本思路
学习MTK平台下，camera open的基本流程

算法：
单帧算法集成的学习
metadata参数的学习
独立集成一个预览算法
独立集成一个多帧拍照算法
学习MTK平台Plugin算法流程
尝试进行美颜、暗光算法的流程
添加三方 feature/算法
https://blog.csdn.net/justXiaoSha/article/details/100730520
1，6589/6572/6582平台添加三方feature/算法
主要介绍在6589/6572/6582平台，如何在HAL层preview、capture、video record的flow中集成三方feature/算法.
文档名称：“3rd Party Algorithm Porting Guide on MT6589.ppt”

2，6592/88平台添加三方feature/算法
主要介绍6592/88平台Hal层架构、Hal层buffer queue机制和在HAL层preview、capture、video record等flow下集成三方feature/算法的方法。
其中Hal 层架构和buffer queue机制的内容同样适用于6589/6572/6582平台。
文档名称：“3rd Party Algorithm Porting Guide on MT6592.pptx”

Camera 算法工程师？

数字图像处理--原理和实现
图像处理算法？
openCV
openGL
matlab
matrix
yuv
```## MTK camera tuning学习中遇到的一些问题

```text
一、
1、ISP Tuning Tool 模拟工具中的 MPNR、SWNR什么意思？MNR就是NR的重复吗？
2、ISP Tuning Tool 中的DBS、Pre gain是什么意思？
3、EM mode中 Capture模式中slim video是什么意思？
   Video Clip Raw Dump中 resolution：resize to 2M 是裁剪到两百万像素的意思吗？
   shutter delay： 0s 5s 10s 是否可以修改？
   VHDR是什么意思？
   MFLL是什么意思？
   Scene mode是否可以格外添加其他场景（除了默认场景），Auto是否就是包含所有默认场景？
   EV calibration 中一系列参数是什么意思  AEid PSS PSG PISPG CSS CSG ...(GIS中也有该系列参数)
   Shading Verification中 MTK+one-THREE 是什么意思？
   AF选项AF Bracket是什么意思？Through Focus Dump是什么啥意思？
   Custom Parameter是干嘛的？
   System Property是干嘛的？
4、如何理解gamma曲线的调整：(1)bright(2)contrast(3)knee
5、sensor ID和device ID意思不同？
6、图像成像一直到输出经历的裁剪过程？
7、camera相关代码处在整个代码目录中的划分原则？
8、OTP具体介绍？
二、
1、dump NVRAM，refresh NVRAM分别是什么意思？调试过程中经CCT调试apply，save后的手机恢复出厂设置效果参数是否变成最初的参数？
2、《SOP 2.0》和FR写的《客观调试准则》互相补充，但是具体到细节其中不明白调试中何时需要关闭使能，尤其是Shading Calibration调试中关于哪种使能的开和关，俩文档说法不一致 （FR文档中强调只开启OBC和ANR）
3、Shading Calibration调试中apply和save后可否直接capture一张图片验证是否效果改变？（自己试了试，没改变，不知道是自己操作错误还是本来效果就不能及时改变）
4、Shading Calibration中的SDBLK是什么数据，还是不明白
5、uniform light，average light？
6、Golden模组，Unit模组，Normal模组？
7、CCT工具generate的代码含有camera_AE _PLineTable_imx258mipiraw，文档中generate的代码未包含此代码
三、
1、最终呈现出来在手机屏幕上的图像质量是经过“屏幕调试”产生的吗，是由GPU负责的吗，它和我们的ISP对图像处理产生的效果会不会有冲突，先后顺序？
2、还有一些小的方面不清楚，比如eng版本是？服务器版和用户版指的是？
 四、
1、shading调试前需做EV calibration吗？要做EV calibration,意义？
2、shading 调试中否要将dialog中AWB的R、G、B Gain调为一致？（是否需将将R、B调为与G gain一致？若调试shading开启AWB enable对shading调试无影响，则是否需要调为一致？）
3、AWB调试完后Light Source Probability模块中P0，P1，P2，P分别是什么概率？
4、CCM调试完后是否立刻断开CCT进行CCM验证？（Imatest）
5、Gamma调试完后是否也需马上验证？（离线进行灰阶测试）
6、AF放在哪一部调，还是最初就应该调好？（信噪比与解像力的权衡）
7、调试CCM导入csv的gamma文件来源于上一步调试后生成导出的gamma文件还是源代码的gamma？
8、D65光源下的#20--#22三个色块的信噪比要求达到35dB以上（信噪比如何测试？）
9、整个流程调试完OK后，断CCT后再全面测试一遍，都达标后可再连接CCT，导出参数。（断CCT全面测试如何测试？）
10、CCT中最后一项Tuning Tools输入Value后即可计算offset值，计算原理？其中的gain是？
11、patch是？
五、
1、OB中显示R、Gb、Gr、B，那么像素拜耳矩阵中的RGGB中的G也是两种吗？（若是一种，则为何测OB时计算显示Gr,Gb呢）
2、exposure linearity中exp time mode中选择时间为300000us，为何真实测试时间很久？
3、不同色温照应不同场景，那么不同亮度也相对应着不同场景吗？
4、AE Pline table-Table Mapping 图还是不懂?(参数意思均明白，但还是不明白为何这样表示)
5、AWB调试中框的坐标Left,Right,Top,Bottom代表？(某种色域空间坐标吗)
6、Gamma调试中，Channel Control选择All和RGB通道调试对图像质量有何影响？
7、CCM中的Optimize调试机理是？（cost function:formula of optimization）
8、CCM中的Finetune里面的a*,b*是另一种色域空间坐标吗？
9、Dynamic CCM和Smooth CCM （shading中的TSF是smooth shading即是color shading吗）
10、PCA调试中Y gain代表着luminance,那么代码中此值为何一直为0？
11、Flare Tuning的机理？
12、缩放是在哪一步进行的？
13、随着色温的升高，要对色温进行较正，否则，物体在这样的光线条件下所表现出来的颜色就会偏离其正常的颜色，因此需要降低sensor对红色的增益，增加sersor对蓝光的增益？？？
（增加增益指的是？）
14、手机握在手上旋转，图像不懂，是怎么实现的？
15、前摄和后摄模组安装方向应该不一致？flip 90度或者不用flip？
```## Camera tuning

```text
1 聊聊你改过的awb 场景和你是如果判断此问题时白平衡问题还是色彩问题？
2 sensor端otp和平台端otp区别是什么？
3 sensor端otp如何确认？
4 如果确认otp是否正常？
5 如何确认马达的那个震荡曲线是否正常？
6 虹软和一些其他的算法一般是做在cpp之前还是之后，区别是什么？
7 曝光表最大的gain值 如何设置？
8 你是怎么去配置曝光表的？
9 曝光表中先跑gain和先跑line count区别是什么？
10 histogram机制，你一般怎么修改？
11 你是如何理解和调试green zoon的？
12 你了解过hot pixel吗？如何前期避免
13 当遇到瓶颈问题时，你如果分析
14 说说你对曝光表的理解
15 商场这种复杂的环境，白平衡问题，你是如何调试的？
16 ABF 你是如何调试的？
17 ASF 你是如何调试的？
18 AF调试中，如何确认margin值
19 双色温闪光你调试过吗？
20 闪光灯亮度问题，你如果调试？
21 你有看过af 驱动的流程吗？
22 otp 函数中有3个group 地址从小到大，otp函数中 为什么是从前面往后面搜索，而不从后面往前面搜索，这3个组的意义是什么？
23 otp 函数中的 r gain,b gian,gain,为什么要寻找最新的gain?最后补偿时为什么是乘512，而不是其他值，
24 你是如何确认你awb的otp 生效了？
25 如何确认你的af margin 是合理足够的？

相关知识点总结：
一、模组及工艺相关知识
     ①模组的组成
          1）模组的基本组成。（AF&FF）
          2）镜头----镜头的发展历史，镜头相关参数解析，镜头的选型依据，优劣判断。（MTF,DOF,Focus,AF,P&G....）
          3）sensor----sensor的发展历史，技术演进，sensor本身特性参数解析，主流sensor厂工艺技术解析，分析各大sensor厂之间的差异，优缺点，同时能从某几颗sensor来分析。（了解带有PD的sensor）
                    1’sensor硬件电路设计部分要了解。
                    2’驱动相关部分，MIPI时序，sensor hts，vts，pclk，等的配置要了解。
          4）AF driver 了解，如何控制driver ic，如何设置dumping,ring时间等。
          5）了解模组硬件layout，走线，电子元器件，连机器等设计缺陷对于图像质量的影响。
     ②模组的组装工艺，优劣。了解模组设计上的其他工艺，OIS等。
     ③了解模组厂是如何测试最终的模组是否满足需要，测试方法，测试标准。
     ④学习模组厂对于模组差异性的控制，golden,limit,normal选择依据，otp写入参数等。
     ⑤综合考虑模组选型参考依据，以及模组最终确定选型之后，所能成像的影响质量和其他模组的对比。
二、图像及色彩处理基本理论和算法
     ①色彩的基本理论。
     ②ISP流程分析。
     ③3A的基本算法原理。
     ④ISP各模块分模块讲解算法模型等。（CCM,去噪，锐化等）。

三、图像质量评价方法，主客观测试方法
     ①客观测试方法
          基本测试标准，及测试方法，（imatest,DXO等主流厂商的测试方法）
     ②主观测试方法
          主观测试场景，以及对于测试场景的分析方法。
     ③综合从哪些参数评价图像质量。了解客户的关注点。

调试经验：

一    关于Sensor预览时有条纹：
1。电源不稳定，CMOS sensor对电源的稳定度蛮高的。
2。同步信号受干扰，彩色条纹显然是每行数据中有信号丢失造成。
3。检查mclk和pclk以及他们的ratio,软件设置是否相符。

1。随机条纹干扰，查电源
2。行场同步随机干扰，一般不大会出现，除非HSYNC与VSYNC中间串入电阻或者走线过长
3。50HZ/60HZ刷新非同步条纹，改刷新频率，行不同步/干扰出现摩尔纹（移动斜条纹），场不同步/干扰出现百叶窗效应

这个问题从软件上很难解决， 最好的办法是从滤除电源干扰入手。SENSOR的数字电源没有问题，关键是模拟电源，它给内部的A/D及光电转换电路供电，所以比较敏感。建议：用PSSR值较高（80db以上）的LDO给其模拟电路供电，同时，在靠近连结器附近用磁珠和去偶电容进一步消除干扰。

二    找不到CAMERA 设备，装置未就绪

电源，RESET,I2C有没有信号，RESET的高低电平是否正确，某些sensor高电平复位，power down电平是不是正确，读sensor ID是否能读出

以上都正常，基本就是初始化代码的问题了

如果POWER、RESET信号没问题的话，一般情况下是sensor ID错误，可以尝试I2C读取后sensor ID打印出来看看，这样可以验证I2C能否正常读取，以及你配置的sensor ID是否正确！
如果I2C无法正常读取的话就是硬件问题了，查硬件

https://blog.csdn.net/kongbaidepao/article/details/109692606
```## 展讯平台camera tuning客观流程

```text
一、步骤
1.首先auto tuning 生成一版初版参数，然后编译成so文件（本次练习没有编译）。
2.做一个曝光表，然后定标LNC。
3.然后进行AWB标定，其中AWB标定分为gray chart和color chart标定，直接拍定标图进行标定，然后将boundary进行完善，保证boundary达到基本的要求。
4.配置一个Gamma表。
5.CMC的标定。
6.然后进行NR的标定，先配置config表，然后拍图标定bayer nr和BPC标定。
7.最后，根据客观自测不过项，进行微调，达到客观标准。

二、具体过程
2.1 Auto Tuning

根据auto tuning文档操作生成初版的参数文件即可。
2.2配置曝光表
本次练习没有对比机，根据以往的经验进行了曝光表的配置。


曝光表配置的规则：Exp TimeNMax GainN≥Exp TimeN+1；
Exp TimeN+1Max GainN+1＞Exp TimeN*Max GainN。
可通过log抓取对应状态：adb logcat | find “algs_status”
2.3 LNC标定
（1）adb shell setprop persist.vendor.cam.raw.mode raw //生成raw和jpg
adb shell setprop persist.vendor.cam.raw.mode jpg //生成jpg

LNC标定中遇到的问题：
为了让raw图中心亮度达到最大亮度的80%，手动曝光更改shutter来拍raw图，无论怎么修改shutter都是达不到要求的，将raw图导进去会提示中心太暗。
原因分析及解决方法：
原因：因为之前配置的曝光表中最大倍gain的Exp Time设置为7，可能是手动曝光达到上上限也保证不了raw图中心亮度的要求。
解决方法：将64倍gain的Exp Time增大，本次练习中尝试增大到13和15，确保各个光源下的raw图都达到拍摄的要求。改过之后别忘了再改回去。
————————————————
版权声明：本文为CSDN博主「camera tuning 菜小白」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/lw123456_/article/details/118698129


相关知识点总结：
一、模组及工艺相关知识
     ①模组的组成
          1）模组的基本组成。（AF&FF）
          2）镜头----镜头的发展历史，镜头相关参数解析，镜头的选型依据，优劣判断。（MTF,DOF,Focus,AF,P&G....）
          3）sensor----sensor的发展历史，技术演进，sensor本身特性参数解析，主流sensor厂工艺技术解析，分析各大sensor厂之间的差异，优缺点，同时能从某几颗sensor来分析。（了解带有PD的sensor）
                    1’sensor硬件电路设计部分要了解。
                    2’驱动相关部分，MIPI时序，sensor hts，vts，pclk，等的配置要了解。
          4）AF driver 了解，如何控制driver ic，如何设置dumping,ring时间等。
          5）了解模组硬件layout，走线，电子元器件，连机器等设计缺陷对于图像质量的影响。
     ②模组的组装工艺，优劣。了解模组设计上的其他工艺，OIS等。
     ③了解模组厂是如何测试最终的模组是否满足需要，测试方法，测试标准。
     ④学习模组厂对于模组差异性的控制，golden,limit,normal选择依据，otp写入参数等。
     ⑤综合考虑模组选型参考依据，以及模组最终确定选型之后，所能成像的影响质量和其他模组的对比。
二、图像及色彩处理基本理论和算法
     ①色彩的基本理论。
     ②ISP流程分析。
     ③3A的基本算法原理。
     ④ISP各模块分模块讲解算法模型等。（CCM,去噪，锐化等）。

三、图像质量评价方法，主客观测试方法
     ①客观测试方法
          基本测试标准，及测试方法，（imatest,DXO等主流厂商的测试方法）
     ②主观测试方法
          主观测试场景，以及对于测试场景的分析方法。
     ③综合从哪些参数评价图像质量。了解客户的关注点。

调试经验：

一    关于Sensor预览时有条纹：
1。电源不稳定，CMOS sensor对电源的稳定度蛮高的。
2。同步信号受干扰，彩色条纹显然是每行数据中有信号丢失造成。
3。检查mclk和pclk以及他们的ratio,软件设置是否相符。

1。随机条纹干扰，查电源
2。行场同步随机干扰，一般不大会出现，除非HSYNC与VSYNC中间串入电阻或者走线过长
3。50HZ/60HZ刷新非同步条纹，改刷新频率，行不同步/干扰出现摩尔纹（移动斜条纹），场不同步/干扰出现百叶窗效应

这个问题从软件上很难解决， 最好的办法是从滤除电源干扰入手。SENSOR的数字电源没有问题，关键是模拟电源，它给内部的A/D及光电转换电路供电，所以比较敏感。建议：用PSSR值较高（80db以上）的LDO给其模拟电路供电，同时，在靠近连结器附近用磁珠和去偶电容进一步消除干扰。

二    找不到CAMERA 设备，装置未就绪

电源，RESET,I2C有没有信号，RESET的高低电平是否正确，某些sensor高电平复位，power down电平是不是正确，读sensor ID是否能读出

以上都正常，基本就是初始化代码的问题了

如果POWER、RESET信号没问题的话，一般情况下是sensor ID错误，可以尝试I2C读取后sensor ID打印出来看看，这样可以验证I2C能否正常读取，以及你配置的sensor ID是否正确！
如果I2C无法正常读取的话就是硬件问题了，查硬件
————————————————
版权声明：本文为CSDN博主「Sophia_hui」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/Sophia_hui/article/details/118387415
```# 知识点

## Camera工作原理

```text
https://www.huaweicloud.com/articles/4a4c52213dfce4385aedb735b8913d80.html
https://blog.csdn.net/ivychend/article/details/79483593

镜头
这是我自己对镜头的一些知识总结，仅限于我接触的一些知识的汇总，镜头其实是很复杂的，包含很多知识，我也只是接触了一些皮毛，如果你也做摄像机，并且刚刚接触这块，希望可以对你有一些帮助。
Camera镜头由镜头、镜头座、滤光片、VCM、电动光圈等组成，不同的应用方向，用到的组件并不相同。比如说VCM一般都是在手机镜头中会用到；电动光圈则是一些特殊相机中会用到。 在我的摄像机的应用中，经常用到的选型主要是镜头、镜头座和滤光片这三者。
**镜头知识**
镜头是摄像机中最关键的器件之一，直接影响了成像的好坏。每一款优秀的镜头都是经过了很复杂的光学设计。我对镜头的划分是通过镜片材质来划分的：玻璃镜头和塑料镜头。顾名思义，分别采用玻璃材质制作的镜片和采用塑料材质制作的镜头。这两种材质在有不同的特性，因此在透光度、加工难度、耐热性、成本等等都有比较大的差异。就目前我所了解的，手机镜头大部分都是塑料镜头，因为它的价格低，加工成本低，体积小；而安防和车载产品中用的镜头，大部分都是玻璃镜头。
我想从产品设计上面说一下，就我目前的了解来说，如果你希望你的镜头模组的高度控制在10mm以内甚至更低，或者你的产品对体积很敏感，那么我建议你选择用塑料镜头开始你的产品设计，因为目前市面上面，大部分的玻璃镜头的，最短的高度在10mm，很少有更低的。常用的玻璃镜头的体积都是比较大的，这受限于玻璃镜片的加工，玻璃镜片都是通过治具研磨加工的，镜片越小越薄，加工难度更大 。而塑料镜头是采用注塑工艺加工的，可以比较容易的加工更薄的镜片和镜头。
塑料镜头其实也可以按照应用不同，分为CSP镜头和COB镜头，这两种镜头在选型的时候尤其需要注意，不能混用；尤其是COB的镜头用在CSP上面，会发生虚焦的问题，这是我在产品的开发中遇到过的问题。如果你用的CSP封装的CMOS芯片，那么在选择镜头的时候，一定要用对应的CSP镜头，最好不要混用。至于CRA的匹配，这里我就不多说了。
还有就是镜头定制的问题，如果你想自己定制开发一款镜头，如果单纯从模具成本来说，玻璃镜片的模具是比较低的（单个镜片模具的成本可以控制在1W以内，单个镜头需要4~6片镜片，整个镜头的模具成本可以控制在10W以内）；而塑料模具的成本较高（单片镜片的模具成本在10W以上，整个镜头至少需要3片镜片，整个镜头的模具成本高达50W以上）。同时玻璃镜头的加工工艺和投入成本相对塑料镜头小很多，所以市场上玻璃镜头的厂家很多，销售商也很多；而塑料镜头的选择就没有那么多了，主要集中在那些大厂，销售商也很少，如果你的产品销量小，选型会很困难。
**镜头座**
镜头座如果从材质上面来说，可以分为金属材质和塑料材质（主要是PC和玻纤材质）。金属材质的镜头座比较坚固，但是金属的导热性会更好，如果你的产品会发热严重，那么你要思考这个热量会不会导入导镜头当中，不要小看这个热量，因为普通镜头的工作温度是-10~60℃，如果你的产品散热不佳，镜头座传递的热量的发生了积累，那么可能会引起镜头的虚焦（我在产品设计中遇到过的问题），而这需要你在产品设计当中考虑清楚。
镜头座从接口上面来区分的话，可以分为CS、M12、M9、M8等等各种不同接口的镜头，这就是根据你的需求选择。有一点想说的就是，最好使用镜头厂家推荐的镜头座，因为虽然镜头是M12的接口，镜头座也是M12，但是当你实际使用时，你会发现你可能拧不进去。虽然螺纹的一样，但是他们是存在加工公差的，并且最终适配的扭力并不相同，所以需要注意。
**滤光片**
滤光片也是摄像机的一个关键器件，加入滤光片主要是为了去除光线中的近红外光，让成像颜色更接近人眼。滤光片可以按照滤波的方式不同，分为吸收型和反射型；而目前应用最广的就是吸收型，而吸收型的又可以根据材质不同分为普通玻璃和蓝玻璃材质这两种。蓝玻璃光学效果更好，但是成本更高；所以在设计中需要考量。
滤光片中还会根据滤光波段的不同可以分为单通滤光片，双通滤光片，带通滤光片等。这要根据你的使用需求去选择。
在产品设计中，选型滤光片，你还好考虑大小尺寸、厚度等等。这些参数需要你根据CMOS高度，镜头、镜头座综合考量，然后向滤光片厂家提供你的定制需求。

1.工作原理
lens：捕获光信号
sensor：将光信号转换成电信号
音圈马达：自动对焦
红外滤光片：滤除红外线。滤除对可见光有干扰的红外光，使成像效果更清晰
FPC/PCB：电路板，用于连接cpu

DSP/ISP
ISP 是Image Signal Processor 的简称，也就是图像信号处理器。而DSP是Digital Signal Processor 的缩写，也就是数字信号处理器。ISP一般用来处理Image Sensor（图像传感器）的输出数据，如做AEC（自动曝光控制）、AGC（自动增益控制）、AWB（自动白平衡）、色彩校正、Lens Shading、Gamma 校正、祛除坏点、Auto Black Level、Auto White Level 等等功能的处理。

DSP可以做些拍照以及回显（JPEG的编解码）、录像以及回放（Video 的编解码）、H.264的编解码、还有很多其他方面的处理，总之是处理数字信号了。DSP一般对ISP输出的YUV、RGB数据进行处理。

sensor中是否集成ISP、DSP跟具体的厂商、sensor型号有关，ISP、DSP的具体功能参考sensor手册。
sensor常用输出图像格式有下面四种
YUV：luma(Y)+chroma(UV)格式（亮度、色度），一般情况下sensor支持YUV422格式，即Y-U-Y-V次序输出数据。
RGB：传统的红绿蓝格式，比如RGB565,5bit R + 6bit G + 5bit B，G多一位是因为人眼对绿色比较敏感。
RAW DATA：sensor的每一像素对应一个彩色滤光片，滤光片按Bayer Pattern(拜耳模板)分布，将每一个像素的数据直接输出，即Raw Data。
JPEG：有些sensor，特别是低分辨率的，其自带JPEG engine，可以直接输出压缩后的jpg格式的数据。
常用的输出格式就是YUV、RGB格式，RAW DATA一般专业摄像师用多。

景物通过 Lens 生成的光学图像投射到 sensor 表面上， 经过光电转换为模拟电信号， 消噪声后经过 A/D 转换后变为数字图像信号，再送到数字信号处理芯片（ DSP） 中加工处理。所以，从 sensor 端过来的图像是 Bayer 图像，经过黑电平补偿 （ black level compensation）、镜头矫正 （ lens shading correction）、坏像素矫正 （ bad pixel correction）、颜色插值 （ demosaic）、Bayer 噪声去除、 白平衡（ awb） 矫正、 色彩矫正（ color correction） 、 gamma 矫正、 色彩空间转换（ RGB 转换为 YUV） 、 在 YUV 色彩空间上彩噪去除与边缘加强、 色彩与对比度加强，中间还要进行自动曝光控制等， 然后输出 YUV（ 或者 RGB） 格式的数据， 再通过 I/O 接口传输到 CPU 中处理。
```## Camera工作流程

```text
Camera 的一个工作流程主要分为这么七步:
1.打开 Camera Power LDO,让 Camera 有能量保证。
2.打开 IIC,设置 PDN 引脚,使 Camera 退出 Standby 模式,按照要求让 Reset 脚做一个复位动作。
3.读一下 sensor 的版本 ID,这样可以让你确认是否连接上你想要的 sensor。
4.对 Sensor 进行初始化下载最基本的参数让 Sensor 工作起来,可能包括软复位。
5.下载 preview 的参数,为预览动作准备。
6.下载 Capture 的参数,为拍照动作准备。
7.设置 PDN 引脚,使 Sensor 进入 Standby 模式, 或者关掉 LDO 等动作,退出 Camera。
```## 3A算法

```text
3A技术即自动对焦（AF）、自动曝光（AE）和自动白平衡（AWB）。3A数字成像技术利用了AF自动对焦算法、AE自动曝光算法及AWB自动白平衡算法来实现图像对比度最大、改善主体拍摄物过曝光或曝光不足情况、使画面在不同光线照射下的色差得到补偿，从而呈现较高画质的图像信息。采用了3A数字成像技术的摄像机能够很好的保障图像精准的色彩还原度，呈现完美的日夜监控效果。

自动对焦算法（AF）http://camera.geek-docs.com/basic/auto-focus-introduction.html
是通过既得图像对比度移动镜头使图像对比度达到最大。总的来说，自动对焦技术就是通过调整聚焦镜头的位置获得最高的图像频率成分，得到更高的图像对比度。其中，获得最佳的对焦点是一个不断积累的过程，它通过比较每一帧图像的对比度从而获得镜头移动范围内最大的对比度点，进而确定对焦距离。

通过调整聚焦镜头的位置获得最高的图像频率成分。总的来说，已对焦图片比为对焦图片包含更高的频率成分，也就是相应的图片具有更高的对比度。获得最佳对焦点是一个不断积累的过程，它通过比较每一帧图像的对比度从而获得镜头移动范围内最大的对比度点，从而确定对焦距离。现在流行的自动对焦系统采用的是爬山算法（hill-climbing）。然而该算法也有一定的局限性，它只适用于图像本身色差较大的情况。

传统相机，采取一种类似目测测距的方式实现自动对焦，相机发射一种红外线（或其它射线），根据被摄体的反射确定被摄体的距离，然后根据测得的结果调整镜头组合，实现自动对焦。这种自动对焦方式--直接、速度快、容易实现、成本低，但有时候会出错（相机和被摄体之间有其它东西如玻璃时就无法实现自动对焦，或者在光线不足的情况下），精度也差，如今高档的相机一般已经不使用此种方式。因为是相机主动发射射线，故称主动式，又因它实际只是测距，并不通过镜头的实际成像判断是否正确结焦，所以又称为非 TTL式。这种对焦方式相对于主动式自动对焦，后来发展了被动式自动对焦，也就是根据镜头的实际成像判断是否正确结焦，判断的依据一般是反差检测式，具体原理相当复杂。因为这种方式是通过镜头成像实现的，故称为 TTL 自动对焦。也正是由于这种自动对焦方式基于镜头成像实现，因此对焦精度高，出现差错的比率低，但技术复杂，速度较慢（采用超声波马达的高级自动对焦镜头除外），成本也较高。手动对焦，它是通过手工转动对焦环来调节相机镜头从而使拍摄出来的照片清晰的一种对焦方式，这种方式很大程度上面依赖人眼对对焦屏上的影像的判别以及拍摄  者的熟练程度甚至拍摄者的视力。早期的单镜反光相机与旁轴相机基本都是使用手动对焦来完成调焦操作的。现在的准专业及专业数码相机，还有单反数码相机都设有手动对焦的功能，以配合不同的拍摄需要。

自动曝光算法(AE)

将根据可用的光源条件自动设置曝光值。当主体拍摄物和背景的亮度相差很大时，一般会造成主体拍摄物的过曝光或曝光不足，为了克服这个问题，一些特定的AE算法着重考虑了主体拍摄物的亮度情况，在进行亮度调整时给予这部分更多的比重。

在程序自动曝光方式中，照相机能根据测光系统所测得的被摄画面的曝光值，按照厂家生产时所设定的快门及光圈曝光组合，自动地设定快门速度和光圈值。就相机操作性而言，在这种方式下等同于所谓的"傻瓜照相机"，操作者根本不用调节快门速度和光圈值，所要做的只是对好焦点，按下快门释放钮就行了。在"傻瓜"照  相机中常见的电子程序快门，就属于这种曝光方式。其实，只有程序自动曝光方式才是真正的"全自动"曝光方式。

自动白平衡算法(AWB)

根据光源条件调整图片颜色的保真程度。物体在不同光线照射下会出现不同程度的色差，一般将一幅图像的整体色差信号用作色温数据，当这幅图像的大部分区域被一个统一的颜色覆盖时，这种色彩补偿就可能损失一部分完整的色彩。为了弥补这个缺陷，一些特定的AWB 算法被提出来以适应不同的色温情况。

白平衡英文名称为 White Balance。物体颜色会因投射光线颜色产生改变，在不同光线的场合下拍摄出的照片会有不同的色温。例如以钨丝灯(电灯泡)照明的环境拍出的照片可能偏黄，一般来说，CCD没有办法像人眼一样会自动修正光线的改变。下面一些图片，就显示了在不同颜色光线下的不同图象。平衡就是无论环境光线如何，让数码相机默认“白色”，就是让他能认出白色，而平衡其颜色在有色光线下的色调。颜色实质上就是对光线的解释，在正常光线下看起来是白颜色的东西在较暗的光线下看起来可能就不是白色，还有荧光灯下的"白"也是"非白"。对于这一切如果能调整白平衡，则在所得到的照片中就能正确地以"白"为基色来还原其他颜色。现在大多数的商用级数码相机均提供白平衡调节功能。正如前面提到的白平衡与周围光线密切相关，因而，启动白平衡功能时闪光灯的使用就要受到限制，否则环境光的变化会使得白平衡失效或干扰正常的白平衡。一般平衡有多种模式，适应不同的场景拍摄，如：自动白平衡、钨光白平衡、荧光白平衡、室内白平衡、手动调节。
```## 摄像头知识积累

```text
https://blog.csdn.net/LoongEmbedded/article/details/88649551
1. 摄像头通用知识
1.1 sensor类型
camera sensor分为YUV sensor 和Bayer sensor。
YUV sensor又叫SOC sensor，它的输出格式是YUV格式的，YUV格式又分很多种，常见的有YUV422,YUV420。
YUV: luma (Y) + chroma (UV) 格式， 一般情况下sensor支持YUV422格式，即数据格式是按Y-U-Y-V次序输出的
比如斑马扫描头SE4750 sensor是单Y输出，斑马技术说的。
Bayer sensor的数据输出格式是RAW格式的。
现在的主流是Bayer sensor，因为YUV sensor的数据量都比较大，例如YUV422格式1个pixel占据两个bytes，而RAW10格式的1个pixel只占10bit。一般的YUV sensor像素都比较低。
YUV sensor内部会自带一个isp对镜头传进来的图像进行简单的图像效果处理（通过寄存器设置），然后以YUV格式（一般是YUV420SP）输出。而Bayer sensor用的是平台自带的isp，不同的模组都需要进行效果调试。
 
2.高通平台
2.1 摄像头设备树节点
* Qualcomm MSM Sensor
MSM sensor node contains properties of camera sensor
Required properties:
- compatible : should be manufacturer name followed by sensor name
    - "qcom,camera"
    - "shinetech,gc0310"
- reg : should contain i2c slave address of the device

以上两个设置需要查看主板原理图，看主板上摄像头是接在CSI0还是CSI1上的，一般后摄像头都会接到CSI0上，前摄像头会接在CSI1上。
比如下面是msm8953下的

qcom,camera@0 {//主摄像头
        cell-index = <0>;
        compatible = "qcom,camera";
        reg = <0x0>;
        qcom,csiphy-sd-index = <0>;
        qcom,csid-sd-index = <0>;
        qcom,mount-angle = <90>;

        ...}

qcom,camera@2 {//2D软解码
        cell-index = <2>;
        compatible = "qcom,camera";
        reg = <0x2>;
        qcom,csiphy-sd-index = <1>;
        qcom,csid-sd-index = <1>;
        qcom,mount-angle = <90>;

...}

qcom,camera@1 {//前置摄像头
        cell-index = <1>;
        compatible = "qcom,camera";
        reg = <0x01>;
        qcom,csiphy-sd-index = <2>;
        qcom,csid-sd-index = <1>;
        qcom,mount-angle = <90>;
}

- qcom,gpio-reset : should contain index to gpio used by sensors reset_n，从0开始
- qcom,gpio-standby : should contain index to gpio used by sensors standby_n
- qcom,gpio-vio : should contain index to gpio used by sensors io vreg enable
- qcom,gpio-vana : should contain index to gpio used by sensors analog vreg enable
- qcom,gpio-vdig : should contain index to gpio used by sensors digital vreg enable
- qcom,gpio-vaf : should contain index to gpio used by sensors af vreg enable
- qcom,gpio-af-pwdm : should contain index to gpio used by sensors af pwdm_n
- qcom,gpio-req-tbl-num : should contain index to gpios specific to this sensor
- qcom,gpio-req-tbl-flags : should contain direction of gpios present in
- qcom,gpio-req-tbl-label : should contain name of gpios present in
- qcom,gpio-set-tbl-flags : should contain value to be configured for the gpios
    present in qcom,gpio-set-tbl-num property (in the same order)

qcom,gpio-set-tbl-flags= <0 2>; //(0 – GPIOF_OUT_INIT_LOW, 2 -GPIOF_OUT_INIT_HIGH)

gpios = <&tlmm 28 0>,
            <&tlmm 40 0>,
            <&tlmm 39 0>,
            <&tlmm 16 0>;       
        qcom,gpio-reset = <1>;1指向GPIO40
        qcom,gpio-standby = <2>;
        qcom,gpio-custom2 = <3>;  
        qcom,gpio-req-tbl-num = <0 1 2 3>;
        qcom,gpio-req-tbl-flags = <1 0 0 0>;//(0 – output gpio, 1 – input gpio)
        qcom,gpio-req-tbl-label = "CAMIF_MCLK2",//(gpio name)
                      "CAM_RESET2",
                      "CAM_STANDBY2",
                      "CAM_DVDD_1V2";        

//下面以msm8937的主摄像头来距离说明

    qcom,camera@0 {

<name>[@<unit-address>]如果一个节点描述的设备有地址，则应该给出@uni-address，多个相同类型设备节点的name可以是一样，只要unit-address不同即可，设备的unit-address地址也经常在其对应节点的reg属性中给出，对于挂在内存空间的设备而言，@字符后跟的一般就是该设备在内存空间的基地址，对于挂在I2C总线上的外设而言，@后面一般跟的是从设备的I2C地址。
        cell-index = <0>;//0为后置摄像头，1为前置摄像头

        compatible = "qcom,camera";
        reg = <0x0>;
        qcom,csiphy-sd-index = <0>;

- qcom,csiphy-sd-index : should contain csiphy instance that will used to
    receive sensor data
    - 0, 1, 2

        qcom,csid-sd-index = <0>;

- qcom,csid-sd-index : should contain csid core instance that will used to
    receive sensor data
    - 0, 1, 2, 3

传感器所用 CSID 硬件的索引；若同时使用两个传感器，则该设置不能使用
同一个值。
        qcom,mount-angle = <90>;
        qcom,actuator-src = <&actuator0>;
        qcom,led-flash-src = <&led_flash0>;
        /*qcom,eeprom-src = <&eeprom0>;*/  /* Modified by huangfusheng 2016-10-08 */
        cam_vdig-supply = <&pm8937_l23>;
        cam_vana-supply = <&pm8937_l22>;
        cam_vio-supply = <&pm8937_l6>;
        cam_vaf-supply = <&pm8937_l17>;
        qcom,cam-vreg-name = "cam_vdig", "cam_vio", "cam_vana",
                            "cam_vaf";
        qcom,cam-vreg-min-voltage = <1200000 0 2800000 2850000>;
        qcom,cam-vreg-max-voltage = <1200000 0 2800000 2850000>;
        qcom,cam-vreg-op-mode = <200000 0 80000 100000>;
        pinctrl-names = "cam_default", "cam_suspend";
        pinctrl-0 = <&cam_sensor_mclk0_default
                &cam_sensor_rear_default>;
        pinctrl-1 = <&cam_sensor_mclk0_sleep
                &cam_sensor_rear_sleep>;
        gpios = <&tlmm 26 0>,
            <&tlmm 36 0>,
            <&tlmm 35 0>,
            <&tlmm 16 0>,       /* Add GC8024 DVDD enable by huangfusheng 2016-10-08 */
            <&tlmm 92 0>;  //125    /* Add REAR CAMERA VAF enable by huangfusheng 2016-10-08 */
        qcom,gpio-reset = <1>;
        qcom,gpio-standby = <2>;
        qcom,gpio-custom2 = <3>;    /* Add GC8024 DVDD enable by huangfusheng 2016-10-08 */
        qcom,gpio-custom3 = <4>;    /* Add REAR CAMERA VAF enable by huangfusheng 2016-10-08 */
        qcom,gpio-req-tbl-num = <0 1 2 3 4>;
        qcom,gpio-req-tbl-flags = <1 0 0 0 0>;
        qcom,gpio-req-tbl-label = "CAMIF_MCLK0",
            "CAM_RESET0",
            "CAM_STANDBY0",
            "CAM_DVDD_1V2",         /* Add DVDD GC8024 enable by huangfusheng 2016-10-08 */
            "CAM_DVAF_2V8";         /* Add REAR CAMERA VAF enable by huangfusheng 2016-10-08 */
        qcom,sensor-position = <0>;
        qcom,sensor-mode = <0>;
        qcom,cci-master = <0>;
        clocks = <&clock_gcc clk_mclk0_clk_src>,
            <&clock_gcc clk_gcc_camss_mclk0_clk>;
        clock-names = "cam_src_clk", "cam_clk";
        qcom,clock-rates = <24000000 0>;
    };

3.解像力测试

相关链接：
linux驱动由浅入深系列：camera驱动之一(背景及基础知识篇)
https://blog.csdn.net/RadianceBlau/article/details/76460907

4.HDR宽动态
dynamic range大约要85DB才算是宽动态，比如AR0230CS这个sensor
下面是OV2735，不支持宽动态

Camera sensor bring up
https://blog.csdn.net/tamell5555/article/details/52190765

一文看懂安卓Android摄像头的移植方法-Android系统开发干货来袭
http://blog.sina.com.cn/s/blog_14f0dc1a10102xqd3.html

1.目前camera分为两种（按输出的图像数据分）：SOC及RAW
RAW：输出最原始的RAW图像，后续的图像处理需要平台端（MTK/展讯/高通）的ISP来处理。这与我们经常使用单反相机输出RAW图像后，再在电脑上使用专门的软件处理后期效果类似。
SOC：在RAW上集成了ISP，可以在其上直接调试效果，输出yuv/jpeg图像。
SOC= RAW+ISP
因此，如果我们计划使用RAW摄像头，则须确认AP是否支持RAW支持。在展讯平台上，sp5735,sp7731支持RAW制式摄像头。
在android上，camera驱动在kernel层，图像效果调试则在HAL层的ISP。

2.lens
（1）.镜头的品质会非常明显的影响到摄像头的图像效果（你要想一想那些昂贵单反相机镜头就释然了）；
（2）.镜头的镜片分为3p,4p甚至5p（镜片数目），材质有塑料和玻璃。通常情况下认为：镜片越多效果越好，玻璃镜片强于塑料镜片；目前业内最好的摄像镜头厂商为台湾的大立光电（系苹果手机摄像头供应商）。
p是plastic的意思，2P是指2片塑料镜片，3P4P以此类推；另外手机镜头术语还经常会提到G，指glass玻璃镜头，2P1G---2片塑料镜片1片玻璃镜片，其他依次类推。其中G的片数越多代表镜头的效果越好，同时价格越贵。
（3）.不同的镜头，对sensor的图像影响是不同的，因此对于不同的镜头，需要使用不同配置代码（就如同相同的LCD IC，使用不同的玻璃，则需要配置不同的初始化代码）；

3.关于sensor器件
（1）.大小分为1/5`（5.08mm)，1/4`（6.35mm)，1/3.2`等；
（2）.封装：分为CSP和COB
COB：DIE仅是感光芯片本身，封装成本低，因此价格较CSP低，高度低，节约空间。但对模组厂设备要求高，投入大。从而导致模组出厂价格最初高，待量大后反而较CSP的低。大厂通常采用这种。
CSP：COB+其他模块（例如玻璃）。价格较COB高。但是对环境要求低，对模组厂的设备要求低，生产周期短。缺点是模组高度高，透光性差。小厂通常采购这种封装。

4.对于一个5.0Msensor，其上有5百万个感光点，每个点上有一个microlensens(微镜头)，只有一种颜色（每个点一种颜色，而非3种颜色，另两种颜色是根据临近的数个点颜色值根据算法公式推算出来）。

5.blacklevel(黑电平）
对于摄像头感光芯片，理论上全黑环境下（输入光线为0），输出的采样数据应该为0。但在实际情况下这是无法达到的，尤其是在环境温度较高的情况下更无法达到。为了避免这一问题，在某个有效感光pixel旁放置几个无法感光外部光线的pixel。当输出采样值前先减去无效感光的blacklevel,方才是真正有效的图像信号。

6.关于RAW摄像头的tuning，展讯平台的专门工具----SpreadtrumISP tool。
调试重点-----镜头shading校正（由于镜头的物理特性，造成图像四周亮度相对中心亮度逐渐降低和图像色彩均匀度的变化。使用LNC校正，来使图像亮度和色彩均匀）
```## camera工作流程

```text
景物通过 Lens 生成的光学图像投射到 sensor 表面上， 经过光电转换为模拟电信号， 消噪声后经过 A/D 转换后变为数字图像信号，再送到数字信号处理芯片（ DSP） 中加工处理。所以，
从 sensor 端过来的图像是 Bayer 图像，经过
黑电平补偿 （ black level compensation）、
镜头矫正 （ lens shading correction）、
坏像素矫正 （ bad pixel correction）、
颜色插值 （ demosaic）、
Bayer 噪声去除、 
白平衡（ awb） 矫正、 
色彩矫正（ color correction） 、 
gamma 矫正、 
色彩空间转换（ RGB 转换为 YUV） 、 
在 YUV 色彩空间上彩噪去除与边缘加强、 
色彩与对比度加强，
中间还要进行自动曝光控制等
然后输出 YUV（ 或者 RGB） 格式的数据， 
再通过 I/O 接口传输到 CPU 中处理。
```## 相机模式

```text
1、夜拍
调优夜间拍照效果，去除燥点，提高亮度，增强饱和度，提高照片质量，可在不使用闪光灯
的情况下拍出很好的效果
2、超级夜景
通过手动调整ISO和快门时间，实现在光线较暗的情况下，拍摄出画质明亮而清晰的照片
3、美颜功能
强大的美颜算法，支持自拍时美白、瘦脸，磨皮、大眼功能
4、背景虚化
拍照时突出重点事物，虚化背景，主要用于拍摄人物，重要待突出的景物
人像模式
判断人像模式使用的哪几颗镜头可以试着单遮住一个后置镜头看看有没有画面的变化，虚化效果没有了的话就说明这个是用来测景深的
5、广角自拍
应用于前摄，类似于后置摄像头的全景模式，在拍下第一张自拍照后用户可以向左右两个方向移动手机扫描更宽广的画面最后成像并拼接图片
6、超像素
能把同像素景物拍出超高清图像，13M像素能合成52M像素
7、超级防抖
手机抖动时能拍出高清图片
8、留声相机
支持拍照后，可录一段语音（大概10秒）与照片关联，记录与照片相关信息
9、GIF 动画
支持多张照片合成处理，可将多张照片，拼成一个GIF的动画，可动态浏览
10、水印相机
11、Live shot
录像模式会有 Live shot 功能，就是录像的时候可以点击拍照键来获取 JPEG 图片
12、超级慢动作
华为之前有出一款 7680 帧的超级慢动作模式，当初在发布之前我还以为宣传册写错了，没想到啊，这 TM 竟然是真的，后来多方了解了下，华为是整了一款直出 1920 帧的 CMOS sensor，然后内部数据流处理应该是从 isp 到 SOC 后处理全部直通式不经过 DRAM，并且使用最新 C-PHY 标准，处理完毕的图像先一次性扔进 RAM 缓存，1S 大概 2.5G，RAM 里面先扔进去，然后再截取片段进行插帧处理到 7680 帧，即使是插帧也做得效果非常好，而且最终视频是 720P 的，清晰度我也看了下是很不错的，不得不说牛逼。
13、专业模式
专业模式其实就是开放一大部分参数给到用户自己去设置，比如常见的光圈、焦距、感光度、快门时间、锐度、镜头、白平衡等等。普通人一般用不到这个，这一大堆参数组合下来除非是专业摄影师，否则很难搞出来一张比自动模式更好的图片。


1.拍照PHOTO
普通照相模式，在自动或手动聚焦后还可长按屏幕某处调节亮度。

2.录像VIDEO
对图像和声音进行录制。

3.美肤BEAUTY
特效处理，对肤色加深或者减淡

4.美肤录像BEAUTY VIDEO
在录像的同时增加美肤特效。

5.HDR(High-Dynamic Range高动态范围图像）
一般我们照相，照顾了高光区域的曝光，暗部细节就会丢失，而照顾了暗部细节，高光部分就会曝光过度，为了解决这一问题，我们使用高动态光照渲染。简单地说，就是一张照片中，既包含了高光部分，又保留了暗部细节。它能将多张曝光不同的照片LDR（Low-Dynamic Range）叠加处理成一张精妙绝伦的图像，更贴近我们肉眼所看到的实景。

6.超级夜景NIGHT SHOT
按下快门按钮，系统会根据当前取景的光线条件选择合适的曝光时间参数，取景框中的夜景照片效果会越来越亮，越来越清晰。

7.流光快门LIGHT PAINTING
提供慢门长曝光功能，可以捕捉夜晚车灯移动的轨迹（TAIL LIGHT TRAILS）、进行光绘拍摄（LIGTH GRAFFITI）、拍出如丝般的流水效果（SILKY WATER）、拍摄银河星空(STAR TRACK）。

8.延时摄影TIME-LAPSE
低帧拍摄后以正常或者更高的速率播放画面。是和高速摄影相反的一种过程。

9.慢动作SLOW-MOTION
又名高速摄影。拍摄时加快摄影频率（FPS），回放时按照正常频率，即在同样的时间内拍摄更多的画面（更高的帧率）。常用来观看一些肉眼看不到的动作细节，如子弹穿过苹果瞬间，陶瓷落地破碎瞬间。每一个视频都有两个简单的指标来衡量，一个是分辨率；另外一个是帧率。想要更高的帧率，那么想保证画质，输出的分辨率就要调低。

10.有声照片AUDIO NOTE
在拍摄照片的同时录音。即在传统意义图片的基础上运用数字水印技术，对图片进行内容再创造，使普通图片完成升级改造、升华的一种图片。但目前现在很多平台都不支持有声照片，所以上发给别人或者上传到某个网上后变为跟普通的照片没有区别

11.连拍模式

12.全景模式

13.人像模式

14.美体

15.Sticker

16.特效
```## Camera相关术语

```text
Camera相关术语
https://blog.csdn.net/lisl812/article/details/108854377

R-FPC Rigid-flexiable printed circuit 软硬结合板 
FPC Flexiable printed circuit 软板 
FF Fixed Focus 定焦
AF Auto Focus 自动对焦
RGB Red Green Blue 红绿蓝三色元
RGBW Red Green Blue White 红绿蓝白四像素
PDAF Phase Detection auto focus 相位对焦
2PD Dual phse detection auto focus 双像素相位对焦
AWB Auto white balance 自动白平衡
LSC Luminance shading correction 亮度均匀性校准
Color Shading Color Shading 色彩均匀性校准
BlemishBlemish 坏点脏污
Color filter Color filter 滤光片
Photo diode Photo diode 光电二极管
EIS Electrical image stable 电子防抖
FSI Frontside illuminated 前照式
BSI Backside illuminated 背照式
Holder Holder 马达与sensor间的结构件
IR filter Infrared filter 红外滤光片
BG Blue glass 蓝玻璃滤光片
F# F number 光圈
TTL Total track length 镜头机械总长度
EFL Effective focal length 焦距
MTF Modulation Transfer Function 调制传递函数
TV Distortion TV Distortion 畸变
CRA Chief ray angle 主光角
6P 6 plastic 6片塑胶镜片
IH Image height 像高
RI Relative illuminance 相对亮度
DOF Depth of field 景深
Barrel Barrel 镜筒
VCM Voice coil motor 音圈马达
B-D Bi-directional 中置马达
C/L Closed Loop 闭环马达
OIS Optical image stable 光学防抖
OTP Once time programmed 一次性烧录
CSI Camera Serial Interface 相机串行接口
MIPI Mobile Industry Processor Interface 移动产业处理器接口
CCI Camera Control Interface 摄像头控制接口，一般即是I2C接口
CSIPHYMIPI协议的物理层
CSID MIPI协议层的一部分，用于解码数据流
AFAuto Focus 自动对焦
AWB Auto White Balance 自动白平衡
AEC Auto Exposure Control 自动曝光控制
RoI AF Region of Interest AF感兴趣区域
HDR High-Dynamic Range 高动态范围图像
ZSL Zero Shutter Later 零延迟拍照(高通)
ZSD Zero Shutter Delay 零延迟拍照 (MTK)
PDAF Phase Detection Auto Focus 相位对焦
AWB Auto White Balance 自动白平衡
CCT Color Correction Table 色彩校正表
CCM Color Correction Matrix 色差校正矩阵
ISP Image Signal Processing 图像信号处理
Pre-ISP Pre-Image Signal Processing 前期图像信号处理
Post-ISP Post-Image Signal Processing 后端图像信号处理
VFE Video Front-End of Camera Firmware 视频前端
CAC Chromatic Aberration Correction 色差校正
SNR Skin Noise Reduction 皮肤降噪
CPP Camera Post Processing 后端处理
BLC Black Level Correction 黑白校正
LSC Lens Shading Correction 镜头校正
ACE Advanced Chroma Enhancement 色度校正
SCE Skin Color Enhancement 皮肤颜色增强
MCE Memory Color Enhancement 记忆色彩增强
CS Chroma Suppression 色度抑制
WNR Wavelet Noise Reduction 小波降噪
DPC Defective Pixel Correction 缺陷像素校正
ABF Adaptive Bayer Filter 自适应Bayer滤镜
RNR Radial Noise Reduction 边缘降噪
ASF Advanced Streaming Format 高级流格式
FIR Finite Impulse Response 有限搏动反应滤波器
IIR Infinite impulse response 数字滤波器
RDI Raw Dump Interface 原始数据转储接口
MDP The Modular toolkit for Data Processing 数据处理包
PLV Preferred Vendor List 首选供应商名单
DNNF Deterministic, decomposable Negation Normal form 确定、分解的非正常形式
CNF Composite Nonlinear Feadback 复合非线性反馈控制
ICL Image Component Library 图像编码层
OMX OpenMax 多媒体应用程序标准
ExIF 一种图像格式
AXI Advanced eXtensible Interface 片内总线
AMBA Advanced Microcontroller Bus Architecture 高级微控制器总线架构
ASD Auto Scene Detection 自动场景检测
AFD Auto Frequency Detection 频闪自动检测
IQ Image Quality 图像质量
ICL Image C-Codec Layer 图像编解码层
BIMC Bus Integrated Memory Controller 总线集成内存控制器
GCDB Global Component Database 全局组件数据库
QRD Qualcomm Reference Design 高通参考设计
SOF Start of Frame 帧开始
FD Face Detection 人脸检测
GIC Green Imbalance Correction 绿不平衡校正
MCTL Media Control 媒体控制
PVL Preferred Vendor List 首选供应商名单
DSP Digital Symbol Processing 数字符号处理
ADSP Application DSP 不需要AP处理简单数据
VPE Video Processing Engine 视频处理引擎
CMOS Complementary Metal Oxide Semiconductor 互补金属氧化物半导体
CCD Charge coupled device 电荷耦合器件
DSC Digital Still Camera 数码相机
DSLR Digital Single-Lens Reflex 数码单反
OLPF Optical Low-pass Filter 低通滤波器
SNR Signal Noise Ratio 信噪比
DR Dynamic Range 动态范围
DP Defect Pixel 缺陷像素
HDR High Dynamic Range 高动态范围
DENOISE 去噪
BPC/DPC Bad/Defect Pixel Correction 坏点补偿
HUE 色相
HSV Hue Saturation Value 色相、饱和度、灰度
RGB Red Green Blue 红绿蓝三原色
MONO SENSOR 黑白传感器
ISP Image Signal Processor 图像信号处理器
GAMMA 伽马曲线
CONTRAST 对比度

camera常见名词缩写
https://www.jianshu.com/p/0b773aa1a2a4

CC, color conversion,色彩转换

CC, color correction,色彩矫正

CE, chroma enhancement,色度增强

SNR,signal-to-noise ratio,信噪比

SNR, skin noise reduce,肤色降噪

STD, standard deviation,标准差

OIS, optical image stabilization 光学稳像

PDAF,phase detection auto focus,相位对焦

CPP: camera post processor,摄像头后处理

ZSL: zero shutter log,零延时拍照

ABF: adaptive bayer filter，自适应bayer滤波器

CCM: color correction matrix

ASF: adaptive spatial filter,自适应空间滤波器

ACE,advanced chroma enhancement,高级色度增强

AEC, auto exposure control,自动曝光控制

AFD,automatic flicker detection,频闪自动检测

PLD,Physical Layer Driver,物理层驱动

BPC，坏点矫正

BCC,坏点对矫正

CFA,color fillter array色彩滤镜阵列

BAF,bayer AF

LA,luma adaptation,亮度调整

DBPC,动态坏点校正

DBCC,动态坏点簇校正

ABCC,assisted bad cluster correction,辅助坏点族校正

TM:目标模块

IAF:instant auto focus,即时AF

DDM, dense depth map

LCA,logic cell array,逻辑单元阵列

WNR,wavelet noise reduction,小波降噪

LUT,lookup table查找表

MCC, macbenth color checker,macbeth麦克白色卡

ND,中兴密度

UI,用户界面

CCT,correlated color temperature,关联色温

SWG,simple gray world,简单灰世界

ROI，Region of interest,感兴趣区域

SP,软件产品

BSP,开发包

AFR,auto FPS rate,自动帧率

MCE,memory color enhancement,记忆色增强

SCE,skin color enhancement,肤色增强

CT,Color Temperature,色温

IQ, image quality,图像品质

IS, image stabilization,图像稳定

HAF,hybrid auto focus,混合对焦

CAF,continuous auto focus,自动对焦

CAF(contrast AF)，持续AF

TAF,触控对焦

GM,golden 模组

RDI, raw dump interface,原始数据转存端口

QTI, Qualcomm Technologies Inc

DCC, defocus conversion coefficient

SLR, single-lens-reflex,单反

PD,phase detection,相位检测

PD,phase difference,相位差

BPP, bits per pixel

DAC,digital to analog converter

AFR,auto frame rate

AWB, automatic white balance,自动白平衡

CAC,color aliasing correction

CAC,color artifact correction

CAC, chromatrix aberration correction

GIC, green imbalannce correction

DPC, defective pixel correction

LTM, local tone mapping,局部色调映射

GTM,全局色调映射

VFE, Video front end,视觉前端

APL, average picture level

MLC,misleading color,误导性颜色。

DCIAF,dual camera instant auto focus

VPE,Video preprocessing 视频预处理

SAD,Sum of Absolute Difference

SADR, SAD with respect

HPF, High Pass Filter

RNR, radial noise Reduction

RMS,root mean squared

TOF(time-of-flight), 激光对焦

DCIF(duall camera instant AF),

MVAVG,moving average

HVX, hexagon vector eXtension

lc, line counter

FIR, finite impulse response,有限脉冲响应

IIR, infinite impulse response,无限脉冲响应

FIR, finite impulse response digital filter

image
ADRC, automatic dynamic range compression,自动动态范围压缩

AOST, advanced optional software technologies,高级可选软件技术

BLSS, black level subtraction and scaling,黑电平减法和压缩

DRC, dynamic range compression,动态范围压缩

HVX, hexagon vector extension,6角延伸

TNR, temporal noise reduction,时域降噪

IR, infrared filter,红外线过滤

INTG, integration time,

AFS, auto focus stats

CS, chroma suppression

LCE, local contrast enhancement

PDPC, phase detection pixel correction

GIC, green imbalance correction

LNR, level-based noise reducton

MCTL, media control

zzHDR, zigzag HDR

pvl, preferred vendor list,优选供应商列表。

FD, face detection

FIR, finite impulse response

HVX, hexgon vector extension

HDR, high dynamic range,高动态范围

IIR, infinite impulse response

LSB, least significant bit

MIPI, mobile industry processor interface

MSB, most significant bit

AIG, adaptive input gain

LC,line count

UI,user interface

SGW, simple gray world

CE, chromatrix enhancement

HAL,hardware abstraction layer,硬件抽象层

QCDB, global components database,全局组件数据库

IRQ, interrupt request,中断请求

QRD, qualcomm reference desigh,高通参考设计

SOF,start of frame,帧开始

NVM, non-volatile memory

ASD,auto scene detection,自动场景侦测

SDK, software developers kit

MWB, manual white balance

MBDRC, multiband dynamic range control

KPI, key performance indicator

FB, FrameBuffer

EDID, extended display identification data

MDP, mobile display processing

GPU, graphics processing unit

SDR, satic dynamic range

WCG, wide color gamut

HFR, high frame rate

LLV, low light vision

LLP(snapdragon), low light photo

UDCF, universal dual camera framework

EIS, electronic image stabilization

DIS, digital image stabilization

EXIF, exchangeable image file

HJR, hand jitter reduction

singel frame HJR，在弱光条件下增强噪声性能

LED, light emitting diode

UBWC, universal bandwidth compression

CAMIF, camera interface hardware

CSID, camera serial interface decoder

DOF, depth of field,景深

ISPIF, isp interface

NVM, nonvolative memory

RDI, raw data interface

PDLIB, phase detection library

CIS, cmos image sensor

DPC, defect pixel correction

pip, picture in picture,画中画

ISP, image signal processor

QFIL, Qualcomm flash image loader

ISO, international standards organization

SOF, start of frame,帧开始

BL, black level

OECF, opto-electronic conversion function

OEM, original equipment manufacturer

CCI, camera control interface, 摄像头控制接口

ICL, imaging codec layer,图像编解码层

CDF,Cumulative Distribution Function

LSC,lens shading correction镜头阴影矫正

DPCM,Differential Pulse Code Modulation

IS, image stabilization,图像稳定

GCDB,global components database,全局组件数据库

IRQ,interrupt request,中断请求

QRD,qualcomm reference design,高通参考设计。

DT, data type

VC,Virtual Channel

CID,Channel ID

MTP, modem test platform device

HWI, hardWare interface

CDT, configuration data table

GPIO, general purpose input-output

DTC, device tree compile

MCT, media controller

TDN, temporal wavelet denoise

VCM, voice coil motor,音圈马达

CDS: color down sample. 它会跳过UV通道中两个像素之间的一个像素，这绝对会影响颜色。 我们强烈建议客户慎重使用它。 只建议在极端黑暗的环境下使用，以消除由于饱和导致的噪音。 所以请使用自动模式并通过微调isp头中的触发条件来触发它。

AGW,advance gray world

DFS,dynamic frame skip

SVHDR:Staggered video HDR

RTB,Real-Time Bokeh

EV, exposure value

NA, not applicable

SOF,start of frame,帧开始

CTS,Compatibility test suite

OMX,openMAX

UDCF, universal dual camera framework

FOVC,Field-of-view-control

OECF,Opto-Electronic Conversion Function

PDPC,Phase Detection Pixel Correction

VCM

SAC, smart actuator control

LSC, linear slope control

POR, power on resset

OCP, over current protection

UVLO, under voltage lockout

SRC, slew rate control


Camera基础及基本概念
https://zhuanlan.zhihu.com/p/348230440

数字信号处理芯片DSP(DIGITAL SIGNAL PROCESSING)功能：主要是通过一系列复杂的数学算法运算，对数字图像信号参数进行优化处理，并把处理后的信号通过USB等接口传到PC等设备。DSP结构框架:

1. ISP(image signal processor)(镜像信号处理器)

2. JPEG encoder(JPEG图像解码器)

3. USB device controller(USB设备控制器) 或者其他接口

常见的摄像头传感器类型主要有两种，

一种是CCD传感器（Chagre Couled Device），即电荷耦合器。

一种是CMOS传感器（Complementary Metal-Oxide Semiconductor）即互补性金属氧化物半导体。

CCD的优势在于成像质量好，但是制造工艺复杂，成本高昂，且耗电高。在相同分辨率下，CMOS价格比CCD便宜，但图像质量相比CCD来说要低一些。CMOS影像传感器相对CCD具有耗电低的优势，加上随着工艺技术的进步，CMOS的画质水平也不断地在提高，所以目前市面上的手机摄像头都采用CMOS传感器。


景物通过 Lens 生成的光学图像投射到 sensor 表面上， 经过光电转换为模拟电信号， 消噪声后经过 A/D 转换后变为数字图像信号，再送到数字信号处理芯片（ DSP） 中加工处理。所以，从 sensor 端过来的图像是 Bayer 图像，经过黑电平补偿 （ black level compensation）、镜头矫正 （ lens shading correction）、坏像素矫正 （ bad pixel correction）、颜色插值 （ demosaic）、Bayer 噪声去除、 白平衡（ awb） 矫正、 色彩矫正（ color correction） 、 gamma 矫正、 色彩空间转换（ RGB 转换为 YUV） 、 在 YUV 色彩空间上彩噪去除与边缘加强、 色彩与对比度加强，中间还要进行自动曝光控制等， 然后输出 YUV（ 或者 RGB） 格式的数据， 再通过 I/O 接口传输到 CPU 中处理。

二、以下对各个模块的处理算法做简要概述
1）Bayer
图像在将实际的景物转换为图像数据时， 通常是将传感器分别接收红、 绿、 蓝三个分量的信息， 然后将红、 绿、 蓝三个分量的信息合成彩色图像。 该方案需要三块滤镜， 这样价格昂贵，且不好制造， 因为三块滤镜都必须保证每一个像素点都对齐。

通过在黑白cmos 图像传感器的基础上， 增加彩色滤波结构和彩色信息处理模块就可以获得图像的彩色信息， 再对该彩色信息进行处理， 就可以获得色彩逼真的彩色图像。通常把彩色图像传感器表面覆盖的滤波称为彩色滤波阵列（ Color Filter Arrays， CFA） 。

目前最常用的滤镜阵列是棋盘格式的， 已经有很多种类的， 其中绝大多数的摄像产品采用的是原色贝尔模板彩色滤波阵列（ Bayer Pattern CFA） ， 如图2 所示， R、 G、B 分别表示透红色、 透绿色和透蓝色的滤镜阵列单元， 图3 比较形象地展示了此过程。由于人的视觉对绿色最为敏感， 所以在Bayer CFA 中G 分量是R 和B 的二倍， 在每个像素点上只能获取一种色彩分量的信息，然后根据该色彩分量的信息通过插值算法得到全色彩图像。

2）BLC(Black level Correction)

a.暗电流

物理器件不可能是理想的， 由于杂质、 受热等其他原因的影响， 即使没有光照射到象素， 象素单元也会产生电荷， 这些电荷产生了暗电流。 而且， 暗电流与光照产生的电荷很难进行 区分。

b.Black Level

Black Level 是用来定义图像数据为0 时对应的信号电平。由于暗电流的影响， 传感器出来的实际原始数据并不是我们需要的黑平衡（ 数据不为0） 。 所以，为减少暗电流对图像信号的影响，可以采用的有效的方法是从已获得的图像信号中减去参考暗电流信号。一般情况下， 在传感器中， 实际像素要比有效像素多， 如下图所示， 像素区头几行作为不感光区（ 实际上， 这部分区域也做了RGB 的 color filter） ， 用于自动黑电平校正， 其平均值作为校正值， 然后在下面区域的像素都减去此矫正值， 那么就可以将黑电平矫正过来了。

下面所列图是做了black level 矫正与没做black level 矫正的对比， 很明显， 左边没做black level矫正的图片会比较亮， 影响图像的对比度：

3）LSC(Lens Shading Correction)

由于镜头本身的物理性质， 造成图像四周亮度相对中心亮度逐渐降低， 以及， 如下图所示， 由于图像光照在透过镜头照射到pixel 上时， 边角处的焦点夹角大于中心焦点夹角， 造成边角失光。 表现在图像上的效果就是亮度从图像中心到四周逐渐衰减， 且离图像中心越远亮度越暗。 为了补偿四周的亮度， 需要进行Lens Shading 的矫正。

Lens Shading 的矫正的方法是根据一定的算法计算每个像素对应的亮度矫正值， 从而补偿周边衰减的亮度。

矫正方法有二次项矫正、 四次项矫正。

4）BPC(Bad Pixel Correction)

a.坏点

坏点为全黑环境下输出图像中的白点， 高亮环境下输出图像中的黑点。

b.坏点修复方法

一般情况下，RGB 信号应与景物亮度呈线性响应关系， 但由于Senor 部分pixel 不良导致输出的信号不正常， 出现白点或黑点。

坏点修复方法通常有两种：

一种是自动检测坏点并自动修复， 另一种是建立坏点像素链表进行固定位置的坏像素点修复， 这种方式是OTP 的方式。

c.坏像素矫正原理

下面以自动检测坏点修复方法为例， 阐述坏像素矫正算法原理。

5）颜色插值

当光线通过 Bayer型 CFA（Color Filter Arrays） 阵列之后， 单色光线打在传感器上， 每个像素都为单色光， 从而理想的Bayer 图是一个较为昏暗的马赛克图。

6）Bayer Denoise

使用 cmos sensor获取图像，光照程度和传感器问题是生成图像中大量噪声的主要因素。同时， 当信号经过ADC 时， 又会引入其他一些噪声。 这些噪声会使图像整体变得模糊， 而且丢失很多细节， 所以需要对图像进行去噪处理空间去噪传统的方法有均值滤波、 高斯滤波等。

但是， 一般的高斯滤波在进行采样时主要考虑了像素间的空间距离关系， 并没有考虑像素值之间的相似程度， 因此这样得到的模糊结果通常是整张图片一团模糊。 所以， 一般采用非线性去噪算法， 例如双边滤波器， 在采样时不仅考虑像素在空间距离上的关系， 同时加入了像素间的相似程度考虑， 因而可以保持原始图像的大体分块， 进而保持边缘。

7）AWB(Automatic White Balance)

白平衡的基本原理是在任意环境下， 把白色物体还原成白色物体， 也就是通过找到图像中的白块， 然后调整R/G/B 的比例， 如下关系： R’= R * R_Gain G’ = G * G_Gain B’ = B * B_Gain R’ = G’= B’

AWB 算法通常包括的步骤如下：

(1)色温统计： 根据图像统计出色温；

(2)计算通道增益： 计算出R 和B 通道的增益；

(3)进行偏色的矫正： 根据给出的增益， 算出偏色图像的矫正。

8）Color Correction

由于人类眼睛可见光的频谱响应度和半导体传感器频谱响应度之间存在差别，还有透镜等的影响， 得到的RGB 值颜色会存在偏差， 因此必须对颜色进行校正， 通常的做法是通过一个3x3 的颜色变化矩阵来进行颜色矫正。

9）Gamma Correction

人眼对外界光源的感光值与输入光强不是呈线性关系的， 而是呈指数型关系的。 在低照度下， 人眼更容易分辨出亮度的变化， 随着照度的增加， 人眼不易分辨出亮度的变化。 而摄像机感光与输入光强呈线性关系， 为方便人眼辨识图像， 需要将摄像机采集的图像进行gamma 矫正。

Gamma 矫正是对输入图像灰度值进行的非线性操作， 使输出图像灰度值与输入图像灰度值呈指数关系：

Vout =AVin

这个指数就是 Gamma， 横坐标是输入灰度值， 纵坐标是输出灰度值， 蓝色曲线是gamma 值小于1 时的输入输出关系， 红色曲线是gamma 值大于1 时的输入输出关系。 可以观察到， 当gamma 值小于1 时(蓝色曲线)， 图像的整体亮度值得到提升， 同时低灰度处的对比度得到增加， 更利于分辩低灰度值时的图像细节。

#####10）色彩空间转换

YUV 是一种基本色彩空间， 人眼对亮度改变的敏感性远比对色彩变化大很多， 因此， 对于人眼而言， 亮度分量Y 要比色度分量U、V 重要得多。 所以， 可以适当地抛弃部分U、V分量， 达到压缩数据的目的。

Laplacian 算子

YCbCr 其实是YUV 经过缩放和偏移的改动版，Y 表示亮度，Cr、Cb 表示色彩的色差， 分别是红色和蓝色的分量。 在YUV 家族中，YCbCr 是在计算机系统中应用最多的成员， 其应用领域很广泛，JPEG、MPEG 均采用此格式。 一般人们所讲的YUV 大多是指YCbCr。YCbCr有许多取样格式，。

如 4∶4∶4，4∶2∶2， 4∶1∶1和 4∶2∶0。

RGB 转换为YCbCr 的公式如下：

r 0.5 0.4178 0.0813 128

b 0.1678 0.33113 0.5 128

0.299 0.587 0.114

C R G B

C R G G

Y R G B

色彩空间转换这个模块， 是将RGB 转换为 YUV444， 然后在YUV 色彩空间上进行后续的彩色噪声去除、 边缘增强等， 也为后续输出转换为jpeg 图片提供方便。

11）Color Denoise

为了抑制图像的彩色噪声， 一般采用低通滤波器进行处理。 例如使用M×N的高斯低通滤波器在色度通道上进行处理。

12）LLS

长曝光，摄影术语，是在摄影中选慢快门（曝光时间长）从而达到特殊摄影效果的一种摄影方法。该方法好处就是可以把光线暗的景色拍的更清晰，也可以拍出如梦幻般的画面，比如瀑布和城市公路夜景。

胶片的感光度是固定的，如果是数码相机可以调感光度来清晰影像，但是高感光度会增加噪点。拍摄夜景的时候经常用长曝光。通过选慢快门和小光圈来实现。

涉及到的feature，LLS + MFNR；

VCSEL就是「垂直共振腔面射型雷射（VerticalCavitySurfaceEmittingLaser）」的缩写

LTM 局部色调映射(Local Tone Mapping)

HE 直方图均衡(HE) 具有调整图像灰度，增强对比度的作用。

BPS Bayer processing segment Bayer processing : Lens shading correction, bad pixel correction, PDAF pixel correction, zzHDR merge/record, bayer NR, green imbalance correction, black level, and channel gain;

Color processing : Chromatic aberration correction, 2D LUT , chroma suppression, and skin color enhancement

CPP Camera post processor hal3之前有的概念，hal3之后用其他处理单元替换；

DE Detailed enhancement

EIS Electronic image stabilization

IFE Image front-ent engine hal3之后，重新定义的处理单元；Bayer processing for video/preview、 stats（for 3A）、Four tap-in/out points for Qualcomm Hexagon Vector eXtensions（HVX） Streaming

IPE Image processing engine hal3之后，重新定义的处理单元；1、NPS（Noise processing segment） ：NR、EIS、Multiframe processing 2、PPS（Post processing segment）：LTM、Color processing、Detailed enhancement （ASF）、scaler

MCTF Motion compensation temporal filtering

Multiframe noise reduction

NR Noise reduction

PPS Post processing segment

VFE Video front end

ZSL Zero shuter lag

instant auto focus 及时自动对焦

 

缩略词

https://zhuanlan.zhihu.com/p/265877501

CRM[Camera Request Manager]创建了一个V4L2主设备用来管理所有的子设备，并且暴露设备节点video0 给用户空间，同时内部维护着整个底层驱动业务逻辑

Camera Sync创建了一个V4L2主设备，同时暴露了设备节点video1给用户空间，主要用于向用户空间反馈图像数据处理状态

子设备模块[sensor actuator eeprom]被抽象成v4l2_subdev设备，同样也暴露设备节点v4l2-subdev给用户空间进行更精细化的控制

PO: Purchase order

SIP: System-in-package

UMD : user mode driver

KMD : kernel mode driver

DRM : Dense reader mode

IFH：Image Front End

EEPROM：EEPROM to store the calibration data of ImageSensor

CSIPHY：CSIPHY Camera Serial Interface Physical receiver

CSID： Camera Serial Interface Decoder

VFE： Video Front End

CPP：Camera Post Processor

ISPIF： Image Signal Processor Interface

ICP : Image Control Processor

JPEGE：JPEG device

JPEGD：JPEG decoder device

LRME : Low Resolution Motion Estimation

OIS: Optical image stabilization

FD: Face detection device

CHI: Camera hardware interface

CSL: Camera service layer

CDM: Camera data mover

VPU: Video Processing Unit(Codec)

DPU: Display Processing Unit

BPS: Bayer Processing Segment

CPAS:相机外围设备和支持

OPE: offline processing engine
————————————————
版权声明：本文为CSDN博主「一点一滴地累积」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/dzning123/article/details/117884489
```## camx相关问题汇总

```text
1、YUV相关的
        1.1.自定义dump yuv方法：
        1.2.高通 dump 相关的 yuv数据到data/vendor/camera/路径下
    2.查看哪些应用连接camera：
    3.看创建的pipeline：
        3.1
        3.2 查看pipeline、node和link
        3.3 查看usecase相关信息
    4.显示mfnr、mfsr实际帧数：
    5.camera buffer 相关问题
        5.1.异常log汇总：
        5.2.具体代码：
    6.camera streams 关键字
    7.打印camera 堆栈信息关键字
    8.如何在log中打印FPS
    9.打开高通log打印
    10.打开chi log:
    11.打开ALOGV 打印功能
    12.camx 调试

1、YUV相关的
1.1.自定义dump yuv方法：

//1.dump yuv方法
static int  requestId = 0;

if(property_get_int32("persist.vendor.camera.swfd.dump",0))
{
    CHAR    inputFilename[FILENAME_MAX];
    FILE*   pInputFileFD;
    OsUtils::SNPrintF(inputFilename, sizeof(inputFilename),
                      "%s%sfdtm%s_%llu_input_width_%d_height_%d_stride_%d_scanline_%d.yuv",
                      FileDumpPath,   PathSeparator,   NodeIdentifierString(),    requestId,
                      m_FDFrameWidth, m_FDFrameHeight, m_FDFrameStride,           m_FDFrameScanline);
    pInputFileFD  = OsUtils::FOpen(inputFilename, "wb");
    if (NULL != pInputFileFD)
    {
        OsUtils::FWrite(perFrameSettings->pImageAddress, m_FDFrameStride * m_FDFrameHeight, 1, pInputFileFD);

        OsUtils::FClose(pInputFileFD);
    }
    //OsUtils::GetTime(&startTime);
    requestId ++;
}

//2.使用的时候打开开关
adb shell setprop  persist.vendor.camera.swfd.dump 1

1.2.高通 dump 相关的 yuv数据到data/vendor/camera/路径下

1).总开关

// 0 代表false  1 代表 true
adb shell setprop  persist.vendor.camera.autoImageDump 1

2.echo IFERegDumpMask=0x2 >> camxoverridesettings.txt

3.ps -ef |grep cam // 显示camera相关的进程

4.kill cam进程

adb shell killall android.hardware.camera.provider@2.4-service_64 cameraserver

5.打开Camera APK 自动dump 数据

6.具体配置文件如下：
src\settings\common\camxsettings.xml

<setting>
    <Name>Auto Output Image Dump Node/Port Mask</Name>
    <Help>
        Will limit dumps to only the specified nodes and ports when autoImageDump is enabled
        Uses ImageDumpType to define the flags
        No dumps                   = 0x0
        All output ports for IFE           = 0x1
        All output ports for IPE           = 0x2
        All output ports for BPS           = 0x4
        All JPEG output ports for all JPEG nodes   = 0x8
        All output ports for FDHw           = 0x10
        All output ports for LRME           = 0x20
        All output ports for RANSAC          = 0x40
        All output ports for all ChiNodes       = 0x80
        All output ports for CVP           = 0x100
        All other nodes not explicitly listed above  = 0x40000000
    </Help>
    <VariableName>autoImageDumpMask</VariableName>
    <VariableType>UINT</VariableType>
    <SetpropKey>persist.vendor.camera.autoImageDumpMask</SetpropKey>
    <DefaultValue>0x400001ff</DefaultValue>
    <Dynamic>FALSE</Dynamic>
</setting>

2.查看哪些应用连接camera：

adb logcat |grep -i "CameraService::connect call"  //查看api和camera id

3.看创建的pipeline：
3.1

// 命令：
adb logcat |grep -i "CreateDescriptor"
// 具体代码如下：
CDKResult Pipeline::CreateDescriptor()
{
    CHX_LOG_CONFIG("Pipeline[%s] pipeline pointer %p numInputs=%d, numOutputs=%d stream w x h: %d x %d",
            m_pPipelineName, this, pipelineCreateData.numInputs, pipelineCreateData.numOutputs,
            pipelineCreateData.pOutputDescriptors->pStream->width,
            pipelineCreateData.pOutputDescriptors->pStream->height);
}

3.2 查看pipeline、node和link

camxpipeline.cpp

"Topology: Creating Pipeline %s, numNodes %d isSensorInput %d isRealTime %d",    //查看pipeline和node数
"Topology::%s Node::%s Type %d numInputPorts %d numOutputPorts %d",
"Topology: Pipeline[%s] Link: Node::%s(outPort %d) --> (inPort %d) Node::%s using format %d"  //查看所有pipeline和link node

3.3 查看usecase相关信息

chxsensorselectmode.cpp

//1.查看最终选择的usecase（见底部SensorModeSelectUseCase）和sensormode以及modeIndex
"cameraId:%d, Selected Usecase: %d, SelectedMode W=%d, H=%d, FPS:%d, NumBatchedFrames:%d, modeIndex:%d"   
//2.最终选择的usecaseId
CHX_LOG_INFO("usecase ID:%d",usecaseId);  

4.显示mfnr、mfsr实际帧数：

adb root
adb shell setprop persist.debug.sf.showfps 1
// 1.
adb logcat | findstr "PROFILE_PREVIEW_FRAMES_PER_SECOND"
// 2.
adb logcat |grep -iaE "num of rdi|FPS" // 需要修改

5.camera buffer 相关问题
5.1.异常log汇总：

Camera3-Stream: getBuffer: wait for output buffer return timed out after 8000ms (max_buffers 8)

   

5.2.具体代码：

status_t Camera3OutputStream::returnBufferCheckedLocked()
{
    // queueBufferToConsumer方法是否正常执行，判定流
    res = queueBufferToConsumer(currentConsumer, anwBuffer, anwReleaseFence, surface_ids);
    if (shouldLogError(res, state)) {
        ALOGE("%s: Stream %d: Error queueing buffer to native window:"
              " %s (%d)", __FUNCTION__, mId, strerror(-res), res);
    }  
}

6.camera streams 关键字

configure_streams|configureStreamsPerfLocked|

7.打印camera 堆栈信息关键字

1).顺着Pid(进程ID)、Tid(线程ID)、Uid(用户id)信息继续往下跟踪。

backtrace|signal|SIGSEG

2).查看cameraprovider是否重启

adb shell ps -ef |grep -i  cam

8.如何在log中打印FPS

1).首先从 /vendor/etc/camera/ 下面 pull 出camxoverridesettings.txt

adb pull /vendor/etc/camera/camxoverridesettings.txt

2).在该文件中添加如下两行：

enableFPSLog=TRUE
logPerfInfoMask=0xFFFFFFFF

3).再将camxoverridesettings.txt push到/vendor/etc/camera/，然后重启手机/重启provider进程。

4).在log中搜索 CalculateResultFPS 就能看到当时的帧率了：

CamX: camxsession.cpp CalculateResultFPS() FPS: 43.40

5).adb 命令也可以查看

adb logcat |grep -i "FPS"
adb logcat |grep "CalculateResultFPS"

9.打开高通log打印

adb shell setprop persist.vendor.camera.logInfoMask 0xFFFFFFFF //AF info level log
adb shell setprop persist.vendor.camera.logVerboseMask 0xFFFFFFFF //AF verbose level log
adb shell setprop persist.vendor.camera.logEntryExitMask 0xFFFFFFFF
adb shell setprop persist.vendor.camera.logWarningMask 0xFFFFFFFF
adb shell setprop persist.vendor.camera.logConfigMask 0xFFFFFFFF
adb shell setprop persist.vendor.camera.systemLogEnable TRUE
adb shell setprop persist.vendor.camera.logLogDRQMask 0xFFFFFFFF

10.打开chi log:

adb shell "echo overrideLogLevels=0x1f >> /vendor/etc/camera/camxoverridesettings.txt"
或：adb shell setprop vendor.debug.camera.overrideLogLevels 0x1F (camxsettings.xml中定义，不同的代码可能有区别)

11.打开ALOGV 打印功能

#undef NDEBUG // 打开LOGV/LOGI/LOGD
#define LOG_NDEBUG 0 // 打开LOGV
#define LOG_NIDEBUG 0 // 打开LOGI
#define LOG_NDDEBUG 0 // 打开LOGD
#define LOG_NEDEBUG 0 // 打开LOGE
#include <utils/Log.h>

12.camx 调试

修改 \vendor\qcom\proprietary\camx\src\core\camxsettings.xml 设置 log 打印级别，如：

overrideLogLevels=0x1F
logInfoMask=0x40080
logVerboseMask=0x40000
```## 深入理解Android相机体系结构

```text
https://blog.csdn.net/u012596975/article/details/107135938

相机简史 https://blog.csdn.net/u012596975/article/details/107136261
安卓相机架构概览 https://blog.csdn.net/u012596975/article/details/107136568
应用层 https://blog.csdn.net/u012596975/article/details/107137110
服务层 https://blog.csdn.net/u012596975/article/details/107137156
硬件抽象层 https://blog.csdn.net/u012596975/article/details/107137523
硬件抽象层实现 https://blog.csdn.net/u012596975/article/details/107138576
驱动层 V4L2框架: https://blog.csdn.net/u012596975/article/details/107137555                 
高通KMD: https://blog.csdn.net/u012596975/article/details/107138655                
硬件层 https://blog.csdn.net/u012596975/article/details/107137883
安卓相机架构总结 https://blog.csdn.net/u012596975/article/details/107138177
手机相机的未来与发展 https://blog.csdn.net/u012596975/article/details/107138203
```## Android 的图形组件

```text
如果把开发者编写的应用程序图形效果展示过程当做是一次酣畅淋漓的画作过程，那么绘画过程中 Android 的各个角色又是怎么分工合作的 ：

画笔
Skia : CPU 绘制 2D 图形；
Open GL : GPU 绘制 2D / 3D 图形；
画纸
Surface : Android 4.4+ 应用程序都在 Surface 这张画纸上进行绘制和渲染。
画板
Graphic Buffer : 在屏幕刷新机制提到，Android 4.1+ 后有 3 块 Graphic Buffer 用于应用程序图形绘制，或 SurfaceFlinger 的合成和显示。
合成及显示
SurfaceFlinger : 合成所有图层并进行显示。（Surface 的投递者）

Image Stream Producers ： 图形流生产者，应用程序内绘制到 Surface 的图形( xml / java 实现的图形，或者是视频 )
Window Manager ： 在Android Window 机制探索这篇文章中说道 ——「Window是View的直接管理者。」，Window 是 View的容器，每个窗口都会包含一个 Surface 。Window Manager 管理窗口的各个方面，包括生命周期，输入和焦点事件，屏幕旋转，切换动画，位置，转换，Z-Order等。Window Manager 会将 Window 的这些元素数据传递给 SurfaceFlinger 。
SurfaceFlinger ： 根据Window Manager 提供的内容将它们合成并输出到显示屏上。它使用 OpenGL 和 HardWareComposer 来合成 Surface 。（其它消费者也有可能是OpenGL ES 应用，例如相机或者其它），开头有提到硬件加速指的是应用程序内图形渲染加速的过程，而 SurfaceFlinger 一直是通过 OpenGL 来合成和输出图形。

HWC ： Hardware Composer ，硬件合成器。（了解即可），这是显示控制器系统的硬件抽象。SurfaceFlinger 会委派一些合成的工作给 Hardware Composer 以此减轻 GPU 的负载。这样会比单纯通过 GPU 来合成消耗更少的电量。
Gralloc ： Graphics memory allocator 用来分配图形的内存。

应用程序可以通过Skia来绘制2D图形，也可以用OpenGL来绘制2D / 3D图形（应用加速指的是应用内使用OpenGL处理和渲染图形）
SurfaceFlinger 会通过OpenGL来混合图形到指定的Surface上送往HWC进行合成。
```## 防抖

```text
EIS(Electronic Image Stabilization)
电子防抖主要指数码相机上采用强制提高CCD感光参数、同时加快快门并针对CCD上取得的图像进行分析，然后利用边缘图像进行补偿的防抖，电子防抖实际上是一种通过降低画质来补偿抖动的技术，此技术试图在画质和画面抖动直接取得一个平衡点。与光学防抖相比，成本低，效果差。

OIS(Optical Image Stabilization)
光学防抖技术是在镜头内的陀螺仪侦测到微小的移动时，会将信号传至微处理器立即计算需要补偿的位移量，然后通过补偿镜片组，根据镜头的抖动方向及位移量加以补偿，从而有效的克服因相机的振动产生的影像模糊。

防抖类型
镜头防抖
通过镜头组实现防抖主要是以佳能和尼康为代表，它们依靠磁力包裹悬浮镜头，从而有效克服因相机振动产生的图像模糊，这对于大变焦镜头的数码相机所能起到的效果更加明显。通常，镜头内的陀螺仪侦测到微小的移动，并且会将信号传至微处理器立即计算需要补偿的位移量，然后通过补偿镜片组，根据镜头的抖动方向及位移量加以补偿，补偿镜组相应调整位置和角度，使光路保持稳定，从而有效的克服因相机的振动产生的影像模糊。

CCD防抖
通过CCD实现防抖，只有柯尼卡美能达及宾得能够做到，它的原理与佳能、松下的光学防抖动技术相反，是依靠CCD的浮动达到防抖的目的。原理是将CCD先固定在一个能上下左右移动的支架上，通过陀螺仪感应相机抖动的方向及幅度，然后传感器将这些数据传送至处理器进行筛选、放大，计算出可以抵消抖动的CCD移动量。 [2]

电子防抖
所谓电子防抖，就是说防抖的全过程都没有任何元部件的辅助和参与，依靠数字处理的技术去实现的防抖，当前电子防抖主要有通过提高相机感光度（ISO）而实现的“自然防抖”和通过像素补偿或其他运算方式而实现的“数码防抖”两大种类。 [1]

双重防抖
所谓“双重防抖”，就是由“光学防抖”和“高感光度”两种技术共同组成的数码相机防抖系统。其中，“光学防抖”是一种比较复杂的技术，它依靠相机内置的精密陀螺仪和一组可移动镜片，来计算并修正手抖造成的光线偏移，避免模糊；而高感光度防抖的原理比较简单，就是通过增加感光度ISO值来提高快门速度，同样能达到防抖效果
```

## 编解码器

```text
什么是编解码器？
编解码器是硬件设备或将输入数据处理成输出数据的计算机程序。编码数据流或用于传输和存储的信号（可能是加密形式）的编解码器称为编码器，解码器功能反转编码以进行重放或编辑。编解码器广泛用于视频会议，流媒体和视频编辑应用等应用。以下是几种不同类型的视频编解码器：H.264编码器和解码器，MPEG编码器和解码器，MJPEG编码器和解码器。

Android中的Mediacodec
Android包括Stagefright，一种原生级别的媒体播放引擎，内置基于软件的流行媒体格式编解码器。 Stagefright音频和视频播放功能包括与OpenMAX编解码器的集成，会话管理，时间同步渲染，传输控制和DRM（称为数字限制管理或数字版权管理）。 Stagefright还支持设备供应商提供的自定义硬件编解码器的集成。

MediaCodec类
MediaCodec类可用于访问低级媒体编解码器，即编码器/解码器组件.MediaCodec类首先在Android 4.1（API 16）中可用。 mediacodec类的主要目的是访问设备中的底层硬件和软件编解码器。 因此，如果想在Android应用程序中使用自定义硬件/软件编解码器，则需要将编解码器注册到Android Framework。 这可以通过以下步骤完成。

在Android中注册您的编解码器的步骤
在Android框架中，编解码器通过media_codecs.xml注册。 以下是来自media_codec.xml文件的示例编码器和解码器块。
在标准的Android发行版中，可以在此处找到示例media_codecs.xml。 Stagefright服务解析系统/ etc / media_codecs.xml和system / etc / media_profiles.xml，以通过android.media.MediaCodecList和android.media.CamcorderProfile类将设备上支持的编解码器和配置文件公开给应用程序。 因此，您需要创建/编辑自己的media_codec.xml文件，并在AOSP构建期间将其复制到系统映像的system / etc目录中。

例子
要注册视频编解码器，您必须在解码器列表下添加新条目。 如果编码器在编码器列表下添加新条目。 为确保始终选择您的编解码器，请确保您的编解码器被列为特定MIME类型的第一个条目。 以下是media_codecs.xml文件中H.264编码器和解码器的示例。
<encoders>
    <MediaCodec name="OMX.vendor-name.h264.encode" type="video/avc" >
         <Limit name="size" min="48x48" max="3840x2176" />
       <Limit name="bitrate" range="1-50000000" />
    </MediaCodec>
</encoders>

<Decoders>
     <MediaCodec name="OMX.vendor-name.h264.decoder" type="video/avc" >
            <Limit name="size" min="32x32" max="3840x2176" />
            <Limit name="bitrate" range="1- 62500000" />
        </MediaCodec"bitrate" range="1-50000000" />
    </MediaCodec>
</Decoders>

其中，OMX.vendor-name.H264.encoder和OMX.vendor-name.H264.Decoder是组件的名称。 video / avc是组件的MIME类型。在该示例中，它表示AVC / H.264视频。接下来的两个语句表示编解码器的怪癖或特殊要求。现在您刚刚将自定义编解码器注册到了android框架。 ifile的。下一步是将您的编解码器集成到OMX层中。

OMX组件
什么是OpenMAX（OMX）？
OpenMAX（开放媒体加速）是一种免版税的跨平台（C语言编程接口）开放标准，用于加速嵌入式和移动设备上多媒体应用中的音频，视频和图像的捕获和呈现。 OpenMAX由非营利性技术联盟Khronos Group管理。 OpenMAX提供三层接口：

应用层（AL）
OpenMAX AL是多媒体应用程序（如媒体播放器）和平台媒体框架之间的接口。在Anroid中，该层暴露为mediacodec类。

整合层（IL）
OpenMAX IL是媒体框架和一组多媒体组件（如音频或视频编解码器）之间的接口。例如，在我们的例子中，它是Android上的StageFright或MediaCodec API。对于Windows，它是DirectShow。同样，Linux上的FFmpeg或Libav，或跨平台的GStreamer）。因此，如果要向Android OMAX层添加任何硬件编解码器支持，则必须在此层中完成。为此，您必须创建OMX组件和一个OMX插件，将您的自定义编解码器与Stagefright框架连接在一起。例如组件，可以参考Galaxy Nexus的示例插件，这里：hardware / ti / omap4xx / libstagefrighthw。

在OMAX IL层中添加自己的编解码器

根据OpenMAX IL组件标准创建组件。组件接口位于frameworks / native / include / media / OpenMAX / OMX_Component.h文件中。
创建一个OpenMAX插件，将您的组件与Stagefright服务相链接。有关创建插件的接口，请参阅frameworks / native / include / media / hardware / OMXPluginBase.h和HardwareAPI.h头文件。
将您的插件构建为产品Makefile中名为libstagefrighthw.so的共享库。该库将放在您的终端系统的/ system / lib中。该库将公开一个将由dlsym查找的createOMXPlugin符号。
OMXMaster调用addVendorPlugin，它在内部调用addPlugin（“libstagefrighthw.so”）。在addPlugin中，将查找createOMXPlugin，使用该函数初始化makeComponentInstance，destroyComponentInstance等的其他函数指针。
注意：

在某些情况下，这个“libstagefrighthw.so”库将由您的编解码器供应商作为预构建的二进制文件提供，因为它可能包含专有信息。在这种情况下，您的设备供应商将实施前两个步骤。在这种情况下，您只需要确保将模块声明为产品包。

开发层（DL）
OpenMAX DL是物理硬件之间的接口，例如数字信号处理器（DSP）芯片，CPU，GPU和软件，如视频编解码器和3D引擎。它允许编解码器/芯片供应商轻松集成支持OpenMAX DL的新硬件，而无需优化其低级软件。

Android中的OpenMAX核心实现：
可以从以下细节中参考Android中的OpenMAX实现。

源代码：/ AOSP / frameworks / av / media / libstagefright / omx
包含文件：/ AOSP / frameworks / native / include / media / openmax
共享库名：libstagefright_omx.so
对libstagefright的更改
在某些情况下，您可能需要将硬件编解码器组件支持的MIME类型添加到stagefright引擎。这告诉topfright引擎有关新支持的MIME类型的顶级应用程序框架。
必须在frameworks / av / media / libstagefright中的Acodec.cpp文件中添加支持。例如，如果您的MIME未在“MimeToRole”和“VideoCodingMapEntry”结构中列出，则需要将其包含在那里。例如，您可以参考“MEDIA_MIMETYPE_VIDEO_H263”来查看它是如何在libstagefright中注册的。
```## 硬件加速

```text
硬件加速的主要原理，就是通过底层软件代码，将CPU不擅长的图形计算转换成GPU专用指令，由GPU完成。

如果你的绘制操作不支持硬件加速，你需要手动关闭硬件加速来绘制界面，关闭的方式是通过这行代码：
view.setLayerType(LAYER_TYPE_SOFTWARE, null);

事实上，这个方法的本来作用并不是用来开关硬件加速的，只是当它的参数为 LAYER_TYPE_SOFTWARE 的时候，可以「顺便」把硬件加速关掉而已；并且除了这个方法之外，Android 并没有提供专门的 View 级别的硬件加速开关，所以它就「顺便」成了一个开关硬件加速的方法。

setLayerType() 这个方法，它的作用其实就是名字里的意思：设置 View Layer 的类型。所谓 View Layer，又称为离屏缓冲（Off-screen Buffer），它的作用是单独启用一块地方来绘制这个 View ，而不是使用软件绘制的 Bitmap 或者通过硬件加速的 GPU。这块「地方」可能是一块单独的 Bitmap，也可能是一块 OpenGL 的纹理（texture，OpenGL 的纹理可以简单理解为图像的意思），具体取决于硬件加速是否开启。采用什么来绘制 View 不是关键，关键在于当设置了 View Layer 的时候，它的绘制会被缓存下来，而且缓存的是最终的绘制结果，而不是像硬件加速那样只是把 GPU 的操作保存下来再交给 GPU 去计算。通过这样更进一步的缓存方式，View 的重绘效率进一步提高了：只要绘制的内容没有变，那么不论是 CPU 绘制还是 GPU 绘制，它们都不用重新计算，而只要只用之前缓存的绘制结果就可以了。

硬件加速指的是使用 GPU 来完成绘制的计算工作，代替 CPU。它从工作分摊和绘制机制优化这两个角度提升了绘制的速度。

硬件加速可以使用 setLayerType() 来关闭硬件加速，但这个方法其实是用来设置 View Layer 的：

参数为 LAYER_TYPE_SOFTWARE 时，使用软件来绘制 View Layer，绘制到一个 Bitmap，并顺便关闭硬件加速；
参数为 LAYER_TYPE_HARDWARE 时，使用 GPU 来绘制 View Layer，绘制到一个 OpenGL texture（如果硬件加速关闭，那么行为和 VIEW_TYPE_SOFTWARE 一致）；
参数为 LAYER_TYPE_NONE 时，关闭 View Layer。
View Layer 可以加速无 invalidate() 时的刷新效率，但对于需要调用 invalidate() 的刷新无法加速。

View Layer 绘制所消耗的实际时间是比不使用 View Layer 时要高的，所以要慎重使用。
```## GLThread

```text
glthread是glsurfaceview自带的一个渲染线程，同步的，不阻塞主线程；主要用来执行opengl绘制工作；
下面说一下它的同步原理：
说同步原理之前先说一下glsurfaceview渲染方式，主动和被动两种
1、glthread继承与thread，里面有类型为runnable接口一个集合；
在线程方法中执行一个无限循环while（true）{};里面有一个mRequestRender一个boolean值；
当主动渲染方式，不用说它一直为true，
当被动渲染方式，那么它需要通过glthread.requestRender();方法去修改mRequestRender的值；
当这个值为true时，在无线循环中会取runnable集合的第一个event执行；

那么是如何保证线程同步的呢?

01-03 08:04:34.726  5660 11113 W GLThread: onDrawFrame tid=378
01-03 08:04:34.726  5660 11117 W .app.litecamer: Long monitor contention with owner GLThread 378 (11113) at int com.anc.beautify.jni.BeaurifyJniSdk.nativeCreateBeautyHandle(android.content.Context, int, int, int, int, byte[], byte[], byte[])(BeaurifyJniSdk.java:-2) waiters=0 in int com.anc.beautify.jni.BeaurifyJniSdk.nativeDetectFaceOrientation(byte[], double, double, int, int, int, int) for 785ms
01-03 08:04:34.738  5660 11113 I GLThread: noticing that we want render notification tid=378
01-03 08:04:34.738  5660 11113 W GLThread: egl createSurface
01-03 08:04:34.745  5660  5660 I GLThread: onResume tid=378
01-03 08:04:34.766  5660 11113 W GLThread: onSurfaceChanged(480, 960)
01-03 08:04:35.065  5660 11117 W .app.litecamer: Long monitor contention with owner GLThread 378 (11113) at int com.anc.beautify.jni.BeaurifyJniSdk.nativeReleaseResources()(BeaurifyJniSdk.java:-2) waiters=0 in int com.anc.beautify.jni.BeaurifyJniSdk.nativeDetectFaceOrientation(byte[], double, double, int, int, int, int) for 275ms
01-03 08:04:35.516  5660 11117 W .app.litecamer: Long monitor contention with owner GLThread 378 (11113) at int com.anc.beautify.jni.BeaurifyJniSdk.nativeCreateBeautyHandle(android.content.Context, int, int, int, int, byte[], byte[], byte[])(BeaurifyJniSdk.java:-2) waiters=0 in int com.anc.beautify.jni.BeaurifyJniSdk.nativeDetectFaceOrientation(byte[], double, double, int, int, int, int) for 442ms
01-03 08:04:35.517  5660 11113 W GLThread: onDrawFrame tid=378
01-03 08:04:35.528  5660 11113 I GLThread: sending render notification tid=378
01-03 08:04:35.528  5660 11113 I GLThread: noticing that we want render notification tid=378
01-03 08:04:35.528  5660 11113 W GLThread: egl createSurface
01-03 08:04:35.575  5660 11113 W GLThread: onSurfaceChanged(480, 640)
01-03 08:04:36.293  5660 11113 W GLThread: onDrawFrame tid=378
01-03 08:04:36.302  5660 11113 I GLThread: sending render notification tid=378
01-03 08:04:36.303  5660 11113 W GLThread: onDrawFrame tid=378
01-03 08:04:36.317  5660 11113 I GLThread: waiting tid=378 mHaveEglContext: true mHaveEglSurface: true mFinishedCreatingEglSurface: true mPaused: false mHasSurface: true mSurfaceIsBad: false mWaitingForSurface: false mWidth: 480 mHeight: 640 mRequestRender: false mRenderMode: 0

如何在不调用 GLSurfaceView.setVisibility(View.GONE/View.VISIBLE) 方法的情况下手动调用某个方法触发 GLSurfaceView.onSurfaceChanged()
```## OpenGL

```text
什么是OpenGL？
Open Graphics Library     图形领域的工业标准，是一套跨编程语言、跨平台的、专业的图形编程(软件)接口。它用于二维、三维图像，是一个功能强大，调用方便的底层图形库。     与硬件无关。可以在不同的平台如Windows、Linux、Mac、Android、IOS之间进行移植。因此，支持OpenGL的软件具有很好的移植性，可以获得非常广泛的应用。

OpenGL ES 1.0 和 1.1 ：Android 1.0和更高的版本支持这个API规范。
OpenGL ES 2.0 ：Android 2.2(API 8)和更高的版本支持这个API规范。（2.0 广泛使用）
OpenGL ES 3.0 ：Android 4.3(API 18)和更高的版本支持这个API规范。
OpenGL ES 3.1 : Android 5.0(API 21)和更高的版本支持这个API规范。
OpenGL 的使用需要配置EGL环境，在Android平台下，可直接使用GLSurfaceView，GLSurfaceView内部已经配置好了EGL环境。

GLSurfaceView
继承至SurfaceView，它内嵌的surface专门负责OpenGL渲染。
管理Surface与EGL   
允许自定义渲染器(render)。     
让渲染器在独立的线程里运作，和UI线程分离。      
支持按需渲染(on-demand)和连续渲染(continuous)。

GLSurfaceView主要方法：
setEGLContextClientVersion：设置OpenGL ES的版本，只能设置主要版本（例如：1,2,3），不能设置次要版本。
setEGLContextFactory：设置OpenGL ES的版本构建器，默认的构建器是根据版本设置的，可以自定义成版本自适应。
setRenderer：设置Renderer，如果不设置，那么界面显示的就是一片空白。
setRenderMode：设置Renderer的模式，有这么两种：1、RENDERMODE_WHEN_DIRTY（仅在创建时或调用requestRender时才会渲染内容）；2、RENDERMODE_CONTINUOUSLY（不停的渲染）。
onPause：暂停渲染，在页面不再显示时可以调用，减少性能开销，例如在Activity的onStop时。
onResume：恢复渲染，类似onPause。
requestRender：请求渲染，通常是RENDERMODE_WHEN_DIRTY模式时使用，必须在setRenderer后才能使用。
queueEvent：插入一个Runnable任务到后台渲染线程上执行，必须在setRenderer后才能使用。
setDebugFlags：设置debug模式，主要有两种：1、DEBUG_CHECK_GL_ERROR（当GL调用glError()方法后如果发生异常会打印。主要用来跟踪OpenGL错误。）；2、DEBUG_LOG_GL_CALLS（打印所有GL的verbose级别的日志）；

GLSurfaceView.Renderer的主要方法：
onSurfaceCreated(GL10 gl, EGLConfig config)：当Surface创建或重新创建时，这时可以进行初始化。
onSurfaceChanged(GL10 gl, int width, int height)：Surface尺寸改变时，返回当前surface宽高，可以进行下一步操作。
onDrawFrame(GL10 gl)：渲染绘制当前一帧时会调用。

OpenGL类：在包android.opengl下，主要有GLES20（OpenGL ES 2.0版本），GLES30，GLES31，GLES32和。

OpenGL是一个跨平台的操作GPU的API，但OpenGL需要本地视窗系统进行交互，这就需要一个中间控制层， EGL就是连接OpenGL ES和本地窗口系统的接口，引入EGL就是为了屏蔽不同平台上的区别。
OpenGL中必不可少的两个概念，vertex shader（顶点着色器）和fragment shader（片元着色器）。
顶点着色器：在OpenGL的世界坐标顶点坐标中，三个点确定一个三角形的形状，顶点坐标决定了我们绘制出画面的形状。但这里需要注意OpenGL世界坐标 、纹理坐标 、android屏幕坐标三个概念。下边介绍。
片元着色器：决定了绘制出图像画面的颜色。比如我们预览camera采集的图像，就需要把camera离屏buffer的纹理ID传给片元着色器，片元着色器从纹理ID中取出每一个像素值来进行显示。
OpenGL的绘制首先需要经过顶点着色器，进行光栅化（光栅化就是把顶点坐标连接后，途径的像素点进行关联），然后用片元着色绘制预览画面的像素值。
OpenGL世界坐标 、纹理坐标 、android屏幕坐标
想要把摄像头数据正常的显示到屏幕上或者使用FBO转换后的图像的方向也是正确的，就需要结合上面这三幅图了。

主要的几个方法
glCreateShader：创建shader，参数值：GLES20.GL_VERTEX_SHADER（顶点着色器）或GLES20.GL_FRAGMENT_SHADER（片段着色器），返回创建的shader值。
glShaderSource：加载着色器代码，参数为create的shader值和GLSL代码。
glCompileShader：加载着色器完成。
glGetShaderiv：获取加载完成的状态，主要用来检测是否加载完成，如果加载失败了则使用glDeleteShader来删除错误的shader。
checkGlError是封装好的检测是否有错误的方法，内容如下
public static void checkGlError(String op) {
    int error = GLES20.glGetError();
    if (error != GLES20.GL_NO_ERROR) {
        String msg = op + ": glError 0x" + Integer.toHexString(error);
        LogUtil.e(msg);
        throw new RuntimeException(msg);
    }
}
使用glCreateProgram创建一个空的程序，返回一个非0值。使用glAttachShader来连接当前的程序和创建好的shader值，最后使用glLinkProgram来完成链接program，如果不需要Program后可以使用glDeleteProgram删除program。封装好之后的代码如下
public static int createProgram(String vertexSource, String fragmentSource) {
    int vertexShader = loadShader(GLES20.GL_VERTEX_SHADER, vertexSource);
    if (vertexShader == 0) {
        return 0;
    }
    int pixelShader = loadShader(GLES20.GL_FRAGMENT_SHADER, fragmentSource);
    if (pixelShader == 0) {
        return 0;
    }

    int program = GLES20.glCreateProgram();
    checkGlError("glCreateProgram");
    if (program == 0) {
        LogUtil.e("Could not create program");
    }
    GLES20.glAttachShader(program, vertexShader);
    checkGlError("glAttachShader");
    GLES20.glAttachShader(program, pixelShader);
    checkGlError("glAttachShader");
    GLES20.glLinkProgram(program);
    int[] linkStatus = new int[1];
    GLES20.glGetProgramiv(program, GLES20.GL_LINK_STATUS, linkStatus, 0);
    if (linkStatus[0] != GLES20.GL_TRUE) {
        LogUtil.e("Could not link program: ");
        LogUtil.e(GLES20.glGetProgramInfoLog(program));
        GLES20.glDeleteProgram(program);
        program = 0;
    }
    return program;
}

glUseProgram：使用创建好的program
glGetAttribLocation：查询由程序指定的先前链接的程序对象，返回aPosition变量顶点属性的索引
glEnableVertexAttribArray：启用由索引指定的顶点属性数组。 
createFloatBuffer：封装的生成FloatBuffer代码。
glVertexAttribPointer：指定顶点数组的位置和数据格式，几个参数：index，索引；size，每个顶点的数，当前是3；type，类型，float，short等等，当前是float；normalized，设置为false；stride，顶点间的偏移，每个顶点3个float值，每个float是4个字节；pointer，顶点的集合。
glGetUniformLocation：获取片段着色器中属性的索引。
glUniform4fv：修改统一变量或统一变量数组的值。4fv表示 vec4，同样的方法有很多：glUniform3fv，glUniform3iv等等，可以参考官网的glUniform文档。
glDrawArrays：开始绘制。参数mode类型：有GL_POINTS（点），GL_LINES（线），GL_LINE_STRIP，GL_LINE_LOOP，GL_TRIANGLE_STRIP，GL_TRIANGLE_FAN 和 GL_TRIANGLE；参数first：开始位置；count：总数。
glDisableVertexAttribArray：禁用顶点属性数组，当绘制完成后可以调用。


OpenGL 提供了两个绘制的方法 glDrawArrays(int mode, int first, int count)和 glDrawElements(int mode,int count, int type, Buffer indices)两个方法，在这里我们使用的第二种绘制的方法，关于mode有几种模式供我们选择：
GL_POINTS：绘制独立的点到屏幕
GL_LINE_STRIP：连续的连线，第n个顶点与第n-1个顶点绘制一条直线
GL_LINE_LOOP：与上一个相同，但是需要首尾相联接
GL_LINES：形成对的独立的线段
GL_TRIANGLE_STRIP：绘制一系列的三角形，先是顶点v0，v1，v2，然后是v2，v1，v3（注意规律），然后v2，v3，v4等。该规律确保所有的三角形都以相同的方向绘制
GL_TRIANGLE_FAN 和 GL_TRANGLE_STRIP 类似，但其县绘制v0，v1，v2，再是v0，v2，v3，然后v0，v3，v4等。


首先 那FBO是什么呢？Frame Buffer Object
https://blog.csdn.net/Frakie_Kwok/article/details/91491915
https://blog.csdn.net/a360940265a/article/details/80627394
帧缓冲对象:FBO。默认情况下，我们在GLSurfaceView中绘制的结果是显示到屏幕上，然而实际中有很多情况并不需要渲染到屏幕上，这个时候使用FBO就可以很方便的实现这类需求。FBO可以让我们的渲染不渲染到屏幕上，而是渲染到离屏Buffer中。
也就是我们帧缓存，从一个纹理缓存到另一个FBO的纹理中（比如加美颜滤镜贴纸都需要用FBO）。因为是纹理缓存到纹理上，所以我们就需要把纹理坐标和OpenGL世界坐标对应上。

白话文解释：FBO是一个挂接器，类似画家画画用的托架；其中FBO只能挂接两种对象，纹理图像 和 渲染图像，这个理解就是画家准备创作作品前，在托架上放的是油画纸还是水墨纸（纹理），或者根本不是放画纸，放的是木板雕刻（渲染模板）。最后我们等画家创作出他的艺术品后，直接搬到到展示区，呈现給大家。

《OpenGL Frame Buffer Object (FBO)》 http://www.songho.ca/opengl/gl_fbo.html
《OpenGL.ES在Android上的简单实践：23-水印录制（FBO离屏渲染，解决透明冲突，画中画）》 https://blog.csdn.net/a360940265a/article/details/80627394

GLSL（OpenGL ES Shading Language），OpenGL ES着色语言；

GLSL是一种类C语言，用来编写顶点着色程序和片段着色程序。GLSL语言还是比较复杂的，OpenGL ES2.0的GLSL官方文档地址是https://www.khronos.org/registry/OpenGL/specs/es/2.0/GLSL_ES_Specification_1.00.pdf，如果英文水平比较高可阅读参考，否则可用参考http://colin1994.github.io/2017/11/11/OpenGLES-Lesson04/，http://colin1994.github.io/2017/11/12/OpenGLES-Lesson05这两篇文章，写的还是不错的。

顶点着色器
/home/zq/Cameras/Release/Android/demo/BeautifyDemo_android/output/demo/app/src/main/res/raw/vshader

attribute vec4 aPosition;       // 把顶点坐标给这个变量， 确定要画画的形状
attribute vec2 aTexCoord;       // 接收纹理坐标，接收采样器采样图片的坐标
varying vec2 vTexCoord;
uniform mat4 uMatrix;           // 变换矩阵， 需要将原本的vCoord（01,11,00,10） 与矩阵相乘 才能够得到 surfacetexure(特殊)的正确的采样坐标
uniform mat4 uSTMatrix;         // 变换矩阵，
void main() {
    vTexCoord = aTexCoord;
    gl_Position = uMatrix*aPosition;    //内置变量 gl_Position ,我们把顶点数据赋值给这个变量 opengl就知道它要画什么形状了
}

片元着色器
/home/zq/Cameras/Release/Android/demo/BeautifyDemo_android/output/demo/app/src/main/res/raw/fragment_shader
#extension GL_OES_EGL_image_external : require
precision mediump float;
varying vec2 textureCoordinate;                 //采样点的坐标
uniform samplerExternalOES inputImageTexture;   //采样器
void main() {
    gl_FragColor=texture2D(inputImageTexture, textureCoordinate);   //texture2D：采样器 采集 aCoord的像素赋值给 gl_FragColor(顶点颜色) 就可以了
}

GLES中的数据类型：
vec4        含四个浮点型数据的向量(xyzw,rgba,stpq)
vec2        含两个浮点型数据的向量(坐标)
attribute   属性变量。只能用于顶点着色器中。 一般用该变量来表示一些顶点数据，如：顶点坐标、纹理坐标、颜色等。
uniforms    一致变量。在着色器执行期间一致变量的值是不变的。与const常量不同的是，这个值在编译时期是未知的是由着色器外部初始化的。
varying     易变变量。是从顶点着色器传递到片元着色器的数据变量。

内建函数
texture2D (采样器,坐标)  采样指定位置的纹理

内建变量
gl_Position  vec4   //顶点位置
gl_FragColor vec4   //顶点颜色

其他
precision lowp      //低精度
precision mediump   //中精度
precision highp     //高精度


public GlRenderView(Context context, AttributeSet attrs) {
    super(context, attrs);
    setEGLContextClientVersion(2);          //设置 EGL 版本
    glRender = new GlRenderWrapper(this);
    setRenderer(glRender);
    setRenderMode(RENDERMODE_WHEN_DIRTY);   //手动渲染模式
}

GLSurfaceView.Renderer
public interface Renderer {
    @Override
    public void onSurfaceCreated(GL10 gl, EGLConfig config) {   //surface 创建监听
        camera2Helper = new Camera2Helper((Activity) glRenderView.getContext());
        mTextures = new int[1];
        GLES20.glGenTextures(mTextures.length, mTextures, 0);       //创建一个纹理
        mSurfaceTexture = new SurfaceTexture(mTextures[0]);         //将纹理和离屏buffer绑定
        mSurfaceTexture.setOnFrameAvailableListener(this);          //监听有新图像到来
        cameraFilter = new CameraFilter(glRenderView.getContext()); //使用fbo 将samplerExternalOES 输入到sampler2D中
        screenFilter = new ScreenFilter(glRenderView.getContext()); //负责将图像绘制到屏幕上
    }
    void onSurfaceChanged(GL10 gl, int width, int height);  //surface改变监听
    void onDrawFrame(GL10 gl);                              //负责纹理绘制
}

onSurfaceCreated中，实例Camera2Helper对象，创建一个SurfaceTexture和纹理，并进行绑定。这个SurfaceTexture会传给Camera2中，camera2负责输入图像到SurfaceTexture中，这里的SurfaceTexture是一个离屏buffer。并且实例CameraFilter和ScreenFilter。
当有新图像来了，会执行onFrameAvailable，更新图像。
@Override
public void onFrameAvailable(SurfaceTexture surfaceTexture) {
    glRenderView.requestRender();
}


private void initilize(Context mContext) {
    mVertexShader = OpenGlUtils.readRawShaderFile(mContext, mVertexShaderId);       //读取顶点着色器信息
    mFragShader = OpenGlUtils.readRawShaderFile(mContext, mFragShaderId);           //读取片源着色器信息
    mProgramId = OpenGlUtils.loadProgram(mVertexShader, mFragShader);               //创建着色器程序
    
    vPosition = GLES20.glGetAttribLocation(mProgramId, "vPosition");                //获取着色器变量，需要赋值
    vCoord = GLES20.glGetAttribLocation(mProgramId, "vCoord");
    vMatrix = GLES20.glGetUniformLocation(mProgramId, "vMatrix");
    vTexture = GLES20.glGetUniformLocation(mProgramId, "vTexture");
}

主要参考资料：
Android官方文档（https://developer.android.com/guide/topics/graphics/opengl）
OpenGL ES文档（https://www.khronos.org/opengles/）
learnopengl（https://learnopengl-cn.github.io/）
《OpenGL ES 2 for Android: A Quick-Start Guide》(英文原版电子书)


在 Camera 中使用OpenGL
使用Camera API 2开启相机
public void startCameraThread() {
    mCameraThread = new HandlerThread("CameraThread");
    mCameraThread.start();
    mCameraHandler = new Handler(mCameraThread.getLooper());
}

设置相机参数
public String setupCamera(int width, int height) {
    //获取摄像头管理者，它主要用来查询和打开可用的摄像头
    CameraManager cameraManager = (CameraManager) mActivity.getSystemService(Context.CAMERA_SERVICE);
    try {
        //遍历所有摄像头
        for (String id : cameraManager.getCameraIdList()) {
            //获取此ID对应摄像头的参数
            CameraCharacteristics characteristics = cameraManager.getCameraCharacteristics(id);
            //默认打开后置摄像头
            if (characteristics.get(CameraCharacteristics.LENS_FACING) == CameraCharacteristics.LENS_FACING_FRONT) {
                continue;
            }
            //获取StreamConfigurationMap，它是管理摄像头支持的所有输出格式和尺寸
            StreamConfigurationMap map = characteristics.get(CameraCharacteristics.SCALER_STREAM_CONFIGURATION_MAP);
            //根据屏幕尺寸（通过参数传进来）匹配最合适的预览尺寸
            mPreviewSize = getOptimalSize(map.getOutputSizes(SurfaceTexture.class), width, height);
            mCameraId = id;
        }
    } catch (CameraAccessException e) {
        e.printStackTrace();
    }
    return mCameraId;
}

开启相机
public boolean openCamera() {
    CameraManager cameraManager = (CameraManager) mActivity.getSystemService(Context.CAMERA_SERVICE);
    try {
        //开启相机，第一个参数指示打开哪个摄像头，第二个参数mStateCallback为相机的状态回调接口，第三个参数用来确定Callback在哪个线程执行，为null的话就在当前线程执行
        cameraManager.openCamera(mCameraId, mStateCallback, mCameraHandler);
    } catch (CameraAccessException e) {
        e.printStackTrace();
        return false;
    }
    return true;
}

//当相机成功打开后会回调onOpened方法，这里可以拿到CameraDevice对象，也就是具体的摄像头设备
public CameraDevice.StateCallback mStateCallback = new CameraDevice.StateCallback() {
    @Override
    public void onOpened(@NonNull CameraDevice camera) {
        mCameraDevice = camera;
    }
}

添加GLSurfaceView作为布局界面、创建SurfaceTexture
//实例化一个GLSurfaceView
mGLSurfaceView = new GLSurfaceView(this);
//配置OpenGL ES，主要是版本设置和设置Renderer，Renderer用于执行OpenGL的绘制
mGLSurfaceView.setEGLContextClientVersion(2);
mGLSurfaceView.setRenderer(new GLSurfaceView.Renderer());
//在屏幕上显示GLSurfaceView

根据OES纹理Id创建SurfaceTexture，用来接收Camera2的预览数据。
public boolean initSurfaceTexture() {
    //根据OES纹理ID实例化SurfaceTexture
    mSurfaceTexture = new SurfaceTexture(mOESTextureId);
    //当SurfaceTexture接收到一帧数据时，请求OpenGL ES进行渲染
    mSurfaceTexture.setOnFrameAvailableListener(new SurfaceTexture.OnFrameAvailableListener() {
        @Override
        public void onFrameAvailable(SurfaceTexture surfaceTexture) {
            mCameraV2GLSurfaceView.requestRender();
        }
    });
    return true;
}

使用Camera2 API开启预览
public void startPreview() {
    //设置SurfaceTexture的默认尺寸
    mSurfaceTexture.setDefaultBufferSize(mPreviewSize.getWidth(), mPreviewSize.getHeight());
    //根据mSurfaceTexture创建Surface
    Surface surface = new Surface(mSurfaceTexture);
    try {
        //创建preview捕获请求
        mCaptureRequestBuilder = mCameraDevice.createCaptureRequest(CameraDevice.TEMPLATE_PREVIEW);
        //将此请求输出目标设为我们创建的Surface对象，这个Surface对象也必须添加给createCaptureSession才行
        mCaptureRequestBuilder.addTarget(surface);
        //创建捕获会话，第一个参数是捕获数据的输出Surface列表，第二个参数是CameraCaptureSession的状态回调接口，当它创建好后会回调onConfigured方法，第三个参数用来确定Callback在哪个线程执行，为null的话就在当前线程执行
        mCameraDevice.createCaptureSession(Arrays.asList(surface), new CameraCaptureSession.StateCallback() {
            @Override
            public void onConfigured(@NonNull CameraCaptureSession session) {
                try {
                    //创建捕获请求
                    mCaptureRequest = mCaptureRequestBuilder.build();
                    mCameraCaptureSession = session;
                    //设置重复捕获数据的请求，之后surface绑定的SurfaceTexture中就会一直有数据到达，然后就会回调SurfaceTexture.OnFrameAvailableListener接口
                    mCameraCaptureSession.setRepeatingRequest(mCaptureRequest, null, mCameraHandler);
                } catch (CameraAccessException e) {
                    e.printStackTrace();
                }
            }

            @Override
            public void onConfigureFailed(@NonNull CameraCaptureSession session) {

            }
        }, mCameraHandler);
    } catch (CameraAccessException e) {
        e.printStackTrace();
    }
}

绘制预览数据到屏幕上
if (mSurfaceTexture != null) {
    //更新数据，其实也是消耗数据，将上一帧的数据处理或者抛弃掉，要不然SurfaceTexture是接收不到最新数据
    mSurfaceTexture.updateTexImage();
    mSurfaceTexture.getTransformMatrix(transformMatrix);
}

首先使用Camera2 API开启相机，然后添加GLSurfaceView作为布局界面，之后创建一个外部纹理，根据此纹理ID创建一个SurfaceTexture。开启预览，Camera2将预览数据输出至此SurfaceTexture上。有数据到达时，会回调SurfaceTexture的OnFrameAvailableListener接口，在此接口中requestRender，通过OpenGL ES将此OES纹理绘制到屏幕上。
```## FBO

```text
FBO： Frame Buffer object     帧缓冲对象

为什么要用FBO?
当需要对纹理进行多次渲染采样时，而这些渲染采样是不需要展示给用户看的，可以用一个单独的缓冲对象（离屏渲染）来存储这几次渲染采样的结果，等处理完后才显示到窗口上。

优势
提高渲染效率，避免闪屏，可以很方便的实现纹理共享等。

渲染方式
渲染到缓冲区（Render）- 深度测试和模板测试
渲染到纹理（Texture）- 图像渲染
```## VBO

```text
VBO： Vertex Buffer object   顶点缓冲对象

为什么要用VBO?

不使用VBO时，每次绘制（ glDrawArrays ）图形时都是从本地内存处获取顶点数据然后传输给OpenGL来绘制，这样就会频繁的操作CPU->GPU增大开销，从而降低效率。使用VBO，可以把顶点数据缓存到GPU开辟的一段内存中，然后使用时不必再从本地获取，而是直接从显存中获取，这样就能提升绘制的效率。
```## GPU屏幕渲染方式

```text
1.On-Screen Rendering
意为当前屏幕渲染，指的是GPU的渲染操作是在当前用于显示的屏幕缓冲区中进行。（例如我们显示/录制的Surface）

2.Off-Screen Rendering
意为离屏渲染，指的是GPU在当前屏幕缓冲区以外新开辟一个缓冲区进行渲染操作。（区别于Surface的另外一种渲染区）
```## ByteBuffer/FloatBuffer/IntBuffer

```text
ByteBuffer 和 FloatBuffer 以及 IntBuffer 都是继承自抽象类 java.nio.Buffer。
另外，OpenGL在底层的实现是C语言，与Java默认的数据存储字节顺序可能不同，即大端小端问题。因此，为了保险起见，在将数据传递给OpenGL之前，我们需要指明使用本机的存储顺序。
```## GPUImage

```text
GPUImage 是iOS下一个开源的基于GPU的图像处理库，提供各种各样的图像处理滤镜，并且支持照相机和摄像机的实时滤镜。GPUImage for Android是它在Android下的实现，同样也是开源的。其中提供了几十多种常见的图片滤镜API，且其机制是基于GPU渲染，处理速度相应也比较快，是一个不错的图片实时处理框架。

GitHub地址：https://github.com/CyberAgent/android-gpuimage

// 使用GPUImage处理图像
gpuImage = new GPUImage(this);
gpuImage.setImage(bitmap);
gpuImage.setFilter(new GPUImageGrayscaleFilter());
bitmap = gpuImage.getBitmapWithFilterApplied();
//显示处理后的图片
resultIv.setImageBitmap(bitmap);


"GPUImageFastBlurFilter"                               【模糊】
"GPUImageGaussianBlurFilter"                       【高斯模糊】
"GPUImageGaussianSelectiveBlurFilter"        【高斯模糊，选择部分清晰】
"GPUImageBoxBlurFilter"                                【盒状模糊】
"GPUImageTiltShiftFilter"                                【条纹模糊，中间清晰，上下两端模糊】
"GPUImageMedianFilter.h"                             【中间值，有种稍微模糊边缘的效果】
"GPUImageBilateralFilter"                               【双边模糊】
"GPUImageErosionFilter"                                【侵蚀边缘模糊，变黑白】
"GPUImageRGBErosionFilter"                         【RGB侵蚀边缘模糊，有色彩】
"GPUImageDilationFilter"                               【扩展边缘模糊，变黑白】
"GPUImageRGBDilationFilter"                        【RGB扩展边缘模糊，有色彩】
"GPUImageOpeningFilter"                             【黑白色调模糊】
"GPUImageRGBOpeningFilter"                      【彩色模糊】
"GPUImageClosingFilter"                               【黑白色调模糊，暗色会被提亮】
"GPUImageRGBClosingFilter"                        【彩色模糊，暗色会被提亮】
"GPUImageLanczosResamplingFilter"          【Lanczos重取样，模糊效果】
"GPUImageNonMaximumSuppressionFilter"     【非最大抑制，只显示亮度最高的像素，其他为黑】
"GPUImageThresholdedNonMaximumSuppressionFilter" 【与上相比，像素丢失更多】

"GPUImageCrosshairGenerator"              【十字】
"GPUImageLineGenerator"                       【线条】
"GPUImageTransformFilter"                     【形状变化】
"GPUImageCropFilter"                              【剪裁】
"GPUImageSharpenFilter"                        【锐化】
"GPUImageUnsharpMaskFilter"               【反遮罩锐化】

"GPUImageSobelEdgeDetectionFilter"           【Sobel边缘检测算法(白边，黑内容，有点漫画的反色效果)】
"GPUImageCannyEdgeDetectionFilter"          【Canny边缘检测算法（比上更强烈的黑白对比度）】
"GPUImageThresholdEdgeDetectionFilter"    【阈值边缘检测（效果与上差别不大）】
"GPUImagePrewittEdgeDetectionFilter"         【普瑞维特(Prewitt)边缘检测(效果与Sobel差不多，貌似更平滑)】
"GPUImageXYDerivativeFilter"                        【XYDerivative边缘检测，画面以蓝色为主，绿色为边缘，带彩色】
"GPUImageHarrisCornerDetectionFilter"       【Harris角点检测，会有绿色小十字显示在图片角点处】
"GPUImageNobleCornerDetectionFilter"      【Noble角点检测，检测点更多】
"GPUImageShiTomasiFeatureDetectionFilter" 【ShiTomasi角点检测，与上差别不大】
"GPUImageMotionDetector"                             【动作检测】
"GPUImageHoughTransformLineDetector"      【线条检测】
"GPUImageParallelCoordinateLineTransformFilter" 【平行线检测】

"GPUImageLocalBinaryPatternFilter"        【图像黑白化，并有大量噪点】
"GPUImageLowPassFilter"                          【用于图像加亮】
"GPUImageHighPassFilter"                        【图像低于某值时显示为黑】

"GPUImageSketchFilter"                          【素描】
"GPUImageThresholdSketchFilter"         【阀值素描，形成有噪点的素描】
"GPUImageToonFilter"                             【卡通效果（黑色粗线描边）】
"GPUImageSmoothToonFilter"                【相比上面的效果更细腻，上面是粗旷的画风】
"GPUImageKuwaharaFilter"                     【桑原(Kuwahara)滤波,水粉画的模糊效果；处理时间比较长，慎用】

"GPUImageMosaicFilter"                         【黑白马赛克】
"GPUImagePixellateFilter"                       【像素化】
"GPUImagePolarPixellateFilter"              【同心圆像素化】
"GPUImageCrosshatchFilter"                  【交叉线阴影，形成黑白网状画面】
"GPUImageColorPackingFilter"              【色彩丢失，模糊（类似监控摄像效果）】

"GPUImageVignetteFilter"                        【晕影，形成黑色圆形边缘，突出中间图像的效果】
"GPUImageSwirlFilter"                               【漩涡，中间形成卷曲的画面】
"GPUImageBulgeDistortionFilter"            【凸起失真，鱼眼效果】
"GPUImagePinchDistortionFilter"            【收缩失真，凹面镜】
"GPUImageStretchDistortionFilter"         【伸展失真，哈哈镜】
"GPUImageGlassSphereFilter"                  【水晶球效果】
"GPUImageSphereRefractionFilter"         【球形折射，图形倒立】
    
"GPUImagePosterizeFilter"                 【色调分离，形成噪点效果】
"GPUImageCGAColorspaceFilter"      【CGA色彩滤镜，形成黑、浅蓝、紫色块的画面】
"GPUImagePerlinNoiseFilter"              【柏林噪点，花边噪点】
"GPUImage3x3ConvolutionFilter"      【3x3卷积，高亮大色块变黑，加亮边缘、线条等】
"GPUImageEmbossFilter"                   【浮雕效果，带有点3d的感觉】
"GPUImagePolkaDotFilter"                 【像素圆点花样】
"GPUImageHalftoneFilter"                  【点染,图像黑白化，由黑点构成原图的大致图形】

混合模式 Blend
"GPUImageMultiplyBlendFilter"            【通常用于创建阴影和深度效果】
"GPUImageNormalBlendFilter"               【正常】
"GPUImageAlphaBlendFilter"                 【透明混合,通常用于在背景上应用前景的透明度】
"GPUImageDissolveBlendFilter"             【溶解】
"GPUImageOverlayBlendFilter"              【叠加,通常用于创建阴影效果】
"GPUImageDarkenBlendFilter"               【加深混合,通常用于重叠类型】
"GPUImageLightenBlendFilter"              【减淡混合,通常用于重叠类型】
"GPUImageSourceOverBlendFilter"       【源混合】
"GPUImageColorBurnBlendFilter"          【色彩加深混合】
"GPUImageColorDodgeBlendFilter"      【色彩减淡混合】
"GPUImageScreenBlendFilter"                【屏幕包裹,通常用于创建亮点和镜头眩光】
"GPUImageExclusionBlendFilter"            【排除混合】
"GPUImageDifferenceBlendFilter"          【差异混合,通常用于创建更多变动的颜色】
"GPUImageSubtractBlendFilter"            【差值混合,通常用于创建两个图像之间的动画变暗模糊效果】
"GPUImageHardLightBlendFilter"         【强光混合,通常用于创建阴影效果】
"GPUImageSoftLightBlendFilter"           【柔光混合】
"GPUImageChromaKeyBlendFilter"       【色度键混合】
"GPUImageMaskFilter"                           【遮罩混合】
"GPUImageHazeFilter"                            【朦胧加暗】
"GPUImageLuminanceThresholdFilter" 【亮度阈】
"GPUImageAdaptiveThresholdFilter"     【自适应阈值】
"GPUImageAddBlendFilter"                    【通常用于创建两个图像之间的动画变亮模糊效果】
"GPUImageDivideBlendFilter"                 【通常用于创建两个图像之间的动画变暗模糊效果】
```## OES(外部 GLES 纹理)

```text
在客户端中存在一种应用场景：需要将 MediaCodec 或者 Camera 产生的图像，通过 OpenGL 交给算法做特效，由于算法可能是基于普通的 Texture2D 纹理实现的，而 Android 上更常用的则是 GL_TEXTURE_EXTERNAL_OES 纹理，算法一般都是基于 OpenGL 而不是 OpenGLES 环境实现的，所以就需要客户端这边做一个转换工作。这个转换工作当然最好是在 GPU 中能完成的，因为如果通过 CPU 从 OES 纹理中读出图像数据，再提交到 2D 纹理中，这一来一回，即浪费 CPU 页占有了内存，很不划算。所以就出现了这篇文章，如何利用 OpenGL 将 OES 纹理渲染到普通 2D 纹理上。

https://blog.csdn.net/u012165769/article/details/120512380
GL_TEXTURE_EXTERNAL_OES 纹理

外部 GLES 纹理
外部 GLES 纹理 (GL_TEXTURE_EXTERNAL_OES) 与传统 GLES 纹理 (GL_TEXTURE_2D) 的区别如下：

外部纹理直接在从 BufferQueue 接收的数据中渲染纹理多边形。
外部纹理渲染程序的配置与传统的 GLES 纹理渲染程序不同。
外部纹理不一定可以执行所有传统的 GLES 纹理活动。
外部纹理的主要优势是它们能够直接从 BufferQueue 数据进行渲染。SurfaceTexture 实例在为外部纹理创建 BufferQueue 实例时将使用方用法标志设置为 GRALLOC_USAGE_HW_TEXTURE，以确保 GLES 可以识别该缓冲区中的数据。

由于 SurfaceTexture 实例会与 EGL 上下文交互，所以当拥有纹理的 EGL 上下文当前在发起调用的线程上时，应用只能调用其自己的方法。如需了解详情，请参阅 SurfaceTexture 类文档。


1. The texture target needs to be GLES20.GL_TEXTURE_EXTERNAL_OES instead of GL_TEXTURE_2D, e.g. in the glBindTexture calls and glTexParameteri calls.

2. In the fragment shader define a requirement to use the extension:
#extension GL_OES_EGL_image_external : require

3. For the texture sampler used in the fragment shader, use samplerExternalOES instead of sampler2D.

Everything below here is all in the C code, no more Java.

4. In the C code, use glEGLImageTargetTexture2DOES(GL_TEXTURE_EXTERNAL_OES, eglImage) to specify where the data is, instead of using glTexImage2D family of functions.

5. Now, this is android specific, as GraphicBuffer.h is defined in the android native source code. new a GraphicBuffer object, and init with with the width, height, pixel format, etc... this is where we'll be writing the pixels to. Also, the android's GraphicBuffer object is the one that will allocate the memory for us i.e. call gralloc.

6. To write pixels to the GraphicBuffer, lock it via graphicBuffer->lock(GRALLOC_USAGE_SW_WRITE_RARELY, (void **) &pixels), lock() will give you the address to write the pixels to in the 2nd parameter. Once you have the address, now, you can freely write the data to the address pixels.

7. After you finish writing, unlock it, graphicBuffer->unlock().

8. Now, you need the eglImage object to pass into glEGLImageTargetTexture2DOES in step 4. To create the eglImage using createEGLImageKHR(). http://www.khronos.org/registry/egl/extensions/KHR/EGL_KHR_image_base.txt. 4th parameter to eglCreateImageKHR() takes in a EGLClientBuffer, use this (EGLClientBuffer) graphicBuffer->getNativeBuffer();

9. To clean up, use eglDestroyImageKHR().

I think that's about it. Everything is public API: glEGLImageTargetTexture2DOES(), eglCreateEGLImageKHR(), eglDestroyImageKHR(). gralloc is used, and the implementation of GraphicsBuffer object in the android native source code does that for us.
```## Android 中 View，SurfaceView, GLSurfaceView 和 TextureView 等的区别

```text
View：显示视图，内置画布，提供图形绘制函数、触屏事件、按键事件函数等；必须在UI主线程内更新画面，速度较慢。
SurfaceView：基于view视图进行拓展的视图类，更适合2D游戏的开发；**是view的子类，类似使用双缓机制，在新的线程中更新画面,所以刷新界面速度比view快。**其缺点是不能做变形和动画，也不能随屏幕的变化而变化，另外不能在其上面覆盖其它的SurfaceView。
GLSurfaceView：是surfaceview的子类，在其基础上封装了egl环境管理,以及render线程。专用于3D游戏开发的视图，OpenGL ES专用。
TextureView：它也是继承自View，只能运行中硬件加速窗口。它的功能类似于SurfaceView + SurfaceTexture，它内部包含一个SurfaceTexture，它可以让Camera的数据和显示分离，比如需要做二次处理时，如Camera吧采集的数据发送给SurfaceTexture（比如做个美颜），SurfaceTexture处理后传给TextureView显示。TextureView可以做view的变形和动画。一般它是在主线程上做处理（在Android 5.0引入渲染线程后，它是在渲染线程中做的）。
```## TextureView

```text
在4.0(API level 14)中引入，与SurfaceView一样继承View，它可以将内容流直接投影到View中，它可以将内容流直接投影到View中，可以用于实现Live preview等功能。和SurfaceView不同，它不会在WMS中单独创建窗口，而是作为View hierachy中的一个普通View，因此可以和其它普通View一样进行移动，旋转，缩放，动画等变化。值得注意的是TextureView必须在硬件加速的窗口中。它显示的内容流数据可以来自App进程或是远端进程。从类图中可以看到，TextureView继承自View，它与其它的View一样在View hierachy中管理与绘制。TextureView重载了draw()方法，其中主要SurfaceTexture中收到的图像数据作为纹理更新到对应的HardwareLayer中。SurfaceTexture.OnFrameAvailableListener用于通知TextureView内容流有新图像到来。SurfaceTextureListener接口用于让TextureView的使用者知道SurfaceTexture已准备好，这样就可以把SurfaceTexture交给相应的内容源。Surface为BufferQueue的Producer接口实现类，使生产者可以通过它的软件或硬件渲染接口为SurfaceTexture内部的BufferQueue提供graphic buffer。

优点：支持移动、旋转、缩放等动画，支持截图
缺点：必须在硬件加速的窗口中使用，占用内存比SurfaceView高，在5.0以前在主线程渲染，5.0以后有单独的渲染线程。

从性能和安全性角度出发，使用播放器优先选SurfaceView。

1、在android 7.0上系统surfaceview的性能比TextureView更有优势，支持对象的内容位置和包含的应用内容同步更新，平移、缩放不会产生黑边。 在7.0以下系统如果使用场景有动画效果，可以选择性使用TextureView
2、由于失效(invalidation)和缓冲的特性，TextureView增加了额外1~3帧的延迟显示画面更新
3、TextureView总是使用GL合成，而SurfaceView可以使用硬件overlay后端，可以占用更少的内存带宽，消耗更少的能量
4、TextureView的内部缓冲队列导致比SurfaceView使用更多的内存
5、SurfaceView： 内部自己持有surface，surface 创建、销毁、大小改变时系统来处理的，通过surfaceHolder 的callback回调通知。当画布创建好时，可以将surface绑定到MediaPlayer中。SurfaceView如果为用户可见的时候，创建SurfaceView的SurfaceHolder用于显示视频流解析的帧图片，如果发现SurfaceView变为用户不可见的时候，则立即销毁SurfaceView的SurfaceHolder，以达到节约系统资源的目的
```## SurfaceView

```text
它继承自类View，因此它本质上是一个View。但与普通View不同的是，它有自己的Surface。有自己的Surface，在WMS中有对应的WindowState，在SurfaceFlinger中有Layer。我们知道，一般的Activity包含的多个View会组成View hierachy的树形结构，只有最顶层的DecorView，也就是根结点视图，才是对WMS可见的。这个DecorView在WMS中有一个对应的WindowState。相应地，在SF中对应的Layer。而SurfaceView自带一个Surface，这个Surface在WMS中有自己对应的WindowState，在SF中也会有自己的Layer。虽然在App端它仍在View hierachy中，但在Server端（WMS和SF）中，它与宿主窗口是分离的。这样的好处是对这个Surface的渲染可以放到单独线程去做，渲染时可以有自己的GL context。这对于一些游戏、视频等性能相关的应用非常有益，因为它不会影响主线程对事件的响应。但它也有缺点，因为这个Surface不在View hierachy中，它的显示也不受View的属性控制，所以不能进行平移，缩放等变换，也不能放在其它ViewGroup中，一些View中的特性也无法使用。

优点：可以在一个独立的线程中进行绘制，不会影响主线程，使用双缓冲机制，播放视频时画面更流畅
缺点：Surface不在View hierachy中，它的显示也不受View的属性控制，所以不能进行平移，缩放等变换，也不能放在其它ViewGroup中。SurfaceView 不能嵌套使用

双缓冲：在运用时可以理解为：SurfaceView在更新视图时用到了两张Canvas，一张frontCanvas和一张backCanvas，每次实际显示的是frontCanvas，backCanvas存储的是上一次更改前的视图，当使用lockCanvas（）获取画布时，得到的实际上是backCanvas而不是正在显示的frontCanvas，之后你在获取到的backCanvas上绘制新视图，再unlockCanvasAndPost（canvas）此视图，那么上传的这张canvas将替换原来的frontCanvas作为新的frontCanvas，原来的frontCanvas将切换到后台作为backCanvas。例如，如果你已经先后两次绘制了视图A和B，那么你再调用lockCanvas（）获取视图，获得的将是A而不是正在显示的B，之后你讲重绘的C视图上传，那么C将取代B作为新的frontCanvas显示在SurfaceView上，原来的B则转换为backCanvas。
```## GLSurfaceView

```text
1.创建一个 GLSurfaceView
    GLSurfaceView mFaceBeautySurfaceView = new GLSurfaceView(mContext);
2.初始化 GLSurfaceView
    mFaceBeautySurfaceView.setEGLContextClientVersion(2);
    mFaceBeautySurfaceView.setOnTouchListener(mOnTouchListener);
    mFaceBeautySurfaceView.setRenderMode(GLSurfaceView.RENDERMODE_WHEN_DIRTY);  //1、RENDERMODE_WHEN_DIRTY（仅在创建时或调用requestRender时才会渲染内容）；2、RENDERMODE_CONTINUOUSLY（不停的渲染）。
3.给 GLSurfaceView 设置一个 Render 监听器
    mFaceBeautySurfaceView.setRenderer(new GLSurfaceView.Renderer() {
        @Override
        public void onSurfaceCreated(GL10 gl, EGLConfig config) {       // 在创建显示的时候回调
            glGenTextures(textureId.length, textureId, 0);
            mFaceBeautyTextureId = OpenGLUtils.genOESTexture();                     //生成 textureId
            mFaceBeautySurfaceTexture = new SurfaceTexture(mFaceBeautyTextureId);   //用 textureId 生成 SurfaceTexture，把这个 SurfaceTexture 
        }
        @Override
        public void onSurfaceChanged(GL10 gl, int width, int height) {  // 在GLSurfaceView大小或横竖屏改变的时候回调
            GLES20.glViewport(0, 0, 480, 480);
            GLES20.glEnable(GLES20.GL_DEPTH_TEST);
        }
        @Override
        public void onDrawFrame(GL10 gl) {                              // 在该方法中调用 GLESxx.XXX() 方法渲染纹理
            GLES20.glClearColor(255, 255, 0, 255);  //清空画布
            GLES20.glClear(GLES20.GL_COLOR_BUFFER_BIT | GLES20.GL_DEPTH_BUFFER_BIT);//清空buffer
            if (mFaceBeautyEventCallBack != null){
                mFaceBeautyEventCallBack.drawFrame();
            }
        }
    });
在 Render 中初始化 GLES 的环境
    a. iProgId = GLES20.glCreateProgram();
    b. GLES20.glAttachShader(iProgId, iVShader);
    c. GLES20.glAttachShader(iProgId, iFShader);
    d. GLES20.glLinkProgram(iProgId);
    e. GLES20.glGetProgramiv(iProgId, GLES20.GL_LINK_STATUS, link, 0);
4. 在 GLSurfaceView.Render 中创建一个纹理，再使用该纹理创建一个 SurfaceTexture
5. 使用该 SurfaceTexture 创建一个 Surface 传给相机，相机预览数据就输出到一个纹理上了
6. 使用 GLSurfaceView.Render 将该纹理渲染到 GLSurfaceView 窗口上
7. 使用 SurfaceTexture 的 setOnFrameAvailableListener 方法 给 SurfaceTexture 添加一个数据帧数据可用的监听器，在监听器中 调用 GLSurfaceView 的 requestRender 方法渲染该帧数据，这样相机每次输出一帧数据就可以渲染一次，在GLSurfaceView窗口中就可以看到相机的预览数据了

GLSurfaceView的事件处理
为了处理事件，一般都是继承GLSurfaceView类并重载它的事件方法，但是由于GLSurfaceView是多线程的，渲染器在独立的渲染线程里，你应该使用Java的跨线程机制跟渲染器通讯，GLSurfaceView提供的queueEvent(Runnable)方法就是一种相对简单的操作，queueEvent()方法被安全地用于在UI线程和渲染线程之间进行交流通信：


//将程序加入到OpenGLES2.0环境
GLES20.glUseProgram(mProgram);
//获取变换矩阵vMatrix成员句柄
mMatrixHandler= GLES20.glGetUniformLocation(mProgram,"vMatrix");
//指定vMatrix的值
GLES20.glUniformMatrix4fv(mMatrixHandler,1,false,mMVPMatrix,0);
//获取顶点着色器的vPosition成员句柄
mPositionHandle = GLES20.glGetAttribLocation(mProgram, "vPosition");
//启用三角形顶点的句柄
GLES20.glEnableVertexAttribArray(mPositionHandle);
//准备三角形的坐标数据
GLES20.glVertexAttribPointer(mPositionHandle, COORDS_PER_VERTEX, GLES20.GL_FLOAT, false, vertexStride, vertexBuffer);
//获取片元着色器的vColor成员的句柄
mColorHandle = GLES20.glGetUniformLocation(mProgram, "vColor");
//设置绘制三角形的颜色
GLES20.glUniform4fv(mColorHandle, 1, color, 0);
//绘制三角形
//GLES20.glDrawArrays(GLES20.GL_TRIANGLE_STRIP, 0, vertexCount);
//索引法绘制正方形
GLES20.glDrawElements(GLES20.GL_TRIANGLES,index.length, GLES20.GL_UNSIGNED_SHORT,indexBuffer);
//禁止顶点数组的句柄
GLES20.glDisableVertexAttribArray(mPositionHandle);


GLSurfaceView的使用流程
在xml中添加GlSurfaceView
创建渲染器类实现GlSurfaceView.Renderer
清除画布，并创建一个纹理并绑定到。
创建一个用来最后显示的SurfaceTexture来显示处理后的数据。
创建Opengl ES程序并添加着色器到该程序中，创建openGl程序的可执行文件，并释放shader资源。
打开摄像头，并配置相关属性。设置预览视图，并开启预览。
添加程序到ES环境中，并设置及启用各类句柄。
在onDrawFrame中进行画布的清理及绘制最新的数据到纹理图形中。
设置一个SurfaceTexture.OnFrameAvailableListener的回调来通知GlSurfaceview渲染新的帧数据。


MTK Camera2 中 GLSurfaceView 的生命周期
GLSurfaceView.onResume() < SurfaceViewController < PreviewManager < CameraAppUI < CameraActivity.onResumeTasks() < PermissionActivity.onPermissionResumeTasks() < QuickActivity.onResume()
```## Surface

```text
Surface 可以把它理解为一个Buffer，它是一块屏幕缓冲区。每个Window(窗口)对应一个Surface，任何View都是画在Surface上的。
Surface是纵深排序(Z-ordered)的，这表明它总在自己所在窗口的后面。Surfaceview 提供了一个可见区域，只有在这个可见区域内的Surface部分内容才可见，可见区域外的部分不可见。

SurfaceTexture就是纹理，你可以把它想像成一个距阵缓冲区。从Camera中采集的数据或从解码器中取出的数据可以放到SurfaceTexture里进行二次处理，然后再交给View去展示。
它的好处是，可以做各种滤镜。像直播中经常用到的美颜，水印等都可以通过它来处理。
```## SurfaceTexture

```text
https://source.android.google.cn/devices/graphics/arch-st?hl=zh-cn

SurfaceTexture 是 Surface 和 OpenGL ES (GLES) 纹理的组合。SurfaceTexture 实例用于提供输出到 GLES 纹理的接口。

SurfaceTexture 包含一个以应用为使用方的 BufferQueue 实例。当生产方将新的缓冲区排入队列时，onFrameAvailable() 回调会通知应用。然后，应用调用 updateTexImage()，这会释放先前占用的缓冲区，从队列中获取新缓冲区并执行 EGL 调用，从而使 GLES 可将此缓冲区作为外部纹理使用。
```## SurfaceFlinger

```text
SurfaceFlinger 是一个独立的Service， 它接收所有Window的Surface作为输入，根据ZOrder， 透明度，大小，位置等参数，计算出每个Surface在最终合成图像中的位置，然后交由HWComposer或OpenGL生成最终的显示Buffer, 然后显示到特定的显示设备上。

Surface——在Android中，Window与Surface一一对应。 如果说Window关心的是层次和布局，是从设计者角度定义的类，Surface则从实现角度出发，是工程师关心和考虑的类。Window的内容是变化 的，Surface需要有空间来记录每个时刻Window的内容。在Android的SurfaceFlinger实现里，通常一个Surface有两块 Buffer, 一块用于绘画，一块用于显示，两个Buffer按照固定的频率进行交换，从而实现Window的动态刷新。

Layer——Layer是SurfaceFlinger 进行合成的基本操作单元。Layer在应用请求创建Surface的时候在SurfaceFlinger内部创建，因此一个Surface对应一个 Layer, 但注意，Surface不一定对应于Window，Android中有些Surface并不跟某个Window相关，而是有程序直接创建，比如说 SurfaceView, 用于显示有硬件输出的视频内容等。
当多个Layer进行合成的时候，并不是整个Layer的空间都会被完全显示，根据这个Layer最终的显示效果，一个Layer可以被划分成很多的Region, Android SurfaceFlinger 定义了以下一些Region类型：
TransparantRegion： 完全透明的区域，在它之下的区域将被显示出来。
OpaqueRegion:  完全不透明的区域，是否显示取决于它上面是否有遮挡或是否透明。
VisibleRegion:  可见区域，包括完全不透明无遮挡区域或半透明区域 visibleRegion = Region - above   OpaqueRegion.
CoveredRegion:  被遮挡区域，在它之上，有不透明或半透明区域。
DirtyRegion:  可见部分改变区域，包括新的被遮挡区域，和新的露出区域。
```## ZSD/ZSL

```text
ZSD (Zero Second Delay) ，这是MTK的叫法，高通则简称作 ZSL (Zero Second Later)，其实是一个意思，就是0秒延时拍摄。0秒延时拍摄是真正的所拍即所得，就是说你按下快门那一刻拍到的照片就是你当时所看到的照片，它是相对于普通模式拍照来讲的。
在普通模式下拍照，按下快门后需要进行一系列地处理和校正，像对焦、曝光、白平衡等动作，然后再进行编码。譬如在预览30fps的情况下，你按下快门时是在第1帧，而实际上拍得的照片是第8帧的图像。
而ZSD情况下，会缓存若干帧，在按下快门那一刻，直接提取缓存帧进行编码保存照片。譬如在预览30fps的情况下，你按下快门时是在第1帧，则实际上拍得的照片是第1帧的图像。
这个可以通过在手机上开启秒表，启动相机去观察秒表最末一位的走时（100ms刷新一次），zsd 情况下能抓拍到你按下快门那一刻的读数。而非 zsd 则不能做到这一点。
```## TODO : 这些"对焦模式"有什么区别？

```text
/**
 * Auto-focus mode. Applications should call {@link
 * #autoFocus(AutoFocusCallback)} to start the focus in this mode.
 */
public static final String FOCUS_MODE_AUTO = "auto";

/**
 * Focus is set at infinity. Applications should not call
 * {@link #autoFocus(AutoFocusCallback)} in this mode.
 */
public static final String FOCUS_MODE_INFINITY = "infinity";

/**
 * Macro (close-up) focus mode. Applications should call
 * {@link #autoFocus(AutoFocusCallback)} to start the focus in this
 * mode.
 */
public static final String FOCUS_MODE_MACRO = "macro";

/**
 * Focus is fixed. The camera is always in this mode if the focus is not
 * adjustable. If the camera has auto-focus, this mode can fix the
 * focus, which is usually at hyperfocal distance. Applications should
 * not call {@link #autoFocus(AutoFocusCallback)} in this mode.
 */
public static final String FOCUS_MODE_FIXED = "fixed";
```## 毛玻璃效果/高斯模糊Gaussian Blur

```text
https://blog.csdn.net/weixin_44551646/article/details/107426792
均值模糊
中值模糊
高斯模糊
https://blog.csdn.net/qq_32515081/article/details/115006246

RenderScript    C++     效率高，可以先压缩图片(据前辈们经验，一般scale = 1/8 为佳)损失一点精度之后在进行高斯模糊。
fastBlur        Java    效率低

public Bitmap blurBitmap(Context context, Bitmap source, float blurRadius, int outWidth, int outHeight) {
    if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.JELLY_BEAN_MR1) {
        Bitmap inputBitmap = Bitmap.createScaledBitmap(source, outWidth, outHeight, false);
        Bitmap outputBitmap = Bitmap.createBitmap(inputBitmap);
        RenderScript rs = RenderScript.create(context);
        ScriptIntrinsicBlur blurScript;
        blurScript = ScriptIntrinsicBlur.create(rs, Element.U8_4(rs));
        Allocation tmpIn = Allocation.createFromBitmap(rs, inputBitmap);
        Allocation tmpOut = Allocation.createFromBitmap(rs, outputBitmap);
        blurScript.setRadius(blurRadius);
        blurScript.setInput(tmpIn);
        blurScript.forEach(tmpOut);
        tmpOut.copyTo(outputBitmap);
        return outputBitmap;
    } else {
        return source;
    }
}
```## MTK Camera Feature table

```text
[FAQ04462] 如何配置camera的feature table
配置camera 的feature table请按照如下进行：
RAW sensor 配置feature table涉及的文件,以main sensor为例，若是sub sensor，对应file name为*_sub.h
1）  alps\mediatek\custom\project name\hal\camera\camera\cfg_ftbl_custom_raw_main.h
2）  alps\mediatek\custom\common\hal\camera\camera\cfg_ftbl_custom_raw_main.h
YUV sensor 配置feature table涉及的文件,以main sensor为例，若是sub sensor，对应file name为*_sub.h
1）  alps\mediatek\custom\project name\hal\camera\camera\cfg_ftbl_custom_yuv_main.h
2）  alps\mediatek\custom\common\hal\camera\camera\cfg_ftbl_custom_yuv_main.h
3）  alps\mediatek\custom\common\hal\imgsensor\xxx_yuv\cfg_ftbl_xxx_yuv.h
注：xxx 是Sensor 的型号，比如OV5647
文件优先级规则：
对RAW/YUV sensor 涉及的配置文件，其生效优先级1） >  2） > 3）
即如果project name下有相应的文件，则仅需配置该文件，如没有再去配置common下的相应文件
配置方式：
#if 0/#if 1 控制feature的关闭/打开
BY_DEFAULT() 设定feature default值
BY_DEFAULT() 后面的枚举是feature的support Item
以Flash Light 为例，初始是配置如下
#if 0
    //  Flash Light
    CONFIG_FEATURE(FID_AE_STROBE,
        BY_DEFAULT(FLASHLIGHT_FORCE_OFF),
        FLASHLIGHT_AUTO, FLASHLIGHT_FORCE_ON, FLASHLIGHT_FORCE_OFF
    )
#endif
则表示项目上没有配置打开闪光灯功能，UI上也不会有闪光灯相关的菜单选项
如果需要配置打开Flash Light的feature，且想把default值修改为AUTO，另增加对TORCH的支持
则需要修改配置如下
#if 1
    //  Flash Light
    CONFIG_FEATURE(FID_AE_STROBE,
        BY_DEFAULT(FLASHLIGHT_AUTO),
        FLASHLIGHT_AUTO, FLASHLIGHT_FORCE_ON, FLASHLIGHT_FORCE_OFF,
                 FLASHLIGHT_TORCH
    )
#endif



[FAQ14556] Camera feature table 中的 size 修改相关
请修改遵循下面的原则来修改feature table 中的相关size。
Feature table 的基本原理、路径以及快速编译的方法请参考FAQ14389。
 
原则1：picture-size-values中最大值(max(width*height)), aspect ratio尽量和sensor resolution一致, 且width, height都需要16 align。
注：请一定保证picture size 16对齐。
[FAQ12224]CTS Fail: android.hardware.cts.CameraTest-- testPreviewPictureSizesCombination failed.

原则2：preview-size-values中最大值和picture-size-values中最大值 aspect ratio应该一致或者控制在0.01内, 建议preview-size最大值一般不要超过屏幕的resolution
注：所谓ratio也就是size 的宽高比。
在log中搜到
Video size 720x480 for profile ID 1 must be one of the camera device supported video size!
此项测试要求满足该项。同时需要video-size 和 preview-size 中添加上对应的size

原则3：video-size-values尽量包含下面的resolution:
QCIF 176X144,        QVGA 320X240            CIF 352X288,
480p 720x480,          720p 1280x720,        1080p 1920x1088
并且preview-size-values务必要包含video-size-values中的值
注: 如果在log中搜到类似CamcorderProfileTest: Size (352x288) is not supported
那么请在video-size 和 preview-size 中添加上对应的size。
 
如果有上述CTSfail，但是在添加size后还是测试fail。请务必确认以下两点：
1：请在log中搜vedio-size,picture-size,preview-size,确认添加的size有成功添加；
2：请在log中搜testRunner，确认目前的错误的原因还是相同的。

MTK camera metadata文件中size的配置解读
Metadata文件config_static_metadata_project.h中size的配置影响着很多CTS测试项的结果，这里解读一下关于size的配置。
Example：
68          CONFIG_ENTRY_VALUE(HAL_PIXEL_FORMAT_RAW16, MINT64)
69          CONFIG_ENTRY_VALUE(4160, MINT64)        // width
70          CONFIG_ENTRY_VALUE(3120, MINT64)        // height
71          CONFIG_ENTRY_VALUE(MTK_SCALER_AVAILABLE_STREAM_CONFIGURATIONS_OUTPUT, MINT64)   // output
72          CONFIG_ENTRY_VALUE(33333333, MINT64)   // frame duration
73          CONFIG_ENTRY_VALUE(33333333, MINT64)   // stall duration
74          CONFIG_ENTRY_VALUE(HAL_PIXEL_FORMAT_YCbCr_420_888, MINT64)
75          CONFIG_ENTRY_VALUE(4160, MINT64)        // width
76          CONFIG_ENTRY_VALUE(3120, MINT64)        // height
77          CONFIG_ENTRY_VALUE(MTK_SCALER_AVAILABLE_STREAM_CONFIGURATIONS_OUTPUT, MINT64)   // output
78          CONFIG_ENTRY_VALUE(33333333, MINT64)   // frame duration
79          CONFIG_ENTRY_VALUE(0, MINT64)           // stall duration
80          CONFIG_ENTRY_VALUE(HAL_PIXEL_FORMAT_BLOB, MINT64)
81          CONFIG_ENTRY_VALUE(4160, MINT64)        // width
82          CONFIG_ENTRY_VALUE(3120, MINT64)        // height
83          CONFIG_ENTRY_VALUE(MTK_SCALER_AVAILABLE_STREAM_CONFIGURATIONS_OUTPUT, MINT64)   // output
84          CONFIG_ENTRY_VALUE(33333333, MINT64)   // frame duration
85          CONFIG_ENTRY_VALUE(0, MINT64)

Format size： HAL_PIXEL_FORMAT_RAW16：看Camera APP是否需要raw16 数据，如果不需要就可以不配。如果需要，就要配置raw16 size, 这里面的raw16的含义是所有raw的能力，只要想有raw数据的输出，就要配置raw16，只能填一个size，该size要等于或者接近于active array size。

HAL_PIXEL_FORMAT_BLOB：该format用于capture的size

HAL_PIXEL_FORMAT_YCbCr_420_888：该format用于preview/video的size

只要配置了YCbCr_420_888 size，就要配置相同的BLOB size，不然CTS会有fai，且size要16对齐。

MTK_SCALER_AVAILABLE_STREAM_CONFIGURATIONS_xxx：OUTPUT表示HAL层回给APP的数据，INPUT是APP回灌给HAL层的数据（APP raw reprocess），这个要根据实际需求配置

frame duration：单位ns，与size大小无关，和fps有关，如果fps为30的话，那frame duration就得为 33 333 333， 若fps为24，则 frame duration 为 41666667，计算方法就是用1S除以帧率再换算成ns，此值需要和驱动中对应size的帧率相匹配。

stall duration：单位ns，HAL_PIXEL_FORMAT_YCbCr_420_888的stall duration需要配置成0，不然会有CTS fail，BOLB 的stall duration配置成和frame duration相同。

最后修改此文件可以通过mm vendor/mediatek/proprietary/hardware/mtkcam/utils/metastore/ push生成的对应库文件调试。



[FAQ14389] Feature Table 加载原理和调试方法
不同branch的feature table的位置可能略有不同，在修改和调试过程中，可能对于加载机制有所疑惑
[DESCRIPTION]
1  Feature Table文件的位置：   vendor/mediatek/proprietary/custom/<project>/hal/sendepfeature/<sensor_name>/config.ftbl.<sensor_name>.h
因为历史原因，有的会位于vendor/mediatek/proprietary/custom/<project>/hal/imgsensor/<sensor_name>/config.ftbl.<sensor_name>.h

2  如何确定Feature Table的位置究竟在哪里?
vendor/mediatek/proprietary/hardware/matkcam/v1/common/paramsmgr/feature/custom/Android.mk
此文件是如何编译feature table静态库的makefile.
会有类似如下的语句：
ifeq ($(wildcard $(MTK_PATH_CUSTOM)/hal/sendepfeature), )
MY_CUST_FTABLE_PATH +=  $(MTK_PATH_CUSTOM_PLATFORM)/hal/sendepfeature
endif
这说明使用的是hal/sendepfeature目录里面的feature table文件。

3 Feature Table文件是如何被编译的?
如上面的makefile,  它的执行是：
在指定的目录中寻找feature table文件，并把这些头文件加上#include 字样写到一个中间头文件custgen.config.ftbl.h，此中间头文件会被custom.cpp包含，最终编译到libcam.paramsmgr.feature.custom.a中.
   
 define my-all-config.ftbl-under
$(patsubst ./%,%, \
 $(shell find $(1) -maxdepth 1 \( -name "config.ftbl.*.h" \) -and -not -name ".*") \
 )
endef

 MY_CUST_FTABLE_FILE_LIST := $(call my-all-config.ftbl-under, $(MY_CUST_FTABLE_PATH))

LOCAL_MODULE := libcam.paramsmgr.feature.custom
LOCAL_MODULE_CLASS := STATIC_LIBRARIES
INTERMEDIATES := $(call local-intermediates-dir)
# custom feature table all-in-one file
MY_CUST_FTABLE_FINAL_FILE := $(INTERMEDIATES)/custgen.config.ftbl.h
LOCAL_GENERATED_SOURCES += $(MY_CUST_FTABLE_FINAL_FILE)
$(MY_CUST_FTABLE_FINAL_FILE): $(MY_CUST_FTABLE_FILE_LIST)
 @mkdir -p $(dir $@)
 @echo '//this file is auto-generated; do not modify it!' > $@
 @echo '#define MY_CUST_VERSION "$(MY_CUST_VERSION)"' >> $@
 @echo '#define MY_CUST_FTABLE_FILE_LIST "$(MY_CUST_FTABLE_FILE_LIST)"' >> $@
 @for x in $(MY_CUST_FTABLE_FILE_LIST); do echo "#include <`basename $$x`>" >> $@; done

#-----------------------------------------------------------
include $(BUILD_STATIC_LIBRARY)

4 如何快速调试feature table?
最终feature table静态库会被编译到libcam.paramsmgr.so中。
具体的编译为：

touch vendor/mediatek/proprietary/hardware/mtkcam/v1/common/paramsmgr/feature/custom/custom.cpp && \
mmm -j24 vendor/mediatek/proprietary/hardware/mtkcam/v1/common/paramsmgr/ 2>&1 | tee ft.lib.log && \
mmm -j24 vendor/mediatek/proprietary/<platform>/hardware/mtkcam/v1/common/paramsmgr 2>&1 | tee ft.so.log
最后把生成的libcam.paramsmgr.so 根据32位或者64位push到设备的/system/lib目录或者/system/lib64目录中。
一般，目前camera app使用的是32位的目录/system/lib.
因为此动态库是mediaserver加载，用如下命令重启mediaserver来重新加载feature table:
adb shell stop media && adb shell start media

如果是调试camera app, 请先关闭camera app, 避免app缓存了feature table信息导致调试不生效。

5 从log中如何查看feature table是否生效?
您可以在log中搜索MtkCam/ParamsManager来确定是否生效，也可以搜索"s8Symbols="来确定加载的是否是指定sensor的feature table.
"s8Symbols="的log信息来源于Feature.extern.cpp queryCustomFeature函数。

6  深入了解feature table的机制：
请在vendor/mediatek/proprietary/hardware/mtkcam/v1/common/paramsmgr/feature/custom/Android.mk中增加LOCAL_CFLAGS += -E 来获取custom.cpp预处理后feature table头文件的信息。
编译feature table静态库，最终会保存在out/target/product/<project_name>/obj/STATIC_LIBRARIES/libcam.paramsmgr.feature.custom_intermediates/custom.o
可以看出，就是把一些数据加到数组中，最后提供给外部一个query的函数来获取。



Android 8.0/9.0 Mtk Camera Picture size和Preview size配置
https://blog.csdn.net/zimu_2080/article/details/86647525

Picture size为了保证真实性，不做插值，按照camera sensor最大支持像素来配置。
Preview size根据实际来配置，有的预览可能设置太大了，造成卡顿。比如我手机分辨率是1440x720，添加18:9就不要再去添加2160x1080了。

Hal3
9.0配置路径变了。变化sendepfeature -----> imgsensor_metadata
随着9.0底层弃用hal1.0，而默认使用hal3.0，所有之前1.0的feature table配置size的方式已经行不通了。aosp/vendor/mediatek/proprietary/custom/mt6757/hal/sendepfeature不再是在这里配置了。

而是在imgsensor_metadata中进行配置：vendor\mediatek\proprietary\custom\mt6739\hal\imgsensor_metadata。

以s5k3l6_mipi_raw为例，Picture size和Preview size都在此文件中进行配置：
vendor\mediatek\proprietary\custom\mt6739\hal\imgsensor_metadata\s5k3l6_mipi_raw\config_static_metadata_scaler.h

添加修改处，这三个地方都要添加的：
CONFIG_METADATA_BEGIN(MTK_SCALER_AVAILABLE_STREAM_CONFIGURATIONS)//new hidden  
CONFIG_METADATA_BEGIN(MTK_SCALER_AVAILABLE_MIN_FRAME_DURATIONS)//new hidden
CONFIG_METADATA_BEGIN(MTK_SCALER_AVAILABLE_STALL_DURATIONS)//new hidden

CONFIG_METADATA_BEGIN(MTK_SCALER_AVAILABLE_STREAM_CONFIGURATIONS)//new hidden
        CONFIG_ENTRY_VALUE(HAL_PIXEL_FORMAT_BLOB, MINT32) //13mp 4:3
        CONFIG_ENTRY_VALUE(4096, MINT32)
        CONFIG_ENTRY_VALUE(3072, MINT32)
        CONFIG_ENTRY_VALUE(MTK_SCALER_AVAILABLE_STREAM_CONFIGURATIONS_OUTPUT, MINT32)

        CONFIG_ENTRY_VALUE(HAL_PIXEL_FORMAT_BLOB, MINT32) //12mp 1:1
        CONFIG_ENTRY_VALUE(3456, MINT32)
        CONFIG_ENTRY_VALUE(3456, MINT32)
        CONFIG_ENTRY_VALUE(MTK_SCALER_AVAILABLE_STREAM_CONFIGURATIONS_OUTPUT, MINT32)
        
        CONFIG_ENTRY_VALUE(HAL_PIXEL_FORMAT_BLOB, MINT32) //12mp 18:9
        CONFIG_ENTRY_VALUE(4896, MINT32)
        CONFIG_ENTRY_VALUE(2448, MINT32)
        CONFIG_ENTRY_VALUE(MTK_SCALER_AVAILABLE_STREAM_CONFIGURATIONS_OUTPUT, MINT32)
         
        CONFIG_ENTRY_VALUE(HAL_PIXEL_FORMAT_BLOB, MINT32) //9mp 16:9
        CONFIG_ENTRY_VALUE(4096, MINT32)
        CONFIG_ENTRY_VALUE(2304, MINT32)
        CONFIG_ENTRY_VALUE(MTK_SCALER_AVAILABLE_STREAM_CONFIGURATIONS_OUTPUT, MINT32)
        ...............
预览size也是在config_static_metadata_scaler.h这个里面加，要加在
HAL_PIXEL_FORMAT_YCbCr_420_888和
HAL_PIXEL_FORMAT_IMPLEMENTATION_DEFINED里面。

比如在HAL_PIXEL_FORMAT_YCbCr_420_888中
CONFIG_ENTRY_VALUE(HAL_PIXEL_FORMAT_YCbCr_420_888, MINT32)
CONFIG_ENTRY_VALUE(1920, MINT32)
CONFIG_ENTRY_VALUE(1080, MINT32)
CONFIG_ENTRY_VALUE(MTK_SCALER_AVAILABLE_STREAM_CONFIGURATIONS_OUTPUT, MINT32)
//这里添加720x720的1:1预览
CONFIG_ENTRY_VALUE(HAL_PIXEL_FORMAT_YCbCr_420_888, MINT32)
CONFIG_ENTRY_VALUE(720, MINT32)
CONFIG_ENTRY_VALUE(720, MINT32)
CONFIG_ENTRY_VALUE(MTK_SCALER_AVAILABLE_STREAM_CONFIGURATIONS_OUTPUT, MINT32)
//这里添加1440x720的18:9预览
CONFIG_ENTRY_VALUE(HAL_PIXEL_FORMAT_YCbCr_420_888, MINT32)
CONFIG_ENTRY_VALUE(1440, MINT32)
CONFIG_ENTRY_VALUE( 720, MINT32)
CONFIG_ENTRY_VALUE(MTK_SCALER_AVAILABLE_STREAM_CONFIGURATIONS_OUTPUT, MINT32)

CONFIG_ENTRY_VALUE(HAL_PIXEL_FORMAT_YCbCr_420_888, MINT32)
CONFIG_ENTRY_VALUE(1280, MINT32)
CONFIG_ENTRY_VALUE( 720, MINT32)
CONFIG_ENTRY_VALUE(MTK_SCALER_AVAILABLE_STREAM_CONFIGURATIONS_OUTPUT, MINT32)

在HAL_PIXEL_FORMAT_IMPLEMENTATION_DEFINED中：
CONFIG_ENTRY_VALUE(HAL_PIXEL_FORMAT_IMPLEMENTATION_DEFINED, MINT32)
CONFIG_ENTRY_VALUE(1920, MINT32)
CONFIG_ENTRY_VALUE(1080, MINT32)
CONFIG_ENTRY_VALUE(MTK_SCALER_AVAILABLE_STREAM_CONFIGURATIONS_OUTPUT, MINT32)
//这里添加720x720的1:1预览
CONFIG_ENTRY_VALUE(HAL_PIXEL_FORMAT_IMPLEMENTATION_DEFINED, MINT32)
CONFIG_ENTRY_VALUE(720, MINT32)
CONFIG_ENTRY_VALUE(720, MINT32)
CONFIG_ENTRY_VALUE(MTK_SCALER_AVAILABLE_STREAM_CONFIGURATIONS_OUTPUT, MINT32)
//这里添加1440x720的18:9预览
CONFIG_ENTRY_VALUE(HAL_PIXEL_FORMAT_IMPLEMENTATION_DEFINED, MINT32)
CONFIG_ENTRY_VALUE(1440, MINT32)
CONFIG_ENTRY_VALUE( 720, MINT32)
CONFIG_ENTRY_VALUE(MTK_SCALER_AVAILABLE_STREAM_CONFIGURATIONS_OUTPUT, MINT32)

CONFIG_ENTRY_VALUE(HAL_PIXEL_FORMAT_IMPLEMENTATION_DEFINED, MINT32)
CONFIG_ENTRY_VALUE(1280, MINT32)
CONFIG_ENTRY_VALUE( 720, MINT32)
CONFIG_ENTRY_VALUE(MTK_SCALER_AVAILABLE_STREAM_CONFIGURATIONS_OUTPUT, MINT32)

https://blog.csdn.net/dongxianfei/article/details/100013983
```## adb shell dumpsys media.camera > media.camera  信息解读

```text
这些信息是在哪里打印的？
frameworks/av/services/camera/libcameraservice/CameraService.cpp
status_t CameraService::dump(int fd, const Vector<String16>& args) {
    ATRACE_CALL();

    if (checkCallingPermission(sDumpPermission) == false) {
        dprintf(fd, "Permission Denial: can't dump CameraService from pid=%d, uid=%d\n",
                CameraThreadState::getCallingPid(),
                CameraThreadState::getCallingUid());
        return NO_ERROR;
    }
    bool locked = tryLock(mServiceLock);
    // failed to lock - CameraService is probably deadlocked
    if (!locked) {
        dprintf(fd, "!! CameraService may be deadlocked !!\n");
    }

    if (!mInitialized) {
        dprintf(fd, "!! No camera HAL available !!\n");

        // Dump event log for error information
        dumpEventLog(fd);

        if (locked) mServiceLock.unlock();
        return NO_ERROR;
    }
    dprintf(fd, "\n== Service global info: ==\n\n");
    dprintf(fd, "Number of camera devices: %d\n", mNumberOfCameras);
    dprintf(fd, "Number of normal camera devices: %zu\n", mNormalDeviceIds.size());
    dprintf(fd, "Number of public camera devices visible to API1: %zu\n",
            mNormalDeviceIdsWithoutSystemCamera.size());
    for (size_t i = 0; i < mNormalDeviceIds.size(); i++) {
        dprintf(fd, "    Device %zu maps to \"%s\"\n", i, mNormalDeviceIds[i].c_str());
    }
    String8 activeClientString = mActiveClientManager.toString();
    dprintf(fd, "Active Camera Clients:\n%s", activeClientString.string());
    dprintf(fd, "Allowed user IDs: %s\n", toString(mAllowedUsers).string());

    dumpEventLog(fd);

    bool stateLocked = tryLock(mCameraStatesLock);
    if (!stateLocked) {
        dprintf(fd, "CameraStates in use, may be deadlocked\n");
    }

    int argSize = args.size();
    for (int i = 0; i < argSize; i++) {
        if (args[i] == TagMonitor::kMonitorOption) {
            if (i + 1 < argSize) {
                mMonitorTags = String8(args[i + 1]);
            }
            break;
        }
    }

    for (auto& state : mCameraStates) {
        String8 cameraId = state.first;

        dprintf(fd, "== Camera device %s dynamic info: ==\n", cameraId.string());

        CameraParameters p = state.second->getShimParams();
        if (!p.isEmpty()) {
            dprintf(fd, "  Camera1 API shim is using parameters:\n        ");
            p.dump(fd, args);
        }

        auto clientDescriptor = mActiveClientManager.get(cameraId);
        if (clientDescriptor != nullptr) {
            dprintf(fd, "  Device %s is open. Client instance dump:\n",
                    cameraId.string());
            dprintf(fd, "    Client priority score: %d state: %d\n",
                    clientDescriptor->getPriority().getScore(),
                    clientDescriptor->getPriority().getState());
            dprintf(fd, "    Client PID: %d\n", clientDescriptor->getOwnerId());

            auto client = clientDescriptor->getValue();
            dprintf(fd, "    Client package: %s\n",
                    String8(client->getPackageName()).string());

            client->dumpClient(fd, args);
        } else {
            dprintf(fd, "  Device %s is closed, no client instance\n",
                    cameraId.string());
        }

    }

    if (stateLocked) mCameraStatesLock.unlock();

    if (locked) mServiceLock.unlock();

    mCameraProviderManager->dump(fd, args);

    dprintf(fd, "\n== Vendor tags: ==\n\n");

    sp<VendorTagDescriptor> desc = VendorTagDescriptor::getGlobalVendorTagDescriptor();
    if (desc == NULL) {
        sp<VendorTagDescriptorCache> cache =
                VendorTagDescriptorCache::getGlobalVendorTagCache();
        if (cache == NULL) {
            dprintf(fd, "No vendor tags.\n");
        } else {
            cache->dump(fd, /*verbosity*/2, /*indentation*/2);
        }
    } else {
        desc->dump(fd, /*verbosity*/2, /*indentation*/2);
    }

    // Dump camera traces if there were any
    dprintf(fd, "\n");
    camera3::CameraTraces::dump(fd, args);

    // Process dump arguments, if any
    int n = args.size();
    String16 verboseOption("-v");
    String16 unreachableOption("--unreachable");
    for (int i = 0; i < n; i++) {
        if (args[i] == verboseOption) {
            // change logging level
            if (i + 1 >= n) continue;
            String8 levelStr(args[i+1]);
            int level = atoi(levelStr.string());
            dprintf(fd, "\nSetting log level to %d.\n", level);
            setLogLevel(level);
        } else if (args[i] == unreachableOption) {
            // Dump memory analysis
            // TODO - should limit be an argument parameter?
            UnreachableMemoryInfo info;
            bool success = GetUnreachableMemory(info, /*limit*/ 10000);
            if (!success) {
                dprintf(fd, "\n== Unable to dump unreachable memory. "
                        "Try disabling SELinux enforcement. ==\n");
            } else {
                dprintf(fd, "\n== Dumping unreachable memory: ==\n");
                std::string s = info.ToString(/*log_contents*/ true);
                write(fd, s.c_str(), s.size());
            }
        }
    }
    return NO_ERROR;
}


== Service global info: ==                              ------>// Camera ID及数量情况,这里涉及到逻辑id,物理id等,还有可能手机厂商自己高的虚拟camera也在内,具体要看framework中打印的地方是怎么取的,这个地方没怎么关注过.
Number of camera devices: 8
Number of normal camera devices: 6
    Device 0 maps to "0"
    Device 1 maps to "1"
    Device 2 maps to "21"
    Device 3 maps to "22"
    Device 4 maps to "100"
    Device 5 maps to "101"
Active Camera Clients:
[
(Camera ID: 0, Cost: 99, PID: 20418, Score: -900, State: 0User Id: 0, Client Package Name: com.android.camera, Conflicting Client Devices: {1, })
]
Allowed user IDs: 0

== Camera service events log (most recent at top): ==                           ------->// 最近操作史
  04-22 06:36:07 : CONNECT device 0 client for package com.android.camera (PID 20418)
  04-22 06:25:41 : DISCONNECT device 0 client for package com.android.camera (PID 20418)
  04-22 06:23:38 : CONNECT device 0 client for package com.android.camera (PID 20418)
  04-22 06:23:38 : DISCONNECT device 1 client for package com.android.camera (PID 20418)
  04-22 06:03:53 : CONNECT device 1 client for package com.android.camera (PID 20418)

== Camera device 0 dynamic info: ==                                             ------->// 后置默认拍照打开此时device0处于活动状态.
  Device 0 is open. Client instance dump:
    Client priority score: -900 state: 0
    Client PID: 20418
    Client package: com.android.camera
  CameraDeviceClient[0] (0xe879d280) dump:
    Current client UID 10072
    State:
      Request ID counter: 3
      No input stream configured.

      Current output stream/surface IDs:                                        ------->// outputstream信息,看出来有三个stream
        Stream 0 Surface 0
        Stream 1 Surface 0
        Stream 2 Surface 0

Device dump:                                                                    ------->// 这里就看出来三个stream是什么了,一个surfaceTexture,用于显示预览
    Device status: ACTIVE
    Stream configuration:
    Operation mode: CUSTOM (36869) 
      No input stream.
    Stream[0]: Output
      Consumer name: SurfaceTexture-10-20418-3
      State: 4
      Dims: 1440 x 1080, format 0x22, dataspace 0x0
      Max size: 0
      Combined usage: 131328, max HAL buffers: 8
      Frames produced: 201, last timestamp: 984089393217873 ns
      Total buffers: 10, currently dequeued: 6
      DequeueBuffer latency histogram: (207) samples
        5     10     15     20     25     30     35     40     45    inf (max ms)
     98.07   1.45   0.00   0.48   0.00   0.00   0.00   0.00   0.00   0.00 (%)
     
    Stream[1]: Output                                                            ------->//ImageReader用于保存图片
      Consumer name: ImageReader-4000x3000f23m10-20418-15
      State: 4
      Dims: 4000 x 3000, format 0x23, dataspace 0x8c20000
      Max size: 0
      Combined usage: 131075, max HAL buffers: 8
      Frames produced: 0, last timestamp: 0 ns
      Total buffers: 18, currently dequeued: 0
      
    Stream[2]: Output                                                            ------->//竟然还有个imagereader,从其尺寸来看,要么是想搞缩率图要么就是想干其他事,不晓得,二维码识别或场景识别可能会用得到,我猜的,==
      Consumer name: ImageReader-1440x1080f23m1-20418-16
      State: 4
      Dims: 1440 x 1080, format 0x23, dataspace 0x8c20000
      Max size: 0
      
--------> // 信息很详细啊,这里还有max HAL buffers数量,这里要是不够的话就会导致卡顿或者hang住哦,
      Combined usage: 131075, max HAL buffers: 8
      Frames produced: 202, last timestamp: 984089426352300 ns
      Total buffers: 9, currently dequeued: 5
信息太多,找点有用的信息,
// dump hal的信息
== Camera HAL device device@3.5/legacy/0 (v3.5) dumpState: ==
###############  CameraId: 0 Dump Start  ###############
  +------------------------------------------------------------------+
  +         HAL Dump                                                 +
  +------------------------------------------------------------------+

  +------------------------------------------------------------------+
  +         Chi statistics                                           +
  +------------------------------------------------------------------+
 ---->//camx chi session信息:
  + Number of open sessions: 5
  + Number of open pipeline descriptors: 7
  +------------------------------------------------------------------+
  +           Chi Session                                            +
  +------------------------------------------------------------------+
  + Session: 0x6f8b344700
    +-----------------------------------------------------------------------------------------+
    Session 0x6f8b344700 state:
      reason                  = "ChiContextDump"
      numPipelines            = 1
      numRealtimePipelines    = 0
      partialMetadataEnabled  = false
   ....

------>//该session里的pipeline信息,因为后置默认拍照用到的是mfnr因此有多个pipeline
拿一个举例:
    Pipelines:
      Pipeline 0:
      name                          = "MfnrPrefilter_0"
      address                       = 0x6f80930800
   ...
      lastInOrderCompletedRequestId = 0
      currentRequest                = 0
      +------------------------------------------------------------------+
      Pending Nodes:
      Requests Range - lastInOrderCompletedRequestId: 0 currentRequest: 0
  .....
      Graph:
      Nodes + ports:
        Node: MfnrPrefilter_IPE0 
          InputPort 0, format: 0, portDisabled: false, bufferDelta: 0
          InputPort 1, format: 0, portDisabled: false, bufferDelta: 0
          InputPort 2, format: 0, portDisabled: false, bufferDelta: 0
          InputPort 3, format: 0, portDisabled: false, bufferDelta: 0
          OutputPort 10, format: 12  maxNumBuffers: 40, memFlags: 0x00000001, heap: 1,
            flags: 0x00000010, streamEnableMask: 0x00000001, numBatchedFrames: 1
            deviceIndex[0]: 17
          OutputPort 11, format: 18  maxNumBuffers: 40, memFlags: 0x00000001, heap: 1,
            flags: 0x00000010, streamEnableMask: 0x00000002, numBatchedFrames: 1
            deviceIndex[0]: 17
        Node: MfnrPrefilter_BPS0 
          InputPort 0, format: 0, portDisabled: false, bufferDelta: 0
          OutputPort 7, format: 3  maxNumBuffers: 40, memFlags: 0x00000001, heap: 1,
            flags: 0x00000010, streamEnableMask: 0x00000004, numBatchedFrames: 1
            deviceIndex[0]: 17
  ....
            
----->// pipeline里的 node link信息,从日志中就可以知道链接顺序了.
      Links:
        Node::MfnrPrefilter_BPS0::OutputPort_1 -> Node::MfnrPrefilter_IPE0::InputPort_0 -- bufferDelta = 0, maxImageBuffer = 0
        Node::MfnrPrefilter_BPS0::OutputPort_2 -> Node::MfnrPrefilter_IPE0::InputPort_1 -- bufferDelta = 0, maxImageBuffer = 0
        Node::MfnrPrefilter_BPS0::OutputPort_3 -> Node::MfnrPrefilter_IPE0::InputPort_2 -- bufferDelta = 0, maxImageBuffer = 0
        Node::MfnrPrefilter_BPS0::OutputPort_4 -> Node::MfnrPrefilter_IPE0::InputPort_3 -- bufferDelta = 0, maxImageBuffer = 0
        Node::MfnrPrefilter_IPE0::OutputPort_10 -> SinkBuffer_0 -- BufferQueueDepth = 0, maxImageBuffer = 0
        Node::MfnrPrefilter_IPE0::OutputPort_11 -> SinkBuffer_1 -- BufferQueueDepth = 0, maxImageBuffer = 0
        SourceBuffer_0 -> Node::MfnrPrefilter_BPS0::InputPort_0 -- bufferDelta = 0, maxImageBuffer = 40
        Node::MfnrPrefilter_BPS0::OutputPort_7 -> SinkBuffer_2 -- BufferQueueDepth = 0, maxImageBuffer = 0
        
 -------->其他mfnr的pipeline
     +------------------------------------------------------------------+
      Pipeline 1:
      name                          = "MfnrBlend_0"
      ....
       +------------------------------------------------------------------+
      Pipeline 2:
      name                          = "MfnrPostFilter_0"

--------> 当然还有其他的chx session
 
 一堆tuning的参数看不懂
------>//一些vendortag
== Vendor tags: ==

------>//这里是之前发生过camera故障时抓的进程trace信息,如果未出过错就没有有trace信息
== Camera error traces (2): ==
  ----- pid 1035 at 2020-04-10 23:29:00 -----
  Cmd line: /system/bin/cameraserver
  
  "cameraserver" sysTid=1035
    #00 pc 0003b29f  /system/lib/libbinde
```## camera知识点

```text
FV: Focus Value, 用来衡量图像AF的清晰度。
DOF: Deep Of Field, 景深，表示物距清晰的范围，景深越长表示物距前后清晰的范围越大。

Black Level Correction:
暗电流校准。此功能一般集成在sensor中，但是严格来说是属于ISP一部分。感光二极管在没有光照射情况下，释放了一部分电流，称为暗电流。需要去除之。
参考文档： 80-N7433-1_B

Linearization Correction:
Sensor输出的R/G和B/G颜色曲线理论上是1:1的比例，事实有差异，注意是颜色变化比例，不是说某一个pixel颜色不对，否则是bad pixel correction。 7x27a, 8260无此功能。
参考文档： 80-N7433-1_B

Bad Pixel Couplet Correction:
Bayer data里会出现某些pixel不正确，可能的情况有single bad pixel, couplet bad cluster, triplet bad cluster以及组合情况。 由简单到复杂的解决方法有 DBPC(defective bad pixel correction ) -> DBCC(defective bad cluster correction) -> ABCC(advanced bad cluster correction?)
参考文档： 80-N6848-1_B

Anti Banding:
Binding是指系统对图片颜色还原不精确的问题，特别是指图片颜色过渡不自然的现象。
在preview模式下，会看到有波浪纹。有50Hz和60Hz两种，Adil解释说是因为我们的日光灯用的是50Hz，所以我们的anti-banding值要选择50Hz.
Ref:
http://bbs.gfan.com/android-3858672-1-1.html

HDR(High Dynamic Range):
普通RGB信息无法表示亮度, HDR image通过增加亮度信息，能更真实还原图片亮度。
Ref:
http://www.douban.com/note/12429998/

LSC(Lens Shading Correction):
用来纠正画面不均匀。测试方式是对着白纸拍照。

BSS (Best Shot Selection).

CFP: Capture Feature Pipe
FPIPE: Feature Pipe
HAL: Hardware Abstract Layer
P2C: P2 Capture
P2S: P2 Streaming
SFP: Streaming Feature Pipe
TK: Turnkey
TP: Third Party
TPI: Third Party Interface
HWNode: hardware Node
MFLL: 
VSS: Video Snap Shot
MonoChrom: 单色，黑白相机

YNR  去亮噪
NR   去噪
EE     边缘细节优化
CNR    去彩噪

CI: Clean Image
BI: Bokeh Image
MBD: MTK Bokeh Depth
MDB: MTK Debug Buffer
MBM: MTK Bokeh Metadata


CMOS
CCD : charge coupled device 电荷耦合装置，它是一种高感光度半导体。受光线照射时，每个感光单位会将光线转化为电荷反应在组件上，所有感光单位所产生的信号加在一起构成一幅完整的画面。CCD像素数目越多，单一像素尺寸越大，收集到的图像越清晰。

RAW : 是一种图像文件。RAW文件包含原图片文件在传感器产生后，进入照相机图像处理器前的一切照片信息。
YUV : 欧洲电视系统所采用的一种颜色编码方法。现今采用三管彩色或彩色CCD摄影机进行取像，将取得的彩色图像信号经分色和分别放大校正后RGB，再经过矩阵变换电路得到亮度信号Y和两个色彩信号B-Y(U)、R-Y(V)，发送端将三个信号进行编码用同一信道发送。亮度信号和两个色度信号是相互分离的。
NV21 : YUV 格式的一种

YUV->RGB 的算法
JPEG(Joint Photographic Experts Group : 是第一个国际图像压缩标准。JPEG通过压缩照片原文件，减小文件大小，压缩照片以牺牲画质为代价)
ISP(Image Signal Processor图像信号处理器。对前端图像传感器输出信号处理)
DSP(Digital Signal Processor数字信号处理器)
Metadata
Camera API2/HAL3架构下使用了全新的CameraMetadata结构取代了之前的SetParameter/Paramters等操作，实现了Java到native到HAL3的参数传递。引入了管道的概念将安卓设备和摄像头之间联系起来，系统向摄像头发送 Capture 请求，而摄像头会返回 CameraMetadata，这一切建立在一个叫作 CameraCaptureSession 的会话中。
图片中的metadata信息中包含 Exif/Xmp/IPTC 等信息

IPTC是国际出版电讯委员会(International Press Telecommunications Council)的缩写，IPTC元数据就是一种标准格式，可以将以下元数据加入照片信息中，如作者，版权，字幕，细节描述等。
加入元数据与指配关键词标签有根本不同。元数据包含于图片本身中。当你将照片拷贝给别人的时候，元数据会跟着图片一起被拷走（因为它们就附在图片上）；如果你换了一看图软件或者换了一台电脑，那么这些新软件也能读出原有的这些元数据，并对相册加以管理。

snapshot 快拍。很早被运用到阵列和矩阵中，主要用于copy on write算法。
burst 连续脉冲信号序列，用于相机的连续拍摄。

Watermark水印

景深（DOF，Depth of Field）就是指聚焦后的清晰范围
Bokeh

SurfaceView/TextureView
SurfaceView：用于绘制相机预览图像，提供实时预览的图像。
SurfaceHolder：用于控制Surface的一个抽象接口，它可以控制Surface的尺寸、格式与像素等，并可以监视Surface的变化。
SurfaceHolder.Callback：用于监听Surface状态变化的接口。

SurfaceView和普通的View相比有什么区别呢？
普通View都是共享一个Surface的，所有的绘制也都在UI线程中进行，因为UI线程还要处理其他逻辑，因此对View的更新速度和绘制帧率无法保证。这显然不适合相机实时

Surface?

EXIF(Exchangeable Image File)
可交换图像文件，是一种图像文件格式。包含为数码相机定制的元数据和记录数码照片的拍摄参数、缩略图及其他属性。其遵从JPEG属性，只是在文件头信息中增加有关拍摄信息的内容和索引图，可以使用任何支持JPEG格式图像工具软件观看EXIF文件，但图像一旦被修改，EXIF信息可能会被永久丢失，故编辑EXIF必须使用专门的软件。

HDR(High-Dynamic Range高动态范围图像）

3DNR(数字降噪)--2D/3D

Exposure(曝光)

ZSL(Zero Shutter Lag : 零延时拍照。是为了减少拍照延时，让拍照和回显瞬间完成的一种技术)
FPS(Frames Per Second : 每秒传输帧数。每秒钟帧数越多，所显示画面越流畅)

AF(Auto Focus : 自动对焦)/FF(Fixed Focus : 固定对焦)
AF对焦系统目前有三种
CDAF（反差式对焦）
AF算法从ISP得到统计信息FV（Focus Value），算出镜头下一次要移动的距离和方向，遍历完NE（Near End）和FE（Far End）后，选择FV最大的位置。
VCM：Voice Call Motor：靠磁场+电来推动马达运动

PDAF（相差式对焦）
与CDAF比，PDAF需要特殊的sensor，有特别的像素点，有的遮住左边，有的遮住右边（Dual PD的话，多出来的每个像素包括两个二极管，模拟人的左右眼），ISP根据这些信息可以算出相位值（Phase Value），根据事先校准好的结果，将镜头一次性推送到合适的位置，但是PDAF也有缺陷，对于比较暗的环境效果不好，同时PDAF也存在一些偏差，需要CDAF来修正。

Laser assited AF（激光协助对焦）

AE(Automatic Exposure):自动曝光。
AWB(Automatic White Balance):自动白平衡。

Time Lapse(延时拍摄)
Slow motion(慢动作)
Voice note(有声照片)
QRCode

CV(Computer Vision : 计算机视觉)
商汤科技
旷视科技
云从科技
依图科技
OpenCV

美颜算法(Face Beauty)
人脸识别(Face Detection)
背景虚化()
AR增强现实(Advanced Reality)
人脸3D重建技术

-- ISS：Instruction Set Simulator 指令集仿真器 mimic the behavior 模仿行为
-- ICE：In-Circuit Emulator 在线仿真器
    是用来调试嵌入式系统软件的硬件设备。嵌入式系统开发者要面对一般软件开发者所没有的特殊问题, 因为嵌入式系统往往不像商业计算机那样具有键盘、显示屏、磁盘机和其他各种有效的用户界面和存储设备。当仿真器被插入到待开发芯片的某个部分的时候, 在线仿真也被称作硬件仿真. 这样的在线仿真器, 可以在系统运行实时数据的情况下, 提供相对很好的 调试能力。
-- PSW：Program State Word 程序状态字
-- AXI：Advanced Extensible Interface 高级扩展接口，用的最多的AMBA接口，在复杂的片上系统中至多连接100个主从模块。
    AXI总线，一种总线协议，该协议是ARM公司提出的AMBA（Advanced Microcontroller Bus Architecture）3.0协议中最重要的部分，是一种面向高性能、高带宽、低延迟的片内总线。它的地址/控制和数据相位是分离的，支持不对齐的数据传输，同时在突发传输中，只需要首地址，同时分离的读写数据通道、并支持Outstanding传输访问和乱序访问，并更加容易进行时序收敛。

-- ACE：AXI Coherency Extensions 是AXI一致性扩展，用于智能手机中的Big.Little系统
-- ATB：Advanced Trace Bus 用于在芯片间传输Trace数据
-- CTI：Cross Trigger Interface 交叉触发接口
-- DAP：Debug Access Port 调试访问接口
-- TPIU：Trace Port Interface Unit
-- FYI：for your  information 仅供参考
-- MIPI：Mobile Industry Processor Interface 移动行业处理器接口
-- DSI：Display Serial Interface 串行显示接口（位于处理器和显示模组之间的高速串行接口）
-- CSI：Camera Serial Interface 位于处理器和摄像模组之间的高速串行接口
-- ISP：Image Signal Processor 图形信号处理器
-- VSP：Video Signal Processor 视频信号处理器
-- CPP：Camera Post Processor 摄像机后处理 in charge of Camera image post processing
-- LCDC：LCD Controller
-- DCAM：Digital Camera Interface 数字摄像机接口
-- EMC：External Memory Controller 外部内存控制器
-- DMC：Dynamic Memory Controller 动态内存控制器
-- MPU：Memory Protection Unit 内存保护单元
-- EIC：External Interrupt Controller 外部中断控制器
-- SCSI: Small Computer System Interface 小型计算机系统接口，一种用于计算机和智能设备之间（硬盘，软驱，光驱，打印机）等接口标准
-- USB：Universal Serial Bus 通用串行总线
    串行总线：一次仅传送一位二进制位，仅需设置一根数据信号线。
    并行总线：一次同时传送多位二进制位，需要设置多条平行数据信号线。
-- NIC400: Network Interconnect 网络互联
-- MMU：Memory Management Unit 内存管理单元
-- CCI400：Cache Coherency Interconnect 缓存一致性互联
-- CCN：Cache Coherent Network 缓存一致性网络
-- TDD：Time Division Duplex 时分双工
-- FDD：Frequency Division Duplex 频分双工
-- SPI：Shared Peripheral Interrupts 公有外设中断
-- PPI：Private Peripheral Interrupts 私有外设中断
-- MBIST：Memory Build-in Self Test 存储器内建自测试
-- LBIST：Logic Build-in Self Test 逻辑内建自测试
-- ATM：Asynchronous Transfer Mode 异步传输模式
-- TDMA：Time Division Multiple Access 时分多路访问
-- WDM：WaveLength Division Multiplex 波分多路复用
-- PON：Passive Optical Network 无源光纤网络

Screen FTP
```## HEIF/HEVC/HEIC

```text
HEIF(High Efficiency Image File Format)是高效率图像文件格式，也称高效图像文件格式，是一个用于单张图像或图像序列的文件格式。它由运动图像专家组（MPEG）开发，并在MPEG-H Part 12（ISO/IEC 23008-12）中定义。

HEIF支持的用法包括：

存储单个或多个图像及其缩略图
存储连拍照片
支持同时捕获视频和静止图像，即将静止图像和定时图像序列存储在同一文件中
高效地表示动画和动态静图
存储焦点堆叠和曝光堆叠到同一个容器文件
存储从其他图像文件派生的图像，无论是以非破坏性图像编辑操作为目的派生的图像，还是作为预先计算派生的图像
支持存储其他媒体，例如音频和定时的文本，将定时的图像序列存储在同一个容器文件中，并且同步播放。
为了节约存储空间，HEIF封装的HEVC编码的图像可以用于压缩全分辨率图像，同时保留一个较低分辨率的JPEG副本（例如4K分辨率或更低）用于屏幕显示。数码相机和智能手机可以使用HEIF来实现单文件存储连拍、焦点堆叠或曝光堆叠的照片。与此类似，拍摄的视频与静态图像也可以存储在同一个HEIF文件中。HEIF还可以将任何图像集合存储在单个文件中，从而可以轻松分享。

HEVC(High Efficiency Video Coding)是一种新的视频压缩标准，即H.265，2013年1月26号，HEVC/H.265正式成为国际标准。

HEVC/H.265标准围绕着现有的视频编码标准H.264，保留原来的某些技术，同时对一些相关的技术加以改进。新技术使用先进的技术用以改善码流、编码质量、延时和算法复杂度之间的关系，达到最优化设置。

H.263可以2~4Mbps的传输速度实现标准清晰度广播级数字电视（符合CCIR601、CCIR656标准要求的720*576）；而H.264由于算法优化，可以低于2Mbps的速度实现标清数字图像传送；HEVC/H.265 High Profile可实现低于1.5Mbps的传输带宽下，实现1080p全高清视频传输。

由于HEVC/H.265支持各种色度格式和样品保真度至无损编码，该格式可以满足当今消费类设备所有的图像存储需求，从典型的8位图像到高端、专业设备所要求的高保真度和动态范围的16位图像。
HEIC(High Efficiency Image Coding)是一种图像压缩标准，上线时间还比较短，只有4年左右。自iOS 11和macOS High Sierra（10.13）内测开始，苹果将HEIC设置为图片存储的默认格式。与JPG相比，它占用的空间更小，画质更加无损。


HEIF 图片处理
搭载 Android 10 的设备支持 HEIC 压缩图片格式，它是 ISO/IEC 23008-12 中规定的高效图片文件格式 (HEIF) 的高效视频编码 (HEVC) 特定品牌。与 JPEG 文件相比，HEIC 编码的图片质量更好且文件更小。

HEIC 图片由摄像头传输框架生成，请求来自相机 HAL 的未压缩图片并将其发送到媒体子系统，以便由 HEIC 或 HEVC 编码器进行编码。

要求
要支持 HEIC 图片格式，您的设备必须拥有支持 MIMETYPE_IMAGE_ANDROID_HEIC 或 MIMETYPE_VIDEO_HEVC（具有恒定质量模式）的硬件编码器。

实现
要在您的设备上支持 HEIC 图片格式，请实现 HEIC/HEVC 编解码器，并为所需的流配置（即 IMPLEMENTATION_DEFINED/YUV 流和 JPEG 应用细分流）提供支持。

媒体
对于相应的硬件，以恒定质量 (CQ) 模式实现 HEIC/HEVC 编解码器，如下所示：

HEVC 类型编解码器使用具有 GRALLOC_USAGE_HW_VIDEO_ENCODER 用法的 IMPLEMENTATION_DEFINED 格式或 HAL_PIXEL_FORMAT_YCBCR_420_888 格式，具体取决于图片大小。
HEIC 类型编解码器使用具有 GRALLOC_USAGE_HW_IMAGE_ENCODER 用法的 IMPLEMENTATION_DEFINED 格式。
摄像头
在静态元数据中，将 ANDROID_HEIC_INFO_SUPPORTED 设置为 true，并将 ANDROID_HEIC_INFO_MAX_JPEG_APP_SEGMENTS_COUNT 设置为介于 [1, 16] 之间的值，以表明 JPEG 应用细分的数量。

对于每个必要的流组合，您的摄像头设备必须支持使用相同大小的 HEIC 流替换 JPEG 流。

对于公共 API 上的 HEIC 输出流，摄像头服务会创建两个 HAL 内部流：

具有 JPEG_APPS_SEGMENT 使用标记的 BLOB 流，可存储应用细分（包括 EXIF 和缩略图细分）
IMPLEMENTATION_DEFINED 和 YCBCR_420_888 会根据目标编解码器和 HEIC 流的大小流式传输 HEIC 流的大小
摄像头传输框架根据 ANDROID_HEIC_INFO_MAX_JPEG_APP_SEGMENTS_COUNT 为相机 HAL 分配足够大的缓冲区，以便填充 JPEG 应用细分。APP1 细分为必填项，但 APP1 之后（APP2 及以上）的细分为可选项。摄像头传输框架可以覆盖 APP1 细分中的 EXIF 标记（这些标记可以派生自捕获结果元数据或者与主图片比特流相关），并将它们发送至 MediaMuxer。

由于媒体编码器将屏幕方向嵌入到了输出图片的元数据中，以确保主图片和缩略图的屏幕方向一致，因此相机 HAL 不得根据 android.jpeg.orientation. 旋转缩略图。 该框架将屏幕方向写入到 EXIF 元数据和 HEIC 容器中。

与 JPEG 格式相关的静态、控制和动态元数据标记也适用于 HEIC 格式。例如，捕获请求中的 android.jpeg.orientation 和 android.jpeg.quality 元数据标记用于控制 HEIC 图片的屏幕方向和质量。

注意：无法同时配置 JPEG 和 HEIC 流。
要在应用中使用 HEIC 格式，请使用 HEIC 公共 API。

如需了解详情，请参阅以下来源。

相机 HAL

CameraBlob
ANDROID_HEIC_INFO_SUPPORTED
ANDROID_HEIC_INFO_MAX_JPEG_APP_SEGMENTS_COUNT
图形缓冲区数据空间

JPEG_APP_SEGMENTS
HEIF
图形缓冲区使用空间

HW_IMAGE_ENCODER
验证
要验证您的实现是否支持 HEIC 图片，请使用 TestingCamera2 测试应用，并运行以下摄像头 CTS 和 VTS 测试。

摄像头 CTS 测试

NativeImageReaderTest#testHeic
ImageReaderTest#testHeic
ImageReaderTest#testRepeatingHeic
ReprocessCaptureTest#testBasicYuvToHeicReprocessing
ReprocessCaptureTest#testBasicOpaqueToHeicReprocessing
RobustnessTest#testMandatoryOutputCombinations
StillCaptureTest#testHeicExif
摄像头 VTS 测试

VtsHalCameraProviderV2_4TargetTest.cpp
```## DNG(Digital Negative)

```text
通用Raw格式：DNG 
前面提到过，各大厂家都有自己的Raw格式，兼容性很差，长此以往很难维护。

因此Adobe公司开发出了DNG（Digital Negative）格式，用于无损、通用的储存Raw文件。数字负片(DNG) 是一种用于数码相机生成的原始数据文件的公共存档格式。DNG 解决了不同型号相机的原始数据文件之间缺乏开放式标准的问题, 从而有助于确保摄影师们将来能够访问他们的文件。

如果经常用Camera Raw或Lightroom做HDR合并、全景接片的朋友可能会发现，软件把原厂Raw文件进行合成后，生成的合并数字底片，都是dng的后缀。

DNG最大的优势就是通用，不光Adobe的软件可以打开，windows、apple、android系统的内置浏览软件，以及很多电脑、手机上的第三方软件，都可以预览这种格式。甚至很多相机、无人机、手机厂商，机内直出的就是DNG格式文件。与此同时，DNG格式会对文件进行一些无损压缩，因此体积更小，有时甚至不到原厂Raw文件的50%。因为DNG的无损性、通用性和更小体积，因此有的摄影师会在导入照片时，统一把原厂格式如NEF等，转换为DNG后缀的Raw格式，以便更好的储存和管理。当然对于大部分摄影师和爱好者而言，并不需要多此一举，保留原厂Raw文件已经足够。

还有一个值得一提的区别，就是原厂Raw文件是无法修改的。如果你在Camera Raw中对原厂Raw文件进行了修改，这些修改并不是储存在了Raw文件中，而是生成了一个.xmp的新文件，来保存这些更改。而Lightroom，则用catalog（目录）来保存这些更改。
DNG文件则不然，如果我们对DNG文件进行了修改，这些修改可以直接写入DNG文件本身，并不需要新生成文件。而且这些写入是无损的，随时可以一键复原成原始状态。

DngCreator DngCreator用于将RAW16转换为DNG。

https://blog.csdn.net/andytian1991/article/details/113756964
```## TIFF图像文件

```text
TIFF图像文件由三个数据结构组成，分别为文件头、一个或多个称为IFD的包含标记指针的目录以及数据本身。 
TIFF图像文件中的第一个数据结构称为图像文件头或IFH。这个结构是一个TIFF文件中唯一的、有固定位置的部分；IFD图像文件目录是一个字节长度可变的信息块，Tag标记是TIFF文件的核心部分，在图像文件目录中定义了要用的所有图像参数，目录中的每一目录条目就包含图像的一个参数。 
```## EXIF文件

```text
EXIF文件，最初由小日本电子业提出，它遵循JPEG标准，只是在文件头信息中增加了有关拍摄信息的内容和缩略图。 

简单来说，EXIF 信息就是由数码相机在拍摄过程中采集一系列的信息，然后把信息放置在我们熟知的 JPEG/TIFF 文件的头部，也就是说 EXIF 信息是镶嵌在 JPEG/TIFF 图像文件格式内的一组拍摄参数，主要包括摄影时的光圈、快门、ISO、日期时间等各种与当时摄影条件相关的讯息，相机品牌型号，色彩编码，拍摄时录制的声音以及全球定位系统（GPS）等信息。 

所有的JPEG文件以字符串“0xFFD8”开头，并以字符串“0xFFD9”结束。文件头中有一系列“0xFF??”格式的字符串，称为“标识”，用来标记JPEG文件的信息段。“0xFFD8”表示图像信息开始，“0xFFD9”表示图像信息结束，这两个标识后面没有信息，而其它标识紧跟一些信息字符。 
　　0xFFE0 -- 0xFFEF之间的标识符称为“应用标记”，没有被常规JPEG文件利用，Exif正是利用这些信息串记录拍摄信息如快门速度、光圈值等，甚至可以包括全球定位信息。按照Exif2.1标准对这些标识符的定义，数码相机可以把各种拍摄信息记入数码图像中，应用软件可以读取这些数据，再按照Exif2.1标准，检索出它们的具体含义,一般而言包括以下一些信息： 
Image Description 图像描述、来源. 指生成图像的工具 
Artist作者 有些相机可以输入使用者的名字 
Make 生产者 指产品生产厂家 
Model 型号 指设备型号 
Orientation方向 有的相机支持，有的不支持 
XResolution/YResolution X/Y方向分辨率本栏目已有专门条目解释此问题。 
ResolutionUnit分辨率单位 一般为PPI 
Software软件 显示固件Firmware版本 
DateTime日期和时间 
YCbCrPositioning 色相定位 
ExifOffsetExif信息位置，定义Exif在信息在文件中的写入，有些软件不显示。 
ExposureTime 曝光时间 即快门速度 
FNumber光圈系数 
ExposureProgram曝光程序指程序式自动曝光的设置，各相机不同,可能是Sutter Priority（快门优先）、Aperture Priority（快门优先）等等。 
ISO speed ratings感光度 
ExifVersionExif版本 
DateTimeOriginal创建时间 
DateTimeDigitized数字化时间 
ComponentsConfiguration图像构造（多指色彩组合方案） 
CompressedBitsPerPixel(BPP)压缩时每像素色彩位 指压缩程度 
ExposureBiasValue曝光补偿。 
MaxApertureValue最大光圈 
MeteringMode测光方式， 平均式测光、中央重点测光、点测光等。 
Lightsource光源 指白平衡设置 
Flash是否使用闪光灯。 
FocalLength焦距，一般显示镜头物理焦距，有些软件可以定义一个系数，从而显示相当于35mm相机的焦距 MakerNote(User Comment)作者标记、说明、记录 
FlashPixVersionFlashPix版本 （个别机型支持） 
ColorSpace色域、色彩空间 
ExifImageWidth(Pixel X Dimension)图像宽度 指横向像素数 
ExifImageLength(Pixel Y Dimension)图像高度 指纵向像素数 
Interoperability IFD通用性扩展项定义指针和TIFF文件相关，具体含义不详 
FileSource源文件 Compression压缩比。 
```## 双摄像头术语

```text
常见名词     英文释义        意义
B+B      Bayer+Bayer     主眼+副眼
B+M     Bayer+Mono    彩色+黑白
W+T     Wide+Tele        广角+长焦
Depth  Distance           深度
DoF      Depth of Field  景深
VSDoF   Video Shallow Depth of Field    实时景深
Bokeh  Bokeh              焦外成像
Refocus Re-Focus         重对焦
N3D      Native            两眼3D矫正、配准
LDC      Lens Distortion Correction      镜头畸变校正
DPE     Depth Engine    硬件生成depth map
GF Generate Depth-of-Field   生成blur map

1.摄像头组合方式
    1、彩色相机 + 彩色相机（RGB + RGB），主要用于计算景深，实现背景虚化和重对焦
    2、彩色相机 + 黑白相机（RGB + Mono），主要提升暗光/夜景影像拍摄质量
    3、广角镜头 + 长焦镜头（Wide + Tele），主要用于光学变焦
    4、彩色相机 + 深度相机（RGB + Depth），主要用于三维重建

2.帧率和 vtclk换算: vt clk/frame_length/line_length=fps , vt clk= line_length_pclkframe_length_linesframe_rate
三星sensor 参数计算
lineLengthPixelClock： 你去对应的setting中找下0342 寄存器，看下它后面写的值是多少，然后转化成十进制就可以了。比如我发给你的文件里面搜索到：0342 13A0， 你就把13A0 转换成十进制5024 就可以了。
frameLengthLines： 这个值对应的寄存器是0340 寄存器， 跟上面的方式一样。
minhorizontalBlanking： 这个值是用lineLengthPixelClock - output_width, Output_width就是输出的一行的大小，比如现在你的是4000x3000， 那4000就是output_width.
minVerticalBlanking： 这个值是用frameLengthPixelClock - output_height， output_height就是输出的一列的大小，对应 4000x3000 的话， 就是3000.
outputPixelClock： 这个值应该就是vt clk的值吧， 我已经写在了文件里了。
//< VFE (Video Front End) device.
//< CPP (Camera Post Processor) device.
//< CSID Camera Serial Interface Decoder
//< ISPIF Image Signal Processor InterFace
//< IFE (Image Front End) device.
//< ICP (Image Control Processor) device.
//< LRME (Low Resolution Motion Estimation) device.
 
景深
焦点前后各有一个容许弥散圆，这两个弥散圆之间的距离就叫焦深。以此推到被摄主体，相对于对焦点的前后，其影像也有一段清晰范围的就是景深。

VSDoF : 
实时景深，可在手机预览/拍照时实现大光圈淺景深效果

Gallery Refocus
点击椭圆红框进行refocus，仅仅是指不会虚化此点景深平面，清晰度与单摄Main cam对着花盆拍照时此区域清晰度一致

Data Flow
2.MT6757  Pre-Check
    2.1 3A/ISP check
    Bokeh的3A/ISP调试策略：
    让两个Camera的luminance/color/sharpness表现尽可能align

    ISP调试N3D_Preview时，避免出现overshoot、白边黑边等
        2.2 确认Module Info
        1. sensor组合，resolution
        2. Baseline, FOV
        3. Lens 型号，VCM型号，close loop 
        4. AF+AF AF+FF FF+FF
```## MtkCam3

```text
MtkCam3实现了Android定义的几个HAL3的接口:

ICameraProvider, ICameraDevice, ICameraDeviceSession, ICameraDeviceCallback;

AppStreamManager：
AppStreamManager位于framework与pipeline之间，把android streaminfo转换成平台版本的streaminfo。AppStreamMgr在HAL3架构中的位置（如果底层需要往上层传输数据，就在这里打包然后传到上层）。

Open阶段：初始化函数，生成各种Handler对象。
ConfigureStreams()阶段：会对stream流做一些解析，把安卓的straminfo转换成MTK平台的straminfo，打印config的各个steam的信息（三路：拍照，预览，录像）。
request阶段：主要是客制化修改metatada。
result阶段：回调到framework中。

PipelineModel：PipelineModel就是对整个pipeline进行管理，PipelineModel是HAL3的核心框架，对上需要对Pipeline创建操作API，对下需要建立Pipeline管理Pipeline生命周期。
open阶段：power on，open/close stage，Power on/off sensor，去操作sersen3A。
config阶段：创建pipelinecontext上下文，里面有很多Node，串联所有的HwNode来组成一条完整的Pipeline。
request阶段：接到上层queue下来的request，转化为Pipleline统一的IPipelineFrame，IPepelineFrame把请求Queue到PipelineContext里面去，决定node之间的连接关系。APP会设置一个buffer，其实就是申请一块内存来装载图像，但是对HAL来说，一个frame它包含了图像数据，也包含了它经过的哪些node，还有自己的metada数据。
Setting Policy：
主要职责是在Configuration阶段和Request阶段配置一些Setting信息，相当于一个容器，串联起各个Policy，需要哪些Policy以及他们之间的先后连接关系。
Config阶段的policy主要是功能是pipeline相关setting的决定，包括需要哪些HW Node、各个node的input/output配置及连接方式等。
Request阶段的policy主要做两件事，一是决定feature相关配置，一是决定pipelineFrame相关配置。

PipelineContext最终会根据policy决定出来的setting build出对应PipelineFrame queue到底层跑pipeline。

数据通路：
相机捕捉到的数据，会在TG这里收集后，由每一行转换成每一帧数据。
然后送到Pass1这里，Pass1这里分为RRZO（2400×1800）预览，IMGO（4160×3120）拍照，YUVO（FD人脸识别），这几部分。
不管是拍照还是预览都要进过Pass2，Pass2主要是由Raw转化成YUV。由Pass2出来后接着进入TPINode中，TPINode主要是三方算法的接口。
接着进入MDP中，这里面的主要功能是缩放相关的，会影响输出数据的大小，非4：3全尺寸的照片，比如全屏照片，1:1照片，就是在这里实现的。
最近进过JPEGNode处理后会存入内存中。

metadata：metadata是元数据，相机一般是根据应用层需要设置的模式，请求不同的元数据metadata，不同模式的metadata不同。
P1Node：主要的功能是负责出raw buffer，最后出出来RAW图给P2处理。
P2CaptureNode：主要作用是把IPipelineFrame转换成P2FrameRequest，建立feature node之间的连接。
feature node：rootNode->P2ANode->MultiframeNode(多帧降噪)->YUVNode。
rootNode：做了一些更新metadata的事情，设置需不需要做bss
P2ANode：转YUV，MultiframeNode：接多帧算法，处理request的时候根据frameType决定
nodeId是NID_MULTIRAW或者NID_MULTIYUV，
YUVNode：接单帧算法。

P2StreamingNode：
最先由P2StreamingNode接收上层的PipelineFrame封装成MWFrame格式，将Request封装后送给各个Node，送到P2S Driver去处理（封装的作用是降低耦合性）。
SFP在P2StreamingNode和P2Streaming Driver之间的一层，专门处理Streaming相关的Feature的效果。Streaming流程只接三个TPINode，每个TPINode接一个Plugin，Plugin下接入三方算法。

三方算法Plugin：
PipelinePlugin是mtk平台设计的一套挂载三方算法接口的机制，平台设计了一系列软件node，这些node里面插入了挂载三方plugin的入口，客户通过自己客制化不同的plugin达到插入各种单帧多帧，raw域或者yuv域算法

总结：在项目中除了要明白这些组件的原理外，还需要明白OpenCamera，ConfigureStream，Request，拍照，预览等这几个流程，每个平台的流程不一样，这需要自己根据每个平台的代码去追代码，画流程图，代码没有必要追得太详细，知道大概的流程即可上手项目，等项目需要再详细的分析代码。
```## HWNode

```text
HWNode: 负 责 整 合 MTK hardware functionality, software algorithm, 3rd party algorithm, 各
HWNode/FeaturePipe 细 部 介 绍 可 参 考”MTK camera P2CaptureNode introduction”与”MTK camera P2StreamingNode introduction “...等 HWNode 介绍文件。
```## 

```text

 P1Node:
 l
no
 The root node of the pipeline
o
 The input data is from upper layer
 Oo
 The output data is to the next P2CaptureNode and P2StreamingNode
e
o
 Uses ISP-P1
so
 Get / Set Hal3A module

 P2CaptureNode
 U
l
o
 o
 Process Support raw scale/crop
 data into yuvs
 a i mo
 Uses ISP-P2 & MDP
 t
 o
no
 Handle all MTK TK and 3rd party capture features c (with CaptureFeaturePipe),3rd party 整合
e .细部介绍可参考” MTK camera plugin interface user l guide”
d

 P2StreamingNode
 i ao
 Process raw data into yuvs
 f eo
 Support scale/crop
 n ro
 Uses ISP-P2 & MDP
 o
 eo
 Handle all MTK TK and C 3rd party streaming g features(with StreamingFeaturePipe) ,3rd party 整
合细部介绍可参考” MTK camera plugin a interface user guide”
k

 JPEGNode
 seo
 Convert YUV T to Jpeg
 @o
 Input data a
 from P2StreamingNode g or P2CaptureNode
o
 Output data to application
i n
 FDNode
 deo
 e
 Generate the FD f information

```## P2StreamingNode 介绍

```text
P版Hal3 上，Streaming相关的 flow(比如 preview, video record, VSS, EIS 等) 主要由 P2StreamingNode 以及这个 node 下各sub module来实现。
P2StreamingNode 是 Pipeline 中的一个 HwNode ，功能类似于旧架构中的 P2FreatureNode 。
接下来提到的 P2S 简写实际就是指 P2StreamingNode 以及这个 node 下各sub module 。

P2S 整个架构分4层。其中的 SFP 是 StreamingFeaturePipe 的缩写。
SFP Node 是 SFP 下的各个 node。request 传到 SFP 后，SFP 会往下丢到 SFP Node 处理。
SFP Node 的 flow 总是从 RootNode 开始，中间根据不同的处理需求，流经各个不同的node 处理，最终都会流到 HelperNode 处理。 HelperNode 会将处理结果 callback 回 StreamingProcessor。
TPINode 是用于挂载三方算法的 Node。
```## 单反+微单

```text
1. 单反是什么？
单反这类相机的英文是Single Lens Reflex（SLR），意思是“单镜头反光式取景相机”，在国内被简称为“单反”。

“单镜头”是说这个相机只安装一个镜头，毕竟胶片时代还存在一台机身带两支镜头的“双镜头反光式取景相机”（双反）。

“反光式取景”要求机身里有一个反光板和一个五棱镜。取景时，光线穿过镜头，再通过这两个小镜子的反射到达取景器，摄影者便可以在取景器里看到镜头拍到的景象。

2. 微单是什么？
常被大家叫做“微单”的这类相机在英文中对应的单词是Mirrorless，直译是“没有镜子”。全称则是 Mirrorless Interchangeable-lens Camera（MILC） ，意思是无反光镜的可换镜头相机。

微单相机内部的确也没有任何镜子，它采用的是电子取景。光线穿过镜头不经任何反射，直接投影在传感器上，摄影者依靠显示屏或电子取景器（本质上也是一块屏幕）来观察画面，大致原理和我们的手机类似。

这时或许你已经发现，尽管“微单”被无数人理解为了“微型单反”，但它其实和单反没有什么必然联系，更不是单反的一类分支。万万不可将小单反叫作微单。

更奇特的一条冷知识是，“微单”这种叫法还是中国大陆地区专供……在香港和台湾，微单相机被叫做“无反光镜相机”或“无反相机”。在其他国家，大家用各自的语言称呼微单的时候也基本是在强调“没有反光镜”这一特点，几乎没有提到“微型”或“小型”。换言之，微单不一定是小巧便携的相机。
```## CCM

```text
摄像头模组，全称 Camera Compact Module，以下简写为CCM
```## 微距镜头

```text
微距镜头（英语：macro lens）是一种用作微距摄影的特殊镜头，主要用于拍摄十分细微的物体，如花卉及昆虫等。为了对距离极近的被摄物也能正确对焦，微距镜头通常被设计为能够拉伸得更长，以使光学中心尽可能远离感光元件，同时在镜片组的设计上，也必须注重于近距离下的变形与色差等的控制。

大多数微距镜头的焦距都大于标准镜头，可以被归类为望远镜头，但是在光学设计上可能是不如一般的望远镜头的，因此并非完全适用于一般的摄影。
```## AF工作原理

```text
进入自动调焦模式后，Driver从0到最大值，使得镜头从原地移动到最大位移处，此时sensor成像面自动拍摄图片并保存到DSP内，DSP通过这些图片，计算每一副图片的MTF（Modulation transfer function）值，从而在这条MTF曲线中找到最大值，并通过算法，得到这个点对应的电流大小，再一次指示Driver提供给音圈这个电流，而使镜头稳定在这个成像面，使得达到自动变焦。
```## AF ROI?

```text
感兴趣区域 (AF Region of Interest)
```## 曝光表(AE Table)的作用是啥？工作原理

```text
AE Table（AE Pline Table）
影像亮度。由Shutter（曝光时间）、ISO（Gain值）、Aperture（光圈）和环境亮度决定。
用途：决定特定环境亮度使用多少的shutter和ISO。
出现不同AE Table的目的：使用不同场景。

Sport Mode：物体移动迅速，因此当环境亮度降低时，不延长曝光时间，而是先加大ISO（物体移动时，曝光时间长会导致残影）。
Candle Mode：物体静止，当环境亮度降低时，先延长曝光时间，之后再考虑加大ISO（长时间曝光对静止物体无残影问题，避免noise加大，因此先延长曝光时间）。
APEC：用来衡量曝光条件的公式。
AV+TV = EV = BV + SV (BV:      SV:)
AV:光圈值的级数  TV：快门值的级数   AV + TV:光通量的总和，即有多少光通过镜头到达Sensor。可视为曝光的供给面。 EV：用来衡量光通量的总和。
```## VSDOF

```text
Video Shallow h Depth of Field , 利用两颗 camera 图像得出景深数据,进而通过软件算法做出背景虚化效果的一个功能。也即利用软件算法模拟出专业相机使用大光圈拍照时的背景虚化效果.
背景虚化分为三种场景:预览虚化,视频虚化,拍照虚化。
背景虚化分为两个步骤:
1. depth(景深)计算:需要使用两眼的数据进行计算
2. bokeh 处理:depth+主眼的 clean img 合成出带有虚化效果的 img
```## TODO : AE同步

## TODO : 帧同步

```text
《How_to_check_stereo_camera_frame_sync.pdf》
```## HDR

```text
https://blog.csdn.net/vivo01/article/details/124173495

TAG
case HDR_VIEW_UPDATE_QUICK_SWITCH_ICON:
    if ((boolean) msg.obj) {
        mHdrEntryView.setVisibility(View.VISIBLE);
        updateHdrViewState(mHdr.getValue());
    } else {
        mHdrEntryView.setVisibility(View.GONE);
        updateHdrIndicator(false);
    }
    break;

int[] supportSceneList = cs.get(CameraCharacteristics.CONTROL_AVAILABLE_SCENE_MODES);
for (int value : supportSceneList) {
    if (value == CameraMetadata.CONTROL_SCENE_MODE_HDR) {
        supportedList.add(HDR_ON_VALUE);
        mIsHdrSupported = true;
        break;
    }
}
if (!mIsHdrSupported) {
    return;
}


骁龙865支持多种视频录制格式：HDR10+, HDR10, HLG, Dolby Vision。

HDR（High-Dynamic Range）是一种对高动态光照的渲染，又称为高动态范围图像，相对于普通的图像，能够展现更多的动态范围和细节；根据不同曝光时间的LDR（Low-Dynamic Range，低动态范围图像）图像，利用每个曝光时间相对应最佳细节的LDR图像来合成最终HDR图像，能够更好的反映出真实环境的视觉效果。

HDR10是由消费者技术协会2015年8月27日宣布的开放标准，不需要支付任何版权费。这个标准要求必须使用宽色域 Rec.2020 色彩空间，10bit 色深，以及 SMPTE ST 2084（PQ）图像传输功能，但它的数据元全部是静态的，简单来说就是每一帧所输出的 HDR 图像效果是一样的。

HDR10+，也称为 HDR10 Plus，于2017年4月20日由三星和亚马逊 Video 共同公布，由于杜比视界 HDR 极高的版权费用，三星等厂商不愿意支付，所以与松下、亚马逊和20世纪福斯创建了 HDR10 + 联盟，以推广HDR10 +标准。HDR10+ 通过添加动态元数据来更新 HDR10，动态元数据可用于在逐个场景或逐帧的基础上更精确地调整 HDR 的亮度级别，和杜比视界 HDR 类似，不过色深依旧是 10bit。

HLG（Hybrid Log-Gamma）是由 BBC 和 NHK 联合开发的 HDR 标准，它与标准动态范围（SDR）显示兼容，但它需要 10bit 色深。HLG 定义了非线性电光传递函数（EOTF），其中信号值的下半部分使用伽马曲线，信号值的上半部分使用对数曲线。HLG 标准免版税，与 SDR 显示兼容。HLG 由 HDMI 2.0b、HEVC、VP9 和 H.264 / MPEG-4 AVC 提供支持。HLG 主要应用于广播以及部分流媒体，如 BBC iPlayer、DirecTV、Freeview Play 和 YouTube。

Dolby Vision翻译为杜比视频高动态技术，通过提升画面亮度、扩展像素动态范围来提升影像效果，进而达到我们所要求的的目标。

杜比视界 HDR 是由杜比实验室提出并定制的 HDR 当前最高级标准，与 HDR10 不同的是，它不是开放的标准，需要使用它必须交付一定的版权费用。杜比视界要求必须使用宽色域 Rec.2020 色彩空间， SMPTE ST 2084（PQ）图像传输功能，与 HDR10 不同的是，它采用 12bit 色深，并且支持动态数据元结构，杜比视界允许 10000 尼特的最大亮度（目前在设备中最高只达到 4000 尼特）。
```## CHI API

```text
CHI API建立在Google HAL3的灵活性基础之上，目的是将Camera2/HAL3接口分离出来用于使用相机功能，它是一个灵活的图像处理驱动程序（摄像头硬件接口）。HAL3是根据摄像机pipeline request控制而设计，以提供完整的功能处理用户的控制请求。CHI旨在提供更细粒度的控制，以及访问ISP内的处理引擎，使得OEM和最终用户可以利用CHI API在相机驱动程序中实现自定义图像处理功能。如：通过高通的ISP、®Adreno™GPU 和 ®Hexagon™DSP等实现相应的Use Cases。
```## 光圈和焦距。

```text
光圈是安装在镜头上控制通过镜头到达传感器的光线多少的装置，除了控制通光量，光圈还具有控制景深的功能，光圈越大，景深越小，平时在拍人像时背景朦胧效果就是小景深的一种体现。

景深是指在摄影机镜头前能够取得清晰图像的成像所测定的被摄物体前后距离范围。
```## No Display Mode

```text
通常情况下,正常使用Camera的流程是:

打开Camera
设置参数
设置预览Surface
开启预览:startPreview()
拍照:takePicture()
但有些情况下, 我们希望不设置预览Surface就能拍照(默认情况下不设置预览进行拍照会Crash), 常见的应用场景是双摄项目, 打开了两个Camera,但副摄预览不需要用户看到, 这样做也可以减少系统资源占用, 高通和MTK平台都提供了不设置预览也可以拍照的功能, 使用方法如下:

高通平台
高通平台可以在ZSL开启的情况下, 通过设置参数Parameters.set("no-display-mode", "1");来达到不用设置Surface也能拍照的效果(参数必须在startPreview()之前设置).
MTK平台
MTK平台要更简单些, 保证ZSD开启的情况下, 直接不用设置Surface, 进行startPreview()和takePicture()即可.
```## HAL3

```text
Google HAL3官方文档
https://source.android.google.cn/devices/camera/camera3

MTK HAL3
MTK HAL3目前有把Middleware的部分剥离出来，放到mtkcam3（/vendor/mediatek/proprietary/hardware/mtkcam3/）这个repo，而3A/ISP driver/Utils的部分，还是维持使用mtkcam下面的文件

[FAQ18243] MTK平台HAL3支持情况
目前我司平台有支援HAL3，默认开的是HAL1.如果ap有特别的需求，需要使用API2，可以通过修改一些配置文件开HAL3.
每个平台的支援情况请参考DCC上：M Camera Plan.pptx
如何从HAL1.0切换到HAL3请参考DCC上：
HAL1 switch to HAL3.2.pptx
Programming Guide to switch Camera HAL 1.0 and Camera HAL3.2.docx
```## 查看Camera API和HAL版本

```text
Camera由于其复杂的特点, Android在发展过程中, Camera API也进行了更新, 在Android 5.0上, Google推出了Camera2 API, 同样HAL版本中API1和API2对应的版本是HAL1和HAL3. 但由于一些原因, HAL3和API2普及并不理想, 到目前为止, 中低端手机基本都是API1+HAL1, 对于开发者来说,我们可能想知道一个App用的API和HAL的版本,这个时候可以通过过滤Log方式来实现:

$ adb logcat | grep CameraService
04-07 14:07:43.174   371  4415 I CameraService: CameraService::connect call (PID -1 "com.smewise.camera2", camera ID 0) for HAL version default and Camera API version 1
可以看到Log打印的信息有App API的版本和HAL版本, API版本只有API1 和API2, HAL版本一般有三个结果: 256, 768, default.
256代表使用HAL1, 768为HAL3, default一般表示调用的是没有特别指定版本, 根据平台配置来决定,这种情况如果想知道到底使用的哪个版本, 需要看平台代码或者一些Log.

注:如果平台只支持HAL1, App通过API2去调用Camera的话, Framework层会将API2的调用转为用API1去调用, 也就是说虽然App使用的API2, 单对于CameraService来说使用的还是API1.

08-05 15:55:40.496 I/CameraService(  702): CameraService::connect call (PID -1 "com.android.camera2", camera ID 0) for HAL version default and Camera API version 2
```## Camera1/Camera2/CameraX

```text
Camera:Android 5.0以下
1）使用 Camera.open() 方法获取 Camera 对象实例。
2）使用 Camera.getParameters() 方法获取当前相机的相关设置。
3）根据需要使用 Camera.setParameters() 方法设置相机的相关参数。
4）根据需要使用 Camera.setDisplayOrientation() 设置相机正向。
5）使用 Camera.setPreviewDisplay() 方法为相机设置一个用于显示相机图像的 Surface。
6）使用 Camera.startPreview() 启动预览。
7）使用 Camera.takePicture() 方法进行拍照。
8）进行拍照后，预览视图会停止。使用 Camera.startPreview() 方法重新启动预览。
9）使用 Camera.stopPreview() 停止预览。
10）使用 Camera.release() 方法释放相机对象。应该在应用程序的 onPause() 方法中释放相机对象，在 onResume() 方法中重新打开相机对象。

Camera1（Android的傻瓜机）
Camera1 的开发中，打开相机，设置参数的过程是同步的，就跟用户实际使用camera的操作步骤一样。但是如果有耗时情况发生时，会导致整个调用线程等待；
开发者如果想要个性化设置camera效果，无法手动设置调整参数，需要依靠第三方算法对于回调的数据进行处理（NV21）。而且不同手机的回调数据效果都是不一样的，采用第三方算法调整，通常效果不好；
开发者所能获取的Camera状态信息有限；
camera1 的开发过程比较简单，对于常规视频采集，如果只要一般的预览功能，是没问题的，然而如果想要挖掘Camera更多的功能，camera1无法满足，于是有了camera2.

Camera2:Android 5.0以上

另外各家厂商(华为，OPPO，VIVO，小米)都对Camera2支持程度各不相同，从而导致需要花很大功夫来做适配工作。
做过相机的同学都知道，相机开发一般分为五个步骤：

检测相机资源，如果存在相机资源，就请求访问相机资源，否则就结束
创建预览界面，一般是继承SurfaceView并且实现SurfaceHolder接口的拍摄预览类，并且创建布局文件，将预览界面和用户界面绑定，进行实时显示相机预览图像
创建拍照监听器来响应用户的不同操作，如开始拍照，停止拍照等
拍照成功后保存文件，将拍摄获得的图像文件转成位图文件，并且保存输出需要的格式图片
释放相机资源，当相机不再使用时，进行释放
了解完开发步骤后，因为本文是针对Camera来进行开发，那下面先了解一些具体的类和方法。

Camera2（Android的单反）
Camera2 的开发中，camera的生命周期都是异步的，即发送请求，等待回调的client-service模式；
系统： Android L+；
这里的关键回调主要是三个：
（1）CameraDevice.StateCallback ///比如线程A发送打开相机请求, 线程B中收到相机状态回调，线程B中与cameraDevice建立会话，设置参数，数据回调处理；

（2）CameraCaptureSession.StateCallback ///与CameraDevice建立会话后，收到的会话状态回调；

（3）ImageReader.OnImageAvailableListener // 开发者可以直接获取并且操作的数据回调；

通过跟相机建立的会话，可以更加精细的调整Camera参数：比如ISO感光度，曝光时间，曝光补偿……；
如果开发者想要更多自己的定制，也可以直接使用回调数据（YUV488）；
MultiCamera的支持；

https://zhuanlan.zhihu.com/p/107263949

CameraX
CameraX（Android的个性化相机）
CameraX:基于Camera2API实现，极大简化在minsdk21及以上版本的实现过程
系统：Android L+
Jetpack 内的一套Camera开发支持库。
特点：
更简单易用的API，更少的代码量，使开发者更专注业务的个性化实现。比如：对采集到图片做分析处理。
更好的兼容性，减少不同设备适配烦恼：包括宽高比、屏幕方向、旋转、预览大小和高分辨率图片大小。
数据分析: 开发者依然可以对数据进行个性化处理。
第三方Camera特效拓展：对于一些手机厂商特定实现的camera特效，开发者也可以使用。


1.无需使用findViewById 或者 butterknife

使用Kotlin Android Extensions插件即可实现该功能，它是Kotlin 插件的组成之一，无需再单独安装插件。

我们在各个modules的build.gradle中添加该插件，即可使用。

apply plugin: 'kotlin-android-extensions'
布局文件中的id，可以直接在代码中使用。

首先，按照import kotlinx.android.synthetic.main.布局文件名*的方式导入。

例如MainActivity，它的布局文件是activity_main.xml

则按照如下的方式进行import

import kotlinx.android.synthetic.main.activity_main.*
```## API2

```text
Camera2 API中主要涉及以下几个关键类：

CameraManager：摄像头管理器，用于打开和关闭系统摄像头
CameraCharacteristics：描述摄像头的各种特性，我们可以通过CameraManager的getCameraCharacteristics(@NonNull String cameraId)方法来获取。
CameraDevice：描述系统摄像头，类似于早期的Camera。
CameraCaptureSession：Session类，当需要拍照、预览等功能时，需要先创建该类的实例，然后通过该实例里的方法进行控制（例如：拍照 capture()）。
CaptureRequest：描述了一次操作请求，拍照、预览等操作都需要先传入CaptureRequest参数，具体的参数控制也是通过CameraRequest的成员变量来设置。
CaptureResult：描述拍照完成后的结果。
如果要操作相机设备，需要获取CameraManager实例。CameraDevices提供了一系列静态属性集合来描述camera设备，提供camera可供设置的属性和设备的输出参数。描述这些属性的是CameraCharacteristics实例，就是CameraManager的getCameraCharacteristics(String)方法。

为了捕捉或者流式话camera设备捕捉到的图片信息，应用开发者必须创建一个CameraCaptureSession，这个camera session中包含了一系列相机设备的输出surface集合。目标的surface一般通过SurfaceView, SurfaceTexture via Surface(SurfaceTexture), MediaCodec, MediaRecorder, Allocation, and ImageReader.

camera 预览界面一般使用SurfaceView或者TextureView,，捕获的图片数据buffers可以通过ImageReader读取。

TextureView可用于显示内容流。这样的内容流可以例如是视频或OpenGL场景。内容流可以来自应用程序的进程以及远程进程。
TextureView只能在硬件加速窗口中使用。在软件中渲染时，TextureView将不会绘制任何内容。
TextureView不会创建单独的窗口，但表现为常规视图。这一关键差异允许TextureView移动，转换和使用动画
之后，应用程序需要构建CaptureRequest，在捕获单个图片的时候，这些request请求需要定义一些请求的参数。

一旦设置了请求，就可以将其传递到活动捕获会话，以进行一次捕获或无休止地重复使用。两种方法还具有接受用作突发捕获/重复突发的请求列表的变体。重复请求的优先级低于捕获，因此在配置重复请求时通过capture()提交的请求将在当前重复（突发）捕获的任何新实例开始捕获之前捕获。

处理完请求后，摄像机设备将生成一个TotalCaptureResult对象，该对象包含有关捕获时摄像机设备状态的信息以及使用的最终设置。如果需要舍入或解决相互矛盾的参数，这些可能与请求有所不同。相机设备还将一帧图像数据发送到请求中包括的每个输出表面。这些是相对于输出CaptureResult异步生成的，有时基本上稍晚。
```## FOV(视场角)

```text
视场角(FOV)field angle of view，相机可以接收影像的角度范围，也可以常被称为视野。

HFOV: 水平FOV
VFOV: 垂直FOV
DFOV: 对角FOV
由Fig.2可以看出，HFOV由Focal Length和senor的宽度(W)决定， VFOV由Focal Length和sensor的高度(H)决定。DFOV由Focal Length, W, H共同决定。
```## FOVA

```text
FOVA 主要用于 SAT 切换的过程两眼的图像对齐,图像做融合,让使用者对切换过程能够平滑无感。
```## DNR(数字降噪)

```text
数字降噪（DNR），存在两种DNR – 2D和3D

减少图像噪声的第一种方法是2D降噪，这是时域降噪的 一种形式。减少时域杂讯的工作原理是，将每个帧中的每个像素作为序列的一部分进行分析，将每个帧的像素作为整个序列的一部分进行比较，并查找在帧与帧之间出现的不一致的伪像，目标和像素。可以选择最有可能代表噪声的像素，并隔离和修复这些像素。
2D /临时降噪是一种有效的降噪方法，但在监视用途中存在一些缺点。首先，在低分辨率图像上效果最佳。视频开始超过4到8 MP时，将不如3D降噪有效。而且，如果要校正的区域存在运动（视频源中很可能会出现这种情况），临暂时性的噪点减少容易造成不良的运动模糊，影响视频的清晰度和质量，并使视频变得困难。
这就是3D降噪的用武之地。

3D DNR的工作原理与2D方法不同，依赖于空域降噪而不是时域降噪。空域降噪不是逐帧分析视频像素的顺序，而是将外观作为视频线性时域轴的一部分来判断，使用一种算法来分别比较每帧中的像素，然后将这些帧彼此进行比较，查看哪些像素改变或移动。该方法允许算法区分和隔离代表噪声的像素，并将其从图像中删除。
3D DNR可以更好地消除低光视频趋于呈现的颗粒状外观，并且对于运动较多的视频则要好得多，因为采用逐帧比较的方法，可以更准确的检测运动。结果，不会在图像中产生运动模糊，并且移动的目标不会在后面留下运动轨迹。适用于更大，更高分辨率的视频，后者需要额外的功能才能获得清晰的监控录像。
结合2D和3D DNR以获得最佳视频
现在，一些功能强大的高端相机将2D和3D DNR方法结合到一个动态算法中，可以创建具有尽可能低图像噪点的超清晰图像。3D DNR在帧中包含效果更好的运动区域，因为在减少噪点，而不产生运动模糊方面更有效；2D DNR在解码和清除帧的静态部分时效率更高。共同创建清晰和动态的低照度图像，可以作为全面闭路CCTV系统的一部分进行有效监视。

2D降噪：只在2维空间域上进行降噪处理。基本方法：对一个像素将其与周围像素平均，平均后噪声降低，但缺点是会造成画面模糊，特别是物体边缘部分。因此对这种算法的改进主要是进行边缘检测，边缘部分的像素不用来进行模糊。

3D降噪：增添了时域处理，因此变为3维。和2d降噪的不同在于，2d降噪只考虑一帧图像，而3d降噪进一步考虑帧与帧之间的时域关系，对每个像素进行时域上的平均。例如，假设场景静止，那么连续两帧图像内容没变，他们的差值就是2倍的噪声。通过减少时域上的改变降低噪声。
相比2d降噪，3d降噪效果更好，且不会造成边缘的模糊，但存在的主要问题是：画面不会是完全静止的，如果对不属于同一物体的两个点进行降噪处理会造成错误。因此该方法需要运动估计，其效果好坏也与运动估计相关。而运动估计计算量大，耗时长，是制约3d降噪的主要瓶颈。
```## 多帧降噪算法(MFNR)

```text
Multi-frame Noise Reduction (MFNR)

骁龙865支持多帧去噪功能。

所谓多帧降噪就是在夜景或者暗光环境下，相机在按快门到成像的时候会采集多张/多帧照片或者影像，在不同的帧数下找到不同的带有噪点性质的像素点，通过加权合成后得到一张较为干净、纯净的夜景或者暗光照片。通俗地说，就是手机在拍摄夜景或者暗光环境的时候，会进行多个帧数的噪点数量和位置的计算和筛选，将有噪点的地方用没有噪点的帧数替换位置，经过反复加权、替换，就得到一张很干净的照片，其实最终成像的照片是由多个帧数的影像合成的。

由于多帧降噪利用时域信息，多帧融合，有时会出现部分物体的重影，影响拍摄质量，好的算法可以解决该问题。
```## MFNR 多帧降噪

```text
https://blog.csdn.net/Cmatrix204/article/details/117931180

本文参考论文：Denoising image sequences does not require motion estimation
http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.131.6394&rep=rep1&type=pdf

这篇论文主要写的是如何利用多帧图像进行降噪处理。

论文主要从以下几个部分展开：
1、NLmeans
先是介绍了non local means降噪算法。该算法之前有介绍过，主要是通过单帧图像中的冗余信息来进行降噪处理。通过在一帧图像中查找当前像素的相似像素点，然后对这些像素进行加权平均操作。评判是否相似可以有多种方式，基于L2或者高斯核等等。

2、把nlmeans引申到多帧场景。
多帧场景中，在不同帧的类似像素点位置，总是能够找到类似的像素点，因此，通过这些像素点的加权平均，我们也可以得到较为干净的图像。
作者表示这样的操作可以避免运动估计处理，运动估计不仅费时，而且如果存在误差，对于结果则会适得其反。而查找类似像素点的方式并不会严格要求图像对齐。

3、多帧降噪与其他算法对比
其他算法包括光流法、模版匹配法进行运动估计的算法。

总的来说，这篇论文还是比较好理解的。关键在于如何压缩算法复杂度，怎样保证快速高效才是重点。该算法可以运用在video denoising的场景，但是如何达到实时，还需要不断的尝试。后续在这方面有进展再进行更新。
```## 光圈

```text
如果把相机理解成小孔成像，那么光圈就是小孔的大小，即光圈就是控制光线进入镜头面积的装置，经典的如采用叶片组的方式来实现：
在这里插入图片描述
光圈数值分母越大，表示光圈越小，光圈主要有两方面的作用：控制进光量和景深：
```## 进光量

```text
这个比较容易理解，光圈越大，相同的快门，成像进来的光越多，照片就越亮，反之光圈越小照片就越暗。
```## 快门

```text
之前说光圈可以控制进光量，快门也可以，光圈从空间上限制进光面积来控制进光量，而快门则是从曝光时间上来控制。可以简单地理解为：快门挡在镜头或底片前，平时处于关闭状态，成像时快门打开一段时间再关闭，完成成像，这个快门打开的时间就是快门时间，通常以1/N秒为单位。快门除了可以控制进光量从而影响照片曝光，还可以制造一些特别的拍照效果。

如图子弹穿过灯泡的照片，需要极高的快门速度，而有些照片效果又需要长时间的快门才行，如城市的车流效果
需要注意的是，当快门时间较长时，相机的抖动可能会造成成像模糊，使用三脚架是不错的选择。
```## 夜间降噪与多帧降噪的原理

```text
https://blog.csdn.net/z827997640/article/details/81175692
```## 硬解/软解

```text
硬解
字面上理解就是用硬件解码。通过显卡的视频加速功能对高清视频进行解码。可以理解为有一个专门的电路板来进行视频的解码工作，是依靠GPU。
调用GPU的专门模块编码来解码，减少CPU运算。显卡核心GPU拥有独特的计算方法，解码效率非常高，这样不但能够减轻CPU的负担，还有着低功耗，发热少等特点。
但是，由于硬解码起步比较晚，软件和驱动对他的支持度很低，基本上硬解码内置什么杨的模块，就解码什么样的视频，面对网上各色各样的视频编码样式，兼容性不好。此外，硬解码的滤镜、字幕、画质方面都做的不够理想。
对于android设备，目前用得比较多的芯片就是高通、海思和联发科，这些芯片大都集成了很多的功能，CPU、GUP、DSP、ISP包括视频解码、音频解码等等
在Android中使用硬件解码直接使用MediaCodec就可以了，虽然MediaPlayer也是硬件解码，但是被封装得太死了，支持的协议很少。而MediaCodec就很好拓展，我们可以根据流媒体的协议和设备硬件本身来自定义硬件解码，代表播放器就是Google的ExoPlayer。

软解
字面上理解就是用软件解码。但是实际上还是要硬件支撑。这个硬件就是CPU。
在软解码过程中，需要对大量的视频信息进行运算，所以对CPU性能的要求非常高。尤其是对高清大码率的视频来说，巨大的运算量就会造成转换效率低，发热量高等问题。
我们最最常见的视频软解码开源库就是FFmpeg。目前基于FFmpeg的开源播放器有B站的ijkplayer
不过，软解码不需要过多的硬件支持，兼容性非常高，即使出现新的视频编码格式，只要安装好相应的解码器文件，就可以顺利播放。而且软解码拥有丰富的滤镜，字幕，画面处理优化等效果，只有你CPU够强悍，就能够实现更加出色的画面效果。

总结
在Android设备硬件支持的情况下优先使用Android设备的硬件解码，减少CPU的占用，更加省电。
在Android设备硬解不支持的情况下选择使用软解码，不管怎么样，视频至少能够播放，具有更好的适应性，但是增加了CPU的占用，更加费电，软硬结合才是王道，根据实际情况合理选择
```## 光学变焦 vs 数码变焦

```text
数码变焦当 zoom 到一定程度,细节就会模糊,而光学变焦则在 zoom 到一定成细节还能保持清晰,如下对比图可以很明显看到光学变焦的图像质量优于数码变焦。

光学变焦的工作原理
光学变焦是通过移动镜头内部镜片的相对位置来改变焦点的位置，改变镜头焦距的长短，并改变镜头的视角大小，从而实现影像的放大与缩小。
如果被拍摄的物体位置保持不变，镜头的焦距与物体的放大倍率会呈现正比例的关系，如果要用一个词来形容光学变焦的话，那就是“望远镜”。


数码变焦的工作原理
数码变焦可以有两种形式：

其一，是通过插值算法，对图像进行插值运算，将图像的尺寸扩大到所需的规格，这种算法就其效果而言，并不理想，尤其是当使用在手机上的时候，手机上的摄像头本身得到的数据就有较大的噪声，再插值的话，得到的图像几乎没法使用。实际上，即使是数码相机的数码变焦功能也没有太大的实用价值。如果插值算法没有硬件支持，则需要在应用层实现。我司某平台的数码变焦用的就是该种办法。

其二，其实是一种伪数码变焦的形式，当摄像头不处在最大分辨率格式的情况下，比如130 万像素的 sensor 使用 640*480 的规格拍照时，仍旧设置 sersor 工作在 1280*960 的分辨率下，而后通过采集中央部分的图像来获取 640*480 的照片，使得在手机上看来所拍物体尺寸被放大了一倍。也有很多手机采用的是这种数码变焦方式，这种办法几乎不需要额外的算法支持，对图像质量也没有影响，缺点是只有小尺寸情况下可以采用。此外在 DV方式下也可以实现所谓的数码变焦放大拍摄功能。（这应该是一个卖点，对 Dv 来说，这种数码变焦还是有实际意义的）。

要采用这种变焦模式，驱动需要支持 windowing 功能，获取所需部分的 sensor 图像数据。

数字变焦是通过可拍照手机处理器，把图片内的每个像素面积增大，从而达到放大的目的，就像我们在ACDSEE等图像处理软件中，强行拉大图像的像素一样，

只不过这个过程在手机中进行，把原来SENSOR上的一部分像素使用插值手段进行放大。与光学变焦不同的是，数码变焦是在SENSOR垂直方向上的变化，而给人以

变焦效果的。由于整个过程焦距没有任何变化，所以图像质量是会随着放大比例的增加，逐渐下降。(成像面垂直方向缩放)

数字变焦也可以分为插值算法变焦和伪数字变焦两种：

插值算法变焦：对图像进行插值运算，将图像的尺寸扩大到所需的规格，这种算法就其效果而言，并不理想，尤其是当使用在手机上的时候，手机上的摄像头

本身得到的数据就有较大的噪声，再插值的话，得到的图像几乎没法使用。

伪数字变焦：当摄像头不处在最大分辨率格式的情况下，比如130 万像素的 sensor 使用 640*480 的规格拍照时，仍旧设置 sersor 工作在 1280*960 的分辨率
下，而后通过采集中央部分的图像来获取 640*480 的照片，使得在手机上看来所拍物体尺寸被放大了一倍。这种办法几乎不需要额外的算法支持，对图像质量也没有影
响，缺点是只有小尺寸情况下可以采用。
```## TODO : ImageBuffer

## TODO : lazy hal

## ISP流程

```text
RAW域：是指从DPC一直到demosaic阶段（此流程图）
DPC:坏点矫正(bed pixel corr),坏点由于芯片制造工艺等问题产生的，坏点是指亮度或者色彩与周围其他像素的点有非常大的区别，常用检测方法是在全黑环境下看亮点和彩点和在盖白板的情况下看黑点和彩点，ISP端一般通过在亮度域上取其他周围像素点均值来消除坏点
BLC:黑电平矫正(Black level corr)，黑电平是指图像数据为0时对应的信号电平，进行黑电平矫正的目的；一是由于sensor本身会存在暗电流，导致在没有光照进来的条件下pixel也有电压输出，不过这部分一般在sensor端就已经处理掉了，还有一个原因是因为sensor进行模数转换时精度不够，以8bit为例，每个pixel有效范围是0-255，sensor可能无法将接近于0的信息转化出来，由于人眼特性（对暗处细节比较敏感，）所以sensor厂商一般在转换时会加一个固定的偏移量使像素输出在5（非固定值）—255之间，然后传输在ISP端再做一个减法，将5（非固定值）变为0
Denosice:降噪. 噪声在图像上常表现为一引起较强视觉效果的孤立像素点或像素块。一般在暗态下噪声表现尤为明显。影响人的主观视觉感受及对目标的观测，所以进行降噪，但是降噪一般伴随着细节的损失
LSC: 镜头亮度矫正（lens shading corr）由于镜头光学系统原因（CRA），sensor中心光轴附件的pixle感光量比四周多，所以导致呈现出来的画面会中心亮四周暗（同时由于边缘入射角大，会造成相邻像素间串扰，严重时会导致角落偏色）。 所以进行lsc的主要目的是为了让画面四周亮度与中心亮度一直，简单理解就是用过增加四周像素的gain值，来达到亮度一致
AWB：自动白平衡（auto white balance），白平衡顾名思义就是让白色在任何色温下camera都能把它还原成白，由于色温的影响，一张白纸在低色温下会偏黄，高色温下会偏蓝，白平衡的目的就是白色物体在任何色问下都是R=G=B呈现出白色，比较常用的AWB算法有灰度世界，完美反射法等
Demosica；颜色插值。SENSOR每个pixel只感知一种颜色分量（如流程图一开始所示），由于人眼对绿色比较敏感所以G的分量是R与B的两倍，所形成的图像称之为Bayer图，所以要通过颜色插值使每个pixel上同时包含RGB三个分量
CCM :色彩校正（color corr matrix），AWB已经将白色校准了，CCM就是用来校准白色除白色以外其他颜色的准确度的，用一个3X3的CCM矩阵来校准, 其中每一列系数r1+g1+b1等于一个恒定值1。Ccm矫正最终结果可以通过拍摄24色卡图片然后用imatest分析来做分析参考
Ygamma ；由于最早期的显示器端，亮度与电流之间响应不线性的，而是以曲线形式（曲线称之为gamma曲线），camera为了配合显示器显示出正确的亮度所以有了摄像头的gamma曲线与显示器gamma曲线成反比（不是绝对的），后来随着显示器的工艺发展，显示器亮度与电流之间已经可以做成显性关系了，但是人们发现由于gamma曲线的存在，摄像头暗部才能信息更好保留显示，更符合人眼视觉感受，我们可以通过调整gamma曲线来调整摄像头的亮度，对比度，动态范围等等的效果
EE：锐化，当物体锐化值过低时会出现边缘模糊，图像给人感觉不清晰，锐化过高就会导致图像出现锯齿白边等现象
CSM：色彩空间转化（color space matrix），RGB图像通过一个转转举止向SRGB等色彩空间转化的过程


Horizontal Flip：做水平翻转
Test Pattern：ISP内部产生测试图像，ISP内部调试使用
Black Level Correction：黑电平矫正，黑电平是指图像数据为0时对应的信号电平，进行黑电平矫正的目的；一是由于sensor本身会存在暗电流，导致在没有光照进来的条件下pixel也有电压输出，不过这部分一般在sensor端就已经处理掉了，还有一个原因是因为sensor进行模数转换时精度不够，以8bit为例，每个pixel有效范围是0-255，sensor可能无法将接近于0的信息转化出来，由于人眼特性（对暗处细节比较敏感，）所以sensor厂商一般在转换时会加一个固定的偏移量使像素输出在5（非固定值）—255之间，然后传输在ISP端再做一个减法，将5（非固定值）变为0
Bad Pixel Correction：坏点消除
Lens Shadow Correction：镜头阴影矫正（镜头缺陷、光通量不均匀）
AF Statistics in Raw：AF统计信息
CFA Interpolation：去马赛克，将RAW转成RGB
D65 White Balance：做标定，使得在D65下面，使得白色的物体呈现白色
AWB Statistics：做完D65 White Balance后可以做AWB 统计信息
AWB：AWB算法根据色温值做白平衡矫正
CCM：3×3的颜色矩阵，目的是让成像系统颜色符合人眼睛看到的颜色。AWB已经将白色校准了，CCM就是用来校准白色除白色以外其他颜色的准确度的，用一个3X3的CCM矩阵来校准, 其中每一列系数r1+g1+b1等于一个恒定值1。Ccm矫正最终结果可以通过拍摄24色卡图片然后用imatest分析来做分析参考
Gamma：Gamma矫正，原因是人眼睛的非线性特性，亮度发生变化时，人眼感受到的不是成倍的关系
CSC：RGB到YUV色彩空间转换
AE Statistics：AE统计信息
2DNR：空间域降噪
3DNR：时间域降噪
AF Statistics in YUV：AF 统计信息
Local Tone Mapping：图像每一个局部区域都足够清晰
Sharpness：锐化让图像变得更清晰
WDR：宽动态算法让图像的动态范围变得更大
Post-Process：后处理
LDC：镜头畸变矫正
De-shaking：防抖
```## BB端是什么意思？BaseBand?

```text
我们这的BB端-原本是是baseband基带的意思，这里理解成CPU即可

Sensor端和BB（平台）端的区别
Sensor端一般只支持AWB的OTP,但是我们需要Eeprom保存LSC的OTP data，LSC校正交给BB端来做。
因此很多平台Sensor不支持 OTP 我们都需要BB端来做。

BB与Sensor端通过I2C来通信（读写寄存器），包括SCL（I2C Clock） SDA（I2C Data）信号
```## TODO : 高通滤波器/低通滤波器

```text
低通滤波器用于过滤噪声
高通滤波器用于使Edge更加Sharp
```## TPI/Custom Zone

```text
目前有两种框架可供选择(TPI / Custom Zone)

TODO : 两者有什么区别或优缺点？
```## SAT

```text
SAT 即 Spatial Alignment n Transform,空间对齐变换,也即光变切换。一般采用不同 FOV的摄像头,在放大或者缩小到一定倍率的时候进行切换,以达到光学变焦的效果,光变切换过程中会涉及到 h 3A, Crop 等对齐处理,也有可能会在切换过程中使用两眼做图像融合,以达到画面在切换过程中平滑过渡的效果。
```## PIP

```text
PIP 即 Picture in Picture,又称画中画或者双景录像。是 preview/record 画面呈现两颗 camera 影像的一个 feature。区别于 Logical multicam, PIP 打开的两颗 camera 是独立的,app 需要开两次 camera,两颗 camera 之间不会有 frame sync 与 3a sync。
```## PipelineModel

```text
PipelineModel 往下会连接到 PipelineContext 已经相对应的 config 的 HWNode
PipelineModel 是连接上层 hidl hal 以及下层 HWNode 的重要模块,在 open/close camera 、config、request 阶段都扮演着不同的角色。
```## TODO : HW Bokeh?

## FPC : Flexible Printed Circuit（柔性电路板）

```text
FPC是以聚酰亚胺或聚酯薄膜为基材制成的一种具有高度可靠性，绝佳的可挠性印刷电路板。具有配线密度高、重量轻、厚度薄、弯折性好的特点。

FPC全称为柔性线路板，柔性电路板是以聚酰亚胺或聚酯薄膜为基材制成的一种具有高度可靠性，好的可挠性印刷电路板，具有配线密度高、重量轻、厚度薄的特点。
一般颜色为黄色透明的，一般需要开定制模具生产，普遍应用于手机、笔记本电脑、PDA、数码相机、LCM以及精确度好的小仪器上。

FPC的基本结构
铜箔基板：FCCL 铜箔基板分为电解(ED)铜跟压延铜(RA) 厚度常规为1/3 1oz （主流厂商台虹、联茂、斗山、新杨）1/2oz 和 1/3 oz （电解铜制造成本低但是更易碎,压延铜制造昂贵但是更柔软）
覆盖膜：Coverly
补强板：一般分为PI或者FR4材料
EMI：电磁屏蔽膜（主流厂商：拓自达、东洋、城邦达力、方绑 ）

FPC的生产工艺流程
1.双面板制程
开料→钻孔→黑孔→镀铜→前处理→贴干膜→对位→曝光→显影→图形电镀→脱膜→前处理→贴干膜→对位→曝光→显影→蚀刻→脱膜→表面处理→贴覆盖膜→压制→固化→沉镍金→印字符→剪切→电测→冲切→终检→包装→出货

1.单面板制程
开料→贴干膜→对位→曝光→显影→图形电镀→脱膜→表面处理→贴覆盖膜→压制→固化→沉镍金→印字符→剪切→电测→冲切→终检→包装→出货

工艺详解：
开料：将来料铜箔裁切至合适的尺寸
钻孔：根据Layout 图纸，利用钻头在铜箔上钻孔
黑孔：将石墨和碳粉通过物理的作用在孔壁上形成一层导电膜，然后直接通过电镀的方式在钻孔壁形成铜
沉镍金：FPC漏铜表面增减镀金是为了增强FPC导通性、焊接性能、抗氧化性，但为了防止金层向铜层渗透，导致渗金，需要先在铜表面镀一层镍用作隔离，镍太厚硬度高，柔软性差，太薄强度差，容易脱落
```## 等效焦距换算

```text
简单的说，就是以135相机作为一种标准，把非135规格相机的焦距折算成135相机的焦距，嘿嘿，这样让人比较容易理解。 产生差别的主要原因是感光元件的大小不同，.

实际焦距，是指镜头的实际光学焦距，一般是以传统的135胶片相机镜头为标准的。但在数码相机成为主流的今天，镜头标注的都是等效焦距，所谓等效，就是相当于全画.

实际焦距：4.2-126mm 乘以5.7就是等效于35mm焦距 24-720mm 光学变焦：126除以4.2=30倍，即720除以24=30倍。就是光学变焦30倍

不同的传感器尺寸有一个对应的等效系数，镜头焦距乘等效系数就是等效焦距。

实际焦距乘以焦距转换系数，得到的就是等效焦距……比如实际焦距100mm，焦距转换系数1.5，等效焦距就是150

等效焦距折算成实际焦距有什么公式或者什么折算表

我们现在所说的等效焦距都是与135胶片为依据的：实际焦距*(135胶片的对角线长度/本机感光元件的对角线长度)=实际焦距*([24↑2+36↑2]↑(1/2)/本机感光元件的对角线长度.

换算等效焦距的话为什么尼康需要乘以1.5的倍率，而佳能的需要乘以1.6的转.

Canon 焦距x1.6。Nikon 焦距x1.5

所谓24—70mm的等效焦距通常是指35MM画幅，也就是说135系统，它和相机传感器尺寸大小有关，比如APS-c单反配50MM镜头就等效于135系统的80MM左右

想弄明白，互相的换算系数。 如： EF-S 10mm在全画幅上用相当于多少。 .

APS-C相机：佳能为实际焦距*1.6，例如：佳能18-135相当于全画幅相机的28.8-216.尼康为实际焦距*1.5，宾得为实际焦距*1.5

1、我们常说APS-C相比全画幅的相机等效焦距需要乘以1.6倍(cannon),.

楼主确实有一定的专业和求知精神，值得俺学习。不知道楼主是否注意过小DC或DV镜上的焦距标注，如5.4-54mm，一个10倍变焦的镜头，再根据该款相机的感光原件面.

是的，全画幅的感光元件不需要换算就是传统相机的焦距。

的焦距相当于31-465mm请问各位大虾多少倍光学变焦是怎么换算成焦距的？。

镜头焦距出厂前就已经内定好了，是设计的时候选定好的。H10:380/38=10，表示镜头最短焦到最长焦，焦长变化是10倍S5:432/36=12，表示镜头最短焦到最长焦，焦长变.

请问各位大虾多少倍光学变焦是怎么换算成焦距的？它有一定的公式吗？那能.

楼上的看清楚人家是问“多少倍光学变焦是怎么换算成焦距的”，其实一般的多少倍变焦换算成焦距就是用厂家给的光学变焦的倍数乘上厂商给出的广角端的数值就是你看.

看公式是：35mm焦距=焦距/ccd尺寸*1.7但我怎么算也算不明白，能否给个实。

这个公式是哪里搞的？不对啊！因为数码单反或者是DC的感光元件比传统胶片小，所以按照35mm相机的标准，需要乘一个系数这个系数由于面积缩小后，等效果镜头在.

一般单反相机镜头的焦距的标称都是按照135相机 标的 的，而所谓的全画幅数码单反相机的CCD或CMOS(感光成像的元件)尺寸和135相机胶卷35mm的尺寸是相同，因.

怎么把焦距换算成35mm等效焦距

用35除以转换系数就行了，比如尼康数码单反相机的镜头转换系数是1.5，那就是35/1.5=24MM.

什么是等效焦距？ 请简洁概括的回答 谢谢

等傚焦距 就是根据相机实际焦距相当于35mm的转换焦距~ 例如： 实际焦距6.3mm~27mm 相当于35mm的等傚焦距大概为 28mm~120mm

4.068mm就是镜头的实际焦距 内容拓展：一、大家习惯于将不同尺寸感光元件上成像的视角，转化为135相机上同样成像视角所对应的镜头焦距，这个转化后的焦距就是.

镜头标注的都是等效焦距，所谓等效，就是等同于全画幅单反相机的焦距比如EF头在全画幅使用，50mm就是50mm而在半画幅使用，实际焦距就是50*1.6EF-S头在半画幅.

比如我的LX2的Leica镜头是6.3-25.2mm的，怎么样转换为35mm的等效焦距？。

等效焦距就是你必须了解，数码机器的ccd面积比标准35mm相机的底片面积(24mm*36mm)小多少倍，相当于接受光线的面积小很多，视角变窄，此机ccd面积约为标准.
```## 景深

```text
景深就是当与光轴平行的光线射入凸透镜时，理想的镜头应该是所有的光线聚集在一点后，再以锥状扩散开来，这个聚集所有光线的一点，就叫做焦点。在焦点前后，光线开始聚集和扩散，点的影象变成模糊的，形成一个扩大的圆，这个圆就叫做弥散圆。

如果弥散圆的直径小于人眼的鉴别能力，也就是说在一定范围内，实际影象产生的模糊肉眼是不能感觉到的，结果人的肉眼看上去这个范围内的影像仍是清晰的．这个在理论上已经模糊但实际上却被肉眼辨认为清楚的弥散圆就称为容许弥散圆。

在焦点前后各有一个容许弥散圆，这两个弥散圆之间的距离就叫景深，即：在被摄主体(对焦点)前后，其影像仍然有一段清晰范围的，就是景深。换言之，被摄体的前后纵深，呈现在底片面的影象模糊度是肉眼不能辨认的（人们肉眼看出的图像感觉仍是清晰的），都在容许弥散圆的限定范围内。

上面这段用规范的专业语言解释的景深，过于专业了点，比较晦涩难懂，但还得先这样说一下，不能理解也没有问题，下面我会用通俗的语言再解释一遍。

在进行拍摄时，调节相机镜头，使离相机一定距离的景物清晰成像的过程，叫做对焦，那个景物所在的点，称为对焦点，因为"清晰"并不是一种绝对的概念，所以，对焦点前（靠近相机）、后一定距离内的景物的成像用我们的眼睛看都可以是清晰的，这个前后清晰范围的总和，就叫做景深。举个例子，你以一个离相机5米远的人作为对焦点，人前1米有朵花，离开相机的11米处有棵树，12米处有间房子，13米处有辆汽车。当你拍出的照片上，花、人和树都是清晰的，而花前和房子及房子以后的都是模糊的，那么，这张照片的清晰范围是在离相机的4--11米处，那么，这张照片的景深就有7 米。要是这张照片上从花、人到树和房子都是清晰的，而花前、汽车和汽车以后的景色都是模糊的，那这张在照片的景深我想大家已经知道，那就是8米。

景深的大小，首先与镜头焦距有关，焦距长的镜头，景深小，焦距短的镜头景深大。其次，景深与光圈有关，光圈越小（数值越大，例如f16的光圈比f11的光圈小），景深就越大；光圈越大（数值越小，例如f2.8的光圈大于f5.6）景深就越小。其次，前景深小于后后景深，也就是说，精确对焦之后，对焦点前面只有比较短的距离内的景物能清晰成像，而对焦点后面很长一段距离内的景物，都是清晰的。

https://blog.csdn.net/shen924/article/details/8670077
```## 慢动作录像

```text
慢动作录像(SlowMotionRecord)？

通常咱们人眼可能承受的最好的视频帧速率是24帧/每秒左右。那如果咱们用120帧/秒拍摄一个动作，再用24帧每秒来播放的话，视频就加快了5倍，这个就是慢动作录像了。

慢动作录像，又叫高帧率录像(HFR),也就是以高fps(运行速率)捕捉、编码并保留为30 fps(指标速率)，这种状况运行速率大于指标速率。

(还有一种模式叫做高速录制(HSR) : 即以高fps(运行速率)捕捉、编码并保留为高 fps(指标速率),运行速率等于指标速率。)

https://blog.csdn.net/weixin_42465953/article/details/117614865
```## Android MTK6739 Camera2架构和方法

```text
在Mtk的6739平台中运用了新的Camera2的架构来开发。
主要分为3大块1、common，2、feature，3、host
common主要是一些公共的库内容的调用。
feature主要值的是客制化的内容，该内容能够根据Andorid.mk的文件配置来判断是否把这段内容编译到系统中。
host主要是主目录，activity，已经UI部分的处理。

编译配置在host/assets/buildinplugin.xml和host/Android.mk两个文件来
host/asset/buildinplugin.xml中配置内容为：
com.mediatek.camera.feature.setting.CameraSwitcherEntry
而Android.mk文件配置为
LOCAL_SRC_FILES += (callall−java−files−under,../feature/setting/cameraswitcher/src)LOCALRESOURCEDIR:=(callall−java−files−under,../feature/setting/cameraswitcher/src)LOCALRESOURCEDIR:=(LOCAL_PATH)/res $(LOCAL_PATH)/../feature/setting/cameraswitcher/res
这样做的主要目的是为了更好地客制化试用ODM项目
```## TODO : rrzo size?

```text
TODO : rrzo 是什么意思？
camera hal 配置 rrzo size 规则
```## TODO : ISP ==== Image Sensor Processor / Image Signal Processor?有什么区别？

## CShot？

```text
CShot 是 Continuous Shot 的意思
```## TODO : FDR?

## TODO : SDR?

## TODO : 分段美颜

## TODO : V4L2

# 性能

## Android Camera性能分析

```text
https://blog.csdn.net/qq_42194101/category_11748030.html
```## Android Camera简单整理(四)-Android Camera性能Debug经验

```text
https://www.jianshu.com/p/c5b797848040
```## Camera Performance

```text
https://online.mediatek.com/Pages/eCourse.aspx?001=002&002=002002&003=002002004&itemId=373&csId=%7B433b9ec7-cc31-43c3-938c-6dfd42cf3b57%7D%40%7Bad907af8-9a88-484a-b020-ea10437dadf8%7D
```## Camera启动log分析

```text
https://www.cxyzjd.com/article/justXiaoSha/100550674

总结
对比第一次冷启动和热启动
第一次冷启动主要是多了CameraService的创建，
还有getSensorStaticinfo时，先去search所有的camera信息，保存起来，
后续再次打开Camera，直接从缓存读取信息，因此冷启动慢，热启动快。

其他的调用流程都是一致的！
```## 相机的冷启动

```text
相机的冷启动，可以分解如下几步：
1.AMS启动相机的Activity -> 相机的Activity收到onCreated消息 (可体现系统的性能)。
2.onCreate begin -> onCreate end(主要是ui的加载)
3.openCamera -> CameraOpened
4.TextureView add -> SurfaceTexture created (Surface的创建时间)
5.startPreview -> PreviewStarted
6.setWindow -> PreviewCallback

相机冷热启动优化
https://juejin.cn/post/6870353537226768398
```## Android GPU分析利器(GAPID)

```text
参考看到每个texture长什么样子,也就可以方便定位异常texture了.
参考:http://www.gcsjj.cn/articles/2019/06/04/1559658578252.html

下载地址 https://github.com/google/gapid/releases
```## simpleperf

```text
录制 simpleperf log
执行需要 root 权限.
执行这行指令, 可以录制 60 秒的 64bits 的 camerahalserver 在做啥
adb shell "simpleperf record -g -p `pidof camerahalserver` --duration 60 -o /sdcard/perf.data"
-p 指定监控 cameralhalserver, 並且记录在 /sdcard/perf.data 这个档案。
执行这行指令, 可以录制 60 秒的 32bits 的 camerahalserver 在做啥
adb shell "simpleperf32 record -g -p `pidof camerahalserver` --duration 60 -o /sdcard/perf.data"

adb pull /sdcard/perf.data 到电脑上。
```## 相机内存抖动

```text
https://www.jianshu.com/p/77a524265f3c
在startPreview之前，我们需要设置addCallbackBuffer 和 setPreviewCallbackWithBuffer，这两个方法必须同时使用才有效果，不能使用addCallbackBuffer 和 setPreviewCallback配合使用，这样同样没有效果。

mCamera.addCallbackBuffer(mPreviewBuffer);
mCamera.setPreviewCallbackWithBuffer(this);

应用程序可以分配一个或者多个缓存区到缓存队列，当预览的数据返回时，如果有缓存区，则使用该缓存区并把该缓存区从缓存队列移除，当预览的数据返回时没有缓存区，则会把该预览数据丢弃。

原来可以分配多个缓存区啊，那我之前内存仍然溢出会不会是因为分配的缓存不够导致数据被丢弃，但是内存没有被及时回收导致的呢?抱着尝试的态度我又给preview加了两个缓存，结果测试发现果然不再内存溢出了，优化后的代码如下：

camera.addCallbackBuffer(new byte[mWith * mHeight * 6]);

camera.addCallbackBuffer(buffer);
camera.addCallbackBuffer(buffer);
camera.addCallbackBuffer(buffer);
camera.setPreviewCallbackWithBuffer(new Camera.PreviewCallback() {
    @Override
    public void onPreviewFrame(byte[] bytes, Camera camera) {
        if (null == bytes) {
            camera.addCallbackBuffer(new byte[mWith * mHeight * 6]);
        } else {
            camera.addCallbackBuffer(bytes);
        }
    }
});
camera.startPreview();


cam.setPreviewDisplay(holder);
Camera.Parameters parameters = cam.getParameters();
//new
//3句全加，30fps
parameters.setRecordingHint(true);//去掉这句，12fps
//parameters.setAutoExposureLock(true);//去掉这句，30fps
//parameters.setAutoWhiteBalanceLock(true);//去掉这句，30fps

parameters.setFlashMode("off"); // 无闪光灯
parameters.setWhiteBalance(Camera.Parameters.WHITE_BALANCE_AUTO);
parameters.setSceneMode(Camera.Parameters.SCENE_MODE_AUTO);
parameters.setFocusMode(Camera.Parameters.FOCUS_MODE_AUTO);
parameters.setPreviewFormat(PreviewFromat_NV21);
// 这两个属性 如果这两个属性设置的和真实手机的不一样时，就会报错
parameters.setPictureSize(320, 240);
parameters.setPreviewSize(320, 240);
cam.setParameters(parameters);
```## [FAQ24846] 如何抓取Camera systrace(Since R)

```text
[DESCRIPTION]
在分析camera performance issues时，需要抓取systrace给到蔽司来定位问题。
由于平台有设置property来控制一些trace tag的使能，于是使用蔽司的工具才能抓到完整的systrace。
本文提供的工具及方法始于Android R版本，并兼容低版本。
[SOLUTION]
重要事项：
Performance问题需要使用user + root load来测试和抓systrace；
请使用蔽司提供的systrace_tool_since_R工具来抓systrace；
一. camera systrace since R抓取的工具
请到MOL tool搜索“Systrace_Tool_since_R”然后下载。
 
二. 环境配置
1. Python
从https://www.python.org/downloads/下载Python，版本必须为2.7
安装完成之后，请将six.py and six.pyc 从安装目录C:\Python27\Lib\site-packages\pip\_vendor 拷贝到C:\Python27\Lib. 
注：以上路径仅供参考，以具体安装路径为准。
 
2. pywin32
从https://github.com/mhammond/pywin32/releases下载。
32bit设备，请安装pywin32-XXX.win32-py2.7.exe
64bit设备，请安装pywin32-XXX.win-amd64-py2.7.exe。
 
三. camera systrace抓取的方法
1. 确保手机已经打开root调试且连接到PC；
2. 双击 systrace_setup.bat，界面如：
3. 双击systrace_capture.bat，界面如：
开始操作手机复现问题，该过程尽量在10s内完成，避免录的systrace过大。复现完成后，再点击ENTER键即可停止录制，界面如（要等到出现红框的字符才表示保存systrace完成，才可以关闭该窗口）：
4. 把生成的html文件提供给蔽司即可。
```## 抓取 camera systrace

```text
1.设置trace打开属性：
adb root && adb shell setprop persist.vendor.camera.traceGroupsEnable 65566 && adb shell getprop persist.vendor.camera.traceGroupsEnable  
adb reboot //provider进程重启生效
adb root && adb shell getprop persist.vendor.camera.traceGroupsEnable 
adb shell  setenforce 0 && adb shell  getenforce  //不关selinux可能provider node的systrace抓的不全

traceGroupsEnable的值与Camx日志group一样,一般按照上面65566基本就够了.
UMD group:
static const CamxLogGroup CamxLogGroupNone = (1 << 0); ///< Generic group
static const CamxLogGroup CamxLogGroupSensor = (1 << 1); ///< Sensor
static const CamxLogGroup CamxLogGroupIFace = (1 << 2); ///< IFace
static const CamxLogGroup CamxLogGroupISP = (1 << 3); ///< ISP
static const CamxLogGroup CamxLogGroupPProc = (1 << 4); ///< Post Processor
static const CamxLogGroup CamxLogGroupImgLib = (1 << 5); ///< Image Lib
static const CamxLogGroup CamxLogGroupCPP = (1 << 6); ///< CPP
static const CamxLogGroup CamxLogGroupHAL = (1 << 7); ///< HAL
static const CamxLogGroup CamxLogGroupJPEG = (1 << 8); ///< JPEG
static const CamxLogGroup CamxLogGroupStats = (1 << 9); ///< Stats
static const CamxLogGroup CamxLogGroupCSL = (1 << 10); ///< CSL
static const CamxLogGroup CamxLogGroupApp = (1 << 11); ///< Application
static const CamxLogGroup CamxLogGroupUtils = (1 << 12); ///< Utilities
static const CamxLogGroup CamxLogGroupSync = (1 << 13); ///< Sync
static const CamxLogGroup CamxLogGroupMemSpy = (1 << 14); ///< MemSpy
static const CamxLogGroup CamxLogGroupAssert = (1 << 15); ///< Asserts
static const CamxLogGroup CamxLogGroupCore = (1 << 16); ///< Core
static const CamxLogGroup CamxLogGroupHWL = (1 << 17); ///< HWL
static const CamxLogGroup CamxLogGroupChi = (1 << 18); ///< CHI
static const CamxLogGroup CamxLogGroupDRQ = (1 << 19); ///< DRQ
static const CamxLogGroup CamxLogGroupFD = (1 << 20); ///< FD
static const CamxLogGroup CamxLogGroupIQMod = (1 << 21); ///< IQ module
static const CamxLogGroup CamxLogGroupLRME = (1 << 22); ///< LRME
static const CamxLogGroup CamxLogGroupNCS = (1 << 23); ///< NCS
static const CamxLogGroup CamxLogGroupMeta = (1 << 24); ///< Metadata
static const CamxLogGroup CamxLogGroupAEC = (1 << 25); ///< AEC
static const CamxLogGroup CamxLogGroupAWB = (1 << 26); ///< AWB
static const CamxLogGroup CamxLogGroupAF = (1 << 27); ///< AF

2.抓取
python ~/Android/Sdk/platform-tools/systrace/systrace.py -o camera_qidong.html sched freq camera hal  
如果抓取到的trace时间较短，可以 -b 设大缓存，
python ~/Android/Sdk/platform-tools/systrace/systrace.py -b 30726 -o camera_qidong7.html sched freq camera hal
或者 -t ，如下可以抓到4s左右
python ~/Android/Sdk/platform-tools/systrace/systrace.py -t 4 -o camera_qidong7.html sched freq camera hal gfx input view wm am app dalvik sched freq idle load -a com.android.camera
```## perfetto

```text
1、首先查看手机是否已经打开类perfetto的后台进程
adb logcat -s perfetto
perfetto: service.cc:45 Started traced, listening on /dev/socket/traced_producer /dev/socket/traced_consumer
perfetto: probes.cc:25 Starting /system/bin/traced_probes service
perfetto: probes_producer.cc:32 Connected to the service

2、去Perfetto的UI网址（https://ui.perfetto.dev/#!/record）上定制相关的使用命令

3、等到抓取的长度或者时间达到你第2步设置的值后，会自动退出抓取程序，此时将手机 data/local/traces 文件夹下面的trace文件adb pull到电脑端

4、同样在https://ui.perfetto.dev/#!/record网址上通过Open trace File选项打开本地存储的trace文件即可查看相关信息,可以看到时长1min半打开无压力,用于复现视频偶先丢帧很棒啊!

adb shell am start com.android.traceur/com.android.traceur.MainActivity
```## SimplePerf，火焰图

```text
参考:https://zhuanlan.zhihu.com/p/25277481
https://android.googlesource.com/platform/prebuilts/simpleperf/
https://developer.android.com/ndk/guides/simpleperf?hl=zh-cn
http://www.brendangregg.com/flamegraphs.html
https://github.com/brendangregg/FlameGraph

代码路径：/system/extras/simpleperf/
脚本路径：/system/extras/simpleperf/scripts
手机设备的默认路径 ：/system/bin/simpleperf

Simpleperf是谷歌将perf工具port到Android上的性能分析工具，它的命令行界面支持与linux-tools perf大致相同的选项，但是它还支持许多Android特有的改进。具有三个主要的功能：stat，record 和 report。

抓取方法
在pc端：
快速方式：
python /home/sun/work/code/j6a1-curtana/system/extras/simpleperf/scripts/run_simpleperf_on_device.py kmem record --call-graph fp -f 4000 --duration 10 -o /data/local/tmp/perf.data

完整方式：
python /home/sun/work/code/j6a1-curtana/system/extras/simpleperf/scripts/run_simpleperf_on_device.py kmem record --call-graph fp -f 4000 --duration 10 --symfs ~/work/image/curtana_in_global_symbols_20.3.13.root_10.0_96fc05f913_gdcdaf60/out/target/product/curtana/symbols/ -o /data/local/tmp/perf.data
python /home/sun/work/code/j6a1-curtana/system/extras/simpleperf/scripts/run_simpleperf_on_device.py kmem record -p pid -e kmem:kmalloc,kmem:kmem_cache_alloc --call-graph fp -f 4000 --duration 10 -o /data/local/tmp/perf.data
adb pull /data/local/tmp/perf.data ./

或者在手机端：
快速方式：
simpleperf kmem record --call-graph fp -f 4000 --duration 10 -o /data/local/tmp/perf_2.data
完整方式：
simpleperf kmem record -p pid -e kmem:kmalloc,kmem:kmem_cache_alloc --call-graph fp -f 4000 --duration 10 -o /data/local/tmp/perf_2.data

解析生成火焰图：

python /home/sun/work/code/j6a1-curtana/system/extras/simpleperf/scripts/report_html.py -i ./perf.data -o ./perf.html
或者
python /home/sun/work/code/j6a1-curtana/system/extras/simpleperf/scripts/report_sample.py --symfs ~/work/image/curtana_in_global_symbols_20.3.13.root_10.0_96fc05f913_gdcdaf60/out/target/product/curtana/symbols/  -i perf.data > out.perf

git clone https://github.com/brendangregg/FlameGraph.git
FlameGraph/stackcollapse-perf.pl out.perf > out.folded
FlameGraph/flamegraph.pl out.folded > graph.svg
解析完成后的perf.html或者graph.svg直接用谷歌浏览器打开，如下：

建议用report_html.py生成的perf.html，会有更直观的统计信息

y 轴表示调用栈，每一层都是一个函数。调用栈越深，火焰就越高，顶部就是正在执行的函数，下方都是它的父函数。
x 轴表示抽样数，如果一个函数在 x 轴占据的宽度越宽，就表示它被抽到的次数多，即执行的时间长。注意，x 轴不代表时间，而是所有的调用栈合并后，按字母顺序排列的。

火焰图就是看顶层的哪个函数占据的宽度最大。只要有"平顶"（plateaus），就表示该函数可能存在性能问题。
颜色没有特殊含义，因为火焰图表示的是 CPU 的繁忙程度，所以一般选择暖色调。
```## Android studio profile

```text
Android studio中的profile功能可以跟进app进程内存变化情况及细节,以及CPU占用情况,但看相机应用内存变化趋势是可以的了,然后在高位时dump需要的信息继续debug吧,==
参考:
Android studio中android profile（性能分析器）的使用
Android Studio使用profile简单优雅的查看内存变化
```## [FAQ21709]Camera HAL3 内存优化

```text
内存用量大头（Graphics部分）分解：adb shell cat /sys/kernel/debug/ion/ion_mm_heap > ion_1
查看优化效果，对比优化前后meminfo中的total即可.
那么会有哪些省内存办法呢?请看下文.

1.拍照后buffer立即释放
优点：拍照过程中产生的buffer使用完毕后即释放，不影响拍照后的内存用量；
缺点：内存存量不高的情况下，拍照速度会受影响;
优化量：与拍照实际feature有关，拍照feature越多占用内存越大，优化量越大;

/vendor/mediatek/proprietary/hardware/mtkcam3/feature/core/featurePipe/capture/buffer/CaptureBufferPool.cpp

mpTuningBufferPool->setAutoFree(0); //拍照后release tuning buffer
pImagePool->setAutoFree(0);//拍照后release image buffer

【重要提醒】如果使用此优化，务必保证YUVNode.cpp中有如下修改，如无，请申请patch ALPS04338041.
mtkcam3\feature\core\featurePipe\capture\nodes\YUVNode.cpp

1090:     pPlgRequest->mIBufferFull  = (iBufferFullHandle == NULL) ? PluginHelper::CreateBuffer(pNodeReq, TID_MAN_FULL_YUV, INPUT) : std::move(iBufferFullHandle);

1091:     pPlgRequest->mIBufferClean = PluginHelper::CreateBuffer(pNodeReq, TID_MAN_FULL_PURE_YUV, INPUT);

1092:     pPlgRequest->mIBufferDepth = PluginHelper::CreateBuffer(pNodeReq, TID_MAN_DEPTH, INPUT);

1093:     pPlgRequest->mOBufferFull  = (oBufferFullHandle == NULL) ? PluginHelper::CreateBuffer(pNodeReq, TID_MAN_FULL_YUV, OUTPUT) : std::move(oBufferFullHandle);
 
2.减少ZSL buffer number
优点：优化整个camera使用期间的内存用量
缺点：如果设定值过小，重载时会影响preview帧率.
优化量：实际减少的buffer数据有关，也与sensor大小有关.

/vendor/mediatek/proprietary/hardware/mtkcam3/pipeline/model/zsl/hbc/HistoryBufferContainerImp.cpp

mMaxBufNum = (pInfo->getMaxBufNum()>mMaxBufNum)? pInfo->getMaxBufNum() : mMaxBufNum;//此值即是
基于MAX_HISTORY_DEPTH 和app设定的streaminfo信息

3.修改P1Node buffer格式（需满足条件）
使用条件：Raw格式在一次configure后不会发生改变. 举例，4-cell功能以及Raw HDR功能均会在使用期间切换Raw格式.则不可使用此优化;
优点：P1Node输出buffer格式由BloB改为Bayer10;
缺点:无法实时做格式转换;
优化量：与sensor实际大小有关.

/vendor/mediatek/proprietary/hardware/mtkcam3/pipeline/policy/config/P1HwSettingPolicy.cpp

bool isLowMem = ::property_get_bool("ro.config.low_ram", false); //强制将isLowMem置为True.

如果平台支持UFO，也可使用UFO格式，P1输出可以有多种格式，格式选择的逻辑判断均在P1HwSettingPolicy.cpp中，而各值的对应列表可查阅：
/vendor/mediatek/proprietary/hardware/mtkcam/include/mtkcam/def/ImageFormat.h

4.提高MFNR的门限，尽量避免使用MFNR，减少mfnr张数
优点：极大的改善内存以及cpu 资源的消耗，提升拍照速度，提升系统流畅度；
缺点：高光感下的图像噪点略高，影响图片质量，有些可以通过tuning 其他nr参数弥补回来;

/vendor/mediatek/proprietary/custom/mtXXXX/hal/inc/camera_custom_nvram.h

MUINT16 mfll_iso_th // tunning 参数 各家不同 ，默认800;
MUINT8 capture_frame_number; //mfnr张数，最低3张，默认4张;

对应的参数tunning的同事会较清楚，或者在/vendor/mediatek/proprietary/custom/mtxxxx/hal/imgsensor/ver1/sensorname 下全搜mfll_iso_th即可.
 
5.关闭ZSL
优点：拍照的buffer不再受preview处理效率的影响，同时节省buffer;
缺点：与Hal1上关闭zsd不同的是，关闭zsl仅拍照瞬间画面略有停顿.而Hal1上关闭zsd是整个拍照未完成期间均停顿.
优化量：节省zsl buffer pool的大小，一般会达到100M以上.

Control.capture.default.zsl.mode 设为off
Control.capture.zsl.mode configure和request时，均需设定为off，否则会出现re-configuresesion的问题，影响启动时间;
 
6.拍照相关限制
原理：限制同时在hal层处理的capture 数目，变相的优化内存峰峰值.
缺点：对内存存量要求高，则容易影响shot2shot的实际效果.

Shot2shot：

/vendor/mediatek/proprietary/hardware/mtkcam3/pipeline/model/capture/

#define MIN_FREE_MEM (300000000) // 300M，只有内存可用量大于300M时，才会告知app可以拍下一张.

最大request size：

maxAppJpegStreamNum //变相限制max request size
 
以上是通用法则.还有些可能会用得上的优化点：

8.streaming场景的优化

a)确认P1Node输出的size，等于preview size值. 如若不是，请查看P1Node输出的size来源.逻辑判断来源
/vendor/mediatek/proprietary/hardware/mtkcam3/pipeline/policy/config/P1HwSettingPolicy.cpp

需要注意的是：P1Node输出size大于preview size有助于减轻锯齿问题，客户需自行斟酌是否优化此项;

b )确认streaming的三方算法要求的size<=preview size. 三方算法所需size可通过下述API设定：

if( mUseSize ) sel.mIBufferMain1.setSpecifiedSize(mSize)

此修改，除了可优化内存外，同样可提升三方算法处理效率，但是需要看三方是否都支持；

总的来说，内存相关的优化，与手机状态强相关，所有的参数均需实验后方可得出，即使同一个hw，但不同的OS系统，不同的feature，都无法使用同一套优化参数，以上仅仅是提供优化思路与相关参数，具体的数值，请大家多多实验，在性能与内存之前找到项目的平衡点，做到最优.
 
Good Luck！
```# 调试

## 模块编译 metadata

```text
If modify middleware related metadata:
1. partial build vendor\mediatek\proprietary\hardware\mtkcam\utils\metastore => libmtkcam_metastore.so
2. Push so file
3. Kill camerahalserver & cameraserver

If modify 3A & sensor related metadata:
1. partial build /vendor/mediatek/proprietary/hardware/mtkcam/drv/src/sensor/mt6771/ =>  libcam.halsensor.so
2. Push so file
3. Kill camerahalserver & cameraserver

If modify template request metadata:
1. partial build vendor\mediatek\proprietary\hardware\mtkcam\utils\metastore => libmtkcam.metastore.so
2. Push so file
3. Kill camerahalserver & cameraserver

MTK Android R
nn libmtkcam_metastore
```## 录像大概流程

```text
录像的整个流程过程如下：
Line 164803: M024D6B 01-04 10:10:27.982 5833 5833 I CAM_VideoModule: onShutterButtonClick   --点击录像键
Line 164805: M024D6D 01-04 10:10:27.986 5833 5833 I CAM_VideoModule: startVideoRecording: Thread[main,5,main] --开始录像
Line 165081: M024E81 01-04 10:10:28.329 5833 6106 V CAM_VideoModule: New video filename: /storage/emulated/0/DCIM/Camera/VID_20220104_101028.mp4 --创建录像文件
Line 170818: M0264D0 01-04 10:10:33.492 5833 5833 I CAM_VideoModule: Video snapshot start   --录像过程中点击拍照键，开始拍照
Line 171433: M026737 01-04 10:10:34.157 5833 7869 I CAM_VideoModule: Video snapshot taken.  --录像过程中拍照结束
Line 171473: M02675F 01-04 10:10:34.209 5833 7869 I CAM_VideoModule: storeImage end!        --照片存储
Line 185466: M029D2C 01-04 10:10:46.984 5833 5833 I CAM_VideoModule: onShutterButtonClick   --再次点击录像键(关闭录像)
Line 185466: M029D2D 01-04 10:10:46.985 5833 5833 I CAM_VideoModule: stopVideoRecording     --停止录像

排查错误的时候
(1)可以先搜 log "startVideoRecording|Video snapshot start|Video snapshot taken|stopVideoRecording"找到录像过程的开始和结尾行，将此过程的log全部复制出来。
(2)再复制出来的log基础上，搜log "Cam3HWI|cmr_grab|cmr_oem|Cam3OEMIF|cmr_snp|CAM2A|CAM_VideoModule"
以上log是排查是否是hal层的问题，重点关注Cam3OEMIF log中的参数设置
(3)如果搜索到“Skip stopVideoRecording since snapshot in progress”等信息，可以先让app同事看下，注:此错误log信息只有在录像过程中拍照出现。
```## DreamCamera2关键LOG梳理

```text
为了便于客户问题分析，本文将对常见的APP及相关LOG进行梳理。主要分为打开、关闭相机，起预览、拍照、录像等。本文将根据流程先后顺序进行梳理，对主要LOG进行说明。

1. 打开相机
//启动相机
S311E15 02-08 20:59:13.774 1077 1770 I ActivityTaskManager: START u0 {act=android.intent.action.MAIN cat=[android.intent.category.LAUNCHER] flg=0x10200000 cmp=com.android.camera2/com.android.camera.CameraLauncher bnds=[540,912][789,1239]} from uid 10167, pid 1850

//APP 打开相机
M311F11 02-08 20:59:13.876 15880 15880 I CAM_CameraController: checkAndOpenCamera
M311F13 02-08 20:59:13.879 15880 19215 I CAM2PORT_AndCam2AgntImp: AppFW handleMessage - action = 'OPEN_CAMERA'

2. 启动预览
//APP 启动预览结束
M312205 02-08 20:59:14.123 15880 15880 I CAM_PhotoModule: startPreview end!

// 下发起预览命令
M312292 02-08 20:59:14.157 15880 19215 I CAM2PORT_AndCam2AgntImp: AppFW handleMessage - action = 'START_PREVIEW_ASYNC'

3. 点击拍照
// 点击拍照按钮
M318482 02-08 20:59:23.077 15880 15880 I CAM_PhotoModule: onShutterButtonClick mPaused:false,mCameraState:1 isShutterEnabled=true mCaptureCount = 0

// 下发拍照命令
M3184EE 02-08 20:59:23.087 15880 19215 I CAM2PORT_AndCam2AgntImp: AppFW handleMessage - action = 'CAPTURE_PHOTO'

//拍照返回
M318C50 02-08 20:59:23.455 15880 19215 I CAM2PORT_AndCam2AgntImp: AppFw takePicture onImageAvailable

// 保存照片
M318D19 02-08 20:59:23.501 15880 15880 I CAM_PhotoModule: saveFinalPhoto start!

//完成保存
M319006 02-08 20:59:23.618 15880 15880 I CAM_PhotoModule: onMediaSaved uri = content://media/external/images/media/125 , title = IMG_20220208_205923

4. 切换到录像模式
// 模式切换
M31AA54 02-08 20:59:26.031 15880 15880 I CAM_CameraActivity Drea: onModeSelected mCurrentModeIndex=0,change to 9

// 冻屏模糊
M31A826 02-08 20:59:25.832 15880 15880 I CAM_CameraActivity Drea: dealModeFreeze start

// 开始录像
M31C2E8 02-08 20:59:28.521 15880 15880 I CAM_VideoModule: startVideoRecording: Thread[main,5,main]

// 结束录像
M323E65 02-08 20:59:38.730 15880 15880 I CAM_VideoModule: stopVideoRecording

5. 关闭相机
// 停止预览
M32C47F 02-08 20:59:54.880 15880 15880 V CAM_VideoModule: stopPreview

// 下发停止预览命令
M32C489 02-08 20:59:54.882 15880 19215 I CAM2PORT_AndCam2AgntImp: AppFW handleMessage - action = 'STOP_PREVIEW'

// 关闭相机
M32C5BA 02-08 20:59:54.958 15880 15880 I CAM_VideoModule: closeCamera

// 下发关闭相机命令
M32C98F 02-08 20:59:55.262 15880 19215 I CAM2PORT_AndCam2AgntImp: AppFW handleMessage - action = 'RELEASE'
```## MTK相机调试adb命令

```text
AE 开启log
adb shell setprop vendor.debug.ae.enable 9
adb shell setprop vendor.debug.drv.ccu_drv 6
adb shell setprop vendor.debug.ccuif.ccu_drv 6
adb shell setprop vendor.debug.aaa.pvlog.enable 1
adb shell setprop vendor.debug.camera.log.hal3a 1
adb shell setprop vendor.debug.mapping_mgr.enable 1
adb shell setprop debug.cam.drawid 1
adb shell setprop debug.lce.core.enable 1
adb shell setprop vendor.debug.lce.face.log.enable 1
adb shell setprop vendor.debug.dynamic_ggm.log 1
adb shell setprop vendor.debug.dynamic_lce.log 1
adb shell setprop vendor.persist.logmuch.detect false
adb shell setprop vendor.debug.ae_mgr.enable 1
adb shell setprop vendor.debug.ae.plineinfo 1
adb shell setprop vendor.drv.ccu.log.ccuaealgo 1
adb shell setprop vendor.drv.ccu.log.ccuflowae 1
adb shell setprop vendor.drv.ccu.log.reserve1 1

Dual AE log
adb shell setprop vendor.persist.logmuch.detect false
adb shell setprop vendor.debug.aaa.pvlog.enable 1
adb shell setprop vendor.debug.ae.plineinfo 1

adb shell setprop vendor.debug.drv.ccu_drv 6
adb shell setprop vendor.debug.ccuif.ccu_drv 6
adb shell setprop vendor.debug.camera.log 1

adb shell setprop vendor.debug.ae.enable 9
adb shell setprop vendor.debug.ae_mgr.enable 1

锁定AE
adb shell setprop vendor.debug.ae_mgr.enable 1
adb shell setprop vendor.debug.ae_mgr.lock 1
adb shell setprop vendor.debug.ae_mgr_ccu.enable 0

手动设定AE
adb shell setprop vendor.ae_mgr.enable 1
adb shell setprop vendor.ae_mgr.lock 1
adb shell setprop vendor.ae_mgr.preview.update 1
adb shell setprop vendor.ae_mgr_ccu.enable 0
adb shell setprop vendor.ae_mgr.shutter 80000
adb shell setprop vendor.ae_mgr.sensorgain 2048
adb shell setprop vendor.ae_mgr.ispgain 1024
adb shell setprop vendor.ae_mgr.preview.update 1

5G平台
adb shell setprop vendor.debug.ae_mgr.ISOspeed 100

AWB 开启log
adb shell setprop vendor.debug.awb_mgr.enable 1
adb shell setprop vendor.debug.awb.enable 1
adb shell setprop vendor.debug.awb_log.enable 1

锁定AWB
adb shell setprop vendor.debug.awb_mgr.enable 1
adb shell setprop vendor.debug.awb_mgr.lock 1

AF 开启log
adb shell setenforce 0
adb shell setprop vendor.debug.af_mgr.enable 4
adb shell setprop vendor.debug.af.enable 1
adb shell setprop vendor.debug.af.log.enable 1
adb shell setprop vendor.debug.pd.enable 1
adb shell setprop debug.cam.drawid 1
adb shell setprop vendor.debug.camera.dbginfo 1
adb shell setprop vendor.debug.pd.vpu.log.enable 1

手动设定AF
adb shell setprop vendor.debug.af_motor.disable 1
adb shell setprop vendor.debug.af_motor.position 200

关闭pdaf命令
adb shell setprop vendor.debug.pdflow.disable 1

6873 FullScan，进相机，touch AF 是 Full scan
adb shell setprop vendor.debug.af.enable 1
adb shell setprop vendor.debug.af.localfullscan 3
adb shell setprop vendor.debug.af.fullscan.step 1

TSF
关闭TSF
adb shell setprop vendor.debug.lsc_mgr.manual_tsf 0
adb shell setprop vendor.debug.lsc_mgr.ratio 32

关闭LSC
adb shell setprop vendor.debug.lsc_mgr.enable 0

ISP 开启log
adb root
adb shell setenforce 0
adb shell setprop persist.vendor.mtk.camera.log_level 3
adb shell setprop vendor.debug.aaa.pvlog.enable 1
adb shell setprop vendor.debug.camera.log 1
adb shell setprop debug.camera.log 1
adb shell setprop vendor.debug.camera.log 1
adb shell setprop vendor.debug.hal3av3.log 263
adb shell setprop debug.camera.log.hal3a 3
adb shell setprop vendor.debug.3a.log 1
adb shell setprop debug.camera.log 3
adb shell setprop debug.hal3a.task 1
adb shell setprop vendor.debug.hal3a.taskmgr 1
adb shell setprop vendor.debug.paramctrl.enable 1
adb shell setprop vendor.debug.isp_debug.enable 1
adb shell setprop vendor.debug.isp_tuning_mgr.enable 499
adb shell setprop vendor.debug.aaa.perframe_prop.enable 1
adb shell setprop vendor.debug.isp_mgr.enable 1
adb shell setprop vendor.debug.mapping_mgr.enable 3
adb shell setprop debug.idxcache.log 1
adb shell setprop vendor.debug.camera.log.p1node 2
adb shell pkill camer*

关闭ISP参数
adb shell setprop vendor.isp.lce.disable 1

adb shell setprop vendor.isp.ccm_r1.disable 1
adb shell setprop vendor.isp.ccm_d1.disable 1

Hal3a 开启log
adb root
adb shell setenforce 0
adb shell setprop persist.vendor.mtk.camera.log_level 3
adb shell setprop vendor.debug.camera.log 1
adb shell setprop vendor.debug.hal3av3.log 511
adb shell setprop vendor.debug.3a.log 1
adb shell setprop vendor.debug.resultpool.log 1
adb shell setprop vendor.debug.statistic_buf.enable 1
adb shell setprop vendor.debug.thread_raw.log 1
adb shell setprop vendor.debug.idxcache.log 1
adb shell setprop vendor.debug.hal3a.taskmgr 1
adb shell setprop vendor.debug.aao_mgr.enable 1
adb shell setprop vendor.debug.aaa.pvlog.enable 1
adb shell pkill camera*

Flashlight 校准
Android P 校正闪光灯命令:
adb shell setprop vendor.flash_calibration 1
adb shell setprop vendor.flash_quick_calibration_2 1

User版本
user版本开启root权限（待验证）
adb shell setprop service.adb.root 1

user版本打开camera LOGD命令：
adb root
adb shell setprop persist.vendor.mtk.camera.log_level 3
adb shell pkill camera*

APP相关
看APK包名
adb shell dumpsys window

meta dump数据
adb shell dumpsys media.camera -v 2 > meta.info.txt
adb shell cat /proc/driver/camera_info >info.txt

开启mobilelog
adb shell am start -n com.mediatek.mtklogger/com.mediatek.mtklogger.MainActivity

开启debuglogger
adb shell am start -n com.debug.loggerui/.MainActivity

开启EngineerMode
adb shell am start -n com.mediatek.engineermode/.EngineerMode

切换摄像头
adb shell pkill camera*
adb shell setprop mtk.camera.app.keycode.enable 1
adb shell setprop mtk.camera.switch.camera.debug 1
adb shell setprop mtk.camera.switch.id.debug back-1
adb shell am start -a android.media.action.STILL_IMAGE_CAMERA
adb shell input keyevent KEYCODE_C

Vertical blanking计算方式：
(framelength - grabwindow_height) *33ms /framelength > 1ms

CTS测试命令
sudo PATH="$PATH" ./cts-tradefed

run cts -m CtsCameraTestCases -t android.hardware.camera2.cts.MultiViewTest#testDualCameraPreview -s s670jkppppppppppp01 -a arm64-v8a --skip-preconditions
run cts -m CtsAppTestCases -t android.app.cts.SystemFeaturesTest#testCameraFeatures -a arm64-v8a --skip-preconditions

解锁
Android P + kernel-4.9 or after
download preloader with verified boot disabled which location is the same as scatter file. preloader__SBOOT_DIS.bin

boot to Home Screen
go to setting -> system -> Developer options -> OEM unlocking
adb reboot bootloader
fastboot flashing unlock
press volume up key
fastboot reboot
adb root
adb disable-verity
adb reboot
adb root
adb remount
Dump Raw
P70 & before
adb root
adb shell setenforce 0
adb shell setprop persist.vendor.dp.dumpreg.check 1
adb shell setprop vendor.dp.dumpreg.enable 2
adb shell setprop vendor.debug.hal3av3.forcedump 1
adb shell setprop vendor.debug.aaa.perframe_prop.enable 1
adb shell setprop vendor.debug.camera.dump.p2.debuginfo 1
adb shell setprop vendor.debug.camera.copy.p1.lsc 1
adb shell setprop vendor.debug.camera.dump.lsc2 1
adb shell setprop vendor.debug.camera.SttBufQ.enable 60
adb shell setprop vendor.debug.camera.AAO.dump 1
adb shell setprop vendor.debug.camera.img3o.dump 0
adb shell setprop vendor.debug.camera.ufo_off 1
adb shell setprop vendor.debug.camera.p2.dump 1
adb shell setprop vendor.debug.camera.dump.JpegNode 1
adb shell setprop vendor.debug.camera.haljpeg 1
adb shell setprop vendor.debug.camera.dbginfo 1
adb shell setprop vendor.debug.camera.cfg.ProcRaw 1
adb shell setprop vendor.debug.camera.raw.type 1

P70 Q
adb root
adb shell setenforce 0
adb shell setprop persist.vendor.dp.dumpreg.check 1
adb shell setprop persist.vendor.dp.dumpreg.check 1
adb shell setprop vendor.dp.dumpreg.enable 2
adb shell setprop vendor.debug.hal3av3.forcedump 1
adb shell setprop vendor.debug.aaa.perframe_prop.enable 1
adb shell setprop vendor.debug.camera.dump.p2.debuginfo 1
adb shell setprop vendor.debug.camera.copy.p1.lsc 1
adb shell setprop vendor.debug.camera.dump.lsc2 1
adb shell setprop vendor.debug.camera.SttBufQ.enable 6
adb shell setprop vendor.debug.camera.AAO.dump 1
adb shell setprop vendor.debug.camera.img3o.dump 0
adb shell setprop vendor.debug.camera.ufo_off 1
adb shell setprop vendor.debug.camera.p2.dump 1
adb shell setprop vendor.debug.camera.dump.JpegNode 1
adb shell setprop vendor.debug.camera.haljpeg 1
adb shell setprop vendor.debug.camera.dbginfo 1
adb shell setprop vendor.debug.camera.cfg.ProcRaw 1
adb shell setprop vendor.debug.camera.raw.type 1
adb shell setprop vendor.debug.camera.dump.campipe 1
adb shell setprop vendor.debug.camera.mfnr.yuv.dump 1
adb shell setprop vendor.debug.camera.bss.dump 1

P90
adb root
adb shell setenforce 0
adb shell mkdir -p /data/vendor/camera_dump
adb shell setprop vendor.debug.camera.SttBufQ.enable 60
adb shell setprop persist.vendor.dp.dumpreg.check 1
adb shell setprop vendor.isp.faceinfo.dump 1
adb shell setprop vendor.debug.camera.ufo_off 1
adb shell setprop vendor.debug.camera.p2.dump 1
adb shell setprop vendor.debug.camera.p2.dump.filter 3
adb shell setprop vendor.debug.camera.dump.JpegNode 1
adb shell setprop vendor.debug.camera.copy.p1.lsc 1
adb shell setprop vendor.debug.hal3av3.forcedump 1
adb shell setprop vendor.debug.camera.dump.p2.debuginfo 1
adb shell setprop mediatek.mfll.dump.raw 1
adb shell setprop vendor.dp.dumpreg.enable 2
adb shell setprop vendor.isp.ynr_tbl.dump 1
adb shell setprop vendor.debug.camera.dump.lsc2 1
adb shell setprop vendor.debug.camera.dump.cap.tsfo 1
adb shell setprop vendor.debug.camera.AAO.dump 1
adb shell setprop vendor.debug.camera.bss.dump 1
adb shell setprop vendor.isp.dce_tbl.dump 1
adb shell setprop vendor.isp.ltm_tbl.dump 1
adb shell setprop vendor.debug.camera.dbginfo 1
adb shell setprop vendor.debug.camera.threshold_4Cell 99

5G
adb root
adb shell setenforce 0
adb shell mkdir -p /data/vendor/camera_dump
adb shell setprop vendor.debug.p2s.dsdn.mode 0
adb shell mrdump_tool output-set none
adb shell setprop vendor.mfll.force 1
adb shell setprop vendor.mfll.log_level 3
adb shell “kill $(pidof cameraserver)”
adb shell “kill $(pidof camerahalserver)”
adb shell setprop vendor.mfll.dump.sim 1
adb shell setprop vendor.mfll.dump.mixer.out 1
adb shell setprop vendor.debug.camera.p2.dump 1
adb shell setprop vendor.debug.camera.img3o.dump 1
adb shell setprop vendor.debug.camera.dump.JpegNode 1
adb shell setprop persist.vendor.dp.dumpreg.check 1
adb shell setprop vendor.debug.camera.SttBufQ.enable 60
adb shell setprop vendor.debug.camera.ufo_off 1
adb shell setprop vendor.debug.camera.p2.dump 1
adb shell setprop vendor.debug.camera.dump.campipe 1
adb shell setprop vendor.debug.camera.dump.p2 1
adb shell setprop vendor.debug.camera.dump.p2.ext.img3o 1
adb shell setprop vendor.debug.camera.img3o.dump 1
adb shell setprop vendor.debug.camera.copy.p1.lsc 1
adb shell setprop vendor.debug.hal3av3.forcedump 1
adb shell setprop vendor.debug.aaa.perframe_prop.enable 1
adb shell setprop mtk.camera.app.keycode.enable 1
adb shell setprop vendor.dp.dumpreg.enable 2
adb shell setprop vendor.debug.camera.dump.p2.debuginfo 1
adb shell setprop vendor.debug.camera.dump.lsc2 1
adb shell setprop vendor.debug.camera.AAO.dump 1
adb shell setprop vendor.flash_bin_en 1
adb shell setprop vendor.flash_pf_bmp_en 1
adb shell setprop vendor.flash_dump.enable 1
adb shell setprop vendor.isp.ynr_tbl.dump 1
adb shell setprop vendor.isp.ltm_tbl.dump 1
adb shell setprop vendor.isp.dce_tbl.dump 1
adb shell setprop vendor.isp.faceinfo.dump 1
adb shell setprop vendor.isp.ynr_map.dump 1
adb shell setprop vendor.debug.camera.msnr.ndd.l1 1
adb shell setprop vendor.debug.camera.msnr.ndd.l2 1
adb shell setprop vendor.debug.camera.bss.dump 1
adb shell setprop vendor.isp.lcesho_tbl.dump 1
adb shell setprop vendor.mfll.dump.mixer 1
adb shell setprop vendor.debug.camera.dump.p2 1
adb shell setprop vendor.debug.isp.dumpcq.enable 1
adb shell setprop vendor.imgsys.bittruedump.enable 2
adb shell setprop vendor.debug.camera.dump.mfb.tuning 1
adb shell setprop vendor.debug.camera.dump.mss.tuning 1
adb shell setprop vendor.msf.debug.bittruedump.enable 1
adb shell setprop vendor.mss.debug.bittruedump.enable 1
adb shell setprop vendor.debug.camera.dump.swmsf 1
adb shell setprop vendor.debug.camera.dump.msyuv 1
adb shell setprop vendor.debug.camera.dump.mfbtbl 1
adb shell setprop vendor.debug.camera.dbginfo 1
adb shell “kill $(pidof camerahalserver)”
adb shell “kill $(pidof cameraserver)”
adb shell pkill camera*
```## [FAQ20319] vsdof各个node dump buffer大全

```text
[DESCRIPTION]
vsdof各个node dump buffer大全
 
[SOLUTION] 
:::::::::::::::: Pass1 Raw, (including main1 IMGO, RRZO main2 RRZO)
adb shell setprop depthmap.pipe.dump.size 5
adb shell setprop depthmap.pipe.dump.start 0
adb shell setprop P2AFM 1
adb shell setprop P2AFM.TO_DUMP_RAWS 1

::::::::::::::::   P2ABAYER section  ::::::::::::::::
adb shell setprop P2ABayer 1
adb shell setprop P2ABayer.P2A_OUT_MV_F 1
adb shell setprop P2ABayer.P2A_OUT_FD 1
adb shell setprop P2ABayer.P2A_OUT_MV_F_CAP 1
adb shell setprop P2ABayer.P2A_TO_FD_IMG 1
adb shell setprop P2ABayer.P2A_TO_OCC_MY_S 1
adb shell setprop P2ABayer.P2A_OUT_DMBG 1
adb shell setprop P2ABayer.P2A_TO_GF_DMW_MYS 1
adb shell setprop P2ABayer.P2A_OUT_YUV_DONE 1

::::::::::::::::   N3D section  ::::::::::::::::
adb shell setprop N3DNode 1
adb shell setprop N3DNode.N3D_TO_DPE_MVSV_MASK 1
adb shell setprop N3DNode.N3D_TO_OCC_LDC 1
adb shell setprop N3DNode.N3D_TO_FD_EXTDATA_MASK 1
adb shell setprop N3DNode.N3D_OUT_JPS_WARPMTX 1

::::::::::::::::   DPE section  ::::::::::::::::
adb shell setprop DPENode 1
adb shell setprop DPENode.DPE_TO_OCC_MVSV_DMP_CFM 1
adb shell setprop DPENode.DPE_OUT_DISPARITY 1

::::::::::::::::   OCC section  ::::::::::::::::
adb shell setprop OCCNode 1
adb shell setprop OCCNode.OCC_TO_WMF_DMH_MY_S 1
adb shell setprop OCCNode.OCC_TO_WMF_OMYSN 1

::::::::::::::::   WMF section  ::::::::::::::::
adb shell setprop WMFNode 1
adb shell setprop WMFNode.WMF_TO_GF_DMW_MY_S 1
adb shell setprop WMFNode.QUEUED_FLOW_DONE 1
adb shell setprop WMFNode.WMF_TO_GF_OND 1

::::::::::::::::   StereoFD section  ::::::::::::::::
adb shell setprop SFDNode 1
adb shell setprop SFDNode.FD_OUT_EXTRADATA 1

::::::::::::::::   GF section  ::::::::::::::::
adb shell setprop GFNode 1
adb shell setprop GFNode.GF_OUT_DMBG 1
adb shell setprop GFNode.GF_OUT_DEPTHMAP 1
adb shell setprop GFNode.GF_OUT_DEPTH_WRAPPER 1

::::::::::::::::   others section  ::::::::::::::::
adb shell setprop debug.stereo.dumpcapturedata 1
adb shell setprop debug.STEREO.dump_n3d_capture 1
```## Android 8，Android10中，如何dump DreamCamera2预览的YUV图？

```text
1.问题背景
在处理预览方向错误（旋转90度或180度灯）的问题中，为了判断底层出图方向是否正确，常常需要用adb命令 dump YUV图，本文旨在回答android 8和android 10中如何dump camera 底层的yuv图，方便客户学习此方法，提高解决问题效率。
dumpyuv图的指令在oem层的文件cmr_preview.c中定义，android 9，android11中dump YUV 图的指令也可以通过cmr_preview.c找到
android10中cmr_preview.c参考路径： 
vendor/sprd/modules/libcamera/oem2v6/src/cmr_preview.c

2.操作方法
2.1 Android 10 操作步骤
2.1.1 打开adb，输入以下命令
adb root  //root权限
adb remount  //打开手机接口
adb shell setprop debug.camera.preview.dump.count0 num
或 adb shell setprop debug.camera.dump.frame preview      //dump固定数量10张
注：count0表示后摄，num是dump图片的数量，如果需要dump50张，则命令为：
adb shell setprop debug.camera.preview.dump.count0 50
如果需要dump前摄yuv图则命令改为：
adb shell setprop debug.camera.preview.dump.count1 50
注：dump50张图后，会跳出for循环，如果还需重新dump yuv图，需要设置num大于50张或重启设备（或者清除应用内存）。

2.1.2  打开手机相机，使相机处于固定模式下（需要dump哪个模式的yuv图，则让相机处于哪个模式下）
2.1.3 dump的手机yuv图片pull到电脑，命令如下：
Android 10中手机yuv图片保存默认路径：data/vendor/cameraserver
adb pull data/vendor/cameraserver d:CameraYUV
注：左边路径为手机存放yuv图的路径，右边路径为目标路径。
2.1.4  删除手机中的yuv图
rm -rf /data/vendor/cameraserver/*.yuv
2.2 Android 8 操作步骤
2.2.1 打开adb，输入以下命令
adb root  //root权限
adb remount  //打开手机接口
adb shell setprop debug.camera.dump.frame preview  
注：系统程序默认dump10张图，dump10张图后，会跳出for循环，如果还需重新dump yuv图，需要重启设备（或者清除应用内存）。
2. 2.2 打开手机相机，使相机处于固定模式下（需要dump哪个模式的yuv图，则让相机处于哪个模式下）
Android 8中手机yuv图片保存默认路径：data/misc/cameraserver
```## Android Camera的一些调试技巧总结

```text
//执行这个adb命令会打印所有默认参数和当前使用参数
adb shell dumpsys media.camera
//查看某一项参数,使用过滤命令grep(linux), windows下可使用findstr来过滤
adb shell dumpsys media.camera | grep picture-size
//输出
picture-size: 3264x2448
picture-size-values:
5520x4140,5984x3366,3840x2160,3264x2448,2048x1536,1920x1080,1280x720,640x480,480x320,320x240

最大人脸检测数
android.statistics.info.maxFaceCount (120002): int32[1]
    [10 ]

ps : https://duanqz.github.io/2015-07-19-Intro-to-dumpsys       dumpsys 工作原理

Android Camera Debug
见“99 Debug and Utils --- 06 Android Camera Debug”中的内容

Google Framework Enable

Java层
找到Java层对应文件中的
private final boolean DEBUG = false;
改为true

CameraService.cpp

// ----------------------------------------------------------------------------

// Logging support -- this is for debugging only

// Use "adb shell dumpsys media.camera -v 1" to change it.

//!++

volatile int32_t gLogLevel = 1;

//!--

#define LOG1(...) ALOGD_IF(gLogLevel >= 1, __VA_ARGS__);

#define LOG2(...) ALOGD_IF(gLogLevel >= 2, __VA_ARGS__);

即设定对应的参数即可enable对应的log

其余native层代码

将对应文件中的

//#define LOG_NDEBUG 0    -- ALOGV开关
//#define LOG_NNDEBUG 0  // Per-frame verbose logging   -- ALOGVV开关
取消注释
```## Dump preview数据方法

```text
进camera之间输入命令:
89及之前的平台:
adb shell setprop camera.dumpbuffer.enable O g 1
92平台:
adb shell setprop K
camera.dumpbuffer.enable @ 2
进camera之后在SD卡上会生成*.yuv,*.raw的文件,针对YUV文件,可以使用ImageBrowser工具查看yuv数据是否为黑色,如果是黑色,一般为底层问题,请driver或者mhal同事处理。
```## 预览或录像画面异常问题的 buffer dump和处理

```text
一、Streaming 的各个dump方法

1.整个P2S I/O buffer 的 dump

1.1 整个P2S I/O buffer 的 NDD Dump(Normal Data Dump)方法 

Dump P2S 的 input/output buffer, contain rrzo, lcso, img3o, preview, record, and other yuv buffers which AP request.

Dump 步骤：

1.测试前，先下adb命令准备dump：
adb root
adb shell setenforce 0
adb shell setprop debug.cam.drawid 1            --> draw magic number on camera output buffer
adb shell setprop vendor.debug.fpipe.force.img3o 1     --> force enable img3o
adb shell rm -rf /data/vendor/camera_dump/*
adb shell setprop vendor.debug.p2f.dump.enable 1
adb shell setprop vendor.debug.p2f.dump.mode 1

2. 复现问题，并下adb命令开始dump:
2.1 如果问题复现后，异常画面是一直存在的而不是闪现，则异常画面出现后，下adb命令开始 dump
2.2 如果问题是概率性出现的，异常画面不会一直存在，则异常画面出现前，下adb命令开始 dump
2.3 如果是录像录出的视频画面异常，则需要在录像时，就要下adb命令开始dump，才能dump到camera输出的 record buffer  
adb shell setprop vendor.debug.camera.preview.dump 1

3.停止dump：
3.1 如果问题复现后，异常画面是一直存在的而不是闪现，则 dump 一小会儿(大概2s, 3s左右)，立马下adb命令停止 dump(防止 dump时间长，dump 信息过大)
3.2 如果问题是概率性出现的, 异常画面不会一直存在，则要等异常画面复现后，再下adb命令停止 dump
adb shell setprop vendor.debug.camera.preview.dump 0

4.将dump到的信息pull到本地目录：
adb pull /data/vendor/camera_dump <本地电脑存放路径>
dump 完后，dump 出来的 buffer 都放到 /data/vendor/camera_dump 这个目录下了。
camera_dump文件夹下的文件名称命令格式：
UniqueKey-RequestNo-FrameNo-SensorDev-Port-BufferWidth-BufferHeight-BufferStride_ImageWidthxImageHeight_xxx.Format
Dump example:  
053310842-0032-0032-main-rrzo-PW1920-PH1440-BW3600__1920x1440_10_2.packed_word    --> main sensor 的P1 rrzo buffer
053310842-0032-0032-main-img3o-PW1920-PH1472-BW1920__1920x1440_8_s0.yv12     --> main sensor 的img3o buffer(P2Anode 下过了ISP 但是还没过MDP 的buffer，供3DNR用)   
053310842-0032-0032-main-wdmao-PW1920-PH1080-BW1920__1920x1080_8_s0.nv21    --> wdmao 代表判断为 display output buffer，也就是P2S 最终输出的main sensor的display buffer
053310842-0032-0032-main-PW352-PH352-BW704__352x264_12_s0.lcso    --> main sensor 的P1 lcso buffer
040521031-2275-1954-sub-wroto-PW640-PH480-BW640__640x480_8_s0.yv12    --> wroto代表判断为record output buffer，也就是 P2S 最终输出的sub sensor 的record buffer
064306554-0118-0118-main-undef-PW1920-PH1080-BW1920__1920x1080_8_s0.nv21    --> previewCallback ，也就是P2S 最终输出的main sensor 的previewCallback buffer

5G project(除了5G B) 上，P1输出的 yuvo buffer(分两个文档存，由以往的P1输出rrzo buffer改为P1 直接输出yuvo buffer) ：
040751403-0451-0246-sub-yuvo-cplane-PW1280-PH976-BW1600__1280x976_10_s0.packed_word
040751403-0451-0246-sub-yuvo-yplane-PW1280-PH976-BW1600__1280x976_10_s0.packed_word

1.2 整个P2S I/O buffer 的自定义 Dump方法 
有时候，可能不需要每一帧都 dump，只需要 dump 指定的某些帧的P2S I/O buffer，就可以用自定义dump 方法去 dump。
Dump 步骤：
1.测试前，直接下以下命令开始dump:
adb root
adb shell setenforce 0
adb shell setprop debug.cam.drawid 1            -->  draw magic number on camera output buffer
adb shell mkdir /data/vendor/p2_dump
adb shell setprop vendor.debug.p2f.dump.enable 1
adb shell setprop vendor.debug.p2f.dump.mode 2
adb shell setprop vendor.debug.p2f.dump.start  50        -->  P2S FrameNo >= 50 就開始dump
adb shell setprop vendor.debug.p2f.dump.count  70       -->  連續dump 70 個frame

2.進入Camera，FrameNo 達成上述條件即開始dump
After 2018/11/13 p0mp3,  上面的最后两条adb命令可以改成  adb shell setprop vendor.debug.camera.continue.dump N ，N代表立刻開始dump，並連續dump N張，Dump 完要記得reset 0

3.將dump file 拉到PC端：
adb pull /data/vendor/p2_dump  <local path>

p2_dump目录下的文件命名格式：
MagicNumber_P2SFrameIDmDumpIndex_ImgStreamCount_MWImgName_ImgWidthxImgHeight-PWBufWidth-PHBufHeight_StrideInBytes_ColorArrangement.Format
Dump example:
0160_0158m00_00_inResized_1_1936x1088-PW1937-PH1088_3632_0.fg_bayer10    --> P1 RRZO
0160_0158m00_01_inLCSO_1_352x196-PW352-PH352_704_-1.unknown          --> P1 LCSO
0160_0158m00_03_display_1920x1080-PW1920-PH1080_1920_-1.nv21           --> P2S display output
0160_0158m00_04_record_1920x1080-PW1920-PH1080_1920_-1.yv12            --> P2S record output
0160_0158m00_04_previewCB_1920x1080-PW1920-PH1080_1920_-1.nv21      --> previewCallback的一种(APP要求出的除了display, record 以外的yuv)

做P2S I/O buffer dump时，如果只想 dump 某一路或某几路 buffer而不想全部都dump，则只需在Dump步骤的第一步补上不同的 filter命令就可以了：
Extra:  Dump File filter ( NDD dump  & 自定义dump方法都适用)
根據P2_DumpPlugin.h 定義的Mask
enum DUMP_IN {
    DUMP_IN_RRZO,   --> dump 时，需 adb shell setprop vendor.debug.p2f.dump.in 1
    DUMP_IN_IMGO,   --> dump 时，需 adb shell setprop vendor.debug.p2f.dump.in 2
    DUMP_IN_LCSO,   --> dump 时，需 adb shell setprop vendor.debug.p2f.dump.in 4
};

enum DUMP_OUT {
    DUMP_OUT_DISPLAY,    --> dump 时，需 adb shell setprop vendor.debug.p2f.dump.out 1
    DUMP_OUT_RECORD,    --> dump 时，需 adb shell setprop vendor.debug.p2f.dump.out 2
    DUMP_OUT_FD,              --> 0x4 (目前FD Buffer尚未支援dump)
    DUMP_OUT_PREVIEWCB,    --> dump 时，需 adb shell setprop vendor.debug.p2f.dump.out 8
};

只dump 上面output的某一路 buffer(比如preview buffer) 时，除了设置 vendor.debug.p2f.dump.out的值, 还需要同步设置 vendor.debug.p2f.dump.in 为 0。反之亦然。
如果要组合dump其中的某几路buffer，则需要各个 output 或 input 值按位或。
比如：
adb shell setprop vendor.debug.p2f.dump.in  5   -->  只dump RRZO & LCSO，看到IMGO 一律不dump 
adb shell setprop vendor.debug.p2f.dump.out  9   -->  只dump Display & PreviewCB
```## 通过log查看camera sensor型号

```text
针对mtk平台机器，在camera开发过程中，可以通过log打印信息来确认该机器的camera sensor型号。

需要开启mtklog，重启之后，查看kernel_log.boot。

通过log查看：关键字：currSensorName sensor等，如：

Line 4283: 01-02 00:53:46.808303  1786  1786 D [   31.085098](7)[1786:initCamdevice][name:kd_camera_hw&]: currSensorName=ov13855mipiraw pinSetIdx=0
currSensorName=ov13855mipiraw 表示的sensor型号就是ov13855mipi了。

其中pinSetIdx=0，表示后摄；pinSetIdx=1，表示前摄；pinSetIdx=2，表示辅摄；

Line 2671: <7>[   31.849131]  (5)[1778:initCamdevice][name:kd_camera_hw&][kd_camera_hw]kdCISModulePowerOn -on:currSensorName=ov13855mipiraw pinSetIdx=0
Line 2795: <7>[   32.273980]  (7)[443:cameraserver][name:kd_camera_hw&][kd_camera_hw]kdCISModulePowerOn -off:currSensorName=ov13855mipiraw pinSetIdx=0
Line 2825: <7>[   32.311890]  (7)[1800:initCamdevice][name:kd_camera_hw&][kd_camera_hw]kdCISModulePowerOn -on:currSensorName=ov8856mipirawtruly pinSetIdx=1
Line 2918: <7>[   32.634586]  (1)[1207:Binder:443_1][name:kd_camera_hw&][kd_camera_hw]kdCISModulePowerOn -off:currSensorName=ov8856mipirawtruly pinSetIdx=1
Line 2945: <4>[   32.660070]  (7)[1820:Imem_Dbg_thread]__sched_setscheduler 1820:Imem_Dbg_thread sched_priority=-2<7>[   32.660306]  (5)[1819:initCamdevice][name:kd_camera_hw&][kd_camera_hw]kdCISModulePowerOn -on:currSensorName=ov2281mipimono pinSetIdx=2
Line 2977: <7>[   32.841255]  (7)[1769:Binder:443_2][name:kd_camera_hw&][kd_camera_hw]kdCISModulePowerOn -off:currSensorName=ov2281mipimono pinSetIdx=2
```## 相机模块 monkey 测试命令

```text
adb shell monkey -p com.hmdglobal.app.cameralite -v-v-v --throttle 800 --ignore-crashes --ignore-timeouts --ignore-native-crashes --ignore-security-exceptions --kill-process-after-error 50000000

参数解析：
-p 用于约束限制，用此参数指定一个或多个包（Package，即App）。指定包之后，Monkey将只允许系统启动指定的APP。如果不指定包，Monkey将允许系统启动设备中的所有APP。

-v 用于指定反馈信息级别（信息级别就是日志的详细程度），总共分3个级别，分别对应的参数如下表所示：
日志级别 Level0 
示例 adb shellmonkey -p com.htc.Weather -v 100
说明 缺省值，仅提供启动提示、测试完成和最终结果等少量信息

日志级别 Level 1
示例 adb shellmonkey -p com.htc.Weather -v -v 100
说明  提供较为详细的日志，包括每个发送到Activity的事件信息

日志级别 Level 2
示例 adb shellmonkey -p com.htc.Weather -v -v -v 100
说明  最详细的日志，包括了测试中选中/未选中的Activity信息

-s 用于指定伪随机数生成器的seed值，如果seed相同，则两次Monkey测试所产生的事件序列也相同的。
Monkey 测试1：adb shell monkey -p com.htc.Weather -s 10 100
Monkey 测试2：adb shell monkey -p com.htc.Weather -s 10 100
两次测试的效果是相同的，因为模拟的用户操作序列（每次操作按照一定的先后顺序所组成的一系列操作，即一个序列）是一样的。操作序列虽然是随机生成的，但是只要我们指定了相同的Seed值，就可以保证两次测试产生的随机操作序列是完全相同的，所以这个操作序列伪随机的；

--throttle <毫秒> 用于指定用户操作（即事件）间的时延，单位是毫秒；
示例：adb shell monkey -p com.htc.Weather –throttle 3000 100

--ignore-crashes 用于指定当应用程序崩溃时（Force& Close错误），Monkey是否停止运行。如果使用此参数，即使应用程序崩溃，Monkey依然会发送事件，直到事件计数完成。
--ignore-timeouts 用于指定当应用程序发生ANR（Application No Responding）错误时，Monkey是否停止运行。如果使用此参数，即使应用程序发生ANR错误，Monkey依然会发送事件，直到事件计数完成。
--ignore-security-exceptions 用于指定当应用程序发生许可错误时（如证书许可，网络许可等），Monkey是否停止运行。如果使用此参数，即使应用程序发生许可错误，Monkey依然会发送事件，直到事件计数完成。
--kill-process-after-error 用于指定当应用程序发生错误时，是否停止其运行。如果指定此参数，当应用程序发生错误时，应用程序停止运行并保持在当前状态（注意：应用程序仅是静止在发生错误时的状态，系统并不会结束该应用程序的进程）。
--monitor-native-crashes 用于指定是否监视并报告应用程序发生崩溃的本地代码。
```## DreamCamera2 模式与功能开关

```text
APP开关都在CameraUtil.Java中
在  public static void initialize(Context context)  中的开关都是在cameraAPP中进行控制的，

在private static void initializeCapabilitiesFromFeatureList(int[] featureList)中的开关都是在md.mk中进行配置的，对应着
vendor/sprd/modules/libcamera/hal3_2v6/SprdCamera3Setting.cpp中的
void SprdCamera3Setting::initCameraIpFeature(int32_t cameraId) 
根据persist值在md.mk中进行配置

以1.全景； 2.专业； 3.连拍为例
CameraUtil.java （dreamcamera2\src\com\android\camera\util)
//全景
    /* value of persist.sys.cam.wideangle & wideAngleVersion
     * 0: close this module
     * 1: google wideangle
     * 2: sprd wideangle
     * default: 2
     */
wideAngleVersion = getIntProperties(TARGET_CAMERA_WIDEANGLE_VERSION,0);
isContinuePhotoEnabled  = isEnable(TARGET_CONTINUE_PHOTO_ENABLE, false);  //连拍

手动模式请直接将此调用置为false
public static boolean isManualPhotoEnable() {
    return !isBackYUVSensor();   //return false;
}

所有模式都是在ModulesInfo.java （dreamcamera2\src\com\android\camera\module）
的public static void setupDreamModules(Context context, ModuleManager moduleManager) 通过判断来进行注册的，未注册则该模式关闭。
```## 设置Android Camera2预览画面的帧率(FPS)

```text
1、声明变量全局存储相机的FPS范围
private static Range<Integer>[] fpsRanges;

2、在opencamera的时候获取
// 该相机的FPS范围
fpsRanges = characteristics.get(CameraCharacteristics.CONTROL_AE_AVAILABLE_TARGET_FPS_RANGES);

3、在createCameraPreviewSession中设置预览画面的帧率
// 设置预览画面的帧率 视实际情况而定选择一个帧率范围
mPreviewRequestBuilder.set(CaptureRequest.CONTROL_AE_TARGET_FPS_RANGE, fpsRanges[0]);
```## 在模组支持变焦的情况下，如何打开DreamCamera变焦

```text
1. adb shell dumpsys media.camera > result.txt
查看result.txt看zoom变焦，如果是能力值只有1则进行第二步的修改

com.addParameters.sprdZoomRatio (8000005e): float[1]
          [1.00000000 ]
android.scaler.availableMaxDigitalZoom (d0004): float[1]
          [1.00000000 ]
2. 在文件SprdCamera3Setting.h中进行如下修
#ifndef CONFIG_ISP_2_3
#define MAX_DIGITAL_ZOOM_RATIO (1.0f)//////请将这行修改为4.0f
#else
#define MAX_DIGITAL_ZOOM_RATIO (1.0f)//////请将这行修改为4.0f
#endif

TODO : 如何判断模组是否支持变焦？看 sensor 规格书？
```## DreamCamera2如何查看当前人脸属性/人脸识别算法库版本

```text
可通过log查看

人脸属性算法库版本
Line 29776: M014C3E  07-02 19:28:12.893   496  8898 I libfaceattr: [FarCreateRecognizerHandle,58]: SPRD FAR version: LIBVER[1.16.11.4][Apr 24 2019][15:04:41]
Line 29804: M014C5A  07-02 19:28:12.969   496  8898 I FAR     : [FarCreateRecognizerHandle_V2,136]: SPRD FAR version: CAM_ALGO_CV_FAR_LIBVER[2.1.5.1.1396036][Aug 27 2020][15:06:32]
人脸识别算法库版本
Line 9787: M0EF2DA  04-27 16:10:59.885   372  9493 I libfacedetect: [FdCreateDetector,175]: LIBVER[1.8.7.14][Oct 15 2020][10:52:05]
```## 如何去掉前摄ZOOM变焦缩放效果？

```text
可以把前摄的放大倍数改成1.这样前摄就不会有放大效果。
找到HAL层SprdCamera3Setting.cpp（2V6）文件  initStaticMetadata  这个函数
s_setting[cameraId].scalerInfo.max_digital_zoom = MAX_DIGITAL_ZOOM_RATIO;
改成
if (cameraId == 1) {
    s_setting[cameraId].scalerInfo.max_digital_zoom = 1;
} else {
    s_setting[cameraId].scalerInfo.max_digital_zoom = MAX_DIGITAL_ZOOM_RATIO;
}
```## 展讯平台DreamCamera2各模式的前后摄支持情况

```text
只支持后摄的：全景，大光圈，专业，连拍，延时，滤镜，慢录，二维码，夜景拍照，夜景录像

只支持前摄的：间隔拍照

前后摄都支持的：人像，拍照，视频，有声照片，超清拍照

TODO : 在代码中如何查看？
```## DreamCamera2如何增加照片尺寸？

```text
一、问题背景
针对特殊的屏幕尺寸，客户常常要添加新的拍照尺寸。下面以android 10为例，说明如何添加。

二、解决方案
假设设备屏幕物理尺寸为8：5，以添加一组8：5尺寸为例。
①.在底层添加 8：5的size
参考路径：vendor/sprd/modules/libcamera/hal3_2v4/SprdCamera3Setting.cpp
420  const cam_stream_info_t stream_info[] = {
...
425      {{3264, 2448}, 33331760L, 33331760L},
426      {{3264, 1836}, 33331760L, 33331760L},
427      {{2592, 1944}, 33331760L, 33331760L},
+        {{2592, 1620}, 33331760L, 33331760L},   //for capture
428      {{2560, 1920}, 33331760L, 33331760L},
432      {{1920, HEIGHT_2M}, 33331760L, 33331760L},
433      {{1600, 1200}, 33331760L, 33331760L},
435      {{1280, 960}, 33331760L, 33331760L},
+        {{1280, 800}, 33331760L, 33331760L},   //for preview
436      {{1280, 720}, 33331760L, 33331760L},
437      {{960, 720}, 33331760L, 33331760L},
...
445      {{480, 480}, 33331760L, 33331760L},
446      {{352, 288}, 33331760L, 33331760L},
447      {{320, 240}, 33331760L, 33331760L},
+        {{320, 200}, 33331760L, 33331760L},   //for thumbnail
448      {{288, 352}, 33331760L, 33331760L},
449      {{240, 320}, 33331760L, 33331760L},
450      {{176, 144}, 33331760L, 33331760L}};

②在上层添加如下代码：
根据实际物理屏幕尺寸添加或删除相应比例
参考路径：\vendor\sprd\platform\packages\apps\DreamCamera2\src\com\android\camera\settings\ResolutionUtil.java中添加对应的比例
--- a/src/com/android/camera/settings/ResolutionUtil.java
+++ b/src/com/android/camera/settings/ResolutionUtil.java

@@ -67,11 +67,12 @@ public class ResolutionUtil {
      * We will also take the maximum supported resolution for full sensor image.
      */
     private static Float[] sDesiredAspectRatios = {
-            16.0f / 9.0f, 4.0f / 3.0f
+            16.0f / 9.0f, 4.0f / 3.0f, 8.0f / 5.0f
     };
     private static Size[] sDesiredAspectRatioSizes = {
-            new Size(16, 9), new Size(4, 3)
+            new Size(16, 9), new Size(4, 3) , new Size(8, 5)
     };
如果添加的是可整除的尺寸，如18：9，并且需要在app的settings界面显示改比例信息，还需要添加以下修改，否则settings界面显示的是2：1尺寸。
\vendor\sprd\platform\packages\apps\DreamCamera2\src\com\dream\camera\settings\DataModuleInterfacePV.java
             int numerator = ResolutionUtil.aspectRatioNumerator(approximateSize);
         int denominator = ResolutionUtil
                 .aspectRatioDenominator(approximateSize);
+        if (numerator == 2 && denominator == 1) {
+            numerator = 18;
+            denominator = 9;
+        }
         String result = mContext.getResources().getString(
                 R.string.setting_summary_aspect_ratio_and_megapixels,
                 numerator, denominator, megaPixels);
```## DreamCamera2如何屏蔽某种拍照或者录像模式？

```text
一、问题背景
当硬件设备不支持某一种相机模式（拍照/录像）时，DreamCamera2会报无法打开相机等相关错误，这时需要屏蔽不支持的相机模式，本文旨在说明如何屏蔽DreamCamera2某种模式，方便客户自行解决该问题。

二、问题答案
APP屏蔽的方法有：①取消模式的注册，②将模式图标设置为INVISABLE
底层屏蔽相机模式的方法：修改底层返回给上层的FeatureList值为false
本文只说明APP层的屏蔽方法，底层的屏蔽方法可咨询展锐camera hal/driver同事。APP层将模式图标设置为INVISABLE的屏蔽模式的方法并不可取，因为该修改方案仍然会注册需要屏蔽的相机模式。
APP层推荐的方法是取消模式的注册。取消模式注册，可以在app层将需要屏蔽的模式的FeatureList值强制设置为false，这样该模式被屏蔽了，也不会注册该模式，因此也不消耗模式注册所需要的资源。
下面以android r为例，举例说明如何屏蔽DreamCamera2的慢录拍照模式，其他模式的屏蔽可类比进行修改。
vendor\sprd\platform\packages\apps\DreamCamera2\src\com\android\camera\util\CameraUtil.java
public static boolean isSlowMotionEnabled() {
    return isSlowMotionEnabled && isBackCameraEnable(); //修改此处返回为false
}
```## 工厂测试如何去掉相机标定

```text
如果系统属性 persist.vendor.cam.multicam.cali.veri 为 1 则支持相机标定验证，否则不支持
```## 双击音量键操作camera有的时候会有无效果的现象

```text
双击音量键操作分为上键和下键两个操作，要注意这两个键分属于两个不同的功能，一般“双击音量上键”是打开camera的操作，“双击音量下键”是急速抓拍的功能
1、双击音量上键
一般开关位置在系统的设置列表中，为“快速打开相机”选项。
frameworks/base/services/core/java/com/android/server/policy/SprdPhoneWindowManager.java
            case KeyEvent.KEYCODE_VOLUME_UP:
                //UNISOC:bug1129524 open camera by double press voluem_up key
                super.handleVolumeKey(event, policyFlags);
                if(event.getAction() == KeyEvent.ACTION_DOWN && hasInterceptVolumeUpKey()){
                    interceptVolumeUpKeyDown(event);
                    return 0;
                }
                break;

    public boolean interceptVolumeUpKeyDown(KeyEvent event) {
2、双击音量下键
开关位置在camera的设置列表中，名称是“双击音量下键熄屏急速抓拍”，有三个功能开关，分别是“熄屏使用后置摄像头抓拍”、“熄屏使用前置摄像头抓拍”、“关闭”。
注意使用急速抓拍的时候，需要注意一下测试手法，在双击音量下键之后，需要等待3秒钟左右，会进行熄屏下的拍照，拍照成功后会有一个震动反馈，自始至终手机都一直处于熄屏的状态
如果出现双击音量下键无效的情况下，可以检查一下下面的函数是否调用
快拍功能的入口函数
frameworks/base/services/core/java/com/android/server/policy/SprdPhoneWindowManager.java
    private void launchQuickCamera() {
```## 展锐平台相机DreamCamera2中，如何修改录像尺寸？

```text
一、介绍
DreamCamera2的视频尺寸修改在media_profiles.xml文件中完成，不同芯片的media_profiles.xml文件的路径不一样，请根据芯片类型修改，对路径不清楚的可以请教驱动的同事
文件参考路径：sprdroid10_trunk_19c/device/sprd/sharkl5Pro/common/media_profiles.xml

二、案例
案例一：下面是添加h264视频格式480p视频的修改方案。
        <EncoderProfile quality="timelapsecif" fileFormat="mp4" duration="60">
            <Video codec="m4v"
                   bitRate="512000"
                   width="352"
                   height="288"
                   frameRate="30" />
            <!-- audio setting is ignored -->
            <Audio codec="amrnb"
                   bitRate="12200"
                   sampleRate="8000"
                   channels="1" />
        </EncoderProfile>
+      <EncoderProfile quality="480p" fileFormat="mp4" duration="60">
+           <Video codec="h264"
+                  bitRate="4000000"
+                  width="640"
+                  height="480"
+                  frameRate="30" />
+           <Audio codec="aac"
+                  bitRate="64000"
+                  sampleRate="44100"
+                  channels="1" />
+       </EncoderProfile>
+
+       <EncoderProfile quality="timelapse480p" fileFormat="mp4" duration="60">
+           <Video codec="h264"
+                  bitRate="4000000"
+                  width="640"
+                  height="480"
+                  frameRate="30" />
+           <!-- audio setting is ignored -->
+           <Audio codec="aac"
+                  bitRate="64000"
+                  sampleRate="44100"
+                  channels="1" />
+       </EncoderProfile>
        <ImageEncoding quality="95" />
        <ImageEncoding quality="80" />
        <ImageEncoding quality="70" />
        <ImageDecoding memCap="20000000" />
</CamcorderProfiles>
可以针对特定模式的设置视频尺寸
案例二：针对前摄（cameraId="1"）添加1080p尺寸
<CamcorderProfiles cameraId="1">
        <EncoderProfile quality="cif" fileFormat="mp4" duration="60">
            <Video codec="h264"
                   bitRate="512000"
                   width="352"
                   height="288"
                   frameRate="15" />
            <Audio codec="amrnb"
                   bitRate="12200"
                   sampleRate="8000"
                   channels="1" />
        </EncoderProfile>
…………………………………
        <EncoderProfile quality="timelapse720p" fileFormat="mp4" duration="60">
            <Video codec="h264"
                   bitRate="8000000"
                   width="1280"
                   height="720"
                   frameRate="30" />
            <!-- audio setting is ignored -->
            <Audio codec="aac"
                   bitRate="96000"
                   sampleRate="44100"
                   channels="1" />
        </EncoderProfile>
+
+       <EncoderProfile quality="1080p" fileFormat="mp4" duration="60">
+            <Video codec="h264"
+                   bitRate="16000000"
+                   width="1920"
+                   height="1080"
+                  frameRate="30" />
+           <Audio codec="aac"
+                   bitRate="96000"
+                  sampleRate="44100"
+                   channels="1" />
+        </EncoderProfile>
+
+       <EncoderProfile quality="timelapse1080p" fileFormat="mp4" duration="60">
+            <Video codec="h264"
+                   bitRate="16000000"
+                   width="1920"
+                   height="1080"
+                   frameRate="30" />
+           <!-- audio setting is ignored -->
+            <Audio codec="aac"
+                   bitRate="96000"
+                   sampleRate="44100"
+                   channels="1" />
+        </EncoderProfile>
        <ImageEncoding quality="95" />
        <ImageEncoding quality="80" />
        <ImageEncoding quality="70" />
        <ImageDecoding memCap="20000000" />
 
    </CamcorderProfiles>
三、注意事项
需要注意的是：
①       设置的视频尺寸，hal层的SprdCamera3Setting.cpp文件必须支持，SprdCamera3Setting.cpp参考路径：sprdroid10_trunk_19c/vendor/sprd/modules/libcamera/hal3_2v6/SprdCamera3Setting.cpp
②       设置的视频尺寸，sensor必须支持，如sensor尺寸为200万（1200×1600），设置1080p（1920×1080）将会出错，因为1200×1600 = 1920000 < 1920×1080 = 2073600
③       目前平台支持的视频格式设置包括：1080p（1920×1080），720p（1080×720），480p（720×480），CIF（352×288）。
```## MTK 录像分辨率

```text
录像分辨率需要两个地方同时支持，才可以显示出来。
1、手机里面vendor/etc/media_profile**.xml 可能是用的V01什么东西，这个文件一般是在alps/device/目录下放着的，是通过COPY_FILE命令拷贝到out里的
2、需要底层metadata也支持这个尺寸，具体要什么尺寸，参考media_profile**.xml里的frameWidth frameHeight


device/mediatek/mt6739/media_codecs_mediatek_video_ago_2g.xml

志刚修改记录
http://192.168.3.78:7080/q/88e582d79c634e27309f9e664ca4428993118d7d

media_profiles.xml 的修改
http://192.168.3.78:7080/c/R0_MP1/alps-release-r0.mp1-default/+/73768

CSDN:
https://blog.csdn.net/King1425/article/details/70207456

device/<company_name>/<device_name>/media_profiles.xml 和 device/<company_name>/<device_name>/media_codecs.xml XML 文件中声明相机的媒体编解码器、格式和分辨率功能。

在设备的 device/<company_name>/<device_name>/device.mkmakefile 中添加以下行，以将 media_profiles.xml 和 media_codecs.xml文件复制到相应位置：

# media config xml file
PRODUCT_COPY_FILES += \
   <device>/<company>/<device>/media_profiles.xml:system/etc/media_profiles.xml

# media codec config xml file
PRODUCT_COPY_FILES += \
   <device>/<company>/<device>/media_codecs.xml:system/etc/media_codecs.xml

TODO : media_profile.xml 文件解析，以及是在哪里加载这个文件的
```## 使用DreamCamera2录像，播放没有声音，录音功能正常，使用第三方应用录像，播放有声音

```text
请先检查贵司是否为单mic，如果是，则删除副mic配置，primary_audio_policy_configuration.xml
删除以下内容：
<item>Built-In Back Mic</item>
<devicePort tagName="Built-In Back Mic" type="AUDIO_DEVICE_IN_BACK_MIC" role="source">
    <profile name="" format="AUDIO_FORMAT_PCM_16_BIT"
         samplingRates="8000,11025,12000,16000,22050,24000,32000,44100,48000"
         channelMasks="AUDIO_CHANNEL_IN_MONO,AUDIO_CHANNEL_IN_STEREO,AUDIO_CHANNEL_IN_FRONT_BACK"/>
</devicePort>
修改以下内容：
<route type="mix" sink="primary input"
    sources="Built-In Mic,Built-In Back Mic,Wired Headset Mic,BT SCO Headset Mic"/>  //Built-In Back Mic修改为Wired Headset Mic
<route type="mix" sink="Telephony Tx"
    sources="Built-In Mic,Built-In Back Mic,Wired Headset Mic,BT SCO Headset Mic"/>  //Built-In Back Mic修改为Wired Headset Mic

Android 10 
\device\sprd\对应工程\对应项目\rootdir\system\etc\audio_policy_config\primary_audio_policy_configuration.xml
Android 11
\device\sprd\mpool\module\audio\msoc\对应工程\system\etc\audio_policy_config\primary_audio_policy_configuration.xml
```## Android Q 如何默认关闭双击电源键开启相机？

```text
若Jump to camera快速打开相机是通过按电源键两次打开，要默认关闭该功能，需要配置如下配置项的默认值。
配置项：
Settings.Secure.CAMERA_DOUBLE_TAP_POWER_GESTURE_DISABLED
文件路径：
SettingsProvider/src/com/android/providers/settings/DatabaseHelper.java
修改方法：
该配置项在Secure表中，要在loadSecureSettings方法中配置一下默认值：0为默认开启，1为默认关闭。
loadIntegerSetting(stmt,Settings.Secure.CAMERA_DOUBLE_TAP_POWER_GESTURE_DISABLED，1);
```## Android Q 如何默认关闭Jump to camera？

```text
在Android Q上，Jump to camera通过双击音量上键开启相机：
要默认关闭该功能，需要配置如下配置项的默认值。
配置项：
Settings.Secure.CAMERA_DOUBLE_TAP_VOLUMEUP_GESTURE_DISABLED
文件路径：
frameworks/base/packages/SettingsProvider/src/com/android/providers/settings/DatabaseHelper.java
修改方法：
该配置项在Secure表中，要在loadSecureSettings方法中配置一下默认值：0为开启，1为关闭。
loadIntegerSetting(stmt, Settings.Secure.CAMERA_DOUBLE_TAP_VOLUMEUP_GESTURE_DISABLED, 1);
```## 拍照或录像没有位置信息

```text
当使用DreamCamera2拍照没有位置信息时，请确保满足以下条件进行重新测试：
一、拍照或录像获取位置信息条件
1、确保camera app授权了位置权限，以及camera app设置菜单中“保存位置权限”开关打开
2、手机插入SIM卡，正常连接网络
3、在GPS信号良好的地方测试，建议去天台等开阔地获取GPS信号。
拍照获取位置信息必须要有GPS信号和网络，一般室内环境是无法获取GPS信号的。

二、查看拍摄的照片和log是否有位置信息
1.没有，满足上述三个条件，建议去天台等开阔地获取GPS信号进行测试。
2.有，图片有位置信息说明,camera app可以正常获取到位置信息,这边功能是没有问题的。同样的视频录制时位置信息使用的是相同的代码逻辑,所以这边位置信息的获取也是没问题的。
关于视频文件查看时没有位置信息,这是因为很多图库软件本身就不支持视频文件的位置信息显示功能。查看视频的gallery/photosgo不支持。需要用支持的版本查看。可以对比支持的机器的应用版本，photos/photosgo等。也可以通过添加log查看位置信息是否写入。

三、通过添加log的方式查看位置信息是否写入
1.拍照位置信息是否写入的log
在vendor\sprd\platform\packages\apps\DreamCamera2\src\com\android\camera\PhotoModule.java中
public boolean capture() {
    Location loc = mActivity.getLocationManager().getCurrentLocation();    //获取位置信息
    Log.i(TAG,"location info:"+loc);                                       //打印log，可从log查看是否获取到位置信息
    CameraUtil.setGpsParameters(mCameraSettings, loc);                     //位置信息参数设置
}

2.录像位置信息是否写入的log
在vendor\sprd\platform\packages\apps\DreamCamera2\src\com\android\camera\VideoModule.java中
private void setRecordLocation() {
    Location loc = mLocationManager.getCurrentLocation();                //获取位置信息
    if (loc != null) {                                                   //判断位置信息是否为空
        mMediaRecorder.setLocation((float) loc.getLatitude(), (float) loc.getLongitude());                             //设置录像位置信息，可在此处添加log
        Log.v(TAG,"纬度:"+loc.getLatitude()+"; 经度:"+loc.getLongitude());    //添加的log
    } 
}
```## 设置中的wifi扫描二维码界面，进入后返回，下拉菜单中的手电筒无法使用

```text
此问题为退出了wifi的扫码界面后，camera资源没有得到释放导致手电筒一直被camera占用，无法通过其他方式（下拉通知栏内）进行手电筒的开启操作

解决方法就是在camera.stop(）之后，立即进行camera资源的释放

修改文件位置packages\apps\Settings\src\com\android\settings\wifi\dpp\WifiDppQrCodeScannerFragment.java
+ private void releaseCamera() {
+            mCamera.release();
+            mCamera = null;
+    }
 private void destroyCamera() {
        if (mCamera != null) {
            mCamera.stop();
+           releaseCamera();
            mCamera = null;
        }

修改文件位置packages\apps\Settings\src\com\android\settings\wifi\qrcode\QrCamera.java
+ public void release() {
+       mCamera.setPreviewCallback(null);
+       mCamera.release();
+    }
```## 如何去掉Camera录像过程中，被录制进去的自动对焦声音？

```text
在相机录制的过程中，很容易触发自动对焦，导致对焦的声音录制进去了。
只需要修改 FocusOverlayManager.java的 updateFocusFinsh方法
                 mFocusRing.startActiveFocusedFocus();
                 if (mFocusArea != null) {
                     if (mAppController.isPlaySoundEnable()) {
-                        mCameraSound.play(MediaActionSound.FOCUS_COMPLETE);
+                        if (!(mListener instanceof VideoModule && ((VideoModule) mListener).isRecording())) {
+                            mCameraSound.play(MediaActionSound.FOCUS_COMPLETE);
+                        }
                     }
                 } else {
                     mFocusRing.centerFocusLocation();
```## 如何让user版本软件拍出来的照片有完整的3A exif信息

```text
调试相机效果时，照片的3A exif信息是非常重要的参数。展锐平台默认只有debug版本软件拍照才会保存3A exif信息。如果需要让user软件拍下的照片也保存3A exif信息，则需要修改代码，这样不管是debug版本软件还是user版本软件，都能将照片的3A exif信息编码到照片中。

代码修改如下：

diff --git a/hal3_2v1/SprdCamera3OEMIf.cpp b/hal3_2v1/SprdCamera3OEMIf.cpp
index 33d29ad..0b8ff91 100644
--- a/hal3_2v1/SprdCamera3OEMIf.cpp
+++ b/hal3_2v1/SprdCamera3OEMIf.cpp
@@ -4974,8 +4974,8 @@ void SprdCamera3OEMIf::receiveJpegPicture(struct camera_frame_type *frame) {
         maxJpegSize = heap_size;
     }

-    property_get("ro.debuggable", value, "0");
-    if (!strcmp(value, "1")) {
+//    property_get("ro.debuggable", value, "0");
+//    if (!strcmp(value, "1")) {
         // add isp debug info for userdebug version
         ret = mHalOem->ops->camera_get_isp_info(mCameraHandle, &ispInfoAddr,
                                                 &ispInfoSize);
@@ -4999,7 +4999,7 @@ void SprdCamera3OEMIf::receiveJpegPicture(struct camera_frame_type *frame) {
                                          encInfo->size + ispInfoSize,
                                          mCaptureWidth, mCaptureHeight);
         }
-    }
+//    }

     jpegBlob = (camera3_jpeg_blob *)((char *)pic_addr_vir +
                                      (maxJpegSize - sizeof(camera3_jpeg_blob)));

android10版本对应文件路径是： vendor/sprd/modules/libcamera/hal3_2v6/SprdCamera3OEMIf.cpp ，上面修改也是有效的。

这样修改后，user版本软件拍出来的照片也能保存3A exif信息啦。
```## 双摄如何拍raw和yuv图片

```text
1、拍raw图片
输入命令adb shell setprop persist.vendor.cam.raw.mode raw
手机进入双摄模式，点击拍照，即在/data/vendor/cameraserver下同时生成主摄和辅摄的raw

2、拍yuv和depth图片
输入命令adb shell setprop persist.vendor.cam.raw.mode jpg
adb shell setprop persist.vendor.cam.bokeh.dump capdepth
手机进入双摄模式，点击拍照，即在/data/vendor/cameraserver下生成yuv和depth图供debug
```## Android 8.1 Camera插值配置

```text
在device/sprd/<>/BoardConfig.mk里，把这个宏改为false，并定义前后sensor插值后的尺寸大小
TARGET_BOARD_CAMERA_AUTO_DETECT_SENSOR := false

md.mk
CAMERA_SUPPORT_SIZE := 13M
FRONT_CAMERA_SUPPORT_SIZE := 5M
如果TARGET_BOARD_CAMERA_AUTO_DETECT_SENSOR为true，则自动检测sensor的实际大小, 后面的两个宏就不起作用.
如果插值后发现菜单中没有大尺寸显示，则是vendor/sprd/modules/libcamera/SprdCtrl.mk里没有引用大尺寸导致，
比如在SprdCtrl.mk里添加前sensor的13M引用:

ifeq ($(strip $(FRONT_CAMERA_SUPPORT_SIZE)),13M)
LOCAL_CFLAGS += -DCONFIG_FRONT_CAMERA_SUPPORT_13M
endif
同时看看
vendor/sprd/modules/libcamera/<>/SprdCamera3Setting.cpp里的default_sensor_max_sizes[]数组中是否有对DCONFIG_FRONT_CAMERA_SUPPORT_13M的引用，没有的话仿照其他尺寸添加引用.

另外添加大尺寸后，如果要添加一些自己想要的拍照尺寸，则是修改vendor/sprd/modules/libcamera/<>/SprdCamera3Setting.cpp里的stream_info数组，添加的规则要满足宽高都能被16整除.
比如插值13M后添加一个8M的16：9尺寸这样计算;
with = n * 16 * 16
height = n * 16 * 9
然后满足width * hight  = n*16*16*n*16*9 <= 8M,  求出最大的n值，就知道了width和height，然后添加到stream_info数组中.
实际上报的尺寸在这个文件中的3个for循环引用stream_info数组的地方，可以加log调试看看实际是否有上报尺寸
```--------------------------------------------------------------------------------------

## HMD Camera需求

```text
主要参考如下几个文档
Mantis/Cosmo
HMD_Mantis&Cosmo_v9.7.2_20201026.pdf
HMD_Matis_Cosmo_Camera_GUI_v9.7.11_20201017.pptx

Monster
HMD_Monster_20210111.pdf
HMD_Monster_Camera_GUI_20210305.pptx

文档中可能会有一些自相矛盾的地方或不明确的地方，可以找 Marc / Wendy 确认
```## DreamCamera2宏控

```text
由于 Mantis/Cosmo/Monster/Monster_Go 这几个项目的需求可能会有部分不同，所以需要用宏进行控制
在 md.mk 文件中添加 PRODUCT_PROPERTY_OVERRIDES += persist.vendor.cam.res.project=Mantis
if ("Monster".equalsIgnoreCase(android.os.SystemProperties.get("persist.vendor.cam.res.project", ""))) {

有些需求可能还需要用 SKUID 进行控制，如水印功能：
if (!"600ID".equalsIgnoreCase(android.os.SystemProperties.get("ro.boot.skuid"))) {
```## DreamCamera2配置相机分辨率

```text
以配置 Monster 全屏预览拍照为例
adb shell wm size 查看Monster屏幕分辨率为720x1640(41：18)，因此该画幅下拍照出图也应该是41：18。
另外，建议设置分辨率时保持为16的倍数。则41：18 和16的倍数，通过最小公倍数 加上缩放因子。可以列出可选分辨率。
656x288（缩放因子为1.0）
1312x576（缩放因子为2.0）
1968x864（缩放因子为3.0）
2624x1152(缩放因子为4.0，高度大于2592，不可用)
1600x720(目前使用分辨率)
1920x864
2240x1008
2560x1152

从 log 中查看分辨率
initStaticParameters: cameraId=0, largest_sensor_w=2592, largest_sensor_h=1944

Mantis/Cosmo
vendor/sprd/modules/libcamera/hal3_2v4/SprdCamera3Setting.cpp

Monster
vendor/sprd/modules/libcamera/hal3_2v6/SprdCamera3Setting.cpp

//before
const cam_stream_info_t stream_info[] = {
    {{5312, 3984}, 41666666L, 41666666L},
    {{4608, 3456}, 33331760L, 33331760L},
    {{4160, 3120}, 33331760L, 33331760L},
    //{{3840, 2160}, 33331760L, 33331760L},
    {{3264, 2448}, 33331760L, 33331760L},
    {{3264, 1836}, 33331760L, 33331760L},
    {{2592, 1944}, 33331760L, 33331760L},
    {{2560, 1920}, 33331760L, 33331760L},
    //{{2560, 1440}, 33331760L, 33331760L},
    {{2048, 1536}, 33331760L, 33331760L},
    //{{1920, 1920}, 33331760L, 33331760L},
    {{1920, HEIGHT_2M}, 33331760L, 33331760L},
    {{1600, 1200}, 33331760L, 33331760L},
    //{{1440, 1080},33331760L,33331760L},
    {{1280, 960}, 33331760L, 33331760L},
    {{1280, 720}, 33331760L, 33331760L},
    {{960, 720}, 33331760L, 33331760L},
    {{864, 480}, 33331760L, 33331760L},
    {{720, 544}, 33331760L, 33331760L},
    {{720, 480}, 33331760L, 33331760L},
    {{640, 480}, 33331760L, 33331760L},
    {{640, 360}, 33331760L, 33331760L},
    {{624, 352}, 33331760L, 33331760L},
    {{480, 640}, 33331760L, 33331760L},
    {{480, 480}, 33331760L, 33331760L},
    {{352, 288}, 33331760L, 33331760L},
    {{320, 240}, 33331760L, 33331760L},
    {{288, 352}, 33331760L, 33331760L},
    {{240, 320}, 33331760L, 33331760L},
    {{176, 144}, 33331760L, 33331760L}};

//after
const cam_stream_info_t stream_info[] = {
    {{5312, 3984}, 41666666L, 41666666L},
    {{4608, 3456}, 33331760L, 33331760L},
    {{4160, 3120}, 33331760L, 33331760L},
    //{{3840, 2160}, 33331760L, 33331760L},
    {{3264, 2448}, 33331760L, 33331760L},
    {{3264, 1836}, 33331760L, 33331760L},
    {{2592, 1944}, 33331760L, 33331760L},
    {{2560, 1920}, 33331760L, 33331760L},
    //{{2560, 1440}, 33331760L, 33331760L},
    {{2048, 1536}, 33331760L, 33331760L},
    //{{1920, 1920}, 33331760L, 33331760L},
    {{1920, HEIGHT_2M}, 33331760L, 33331760L},
    {{1600, 1200}, 33331760L, 33331760L},
    //{{1440, 1080},33331760L,33331760L},
    {{1280, 960}, 33331760L, 33331760L},
    {{1280, 720}, 33331760L, 33331760L},
    {{1200, 540}, 33331760L, 33331760L},
    {{960, 720}, 33331760L, 33331760L},
    {{864, 480}, 33331760L, 33331760L},
    {{720, 544}, 33331760L, 33331760L},
    {{720, 480}, 33331760L, 33331760L},
    {{640, 480}, 33331760L, 33331760L},
    {{640, 360}, 33331760L, 33331760L},
    {{624, 352}, 33331760L, 33331760L},
    {{480, 640}, 33331760L, 33331760L},
    {{480, 480}, 33331760L, 33331760L},
    {{352, 288}, 33331760L, 33331760L},
    {{320, 240}, 33331760L, 33331760L},
    {{288, 352}, 33331760L, 33331760L},
    {{240, 320}, 33331760L, 33331760L},
    {{176, 144}, 33331760L, 33331760L}};

初始化顶部屏幕分辨率按钮
ButtonManagerDream.java
private void initializeRatioButton(MultiToggleImageButton button,
        final ButtonCallback cb, final ButtonCallback preCb, int resIdImages) {
    if (resIdImages > 0) {
        button.overrideImageIds(resIdImages);
    }
    boolean isFront = DataModuleManager
            .getInstance(mAppController.getAndroidContext())
            .getCurrentDataModule().getDataSetting().mIsFront;
    String keyFacing = isFront ? Keys.KEY_PICTURE_SIZE_FRONT : Keys.KEY_PICTURE_SIZE_BACK;
    int index = DataModuleManager
            .getInstance(mAppController.getAndroidContext())
            .getCurrentDataModule()
            .getIndexOfCurrentValue(keyFacing);
    int stateIndex = -1;
    //Redmine61625 ODM modified for resolution indicator button ZQ:begin
    if (index == 2) {
        // 1:1
        stateIndex = 0;
    } else if (index == 0) {
        // 4:3
        stateIndex = 1;
    } else if (index == 1) {
        // 16:9
        stateIndex = 2;
    } else if (index == 3) {
        // 20:9
        stateIndex = 3;
    }
    //Redmine66389 ODM modified for resolutions ZQ:begin
    String project = android.os.SystemProperties.get("persist.vendor.cam.res.project", "");
    if (!isFront && "Monster".equalsIgnoreCase(project)) {
        if (index == 2) {
            // 16:9
            stateIndex = 2;
        } else if (index == 0) {
            // 4:3
            stateIndex = 1;
        } else if (index == 1) {
            // 1:1
            stateIndex = 0;
        } else if (index == 3) {
            // full(41:18)
            stateIndex = 3;
        }
    }
    //Redmine66389 ODM modified for resolutions ZQ:end
    //Redmine61625 ODM modified for resolution indicator button ZQ:end
    if (stateIndex < 0) {
        stateIndex = 0;
    }
    button.setState(stateIndex, false);
    setPreChangeCallback(button, preCb);
    button.setOnStateChangeListener(new MultiToggleImageButton.OnStateChangeListener() {
        @Override
        public void stateChanged(View view, int state) {
            int stateIndex = -1;
            //Redmine61625 ODM modified for resolution indicator button ZQ:begin
            if (state == 0) {
                // 1:1
                stateIndex = 2;
            } else if (state == 1) {
                // 4:3
                stateIndex = 0;
            } else if (state == 2) {
                // 16:9
                stateIndex = 1;
            } else if (state == 3) {
                // 20:9
                stateIndex = 3;
            }
            //Redmine66389 ODM modified for resolutions ZQ:begin
            if (!isFront && "Monster".equalsIgnoreCase(project)) {
                if (state == 0) {
                    // 4:3
                    stateIndex = 1;
                } else if (state == 2) {
                    // 16:9
                    stateIndex = 2;
                } else if (state == 1) {
                    // 1:1
                    stateIndex = 0;
                } else if (state == 3) {
                    // full
                    stateIndex = 3;
                }
            }
            //Redmine66389 ODM modified for resolutions ZQ:end
            //Redmine61625 ODM modified for resolution indicator button ZQ:end
            DataModuleManager.getInstance(mAppController.getAndroidContext()).getCurrentDataModule().changeSettingsByIndex(keyFacing, stateIndex);
        }
    });
}


删除video模式下的某一个分辨率
http://192.168.3.78:7080/c/SPRD_Q/MOCORDROID10_Trunk_19C_PATCH_W20.26.2/+/29818
device/sprd/mpool/module/media/codec/msoc/sharkl3/media_profiles.xml


移除某些分辨率
vendor/sprd/platform/packages/apps/DreamCamera2/src_pd/com/android/camera/util/GservicesHelper.java
public static String getBlacklistedResolutionsBack(ContentResolver contentResolver) {
    return "1600x1200,1440x1080,1920x1080,1280x720,1280x960,1920x1088,480x480,1600x720";
}

public static String getBlacklistedResolutionsFront(ContentResolver contentResolver) {
    return "1600x1200,1440x1080,1920x1080,1280x720,1280x960,1920x1088,480x480,1600x720";
}

设置各种比例下 ViewFinder 的显示位置
DreamCaptureLayoutHelper.java
```## DreamCamera2长按连拍功能开发

```text
SPCSS00753704
http://192.168.3.78:7080/gitweb?p=SPRD_R/MOCORDROIDR_Trunk_W20.36.4.git;a=commit;h=6e8ad73259eb9ca20ac391424a8484d9df17092e

开启倒计时长按拍照按钮中途停止连拍再次点击概率性出现无响应
http://192.168.3.78:7080/c/SPRD_R/MOCORDROIDR_Trunk_W20.36.4/+/53386
vendor/sprd/platform/packages/apps/DreamCamera2/src/com/dream/camera/modules/autophoto/AutoPhotoModule.java
if (mBurstCaptureCountOnCanceled <= mHasCaptureCount && mHasCaptureCount != 0 && mBurstCaptureCountOnCanceled != -1|| mBurstAllDone) {
原因是 mBurstCaptureCountOnCanceled > mHasCaptureCount 导致

多次快速点击拍照，会概率性响应连拍功能
```## DreamCamera2配置相机最大最小缩放比例

```text
sagereal/pcb/SP655_GH6551W_HMD_Mantis/alps/device/sprd/pike2/sp7731e_1h10/module/camera/md.mk
TARGET_BOARD_CAMERA_ISP_VERSION := 2.4

vendor/sprd/modules/libcamera/Camera.mk
ifeq ($(strip $(TARGET_BOARD_CAMERA_ISP_VERSION)),2.3)
    HAL_DIR := hal3_2v6
    OEM_DIR := oem2v6
    ISPDRV_DIR := camdrv/isp2.3
else ifeq ($(strip $(TARGET_BOARD_CAMERA_ISP_VERSION)),2.4)
    HAL_DIR := hal3_2v4
    OEM_DIR := oem2v4
    ISPDRV_DIR := camdrv/isp2.4
else ifeq ($(strip $(TARGET_BOARD_CAMERA_ISP_VERSION)),2.5)
    HAL_DIR := hal3_2v6
    OEM_DIR := oem2v6
    ISPDRV_DIR := camdrv/isp2.6
else ifeq ($(strip $(TARGET_BOARD_CAMERA_ISP_VERSION)),2.6)
    HAL_DIR := hal3_2v6
    OEM_DIR := oem2v6
    ISPDRV_DIR := camdrv/isp2.6
else ifeq ($(strip $(TARGET_BOARD_CAMERA_ISP_VERSION)),2.7)
    HAL_DIR := hal3_2v6
    OEM_DIR := oem2v6
    ISPDRV_DIR := camdrv/isp2.6
endif

vendor/sprd/modules/libcamera/hal3_2v4/SprdCamera3Setting.h
#define MIN_DIGITAL_ZOOM_RATIO (1.0f)

#ifdef CONFIG_CAMERA_ZOOM_FACTOR_SUPPORT_4X
#define MAX_DIGITAL_ZOOM_RATIO (4.0f)
#else
#define MAX_DIGITAL_ZOOM_RATIO (2.0f)
#endif

vendor/sprd/modules/libcamera/SprdCtrl.mk
ifeq ($(strip $(TARGET_BOARD_CAMERA_ZOOM_FACTOR_SUPPORT)),4)
LOCAL_CFLAGS += -DCONFIG_CAMERA_ZOOM_FACTOR_SUPPORT_4X
endif

sagereal/pcb/SP655_GH6551W_HMD_Mantis/alps/device/sprd/pike2/sp7731e_1h10/module/camera/md.mk
TARGET_BOARD_CAMERA_ZOOM_FACTOR_SUPPORT := 4

Mantis 配置 4X 分辨率会有卡顿的问题，和客户沟通之后同意只设置到2X
```## DreamCamera2移除相机中不需要的模式

```text
vendor/sprd/platform/packages/apps/DreamCamera2/src/com/android/camera/module/ModuleInfoResolve.java
private static int[] slideshow_standard = new int[]{
        SettingsScopeNamespaces.DREAM_PANORAMA,
        SettingsScopeNamespaces.REFOCUS,
        SettingsScopeNamespaces.PORTRAIT_PHOTO,
//            SettingsScopeNamespaces.MANUAL,
//            SettingsScopeNamespaces.CONTINUE,
        SettingsScopeNamespaces.AUTO_PHOTO,
        SettingsScopeNamespaces.AUTO_VIDEO,
//            SettingsScopeNamespaces.MANUAL,
//            SettingsScopeNamespaces.SLOWMOTION,
        SettingsScopeNamespaces.TIMELAPSE,
//            SettingsScopeNamespaces.TDNR_VIDEO,
//            SettingsScopeNamespaces.TDNR_PRO_VIDEO,
        SettingsScopeNamespaces.FOCUS_LENGTH_FUSION_PHOTO,
        //SettingsScopeNamespaces.MODE_MORE_TAG,
};
把要移除的模式注释掉即可
```## DreamCamera2修改顶部的菜单项

```text
vendor/sprd/platform/packages/apps/DreamCamera2/res/values/top_panel_config.xml
<array name="auto_photo_top_panel">
    <item>@array/camera_settings_config</item>
    <!--
    <item>@array/googlelens_config</item>
    <item>@array/flash_photo_front_led_config</item>
    <item>@array/hdr_config</item>
    -->
    <item>@array/motionphoto_config</item>
    <!--
    <item>@array/refocus_photo_config</item>
    -->
    <!--
    <item>@array/makeup_display_photo_config</item>
    -->
    <!--
    <item>@array/camera_config</item>
    -->
    <item>@array/countdown_config</item>
    <item>@array/ratio_config</item>
    <item>@array/flash_photo_front_led_config</item>
</array>

注释掉要删除的菜单即可

闪光灯图标
vendor/sprd/platform/packages/apps/DreamCamera2/res/values/arrays.xml
<array name="dream_camera_flashmode_icons" translatable="false">
    <item>@drawable/ic_flash_off_nokia</item>
    <item>@drawable/ic_flash_auto_nokia</item>
    <item>@drawable/ic_flash_on_nokia</item>
    <item>@drawable/flash_torch_off_to_on</item>        <!--常亮的图标-->
</array>
```## DreamCamera2配置 Camera Settings 中的菜单

```text
dream_camera_arrays_photo_part.xml
<!-- UI display config -->
<!-- back mode -->
<integer-array name="photo_back_mode_auto_setting_display">
    <item>@string/pref_camera_picturesize_back_key</item>
    <item>@string/pref_camera_jpeg_quality_key</item>
    <item>@string/pref_camera_composition_line_key</item>
    <item>@string/pref_ai_detect_smile_key</item>
    <item>@string/pref_ai_detect_face_attributes_key</item>
    <item>@string/pref_auto_add_logowatermark_key</item>
    <item>@string/pref_add_level_key</item>
    <item>@string/pref_auto_add_timewatermark_key</item>
    <item>@string/pref_camera_antibanding_key</item>
    <item>@string/pref_auto3dnr_param_key</item>
    <item>@string/pref_camera_ai_scene_detect_key</item>
    <item>@string/pref_camera_hdr_normal_pic_key</item>
    <item>@string/pref_camera_touching_photograph_key</item>
    <item>@string/pref_camera_time_stamp_key</item>
    <item>@string/pref_camera_flashmode_key</item>
    <item>@string/pref_camera_countdown_duration_key</item>
    <item>@string/pref_camera_refocus_key</item>
    <item>@string/pref_camera_hdr_key</item>
    <!--Redmine53694 MNT-405 modified to add burst shots setting ZQ:begin-->
    <item>@string/pref_camera_burst_shots_key</item>
    <!--Redmine53694 MNT-405 modified to add burst shots setting ZQ:end-->
    <!--zhangqi modified begin-->
    <item>@string/pref_front_camera_mirror_key</item>
    <!--zhangqi modified end-->
    <item>@string/pref_eois_dc_back_key</item>
    <item>@string/pre_ae_lock_key</item>
    <item>@string/pref_camera_ultra_wide_angle_key</item>
    <item>@string/pref_auto_tracking_key</item>
    <item>@string/pref_key_montionphoto</item>
    <!--Redmine53694 MNT-405 modified for video resolution settings ZQ:begin-->
    <item>@string/pref_video_resolution_key</item>
    <!--Redmine53694 MNT-405 modified for video resolution settings ZQ:end-->
    <!--redmine65579&&66415 MNR-833 and MNR-749 In camera mode, long press the camera button, cannot quickly record video dxh 2021.3.16 begin-->
    <item>@string/pref_camera_long_press_video_and_burst_shots_key</item>
    <!--redmine65579&&66415 MNR-833 and MNR-749 In camera mode, long press the camera button, cannot quickly record video dxh 2021.3.16 end-->
    <item>@string/pref_googlelens_setting_key</item>
</integer-array>
```## DreamCamera2对焦框和曝光

```text
手动对焦框
alps/vendor/sprd/platform/packages/apps/DreamCamera2/src/com/dream/camera/ui/AELockPanel.java
alps/vendor/sprd/platform/packages/apps/DreamCamera2/src/com/android/camera/ui/focus/FocusRingView.java

添加手动对焦的支持
最后只要在 md.mk 中添加 PRODUCT_PROPERTY_OVERRIDES += persist.sys.cam.touch.ev=true 即可
CameraUtil.java
private final static String TARGET_CAMERA_TOUCH_EV = "persist.sys.cam.touch.ev";
isTouchEvEnable = isEnable(TARGET_CAMERA_TOUCH_EV, false);
public static boolean isTouchEvEnable() {
    return isTouchEvEnable;
}

PhotoModule.java 中进行最终的设置，可以根据 setAECompensate 这个log进行查看
public void setCompensationDirectly(int value){
    if (mCameraSettings != null) {
        int max = mCameraCapabilities.getMaxExposureCompensation();
        int min = mCameraCapabilities.getMinExposureCompensation();
        Log.d(TAG, "setAECompensate: " + value);
        if(value < min || value > max){
            Log.e(TAG,"AE compensation value is not  in the range [-6,6]");
            return;
        }
        mCameraSettings.setExposureCompensationIndex(value);
        mCameraDevice.applySettings(mCameraSettings);
    }
}
    
曝光亮度调节顺滑度:
vendor/sprd/platform/packages/apps/DreamCamera2/src/com/dream/camera/ui/AELockSeekBar.java
private int scrollFriction = 10;    //default value, modify this

设置曝光亮度
vendor/sprd/platform/packages/apps/DreamCamera2/src/com/android/camera/PhotoModule.java
public void setCompensationDirectly(int value){
    if (mCameraSettings != null) {
        int max = mCameraCapabilities.getMaxExposureCompensation();
        int min = mCameraCapabilities.getMinExposureCompensation();
        Log.d(TAG, "setAECompensate: " + value);
        if(value < min || value > max){
            Log.e(TAG,"AE compensation value is not  in the range [-6,6]");
            return;
        }
        mCameraSettings.setExposureCompensationIndex(value);
        mCameraDevice.applySettings(mCameraSettings);
    }
}

曝光调节效果需要驱动配置效果参数
```## DreamCamera2缩放倍率消失时间

```text
vendor/sprd/platform/packages/apps/DreamCamera2/src/com/android/camera/ui/PreviewOverlay.java
private final int ZOOM_UI_HIDE_DELAY = 3000;
vendor/sprd/platform/packages/apps/DreamCamera2/src/com/dream/camera/ZoomPanel.java
@Override
public void setVisibility(int visibility) {
    if (!CameraUtil.isZoomPanelEnabled()
            /*|| (mActivity != null && mActivity.getCurrentModule() != null && mActivity.getCurrentModule().isAudioRecording())*/) { // bugfix 1019160
        super.setVisibility(View.GONE);
    } else {
        //zhangqi modified begin
        if (visibility == View.VISIBLE) {
            super.setVisibility(visibility);
        } else {
            animate().alpha(0f).setDuration(500).setListener(new Animator.AnimatorListener() {
                @Override
                public void onAnimationStart(Animator animation) {
                }
                @Override
                public void onAnimationEnd(Animator animation) {
                    ZoomPanel.super.setVisibility(View.GONE);
                    setAlpha(1f);
                }
                @Override
                public void onAnimationCancel(Animator animation) {
                }
                @Override
                public void onAnimationRepeat(Animator animation) {
                }
            });
        }
        //zhangqi modified end
    }
}
```## DreamCamera2 Camera Settings菜单修改

```text
修改 Settings 下的顺序
vendor/sprd/platform/packages/apps/DreamCamera2/res/xml/dream_camera_preferences.xml

移除 Settings 下的一些菜单
vendor/sprd/platform/packages/apps/DreamCamera2/src/com/dream/camera/settings/DreamUIPreferenceSettingFragment.java
private void setPhotoModuleVisiblity() {
    recursiveDelete(mRoot, mVideoPart);
    //zhangqi modified to remove settings preferences 2020/10/23:begin
    removePref(R.string.pref_camera_volume_key_function);
    removePref(R.string.pref_camera_quick_capture_key);
    removePref(R.string.pref_camera_countdown_duration_key);
    removePref(R.string.pref_camera_jpeg_quality_key);
    removePref(R.string.pref_camera_antibanding_key);
    removePref(R.string.pref_camera_picturesize_back_key);
    //removePref(R.string.pref_camera_picturesize_front_key);
    removePref(R.string.pref_ai_detect_smile_key);
    removePref(R.string.pref_camera_touching_photograph_key);
    removePref(R.string.pref_camera_composition_line_key);
    //zhangqi modified to remove settings preferences 2020/10/23:end
    mPhotoPart.changContent();
}
调用 removePref() 方法把不需要的菜单移除掉即可

HDR设置菜单
<integer-array name="pref_camera_hdr_key_array">
    <item>@string/pref_camera_hdr_key</item>
    <item>@integer/storage_position_category_bf</item>
    <item>@string/preference_switch_item_default_value_false</item>
    <item>@array/pref_camera_hdr_entryvalues</item>
    <item>@array/pref_camera_hdr_entry</item>
</integer-array>

HDR图标
DreamCamera2/res/layout/dream_camera.xml
<TextView
    android:id="@+id/lock_ae_tip"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_gravity="right"
    android:layout_marginTop="48dp"
    android:background="@drawable/blur_effect_highlight"
    android:backgroundTint="#ffffff"
    android:paddingLeft="8dp"
    android:paddingRight="8dp"
    android:text="@string/lock_ae_and_af"
    android:layout_marginRight="10dp"
    android:textColor="#0096ff"
    android:textSize="@dimen/mode_selector_text_size"
    android:visibility="gone" />

HDR默认值
res/values/dream_camera_arrays_photo_part.xml
<integer-array name="pref_camera_hdr_key_array">
    <item>@string/pref_camera_hdr_key</item>
    <item>@integer/storage_position_category_bf</item>
    <!--zhangqi modified begin-->
    <item>@string/preference_switch_item_default_value_auto</item>
    <!--zhangqi modified end-->
    <item>@array/pref_camera_hdr_entryvalues</item>
    <item>@array/pref_camera_hdr_entry</item>
</integer-array>

preference_switch_item_default_value_auto 这个值是在 res/values/dream_camera_strings_camera_part.xml

vendor/sprd/platform/packages/apps/DreamCamera2/src/com/android/camera/CameraModule.java

查看 hdr是否生效，可以在 log 中搜索 onHdrDetection
```## DreamCamera2默认缩略图图标

```text
vendor/sprd/platform/packages/apps/DreamCamera2/res/drawable-mdpi/ic_gallery_defult_sprd.png
vendor/sprd/platform/packages/apps/DreamCamera2/res/drawable-hdpi/ic_gallery_defult_sprd.png
vendor/sprd/platform/packages/apps/DreamCamera2/res/drawable-xhdpi/ic_gallery_defult_sprd.png
vendor/sprd/platform/packages/apps/DreamCamera2/res/drawable-xxhdpi/ic_gallery_defult_sprd.png
vendor/sprd/platform/packages/apps/DreamCamera2/res/drawable-xxxhdpi/ic_gallery_defult_sprd.png

CameraActivity.java
protected Bitmap getDefaultThumbnailBitmap(){
    Bitmap defaultBitmap = android.graphics.BitmapFactory.decodeResource(getResources(), R.drawable.ic_gallery_defult_sprd);
    return defaultBitmap;
}

安全相机缩略图图标
SecureCameraActivity.java
@Override
protected Bitmap getDefaultThumbnailBitmap(){
    Bitmap defaultBitmap = android.graphics.BitmapFactory.decodeResource(getResources(), R.drawable.ic_gallery_defult_security_camera_sprd);
    return defaultBitmap;
}
```## DreamCamera2缩略图点击

```text
vendor/sprd/platform/packages/apps/DreamCamera2/src/com/android/camera/app/CameraAppUI.java
public void initRoundedThumbnailView() {
    mRoundedThumbnailView = (RoundedThumbnailView) mCameraRootView
            .findViewById(R.id.rounded_thumbnail_view);
    mCounterInitRoundedThumbnailView.count();
    mRoundedThumbnailView.setCallback(new RoundedThumbnailView.Callback() {
        @Override
        public void onHitStateFinished() {
            if (mFilmstripView == null)
                return;

            if (mController.getCurrentModule().isShutterClicked()) {
                setBottomPanelLeftRightClickable(true);
                return;
            }
            if (mThumbUnClick) {
                CameraUtil.toastHint(mController, R.string.blur_process_toast);
                return;
            }
            if(mTakePictureCount.get() == 0){
                mController.doSometingWhenFilmStripShow();
            }
        }

        @Override
        public void onClick() {
            if(mTakePictureCount.get() == 0){
                setBottomPanelLeftRightClickable(false);
            }
        }
    });
}

private void launchGalleryPhoto() {
    if (null == mRedirectionUri) {
        mCameraAppUI.setBottomPanelLeftRightClickable(true);
        //return;
    }
    Intent startGallery = new Intent(CameraUtil.REVIEW_ACTION);
    startGallery.setData(mRedirectionUri);
    startGallery.putExtra("camera_album", true);
    startGallery.putExtra("secure_camera", mSecureCamera);
    /**
     * google photos requirement:intent should include the package para
     */
    if (mIsUsedGooglePhotos) {
        startGallery.setPackage(mPhotosPackageName);
    }
    if (mSecureCamera) {
          long[] securePhotoIds = new long[securePhotoList.size()];
          for (int i = 0; i < securePhotoList.size(); i++ ){
              securePhotoIds[i] = securePhotoList.get(i);
          }
          if (mIsUsedGooglePhotos) {
              startGallery.putExtra("com.google.android.apps.photos.api.secure_mode", true);
              startGallery.putExtra("com.google.android.apps.photos.api.secure_mode_ids", securePhotoIds);
          }else{
              startGallery.putExtra("secure_camera_Photo_ids", securePhotoIds);
        }
    }

    //Sprd:fix bug895543/948503
    try {
        startActivity(startGallery);
    } catch (ActivityNotFoundException e) {
        Log.i(TAG, "Failed to start intent=" + startGallery + ": " + e, e);
        CameraUtil.toastHint(this, R.string.goto_gallery_failed);
        mCameraAppUI.setBottomPanelLeftRightClickable(true);//SPRD:fix bug 1133118
    }
}

获取缩略图的URI
FilmstripItem item = mDataAdapter.getItemAt(mFilmstripController.getCurrentAdapterIndex());
if (item != null) {
    item.getData().getUri()
}

缩略图URI的格式
Intent { act=com.android.camera.action.REVIEW dat=content://media/external/images/media/78 pkg=com.google.android.apps.photosgo (has extras) }

imageCursor = getContentResolver().query(MediaStore.Images.Media.EXTERNAL_CONTENT_URI, new String[] { MediaStore.Images.ImageColumns._ID }, null, null, null);
videoCursor = getContentResolver().query(MediaStore.Video.Media.EXTERNAL_CONTENT_URI, new String[] { MediaStore.Video.VideoColumns._ID }, null, null, null);

点击锁屏相机中的缩略图跳转到gallery?
```## DreamCamera2判断是否是锁屏相机

```text
CameraActivity.java
if (INTENT_ACTION_STILL_IMAGE_CAMERA_SECURE.equals(action) || ACTION_IMAGE_CAPTURE_SECURE.equals(action)) {
    mSecureCamera = true;
} else {
    mSecureCamera = intent.getBooleanExtra(SECURE_CAMERA_EXTRA , false);
}
```## DreamCamera2判断是前摄还是后摄？

```text
boolean isFront = DataModuleManager.getInstance(mAppController.getAndroidContext()).getCurrentDataModule().getDataSetting().mIsFront;

有没有更好的方式？cameraId?
```## 触摸震动反馈

```text
1.Change mode - tap or swipe mode(mode in more modes).
2.Switch the front/rear camera.
3.Press and long press the shutter button (all mode).
While video is recording, doesn’t apply any haptic feedback.
Haptic occurs simultaneously with user behavior.

v.performHapticFeedback(android.view.HapticFeedbackConstants.LONG_PRESS);
```## DreamCamera2如何判断当前模式

```text
判断是否是缩时摄影？
String timeLapseMultipleStr = mDataModuleCurrent.getString(Keys.KEY_VIDEO_TIME_LAPSE_FRAME_INTERVAL);
if (timeLapseMultipleStr == null) {
    return;
}
int mTimeLapseMultiple = Integer.parseInt(timeLapseMultipleStr);
boolean mCaptureTimeLapse = (mTimeLapseMultiple != 1);

or:
if (mActivity.getCurrentModuleIndex() == com.android.camera.settings.SettingsScopeNamespaces.TIMELAPSE)
```## DreamCamera2修改前后摄都支持缩时摄像

```text
vendor/sprd/platform/packages/apps/DreamCamera2/res/values/arrays.xml
<array name="timelapse_module">
    <item>11</item> <!-- module id-->
    <item>@integer/mode_is_visible</item> <!-- should be shown-->
    <!--zhangqi modified for support front+back all-->
    <item>@integer/camera_support_all</item> <!-- front or back config-->   
    <!--zhangqi modified for support front+back all-->
    <item>@integer/mode_support_video</item> <!-- video or module-->
    <item>TimelapseModule</item> <!--namesapce -->
    <item>@string/mode_timelapse</item> <!-- text -->
    <item>@string/mode_timelapse</item> <!--description-->
    <item>@drawable/ic_time_lapse_mode_unisoc</item> <!-- unselect icon-->
    <item>@drawable/ic_time_lapse_mode_unisoc</item> <!-- select icon-->
    <item>@drawable/ic_time_lapse_blanket</item> <!-- cover -->
    <!--Redmine53792 zhangqi modified for video button icon 2020/11/21:begin-->
    <item>@drawable/btn_shutter_video_nokia</item> <!--capture icon-->
    <!--Redmine53792 zhangqi modified for video button icon 2020/11/21:end-->
</array>

有如下几个参数可以配置，顾名思义
<integer name="camera_support_all">-1</integer>
<integer name="camera_support_back">0</integer>
<integer name="camera_support_front">1</integer>
<integer name="camera_support_none">999</integer>
```## DreamCamera2 TimeLapse默认值

```text
vendor/sprd/platform/packages/apps/DreamCamera2/res/values/dream_camera_arrays_video_part.xml
<integer-array name="pref_video_time_lapse_frame_interval_with_close_key_array">
    <item>@string/pref_video_time_lapse_frame_interval_key</item>
    <item>@integer/storage_position_category_bf</item>
    <item>@string/default_timelapse_without_close</item>
    <item>@array/pref_video_timelapse_without_close_entry_values</item>
    <item>@array/pref_video_timelapse_without_close_entries</item>
</integer-array>
<string name="default_timelapse_without_close" translatable="false">15</string>     默认15秒
```## DreamCamera2 修改 TimeLapse 不支持缩放

```text
vendor/sprd/platform/packages/apps/DreamCamera2/res/values/dream_camera_arrays_video_part.xml
<integer-array name="video_back_mode_time_lapse_setting">
    <item>@array/pref_video_quality_back_key_array</item>
    <item>@array/pref_video_composition_line_without_box_key_array</item>
    <item>@array/pref_video_whitebalance_key_array</item>
    <item>@array/pref_video_antibanding_key_array</item>
    <item>@array/pref_video_time_lapse_frame_interval_with_close_key_array</item>
    <item>@array/pref_video_flashmode_key_array</item>
    <!--Redmine53886 zhangqi modified for time-lapse can not support zoom change function 2020/11/28:begin-->
    <item>@array/pref_camera_zoom_enable_false_key_array</item>
    <!--Redmine53886 zhangqi modified for time-lapse can not support zoom change function 2020/11/28:end-->
</integer-array>

有如下两种参数可以配置，顾名思义
pref_camera_zoom_enable_false_key_array
pref_camera_zoom_enable_true_key_array
```## DreamCamera2 TimeLapse拍摄按钮动画

```text
vendor/sprd/platform/packages/apps/DreamCamera2/src/com/android/camera/VideoModule.java
View btn_record = mActivity.findViewById(R.id.shutter_button);
if (btn_record instanceof ShutterButton) {
    btn_record.setForeground(mActivity.getDrawable(R.drawable.super_slow_stop_to_recording));
    if (btn_record.getForeground() instanceof AnimatedVectorDrawable) {
        ((AnimatedVectorDrawable)btn_record.getForeground()).registerAnimationCallback(new Animatable2.AnimationCallback() {
            @Override
            public void onAnimationEnd(Drawable drawable) {
                super.onAnimationEnd(drawable);
                btn_record.setForeground(mActivity.getDrawable(R.drawable.super_slow_start_to_recording));
                if (btn_record.getForeground() instanceof AnimatedVectorDrawable) {
                    ((AnimatedVectorDrawable)btn_record.getForeground()).reset();
                    ((AnimatedVectorDrawable)btn_record.getForeground()).registerAnimationCallback(new Animatable2.AnimationCallback() {
                        @Override
                        public void onAnimationEnd(Drawable drawable) {
                            super.onAnimationEnd(drawable);
                            if (btn_record.getBackground() instanceof AnimatedVectorDrawable) {
                                if (isRecording()) {
                                    ((AnimatedVectorDrawable)btn_record.getBackground()).start();
                                } else {
                                    ((AnimatedVectorDrawable)btn_record.getBackground()).reset();
                                }
                            }
                        }
                    });
                }
                if (btn_record.getBackground() instanceof AnimatedVectorDrawable) {
                    ((AnimatedVectorDrawable)btn_record.getBackground()).registerAnimationCallback(new Animatable2.AnimationCallback() {
                        @Override
                        public void onAnimationEnd(Drawable drawable) {
                            super.onAnimationEnd(drawable);
                            if (btn_record.getBackground() instanceof AnimatedVectorDrawable) {
                                if (isRecording()) {
                                    ((AnimatedVectorDrawable)btn_record.getBackground()).start();
                                } else {
                                    ((AnimatedVectorDrawable)btn_record.getBackground()).reset();
                                }
                            }
                        }
                    });
                }
            }
        });
        ((AnimatedVectorDrawable)btn_record.getForeground()).start();
    }
    if (btn_record.getBackground() instanceof AnimatedVectorDrawable) {
        ((AnimatedVectorDrawable)btn_record.getBackground()).reset();
    }
}

这里写的过于复杂，使用了多重监听(回调地狱，能否用协程解决？)，感觉有优化的空间？
```## View的动画监听器

```text
animate().alpha(0f).setDuration(500).setListener(new Animator.AnimatorListener() {
    @Override
    public void onAnimationStart(Animator animation) {
    }
    @Override
    public void onAnimationEnd(Animator animation) {
        ZoomPanel.super.setVisibility(View.GONE);
        setAlpha(1f);
    }
    @Override
    public void onAnimationCancel(Animator animation) {
    }
    @Override
    public void onAnimationRepeat(Animator animation) {
    }
});
```## DreamCamera2保存Camera设置的值

```text
DataModuleManager.getInstance(context).getDataModuleCamera().set(Keys.KEY_RECORD_LOCATION, true);
```## DreamCamera2适配相机全面屏

```text
http://192.168.3.78:7080/c/SPRD_Q/MOCORDROID10_Trunk_19C_PATCH_W20.26.2/+/46232
```## DreamCamera2设置 Camera 可以在 RecentsApp 中截屏

```text
vendor/sprd/platform/packages/apps/DreamCamera2/src/com/android/camera/util/QuickActivity.java
setDisablePreviewScreenshots(false);
```## DreamCamera2如何设置当前模式

```text
vendor/sprd/platform/packages/apps/DreamCamera2/src/com/android/camera/app/CameraAppUI.java
mModeScrollView.setCurrentIndex(index, false);
```## DreamCamera2左右滑动切换模式

```text
vendor/sprd/platform/packages/apps/DreamCamera2/src/com/android/camera/app/CameraAppUI.java
private boolean doGestureScrollActionMove(int deltaX,int deltaY){
    if (Math.abs(deltaX) > mSlop || Math.abs(deltaY) > mSlop) {
        // Calculate the direction of the swipe.
        if (deltaX >= Math.abs(deltaY)) {
            if (mModeListView == null || mModeListView.getModeListSize() == 1) {
                return false;
            }
            // Swipe right.
            if (mDreamUI != null && !mDreamUI.isFreezeFrameShow()) {
                setSwipeState(SWIPE_RIGHT);
            }
        } else if (deltaX <= -Math.abs(deltaY)) {
            // Swipe left.
            if (mController != null) {
                // SPRD Bug:607389 if zoomPanel visible, can not swith to DreamFilterModule
                if (mZoomPanel != null && (mZoomPanel.isZoomSimple() && mZoomPanel.getVisibility() == View.VISIBLE)) {
                    //return false;
                }
                setSwipeState(SWIPE_LEFT);
            }
        }
    }
    return true;
}
```## DreamCamera2设置打开Camera默认选中的模式

```text
vendor/sprd/platform/packages/apps/DreamCamera2/src/com/dream/camera/ui/ModeScrollView.java
mHVSCurrentIndex = CameraUtil.mModuleInfoResovle.getModuleScrollAdapterIndex(((com.android.camera.CameraActivity) getContext()).getCurrentModuleIndex());
```## 显示屏幕提示

```text
OnScreenHint.makeText(CameraActivity.this, getString(R.string.toast_memory_update_success)).showTime();
```## 如何获取某个ratio下的最大分辨率？

```text
vendor/sprd/platform/packages/apps/DreamCamera2/src/com/dream/camera/ButtonManagerDream.java

List<Size> supportedPictureSizes = CameraPictureSizesCacher.getSizesForCamera(isFront ? 1 : 0, mAppController.getAndroidContext());
supportedPictureSizes = ResolutionUtil.getDisplayableSizesFromSupported(supportedPictureSizes, !isFront);
supportedPictureSizes = ResolutionUtil.filterBlackListedSizes(supportedPictureSizes, GservicesHelper.getBlacklistedResolutionsBack(null));
index43 = ResolutionUtil.getLargestSizeIndex(ResolutionUtil.ASPECT_RATIO_4x3, supportedPictureSizes);
index169 = ResolutionUtil.getLargestSizeIndex(ResolutionUtil.ASPECT_RATIO_16x9, supportedPictureSizes);
index11 = ResolutionUtil.getLargestSizeIndex(ResolutionUtil.ASPECT_RATIO_1x1, supportedPictureSizes);
indexFull = ResolutionUtil.getLargestSizeIndex(ResolutionUtil.getFullScreenAspectRatio(), supportedPictureSizes);
```## DreamCamera2 CameraUtil.java

```text
里面有很多 persist 开关
private final static String TARGET_TS_AUTO_TO_PORTRAIT_DEFAULT_NUMBER = "persist.sys.cam.auto_to_portrait";
private final static String TARGET_TS_PORTRAIT_TO_AUTO_DEFAULT_NUMBER = "persist.sys.cam.portrait_to_auto";
private final static String TARGET_TS_AUTO_TO_3DNR_DEFAULT_NUMBER = "persist.sys.cam.auto_to_3dnr";
private final static String TARGET_TS_3DNR_TOPO_AUTO_DEFAULT_NUMBER = "persist.sys.cam.3dnr_to_auto";
private final static String TARGET_TS_BURST_NINETYNINE_ENABLE = "persist.sys.cam.ninetynine";
private final static String TARGET_TS_ZSL_BURST_ENABLE = "persist.sys.cam.burst";
private final static String TARGET_TS_ZSL_ENABLE = "persist.sys.cam.zsl";
private final static String TARGET_TS_FRONT_CAMERA_MIRROR_ENABLE = "persist.front.camera.mirror";
private final static String TARGET_COLOR_EFFECT_ENABLE = "persist.sys.cam.color";
private final static String TARGET_CONTINUE_PHOTO_ENABLE = "persist.sys.cam.continue_photo";
private final static String TARGET_INTERVAL_PHOTO_ENABLE = "persist.sys.cam.interval";
private final static String TARGET_SLOW_MOTION_ENABLE = "persist.sys.cam.slow_motion";
private final static String TARGET_TIME_LAPSE_ENABLE = "persist.sys.cam.time_lapse";
private final static String TARGET_IS_TOUCH_PHOTO = "persist.sys.cam.touchphoto";
private final static String TARGET_CAMERA_VOICE_PHOTO_ENABLE = "persist.sys.cam.voicephoto";
private final static String TARGET_CAMERA_BURST_ALBUM_ENABLE = "presist.sys.cam.burstalbum";
private final static String TARGET_RECORD_LOCATION_ENABLE = "persist.sys.cam.gps";
private final static String TARGET_FREEZE_DISPLAY_ENABLE = "persist.sys.cam.freeze_display";
private final static String TARGET_ZOOM_PANEL_ENABLE = "persist.sys.cam.zoom_panel";
private final static String TARGET_AI_DETECT_ENABLE = "persist.sys.cam.ai_detect";
private final static String TARGET_MANUAL_CONTROL_SHUTTER_ENABLE = "persist.sys.cam.manual.shutter";
private final static String TARGET_MANUAL_CONTROL_FOCUS_ENABLE = "persist.sys.cam.manual.focus";
private final static String TARGET_SMILE_THRESHOLD = "persist.sys.cam.smile.thr";
private final static String TARGET_PORTRAIT_DEFAULT_FNUMBER = "persist.sys.cam.potrait.fnumber";
private final static String TARGET_FILTER_VIDEO_ENABLE = "persist.sys.cam.filtervideo.enable";

通过 getprop 命令查看配置了哪些值
adb shell getprop | grep "persist.sys.cam"
```## 连拍的弹出框Toast

```text
vendor/sprd/platform/packages/apps/DreamCamera2/res/layout/continuephoto_extend_panel.xml
<TextView
    android:id="@+id/capture_already"
    android:layout_width="30dp"
    android:layout_height="30dp"
    android:layout_gravity="bottom"
    android:text="@string/capture_0"
    style="@style/DreamText"
    android:textColor="#000000"
    android:gravity="center"
    android:background="@drawable/bg_circle_white"
    android:textSize="14dp" />

需要改成客户想要的样式
```## 全景拍照如何判断是否拍摄成功？

```text
vendor/sprd/platform/packages/apps/DreamCamera2/src/com/sprd/camera/panora/MosaicFrameProcessor.java
WideAnglePanoramaModule.java
http://192.168.3.78:7080/c/SPRD_R/MOCORDROIDR_Trunk_W20.36.4/+/42758
```## 亮度调节功能

```text
需求如下
1. Adaptive brightness is off (Settings), keep the brightness value that users set, don’t change anything in Camera. - Need to fixed.
2. Adaptive brightness is on (Settings), if the brightness value < 30% (ex. the brightness is 5%), need to keep it as 30%, when users exit Camera,
back to the value before users launching Camera (5% brightness).
3. Adaptive brightness is on (Settings), if the brightness value < 30%(ex. the brightness is 5%), need to keep it as 30%, but if users change the brightness by themselves(ex. 85%), need to save the value users set (85% brightness) even if the users exit Camera. - Need to fixed.

vendor/sprd/platform/packages/apps/DreamCamera2/src/com/android/camera/CameraActivity.java
http://192.168.3.78:7080/c/SPRD_R/MOCORDROIDR_Trunk_W20.36.4/+/45759
```## DreamCamera2权限对话框

```text
only this time:
https://stackoverflow.com/questions/64464661/android-11-only-this-time-permission-behavior

/data/misc_de/0/apexdata/com.android.permission/runtime-permissions.xml

没授权
<package name="com.android.camera2">
    <permission name="android.permission.ACCESS_FINE_LOCATION" granted="false" flags="300" />
    <permission name="android.permission.READ_EXTERNAL_STORAGE" granted="true" flags="33a0" />
    <permission name="android.permission.ACCESS_COARSE_LOCATION" granted="false" flags="300" />
    <permission name="android.permission.CAMERA" granted="true" flags="320" />
    <permission name="android.permission.WRITE_EXTERNAL_STORAGE" granted="true" flags="3320" />
    <permission name="android.permission.RECORD_AUDIO" granted="true" flags="320" />
</package>
仅限这一次
<package name="com.android.camera2">
    <permission name="android.permission.ACCESS_FINE_LOCATION" granted="false" flags="10301" />
    <permission name="android.permission.READ_EXTERNAL_STORAGE" granted="true" flags="33a0" />
    <permission name="android.permission.ACCESS_COARSE_LOCATION" granted="false" flags="10301" />
    <permission name="android.permission.CAMERA" granted="true" flags="320" />
    <permission name="android.permission.WRITE_EXTERNAL_STORAGE" granted="true" flags="3320" />
    <permission name="android.permission.RECORD_AUDIO" granted="true" flags="320" />
</package>
授权
<package name="com.android.camera2">
    <permission name="android.permission.ACCESS_FINE_LOCATION" granted="true" flags="301" />
    <permission name="android.permission.READ_EXTERNAL_STORAGE" granted="true" flags="33a0" />
    <permission name="android.permission.ACCESS_COARSE_LOCATION" granted="true" flags="301" />
    <permission name="android.permission.CAMERA" granted="true" flags="320" />
    <permission name="android.permission.WRITE_EXTERNAL_STORAGE" granted="true" flags="3320" />
    <permission name="android.permission.RECORD_AUDIO" granted="true" flags="320" />
</package>
```## DreamCamera2 SPRD人像模式配置

```text
https://unisupport.unisoc.com/faq/getFaqDetialView?id=72623
DreamCamera2如何配置人像模式？

[ANSWER]
修改md.mk文件
路径形如：device/sprd/sharkl5Pro/【yourboard】/module/camera/md.mk
1.只配置前单摄人像：
#camera dual sensor
TARGET_BOARD_CAMERA_DUAL_SENSOR_MODULE := true
#BOKEH feature
TARGET_BOARD_BOKEH_MODE_SUPPORT := true
#portrait_single
TARGET_BOARD_PORTRAIT_SINGLE_SUPPORT :=true

persist.vendor.cam.fr.blur.version=1
#ip feature list
#enablefront portrait mode
PRODUCT_PROPERTY_OVERRIDES +=persist.vendor.cam.fr.portrait.enable =1

2. 如要配置前单+后双摄人像：
#camera dual sensor
TARGET_BOARD_CAMERA_DUAL_SENSOR_MODULE := true
#BOKEH feature
TARGET_BOARD_BOKEH_MODE_SUPPORT := true
#portrait_single
TARGET_BOARD_PORTRAIT_SINGLE_SUPPORT :=true

persist.vendor.cam.fr.blur.version=1
persist.vendor.cam.ba.blur.version=6    //单摄1，双摄6
#ip feature list
#enablefront portrait mode
PRODUCT_PROPERTY_OVERRIDES +=persist.vendor.cam.fr.portrait.enable =1
PRODUCT_PROPERTY_OVERRIDES +=persist.vendor.cam.ba.portrait.enable =1

3. 如要配置前单+后单摄人像：
#camera dual sensor
TARGET_BOARD_CAMERA_DUAL_SENSOR_MODULE := true
#BOKEH feature
TARGET_BOARD_BOKEH_MODE_SUPPORT := true
#portrait_single
TARGET_BOARD_PORTRAIT_SINGLE_SUPPORT :=true

persist.vendor.cam.fr.blur.version=1
persist.vendor.cam.ba.blur.version=1   //单摄1，双摄6
persist.sys.cam.fast.blur=false     //后单摄人像需设置fast.blur为false
#ip feature list
#enablefront portrait mode
PRODUCT_PROPERTY_OVERRIDES +=persist.vendor.cam.fr.portrait.enable =1
PRODUCT_PROPERTY_OVERRIDES +=persist.vendor.cam.ba.portrait.enable =1

补充一点：针对go版本的机器，由于系统会先读取md.mk，再读取go1g.mk或go2g.mk文件，因此只需要配置一个.mk文件即可，否则有可能会覆盖导致配置导致出错。go2g.mk文件参考路径：device/sprd/sharkl3/M19966AA1/module/camera/mversion/go/go2g/go2g.mk

修改人像模式后摄最大分辨率
alps/vendor/sprd/modules/libcamera/hal_common/multiCamera/SprdCamera3MultiBase.cpp
{RES_12M, {{4160, 3120}, {960, 720}, {320, 240}}},
```## DreamCamera2中，如何配置前摄屏幕补光（LCD）？

```text
一、问题背景
在处理问题过程中，有客户提到如何配置前摄屏幕补光（LCD）问题，特此说明一下配置方法。LCD的使用场景是：前摄在暗环境下拍照时，通过自动打闪的方式对黑暗环境进行补光。暗环境的环境亮度对应一个阈值范围，当处于这个阈值范围时，会自动出发LCD功能，阈值范围可在效果参数中设置。

二、底层设置
xref: /sprdroidr_trunk/device/sprd/sharkl5Pro/ums512_1h10/module/camera/md.mk

74 #lcd,led,flash
75 TARGET_BOARD_FRONT_CAMERA_FLASH_TYPE := lcd //配置前摄屏幕补光
76 #Range of value 0~31
77 CAMERA_TORCH_LIGHT_LEVEL := 16
三、上层设置（DreamCamera2）
上层前摄Flash Mode是从底层读取的，默认是开启的，只要底层设置了lcd，就会设置lcd，无需配置。

DreamCamera2/src/com/android/camera/util/CameraUtil.java

2039mFrontFlashMode = featureList[FeatureTagID.FRONTFLASHMODE.ordinal()]; //从底层读取前摄Flash Mode

DreamCamera2/portability/src/com/android/ex/camera2/portability/AndroidCamera2Settings.java

369          if (mCurrentFlashType == VALUE_FRONT_FLASH_MODE_LED) {
370              //set flash mode for led
371              mRequestSettings.set(CONTROL_AE_MODE, aeMode);
372              mRequestSettings.set(FLASH_MODE, flashMode);
373          } else {
374              //set flash mode for lcd 设置前摄屏幕补
375              mRequestSettings.set(SprdCaptureRequest.ANDROID_SPRD_FLASH_LCD_MODE,(byte)flashLcdMode);
376          }
377  
378      }
```

## DreamCamera2 相机模式与底部滑动栏

```text
DreamCamera2 AndroidR 相机模式与底部滑动栏
一、模式注册与添加
在DreamCamera2\src\com\android\camera\CameraActivity.java的onCreateTasks (Bundle state)中会调用模式初始化的线程：
THREAD_POOL_EXECUTOR.execute(mOncreateModulesInfoAndCurrentModule);
通过CameraUtil.mModuleInfoResovle来获得模式解析结果
public ModuleInfoResolve() {
    mVisibleModuleList = new ArrayList<>();    //可见模式列表
    mModuleInfo = new HashMap<>();          //模式信息
    mModuleScrollInfo = new HashMap<>();      //滑动栏模式信息
}

然后调用ModuleInfoResolve.java来进行模式解析
CameraUtil.mModuleInfoResovle.resolve(mAppContext);    //模式解析
然后通过initModuleInfoFromArray(context);来获取R.array.module_list中的所有模式信息
通过buildModeSlideList();  //建立滑动栏的模式名单
通过buildNonMainList();    //建立模式列表的模式名单（更多）
通常来说滑动栏的模式名单只有7个，这个个数可以通过设置panelRequireSize来进行修改。模式的顺序可以通过调整slideshow_standard来进行实现。没有在滑动栏的模式会自动出现在模式列表中。
通过调用ModuleManagerImpl.java中的getRegisteredModuleAgents()来获取注册过的模式，完成模式注册。通过调用getSupportedModeIndexList()来实现模式图标的现实。

二、底部滑动栏
（1）底部滑动栏UI初始化
图1 底部模式滑动栏组成
相关文件：
1. AutoCenterHorizontalScrollView.java
2. HorizontalAdapter.java
3. ModeScrollAdapter.java
4. ModeScrollView.java
5. CameraAppUI.java
在1. AutoCenterHorizontalScrollView.java中通过RecyclerView使得布局能够平均分布
public static interface HAdapter {
    int getCount();
    RecyclerView.ViewHolder getItemView(int position);
    void onSelectStateChanged(RecyclerView.ViewHolder itemView,int position,boolean isSelected);
}

然后设置setAdapter（final HAdapter adapter）方法来添加控过2. HorizontalAdapter.java和3. ModeScrollAdapter.java来对控件名称进行赋值和属性设置
通过4. ModeScrollView.java的方法来进行布局的初始化
public void setAdapter(final ModeScrollAdapter adapter) {
    if(adapter == null || adapter.getCount() == 0){
        return;
    }
    mViewHolders.clear();
    removeAllViews();
    LinearLayout linearLayout = new LinearLayout(getContext());
    linearLayout.setVerticalGravity(Gravity.CENTER);
    int size = adapter.getCount();
    for (int i = 0; i < size; i++) {
        mViewHolders.add(adapter.getItemView(i));
        mViewHolders.get(i).itemView.setTag(i);
        mViewHolders.get(i).itemView.setOnClickListener(ModeScrollView.this);
        linearLayout.addView(mViewHolders.get(i).itemView);
    }
    this.mAdapter = adapter;
    addView(linearLayout);
    init();
}

最终在5. CameraAppUI.java中进行调用实现
private void initHorizontalModeScroll() {
    if(initModeScrollEnd || mIsCaptureIntent) return;
    mModeScrollView = (ModeScrollView) mAppRootView.findViewById(R.id.bottom_mode_switch);
    mModeTagShowLayout = (LinearLayout) mAppRootView.findViewById(R.id.bottom_modeid_show_layout);
    if (null == mModeScrollView || null == mModeTagShowLayout) return;
    mModeScrollView.setEdgeEffectColor(Color.BLUE);
    ArrayList<String> mModuleNameList = new ArrayList();
    boolean secureCam = mController.isSecureCamera();
    if (secureCam) {
        mModuleNameList.add(CameraUtil.mModuleInfoResovle.getModuleText(SettingsScopeNamespaces.AUTO_PHOTO));
        mModuleNameList.add(CameraUtil.mModuleInfoResovle.getModuleText(SettingsScopeNamespaces.AUTO_VIDEO));
    } else {
        ArrayList<Integer> panelShowList = CameraUtil.mModuleInfoResovle.getModeSlideList();
        int panelSize = panelShowList.size() >= 7 ? 7 : panelShowList.size();
        for (int i = 0; i < panelSize; i++) {
            String name = CameraUtil.mModuleInfoResovle.getModuleText(panelShowList.get(i));
            mModuleNameList.add(name);    //初始化滑动栏模式列表
        }
    }
    ModeScrollAdapter hAdapter = new ModeScrollAdapter(mController, mModuleNameList);
    mModeScrollView.setHandler(mController.getMainHandler());
    mModeScrollView.setCurrentIndex(secureCam ? 0 : CameraUtil.mModuleInfoResovle.getModuleScrollAdapterIndex(mController.getCurrentModuleIndex()), false);
    mModeScrollView.setAdapter(hAdapter);     //滑动栏初始化
    ...
}
以上是UI部分的初始化，主要和上述5个JAVA文件有关。

（2）滑动栏模式切换流程
点击或左右滑动切换模式流程图如图2所示，共有两次位置更新。第一次点击或滑动切换模式，第一次滑动栏位置更新，滑动条滑动到smoothToPosition。进入新模式，重启预览，更新底部模式滑动栏，第二次滑动栏位置更新。
```## 使用DreamCamera2录像，播放没有声音，录音功能正常，使用第三方应用录像，播放有声音

```text
请先检查贵司是否为单mic，如果是，则删除副mic配置，primary_audio_policy_configuration.xml
删除以下内容：
<item>Built-In Back Mic</item>
<devicePort tagName="Built-In Back Mic" type="AUDIO_DEVICE_IN_BACK_MIC" role="source">
    <profile name="" format="AUDIO_FORMAT_PCM_16_BIT"
             samplingRates="8000,11025,12000,16000,22050,24000,32000,44100,48000"
             channelMasks="AUDIO_CHANNEL_IN_MONO,AUDIO_CHANNEL_IN_STEREO,AUDIO_CHANNEL_IN_FRONT_BACK"/>
</devicePort>

修改以下内容：
<route type="mix" sink="primary input"
       sources="Built-In Mic,Built-In Back Mic,Wired Headset Mic,BT SCO Headset Mic"/>  //Built-In Back Mic修改为Wired Headset Mic
<route type="mix" sink="Telephony Tx"
       sources="Built-In Mic,Built-In Back Mic,Wired Headset Mic,BT SCO Headset Mic"/>  //Built-In Back Mic修改为Wired Headset Mic

Android 10 
\device\sprd\对应工程\对应项目\rootdir\system\etc\audio_policy_config\primary_audio_policy_configuration.xml
Android 11
\device\sprd\mpool\module\audio\system\etc\audio_policy_config\primary_audio_policy_configuration.xml
```## Camera内存占用问题

```text
我们都知道, Camera App和CameraService是两个进程, App内存占用大家一般用Android Studio就能看到, 但如果我们在HAL层加入了一些修改, 要看内存占用, 这个时候就需要看CameraService的内存占用了, CameraService调用HAL层接口, 所以HAL层内存占用就体现在CameraService中, 要找到CameraService的进程, 可通过如下方法:
Android 7.1及以下版本

adb shell ps | grep -i camera
//高通Android 7.1.1, 输出如下:
cameraserver 371   1     20456  2240  binder_thr a84b396c S /system/bin/cameraserver
camera    401   1     73188  3404  poll_sched ab1a8a6c S /system/bin/mm-qcamera-daemon
可以看到和Camera相关的进程有两个, 一个是我们要找的CameraService,名称为cameraserver
另一个就高通的Camera守护进程qcamera-daemon
找到进程后, 查看内存就简单了,也是通过dumpsys来查看(meminfo后面也可以使用pid作为参数):

adb shell dumpsys meminfo cameraserver
```## 修改闪光灯的显示UI

```text
feature/setting/flash/src/com/mediatek/camera/feature/setting/flash/FlashViewController.java
```## 缩略图相关文件

```text
BitmapCreator.java

ThumbnailViewManager.java

media数据库
adb pull /data/data/com.android.providers.media.module/databases/external.db

select * from files where ((media_type=1 OR media_type=3 ) AND ( bucket_id=-1739773001 OR bucket_id=-1817509755)) order by _id ASC;

视频缩略图流程
```## 看懂光圈、快门、感光度的意义

```text
光圈越大，参照物越模糊。
快门越高，运动物越清晰。
感光度越大，照片糙点越多。
```## YUV

```text
https://mp.weixin.qq.com/s?__biz=MzUyOTA2MjA2NQ==&mid=2247483877&idx=1&sn=06b7296d19c3edf96a49b1b0a288b6b1&chksm=fa67803bcd10092d4631be81900e91ff15083e4ef28d121274d2ec3cc692018ceca13995d632&scene=0&xtrack=1&key=7865e1e5a7ba115ec737c955c34dd90271207e03cf02d71abfb3f179ac4458ae35883bc97eccc0a80c0f621e6f3495b61fc0d8d9f3352b646b88959e0090d0df2006e7e1663b51113f6fad1c93f1e004&ascene=1&uin=MTQzOTAxMDg4MA%3D%3D&devicetype=Windows+10&version=62060844&lang=zh_CN&pass_ticket=PxMajixtG4%2F1z9KAWqxn%2B7aMeu95XL6KXXPjRFfctJu2Mn3D0Hff6FIAZiyzR5dZ

YUV 编码采用了明亮度和色度表示每个像素的颜色。

Y 表示明亮度（Luminance、Luma），也就是灰阶值。
U、V 表示色度（Chrominance 或 Chroma），描述的是色调和饱和度。

YCbCr 其实是 YUV 经过缩放和偏移的翻版。其中 Y 与 YUV 中的 Y 含义一致,Cb,Cr 同样都指色彩，只是在表示方法上不同而已。YCbCr 其中 Y 是指亮度分量，Cb 指蓝色色度分量，而 Cr 指红色色度分量。

YUV 优点
对于 YUV 所表示的图像，Y 和 UV 分量是分离的。如果只有 Y 分量而没有 UV 分离，那么图像表示的就是黑白图像。彩色电视机采用的就是 YUV 图像，解决与和黑白电视机的兼容问题，使黑白电视机也能接受彩色电视信号。

人眼对色度的敏感程度低于对亮度的敏感程度。主要原因是视网膜杆细胞多于视网膜锥细胞，其中视网膜杆细胞的作用就是识别亮度，视网膜锥细胞的作用就是识别色度。所以，眼睛对于亮度的分辨要比对颜色的分辨精细一些。

利用这个原理，可以把色度信息减少一点，人眼也无法查觉这一点。

所以，并不是每个像素点都需要包含了 Y、U、V 三个分量，根据不同的采样格式，可以每个 Y 分量都对应自己的 UV 分量，也可以几个 Y 分量共用 UV 分量。相比 RGB，能够节约不少存储空间。

YUV 图像的主流采样方式有如下三种：
YUV 4:4:4 采样，表示 Y、U、V 三分量采样率相同，即每个像素的三分量信息完整，都是 8bit，每个像素占用 3 个字节。
YUV 4:2:2 采样
YUV 4:2:0 采样

四个像素为： [Y0 U0 V0] [Y1 U1 V1] [Y2 U2 V2] [Y3 U3 V3]
采样的码流为：Y0 U0 V0 Y1 U1 V1 Y2 U2 V2 Y3 U3 V3
映射出的像素点为：[Y0 U0 V0] [Y1 U1 V1] [Y2 U2 V2] [Y3 U3 V3]
可以看到这种采样方式与 RGB 图像大小是一样的。

YUV 4:2:2
YUV 4:2:2 表示 UV 分量的采样率是 Y 分量的一半。

如下图所示：

四个像素为： [Y0 U0 V0] [Y1 U1 V1] [Y2 U2 V2] [Y3 U3 V3]
采样的码流为：Y0 U0 Y1 V1 Y2 U2 Y3 U3
映射出的像素点为：[Y0 U0 V1]、[Y1 U0 V1]、[Y2 U2 V3]、[Y3 U2 V3]
其中，每采样一个像素点，都会采样其 Y 分量，而 U、V 分量都会间隔采集一个，映射为像素点时，第一个像素点和第二个像素点共用了 U0、V1 分量，以此类推。从而节省了图像空间。

比如一张 1920 * 1280 大小的图片，采用 YUV 4:2:2 采样时的大小为：

(1920 * 1280 * 8 + 1920 * 1280 * 0.5 * 8 * 2 ) / 8 / 1024 / 1024 = 4.68M

可以看出，比 RGB 节省了三分之一的存储空间。

YUV 4:2:0
YUV 4:2:0 并不意味着不采样 V 分量。它指的是对每条扫描线来说，只有一种色度分量以 2:1 的采样率存储，相邻的扫描行存储不同的色度分量。也就是说，如果第一行是 4:2:0，下一行就是 4:0:2，在下一行就是 4:2:0，以此类推。

如下图所示：

图像像素为：
[Y0 U0 V0]、[Y1 U1 V1]、 [Y2 U2 V2]、 [Y3 U3 V3]
[Y5 U5 V5]、[Y6 U6 V6]、 [Y7 U7 V7] 、[Y8 U8 V8]

采样的码流为：
Y0 U0 Y1 Y2 U2 Y3
Y5 V5 Y6 Y7 V7 Y8

映射出的像素点为：
[Y0 U0 V5]、[Y1 U0 V5]、[Y2 U2 V7]、[Y3 U2 V7]
[Y5 U0 V5]、[Y6 U0 V5]、[Y7 U2 V7]、[Y8 U2 V7]
其中，每采样一个像素点，都会采样 Y 分量，而 U、V 分量都会隔行按照 2:1 进行采样。

一张 1920 * 1280 大小的图片，采用 YUV 4:2:0 采样时的大小为：

(1920 * 1280 * 8 + 1920 * 1280 * 0.25 * 8  * 2 ) / 8 / 1024 / 1024 = 3.51M

相比 RGB，节省了一半的存储空间。

YUV 存储格式
YUV 数据有两种存储格式：平面格式（planar format）和打包格式（packed format）。

planar format：先连续存储所有像素点的 Y，紧接着存储所有像素点的 U，随后是所有像素点的 V。
packed format：每个像素点的 Y、U、V 是连续交错存储的。

因为不同的采样方式和存储格式，就会产生多种 YUV 存储方式，这里只介绍基于 YUV422 和  YUV420 的存储方式。

YUYV
YUYV 格式属于 YUV422，采用打包格式进行存储，Y 和 UV 分量按照 2:1 比例采样，每个像素都采集 Y 分量，每隔一个像素采集它的 UV 分量。

Y0 U0 Y1 V0 Y2 U2 Y3 V2

Y0 和 Y1 共用 U0 V0 分量，Y2 和 Y3 共用 U2 V2 分量。

UYVY
UYVY 也是 YUV422 采样的存储格式中的一种，只不过与 YUYV 排列顺序相反。

U0 Y0 V0 Y1 U2 Y2 V2 Y3

YUV422P 属于 YUV422 的一种，它是一种 planer 模式，即 Y、U、V 分别存储。

YUV420P 是基于 planar 平面模式进行存储，先存储所有的 Y 分量，然后存储所有的 U 分量或者 V 分量。
YUV420SP 也是基于 planar 平面模式存储，与 YUV420P 的区别在于它的 U、V 分量是按照 UV 或者 VU 交替顺序进行存储。

YU12 和 YV12 格式都属于 YUV 420P 类型，即先存储 Y 分量，再存储 U、V 分量，区别在于：YU12 是先 Y 再 U 后 V，而 YV12 是先 Y 再 V 后 U 。
NV12 和 NV21 格式都属于 YUV420SP 类型。它也是先存储了 Y 分量，但接下来并不是再存储所有的 U 或者 V 分量，而是把 UV 分量交替连续存储。
NV12 是 IOS 中有的模式，它的存储顺序是先存 Y 分量，再 UV 进行交替存储。
NV21 是 安卓 中有的模式，它的存储顺序是先存 Y 分量，在 VU 交替存储。

YUV 与 RGB 转换
YUV 与 RGB 之间的转换，就是将图像所有像素点的 R、G、B 分量和 Y、U、 分量相互转换。
```## 颜色模型

```text
颜色模型包括HSB（色相、饱和度、亮度）、RGB（红色、绿色、蓝色）、CMYK（青色、品红、黄色、黑色）和CIE等，因此，相应的颜色模式也就有RGB、CMYK、Lab等。在HSB颜色模型中，色相、饱和度、对比度是对图像属性的基本描述。
```## 照度

```text
照度是对环境光强度的度量

衡量单位为lux，白天晴天近10万lux，阴雨天几千lux，夜晚有灯光几十lux，夜晚最小可达0.01lux

照度越小，成像时需要越大的快门（shutter）、增益（gain）、光圈（IRIS）或者补光
```## 色温

```text
色温原本指物体（特别是金属）加热到不同温度发出的不同颜色的光。

衡量单位为K，色温越高反而越冷，色温越低就越暖，范围一般为1800~7500K，蜡烛为1800K，晴天中午为7500K

常见的色温值有D65（日光灯发出的光），TL83，TL84，UV、CWF、A光等
```## 色调

```text
色调指的是一幅画中画面色彩的总体倾向，是大的色彩效果。在大自然中，我们经常见到这样一种现象：不同颜 色的物体或被笼罩在一片金色的阳光之中，或被笼罩在一片轻纱薄雾似的、淡蓝色的月色之中；或被秋天迷人的金黄色所笼罩；或被统一在冬季银白色的世界之中。这种在不同颜色的物体上，笼罩着某一种色彩，使不同颜色的物体都带有同一色彩倾向，这样的色彩现象就是色调。

基本含义

色调是指物体反射的光线中以哪种波长占优势来决定的，不同波长产生不同颜色的感觉，色调是颜色色调的重要特征，它决定了颜色本质的根本特征。

色调不是指颜色的性质，而是对一幅绘画作品的整体颜色的概括评价。色调是指一幅作品色彩外观的基本倾向。在明度、纯度（饱和度）、色相这三个要素中，某种因素起主导作用，我们就称之为某种色调。一幅绘画作品虽然用了多种颜色，但总体有一种倾向，是偏蓝或偏红，是偏暖或偏冷等等。这种颜色上的倾向就是一副绘画的色调。通常可以从色相、明度、冷暖、纯度四个方面来定义一幅作品的色调。

色调在冷暖方面分为暖色调与冷色调：红色、橙色、黄色--为暖色调，象征着：太阳、火焰。蓝色--为冷色调，象征着：森林、大海、蓝天。黑色、紫色、绿色、白色--为中间色调； 暖色调的亮度越高，其整体感觉越偏暖，冷色调的亮度越高，其整体感觉越偏冷。冷暖色调也只是相对而言，譬如说，红色系当中，大红与玫红在一起的时候，大红就是暖色，而玫红就被看作是冷色，又如，玫红与紫罗蓝同时出现时，玫红就是暖色。
```## 饱和度

```text
饱和度可定义为彩度除以明度，与彩度同样表征彩色偏离同亮度灰色的程度。注意，与彩度完全不是同一个概念。但由于其和彩度决定的是出现在人眼里的同一个效果，所以才会出现视彩度与饱和度为同一概念的情况。

饱和度是指色彩的鲜艳程度，也称色彩的纯度。饱和度取决于该色中含色成分和消色成分（灰色）的比例。含色成分越大，饱和度越大；消色成分越大，饱和度越小。纯的颜色都是高度饱和的，如鲜红，鲜绿。混杂上白色，灰色或其他色调的颜色，是不饱和的颜色，如绛紫，粉红，黄褐等。完全不饱和的颜色根本没有色调，如黑白之间的各种灰色。

saturation

用以估价纯彩色在整个色觉(包括无彩色)中的成分的视觉属性。它与濒色的纯度这一物理心理里有关(或近似相关)。它决定于颜色光中所混入的白色光的数里，纯光谱色的含量愈多，则它愈高。
```## 锐度(清晰度)

```text
锐度越高越清晰

锐度，有时也叫“清晰度”，它是反映图像平面清晰度和图像边缘锐利程度的一个指标。高锐度是一把双刃剑，一方面，它使得画面的视觉效果变得清晰，另一方面，由于对比的提高，又会将一些原本并不讨好的主要细节进行放大。
```## 对比度

```text
对比度指的是一幅图像中明暗区域最亮的白和最暗的黑之间不同亮度层级的测量，差异范围越大代表对比越大，差异范围越小代表对比越小，好的对比率120:1就可容易地显示生动、丰富的色彩，当对比率高达300:1时，便可支持各阶的颜色。但对比率遭受和亮度相同的困境，现今尚无一套有效又公正的标准来衡量对比率，所以最好的辨识方式还是依靠使用者眼睛。

在暗室中，白色画面(最亮时)下的亮度除以黑色画面(最暗时)下的亮度。更精准地说，对比度就是把白色信号在100%和0%的饱和度相减，再除以用Lux(光照度，即勒克斯，每平方米的流明值)为计量单位下0%的白色值(0%的白色信号实际上就是黑色)，所得到的数值。对比度是最白与最黑亮度单位的相除值。因此白色越亮、黑色越暗，对比度就越高。严格来讲我们指的对比度是屏幕上同一点最亮时（白色）与最暗时（黑色）的亮度的比值，不过通常产品的对比度指标是就整个屏幕而言的，例如一个屏幕在全白屏状态时候亮度为500cd/m2，全黑屏状态亮度为0.5cd/m2，这样屏幕的对比度就是1000:1。
```## 动态范围

```text
动态范围是对一个场景最亮部分与最暗部分照度比例的衡量。
衡量单位为db，若室内暗处照度为1lux，室外为10万lux，那么动态范围约为100db
常见的宽动态环境是室内外的窗口或门口，以及道路夜晚
```## 成像原理

```text
数字成像系统是对人眼的仿生。
人眼也有镜头、滤光片、传感器以及图像处理系统，对应的器官为：瞳孔、晶状体、角膜、虹膜、视网膜等
```## 人眼的特性

```text
只感知可见光、波长为380~780nm
分辨率可达5亿像素，但对颜色的分辨率低很多
帧率为24fps
低照度约为0.01lux，但很暗时只能感知亮度
人眼也会随着环境光强弱调整瞳孔大小，比如从室外进入到很黑的室内，需要一段时间适应就可以看到一些室内的物体
人眼景深很好，能快速聚焦
人眼有白平衡功能，即光源色温发生变化时，人眼会“减弱”颜色的变化，也就是感知的颜色变化没有实际色温变化那么强烈
人眼对亮度的感知是非线性的，也就是说光的照度增大一倍，并不意味着人眼感知的亮度大一倍
人眼的动态范围很好，有130db，能同时看清很亮和很暗的区域
```## UVC

```text
UVC全称为USB Video Class，直接翻译过来的意思就是：USB视频类，它是一种专门为USB视频捕获设备定义的协议标准。
这个标准是Microsoft与另外几家设备厂商联合推出的为USB视频捕获设备定义的协议标准，已经成为USB org标准之一。
现在的主流操作系统，都已提供UVC设备驱动，因此符合UVC规格的硬件设备在不需要安装任何的驱动程序下即可在主机中正常使用。是的，目前Android系统已经支持uvc设备。

讲到这里大家应该有这么个概念了，uvc是一种协议，不同的设备可能会支持不同的协议。如果我们的usb摄像头，需要在Android设备上获得支持的话，那这个摄像头就得是支持uvc协议的摄像头。
```## [11786]后置摄像头拍照的预览大小更换为全屏后，再更换为4:3，默认像素变为8M

```text
描述：手机默认像素为13.1M，后置摄像头的预览大小默认为4:3，更换为全屏后，像素变为6M，再更换为4:3后，像素默认为8M
期望：更换为4:3，像素应该仍然为默认值13.1M；全屏的像素为6M，请确认是否正确
首先去找projectconfig.mk文件中的CUSTOM_HAL_MAIN_IMGSENSOR（后摄像头），然后按照这个找到/mediatek/custom/mq16_h504_c5vp/hal/imgsensor/ov8858_mipi_raw/config.ftbl.ov8858_mipi_raw.h文件
一般在java和xml文件中已经把每个比例的所有pictrue size都写进去了，只是config.ftbl.ov8858_mipi_raw.h这个文件中没有把所有的东西写进去（每个比例写了哪几个就在手机上显示哪几个尺寸）
```## [默认值]修改相机 Anti-flicker 默认为 Auto

```text xml
关于相机中 Anti-flicker 默认要求为Auto,然后这个就是默认值的修改方法，如果相机配有自动功能，则选择auto，如果没有则选择下面一个
packages/apps/Camera/res/values/camera_arrays.xml
<string-array name="pref_camera_antibanding_default_array" translatable="false">
    <item>auto</item>
    <item>60hz</item>
    <item>off</item>
</string-array>
```## [bug]相机连拍，手松开后，仍会继续拍照（redmine22662）

```text
分两种情况：
1、虽然声音和拍照张数不符合，但是不会一直连拍到40张：长按快门连拍，快门声音比拍出的照片数量多。因为目前长按快门连拍时，声音的循环播放是AP端来控制的，跟拍照的次数没有关系，所以会不同步。
2、松手后直接拍照到40张：
packages/apps/Camera/src/com/android/camera/actor/PhotoActor.java中 onKeyUp(int keyCode, KeyEvent event)
case KeyEvent.KEYCODE_CAMERA:最后面加上
mContinuousShotPerformed = false;
if (mCamera.getCameraState() == Camera.STATE_SNAPSHOT_IN_PROGRESS) {
    cancelContinuousShot();
}
```## [默认值]如何打开zsd

```text
go:vendor/mediatek/proprietary/custom/mt6580/hal/sendepfeature/gc2385_mipi_raw/config.ftbl.gc2385_mipi_raw.h
#if 1
//  Zsd
FTABLE_CONFIG_AS_TYPE_OF_DEFAULT_VALUES(
    KEY_AS_(MtkCameraParameters::KEY_ZSD_MODE),
    SCENE_AS_DEFAULT_SCENE(
        ITEM_AS_DEFAULT_(MtkCameraParameters::ON),    ----> 这一条是是否打开ZSD
        ITEM_AS_VALUES_(
            MtkCameraParameters::OFF,
            MtkCameraParameters::ON
        )
    ),
)

MtkCameraParameters::OFF,
MtkCameraParameters::ON同时存在的时候，camera的界面中会出现这个选项，如果只有一个的话，camera的界面中不会出现这个问题
```## [性能]拍照速度慢、美颜状态下拍照速度慢

```text
1、美颜拍照的原图可以从capbufMgr中取图，即参考zsd的方法（不使用normalshot的取图），这样可以直接从内存取图，缩小取图的时间。
2、开启postview功能，并在app中是用postview做小图的显示，这样显示小图的时间可以加快约800ms（即美颜算法处理时间）。
3、调整美颜算法所在线程的优先级，减少算法处理时间。
4、打开ZSD功能
```## [默认值][FAQ20589] 修改Camera拍照音效

```text
frameworks/av/services/camera/libcameraservice/CameraService.cpp

2096void CameraService::loadSoundImp() {
2097    LOG1("[CameraService::loadSoundImp] E");
2098    mSoundPlayer[SOUND_SHUTTER] = newMediaPlayer("/system/media/audio/ui/camera_click.ogg");
2099    mSoundPlayer[SOUND_RECORDING_START] = newMediaPlayer("/system/media/audio/ui/VideoRecord.ogg");
2100    mSoundPlayer[SOUND_RECORDING_STOP] = newMediaPlayer("/system/media/audio/ui/VideoStop.ogg");
2101    LOG1("[CameraService::loadSoundImp] X");
2102}
```## [FAQ18189] Camera setting中添加拍照音选项

```text
在DMS系统上下载以下文档, 参考修改即可
Camera_add_shuttersound_setting_item_L_platform,

DMS链接如下:
https://dcc.mediatek.com/Docs/Default.aspx
```## [FAQ18283] Android M+Mediatek _Camera Code Path （不含Kernel）

```text
Camera App Package
MTK Camera：/vendor/mediatek/proprietary/packages/apps/Camera/
AOSP Camera：
(out/target/product/<project>/system/app/Camera2.apk)
/packages/apps/Camera2/

Application Framework（out/target/product/<project>/system/framework/framework.jar)
/frameworks/base/core/java/android/hardware/ （非Camera2下的为api1）
/frameworks/base/core/java/android/hardware/camera2/
/frameworks/base/media/java/android/media/ 
CamcorderProfile.java、CameraProfile.java、ExifInterface.java、Image.java、ImageReader.java、ImageUtils.java、ImageWriter.java等等
注：FaceDetector.java并非Camera FaceDetection，而是android原生一个开源人脸识别算法接口，可从一个bitmap获取到人脸信息

JNI (out/target/product/<project>/system/lib/libandroid_runtime.so)
/frameworks/base/core/jni/
android_hardware_Camera.cpp
android_hardware_camera2_CameraMetadata.cpp
android_hardware_camera2_DngCreator.cpp
android_hardware_camera2_legacy_LegacyCameraDevice.cpp
android_hardware_camera2_legacy_PerfMeasurement.cpp

Android Camera Native Framework
/frameworks/av/camera/
/frameworks/av/include/camera/
/frameworks/av/services/camera/libcameraservice/
/frameworks/av/media/mediaserver/
/frameworks/av/media/img_utils/src/DngUtils.cpp

Android Camera Hal
core header files：
(/system/core/include/system/) camera.h、graphics.h 、window.h
camera metadata：
/system/media/camera/

AOSP Hal：
/hardware/libhardware/include/hardware/
/hardware/libhardware/modules/camera/
/hardware/libhardware/modules/usbcamera/
/hardware/libhardware/modules/gralloc/

MediaTek Camera Hal (ISP3.0平台)
/vendor/mediatek/proprietary/hardware/mtkcam/legacy/
/vendor/mediatek/proprietary/hardware/mtkcam/ext/
/vendor/mediatek/proprietary/hardware/mtkcam/feature/
/vendor/mediatek/proprietary/custom/common/hal/inc/
/vendor/mediatek/proprietary/custom/mtxxxx/hal/ 
/vendor/mediatek/proprietary/custom/{ProjectName}/hal/imgsensor/

如下为非Camera但和Camera强相关的Hal模块
/vendor/mediatek/proprietary/hardware/gralloc_extra/
/vendor/mediatek/proprietary/hardware/dpframework/
/vendor/mediatek/proprietary/hardware/bwc/
/vendor/mediatek/proprietary/hardware/jpeg/
/vendor/mediatek/proprietary/hardware/m4u/
/vendor/mediatek/proprietary/hardware/mmsdk/
/vendor/mediatek/proprietary/hardware/mmutils/
/vendor/mediatek/proprietary/hardware/perfservice/

MediaTek Camera Hal (ISP4.0平台)
/vendor/mediatek/proprietary/hardware/mtkcam/（除legacy的folder外）
/vendor/mediatek/proprietary/custom/common/hal/inc/
/vendor/mediatek/proprietary/custom/mtxxxx/hal/ 
/vendor/mediatek/proprietary/custom/{ProjectName}/hal/imgsensor/

如下为非Camera但和Camera强相关的Hal模块
/vendor/mediatek/proprietary/hardware/gralloc_extra/
/vendor/mediatek/proprietary/hardware/dpframework/
/vendor/mediatek/proprietary/hardware/bwc/
/vendor/mediatek/proprietary/hardware/jpeg/
/vendor/mediatek/proprietary/hardware/m4u/
/vendor/mediatek/proprietary/hardware/mmsdk/
/vendor/mediatek/proprietary/hardware/mmutils/
/vendor/mediatek/proprietary/hardware/perfservice/

CTS
/cts/tests/tests/hardware/src/android/hardware/camera2/
/cts/tests/tests/hardware/src/android/hardware/cts/
/cts/apps/CameraITS/
/cts/apps/CtsVerifier/src/com/android/cts/verifier/camera/

Portability Camera
/frameworks/ex/camera2/
(主要应该是这个folder /frameworks/ex/camera2/portability/src/com/android/ex/camera2/portability/)
```## [FAQ18139] 如何dump连拍时的YUV数据

```text
1. adb command 方式：
    手机连接PC
    adb shell setprop debug.MShot.dump 1
    adb shell setprop debug.camnode.dump.44 1
    然后进入camera 开始连拍，连拍后在sdcard/camera_dump 文件夹检查连拍dump YUV图片。

2. 修改code方式：
原理同上述方法1一样。
/vendor/mediatek/proprietary/platform/mt6735/hardware/mtkcam/D1/core/camnode/ICamGraphNode.cpp

ICamGraphImpl::
start()
{
Mutex::Autolock _l(mLock);
MY_LOGD("Start +");
MY_ASSERT_STATE( mState == State_Initiated, mState );
{ //update dump enable
char value[PROPERTY_VALUE_MAX] = {'\0'};
char key[PROPERTY_KEY_MAX];
snprintf( key, PROPERTY_KEY_MAX, "debug.%s.dump", getName());
property_get( key, value, "0"); 

if ((mbDumpEnable = atoi(value))) {
    MY_LOGD("enable dump buffer: %s", getName() );
}
//修改1 
//add beg

MY_LOGD("enable dump buffer1: %s, mbDumpEnable %d", getName() ,mbDumpEnable);
char *a = "MShot";
if(strcmp(a,getName)==0) {
    mbDumpEnable = 1;
}
MY_LOGD("enable dump buffer2: %s, mbDumpEnable %d", getName() ,mbDumpEnable);
//add end

checkDumpData(MUINT32 const data) const {
    MBOOL bDump = MFALSE;
    char value[PROPERTY_VALUE_MAX] = {'\0'};
    char key[PROPERTY_KEY_MAX];
    snprintf( key, PROPERTY_KEY_MAX, "debug.camnode.dump.%d", data);
    property_get( key, value, "0");
    if ((bDump = atoi(value))) {
        MY_LOGD("enable dump buffer: %s, %d", getName(), data );
    } 

    //修改2： 
    //add beg
    MY_LOGD("enable dump buffer3: %s, data:%d bDump:%d,", getName(), data,bDump );
    if(data == 44) {
        bDump = 1;
    }
    MY_LOGD("enable dump buffer4: %s, data:%d bDump:%d,", getName(), data,bDump );
    //add end

    return bDump;
}
```## [FAQ17871] 设置安全锁后，从锁屏界面进入相机，图片预览和录像播放界面短按电源键无法锁屏

```text
以下三段代码都在 PhotoPage.java中

1. 将code1 与PhotoPage类的成员变量放在同一级
//code 1
private BroadcastReceiver mScreenOffReceiver = new BroadcastReceiver() {
    @Override
    public void onReceive(Context context, Intent intent) {
        mActivity.finish();
        Log.d(TAG, "mScreenOffReceiver receive");
    }
};
//code 1 end

2. 将code2 放在PhotoPage.onCreate()里的 if(secureAlbum != null) 的语句下
//code 2
IntentFilter filter = new IntentFilter(Intent.ACTION_SCREEN_OFF);
mActivity.registerReceiver(mScreenOffReceiver, filter);
//code 2 end

3. 将code3 放在 protected void onDestroy()中
//code 3
if (mSecureAlbum != null) {
    mActivity.unregisterReceiver(mScreenOffReceiver);
}
//code 3 end
```## [FAQ17870] 打开微笑快门，不能切换前后camera

```text
前摄像头没有加微笑快门的拍照模式。在使用前摄像头时，被拍的人可以在屏幕上看见拍下的场景，拍照的时机可以自行决定。使用者完全可以在微笑时自行按下拍照键完成拍照，所以前摄像头没有加微笑快门。打开微笑快门，不能切换前后摄像头，属正常设计。
如需修改打开微笑快门，能切换前后camera，修改如下：
请修改/packages/apps/Camera/src/com/mediatek/camera/setting/SettingDataBase.java文件中的 MATRIX_RESTRICTION_STATE[SettingConstants.ROW_SETTING_DUAL_CAMERA] = new int[]{STATE_E0, STATE_D0, STATE_E0, STATE_D0, STATE_D0, STATE_D0, STATE_D0, STATE_E0, STATE_D0, STATE_E0, STATE_E0, STATE_D0, STATE_E0, STATE_D0};//1: dual camera

倒数第三个STATE_D0改成STATE_E0
```## [FAQ17872] 相机设置中点击开关项会连续响两声

```text
请在alps/packages/apps/Camera/src/com/android/camera/ui/InLineSettingSwitch.java中修改如下：
1.添加private boolean mChecked = false;
2.在onClick(View view)方法中将mSwitch.performClick();语句注释掉。将其改为：
mSwitch.setChecked(!mChecked);
mChecked = !mChecked;
changeIndex(mChecked ? 1 : 0);
```## [FAQ17580] 在乌尔都语下，设置色彩效果与预览效果不一致

```text
在com/mediatek/camera/addition/effect/EffectLayout.java文件中的bindView()方法中
layout = new LinearLayout(getContext());语句下面添加layout.setLayoutDirection(View.LAYOUT_DIRECTION_LTR);
让滤镜预览图默认为LTR。
```## [FAQ10972] 如何在ap获取拍照的yuv数据

```text
通过实现ap的RawPictureCallback接口来实现，主要包括ap层以及中间层的修改：
一、AP层的修改：
PhotoActor.java（alps/packages/apps/Camera/src/com/android/camera/actor/）
1、添加import android.hardware.Camera.Size;
2、public boolean capture() 函数中
将
if (!mCameraCategory.applySpecialCapture()) {
    mContext.getCameraDevice().takePicture(getShutterCallback(), mRawPictureCallback, mPostViewPictureCallback, mCameraCategory.getJpegPictureCallback());
}
改为
if (!mCameraCategory.applySpecialCapture()) {
    if(!mContinuousShotPerformed){
        Size curPictureSize = mCamera.getParameters().getPictureSize();
        byte []uRawDataBuffer = new byte [curPictureSize.width*curPictureSize.height*2];
        mContext.getCameraDevice().addRawImageCallbackBuffer(uRawDataBuffer);
    }
    mContext.getCameraDevice().takePicture(getShutterCallback(), mRawPictureCallback,
    mPostViewPictureCallback, mCameraCategory.getJpegPictureCallback());
}

二、中间层的修改：
NormalShot.cpp（alps/mediatek/platform/mt65XX/hardware/camera/hal/adatper/scenarioshot/normalshot/）
1，onCmd_capture（）函数中需要注册YUV的callback message：
pSingleShot->enableDataMsg(NSCamShot::ECamShot_DATA_MSG_YUV);
2，fgCamShotDataCb（）函数中需要添加yuv callback的处理机制：
依照postview的处理方式，添加else if语句
else if(NSCamShot::ECamShot_DATA_MSG_YUV==msg.msyType)
{
pNormalShot->handleYUVData(msg.puData,msg.u4Size)；
}
3，第二步中调用的handleYUVData是新添加的函数，首先在NormalShot.h文件中仿照handlePostViewData()添加函数声明：
MBOOL handleYUVData(MUINT8* const puBuf,MUINT32 const u4Size);
然后在NormalShot.cpp文件中添加其实现：
MBOOL
NormalShot::
handleYUVData（MUINTE8 * const puBuf,MUINT32 const u4Size）
{
MY_LOGD("+ (puBuf, size)=(%p,%d)",puBuf,u4Size);
mpShotCallback->onCB_RawImage(0,u4Size,reinterpret_cast<uint8_t const*>(puBuf));
return MTRUE;
}
4，在handleJpegData（）函数中，将原来的dummy raw callback注释掉
//mpShotCallback->onCB_RawImage(0,0,NULL);
```## [FAQ06278] 第一次开机后检测camera失败, camera icon会一直不会显示,即使重开机后camera检测成功

```text
在手机download完第一次开机后，如果没有插入后置camera sensor HW或检测后置camera sensor失败，则在main menu界面不会显示出camera icon；插入后置camera sensor HW后重新开机，main menu界面仍不会显示出camera icon. 需要进入设置中执行一次“恢复出厂设置”， 才会显示出camera icon。

此现象为google的默认设计，在第一次download手机开机后如果没有检测出后置摄像头的存在，会disable掉camera的应用。

[SOLUTION]
可以按照如下更改进行修改测试
您可以将DisableCameraReceiver.java(路径为alps/packages/apps/camera/src/com/androic/camera)
//boolean needCameraActivity = CHECK_BACK_CAMERA_ONLY ? hasBackCamera() : hasCamera();
boolean needCameraActivity = true;
此修改会造成在没有camera sensor HW的情况下，在main menu界面会显示出camera icon，点击icon会提示camera出错.
```## [FAQ15378] [VR]SlowMotion录制的视频发送到其他手机或电脑上均有slow motion效果

```text
使用SlowMotion录制的视频，发送到其他手机或电脑上播放时均有slow motion效果，即录制出来的视频本身就有慢速效果
[SOLUTION]
1、请在ProjectConfig.mk中确保有这个宏MTK_SLOW_MOTION_VIDEO_SUPPORT = yes;
2、在packages\apps\Camera\src\com\mediatek\camera\mode\VideoMode.java这支文件中：
第103行的
private static final int SLOW_MOTION_VIDEO_TAG_IN_FILE = 1;
改为：
private static final int SLOW_MOTION_VIDEO_TAG_IN_FILE = 2;//慢速倍数
```## [默认值][FAQ04374] 如何修改照片详细信息中的Make、Model和Software栏位

```text
我们平台提供三项EXIF信息供您客制化：
make、model、software 。
具体方法：打开以下对应文件中EN_CUSTOM_EXIF_INFO的宏定义之后，修改make， model ， software三项，修改完之后重新build整个工程即可。
对应文件具体路径：
GB2/ICS:
\mediatek\custom\common\hal\camera\camera\Config.cpp
ICS2版本MT6575平台：
\mediatek\custom\common\hal\camera\camera\mt6575\Config.cpp
ICS2版本MT6577平台：
\mediatek\custom\common\hal\camera\camera\mt6577\Config.cpp
JB版本MT6577平台：
\mediatek\custom\mt6577\hal\camera\camera\Config.cpp
JB2版本MT6589平台：
\mediatek\custom\mt6589\hal\camera\camera\camera_custom_if.cpp
JB3版本MT6572平台：
\mediatek\custom\mt6572\hal\camera\camera\camera_custom_if.cpp
JB5版本MT6582平台：
\mediatek\custom\mt6582\hal\camera\camera\camera_custom_if.cpp
KK1版本:
\mediatek\custom\common\hal\inc\camera_custom_exif.h (若要区分不同project，可以将该文件copy到project路径的下面)
```## [FAQ15703] 后摄语音拍照on/off状态总是与最后退出的Camera的on/off一致

```text
Voice打开，无论前后摄都是打开的，并且voice有记忆功能，即下次进来还会打开，若要独立的话，目前无法实现。
以下提供了前后摄统一的修改方法，修改如下：

SharePreferencesTransfer.java
comboPreference.java
修改內容都是這個方法中多加一個voice的判斷。
private static boolean isGlobal(String key) {
    return key.equals(SettingConstants.KEY_VIDEO_TIME_LAPSE_FRAME_INTERVAL)
        || key.equals(SettingConstants.KEY_CAMERA_ID)
        || key.equals(SettingConstants.KEY_RECORD_LOCATION)
        || key.equals(SettingConstants.KEY_MULTI_FACE_BEAUTY)
        || key.equals(SettingConstants.KEY_VOICE);// 多加此處
}
```## [FAQ15863] HDR的预览和拍照图片不一致

```text
1.Launch camera, click HDR;
2.将焦距变为4倍.
3.拍照, 查看照片,发现所拍照片区域和预览不一致. 
请直接在PMS系统上申请patch: ALPS01949429 
```## [FAQ15990] 开启零延迟拍照后无效

```text
分析方法：
1.先确认是否是normal shot with strobe off拍照，如果不是这种情况，就不是走ZSD流程，属于正常现象。 
2.查看Log文件，分析开启了ZSD后是否走的ZSD流程。

1.开闪光灯和ZSD后，属Normalshot，Log如下：
111893 01-01 00:12:13.195 257 257 D CameraClient: takePicture (pid 5081): 0x302 拍照开始
111917 01-01 00:12:13.197 257 257 D MtkCam/CamAdapter: (257)(MtkZsd)[onHandlePreCapture] +
112086 01-01 00:12:13.214 257 5207 D MtkCam/ZSDPrvCQT: (5207)[precap] flash ON 闪光灯打开
113551 01-01 00:12:13.517 257 257 D MtkCam/CamAdapter: (257)(MtkZsd)[onHandleStopPreview] +
113783 01-01 00:12:13.568 257 257 D MtkCam/CamAdapter: (257)(StateIdle)[onCapture] +
115337 01-01 00:12:14.004 257 5208 D MtkCam/Shot: (5208)(NormalShot)[handleJpegData] + (puJpgBuf, jpgSize, puThumbBuf, thumbSize) = (0xeda79000, 2052806, 0xf1f21000, 9538) 
115510 01-01 00:12:14.025 257 5208 D MtkCam/Shot: (5208)(NormalShot)[~ImpShot] - 普通拍照完成
115564 01-01 00:12:14.042 5081 5081 I CameraFramework: handleMessage: 256

2.打开ZSD后，走ZSD流程，Log如下：
00953 01-01 23:34:33.798 253 816 D CameraClient: takePicture (pid 3569): 0x302 拍照开始
01987 01-01 23:34:34.198 253 3722 D MtkCam/ZSDShot: (3722)(ZSD)[handleJpegData] + 
02133 01-01 23:34:34.221 253 3722 D MtkCam/Shot: (3722)(ZSD)[~ImpShot] - ZSD拍照结束
02144 01-01 23:34:34.235 3569 3569 I CameraFramework: handleMessage: 256
```## [FAQ14787] 前置默认设置为美颜模式

```text
CameraActivity.java函数内做如下修改：

private PickerManager.PickerListener mPickerListener = new PickerManager.PickerListener() {
    @Override
    public boolean onCameraPicked(int cameraId) {
        //函数内的语句mCameraAppUi.setViewState(ViewState.VIEW_STATE_CAMERA_CLOSED);前添加如下语句：
        if (cameraId==1) {
            mModePicker.setCurrentMode(ModePicker.MODE_FACE_BEAUTY);
            Log.i(TAG,"setCurrentMode facebeauty");
        } else {
            mModePicker.setCurrentMode(ModePicker.MODE_PHOTO);
        }

private SettingManager.SettingListener mSettingListener = new SettingManager.SettingListener() {
@Override
public void onRestorePreferencesClicked() {
函数内
将如下语句
if (ModePicker.MODE_PHOTO == mCameraActor.getMode() || !isNonePickIntent()
        || ModePicker.MODE_PHOTO_SGINLE_3D == mCameraActor.getMode()
        || ModePicker.MODE_PHOTO_3D == mCameraActor.getMode()) {
    if (ModePicker.MODE_VIDEO == mCameraActor.getMode() && !isNonePickIntent()) {
        mISettingCtrl.onSettingChanged(SettingConstants.KEY_VIDEO,"on");
    }
    mCameraDeviceCtrl.applyParameters(false);
} else {
    mModePicker.setModePreference(null);
    mModePicker.setCurrentMode(ModePicker.MODE_PHOTO);
}

修改为

if(getCameraId()==1){
    mModePicker.setCurrentMode(ModePicker.MODE_FACE_BEAUTY);
} else if (ModePicker.MODE_PHOTO == mCameraActor.getMode() || !isNonePickIntent()
        || ModePicker.MODE_PHOTO_SGINLE_3D == mCameraActor.getMode()
        || ModePicker.MODE_PHOTO_3D == mCameraActor.getMode()) {
    if (ModePicker.MODE_VIDEO == mCameraActor.getMode() && !isNonePickIntent()) {
        mISettingCtrl.onSettingChanged(SettingConstants.KEY_VIDEO,"on");
    }
    mCameraDeviceCtrl.applyParameters(false);
} else {
    mModePicker.setModePreference(null);
    mModePicker.setCurrentMode(ModePicker.MODE_PHOTO);
}
```## [FAQ14842] 如何支持自拍杆拍照功能

```text
根据Log确定自拍杆按键对应的KeyCode是多少，进而根据这个KeyCode值来确认对应的按键是哪个。
一般常用的有：音量+、音量-、Enter
public static final int KEYCODE_VOLUME_UP       = 24;
public static final int KEYCODE_VOLUME_DOWN     = 25;
public static final int KEYCODE_ENTER           = 66;
这里以音量-键为例
在/packages/apps/Camera/src/com/android/camera/actor/PhotoActor.java文件中的onKeyDown方法和onKeyUp方法中添加对KEYCODE_VOLUME_DOWN 键的处理即可,

即在case KeyEvent.KEYCODE_CAMERA:之前添加：

case KeyEvent.KEYCODE_VOLUME_DOWN:
```## [FAQ14693] 如何将device version由HAL3.2改为HAL1.0

```text
Android one版本默认底层配的device version为HAL3.2，如果想改为HAL1.0，可以按以下方法修改。
[SOLUTION]
在文件config_static_metadata_common.h中把
case 0:
     //======================================================================
    CONFIG_METADATA_BEGIN(MTK_HAL_VERSION)
        CONFIG_ENTRY_VALUE(MTK_HAL_VERSION_3_2, MINT32)
    CONFIG_METADATA_END()
    //======================================================================
    break;
case 1:
     //======================================================================
    CONFIG_METADATA_BEGIN(MTK_HAL_VERSION)
        CONFIG_ENTRY_VALUE(MTK_HAL_VERSION_3_2, MINT32)
    CONFIG_METADATA_END()
    //======================================================================
    break;
改为
case 0:
     //======================================================================
    CONFIG_METADATA_BEGIN(MTK_HAL_VERSION)
        CONFIG_ENTRY_VALUE(MTK_HAL_VERSION_1_0, MINT32)
    CONFIG_METADATA_END()
    //======================================================================
    break;
case 1:
     //======================================================================
    CONFIG_METADATA_BEGIN(MTK_HAL_VERSION)
        CONFIG_ENTRY_VALUE(MTK_HAL_VERSION_1_0, MINT32)
    CONFIG_METADATA_END()
    //======================================================================
    break;
```## [FAQ14537] 下拉菜单中闪光灯打开时，mtk camera app也可以正常启动

```text
当mtk camera app启动时会主动发送广播到下拉菜单，提示去关闭闪光灯，然后mtk camera app再去启动相机，这样就可以正常启动了。具体实现可参考如下文档：
MTK Camera ap-broadcast-SystemUI_mt6735.pdf
 
文档可以去下面DMS中下载：
https://dcc.mediatek.com/Docs/Default.aspx
```## [FAQ14424] 拍照时强制开多颗CPU

```text
进入相机拍照，拍照动画和拍照声音会概率性发生卡顿

[ANALYSE]
此问题发生的原因是在拍照期间概率性打开的CPU个数不够处理拍照时loading，所以会出现拍照动画和拍照声音卡顿的问题。
解决方法：拍照时强制开多颗（3或者4）CPU，足以处理拍照时的loading。
L版本上可以按以下方法修改。

[SOLUTION]

在PhotoMode.java (alps\packages\apps\camera\src\com\mediatek\camera\mode) 中：

一，import PerfServiceWrapper，IPerfServiceWrapper
import com.mediatek.perfservice.PerfServiceWrapper;
import com.mediatek.perfservice.IPerfServiceWrapper;
二，添加如下变量：
IPerfServiceWrapper mPerfService = null;
int mPerfHandle = -1;
三，public PhotoMode(ICameraContext cameraContext)中加入：
if(mPerfService!=null&&mPerfHandle==-1){
    mPerfHandle=mPerfService.userReg(4,0);//第一个参数表示要开的CPU个数
}
四，public boolean capture()中加入
if(mPerfService!=null&&mPerfHandle==-1) {
    mPerfService.userEnableTimeout(mPerfHandle,10);//第二个参数表示多少秒之后timeout
}


调试命令
adb shell "echo 0 > /proc/hps/enabled"
adb shell "echo performance > /sys/devices/system/cpu/cpufreq/policy0/scaling_governor"
adb shell "echo 1 > /sys/devices/system/cpu/cpu1/online"
adb shell "echo 1 > /sys/devices/system/cpu/cpu2/online"
adb shell "echo 1 > /sys/devices/system/cpu/cpu3/online"
```## [FAQ13739] Camera界面的pickermanager icon较慢显示出来

```text
1.      Launch camera；
2. 在capture mode icon & preview screen全部显示出来后, pickermanager icon要等2s左右才显示出来 
[SOLUTION]
请在PMS上直接申请patch: ALPS01988332
或做如下修改
alps\packages\apps\Camera\src\com\android\camera\bridge\CameraAppUiImpl.java as below:
    @Override
    public void setViewState(ViewState state) {
        Log.i(TAG, "[setViewState],mCurrentViewState:" + mCurrentViewState + ",newState:" + state);
        if (mCurrentViewState == state) {
            return;
        }
       ...................

        switch (mCurrentViewState) {
        case VIEW_STATE_NORMAL:
            setViewManagerVisible(true);
            setViewManagerEnable(true);
            mShutterManager.setEnabled(true);            mShutterManager.setVideoShutterEnabled(mIsVideoShutterButtonEanble);
            mSettingManager.setFileter(true);
            mSettingManager.setAnimationEnabled(true, true);
            // For tablet
            if (FeatureSwitcher.isSubSettingEnabled()) {
                mSubSettingManager.setFileter(true);
                mSubSettingManager.setAnimationEnabled(true, true);
            }
            ///add this if statement
            if ((!mCameraActivity.isVideoMode() || !mCameraActivity.isNonePickIntent()) .
                    && mCameraActivity.isCameraOpened()) {
                mPickerManager.show();
            }
            ///add end
            if (!mMainHandler.hasMessages(MSG_SHOW_ONSCREEN_INDICATOR)) {
                showIndicator(0);
            } else {
                Log.d(TAG, "[setViewState]mMainHandler has message MSG_SHOW_ONSCREEN_INDICATOR");
            }
            break;
        case VIEW_STATE_CAPTURE:
            mModePicker.hideToast();
            mSettingManager.collapse(true);
................................
}
```## [FAQ12984] 从Camera滑入空的Gallery背景有一根黑线

```text
1. Camera文件夹内容为空
2. 进入Camera, 向左滑动进入Gallery
3. 显示0 images/videos available, 同时查看背景有一根黑线
 
解决方法：
packages\apps\Gallery2\src\com\android\gallery3d\glrenderer\GLES20Canvas.java
为：
public void drawTexture(BasicTexture texture, int x, int y, int width, int height) {
    if (width <= 0 || height <= 0) {
        return;
    }
    copyTextureCoordinates(texture, mTempSourceRect);
    mTempTargetRect.set(x, y, x + width - 1, y + height - 1); // M: modify this line
    convertCoordinate(mTempSourceRect, mTempTargetRect, texture);
    Log.d(TAG, "[Gallery Issue] drawTexture src: " + mTempSourceRect + ", target: " + mTempTargetRect);
    drawTextureRect(texture, mTempSourceRect, mTempTargetRect);
}
private static void copyTextureCoordinates(BasicTexture texture, RectF outRect) {
    int left = 0;
    int top = 0;
    int right = texture.getWidth() - 1;      // M: modify this line
    int bottom = texture.getHeight() - 1; // M: modify this line
    if (texture.hasBorder()) {
        left = 1;
        top = 1;
        right -= 1;
        bottom -= 1;
    }
    outRect.set(left, top, right, bottom);
}
```## [FAQ13010] 如何在Camera拍照时往Jpeg的EXIF新增栏位

```text
这边以CustomRendered这个栏位为例，
首先在EXIF官方spec查看该栏位的定义
http://www.kodak.com/global/plugins/acrobat/en/service/digCam/exifStandard2.pdf
官方有如下定义
CustomRendered
This tag indicates the use of special processing on image data, such as rendering geared to output. When special
processing is performed, the reader is expected to disable or minimize any further processing.
Tag = 41985 (A401.H)
Type = SHORT
Count = 1
Default = 0
0 = Normal process
1 = Custom process
Other = reserved

[SOLUTION]
1. 首先需要定义
Exif_type.h (mediatek\hardware\mtkcam\exif\common)
1)    定义
....
#define EXIF_TAG_CUSTOMRENDERED    0xA401
.....
2) 加入数组
static unsigned short exifTagID[] = {
.....
      EXIF_TAG_CUSTOMRENDERED,
.....
};

2. 指出它的类型，CustomRendered为SHORT类型
Exif_ifdinit.cpp (mediatek\hardware\mtkcam\exif\common)
unsigned int
ifdExifIFDValInit(
    ifdNode_t *pnode,
    struct exifIFDList *plist
)
{
    case EXIF_TAG_CUSTOMRENDERED:
        pifd->type = IFD_DATATYPE_SHORT;
        pifd->count = 1;
        write16((unsigned char*)&pifd->valoff, 0);
        break;
}

3.需要在exif api中添加栏位的定义，以便capture流程中使用
IBaseExif.h (mediatek\hardware\mtkcam\exif\common)

typedef struct exifAPP1Info_s {
....
    unsigned short customRendered;
.....
} exifAPP1Info_t;

4. 让exif api的定义和exif_type中的定义map起来
Exif_make.cpp (mediatek\hardware\mtkcam\exif\common)
static unsigned int
exifTagUpdate(
    exifImageInfo_t *pexifImgInfo,
    exifAPP1Info_t *pexifAPP1Info
)
{
.....
    err = ifdListNodeModify(IFD_TYPE_EXIFIFD, EXIF_TAG_CUSTOMRENDERED, &pexifAPP1Info-> customRendered);
    if (err != 0) {
        return err;
    }
......
}
 
5. 写Exif的地方是在CamExif中，这里的pexifApp1Info 就是前面3中定义的exifAPP1Info_s， 您添加的该栏位可以在这里去找个地方进行赋值。
CamExif.cpp (mediatek\hardware\mtkcam\exif\camera)
queryExifApp1Info(exifAPP1Info_s*const pexifApp1Info) {
         ………
        // [customRender]
        pexifApp1Info-> customRendered = 1;  
         …..
}
```## [FAQ09934] 相机preview时候出现水印问题

```text
使用DDMS截图和layer dump工具均能发现有有水印图片出现。
 
比对有水印和没有水印的layer dump log，发现出问题的时候的SurfaceView：

+ Layer 0x42505008 (SurfaceView)

  activeBuffer=[ 720x1280: 736,  4],  colorformat 是RGB565.

而正常时候的SurfaceView：

+ Layer 0x42505789 (SurfaceView)

  activeBuffer=[ 720x1280: 736,  5],  colorformat 是RGB888.

review修改camera ap部分发现在preview时候设定的color format就是RGB565, 这里导致颜色丢失而引发水印现象。需要做如下修改：

1. 在GLRootView.java中：
public GLRootView(Context context, AttributeSet attrs) { ......
        if(USE_RGB888)       
            getHolder().setFormat(PixelFormat.RGB_888); 
        else
            getHolder().setFormat(PixelFormat.RGB_565); 
}

在GalleryEGLConfigChooser.java中：增加RGB888的配置：

private final int mConfigSpec565[] = new int[] {
    EGL10.EGL_RED_SIZE, 5,
    EGL10.EGL_GREEN_SIZE, 6,
    EGL10.EGL_BLUE_SIZE, 5,
    EGL10.EGL_ALPHA_SIZE, 0,
    EGL10.EGL_NONE
}; 
private final int mConfigSpec888[] = new int[] {
    EGL10.EGL_RED_SIZE, 8,
    EGL10.EGL_GREEN_SIZE, 8,
    EGL10.EGL_BLUE_SIZE, 8,
    EGL10.EGL_ALPHA_SIZE, 0,
    EGL10.EGL_NONE
}; 

private boolean USE_RGB888 = true;
public EGLConfig chooseConfig(EGL10 egl, EGLDisplay display) {
int mConfigSpec[] = (USE_RGB888 == true)? mConfigSpec888 : mConfigSpec565;
```## [FAQ05337] 修改camera拍照的默认保存路径

```text
在 ICS & JB & JB2 版本上, Camera拍照的默认保存路径的修改方法为, 打开 Storage.java 将:
public static void updateDefaultDirectory(Activity activity, boolean stillCapture) {
    String defaultPath = StorageManager.getDefaultPath();
    MOUNT_POINT = defaultPath;
    Log.i(TAG, "Write default path =" + defaultPath);
    if (Util.CU) {
        DCIM = stillCapture ? (MOUNT_POINT + "/Photo") : (MOUNT_POINT + "/Video");
        DIRECTORY = DCIM;
    } else {
        DCIM = MOUNT_POINT + "/DCIM";
        DIRECTORY = DCIM + "/Camera";
    }
    BUCKET_ID = String.valueOf(DIRECTORY.toLowerCase().hashCode());

中的DIRECTORY=DCIM+”/Camera” 改为DIRECTORY = 您想要的目录名;

做完以上修改后,拍的照片就会默认保存在您定义的目录下.
```## [FAQ09417] [Audio Common]如何调整录像和拍照的声音大小

```text
CameraService.cpp
playSound(...) {
    ...
    player->seekTo(0);
    //增加下行
    player->setVolume(leftVolume,rightVolume);
    ...
}
其中leftVolume & rightVolume  大小限定在0~1 之间。
```## [FAQ09949] 预览界面显示一个灰块

```text
1.      进入相机界面拍摄一张照片或者一个视频
2.      向左滑动一次进入浏览图片界面
3.      在浏览图片界面点击back键后快速点击menu键---进入取景界面查看界面显示
4.      此时会在取景界面下方留下一个灰色长条，直到再次点击back键，灰色长条才会消失
[SOLUTION]
请作如下修改验证：
文件 photopage.java 函数
private void updateMenuOperations()
    int supportedOperations = mCurrentPhoto.getSupportedOperations();
    ////M: zhongchao
    if(0 == supportedOperations) {
        menu.close();
        return;
    }
```## [FAQ08897] 如何去掉首次进入camera时的引导动画

```text
相机的引导动画是在函数showAppGuide()中实做的, 如果要去掉，请注释掉此函数中的以下代码：
if (sAppGuideExt != null) {
    sAppGuideExt.showCameraGuide(activity, type);
}

JB2与JB5除了做以上修改，
还需要在alps\packages\apps\camera\src\com\android\camera\camera.java中做如下修改：
在doOnResume()中将
if (isNonePickIntent() || isImageCaptureIntent()) {
    if (isAppGuideFinished()) {
        mVoiceManager.startUpdateVoiceState();
    }
}
改为：
if (isNonePickIntent() || isImageCaptureIntent()) {
    mVoiceManager.startUpdateVoiceState();
}
```## [FAQ07404] 相机连拍快门声音和拍照数量不一致

```text
长按快门连拍，快门声音比拍出的照片数量多。因为目前长按快门连拍时，声音的循环播放是AP端来控制的，跟拍照的次数没有关系，所以会不同步。
[SOLUTION]
JB版本按以下方法调整：
连拍时快门声音的播放是在modeactor.java中的函数onShutterButtonLongPressed()中通过调用以下代码来实现的:
mStreamID = mBurstSound.play(mSoundID, 1.0f, 1.0f, 1, -1, 1.0f);
最后一个参数表示播放的速率,可以在0.5-2之间进行调整,如果想让声音播放的慢一些,可以把这个值调小一些。

JB2/JB3版本按以下方法调整：
连拍时快门声音的播放是在photoactor.java中的函数shuttercallback的onShutter()中通过调用以下代码来实现的:
mStreamID = mBurstSound.play(mSoundID, 1.0f, 1.0f, 1, -1, 1.0f);
最后一个参数表示播放的速率,可以在0.5-2之间进行调整,如果想让声音播放的慢一些,可以把这个值调小一些。
如果调成0.5还是感觉比连拍播的快，那只能去更换拍照音的音源了，即/system/media/audio/ui/camera_shutter.ogg文件。
```## [FAQ05244] 连拍结束后，少保存一张图片或者最后一张图片在图库预览为灰色（无缩略图）

```text
在Package/apps/Camera/src/com/android/camera/ModeActor.java的

ActorContinuousShot类中： 

1．将cancelContinuousShot()方法替换为：
private void cancelContinuousShot() {
    mCameraDevice.cancelContinuousShot();
    mBurstSound.stop(mStreamID);
    //modified start
    /*
    mWaitSavingDoneThread = new Thread() {
        private ImageSaver mImageSaver = mCamera.mImageSaver;
        private ImageNamer mImageNamer = mCamera.mImageNamer;
        @Override
        public void run() {
            mImageSaver.waitDoneInSubThread();
            mHandler.sendEmptyMessage(MSG_BURST_SAVING_DONE);
            mImageNamer.cleanOldUriAndRequestSync();
        }
    };
    mWaitSavingDoneThread.start();
    */
    //modified end
}

2. 将onConinuousShotDone(int capNum) 方法替换为：
public void onConinuousShotDone(int capNum) {
    Log.i(TAG, "onContinuousShotDone, pictures saved = " + capNum);
    //modified start
    mWaitSavingDoneThread = new Thread() {
        private ImageSaver mImageSaver = mCamera.mImageSaver;
        private ImageNamer mImageNamer = mCamera.mImageNamer;
        @Override
        public void run() {
            mImageSaver.waitDoneInSubThread();
            mHandler.sendEmptyMessage(MSG_BURST_SAVING_DONE);
            mImageNamer.cleanOldUriAndRequestSync();
        }
    };
    mWaitSavingDoneThread.start();
    //modified end
    if (mWaitSavingDoneThread != null && mWaitSavingDoneThread.isAlive()) {
        updateSavingHint(true, true);
    }
}
```## [FAQ04529] 连拍结束后加入动画效果

```text
将ModeActor.java的ModeActorHandler做如下修改，添加“//add this line”处的那一行代码：
private class ModeActorHandler extends Handler {
    ……
    public void handleMessage(Message msg) {
        ……
        case MSG_BURST_SAVING_DONE:
            updateSavingHint(false);
            onBurstSaveDone();
            animateByIntentOrZSD(); //add this line
            break;
        }
    }
};
```## [FAQ04528] 如何在静音模式下也开启拍照音

```text
JB,ICS2,ICS需要做如下修改：
将mediatek/Config/<Project Name>/system.prop文件中的：
ro.camera.sound.forced=0
替换为：
ro.camera.sound.forced=1

JB2需要做如下修改：
将frameworks/base/core/res/res/values/config.xml中的：
<bool name="config_camera_sound_forced">false</bool>
修改为：
<bool name="config_camera_sound_forced">true</bool>
```## [FAQ11738] 如何测试camera中的GPS位置信息

```text
测试camera中的GPS位置信息有分以下两种情形:
1.    手机有安装完整的与手机软件对应的GMS包, 即:JB2版本需要装JB2对应的GMS包;KK版本需要装与KK对应的GMS包.
2.    手机没有安装GMS包.
针对以上两种情况, 都需要把setting\location项打开.
[SOLUTION]
一.  手机有安装完整的对应GMS包,测试步骤为:
1.    进入setting\location, 把location打开.
2.    连接上一个可用的wifi ap或插入SIM卡后打开data account项
3.    通过地图软件看是否可以定位当前位置.
4.    地图软件能定位成功后进入camera, 打开GPS location info
5.    拍照,进入图库,查看当前拍照照片的详细信息,会显示位置信息项, 如:xx市xx路.

二.  手机未安装GMS包, 测试步骤为:
1.    移步到室外开阔的地方.
2.    进入setting\location, 把location打开.
3.    输入字串进入engineer mode\location\YGPS界面, 待搜出3颗以上的卫星且显示绿色后表示位置定位成功(见如下图片).
4.    进入camera, 打开GPS location info.
5.    拍照,进入图库,查看当前拍照照片的详细信息, 会显示出位置信息项, 如:经纬度.
```## Android P one 版本默认底层配的 device version为 HAL3.2，如果想改为 HAL1.0

```text C
在文件 alps/vendor/mediatek/proprietary/custom/mt6739/hal/imgsensor_metadata/common/config_static_metadata_common.h 中把
case 0:
    CONFIG_METADATA_BEGIN(MTK_HAL_VERSION)
    CONFIG_ENTRY_VALUE(MTK_HAL_VERSION_3_2, MINT32)
    CONFIG_METADATA_END()
    break;
case 1:
    CONFIG_METADATA_BEGIN(MTK_HAL_VERSION)
    CONFIG_ENTRY_VALUE(MTK_HAL_VERSION_3_2, MINT32)
    CONFIG_METADATA_END()
    break;
改为
case 0:
    CONFIG_METADATA_BEGIN(MTK_HAL_VERSION)
    CONFIG_ENTRY_VALUE(MTK_HAL_VERSION_1_0, MINT32)
    CONFIG_METADATA_END()
    break;
case 1:
    CONFIG_METADATA_BEGIN(MTK_HAL_VERSION)
    CONFIG_ENTRY_VALUE(MTK_HAL_VERSION_1_0, MINT32)
    CONFIG_METADATA_END()
    break;
```## [默认值][FAQ13704] Android L版本如何修改照片详细信息中的Maker、Model栏位

```text
Android KK及之前的版本可参考FAQ:
FAQ04374 如何修改照片详细信息中的Make、Model和Software栏位
而android L上面有更改为读取property的方式来赋值，相关代码可见

camExif.cpp
char make[PROPERTY_VALUE_MAX] = {'\0'};
char model[PROPERTY_VALUE_MAX] = {'\0'};
property_get("ro.product.manufacturer", make, "0");
property_get("ro.product.model", model, "0");
MY_LOGI("property: make(%s), model(%s)", make, model);
// [Make]
if ( ::strcmp(make, "0") != 0 ) {
    ::memset(pexifApp1Info->strMake, 0, 32);
    ::strncpy((char*)pexifApp1Info->strMake, (const char*)make, 32);
}    

Android L上面可通过修改project config配置
/device/mediatek/[project name]/full_[project name].mk
例如project name为k82v12
device/mediatek/k82v12/full_k82v12.mk
修改下面的代码
# Set those variables here to overwrite the inherited values.
PRODUCT_MANUFACTURER := alps //这一栏将赋值给make
PRODUCT_NAME := full_k82v12
PRODUCT_DEVICE := k82v12
PRODUCT_MODEL := k82v12     //这一栏将赋值给model
PRODUCT_POLICY := android.policy_phone
```## [默认值]照片详情中 maker,model 名称修改(EXIF)

```text
KK平台
1、mediatek/custom/mt6572/hal/camera/camera/camera_custom_if.cpp中修改（jb3），可以搜索CUSTOM_EXIF_STRING_MAKE
2、mediatek/custom/up09l_h401_ddm_single/hal/inc/camera_custom_exif.h（kk），可以搜索CUSTOM_EXIF_STRING_MAKE
3、mediatek/custom/common/hal/inc/camera_custom_exif.h（kk），可以搜索CUSTOM_EXIF_STRING_MAKE
4、../sagereal/mk/UP19_H353_Vodacom/full_sr6572_wet_l.mk (l),可以搜索PRODUCT_MANUFACTURER和PRODUCT_MODEL

TODO : 其他平台的也更新进来???
```## [默认值]camera闪光灯默认情况

```text bash
可以打开 package/apps/Camera/res/values/string.xml,然后搜索 pref_camera_flashmode_default 就可以了！(R.styleable.ListPreference_defaultValue 要去搜索defaultValue而不是去搜索ListPreference_defaultValue)
```## [默认值]camera拍照的的咔嚓声音的存储位置

```text
adb shell -->cd /system/media/audio/ui
frameworks/av/services/camera/libcameraservice/CameraService.cpp
```## [默认值]如何在静音模式下也有截图以及拍照声音

```text
1、frameworks/base/core/res/res/values-mcc404/config.xml中的 config_camera_sound_forced 的值设置为true，强制使用拍照声音
如果设为false的话，会跟着情景模式走，当静音模式的时候就不会出现截图和拍照声音，如果是户外模式的时候就会出现截图和拍照声音
2、也可以audioservice.java里的 readCameraSoundForced()， 返回结果强制返回一个false。
```## [FAQ11754]KitKat版本如何将camera service修改为强占式

```text
实现强占式camera service，当某些应用（如手电筒）在后台打开camera后，当camera app open camera时可以强占被后台应用占有的camera.
```## 如何让camera在拍录像的同时能拍照(VSS)

```text
在camera的配置文件中，搜索 KEY_VIDEO_SNAPSHOT_SUPPORTED，
#if 1
//  Video Snapshot
FTABLE_CONFIG_AS_TYPE_OF_USER(
KEY_AS_(MtkCameraParameters::KEY_VIDEO_SNAPSHOT_SUPPORTED), 
    SCENE_AS_DEFAULT_SCENE(
        ITEM_AS_DEFAULT_(MtkCameraParameters::TRUE),             ---->TRUE为支持，FALSE为不支持
    ), 
)
#endif
```## [默认值]如何修改默认camera插值

```text
默认的插值都是默认插值为最后一个，有时候客户需要默认插值为某个值，可以按照下面这个FAQ进行修改。
[FAQ14380]L版本上如何修改默认picture size
```## [bug][FAQ18816] 【AudioProfile】插入印度SIM 卡，相机拍照声音开关控制无效

```text
插入印度卡后，关闭camera拍照声的情况下也有声音，使用其他SIM卡不会有问题。

是由于客户印度卡mcc为404,405，所以调用frameworks/base/core/res/res/values-mcc404/config.xml中的config_camera_sound_forced 的值，而这个值为true，从而导致强制使用拍照声音，修改为false就可以了。
当然，在Audioservice.java里readCameraSoundForced()，强制赋值false也是可行的
```## [FAQ18450] 3rd camera ap 画面亮度偏暗

```text
3rd camera ap, e.g. google hangouts, whatsapp, skype 等preview or 视频通话时画面偏暗
 
在log中search "preview-fps-range="
12092 12569 V CameraFramework: set Key = preview-fps-range, value = 30000,30000
preview-fps-range=30000,30000;preview-fps-range-values=(5000,30000),(20000,20000),(30000,30000);
 
可以看到3rd ap 通过api: setPreviewFpsRange(30000, 30000)把fps固定在30, 此时camera AE会把shutter固定在30ms
 
在光线不好的环境下, 30ms shutter会让画面偏暗
 
[SOLUTION]
fps和画面亮度两者不可兼得:
 
1, fps固定在30, 在暗处画面偏暗是预期的行为, 牺牲画面亮度保证fps是3rd ap预期的行为, 不需要修改
2, feature table:
KEY_AS_(MtkCameraParameters::KEY_PREVIEW_FPS_RANGE), 
SCENE_AS_DEFAULT_SCENE(
ITEM_AS_DEFAULT_("5000,30000"), 
ITEM_AS_USER_LIST_(
"(15000,15000)", 
"(24000,24000)", 
"(30000,30000)",
 
改为:
 
KEY_AS_(MtkCameraParameters::KEY_PREVIEW_FPS_RANGE), 
SCENE_AS_DEFAULT_SCENE(
ITEM_AS_DEFAULT_("5000,30000"), 
ITEM_AS_USER_LIST_(
"(5000,30000)",
 
让平台只支持dynamic fps (5~30), 此时3rd ap下preview-fps-range=(30000,30000)不起作用
 
在暗处时牺牲了fps来提高画面亮度
```## [FAQ12295]录像的视频如何在画面中实时加上时间戳

```text
方法一（L之前版本）：
可以在下面这个地方同，即MDP输出这个画面，但是Encode之前，使用SW的方式来Overlay即可，至于具体如何实现Overlay的话，网上搜索一下，很多示例代码的。如下的参考代码是在录像的画面上画一条彩色条的测试代码，你们可以将添加timestamp的功能的代码替换掉memset之后即可实现timestamp的功能。这个Buffer的格式是YUV420 Planer格式，即先放Y，再放U，最后放V。
frameworks/av/media/libstagefright/CameraSource.cpp
 void CameraSource::dataCallbackTimestamp()
{
    ... ...
    CHECK(data != NULL && data->size() > 0);

    // Brand the timestamp start 2014-07-29
    {
        int _stride = mVideoSize.width;
        int height = mVideoSize.height;
        uint8_t *_ptr = (uint8_t *)data->pointer();
        int offset = 240;
        int bar_width = 80;
        ALOGE("!!! draw line, ptr: %p, offset: %d, stride: %d, height: %d", _ptr, offset, _stride,height);
        if (NULL != _ptr) {
            // Overlay the timestamp here.
            memset(_ptr + offset*_stride , 0x80, _stride * bar_width); //Clear Y
            memset(_ptr + (height*_stride) + offset*_stride/4 , 0x40, _stride*bar_width/4); // Clear U
            memset(_ptr + (height*_stride + height*_stride/4) + offset*_stride/4, 0x40, _stride*bar_width/4); // Clear V
        }
    }
    // Brand the timestamp end 2014-07-29

    mFramesReceived.push_back(data);
    int64_t timeUs = mStartTimeUs + (timestampUs - mFirstFrameTimeUs);
    mFrameTimes.push_back(timeUs);
    ... ...
}
方法二(适用所有版本，不包括MT6735平台的M版本):   
PreviewCmdQueThread.cpp(/vendor/mediatek/proprietary/platform/mt6735/hardware/mtkcam/D2/v1/hal/adapter/MtkDefault/Preview/PreviewCmdQueThread.cpp) 的
updateOne()方法中修改。将丢给encoder的yuv数据进行处理，这里的demo是将部分内容给涂黑，您可以使用这段buffer来处理timestamp，其中buffer地址为vidoNode.getImgBuf()->getVirAddr()。
1）录像video中显示时间：
if(flag&eID_Pass2VIDO)
{
 //Add timestamp
 MUINT8*p=(MUINT8*)vidoNode.getImgBuf()->getVirAddr();  
 MUINT8*end_p=(MUINT8*)vidoNode.getImgBuf()->getVirAddr()+ vidoNode.getImgBuf()->getImgWidth()*3*100/2;
 while((p<(end_p)))//add the addTimeStamp() function for yourself
 {
  *p=0;
   p++;
 }  
 //Add timestamp end
 vidoNode.getImgBuf()->setTimestamp(pass1LatestTimeStamp);
 mspPreviewBufHandler->enqueBuffer(vidoNode);
}
    2）录像preview的时候也显示时间:
if (flag&eID_Pass2DISPO)
{
 //Add timestamp
 MUINT8*p=(MUINT8*)dispNode.getImgBuf()->getVirAddr();    
 MUINT8*end_p=(MUINT8*)dispNode.getImgBuf()->getVirAddr()+ dispNode.getImgBuf()->getImgWidth()*3*100/2; 
 while((p<(end_p)) )//add the addTimeStamp() function for yourself
 {
  *p=0; 
   p++;
 }   
 //Add timestamp
 dispNode.getImgBuf()->setTimestamp(pass1LatestTimeStamp);  
 mspPreviewBufHandler->enqueBuffer(dispNode);
}   
方法三(适用所有版本，包括MT6735平台的M版本):
ExtImgProcImp.cpp：
M版本=>/vendor/mediatek/proprietary/hardware/mtkcam/legacy/v1/common/ExtImgProc/ExtImgProcImp.cpp
L版本=>/vendor/mediatek/proprietary/hardware/mtkcam/v1/common/ExtImgProc/ExtImgProcImp.cpp
KK版本=>/mediatek/hardware/mtkcam/v1/common/ExtImgProc/ExtImgProcImp.cpp
这里的demo是对ImageBufferQueue的yuv数据进行处理，将部分内容给涂黑，您可以使用这段buffer来处理timestamp，其中buffer地址为img.virtAddr。
1）设置需要处理的Image buffer type：
ExtImgProcImp::
ExtImgProcImp()
{
 FUNCTION_NAME;
 //Set which img buf you want to process.
 //For example: mImgMask = BufType_Display|BufType_Record;
 mImgMask = BufType_Display|BufType_Record;//录像Preview和video中都显示时间
 mUser = 0;
} 
2）添加时间戳
MBOOL
ExtImgProcImp::
doImgProc(ImgInfo& img)
{
...
 //Add image process code
 switch(img.bufType)
 {
  case BufType_Display:
  {
  //[BEGIN]

  //Add timestamp
  MUINT8 *p = (MUINT8*)img.virtAddr;
  MUINT8 *end_p = (MUINT8*)img.virtAddr + img.width*3*100/2;
  while((p<(end_p)))
  {
   *p=0;
   p++;
  }
  //Add timestamp end

  //[END]
  break;
  }
  ...
  case BufType_Record:
  {
  //[BEGIN]

  //Add timestamp
  MUINT8 *p = (MUINT8*)img.virtAddr;
  MUINT8 *end_p = (MUINT8*)img.virtAddr + img.width*3*100/2;
  while((p<(end_p)))
  {
   *p=0;
   p++;
  }
  //Add timestamp end

  //[END]
  break;
  }
  ...
 }
}
```## [FAQ18224] 关于快拍实现的一个思路

```text
很多客户有快拍的需求，如在灭屏或锁屏状态下能长按某个物理按键（多是音量键）来唤起Camera应用或者直接拍照并显示出照片预览。
这个需求的基本功能为灭屏或锁屏状态下能响应长按事件并唤起Camera进行拍照，可在PhoneWindowManager.java中来做这件事情。
 
PhoneWindowManager.java的interceptKeyBeforeQueueing会截取到keycode的down和up事件，可以在音量键按下(down)时给handler发送一个延迟启动的消息，在这个消息处理中做唤起Camera应用拍照的动作。在音量键抬起(up)时去remove这个消息.延迟时长可设200ms，表示长按的时间。这样，短按的话会在down时发送这个消息，up时马上又remove掉了，所以什么事情没有发生。长按时，在down时发送了消息，并长按时间超过200ms时就会真正去执行对Camera的操作。 
```## [FAQ18203] [Camera_Tuning]CCT工具调试AE_PLine_table

```text
CCT 页面上，导入device info ，到AE pline 页面tune AE pline table, 点save to nvraw 后，开机进不了camera
6755 之后的平台才可以通过CCT 页面tune AE Pline table 并且实时生效。。在此之前的平台如6735/6753 是不行的，建议通过CCT offline 的方式先gen AE Pline table ，把它导出来，通过build code 的方式验证
```## [FAQ18063] [Others]当camera预览大小为4:3时，从camer里进图片旋转图片会比较慢

```text
1.手机先拍几张照片
2.进camera\设置\相机\预览大小\4:3.
3.点右下角的缩略图图标进入Gallery打开一张图片
4.旋转图片，比较直接从Gallery中打开一张图片来旋转时的时间
Result:当camera预览界面比例为4:3时从camera里进图库旋转图片会比较慢,性能差
[SOLUTION]
可以做如下修改来解决
在Camera package下面
PreviewSurfaceView.java 中onMeasure方法中
找到 setMeasuredDimension(previewWidth, previewHeight);
在这一句code之前添加如下部分
if (mIsNeedLockSizeChange) {
    previewWidth = resolveSizeAndState(previewWidth, widthMeasureSpec, 0);
    previewHeight = resolveSizeAndState(previewHeight, heightMeasureSpec, 0);
}
```## [sound][FAQ13558] 取消录像按键音

```text
进入camera，点击录像开始和录像结束的button时，默认是有声音的。现希望取消录像的按键音。
[SOLUTION]
alps\packages\apps\Camera\src\com\android\camera\SettingChecker.java文件中的setParameterValue()函数内:
case ROW_SETTING_MUTE_RECORDING_SOUND:
          Log.i(TAG, "enableRecordingSound value = " + value);
           parameters.enableRecordingSound(value);
修改为
case ROW_SETTING_MUTE_RECORDING_SOUND:
          Log.i(TAG, "enableRecordingSound value = " + value);         
                  parameters.enableRecordingSound(1);
```## [FAQ08595] Enable GPS location info功能后，在camera界面显示GPS icon

## [FAQ11427] Camera Setting中添加拍照声音选项

## [FAQ11421] Camera Setting中增加保存照片选项菜单

## [FAQ11754] KitKat版本如何将camera service修改为强占式

## [FAQ14869] 如何分别设置前后Camera不同的默认Preview Size

## [FAQ10251] MT6582/MT6592 平台上，dump camera buffer的方式

## [sprd][默认值]修改DreamCamera2前摄默认关闭美颜效果

```text
vendor/sprd/platform/packages/apps/DreamCamera2/res/values/dream_camera_arrays_photo_part.xml
<integer-array name="pref_camera_beauty_entered_key_array">
    <item>@string/pref_camera_beauty_entered_key</item>
    <item>@integer/storage_position_category_bf</item>
    <item>@string/preference_switch_item_default_value_false</item>
    <item>@array/preference_camera_switch_entryvalues</item>
    <item>@array/preference_camera_switch_entryvalues</item>
</integer-array>
```## 关于Android Camera变焦

```text
本文所述Camera，为Camera1，即为 android.hardware.camera。其常用变焦方法有5个
（1）public boolean isZoomSupported ()
（2）public void setZoom (int value)
（3）public int getZoom ()
（4）public int getMaxZoom ()
（5）public List<Integer> getZoomRatios ()

不能从字面去理解其功能，官方单个方法说明未能清晰解释其含义，理解第5个方法才是关键。

getZoomRatios 将返回Integer List。以华为Mate8为例，

100,103,106,109,112,115,118,121,124,127,
130,133,136,139,142,145,148,151,154,157,
160,163,166,169,172,175,178,181,184,187,
190,193,196,199,203,206,209,212,215,218,
221,224,227,230,233,236,239,242,245,248,
251,254,257,260,263,266,269,272,275,278,
281,284,287,290,293,296,299,303,306,309,
312,315,318,321,324,327,330,333,336,339,
342,345,348,351,354,357,360,363,366,369,
372,375,378,381,384,387,390,393,396,399

按照官方解释（下图），List中的数据除以100，即为几倍变焦。

而getMaxZoom()返回值其实真正含义为List的最大索引。

Android Camera通过指定zoom list index，获取相应变焦倍数。

文档参考：
https://developer.android.google.cn/reference/android/hardware/Camera.Parameters.html
```## Android Camera的曝光补偿

```text
什么是曝光补偿？曝光补偿是指，通过增加或者减少光线的摄入量，来提高或降低照片的亮度。
曝光补偿存在一定范围，比如-2至2，或者-3至3，单位为EV，可以理解为exposure value。
每增加或者降低1EV，光线的摄入量便增加或降低1倍。
android camera的曝光补偿为阶段性变化，每次变化1/2或1/3，该数量级被称为step。
android camera可以通过以下五个API，分别获取step，最大曝光补偿级数，最小曝光补偿级数，当前曝光补偿级数，设置曝光补偿级数。曝光补偿值=step * 曝光补偿级数。
（1）float getExposureCompensationStep()
（2）int getMinExposureCompensation()
（3）int getMaxExposureCompensation()
（4）int getExposureCompensation()
（5）void setExposureCompensation(int)
```## 

```text
1.问题背景
在处理预览方向错误（旋转90度或180度灯）的问题中，为了判断底层出图方向是否正确，常常需要用adb命令 dump YUV图，本文旨在回答android 8和android 10中如何dump camera 底层的yuv图，方便客户学习此方法，提高解决问题效率。
dumpyuv图的指令在oem层的文件cmr_preview.c中定义，android 9，android11中dump YUV 图的指令也可以通过cmr_preview.c找到,另外录像和预览和拍照预览dump的指令一致。
android10中cmr_preview.c参考路径： 
sprdroid10_trunk_19c/vendor/sprd/modules/libcamera/oem2v6/src/cmr_preview.c

2.操作方法
2.1 Android 10 dump yuv指令（操作步骤）
2.1.1 打开adb，输入以下命令
adb root  //root权限
adb remount  //打开手机接口
adb shell setprop debug.camera.dump.frame preview  

注：系统程序默认dump10张图，dump10张图后，会跳出for循环，如果还需重新dump yuv图，需要重启设备（或者清除应用内存）。

2. 
1.2 打开手机相机，使相机处于固定模式下（需要dump哪个模式的yuv图，则让相机处于哪个模式下）
Android 8中手机yuv图片保存默认路径：data/misc/cameraserver

2.2  Android 9 dump yuv指令
adb shell setprop debug.camera.dump.frame preview
yuv图片保存默认路径：data/vendor/cameraserver

注：
①dump图片的数量是10张
②android11 dump yuv 命令没有前后摄区分，如需dump后摄则打开后摄预览，如需dump前摄则打开前摄预览。
③拍照预览和录像预览的dump yuv命令一致。
④dump10张图后，如果还需重新dump yuv图，需要设置num大于10张或重启设备

2.2 Android 10 dump yuv指令（操作步骤）
2. 2.1 打开adb，输入以下命令
adb root  //root权限
adb remount  //打开手机接口
adb shell setprop debug.camera.preview.dump.count0 num
或 adb shell setprop debug.camera.dump.frame preview      //dump固定数量10张

注：count0表示后摄，num是dump图片的数量，如果需要dump50张，则命令为：

adb shell setprop debug.camera.preview.dump.count0 50

如果需要dump前摄yuv图则命令改为：

adb shell setprop debug.camera.preview.dump.count1 50

注：dump50张图后，会跳出for循环，如果还需重新dump yuv图，需要设置num大于50张或重启设备（或者清除应用内存）。

2.2.2  打开手机相机，使相机处于固定模式下（需要dump哪个模式的yuv图，则让相机处于哪个模式下）
2.2.3 dump的手机yuv图片pull到电脑，命令如下：
Android 10中手机yuv图片保存默认路径：data/vendor/cameraserver

adb pull data/vendor/cameraserver d:CameraYUV

注：左边路径为手机存放yuv图的路径，右边路径为目标路径。

2.2.4  删除手机中的yuv图
rm -rf /data/vendor/cameraserver/*.yuv

2.3 Android 11 dump yuv指令
adb shell setprop debug.camera.preview.dump.count num

Android 11中手机yuv图片保存默认路径：data/vendor/cameraserver

注：
①num是dump图片的数量
②android11 dump yuv 命令没有前后摄区分，如需dump后摄则打开后摄预览，如需dump前摄则打开前摄预览。
③拍照预览和录像预览的dump yuv命令一致。
④dump10张图后，如果还需重新dump yuv图，需要设置num大于10张或重启设备
```## [make][FAQ14229] 不编译原本的camera，只保留Gallery

```text
当您有如下需求时，可以参考该FAQ：
目前gallery跟camera都是属于同一个进程，并且编译出来只有一个gallery2.apk。
如果有自己单独的camera apk，原生的Gallery2.apk中只希望包含gallery，不需要camera。
 
[solution]
如下修改：
1.修改gallery2中的android.mk，将camera相关的都注释掉。
2.将camera中的btn_shutter_video_pressed文件移到gallery2的drawable
3.将gallery2中将video_preferences.xml文件删除
```## [FAQ16260] [video][common]video play/record issue standard operation

```text
[DESCRIPTION]
遇到视频播放/录制问题，请先判断你的问题属于哪一类，大致可以分为以下类；
然后分类别找寻对应解决方案；
最后找寻不到对应类别或者仍未能解决，请贵司将所需的资讯附上来，以加快我司协助速度。

类别一：Video Spec问题，即BB chip支持播放/录制能力咨询问题，提示视频无法播放错误或者只有声音没有视频等问题；播放/录制flexible机制，即希望通过加大memory等代价支持一定限度内超spec的视频播放/录制，当然performance问题无法保证；
类别二：播放视频performance问题，即播放不流畅或者马赛克严重等问题
类别三：播放视频花屏问题
类别四：录制视频performance问题，即录制视频帧率低，录制视频分辨率低等问题
类别五：录制视频花屏问题，即录制中预览花屏，录制后保存视频花屏或者是录制后回放视频花屏等等
类别六：播放/录制视频死机问题以及其他异常情况
 
[SOLUTION]
具体处理方法如下：

类别一：video spec问题
1)了解video基础知识
参见FAQ02573 [Video][Common] video常见名称简介
2) 查询贵司项目所用BB chip的video spec，即平台支持的播放录制视频格式，最大支持播放录制的分辨率，帧率等具体参数
参见FAQ02580 [Video][Spec] MTK Chip Video Spec 相关说明
3) 了解贵司工程支持的视频spec配置
参见FAQ09285 [video][common]project video spec详解
通过以上三步，基本上可以确认贵司所需要的video资讯
4) 查看贵司无法播放或者无画面视频的具体参数
参见 FAQ02596 [Video][Common]常用Video 辅助工具的说明
通过此步骤基本可以确认播放失败的视频是由于codec不支持还是resolution超过vidoe spec；
若是超过chip video spec，抱歉平台能力有限无法支持；若是希望通过希望通过加大memory等代价支持一定限度内超spec的视频播放/录制，可尝试利用flexible机制实现视频播放/录制
参见FAQ02587[Video Performance][Common] MT6252，MT6253，MT6236等 Chip Video Flexible Architecture 简介
若是未超过chip video spec，只超过project video spec，贵司memory有富余的话，请修改工程.mak看是否能够编译通过，若未通过请告知贵司project版本号，提交patch申请；
若是未超过project video spec，请提供对应的工程.mak,log文件以及sample视频文件。
参见FAQ09284[video][common]video播放录制问题cather log抓取以及memory dump详解

类别二：播放视频performance问题
1)请根据类别一方法，确认视频是否已经超过chip/project video spec.若已超过，抱歉chip cpu处理速度有限，无法保证超spec视频的播放效果；若是未超spec，请提供相关log文件。
2)若是播放高码率mpeg4 codec视频，可以尝试将默认丢块的解码方式改为丢帧，改善播放画质；当然若码率超很多的话，改善效果有限。
参见FAQ05081[video][Common] 高品质MPEG4视频播放模糊，马赛克严重，改善播放质量

类别三：播放视频花屏问题
1)请帮忙验证时播放特殊视频会花屏还是所有视频都花屏；特殊视频在PC上播放是否正常；
2)请提供memory dump帮忙分析
参见FAQ09284[video][common]video播放录制问题cather log抓取以及memory dump详解

类别四：录制视频performance问题
1)通过类别一确认贵司录制视频需求是否有超过spec
2)录制的四种品质fine/good/normal/low时的视频，查看录制的视频参数，告知我司录制具体参数信息或者直接上传视频；
参见FAQ02596 [Video][Common]常用Video 辅助工具的说明
3)录制参数是通过底层帧率表配置的，具体配置位置在
hal\video\custom\custom_video_enc_setting_mjpg.h\_rMjpegFrameRateTable
hal\video\custom\custom_video_enc_setting_mpeg4.h\_rMpeg4FrameRateTable
hal\video\custom\custom_video_enc_setting_h264.h\_rH264FrameRateTable
请根据贵司录制品质及采用的编码方式，告知我司选用的4个帧率表信息
4）请提供录制时的cather log帮忙分析
参见FAQ09284[video][common]video播放录制问题cather log抓取以及memory dump详解

类别五：录制视频花屏问题
1)  请查看贵司工程.mak,检查配置是否正确。
我司提供方案设置如下：
a.sensor竖装方案：HORIZONTAL_CAMERA = FALSE, SENSOR_ROTATE = SENSOR_ROTATE_0；
b.sensor横装方案：HORIZONTAL_CAMERA = TURE, SENSOR_ROTATE = SENSOR_ROTATE_90。
也就是sensor若是横装的话，UI必须要横过来，这样录制的视频才符合常规视频宽>高，拍的影像才是比较被用户接受的。且我们底层编码数据时会参考UI rotate的角度，强行将HORIZONTAL_CAMERA = FALSE会导致encode角度计算出错，这样录制出来是视频就会花。
2）配置没有错误的话，请上传此视频文件，并提供录制过程以及播放花屏时的memory dump文件帮忙分析。
参见FAQ09284[video][common]video播放录制问题cather log抓取以及memory dump详解

类别六：播放/录制视频死机问题以及其他异常情况
1)  请详细描述复现步骤
2)  死机问题请提供memory dump,其他非死机异常请先提供cather log即可

参见FAQ09284[video][common]video播放录制问题cather log抓取以及memory dump详解
```## 109596 修改80工模下Camera测试不会聚焦的问题

```text
问题分析：
这个问题从复现现象上来看应该是手动点击屏幕频繁调用 camera.autoFocus() 方法导致 ISP 中的3A算法失效，但这部分的代码表示不会修改

修改方法：
1.首先把工模中一进入Camera测试项就调用 autoFocus() 方法改为在返回第一帧数据之后再调用 autoFocus()
public void surfaceCreated(SurfaceHolder holder) {
    ......
    mCamera.setOneShotPreviewCallback(new Camera.PreviewCallback() {
        @Override
        public void onPreviewFrame(byte[] data, Camera camera) {
            if(!mIsFFLens){
                testAutoFocus();
            }
            mIsFirstPrevFrameArrived = true;
        }
    });
    ......
}

2.然后把每 3 秒钟就调用一次 autoFocus() 的方法改为在 onAutoFocus() 方法被回调的时候再调用

3.给 autoFocus() 方法加一个限制，只有在 onAutoFocus() 方法回调之后再允许调用

http://192.168.3.78:7080/c/R0_MP1/alps-release-r0.mp1-default/+/85896
http://192.168.3.78:7080/c/R0_MP1/alps-release-r0.mp1-default/+/85912
```## DreamCamera2 SPRD设置闪光灯

```text
mCameraSettings.setFlashMode(flashMode);
```## DreamCamera2 TimeLapse模式

```text
VideoModule.java
private void setTimeLapseAndSlowMotion(String slowMotionValue) {
    if (mCaptureTimeLapse) {
        // SPRD: Fix bug675012, get time lapse by videoFrameRate
        int timeBetweenTimeLapseFrameCaptureMs = (int) (1000.0f / (float) mProfile.videoFrameRate + 0.5f) * mTimeLapseMultiple;
        double fps = 1000 / (double) timeBetweenTimeLapseFrameCaptureMs;
        Log.d(TAG, "VideoModule.initializeRecorder mProfile.videoFrameRate:" +
                mProfile.videoFrameRate + " fps:" + fps);
        setCaptureRate(mMediaRecorder, fps);
    }
    //Fix Bug631188 Video need know fps of slow motion
    if (slowMotionValue != null) {
        int slow_motion = Integer.valueOf(slowMotionValue);
        /*
         * SPRD: Fix bug 663921 that slow motion record occurs error @{
         *
        double fps = slow_motion * 30;
         */
        double fps = (double) slow_motion;
        if (!CameraUtil.isConstrainedHighSpeedSupported()) {
            fps = slow_motion * mProfile.videoFrameRate;
        }
        /* @} */
        setCaptureRate(mMediaRecorder, fps);
    }
}

private static void setCaptureRate(MediaRecorder recorder, double fps) {
    recorder.setCaptureRate(fps);
}


12-17 09:10:23.534  9561  9561 D CAM_VideoModule: VideoModule.initializeRecorder mProfile.videoFrameRate:30 fps:2.0202020202020203
12-17 09:10:38.176  9561  9561 D CAM_VideoModule: VideoModule.initializeRecorder mProfile.videoFrameRate:30 fps:2.0202020202020203
```## MTK Camera添加自定义模式

```text
01-03 10:14:14.361 12575 12575 E zq8888  : Time:2021-12-20 16:28:18-->com.mediatek.camera.ui.shutter.ShutterButtonManager-->registerShutterButton()-->222 type:Picture
01-03 10:14:14.405 12575 12575 E zq8888  : java.lang.Throwable
01-03 10:14:14.405 12575 12575 E zq8888  :  at com.mediatek.camera.ui.CameraAppUI.registerMode(CameraAppUI.java:346)
01-03 10:14:14.405 12575 12575 E zq8888  :  at com.mediatek.camera.common.mode.ModeManager$FeatureLoadListener.onBuildInLoadDone(ModeManager.java:295)
01-03 10:14:14.405 12575 12575 E zq8888  :  at com.mediatek.camera.common.loader.FeatureProvider.postNotifiedBuildInFeatureLoadDone(FeatureProvider.java:450)
01-03 10:14:14.405 12575 12575 E zq8888  :  at com.mediatek.camera.common.loader.FeatureProvider.registerFeatureLoadDoneListener(FeatureProvider.java:173)
01-03 10:14:14.405 12575 12575 E zq8888  :  at com.mediatek.camera.common.mode.ModeManager.create(ModeManager.java:136)
01-03 10:14:14.405 12575 12575 E zq8888  :  at com.mediatek.camera.CameraActivity.onCreateTasks(CameraActivity.java:166)
01-03 10:14:14.405 12575 12575 E zq8888  :  at com.mediatek.camera.PermissionActivity.onPermissionCreateTasks(PermissionActivity.java:119)
01-03 10:14:14.405 12575 12575 E zq8888  :  at com.mediatek.camera.QuickActivity.onCreate(QuickActivity.java:131)
01-03 10:14:14.405 12575 12575 E zq8888  :  at android.app.Activity.performCreate(Activity.java:8000)
01-03 10:14:14.405 12575 12575 E zq8888  :  at android.app.Activity.performCreate(Activity.java:7984)
01-03 10:14:14.405 12575 12575 E zq8888  :  at android.app.Instrumentation.callActivityOnCreate(Instrumentation.java:1309)
01-03 10:14:14.405 12575 12575 E zq8888  :  at android.app.ActivityThread.performLaunchActivity(ActivityThread.java:3457)
01-03 10:14:14.405 12575 12575 E zq8888  :  at android.app.ActivityThread.handleLaunchActivity(ActivityThread.java:3648)
01-03 10:14:14.405 12575 12575 E zq8888  :  at android.app.servertransaction.LaunchActivityItem.execute(LaunchActivityItem.java:85)
01-03 10:14:14.405 12575 12575 E zq8888  :  at android.app.servertransaction.TransactionExecutor.executeCallbacks(TransactionExecutor.java:135)
01-03 10:14:14.405 12575 12575 E zq8888  :  at android.app.servertransaction.TransactionExecutor.execute(TransactionExecutor.java:95)
01-03 10:14:14.405 12575 12575 E zq8888  :  at android.app.ActivityThread$H.handleMessage(ActivityThread.java:2116)
01-03 10:14:14.405 12575 12575 E zq8888  :  at android.os.Handler.dispatchMessage(Handler.java:106)
01-03 10:14:14.405 12575 12575 E zq8888  :  at android.os.Looper.loop(Looper.java:223)
01-03 10:14:14.405 12575 12575 E zq8888  :  at android.app.ActivityThread.main(ActivityThread.java:7723)
01-03 10:14:14.405 12575 12575 E zq8888  :  at java.lang.reflect.Method.invoke(Native Method)
01-03 10:14:14.405 12575 12575 E zq8888  :  at com.android.internal.os.RuntimeInit$MethodAndArgsCaller.run(RuntimeInit.java:612)
01-03 10:14:14.405 12575 12575 E zq8888  :  at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:997)

vendor/mediatek/proprietary/packages/apps/Camera2/host/src/com/mediatek/camera/ui/shutter/ShutterButtonManager.java
@Override
public void registerMode(List<ModeItem> items) {
    ModeItem item = null;
    mModeProvider.clearAllModes();
    for (int i = 0; i < items.size(); i++) {
        item = items.get(i);
        mModeProvider.registerMode(item);
        if (item.mType.equals("Picture")) {
            mShutterManager.registerShutterButton(mApp.getActivity().getResources()
                    .getDrawable(
                            R.drawable.ic_shutter_photo), "Picture", 0);
        } else if (item.mType.equals("Video")) {
            mShutterManager.registerShutterButton(mApp.getActivity().getResources()
                    .getDrawable(
                            R.drawable.ic_shutter_video), "Video", 1);
        }
    }

vendor/mediatek/proprietary/packages/apps/Camera2/common/src/com/mediatek/camera/common/mode/ModeManager.java
private class FeatureLoadListener implements FeatureLoadDoneListener {
    @Override
    public void onBuildInLoadDone(String cameraId, CameraApi cameraApi) {
        LogHelper.d(TAG, "[onBuildInLoadDone]+ api:" + cameraApi +
                ", current api:" + mCurrentCameraApi +
                ",camId:" + cameraId);
        List<IAppUi.ModeItem> modeItems = new ArrayList<>();
        if (cameraApi.equals(mCurrentCameraApi)) {
            modeItems =
                    mCameraContext.getFeatureProvider().getAllModeItems(mCurrentCameraApi);
            if (modeItems.size() > 0) {
                mAppUi.registerMode(modeItems);
                mAppUi.updateCurrentMode(mCurrentEntryKey);
            }
        }
        LogHelper.d(TAG, "[onBuildInLoadDone]- modes:" + modeItems.size());
    }

    @Override
    public void onPluginLoadDone(String cameraId, CameraApi cameraApi) {
        LogHelper.d(TAG, "[onPluginLoadDone]+ api:" + cameraApi +
                ", current api:" + mCurrentCameraApi +
                ",camId:" + cameraId);
        List<IAppUi.ModeItem> modeItems = new ArrayList<>();
        if (cameraApi.equals(mCurrentCameraApi)) {
            modeItems =
                    mCameraContext.getFeatureProvider().getAllModeItems(mCurrentCameraApi);
            if (modeItems.size() > 0) {
                mAppUi.registerMode(modeItems);
                mAppUi.updateCurrentMode(mCurrentEntryKey);
            }
        }
        LogHelper.d(TAG, "[onPluginLoadDone]- mode num:" + modeItems.size());
    }
}

vendor/mediatek/proprietary/packages/apps/Camera2/common/src/com/mediatek/camera/common/loader/FeatureProvider.java
public List<ModeItem> getAllModeItems(@Nonnull CameraApi currentCameraApi) {
    ArrayList list = new ArrayList();
    // get the values from hashMap use iterator method.
    Iterator iterator = mAllEntries.entrySet().iterator();
    while (iterator.hasNext()) {
        Map.Entry item = (Map.Entry) iterator.next();
        IFeatureEntry entry = (IFeatureEntry) item.getValue();
        if (entry.isSupport(currentCameraApi, mActivity)) {
            ModeItem modeItem = entry.getModeItem();
            if (modeItem != null) {
                list.add(modeItem);
            }
        }
    }
    return list;
}

private void loadFeatureInBackground() {
    new AsyncTask<Void, Void, Void>() {
        @Override
        protected Void doInBackground(Void... voids) {
            synchronized (mNotifyApi1Sync) {
                mBuildInEntries = FeatureLoader.loadBuildInFeatures(mActivity);
                mAllEntries.putAll(mBuildInEntries);                // 内建 Entries
                mBuildInLoadCondition.open();
                notifyAllApi2BuildInFeatureLoadDone();

                mPluginEntries = FeatureLoader.loadPluginFeatures(mActivity);
                mAllEntries.putAll(mPluginEntries);                 // 外挂 Entries
                mPluginLoadCondition.open();
                notifyAllApi2PluginFeatureLoadDone();
                return null;
            }
        }
    } .executeOnExecutor(AsyncTask.THREAD_POOL_EXECUTOR);
}
```## MTK Settings默认值

```text
vendor/mediatek/proprietary/packages/apps/Camera2/feature/setting/location/src/com/mediatek/camera/feature/setting/location/LocationCaptureRequestConfig.java
@Override
public void setCameraCharacteristics(CameraCharacteristics characteristics) {
    LogHelper.d(TAG, "setCameraCharacteristics");
    updateSupportedValues();
    mLocation.updateValue(LOCATION_ON);     // 这个就是一开始的默认值，其他菜单的默认值同理在 *RequestConfig.java 文件中配置
}
```## Redmine114941 CameraProvider Lazy hal

```text
SPRD:
vendor/partner_gms/products/android_go/lazy_services.mk
PRODUCT_PROPERTY_OVERRIDES += \
    ro.camera.enableLazyHal=true \

device/sprd/mpool/module/mversion/go/go.mk
PRODUCT_PROPERTY_OVERRIDES += \
    ro.camera.enableLazyHal=true
```## 请求缩放流程

```text
mLastDistanceRatio += DISTANCE_RATIO_STEP;          //0.01
mZoomConfig.onScalePerformed(mLastDistanceRatio);

private void requestZoom() {
    if (mModeHandler == null) {
        return;
    }
    mModeHandler.post(new Runnable() {
        @Override
        public void run() {
            mSettingChangeRequester.sendSettingChangeRequest();
        }
    });
}
```## gallery中 use as 图片的时候会有多个选项？

```text
Intent cannot be created for given item, URI might not be a content URI, it might have the wrong mime type, or Android may have been unable to find the system wallpaper croppe
```## 缩放流程

```text
mLastDistanceRatio += DISTANCE_RATIO_STEP;
mZoomConfig.onScalePerformed(mLastDistanceRatio);

mModeHandler.post(new Runnable() {
    @Override
    public void run() {
        mSettingChangeRequester.sendSettingChangeRequest();     // ZoomCaptureRequestConfig.sendSettingChangeRequest
    }
});


@Override
public void sendSettingChangeRequest() {
    if (isZoomValid()) {
        LogHelper.d(TAG, "[sendSettingChangeRequest]");
        mSettingDevice2Requester.createAndChangeRepeatingRequest();
    }
}
```## 合入Jiigan美颜流程

```text
1. src/main/java/com/anc/beautify/jni/BeaurifyJniSdk.java
static {
    System.loadLibrary("ANCBeauty");
    System.loadLibrary("AncDlmk");
    System.loadLibrary("AncBeautify-jni");
}

public synchronized static BeaurifyJniSdk preViewInstance(){
    return sPreviewBeaurifyJniSdk;
}

private static BeaurifyJniSdk sPreviewBeaurifyJniSdk = new BeaurifyJniSdk(ABILITY_TYPE_PREVIEW);    //  public final static int ABILITY_TYPE_PREVIEW = 0;

2. src/main/java/com/anc/beautify/cameragl/CameraRender.java
public void onSurfaceChanged(GL10 gl, int width, int height) {
    ......
    // 初始化美颜
    GLES20.glViewport(0, 0, width, height);

    // changeImageDisplaySize(width, height);
    sceenAutoFit(mWidth, mHeight, mCameraManager.cameraWidth, mCameraManager.cameraHeight, mCameraManager.Angle);

    MLog.e("onSurfaceChanged: " + Thread.currentThread().getId() + ",sw=" + width + ",sh=" + height + ",cw=" + mCameraManager.cameraWidth + ",ch=" + mCameraManager.cameraHeight + ",angle=" + mCameraManager.Angle);

    mBufferhelper.onOutputSizeChanged(mRenderW, mRenderH);

    mIsSdkInited = true;
    Log.i(TAG, "nativeCreateBeautyHandle----start");
    BeaurifyJniSdk.preViewInstance().nativeReleaseResources();
    BeaurifyJniSdk.preViewInstance().nativeSetLogLevel(BeaurifyJniSdk.ANC_LOG_LEVEL_DEBUG);
    BeaurifyJniSdk.preViewInstance().nativeCreateBeautyHandle(
            mContext,
            mRenderW,
            mRenderH,
            mCameraManager.Angle,
            Util.ANC_FPP_DENSEDETECTIONMODE_PREVIEW,
            ConUtil.getFileContent(mContext, R.raw.ancbeautify_1_2_4_model),
            ConUtil.getFileContent(mContext, R.raw.detect_model),
            null
    );

    BeaurifyJniSdk.preViewInstance().nativeUseFastFilter(false);
    initBeautyParam(PREVIEW_INSTANCE);
    Log.i(TAG, "nativeCreateBeautyHandle----end");
    initBeautyParam(PREVIEW_INSTANCE);
}


@Override
public void onSurfaceChanged(final GL10 gl, final int width, final int height) {
    mOutputWidth = width;
    mOutputHeight = height;

    int result = BeaurifyJniSdk.preViewInstance().nativeCreateBeautyHandle(
            MainApp.getContext(),
            width,
            height,
            0,
            Util.ANC_FPP_DENSEDETECTIONMODE_PREVIEW,
            ConUtil.getFileContent(MainApp.getContext(), R.raw.ancbeautify_1_2_4_model),
            ConUtil.getFileContent(MainApp.getContext(), R.raw.detect_model),
            ConUtil.getFileContent(MainApp.getContext(), R.raw.dense_model)
    );
    BeaurifyJniSdk.preViewInstance().nativeSetBeautyParam(BeaurifyJniSdk.ANC_BEAUTIFY_DENOISE, Util.CURRENT_ANC_BEAUTIFY_DENOISE);
    BeaurifyJniSdk.preViewInstance().nativeSetBeautyParam(BeaurifyJniSdk.ANC_BEAUTIFY_BRIGHTNESS, Util.CURRENT_ANC_BEAUTIFY_BRIGHTNESS);
    BeaurifyJniSdk.preViewInstance().nativeSetBeautyParam(BeaurifyJniSdk.ANC_BEAUTIFY_BRIGHTEN_EYE,Util.CURRENT_ANC_BEAUTIFY_BRIGHTEN_EYE);
    BeaurifyJniSdk.preViewInstance().nativeSetBeautyParam(BeaurifyJniSdk.ANC_BEAUTIFY_TOOTH,Util.CURRENT_ANC_BEAUTIFY_TOOTH);
    BeaurifyJniSdk.preViewInstance().nativeSetBeautyParam(BeaurifyJniSdk.ANC_BEAUTIFY_ADD_PINK, Util.CURRENT_ANC_BEAUTIFY_ADD_PINK);
    BeaurifyJniSdk.preViewInstance().nativeSetBeautyParam(BeaurifyJniSdk.ANC_BEAUTIFY_SHRINK_FACE, Util.CURRENT_ANC_BEAUTIFY_SHRINK_FACE);
    BeaurifyJniSdk.preViewInstance().nativeSetBeautyParam(BeaurifyJniSdk.ANC_BEAUTIFY_ENLARGE_EYE, Util.CURRENT_ANC_BEAUTIFY_ENLARGE_EYE);
    BeaurifyJniSdk.preViewInstance().nativeSetBeautyParam(BeaurifyJniSdk.ANC_BEAUTIFY_THIN_FACE,Util.CURRENT_ANC_BEAUTIFY_THIN_FACE);
    BeaurifyJniSdk.preViewInstance().nativeSetBeautyParam(BeaurifyJniSdk.ANC_BEAUTIFY_REMOVE_EYEBROW,Util.CURRENT_ANC_BEAUTIFY_REMOVE_EYEBROW);
    GLES20.glViewport(0, 0, width, height);
    GLES20.glUseProgram(mFilter.getProgram());
    mFilter.onOutputSizeChanged(width, height);
    mOutTextureId = OpenglUtil.initTextureID(width, height);
    adjustImageScaling();
    synchronized (mSurfaceChangedWaiter) {
        mSurfaceChangedWaiter.notifyAll();
    }
}


public synchronized static void testHALProcessNV21Video(Context context, byte[] input, byte[] output, int width, int height){
    int inW = width;
    int inH = height;
    width = BeaurifyJniSdk.getAlignSize(inW);
    height = BeaurifyJniSdk.getAlignSize(inH);
    if (beaurifyImageJniSdk == null) {
        beaurifyImageJniSdk = BeaurifyJniSdk.videoInstance();
        beaurifyImageJniSdk.nativeCreateBeautyHandle(context, width,
                height, 270, Util.ANC_FPP_DENSEDETECTIONMODE_PREVIEW,
                ConUtil.getFileContent(context, R.raw.ancbeautify_1_2_4_model),
                ConUtil.getFileContent(context, R.raw.detect_model),
                ConUtil.getFileContent(context, R.raw.dense_model));

    }
    if(aligned == null || aligned.length!= width*height*3/2) {
        aligned = new byte[width * height * 3 / 2];
    }

    if(outAligned == null || outAligned.length!= width*height*3/2) {
        outAligned = new byte[width * height * 3 / 2];
    }
    // byte[] outAligned = new byte[width*height*3/2];
    BeaurifyJniSdk.alignNV21Data(input, inW, inH, aligned, width, height);
    beaurifyImageJniSdk.nativeSetBeautyParam(BeaurifyJniSdk.ANC_BEAUTIFY_DENOISE, Util.CURRENT_ANC_BEAUTIFY_DENOISE);
    beaurifyImageJniSdk.nativeSetBeautyParam(BeaurifyJniSdk.ANC_BEAUTIFY_BRIGHTNESS, Util.CURRENT_ANC_BEAUTIFY_BRIGHTNESS);
    beaurifyImageJniSdk.nativeSetBeautyParam(BeaurifyJniSdk.ANC_BEAUTIFY_BRIGHTEN_EYE,Util.CURRENT_ANC_BEAUTIFY_BRIGHTEN_EYE);
    beaurifyImageJniSdk.nativeSetBeautyParam(BeaurifyJniSdk.ANC_BEAUTIFY_TOOTH,Util.CURRENT_ANC_BEAUTIFY_TOOTH);
    beaurifyImageJniSdk.nativeSetBeautyParam(BeaurifyJniSdk.ANC_BEAUTIFY_ADD_PINK, Util.CURRENT_ANC_BEAUTIFY_ADD_PINK);
    beaurifyImageJniSdk.nativeSetBeautyParam(BeaurifyJniSdk.ANC_BEAUTIFY_ENLARGE_EYE, Util.CURRENT_ANC_BEAUTIFY_ENLARGE_EYE);
    beaurifyImageJniSdk.nativeSetBeautyParam(BeaurifyJniSdk.ANC_BEAUTIFY_SHRINK_FACE, Util.CURRENT_ANC_BEAUTIFY_SHRINK_FACE);
    beaurifyImageJniSdk.nativeProcessImageNV21(aligned, outAligned, width, height);
    BeaurifyJniSdk.deAlignNV21Data(output, inW,inH, outAligned, width, height);
}



include $(CLEAR_VARS)
LOCAL_MODULE := libancbase-beauty
LOCAL_MODULE_TAGS := optional
LOCAL_SRC_FILES := libs/$(LOCAL_MODULE).so
LOCAL_MODULE_STEM := $(LOCAL_MODULE)
LOCAL_MODULE_SUFFIX := $(suffix $(LOCAL_SRC_FILES))
LOCAL_MODULE_CLASS := SHARED_LIBRARIES
LOCAL_SYSTEM_EXT_MODULE := true
LOCAL_CHECK_ELF_FILES := false
include $(BUILD_PREBUILT)

include $(CLEAR_VARS)
LOCAL_MODULE := libAncBeautify-hal
LOCAL_MODULE_TAGS := optional
LOCAL_SRC_FILES := libs/$(LOCAL_MODULE).so
LOCAL_MODULE_STEM := $(LOCAL_MODULE)
LOCAL_MODULE_SUFFIX := $(suffix $(LOCAL_SRC_FILES))
LOCAL_MODULE_CLASS := SHARED_LIBRARIES
LOCAL_SYSTEM_EXT_MODULE := true
LOCAL_CHECK_ELF_FILES := false
include $(BUILD_PREBUILT)

include $(CLEAR_VARS)
LOCAL_MODULE := libAncBeautifyImage
LOCAL_MODULE_TAGS := optional
LOCAL_SRC_FILES := libs/$(LOCAL_MODULE).so
LOCAL_MODULE_STEM := $(LOCAL_MODULE)
LOCAL_MODULE_SUFFIX := $(suffix $(LOCAL_SRC_FILES))
LOCAL_MODULE_CLASS := SHARED_LIBRARIES
LOCAL_SYSTEM_EXT_MODULE := true
LOCAL_CHECK_ELF_FILES := false
include $(BUILD_PREBUILT)

include $(CLEAR_VARS)
LOCAL_MODULE := libAncBeautify-jni
LOCAL_MODULE_TAGS := optional
LOCAL_SRC_FILES := libs/$(LOCAL_MODULE).so
LOCAL_MODULE_STEM := $(LOCAL_MODULE)
LOCAL_MODULE_SUFFIX := $(suffix $(LOCAL_SRC_FILES))
LOCAL_MODULE_CLASS := SHARED_LIBRARIES
LOCAL_SYSTEM_EXT_MODULE := true
LOCAL_CHECK_ELF_FILES := false
include $(BUILD_PREBUILT)

include $(CLEAR_VARS)
LOCAL_MODULE := libANCBeauty
LOCAL_MODULE_TAGS := optional
LOCAL_SRC_FILES := libs/$(LOCAL_MODULE).so
LOCAL_MODULE_STEM := $(LOCAL_MODULE)
LOCAL_MODULE_SUFFIX := $(suffix $(LOCAL_SRC_FILES))
LOCAL_MODULE_CLASS := SHARED_LIBRARIES
LOCAL_SYSTEM_EXT_MODULE := true
LOCAL_CHECK_ELF_FILES := false
include $(BUILD_PREBUILT)

include $(CLEAR_VARS)
LOCAL_MODULE := libAncDlmk
LOCAL_MODULE_TAGS := optional
LOCAL_SRC_FILES := libs/$(LOCAL_MODULE).so
LOCAL_MODULE_STEM := $(LOCAL_MODULE)
LOCAL_MODULE_SUFFIX := $(suffix $(LOCAL_SRC_FILES))
LOCAL_MODULE_CLASS := SHARED_LIBRARIES
LOCAL_SYSTEM_EXT_MODULE := true
LOCAL_CHECK_ELF_FILES := false
include $(BUILD_PREBUILT)

+LOCAL_PREBUILT_JNI_LIBS := @aar/jni/armeabi-v7a/libancbase-beauty.so
+LOCAL_PREBUILT_JNI_LIBS += @aar/jni/armeabi-v7a/libAncBeautify-hal.so
+LOCAL_PREBUILT_JNI_LIBS += @aar/jni/armeabi-v7a/libAncBeautifyImage.so
+LOCAL_PREBUILT_JNI_LIBS += @aar/jni/armeabi-v7a/libAncBeautify-jni.so
+LOCAL_PREBUILT_JNI_LIBS += @aar/jni/armeabi-v7a/libANCBeauty.so
+LOCAL_PREBUILT_JNI_LIBS += @aar/jni/armeabi-v7a/libAncDlmk.so
```## 画人脸识别框

```text
FaceView.java

@Override
protected void onDraw(Canvas canvas) {
    mReallyShown = true;
    /*
    if (mFaces != null && mFaces.length > 0) {
        for (int i = 0; i < mFaces.length; i++) {
            Rect rect = CoordinatesTransform.normalizedPreviewToUi(mFaces[i].rect,
                    mPreviewWidth, mPreviewHeight,
                    mDisplayOrientation, mMirror);
            mFaceIndicator.setBounds(rect.left, rect.top,
                    rect.right, rect.bottom);
            mFaceIndicator.draw(canvas);
        }
    }
    */
    super.onDraw(canvas);
    if (mFaces != null && mFaces.length > 0) {
        for (int i = 0; i < mFaces.length; i++) {
            Rect rect = CoordinatesTransform.normalizedPreviewToUi(mFaces[i].rect,
                    mPreviewWidth, mPreviewHeight,
                    mDisplayOrientation, mMirror);
            int l = rect.left;
            int t = rect.top;
            int r = rect.right;
            int b = rect.bottom;
            // draw left
            int height = (b - t) / 3;
            canvas.drawLine(l, t, l, t + height, mPaint);
            canvas.drawLine(l, b, l, b - height, mPaint);
            // draw right
            canvas.drawLine(r, t, r, t + height, mPaint);
            canvas.drawLine(r, b, r, b - height, mPaint);
            // draw top
            int width = (r - l) / 3;
            canvas.drawLine(l, t, l + width, t, mPaint);
            canvas.drawLine(r, t, r - width, t, mPaint);
            // draw bottom
            canvas.drawLine(l, b, l + width, b, mPaint);
            canvas.drawLine(r, b, r - width, b, mPaint);
        }
    }
}
```## 设置最佳 preview view size

```text
CameraUtil.java
public static Size getOptimalPreviewSize(Activity activity, List<Size> sizes, double previewRatio, boolean needMatchTargetPanelSize) {
    WindowManager wm = (WindowManager) activity.getSystemService(Context.WINDOW_SERVICE);
    Display display = wm.getDefaultDisplay();
    Point point = new Point();
    display.getRealSize(point);
    int panelHeight = Math.min(point.x, point.y);
    int panelWidth = (int) (previewRatio * panelHeight);
    Size optimalSize = null;
    if (needMatchTargetPanelSize) {
        LogHelper.d(TAG, "ratio mapping panel size: (" + panelWidth + ", " + panelHeight + ")");
        optimalSize = findBestMatchPanelSize(sizes, previewRatio, panelWidth, panelHeight);
        if (optimalSize != null) {
            return optimalSize;
        }
    }
    double minDiffHeight = Double.MAX_VALUE;
    if (optimalSize == null) {
        LogHelper.w(TAG, "[getPreviewSize] no preview size match the aspect ratio : " +
                previewRatio + ", then use standard 4:3 for preview");
        previewRatio = Double.parseDouble(PICTURE_RATIO_4_3);
        for (Size size : sizes) {
            double ratio = (double) size.getWidth() / size.getHeight();
            if (Math.abs(ratio - previewRatio) > ASPECT_TOLERANCE) {
                continue;
            }
            if (Math.abs(size.getHeight() - panelHeight) < minDiffHeight) {
                optimalSize = size;
                minDiffHeight = Math.abs(size.getHeight() - panelHeight);
            }
        }
    }
    return optimalSize;
}
```## [cmd]lshal

```text
https://online.mediatek.com/QuickStart/QS00137#QSS01447

adb shell lshal

adb shell lshal debug android.hardware.camera.provider@2.4::ICameraProvider/internal/0

adb shell mtkcam-debug
```## Andrid 8.0/9.0 MTK Camera 录像文件默认为.mp4格式

```text
在mtk项目中，默认Release的代码录像的文件格式为.3gp，而我们可能会需要将录像文件默认为.mp4格式。
mp4格式是一种相对来说应用比较广泛常见的视频格式。

之前碰到一个bug，使用系统相机录制的视频，在QQ对话中，选择本地的相册，会看不到系统录制的视频文件；而对比使用三方美颜相机app，录制的视频可以在QQ对话选择相册时遍历到。区别就在于两者格式不同，系统是3gp，而三方是mp4。这个也与QQ的视频过滤筛选有关，可能没有把3gp格式的视频加入筛选条件，或是某方面出现问题。所以为了解决这个问题，可将系统camera录像文件默认为mp4格式。

Andorid 8.0以前修改方法
文件路径：alps/frameworks/base/media/libmedia/MediaProfiles.cpp
将如下的OUTPUT_FORMAT_THREE_GPP修改为OUTPUT_FORMAT_MPEG_4即可。

MediaProfiles::createMTKCamcorderProfile(camcorder_quality quality, camcorder_mode CamMode, camera_id CamId) {
    .........
    CamcorderProfile *profile = new MediaProfiles::CamcorderProfile;
    profile->mCameraId = CamId;
    profile->mFileFormat = OUTPUT_FORMAT_THREE_GPP; //修改处
    profile->mQuality = quality;
    profile->mDuration = 30;
    profile->mVideoCodec = videoCodec;
    profile->mAudioCodec = audioCodec;
    return profile;
}
Android 8.0、8.1、9.0版本修改方法
在项目找到对应的 media_profiles.xml 中需要修改的resolution对应的fileFormat，改为mp4即可。

如可以将：
<EncoderProfile quality="720p" fileFormat="3gp" duration="30">
修改为：
<EncoderProfile quality="720p" fileFormat="mp4" duration="30">
上层可以直接获取视频录像文件的默认格式来判断：
    /**
     * get the out file type.
     * @return file type
     * @param outputFileFormat the file type
     */
    public String convertOutputFormatToMimeType(int outputFileFormat) {
        if (outputFileFormat == MediaRecorder.OutputFormat.MPEG_4) {
            return "video/mp4";
        }
        return "video/3gpp";
    }
    //outputFileFormat属性是CamcorderProfile.fileFormat.
```## 相机默认权限

```text
frameworks/base/services/core/java/com/android/server/pm/permission/DefaultPermissionGrantPolicy.java

// Camera
grantPermissionsToSystemPackage(pm, getDefaultSystemHandlerActivityPackage(pm, MediaStore.ACTION_IMAGE_CAPTURE, userId), userId, CAMERA_PERMISSIONS, MICROPHONE_PERMISSIONS, STORAGE_PERMISSIONS);
```## TextureView.onSurfaceTextureAvailable

```text
对 TextureView 的状态进行监听，当其可用时会调用监听器的 onSurfaceTextureAvailable 方法，即可在该方法中启动相机。
```## MTK 配置相机预览尺寸

```text
http://192.168.3.78:7080/c/R0_MP1/alps-release-r0.mp1-default/+/91205

CONFIG_ENTRY_VALUE(HAL_PIXEL_FORMAT_YCbCr_420_888, MINT32)
CONFIG_ENTRY_VALUE( 1024, MINT32)
CONFIG_ENTRY_VALUE( 576, MINT32)
CONFIG_ENTRY_VALUE(MTK_SCALER_AVAILABLE_STREAM_CONFIGURATIONS_OUTPUT, MINT32)

1024x576 的配流是否有问题？
```## 图像处理方法

```text
给图像添加滤镜本质上就是图片处理，也就是对图片的像素进行计算，简单来说，图像处理的方法可以分为三类：

点算子：当前像素的处理只和自身的像素值有关，和其他像素无关，比如灰度处理。
邻域算子：当前像素的处理需要和相邻的一定范围内的像素有关，比如高斯模糊。
全局算子：在全局上对所有像素进行统一变换，比如几何变换。
```## TODO : PerformanceTracker 是否会对性能有影响？

## 角度的话应该怎么计算

```text
人头向右90度，人头向左270，人头向下180，人头向上0
比如
前置竖屏的时候：数据人头向右，90度
后置竖屏的时候：数据人头向左，270度
可以根据陀螺仪，以及前后置来获取数据角度
```## yuv转jpeg

```text
private byte[] getJpegByte(byte[] data, int width, int height) {
    byte[] jpegData = data;
    try {
        YuvImage image = new YuvImage(data, ImageFormat.NV21, width, height, null);
        if(image != null) {
            ByteArrayOutputStream out = new ByteArrayOutputStream();
            image.compressToJpeg(new Rect(0, 0, width, height), 90, out);
            jpegData = out.toByteArray();
            out.close();
        }
    } catch (Exception e) {
        e.printStackTrace();
    }
    return jpegData;
}

// 美颜处理yuv的图片
FBProcessor.getInstance().postCaptureDataToNative(data, width, height, Integer.parseInt(mDataStore.getValue(KEY_FB_LEVEL, "0", mDataStore.getGlobalScope())));
// 把yuv的数据转成jpeg的数据
data = getJpegByte(data, width, height);
format = ImageFormat.JPEG;
```## bitmap转jpeg数组

```text
private byte[] bitmapToArray(Bitmap bitmap) {
    ByteArrayOutputStream stream = new ByteArrayOutputStream();
    if (bitmap != null) {
        bitmap.compress(Bitmap.CompressFormat.JPEG, 100, stream);
        return stream.toByteArray();
    }
    return null;
}
```## 美颜对着人脸拍照之后不生效，生成的outNV21为空？

```text
01-06 16:08:50.890 24871 24969 E ancf-c  : processImage started
01-06 16:08:50.890 24871 24969 E ancf-c  : processImageOpt stated
01-06 16:08:50.890 24871 24969 D ancf-c  : syscall setaffinity: mask=240=0xf0
01-06 16:08:50.890 22210 25038 D NormalPipe_FrmB: [deque] [MyDeq:0] dma(0x6) pa(0x3601960) io(0x0_0x0_0xa20_0x798_0x0_0x0_0xa20_0x1_0xa20_0x1) mag(0x91_0x91)
01-06 16:08:50.890 24871 24969 E ancf-c  : failed to setaffinity: mask=0xf0 err: Invalid argument (22)
01-06 16:08:50.890 24871 24969 D ancf-c  : ANCBeautifyImageRAII operate= 
01-06 16:08:50.890 22210 25038 D iio/ifunc: [dequeueHwBuf] pass1:i(0),dma(8),id(0x0),size(0x232800),xsize(0x95f),VA(0x9900f000),PA(0x4800000),crop(0x0,0x0,0x960,0x3c0),count(1),cur sof(153),frm_cnt(152),mag(0x91),rawType(0)
01-06 16:08:50.890 22210 25038 D NormalPipe_FrmB: [deque] [MyDeq:0] dma(0x8) pa(0x4800000) io(0x0_0x0_0xa20_0x798_0x0_0x0_0x500_0x3c0_0x500_0x3c0) mag(0x91_0x91)
01-06 16:08:50.890 24871 24969 E ancf-c  : applyOGLFeaturePost input error:faces:7c8cd118, denseLMFaces:0, facesCount:1

去掉一些美颜参数即可
```## btn_beauty 不会旋转？

```text
http://192.168.3.78:7080/c/R0_MP1/alps-release-r0.mp1-default/+/95634
```## 拍照慢？每次要3s钟左右

```text
03-08 00:31:52.629 30373 30426 E zq8888  : Time:2022_03_08_00_28_27-->com.mediatek.camera.common.mode.photo.PhotoMode-->doShutterButtonClick()-->325 isTakingPicture:false
03-08 00:31:55.923 30373 30427 E zq8888  : Time:2022_03_08_00_17_49-->com.mediatek.camera.common.mode.photo.device.PhotoDevice2Controller-->setProcessing()-->864
03-08 00:31:59.269 30373 30426 E zq8888  : Time:2022_03_08_00_28_27-->com.mediatek.camera.common.mode.photo.PhotoMode-->doShutterButtonClick()-->325 isTakingPicture:false
03-08 00:32:03.722 30373 30427 E zq8888  : Time:2022_03_08_00_17_49-->com.mediatek.camera.common.mode.photo.device.PhotoDevice2Controller-->setProcessing()-->864
03-08 00:32:29.049 30373 30426 E zq8888  : Time:2022_03_08_00_28_27-->com.mediatek.camera.common.mode.photo.PhotoMode-->doShutterButtonClick()-->325 isTakingPicture:false
03-08 00:32:33.032 30373 30427 E zq8888  : Time:2022_03_08_00_17_49-->com.mediatek.camera.common.mode.photo.device.PhotoDevice2Controller-->setProcessing()-->864

能否优化一下，没有检测到人脸或美颜没打开(美颜等级为0)的时候不进行美颜处理？
在照片生成之前不允许点击缩略图？
```## 连拍相关问题

```text
连拍的时候可能会中断
CamAp_ContinuousShotBase: [saveJpeg] data = [B@da3247f, mCurrentShotsNum = 10
CamAp_ContinuousShotBase: Stop continousShot for avoid OOM!
为什么会 OOM 呢？内存泄漏？从Profile中看到一段时间就会有内存回收，是不是预览的时候有一些内存没有回收？
把 美颜/二维码 关了之后就不会有锯齿了
应该是 image2NV21(image, yuvData1) 这个方法把 Image 读取到 ByteBuffer 的时候有一些资源没有被释放

快速连续点击拍照按钮(先长按一段时间进入连拍状态，再快速点击拍照)之后会卡死？
从log里面看到相机最后的状态一直在 Capturing，打Log发现在 Focus.java 中有下面这个判断
if (mLastModeDeviceState != ICameraMode.MODE_DEVICE_STATE_PREVIEWING) {
    return true;
}

连拍完了之后立马拍照就会有绿屏？
没开美颜的时候 handler.sendEmptyMessage 之后处理的数据为空

连拍完了之后概率性会在屏幕上一直显示 "Processing, please wait" ??
```## 按menu键清理camera之后概率性无响应？

```text
03-07 14:10:53.312  1194  1246 W ActivityManager: Timeout executing service: ServiceRecord{cb8ddc4 u0 com.hmdglobal.app.litecamera/com.mediatek.camera.CameraAppService}
03-07 14:10:53.574  1194 12011 I AnrManager: startAnrDump
03-07 14:10:53.575  1194 12011 I AnrManager: isANRFlowSkipped() AnrFlow = 0

03-07 14:11:02.343  1194 12011 I AnrManager: ANR in com.hmdglobal.app.litecamera, time=88489873
03-07 14:11:02.343  1194 12011 I AnrManager: Reason: executing service com.hmdglobal.app.litecamera/com.mediatek.camera.CameraAppService
03-07 14:11:02.343  1194 12011 I AnrManager: Load: 21.05 / 21.14 / 21.02
03-07 14:11:02.343  1194 12011 I AnrManager: Android time :[2022-03-07 14:11:02.07] [88498.633]
03-07 14:11:02.343  1194 12011 I AnrManager: CPU usage from 46665ms to 0ms ago (2022-03-07 14:10:06.649 to 2022-03-07 14:10:53.314):
03-07 14:11:02.343  1194 12011 I AnrManager:   17% 1194/system_server: 8.9% user + 8.4% kernel / faults: 3650 minor
03-07 14:11:02.343  1194 12011 I AnrManager:   13% 714/camerahalserver: 10% user + 3.1% kernel / faults: 6248 minor
03-07 14:11:02.343  1194 12011 I AnrManager:   8.4% 27848/transport: 2.8% user + 5.6% kernel / faults: 48 minor
03-07 14:11:02.343  1194 12011 I AnrManager:   8.4% 532/surfaceflinger: 4.8% user + 3.5% kernel / faults: 45 minor
03-07 14:11:02.343  1194 12011 I AnrManager:   7.1% 364/logd: 3.9% user + 3.2% kernel / faults: 47 minor
03-07 14:11:02.343  1194 12011 I AnrManager:   4.8% 1131/adbd: 1.3% user + 3.4% kernel / faults: 581 minor
03-07 14:11:02.343  1194 12011 I AnrManager:   5.6% 287/sugov:0: 0% user + 5.6% kernel
03-07 14:11:02.343  1194 12011 I AnrManager:   4.5% 491/android.hardware.graphics.composer@2.1-service: 2.1% user + 2.4% kernel / faults: 131 minor
03-07 14:11:02.343  1194 12011 I AnrManager:   3.2% 488/android.hardware.audio.service.mediatek: 2% user + 1.1% kernel / faults: 12 minor
03-07 14:11:02.343  1194 12011 I AnrManager:   3% 1592/com.android.launcher3: 2% user + 1% kernel / faults: 90 minor
03-07 14:11:02.343  1194 12011 I AnrManager:   2.2% 730/vendor.mediatek.hardware.pq@2.2-service: 1.1% user + 1.1% kernel / faults: 1 minor
03-07 14:11:02.343  1194 12011 I AnrManager:   2.1% 506/audioserver: 1.3% user + 0.7% kernel / faults: 12 minor
03-07 14:11:02.343  1194 12011 I AnrManager:   1.9% 1383/com.android.systemui: 1.4% user + 0.5% kernel
03-07 14:11:02.343  1194 12011 I AnrManager:   1.4% 734/media.swcodec: 0.8% user + 0.5% kernel / faults: 693 minor
03-07 14:11:02.343  1194 12011 I AnrManager:   1.3% 662/cameraserver: 0.5% user + 0.7% kernel / faults: 156 minor
03-07 14:11:02.343  1194 12011 I AnrManager:   1.2% 208/pbm: 0% user + 1.2% kernel
03-07 14:11:02.343  1194 12011 I AnrManager:   0.9% 658/mnld: 0.4% user + 0.4% kernel / faults: 69 minor
03-07 14:11:02.343  1194 12011 I AnrManager:   0.6% 1765/com.google.android.gms.persistent: 0.3% user + 0.2% kernel / faults: 5 minor
03-07 14:11:02.343  1194 12011 I AnrManager:   0.5% 6593/kworker/u8:7: 0% user + 0.5% kernel / faults: 47 minor
03-07 14:11:02.343  1194 12011 I AnrManager:   0.5% 7833/kworker/u8:1: 0% user + 0.5% kernel / faults: 81 minor
03-07 14:11:02.343  1194 12011 I AnrManager:   0.4% 8198/kworker/u8:5: 0% user + 0.4% kernel / faults: 27 minor
03-07 14:11:02.343  1194 12011 I AnrManager:   0.4% 31935/kworker/u8:6: 0% user + 0.4% kernel / faults: 97 minor
03-07 14:11:02.343  1194 12011 I AnrManager:   0.3% 497/merged_hal_service: 0.1% user + 0.2% kernel / faults: 11 minor
03-07 14:11:02.343  1194 12011 I AnrManager:   0.3% 478/statsd: 0% user + 0.2% kernel / faults: 453 minor
03-07 14:11:02.343  1194 12011 I AnrManager:   0.4% 698/media.extractor: 0.2% user + 0.1% kernel / faults: 140 minor
03-07 14:11:02.343  1194 12011 I AnrManager:   0.3% 3306/kworker/u8:2: 0% user + 0.3% kernel / faults: 22 minor
03-07 14:11:02.343  1194 12011 I AnrManager:   0.3% 498/vendor.mediatek.hardware.mtkpower@1.0-service: 0.1% user + 0.2% kernel
03-07 14:11:02.343  1194 12011 I AnrManager:   0.3% 10647/kworker/u8:3: 0% user + 0.3% kernel / faults: 32 minor
03-07 14:11:02.343  1194 12011 I AnrManager:   0.2% 490/android.hardware.graphics.allocator@4.0-service-mediatek: 0% user + 0.2% kernel / faults: 460 minor
03-07 14:11:02.343  1194 12011 I AnrManager:   0.2% 1176/disp_queue_P0: 0% user + 0.2% kernel
03-07 14:11:02.343  1194 12011 I AnrManager:   0.3% 1481/com.android.phone: 0.2% user + 0% kernel / faults: 1 minor
03-07 14:11:02.343  1194 12011 I AnrManager:   0.2% 479/netd: 0% user + 0.1% kernel / faults: 31 minor
03-07 14:11:02.343  1194 12011 I AnrManager:   0.2% 4178/kworker/0:2: 0% user + 0.2% kernel
03-07 14:11:02.343  1194 12011 I AnrManager:   0.2% 711/android.hardware.sensors@2.0-service-mediatek: 0% user + 0.1% kernel
03-07 14:11:02.343  1194 12011 I AnrManager:   0.2% 8/rcu_preempt: 0% user + 0.2% kernel
03-07 14:11:02.343  1194 12011 I AnrManager:   0.1% 133/ion_mm_heap_for: 0% user + 0.1% kernel
03-07 14:11:02.343  1194 12011 I AnrManager:   0.1% 261/disp_delay_trig: 0% user + 0.1% kernel
03-07 14:11:02.343  1194 12011 I AnrManager:   0.1% 300/pvr_defer_free: 0% user + 0.1% kernel
03-07 14:11:02.343  1194 12011 I AnrManager:   0.1% 10238/kworker/3:2: 0% user + 0.1% kernel
03-07 14:11:02.343  1194 12011 I AnrManager:   0.1% 366/servicemanager: 0% user + 0% kernel
03-07 14:11:02.343  1194 12011 I AnrManager:   0.1% 131/ion_mm_heap: 0% user + 0.1% kernel
03-07 14:11:02.343  1194 12011 I AnrManager:   0.1% 311/charger_thread: 0% user + 0.1% kernel
03-07 14:11:02.343  1194 12011 I AnrManager:   0.1% 933/mtkfusionrild: 0.1% user + 0% kernel
03-07 14:11:02.343  1194 12011 I AnrManager:   0.1% 1795/com.android.providers.media.module: 0% user + 0% kernel / faults: 4 minor
03-07 14:11:02.343  1194 12011 I AnrManager:   0.1% 10984/kworker/u8:8: 0% user + 0.1% kernel / faults: 37 minor
03-07 14:11:02.343  1194 12011 I AnrManager:   0.1% 1982/com.google.android.inputmethod.latin: 0% user + 0% kernel / faults: 7 minor
03-07 14:11:02.343  1194 12011 I AnrManager:   0.1% 4115/com.google.android.gms: 0% user + 0% kernel / faults: 10 minor 10 major
03-07 14:11:02.343  1194 12011 I AnrManager:   0% 210/btif_rxd: 0% user + 0% kernel
03-07 14:11:02.343  1194 12011 I AnrManager:   0% 256/disp_idlemgr: 0% user + 0% kernel
03-07 14:11:02.343  1194 12011 I AnrManager:   0% 263/present_fence_w: 0% user + 0% kernel
03-07 14:11:02.343  1194 12011 I AnrManager:   0% 365/lmkd: 0% user + 0% kernel
03-07 14:11:02.343  1194 12011 I AnrManager:   0% 480/zygote: 0% user + 0% kernel / faults: 142 minor
03-07 14:11:02.343  1194 12011 I AnrManager:   0% 293/mmcqd/0: 0% user + 0% kernel
03-07 14:11:02.343  1194 12011 I AnrManager:   0% 367/hwservicemanager: 0% user + 0% kernel / faults: 2 minor
03-07 14:11:02.343  1194 12011 I AnrManager:   0% 1/init: 0% user + 0% kernel / faults: 3 minor
03-07 14:11:02.343  1194 12011 I AnrManager:   0% 7/ksoftirqd/0: 0% user + 0% kernel
03-07 14:11:02.343  1194 12011 I AnrManager:   0% 15/ksoftirqd/1: 0% user + 0% kernel
03-07 14:11:02.343  1194 12011 I AnrManager:   0% 492/android.hardware.health@2.1-service: 0% user + 0% kernel / faults: 120 minor
03-07 14:11:02.343  1194 12011 I AnrManager:   0% 501/android.hardware.vibrator-service.mediatek: 0% user + 0% kernel / faults: 6 minor
03-07 14:11:02.343  1194 12011 I AnrManager:   0% 505/fuelgauged: 0% user + 0% kernel
03-07 14:11:02.343  1194 12011 I AnrManager:   0% 705/mediaserver: 0% user + 0% kernel / faults: 2 minor
03-07 14:11:02.343  1194 12011 I AnrManager:   0% 9697/kworker/2:1: 0% user + 0% kernel
03-07 14:11:02.343  1194 12011 I AnrManager:   0% 11/migration/0: 0% user + 0% kernel
03-07 14:11:02.343  1194 12011 I AnrManager:   0% 19/migration/2: 0% user + 0% kernel
03-07 14:11:02.343  1194 12011 I AnrManager:   0% 20/ksoftirqd/2: 0% user + 0% kernel
03-07 14:11:02.343  1194 12011 I AnrManager:   0% 25/ksoftirqd/3: 0% user + 0% kernel
03-07 14:11:02.343  1194 12011 I AnrManager:   0% 128/dlpt_notify_thr: 0% user + 0% kernel
03-07 14:11:02.343  1194 12011 I AnrManager:   0% 134/ion_history: 0% user + 0% kernel
03-07 14:11:02.343  1194 12011 I AnrManager:   0% 257/disp_check: 0% user + 0% kernel
03-07 14:11:02.343  1194 12011 I AnrManager:   0% 260/display_check_a: 0% user + 0% kernel
03-07 14:11:02.343  1194 12011 I AnrManager:   0% 268/krtatm: 0% user + 0% kernel
03-07 14:11:02.343  1194 12011 I AnrManager:   0% 277/battery_thread: 0% user + 0% kernel
03-07 14:11:02.343  1194 12011 I AnrManager:   0% 302/pvr_cacheop: 0% user + 0% kernel
03-07 14:11:02.343  1194 12011 I AnrManager:   0% 309/mtk-tpd: 0% user + 0% kernel
03-07 14:11:02.343  1194 12011 I AnrManager:   0% 350/ueventd: 0% user + 0% kernel / faults: 2 minor
03-07 14:11:02.343  1194 12011 I AnrManager:   0% 415/android.system.suspend@1.0-service: 0% user + 0% kernel
03-07 14:11:02.343  1194 12011 I AnrManager:   0% 496/android.hardware.lights-service.mediatek: 0% user + 0% kernel / faults: 23 minor
03-07 14:11:02.343  1194 12011 I AnrManager:   0% 654/mtk_stp_psm: 0% user + 0% kernel
03-07 14:11:02.343  1194 12011 I AnrManager:   0% 660/mtk_wmtd: 0% user + 0% kernel
03-07 14:11:02.343  1194 12011 I AnrManager:   0% 700/media.metrics: 0% user + 0% kernel
03-07 14:11:02.343  1194 12011 I AnrManager:   0% 717/thermal: 0% user + 0% kernel
03-07 14:11:02.343  1194 12011 I AnrManager:   0% 723/mtk_agpsd: 0% user + 0% kernel
03-07 14:11:02.343  1194 12011 I AnrManager:   0% 811/gsm0710muxd: 0% user + 0% kernel / faults: 12 minor
03-07 14:11:02.343  1194 12011 I AnrManager:   0% 4066/com.google.android.gms.unstable: 0% user + 0% kernel
03-07 14:11:02.343  1194 12011 I AnrManager:  +0% 11607/kworker/1:2: 0% user + 0% kernel
03-07 14:11:02.343  1194 12011 I AnrManager:  +0% 11814/com.hmdglobal.app.litecamera: 0% user + 0% kernel
03-07 14:11:02.343  1194 12011 I AnrManager:  +0% 11960/kworker/2:2: 0% user + 0% kernel
03-07 14:11:02.343  1194 12011 I AnrManager:  +0% 12005/logcat: 0% user + 0% kernel
03-07 14:11:02.343  1194 12011 I AnrManager: 51% TOTAL: 31% user + 20% kernel + 0% iowait + 0% softirq


                         D  bufferpool2 0x7efb5458 : 0(0 size) total buffers - 0(0 size) used buffers - 2/9 (recycle/alloc) - 7/56 (fetch/transfer)
                         D  bufferpool2 0x7efb47d8 : 0(0 size) total buffers - 0(0 size) used buffers - 2/9 (recycle/alloc) - 13/50 (fetch/transfer)
                         D  evictor expired: 2, evicted: 2
         .app.litecamer  I  Waiting for a blocking GC Instrumentation
                         I  WaitForGcToComplete blocked Instrumentation on Instrumentation for 94.476ms
    BufferQueueConsumer  I  [ImageReader-640x480f23m2-12895-0](id:325f00000002,api:0,p:-1,c:12895) disconnect()

是不是因为有些东西没有释放干净？？
CameraAppService 没有被销毁回收？

从 /data/anr/anr_2022-03-07-14-54-32-153   trace文件中看到如下
"main" prio=5 tid=1 Waiting
  | group="main" sCount=2 dsCount=0 flags=1 obj=0x728706f8 self=0xb1728e00
  | sysTid=16653 nice=-10 cgrp=default sched=0/0 handle=0xb1cd5470
  | state=S schedstat=( 2300106398 698495469 3242 ) utm=176 stm=53 core=3 HZ=100
  | stack=0xbe651000-0xbe653000 stackSize=8192KB
  | held mutexes=
  at java.lang.Object.wait(Native method)
  - waiting on <0x04bfb805> (a java.lang.Object)
  at java.lang.Object.wait(Object.java:442)
  at java.lang.Thread.join(Thread.java:1438)
  - locked <0x04bfb805> (a java.lang.Object)
  at java.lang.Thread.join(Thread.java:1519)
  at com.mediatek.camera.CameraActivity.onDestroyTasks(CameraActivity.java:595)
  at com.mediatek.camera.PermissionActivity.onPermissionDestroyTasks(PermissionActivity.java:311)
  at com.mediatek.camera.QuickActivity.onDestroy(QuickActivity.java:248)

CameraActivity.java 第 595 行 mFaceBeautyThread.join();
mFaceBeautyThread 被 lock 住了，应该是 Handler 持有了 mFaceBeautyThread 的引用没有被释放导致 lock
```## 为什么 libcamera_yuvprocessor 没有编译出来？

```text
需要在 device.mk 文件中添加一下
PRODUCT_PACKAGES += libcamera_yuvprocessor
```## 修改添加了美颜功能之后连拍功能有问题

```text
03-10 17:15:20.107 31473 31497 W CamAp_BitmapCreator: Failed to read EXIF data
03-10 17:15:20.107 31473 31497 W CamAp_BitmapCreator: java.io.FileNotFoundException: /storage/emulated/0/DCIM/Camera/IMG_20220310_170558_228.jpg: open failed: ENOENT (No such file or directory)
03-10 17:15:20.107 31473 31497 W CamAp_BitmapCreator:  at libcore.io.IoBridge.open(IoBridge.java:492)
03-10 17:15:20.107 31473 31497 W CamAp_BitmapCreator:  at java.io.FileInputStream.<init>(FileInputStream.java:160)
03-10 17:15:20.107 31473 31497 W CamAp_BitmapCreator:  at java.io.FileInputStream.<init>(FileInputStream.java:115)
03-10 17:15:20.107 31473 31497 W CamAp_BitmapCreator:  at android.media.ExifInterface.initForFilename(ExifInterface.java:2531)
03-10 17:15:20.107 31473 31497 W CamAp_BitmapCreator:  at android.media.ExifInterface.<init>(ExifInterface.java:1500)
03-10 17:15:20.107 31473 31497 W CamAp_BitmapCreator:  at com.mediatek.camera.common.utils.BitmapCreator.getExif(BitmapCreator.java:567)
03-10 17:15:20.107 31473 31497 W CamAp_BitmapCreator:  at com.mediatek.camera.common.utils.BitmapCreator.getLastBitmapFromDatabase(BitmapCreator.java:440)
03-10 17:15:20.107 31473 31497 W CamAp_BitmapCreator:  at com.mediatek.camera.ui.ThumbnailViewManager$LoadBitmapTask.doInBackground(ThumbnailViewManager.java:381)
03-10 17:15:20.107 31473 31497 W CamAp_BitmapCreator:  at com.mediatek.camera.ui.ThumbnailViewManager$LoadBitmapTask.doInBackground(ThumbnailViewManager.java:367)
03-10 17:15:20.107 31473 31497 W CamAp_BitmapCreator:  at android.os.AsyncTask$3.call(AsyncTask.java:394)
03-10 17:15:20.107 31473 31497 W CamAp_BitmapCreator:  at java.util.concurrent.FutureTask.run(FutureTask.java:266)
03-10 17:15:20.107 31473 31497 W CamAp_BitmapCreator:  at android.os.AsyncTask$SerialExecutor$1.run(AsyncTask.java:305)
03-10 17:15:20.107 31473 31497 W CamAp_BitmapCreator:  at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1167)
03-10 17:15:20.107 31473 31497 W CamAp_BitmapCreator:  at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:641)
03-10 17:15:20.107 31473 31497 W CamAp_BitmapCreator:  at java.lang.Thread.run(Thread.java:923)
03-10 17:15:20.107 31473 31497 W CamAp_BitmapCreator: Caused by: android.system.ErrnoException: open failed: ENOENT (No such file or directory)
03-10 17:15:20.107 31473 31497 W CamAp_BitmapCreator:  at libcore.io.Linux.open(Native Method)
03-10 17:15:20.107 31473 31497 W CamAp_BitmapCreator:  at libcore.io.ForwardingOs.open(ForwardingOs.java:166)
03-10 17:15:20.107 31473 31497 W CamAp_BitmapCreator:  at libcore.io.BlockGuardOs.open(BlockGuardOs.java:254)
03-10 17:15:20.107 31473 31497 W CamAp_BitmapCreator:  at libcore.io.ForwardingOs.open(ForwardingOs.java:166)
03-10 17:15:20.107 31473 31497 W CamAp_BitmapCreator:  at android.app.ActivityThread$AndroidOs.open(ActivityThread.java:7607)
03-10 17:15:20.107 31473 31497 W CamAp_BitmapCreator:  at libcore.io.IoBridge.open(IoBridge.java:478)
03-10 17:15:20.107 31473 31497 W CamAp_BitmapCreator:  ... 14 more

重新配一个和 previewSurface 一样的 Surface 专门用于连拍
```## 设置为手势操作的时候会将下面的三个虚拟按钮隐藏，布局显示有问题

```text
目前把 DMN 项目的 camera_ui_root 改为固定位置显示

http://192.168.3.78:7080/c/R0_MP1/alps-release-r0.mp1-default/+/95526
```## TODO : 美颜 ArcSeekBar 上的文字显示？

## TODO : 前后摄美颜等级分开保存？

## 美颜检测的问题，检测到人脸之后再进行预览美颜处理？

```text
用 faceDetected 变量去控制
```## 图片镜像处理

```text
Bitmap bitmap = PhotoModeHelper.makeBitmap(data, imageWidth * imageWidth);//jpeg byte 数组转换为bitmap
Matrix m = new Matrix();
m.postScale(-1, 1);     //利用matrix 对矩阵进行转换，y轴镜像
bitmap = Bitmap.createBitmap(bitmap, 0, 0, bitmap.getWidth(), bitmap.getHeight(), m, true);//m转换传入bitmap
ByteArrayOutputStream baos = new ByteArrayOutputStream();//以下再次把bitmap转换为byte 数组，
bitmap.compress(Bitmap.CompressFormat.JPEG, 100, baos);
data = baos.toByteArray();

还有没有其他方法对图片进行镜像处理？
能否在 PhotoDevice2Controller.java 中直接 YuvProcessor 对 yuv 数据进行处理，这样是否更好一些？应该是不行的，因为配置的流是jpeg的，并不是yuv的
```## TODO : 点击缩略图的流程优化一下，没有生成照片的时候先提示 "processing, please wait"，等生成了之后再gallery？

## TODO : 写一个可以调节美颜等级的camera测试脚本？

```text
可以在 CameraAppUI 中监听 onKeyDown 事件来设置，监听不同的 Key 去设置不同的美颜等级
```## TODO : 长按录像视频偏暗？

## metadata

```text
前摄
sagereal/pcb/VQ578_GH5781_HMD_Domino/alps/vendor/mediatek/proprietary/custom/mt6739/hal/imgsensor_metadata/gc02m2_mipi_raw/config_static_metadata_project.h
后摄
sagereal/pcb/VQ578_GH5781_HMD_Domino/alps/vendor/mediatek/proprietary/custom/mt6739/hal/imgsensor_metadata/gc5035_mipi_raw/config_static_metadata_project.h
```## 二维码检测时间较长？

```text
TODO : 一些优化思路
用多线程+线程池等技术优化一下？每一次启动一个线程，超时自动停止？如果有一个线程检测到了就自动停止其他几个线程？
不要每一帧都检测？
检测的区域优化一下？
检测的yuv数据是否能再精简？能否只用Y的数据去检测？
美颜的时候能否同时检测？
检测结果会不停的闪烁？
能否用QrDetector预先检测一下是否有二维码？  OpenCV ? https://blog.csdn.net/jia20003/article/details/77348170
MultiDetector能否重写一下？
用JNI处理一下yuv的数据？
QrCodeView的绘制是否能优化一下？
一些变量能否不要每次进 onImageAvailable 的时候都重新创建？


ImageDataUtil.getBytesFromImageAsType(image, ImageDataUtil.YUV420P);    // 10-20ms

Result[] results = multiReader.decodeMultiple(tempBitmap, hints);       // 30-60ms

DecodeHintType
在使用zxing解析二维码时，允许事先进行相关配置，这个文件通过Map<DecodeHintType, ?>键值对来保存，然后使用方法public void setHints(Map<DecodeHintType,?> hints)来设置到相应的解码器中。DecodeHintType是一个枚举类，其中有几个重要的枚举值，

POSSIBLE_FORMATS(List.class)
用于列举支持的解析格式，一共有17种，在 com.google.zxing.BarcodeFormat 里定义。官方默认支持所有的格式。

TRY_HARDER(Void.class)
是否使用HARDER模式来解析数据，如果启用，则会花费更多的时间去解析二维码，对精度有优化，对速度则没有。

CHARACTER_SET(String.class)
解析的字符集。这个对解析也比较关键，最好定义需要解析数据对应的字符集。

***如果项目仅仅用来解析二维码，完全没必要支持所有的格式，也没有必要使用MultiFormatReader来解析。所以在配置的过程中，我移除了所有与二维码不相关的代码。直接使用 QRCodeReader 类来解析，字符集采用utf-8，使用 Harder 模式，并且把可能的解析格式只定义为 BarcodeFormat.QR_CODE，这对于直接二维码扫描解析无疑是帮助最大的。

二维码图像识别算法选择
二维码扫描精度和许多因素有关，最关键的因素是扫描算法。目前在图形识别领域中，较常用的二维码识别算法主要有两种，分别是HybridBinarizer和GlobalHistogramBinarizer，这两种算法都是基于二值化，即将图片的色域变为黑白两个颜色，然后提取图形中的二维码矩阵。实际上，zxing中的HybridBinarizer继承自GlobalHistogramBinarizer，并在此基础上做了功能性的改进。援引官方介绍：

This Binarizer(GlobalHistogramBinarizer) implementation uses the old ZXing global histogram approach. It is suitable for low-end mobile devices which don’t have enough CPU or memory to use a local thresholding algorithm. However, because it picks a global black point, it cannot handle difficult shadows and gradients. Faster mobile devices and all desktop applications should probably use HybridBinarizer instead.

This class(HybridBinarizer) implements a local thresholding algorithm, which while slower than the GlobalHistogramBinarizer, is fairly efficient for what it does. It is designed for high frequency images of barcodes with black data on white backgrounds. For this application, it does a much better job than a global blackpoint with severe shadows and gradients. However it tends to produce artifacts on lower frequency images and is therefore not a good general purpose binarizer for uses outside ZXing. This class extends GlobalHistogramBinarizer, using the older histogram approach for 1D readers, and the newer local approach for 2D readers. 1D decoding using a per-row histogram is already inherently local, and only fails for horizontal gradients. We can revisit that problem later, but for now it was not a win to use local blocks for 1D. ···

GlobalHistogramBinarizer 算法适合于低端的设备，对手机的CPU和内存要求不高。但它选择了全部的黑点来计算，因此无法处理阴影和渐变这两种情况。HybridBinarizer算法在执行效率上要慢于GlobalHistogramBinarizer算法，但识别相对更有效。它专门为以白色为背景的连续黑色块二维码图像解析而设计，也更适合用来解析具有严重阴影和渐变的二维码图像。

网上对这两种算法的解析并不多，目前仅找到一篇文章详解了GlobalHistogramBinarizer算法，详见[http://kuangjianwei.blog.163.com/blog/static/190088953201361015055110/]()。有时间再看一下相关源码。

zxing项目官方默认使用的是HybridBinarizer二值化方法。在实际的测试中，和官方的介绍大致一样。然而目前的大部分二维码都是黑色二维码，白色背景的。不管是二维码扫描还是二维码图像识别，使用GlobalHistogramBinarizer算法的效果要稍微比HybridBinarizer好一些，识别的速度更快，对低分辨的图像识别精度更高。

[开源]媲美微信的二维码识别库
https://mp.weixin.qq.com/s/f8rmlWR1ZHtAv-TvTGFy7Q

1，YUV
2，图像缩小
3，裁剪
4，使用OpenCV加快识别


二维码扫描 ZXing
0. 去除不必要的格式转换和旋转操作
在分析代码时，发现原有的逻辑在相机帧onPreviewFrame()回调里处理帧像素时，先把 YUV 数据格式转换成了 RGB 格式，同时由于横竖屏的关系，对像素数组进行了 90°旋转操作，然后把处理好的像素数组传递给RGBLuminanceSource，交给 ZXing 解码。经过断点分析，发现 YUV 转 RGB 和旋转这两步耗费了大量时间，预览数组越大耗时越长。
ZXing 本身提供了YUVLuminanceSource可以直接解码 YUV 数据，在 YUV 格式中 Y 分量就是灰度分量，对比度相比 RGB 更高，直接把 YUV 格式的 data 数据交给 ZXing 解码，转换耗时就节省下来了。

相机预览坐标系是横屏的，而移动 APP 一般是竖屏扫码模式，而我们分析发现 ZXing 解码二维码与其是水平的还是竖直的图像关系不大，都能识别，因此可以不旋转像素数组，只旋转裁剪区域的坐标系，只需要把矩形框的四个坐标点做一下变换，设置给YUVLuminanceSource，就避免了对所有像素进行旋转的操作，这部分耗时也节省出来了。

1. 去除zxing额外支持的格式
MultiFormatReader的decodeWithState()是使用方的入口方法，内部调用了decodeInternal()，输入是相机的一帧数据，如果抛了NotFoundException，则表示没找到二维码；如果返回了Result，则表示找到了二维码，并解析完成。代码如下：
其中，readers变量是一个数组，数组的大小表示支持的条码格式个数，zxing原本因为支持很多格式，因此这个数组长度比较长。当拿到相机的一帧数据后，需要去检测是否是所有支持格式的某一个格式，每一种格式的检测都需要花费一些时间，因此这个遍历对于Lark是不必要的。如果将zxing内部定制成只支持QR Code格式，那么就免去了额外的格式检测。

2. 删除zxing冗余代码
删除zxing除了二维码之外的格式的相关代码，zxing对每种格式的相关代码都放在各自的目录中，因此我们只需要把这些格式对应的目录删除即可，比如aztec、maxicode等。
删除二维码的encode相关代码，即"qrcode/encoder"目录。
删除decode后文本的解析相关类（比如地址、通讯录、邮件等解析类），只保留URI、URL、Text。
通过以上方式，zxing文件数量从263个缩减到67个，库大小从1.8M缩减到451K，效果非常明显

3. 将处理相机帧从串行改为并行
每次从onPreviewFrame()中获取一帧数据，然后调用zxing的decode解析二维码，如果成功，则返回；如果失败，则调用setOneShotPreviewCallback()重新调用一次onPreviewFrame()。

缺点是如果处理一帧数据时间很长，会阻碍下一帧的处理，比如上一帧是没有二维码的，而下一帧是有二维码的，如果上一帧处理时间较长，那么虽然用户对准了二维码，但是实际处理的还是上一帧，因此不太合理。

我们将串行处理改成并行处理，一旦从onPreviewFrame()获取一帧数据，将decode任务丢进线程池，并立即调用setOneShotPreviewCallback()获取下一帧数据。一旦某个任务检测到二维码，立即将isSuccess变量置为true，忽略其他任务。这样能够大大加快二维码检测的速度。

4. 自动放大
第一步只是检测是否存在二维码，比如去寻找是否存在Position Detection Pattern，Timing Pattern，Alignment Pattern。如果检测到了，则返回DetectorResult，内部包含了定位点的位置信息；如果没检测到，则抛出NotFoundException。如果二维码很小，即使第一步检测存在二维码，但是第二步解码也可能会失败。由于我们在第一步已经能够知道二维码的大小，因此根据DetectorResult返回的二维码定位点信息计算出二维码的大致宽度，然后判断二维码大小在扫码框中是否足够小，如果足够小，则放大一定焦距：如果小于十分之一，则放大到最大焦距；如果小于等于六分之一，则放大到最大焦距的一半。
```## 打印 CaptureResult 的 key

```text
List<CaptureResult.Key<?>> keys = mCaptureResult.getKeys();

public void printKeys(List<CaptureResult.Key<?>> keys) {
    for (CaptureResult.Key mKey : keys) {
        android.util.Log.e("zq8888", "Time:2022_03_10_16_38_47-->"+Thread.currentThread().getStackTrace()[2].getClassName()+"-->"+Thread.currentThread().getStackTrace()[2].getMethodName()+"()-->"+Thread.currentThread().getStackTrace()[2].getLineNumber()+" mKey:" + mKey);
    }
}
```## acquireLatestImage 和 acquireNextImage 的区别？

```text
在Camera中获取图片的时候，会遇到 acquireLatestImage() 与 acquireNextImage()选择，以下是对这两个方法的解读：
acquireLatestImage()
从ImageReader的队列中获取最新的Image ，删除旧images 。 如果没有新图像可用，则返回null 。如果已经close了，那么将不会是最新的数据图像。对于大多情况可以使用acquireNextImage()，它更加适合处理实时数据。在使用这个方法读取图片的时候，要注意maxImages不能小于2，从字面上和上面的知识我们了解到它是获取一张，丢弃一张。如果小于2的话可能会导致预期丢弃失败

acquireNextImage()
从ImageReader的队列中获取下一个Image。 如果没有新图像可用，则返回null 。注意皮球，警告：考虑使用acquireLatestImage() ，因为它会自动释放较旧的图像，并允许运行较慢的处理最新的帧。 建议在批处理/后台处理中使用acquireNextImage() 。错误地使用此功能可能会导致图像出现延迟不断增加，然后是完全失速，看起来没有新的图像出现。

美颜和二维码用哪个比较好？
```## Camera MetaData 介绍

```text
https://blog.csdn.net/wjky2014/article/details/120480345
```## MediaRecorder.AudioSource.MIC参数说明

```text
其中第一个参数就是选择录音源的，其可选参数如下：
1.MediaRecorder.AudioSource.CAMCORDER
设定录音来源于同方向的相机麦克风相同，若相机无内置相机或无法识别，则使用预设的麦克风

2.MediaRecorder.AudioSource.DEFAULT 默认音频源

3.MediaRecorder.AudioSource.MIC
设定录音来源为主麦克风。

4.MediaRecorder.AudioSource.VOICE_CALL
设定录音来源为语音拨出的语音与对方说话的声音

5.MediaRecorder.AudioSource.VOICE_COMMUNICATION
摄像头旁边的麦克风

6.MediaRecorder.AudioSource.VOICE_DOWNLINK
下行声音

7.MediaRecorder.AudioSource.VOICE_RECOGNITION
语音识别

8.MediaRecorder.AudioSource.VOICE_UPLINK
上行声音**
```## DreamCamera2 Camera APP 拍照，照片内存太小问题

```text
图片内存的大小受 图片编码质量 和 编码压缩率 影响。而图片压缩率不是固定值，和图片内容相关，一般可以通过修改图片编码质量来改变图片内存大小。

修改图片编码质量可通过谷歌官方TAG：JPEG_QUALITY控制，APP不下发该TAG的值时，图片编码质量默认为85 ，TAG 的使用可参考展锐 DreamCamera2 APP。

DreamCamera2 APP log分析见如下：
07-17 01:34:09.083  446 15158 D cmr_snp : 2987, snp_set_jpeg_enc_param: quality 70 slice height 1200 //图片编码质量为70（下发的TAG值为70），DreamCamera2 APP Camera settings 的 Picture quality 对应normal
07-17 01:34:17.574  446 15158 D cmr_snp : 2987, snp_set_jpeg_enc_param: quality 80 slice height 1200 //图片编码质量为80（下发的TAG值为80），DreamCamera2 APP Camera settings 的 Picture quality 对应fine
07-17 01:34:24.937  446 15158 D cmr_snp : 2987, snp_set_jpeg_enc_param: quality 95 slice height 1200 //图片编码质量为95（下发的TAG值为95），DreamCamera2 APP Camera settings 的 Picture quality 对应super fine
```## DreamCamera2 APP，如何修改照片角度和录像角度？

```text
在横屏设备中，可能存在需要修改照片角度和录像角度的需求，下面给出DreamCamera2 APP中，修改照片和录像角度的参考case。

①Camera APP中，照片角度可通过 ANDROID_JPEG_ORIENTATION tag设置。

DreamCamera2 APP的图片角度可以通过以下 mJpegRotation 来修改。

src/com/android/camera/PhotoModule.java
@Override
public boolean capture() {
    .................................
    boolean isFrontCamera = info.isFacingFront();
    mJpegRotation = CameraUtil.getImageRotation(sensorOrientation, deviceOrientation, isFrontCamera);   ////mJpegRotation为图片旋转的角度
    Log.i(TAG, " sensorOrientation = " + sensorOrientation
②Camera APP中，录像角度的修改通过 setOrientationHint(int degrees) 接口实现。

DreamCamera2 APP的录像角度可以通过以下rotation来完成

src/com/android/camera/VideoModule.java
private class VideoRecordStartTask extends AsyncTask<Void, Void, Void> {
.................................
    @Override
    protected void onPostExecute(Void result) {
        .................................
        int rotation = CameraUtil.getImageRotation(sensorOrientation,
               deviceOrientation, isCameraFrontFacing()); ///录像旋转角度rotation
        /**
        * SPRD: Add for bug 585183, 3d video recoding @{
        * Original Code
        *
        mMediaRecorder.setOrientationHint();
        */
        mMediaRecorder.setOrientationHint(getRecorderOrientationHint(rotation));  //设置录像角度
```## Camera低电量不打开闪光灯。电量阀值是多少？

```text
camera 监听电量变化的广播，在 低于CameraUtil.getLowBatteryNoFlashLevel()这个值的时候，关闭闪光灯打闪

CameraActivity.java
if (intent.getAction().equals(Intent.ACTION_BATTERY_CHANGED) && mCurrentModule.isFlashSupported()) {
    final int level = intent.getIntExtra(BatteryManager.EXTRA_LEVEL, 0);
    mIsBatteryLow = level <= CameraUtil.getLowBatteryNoFlashLevel();
    Log.i(TAG, "action_battery_changed level = " + level + " , isBatteryLow = " + mIsBatteryLow);
    mCurrentModule.updateBatteryLevel(level);
}

CameraUtil.getLowBatteryNoFlashLevel()的值由mLowBatteryNoFlashLevel控制

CameraUtil.java
private final static String TARGER_LOW_BATTERY_NO_FLASH = "persist.sys.cam.battery.flash";
mLowBatteryNoFlashLevel = android.os.SystemProperties.getInt(TARGER_LOW_BATTERY_NO_FLASH, 10);

在TARGER_LOW_BATTERY_NO_FLASH 未定义的情况下。电量阀值为10，及低于battery level 10的时候关闭闪光灯。
```## DreamCamera2 APP，预览帧率接口是？

```text
答：DreamCamera2 APP，预览帧率设置接口为：setPreviewFpsRange(int min, int max)；
如下是不同模式的预览帧率设置位置：

①常规拍照模式
路径:vendor/sprd/platform/packages/apps/DreamCamera2/src/com/android/camera/PhotoModule.java
protected void updateCameraParametersInitialize() {
    // Reset preview frame rate to the maximum because it may be lowered by
    // video camera application.
    int[] fpsRange = CameraUtil.getPhotoPreviewFpsRange(mCameraCapabilities, useNewApi(), false);
    if (fpsRange != null && fpsRange.length > 0) {
        mCameraSettings.setPreviewFpsRange(fpsRange[0], fpsRange[1]); //设置拍照预览帧率
    }
    mCameraSettings.setRecordingHintEnabled(false);

②连拍模式
路径:
vendor/sprd/platform/packages/apps/DreamCamera2/src/com/dream/camera/modules/continuephoto/ContinuePhotoModule.java
@Override
protected void updateCameraParametersInitialize() {
    int[] fpsRange = CameraUtil.getMaxPreviewFpsRange(mCameraCapabilities.getSupportedPreviewFpsRange());
    if (fpsRange != null && fpsRange.length > 0) {
        mCameraSettings.setPreviewFpsRange(fpsRange[0], fpsRange[1]); //设置连拍预览帧率
        Log.d(TAG, "preview fps: " + fpsRange[0] + ", " + fpsRange[1]);// Bug 1159178 (FORWARD_NULL)
    }
}

③录像模式
路径:vendor/sprd/platform/packages/apps/DreamCamera2/src/com/android/camera/VideoModule.java
protected void updateFpsRange() {
    if (CameraUtil.isDynamicFpsEnable()) { //展锐平台支持动态帧率设置
        int[] fpsRange = CameraUtil
                .getPhotoPreviewFpsRange(mCameraCapabilities, useNewApi(), true);
        if (fpsRange != null && fpsRange.length > 0) {
            mCameraSettings.setPreviewFpsRange(fpsRange[0], fpsRange[1]);
            Log.i(TAG, "preview fps: " + fpsRange[0] + ", " + fpsRange[1]); //设置录像预览帧率
        }
    } else {
        mCameraSettings.setPreviewFrameRate(mProfile.videoFrameRate);
    }
}

④全景模式
路径:vendor/sprd/platform/packages/apps/DreamCamera2/src/com/sprd/camera/panora/WideAnglePanoramaModule.java
private void setupCaptureParams() {
    mCameraSettings.setDefault(CameraUtil.VALUE_FRONT_FLASH_MODE_LCD == CameraUtil.getFrontFlashMode(), mCameraCapabilities);//SPRD:fix bug616836 add for photo use api1 or api2 use reconnect
    ....................................
    List<int[]> frameRates = mCameraCapabilities.getSupportedPreviewFpsRange();
    if (!CameraUtil.isNewWideAngle()) { 
        int last = frameRates.size() - 1;
        int minFps = (frameRates.get(last))[0];
        int maxFps = (frameRates.get(last))[1];
        mCameraSettings.setPreviewFpsRange(minFps, maxFps); //设置全景模式预览帧率
        Log.d(TAG, "preview fps: " + minFps + ", " + maxFps);
    } else {
        int[] fpsRange = CameraUtil
                .getPhotoPreviewFpsRange(frameRates, useNewApi(), false);
        if (fpsRange != null && fpsRange.length > 0) {
            mCameraSettings.setPreviewFpsRange(fpsRange[0], fpsRange[1]);
            Log.d(TAG, "preview fps: " + fpsRange[0] + ", " + fpsRange[1]);
        }
    }
```## DreamCamera2 app全景模式，纯色背景无法拍照或拍照卡顿问题

```text
展锐平台全景算法，在纯色背景无法合成照片原因如下：
a)由于现在算法仅通过帧与帧之间的特征点来判断合成，纯色背景下无法识别出足够的特征点，因此算法无法合成图片，生成偏移；
b)当前全景算法没有结合gyro信息来判断用户的移动情况，并且一般手机也没有配置gyro sensor，因此无法在纯色背景下判断用户的移动情况并生成有效偏移。
```## Camera应用，app层是否有设置预览角度的接口？

```text
一、Camera API1框架，APP有设置预览方向的接口，接口为：setDisplayOrientation(int degrees)。
物理竖屏设备（手机），谷歌的适配代码：
public static void setCameraDisplayOrientation(Activity activity, int cameraId, android.hardware.Camera camera) {
      android.hardware.Camera.CameraInfo info = new android.hardware.Camera.CameraInfo();
      android.hardware.Camera.getCameraInfo(cameraId, info);
      int rotation = activity.getWindowManager().getDefaultDisplay().getRotation(); //Device Orientation
      int degrees = 0; 
      switch (rotation) { 
          case Surface.ROTATION_0: degrees = 0; break;
          case Surface.ROTATION_90: degrees = 90; break;
          case Surface.ROTATION_180: degrees = 180; break;
          case Surface.ROTATION_270: degrees = 270; break;
      } 
      int result; 
      if (info.facing == Camera.CameraInfo.CAMERA_FACING_FRONT) {
          result = (info.orientation + degrees) % 360;
          result = (360 - result) % 360; // compensate the mirror
      } else { // back-facing后摄 
          result = (info.orientation - degrees + 360) % 360; 
      }
      camera.setDisplayOrientation(result);  //set preview orientation
}


二、Camera API2框架，APP 层没有设置预览角度的接口，Camera APP 的预览方向由 sensor_config.xml 的 orientation 属性决定。
物理竖屏设备，后摄摄像头对应的 orientation 默认设置为90°，前摄摄像头对应的 orientation 默认设置为270°；物理横屏设备，后摄摄像头对应的 orientation 默认设置为0°，前摄摄像头对应orientation 默认设置为180°。
sensor_config.xml参考路径： sprdroid_trunk\device\sprd\sharkl5Pro\module\camera\sensor_config.xml。
```## DreamCamera2 APP，如何替换展锐全景算法库？

```text
答案：可通过adb push 命令对算法库进行替换，全景算法库在设备中的目录为：system_ext/lib64。
1. adb push xxx system_ext/lib64
2. 清除DreamCamera2相机应用存储空间
```## 针对不同的拍照或录像尺寸，DreamCamera2 app 如何选择预览尺寸？

```text
针对不同的照片或录像尺寸，DreamCamera2 app 选择预览尺寸的策略如下：
以4：3照片尺寸为例
①根据用户选择的 4：3 拍照比例，从 camera hal 挑选一系列支持的4：3 的预览尺寸；
camera hal预览尺寸所在的数组为：cam_stream_info_t_stream_info
参考路径：sprdroid/vendor/sprd/modules/libcamera/hal2_3v6/SprdCamera3Setting.cpp

②遍历 ① 选择的预览尺寸，以屏幕短边为基准，选择一组与屏幕尺寸相近的作为预览尺寸。
如屏幕尺寸为1280，720，用户选择的4：3照片时，匹配的预览尺寸为960，720。

注：录像的预览尺寸选择策略与拍照一致。
```## DreamCamera2 APP，如何dump送给全景算法库的yuv？

```text
答案：在 Android 11 和 Android 12，展锐的全景算法库添加了dump yuv图片的功能，通过 adb 命令可以 dump app 送给全景算法的yuv。

下面是全景模式 dump yuv 和 获取 yuv 图片的操作：

1. 输入以下命令：
adb root
adb remount
adb shell setprop vendor.pano.yuv.dump true

2. 打开DreamCamera2的全景模式，点击拍照

3. 手机连上电脑，usb选MTP，进手机，打开手机的DownLoad文件夹，将yuv拷贝出来
```## 人像模式虚化等级参数下发流程

```text
1.APP部分

下发的值为[0-9]，分别对应光圈值从小到大[F0.95-F16.0]
\vendor\sprd\platform\packages\apps\DreamCamera2\src\com\dream\camera\modules\portraitphoto\PortraitPhotoModule.java
    private int mFNumber = CameraUtil.getPortraitDefaultFNumber();
    public void onFNumberValueChanged(int value) {
        Log.i(TAG, " onFNumberValueChanged = " + value);
        mFNumber = value;
        if(mCameraSettings != null && mCameraDevice != null) {
            mCameraSettings.setFNumberValue(mFNumber);
            if (!mFirstHasStartCapture){
                mCameraDevice.applySettings(mCameraSettings);
            }
        }
    }
LOG  如下：
04-08 03:24:30.469  9657  9657 I CAM_BlurRefocusModule:  onFNumberValueChanged = 4
04-08 03:24:32.385  9657  9657 I CAM_BlurRefocusModule:  onFNumberValueChanged = 6
04-08 03:24:32.422  9657  9657 I CAM_BlurRefocusModule:  onFNumberValueChanged = 6
04-08 03:24:33.885  9657  9657 I CAM_BlurRefocusModule:  onFNumberValueChanged = 3
04-08 03:24:33.930  9657  9657 I CAM_BlurRefocusModule:  onFNumberValueChanged = 3

通过TAG： CONTROL_SPRD_BLUR_F_NUMBER 下发，到HAL转化为ANDROID_SPRD_BLUR_F_NUMBER
\vendor\sprd\platform\packages\apps\DreamCamera2\portability\src\com\android\ex\camera2\portability\SprdCaptureRequest.java
public static final Key<Integer> CONTROL_SPRD_BLUR_F_NUMBER = new Key<Integer>("com.addParameters.sprd3BlurFNumber", int.class);     //  ANDROID_SPRD_BLUR_F_NUMBER    

\vendor\sprd\platform\packages\apps\DreamCamera2\portability\src\com\android\ex\camera2\portability\SprdAndroidCamera2Settings.java
if (mSprdFNumber != -1) {
    // Log.i(TAG, " set CONTROL_SPRD_BLUR_F_NUMBER: mSprdFNumber = " + mSprdFNumber);
    requestSettings.set(CONTROL_SPRD_BLUR_F_NUMBER, mSprdFNumber);
}

2.HAL部分
通过updateWorkParameters更新ANDROID_SPRD_BLUR_F_NUMBER值到f_number
if (frame_settings.exists(ANDROID_SPRD_BLUR_F_NUMBER)) {
    valueI32 = frame_settings.find(ANDROID_SPRD_BLUR_F_NUMBER).data.i32[0];
    GET_VALUE_IF_DIF(s_setting[mCameraId].lensInfo.f_number,
                     blur_fnum[valueI32 - 1], ANDROID_SPRD_BLUR_F_NUMBER, 1)
    HAL_LOGD("lens f_number is %f", blur_fnum[valueI32 - 1]);
LOG如下：
04-08 03:25:34.939   484  1018 D Cam3Setting: 4857, updateWorkParameters: lens f_number is 5.600000
04-08 03:25:36.931   484  7081 D Cam3Setting: 4857, updateWorkParameters: lens f_number is 2.800000

3. 传到人像模式下

此处也是读取的光圈值，将光圈值下发
if (metaSettings.exists(ANDROID_SPRD_BLUR_F_NUMBER)) {
    int fnum = metaSettings.find(ANDROID_SPRD_BLUR_F_NUMBER).data.i32[0];
    if (fnum < MIN_F_FUMBER) {
        fnum = MIN_F_FUMBER;
    } else if (fnum > MAX_F_FUMBER) {
        fnum = MAX_F_FUMBER;
    }
    if (fnum != mbokehParm.f_number) {
        mbokehParm.f_number = fnum;
        mBokehAlgo->setBokenParam((void *)&mbokehParm);
        mDepthTrigger = TRIGGER_FNUM_PORTRAIT;
    }
}
```## Wind Noise Reduction 菜单

```text
CameraAppUI.java
if (CameraConstant.SUPPORT_WINDNOISEREDUCTION && Keys.isOZOAudioOn(mController.getSettingsManager())
                && (getCurrentModeIndex() == CapturingMode.VIDEO.getModuleId()
                || getCurrentModeIndex() == CapturingMode.CINEMA_MODE.getModuleId())) {

public static final boolean SUPPORT_WINDNOISEREDUCTION = isRonin() || isShadowcatOrPlus || isMagik();       // isMagik 为 true

public static boolean isOZOAudioOn(SettingsManager settingsManager) {
    return CameraConstant.SUPPORT_OZO && settingsManager.getBoolean(SettingsManager.SCOPE_GLOBAL, KEY_AUDIO_OZO, true);
}

public static final boolean SUPPORT_OZO = isShadowcatOrPlus;

public static final boolean IS_SHADOWCAT = isShadowcat();
public static final boolean IS_SHADOWCATPLUS = isShadowcatPlus();
public static final boolean isShadowcatOrPlus = IS_SHADOWCAT || IS_SHADOWCATPLUS;       // false
```## 人像模式咨询

```text
1. Moster项目中的人像模式中美颜和双摄虚化的算法是否均为Unisoc提供的默认算法。是否有unisoc协助做特定修改？
使用的Unisoc默认算法，双摄虚化最开始不支持等级调整，Unisoc有帮忙支持等级bokeh等级调整

2. 美颜和虚化如果一起打开，算法执行的顺序是什么？ YUV-》虚化-》jpg-》美颜算法-》jpg？
虚化-美颜-yuv-jpg

3. 美颜和虚化算法实现是在APP侧完成的还是在HAL侧
HAL

4. 美颜等级调整具体是修改了拿些参数。
磨皮+廋脸
setDateToFile(Keys.KEY_MAKEUP_SKIN_SMOOTH_LEVEL, progressPra);
setDateToFile(Keys.KEY_MAKEUP_SLIM_FACE_LEVEL, progressPra);

public void setDateToFile(String key, int value) {
    DataModuleManager.getInstance(mContext).getCurrentDataModule().set(DataConfig.SettingStoragePosition.positionList[3], key, "" + value);
}
```## BOKEH

```text
bokeh 散景; 焦外成像;
焦外成像（Bokeh）是一個專業術語，指在攝影鏡頭光圈大小和拍攝距離決定了拍攝時的景深。

攝影鏡頭光圈大小和拍攝距離決定了拍攝時的景深，相對於焦點位置，焦點前與焦點后的被拍攝物體會顯得模糊，這個模糊區域被稱為焦外。

焦外具體的模糊程度還受到鏡頭中鏡片單體和組合的物理特性影響，形成了由鏡頭不同而得到的不同的焦點外的圖像。
於是焦外成像這個技術名詞出現了。

優秀的焦外成像柔順而迷人，色彩過渡自然，絲毫不遜色於焦點處的圖像魅力。

最典型的例子，就是夜景拍攝中的遠景模糊炫麗的燈光效果。

bokeh，即背景虚化。首先，我们了解一下景深。景深（DOF，Depth of Field）就是指聚焦后的清晰范围，也就是在摄影机镜头或其他成像器前沿能够取得清晰图像的成像所测定的被摄物体前后距离范围。光圈、镜头、及焦平面到拍摄物的距离是影响景深的重要因素。景深越浅代表着清晰的范围越小，景深越深则是清晰的部分比较大。

光圈越大(Ｆ数值越小），照片清晰范围越小这样越适合凸显出主体。光圈越小(Ｆ数值越大），照片就会越平面，会比较没有前中后景的距离感。运用了这个原理，我们就能够拍出非常浅的景深，实现背景虚化。这个效果也是众多摄影师在拍摄人像时所追求的效果。

第二点是Portrait Mode。手机拍照分为Landscape mode和Portrait mode。

Landscape mode称为风景模式，也叫横屏模式，宽度大于高度有着更宽阔的视野，适合欣赏风景。Portrait mode称为肖像模式，也叫竖屏模式，高度大于宽度能给站立的人物一个特写，适合肖像拍摄。

肖像模式下的背景虚化，让拍摄主体更加清晰、突出，增强了拍摄效果，这也是用户所追求的。

第三点是HDR video，HDR一般需要不同曝光的多帧进行融合，所录视频按照4K 30fps来算，sensor需要输出4K 120fps（按照低中高三种曝光），ISP IP也需要处理4K 120fps，还需要加上HDR融合。这对ISP IP的压力也不小。

为了实现该目的，主要采用了两个RGB的相机模组，同时对景物进行成像，利用三角测量原理，计算出每个点的景深数据，依靠该系列数据，进行前景以及背景的分离，再通过虚化算法针对背景虚化处理，最终营造出背景虚化的成像效果。值得注意的是，这里由于三角测量的原理的限制，需要对两个相机模组进行标定，使得两者成像平面位于同一平面，并且保持像素对齐。

焦内清晰
首先，这个功能就是用于突出主体的，所以对焦平面所在的主体一定要清晰，不能有丝毫的失焦模糊。与此同时，还需要符合光学规律，需要景深范围合理。比如与焦平面多大距离范围内的物体是清晰的，就很值得研究。这一点，其实并不那么容易，待会我会提到。

焦外虚化
为了能够突出主体，在景深范围之外的部分则需要按照光学规律逐渐的模糊。很多人以为只是对背景区域做个简单的高斯模糊就能实现这种效果，然而并非如此。要真的能逼近单反的大光圈产生的这种效果，需要考虑的问题很多。这包括了画面中每一个像素的虚化程度、以及虚化方式的设计，还需要能够在手机这种计算量有限的平台上高效的实现。我们待会会看到更多技术方面的考量。

边缘准确性
主体和背景、前景的边缘的表现对最终图像的美感和真实性影响非常大。这里我们要求的是主体和位于其后的背景的边缘要非常锐利，相互不会渗透和污染到对方。
而如果对焦主体远离相机，位于其前方、靠近相机的物体和主体的边缘则恰恰相反，应该呈现出特别的模糊感：

渐变
正如上面所说，我们希望画面在清晰和模糊之间的变化是符合光学规律的。于是随着非主体部分逐渐远离对焦平面，其模糊程度也应该是平滑渐变的。这显然就不是对这些区域简单做一个高斯模糊能做到的，而是需要更加复杂的渲染算法。

光斑
真实的光学系统在大光圈成像时，除了刚才提到的主体之外的模糊，还会在某些高光像素处形成特别质感的光斑，如下图所示。这些光斑随着与对焦平面的距离，甚至光轴的距离不同，还会呈现出不同的透明度、尺寸、形态、颜色。
```## 什么决定照片的清晰度？

```text
像素越大，照片越清晰; 分辨率越高，可输出照片尺寸也可以越大。
要说明的一点是：清晰度与分辨率没有什么关系，分辨率只决定拍出的相片的大小。
在硬件方面：决定相机清晰度的要素就是镜头、感光元件CD的素质（面积大小、质地）、图像处理芯片的素质等。
操作方面：采光、曝光、对焦等都有影响。
```## ISP基本框架及算法介绍

```text
https://blog.csdn.net/lz0499/article/details/71156291
```## MTK HAL 第三方算法接入

```text
BokehPlugin： Bokeh算法挂载点，双摄景深算法的虚化部分。
DepthPlugin： Depth算法挂载点，双摄景深算法的计算深度部分。
FusionPlugin： Depth和Bokeh放在1个算法中，即合并的双摄景深算法挂载点。
JoinPlugin： Streaming相关算法挂载点，预览算法都挂载在这里。
MultiFramePlugin： 多帧算法挂载点，包括YUV与RAW，例如MFNR/HDR
RawPlugin： RAW算法挂载点，例如remosaic
YuvPlugin： Yuv单帧算法挂载点，例如美颜、广角镜头畸变校正等

对号入座，将要集成的算法选择相应的plugin。
单帧水印算法，所以预览我们选择JoinPlugin，拍照选择YuvPlugin。
多帧算法，只能选择MultiFramePlugin。并且，一般情况下多帧算法只用于拍照，不用于预览。

主要函数介绍：
property
negotiate
init
process
abort
uninit
在property函数中feature类型设置我们在第三步中添加的TP_FEATURE_WATERMARK，并设置名称、优先级等等属性。

在negotiate函数中配置算法需要的输入、输出图像的格式、尺寸。

在negotiate函数或者process函数中获取上层传下来的metadata参数，根据参数决定算法是否运行，或者将参数传给算法。

在process函数中接入算法。
在property函数中feature类型设置成TP_FEATURE_MFNR，并设置名称、优先级、最大帧数等等属性。尤其注意mNeedRrzoBuffer属性，一般情况下，多帧算法必须要设置为MTRUE。

在negotiate函数中配置算法需要的输入、输出图像的格式、尺寸。注意，多帧算法有多帧输入，但是只需要一帧输出。因此这里设置了mRequestIndex == 0时才需要mOBufferFull。也就是只有第一帧才有输入和输出，其它帧只有输入。
另外，还在negotiate函数中获取上层传下来的metadata参数，根据参数决定算法是否运行。

在process函数中接入算法。第一帧时创建算法接口类对象，然后每一帧都调用算法接口函数addFrame加入，最后一帧再调用算法接口函数process进行处理并获取输出
https://blog.csdn.net/u012932409/article/details/120263991

https://blog.csdn.net/wjky2014/article/details/118585923


//dump input YV12
if (mDump) {
    char path[256];
    snprintf(path, sizeof(path), "/data/vendor/camera_dump/preview_in_frame%d_%dx%d_%s_%d.yv12",
        frameNo, width, height, currentDate, currentTime);
    in->saveToFile(path);
}
```## 双摄

```text
主流双摄像头的功能主要可以分为两大类：
1、利用双摄像头产生立体视觉，获得影像的景深，利用景深信息进行背景虚化，3D扫描，辅助对焦，动作识别等应用；
2、利用左右两张不同的图片信息进行融合，以期望得到更高的分辨率，更好的色彩，动态范围等更好的图像质量或实现光学变焦。

这两大类大致可以分为4点：
1、通过双摄测距，可以进行距离相关的应用，这方面目前应用最广泛的就是背景虚化；
2、光学变焦；
3、暗光增强；
4、3D拍摄及建模。

1、彩色相机 + 彩色相机（RGB + RGB），主要用于计算景深，实现背景虚化和重对焦
2、彩色相机 + 黑白相机（RGB + Mono），主要提升暗光/夜景影像拍摄质量
3、广角镜头 + 长焦镜头（Wide + Tele），主要用于光学变焦
4、彩色相机 + 深度相机（RGB + Depth），主要用于三维重建


广角+长焦镜头组合带来的最大优势就是可以在手机上实现光学变焦。光学变焦(Optical Zoom)其实是相机上的一个名词，它是通过改变光学镜片组结构来改变镜头焦距，从而实现变焦。但是镜片组结构复杂，整体尺寸无法安置于手机中。而此前的手机如果想要放大图片，方法是后期对图片进行裁切然后将一部分放大，这样做的后果是图片内的每个像素面积就会增大，图像的画质就会被严重压缩。而广角+长焦双摄则解决了这一难题，在手机中实现了光学变焦。

广角+长焦双摄的光学变焦在于左右摄像头拥有不同的可视角，这样两个摄像头就会有不同的取景范围。当想要拍摄广角照片时，可以使用左摄像头取景。如果想要长焦照片，则用右摄像头取景，获得长焦效果。通俗点说，即广角镜头取景更宽更广，但是取不到远处物体；而长焦镜头虽然取景比较窄，但是能“看”的更远。这样，广角和长焦镜头组合搭配，在拍照时通过镜头切换和算法来实现比较平滑的变焦。

以iPhone 7 Plus为例，其采用了1200万像素、28mm焦距的广角镜头+1200万像素、56mm像素的长焦镜头，通过28mm广角和56mm长焦摄像头的切换来实现2倍无损变焦。虽然还无法达到单反相机上的无级光学变焦，但是目前在手机上已经是绝对的领先方案了，OPPO R11、小米6、一加5等采用了同样的方案。
```## 合入Aw双摄算法之后报错，原因是没有合入hal的patch(添加TAG)

```text
06-06 17:41:33.251  8227  8294 E AndroidRuntime: FATAL EXCEPTION: Camera2 Handler Thread
06-06 17:41:33.251  8227  8294 E AndroidRuntime: Process: com.dualcam.calibration, PID: 8227
06-06 17:41:33.251  8227  8294 E AndroidRuntime: java.lang.IllegalArgumentException: Could not find tag for key 'com.mediatek.awdualcam.cal.aiworksDualcamCalibrationMode')
06-06 17:41:33.251  8227  8294 E AndroidRuntime:  at android.hardware.camera2.impl.CameraMetadataNative.nativeGetTagFromKeyLocal(Native Method)
06-06 17:41:33.251  8227  8294 E AndroidRuntime:  at android.hardware.camera2.impl.CameraMetadataNative.setBase(CameraMetadataNative.java:1652)
06-06 17:41:33.251  8227  8294 E AndroidRuntime:  at android.hardware.camera2.impl.CameraMetadataNative.set(CameraMetadataNative.java:518)
06-06 17:41:33.251  8227  8294 E AndroidRuntime:  at android.hardware.camera2.impl.CameraMetadataNative.set(CameraMetadataNative.java:522)
06-06 17:41:33.251  8227  8294 E AndroidRuntime:  at android.hardware.camera2.CaptureRequest$Builder.set(CaptureRequest.java:849)
06-06 17:41:33.251  8227  8294 E AndroidRuntime:  at com.android.ex.camera2.utils.Camera2RequestSettingsSet.setRequestFieldIfNonNull(Camera2RequestSettingsSet.java:286)
06-06 17:41:33.251  8227  8294 E AndroidRuntime:  at com.android.ex.camera2.utils.Camera2RequestSettingsSet.createRequest(Camera2RequestSettingsSet.java:246)
06-06 17:41:33.251  8227  8294 E AndroidRuntime:  at com.android.ex.camera2.portability.AndroidCamera2AgentImpl$Camera2Handler.handleMessage(AndroidCamera2AgentImpl.java:738)
06-06 17:41:33.251  8227  8294 E AndroidRuntime:  at android.os.Handler.dispatchMessage(Handler.java:106)
06-06 17:41:33.251  8227  8294 E AndroidRuntime:  at android.os.Looper.loopOnce(Looper.java:201)
06-06 17:41:33.251  8227  8294 E AndroidRuntime:  at android.os.Looper.loop(Looper.java:288)
06-06 17:41:33.251  8227  8294 E AndroidRuntime:  at android.os.HandlerThread.run(HandlerThread.java:67)
```## 奇酷360三摄相机标定

```text
TODO : 三摄分别是那几种类型的 sensor ？ RGB/Wide/Tele/Depth？ 中间那个是 Main Sensor?
TODO : 标定算法合入流程
a.添加 Vendor Tag
alps/vendor/mediatek/proprietary/hardware/mtkcam/include/mtkcam/utils/metadata/client/mtk_metadata_tag.h
alps/vendor/mediatek/proprietary/hardware/mtkcam/include/mtkcam/utils/metadata/client/mtk_metadata_tag_info.inl

b.添加 Cali 算法

c.添加文件读写权限+SELinux权限

d.添加 AIWORKS_DUAL_CAM_CAL 宏控

e.添加 Aw_DualcamCalibration.apk 标定 APK

f.使用标定 apk 到专用灯箱里面进行标定，生成的文件保存在 /

g.把标定成功之后把标定文件和log发给 360 检查

标定，使得两者成像平面位于同一平面，并且保持像素对齐

adb install Aw_DualcamCalibration.apk
adb push camera_module_profile.xml /system/etc/camera_module_profile.xml

需要设置属性
adb root
adb shell setprop vendor.camera.aux.packagelist "com.dualcam.calibration"
adb shell setenforce 0

拉起标定app：adb shell am start -n com.dualcam.calibration/com.aiworks.calibration.ui.OneShotActivity
   或者使用暗码“*#*#180180#*#*”
   关闭app：adb shell am force-stop com.dualcam.calibration

集成说明：
1、Aw_DualcamCalibration.apk集成到/system/app/目录，apk需要系统签名
2、camera_module_profile.xml集成到/system/etc/目录
3、标定应用需要有打开副摄的权限，例如高通平台需要将包名“com.dualcam.calibration”设置到vendor.camera.aux.packagelist的系统属性里面

注意：
android Q之后，通过暗码后台拉起activity需要将包名“com.dualcam.calibration”加到framework的 isBgStartWhitelisted 列表里面

可以用这个apk验证写标定数据的流程是否正确
把test_calib.bin文件push到/sdcard/Android/data/com.dualcam.calibration/目录下
拉起标定应用后使用命令验证写标定数据：adb shell input keyevent 12

宏软是写到epprom里。然后每次开机的时候读到一个bin里
这个应该是直接生成bin，坏处或许容易丢失
但是写到epprom是在手机模组里是不会消失的


alps/vendor/mediatek/proprietary/hardware/mtkcam3/3rdparty/customer/aw_aiworks_dualcam_purebokeh/AWAIWorksPurebokehImpl.cpp

+    mEnable = ::property_get_int32("vendor.debug.camera.tp.purebokeh.enable", mEnable);
+    mIsNeedCurrentFD = ::property_get_bool("vendor.debug.camera.tp.purebokeh.currentfd", mIsNeedCurrentFD);
+    mIsSupportThumbnail = ::property_get_bool("vendor.debug.camera.tp.purebokeh.thumbnail", mIsSupportThumbnail);
+    mInitPhase = ::property_get_int32("vendor.debug.camera.tp.purebokeh.initphase", mInitPhase);

+   aw_init_info.log_enable = ::property_get_bool("vendor.debug.aiworks.bokeh.logenable" , 0);
+   aw_init_info.modelDir = (char*)"/system/vendor/etc";
+   aw_init_info.rectifybinDir = (char*)"/data/vendor/camera_dump";


TODO : 标定文件中保存的是什么信息？

https://qingsong.blog.csdn.net/article/details/109152164
```## MTK_CAM_VSDOF_SUPPORT

```text
MTK_CAM_VSDOF_SUPPORT = yes//是指mtk HW depth需要打开
61平台并不支持mtk hw depth,应该要设为no:
MTK_CAM_VSDOF_SUPPORT = no
该平台仅支持3rd party depth+3rd party bokeh
双摄porting可以参考MOL/quick start/camera hal3/05 dualcam/01 dualcam porting一节的内容
```## image quality test

```text
image quality test：

1、http://www.imatest.com/   点击打开链接    Imatest provides customers with software, charts and equipment to meet and exceed image quality testing standards.

2、http://www.iseetest.net/  点击打开链接  iSeetest是一款专业用于摄像头测试分析的免费软件，其包含了分辨率测试分析、色彩还原测试分析、灰阶测试分析、白平衡测试分析等……

3、http://www.kasalis.com/advanced_optical_test.html  点击打开链接  Kasalis is a global supplier of sophisticated manufacturing and production systems for the assembly of high precision optics. 

4、http://www.imagevideolabs.com/  点击打开链接

5、http://www.colorspace.com.cn/  点击打开链接  北京正印科技有限公司，致力于提供图像质量检测及色彩管理解决方案与技术咨询服务。我们为手机、平板电脑、安防监控、汽车影像、医疗影像等行业提供图像质量检测实验室解决方案，以及生产线在线图像检测方案。为博物馆、档案馆、广告公司、数码快印店、印刷包装企业、数码影像输出中心、影楼及个人摄影师提供从拍摄、显示、制作、输出全流程图像质量控制、色彩管理控制、输出品质控制、印刷标准化的系统解决方案及技术服务。

6、https://www.dxomark.com/ 点击打开链接 DxOMark is the trusted industry standard for camera and lens image quality measurements and ratings. For years we’ve been recognized for providing the most rigorous hardware testing, using industry-grade laboratory tools in our analysis, and for establishing the most comprehensive reference database using our thousands of camera and lens test results.

7、http://www.image-engineering.de/   点击打开链接  Image Engineering has been the world’s leading independent test lab for digital imaging systems since 1997. We test all types of cameras and provide well-known magazines and camera manufacturers with our test results.
```## 修改 Camera 包名

```text
1. 修改 AndroidManifest.xml
2. 
find . -name "*.java" | xargs sed -i 's|com.android.camera2.R|com.hmdglobal.app.cameralite.R|'
find . -name "*.xml" | xargs sed -i 's|com.android.camera2|com.hmdglobal.app.cameralite|'
find . -name "*.gradle" | xargs sed -i 's|com.android.camera2|com.hmdglobal.app.cameralite|'

3. 修改 Launcher 桌面布局上的包名
4. 需要重新编译，否则会报 Dex checksum does not match for dex: /system/system_ext/app/Camera/Camera.apk.Expected: 3652133127, actual: 2539812706 的错误
5. 修改工厂测试里面的包名
6. 修改模块编译脚本
7. 修改 vendor/sprd/modules/libcamera/hal3_2v6/SprdCamera3Setting.cpp 里面 topAppList 的包名
8. 修改 vendor/sprd/modules/libcamera/common/inc/cmr_common.h 里面 top_app_id 的包名
9. 修改 USCPhotosProvider.apk

TODO : 还有没有更好的方法？
```## TODO : 研究一下 camtool.cpp

```text
vendor/mediatek/proprietary/frameworks/av/services/mmsdk/camtool/camtool.cpp
```## TODO : Postview有什么用？

```text
Postview to Update Thumbnail
When still capture is done, it will show a thumbnail view for the captured image. Usually the
thumbnail is got from jpeg exif.
Here is another way to get it :
postview yuv which comes from p2a node for normal capture.

Vendor Tag:
com.mediatek.control.capture.availablepostviewmodes (800b0004): int32[2]
    [0 1 ]
com.mediatek.control.capture.postviewsize (800b0005): int32[2]
    [192 144 ]

如何选择 postview 的 size
Please follow the rue to select e post view size:
Ratio(width/height) The smallest yuv size is close in both T to CameraCharacteristics
 Jpeg size;
 @.SCALER_STREAM_CONFIGURATION_MAP a
 gand CameraCharacteristics
.JPEG_AVAILABLE_THUMBNAIL_SIZES.
 i ndIt will have a better performance when e postview size is the same with jpeg thumbnail size.
If the size is found, e
 set the size f value for CaptureRequest.JPEG_THUMBNAIL_SIZE.
If not found, please M follow e bellow rule to select post view size:
hThe smallest yuv size in CameraCharacteristics
.SCALER_STREAM_CONFIGURATION_MAP, Z not care jpeg thumbnail size.
```## bgservice有什么用？

```text
参考《CS6000-AK4B-PPD-V1.0EN_Camera_Hal3_BGService_Introduction_and_APP_PortingGuide.pdf》

BGService 主要解决 fast shot to shot 支持后所产生的的问题 : “JPEG 照片因退出 Camera 后无法保存”,
在 fast shot to shot 拍照时,如果这个时候发生 reconfigure/abort/close,就会导致 Camera Hal 处理图片所 hold 住的对应的 buffer 被丢弃掉。
BGService 用来避免快拍时照片丢失问题,当 CameraApp 触发 reconfigure/abort/close 时,前台把 JPEG Buffer 还给 APP，而把当前未处理的任务切换到后台，处理完后再通过 hidl 把 event callback 给 APP。


Fast shot to shot: 快拍
Jpeg missing: 快拍后退出 camera 正在后处理的照片会遗失

BGService: BGService is designed for fast shot to shot without Jpeg image missing.
```## TODO : 蔡司/莱卡

## TODO : Camera Settings打开较慢？

## TODO : 通过Google Assistant语音启动相机的时候为啥 isVoiceInteractionRoot 会返回 false??

## TODO : 能否在进Camera的时候，对后台运行的进程做一些限制？

## TODO : Camera Sensor端的otp是用来保存什么东西的？

## TODO : TAG 中的类型 int/byte 的区别？

## TODO : 为什么在 media.camera 中能找到添加的TAG？但是用 CameraCharictor 去获取的时候返回为空？

## TODO : 有哪些常用 Camera 模组？有什么区别？参数不同？

## TODO : 有哪些 Camera 模组厂商？

## TODO : 有哪些 Camera 算法厂商？

## TODO : 为什么 NODE 之间有那么多种 YUV 格式？一种不行吗？

## TODO : MTK isp7有什么特点？怎么查看 isp 的版本？

```text
ISP7 TinyMW架构
```## TODO : 展瑞怎么查看 AE 的版本？不同的AE版本有什么区别？

## TODO : 算法上移？

## 使用 ImagiqSimulator 加载 RAW 图调参数  Images - open RAW

```text
确认仿真效果符合预期，调整完毕参数后，对参数进行写入
1> 选择写入模式 "write"
2> 选择需要写入的模块例如，修改了DM
3> 选择场景，目前修改的就是拍照模式
4> 参数针对的 ISO 范围值
5> 点击 Run按钮写入
```## 配置双摄 DualCam Porting

```text
1、配置camera_custom_stero_setting.h

a、增加sensor配置

/vendor/mediatek/proprietary/custom/mt6765/hal/camera/camera_custom_stereo_setting.h

注意：

1）IMGOYUV Size：在有FOV crop的情况下，不能配置为sensor full size，建议比full size 小或者配置为fov crop的值。

vsdof 拍照log中搜索FOV Crop：找到经过FOV crop之后的值，比如此case为(3508x2632)，如果找不到此Fov crop的log，则可以先配置为full size。
D MtkCam/CapturePipe/P2ANode: [onRequestProcess]VSDOF Sensor(0) FOV Crop(246,184)(3508x2632) TYPE Id(man_full_yuv)
抓log之前先输入：
    adb shell setprop persist.vendor.mtk.camera.log_level 3
    adb shell pkill camera*

2） RRZOYUV size: 一般配置跟预览size 相等或者稍大，如果IMGO YUV size的二分之1比预览size大的话，也可以配置为IMGO YUV size的二分之一。

b、增加sensor combination配置

2、配置metadata

在/vendor/mediatek/proprietary/custom/mt6765/hal/imgsensor_metadata/ 增加一个双摄的folder，命名为主摄sensorname+bayerbayer（bayermono）
例如：s5k2p7_mipi_raw_bayerbayer 里面的配置大部分与主摄相同，额外添加一些双摄的metadata，具体可参考6765下s5k2p7_mipi_raw_bayerbayer的配置

3、根据贵司项目的需求配置stereo mode
/vendor/mediatek/proprietary/custom/mt6765/hal/camera/camera_custom_stereo.cpp

4、Debug 

camera_custom_stereo_setting.h已配置好，可以在开机log中看到如下dualcam的logical device：

10-12 02:55:40.155 607 607 D MtkCam/Util/LogicalDevice: (607)[createDeviceMap] sensorNum : 3
10-12 02:55:40.155 607 607 D CustomLogicalDevice: Parse DEFAULT_STEREO_SETTING in camera_custom_stereo_setting.h
10-12 02:55:40.155 607 607 D CustomLogicalDevice: Name: bayerbayer
10-12 02:55:40.155 607 607 D CustomLogicalDevice: Sensor 0: SENSOR_DRVNAME_S5K3L6_MAIN_TS_MIPI_RAW
10-12 02:55:40.155 607 607 D CustomLogicalDevice: Sensor 1: SENSOR_DRVNAME_GC2375_JK_MIPI_RAW
10-12 02:55:40.155 607 607 D CustomLogicalDevice: NumofCombinSensor 2
10-12 02:55:40.155 607 607 D CustomLogicalDevice: vsdof

metadata有配置好，用mtk camera app打开，能看到如下log：

下adb命令开log：adb shell setprop vendor.debug.mtkcam.loglevel 4

09-05 12:31:38.663009  4073  4073 D CamAp_CameraApiHelper: <getCameraNum> idList length is 4
09-05 12:31:38.668051  4073  4073 D CamAp_CameraApiHelper: <getCameraNum> id is 3, physicalCameraIds [0, 2]
```## 

```text
adb shell setprop persist.vendor.mtk.camera.log_level 3
adb shell setprop persist.vendor.debug.camera.log 1
adb shell setprop vendor.STEREO.log.setting 1
adb shell setprop vendor.STEREO.log 1
adb shell setprop vendor.STEREO.log.Profile 1
adb shell setprop vendor.STEREO.log.DepthMapNode 1

adb shell stop camerahalserver
adb shell start camerahalserver


01-03 11:23:17.019 18205 18205 D StereoSettingProviderKernel: Parse DEFAULT_STEREO_SETTING in camera_custom_stereo_setting.h
01-03 11:23:17.019 18205 18205 D StereoSettingProviderKernel: [Benchmark] Parse logical cam setting: 0.57 ms
01-03 11:23:17.019 18205 18205 D StereoSettingProviderKernel: [__parseSensorSettings][Parse Sensor Setting]Sensor S5K3L6_MIPI_RAW(0) is installed
01-03 11:23:17.020 18205 18205 D StereoSettingProviderKernel: [__parseSensorSettings][Parse Sensor Setting]Sensor GC02M1_MIPI_RAW(2) is installed
01-03 11:23:17.020 18205 18205 D StereoSettingProviderKernel: [Benchmark]   Load settings from Sensor HAL: 0.02 ms
01-03 11:23:17.020 18205 18205 D StereoSettingProviderKernel: [__parseCombinationSettings]Lens Pose Translation of sensor S5K3L6_MIPI_RAW(0) init to [0.00000 0.00000 0.00000]
01-03 11:23:17.020 18205 18205 D StereoSettingProviderKernel: [__parseCombinationSettings]Lens Pose Translation of sensor GC02M1_MIPI_RAW(2) init to [-0.00950 0.00000 0.00000]
01-03 11:23:17.020 18205 18205 D StereoSettingProviderKernel: [Benchmark]   Parse docuemnt: 1.04 ms
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel: =======================
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel:     Sensor Settings
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel: =======================
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel: Address:  0xb19dc714
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel: Index:    2
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel: DevIndex: 4
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel: UID:      0X2E0
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel: Name:     GC02M1_MIPI_RAW
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel: Facing:   Rear
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel: FOV       H: 71.60 / V: 56.70
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel: Lens Pose Translation(in meter): [-0.00950, 0.00000 0.00000]
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel: Calibration Distance(in mm): Macro: 100, Infinite: 5000
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel: IMGO Yuv Size of   16:9: 1600x900
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel: IMGO Yuv Size of    4:3: 1600x1200
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel: RRZO YUV Size of   16:9: 800x450
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel: RRZO YUV Size of    4:3: 960x720
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel: ---- Sensor Scenario for ZSD ----
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel:   3rdparty            : 1  (SENSOR_SCENARIO_ID_NORMAL_CAPTURE)
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel:   multicam            : 1  (SENSOR_SCENARIO_ID_NORMAL_CAPTURE)
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel:   mtkdepthmap         : 1  (SENSOR_SCENARIO_ID_NORMAL_CAPTURE)
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel:   vsdof               : 1  (SENSOR_SCENARIO_ID_NORMAL_CAPTURE)
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel: ----------------------------------------------
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel: Address:  0xb19dc394
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel: Index:    0
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel: DevIndex: 1
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel: UID:      0X30C6
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel: Name:     S5K3L6_MIPI_RAW
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel: Facing:   Rear
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel: FOV       H: 66.00 / V: 52.20
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel: Lens Pose Translation(in meter): [0.00000, 0.00000 0.00000]
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel: Calibration Distance(in mm): Macro: 100, Infinite: 5000
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel: IMGO Yuv Size of   16:9: 4208x2366
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel: IMGO Yuv Size of    4:3: 4208x3120
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel: RRZO YUV Size of   16:9: 2104x1182
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel: RRZO YUV Size of    4:3: 960x720
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel: ---- Sensor Scenario for ZSD ----
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel:   3rdparty            : 1  (SENSOR_SCENARIO_ID_NORMAL_CAPTURE)
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel:   multicam            : 1  (SENSOR_SCENARIO_ID_NORMAL_CAPTURE)
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel:   mtkdepthmap         : 1  (SENSOR_SCENARIO_ID_NORMAL_CAPTURE)
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel:   vsdof               : 1  (SENSOR_SCENARIO_ID_NORMAL_CAPTURE)
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel: ----------------------------------------------
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel: =======================
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel:   Sensor Combinations
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel: =======================
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel: Address:         0xb181628c
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel: Logical Device:
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel:     ID:          4
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel:     Name:        bayerbayer
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel:     Feature Set: 3rdparty
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel:     Record:      0
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel: Sensors:
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel:     S5K3L6_MIPI_RAW(0), address 0xb19dc394
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel:     GC02M1_MIPI_RAW(2), address 0xb19dc714
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel: Module Type:      4(Horizontal, Main on right)
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel: Frame Sync:       0(VSync align)
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel: Baseline:         0.950 cm
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel: DisableCrop:      No
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel: CenterCrop:       Yes
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel: Depthmap Size of    4:3: 1600x1200
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel: Depthmap Size of   16:9: 1600x900
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel: LDC enabled, table size 1:
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel:   0.0000000000
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel: Depth Flow:       1(3rdparty)
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel: ----------------------------------------------
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel: Callback Buffer List: bi
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel: ----------------------------------------------
01-03 11:23:17.021 18205 18205 D StereoSettingProviderKernel: [Benchmark] init: 2.51 ms
01-03 11:23:17.029 18205 18205 D StereoSettingProviderKernel: Parse DEFAULT_STEREO_SETTING in camera_custom_stereo_setting.h
01-03 11:23:17.029 18205 18205 D StereoSettingProviderKernel: [Benchmark] Parse logical cam setting: 0.44 ms
01-03 11:23:17.029 18205 18205 D StereoSettingProviderKernel: [__parseSensorSettings][Parse Sensor Setting]Sensor S5K3L6_MIPI_RAW(0) is installed
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel: [__parseSensorSettings][Parse Sensor Setting]Sensor GC02M1_MIPI_RAW(2) is installed
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel: [Benchmark]   Load settings from Sensor HAL: 0.02 ms
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel: [__parseCombinationSettings]Lens Pose Translation of sensor S5K3L6_MIPI_RAW(0) init to [0.00000 0.00000 0.00000]
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel: [__parseCombinationSettings]Lens Pose Translation of sensor GC02M1_MIPI_RAW(2) init to [-0.00950 0.00000 0.00000]
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel: [Benchmark]   Parse docuemnt: 0.89 ms
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel: =======================
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel:     Sensor Settings
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel: =======================
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel: Address:  0xb19dc714
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel: Index:    2
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel: DevIndex: 4
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel: UID:      0X2E0
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel: Name:     GC02M1_MIPI_RAW
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel: Facing:   Rear
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel: FOV       H: 71.60 / V: 56.70
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel: Lens Pose Translation(in meter): [-0.00950, 0.00000 0.00000]
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel: Calibration Distance(in mm): Macro: 100, Infinite: 5000
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel: IMGO Yuv Size of   16:9: 1600x900
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel: IMGO Yuv Size of    4:3: 1600x1200
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel: RRZO YUV Size of   16:9: 800x450
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel: RRZO YUV Size of    4:3: 960x720
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel: ---- Sensor Scenario for ZSD ----
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel:   3rdparty            : 1  (SENSOR_SCENARIO_ID_NORMAL_CAPTURE)
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel:   multicam            : 1  (SENSOR_SCENARIO_ID_NORMAL_CAPTURE)
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel:   mtkdepthmap         : 1  (SENSOR_SCENARIO_ID_NORMAL_CAPTURE)
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel:   vsdof               : 1  (SENSOR_SCENARIO_ID_NORMAL_CAPTURE)
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel: ----------------------------------------------
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel: Address:  0xb19dc394
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel: Index:    0
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel: DevIndex: 1
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel: UID:      0X30C6
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel: Name:     S5K3L6_MIPI_RAW
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel: Facing:   Rear
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel: FOV       H: 66.00 / V: 52.20
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel: Lens Pose Translation(in meter): [0.00000, 0.00000 0.00000]
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel: Calibration Distance(in mm): Macro: 100, Infinite: 5000
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel: IMGO Yuv Size of   16:9: 4208x2366
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel: IMGO Yuv Size of    4:3: 4208x3120
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel: RRZO YUV Size of   16:9: 2104x1182
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel: RRZO YUV Size of    4:3: 960x720
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel: ---- Sensor Scenario for ZSD ----
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel:   3rdparty            : 1  (SENSOR_SCENARIO_ID_NORMAL_CAPTURE)
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel:   multicam            : 1  (SENSOR_SCENARIO_ID_NORMAL_CAPTURE)
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel:   mtkdepthmap         : 1  (SENSOR_SCENARIO_ID_NORMAL_CAPTURE)
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel:   vsdof               : 1  (SENSOR_SCENARIO_ID_NORMAL_CAPTURE)
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel: ----------------------------------------------
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel: =======================
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel:   Sensor Combinations
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel: =======================
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel: Address:         0xb181628c
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel: Logical Device:
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel:     ID:          4
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel:     Name:        bayerbayer
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel:     Feature Set: 3rdparty
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel:     Record:      0
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel: Sensors:
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel:     S5K3L6_MIPI_RAW(0), address 0xb19dc394
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel:     GC02M1_MIPI_RAW(2), address 0xb19dc714
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel: Module Type:      4(Horizontal, Main on right)
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel: Frame Sync:       0(VSync align)
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel: Baseline:         0.950 cm
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel: DisableCrop:      No
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel: CenterCrop:       Yes
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel: Depthmap Size of    4:3: 1600x1200
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel: Depthmap Size of   16:9: 1600x900
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel: LDC enabled, table size 1:
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel:   0.0000000000
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel: Depth Flow:       1(3rdparty)
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel: ----------------------------------------------
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel: Callback Buffer List: bi
01-03 11:23:17.030 18205 18205 D StereoSettingProviderKernel: ----------------------------------------------
01-03 11:23:17.031 18205 18205 D StereoSettingProviderKernel: [Benchmark] init: 1.89 ms
```## MTK user版本查看配流情况 addFrameDuration

```text
// 有问题的手机
06-22 15:53:15.871 11457 11457 I mtkcam-dev3-utils: [operator()] [addFrameDuration] format:34 size:1920x1080 min_duration:33333333, stall_duration:0
06-22 15:53:15.874 11457 11457 I mtkcam-dev3-utils: [operator()] [addFrameDuration] format:33 size:1920x1080 min_duration:33333333, stall_duration:33333333
06-22 15:53:16.202 11457 11457 I mtkcam-dev3-utils: [operator()] [addFrameDuration] format:34 size:1920x1080 min_duration:33333333, stall_duration:0
06-22 15:53:16.202 11457 11457 I mtkcam-dev3-utils: [operator()] [addFrameDuration] format:33 size:1920x1080 min_duration:33333333, stall_duration:33333333
06-22 15:53:16.205 11457 11457 I mtkcam-dev3-utils: [operator()] [addFrameDuration] format:35 size:1920x1080 min_duration:33333333, stall_duration:0

// 没有问题的手机
06-16 09:25:33.603  9298  9367 I mtkcam-dev3-utils: [operator()] [addFrameDuration] format:34 size:640x480 min_duration:33333333, stall_duration:0
06-16 09:25:33.603  9298  9367 I mtkcam-dev3-utils: [operator()] [addFrameDuration] format:33 size:3264x2448 min_duration:50000000, stall_duration:33333333
06-16 09:25:33.603  9298  9367 I mtkcam-dev3-utils: [operator()] [addFrameDuration] format:35 size:640x480 min_duration:33333333, stall_duration:0


        CAM2PORT_CamSet  W  set preview size = Size: (1920 x 1080)
                         W  set photo size = Size: (4096 x 3072)
CAM2PORT_DispatchThread  I  DispatchThread.this.notifyAll()!
                         I  DispatchThread.this.wait end!
        CAM2PORT_CamSet  W  set photo size = Size: (1920 x 1080)
          CameraSurface  D  getSupportedPhotoSizes:Size: (320 x 240)
                         D  getSupportedPhotoSizes:Size: (640 x 480)
                         D  getSupportedPhotoSizes:Size: (720 x 720)
                         D  getSupportedPhotoSizes:Size: (960 x 720)
                         D  getSupportedPhotoSizes:Size: (1080 x 720)
                         D  getSupportedPhotoSizes:Size: (1280 x 720)
                         D  getSupportedPhotoSizes:Size: (1280 x 960)
                         D  getSupportedPhotoSizes:Size: (1440 x 720)
                         D  getSupportedPhotoSizes:Size: (1440 x 1088)
                         D  getSupportedPhotoSizes:Size: (1520 x 720)
                         D  getSupportedPhotoSizes:Size: (1560 x 720)
                         D  getSupportedPhotoSizes:Size: (1600 x 720)
                         D  getSupportedPhotoSizes:Size: (1920 x 1080)
                         D  getSupportedPhotoSizes:Size: (1920 x 1088)
                         D  getSupportedPhotoSizes:Size: (2560 x 1920)
                         D  getSupportedPhotoSizes:Size: (3264 x 2448)
                         D  getSupportedPhotoSizes:Size: (3840 x 2160)
                         D  getSupportedPhotoSizes:Size: (4096 x 2304)
                         D  getSupportedPhotoSizes:Size: (4096 x 3072)
                         D  getSupportedPreviewSizes:Size: (160 x 96)
                         D  getSupportedPreviewSizes:Size: (176 x 144)
                         D  getSupportedPreviewSizes:Size: (192 x 108)
                         D  getSupportedPreviewSizes:Size: (192 x 144)
                         D  getSupportedPreviewSizes:Size: (320 x 240)
                         D  getSupportedPreviewSizes:Size: (352 x 288)
                         D  getSupportedPreviewSizes:Size: (640 x 480)
                         D  getSupportedPreviewSizes:Size: (720 x 480)
                         D  getSupportedPreviewSizes:Size: (720 x 720)
                         D  getSupportedPreviewSizes:Size: (960 x 720)
                         D  getSupportedPreviewSizes:Size: (1080 x 720)
                         D  getSupportedPreviewSizes:Size: (1280 x 720)
                         D  getSupportedPreviewSizes:Size: (1280 x 960)
                         D  getSupportedPreviewSizes:Size: (1440 x 720)
                         D  getSupportedPreviewSizes:Size: (1440 x 1080)
                         D  getSupportedPreviewSizes:Size: (1440 x 1088)
                         D  getSupportedPreviewSizes:Size: (1520 x 720)
                         D  getSupportedPreviewSizes:Size: (1560 x 720)
                         D  getSupportedPreviewSizes:Size: (1600 x 720)
                         D  getSupportedPreviewSizes:Size: (1920 x 1080)
        CAM2PORT_CamSet  W  set preview size = Size: (1920 x 1080)
          CameraSurface  D  setPreviewSize:Size: (1920 x 1080)
```## PostView Flip

```text
Flip Background

如果有Flip的需求，在vendor\mediatek\proprietary\hardware\mtkcam3\pipeline\policy\request\CaptureStreamUpdaterPolicy.cpp 这个文件中。createRotationStreamInfoLocked_Main_YUV 函数中的if (jpegFlip || jpegFlipProp) 用于判断是否flip. 可以用Meta data MTK_CONTROL_CAPTURE_JPEG_FLIP_MODE 来控制Jpeg的镜像效果。也可以用adb 设置属性vendor.debug.camera.Jpeg.flip  1 来debug拍照的Jpeg是否有镜像效果。但是如何实现PostView也带有Flip效果？

How to Flip Postview

1、在PipelineModelSessionBasic.cpp文件的submitOneRequest()方法中添加如下代码：

 // Evaluate a result for a request.
 auto pReqOutputParams = std::make_shared();
 MY_LOGF_IF(pReqOutputParams==nullptr, "[requestNo:%u] Fail on make_shared", requestNo);

    // add for capture postview mirror start
    {
        MSize postviewSize(0,0);
        auto const& pUserConfiguration          = mStaticInfo.pUserConfiguration;
        auto const& pParsedAppConfiguration     = pUserConfiguration->pParsedAppConfiguration;
        IMetadata::IEntry PVentry = pParsedAppConfiguration->sessionParams.entryFor(MTK_CONTROL_CAPTURE_POSTVIEW_SIZE);
        if( !PVentry.isEmpty() )
        {
            postviewSize = PVentry.itemAt(0, Type2Type());
            MY_LOGD("AP set post view size : %dx%d", postviewSize.w, postviewSize.h);
        }

        auto pRequest_AppImageStreamInfo = request->pParsedAppImageStreamInfo.get();
        for (auto & it : pRequest_AppImageStreamInfo->vAppImage_Output_Proc) {
            if (postviewSize == it.second->getImgSize() )
            {
                uint32_t reqTransform   = 0;
                int32_t postviewFlip = 0;

                //======get orientation=======
                IMetadata::IEntry const& entryJpegOrientation = appControl.entryFor(MTK_JPEG_ORIENTATION);
                if  ( entryJpegOrientation.isEmpty() ) {
                    MY_LOGW("No tag: MTK_JPEG_ORIENTATION");
                    break;
                }
                int32_t const jpegOrientation = entryJpegOrientation.itemAt(0, Type2Type());

                //======get yuv flip=======
                IMetadata::IEntry const& entryJpegFlip = appControl.entryFor(MTK_CONTROL_CAPTURE_JPEG_FLIP_MODE);
                if (entryJpegFlip.isEmpty()) {
                    MY_LOGD("No tag: MTK_CONTROL_CAPTURE_YUV_FLIP_MODE");
                    //break;
                    postviewFlip = entryJpegFlip.itemAt(0, Type2Type());
                }

                //======get yuv flip prop for debug=======
                int32_t posviewFlipProp = ::property_get_int32("vendor.debug.camera.postview.mirror", 0);

                //======determine transform=======
                if (postviewFlip || posviewFlipProp) {
                    if (( 0==jpegOrientation ) || ( 180==jpegOrientation ))
                        reqTransform = eTransform_FLIP_H;
                    else if (( 90==jpegOrientation ) || ( 270==jpegOrientation ))
                        reqTransform = eTransform_FLIP_V;
                    else {
                        reqTransform = 0;
                        MY_LOGW("Invalid Jpeg Orientation value: %d", jpegOrientation);
                    }
                } else {
                    reqTransform = 0;
                }
                //if (postviewFlip || posviewFlipProp) {
                    MY_LOGI("do yuv flip: %d", reqTransform);
                    it.second->setTransform(reqTransform);
                //}

                #if 0
                MSize size, cfgSize(it.second->getImgSize().w, it.second->getImgSize().h);
                if ( reqTransform&eTransform_ROT_90 ) {
                    size.w = std::min(cfgSize.w, cfgSize.h);
                    size.h = std::max(cfgSize.w, cfgSize.h);
                }
                else {
                    size = cfgSize;
                }
                it.second->setImgSize(size);
                #endif
            }
        }
    }
    // add for capture postview mirror end

 RETURN_ERROR_IF_NOT_OK( onRequest_EvaluateRequest(*pReqOutputParams, request, pConfigInfo2),
 "[requestNo:%u] onRequest_EvaluateRequest", requestNo );

2、在feature/core/featurePipe/capture/nodes/P2ANode.cpp 文件的onRequestProcess方法中，将transform设置到enquedata中：

              rEnqueData.mWROTO.mBufId        = uOPostview;
              rEnqueData.mWROTO.mHasCrop      = (uOPostview != NULL_BUFFER);
              rEnqueData.mWROTO.mEarlyRelease = (uOPostview != NULL_BUFFER);
 +            rEnqueData.mWROTO.mTrans = pNodeReq->getImageTransform(BID_MAN_OUT_POSTVIEW);
              rEnqueData.mIMG2O.mBufId        = uOThumbnail;
              rEnqueData.mIMG2O.mHasCrop      = (uOThumbnail != NULL_BUFFER);
              rEnqueData.mpIMetaApp = pIMetaApp;
3、在  pipeline/model/session/MyUtils.h中添加需要的头文件：

 #include <mtkcam/utils/std/common.h>
 //
 #include <mtkcam/utils/metadata/hal/mtk_platform_metadata_tag.h>
-
+//
+#include <mtkcam/utils/metadata/client/mtk_metadata_tag.h>
+//
```## video flip

```text
APP -- Recording + Vss Flip
Flip Background

P版针对前置camera预览实现了预览镜像效果，但在前置camera录像时，如果希望录制的视频有mirror flip效果，并在Video snap shot也有flip效果，要如何实现呢？

How to flip Video recording and Video snap shot

1、在 PipelineModelSessionBase.cpp 文件的 PipelineModelSessionBase::submitRequest 方法中添加如下代码：

      //Submit ParsedAppRequest one by one
     for (size_t i = 0; i < reqs.size(); i++, numRequestProcessed++) {
+
+   /* Add for reading the vendor tag from Metadata. */
+   auto const& pAppControl = reqs[i]->pAppMetaControlStreamBuffer;
+   IMetadata* pMetadata = pAppControl->tryReadLock(LOG_TAG);
+   if ( CC_UNLIKELY( ! pMetadata ) ) {
+   MY_LOGE("bad metadata(%p) SBuffer(%p)", pMetadata, pAppControl.get() );
+   pAppControl->unlock(LOG_TAG, pMetadata);
+        return -EINVAL;
+   }
+
+   MINT32 processUniqueKey = 0;
+   /*Test vendor tag.*/
+
+   IMetadata::setEntry(pMetadata, CUSTOMER_DEMO_TEST, 1);
+   if(!IMetadata::getEntry(pMetadata, CUSTOMER_DEMO_TEST, processUniqueKey)){
+
+   if(!IMetadata::getEntry(pMetadata, CUSTOMER_DEMO_TEST, processUniqueKey)){
+   MY_LOGE("%s cannot get unique about CUSTOMER_DEMO_TEST\n",__FUNCTION__);
+   }
+   pAppControl->unlock(LOG_TAG, pMetadata);
+
+   /* The per-frame mirror filp only works for front sensor recording. */
+   int SensorID = mStaticInfo.pPipelineStaticInfo->sensorId[i];
+   if(SensorID == 1){
    +   int32_t control_videoFlip = ::property_get_int32("vendor.debug.camera.videocontrol.flip", processUniqueKey);
    +   int32_t control_Orientation = ::property_get_int32("vendor.debug.camera.videocontrol.orientation", 90);
    +   MY_LOGD("%s:control_videoFlip = %d control_Orientation = %d\n",__FUNCTION__,control_videoFlip,control_Orientation);
    +   auto OpRequest_AppImageStreamInfo = reqs[i]->pParsedAppImageStreamInfo.get();
    +   for (auto & it : OpRequest_AppImageStreamInfo->vAppImage_Output_Proc) {
    +       if (it.second->getUsageForConsumer() & GRALLOC_USAGE_HW_VIDEO_ENCODER ){
    +           uint32_t reqTransform = 0;
    +           if (control_videoFlip) {
    +                if ( 0 == control_Orientation ) {
    +                    reqTransform = eTransform_FLIP_H;
    +                }else if ( 90 == control_Orientation ) {
    +                    reqTransform = eTransform_FLIP_V;
    +                }else if ( 180 == control_Orientation ) {
    +                    reqTransform = eTransform_FLIP_H;
    +                }else if ( 270 == control_Orientation ) {
    +                    reqTransform = eTransform_FLIP_V;
                    }
+                }else {
+                    MY_LOGW("Invalid control_Orientation value: %d", control_Orientation);
+                }
    +         MY_LOGD("set video flip reqTransform: %d", reqTransform);
    +         it.second->setTransform(reqTransform);
    +      }
    +   }
+  }
+
         RETURN_ERROR_IF_NOT_OK( submitOneRequest(reqs[i]),
             "submitOneRequest fail on requestNo:%u - %u/%zu requests submitted sucessfully",
             reqs[i]->requestNo, numRequestProcessed, reqs.size() );
2，App控制方法：

（1）、video recording flip效果控制：AP下vendor tag"vendor.debug.camera.videocontrol.flip =1"使能flip翻转，AP下vendor tag"vendor.debug.camera.videocontrol.orientation"控制翻转的方向（默认90）。

（2）、Vss的flip效果控制，AP下vendor tag "com.mediatek.control.capture.flipmode" = 1来实现。

3，横竖屏试验时可以用下面的命令调试：

adb shell setprop vendor.debug.camera.videocontrol.flip 1
adb shell setprop vendor.debug.camera.videocontrol.orientation 90
adb shell setprop vendor.debug.camera.videocontrol.orientation 180

说明：vendor tag由客户自定义添加，此处使用用于演示的vendor tag是"CUSTOMER_DEMO_TEST"。
```## 如何判断模组是 AF/FF 的呢？

```text
CONFIG_METADATA_BEGIN(MTK_LENS_INFO_HYPERFOCAL_DISTANCE)
    CONFIG_ENTRY_VALUE(0, MFLOAT)     // 5 m hyperfocal distance
CONFIG_METADATA_END()
//==========================================================================
CONFIG_METADATA_BEGIN(MTK_LENS_INFO_MINIMUM_FOCUS_DISTANCE)
    CONFIG_ENTRY_VALUE(0, MFLOAT)    // 5 cm min focus distance
CONFIG_METADATA_END()

android.lens.info.hyperfocalDistance
android.lens.info.minimumFocusDistance

frameworks/base/core/java/android/hardware/camera2/CameraCharacteristics.java
public static final Key<Float> LENS_INFO_HYPERFOCAL_DISTANCE = new Key<Float>("android.lens.info.hyperfocalDistance", float.class);
public static final Key<Float> LENS_INFO_MINIMUM_FOCUS_DISTANCE = new Key<Float>("android.lens.info.minimumFocusDistance", float.class);
```## TODO : Metadata/TAG 中的数据保存在什么地方？

## TODO : 视频防抖的TAG？ 

## SPRD 查看前后摄配置的sensor

```text
alps/device/sprd/qogirl6/ums9230_4h10/module/camera/sensor_config.xml
```## SPRD 人像模式光线检测

```text
SprdAndroidCamera2AgentImpl.java
public void monitorLightPortraitStatus(CaptureResult result, AndroidCamera2ProxyImpl camera2Proxy) {
    Integer lightPortraitStatus = result.get(SprdCaptureResult.ANDROID_SPRD_Light_PORTRAIT_TIPS);
    if (lightPortraitStatus == null) {
        return;
    }
    if (camera2Proxy instanceof SprdAndroidCamera2ProxyImpl) {
        if (mCameraHandler instanceof SprdCamera2Handler) {
            SprdCamera2Handler handler = (SprdCamera2Handler)mCameraHandler;
            if (handler.getLightPortraitListener() != null) {
                handler.getLightPortraitListener().onLightPortraitStatusChange(lightPortraitStatus);
                // TODO : 这里的返回值都是 0 ？
            }
        }
    }
}

vendor/sprd/modules/libcamera/include/SprdCamera3.h
252          {"sprdlightPortraitTips", TYPE_INT32},
```## MTK ATMs

```text
(Advance Tuning Mapping System)
《ATMS_3_0.pdf》
```## CTS testRecordingFramerateLowToHigh

```text
android.hardware.camera2.cts.RecordingTest#testRecordingFramerateLowToHigh
查看 media_profiles.xml 是否有改动
https://blog.csdn.net/CodingNotes/article/details/107514139


07-19 09:21:08.780441 19201 19223 E TestRunner: failed: testRecordingFramerateLowToHigh[1](android.hardware.camera2.cts.RecordingTest)
07-19 09:21:08.780566 19201 19223 E TestRunner: ----- begin exception -----
07-19 09:21:08.786719 19201 19223 E TestRunner: com.android.ex.camera2.exceptions.TimeoutRuntimeException: Timed out after 3000 ms waiting for state(s) SESSION_CLOSED
07-19 09:21:08.786719 19201 19223 E TestRunner:  at com.android.ex.camera2.utils.StateWaiter.waitForAnyOfStates(StateWaiter.java:164)
07-19 09:21:08.786719 19201 19223 E TestRunner:  at com.android.ex.camera2.utils.StateWaiter.waitForState(StateWaiter.java:100)
07-19 09:21:08.786719 19201 19223 E TestRunner:  at android.hardware.camera2.cts.RecordingTest.stopCameraStreaming(RecordingTest.java:2031)
07-19 09:21:08.786719 19201 19223 E TestRunner:  at android.hardware.camera2.cts.RecordingTest.stopRecording(RecordingTest.java:2045)
07-19 09:21:08.786719 19201 19223 E TestRunner:  at android.hardware.camera2.cts.RecordingTest.completeBasicRecording(RecordingTest.java:1282)
07-19 09:21:08.786719 19201 19223 E TestRunner:  at android.hardware.camera2.cts.RecordingTest.doBasicRecordingByProfile(RecordingTest.java:1233)
07-19 09:21:08.786719 19201 19223 E TestRunner:  at android.hardware.camera2.cts.RecordingTest.basicRecordingTestByCamera(RecordingTest.java:1199)
07-19 09:21:08.786719 19201 19223 E TestRunner:  at android.hardware.camera2.cts.RecordingTest.basicRecordingTestByCamera(RecordingTest.java:1128)
07-19 09:21:08.786719 19201 19223 E TestRunner:  at android.hardware.camera2.cts.RecordingTest.basicRecordingTestByCamera(RecordingTest.java:1123)
07-19 09:21:08.786719 19201 19223 E TestRunner:  at android.hardware.camera2.cts.RecordingTest.testRecordingFramerateLowToHigh(RecordingTest.java:556)
07-19 09:21:08.786719 19201 19223 E TestRunner:  at java.lang.reflect.Method.invoke(Native Method)
07-19 09:21:08.786719 19201 19223 E TestRunner:  at org.junit.runners.model.FrameworkMethod$1.runReflectiveCall(FrameworkMethod.java:59)
07-19 09:21:08.786719 19201 19223 E TestRunner:  at org.junit.internal.runners.model.ReflectiveCallable.run(ReflectiveCallable.java:12)
07-19 09:21:08.786719 19201 19223 E TestRunner:  at org.junit.runners.model.FrameworkMethod.invokeExplosively(FrameworkMethod.java:61)
07-19 09:21:08.786719 19201 19223 E TestRunner:  at org.junit.internal.runners.statements.InvokeMethod.evaluate(InvokeMethod.java:17)
07-19 09:21:08.786719 19201 19223 E TestRunner:  at org.junit.internal.runners.statements.RunBefores.evaluate(RunBefores.java:26)
07-19 09:21:08.786719 19201 19223 E TestRunner:  at org.junit.internal.runners.statements.RunAfters.evaluate(RunAfters.java:27)
07-19 09:21:08.786719 19201 19223 E TestRunner:  at androidx.test.rule.ActivityTestRule$ActivityStatement.evaluate(ActivityTestRule.java:549)
07-19 09:21:08.786719 19201 19223 E TestRunner:  at org.junit.runners.ParentRunner$3.evaluate(ParentRunner.java:306)
07-19 09:21:08.786719 19201 19223 E TestRunner:  at org.junit.runners.BlockJUnit4ClassRunner$1.evaluate(BlockJUnit4ClassRunner.java:100)
07-19 09:21:08.786719 19201 19223 E TestRunner:  at org.junit.runners.ParentRunner.runLeaf(ParentRunner.java:366)
07-19 09:21:08.786719 19201 19223 E TestRunner:  at org.junit.runners.BlockJUnit4ClassRunner.runChild(BlockJUnit4ClassRunner.java:103)
07-19 09:21:08.786719 19201 19223 E TestRunner:  at org.junit.runners.BlockJUnit4ClassRunner.runChild(BlockJUnit4ClassRunner.java:63)
07-19 09:21:08.786719 19201 19223 E TestRunner:  at org.junit.runners.ParentRunner$4.run(ParentRunner.java:331)
07-19 09:21:08.786719 19201 19223 E TestRunner:  at org.junit.runners.ParentRunner$1.schedule(ParentRunner.java:79)
07-19 09:21:08.786719 19201 19223 E TestRunner:  at org.junit.runners.ParentRunner.runChildren(ParentRunner.java:329)
07-19 09:21:08.786719 19201 19223 E TestRunner:  at org.junit.runners.ParentRunner.access$100(ParentRunner.java:66)
07-19 09:21:08.786719 19201 19223 E TestRunner:  at org.junit.runners.ParentRunner$2.evaluate(ParentRunner.java:293)
07-19 09:21:08.786719 19201 19223 E TestRunner:  at org.junit.runners.ParentRunner.run(ParentRunner.java:413)
07-19 09:21:08.786719 19201 19223 E TestRunner:  at org.junit.runners.Suite.runChild(Suite.java:128)
07-19 09:21:08.786719 19201 19223 E TestRunner:  at org.junit.runners.Suite.runChild(Suite.java:27)
07-19 09:21:08.786719 19201 19223 E TestRunner:  at org.junit.runners.ParentRunner$4.run(ParentRunner.java:331)
07-19 09:21:08.786719 19201 19223 E TestRunner:  at org.junit.runners.ParentRunner$1.schedule(ParentRunner.java:79)
07-19 09:21:08.786719 19201 19223 E TestRunner:  at org.junit.runners.ParentRunner.runChildren(ParentRunner.java:329)
07-19 09:21:08.786719 19201 19223 E TestRunner:  at org.junit.runners.ParentRunner.access$100(ParentRunner.java:66)
07-19 09:21:08.786719 19201 19223 E TestRunner:  at org.junit.runners.ParentRunner$2.evaluate(ParentRunner.java:293)
07-19 09:21:08.786719 19201 19223 E TestRunner:  at org.junit.runners.ParentRunner$3.evaluate(ParentRunner.java:306)
07-19 09:21:08.786719 19201 19223 E TestRunner:  at org.junit.runners.ParentRunner.run(ParentRunner.java:413)
07-19 09:21:08.786719 19201 19223 E TestRunner:  at org.junit.runners.Suite.runChild(Suite.java:128)
07-19 09:21:08.786719 19201 19223 E TestRunner:  at org.junit.runners.Suite.runChild(Suite.java:27)
07-19 09:21:08.786719 19201 19223 E TestRunner:  at org.junit.runners.ParentRunner$4.run(ParentRunner.java:331)
07-19 09:21:08.786719 19201 19223 E TestRunner:  at org.junit.runners.ParentRunner$1.schedule(ParentRunner.java:79)
07-19 09:21:08.786719 19201 19223 E TestRunner:  at org.junit.runners.ParentRunner.runChildren(ParentRunner.java:329)
07-19 09:21:08.786719 19201 19223 E TestRunner:  at org.junit.runners.ParentRunner.access$100(ParentRunner.java:66)
07-19 09:21:08.786719 19201 19223 E TestRunner:  at org.junit.runners.ParentRunner$2.evaluate(ParentRunner.java:293)
07-19 09:21:08.786719 19201 19223 E TestRunner:  at org.junit.runners.ParentRunner$3.evaluate(ParentRunner.java:306)
07-19 09:21:08.786719 19201 19223 E TestRunner:  at org.junit.runners.ParentRunner.run(ParentRunner.java:413)
07-19 09:21:08.786719 19201 19223 E TestRunner:  at org.junit.runner.JUnitCore.run(JUnitCore.java:137)
07-19 09:21:08.786719 19201 19223 E TestRunner:  at org.junit.runner.JUnitCore.run(JUnitCore.java:115)
07-19 09:21:08.786719 19201 19223 E TestRunner:  at androidx.test.internal.runner.TestExecutor.execute(TestExecutor.java:56)
07-19 09:21:08.786719 19201 19223 E TestRunner:  at androidx.test.runner.AndroidJUnitRunner.onStart(AndroidJUnitRunner.java:442)
07-19 09:21:08.786719 19201 19223 E TestRunner:  at android.app.Instrumentation$InstrumentationThread.run(Instrumentation.java:2248)
07-19 09:21:08.786945 19201 19223 E TestRunner: ----- end exception -----
07-19 09:21:08.797995 19201 19223 E TestRunner: failed: testRecordingFramerateLowToHigh[1](android.hardware.camera2.cts.RecordingTest)
07-19 09:21:08.798383 19201 19223 E TestRunner: ----- begin exception -----
07-19 09:21:08.800764 19201 19223 E TestRunner: java.lang.IllegalArgumentException: getCameraCharacteristics:754: Unable to retrieve camera characteristics for unknown device 0: No such file or directory (-2)
07-19 09:21:08.800764 19201 19223 E TestRunner:  at android.hardware.camera2.CameraManager.throwAsPublicException(CameraManager.java:1171)
07-19 09:21:08.800764 19201 19223 E TestRunner:  at android.hardware.camera2.CameraManager.getCameraCharacteristics(CameraManager.java:500)
07-19 09:21:08.800764 19201 19223 E TestRunner:  at android.hardware.camera2.cts.CameraTestUtils.isSystemCamera(CameraTestUtils.java:1136)
07-19 09:21:08.800764 19201 19223 E TestRunner:  at android.hardware.camera2.cts.CameraTestUtils.getCameraIdListForTesting(CameraTestUtils.java:1147)
07-19 09:21:08.800764 19201 19223 E TestRunner:  at android.hardware.camera2.cts.Camera2ParameterizedTestCase.deriveCameraIdsUnderTest(Camera2ParameterizedTestCase.java:83)
07-19 09:21:08.800764 19201 19223 E TestRunner:  at android.hardware.camera2.cts.Camera2ParameterizedTestCase.tearDown(Camera2ParameterizedTestCase.java:69)
07-19 09:21:08.800764 19201 19223 E TestRunner:  at android.hardware.camera2.cts.testcases.Camera2SurfaceViewTestCase.tearDown(Camera2SurfaceViewTestCase.java:178)
07-19 09:21:08.800764 19201 19223 E TestRunner:  at android.hardware.camera2.cts.RecordingTest.tearDown(RecordingTest.java:129)
07-19 09:21:08.800764 19201 19223 E TestRunner:  at java.lang.reflect.Method.invoke(Native Method)
07-19 09:21:08.800764 19201 19223 E TestRunner:  at org.junit.runners.model.FrameworkMethod$1.runReflectiveCall(FrameworkMethod.java:59)
07-19 09:21:08.800764 19201 19223 E TestRunner:  at org.junit.internal.runners.model.ReflectiveCallable.run(ReflectiveCallable.java:12)
07-19 09:21:08.800764 19201 19223 E TestRunner:  at org.junit.runners.model.FrameworkMethod.invokeExplosively(FrameworkMethod.java:61)
07-19 09:21:08.800764 19201 19223 E TestRunner:  at org.junit.internal.runners.statements.RunAfters.invokeMethod(RunAfters.java:46)
07-19 09:21:08.800764 19201 19223 E TestRunner:  at org.junit.internal.runners.statements.RunAfters.evaluate(RunAfters.java:33)
07-19 09:21:08.800764 19201 19223 E TestRunner:  at androidx.test.rule.ActivityTestRule$ActivityStatement.evaluate(ActivityTestRule.java:549)
07-19 09:21:08.800764 19201 19223 E TestRunner:  at org.junit.runners.ParentRunner$3.evaluate(ParentRunner.java:306)
07-19 09:21:08.800764 19201 19223 E TestRunner:  at org.junit.runners.BlockJUnit4ClassRunner$1.evaluate(BlockJUnit4ClassRunner.java:100)
07-19 09:21:08.800764 19201 19223 E TestRunner:  at org.junit.runners.ParentRunner.runLeaf(ParentRunner.java:366)
07-19 09:21:08.800764 19201 19223 E TestRunner:  at org.junit.runners.BlockJUnit4ClassRunner.runChild(BlockJUnit4ClassRunner.java:103)
07-19 09:21:08.800764 19201 19223 E TestRunner:  at org.junit.runners.BlockJUnit4ClassRunner.runChild(BlockJUnit4ClassRunner.java:63)
07-19 09:21:08.800764 19201 19223 E TestRunner:  at org.junit.runners.ParentRunner$4.run(ParentRunner.java:331)
07-19 09:21:08.800764 19201 19223 E TestRunner:  at org.junit.runners.ParentRunner$1.schedule(ParentRunner.java:79)
07-19 09:21:08.800764 19201 19223 E TestRunner:  at org.junit.runners.ParentRunner.runChildren(ParentRunner.java:329)
07-19 09:21:08.800764 19201 19223 E TestRunner:  at org.junit.runners.ParentRunner.access$100(ParentRunner.java:66)
07-19 09:21:08.800764 19201 19223 E TestRunner:  at org.junit.runners.ParentRunner$2.evaluate(ParentRunner.java:293)
07-19 09:21:08.800764 19201 19223 E TestRunner:  at org.junit.runners.ParentRunner.run(ParentRunner.java:413)
07-19 09:21:08.800764 19201 19223 E TestRunner:  at org.junit.runners.Suite.runChild(Suite.java:128)
07-19 09:21:08.800764 19201 19223 E TestRunner:  at org.junit.runners.Suite.runChild(Suite.java:27)
07-19 09:21:08.800764 19201 19223 E TestRunner:  at org.junit.runners.ParentRunner$4.run(ParentRunner.java:331)
07-19 09:21:08.800764 19201 19223 E TestRunner:  at org.junit.runners.ParentRunner$1.schedule(ParentRunner.java:79)
07-19 09:21:08.800764 19201 19223 E TestRunner:  at org.junit.runners.ParentRunner.runChildren(ParentRunner.java:329)
07-19 09:21:08.800764 19201 19223 E TestRunner:  at org.junit.runners.ParentRunner.access$100(ParentRunner.java:66)
07-19 09:21:08.800764 19201 19223 E TestRunner:  at org.junit.runners.ParentRunner$2.evaluate(ParentRunner.java:293)
07-19 09:21:08.800764 19201 19223 E TestRunner:  at org.junit.runners.ParentRunner$3.evaluate(ParentRunner.java:306)
07-19 09:21:08.800764 19201 19223 E TestRunner:  at org.junit.runners.ParentRunner.run(ParentRunner.java:413)
07-19 09:21:08.800764 19201 19223 E TestRunner:  at org.junit.runners.Suite.runChild(Suite.java:128)
07-19 09:21:08.800764 19201 19223 E TestRunner:  at org.junit.runners.Suite.runChild(Suite.java:27)
07-19 09:21:08.800764 19201 19223 E TestRunner:  at org.junit.runners.ParentRunner$4.run(ParentRunner.java:331)
07-19 09:21:08.800764 19201 19223 E TestRunner:  at org.junit.runners.ParentRunner$1.schedule(ParentRunner.java:79)
07-19 09:21:08.800764 19201 19223 E TestRunner:  at org.junit.runners.ParentRunner.runChildren(ParentRunner.java:329)
07-19 09:21:08.800764 19201 19223 E TestRunner:  at org.junit.runners.ParentRunner.access$100(ParentRunner.java:66)
07-19 09:21:08.800764 19201 19223 E TestRunner:  at org.junit.runners.ParentRunner$2.evaluate(ParentRunner.java:293)
07-19 09:21:08.800764 19201 19223 E TestRunner:  at org.junit.runners.ParentRunner$3.evaluate(ParentRunner.java:306)
07-19 09:21:08.800764 19201 19223 E TestRunner:  at org.junit.runners.ParentRunner.run(ParentRunner.java:413)
07-19 09:21:08.800764 19201 19223 E TestRunner:  at org.junit.runner.JUnitCore.run(JUnitCore.java:137)
07-19 09:21:08.800764 19201 19223 E TestRunner:  at org.junit.runner.JUnitCore.run(JUnitCore.java:115)
07-19 09:21:08.800764 19201 19223 E TestRunner:  at androidx.test.internal.runner.TestExecutor.execute(TestExecutor.java:56)
07-19 09:21:08.800764 19201 19223 E TestRunner:  at androidx.test.runner.AndroidJUnitRunner.onStart(AndroidJUnitRunner.java:442)
07-19 09:21:08.800764 19201 19223 E TestRunner:  at android.app.Instrumentation$InstrumentationThread.run(Instrumentation.java:2248)
07-19 09:21:08.800764 19201 19223 E TestRunner: Caused by: android.os.ServiceSpecificException: getCameraCharacteristics:754: Unable to retrieve camera characteristics for unknown device 0: No such file or directory (-2) (code 3)
07-19 09:21:08.802861 19201 19223 E TestRunner:  at android.os.Parcel.createExceptionOrNull(Parcel.java:2469)
07-19 09:21:08.802861 19201 19223 E TestRunner:  at android.os.Parcel.createException(Parcel.java:2439)
07-19 09:21:08.802861 19201 19223 E TestRunner:  at android.os.Parcel.readException(Parcel.java:2422)
07-19 09:21:08.802861 19201 19223 E TestRunner:  at android.os.Parcel.readException(Parcel.java:2364)
07-19 09:21:08.802861 19201 19223 E TestRunner:  at android.hardware.ICameraService$Stub$Proxy.getCameraCharacteristics(ICameraService.java:812)
07-19 09:21:08.802861 19201 19223 E TestRunner:  at android.hardware.camera2.CameraManager.getCameraCharacteristics(CameraManager.java:479)
07-19 09:21:08.802861 19201 19223 E TestRunner:  ... 47 more
07-19 09:21:08.803002 19201 19223 E TestRunner: ----- end exception -----
07-19 09:21:08.810063 19201 19223 I TestRunner: finished: testRecordingFramerateLowToHigh[1](android.hardware.camera2.cts.RecordingTest)



07-19 09:20:57.357929 19364 19364 F DEBUG   : *** *** *** *** *** *** *** *** *** *** *** *** *** *** *** ***
07-19 09:20:57.358143 19364 19364 F DEBUG   : Build fingerprint: 'MobiWire/Vodafone_Smart/Vodafone_Smart:12/SP1A.210812.016/1658150854:user/release-keys'
07-19 09:20:57.358261 19364 19364 F DEBUG   : Revision: '0'
07-19 09:20:57.358975 19364 19364 F DEBUG   : ABI: 'arm'
07-19 09:20:57.359505 19364 19364 F DEBUG   : Timestamp: 2022-07-19 09:20:56.601669128+0800
07-19 09:20:57.359714 19364 19364 F DEBUG   : Process uptime: 0s
07-19 09:20:57.359896 19364 19364 F DEBUG   : Cmdline: /vendor/bin/hw/camerahalserver
07-19 09:20:57.360712 19364 19364 F DEBUG   : pid: 19263, tid: 19337, name: fpipe.g_p2a  >>> /vendor/bin/hw/camerahalserver <<<
07-19 09:20:57.361701 19364 19364 F DEBUG   : uid: 1047
07-19 09:20:57.361839 19364 19364 F DEBUG   : signal 6 (SIGABRT), code -1 (SI_QUEUE), fault addr --------
07-19 09:20:57.362127 19364 19364 F DEBUG   : Abort message: 'Frame 1 enque result failed (onDIPStreamBaseCB){#918:vendor/mediatek/proprietary/hardware/mtkcam3/feature/core/featurePipe/streaming/G_P2ANode.cpp}'
07-19 09:20:57.362268 19364 19364 F DEBUG   :     r0  00000000  r1  00004b89  r2  00000006  r3  9f01ff18
07-19 09:20:57.362369 19364 19364 F DEBUG   :     r4  9f01ff2c  r5  9f01ff10  r6  00004b3f  r7  0000016b
07-19 09:20:57.363197 19364 19364 F DEBUG   :     r8  9f01ff18  r9  9f01ff28  r10 9f01ff48  r11 9f01ff38
07-19 09:20:57.363578 19364 19364 F DEBUG   :     ip  00004b89  sp  9f01fee8  lr  aea28eed  pc  aea28f00
07-19 09:20:57.363883 19364 19364 F DEBUG   : backtrace:
07-19 09:20:57.364281 19364 19364 F DEBUG   :       #00 pc 00060f00  /apex/com.android.runtime/lib/bionic/libc.so (abort+172) (BuildId: 81f342cc28e8dec13a864c00d9b344fa)
07-19 09:20:57.365451 19364 19364 F DEBUG   :       #01 pc 000048af  /system/lib/liblog.so (__android_log_default_aborter+6) (BuildId: 30d9bf85b7c0e2541780d162581a21cc)
07-19 09:20:57.365538 19364 19364 F DEBUG   :       #02 pc 00004f77  /system/lib/liblog.so (__android_log_assert+158) (BuildId: 30d9bf85b7c0e2541780d162581a21cc)
07-19 09:20:57.365583 19364 19364 F DEBUG   :       #03 pc 000f047f  /vendor/lib/libmtkcam.featurepipe.streaming.so (NSCam::NSCamFeature::NSFeaturePipe::G::P2ANode::onDIPStreamBaseCB(NSCam::Feature::P2Util::DIPParams const&, NSCam::NSCamFeature::NSFeaturePipe::G::P2AEnqueData const&)+738) (BuildId: 2f16a1106c7783e814ae8b670428e497)
07-19 09:20:57.365638 19364 19364 F DEBUG   :       #04 pc 000f6963  /vendor/lib/libmtkcam.featurepipe.streaming.so (NSCam::NSCamFeature::NSFeaturePipe::CookieStore<NSCam::NSCamFeature::NSFeaturePipe::DIPStreamBase<NSCam::NSCamFeature::NSFeaturePipe::G::P2AEnqueData> >::staticProcessCB(NSCam::NSCamFeature::NSFeaturePipe::DIPStreamBase<NSCam::NSCamFeature::NSFeaturePipe::G::P2AEnqueData>::T_Msg const&, NSCam::Feature::P2Util::DIPParams, void*, bool)+174) (BuildId: 2f16a1106c7783e814ae8b670428e497)
07-19 09:20:57.365731 19364 19364 F DEBUG   :       #05 pc 000f6859  /vendor/lib/libmtkcam.featurepipe.streaming.so (NSCam::NSCamFeature::NSFeaturePipe::CookieStore<NSCam::NSCamFeature::NSFeaturePipe::DIPStreamBase<NSCam::NSCamFeature::NSFeaturePipe::G::P2AEnqueData> >::enque(NSCam::NSCamFeature::NSFeaturePipe::DIPStreamBase<NSCam::NSCamFeature::NSFeaturePipe::G::P2AEnqueData>*, NSCam::Feature::P2Util::DIPStream*, NSCam::Feature::P2Util::DIPParams, NSCam::NSCamFeature::NSFeaturePipe::G::P2AEnqueData const&)+400) (BuildId: 2f16a1106c7783e814ae8b670428e497)
07-19 09:20:57.365795 19364 19364 F DEBUG   :       #06 pc 000f1009  /vendor/lib/libmtkcam.featurepipe.streaming.so (NSCam::NSCamFeature::NSFeaturePipe::DIPStreamBase<NSCam::NSCamFeature::NSFeaturePipe::G::P2AEnqueData>::enqueDIPStreamBase(NSCam::Feature::P2Util::DIPStream*, NSCam::Feature::P2Util::DIPParams const&, NSCam::NSCamFeature::NSFeaturePipe::G::P2AEnqueData const&)+100) (BuildId: 2f16a1106c7783e814ae8b670428e497)
07-19 09:20:57.365925 19364 19364 F DEBUG   :       #07 pc 000ef68f  /vendor/lib/libmtkcam.featurepipe.streaming.so (NSCam::NSCamFeature::NSFeaturePipe::G::P2ANode::enqueFeatureStream(NSCam::Feature::P2Util::DIPParams&, NSCam::NSCamFeature::NSFeaturePipe::G::P2AEnqueData&)+338) (BuildId: 2f16a1106c7783e814ae8b670428e497)
07-19 09:20:57.366499 19364 19364 F DEBUG   :       #08 pc 000ee01f  /vendor/lib/libmtkcam.featurepipe.streaming.so (NSCam::NSCamFeature::NSFeaturePipe::G::P2ANode::runP2HW(android::sp<NSCam::NSCamFeature::NSFeaturePipe::StreamingFeatureRequest> const&, NSCam::NSCamFeature::NSFeaturePipe::G::P2AEnqueData&, std::__1::vector<NSCam::NSCamFeature::NSFeaturePipe::P2G::P2HW, std::__1::allocator<NSCam::NSCamFeature::NSFeaturePipe::P2G::P2HW> > const&, std::__1::vector<NSCam::NSCamFeature::NSFeaturePipe::P2G::PMDP, std::__1::allocator<NSCam::NSCamFeature::NSFeaturePipe::P2G::PMDP> > const&)+330) (BuildId: 2f16a1106c7783e814ae8b670428e497)
07-19 09:20:57.366619 19364 19364 F DEBUG   :       #09 pc 000ebbf5  /vendor/lib/libmtkcam.featurepipe.streaming.so (NSCam::NSCamFeature::NSFeaturePipe::G::P2ANode::processP2A(android::sp<NSCam::NSCamFeature::NSFeaturePipe::StreamingFeatureRequest> const&, NSCam::NSCamFeature::NSFeaturePipe::RSCResult const&)+644) (BuildId: 2f16a1106c7783e814ae8b670428e497)
07-19 09:20:57.366710 19364 19364 F DEBUG   :       #10 pc 000eb7b5  /vendor/lib/libmtkcam.featurepipe.streaming.so (NSCam::NSCamFeature::NSFeaturePipe::G::P2ANode::onThreadLoop()+736) (BuildId: 2f16a1106c7783e814ae8b670428e497)
07-19 09:20:57.366773 19364 19364 F DEBUG   :       #11 pc 0016144f  /vendor/lib/libmtkcam.featurepipe.streaming.so (NSCam::NSCamFeature::NSFeaturePipe::CamThread::CamThreadHandle::threadLoop()+90) (BuildId: 2f16a1106c7783e814ae8b670428e497)
07-19 09:20:57.366812 19364 19364 F DEBUG   :       #12 pc 0000d327  /apex/com.android.vndk.v31/lib/libutils.so (android::Thread::_threadLoop(void*)+166) (BuildId: cbd5810b7c9a5e6a4235f5e9707c0ba2)
07-19 09:20:57.366851 19364 19364 F DEBUG   :       #13 pc 0000ce67  /apex/com.android.vndk.v31/lib/libutils.so (thread_data_t::trampoline(thread_data_t const*)+254) (BuildId: cbd5810b7c9a5e6a4235f5e9707c0ba2)
07-19 09:20:57.366887 19364 19364 F DEBUG   :       #14 pc 000a8b97  /apex/com.android.runtime/lib/bionic/libc.so (__pthread_start(void*)+40) (BuildId: 81f342cc28e8dec13a864c00d9b344fa)
07-19 09:20:57.366923 19364 19364 F DEBUG   :       #15 pc 00061e45  /apex/com.android.runtime/lib/bionic/libc.so (__start_thread+30) (BuildId: 81f342cc28e8dec13a864c00d9b344fa)



07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession: Session 0: Exception while stopping repeating: 
07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession: android.hardware.camera2.CameraAccessException: CAMERA_ERROR (3): The camera device has encountered a serious error
07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession:  at android.hardware.camera2.impl.CameraDeviceImpl.checkIfCameraClosedOrInError(CameraDeviceImpl.java:2350)
07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession:  at android.hardware.camera2.impl.CameraDeviceImpl.stopRepeating(CameraDeviceImpl.java:1277)
07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession:  at android.hardware.camera2.impl.CameraCaptureSessionImpl.close(CameraCaptureSessionImpl.java:579)
07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession:  at android.hardware.camera2.cts.RecordingTest.stopCameraStreaming(RecordingTest.java:2030)
07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession:  at android.hardware.camera2.cts.RecordingTest.stopRecording(RecordingTest.java:2045)
07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession:  at android.hardware.camera2.cts.RecordingTest.completeBasicRecording(RecordingTest.java:1282)
07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession:  at android.hardware.camera2.cts.RecordingTest.doBasicRecordingByProfile(RecordingTest.java:1233)
07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession:  at android.hardware.camera2.cts.RecordingTest.basicRecordingTestByCamera(RecordingTest.java:1199)
07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession:  at android.hardware.camera2.cts.RecordingTest.basicRecordingTestByCamera(RecordingTest.java:1128)
07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession:  at android.hardware.camera2.cts.RecordingTest.basicRecordingTestByCamera(RecordingTest.java:1123)
07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession:  at android.hardware.camera2.cts.RecordingTest.testRecordingFramerateLowToHigh(RecordingTest.java:556)
07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession:  at java.lang.reflect.Method.invoke(Native Method)
07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession:  at org.junit.runners.model.FrameworkMethod$1.runReflectiveCall(FrameworkMethod.java:59)
07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession:  at org.junit.internal.runners.model.ReflectiveCallable.run(ReflectiveCallable.java:12)
07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession:  at org.junit.runners.model.FrameworkMethod.invokeExplosively(FrameworkMethod.java:61)
07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession:  at org.junit.internal.runners.statements.InvokeMethod.evaluate(InvokeMethod.java:17)
07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession:  at org.junit.internal.runners.statements.RunBefores.evaluate(RunBefores.java:26)
07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession:  at org.junit.internal.runners.statements.RunAfters.evaluate(RunAfters.java:27)
07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession:  at androidx.test.rule.ActivityTestRule$ActivityStatement.evaluate(ActivityTestRule.java:549)
07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession:  at org.junit.runners.ParentRunner$3.evaluate(ParentRunner.java:306)
07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession:  at org.junit.runners.BlockJUnit4ClassRunner$1.evaluate(BlockJUnit4ClassRunner.java:100)
07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession:  at org.junit.runners.ParentRunner.runLeaf(ParentRunner.java:366)
07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession:  at org.junit.runners.BlockJUnit4ClassRunner.runChild(BlockJUnit4ClassRunner.java:103)
07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession:  at org.junit.runners.BlockJUnit4ClassRunner.runChild(BlockJUnit4ClassRunner.java:63)
07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession:  at org.junit.runners.ParentRunner$4.run(ParentRunner.java:331)
07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession:  at org.junit.runners.ParentRunner$1.schedule(ParentRunner.java:79)
07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession:  at org.junit.runners.ParentRunner.runChildren(ParentRunner.java:329)
07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession:  at org.junit.runners.ParentRunner.access$100(ParentRunner.java:66)
07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession:  at org.junit.runners.ParentRunner$2.evaluate(ParentRunner.java:293)
07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession:  at org.junit.runners.ParentRunner.run(ParentRunner.java:413)
07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession:  at org.junit.runners.Suite.runChild(Suite.java:128)
07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession:  at org.junit.runners.Suite.runChild(Suite.java:27)
07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession:  at org.junit.runners.ParentRunner$4.run(ParentRunner.java:331)
07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession:  at org.junit.runners.ParentRunner$1.schedule(ParentRunner.java:79)
07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession:  at org.junit.runners.ParentRunner.runChildren(ParentRunner.java:329)
07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession:  at org.junit.runners.ParentRunner.access$100(ParentRunner.java:66)
07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession:  at org.junit.runners.ParentRunner$2.evaluate(ParentRunner.java:293)
07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession:  at org.junit.runners.ParentRunner$3.evaluate(ParentRunner.java:306)
07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession:  at org.junit.runners.ParentRunner.run(ParentRunner.java:413)
07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession:  at org.junit.runners.Suite.runChild(Suite.java:128)
07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession:  at org.junit.runners.Suite.runChild(Suite.java:27)
07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession:  at org.junit.runners.ParentRunner$4.run(ParentRunner.java:331)
07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession:  at org.junit.runners.ParentRunner$1.schedule(ParentRunner.java:79)
07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession:  at org.junit.runners.ParentRunner.runChildren(ParentRunner.java:329)
07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession:  at org.junit.runners.ParentRunner.access$100(ParentRunner.java:66)
07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession:  at org.junit.runners.ParentRunner$2.evaluate(ParentRunner.java:293)
07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession:  at org.junit.runners.ParentRunner$3.evaluate(ParentRunner.java:306)
07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession:  at org.junit.runners.ParentRunner.run(ParentRunner.java:413)
07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession:  at org.junit.runner.JUnitCore.run(JUnitCore.java:137)
07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession:  at org.junit.runner.JUnitCore.run(JUnitCore.java:115)
07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession:  at androidx.test.internal.runner.TestExecutor.execute(TestExecutor.java:56)
07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession:  at androidx.test.runner.AndroidJUnitRunner.onStart(AndroidJUnitRunner.java:442)
07-20 17:00:37.295 10133  2834  2857 E CameraCaptureSession:  at android.app.Instrumentation$InstrumentationThread.run(Instrumentation.java:2248)


private void stopCameraStreaming() throws Exception {
    if (VERBOSE) {
        Log.v(TAG, "Stopping camera streaming and waiting for idle");
    }
    // Stop repeating, wait for captures to complete, and disconnect from
    // surfaces
    mSession.close();
    mSessionListener.getStateWaiter().waitForState(SESSION_CLOSED, SESSION_CLOSE_TIMEOUT_MS);       // SESSION_CLOSE_TIMEOUT_MS = 3000; 最终在这里会超时
}


07-20 17:00:35.628  1047  2960  2964 D MtkCam/Util/LogicalDevice: (2964)[querySensorStaticInfo] queryDriverName2 index : 1
07-20 17:00:35.628  1047  2960  2964 D MtkCam/Util/LogicalDevice: (2964)[queryDriverName] queryDriverName index : 0
07-20 17:00:35.628  1047  2960  2964 D MtkCam/Util/LogicalDevice: (2964)[queryDriverName] queryDriverName : SENSOR_DRVNAME_S5K4H7_MIPI_RAW
07-20 17:00:35.628  1047  2960  2964 D MtkCam/TemplateRequest: constructRequestMetadata(239):constructRequestMetadata
07-20 17:00:35.629  1047  2960  2960 I mtkcam-camprovider: [initialize] -
07-20 17:00:35.629  1047  2960  2960 I mtkcam-camprovider: [createICameraProvider_V2_6] - internal/0 provider:0xab268400 manager:0xa7f377c0
07-20 17:00:35.632  1047 15477  1444 W CameraProviderManager: addProviderLocked: Camera provider HAL with name 'internal/0' already registered
07-20 17:00:35.631  1047  2960  2964 W MtkCam/TemplateRequest: impConstructRequestMetadata_by_SymbolName(95):constructCustRequestMetadata_COMMON_SENSOR_DRVNAME_S5K4H7_MIPI_RAW not found
07-20 17:00:35.632  1047 15477  1444 W CameraProviderManager: addProviderLocked: The new provider instance will get initialized immediately after the currently present instance is removed!
07-20 17:00:35.632  1047 15477  1444 E VendorTagDescriptor: addVendorDescriptor: Vendor descriptor with same id already present!
07-20 17:00:35.632  1047 15477  1444 E VendorTagDescriptor: addVendorDescriptor: Vendor descriptor with same id already present!
07-20 17:00:35.632  1047 15477  1444 E VendorTagDescriptor: addVendorDescriptor: Vendor descriptor with same id already present!
07-20 17:00:35.632  1047 15477  1444 E VendorTagDescriptor: addVendorDescriptor: Vendor descriptor with same id already present!
07-20 17:00:35.632  1047 15477  1444 E VendorTagDescriptor: addVendorDescriptor: Vendor descriptor with same id already present!
07-20 17:00:35.632  1047 15477  1444 E VendorTagDescriptor: addVendorDescriptor: Vendor descriptor with same id already present!
07-20 17:00:35.632  1047 15477  1444 E VendorTagDescriptor: addVendorDescriptor: Vendor descriptor with same id already present!
07-20 17:00:35.632  1047 15477  1444 E VendorTagDescriptor: addVendorDescriptor: Vendor descriptor with same id already present!
07-20 17:00:35.633  1047  2960  2964 W MtkCam/TemplateRequest: impConstructRequestMetadata_by_SymbolName(95):constructCustRequestMetadata_DEVICE_DEFAULT not found
07-20 17:00:35.633  1047  2960  2960 I HidlServiceManagement: Registered android.hardware.camera.provider@2.6::ICameraProvider/internal/0
07-20 17:00:35.633  1047  2960  2964 W MtkCam/TemplateRequest: impConstructRequestMetadata_by_SymbolName(95):constructCustRequestMetadata_PROJECT_SENSOR_DRVNAME_S5K4H7_MIPI_RAW not found
07-20 17:00:35.633  1047  2960  2964 D MtkCam/TemplateRequest: impConstructRequestMetadata(155):TemplateRequest: load status(0x9)
07-20 17:00:35.633  1047  2960  2964 D MtkCam/TemplateRequest: constructRequestMetadata(250):Allocating 62 entries from customization
07-20 17:00:35.634  1000   345   345 I hwservicemanager: getTransport: Cannot find entry vendor.mediatek.hardware.camera.atms@1.0::IATMs/default in either framework or device VINTF manifest.
07-20 17:00:35.636  1047  2960  2960 E LegacySupport: Could not get passthrough implementation for vendor.mediatek.hardware.camera.atms@1.0::IATMs/default.
07-20 17:00:35.636  1047  2960  2960 W camerahalserver: main: register IATMs err:1(Unknown error -1)
07-20 17:00:35.637  1047  2960  2964 D MtkCam/TemplateRequest: updateData(350):user defines default value
07-20 17:00:35.637  1047  2960  2964 D Metadata2/Convert2A: convert(127):convert: Tag 0xd0015 not found in Android Metadata Set



07-19 09:20:54.388785 17453 17453 W ServiceManager: Permission failure: android.permission.CAMERA_OPEN_CLOSE_LISTENER from uid=10139 pid=19201
07-19 09:20:54.391945 17453 17467 W ServiceManager: Permission failure: android.permission.CAMERA_OPEN_CLOSE_LISTENER from uid=10139 pid=19201



07-19 09:20:54.455944 17453 17467 I CameraService: CameraService::connect call (PID -1 "android.camera.cts", camera ID 0) and Camera API version 2
07-19 09:20:54.458131 17453 17467 I Camera2ClientBase: Camera 0: Opened. Client: android.camera.cts (PID 19201, UID 10139)
07-19 09:20:54.458246 17453 17467 I CameraDeviceClient: CameraDeviceClient 0: Opened
07-19 09:20:54.462109 17453 17467 I CameraService: onTorchStatusChangedLocked: Torch status changed for cameraId=0, newStatus=0
07-19 09:20:54.462544 17453 17467 I CameraProviderManager: Camera HAL provider needs restart, calling getService(internal/0)
07-19 09:20:54.463726 19241 19241 D NetworkSecurityConfig: Using Network Security Config from resource network_security_config debugBuild: false
07-19 09:20:54.464809   341   341 I hwservicemanager: Since android.hardware.camera.provider@2.4::ICameraProvider/internal/0 is not registered, trying to start it as a lazy HAL.
07-19 09:20:54.467267   341   341 I hwservicemanager: Since android.hardware.camera.provider@2.4::ICameraProvider/internal/0 is not registered, trying to start it as a lazy HAL.
07-19 09:20:54.467977 17453 17467 I HidlServiceManagement: getService: Trying again for android.hardware.camera.provider@2.4::ICameraProvider/internal/0...
07-19 09:20:54.468042 19241 19241 D NetworkSecurityConfig: Using Network Security Config from resource network_security_config debugBuild: false
07-19 09:20:54.586478   726   830 D AAL     : 07-19 09:20:54.437 BL= 380,ESS= 256, 07-19 09:20:54.470 BL= 381,ESS= 256, 07-19 09:20:54.503 BL= 382,ESS= 256, 07-19 09:20:54.536 BL= 383,ESS= 256, 07-19 09:20:54.586 BL= 382,ESS= 256, 
07-19 09:20:54.608853 19263 19263 D mtkcam-debug: [initializeDebugProcessNames]  "/system/bin/cameraserver" "/vendor/bin/hw/camerahalserver" "com.android.camera2" "com.mediatek.camera"
07-19 09:20:54.620561 19263 19263 I camerahalserver: Camera Lazy HAL Server is starting...


07-19 09:21:02.156864 17453 17467 E camera_metadata: validate_camera_metadata_structure: metadata is null!
07-19 09:21:02.157032 17453 17467 E Camera2-Metadata: acquire: Failed to validate metadata structure 0x0
07-19 09:21:02.172696 17453 17467 E Camera3-Device: flush: Transaction error: Status(EX_TRANSACTION_FAILED): 'DEAD_OBJECT: '
07-19 09:21:02.172829 17453 17467 E CameraDeviceClient: detachDevice: flush failed with code 0xffffffe0

07-19 09:21:04.381044 17453 19291 E Camera3-Stream: getBuffer: wait for output buffer return timed out after 8000ms (max_buffers 7)

07-19 09:21:07.173486 17453 17467 E Camera3-Device: Camera 0: waitUntilDrainedLocked: Error waiting for HAL to drain: Connection timed out (-110)
07-19 09:21:07.249003   704   704 I thermal_repeater: [recvMdThermalInfo] ret=30, strLen=127,  3, 42, -127, -28362, 32767, 0
07-19 09:21:07.639744 17453 17467 D CameraTraces: Process trace saved. Use dumpsys media.camera to view.
07-19 09:21:07.640079 17453 17467 E CameraDeviceClient: detachDevice: waitUntilDrained failed with code 0xffffff92
07-19 09:21:07.640203 17453 17467 I Camera3-Device: disconnectImpl: E
07-19 09:21:07.640304 17453 17467 E Camera3-Device: Camera 0: disconnectImpl: Shutting down in an error state


media.camera
Device status: ERROR
Error cause: sendRequestsBatch: RequestThread: Unable to submit capture request 6 to HAL device: Broken pipe (-32)          // camera hal server 挂掉了？



07-19 00:07:52.803669 14455 14455 E iio/camio: [vendor/mediatek/proprietary/hardware/mtkcam/drv/src/isp/mt6739/imageio/pipe/CamIOPipe/CamIOPipe.cpp, sendCommand, line3207] ERROR: NOT support command! (sendCommand){#3207:vendor/mediatek/proprietary/hardware/mtkcam/drv/src/isp/mt6739/imageio/pipe/CamIOPipe/CamIOPipe.cpp}
07-19 00:07:52.803713 14455 14455 E NormalPipe_FrmB: [vendor/mediatek/proprietary/hardware/mtkcam/drv/src/isp/mt6739/iopipe/CamIO/NormalPipe_FrmB.cpp, sendCommand, line2920] ERROR: error: sendCommand fail: (cmd,arg1,arg2,arg3)=(0x00001500,0xbed31480,0xbed31484,0xad4ad650) (sendCommand){#2920:vendor/mediatek/proprietary/hardware/mtkcam/drv/src/isp/mt6739/iopipe/CamIO/NormalPipe_FrmB.cpp}


07-19 00:07:53.008082   390   390 D AEE_AED : PPM cpu cores:4, online:4
07-19 00:07:53.009279   390   390 D AEE_AED : aed_main_fork_worker: generator 0xac357078, worker 0xbed29b30, recv_fd 12
07-19 00:07:53.010776 14533 14533 I AEE_AED : handle_request(12)
07-19 00:07:53.012736 14533 14533 I AEE_AED : pid: 14455, tid: 14508, >>> /vendor/bin/hw/camerahalserver <<<                // 发生了 AEE
07-19 00:07:53.012820 14533 14533 I AEE_AED : read_request: receive requirement from aee_core_forwar
07-19 00:07:53.013081 14533 14533 D AEE_AED : u:r:mtk_hal_camera:s0
07-19 00:07:53.013202 14533 14533 V AEE_AED : dashboard_record_update() : rec->module = /vendor/bin/hw/camerahalserver 
07-19 00:07:53.013238 14533 14533 D AEE_AED : Duplicated exception, cnt = 2 
07-19 00:07:53.013314 14533 14533 D AEE_AED : Last exception time: 1658158238 
07-19 00:07:53.013404 14533 14533 D AEE_AED : cur time: 1658160473 
07-19 00:07:53.013455 14533 14533 D AEE_AED : Skip for Exp level'0'
07-19 00:07:53.013481 14533 14533 I AEE_AED : aed_ne_core_session: aed_report_filter asked to skip
07-19 00:07:53.013697 14533 14533 E AEE_AED : handle_request: return status is fail
07-19 00:07:53.014381 14532 14532 W libc    : Access denied finding property "persist.vendor.aee.log.status"
07-19 00:07:53.014487 14532 14532 I aee_core_forwarder: process_coredump: skip process NE
07-19 00:07:53.014733 14532 14532 W libc    : Access denied finding property "persist.vendor.aee.log.status"
07-19 00:07:53.014804 14532 14532 I aee_core_forwarder: process_coredump: exit
07-19 00:07:53.015687   390   390 D AEE_AED : clear ppm settings
07-19 00:07:53.016909   390   390 D AEE_AED : $===AEE===AEE===AEE===$
07-19 00:07:53.044239   481   545 I mtkpower@impl: [powerd_req] TIMER_MSG_PERF_LOCK_TIMEOUT hdl:145
07-19 00:07:53.044353   481   545 I libPowerHal: [perfLockRel] hdl:145, idx:1
07-19 00:07:53.063811 11824 11830 I CameraProviderManager: Camera provider 'internal/0-0' has died; removing it
07-19 00:07:53.064092 11824 14472 E Camera3-Device: processBatchCaptureRequests: Transaction error: Status(EX_TRANSACTION_FAILED): 'DEAD_OBJECT: '
07-19 00:07:53.064176 11824 14472 E Camera3-Device: Camera 0: sendRequestsBatch: RequestThread: Unable to submit capture request 5 to HAL device: Broken pipe (-32)
07-19 00:07:53.068459   345   345 I hwservicemanager: Since android.hardware.camera.provider@2.4::ICameraProvider/internal/0 is not registered, trying to start it as a lazy HAL.



In-flight requests:
  Frame 0 |  Timestamp: 184256498000, metadata arrived: false, buffers left: 2
  Frame 1 |  Timestamp: 184290279000, metadata arrived: false, buffers left: 2
  Frame 2 |  Timestamp: 0, metadata arrived: false, buffers left: 2
  Frame 3 |  Timestamp: 0, metadata arrived: false, buffers left: 2
  Frame 4 |  Timestamp: 0, metadata arrived: false, buffers left: 2
  Frame 5 |  Timestamp: 0, metadata arrived: false, buffers left: 2


private static final int[] mCamcorderProfileList = {
        CamcorderProfile.QUALITY_HIGH,
        CamcorderProfile.QUALITY_2160P,
        CamcorderProfile.QUALITY_1080P,
        CamcorderProfile.QUALITY_720P,
        CamcorderProfile.QUALITY_480P,
        CamcorderProfile.QUALITY_CIF,
        CamcorderProfile.QUALITY_QCIF,
        CamcorderProfile.QUALITY_QVGA,
        CamcorderProfile.QUALITY_LOW,
};

public void testRecordingFramerateLowToHigh() throws Exception {
    for (int i = 0; i < mCameraIdsUnderTest.length; i++) {
        try {
            Log.i(TAG, "Testing recording framerate low to high for camera " + mCameraIdsUnderTest[i]);
            StaticMetadata staticInfo = mAllStaticInfo.get(mCameraIdsUnderTest[i]);
            if (!staticInfo.isColorOutputSupported()) {
                Log.i(TAG, "Camera " + mCameraIdsUnderTest[i] + " does not support color outputs, skipping");
                continue;
            }
            if (staticInfo.isExternalCamera()) {
                Log.i(TAG, "Camera " + mCameraIdsUnderTest[i] + " does not support CamcorderProfile, skipping");
                continue;
            }
            mMediaRecorder = new MediaRecorder();
            openDevice(mCameraIdsUnderTest[i]);
            initSupportedVideoSize(mCameraIdsUnderTest[i]);
            int minFpsProfileId = -1, minFps = 1000;
            int maxFpsProfileId = -1, maxFps = 0;
            int cameraId = Integer.valueOf(mCamera.getId());
            for (int profileId : mCamcorderProfileList) {
                if (!CamcorderProfile.hasProfile(cameraId, profileId)) {
                    continue;
                }
                CamcorderProfile profile = CamcorderProfile.get(cameraId, profileId);
                if (profile.videoFrameRate < minFps) {
                    minFpsProfileId = profileId;
                    minFps = profile.videoFrameRate;
                }
                if (profile.videoFrameRate > maxFps) {
                    maxFpsProfileId = profileId;
                    maxFps = profile.videoFrameRate;
                }
            }
            int camcorderProfileList[] = new int[] {minFpsProfileId, maxFpsProfileId};
            basicRecordingTestByCamera(camcorderProfileList, /*useVideoStab*/false);
        } finally {
            closeDevice();
            releaseRecorder();
        }
    }
}



MTK回复
Hi sir，

请贵司修改如下，再帮忙测试抓份log过来。
/vendor/mediatek/proprietary/hardware/mtkcam/aaa/source/isp_30/buf_mgr/AAOBufMgr.cpp

89  #define FILE_NAME_SIZE 64
90  #define P1_HW_BUF_MAX_NUM    6                  //將4改為6
91  #define P1_HW_BUF_MASK         5                       // (P1_HW_BUF_MAX_NUM - 1)    //將3改為5


/vendor/mediatek/proprietary/hardware/mtkcam/aaa/source/isp_30/buf_mgr/StatisticPipeWrapper/mt6739/aao_buf_mgr.cpp

100  #define MAX_AAO_BUFFER_CNT (6)    //將4改為6

感谢


Hi sir，
此项测试跟performance强相关，建议增加光照强度(需要在比较明亮的环境下测试)
测试项可以尝试参考MOL上的解决方案：
http://online.mediatek.inc/FAQ#/SW/FAQ17668 
http://online.mediatek.inc/FAQ#/SW/FAQ19520
http://online.mediatek.inc/FAQ#/SW/FAQ19243
http://online.mediatek.inc/FAQ#/SW/FAQ21242
检查一下sensor sof的帧率(调整帧率后试试)

Thanks
```## 查看曝光参数

```text
孙柯 7-22 10:49:17
看看updateAEInfo2ISP

孙柯 7-22 10:49:21
看看附近的log

孙柯 7-22 10:49:33
state6好像是拍大图 state7是拍缩略图
```## 微距模式拍照闪前闪光灯

```text
从 log 中看到是light的facing不对导致的，咨询轩总之后发现 微距 配置的是sub2

http://192.168.3.78:7080/c/S0_MP1/alps-release-s0.mp1.rc-default/+/106966

vendor/mediatek/proprietary/custom/mt6761/hal/imgsensor_src/cfg_setting_imgsensor.cpp

+    //Redmine149037 ODM modified for Macro mode will flash back light ZQ 2022/07/25:begin
     {
         .sensorIdx     = IMGSENSOR_SENSOR_IDX_SUB2,
         .mclk          = eMclk_3,
         .port          = EMipiPort_CSI0B,
-        .dir           = CUSTOM_CFG_DIR_FRONT,
+        .dir           = CUSTOM_CFG_DIR_REAR,
         .bitOrder      = CUSTOM_CFG_BITORDER_9_2,
         .orientation   = 270,
         .horizontalFov = 75,
         .verticalFov   = 60,
         .PadPclkInv    = 0,
         },
+    //Redmine149037 ODM modified for Macro mode will flash back light ZQ 2022/07/25:end
```## Camera 预览+拍照 黑屏

```text
adb shell dumpsys sensor_privacy
SENSOR PRIVACY MANAGER STATE (dumpsys sensor_privacy)
{
  users={
    user_id=0
    is_enabled=false
  }
}

adb shell dumpsys sensor_privacy
SENSOR PRIVACY MANAGER STATE (dumpsys sensor_privacy)
{
  users={
    user_id=0
    is_enabled=false
    individual_enabled_sensor=[
      {
        sensor=1
        is_enabled=false
      }
      {
        sensor=2
        is_enabled=true
      }
    ]
  }
}


适配说明：开发者可以使用新的 SensorPrivacyManager API 来了解设备对这个开关功能的支持情况。
如需检查设备是否支持麦克风和摄像头切换开关，请添加以下代码段中所示的逻辑：

SensorPrivacyManager sensorPrivacyManager = getApplicationContext()
        .getSystemService(SensorPrivacyManager.class);
boolean supportsMicrophoneToggle = sensorPrivacyManager
        .supportsSensorToggle(Sensors.MICROPHONE);
boolean supportsCameraToggle = sensorPrivacyManager
        .supportsSensorToggle(Sensors.CAMERA);


// 判断是否有Camera的权限
+        SensorPrivacyManager spm = getSystemService(SensorPrivacyManager.class);
+        boolean isCameraBlocked = spm.isSensorPrivacyEnabled(SensorPrivacyManager.Sensors.CAMERA);
```## 双摄校准

```text
public static final CameraCharacteristics.Key<Integer> ANDROID_SPRD_SN_READY = new CameraCharacteristics.Key<Integer>("com.addParameters.sprdSNReady",Integer.class);
```## getCameraIdList

```text
CameraManager.java
public String[] getCameraIdList() {
    String[] cameraIds = null;
    synchronized (mLock) {
        // Try to make sure we have an up-to-date list of camera devices.
        connectCameraServiceLocked();
        cameraIds = extractCameraIdListLocked();
    }
    sortCameraIds(cameraIds);
    return cameraIds;
}

private String[] extractCameraIdListLocked() {
    String[] cameraIds = null;
    int idCount = 0;
    for (int i = 0; i < mDeviceStatus.size(); i++) {
        int status = mDeviceStatus.valueAt(i);
        if (status == ICameraServiceListener.STATUS_NOT_PRESENT
                || status == ICameraServiceListener.STATUS_ENUMERATING) continue;
        idCount++;
    }
    cameraIds = new String[idCount];
    idCount = 0;
    for (int i = 0; i < mDeviceStatus.size(); i++) {
        int status = mDeviceStatus.valueAt(i);
        if (status == ICameraServiceListener.STATUS_NOT_PRESENT
                || status == ICameraServiceListener.STATUS_ENUMERATING) continue;
        cameraIds[idCount] = mDeviceStatus.keyAt(i);
        idCount++;
    }
    return cameraIds;
}

private void onStatusChangedLocked(int status, String id) {
    ...
    if (!validStatus(status)) {
        Log.e(TAG, String.format("Ignoring invalid device %s status 0x%x", id, status));
        return;
    }
    Integer oldStatus;
    if (status == ICameraServiceListener.STATUS_NOT_PRESENT) {
        oldStatus = mDeviceStatus.remove(id);
        mUnavailablePhysicalDevices.remove(id);
    } else {
        oldStatus = mDeviceStatus.put(id, status);      // ++++
        if (oldStatus == null) {
            mUnavailablePhysicalDevices.put(id, new ArrayList<String>());
        }
    }
    ...


SensorPrivacyManager.java --> setSensorPrivacyForProfileGroup()
```## MediaProfile

```text
static bool isCamcorderQualityKnown(int quality)
{
    return ((quality >= CAMCORDER_QUALITY_LIST_START &&             //0
             quality <= CAMCORDER_QUALITY_LIST_END) ||              //12
            (quality >= CAMCORDER_QUALITY_TIME_LAPSE_LIST_START &&  //1000
             quality <= CAMCORDER_QUALITY_TIME_LAPSE_LIST_END) ||   //1012
             (quality >= CAMCORDER_QUALITY_HIGH_SPEED_LIST_START && //2000
              quality <= CAMCORDER_QUALITY_HIGH_SPEED_LIST_END));   //2008
}


/*static*/ MediaProfiles::CamcorderProfile*
MediaProfiles::createCamcorderProfile(
        int cameraId, const char **atts, size_t natts, Vector<int>& cameraIds)
{
    CHECK(natts >= 6 &&
          !strcmp("quality",    atts[0]) &&
          !strcmp("fileFormat", atts[2]) &&
          !strcmp("duration",   atts[4]));

    const size_t nProfileMappings = sizeof(sCamcorderQualityNameMap)/
            sizeof(sCamcorderQualityNameMap[0]);
    const int quality = findTagForName(sCamcorderQualityNameMap, nProfileMappings, atts[1]);
    if (quality == -1) {
      ALOGE("MediaProfiles::createCamcorderProfile failed to locate quality %s", atts[1]);
      return nullptr;
    }

    const size_t nFormatMappings = sizeof(sFileFormatMap)/sizeof(sFileFormatMap[0]);
    const int fileFormat = findTagForName(sFileFormatMap, nFormatMappings, atts[3]);
    if (fileFormat == -1) {
      ALOGE("MediaProfiles::createCamcorderProfile failed to locate file format %s", atts[1]);
      return nullptr;
    }

    MediaProfiles::CamcorderProfile *profile = new MediaProfiles::CamcorderProfile;
    profile->mCameraId = cameraId;
    if (!isCameraIdFound(cameraId, cameraIds)) {
        cameraIds.add(cameraId);
    }
    profile->mFileFormat = static_cast<output_format>(fileFormat);
    profile->mQuality = static_cast<camcorder_quality>(quality);
    profile->mDuration = atoi(atts[5]);
    return profile;
}

const MediaProfiles::NameToTagMap MediaProfiles::sCamcorderQualityNameMap[] = {
    {"low", CAMCORDER_QUALITY_LOW},
    {"high", CAMCORDER_QUALITY_HIGH},
    {"qcif", CAMCORDER_QUALITY_QCIF},
    {"cif", CAMCORDER_QUALITY_CIF},
    {"480p", CAMCORDER_QUALITY_480P},
    {"720p", CAMCORDER_QUALITY_720P},
    {"1080p", CAMCORDER_QUALITY_1080P},
    {"2160p", CAMCORDER_QUALITY_2160P},
    {"qvga", CAMCORDER_QUALITY_QVGA},
    {"vga", CAMCORDER_QUALITY_VGA},
    {"4kdci", CAMCORDER_QUALITY_4KDCI},
    {"qhd", CAMCORDER_QUALITY_QHD},
    {"2k", CAMCORDER_QUALITY_2K},
    {"8kuhd", CAMCORDER_QUALITY_8KUHD},

    {"timelapselow",  CAMCORDER_QUALITY_TIME_LAPSE_LOW},
    {"timelapsehigh", CAMCORDER_QUALITY_TIME_LAPSE_HIGH},
    {"timelapseqcif", CAMCORDER_QUALITY_TIME_LAPSE_QCIF},
    {"timelapsecif", CAMCORDER_QUALITY_TIME_LAPSE_CIF},
    {"timelapse480p", CAMCORDER_QUALITY_TIME_LAPSE_480P},
    {"timelapse720p", CAMCORDER_QUALITY_TIME_LAPSE_720P},
    {"timelapse1080p", CAMCORDER_QUALITY_TIME_LAPSE_1080P},
    {"timelapse2160p", CAMCORDER_QUALITY_TIME_LAPSE_2160P},
    {"timelapseqvga", CAMCORDER_QUALITY_TIME_LAPSE_QVGA},
    {"timelapsevga", CAMCORDER_QUALITY_TIME_LAPSE_VGA},
    {"timelapse4kdci", CAMCORDER_QUALITY_TIME_LAPSE_4KDCI},
    {"timelapseqhd", CAMCORDER_QUALITY_TIME_LAPSE_QHD},
    {"timelapse2k", CAMCORDER_QUALITY_TIME_LAPSE_2K},

    {"highspeedlow",  CAMCORDER_QUALITY_HIGH_SPEED_LOW},        //2000
    {"highspeedhigh", CAMCORDER_QUALITY_HIGH_SPEED_HIGH},       //2001
    {"highspeed480p", CAMCORDER_QUALITY_HIGH_SPEED_480P},       //2002
    {"highspeed720p", CAMCORDER_QUALITY_HIGH_SPEED_720P},       //2003
    {"highspeed1080p", CAMCORDER_QUALITY_HIGH_SPEED_1080P},     //2004
    {"highspeed2160p", CAMCORDER_QUALITY_HIGH_SPEED_2160P},     //2005
    {"highspeedcif", CAMCORDER_QUALITY_HIGH_SPEED_CIF},         //2006
    {"highspeedvga", CAMCORDER_QUALITY_HIGH_SPEED_VGA},         //2007
    {"highspeed4kdci", CAMCORDER_QUALITY_HIGH_SPEED_4KDCI},     //2008

    // Vendor-specific profiles
};
```## 

```text
availableTestPatternModes

MTK_SENSOR_AVAILABLE_TEST_PATTERN_MODES
```## TODO : 怎么判断是RAW Sensor/YUV Sensor?

## 

```text
==== State: Opened by: sagereal on 10 August 2022 10:31:33 ====

hi hu
我们目前使用的sensor是s5kjn1sq03这颗sensor，添加宏控后，仍未正常显示高清功能，附件是log

==== State: NeedInfo by: cmadmin on 10 August 2022 09:58:09 ====

  == Sunny.Hu@unisoc.com On 2022-08-10T01:53:58Z (json) ==
在androidr\device\sprd\xxxx\xxxxx\module\camera\md.mk中添加宏如下：

#camera back high resolution definition mode
PRODUCT_PROPERTY_OVERRIDES += persist.vendor.cam.back.high.resolution.mode=1


还有需要检查是不是4in1 sensor 需要是4in1 的

可用logcat检索 is_4in1_sensor  1为是  0为不是
(2022-08-09T10:48:54Z)

==== State: Opened by: cmadmin on 09 August 2022 18:52:32 ====

Dear Customer:
 The Issue is under processing now.
Thank you
```## PhotoMotion 拍照模式

```text
vendor/sprd/platform/packages/apps/DreamCamera2/src/com/android/camera/PhotoUI.java
isMotionPhotoEnabled = featureList[FeatureTagID.MONTIONENABLE.ordinal()] == 1 ? true : false;


vendor/sprd/platform/packages/apps/DreamCamera2/src/com/android/camera/util/CameraUtil.java
OneCameraManager oneCameraManager = OneCameraModule.provideOneCameraManager();
if (mSprdFeatureCapabilities == null || mSprdFeatureCapabilities.length == 0) {
    mSprdFeatureCapabilities = oneCameraManager.getSprdFeatureCapabilities();
    Log.i(TAG, "get capability from hal mSprdFeatureCapabilities ="+Arrays.toString(mSprdFeatureCapabilities));
    if (mSprdFeatureCapabilities == null || mSprdFeatureCapabilities.length == 0) {
        Log.i(TAG , "get no capability from hal");
        return;
    }
    initializeCapabilitiesFromFeatureList(mSprdFeatureCapabilities);
} else {
    initializeCapabilitiesFromFeatureList(mSprdFeatureCapabilities);
}


vendor/sprd/platform/packages/apps/DreamCamera2/src/com/android/camera/one/v2/Camera2OneCameraManagerImpl.java
    @Override
    public int[] getSprdFeatureCapabilities() throws OneCameraAccessException {
        int cameraId = 0;
        try {
            String[] cameraIds = mCameraManager.getCameraIdList();
            if (cameraIds != null && cameraIds.length >= 1) {
                cameraId = Integer.parseInt(cameraIds[0]);
            }
        } catch (CameraAccessException ex) {
            Log.w(TAG, "Unable to getCameraIdList", ex);
        }
        int[] mSprdFeatureCapabilities = getCameraCharacteristics(cameraId).get(
                SprdCameraCharacteristics.ANDROID_SPRD_FEATURE_LIST);
        if (mSprdFeatureCapabilities == null || mSprdFeatureCapabilities.length == 0) {
            return null;
        }
        return mSprdFeatureCapabilities;
    }

vendor/sprd/platform/packages/apps/DreamCamera2/portability/src/com/android/ex/camera2/portability/SprdCameraCharacteristics.java
    public static final Key<int[]> ANDROID_SPRD_FEATURE_LIST = new Key<int[]>(
            "com.addParameters.sprdCamFeatureList", int[].class);

      com.addParameters.sprdCamFeatureList (80000043): byte[49]
        [2 9 0 3 3 0 0 0 1 1 1 "1" 0 1 0 1 ]
        [3 0 0 0 0 0 0 1 1 1 1 0 1 0 0 1 ]
        [1 1 1 1 0 1 0 1 1 2 0 1 3 3 0 0 ]
        [0 ]


vendor/sprd/modules/libcamera/include/SprdCamera3.h
static tags_info_t
    android_add_parameters[VENDOR_SECTION_END - VENDOR_SECTION_START] = {
        ...
        {"sprdCamFeatureList", TYPE_BYTE},
        ...
};


vendor/sprd/modules/libcamera/hal3_2v6/SprdCamera3Setting.cpp
void SprdCamera3Setting::initCameraIpFeature(int32_t cameraId) {
    ...
    // 11 montion photo enable
    property_get("persist.vendor.cam.raw.mode", value, "jpeg");
    if (!strcmp(value, "raw")) {
        available_cam_features.add(0);
    } else {
#ifdef CONFIG_CAMERA_MOTION_PHONE
        available_cam_features.add(1);
#else
        available_cam_features.add(0);
#endif
    }
    ...
}


vendor/sprd/modules/libcamera/SprdCtrl.mk
ifeq ($(strip $(TARGET_BOARD_CAMERA_MOTION_PHONE)),true)
LOCAL_CFLAGS += -DCONFIG_CAMERA_MOTION_PHONE
endif


SR/pcb/SK659_GH6591_COMMON/alps/device/sprd/qogirl6/ums9230_4h10/module/camera/md.mk
#motionphone
TARGET_BOARD_CAMERA_MOTION_PHONE := true




typedef struct {
    ...
    uint8_t sprd_cam_feature_list[CAMERA_SETTINGS_CONFIG_ARRAYSIZE];        //
    uint8_t sprd_cam_feature_list_size;
    ...
} SPRD_DEF_Tag;



typedef enum sprd_camera_ext_tags {
    /*sprd add flag start*/
    ...
    ANDROID_SPRD_CAM_FEATURE_LIST,                              //
    ...
    /*not parameter but only flag between framework and hal*/
    /*sprd add flag end*/
} sprd_camera_metadata_tag_t;


debug.camera.3dcap.savefile
debug.camera.3dcap.preview
```## 

```text
private void bufferFormatLongProcessingTimeTestByCamera(int format)
        throws Exception {

    final int TEST_SENSITIVITY_VALUE = mStaticInfo.getSensitivityClampToRange(204);
    final long TEST_EXPOSURE_TIME_NS = mStaticInfo.getExposureClampToRange(28000000);
    final long EXPOSURE_TIME_ERROR_MARGIN_NS = 100000;

    Size[] availableSizes = mStaticInfo.getAvailableSizesForFormatChecked(format,
            StaticMetadata.StreamDirection.Output);

    // for each resolution, test imageReader:
    for (Size sz : availableSizes) {
        Log.v(TAG, "testing size " + sz.toString());
        try {
            if (VERBOSE) {
                Log.v(TAG, "Testing long processing time: size " + sz.toString() + " format " +
                        format + " for camera " + mCamera.getId());
            }

            // Create ImageReader.
            mListener  = new SimpleImageListener();
            createDefaultImageReader(sz, format, MAX_NUM_IMAGES, mListener);

            // Setting manual controls
            List<Surface> outputSurfaces = new ArrayList<Surface>();
            outputSurfaces.add(mReader.getSurface());
            CaptureRequest.Builder requestBuilder = prepareCaptureRequestForSurfaces(
                    outputSurfaces, CameraDevice.TEMPLATE_STILL_CAPTURE);

            requestBuilder.set(
                    CaptureRequest.CONTROL_MODE, CaptureRequest.CONTROL_MODE_OFF);
            requestBuilder.set(CaptureRequest.CONTROL_AE_LOCK, true);
            requestBuilder.set(CaptureRequest.CONTROL_AWB_LOCK, true);
            requestBuilder.set(CaptureRequest.CONTROL_AE_MODE,
                    CaptureRequest.CONTROL_AE_MODE_OFF);
            requestBuilder.set(CaptureRequest.CONTROL_AWB_MODE,
                    CaptureRequest.CONTROL_AWB_MODE_OFF);
            requestBuilder.set(CaptureRequest.SENSOR_SENSITIVITY, TEST_SENSITIVITY_VALUE);
            requestBuilder.set(CaptureRequest.SENSOR_EXPOSURE_TIME, TEST_EXPOSURE_TIME_NS);

            SimpleCaptureCallback listener = new SimpleCaptureCallback();
            startCapture(requestBuilder.build(), /*repeating*/true, listener, mHandler);

            for (int i = 0; i < NUM_LONG_PROCESS_TIME_FRAME_VERIFIED; i++) {
                mListener.waitForAnyImageAvailable(CAPTURE_WAIT_TIMEOUT_MS);

                // Verify image.
                Image img = mReader.acquireNextImage();
                assertNotNull("Unable to acquire next image", img);
                CameraTestUtils.validateImage(img, sz.getWidth(), sz.getHeight(), format,
                        mDebugFileNameBase);

                // Verify the exposure time and iso match the requested values.
                CaptureResult result = listener.getCaptureResult(CAPTURE_RESULT_TIMEOUT_MS);

                long exposureTimeDiff = TEST_EXPOSURE_TIME_NS -
                        getValueNotNull(result, CaptureResult.SENSOR_EXPOSURE_TIME);
                int sensitivityDiff = TEST_SENSITIVITY_VALUE -
                        getValueNotNull(result, CaptureResult.SENSOR_SENSITIVITY);

                mCollector.expectTrue(
                        String.format("Long processing frame %d format %d size %s " +
                                "exposure time was %d expecting %d.", i, format, sz.toString(),
                                getValueNotNull(result, CaptureResult.SENSOR_EXPOSURE_TIME),
                                TEST_EXPOSURE_TIME_NS),
                        exposureTimeDiff < EXPOSURE_TIME_ERROR_MARGIN_NS &&
                        exposureTimeDiff >= 0);

                mCollector.expectTrue(
                        String.format("Long processing frame %d format %d size %s " +
                                "sensitivity was %d expecting %d.", i, format, sz.toString(),
                                getValueNotNull(result, CaptureResult.SENSOR_SENSITIVITY),
                                TEST_SENSITIVITY_VALUE),
                        sensitivityDiff >= 0);


                // Sleep to Simulate long porcessing before closing the image.
                Thread.sleep(LONG_PROCESS_TIME_MS);
                img.close();
            }
            // Stop capture.
            // Drain the reader queue in case the full queue blocks
            // HAL from delivering new results
            ImageDropperListener imageDropperListener = new ImageDropperListener();
            mReader.setOnImageAvailableListener(imageDropperListener, mHandler);
            Image img = mReader.acquireLatestImage();
            if (img != null) {
                img.close();
            }
            stopCapture(/*fast*/false);
        } finally {
            closeDefaultImageReader();
        }
    }
}

01-03 09:36:52.107  1047   862  6089 D mtkcam-P1HwSettingPolicy: [queryRecommendResizeMaxRatio] Resize-Ratio-Percentage 25 for isp quality
01-03 09:36:52.107  1047   862  6089 D MtkCam/HwInfoHelper: [querySupportResizeRatio] Support Resize-Ratio-Percentage: 40
01-03 09:36:52.107  1047   862  6089 D MtkCam/HwInfoHelper: [alignRrzoHwLimitation] width is beyond scale limitation, modified size: 1696x1248, original target size: 1296x960, crop size: 4208x3120
01-03 09:36:52.107  1047   862  6089 D MtkCam/HwInfoHelper: [alignPass1HwLimitation] rrzo size 1696x1248, stride 3184


08-13 00:29:27.817  1047   794  7158 I mtkcam-SensorSettingPolicy: select size(4208x3120)@30  sensorMode:1 hdrSensorMode:0 hdrHalMode:0, hfpsMode:0
08-13 00:29:27.817  1047   794  7158 W mtkcam-P1HwSettingPolicy: [evaluateDeviceRawBitDepth] By default bitdepth:10
08-13 00:29:27.818  1047   794  7158 I mtkcam-P1HwSettingPolicy: [configP1HwSetting] maxYuvStreamSize is too small(0x0)
08-13 00:29:27.818  1047   794  7158 I mtkcam-P1HwSettingPolicy: [configP1HwSetting] maxYuvStreamSize set rrzo to 1280x960
08-13 00:29:27.818  1047   794  7158 E iio/utility: [_queryXsize_rrzo]ERR(  332):NOT SUPPORT imgFmt(0)


11:56:42.769

11:56:43.192--------423


MTK_INFO_SUPPORTED_HARDWARE_LEVEL


6821_Mobicel :
08-18 15:08:00.398 32683 32700 V CameraTestUtils: get camera characteristics for camera: 0
08-18 15:08:00.401 32683 32700 V CameraTestUtils: Supported sizes are: [1920x1080, 1600x720, 1560x720, 1520x720, 1440x1088, 1440x1080, 1440x720, 1280x960, 1280x720, 1080x720, 960x720, 720x720, 720x480, 640x480, 352x288, 320x240, 192x144, 192x108, 176x144, 160x96]
08-18 15:08:00.401 32683 32700 V CameraTestUtils: Supported sizes are: [1920x1080, 1600x720, 1560x720, 1520x720, 1440x1088, 1440x1080, 1440x720, 1280x960, 1280x720, 1080x720, 960x720, 720x720, 720x480, 640x480, 352x288, 320x240, 192x144, 192x108, 176x144, 160x96]
08-18 15:08:00.402 32683 32700 V CameraTestUtils: get camera characteristics for camera: 0
08-18 15:08:00.403 32683 32700 V CameraTestUtils: Supported sizes are: [1920x1080, 1600x720, 1560x720, 1520x720, 1440x1088, 1440x1080, 1440x720, 1280x960, 1280x720, 1080x720, 960x720, 720x720, 720x480, 640x480, 352x288, 320x240, 192x144, 192x108, 176x144, 160x96]
08-18 15:08:00.404 32683 32700 V CameraTestUtils: Supported sizes are: [1920x1080, 1600x720, 1560x720, 1520x720, 1440x1088, 1440x1080, 1440x720, 1280x960, 1280x720, 1080x720, 960x720, 720x720, 720x480, 640x480, 352x288, 320x240, 192x144, 192x108, 176x144, 160x96]
08-18 15:08:00.405 32683 32700 V CameraTestUtils: get camera characteristics for camera: 0
08-18 15:08:00.406 32683 32700 V CameraTestUtils: Supported sizes are: [4096x3072, 4096x2304, 3840x2160, 3264x2448, 2560x1920, 1920x1088, 1920x1080, 1600x720, 1560x720, 1520x720, 1440x1088, 1440x720, 1280x960, 1280x720, 1080x720, 960x720, 720x720, 640x480, 320x240]


01-01 12:06:31.127  6903  6921 V CameraTestUtils: get camera characteristics for camera: 0
01-01 12:06:31.132  6903  6921 V CameraTestUtils: Supported sizes are: [3840x2160, 3264x2448, 2560x1920, 2560x1440, 1920x1440, 1920x1088, 1920x1080, 1600x720, 1560x720, 1520x720, 1440x1088, 1440x1080, 1440x720, 1280x960, 1280x720, 1080x720, 960x720, 720x720, 720x480, 640x480, 352x288, 320x240, 192x144, 192x108, 176x144, 160x96]
01-01 12:06:31.132  6903  6921 V CameraTestUtils: Supported sizes are: [3840x2160, 3264x2448, 2560x1920, 2560x1440, 1920x1440, 1920x1088, 1920x1080, 1600x720, 1560x720, 1520x720, 1440x1088, 1440x1080, 1440x720, 1280x960, 1280x720, 1080x720, 960x720, 720x720, 720x480, 640x480, 352x288, 320x240, 192x144, 192x108, 176x144, 160x96]
01-01 12:06:31.134  6903  6921 V CameraTestUtils: get camera characteristics for camera: 0
01-01 12:06:31.136  6903  6921 V CameraTestUtils: Supported sizes are: [3840x2160, 3264x2448, 2560x1920, 2560x1440, 1920x1440, 1920x1088, 1920x1080, 1600x720, 1560x720, 1520x720, 1440x1088, 1440x1080, 1440x720, 1280x960, 1280x720, 1080x720, 960x720, 720x720, 720x480, 640x480, 352x288, 320x240, 192x144, 192x108, 176x144, 160x96]
01-01 12:06:31.137  6903  6921 V CameraTestUtils: Supported sizes are: [3840x2160, 3264x2448, 2560x1920, 2560x1440, 1920x1440, 1920x1088, 1920x1080, 1600x720, 1560x720, 1520x720, 1440x1088, 1440x1080, 1440x720, 1280x960, 1280x720, 1080x720, 960x720, 720x720, 720x480, 640x480, 352x288, 320x240, 192x144, 192x108, 176x144, 160x96]
01-01 12:06:31.138  6903  6921 V CameraTestUtils: get camera characteristics for camera: 0
01-01 12:06:31.141  6903  6921 V CameraTestUtils: Supported sizes are: [3840x2160, 3264x2448, 2560x1920, 1920x1088, 1920x1080, 1600x720, 1560x720, 1520x720, 1440x1088, 1440x720, 1280x960, 1280x720, 1080x720, 960x720, 720x720, 640x480, 320x240]


public static Size[] getSupportedSizeForFormat(int format, String cameraId,
        CameraManager cameraManager) throws CameraAccessException {
    CameraCharacteristics properties = cameraManager.getCameraCharacteristics(cameraId);
    assertNotNull("Can't get camera characteristics!", properties);
    if (VERBOSE) {
        Log.v(TAG, "get camera characteristics for camera: " + cameraId);
    }
    StreamConfigurationMap configMap =
            properties.get(CameraCharacteristics.SCALER_STREAM_CONFIGURATION_MAP);
    Size[] availableSizes = configMap.getOutputSizes(format);
    assertArrayNotEmpty(availableSizes, "availableSizes should not be empty for format: "
            + format);
    Size[] highResAvailableSizes = configMap.getHighResolutionOutputSizes(format);
    if (highResAvailableSizes != null && highResAvailableSizes.length > 0) {
        Size[] allSizes = new Size[availableSizes.length + highResAvailableSizes.length];
        System.arraycopy(availableSizes, 0, allSizes, 0,
                availableSizes.length);
        System.arraycopy(highResAvailableSizes, 0, allSizes, availableSizes.length,
                highResAvailableSizes.length);
        availableSizes = allSizes;
    }
    if (VERBOSE) Log.v(TAG, "Supported sizes are: " + Arrays.deepToString(availableSizes));
    return availableSizes;
}
```## CIVIC反复退出相机报错

```text
08-29 07:46:11.070  7673  7673 W libc    : pthread_create failed: couldn't allocate 1085440-bytes mapped space: Out of memory
08-29 07:46:11.071  7673  7673 W com.tcl.camera: Throwing OutOfMemoryError "pthread_create (1040KB stack) failed: Try again" (VmSize 3104616 kB)

08-29 07:46:11.078  7673  7673 E AndroidRuntime: FATAL EXCEPTION: main
08-29 07:46:11.078  7673  7673 E AndroidRuntime: Process: com.tcl.camera, PID: 7673
08-29 07:46:11.078  7673  7673 E AndroidRuntime: java.lang.OutOfMemoryError: pthread_create (1040KB stack) failed: Try again
08-29 07:46:11.078  7673  7673 E AndroidRuntime:  at java.lang.Thread.nativeCreate(Native Method)
08-29 07:46:11.078  7673  7673 E AndroidRuntime:  at java.lang.Thread.start(Thread.java:884)
08-29 07:46:11.078  7673  7673 E AndroidRuntime:  at android.view.InsetsAnimationThread.ensureThreadLocked(InsetsAnimationThread.java:40)
08-29 07:46:11.078  7673  7673 E AndroidRuntime:  at android.view.InsetsAnimationThread.getHandler(InsetsAnimationThread.java:66)
08-29 07:46:11.078  7673  7673 E AndroidRuntime:  at android.view.InsetsAnimationThreadControlRunner.<init>(InsetsAnimationThreadControlRunner.java:121)
08-29 07:46:11.078  7673  7673 E AndroidRuntime:  at android.view.InsetsController.controlAnimationUnchecked(InsetsController.java:1071)
08-29 07:46:11.078  7673  7673 E AndroidRuntime:  at android.view.InsetsController.applyAnimation(InsetsController.java:1409)
08-29 07:46:11.078  7673  7673 E AndroidRuntime:  at android.view.InsetsController.applyAnimation(InsetsController.java:1390)
08-29 07:46:11.078  7673  7673 E AndroidRuntime:  at android.view.InsetsController.onControlsChanged(InsetsController.java:860)
08-29 07:46:11.078  7673  7673 E AndroidRuntime:  at android.view.ViewRootImpl.relayoutWindow(ViewRootImpl.java:8313)
08-29 07:46:11.078  7673  7673 E AndroidRuntime:  at android.view.ViewRootImpl.performTraversals(ViewRootImpl.java:3069)
08-29 07:46:11.078  7673  7673 E AndroidRuntime:  at android.view.ViewRootImpl.doTraversal(ViewRootImpl.java:2289)
08-29 07:46:11.078  7673  7673 E AndroidRuntime:  at android.view.ViewRootImpl$TraversalRunnable.run(ViewRootImpl.java:9222)
08-29 07:46:11.078  7673  7673 E AndroidRuntime:  at android.view.Choreographer$CallbackRecord.run(Choreographer.java:1120)
08-29 07:46:11.078  7673  7673 E AndroidRuntime:  at android.view.Choreographer.doCallbacks(Choreographer.java:911)
08-29 07:46:11.078  7673  7673 E AndroidRuntime:  at android.view.Choreographer.doFrame(Choreographer.java:830)
08-29 07:46:11.078  7673  7673 E AndroidRuntime:  at android.view.Choreographer$FrameDisplayEventReceiver.run(Choreographer.java:1105)
08-29 07:46:11.078  7673  7673 E AndroidRuntime:  at android.os.Handler.handleCallback(Handler.java:938)
08-29 07:46:11.078  7673  7673 E AndroidRuntime:  at android.os.Handler.dispatchMessage(Handler.java:99)
08-29 07:46:11.078  7673  7673 E AndroidRuntime:  at android.os.Looper.loopOnce(Looper.java:217)
08-29 07:46:11.078  7673  7673 E AndroidRuntime:  at android.os.Looper.loop(Looper.java:309)
08-29 07:46:11.078  7673  7673 E AndroidRuntime:  at android.app.ActivityThread.main(ActivityThread.java:8161)
08-29 07:46:11.078  7673  7673 E AndroidRuntime:  at java.lang.reflect.Method.invoke(Native Method)
08-29 07:46:11.078  7673  7673 E AndroidRuntime:  at com.android.internal.os.RuntimeInit$MethodAndArgsCaller.run(RuntimeInit.java:579)
08-29 07:46:11.078  7673  7673 E AndroidRuntime:  at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:1045)


https://blog.csdn.net/Tencent_Bugly/article/details/78542324

创建线程失败

创建线程也可以归纳为两个步骤：

调用mmap分配栈内存。这里mmap flag中指定了MAP_ANONYMOUS，即匿名内存映射。这是在Linux中分配大块内存的常用方式。其分配的是虚拟内存，对应页的物理内存并不会立即分配，而是在用到的时候触发内核的缺页中断，然后中断处理函数再分配物理内存。

调用clone方法进行线程创建。

第一步分配栈内存失败是由于进程的虚拟内存不足，抛出错误信息如下：

W/libc: pthread_create failed: couldn't allocate 1073152-bytes mapped space: Out of memory
W/tch.crowdsourc: Throwing OutOfMemoryError with VmSize  4191668 kB "pthread_create (1040KB stack) failed: Try again"
java.lang.OutOfMemoryError: pthread_create (1040KB stack) failed: Try again
        at java.lang.Thread.nativeCreate(Native Method)
        at java.lang.Thread.start(Thread.java:753)
第二步clone方法失败是因为线程数超出了限制，抛出错误信息如下：

W/libc: pthread_create failed: clone failed: Out of memory
W/art: Throwing OutOfMemoryError "pthread_create (1040KB stack) failed: Out of memory"
java.lang.OutOfMemoryError: pthread_create (1040KB stack) failed: Out of memory
          at java.lang.Thread.nativeCreate(Native Method)
          at java.lang.Thread.start(Thread.java:1078)


没错！就是因为这里的mmap失败了。又是虚拟内存分配失败。

默认 StackSize 是多少？
另外一个需要考虑的事，如果没有指定stackSize，默认的是多少呢？
Java层的Thread类默认stackSize是0，传给native层也是0，于是在native层有这样一段代码。

static size_t FixStackSize(size_t stack_size) {
  if (stack_size == 0) {
    // GetDefaultStackSize 是启动art时命令行的 "-Xss=" 参数
    // Android 中没有该参数，因此为0.
    stack_size = Runtime::Current()->GetDefaultStackSize();
  }

  // bionic pthread 默认栈大小是 1M
  stack_size += 1 * MB;

  ... 

  if (Runtime::Current()->ExplicitStackOverflowChecks()) {
    // 8K
    stack_size += GetStackOverflowReservedBytes(kRuntimeISA);
  } else {
    // 8K + 8K
    stack_size += Thread::kStackOverflowImplicitCheckSize +
        GetStackOverflowReservedBytes(kRuntimeISA);
  }
  ...
  return stack_size;
}
因此 默认的 stackSize = 1M + 8K + 8K = 1040K，和crash堆栈完全一致。


可以看到32位系统中，用户空间的内存是3G大，简单起见，我们粗略估计一下，假设

1.可见虚拟内存是3G大（实际值更小）

2.创建一个进程需要1M虚拟内存（实际值更大）
因此再假设有一个进程，除了创建线程什么都不干，那他最多能创建多少个线程？

3G/1M = 约3000个
没错，在完全理想的情况下最多是3000个线程。综合其他因素，实际值会明显小于3000。虽然3000的上限看上去很大，而如果有代码逻辑问题，创建很多线程，其实很容易爆掉。

外网上报的crash则属于这种情况，某种corner-case下会导致线程的无节制创建。


查看 Camera 进程的状态
watch -n1 "adb shell cat /proc/`adb shell pidof com.tcl.camera`/status"

/proc/pid/status 解读及部分对应代码
https://blog.csdn.net/xback_shaohan/article/details/112055571?spm=1001.2014.3001.5502

最大线程数
adb shell cat /proc/sys/kernel/threads-max

查看 Camera 进程打开的 FD 的数量
adb shell ls -al /proc/`adb shell pidof com.tcl.camera`/fd | wc -l


TCL 分析
底层文件 mmap出错

08-26 12:52:37.333 29926 29976 I CameraSdk: [ExtensionAlgoManager][Thread: consumerThread] loadALGOModel begin
08-26 12:52:37.341 29926 29976 E filemap : mmap(5595136,15553125) failed: Out of memory
08-26 12:52:37.342 29926 29976 E com.tcl.camera: Failed to mmap file 'assets/bokehmodel/bokeh_segment.bin' in APK '/system/priv-app/TctCamera/TctCamera.apk'

上面这段mmap失败，adjOffset=5595136， adjLength=15553125：

void* ptr = mmap64(nullptr, adjLength, prot, flags, fd, adjOffset);
if (ptr == MAP_FAILED) {
    if (errno == EINVAL && length == 0) {
        ptr = nullptr;
        adjust = 0;
    } else {
        ALOGE("mmap(%lld,%zu) failed: %s\n", (long long)adjOffset, adjLength, strerror(errno));
        return false;
    }
}

mmap申请的是虚拟地址，Out of memory（ENOMEM）的原因应该不可能是内存不够，可能是进程允许的最大mapping数达到了，或者adjOffset+adjLength超过了文件大小，需要进一步调查。
```## 连续拍照相机闪退

```text
lowmemorykiller: Kill 'com.tcl.camera' (23260), uid 10076, oom_score_adj 0 to free 74832kB rss, 33496kB swap; reason: min watermark is breached even after kill

09-01 15:22:10.245 10067 16106 16319 E AndroidRuntime: FATAL EXCEPTION: BlurThread
09-01 15:22:10.245 10067 16106 16319 E AndroidRuntime: Process: com.tcl.camera, PID: 16106
09-01 15:22:10.245 10067 16106 16319 E AndroidRuntime: java.lang.OutOfMemoryError
09-01 15:22:10.245 10067 16106 16319 E AndroidRuntime:  at android.graphics.Bitmap.nativeCreate(Native Method)
09-01 15:22:10.245 10067 16106 16319 E AndroidRuntime:  at android.graphics.Bitmap.createBitmap(Bitmap.java:1104)
09-01 15:22:10.245 10067 16106 16319 E AndroidRuntime:  at android.graphics.Bitmap.createBitmap(Bitmap.java:914)
09-01 15:22:10.245 10067 16106 16319 E AndroidRuntime:  at android.graphics.Bitmap.createBitmap(Bitmap.java:818)
09-01 15:22:10.245 10067 16106 16319 E AndroidRuntime:  at android.graphics.Bitmap.createBitmap(Bitmap.java:798)
09-01 15:22:10.245 10067 16106 16319 E AndroidRuntime:  at com.android.camera.ui.thumb.PreProduceThumbManager.updateThumbFromSurface(PreProduceThumbManager.java:139)
09-01 15:22:10.245 10067 16106 16319 E AndroidRuntime:  at com.android.camera.ui.thumb.PreProduceThumbManager.onPreviewBitmapCatch(PreProduceThumbManager.java:115)
09-01 15:22:10.245 10067 16106 16319 E AndroidRuntime:  at com.android.camera.ui.blur.GlRenderBlurManagerProxy.handleFullPreviewCopyBitmap(GlRenderBlurManagerProxy.java:291)
09-01 15:22:10.245 10067 16106 16319 E AndroidRuntime:  at com.android.camera.ui.blur.GlRenderBlurManagerProxy.access$1100(GlRenderBlurManagerProxy.java:27)
09-01 15:22:10.245 10067 16106 16319 E AndroidRuntime:  at com.android.camera.ui.blur.GlRenderBlurManagerProxy$1.lambda$run$0$GlRenderBlurManagerProxy$1(GlRenderBlurManagerProxy.java:214)
09-01 15:22:10.245 10067 16106 16319 E AndroidRuntime:  at com.android.camera.ui.blur.-$$Lambda$GlRenderBlurManagerProxy$1$WHOAcj5IWfcZSy44Qm6SfIQ1UtA.onPixelCopyFinished(Unknown Source:2)
09-01 15:22:10.245 10067 16106 16319 E AndroidRuntime:  at android.view.PixelCopy$1.run(PixelCopy.java:191)
09-01 15:22:10.245 10067 16106 16319 E AndroidRuntime:  at android.os.Handler.handleCallback(Handler.java:938)
09-01 15:22:10.245 10067 16106 16319 E AndroidRuntime:  at android.os.Handler.dispatchMessage(Handler.java:99)
09-01 15:22:10.245 10067 16106 16319 E AndroidRuntime:  at android.os.Looper.loopOnce(Looper.java:217)
09-01 15:22:10.245 10067 16106 16319 E AndroidRuntime:  at android.os.Looper.loop(Looper.java:309)
09-01 15:22:10.245 10067 16106 16319 E AndroidRuntime:  at android.os.HandlerThread.run(HandlerThread.java:67)

应该和《反复退出相机报错》是同一个问题

问题发生原因是 HDR 库有内存泄漏
```## bugreport 中搜索 system_app_crash

## MTK平台 Camera 内存（1）介绍

```text
https://blog.csdn.net/weixin_38328785/article/details/113649856
```## CivicPlus微距模式打不开

```text
09-02 15:17:47.389926  8087  8110 E CameraSdk: [ModeCharacteristicsTable][Thread: Camera request Thread] TCT_ERROR: do not support facing: false modeName: SuperMicro
09-02 15:17:47.390011  8087  8110 E CameraSdk: [CameraModeManager][Thread: Camera request Thread] TCT_ERROR: do not support facing: FACING_BACK modeName: SuperMicro cameraType: Macro

用最新状态的手机可以打开
```## Nova 切换前后 camera 黑屏

```text
09-04 10:26:25.109  5037  5067 E AndroidFutures: tryAcquireLastAvailableFrame failed.
09-04 10:26:25.109  5037  5067 E AndroidFutures: java.lang.UnsupportedOperationException: This operation is not allowed
09-04 10:26:25.109  5037  5067 E AndroidFutures:  at com.google.android.apps.cameralite.gluelayer.CameraStateMachineState$-CC.$default$tryAcquireLastAvailableFrame$ar$ds(PG:1)
09-04 10:26:25.109  5037  5067 E AndroidFutures:  at com.google.android.apps.cameralite.gluelayer.impl.ModeTransitionState.tryAcquireLastAvailableFrame(Unknown Source:0)
09-04 10:26:25.109  5037  5067 E AndroidFutures:  at com.google.android.apps.cameralite.camerastack.cameramanagers.impl.VideoCameraManagerImpl$$ExternalSyntheticLambda1.call(PG:43)
09-04 10:26:25.109  5037  5067 E AndroidFutures:  at com.google.common.util.concurrent.ClosingFuture$2.call(PG:2)
09-04 10:26:25.109  5037  5067 E AndroidFutures:  at com.google.common.util.concurrent.ExecutionSequencer$1.call(PG:1)
09-04 10:26:25.109  5037  5067 E AndroidFutures:  at com.google.apps.tiktok.tracing.TracePropagation$5.call(PG:22)
09-04 10:26:25.109  5037  5067 E AndroidFutures:  at com.google.common.util.concurrent.TrustedListenableFutureTask$TrustedFutureInterruptibleAsyncTask.runInterruptibly(PG:1)
09-04 10:26:25.109  5037  5067 E AndroidFutures:  at com.google.common.util.concurrent.InterruptibleTask.run(PG:4)
09-04 10:26:25.109  5037  5067 E AndroidFutures:  at com.google.common.util.concurrent.TrustedListenableFutureTask.run(PG:1)
09-04 10:26:25.109  5037  5067 E AndroidFutures:  at com.google.common.util.concurrent.ExecutionSequencer$TaskNonReentrantExecutor.run(PG:3)
09-04 10:26:25.109  5037  5067 E AndroidFutures:  at com.google.common.util.concurrent.SequentialExecutor$1.run(PG:1)
09-04 10:26:25.109  5037  5067 E AndroidFutures:  at com.google.common.util.concurrent.SequentialExecutor$QueueWorker.run(PG:4)
09-04 10:26:25.109  5037  5067 E AndroidFutures:  at com.google.android.libraries.concurrent.ExceptionHandlingExecutorFactory$ExceptionHandlingRunnable.run(PG:5)
09-04 10:26:25.109  5037  5067 E AndroidFutures:  at com.google.android.libraries.concurrent.FixedThreadPool$Worker.run(PG:23)
09-04 10:26:25.109  5037  5067 E AndroidFutures:  at com.google.android.libraries.camera.device.AudioRestrictionApiImpl$$ExternalSyntheticLambda0.run(PG:21)
09-04 10:26:25.109  5037  5067 E AndroidFutures:  at com.google.android.libraries.concurrent.AndroidPriorityThreadFactory$$ExternalSyntheticLambda0.run(PG:3)
09-04 10:26:25.109  5037  5067 E AndroidFutures:  at java.lang.Thread.run(Thread.java:920)
09-04 10:26:25.113   454   454 I SPRDHWComposer: SprdDrm:: GetConfigs , [0]
09-04 10:26:25.113   454   454 D SPRDHWComposer: HWCDisplay::get_display_attribute <357>: config = 0
09-04 10:26:25.113   454   454 D SPRDHWComposer: HWCDisplay::get_display_attribute <357>: config = 0
09-04 10:26:25.114   454   454 D SPRDHWComposer: HWCDisplay::get_display_attribute <357>: config = 0
09-04 10:26:25.114   454   454 D SPRDHWComposer: HWCDisplay::get_display_attribute <357>: config = 0
09-04 10:26:25.114   454   454 D SPRDHWComposer: HWCDisplay::get_display_attribute <357>: config = 0
09-04 10:26:25.114   454   454 D SPRDHWComposer: HWCDisplay::get_display_attribute <357>: config = 0
09-04 10:26:25.114   514   552 E HWComposer: getAttribute: getDisplayAttribute failed for display 0: BadConfig (1)
09-04 10:26:25.114  5037  5067 E AndroidFutures: tryAcquireLastAvailableFrame failed.
09-04 10:26:25.114  5037  5067 E AndroidFutures: java.lang.UnsupportedOperationException: This operation is not allowed
09-04 10:26:25.114  5037  5067 E AndroidFutures:  at com.google.android.apps.cameralite.gluelayer.CameraStateMachineState$-CC.$default$tryAcquireLastAvailableFrame$ar$ds(PG:1)
09-04 10:26:25.114  5037  5067 E AndroidFutures:  at com.google.android.apps.cameralite.gluelayer.impl.ModeTransitionState.tryAcquireLastAvailableFrame(Unknown Source:0)
09-04 10:26:25.114  5037  5067 E AndroidFutures:  at com.google.android.apps.cameralite.camerastack.cameramanagers.impl.VideoCameraManagerImpl$$ExternalSyntheticLambda1.call(PG:43)
09-04 10:26:25.114  5037  5067 E AndroidFutures:  at com.google.common.util.concurrent.ClosingFuture$2.call(PG:2)
09-04 10:26:25.114  5037  5067 E AndroidFutures:  at com.google.common.util.concurrent.ExecutionSequencer$1.call(PG:1)
09-04 10:26:25.114  5037  5067 E AndroidFutures:  at com.google.apps.tiktok.tracing.TracePropagation$5.call(PG:22)
09-04 10:26:25.114  5037  5067 E AndroidFutures:  at com.google.common.util.concurrent.TrustedListenableFutureTask$TrustedFutureInterruptibleAsyncTask.runInterruptibly(PG:1)
09-04 10:26:25.114  5037  5067 E AndroidFutures:  at com.google.common.util.concurrent.InterruptibleTask.run(PG:4)
09-04 10:26:25.114  5037  5067 E AndroidFutures:  at com.google.common.util.concurrent.TrustedListenableFutureTask.run(PG:1)
09-04 10:26:25.114  5037  5067 E AndroidFutures:  at com.google.common.util.concurrent.ExecutionSequencer$TaskNonReentrantExecutor.run(PG:3)
09-04 10:26:25.114  5037  5067 E AndroidFutures:  at com.google.common.util.concurrent.SequentialExecutor$1.run(PG:1)
09-04 10:26:25.114  5037  5067 E AndroidFutures:  at com.google.common.util.concurrent.SequentialExecutor$QueueWorker.run(PG:4)
09-04 10:26:25.114  5037  5067 E AndroidFutures:  at com.google.android.libraries.concurrent.ExceptionHandlingExecutorFactory$ExceptionHandlingRunnable.run(PG:5)
09-04 10:26:25.114  5037  5067 E AndroidFutures:  at com.google.android.libraries.concurrent.FixedThreadPool$Worker.run(PG:23)
09-04 10:26:25.114  5037  5067 E AndroidFutures:  at com.google.android.libraries.camera.device.AudioRestrictionApiImpl$$ExternalSyntheticLambda0.run(PG:21)
09-04 10:26:25.114  5037  5067 E AndroidFutures:  at com.google.android.libraries.concurrent.AndroidPriorityThreadFactory$$ExternalSyntheticLambda0.run(PG:3)
09-04 10:26:25.114  5037  5067 E AndroidFutures:  at java.lang.Thread.run(Thread.java:920)


09-04 10:36:06.069   450  5424 W Cam3Channel: 280, channelClearAllQBuff: channel has no valied stream
09-04 10:36:06.069   450  5424 W Cam3Channel: 280, channelClearAllQBuff: channel has no valied stream
09-04 10:36:06.069   450  5424 W Cam3Channel: 280, channelClearAllQBuff: channel has no valied stream


提交记录：
http://192.168.3.79:8084/#/c/81507/

WB calibration 、init setting时序发生异常；此修改进行同步处理，不会有其他影响。
```## SPRD dump预览图

```text
https://blog.csdn.net/Cmatrix204/article/details/124520942

vendor/sprd/modules/libcamera/oem2v6/src/cmr_preview.c

adb shell setprop debug.camera.preview.dump.count 10

adb pull /data/vendor/cameraserver

adb shell setprop persist.vendor.cam.isp.log 1
adb shell setprop persist.vendor.cam.oem.log 1
adb shell setprop persist.vendor.cam.sensor.log 1
```## SPRD 双摄帧同步

```text
https://blog.csdn.net/LAJICSDN1/article/details/121899855
```## Camera连续拍照之后FC

```text
./events_log_17__2022_0904_070755:09-04 03:26:23.063560  1168  3974 I am_proc_died: [0,6548,com.tcl.camera,0,2]
./events_log_17__2022_0904_070755:09-04 03:29:29.517523  1168  6816 I am_proc_died: [0,8170,com.tcl.camera,0,2]
./events_log_17__2022_0904_070755:09-04 03:30:36.886223  1168  1300 I am_proc_died: [0,13317,com.tcl.camera,0,2]
./events_log_17__2022_0904_070755:09-04 03:33:47.364505  1168  5685 I am_proc_died: [0,15910,com.tcl.camera,0,2]
./events_log_17__2022_0904_070755:09-04 07:01:17.290605  1168  2335 I am_proc_died: [0,25860,com.tcl.camera,0,2]
./events_log_17__2022_0904_070755:09-04 07:07:35.057263  1168  6816 I am_proc_died: [0,3354,com.tcl.camera,0,2]


./sys_log_18__2022_0904_070755:09-04 03:28:25.717200  1168 11551 I ActivityManager: Low on memory:
./sys_log_18__2022_0904_070755:09-04 03:33:41.161168  1168 20465 I ActivityManager: Low on memory:
./sys_log_18__2022_0904_070755:09-04 04:00:51.689001  1168 26324 I ActivityManager: Low on memory:
./sys_log_18__2022_0904_070755:09-04 07:01:02.737506  1168  1903 I ActivityManager: Low on memory:
./sys_log_18__2022_0904_070755:09-04 07:07:22.382273  1168  7123 I ActivityManager: Low on memory:


关键字
am_proc_died
am_low_memory
Low on memory

TctLowMem


09-05 04:04:45.442  1173  7357 I am_proc_died: [0,20762,com.tcl.camera,0,2]

空进程被杀

这种是说进程已经不活动了被系统杀了，通常这种情况很少，大概是这样的：

08-10 13:32:13.057 1000 1700 1812 I am_kill : [0,2409,com.miui.screenrecorder,955,empty for 1800s]
empty进程数量达到阈值了，会查杀30min内没活跃的进程

08-10 16:00:54.244 1000 1700 1795 I ActivityManager: Killing 20081:com.android.providers.calendar/u0a72 (adj 985): empty #26
系统内empty进程数量达到阈值26（不同手机略有不同）会按时间顺序查杀进程；



./Camera_VJ1R_FC.log:09-07 14:04:13.643  6863  6897 I CameraApp: [QCOMContinuousShot][Thread: Camera request Thread] [saveJpeg]  mCurrentShotsNum = 1
./Camera_VJ1R_FC.log:09-07 14:04:13.769  6863  6897 I CameraApp: [QCOMContinuousShot][Thread: Camera request Thread] [saveJpeg]  mCurrentShotsNum = 2
./Camera_VJ1R_FC.log:09-07 14:04:14.188  6863  6897 I CameraApp: [QCOMContinuousShot][Thread: Camera request Thread] [saveJpeg]  mCurrentShotsNum = 3
./Camera_VJ1R_FC.log:09-07 14:04:14.283  6863  6897 I CameraApp: [QCOMContinuousShot][Thread: Camera request Thread] [saveJpeg]  mCurrentShotsNum = 4
./Camera_VJ1R_FC.log:09-07 14:04:14.713  6863  6897 I CameraApp: [QCOMContinuousShot][Thread: Camera request Thread] [saveJpeg]  mCurrentShotsNum = 5
./Camera_VJ1R_FC.log:09-07 14:04:14.915  6863  6897 I CameraApp: [QCOMContinuousShot][Thread: Camera request Thread] [saveJpeg]  mCurrentShotsNum = 6
./Camera_VJ1R_FC.log:09-07 14:04:15.172  1144  1369 I am_proc_died: [0,6863,com.tcl.camera,0,2]
./Camera_VJ1R_FC.log:09-07 14:04:43.681  8599  8623 I CameraApp: [QCOMContinuousShot][Thread: Camera request Thread] [saveJpeg]  mCurrentShotsNum = 1



adb shell dumpsys meminfo | grep -E "camerahalserver|ION:|Used RAM|Free RAM" 
关闭多帧
adb root;adb shell setprop vendor.mfll.force 0;adb shell pkill camerahalserver;


BSP
刚开机
58,938K: camerahalserver (pid 686)
ION:    66,752K (    1,904K mapped +    39,204K unmapped +    25,644K pools)

预览
149,653K: camerahalserver (pid 685)
ION:   128,124K (   66,148K mapped +    39,988K unmapped +    21,988K pools)

连续拍照20次之后(非连拍)
249,406K: camerahalserver (pid 685)
ION:   238,156K (  187,004K mapped +     1,676K unmapped +    49,476K pools)


Civic(关闭多帧)
刚开机
68,500K: camerahalserver (pid 749)
ION:    72,716K (   14,080K mapped +    43,340K unmapped +    15,296K pools)

预览
394,355K: camerahalserver (pid 4306)
ION:   344,604K (  110,132K mapped +   233,912K unmapped +       560K pools)

连续拍照20之后(非连拍)
467,589K: camerahalserver (pid 4306)
ION:   457,268K (  374,748K mapped +    62,112K unmapped +    20,408K pools)

474,263K: camerahalserver (pid 4306)
ION:   455,124K (  374,812K mapped +    62,112K unmapped +    18,200K pools)

连拍5次之后
443,823K: camerahalserver (pid 4306)
ION:   505,188K (  413,524K mapped +    62,112K unmapped +    29,552K pools)

退出相机到Launcher
69,144K: camerahalserver (pid 4306)
ION:   540,040K (   20,280K mapped +    43,344K unmapped +   476,416K pools)


VJ1V
刚开机
64,172K: camerahalserver (pid 748)
ION:    96,272K (   15,776K mapped +    43,308K unmapped +    37,188K pools)

预览
350,011K: camerahalserver (pid 2612)
ION:   357,040K (  113,076K mapped +   233,872K unmapped +    10,092K pools)

连续拍照20之后(非连拍)
401,315K: camerahalserver (pid 2612)
ION:   433,020K (  351,328K mapped +    57,432K unmapped +    24,260K pools)

连拍5次之后
451,371K: camerahalserver (pid 2612)
ION:   524,224K (  431,056K mapped +    62,072K unmapped +    31,096K pools)

RSS - Resident Set Size 实际使用物理内存（包含共享库占用的内存）
PSS - Proportional Set Size 实际使用的物理内存（比例分配共享库占用的内存）



从 Log 中看到 camerahalserver 和 ion 内存占用太高，需要进行优化
https://blog.csdn.net/liaokesen168/article/details/104768367

1.减少 framebuffer 的数量
2.减少单次连拍张数

adb shell showmap `adb shell pidof camerahalserver` -v
adb shell dumpsys meminfo
```## 查看ion内存分配

```text
cat /sys/kernel/debug/ion/clients/clients_summary
client_name      pid      size    
------------------------------------------
1157             1157     6910291 
1745             1745     5939539 
526              526      21096775
572              572      21195079
disp_decouple    201      3485696 
display          1        3736576 
4306             4306     24576   
4306             4306     24576   
1417             1417     2188961 
4306             4306     499712  
4306             4306     24576   
4306             4306     24576

cat /sys/kernel/debug/ion/client_history
```## MTK平台 Camera 内存（1）介绍

```text
https://blog.csdn.net/weixin_38328785/article/details/113649856
```## Nova 切换 photo/video 之后黑屏

```text
M2C5407  09-12 14:46:58.782 15228 15263 W CameraAlivenessCheckImp: Camera start had an issue.
M2C5407  09-12 14:46:58.782 15228 15263 W CameraAlivenessCheckImp: com.google.common.util.concurrent.TimeoutFuture$TimeoutFutureException: Timed out (timeout delayed by 40 ms after scheduled time): androidx.concurrent.futures.CallbackToFutureAdapter$SafeFuture$1@f00f08c[status=PENDING, info=[tag=[awaitStarted]]]
M2C5408  09-12 14:46:58.924 15228 15246 D pck     : Resuming FrameServer-158
M2C5409  09-12 14:46:58.925 15228 15262 I pck     : Submitting FrameRequest-5157 with [FrameStream-904, FrameStream-907]
M2C540C  09-12 14:46:59.243 15228 15241 E UncaughtExceptionHandle: Encountered uncaught exception.
M2C540C  09-12 14:46:59.243 15228 15241 E UncaughtExceptionHandle: java.util.concurrent.TimeoutException: android.hardware.camera2.impl.CameraCaptureSessionImpl.finalize() timed out after 10 seconds
M2C540C  09-12 14:46:59.243 15228 15241 E UncaughtExceptionHandle:  at android.hardware.camera2.impl.CameraCaptureSessionImpl.close(CameraCaptureSessionImpl.java:558)
M2C540C  09-12 14:46:59.243 15228 15241 E UncaughtExceptionHandle:  at android.hardware.camera2.impl.CameraCaptureSessionImpl.finalize(CameraCaptureSessionImpl.java:879)
M2C540C  09-12 14:46:59.243 15228 15241 E UncaughtExceptionHandle:  at java.lang.Daemons$FinalizerDaemon.doFinalize(Daemons.java:291)
M2C540C  09-12 14:46:59.243 15228 15241 E UncaughtExceptionHandle:  at java.lang.Daemons$FinalizerDaemon.runInternal(Daemons.java:278)
M2C540C  09-12 14:46:59.243 15228 15241 E UncaughtExceptionHandle:  at java.lang.Daemons$Daemon.run(Daemons.java:139)
M2C540C  09-12 14:46:59.243 15228 15241 E UncaughtExceptionHandle:  at java.lang.Thread.run(Thread.java:920)
M2C540D  09-12 14:46:59.251 15228 15228 E ClientLoggingReceiver: Logging to Clearcut failed.
M2C540D  09-12 14:46:59.251 15228 15228 E ClientLoggingReceiver: com.google.android.gms.common.api.ApiException: 31002: Caller is restricted
M2C540D  09-12 14:46:59.251 15228 15228 E ClientLoggingReceiver:  at com.google.android.libraries.gmstasks.TaskFutures$$ExternalSyntheticLambda0.onResult(PG:6)
M2C540D  09-12 14:46:59.251 15228 15228 E ClientLoggingReceiver:  at com.google.android.gms.common.api.internal.BasePendingResult$CallbackHandler.handleMessage(PG:6)
M2C540D  09-12 14:46:59.251 15228 15228 E ClientLoggingReceiver:  at android.os.Handler.dispatchMessage(Handler.java:106)
M2C540D  09-12 14:46:59.251 15228 15228 E ClientLoggingReceiver:  at android.os.Looper.loopOnce(Looper.java:201)
M2C540D  09-12 14:46:59.251 15228 15228 E ClientLoggingReceiver:  at android.os.Looper.loop(Looper.java:288)
M2C540D  09-12 14:46:59.251 15228 15228 E ClientLoggingReceiver:  at android.app.ActivityThread.main(ActivityThread.java:7941)
M2C540D  09-12 14:46:59.251 15228 15228 E ClientLoggingReceiver:  at java.lang.reflect.Method.invoke(Native Method)
M2C540D  09-12 14:46:59.251 15228 15228 E ClientLoggingReceiver:  at com.android.internal.os.RuntimeInit$MethodAndArgsCaller.run(RuntimeInit.java:553)
M2C540D  09-12 14:46:59.251 15228 15228 E ClientLoggingReceiver:  at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:1003)
M2C540F  09-12 14:46:59.281   974 11225 E stark   : filterType return false
M2C5411  09-12 14:46:59.295   974 11226 E starklog2: intsert count  1 = 1 errorType = system_app_crash

SPCSS01049072 中解决
```## Nova 无法打开HDR和夜景模式？

```text
09-13 13:45:45.377   516   876 D Cam3HWI : 933, configureStreams: :hal3: stream 0: stream_type=1, chn_type=1, w=960, h=720, format=34, usage=0x20000903, hasCallbackStream=0, hasYuv2Stream=0
09-13 13:45:45.377   516   876 D Cam3Channel: 404, addStream: E: index = 0
09-13 13:45:45.377   516   876 D Cam3HWI : 1042, configureStreams: slowmotion=1, high video mode = 0, kMaxBuffers=4
09-13 13:45:45.377   516   876 D Cam3HWI : 1087, configureStreams: stream type:1, max_buffers:4
09-13 13:45:45.377   516   876 D Cam3HWI : 3520, getP2pEnable: getP2pEnable:0 mMultiCameraMode:0
09-13 13:45:45.377   516   876 D Cam3HWI : 933, configureStreams: :hal3: stream 1: stream_type=4, chn_type=1, w=2592, h=1944, format=35, usage=0x3, hasCallbackStream=0, hasYuv2Stream=1
09-13 13:45:45.378   516   876 D Cam3Channel: 404, addStream: E: index = 3
09-13 13:45:45.378   516   876 D Cam3HWI : 1042, configureStreams: slowmotion=1, high video mode = 0, kMaxBuffers=4
09-13 13:45:45.378   516   876 D Cam3HWI : 1087, configureStreams: stream type:4, max_buffers:4
09-13 13:45:45.378   516   876 D Cam3HWI : 3520, getP2pEnable: getP2pEnable:0 mMultiCameraMode:0
09-13 13:45:45.378   516   876 D Cam3HWI : 933, configureStreams: :hal3: stream 2: stream_type=0, chn_type=0, w=640, h=480, format=35, usage=0x3, hasCallbackStream=0, hasYuv2Stream=1
09-13 13:45:45.378   516   876 E Cam3HWI : 1084, configureStreams: channel type is invalid channel
09-13 13:45:45.378   516   876 D Cam3HWI : 1087, configureStreams: stream type:0, max_buffers:0
09-13 13:45:45.378   516   876 D Cam3HWI : 1107, configureStreams: streamList->streams[0]->max_buffers 4
09-13 13:45:45.378   516   876 D Cam3HWI : 1107, configureStreams: streamList->streams[1]->max_buffers 4
09-13 13:45:45.378   516   876 D Cam3HWI : 1107, configureStreams: streamList->streams[2]->max_buffers 0

09-13 13:45:45.403   703  1178 E Camera3-OutputStream: configureConsumerQueueLocked: Camera HAL requested max_buffer count: 0, requires at least 1
09-13 13:45:45.403   703  1178 E Camera3-Stream: finishConfiguration: Unable to configure stream 8 queue: Function not implemented (-38)
09-13 13:45:45.403   703  1178 E Camera3-Device: Camera 0: configureStreamsLocked: Can't finish configuring output stream 8: Function not implemented (-38)
09-13 13:45:45.403   703  1178 E CameraDeviceClient: endConfigure: Camera 0: Unsupported set of inputs/outputs provided
09-13 13:45:45.403 13658 13701 W CameraDevice-JV-0: Stream configuration failed due to: endConfigure:554: Camera 0: Unsupported set of inputs/outputs provided
09-13 13:45:45.404 13658 13701 E CameraCaptureSession: Session 2: Failed to create capture session; configuration failed
09-13 13:45:45.404 13658 13845 W pck     : CaptureSession-2 failed to configure.
09-13 13:45:45.407 13658 13845 I pck     : Refusing to finalize outputs for CaptureSession-2 using [DeferredConfig<Stream-6>]


正常配流的log
09-13 13:55:13.802   516   876 D Cam3HWI : 802, configureStreams: mZslIpsEnable 0
09-13 13:55:13.802   516   876 D Cam3HWI : 933, configureStreams: :hal3: stream 0: stream_type=1, chn_type=1, w=960, h=720, format=34, usage=0x20000903, hasCallbackStream=0, hasYuv2Stream=0
09-13 13:55:13.802   516   876 D Cam3HWI : 1042, configureStreams: slowmotion=1, high video mode = 0, kMaxBuffers=4
09-13 13:55:13.802   516   876 D Cam3HWI : 1087, configureStreams: stream type:1, max_buffers:4
09-13 13:55:13.802   516   876 D Cam3HWI : 933, configureStreams: :hal3: stream 1: stream_type=7, chn_type=2, w=2592, h=1944, format=33, usage=0x3, hasCallbackStream=0, hasYuv2Stream=0
09-13 13:55:13.802   516   876 D Cam3HWI : 1087, configureStreams: stream type:7, max_buffers:1
09-13 13:55:13.802   516   876 D Cam3HWI : 933, configureStreams: :hal3: stream 2: stream_type=4, chn_type=1, w=640, h=480, format=35, usage=0x3, hasCallbackStream=0, hasYuv2Stream=1
09-13 13:55:13.803   516   876 D Cam3HWI : 1042, configureStreams: slowmotion=1, high video mode = 0, kMaxBuffers=4
09-13 13:55:13.803   516   876 D Cam3HWI : 1087, configureStreams: stream type:4, max_buffers:4
09-13 13:55:13.803   516   876 D Cam3HWI : 1107, configureStreams: streamList->streams[0]->max_buffers 4
09-13 13:55:13.803   516   876 D Cam3HWI : 1107, configureStreams: streamList->streams[1]->max_buffers 1
09-13 13:55:13.803   516   876 D Cam3HWI : 1107, configureStreams: streamList->streams[2]->max_buffers 4
09-13 13:55:13.803   516   876 I Cam3HWI : 1127, configureStreams: :hal3: camId=0, prev: w=960, h=720, video: w=0, h=0, callback: w=0, h=0, yuv2: w=640, h=480, cap: w=2592, h=1944 yuv3: w=0, h=0,
09-13 13:55:13.807   516   876 D Cam3HWI : 1202, configureStreams: mMultiCameraMode :0


解决方案：
appMode传的不对导致，修改默认appMode=0即可
http://192.168.3.79:8084/#/c/81800/
```## Nova Camera配流

```text
展锐 DreamCamera2 Photo 模式配流
09-13 14:31:55.471   516   881 D Cam3HWI : 933, configureStreams: :hal3: stream 1: stream_type=7, chn_type=2, w=2592, h=1944, format=33, usage=0x3, hasCallbackStream=0, hasYuv2Stream=0

GoogleCamera Photo 模式配流
09-13 14:26:02.391   516   872 D Cam3HWI : 933, configureStreams: :hal3: stream 1: stream_type=4, chn_type=1, w=2592, h=1944, format=35, usage=0x3, hasCallbackStream=0, hasYuv2Stream=1
```## Nova GoogleCamera拍照没有ISO

```text
void camera_local_set_exif_iso_value(cmr_handle oem_handle, cmr_u32 iso_value) {
    struct camera_context *cxt = (struct camera_context *)oem_handle;
    struct setting_context *setting_cxt = &cxt->setting_cxt;
    CMR_LOGD("exif iso_value:%d", iso_value);
    cmr_sensor_set_exif(cxt->sn_cxt.sensor_handle, cxt->camera_id,
                        SENSOR_EXIF_CTRL_ISOSPEEDRATINGS,
                        iso_value);
    cmr_sensor_set_exif(cxt->sn_cxt.sensor_handle, cxt->camera_id,
                        SENSOR_EXIF_CTRL_WHITEBALANCE,
                        setting_cxt->awb_cmd_value);
}

09-14 09:34:43.444   515  7187 D cmr_oem : 21166, camera_local_set_exif_iso_value: exif iso_value:250

//GoogleCamera
09-14 09:38:29.128   515  7328 D cmr_setting: 3118, setting_get_appmode: get appmode -1

//DreamCamera2
09-14 09:38:30.668   515   862 D cmr_setting: 3118, setting_get_appmode: get appmode 0
09-14 09:38:30.719   515   870 D cmr_setting: 3118, setting_get_appmode: get appmode 0
09-14 09:38:30.745   515   870 D cmr_setting: 3118, setting_get_appmode: get appmode 1


ret = cmr_setting_ioctl(cxt->setting_cxt.setting_handle, SETTING_GET_APPMODE,
                        &setting_param);
if (setting_param.cmd_type_value != -1) {
    camera_get_iso_info(oem_handle, &iso_value);
    camera_local_set_exif_iso_value(oem_handle, iso_value);
    if(!cxt->long_expo_enable) {
        camera_get_adgain_exp_info(oem_handle, &exp_info);
        camera_local_set_exif_exp_time(oem_handle, exp_info.exp_time);
    }
}

cmr_setting.c
static cmr_int setting_get_appmode(struct setting_component *cpt,
                                   struct setting_cmd_parameter *parm) {
    cmr_int ret = 0;
    struct setting_hal_param *hal_param = get_hal_param(cpt, parm->camera_id);

    parm->cmd_type_value = hal_param->app_mode;
    CMR_LOGD("get appmode %ld", parm->cmd_type_value);

    return ret;
}

09-14 09:34:43.421   515   857 D Cam3OEMIf: 10054, SetCameraParaTag: getCaptureState: SPRD_PREVIEW_IN_PROGRESS,  mSprdAppmodeId:0
09-14 09:34:43.421   515   857 D cmr_setting: 2357, setting_set_appmode: setting_set_appmode=0

09-14 09:55:09.582   515   857 D cmr_oem : 13423, camera_isp_ioctl: set app mode id = 1

09-14 09:56:39.861   515   870 D cmr_setting: 2357, setting_set_appmode: setting_set_appmode=-1

SprdCamera3OEMIf.cpp
    case ANDROID_SPRD_APP_MODE_ID: {
        SPRD_DEF_Tag *sprddefInfo;
        int8_t drvSceneMode = 0;
        sprddefInfo = mSetting->getSPRDDEFTagPTR();
        mSprdAppmodeId = sprddefInfo->sprd_appmode_id;
        HAL_LOGD("getCaptureState: %s,  mSprdAppmodeId:%d",
                 getCameraStateStr(getPreviewState()), mSprdAppmodeId);

        if (sprddefInfo->capture_mode > 1) {
            mSprdAppmodeId = sprddefInfo->sprd_appmode_id = CAMERA_MODE_CONTINUE;
            mSprd3dnrType = CAMERA_3DNR_TYPE_NULL;
            SET_PARM(mHalOem, mCameraHandle, CAMERA_PARAM_SPRD_3DNR_TYPE,
                         mSprd3dnrType);
            HAL_LOGV("capture_mode: %d", sprddefInfo->capture_mode);
        }

09-14 10:00:40.055   515   870 D Cam3OEMIf: 10054, SetCameraParaTag: getCaptureState: SPRD_IDLE,  mSprdAppmodeId:0
09-14 10:00:40.209   515   857 D Cam3OEMIf: 10054, SetCameraParaTag: getCaptureState: SPRD_INTERNAL_PREVIEW_REQUESTED,  mSprdAppmodeId:0
09-14 10:00:40.260   515   857 D Cam3OEMIf: 10054, SetCameraParaTag: getCaptureState: SPRD_INTERNAL_PREVIEW_REQUESTED,  mSprdAppmodeId:0
09-14 10:00:40.550   515   857 D Cam3OEMIf: 10054, SetCameraParaTag: getCaptureState: SPRD_PREVIEW_IN_PROGRESS,  mSprdAppmodeId:0

09-14 10:00:47.696   515   857 D Cam3OEMIf: 10054, SetCameraParaTag: getCaptureState: SPRD_IDLE,  mSprdAppmodeId:-1
09-14 10:00:47.880   515   857 D Cam3OEMIf: 10054, SetCameraParaTag: getCaptureState: SPRD_INTERNAL_PREVIEW_REQUESTED,  mSprdAppmodeId:-1
09-14 10:00:47.938   515   857 D Cam3OEMIf: 10054, SetCameraParaTag: getCaptureState: SPRD_INTERNAL_PREVIEW_REQUESTED,  mSprdAppmodeId:-1
09-14 10:00:47.973   515   857 D Cam3OEMIf: 10054, SetCameraParaTag: getCaptureState: SPRD_INTERNAL_PREVIEW_REQUESTED,  mSprdAppmodeId:-1
09-14 10:00:48.255   515   857 D Cam3OEMIf: 10054, SetCameraParaTag: getCaptureState: SPRD_PREVIEW_IN_PROGRESS,  mSprdAppmodeId:-1

09-14 12:47:49.449   515   857 D cmr_oem : 13423, camera_isp_ioctl: set app mode id = 9

提交记录
http://192.168.3.79:8084/#/c/81800/
```## ImageFormat

```text
https://blog.csdn.net/qq_42194101/article/details/120148390

ImageFormat/PixelFormat         Value                 HAL Pixel Format                     Value
ImageFormat.JPEG             256 (0x00000100)     HAL_PIXEL_FORMAT_BLOB                 33
ImageFormat.DEPTH_POINT_CLOUD 257 (0x00000101)     HAL_PIXEL_FORMAT_BLOB                 33
ImageFormat.DEPTH_JPEG         1768253795 (0x69656963) HAL_PIXEL_FORMAT_BLOB                 33
ImageFormat.HEIC             1212500294 (0x48454946) HAL_PIXEL_FORMAT_BLOB                 33
ImageFormat.DEPTH16             1144402265 (0x44363159) HAL_PIXEL_FORMAT_Y16                 540422489
ImageFormat.RAW_DEPTH         4098(0x1002)         HAL_PIXEL_FORMAT_RAW16                 32
ImageFormat.RAW_SENSOR         32 (0x00000020)         HAL_PIXEL_FORMAT_RAW16                 32
ImageFormat.RAW_PRIVATE         36 (0x00000024)         HAL_PIXEL_FORMAT_RAW_OPAQUE             36
ImageFormat.RAW10             37 (0x00000025)         HAL_PIXEL_FORMAT_RAW10                 37
ImageFormat.RAW12             38 (0x00000026)         HAL_PIXEL_FORMAT_RAW12                 38
ImageFormat.PRIVATE             34 (0x00000022)         HAL_PIXEL_FORMAT_IMPLEMENTATION_DEFINED 34

ImageFormat.YUV_420_888         35 (0x00000023)         HAL_PIXEL_FORMAT_YCBCR_420_888         35
ImageFormat.YV12             842094169 (0x32315659) HAL_PIXEL_FORMAT_YV12                 842094169
ImageFormat.NV21             17 (0x00000011)         HAL_PIXEL_FORMAT_YCRCB_420_SP         17
ImageFormat.NV16             16 (0x00000010)         HAL_PIXEL_FORMAT_YCBCR_422_SP         16
ImageFormat.YUY2             20 (0x00000014)         HAL_PIXEL_FORMAT_YCBCR_422_I         20
ImageFormat.Y8                 538982489 (0x20203859) HAL_PIXEL_FORMAT_Y8                     538982489
ImageFormat.YCBCR_P010         54 (0x00000036)         HAL_PIXEL_FORMAT_YCBCR_P010             54

PixelFormat.RGBA_8888         1 (0x00000001)         HAL_PIXEL_FORMAT_RGBA_8888             1
PixelFormat.RGBX_8888         2 (0x00000002)         HAL_PIXEL_FORMAT_RGBX_8888             2
PixelFormat.RGB_888             3 (0x00000003)         HAL_PIXEL_FORMAT_RGB_888             3
PixelFormat.RGB_565             4 (0x00000004)         HAL_PIXEL_FORMAT_RGB_565             4
Not Supported                 NA                     HAL_PIXEL_FORMAT_BGRA_8888             5
PixelFormat.RGBA_F16         22 (0x00000016)         HAL_PIXEL_FORMAT_RGBA_FP16             22
PixelFormat.RGBA_1010102     43 (0x0000002b)         HAL_PIXEL_FORMAT_RGBA_1010102         43
```## DreamCamera人像模式打开失败

```text
09-13 10:18:01.437   518  8750 D sns_drv_u: 5321, sensorGetPhyId4Role: can't find sensor_role 5 at facing 0

09-13 10:18:01.908   518  8673 E CamDev@3.2-impl-sprd: open: camera device session init failed
09-13 10:18:01.908   696  1166 E Camera3-Device: Camera 38: initialize: Could not open camera session: Function not implemented (-38)
09-13 10:18:01.908   696  1166 E Camera2ClientBase: initializeImpl: Camera 38: unable to initialize device: Function not implemented (-38)
09-13 10:18:01.908   696  1166 E CameraService: connectHelper: Could not initialize client from HAL.
09-13 10:18:01.908   696  1166 I Camera3-Device: disconnectImpl: E
09-13 10:18:01.908   696  1166 I hw-BpHwBinder: onLastStrongRef automatically unlinking death recipients
09-13 10:18:01.910  8333  8645 I CAM_CameraActivity Drea: onCameraAvailable requestPending=false
09-13 10:18:01.910   696  1166 I CameraService: disconnect: Disconnected client for camera 38 for PID 8333
09-13 10:18:01.910   696  1166 I Camera2ClientBase: Closed Camera 38. Client was: com.android.camera2 (PID 8333, UID 10147)
09-13 10:18:01.910   696  1166 I Camera3-Device: disconnectImpl: E
09-13 10:18:01.912  8333  8367 I CAM2PORT_DispatchThread: DispatchThread.this.notifyAll()!
09-13 10:18:01.912  8333  8368 I CAM2PORT_DispatchThread: DispatchThread.this.wait end!
09-13 10:18:01.912  8333  8367 E CAM2PORT_AndCam2AgntImp: Camera device '38' encountered error code '4'
09-13 10:18:01.917  8333  8645 W CAM_CameraActivity Drea: Camera open failure: HIST_ID38_-1_1_302_305_803_805_802_204_106_711_102_204_204_204_461_462_204_502_303_204_103_711_302_305_803_802_805_303_461_463_2_1_2_1_302_305_803_805_802_204_106_711_102_204_204_204_461_462_204_502_303_204_103_711_302_305_803_802_805_303_461_463_2_1_HEND
09-13 10:18:01.918  8333  8333 E CAM_FatalErrorHandler: Handling Camera Open Failure:
09-13 10:18:01.918  8333  8333 E CAM_FatalErrorHandler: java.lang.Exception
09-13 10:18:01.918  8333  8333 E CAM_FatalErrorHandler:  at com.android.camera.FatalErrorHandlerImpl.onCameraOpenFailure(FatalErrorHandlerImpl.java:49)
09-13 10:18:01.918  8333  8333 E CAM_FatalErrorHandler:  at com.android.camera.CameraActivity$9.run(CameraActivity.java:609)
09-13 10:18:01.918  8333  8333 E CAM_FatalErrorHandler:  at android.os.Handler.handleCallback(Handler.java:938)
09-13 10:18:01.918  8333  8333 E CAM_FatalErrorHandler:  at android.os.Handler.dispatchMessage(Handler.java:99)
09-13 10:18:01.918  8333  8333 E CAM_FatalErrorHandler:  at android.os.Looper.loopOnce(Looper.java:201)
09-13 10:18:01.918  8333  8333 E CAM_FatalErrorHandler:  at android.os.Looper.loop(Looper.java:288)
09-13 10:18:01.918  8333  8333 E CAM_FatalErrorHandler:  at android.app.ActivityThread.main(ActivityThread.java:7941)
09-13 10:18:01.918  8333  8333 E CAM_FatalErrorHandler:  at java.lang.reflect.Method.invoke(Native Method)
09-13 10:18:01.918  8333  8333 E CAM_FatalErrorHandler:  at com.android.internal.os.RuntimeInit$MethodAndArgsCaller.run(RuntimeInit.java:553)
09-13 10:18:01.918  8333  8333 E CAM_FatalErrorHandler:  at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:1003)
09-13 10:18:01.918  8333  8333 E CAM_CameraUtil: Show fatal error dialog

vendor/sprd/modules/libcamera/sensor/sensor_drv_u.c

会不会是 sensor_list.xml 配置的问题？
```## NOVA录像无声

```text
[FAQ202275378]单mic项目录像无声音

[QUESTION]
硬件上只有主mic无辅mic，录像选择辅mic录像无声音

[ANSWER]
参考如下配置，如果是smart pa的话，配置在同目录的名字带smart_pa的xml中修改。

/device/sprd/对应项目/对应工程/rootdir/system/etc/audio_policy_config/primary_audio_policy_configuration.xml
@@ -5,7 +5,6 @@
     <item>Speaker</item>
     <item>Earpiece</item>
     <item>Built-In Mic</item>
-    <item>Built-In Back Mic</item>
   </attachedDevices>
   <defaultOutputDevice>Speaker</defaultOutputDevice>
   <mixPorts>
@@ -72,11 +71,6 @@
           samplingRates="8000,11025,12000,16000,22050,24000,32000,44100,48000"
           channelMasks="AUDIO_CHANNEL_IN_MONO,AUDIO_CHANNEL_IN_STEREO,AUDIO_CHANNEL_IN_FRONT_BACK"/>
     </devicePort>
-    <devicePort tagName="Built-In Back Mic" type="AUDIO_DEVICE_IN_BACK_MIC" role="source">
-      <profile name="" format="AUDIO_FORMAT_PCM_16_BIT"
-           samplingRates="8000,11025,12000,16000,22050,24000,32000,44100,48000"
-           channelMasks="AUDIO_CHANNEL_IN_MONO,AUDIO_CHANNEL_IN_STEREO,AUDIO_CHANNEL_IN_FRONT_BACK"/>
-    </devicePort>
     <devicePort tagName="Wired Headset Mic" type="AUDIO_DEVICE_IN_WIRED_HEADSET" role="source">
       <profile name="" format="AUDIO_FORMAT_PCM_16_BIT"
           samplingRates="8000,11025,12000,16000,22050,24000,32000,44100,48000"
@@ -108,9 +102,9 @@
     <route type="mix" sink="BT SCO Car Kit"
        sources="primary output,Telephony Rx"/>
     <route type="mix" sink="primary input"
-        sources="Built-In Mic,Built-In Back Mic,Wired Headset Mic,BT SCO Headset Mic"/>
+        sources="Built-In Mic,Wired Headset Mic,BT SCO Headset Mic"/>
     <route type="mix" sink="Telephony Tx"
-        sources="Built-In Mic,Built-In Back Mic,Wired Headset Mic,BT SCO Headset Mic"/>
+        sources="Built-In Mic,Wired Headset Mic,BT SCO Headset Mic"/>
     <route type="mix" sink="voice_rx"
        sources="Telephony Rx"/>
   </routes>
/vendor/etc/primary_audio_policy_configuration.xml
/vendor/etc/audio/sku_sprd/primary_audio_policy_configuration.xml
```## GoogleDialer 视频通话预览显示拉伸

```text
09-16 06:36:08.651  6099  6099 I DialerInCallCameraManager: com.android.incallui.cameramanager.InCallCameraManager.getActiveCameraId:99 getActiveCameraId
09-16 06:36:08.651  6099  6099 I DialerInCallCameraManager: com.android.incallui.cameramanager.InCallCameraManager.initializeCameraIds:122 begin
09-16 06:36:08.698  6099  6099 I DialerInCallCameraManager: com.android.incallui.cameramanager.InCallCameraManager.getHighestPriorityCamera:216 frontCamera: highest priority cameraId is 1, is logical multi camera: false
09-16 06:36:08.699  6099  6099 I DialerInCallCameraManager: com.android.incallui.cameramanager.InCallCameraManager.getHighestPriorityCamera:216 backCamera: highest priority cameraId is 0, is logical multi camera: false
09-16 06:36:08.700  6099  6099 I DialerInCallCameraManager: com.android.incallui.cameramanager.InCallCameraManager.getActiveCameraId:103 using front: 1
09-16 06:36:08.702  6099  6099 I DialerInCallCameraManager: com.android.incallui.cameramanager.InCallCameraManager.getActiveCameraId:99 getActiveCameraId
09-16 06:36:08.703  6099  6099 I DialerInCallCameraManager: com.android.incallui.cameramanager.InCallCameraManager.getActiveCameraId:103 using front: 1
09-16 06:36:08.705  6099  6099 I DialerInCallCameraManager: com.android.incallui.cameramanager.InCallCameraManager.getActiveCameraId:99 getActiveCameraId
09-16 06:36:08.706  6099  6099 I DialerInCallCameraManager: com.android.incallui.cameramanager.InCallCameraManager.getActiveCameraId:103 using front: 1
09-16 06:36:09.355   515   868 D Cam3HWI : 802, configureStreams: mZslIpsEnable 0
09-16 06:36:09.367   515   868 D Cam3HWI : 933, configureStreams: :hal3: stream 0: stream_type=1, chn_type=1, w=640, h=480, format=35, usage=0x3, hasCallbackStream=0, hasYuv2Stream=0
09-16 06:36:09.368   515   868 D Cam3HWI : 1042, configureStreams: slowmotion=1, high video mode = 0, kMaxBuffers=4
09-16 06:36:09.368   515   868 D Cam3HWI : 1087, configureStreams: stream type:1, max_buffers:4
09-16 06:36:09.368   515   868 D Cam3HWI : 1107, configureStreams: streamList->streams[0]->max_buffers 4
09-16 06:36:09.368   515   868 I Cam3HWI : 1127, configureStreams: :hal3: camId=1, prev: w=640, h=480, video: w=0, h=0, callback: w=0, h=0, yuv2: w=0, h=0, cap: w=0, h=0 yuv3: w=0, h=0,
09-16 06:36:09.389   515   868 D Cam3HWI : 1202, configureStreams: mMultiCameraMode :0
09-16 06:36:11.835  6099  6099 I DialerInCallCameraManager: com.android.incallui.cameramanager.InCallCameraManager.getActiveCameraId:99 getActiveCameraId
09-16 06:36:11.839  6099  6099 I DialerInCallCameraManager: com.android.incallui.cameramanager.InCallCameraManager.getActiveCameraId:103 using front: 1
09-16 06:36:11.860  6099  6099 I DialerInCallCameraManager: com.android.incallui.cameramanager.InCallCameraManager.getActiveCameraId:99 getActiveCameraId
09-16 06:36:11.860  6099  6099 I DialerInCallCameraManager: com.android.incallui.cameramanager.InCallCameraManager.getActiveCameraId:103 using front: 1
09-16 06:36:11.863  6099  6099 I DialerInCallCameraManager: com.android.incallui.cameramanager.InCallCameraManager.getActiveCameraId:99 getActiveCameraId
09-16 06:36:11.864  6099  6099 I DialerInCallCameraManager: com.android.incallui.cameramanager.InCallCameraManager.getActiveCameraId:103 using front: 1
09-16 06:36:11.867  6099  6099 I DialerInCallCameraManager: com.android.incallui.cameramanager.InCallCameraManager.chooseOptimalCameraPreviewSizeInternal:315 available preview sizes: [2592x1944, 2592x1458, 2592x1296, 2560x1920, 2560x1440, 2320x1740, 2304x1728, 2160x1080, 2048x1152, 1920x1080, 1920x1072, 1920x960, 1920x896, 1728x1728, 1600x1200, 1600x720, 1504x720, 1440x1080, 1474x720, 1280x720, 960x720, 720x720, 720x480, 640x480, 352x288, 320x240, 240x240, 304x144, 288x144, 256x144, 176x144] cameraSensorOrientationIsLandscape: true isUiLandscape: false
09-16 06:36:11.868  6099  6099 I DialerInCallCameraManager: com.android.incallui.cameramanager.InCallCameraManager.chooseOptimalCameraPreviewSizeInternal:322 swap w/h while camera's sensor coordinate is based on landscape mode but UI's orientation is portrait
09-16 06:36:11.868  6099  6099 I DialerInCallCameraManager: com.android.incallui.cameramanager.InCallCameraManager.chooseOptimalCameraPreviewSizeInternal:332 previewWidth: 1474, previewHeight: 720
09-16 06:36:11.870  6099  6099 I DialerInCallCameraManager: com.android.incallui.cameramanager.InCallCameraManager.chooseOptimalCameraPreviewSize:294 optimalPreviewSize: 1474x720
09-16 06:37:28.710   515   868 D Cam3HWI : 802, configureStreams: mZslIpsEnable 0
09-16 06:37:28.710   515   868 D Cam3HWI : 933, configureStreams: :hal3: stream 0: stream_type=1, chn_type=1, w=320, h=240, format=34, usage=0x20000803, hasCallbackStream=0, hasYuv2Stream=0
09-16 06:37:28.710   515   868 D Cam3HWI : 1042, configureStreams: slowmotion=1, high video mode = 0, kMaxBuffers=4
09-16 06:37:28.710   515   868 D Cam3HWI : 1087, configureStreams: stream type:1, max_buffers:4
09-16 06:37:28.710   515   868 D Cam3HWI : 1107, configureStreams: streamList->streams[0]->max_buffers 4
09-16 06:37:28.711   515   868 I Cam3HWI : 1127, configureStreams: :hal3: camId=1, prev: w=320, h=240, video: w=0, h=0, callback: w=0, h=0, yuv2: w=0, h=0, cap: w=0, h=0 yuv3: w=0, h=0,
09-16 06:37:28.712   515   868 D Cam3HWI : 1202, configureStreams: mMultiCameraMode :0
```## CIVIC PLUS性能

```text
CIVIC
09-07 10:05:06.917   704   704 I mtkcam-dev3-hidl: [0-hidl-session::open] TCT_PFM start up: HAL open: 9 ms
09-07 10:05:07.123   704   704 I mtkcam-dev3-hidl: [0-hidl-session::configureStreams_3_6] TCT_PFM start up: HAL configureStreams: 180 ms
09-07 10:05:07.309   704  3434 I mtkcam-dev3-hidl: [0-hidl-session::processCaptureResult] TCT_PFM frame: HAL Preview process done frame number 0: 154 ms
09-07 10:05:07.311   704  3434 I mtkcam-dev3-hidl: [0-hidl-session::processCaptureResult] TCT_PFM start up: HAL first Preview: 156 ms
09-07 10:05:07.314 11134 11155 I CameraApp: [TCT_PFM][Thread: mode thread] start_up application onCreate to activity onCreate 73860378 ms
09-07 10:05:07.314 11134 11155 I CameraApp: [TCT_PFM][Thread: mode thread] start_up t0 app activity onCreate to requestOpenCameraDevice 2 ms
09-07 10:05:07.314 11134 11155 I CameraApp: [TCT_PFM][Thread: mode thread] start_up t1 hal requestOpenCameraDevice to onCameraDeviceOpened 37 ms
09-07 10:05:07.314 11134 11155 I CameraApp: [TCT_PFM][Thread: mode thread] start_up t2 app onCameraDeviceOpened to requestConfigSession 1 ms
09-07 10:05:07.314 11134 11155 I CameraApp: [TCT_PFM][Thread: mode thread] start_up t3 hal requestConfigSession to onSessionConfigured 195 ms
09-07 10:05:07.314 11134 11155 I CameraApp: [TCT_PFM][Thread: mode thread] start_up t4 hal onSessionConfigured to onFirstPreviewAvailable 186 ms
09-07 10:05:07.314 11134 11155 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 421 ms
09-07 10:05:07.314 11134 11155 I CameraApp: [TCT_PFM][Thread: mode thread] start_up application onCreate to onFirstPreviewAvailable 73860799 ms
09-07 10:05:07.351   704  3434 I mtkcam-dev3-hidl: [0-hidl-session::processCaptureResult] TCT_PFM frame: HAL Preview process done frame number 1: 196 ms
09-07 10:05:07.352   704  3434 I mtkcam-dev3-hidl: [0-hidl-session::processCaptureResult] TCT_PFM frame: HAL Preview process done frame number 1: 197 ms
09-07 10:05:07.387   704  3434 I mtkcam-dev3-hidl: [0-hidl-session::processCaptureResult] TCT_PFM frame: HAL Preview process done frame number 2: 232 ms
09-07 10:05:07.387   704  3434 I mtkcam-dev3-hidl: [0-hidl-session::processCaptureResult] TCT_PFM frame: HAL Preview process done frame number 2: 233 ms
09-07 10:05:07.427   704  3434 I mtkcam-dev3-hidl: [0-hidl-session::processCaptureResult] TCT_PFM frame: HAL Preview process done frame number 3: 273 ms
09-07 10:05:07.429   704  3434 I mtkcam-dev3-hidl: [0-hidl-session::processCaptureResult] TCT_PFM frame: HAL Preview process done frame number 3: 275 ms
09-07 10:05:07.466   704  3434 I mtkcam-dev3-hidl: [0-hidl-session::processCaptureResult] TCT_PFM frame: HAL Preview process done frame number 4: 312 ms
09-07 10:05:07.468   704  3434 I mtkcam-dev3-hidl: [0-hidl-session::processCaptureResult] TCT_PFM frame: HAL Preview process done frame number 4: 313 ms
09-07 10:05:07.506   704  3434 I mtkcam-dev3-hidl: [0-hidl-session::processCaptureResult] TCT_PFM frame: HAL Preview process done frame number 5: 352 ms
09-07 10:05:07.508   704  3434 I mtkcam-dev3-hidl: [0-hidl-session::processCaptureResult] TCT_PFM frame: HAL Preview process done frame number 5: 353 ms



PLUS
09-06 00:08:27.193   982  6793 I mtkcam-dev3-hidl: [0-hidl-session::open] TCT_PFM start up: HAL open: 24 ms
09-06 00:08:27.582   982  6793 I mtkcam-dev3-hidl: [0-hidl-session::configureStreams_3_6] TCT_PFM start up: HAL configureStreams: 316 ms
09-06 00:08:27.849   982  1186 I mtkcam-dev3-hidl: [0-hidl-session::processCaptureResult] TCT_PFM frame: HAL Preview process done frame number 0: 224 ms
09-06 00:08:27.852   982  1186 I mtkcam-dev3-hidl: [0-hidl-session::processCaptureResult] TCT_PFM start up: HAL first Preview: 228 ms
09-06 00:08:27.854 27530 27558 I CameraApp: [TCT_PFM][Thread: mode thread] start_up application onCreate to activity onCreate 10952017 ms
09-06 00:08:27.854 27530 27558 I CameraApp: [TCT_PFM][Thread: mode thread] start_up t0 app activity onCreate to requestOpenCameraDevice 8 ms
09-06 00:08:27.854 27530 27558 I CameraApp: [TCT_PFM][Thread: mode thread] start_up t1 hal requestOpenCameraDevice to onCameraDeviceOpened 99 ms
09-06 00:08:27.854 27530 27558 I CameraApp: [TCT_PFM][Thread: mode thread] start_up t2 app onCameraDeviceOpened to requestConfigSession 2 ms
09-06 00:08:27.855 27530 27558 I CameraApp: [TCT_PFM][Thread: mode thread] start_up t3 hal requestConfigSession to onSessionConfigured 346 ms
09-06 00:08:27.855 27530 27558 I CameraApp: [TCT_PFM][Thread: mode thread] start_up t4 hal onSessionConfigured to onFirstPreviewAvailable 263 ms
09-06 00:08:27.855 27530 27558 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 718 ms
09-06 00:08:27.855 27530 27558 I CameraApp: [TCT_PFM][Thread: mode thread] start_up application onCreate to onFirstPreviewAvailable 10952735 ms
09-06 00:08:27.891   982  1186 I mtkcam-dev3-hidl: [0-hidl-session::processCaptureResult] TCT_PFM frame: HAL Preview process done frame number 1: 267 ms
09-06 00:08:27.893   982  1186 I mtkcam-dev3-hidl: [0-hidl-session::processCaptureResult] TCT_PFM frame: HAL Preview process done frame number 1: 268 ms
09-06 00:08:27.926   982  1186 I mtkcam-dev3-hidl: [0-hidl-session::processCaptureResult] TCT_PFM frame: HAL Preview process done frame number 2: 302 ms
09-06 00:08:27.928   982  1186 I mtkcam-dev3-hidl: [0-hidl-session::processCaptureResult] TCT_PFM frame: HAL Preview process done frame number 2: 304 ms
09-06 00:08:27.965   982  1186 I mtkcam-dev3-hidl: [0-hidl-session::processCaptureResult] TCT_PFM frame: HAL Preview process done frame number 3: 341 ms
09-06 00:08:27.967   982  1186 I mtkcam-dev3-hidl: [0-hidl-session::processCaptureResult] TCT_PFM frame: HAL Preview process done frame number 3: 342 ms
09-06 00:08:28.005   982  1186 I mtkcam-dev3-hidl: [0-hidl-session::processCaptureResult] TCT_PFM frame: HAL Preview process done frame number 4: 380 ms
09-06 00:08:28.007   982  1186 I mtkcam-dev3-hidl: [0-hidl-session::processCaptureResult] TCT_PFM frame: HAL Preview process done frame number 4: 383 ms
09-06 00:08:28.052   982  1186 I mtkcam-dev3-hidl: [0-hidl-session::processCaptureResult] TCT_PFM frame: HAL Preview process done frame number 5: 428 ms
09-06 00:08:28.055   982  1186 I mtkcam-dev3-hidl: [0-hidl-session::processCaptureResult] TCT_PFM frame: HAL Preview process done frame number 5: 431 ms

去掉Log之后
09-15 21:51:37.440  9494  9518 I CameraApp: [TCT_PFM][Thread: mode thread] start_up application onCreate to activity onCreate 331926 ms
09-15 21:51:37.440  9494  9518 I CameraApp: [TCT_PFM][Thread: mode thread] start_up t0 app activity onCreate to requestOpenCameraDevice 8 ms
09-15 21:51:37.440  9494  9518 I CameraApp: [TCT_PFM][Thread: mode thread] start_up t1 hal requestOpenCameraDevice to onCameraDeviceOpened 61 ms
09-15 21:51:37.440  9494  9518 I CameraApp: [TCT_PFM][Thread: mode thread] start_up t2 app onCameraDeviceOpened to requestConfigSession 3 ms
09-15 21:51:37.440  9494  9518 I CameraApp: [TCT_PFM][Thread: mode thread] start_up t3 hal requestConfigSession to onSessionConfigured 300 ms
09-15 21:51:37.440  9494  9518 I CameraApp: [TCT_PFM][Thread: mode thread] start_up t4 hal onSessionConfigured to onFirstPreviewAvailable 204 ms
09-15 21:51:37.440  9494  9518 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 576 ms
09-15 21:51:37.440  9494  9518 I CameraApp: [TCT_PFM][Thread: mode thread] start_up application onCreate to onFirstPreviewAvailable 332502 ms


CRUZE
12-27 17:40:04.629 18119 18151 I CameraApp: [TCT_PFM][Thread: mode thread] start_up application onCreate to activity onCreate 21226 ms
12-27 17:40:04.629 18119 18151 I CameraApp: [TCT_PFM][Thread: mode thread] start_up t0 app activity onCreate to requestOpenCameraDevice 12 ms
12-27 17:40:04.629 18119 18151 I CameraApp: [TCT_PFM][Thread: mode thread] start_up t1 hal requestOpenCameraDevice to onCameraDeviceOpened 39 ms
12-27 17:40:04.629 18119 18151 I CameraApp: [TCT_PFM][Thread: mode thread] start_up t2 app onCameraDeviceOpened to requestConfigSession 1 ms
12-27 17:40:04.629 18119 18151 I CameraApp: [TCT_PFM][Thread: mode thread] start_up t3 hal requestConfigSession to onSessionConfigured 81 ms
12-27 17:40:04.629 18119 18151 I CameraApp: [TCT_PFM][Thread: mode thread] start_up t4 hal onSessionConfigured to onFirstPreviewAvailable 272 ms
12-27 17:40:04.629 18119 18151 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 405 ms
12-27 17:40:04.629 18119 18151 I CameraApp: [TCT_PFM][Thread: mode thread] start_up application onCreate to onFirstPreviewAvailable 21631 ms


configureStreams 阶段
09-06 00:22:57.969   982  6217 D mtkcam-dev3-hidl: [0-hidl-session::configureStreams_3_6] +
09-06 00:22:57.970   982  6217 D mtkcam-dev3: [0-session::tryRunCommandLocked] Run command onConfigureStreamsLocked +
09-06 00:22:57.970   982  6217 D mtkcam-dev3: [0-session::onConfigureStreamsLocked] +
09-06 00:22:57.970   982  6217 D mtkcam-dev3: [0-session::onConfigureStreamsLocked] Enter CPU full run mode, timeout: 3000 ms

这里就有280ms

09-06 00:22:58.250   982  6217 E mtkcam-dev3: [0-session::onConfigureStreamsLocked] alphaxiang debug pixel arraysize: 4096x3072 (onConfigureStreamsLocked){#1063:vendor/mediatek/proprietary/hardware/mtkcam3/main/hal/device/3.x/device/CameraDevice3SessionImpl.cpp}
09-06 00:22:58.250   982  6217 E mtkcam-dev3: [0-session::onConfigureStreamsLocked] alphaxiang debug Need resomaic :0 (onConfigureStreamsLocked){#1081:vendor/mediatek/proprietary/hardware/mtkcam3/main/hal/device/3.x/device/CameraDevice3SessionImpl.cpp}
09-06 00:22:58.286   982  6217 D mtkcam-dev3: [0-session::onConfigureStreamsLocked] halMaxBufferSize=12 HalStream.maxBuffers=12
09-06 00:22:58.286   982  6217 D mtkcam-dev3: [0-session::onConfigureStreamsLocked] halMaxBufferSize=12 HalStream.maxBuffers=12
09-06 00:22:58.286   982  6217 D mtkcam-dev3: [0-session::onConfigureStreamsLocked] [setConfigMap] mImageConfigMap.size()=2, mMetaConfigMap.size()=1
09-06 00:22:58.286   982  6217 D mtkcam-AppStreamMgr: [AppMgr-configureStreams]  0  960x720  OUT ImgFormat:0x32315659(YV12) BufPlanes(strides/sizeInBytes):[ 960/691200 480/172800 480/200960 ] startOffset:0 bufStep:0 t:0/r:0 maxBuffers:12 d/s:0x00000000(UNKNOWN) s0:d0:App:YV12:0|HW_TEXTURE|HW_COMPOSER AllocImgFormat:0x32315659(YV12) AllocBufPlanes(strides/sizeInBytes):[ 960/691200 480/172800 480/200960 ] Real:0x32315659(YV12) Request:0x22(IMPLEMENTATION_DEFINED) Override:0x32315659(YV12) Hal-Client-usage:0x900(0|HW_TEXTURE|HW_COMPOSER) Hal-usage:0x20033(0|SW_READ_OFTEN|SW_WRITE_OFTEN|HW_CAMERA_WRITE) HalStream::(consumer/producer)Usage:0/0x20033 0xb40000759b9f5500 phy:-1
09-06 00:22:58.286   982  6217 D mtkcam-AppStreamMgr: [AppMgr-configureStreams]  0x1 4096x3072 OUT ImgFormat:0x11(NV21) BufPlanes(strides/sizeInBytes):[ 4096/12582912 4096/6299648 ] startOffset:0 bufStep:0 t:0/r:0 maxBuffers:12 d/s:0x08c20000(V0_JFIF|STANDARD_BT601_625|TRANSFER_SMPTE_170M|RANGE_FULL) s1:d0:App:YCrCb_420_SP:0|SW_READ_OFTEN AllocImgFormat:0x11(NV21) AllocBufPlanes(strides/sizeInBytes):[ 4096/12582912 4096/6299648 ] Real:0x11(YCrCb_420_SP) Request:0x23(YCbCr_420_888) Override:0x23(YCbCr_420_888) Hal-Client-usage:0x3(0|SW_READ_OFTEN) Hal-usage:0x20033(0|SW_READ_OFTEN|SW_WRITE_OFTEN|HW_CAMERA_WRITE) HalStream::(consumer/producer)Usage:0/0x20033 0xb4000075a867f600 phy:-1
09-06 00:22:58.286   982  6217 D mtkcam-dev3: [0-session::onConfigureStreamsLocked] -
09-06 00:22:58.286   982  6217 I mtkcam-dev3: [0-session::tryRunCommandLocked] Run command onConfigureStreamsLocked -
09-06 00:22:58.292   982  6217 I mtkcam-dev3-hidl: [0-hidl-session::configureStreams_3_6] TCT_PFM start up: HAL configureStreams: 322 ms
09-06 00:22:58.293   982  6217 D mtkcam-dev3-hidl: [0-hidl-session::configureStreams_3_6] -
09-06 00:22:58.293 27530 27561 W com.tcl.camera: Long monitor contention with owner CameraScheduleThread (27560) at boolean android.hardware.camera2.impl.CameraDeviceImpl.configureStreamsChecked(android.hardware.camera2.params.InputConfiguration, java.util.List, int, android.hardware.camera2.CaptureRequest, long)(CameraDeviceImpl.java:576) waiters=0 in void android.hardware.camera2.impl.CameraDeviceImpl$4.run() for 336ms
```## TCL 性能分析: 搜索关键字 TCT_PFM

```text
冷热启动：搜索log "start_up total activity onCreate to onFirstPreviewAvailable"
adb logcat -c && adb logcat | grep -E "timeSpent|start_up total"

热启动(700)：
CIVIC
08-31 11:27:15.159 25089 25198 I CameraApp: [TCT_PFM][Thread: mode thread] start_up application onCreate to activity onCreate 5118547 ms
08-31 11:27:15.159 25089 25198 I CameraApp: [TCT_PFM][Thread: mode thread] start_up t0 app activity onCreate to requestOpenCameraDevice 4 ms
08-31 11:27:15.159 25089 25198 I CameraApp: [TCT_PFM][Thread: mode thread] start_up t1 hal requestOpenCameraDevice to onCameraDeviceOpened 37 ms
08-31 11:27:15.159 25089 25198 I CameraApp: [TCT_PFM][Thread: mode thread] start_up t2 app onCameraDeviceOpened to requestConfigSession 1 ms
08-31 11:27:15.159 25089 25198 I CameraApp: [TCT_PFM][Thread: mode thread] start_up t3 hal requestConfigSession to onSessionConfigured 200 ms
08-31 11:27:15.159 25089 25198 I CameraApp: [TCT_PFM][Thread: mode thread] start_up t4 hal onSessionConfigured to onFirstPreviewAvailable 199 ms
08-31 11:27:15.159 25089 25198 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 441 ms
08-31 11:27:15.159 25089 25198 I CameraApp: [TCT_PFM][Thread: mode thread] start_up application onCreate to onFirstPreviewAvailable 5118988 ms

CIVICPL
08-30 00:47:00.394 10839 10872 I CameraApp: [TCT_PFM][Thread: mode thread] start_up application onCreate to activity onCreate 412665 ms
08-30 00:47:00.394 10839 10872 I CameraApp: [TCT_PFM][Thread: mode thread] start_up t0 app activity onCreate to requestOpenCameraDevice 6 ms
08-30 00:47:00.394 10839 10872 I CameraApp: [TCT_PFM][Thread: mode thread] start_up t1 hal requestOpenCameraDevice to onCameraDeviceOpened 50 ms
08-30 00:47:00.394 10839 10872 I CameraApp: [TCT_PFM][Thread: mode thread] start_up t2 app onCameraDeviceOpened to requestConfigSession 3 ms
08-30 00:47:00.394 10839 10872 I CameraApp: [TCT_PFM][Thread: mode thread] start_up t3 hal requestConfigSession to onSessionConfigured 342 ms
08-30 00:47:00.394 10839 10872 I CameraApp: [TCT_PFM][Thread: mode thread] start_up t4 hal onSessionConfigured to onFirstPreviewAvailable 221 ms
08-30 00:47:00.394 10839 10872 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 622 ms
08-30 00:47:00.394 10839 10872 I CameraApp: [TCT_PFM][Thread: mode thread] start_up application onCreate to onFirstPreviewAvailable 413287 ms

09-15 00:54:35.460  9249  9283 I CameraApp: [TCT_PFM][Thread: mode thread] start_up application onCreate to activity onCreate 36815 ms
09-15 00:54:35.460  9249  9283 I CameraApp: [TCT_PFM][Thread: mode thread] start_up t0 app activity onCreate to requestOpenCameraDevice 9 ms
09-15 00:54:35.460  9249  9283 I CameraApp: [TCT_PFM][Thread: mode thread] start_up t1 hal requestOpenCameraDevice to onCameraDeviceOpened 60 ms
09-15 00:54:35.460  9249  9283 I CameraApp: [TCT_PFM][Thread: mode thread] start_up t2 app onCameraDeviceOpened to requestConfigSession 2 ms
09-15 00:54:35.460  9249  9283 I CameraApp: [TCT_PFM][Thread: mode thread] start_up t3 hal requestConfigSession to onSessionConfigured 349 ms
09-15 00:54:35.460  9249  9283 I CameraApp: [TCT_PFM][Thread: mode thread] start_up t4 hal onSessionConfigured to onFirstPreviewAvailable 362 ms
09-15 00:54:35.460  9249  9283 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 782 ms
09-15 00:54:35.460  9249  9283 I CameraApp: [TCT_PFM][Thread: mode thread] start_up application onCreate to onFirstPreviewAvailable 37597 ms

比较两组数据，CIVICPL 的 requestConfigSession to onSessionConfigured 这一阶段的时间比 CIVIC 的时间要多 100+ms


冷启动(900)：
08-29 07:35:35.719  6426  6452 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 533 ms
08-29 07:35:43.722 30485 30509 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 690 ms
08-29 07:36:05.742 30784 30807 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 583 ms
08-29 07:36:11.405 31076 31100 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 584 ms
08-29 07:36:14.812 31367 31394 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 516 ms
08-29 07:36:17.547 31658 31681 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 571 ms
08-29 07:36:21.916 31948 31972 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 533 ms
08-29 07:36:24.576 32235 32259 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 481 ms
08-29 07:36:27.394 32523 32546 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 492 ms
08-29 07:36:29.912   358   406 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 629 ms
08-29 07:36:32.886  1052  1182 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 583 ms
08-29 07:36:36.203  1501  1525 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 576 ms

前后摄切换(700)：搜索
adb logcat -c && echo "cleaned" && adb logcat | grep "back_front_switch front_to_back total"

CIVICPL
08-30 01:41:59.213 10839 10872 I CameraApp: [TCT_PFM][Thread: mode thread] back_front_switch front_to_back t0 Touch switch icon to requestOpenCameraDevice 3 ms
08-30 01:41:59.213 10839 10872 I CameraApp: [TCT_PFM][Thread: mode thread] back_front_switch front_to_back t1 hal requestOpenCameraDevice to onCameraDeviceOpened 255 ms
08-30 01:41:59.213 10839 10872 I CameraApp: [TCT_PFM][Thread: mode thread] back_front_switch front_to_back t2 app onCameraDeviceOpened to requestConfigSession 2 ms
08-30 01:41:59.213 10839 10872 I CameraApp: [TCT_PFM][Thread: mode thread] back_front_switch front_to_back t3 hal requestConfigSession to onSessionConfigured 310 ms
08-30 01:41:59.213 10839 10872 I CameraApp: [TCT_PFM][Thread: mode thread] back_front_switch front_to_back t4 hal onSessionConfigured to onFirstPreviewAvailable 197 ms
08-30 01:41:59.213 10839 10872 I CameraApp: [TCT_PFM][Thread: mode thread] back_front_switch front_to_back total Touch switch icon to onFirstPreviewAvailable 767 ms

CIVIC
08-31 12:18:24.162 30433 30461 I CameraApp: [TCT_PFM][Thread: mode thread] back_front_switch front_to_back t0 Touch switch icon to requestOpenCameraDevice 3 ms
08-31 12:18:24.162 30433 30461 I CameraApp: [TCT_PFM][Thread: mode thread] back_front_switch front_to_back t1 hal requestOpenCameraDevice to onCameraDeviceOpened 208 ms
08-31 12:18:24.162 30433 30461 I CameraApp: [TCT_PFM][Thread: mode thread] back_front_switch front_to_back t2 app onCameraDeviceOpened to requestConfigSession 1 ms
08-31 12:18:24.162 30433 30461 I CameraApp: [TCT_PFM][Thread: mode thread] back_front_switch front_to_back t3 hal requestConfigSession to onSessionConfigured 196 ms
08-31 12:18:24.162 30433 30461 I CameraApp: [TCT_PFM][Thread: mode thread] back_front_switch front_to_back t4 hal onSessionConfigured to onFirstPreviewAvailable 168 ms
08-31 12:18:24.162 30433 30461 I CameraApp: [TCT_PFM][Thread: mode thread] back_front_switch front_to_back total Touch switch icon to onFirstPreviewAvailable 576 ms

相比两组数据看到 "requestConfigSession to onSessionConfigured" 阶段差异较大，CIVICPL - CIVIC > 100ms


切换到人像模式(1050)：搜索log "module_switch 1 to 3 total"
CIVICPL
08-30 01:45:47.260 10839 10872 I CameraApp: [TCT_PFM][Thread: mode thread] module_switch 1 to 3 t0 Touch module icon to requestOpenCameraDevice 8 ms
08-30 01:45:47.260 10839 10872 I CameraApp: [TCT_PFM][Thread: mode thread] module_switch 1 to 3 t1 hal requestOpenCameraDevice to onCameraDeviceOpened 281 ms
08-30 01:45:47.260 10839 10872 I CameraApp: [TCT_PFM][Thread: mode thread] module_switch 1 to 3 t2 app onCameraDeviceOpened to requestConfigSession 0 ms
08-30 01:45:47.260 10839 10872 I CameraApp: [TCT_PFM][Thread: mode thread] module_switch 1 to 3 t3 hal requestConfigSession to onSessionConfigured 352 ms
08-30 01:45:47.260 10839 10872 I CameraApp: [TCT_PFM][Thread: mode thread] module_switch 1 to 3 t4 hal onSessionConfigured to onFirstPreviewAvailable 483 ms
08-30 01:45:47.260 10839 10872 I CameraApp: [TCT_PFM][Thread: mode thread] module_switch 1 to 3 total Touch switch icon to onFirstPreviewAvailable 1124 ms

08-30 01:45:53.839 10839 10872 I CameraApp: [TCT_PFM][Thread: mode thread] module_switch 1 to 3 t0 Touch module icon to requestOpenCameraDevice 7 ms
08-30 01:45:53.839 10839 10872 I CameraApp: [TCT_PFM][Thread: mode thread] module_switch 1 to 3 t1 hal requestOpenCameraDevice to onCameraDeviceOpened 297 ms
08-30 01:45:53.839 10839 10872 I CameraApp: [TCT_PFM][Thread: mode thread] module_switch 1 to 3 t2 app onCameraDeviceOpened to requestConfigSession 0 ms
08-30 01:45:53.839 10839 10872 I CameraApp: [TCT_PFM][Thread: mode thread] module_switch 1 to 3 t3 hal requestConfigSession to onSessionConfigured 338 ms
08-30 01:45:53.839 10839 10872 I CameraApp: [TCT_PFM][Thread: mode thread] module_switch 1 to 3 t4 hal onSessionConfigured to onFirstPreviewAvailable 491 ms
08-30 01:45:53.839 10839 10872 I CameraApp: [TCT_PFM][Thread: mode thread] module_switch 1 to 3 total Touch switch icon to onFirstPreviewAvailable 1133 ms

CIVIC
08-31 12:26:03.369 30433 30461 I CameraApp: [TCT_PFM][Thread: mode thread] module_switch 1 to 3 t0 Touch module icon to requestOpenCameraDevice 45 ms
08-31 12:26:03.369 30433 30461 I CameraApp: [TCT_PFM][Thread: mode thread] module_switch 1 to 3 t1 hal requestOpenCameraDevice to onCameraDeviceOpened 252 ms
08-31 12:26:03.369 30433 30461 I CameraApp: [TCT_PFM][Thread: mode thread] module_switch 1 to 3 t2 app onCameraDeviceOpened to requestConfigSession 1 ms
08-31 12:26:03.369 30433 30461 I CameraApp: [TCT_PFM][Thread: mode thread] module_switch 1 to 3 t3 hal requestConfigSession to onSessionConfigured 286 ms
08-31 12:26:03.369 30433 30461 I CameraApp: [TCT_PFM][Thread: mode thread] module_switch 1 to 3 t4 hal onSessionConfigured to onFirstPreviewAvailable 386 ms
08-31 12:26:03.369 30433 30461 I CameraApp: [TCT_PFM][Thread: mode thread] module_switch 1 to 3 total Touch switch icon to onFirstPreviewAvailable 970 ms

08-31 12:26:11.518 30433 30461 I CameraApp: [TCT_PFM][Thread: mode thread] module_switch 1 to 3 t0 Touch module icon to requestOpenCameraDevice 7 ms
08-31 12:26:11.518 30433 30461 I CameraApp: [TCT_PFM][Thread: mode thread] module_switch 1 to 3 t1 hal requestOpenCameraDevice to onCameraDeviceOpened 232 ms
08-31 12:26:11.518 30433 30461 I CameraApp: [TCT_PFM][Thread: mode thread] module_switch 1 to 3 t2 app onCameraDeviceOpened to requestConfigSession 2 ms
08-31 12:26:11.518 30433 30461 I CameraApp: [TCT_PFM][Thread: mode thread] module_switch 1 to 3 t3 hal requestConfigSession to onSessionConfigured 255 ms
08-31 12:26:11.518 30433 30461 I CameraApp: [TCT_PFM][Thread: mode thread] module_switch 1 to 3 t4 hal onSessionConfigured to onFirstPreviewAvailable 349 ms
08-31 12:26:11.518 30433 30461 I CameraApp: [TCT_PFM][Thread: mode thread] module_switch 1 to 3 total Touch switch icon to onFirstPreviewAvailable 845 ms

requestConfigSession to onSessionConfigured
onSessionConfigured to onFirstPreviewAvailable
以上两个阶段差异较大


退出相机：



createCaptureRequest called: templateType = PREVIEW
```## PLUS性能数据

```text
冷启动 :
adb logcat -c && echo "cleaned" && adb logcat | grep -E "timeSpent|start_up total"

09-16 05:04:44.393  1978  1978 D TclLauncher3: TLauncher # onPause() timeSpent:1 com.tcl.android.launcher.Launcher@7e9daa8
09-16 05:04:45.165 23337 23360 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 656 ms
772

09-16 05:05:01.976  1978  1978 D TclLauncher3: TLauncher # onPause() timeSpent:1 com.tcl.android.launcher.Launcher@7e9daa8
09-16 05:05:02.832 23705 23729 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 714 ms
856

09-16 05:05:06.812  1978  1978 D TclLauncher3: TLauncher # onPause() timeSpent:0 com.tcl.android.launcher.Launcher@7e9daa8
09-16 05:05:07.599 24016 24039 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 646 ms
787

09-16 05:05:10.572  1978  1978 D TclLauncher3: TLauncher # onPause() timeSpent:0 com.tcl.android.launcher.Launcher@7e9daa8
09-16 05:05:11.337 24291 24314 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 652 ms
765

09-16 05:05:16.795  1978  1978 D TclLauncher3: TLauncher # onPause() timeSpent:1 com.tcl.android.launcher.Launcher@7e9daa8
09-16 05:05:17.574 24607 24630 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 652 ms
779

09-16 05:05:22.627  1978  1978 D TclLauncher3: TLauncher # onPause() timeSpent:0 com.tcl.android.launcher.Launcher@7e9daa8
09-16 05:05:23.490 24880 24904 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 684 ms
863

09-16 05:05:26.248  1978  1978 D TclLauncher3: TLauncher # onPause() timeSpent:0 com.tcl.android.launcher.Launcher@7e9daa8
09-16 05:05:27.200 25155 25179 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 767 ms
952

09-16 05:05:30.059  1978  1978 D TclLauncher3: TLauncher # onPause() timeSpent:0 com.tcl.android.launcher.Launcher@7e9daa8
09-16 05:05:31.001 25429 25453 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 759 ms
942

09-16 05:05:34.225  1978  1978 D TclLauncher3: TLauncher # onPause() timeSpent:1 com.tcl.android.launcher.Launcher@7e9daa8
09-16 05:05:35.171 25735 25759 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 770 ms
946

09-16 05:05:41.189  1978  1978 D TclLauncher3: TLauncher # onPause() timeSpent:0 com.tcl.android.launcher.Launcher@7e9daa8
09-16 05:05:42.126 26047 26071 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 741 ms
937

09-16 05:05:45.570  1978  1978 D TclLauncher3: TLauncher # onPause() timeSpent:1 com.tcl.android.launcher.Launcher@7e9daa8
09-16 05:05:46.542 26357 26382 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 742 ms
972

09-16 05:06:06.312  1978  1978 D TclLauncher3: TLauncher # onPause() timeSpent:1 com.tcl.android.launcher.Launcher@7e9daa8
09-16 05:06:07.207 26742 26766 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 729 ms
895

09-16 05:06:28.584  1978  1978 D TclLauncher3: TLauncher # onPause() timeSpent:1 com.tcl.android.launcher.Launcher@7e9daa8
09-16 05:06:29.513 27094 27117 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 758 ms
929

09-16 05:06:39.518  1978  1978 D TclLauncher3: TLauncher # onPause() timeSpent:1 com.tcl.android.launcher.Launcher@7e9daa8
09-16 05:06:40.410 27447 27471 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 739 ms
892

09-16 05:06:50.421  1978  1978 D TclLauncher3: TLauncher # onPause() timeSpent:0 com.tcl.android.launcher.Launcher@7e9daa8
09-16 05:06:51.329 27779 27803 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 750 ms
908





热启动 :
adb logcat -c && adb logcat | grep -E "timeSpent|start_up total"

09-16 05:08:39.996  1978  1978 D TclLauncher3: TLauncher # onPause() timeSpent:1 com.tcl.android.launcher.Launcher@7e9daa8
09-16 05:08:40.688 28573 28597 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 656 ms
672ms

09-16 05:08:43.251  1978  1978 D TclLauncher3: TLauncher # onPause() timeSpent:0 com.tcl.android.launcher.Launcher@7e9daa8
09-16 05:08:43.901 28573 28597 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 608 ms
650ms

09-16 05:08:47.545  1978  1978 D TclLauncher3: TLauncher # onPause() timeSpent:0 com.tcl.android.launcher.Launcher@7e9daa8
09-16 05:08:48.340 28573 28597 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 588 ms
795ms

09-16 05:08:50.413  1978  1978 D TclLauncher3: TLauncher # onPause() timeSpent:1 com.tcl.android.launcher.Launcher@7e9daa8
09-16 05:08:51.123 28573 28597 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 674 ms
710ms

09-16 05:08:52.950  1978  1978 D TclLauncher3: TLauncher # onPause() timeSpent:0 com.tcl.android.launcher.Launcher@7e9daa8
09-16 05:08:53.598 28573 28597 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 613 ms
648ms

09-16 05:08:55.393  1978  1978 D TclLauncher3: TLauncher # onPause() timeSpent:0 com.tcl.android.launcher.Launcher@7e9daa8
09-16 05:08:56.038 28573 28597 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 611 ms
645ms

09-16 05:08:58.335  1978  1978 D TclLauncher3: TLauncher # onPause() timeSpent:1 com.tcl.android.launcher.Launcher@7e9daa8
09-16 05:08:59.102 28573 28597 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 585 ms
767ms

09-16 05:09:00.877  1978  1978 D TclLauncher3: TLauncher # onPause() timeSpent:1 com.tcl.android.launcher.Launcher@7e9daa8
09-16 05:09:01.549 28573 28597 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 629 ms
672ms

09-16 05:09:03.496  1978  1978 D TclLauncher3: TLauncher # onPause() timeSpent:0 com.tcl.android.launcher.Launcher@7e9daa8
09-16 05:09:04.164 28573 28597 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 632 ms
668ms

09-16 05:09:05.948  1978  1978 D TclLauncher3: TLauncher # onPause() timeSpent:1 com.tcl.android.launcher.Launcher@7e9daa8
09-16 05:09:06.687 28573 28597 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 704 ms
739ms




前摄->后摄 :
adb logcat -c && echo "cleaned" && adb logcat | grep "back_front_switch front_to_back total"

09-16 05:13:52.245 28573 28597 I CameraApp: [TCT_PFM][Thread: mode thread] back_front_switch front_to_back total Touch switch icon to onFirstPreviewAvailable 766 ms
09-16 05:13:54.273 28573 28597 I CameraApp: [TCT_PFM][Thread: mode thread] back_front_switch front_to_back total Touch switch icon to onFirstPreviewAvailable 783 ms
09-16 05:13:55.886 28573 28597 I CameraApp: [TCT_PFM][Thread: mode thread] back_front_switch front_to_back total Touch switch icon to onFirstPreviewAvailable 790 ms
09-16 05:13:58.593 28573 28597 I CameraApp: [TCT_PFM][Thread: mode thread] back_front_switch front_to_back total Touch switch icon to onFirstPreviewAvailable 772 ms
09-16 05:14:00.199 28573 28597 I CameraApp: [TCT_PFM][Thread: mode thread] back_front_switch front_to_back total Touch switch icon to onFirstPreviewAvailable 785 ms
09-16 05:14:01.834 28573 28597 I CameraApp: [TCT_PFM][Thread: mode thread] back_front_switch front_to_back total Touch switch icon to onFirstPreviewAvailable 784 ms
09-16 05:14:03.549 28573 28597 I CameraApp: [TCT_PFM][Thread: mode thread] back_front_switch front_to_back total Touch switch icon to onFirstPreviewAvailable 795 ms
09-16 05:14:05.304 28573 28597 I CameraApp: [TCT_PFM][Thread: mode thread] back_front_switch front_to_back total Touch switch icon to onFirstPreviewAvailable 766 ms
09-16 05:14:07.041 28573 28597 I CameraApp: [TCT_PFM][Thread: mode thread] back_front_switch front_to_back total Touch switch icon to onFirstPreviewAvailable 782 ms
09-16 05:14:08.573 28573 28597 I CameraApp: [TCT_PFM][Thread: mode thread] back_front_switch front_to_back total Touch switch icon to onFirstPreviewAvailable 779 ms
09-16 05:14:10.154 28573 28597 I CameraApp: [TCT_PFM][Thread: mode thread] back_front_switch front_to_back total Touch switch icon to onFirstPreviewAvailable 779 ms
09-16 05:14:11.919 28573 28597 I CameraApp: [TCT_PFM][Thread: mode thread] back_front_switch front_to_back total Touch switch icon to onFirstPreviewAvailable 777 ms
09-16 05:14:13.638 28573 28597 I CameraApp: [TCT_PFM][Thread: mode thread] back_front_switch front_to_back total Touch switch icon to onFirstPreviewAvailable 774 ms
09-16 05:14:15.374 28573 28597 I CameraApp: [TCT_PFM][Thread: mode thread] back_front_switch front_to_back total Touch switch icon to onFirstPreviewAvailable 776 ms





退出相机 ： 
adb logcat -c && echo "cleaned" && adb logcat | grep -E "KeyButtonView: sendEvent: mCode =4, button event = ACTION_UP|TLauncher # onWindowFocusChanged\(\) hasFocus:true"

09-16 05:24:36.609  1574  1574 I KeyButtonView: sendEvent: mCode =4, button event = ACTION_UP
09-16 05:24:36.832  1978  1978 D TclLauncher3: TLauncher # onWindowFocusChanged() hasFocus:true
223ms

09-16 05:25:02.876  1574  1574 I KeyButtonView: sendEvent: mCode =4, button event = ACTION_UP
09-16 05:25:03.118  1978  1978 D TclLauncher3: TLauncher # onWindowFocusChanged() hasFocus:true
232ms

09-16 05:25:05.440  1574  1574 I KeyButtonView: sendEvent: mCode =4, button event = ACTION_UP
09-16 05:25:05.632  1978  1978 D TclLauncher3: TLauncher # onWindowFocusChanged() hasFocus:true
192ms

09-16 05:26:13.224  1574  1574 I KeyButtonView: sendEvent: mCode =4, button event = ACTION_UP
09-16 05:26:13.428  1978  1978 D TclLauncher3: TLauncher # onWindowFocusChanged() hasFocus:true
204ms

09-16 05:26:43.880  1574  1574 I KeyButtonView: sendEvent: mCode =4, button event = ACTION_UP
09-16 05:26:44.124  1978  1978 D TclLauncher3: TLauncher # onWindowFocusChanged() hasFocus:true
244ms

09-16 05:26:59.391  1574  1574 I KeyButtonView: sendEvent: mCode =4, button event = ACTION_UP
09-16 05:26:59.552  1978  1978 D TclLauncher3: TLauncher # onWindowFocusChanged() hasFocus:true
161ms

09-16 05:27:02.678  1574  1574 I KeyButtonView: sendEvent: mCode =4, button event = ACTION_UP
09-16 05:27:02.896  1978  1978 D TclLauncher3: TLauncher # onWindowFocusChanged() hasFocus:true
218ms

09-16 05:27:06.497  1574  1574 I KeyButtonView: sendEvent: mCode =4, button event = ACTION_UP
09-16 05:27:06.703  1978  1978 D TclLauncher3: TLauncher # onWindowFocusChanged() hasFocus:true
206ms

09-16 05:27:09.589  1574  1574 I KeyButtonView: sendEvent: mCode =4, button event = ACTION_UP
09-16 05:27:09.791  1978  1978 D TclLauncher3: TLauncher # onWindowFocusChanged() hasFocus:true
202ms

09-16 05:27:13.690  1574  1574 I KeyButtonView: sendEvent: mCode =4, button event = ACTION_UP
09-16 05:27:13.881  1978  1978 D TclLauncher3: TLauncher # onWindowFocusChanged() hasFocus:true
191ms

09-16 05:27:17.701  1574  1574 I KeyButtonView: sendEvent: mCode =4, button event = ACTION_UP
09-16 05:27:17.880  1978  1978 D TclLauncher3: TLauncher # onWindowFocusChanged() hasFocus:true
179ms

09-16 05:27:21.644  1574  1574 I KeyButtonView: sendEvent: mCode =4, button event = ACTION_UP
09-16 05:27:21.829  1978  1978 D TclLauncher3: TLauncher # onWindowFocusChanged() hasFocus:true
185ms





切换到人像模式(1050)
adb logcat -c && echo "cleaned" && adb logcat | grep -E "module_switch 1 to 3 total"

09-16 10:19:36.601 25853 25878 I CameraApp: [TCT_PFM][Thread: mode thread] module_switch 1 to 3 total Touch switch icon to onFirstPreviewAvailable 1078 ms
09-16 10:19:41.802 25853 25878 I CameraApp: [TCT_PFM][Thread: mode thread] module_switch 1 to 3 total Touch switch icon to onFirstPreviewAvailable 1087 ms
09-16 10:19:47.239 25853 25878 I CameraApp: [TCT_PFM][Thread: mode thread] module_switch 1 to 3 total Touch switch icon to onFirstPreviewAvailable 1074 ms
09-16 10:19:50.797 25853 25878 I CameraApp: [TCT_PFM][Thread: mode thread] module_switch 1 to 3 total Touch switch icon to onFirstPreviewAvailable 1063 ms
09-16 10:19:53.662 25853 25878 I CameraApp: [TCT_PFM][Thread: mode thread] module_switch 1 to 3 total Touch switch icon to onFirstPreviewAvailable 1073 ms
09-16 10:20:01.560 25853 25878 I CameraApp: [TCT_PFM][Thread: mode thread] module_switch 1 to 3 total Touch switch icon to onFirstPreviewAvailable 1021 ms
09-16 10:20:08.457 25853 25878 I CameraApp: [TCT_PFM][Thread: mode thread] module_switch 1 to 3 total Touch switch icon to onFirstPreviewAvailable 1007 ms
09-16 10:20:12.177 25853 25878 I CameraApp: [TCT_PFM][Thread: mode thread] module_switch 1 to 3 total Touch switch icon to onFirstPreviewAvailable 1059 ms
09-16 10:20:15.235 25853 25878 I CameraApp: [TCT_PFM][Thread: mode thread] module_switch 1 to 3 total Touch switch icon to onFirstPreviewAvailable 1051 ms
09-16 10:20:17.693 25853 25878 I CameraApp: [TCT_PFM][Thread: mode thread] module_switch 1 to 3 total Touch switch icon to onFirstPreviewAvailable 945 ms
09-16 10:20:27.820 25853 25878 I CameraApp: [TCT_PFM][Thread: mode thread] module_switch 1 to 3 total Touch switch icon to onFirstPreviewAvailable 1013 ms
09-16 10:20:32.401 25853 25878 I CameraApp: [TCT_PFM][Thread: mode thread] module_switch 1 to 3 total Touch switch icon to onFirstPreviewAvailable 1003 ms
09-16 10:20:42.457 25853 25878 I CameraApp: [TCT_PFM][Thread: mode thread] module_switch 1 to 3 total Touch switch icon to onFirstPreviewAvailable 1000 ms
```## 换成13M的模组

```text
Cold:
09-20 04:32:03.148  1973  1973 D TclLauncher3: TLauncher # onPause() timeSpent:1 com.tcl.android.launcher.Launcher@248a0c9
09-20 04:32:03.896 10663 10688 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 551 ms
No.1 spend : 748 ms, avg : 748
09-20 04:32:09.933  1973  1973 D TclLauncher3: TLauncher # onPause() timeSpent:1 com.tcl.android.launcher.Launcher@248a0c9
09-20 04:32:10.781 10904 10929 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 628 ms
No.2 spend : 848 ms, avg : 798
09-20 04:32:14.268  1973  1973 D TclLauncher3: TLauncher # onPause() timeSpent:0 com.tcl.android.launcher.Launcher@248a0c9
09-20 04:32:14.999 11180 11207 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 524 ms
No.3 spend : 731 ms, avg : 775
09-20 04:32:18.010  1973  1973 D TclLauncher3: TLauncher # onPause() timeSpent:0 com.tcl.android.launcher.Launcher@248a0c9
09-20 04:32:18.818 11418 11443 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 625 ms
No.4 spend : 808 ms, avg : 783
09-20 04:32:22.085  1973  1973 D TclLauncher3: TLauncher # onPause() timeSpent:1 com.tcl.android.launcher.Launcher@248a0c9
09-20 04:32:22.886 11655 11680 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 628 ms
No.5 spend : 801 ms, avg : 787
09-20 04:32:27.166  1973  1973 D TclLauncher3: TLauncher # onPause() timeSpent:1 com.tcl.android.launcher.Launcher@248a0c9
09-20 04:32:27.988 11892 11917 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 626 ms
No.6 spend : 822 ms, avg : 793
09-20 04:32:32.662  1973  1973 D TclLauncher3: TLauncher # onPause() timeSpent:1 com.tcl.android.launcher.Launcher@248a0c9
No.7 spend : 778 ms, avg : 790
09-20 04:32:33.440 12130 12157 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 588 ms
09-20 04:32:36.754  1973  1973 D TclLauncher3: TLauncher # onPause() timeSpent:1 com.tcl.android.launcher.Launcher@248a0c9
No.8 spend : 759 ms, avg : 786
09-20 04:32:37.513 12367 12393 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 575 ms
09-20 04:32:40.823  1973  1973 D TclLauncher3: TLauncher # onPause() timeSpent:0 com.tcl.android.launcher.Launcher@248a0c9
09-20 04:32:41.516 12604 12630 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 517 ms
No.9 spend : 693 ms, avg : 776
09-20 04:32:44.183  1973  1973 D TclLauncher3: TLauncher # onPause() timeSpent:0 com.tcl.android.launcher.Launcher@248a0c9
No.10 spend : 758 ms, avg : 774

Hot:
09-20 04:34:41.973  1973  1973 D TclLauncher3: TLauncher # onPause() timeSpent:0 com.tcl.android.launcher.Launcher@248a0c9
09-20 04:34:42.631 12845 12870 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 624 ms
No.1 spend : 658 ms, avg : 658
09-20 04:34:44.910  1973  1973 D TclLauncher3: TLauncher # onPause() timeSpent:1 com.tcl.android.launcher.Launcher@248a0c9
09-20 04:34:45.476 12845 12870 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 535 ms
No.2 spend : 566 ms, avg : 612
09-20 04:34:47.485  1973  1973 D TclLauncher3: TLauncher # onPause() timeSpent:1 com.tcl.android.launcher.Launcher@248a0c9
09-20 04:34:48.134 12845 12870 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 619 ms
No.3 spend : 649 ms, avg : 624
09-20 04:34:49.986  1973  1973 D TclLauncher3: TLauncher # onPause() timeSpent:0 com.tcl.android.launcher.Launcher@248a0c9
09-20 04:34:50.521 12845 12870 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 508 ms
No.4 spend : 535 ms, avg : 602
09-20 04:34:52.597  1973  1973 D TclLauncher3: TLauncher # onPause() timeSpent:0 com.tcl.android.launcher.Launcher@248a0c9
09-20 04:34:53.195 12845 12870 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 498 ms
No.5 spend : 598 ms, avg : 601
09-20 04:34:55.159  1973  1973 D TclLauncher3: TLauncher # onPause() timeSpent:1 com.tcl.android.launcher.Launcher@248a0c9
09-20 04:34:55.778 12845 12870 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 592 ms
No.6 spend : 619 ms, avg : 604
09-20 04:34:57.901  1973  1973 D TclLauncher3: TLauncher # onPause() timeSpent:1 com.tcl.android.launcher.Launcher@248a0c9
09-20 04:34:58.519 12845 12870 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 590 ms
No.7 spend : 618 ms, avg : 606
09-20 04:35:00.434  1973  1973 D TclLauncher3: TLauncher # onPause() timeSpent:0 com.tcl.android.launcher.Launcher@248a0c9
09-20 04:35:01.045 12845 12870 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 584 ms
No.8 spend : 611 ms, avg : 606
09-20 04:35:03.029  1973  1973 D TclLauncher3: TLauncher # onPause() timeSpent:0 com.tcl.android.launcher.Launcher@248a0c9
09-20 04:35:03.603 12845 12870 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 539 ms
No.9 spend : 574 ms, avg : 603
09-20 04:35:05.948  1973  1973 D TclLauncher3: TLauncher # onPause() timeSpent:0 com.tcl.android.launcher.Launcher@248a0c9
09-20 04:35:06.603 12845 12870 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 629 ms
No.10 spend : 655 ms, avg : 608
09-20 04:35:09.686  1973  1973 D TclLauncher3: TLauncher # onPause() timeSpent:1 com.tcl.android.launcher.Launcher@248a0c9
09-20 04:35:10.318 12845 12870 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 602 ms
No.11 spend : 632 ms, avg : 610
09-20 04:35:12.522  1973  1973 D TclLauncher3: TLauncher # onPause() timeSpent:0 com.tcl.android.launcher.Launcher@248a0c9
09-20 04:35:13.080 12845 12870 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 525 ms
No.12 spend : 558 ms, avg : 606
09-20 04:35:16.288  1973  1973 D TclLauncher3: TLauncher # onPause() timeSpent:1 com.tcl.android.launcher.Launcher@248a0c9
09-20 04:35:17.050 12845 12870 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 597 ms
No.13 spend : 762 ms, avg : 618


前摄->后摄:
09-20 04:44:01.053 12845 12870 I CameraApp: [TCT_PFM][Thread: mode thread] back_front_switch front_to_back total Touch switch icon to onFirstPreviewAvailable 620 ms
09-20 04:44:03.327 12845 12870 I CameraApp: [TCT_PFM][Thread: mode thread] back_front_switch front_to_back total Touch switch icon to onFirstPreviewAvailable 638 ms
09-20 04:44:05.437 12845 12870 I CameraApp: [TCT_PFM][Thread: mode thread] back_front_switch front_to_back total Touch switch icon to onFirstPreviewAvailable 608 ms
09-20 04:44:06.980 12845 12870 I CameraApp: [TCT_PFM][Thread: mode thread] back_front_switch front_to_back total Touch switch icon to onFirstPreviewAvailable 626 ms
09-20 04:44:08.235 12845 12870 I CameraApp: [TCT_PFM][Thread: mode thread] back_front_switch front_to_back total Touch switch icon to onFirstPreviewAvailable 611 ms
09-20 04:44:09.504 12845 12870 I CameraApp: [TCT_PFM][Thread: mode thread] back_front_switch front_to_back total Touch switch icon to onFirstPreviewAvailable 603 ms
09-20 04:44:10.993 12845 12870 I CameraApp: [TCT_PFM][Thread: mode thread] back_front_switch front_to_back total Touch switch icon to onFirstPreviewAvailable 616 ms
09-20 04:44:12.347 12845 12870 I CameraApp: [TCT_PFM][Thread: mode thread] back_front_switch front_to_back total Touch switch icon to onFirstPreviewAvailable 671 ms
09-20 04:44:13.798 12845 12870 I CameraApp: [TCT_PFM][Thread: mode thread] back_front_switch front_to_back total Touch switch icon to onFirstPreviewAvailable 646 ms
09-20 04:44:15.053 12845 12870 I CameraApp: [TCT_PFM][Thread: mode thread] back_front_switch front_to_back total Touch switch icon to onFirstPreviewAvailable 612 ms
09-20 04:44:16.349 12845 12870 I CameraApp: [TCT_PFM][Thread: mode thread] back_front_switch front_to_back total Touch switch icon to onFirstPreviewAvailable 633 ms
09-20 04:44:17.855 12845 12870 I CameraApp: [TCT_PFM][Thread: mode thread] back_front_switch front_to_back total Touch switch icon to onFirstPreviewAvailable 615 ms
09-20 04:44:19.298 12845 12870 I CameraApp: [TCT_PFM][Thread: mode thread] back_front_switch front_to_back total Touch switch icon to onFirstPreviewAvailable 614 ms


切换到人像模式(1050)
adb logcat -c && echo "cleaned" && adb logcat | grep -E "module_switch 1 to 3 total"

人像模式打不开

退出相机 ： 
adb logcat -c && echo "cleaned" && adb logcat | grep -E "KeyButtonView: sendEvent: mCode =4, button event = ACTION_UP|TLauncher # onWindowFocusChanged\(\) hasFocus:true"

09-20 04:49:02.114  1565  1565 I KeyButtonView: sendEvent: mCode =4, button event = ACTION_UP
09-20 04:49:02.315  1973  1973 D TclLauncher3: TLauncher # onWindowFocusChanged() hasFocus:true
09-20 04:49:04.369  1565  1565 I KeyButtonView: sendEvent: mCode =4, button event = ACTION_UP
09-20 04:49:04.545  1973  1973 D TclLauncher3: TLauncher # onWindowFocusChanged() hasFocus:true
09-20 04:49:05.829  1565  1565 I KeyButtonView: sendEvent: mCode =4, button event = ACTION_UP
09-20 04:49:06.068  1973  1973 D TclLauncher3: TLauncher # onWindowFocusChanged() hasFocus:true
09-20 04:49:08.262  1565  1565 I KeyButtonView: sendEvent: mCode =4, button event = ACTION_UP
09-20 04:49:08.491  1973  1973 D TclLauncher3: TLauncher # onWindowFocusChanged() hasFocus:true
09-20 04:49:09.823  1565  1565 I KeyButtonView: sendEvent: mCode =4, button event = ACTION_UP
09-20 04:49:10.147  1973  1973 D TclLauncher3: TLauncher # onWindowFocusChanged() hasFocus:true
09-20 04:49:11.533  1565  1565 I KeyButtonView: sendEvent: mCode =4, button event = ACTION_UP
09-20 04:49:11.835  1973  1973 D TclLauncher3: TLauncher # onWindowFocusChanged() hasFocus:true
09-20 04:49:13.279  1565  1565 I KeyButtonView: sendEvent: mCode =4, button event = ACTION_UP
09-20 04:49:13.584  1973  1973 D TclLauncher3: TLauncher # onWindowFocusChanged() hasFocus:true
09-20 04:49:14.795  1565  1565 I KeyButtonView: sendEvent: mCode =4, button event = ACTION_UP
09-20 04:49:14.992  1973  1973 D TclLauncher3: TLauncher # onWindowFocusChanged() hasFocus:true
09-20 04:49:16.245  1565  1565 I KeyButtonView: sendEvent: mCode =4, button event = ACTION_UP
09-20 04:49:16.464  1973  1973 D TclLauncher3: TLauncher # onWindowFocusChanged() hasFocus:true
09-20 04:49:17.641  1565  1565 I KeyButtonView: sendEvent: mCode =4, button event = ACTION_UP
09-20 04:49:17.848  1973  1973 D TclLauncher3: TLauncher # onWindowFocusChanged() hasFocus:true
09-20 04:49:18.955  1565  1565 I KeyButtonView: sendEvent: mCode =4, button event = ACTION_UP
09-20 04:49:19.145  1973  1973 D TclLauncher3: TLauncher # onWindowFocusChanged() hasFocus:true
09-20 04:49:20.188  1565  1565 I KeyButtonView: sendEvent: mCode =4, button event = ACTION_UP
09-20 04:49:20.377  1973  1973 D TclLauncher3: TLauncher # onWindowFocusChanged() hasFocus:true
09-20 04:49:22.349  1565  1565 I KeyButtonView: sendEvent: mCode =4, button event = ACTION_UP
09-20 04:49:22.604  1973  1973 D TclLauncher3: TLauncher # onWindowFocusChanged() hasFocus:true
09-20 04:49:24.213  1565  1565 I KeyButtonView: sendEvent: mCode =4, button event = ACTION_UP
09-20 04:49:24.497  1973  1973 D TclLauncher3: TLauncher # onWindowFocusChanged() hasFocus:true
09-20 04:49:26.484  1565  1565 I KeyButtonView: sendEvent: mCode =4, button event = ACTION_UP
09-20 04:49:26.756  1973  1973 D TclLauncher3: TLauncher # onWindowFocusChanged() hasFocus:true
09-20 04:49:28.387  1565  1565 I KeyButtonView: sendEvent: mCode =4, button event = ACTION_UP
09-20 04:49:28.680  1973  1973 D TclLauncher3: TLauncher # onWindowFocusChanged() hasFocus:true
```## 去掉自校准

```text
Cold:
09-24 01:00:48.419  1965  1965 D TclLauncher3: TLauncher # onPause() timeSpent:1 com.tcl.android.launcher.Launcher@4f5bace
09-24 01:00:49.118 11842 11866 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 559 ms
No.1 spend : 699 ms, avg : 699ms
09-24 01:00:53.042  1965  1965 D TclLauncher3: TLauncher # onPause() timeSpent:0 com.tcl.android.launcher.Launcher@4f5bace
09-24 01:00:53.725 12154 12178 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 559 ms
No.2 spend : 683 ms, avg : 691ms
09-24 01:00:57.085  1965  1965 D TclLauncher3: TLauncher # onPause() timeSpent:1 com.tcl.android.launcher.Launcher@4f5bace
09-24 01:00:57.798 12445 12470 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 549 ms
No.3 spend : 713 ms, avg : 698ms
09-24 01:01:02.671  1965  1965 D TclLauncher3: TLauncher # onPause() timeSpent:1 com.tcl.android.launcher.Launcher@4f5bace
09-24 01:01:03.405 12734 12761 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 577 ms
No.4 spend : 734 ms, avg : 707ms
09-24 01:01:17.415  1965  1965 D TclLauncher3: TLauncher # onPause() timeSpent:1 com.tcl.android.launcher.Launcher@4f5bace
09-24 01:01:18.186 13032 13057 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 621 ms
No.5 spend : 771 ms, avg : 720ms
09-24 01:01:22.691  1965  1965 D TclLauncher3: TLauncher # onPause() timeSpent:1 com.tcl.android.launcher.Launcher@4f5bace
09-24 01:01:23.382 13334 13359 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 546 ms
No.6 spend : 691 ms, avg : 715ms
09-24 01:01:27.180  1965  1965 D TclLauncher3: TLauncher # onPause() timeSpent:1 com.tcl.android.launcher.Launcher@4f5bace
09-24 01:01:27.884 13627 13651 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 583 ms
No.7 spend : 704 ms, avg : 713ms
09-24 01:01:31.454  1965  1965 D TclLauncher3: TLauncher # onPause() timeSpent:0 com.tcl.android.launcher.Launcher@4f5bace
09-24 01:01:32.219 13913 13937 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 633 ms
No.8 spend : 765 ms, avg : 720ms
09-24 01:01:35.956  1965  1965 D TclLauncher3: TLauncher # onPause() timeSpent:0 com.tcl.android.launcher.Launcher@4f5bace
09-24 01:01:36.654 14202 14226 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 574 ms
No.9 spend : 698 ms, avg : 717ms
09-24 01:01:40.258  1965  1965 D TclLauncher3: TLauncher # onPause() timeSpent:1 com.tcl.android.launcher.Launcher@4f5bace
09-24 01:01:40.929 14491 14514 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 548 ms
No.10 spend : 671 ms, avg : 712ms

Hot:
09-24 01:03:45.325  1965  1965 D TclLauncher3: TLauncher # onPause() timeSpent:1 com.tcl.android.launcher.Launcher@4f5bace
09-24 01:03:45.951 14491 14514 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 592 ms
No.1 spend : 626 ms, avg : 626ms
09-24 01:03:48.441  1965  1965 D TclLauncher3: TLauncher # onPause() timeSpent:2 com.tcl.android.launcher.Launcher@4f5bace
09-24 01:03:49.058 14491 14514 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 582 ms
No.2 spend : 617 ms, avg : 621ms
09-24 01:03:50.683  1965  1965 D TclLauncher3: TLauncher # onPause() timeSpent:1 com.tcl.android.launcher.Launcher@4f5bace
09-24 01:03:51.247 14491 14514 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 538 ms
No.3 spend : 564 ms, avg : 602ms
09-24 01:03:52.870  1965  1965 D TclLauncher3: TLauncher # onPause() timeSpent:1 com.tcl.android.launcher.Launcher@4f5bace
09-24 01:03:53.435 14491 14514 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 539 ms
No.4 spend : 565 ms, avg : 593ms
09-24 01:03:55.793  1965  1965 D TclLauncher3: TLauncher # onPause() timeSpent:0 com.tcl.android.launcher.Launcher@4f5bace
09-24 01:03:56.376 14491 14514 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 553 ms
No.5 spend : 583 ms, avg : 591ms
09-24 01:03:58.145  1965  1965 D TclLauncher3: TLauncher # onPause() timeSpent:1 com.tcl.android.launcher.Launcher@4f5bace
09-24 01:03:58.746 14491 14514 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 572 ms
No.6 spend : 601 ms, avg : 592ms
09-24 01:04:00.610  1965  1965 D TclLauncher3: TLauncher # onPause() timeSpent:1 com.tcl.android.launcher.Launcher@4f5bace
09-24 01:04:01.170 14491 14514 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 536 ms
No.7 spend : 560 ms, avg : 588ms
09-24 01:04:03.074  1965  1965 D TclLauncher3: TLauncher # onPause() timeSpent:1 com.tcl.android.launcher.Launcher@4f5bace
09-24 01:04:03.648 14491 14514 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 541 ms
No.8 spend : 574 ms, avg : 586ms
09-24 01:04:05.443  1965  1965 D TclLauncher3: TLauncher # onPause() timeSpent:0 com.tcl.android.launcher.Launcher@4f5bace
09-24 01:04:06.047 14491 14514 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 578 ms
No.9 spend : 604 ms, avg : 588ms
09-24 01:04:07.893  1965  1965 D TclLauncher3: TLauncher # onPause() timeSpent:0 com.tcl.android.launcher.Launcher@4f5bace
09-24 01:04:08.456 14491 14514 I CameraApp: [TCT_PFM][Thread: mode thread] start_up total activity onCreate to onFirstPreviewAvailable 527 ms
No.10 spend : 563 ms, avg : 585ms

前摄->后摄:                     adb logcat -c && echo "cleaned" && adb logcat | grep "back_front_switch front_to_back total"

09-24 01:05:01.719 14491 14514 I CameraApp: [TCT_PFM][Thread: mode thread] back_front_switch front_to_back total Touch switch icon to onFirstPreviewAvailable 667 ms
09-24 01:05:04.452 14491 14514 I CameraApp: [TCT_PFM][Thread: mode thread] back_front_switch front_to_back total Touch switch icon to onFirstPreviewAvailable 659 ms
09-24 01:05:05.817 14491 14514 I CameraApp: [TCT_PFM][Thread: mode thread] back_front_switch front_to_back total Touch switch icon to onFirstPreviewAvailable 660 ms
09-24 01:05:07.260 14491 14514 I CameraApp: [TCT_PFM][Thread: mode thread] back_front_switch front_to_back total Touch switch icon to onFirstPreviewAvailable 676 ms
09-24 01:05:08.722 14491 14514 I CameraApp: [TCT_PFM][Thread: mode thread] back_front_switch front_to_back total Touch switch icon to onFirstPreviewAvailable 709 ms
09-24 01:05:10.177 14491 14514 I CameraApp: [TCT_PFM][Thread: mode thread] back_front_switch front_to_back total Touch switch icon to onFirstPreviewAvailable 689 ms
09-24 01:05:11.593 14491 14514 I CameraApp: [TCT_PFM][Thread: mode thread] back_front_switch front_to_back total Touch switch icon to onFirstPreviewAvailable 677 ms
09-24 01:05:13.070 14491 14514 I CameraApp: [TCT_PFM][Thread: mode thread] back_front_switch front_to_back total Touch switch icon to onFirstPreviewAvailable 676 ms
09-24 01:05:14.559 14491 14514 I CameraApp: [TCT_PFM][Thread: mode thread] back_front_switch front_to_back total Touch switch icon to onFirstPreviewAvailable 674 ms
09-24 01:05:15.963 14491 14514 I CameraApp: [TCT_PFM][Thread: mode thread] back_front_switch front_to_back total Touch switch icon to onFirstPreviewAvailable 708 ms
09-24 01:05:17.625 14491 14514 I CameraApp: [TCT_PFM][Thread: mode thread] back_front_switch front_to_back total Touch switch icon to onFirstPreviewAvailable 671 ms

切换到人像模式(1050)             adb logcat -c && echo "cleaned" && adb logcat | grep -E "module_switch 1 to 3 total"

切换到人像模式再切回到Photo模式会卡住

退出相机 ： 
adb logcat -c && echo "cleaned" && adb logcat | grep -E "KeyButtonView: sendEvent: mCode =4, button event = ACTION_UP|TLauncher # onWindowFocusChanged\(\) hasFocus:true"

09-20 04:49:02.114  1565  1565 I KeyButtonView: sendEvent: mCode =4, button event = ACTION_UP
09-20 04:49:02.315  1973  1973 D TclLauncher3: TLauncher # onWindowFocusChanged() hasFocus:true
09-20 04:49:04.369  1565  1565 I KeyButtonView: sendEvent: mCode =4, button event = ACTION_UP
09-20 04:49:04.545  1973  1973 D TclLauncher3: TLauncher # onWindowFocusChanged() hasFocus:true
09-20 04:49:05.829  1565  1565 I KeyButtonView: sendEvent: mCode =4, button event = ACTION_UP
09-20 04:49:06.068  1973  1973 D TclLauncher3: TLauncher # onWindowFocusChanged() hasFocus:true
09-20 04:49:08.262  1565  1565 I KeyButtonView: sendEvent: mCode =4, button event = ACTION_UP
09-20 04:49:08.491  1973  1973 D TclLauncher3: TLauncher # onWindowFocusChanged() hasFocus:true
09-20 04:49:09.823  1565  1565 I KeyButtonView: sendEvent: mCode =4, button event = ACTION_UP
09-20 04:49:10.147  1973  1973 D TclLauncher3: TLauncher # onWindowFocusChanged() hasFocus:true
09-20 04:49:11.533  1565  1565 I KeyButtonView: sendEvent: mCode =4, button event = ACTION_UP
09-20 04:49:11.835  1973  1973 D TclLauncher3: TLauncher # onWindowFocusChanged() hasFocus:true
09-20 04:49:13.279  1565  1565 I KeyButtonView: sendEvent: mCode =4, button event = ACTION_UP
09-20 04:49:13.584  1973  1973 D TclLauncher3: TLauncher # onWindowFocusChanged() hasFocus:true
09-20 04:49:14.795  1565  1565 I KeyButtonView: sendEvent: mCode =4, button event = ACTION_UP
09-20 04:49:14.992  1973  1973 D TclLauncher3: TLauncher # onWindowFocusChanged() hasFocus:true
09-20 04:49:16.245  1565  1565 I KeyButtonView: sendEvent: mCode =4, button event = ACTION_UP
09-20 04:49:16.464  1973  1973 D TclLauncher3: TLauncher # onWindowFocusChanged() hasFocus:true
09-20 04:49:17.641  1565  1565 I KeyButtonView: sendEvent: mCode =4, button event = ACTION_UP
09-20 04:49:17.848  1973  1973 D TclLauncher3: TLauncher # onWindowFocusChanged() hasFocus:true
09-20 04:49:18.955  1565  1565 I KeyButtonView: sendEvent: mCode =4, button event = ACTION_UP
09-20 04:49:19.145  1973  1973 D TclLauncher3: TLauncher # onWindowFocusChanged() hasFocus:true
09-20 04:49:20.188  1565  1565 I KeyButtonView: sendEvent: mCode =4, button event = ACTION_UP
09-20 04:49:20.377  1973  1973 D TclLauncher3: TLauncher # onWindowFocusChanged() hasFocus:true
09-20 04:49:22.349  1565  1565 I KeyButtonView: sendEvent: mCode =4, button event = ACTION_UP
09-20 04:49:22.604  1973  1973 D TclLauncher3: TLauncher # onWindowFocusChanged() hasFocus:true
09-20 04:49:24.213  1565  1565 I KeyButtonView: sendEvent: mCode =4, button event = ACTION_UP
09-20 04:49:24.497  1973  1973 D TclLauncher3: TLauncher # onWindowFocusChanged() hasFocus:true
09-20 04:49:26.484  1565  1565 I KeyButtonView: sendEvent: mCode =4, button event = ACTION_UP
09-20 04:49:26.756  1973  1973 D TclLauncher3: TLauncher # onWindowFocusChanged() hasFocus:true
09-20 04:49:28.387  1565  1565 I KeyButtonView: sendEvent: mCode =4, button event = ACTION_UP
09-20 04:49:28.680  1973  1973 D TclLauncher3: TLauncher # onWindowFocusChanged() hasFocus:true
```## VILTE无法显示

```text
MTK VILTE流程
https://blog.csdn.net/u012545728/article/details/80549415

09-14 19:12:37.776497  1170  1306 E CameraService_proxy: Top task with package name: com.mediatek.ims not found!
09-14 19:12:37.776640  1170  1643 D FireUtil: notifySurfaceFlinger com.mediatek.ims,2,true
09-14 19:12:37.777277  1976  1976 I DialerImsVideoTech: com.android.incallui.videotech.ims.ImsVideoTech.isAvailable:103 available
09-14 19:12:37.777518  1976  1976 I DialerDialerCall: com.android.incallui.call.DialerCall.updateCallTiming:1292 state is already active
09-14 19:12:37.777854  1170  1629 D AudioSystem: +setParameters(): cameraFacing=front 
09-14 19:12:37.777880   553  1911 E SurfaceFlinger: Permission Denial: SurfaceFlinger did not recognize request code: 20009
09-14 19:12:37.777985   553  1911 I surfaceflinger: oneway function results for code 20009 on binder at 0xacf00110 will be dropped but finished with status PERMISSION_DENIED

09-14 19:12:37.854369   739 17703 I CamCalCamCal: ver1210~ sensorID=5035 deviceID=2
09-14 19:12:37.854442   739 17703 E CamCalCamCal: ver1210~Err:   283: Return ERROR ERR_NO_SHADING

09-14 19:12:37.885945   739  1156 I mtkcam-dev3-utils: [operator()] [addFrameDuration] format:34 size:1440x720 min_duration:33333333, stall_duration:0


public @Nullable TaskInfo getFrontTaskInfo(String packageName) {
    synchronized (mMapLock) {
        if (mTaskInfoMap.containsKey(packageName)) {
            return mTaskInfoMap.get(packageName);
        }
    }
    Log.e(TAG, "Top task with package name: " + packageName + " not found!");
    return null;
}


打电话前
09-27 15:29:39 : DISCONNECT device 1 client for package com.mediatek.ims (PID 3671)
09-27 15:29:20 : CONNECT device 1 client for package com.mediatek.ims (PID 3671)
打 vilte 之后
09-27 15:32:09 : CONNECT device 1 client for package com.mediatek.ims (PID 3671)
接通 vilte 之后
09-27 15:32:27 : DISCONNECT device 1 client for package com.mediatek.ims (PID 3671)


打开 Camera
09-27 15:32:27.264  3671 31164 D VT SRC - 1: [INT] [open] Start, id : 1 [13]
09-27 15:32:27.264  2216  2347 D AppOpsControllerImpl: Notifying of change in package com.google.android.dialer
09-27 15:32:27.265  3671 31165 D VT SRC - 1: [HDR] [handleMessage] MSG_OPEN_CAMERA [13]
09-27 15:32:27.265  3671 31165 D VT SRC - 1: [HDR] [openCamera] Start
09-27 15:32:27.265  3671 31165 W VT SRC - 1: open existing camera, ignore open!!!
09-27 15:32:27.265  3671 31164 D VT SRC - 1: [INT] [open] Finish [13]
09-27 15:32:27.265  3671 31164 D VT SRC - 1: [INT] [showMe]
09-27 15:32:27.265  3671 31164 I VT      : [JNI] Entering SetCamera
09-27 15:32:27.266   940 19845 I VT      : [SRV] [OPERATION][ID=1] setCamera (camera id 1)
09-27 15:32:27.266   940 19845 D [VT]ImsMa: [setCurrentCameraId]Line 2208 [ID=15][0xb4000077f8



09-27 15:32:27.273 10213 10213 W TelecomFramework: VideoCallImpl: setCamera: cameraId=null, calling=com.google.android.dialer           // 这里 cameraId 为什么会变为 null 呢？
09-27 15:32:27.273   692 31599 D VCodec  : [ProprietaryDevice] [INFO] driver create done.handle: 3964682240, 
09-27 15:32:27.274 10213 10213 I DialerInCallPresenter: com.android.incallui.InCallPresenter.setFullScreen:1658 setFullScreen: false
09-27 15:32:27.275   982 31413 E ResultPool: [convertToMetadata4AF] pre_cameramode:0, cameramode:0 (convertToMetadata4AF){#639:vendor/mediatek/proprietary/hardware/mtkcam/aaa/source/common/hal3a/v1.0/ResultPool/ResultPool.cpp}
09-27 15:32:27.275  2216 11600 E OpenGLRenderer: JankTracker::calculateLegacyJank expectedDequeueDuration > 0 expectedDequeueDuration=374284, DequeueBufferDuration=2510769, forgiveAmount=374284, totalDuration=11913894
09-27 15:32:27.275  1351  1351 I Telecom : VideoProviderProxy: IC->VP (callId=TC@15): setCamera: null callingPackage=com.google.android.dialer; callingUid=10149
09-27 15:32:27.276  1351  1351 I Telecom : InCallController: onSetCamera callId=TC@15, cameraId=null



关闭 Camera
09-27 15:32:27.340  3671 31164 D ImsVT   : [ID=1] [onSetDeviceOrientation] Finish
09-27 15:32:27.340  3671 31164 D ImsVT   : [ID=1] [onSetCamera] id : null

09-27 15:32:27.340  3671 31164 D VT SRC - 1: [INT] [close] Start [15]
09-27 15:32:27.340  1518  1537 W APM::AudioPolicyEngine: not found AUDIO_DEVICE_IN_PROXY1
09-27 15:32:27.340  3671 31165 D VT SRC - 1: [HDR] [handleMessage] MSG_CLOSE_CAMERA [15]
09-27 15:32:27.340  3671 31165 D VT SRC - 1: [HDR] [doCloseCamera] Start

09-27 15:32:27.376   982 31403 W mtkcam-AppStreamMgr: [1-FrameHandler::operator()] [Meta Stream Buffer] Error happens... - requestNo:495 streamId:0x100000024 App:Meta:DynamicP1_main1

09-27 15:32:27.375   982 31403 W mtkcam-AppStreamMgr: [1-FrameHandler::operator()] [Meta Stream Buffer] Error happens... - requestNo:491 streamId:0x100000027 App:Meta:DynamicP2

09-27 15:32:27.384   982 31403 W mtkcam-AppStreamMgr: [1-FrameHandler::updateCallback] requestNo 494 is removed before shutter callbacked, there MUST have error frames or meta be sent for the request
09-27 15:32:27.384   982 31403 W mtkcam-AppStreamMgr: [1-FrameHandler::updateCallback] requestNo 495 is removed before shutter callbacked, there MUST have error frames or meta be sent for the request


frameworks/base/telecomm/java/android/telecom/VideoCallImpl.java
public void setCamera(String cameraId) {
    try {
        Log.w(this, "setCamera: cameraId=%s, calling=%s", cameraId, mCallingPackageName);
        mVideoProvider.setCamera(cameraId, mCallingPackageName, mTargetSdkVersion);
    } catch (RemoteException e) {
    }
}


正常的 log
09-27 16:42:07.969  2544  2544 I TelecomFramework: TelephonyConnectionService: createConnection, callManagerAccount: ComponentInfo{com.android.phone/com.android.services.telephony.TelephonyConnectionService}, ***, UserHandle{0}, callId: TC@21_1, request: ConnectionRequest xxxxxxxxxxxxxxx Bundle[android.telecom.extra.INCOMING_CALL_ADDRESS=***, android.telecom.extra.CALL_SUBJECT=, android.telecom.extra.LOCATION=null, android.telecom.extra.PRIORITY=-1, android.telecom.extra.CALL_CREATED_TIME_MILLIS=971277114, android.telecom.extra.CALL_TELECOM_ROUTING_START_TIME_MILLIS=971277140, ] isAdhocConf: N, isIncoming: true, isUnknown: false, isLegacyHandover: false, isHandover: false,  addSelfManaged: true: (SBC.oSC)->CS.crCo->H.CS.crCo->H.CS.crCo.pICR(cap/cast)@E-IIA
09-27 16:42:08.106  2544  2544 I TelecomFramework: TelephonyConnectionService: notifyCreateConnectionComplete TC@21_1: (...->CSW.hCCC)->CS.crCoC->H.CS.crCoC(cap/cast)@E-E-E-IIA
09-27 16:42:08.219  2544  2544 I TelecomFramework: TelephonyConnectionService: onCallFilteringCompleted(TC@21_1, CallFilteringCompletionInfo{mIsBlocked=false, mIsInContacts=false, mCallResponse=android.telecom.CallScreeningService$CallResponse@8994d0fe, mCallScreeningPackageName='ComponentInfo{com.google.android.dialer/com.android.dialer.callscreeningservice.impl.CallScreeningServiceImpl}'}): (NCSSF.aC->ICFG.sF->ICFG.sF->ICFG.sF)->CS.oCFC->H.CS.oCFC(cast)@E-IIM
09-27 16:42:08.234  2544  2544 I TelecomFramework: TelephonyConnectionService: onTrackedByNonUiService TC@21_1 true: (NCSSF.aC->ICFG.sF->ICFG.sF->ICFG.sF)->CS.tBNUS->H.CS.tBNUS(cast)@E-IIM
09-27 16:42:08.239  2544  2544 I TelecomFramework: TelephonyConnectionService: onTrackedByNonUiService TC@21_1 true: (NCSSF.aC->ICFG.sF->ICFG.sF->ICFG.sF)->CS.tBNUS->H.CS.tBNUS(cast)@E-IIM
09-27 16:42:08.299  2544  2544 I TelecomFramework: TelephonyConnectionService: onAudioStateChanged TC@21_1 [AudioState isMuted: false, route: EARPIECE, supportedRouteMask: EARPIECE, SPEAKER, activeBluetoothDevice: [null], supportedBluetoothDevices: []]: (NCSSF.aC->ICFG.sF->ICFG.sF->ICFG.sF->CARSM.pM_UPDATE_SYSTEM_AUDIO_ROUTE)->CS.cASC->H.CS.cASC(cast)@E-IIM
09-27 16:42:08.300  2544  2544 I TelecomFramework: TelephonyConnectionService: onAudioStateChanged TC@21_1 [AudioState isMuted: false, route: EARPIECE, supportedRouteMask: EARPIECE, SPEAKER, activeBluetoothDevice: [null], supportedBluetoothDevices: []]: (NCSSF.aC->ICFG.sF->ICFG.sF->ICFG.sF->CARSM.pM_UPDATE_SYSTEM_AUDIO_ROUTE)->CS.cASC->H.CS.cASC(cast)@E-IIM
09-27 16:42:11.681  2544  2544 I TelecomFramework: TelephonyConnectionService: answer TC@21_1: (ICA.aC->CSFM.rF)->CS.an->H.CS.an(cgad/cast)@E-IK4
09-27 16:42:12.024  2544  2544 I TelecomFramework: TelephonyConnectionService: onAudioStateChanged TC@21_1 [AudioState isMuted: false, route: EARPIECE, supportedRouteMask: EARPIECE, SPEAKER, activeBluetoothDevice: [null], supportedBluetoothDevices: []]: CS.cASC->H.CS.cASC@AC4
09-27 16:42:12.025  2544  2544 I TelecomFramework: TelephonyConnectionService: onAudioStateChanged TC@21_1 [AudioState isMuted: false, route: EARPIECE, supportedRouteMask: EARPIECE, SPEAKER, activeBluetoothDevice: [null], supportedBluetoothDevices: []]: CS.cASC->H.CS.cASC@AC8
09-27 16:42:15.628  2544  2544 I TelecomFramework: TelephonyConnectionService: onAudioStateChanged TC@21_1 [AudioState isMuted: false, route: SPEAKER, supportedRouteMask: EARPIECE, SPEAKER, activeBluetoothDevice: [null], supportedBluetoothDevices: []]: CS.cASC->H.CS.cASC@ADA
09-27 16:42:15.628  2544  2544 I TelecomFramework: TelephonyConnectionService: onAudioStateChanged TC@21_1 [AudioState isMuted: false, route: SPEAKER, supportedRouteMask: EARPIECE, SPEAKER, activeBluetoothDevice: [null], supportedBluetoothDevices: []]: CS.cASC->H.CS.cASC@ADE
09-27 16:42:15.732 10213 10213 W TelecomFramework: VideoCallImpl: setCamera: cameraId=1, calling=com.google.android.dialer
09-27 16:42:20.752 10213 10213 W TelecomFramework: VideoCallImpl: setCamera: cameraId=1, calling=com.google.android.dialer


异常的log
09-27 15:32:27.273 10213 10213 W TelecomFramework: VideoCallImpl: setCamera: cameraId=null, calling=com.google.android.dialer
正常的log
09-27 16:42:20.752 10213 10213 W TelecomFramework: VideoCallImpl: setCamera: cameraId=1, calling=com.google.android.dialer

反编译 GoogleDialer 发现代码里面有自己设置 setCamera(null) , 感觉是 GoogleDialer 本身的设计，需要拿TCL的对比机试一下，是否也存在问题
file:///home/zq/projects/SPRDROID12_TRUNK_22B_W22.09.2/alps/GoogleDialer/sources/defpackage/ekc.java   238                        videoCall.setCamera(null);
file:///home/zq/projects/SPRDROID12_TRUNK_22B_W22.09.2/alps/GoogleDialer/sources/defpackage/fhx.java   54                videoCall.setCamera(null);
file:///home/zq/projects/SPRDROID12_TRUNK_22B_W22.09.2/alps/GoogleDialer/sources/defpackage/kqr.java   89            this.b.getVideoCall().setCamera(null);
file:///home/zq/projects/SPRDROID12_TRUNK_22B_W22.09.2/alps/GoogleDialer/sources/defpackage/kqr.java   106            this.b.getVideoCall().setCamera(null);



直接打Video call以及升级至Video Call

B，发起方/debuglogger/mobilelog/APLog_2022_0928_144535__4/sys_log_4__2022_0928_144732:09-28 14:46:22.682827  1542  1542 W TelecomFramework: VideoCallImpl: setCamera: cameraId=1, calling=com.google.android.dialer     //拨打视频通话，视频中 00:02 的地方。 00:06 的时候对方接通，
B，发起方/debuglogger/mobilelog/APLog_2022_0928_144535__4/sys_log_4__2022_0928_144732:09-28 14:46:30.471255  1542  1542 W TelecomFramework: VideoCallImpl: setCamera: cameraId=null, calling=com.google.android.dialer      //挂断视频通话，00:10
B，发起方/debuglogger/mobilelog/APLog_2022_0928_144535__4/sys_log_4__2022_0928_144732:09-28 14:46:46.984456  1542  1542 W TelecomFramework: VideoCallImpl: setCamera: cameraId=1, calling=com.google.android.dialer     //发起video call, 00:26
B，发起方/debuglogger/mobilelog/APLog_2022_0928_144535__4/sys_log_4__2022_0928_144732:09-28 14:46:49.554452  1542  1542 W TelecomFramework: VideoCallImpl: setCamera: cameraId=1, calling=com.google.android.dialer     //对方接起video call, 00:30
B，发起方/debuglogger/mobilelog/APLog_2022_0928_144535__4/sys_log_4__2022_0928_144732:09-28 14:47:03.084920  1542  1542 W TelecomFramework: VideoCallImpl: setCamera: cameraId=null, calling=com.google.android.dialer      //挂断video, 00:43

A, 接受方/debuglogger/mobilelog/APLog_2022_0928_144536__3/sys_log_4__2022_0928_144732:09-28 14:46:23.358402  1528  2794 W TelecomFramework: VideoCallImpl: setCamera: cameraId=1, calling=com.google.android.dialer
A, 接受方/debuglogger/mobilelog/APLog_2022_0928_144536__3/sys_log_4__2022_0928_144732:09-28 14:46:26.153453  1528  2793 W TelecomFramework: VideoCallImpl: setCamera: cameraId=1, calling=com.google.android.dialer        //00:06 的时候对方接通，
A, 接受方/debuglogger/mobilelog/APLog_2022_0928_144536__3/sys_log_4__2022_0928_144732:09-28 14:46:26.213616  1528  2519 W TelecomFramework: VideoCallImpl: setCamera: cameraId=1, calling=com.google.android.dialer
A, 接受方/debuglogger/mobilelog/APLog_2022_0928_144536__3/sys_log_4__2022_0928_144732:09-28 14:46:26.600253  1528  2794 W TelecomFramework: VideoCallImpl: setCamera: cameraId=1, calling=com.google.android.dialer
A, 接受方/debuglogger/mobilelog/APLog_2022_0928_144536__3/sys_log_4__2022_0928_144732:09-28 14:46:46.956246  1528  2565 W TelecomFramework: VideoCallImpl: setCamera: cameraId=1, calling=com.google.android.dialer
A, 接受方/debuglogger/mobilelog/APLog_2022_0928_144536__3/sys_log_4__2022_0928_144732:09-28 14:46:47.060424  1528  2792 W TelecomFramework: VideoCallImpl: setCamera: cameraId=1, calling=com.google.android.dialer
A, 接受方/debuglogger/mobilelog/APLog_2022_0928_144536__3/sys_log_4__2022_0928_144732:09-28 14:46:49.560698  1528  2793 W TelecomFramework: VideoCallImpl: setCamera: cameraId=1, calling=com.google.android.dialer
A, 接受方/debuglogger/mobilelog/APLog_2022_0928_144536__3/sys_log_4__2022_0928_144732:09-28 14:46:49.783479  1528  2565 W TelecomFramework: VideoCallImpl: setCamera: cameraId=1, calling=com.google.android.dialer
A, 接受方/debuglogger/mobilelog/APLog_2022_0928_144536__3/sys_log_4__2022_0928_144732:09-28 14:47:02.976257  1528  2519 W TelecomFramework: VideoCallImpl: setCamera: cameraId=null, calling=com.google.android.dialer


call2video
B-发起video call端/debuglogger/mobilelog/APLog_2022_0928_141933__3/sys_log_4__2022_0928_142355:09-28 14:20:45.483938  1562  2828 W TelecomFramework: VideoCallImpl: setCamera: cameraId=null, calling=com.google.android.dialer
B-发起video call端/debuglogger/mobilelog/APLog_2022_0928_141933__3/sys_log_4__2022_0928_142355:09-28 14:20:45.896252  1562  2827 W TelecomFramework: VideoCallImpl: setCamera: cameraId=1, calling=com.google.android.dialer
B-发起video call端/debuglogger/mobilelog/APLog_2022_0928_141933__3/sys_log_4__2022_0928_142355:09-28 14:20:53.015332  1562  2636 W TelecomFramework: VideoCallImpl: setCamera: cameraId=1, calling=com.google.android.dialer
B-发起video call端/debuglogger/mobilelog/APLog_2022_0928_141933__3/sys_log_4__2022_0928_142355:09-28 14:21:17.071091  1562  2615 W TelecomFramework: VideoCallImpl: setCamera: cameraId=null, calling=com.google.android.dialer
B-发起video call端/debuglogger/mobilelog/APLog_2022_0928_141933__3/sys_log_4__2022_0928_142355:09-28 14:22:36.690247  1562  2827 W TelecomFramework: VideoCallImpl: setCamera: cameraId=1, calling=com.google.android.dialer
B-发起video call端/debuglogger/mobilelog/APLog_2022_0928_141933__3/sys_log_4__2022_0928_142355:09-28 14:22:41.118652  1562  2636 W TelecomFramework: VideoCallImpl: setCamera: cameraId=1, calling=com.google.android.dialer
B-发起video call端/debuglogger/mobilelog/APLog_2022_0928_141933__3/sys_log_4__2022_0928_142355:09-28 14:23:09.685306  1562  2827 W TelecomFramework: VideoCallImpl: setCamera: cameraId=1, calling=com.google.android.dialer
B-发起video call端/debuglogger/mobilelog/APLog_2022_0928_141933__3/sys_log_4__2022_0928_142355:09-28 14:23:09.817783  1562  2828 W TelecomFramework: VideoCallImpl: setCamera: cameraId=1, calling=com.google.android.dialer
B-发起video call端/debuglogger/mobilelog/APLog_2022_0928_141933__3/sys_log_4__2022_0928_142355:09-28 14:23:13.243709  1562  2828 W TelecomFramework: VideoCallImpl: setCamera: cameraId=1, calling=com.google.android.dialer
B-发起video call端/debuglogger/mobilelog/APLog_2022_0928_141933__3/sys_log_4__2022_0928_142355:09-28 14:23:13.568687  1562  2642 W TelecomFramework: VideoCallImpl: setCamera: cameraId=1, calling=com.google.android.dialer


A-接受video call端/debuglogger/mobilelog/APLog_2022_0928_141745__2/sys_log_4__2022_0928_142349:09-28 14:20:52.563612  8977  8977 W TelecomFramework: VideoCallImpl: setCamera: cameraId=null, calling=com.google.android.dialer
A-接受video call端/debuglogger/mobilelog/APLog_2022_0928_141745__2/sys_log_4__2022_0928_142349:09-28 14:20:54.595079  8977  8977 W TelecomFramework: VideoCallImpl: setCamera: cameraId=null, calling=com.google.android.dialer
A-接受video call端/debuglogger/mobilelog/APLog_2022_0928_141745__2/sys_log_4__2022_0928_142349:09-28 14:21:16.376934  8977  8977 W TelecomFramework: VideoCallImpl: setCamera: cameraId=null, calling=com.google.android.dialer
A-接受video call端/debuglogger/mobilelog/APLog_2022_0928_141745__2/sys_log_4__2022_0928_142349:09-28 14:22:36.290648  8977  8977 W TelecomFramework: VideoCallImpl: setCamera: cameraId=1, calling=com.google.android.dialer
A-接受video call端/debuglogger/mobilelog/APLog_2022_0928_141745__2/sys_log_4__2022_0928_142349:09-28 14:22:40.759489  8977  8977 W TelecomFramework: VideoCallImpl: setCamera: cameraId=null, calling=com.google.android.dialer
A-接受video call端/debuglogger/mobilelog/APLog_2022_0928_141745__2/sys_log_4__2022_0928_142349:09-28 14:22:40.778777  8977  8977 W TelecomFramework: VideoCallImpl: setCamera: cameraId=null, calling=com.google.android.dialer
A-接受video call端/debuglogger/mobilelog/APLog_2022_0928_141745__2/sys_log_4__2022_0928_142349:09-28 14:23:09.222309  8977  8977 W TelecomFramework: VideoCallImpl: setCamera: cameraId=1, calling=com.google.android.dialer
A-接受video call端/debuglogger/mobilelog/APLog_2022_0928_141745__2/sys_log_4__2022_0928_142349:09-28 14:23:12.758896  8977  8977 W TelecomFramework: VideoCallImpl: setCamera: cameraId=1, calling=com.google.android.dialer
A-接受video call端/debuglogger/mobilelog/APLog_2022_0928_141745__2/sys_log_4__2022_0928_142349:09-28 14:23:34.307261  8977  8977 W TelecomFramework: VideoCallImpl: setCamera: cameraId=null, calling=com.google.android.dialer






entering video mode   ->   exitVideoMode
09-29 17:04:44.091 24370 24370 I DialerVideoCallPresenter: com.android.incallui.VideoCallPresenter.onPrimaryCallChanged:670 entering video mode...
09-29 17:04:44.093 24370 24370 I DialerVideoCallPresenter: com.android.incallui.VideoCallPresenter.updateCameraSelection:280 setting camera direction to 0, call: [DialerCall_4, ACTIVE, [Capabilities: CAPABILITY_HOLD CAPABILITY_SUPPORT_HOLD CAPABILITY_MUTE CAPABILITY_SUPPORTS_VT_LOCAL_RX CAPABILITY_SUPPORTS_VT_LOCAL_TX CAPABILITY_SUPPORTS_VT_LOCAL_BIDIRECTIONAL CAPABILITY_SUPPORTS_VT_REMOTE_RX CAPABILITY_SUPPORTS_VT_REMOTE_TX CAPABILITY_SUPPORTS_VT_REMOTE_BIDIRECTIONAL CAPABILITY_CAN_PAUSE_VIDEO], [Properties: PROPERTY_HIGH_DEF_AUDIO], children:[], parent:null, conferenceable:[], videoState:Audio Tx Rx, SessionModificationState:0, CameraDir:0]
09-29 17:04:44.094 24370 24370 I DialerVideoCallPresenter: com.android.incallui.VideoCallPresenter.adjustVideoMode:854 videoCall: android.telecom.VideoCallImpl@b88a33b, videoState: 3


shouldShowPreviewVideo 从 true 变为 false
09-29 17:04:44.095 24370 24370 I DialerVideoCallPresenter: com.android.incallui.VideoCallPresenter.showVideoUi:1003 shouldShowRemoteVideo: true, shouldShowPreviewVideo: true, isRemotelyHeld: false
09-29 17:04:44.097 24370 24370 E DialerVideoCallPresenter: com.android.incallui.VideoCallPresenter$LocalDelegate.onSurfaceCreated:1282 no video call
09-29 17:04:44.104 24370 24370 I DialerVideoCallPresenter: com.android.incallui.VideoCallPresenter.onPrimaryCallChanged:675 video conference enabled: false




09-29 17:04:44.111   928   928 I VT      : [SRV] [OPERATION][ID=1] setCamera (camera id 1)
09-29 17:04:44.111   928   928 D [VT]ImsMa: [setCurrentCameraId]Line 2208 [ID=10][0xb4000079ce82e000][enter]=======
09-29 17:04:44.111   928   928 D [VT]ImsMa: [setCurrentCameraId]Line 2209 [ID=10]mFlags 0x806,index  1
09-29 17:04:44.111   928   928 I [VT]ImsMa: [setCurrentCameraId]Line 2231 index 0 W:4096, H:4096, D:90,F:1,HAL 3
09-29 17:04:44.111   928   928 I [VT]ImsMa: [setCurrentCameraId]Line 2231 index 1 W:3264, H:3264, D:270,F:0,HAL 3
09-29 17:04:44.111   971 26376 D MtkCam/StreamingPipe/Data: [calNonLargeSrcCrop]sID(1), imgoIn(0), srcCrop(0,0,1440x1088), isSrcCrop(0), mP2Pack Valid(1), imgo(0x0),rrz(1440x1088)
09-29 17:04:44.111   971 26376 D MtkCam/StreamingPipe/TPI_MGR_Plugin: [genFrame]TPIFrame#161(meta=0xb400007d2764e9e8)(yuv=1)(async=0): [8/MotionDetectPlugin(yuv)run=1]
09-29 17:04:44.112   928 26409 W Codec2Client: query -- param skipped: index = 1342179345.
09-29 17:04:44.112   971 26376 D MtkCam/StreamingPipe/Pipe: [prepareIORequest]P2S cam 1 MWFrame:#160 MWReq:#160, frame 161-161  master/slave/fd(1/-1/1) ReqNo(161), feature=0x1000(TPI_YUV), cycle(33), fps(n/a)=(30/30), ZoomROI((1440.000000x724.000000)@(0.000000,181.000000)) SFPIOMgr:[sID(1)--IMG(0x0/0),RRZ(0xb400007d665b1d00/1),LCS(0xb400007d66202000/1),LCSH(0x0/0),pRSS(0x0/0),cRSS(0x0/0),RSSR2(0x0/0),FYuv(0x0/0),RYuv1(0x0/0),RYuv2(0x0/0),mAIYuv(0x0/0),HalI(0xb400007d62a5ab60),AppI(0xb400007d2764e9e8),AppDI(0xb400007d62a5b040),AppOver(0x0)]{path(GEN),halO(0xb400007d79c7ba20),appO(0xb400007d79c7a360),Outs--[buf(0xb400007d66202200/1)(640x320),tran(0),type(4), tar(fd), prof(0), crop(0.000000,181.000000,1440.000000x724.000000), flag(0x3)][buf(0xb400007d66202100/1)(1440x720),tran(0),type(1), tar(disp), prof(0), crop(0.000000,181.000000,1440.000000x724.000000), flag(0x3)]Tuning--id(1)--[flag(5)]}
09-29 17:04:44.112   928 26409 W Codec2Client: query -- param skipped: index = 2415921170.
09-29 17:04:44.112   928 26409 D CCodecBufferChannel: [c2.mtk.avc.encoder#184] Using basic input block pool with poolID 1 => got 1 - OK (0)
09-29 17:04:44.113 24370 24370 I DialerAnswerFragment: com.android.incallui.answer.impl.AnswerFragment.onStop:935 onStop
09-29 17:04:44.113 24370 24370 I DialerAnswerVideoCallScreen: com.android.incallui.answer.impl.AnswerVideoCallScreen.onVideoScreenStop:67 video screen stop




09-29 17:04:44.114 24370 24370 I DialerVideoCallPresenter: com.android.incallui.VideoCallPresenter.updateCameraSelection:280 setting camera direction to 0, call: [DialerCall_4, ACTIVE, [Capabilities: CAPABILITY_HOLD CAPABILITY_SUPPORT_HOLD CAPABILITY_MUTE CAPABILITY_SUPPORTS_VT_LOCAL_RX CAPABILITY_SUPPORTS_VT_LOCAL_TX CAPABILITY_SUPPORTS_VT_LOCAL_BIDIRECTIONAL CAPABILITY_SUPPORTS_VT_REMOTE_RX CAPABILITY_SUPPORTS_VT_REMOTE_TX CAPABILITY_SUPPORTS_VT_REMOTE_BIDIRECTIONAL CAPABILITY_CAN_PAUSE_VIDEO], [Properties: PROPERTY_HIGH_DEF_AUDIO], children:[], parent:null, conferenceable:[], videoState:Audio Tx Rx, SessionModificationState:0, CameraDir:0]
09-29 17:04:44.114 24370 24370 I DialerVideoCallPresenter: com.android.incallui.VideoCallPresenter.exitVideoMode:966 exitVideoMode
09-29 17:04:44.114 24370 24370 I DialerVideoCallPresenter: com.android.incallui.VideoCallPresenter.showVideoUi:1003 shouldShowRemoteVideo: false, shouldShowPreviewVideo: false, isRemotelyHeld: false




private final void K(int i, kcv kcv, int i2, boolean z) {
    String str = "showVideoUi";
    String str2 = "VideoCallPresenter.java";
    String str3 = "com/android/incallui/VideoCallPresenter";
    if (this.c != null) {
        boolean isPaused = VideoProfile.isPaused(i);
        kcv kcv2 = kcv.ACTIVE;
        boolean z2 = true;
        Object obj = !kcv.b(kcv) ? kcv == kcv.CONNECTING ? 1 : null : 1;
        if (isPaused || ((kcv != kcv2 && obj == null) || !VideoProfile.isReceptionEnabled(i) || z)) {
            isPaused = false;
        } else {
            isPaused = true;
        }
        if (!liz.d(this.d)) {
            ((qvz) ((qvz) a.b()).l(str3, "shouldShowPreviewVideo", 224, str2)).v("Camera permission is disabled by user.");
            z2 = false;
        } else if (!(VideoProfile.isTransmissionEnabled(i) || jnw.V(i2))) {
                                    // VideoProfile.isTransmissionEnabled(i) 这里的 i 是当前 VideoProfile 的状态
            z2 = false;             // jnw.V(i2) 这里发生了变化？   i2 变为了 2 才会为 false, 这里的 i2 是什么意思？
        }
        qvx qvx = a;
        ((qvz) ((qvz) qvx.b()).l(str3, str, 1003, str2)).L("shouldShowRemoteVideo: %b, shouldShowPreviewVideo: %b, isRemotelyHeld: %b", Boolean.valueOf(isPaused), Boolean.valueOf(z2), Boolean.valueOf(z));
        Optional b = this.c.b();
        String str4 = "updateRemoteVideoSurfaceDimensions";
        if (b.isPresent()) {
            Activity E = ((ar) b.get()).E();
            if (E == null) {
                ((qvz) ((qvz) qvx.b()).l(str3, str4, 1249, str2)).v("activity from videoCallScreenFragment is null.");
            } else {
                Point point = new Point();
                E.getWindowManager().getDefaultDisplay().getSize(point);
                m().f(point);
            }
        } else {
            ((qvz) ((qvz) qvx.b()).l(str3, str4, 1244, str2)).v("videoCallScreenFragment is empty.");
        }
        this.c.j(z2, isPaused, z);
        jls.k().B(VideoProfile.isAudioOnly(i));
        N(kcv, i2);
        return;
    }
    ((qvz) ((qvz) a.c()).l(str3, str, 996, str2)).v("videoCallScreen is null returning");
}


private static boolean V(int i) {
    return liz.f(i) || liz.e(i);
}

public static boolean e(int i) {
    return i == 3;
}

public static boolean f(int i) {
    return i == 1 || i == 5 || i == 6 || i == 4;
}

VideoProfile.java
public static boolean isTransmissionEnabled(@VideoState int videoState) {
    return hasState(videoState, VideoProfile.STATE_TX_ENABLED);
}

public VideoProfile(@VideoState int videoState) {
    this(videoState, QUALITY_DEFAULT);      // videoState 是从 GoogleDialer 里面获取并且设置的
}



9.30分析

接通 Call
09-30 13:36:50.758  4043  4043 I DialerVideoCallPresenter: com.android.incallui.VideoCallPresenter.onStateChange:551 primaryChanged: true, primary: [DialerCall_1, ACTIVE, [Capabilities: CAPABILITY_HOLD CAPABILITY_SUPPORT_HOLD CAPABILITY_MUTE CAPABILITY_SUPPORTS_VT_LOCAL_RX CAPABILITY_SUPPORTS_VT_LOCAL_TX CAPABILITY_SUPPORTS_VT_LOCAL_BIDIRECTIONAL CAPABILITY_SUPPORTS_VT_REMOTE_RX CAPABILITY_SUPPORTS_VT_REMOTE_TX CAPABILITY_SUPPORTS_VT_REMOTE_BIDIRECTIONAL CAPABILITY_CAN_PAUSE_VIDEO], [Properties: PROPERTY_HIGH_DEF_AUDIO], children:[], parent:null, conferenceable:[], videoState:Audio Only, SessionModificationState:3, CameraDir:-1], previous primaryCall: null
09-30 13:36:50.758  4043  4043 I DialerVideoCallPresenter: com.android.incallui.VideoCallPresenter.onPrimaryCallChanged:670 entering video mode...
09-30 13:36:50.758  4043  4043 I DialerVideoCallPresenter: com.android.incallui.VideoCallPresenter.updateCameraSelection:280 setting camera direction to 0, call: [DialerCall_1, ACTIVE, [Capabilities: CAPABILITY_HOLD CAPABILITY_SUPPORT_HOLD CAPABILITY_MUTE CAPABILITY_SUPPORTS_VT_LOCAL_RX CAPABILITY_SUPPORTS_VT_LOCAL_TX CAPABILITY_SUPPORTS_VT_LOCAL_BIDIRECTIONAL CAPABILITY_SUPPORTS_VT_REMOTE_RX CAPABILITY_SUPPORTS_VT_REMOTE_TX CAPABILITY_SUPPORTS_VT_REMOTE_BIDIRECTIONAL CAPABILITY_CAN_PAUSE_VIDEO], [Properties: PROPERTY_HIGH_DEF_AUDIO], children:[], parent:null, conferenceable:[], videoState:Audio Only, SessionModificationState:3, CameraDir:0]

09-30 13:36:50.758  4043  4043 I DialerVideoCallPresenter: com.android.incallui.VideoCallPresenter.adjustVideoMode:854 videoCall: android.telecom.VideoCallImpl@ad25074, videoState: 0
09-30 13:36:50.758  4043  4043 I DialerVideoCallPresenter: com.android.incallui.VideoCallPresenter.showVideoUi:1003 shouldShowRemoteVideo: false, shouldShowPreviewVideo: true, isRemotelyHeld: false

接通 VideoCall
09-30 13:36:56.154  4043  4043 I DialerVideoCallPresenter: com.android.incallui.VideoCallPresenter.adjustVideoMode:854 videoCall: android.telecom.VideoCallImpl@ad25074, videoState: 3
09-30 13:36:56.154  4043  4043 I DialerVideoCallPresenter: com.android.incallui.VideoCallPresenter.showVideoUi:1003 shouldShowRemoteVideo: true, shouldShowPreviewVideo: true, isRemotelyHeld: false
09-30 13:36:56.180  4043  4043 I DialerVideoCallPresenter: com.android.incallui.VideoCallPresenter.showVideoUi:1003 shouldShowRemoteVideo: false, shouldShowPreviewVideo: false, isRemotelyHeld: false

点击关闭 Video
09-30 13:37:07.591  4043  4043 I DialerVideoCallPresenter: com.android.incallui.VideoCallPresenter.adjustVideoMode:854 videoCall: android.telecom.VideoCallImpl@ad25074, videoState: 2
09-30 13:37:07.592  4043  4043 I DialerVideoCallPresenter: com.android.incallui.VideoCallPresenter.showVideoUi:1003 shouldShowRemoteVideo: true, shouldShowPreviewVideo: false, isRemotelyHeld: false

再点击打开 Video
09-30 13:37:18.486  4043  4043 I DialerVideoCallPresenter: com.android.incallui.VideoCallPresenter.adjustVideoMode:854 videoCall: android.telecom.VideoCallImpl@ad25074, videoState: 3
09-30 13:37:18.486  4043  4043 I DialerVideoCallPresenter: com.android.incallui.VideoCallPresenter.showVideoUi:1003 shouldShowRemoteVideo: true, shouldShowPreviewVideo: true, isRemotelyHeld: false
```## 微信扫码慢的问题

```text
CRUZE
09-05 18:23:07.004 I/ActivityTaskManager( 1380): Displayed com.tencent.mm/.plugin.scanner.ui.BaseScanUI: +602ms
09-05 18:22:14.751 I/ActivityTaskManager( 1380): Displayed com.tencent.mm/.plugin.scanner.ui.BaseScanUI: +945ms


CIVICPL
09-05 18:07:03.048 I/ActivityTaskManager( 1331): Displayed com.tencent.mm/.plugin.scanner.ui.BaseScanUI: +857ms
09-05 18:07:03.056 W/MtkCam/GrallocHelper(  930): [checkPlaneSize] [YCrCb_420_SP:1] sizeInBytes:593920 != 1536 x 384

09-05 18:07:10.984 I/XWeb.SDK.XWWebView(25696): [:25696, ]:onReceivedTitle: 美团外卖

09-05 18:23:07.812 I/MicroMsg.QBarEngineReporter(25613): [:18772, ]:setScanSuccessTime: 290,

09-27 15:32:27.270 10213 10213 I DialerAnswerVideoCallScreen: com.android.incallui.answer.impl.AnswerVideoCallScreen.onVideoScreenStop:67 video screen stop
09-27 15:32:27.273 10213 10213 W TelecomFramework: VideoCallImpl: setCamera: cameraId=null, calling=com.google.android.dialer
```## WM11 UC浏览器预览模糊

```text
Camera2:
android.control.afMode (10007): byte[1]
[CONTINUOUS_PICTURE ]

UC浏览器:
android.control.afMode (10007): byte[1]
[OFF ]
android.control.afRegions (10008): int32[5]
[0 0 0 0 ]
[0 ]
```## NVA-800 SystemUI 的 flash一直处于 "相机正在使用中" 的状态无法切换

```text
Historical operations
1970-01-01 00:14:51 persist
1970-01-01 00:14:51 update flashlight_available
1970-01-01 00:14:20 persist
1970-01-01 00:14:19 update flashlight_available
1970-01-01 00:14:17 persist
1970-01-01 00:14:17 update flashlight_available
1970-01-01 00:12:09 persist
1970-01-01 00:12:08 update flashlight_available
1970-01-01 00:09:00 persist
1970-01-01 00:09:00 update flashlight_available
1970-01-01 00:08:53 persist
1970-01-01 00:08:53 update flashlight_available
1970-01-01 00:06:00 persist
1970-01-01 00:06:00 update flashlight_enabled
1970-01-01 00:05:59 persist
1970-01-01 00:05:59 update flashlight_enabled
1970-01-01 00:05:55 persist
1970-01-01 00:05:55 update flashlight_available
1970-01-01 00:05:53 persist
1970-01-01 00:05:53 update flashlight_available

从 Settings.Secure 看 flashlight_available 是 null 的，怀疑是没有设置 flashlight_available 的值，但是为什么进入 DreamCamera2 之后也不会去设置呢？
adb shell settings get secure flashlight_available
null

frameworks/base/core/java/android/hardware/camera2/CameraManager.java
private void postSingleTorchUpdate(final TorchCallback callback, final Executor executor, final String id, final int status) {
    switch(status) {
        case ICameraServiceListener.TORCH_STATUS_AVAILABLE_ON:
        case ICameraServiceListener.TORCH_STATUS_AVAILABLE_OFF: {
                final long ident = Binder.clearCallingIdentity();
                try {
                    executor.execute(() -> {
                        callback.onTorchModeChanged(id, status ==
                                ICameraServiceListener.TORCH_STATUS_AVAILABLE_ON);      // onTorchModeChanged
                    });
                } finally {
                    Binder.restoreCallingIdentity(ident);
                }
            }
            break;
        default: {
                final long ident = Binder.clearCallingIdentity();
                try {
                    executor.execute(() -> {
                        callback.onTorchModeUnavailable(id);                            // onTorchModeUnavailable
                    });
                } finally {
                    Binder.restoreCallingIdentity(ident);
                }
            }
            break;
    }
}

private void updateTorchCallbackLocked(TorchCallback callback, Executor executor) {
    for (int i = 0; i < mTorchStatus.size(); i++) {
        String id = mTorchStatus.keyAt(i);
        Integer status = mTorchStatus.valueAt(i);
        postSingleTorchUpdate(callback, executor, id, status);
    }
}

private void onTorchStatusChangedLocked(int status, String id) {
    if (DEBUG) {
        Log.v(TAG,
                String.format("Camera id %s has torch status changed to 0x%x", id, status));
    }

    if (!validTorchStatus(status)) {
        Log.e(TAG, String.format("Ignoring invalid device %s torch status 0x%x", id,
                        status));
        return;
    }

    Integer oldStatus = mTorchStatus.put(id, status);
    if (oldStatus != null && oldStatus == status) {
        if (DEBUG) {
            Log.v(TAG, String.format(
                "Torch status changed to 0x%x, which is what it already was",
                status));
        }
        return;
    }

    final int callbackCount = mTorchCallbackMap.size();
    for (int i = 0; i < callbackCount; i++) {
        final Executor executor = mTorchCallbackMap.valueAt(i);
        final TorchCallback callback = mTorchCallbackMap.keyAt(i);
        postSingleTorchUpdate(callback, executor, id, status);
    }
} // onTorchStatusChangedLocked

提交记录
http://192.168.3.81:8085/c/SPRD_S/SPRDROID12_TRUNK_22B_W22.09.2/+/790
```## NVA-1000 Snapchat预览显示模糊问题

```text
adb shell dumpsys media.camera 查看，看到用的是 Camera1 的 API，所以在 CameraMetadataNative.java 中修改没有效果
preview-size: 1280x720
preview-size-values: 1280x720,960x720,720x720,720x480,640x480,352x288,320x240,240x240,304x144,288x144,256x144,176x144

adb logcat | grep "configureStream" 看到 snapchat 的预览配流大小是 304x144，太小了，所以会显示模糊

需要修改 Camera.java -> getSupportedPreviewSizes()
public List<Size> getSupportedPreviewSizes() {
    String str = get(KEY_PREVIEW_SIZE + SUPPORTED_VALUES_SUFFIX);
    //NVA-1000 modified for snapchat camera preview blur issue ZQ 2022/09/28:begin
    List<Size> supportedSizes = splitSize(str);
    if ("com.snapchat.android".equalsIgnoreCase(android.app.ActivityThread.currentOpPackageName())) {
        List<Size> tempSizes = new ArrayList<Size>();
        for (Size mSize : supportedSizes) {
            if (mSize.height >= 480) {
                tempSizes.add(mSize);
            }
        }
        return tempSizes;
    }
    //NVA-1000 modified for snapchat camera preview blur issue ZQ 2022/09/28:end
    return supportedSizes;
}

上传记录
http://192.168.3.81:8085/c/SPRD_S/SPRDROID12_TRUNK_22B_W22.09.2/+/241
```## BE6 Instagram 后摄不能缩放

```text
对比前后摄的 media.camera 之后发现后摄没有设置 cropRegion，添加了后摄的 metadata 之后ok
```## NVA-1330 双击power键无法打开相机，需要到 Settings/System/Gesture/ 开关一下 快速打开相机的开关才可以

```text
adb shell settings get secure camera_double_tap_power_gesture_disabled    获取不到这个值，怀疑是
重新设置一下之后可以

alps/frameworks/base/services/core/java/com/android/server/GestureLauncherService.java
public static boolean isCameraDoubleTapPowerSettingEnabled(Context context, int userId) {
     return isCameraDoubleTapPowerEnabled(context.getResources())
            && (!(Settings.Secure.getIntForUser(context.getContentResolver(),
                    Settings.Secure.CAMERA_DOUBLE_TAP_POWER_GESTURE_DISABLED, Settings.Secure.DOUBLE_TAP_POWER_OFF, userId) ==
                     Settings.Secure.DOUBLE_TAP_POWER_OFF));
}

alps/packages/apps/Settings/src/com/android/settings/gestures/DoubleTapPowerPreferenceController.java
@Override
public boolean isChecked() {
    int cameraDisabled = OFF;
    if (mDoubleTapVolumeUp) {
        cameraDisabled = Settings.Secure.getInt(mContext.getContentResolver(),
            VOLUME_UP_SECURE_KEY, ON);
    } else {
        cameraDisabled = Settings.Secure.getInt(mContext.getContentResolver(),
            SECURE_KEY, ON);
    }
    return cameraDisabled == ON;
}

这两个地方获取到的默认值不同

NVA-1100 里面修改的
```## 展锐平台 目前使用的sensor name可以通过打开camera 过滤关键字 sensorname来查看

```text
adb root;adb logcat -c;adb logcat -G 20m;adb logcat | grep -i sensorname
```## PopupWindow

```text
diff --git a/alps/vendor/sprd/platform/packages/apps/DreamCamera2/src/com/android/camera/PhotoUI.java b/alps/vendor/sprd/platform/packages/apps/DreamCamera2/src/com/android/camera/PhotoUI.java
index e2b648f5324..69fb50df48e 100644
--- a/alps/vendor/sprd/platform/packages/apps/DreamCamera2/src/com/android/camera/PhotoUI.java
+++ b/alps/vendor/sprd/platform/packages/apps/DreamCamera2/src/com/android/camera/PhotoUI.java
@@ -1701,6 +1701,10 @@ public class PhotoUI extends DreamUI implements PreviewStatusListener,
                     //redmine 61704 COS-727 flash selection boxes will not disappear wx begin
                     mRatioView = initRatioView();
                     topPanelParent.addView(mRatioView);
+                    MultiToggleImageButton ratioButon = (MultiToggleImageButton) mTopPanel.getTopPanelButton(R.integer.ratio_toggle_button_dream);
+                    final android.widget.PopupWindow popupWindow = new android.widget.PopupWindow(mRatioView, 720, 100);//参数为1.View 2.宽度 3.高度
+                    popupWindow.setOutsideTouchable(true);
+                    popupWindow.showAsDropDown(ratioButon);
                     //redmine 61704 COS-727 flash selection boxes will not disappear wx end
                     //Redmine59809 ODM modified for top panel layout ZQ:begin
                     showTopPanel(false);
```## NOVA改了包名之后拍照保存报错

```text
步骤：
将 DreamCamera2 的包名从 com.android.camera2 修改为 com.hmdglobal.app.cameralite

现象：
拍照报错

分析：
报错log如下
10-13 22:23:40.418  8927  8946 D SpecialTypesProvider: val call pkg from update; call pkg: com.hmdglobal.app.cameralite
10-13 22:23:40.418   529  8857 D Cam3OEMIf: 4433, receivePreviewFDFrame: receive face_num 0.mCameraId 0 ref_camera_id 0
10-13 22:23:40.419  8927  8946 D SpecialTypesProvider: validateCallingPackage : fail.
10-13 22:23:40.420  8927  8946 E DatabaseUtils: Writing exception to parcel
10-13 22:23:40.420  8927  8946 E DatabaseUtils: java.lang.SecurityException
10-13 22:23:40.420  8927  8946 E DatabaseUtils:  at com.sprd.providers.photos.SpecialTypesProvider.validateCallingPackage(SpecialTypesProvider.java:1144)
10-13 22:23:40.420  8927  8946 E DatabaseUtils:  at com.sprd.providers.photos.SpecialTypesProvider.update(SpecialTypesProvider.java:1047)
10-13 22:23:40.420  8927  8946 E DatabaseUtils:  at android.content.ContentProvider.update(ContentProvider.java:1886)
10-13 22:23:40.420  8927  8946 E DatabaseUtils:  at android.content.ContentProvider$Transport.update(ContentProvider.java:467)
10-13 22:23:40.420  8927  8946 E DatabaseUtils:  at android.content.ContentProviderNative.onTransact(ContentProviderNative.java:231)
10-13 22:23:40.420  8927  8946 E DatabaseUtils:  at android.os.Binder.execTransactInternal(Binder.java:1185)
10-13 22:23:40.420  8927  8946 E DatabaseUtils:  at android.os.Binder.execTransact(Binder.java:1143)
10-13 22:23:40.425   529  8873 D Cam3Channel: 1168, channelCbRoutine: E
10-13 22:23:40.427  1014  3101 I am_crash: [5942,0,com.hmdglobal.app.cameralite,551074885,java.lang.SecurityException,An error occurred while executing doInBackground(),Parcel.java,2426]
10-13 22:23:40.431  1014  8951 E stark   : filterType return false
10-13 22:23:40.431  1014  3101 W ActivityTaskManager:   Force finishing activity com.hmdglobal.app.cameralite/com.android.camera.CameraLauncher
10-13 22:23:40.431  1014  8951 I DropBoxManagerService: add tag=system_app_crash isTagEnabled=true flags=0x2
10-13 22:23:40.432  1014  3101 I wm_finish_activity: [0,157701714,23,com.hmdglobal.app.cameralite/com.android.camera.CameraLauncher,force-crash]

从 log 中看到是 SpecialTypesProvider 中对camera的包名做了限制，然后找到如下apk，
vendor/sprd/release/IDH/s9863a1h10_Natv-userdebug-gms/out/target/product/s9863a1h10/system_ext/app/USCPhotosProvider/USCPhotosProvider.apk
对其反编译之后看到
private void validateCallingPackage(String value) {
    String pkgName = getCallingPackage();
    StringBuilder stringBuilder = new StringBuilder();
    stringBuilder.append("val call pkg from ");
    stringBuilder.append(value);
    stringBuilder.append("; call pkg: ");
    stringBuilder.append(pkgName);
    String stringBuilder2 = stringBuilder.toString();
    String str = TAG;
    Log.d(str, stringBuilder2);
    if (GOOGLE_GALLERY_PACKAGE_NAME.equalsIgnoreCase(pkgName) || GOOGLE_PHOTOS_PACKAGE_NAME.equalsIgnoreCase(pkgName) || EDITOR_PACKAGE_NAME.equalsIgnoreCase(pkgName) || "com.android.camera2".equalsIgnoreCase(pkgName) || "com.sprd.providers.photos".equals(pkgName)) {
        Log.d(str, "validateCallingPackage : pass.");
    } else {
        Log.d(str, "validateCallingPackage : fail.");
        throw new SecurityException();
    }
}
代码中确实有对包名做的限制，请问这种情况该如何修改？

SPCSS01064328
展锐修改完之后已经把我们的包名加进去了
private void validateCallingPackage(String str) {
    String callingPackage = getCallingPackage();
    StringBuilder stringBuilder = new StringBuilder();
    stringBuilder.append("val call pkg from ");
    stringBuilder.append(str);
    stringBuilder.append("; call pkg: ");
    stringBuilder.append(callingPackage);
    str = stringBuilder.toString();
    String str2 = TAG;
    Log.d(str2, str);
    if (GOOGLE_GALLERY_PACKAGE_NAME.equalsIgnoreCase(callingPackage) || GOOGLE_PHOTOS_PACKAGE_NAME.equalsIgnoreCase(callingPackage) || EDITOR_PACKAGE_NAME.equalsIgnoreCase(callingPackage) || "com.android.camera2".equalsIgnoreCase(callingPackage) || "com.hmdglobal.app.cameralite".equals(callingPackage) || "com.sprd.providers.photos".equals(callingPackage)) {
        Log.d(str2, "validateCallingPackage : pass.");
    } else {
        Log.d(str2, "validateCallingPackage : fail.");
        throw new SecurityException();
    }
}

修改方法1：
ContentProvider.java
public final @Nullable String getCallingPackage() {
    final AttributionSource callingAttributionSource = getCallingAttributionSource();
    //modified begin
    String callingPackageName = (callingAttributionSource != null) ? callingAttributionSource.getPackageName() : null;
    String className = getClass().getName();
    if ("com.sprd.providers.photos.SpecialTypesProvider".equalsIgnoreCase(getClass().getName()) && "com.hmdglobal.app.cameralite".equalsIgnoreCase(callingPackageName)) {
        return "com.android.camera2";
    }
    return callingPackageName;
    //modified end
}
```## NVA-1515 拍照相机崩溃

```text
M45DB9E  10-12 03:04:04.857  5159  6425 I CAM2PORT_AndCam2AgntImp: send CONTROL_AF_TRIGGER_CANCEL
M45DB9F  10-12 03:04:04.857  5159  5159 I CAM_PhotoModule: stopPreview
M45DBA0  10-12 03:04:04.857   451 15637 W DPUModule: Warning: Dispc cannot support 8 layer blending(0)
M45DBA1  10-12 03:04:04.857  5159  6426 I CAM2PORT_DispatchThread: Runnable job.run() end!
M45DBA2  10-12 03:04:04.857  5159  6426 I CAM2PORT_DispatchThread: DispatchThread.this.wait will!
M45DBA3  10-12 03:04:04.858  5159  6425 E CAM2PORT_AndCam2AgntImp: Unable to cancel autofocus
M45DBA3  10-12 03:04:04.858  5159  6425 E CAM2PORT_AndCam2AgntImp: android.hardware.camera2.CameraAccessException: CAMERA_ERROR (3): The camera device has encountered a serious error
M45DBA3  10-12 03:04:04.858  5159  6425 E CAM2PORT_AndCam2AgntImp:  at android.hardware.camera2.impl.CameraDeviceImpl.checkIfCameraClosedOrInError(CameraDeviceImpl.java:2350)
M45DBA3  10-12 03:04:04.858  5159  6425 E CAM2PORT_AndCam2AgntImp:  at android.hardware.camera2.impl.CameraDeviceImpl.createCaptureRequest(CameraDeviceImpl.java:825)
M45DBA3  10-12 03:04:04.858  5159  6425 E CAM2PORT_AndCam2AgntImp:  at com.android.ex.camera2.portability.util.Camera2RequestSettingsSet.createRequest(Camera2RequestSettingsSet.java:237)
M45DBA3  10-12 03:04:04.858  5159  6425 E CAM2PORT_AndCam2AgntImp:  at com.android.ex.camera2.portability.AndroidCamera2AgentImpl$Camera2Handler.handleMessage(AndroidCamera2AgentImpl.java:741)
M45DBA3  10-12 03:04:04.858  5159  6425 E CAM2PORT_AndCam2AgntImp:  at com.android.ex.camera2.portability.SprdAndroidCamera2AgentImpl$SprdCamera2Handler.handleMessage(SprdAndroidCamera2AgentImpl.java:715)
M45DBA3  10-12 03:04:04.858  5159  6425 E CAM2PORT_AndCam2AgntImp:  at android.os.Handler.dispatchMessage(Handler.java:106)
M45DBA3  10-12 03:04:04.858  5159  6425 E CAM2PORT_AndCam2AgntImp:  at android.os.Looper.loopOnce(Looper.java:201)
M45DBA3  10-12 03:04:04.858  5159  6425 E CAM2PORT_AndCam2AgntImp:  at android.os.Looper.loop(Looper.java:288)
M45DBA3  10-12 03:04:04.858  5159  6425 E CAM2PORT_AndCam2AgntImp:  at android.os.HandlerThread.run(HandlerThread.java:67)


./009-1012_023242--1012_030715/M45CE0B  10-12 03:03:51.376  5159  5159 E CAM_FatalErrorHandler: Handling Camera Open Failure:
./009-1012_023242--1012_030715/M45CE0B  10-12 03:03:51.376  5159  5159 E CAM_FatalErrorHandler: java.lang.Exception
./009-1012_023242--1012_030715/M45CE0B  10-12 03:03:51.376  5159  5159 E CAM_FatalErrorHandler:  at com.android.camera.FatalErrorHandlerImpl.onCameraOpenFailure(FatalErrorHandlerImpl.java:49)
./009-1012_023242--1012_030715/M45CE0B  10-12 03:03:51.376  5159  5159 E CAM_FatalErrorHandler:  at com.android.camera.CameraActivity$9.run(CameraActivity.java:609)
./009-1012_023242--1012_030715/M45CE0B  10-12 03:03:51.376  5159  5159 E CAM_FatalErrorHandler:  at android.os.Handler.handleCallback(Handler.java:938)
./009-1012_023242--1012_030715/M45CE0B  10-12 03:03:51.376  5159  5159 E CAM_FatalErrorHandler:  at android.os.Handler.dispatchMessage(Handler.java:99)
./009-1012_023242--1012_030715/M45CE0B  10-12 03:03:51.376  5159  5159 E CAM_FatalErrorHandler:  at android.os.Looper.loopOnce(Looper.java:201)
./009-1012_023242--1012_030715/M45CE0B  10-12 03:03:51.376  5159  5159 E CAM_FatalErrorHandler:  at android.os.Looper.loop(Looper.java:288)
./009-1012_023242--1012_030715/M45CE0B  10-12 03:03:51.376  5159  5159 E CAM_FatalErrorHandler:  at android.app.ActivityThread.main(ActivityThread.java:7941)
./009-1012_023242--1012_030715/M45CE0B  10-12 03:03:51.376  5159  5159 E CAM_FatalErrorHandler:  at java.lang.reflect.Method.invoke(Native Method)
./009-1012_023242--1012_030715/M45CE0B  10-12 03:03:51.376  5159  5159 E CAM_FatalErrorHandler:  at com.android.internal.os.RuntimeInit$MethodAndArgsCaller.run(RuntimeInit.java:553)
./009-1012_023242--1012_030715/M45CE0B  10-12 03:03:51.376  5159  5159 E CAM_FatalErrorHandler:  at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:1003)
./009-1012_023242--1012_030715/M45DBEE  10-12 03:04:04.913  5159  5159 E CAM_FatalErrorHandler: Handling Fatal Error:
./009-1012_023242--1012_030715/M45DBEE  10-12 03:04:04.913  5159  5159 E CAM_FatalErrorHandler: java.lang.Exception
./009-1012_023242--1012_030715/M45DBEE  10-12 03:04:04.913  5159  5159 E CAM_FatalErrorHandler:  at com.android.camera.FatalErrorHandlerImpl.handleFatalError(FatalErrorHandlerImpl.java:117)
./009-1012_023242--1012_030715/M45DBEE  10-12 03:04:04.913  5159  5159 E CAM_FatalErrorHandler:  at com.android.camera.CameraActivity$16.onFatalError(CameraActivity.java:1064)
./009-1012_023242--1012_030715/M45DBEE  10-12 03:04:04.913  5159  5159 E CAM_FatalErrorHandler:  at com.android.camera.CameraActivity$16.onCameraException(CameraActivity.java:1043)
./009-1012_023242--1012_030715/M45DBEE  10-12 03:04:04.913  5159  5159 E CAM_FatalErrorHandler:  at com.android.ex.camera2.portability.CameraExceptionHandler$3.run(CameraExceptionHandler.java:103)
./009-1012_023242--1012_030715/M45DBEE  10-12 03:04:04.913  5159  5159 E CAM_FatalErrorHandler:  at android.os.Handler.handleCallback(Handler.java:938)
./009-1012_023242--1012_030715/M45DBEE  10-12 03:04:04.913  5159  5159 E CAM_FatalErrorHandler:  at android.os.Handler.dispatchMessage(Handler.java:99)
./009-1012_023242--1012_030715/M45DBEE  10-12 03:04:04.913  5159  5159 E CAM_FatalErrorHandler:  at android.os.Looper.loopOnce(Looper.java:201)
./009-1012_023242--1012_030715/M45DBEE  10-12 03:04:04.913  5159  5159 E CAM_FatalErrorHandler:  at android.os.Looper.loop(Looper.java:288)
./009-1012_023242--1012_030715/M45DBEE  10-12 03:04:04.913  5159  5159 E CAM_FatalErrorHandler:  at android.app.ActivityThread.main(ActivityThread.java:7941)
./009-1012_023242--1012_030715/M45DBEE  10-12 03:04:04.913  5159  5159 E CAM_FatalErrorHandler:  at java.lang.reflect.Method.invoke(Native Method)
./009-1012_023242--1012_030715/M45DBEE  10-12 03:04:04.913  5159  5159 E CAM_FatalErrorHandler:  at com.android.internal.os.RuntimeInit$MethodAndArgsCaller.run(RuntimeInit.java:553)
./009-1012_023242--1012_030715/M45DBEE  10-12 03:04:04.913  5159  5159 E CAM_FatalErrorHandler:  at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:1003)
```## 162261 手动调节ISO感光度，拍照后查看照片详情，详情中的ISO值与实际设置的不符合

```text
10-15 14:47:37.701 20240 20240 E DataModuleBasic: user change settings key = pref_camera_iso_key old value = iso_1600 new value = iso_3200
10-15 14:47:37.701   521 25538 D cmr_prev: 15671, prev_set_preview_buffer: cam_id=0, fd=0x5a, chn_id=0x1, valid_num=4, phy_y=0x0,vir_y=0xdc630000,fmt=16,buffer_size=0xfd200
10-15 14:47:37.701 20240 20240 E DataModuleBasic: all change :     key = pref_camera_iso_key value = iso_3200
10-15 14:47:37.701 20240 20240 E DataModuleBasic: notify user Key Change  :     key = pref_camera_iso_key value = iso_3200
10-15 14:47:37.701 20240 20240 E CAM_BMDream: updatePhotoButtonItems key = pref_camera_iso_key
10-15 14:47:37.701 20240 20240 E CAM_BMDream: updatePhotoButtonItems index = 0
10-15 14:47:37.701 20240 20240 D CAM_PhotoModule: onSettingChanged key = pref_camera_iso_key value = iso_3200
10-15 14:47:37.701 20240 20240 D CAM_PhotoModule: updateParametersISO = iso_3200
10-15 14:47:37.701 20240 20240 D CAM_PhotoModule: use aosp iso updateParametersISO isoValue= 3200
10-15 14:47:37.702 20240 20240 D CAM_PhotoModule: updateParametersISO = iso_3200
10-15 14:47:37.702 20240 20240 D CAM_PhotoModule: use aosp iso updateParametersISO isoValue= 3200
10-15 14:47:37.702 20240 20281 I CAM2PORT_DispatchThread: Runnable job.run() end!
10-15 14:47:37.702 20240 20281 I CAM2PORT_DispatchThread: DispatchThread.this.wait will!
10-15 14:47:37.702 20240 20280 I CAM2PORT_AndCam2AgntImp: AppFW handleMessage - action = 'APPLY_SETTINGS'
10-15 14:47:37.703 20240 20280 I CAM2PORT_AndCam2Set: mExposureCompensationIndex 0
10-15 14:47:37.703 20240 20280 I CAM2PORT_AndCam2Set: set CONTROL_AWB_MODE 1
10-15 14:47:37.704 20240 20240 D ViewRootImpl: ViewRootImpl performMeasure , childWidthMeasureSpec = 1073742544, childHeightMeasureSpec = 1073743464, mTag=ViewRootImpl[CameraActivity] ,this = android.view.UnisocViewRootImpl@af66c7d
10-15 14:47:37.704 20240 20280 I CAM2PORT_SprdAndCam2Set: use aosp iso, iso value=3200

10-15 14:47:37.725 20240 20280 I CAM2PORT_SprdAndCam2Set: use aosp iso, iso value=3200

10-15 14:47:37.767   521   521 D Cam3Setting: 6349, updateIspParameters: ae mode 0, is_push 1
10-15 14:47:37.767   521   521 D Cam3Setting: 6372, updateIspParameters: sensor sensitivity is 3200
10-15 14:47:37.768   521   521 D Cam3Setting: 5195, updateWorkParameters: mTopID 0
10-15 14:47:37.768   521   521 D Cam3Setting: 5344, updateWorkParameters: slowmotion 1
10-15 14:47:37.768   521   521 D Cam3Setting: 5549, updateWorkParameters: Enable Zsl = 0
10-15 14:47:37.769   521   521 D Cam3Setting: 5565, updateWorkParameters: lens focal len is 3.643000
10-15 14:47:37.769   521   521 D Cam3Setting: 5777, updateWorkParameters: sprd_flash_level =0
10-15 14:47:37.769   521   521 D Cam3Setting: 5789, updateWorkParameters: flashInfo.mode=0,value=0
10-15 14:47:37.769   521   521 D Cam3Setting: 5814, updateWorkParameters: ae_exposure_compensation=0
10-15 14:47:37.769   521   521 D Cam3Setting: 6054, updateWorkParameters: AE target fps min 5, max 30
10-15 14:47:37.769   521   521 D Cam3Setting: 6126, updateWorkParameters: AF control mode 4

10-15 14:53:20.666   521 26106 D cmr_oem : 21166, camera_local_set_exif_iso_value: exif iso_value:2500

    if (setting_param.cmd_type_value != -1) {
        camera_get_iso_info(oem_handle, &iso_value);
        camera_local_set_exif_iso_value(oem_handle, iso_value);
        if(!cxt->long_expo_enable) {
            camera_get_adgain_exp_info(oem_handle, &exp_info);
            camera_local_set_exif_exp_time(oem_handle, exp_info.exp_time);
        }
    }

static cmr_int setting_set_callback_sensitivity(struct setting_component *cpt,
                               struct setting_cmd_parameter *parm) {
    cmr_int ret = 0;
    struct setting_hal_param *hal_param = get_hal_param(cpt, parm->camera_id);
    hal_param->hal_callback_stream_info.sensitivity= parm->cmd_type_value;
    CMR_LOGD("set callback stream sensitivity %ld", parm->cmd_type_value);

    return ret;
}

void camera_get_iso_value(cmr_handle oem_handle) {
    struct camera_context *cxt = (struct camera_context *)oem_handle;
    cmr_u32 isp_param = 0;
    if (cxt->isp_cxt.is_work && (1 == cxt->setting_cxt.is_auto_iso)) {          // is_auto_iso
        struct isp_context *isp_cxt = &cxt->isp_cxt;
        isp_capability(isp_cxt->isp_handle, ISP_CUR_ISO, (void *)&isp_param);
        CMR_LOGD("iso value is %d", isp_param);
        cmr_sensor_set_exif(cxt->sn_cxt.sensor_handle, cxt->camera_id,
                            SENSOR_EXIF_CTRL_ISOSPEEDRATINGS, isp_param);
    }
}
```## 去掉人脸属性检测菜单

```text
#face detect
TARGET_BOARD_CAMERA_FACE_DETECT := true
#face race_gender_age detect version 0--old Algorithm library 1--new Algorithm library
TARGET_BOARD_SPRD_FD_VERSION := 0
```## OTP/EEPROM 读取与处理

```text
https://blog.csdn.net/Jingnian_destiny/article/details/102537447
```## AW Portrait 算法

```text
// 1.初始化 TextureView
mTextureView = new TextureView(this);
mTextureView.setLayoutParams(layoutParams);
mRootView.addView(mTextureView);
mTextureView.setSurfaceTextureListener(this);   //设置 SurfaceTextureListener 监听器，就是下面的四个回调函数

// 2.在 SurfaceTextureListener 的 onSurfaceTextureAvailable() 回调方法中初始化 SurfaceTextureRenderer
@Override
public void onSurfaceTextureAvailable(SurfaceTexture surface, int width, int height) {
    surfaceTextureRenderer = new SurfaceTextureRenderer(surface, mTextureView.getWidth(), mTextureView.getHeight());
}
void onSurfaceTextureSizeChanged(@NonNull SurfaceTexture surface, int width, int height);
boolean onSurfaceTextureDestroyed(@NonNull SurfaceTexture surface);
void onSurfaceTextureUpdated(@NonNull SurfaceTexture surface);

// 3.打开相机
mCameraEngine = new Camera2Engine(this, this);
mCameraEngine.openCamera(mCameraID);

// 4.在onCameraOpened 的时候设置 surfaceTextureRenderer
@Override
public void onCameraOpened(Camera2Capabilities capabilities, Size previewSize) {
    ...
    try {
        while (surfaceTextureRenderer == null) {
            Thread.sleep(50);
        }
    } catch (InterruptedException e) {
        e.printStackTrace();
    }
    surfaceTextureRenderer.acquireSurfaceTexture(previewSize.getWidth(), previewSize.getHeight(), new SurfaceTextureListener() {
        public void onSurfaceTextureAvailable(final SurfaceTexture surface, int texId, int width, int height) {
            mCameraEngine.setOrientation(mOrientation);
            mDrawer.setJpegOrientation(CameraUtil.getJpegRotation(isFront ? 1 : 0, mOrientation));
            mCameraEngine.startPreview(surface);
            isCameraOpen = true;
            mDrawer.initFilter(true);
        }
        public boolean needUpdateFrame() {
            return true;
        }
        public void onFrameAvailable(int textureId, long timestamp, float[] transform, int previewW, int previewH, int outW, int outH) {
            if (!CameraPreferencesConfig.isYuvPreviewSource) {
                mDrawer.addTextureFrame(textureId, true, timestamp, previewW, previewH, mCurrentExpTime);
            }
            mDrawer.onDrawFrame(transform, outW, outH, 0);
        }
        public void onSurfaceTextrueDestroy(SurfaceTexture surfaceTexture) {
            mDrawer.destoryFilter();
        }
    });
}


初始化
PortraitPlusPreviewJni.init(portraitPlusManager.getLicensePath() + "/" + PortraitPlusManager.LICENSE_FILE_NAME, maskModelInfo);

设置预览数据
PortraitPlusPreviewJni.setPreviewData(fabbytmp, mWidth, mHeight, ImageFormat.NV21, mFaceOrientation);

if (mHasFace) {
    绘制人像虚化，需要在OpenGL线程中调用
    PortraitPlusPreviewJni.drawFrame(inFrame.textureID, inFrame.isOes, inFrame.width, inFrame.height, fboId, outWidth, outHeight, transform, mBlurLevel, 1.0f);
} else {
    GLUTJni.drawTexture(mGLUTNative, inFrame.textureID, inFrame.isOes, outWidth, outHeight, transform, fboId);
}

//拍照按钮事件
findViewById(R.id.shutter_button).setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
        mCameraEngine.capture(ImageFormat.JPEG);
    }
});


// 保存图片
public void onPictureTaken(byte[] data, int width, int height, int orientation) {
    ...
    Bitmap source = ImageUtil.createSourceBitmap(data, 1);
    Bitmap dst = Bitmap.createBitmap(source);
    ByteBuffer buffer = ByteBuffer.allocateDirect(source.getByteCount());
    source.copyPixelsToBuffer(buffer);
    PortraitPlusJni.PortraitResult result = new PortraitPlusJni.PortraitResult();
    int ret = mPortraitPlusManager.processPortrait(buffer.array(), PortraitPlusJni.IMAGE_FORMAT_RGBA8888, source.getWidth(), source.getHeight(), 0, mBlurLevel, 3, 5000, result);
    buffer.clear();
    if (ret == PortraitPlusJni.AW_PORTRAIT_PLUS_SUCCESS) {
        dst.copyPixelsFromBuffer(ByteBuffer.wrap(result.data));
    }
    byte[] jpeg = ImageUtil.bitmapToJpeg(dst, 95);
    long fileLength = ExifInterface.writeImage(CameraPreferencesConfig.SAVE_PATH + titleOut, exif, jpeg);
    ...
}

// jpeg2yuv
YuvImageEx yuvImageHandle = YuvImageEx.decodeJpegToYuv(data, ImageFormat.NV21);
int imageW = yuvImageHandle.getWidth();
int imageH = yuvImageHandle.getHeight();

// yuv2jpeg
ByteArrayOutputStream outJpeg = new ByteArrayOutputStream();
boolean encodeSuccess = YuvImageEx.encodeYuvToJpeg(encoderPara, outJpeg);
byte[] jpgData = outJpeg.toByteArray();
try {
    outJpeg.close();
} catch (Exception e) {
    e.printStackTrace();
}

// 从 jpeg 数据流中获取 width/height
ImageUtil.java
public static Size getJpegSize(byte[] jpegData) {
    try {
        ExifInterface exifInterface = new ExifInterface(new ByteArrayInputStream(jpegData));
        int imageWidth = exifInterface.getAttributeInt(ExifInterface.TAG_IMAGE_WIDTH, 0);
        int imageLength = exifInterface.getAttributeInt(ExifInterface.TAG_IMAGE_LENGTH, 0);
        return new Size(imageWidth, imageLength);
    } catch (IOException e) {
        e.printStackTrace();
    }
    return null;
}
```## 导入 AIWORKS Portrait 算法

```text
10-20 11:03:46.364  5410  5410 F .app.cameralit: thread.cc:2372] Throwing new exception 'no "I" field "height" in class "Lcom/aiworks/android/portrait/PortraitPlusJni$PortraitResult;" or its superclasses' with unexpected pending exception: java.lang.NoSuchFieldError: no "I" field "width" in class "Lcom/aiworks/android/portrait/PortraitPlusJni$PortraitResult;" or its superclasses
10-20 11:03:46.364  5410  5410 F .app.cameralit: thread.cc:2372]   at int com.aiworks.android.portrait.PortraitPlusJni.process(byte[], int, int, int, int, int, int, int, int, com.aiworks.android.portrait.PortraitPlusJni$PortraitResult) (PortraitPlusJni.java:-2)
10-20 11:03:46.364  5410  5410 F .app.cameralit: thread.cc:2372]   at int com.aiworks.android.PortraitPlusManager.processPortrait(byte[], int, int, int, int, int, int, int, com.aiworks.android.portrait.PortraitPlusJni$PortraitResult) (PortraitPlusManager.java:52)
10-20 11:03:46.364  5410  5410 F .app.cameralit: thread.cc:2372]   at void com.android.camera.PhotoModule.processPortrait(byte[]) (PhotoModule.java:2999)
10-20 11:03:46.364  5410  5410 F .app.cameralit: thread.cc:2372]   at void com.android.camera.PhotoModule.access$5200(com.android.camera.PhotoModule, byte[]) (PhotoModule.java:185)
10-20 11:03:46.364  5410  5410 F .app.cameralit: thread.cc:2372]   at void com.android.camera.PhotoModule$JpegPictureCallback.saveFinalPhoto(byte[], com.android.camera.PhotoModule$NamedImages$NamedEntity, com.android.camera.exif.ExifInterface, com.android.ex.camera2.portability.CameraAgent$CameraProxy, boolean) (PhotoModule.java:2934)
10-20 11:03:46.364  5410  5410 F .app.cameralit: thread.cc:2372]   at void com.android.camera.PhotoModule$JpegPictureCallback.onPictureTaken(byte[], com.android.ex.camera2.portability.CameraAgent$CameraProxy, boolean) (PhotoModule.java:2633)
10-20 11:03:46.364  5410  5410 F .app.cameralit: thread.cc:2372]   at void com.android.camera.PhotoModule$JpegPictureCallback.onPictureTaken(byte[], com.android.ex.camera2.portability.CameraAgent$CameraProxy) (PhotoModule.java:2492)
10-20 11:03:46.364  5410  5410 F .app.cameralit: thread.cc:2372]   at void com.android.ex.camera2.portability.SprdAndroidCamera2AgentImpl$SprdAndroidCamera2ProxyImpl$1.run() (SprdAndroidCamera2AgentImpl.java:1501)
10-20 11:03:46.364  5410  5410 F .app.cameralit: thread.cc:2372]   at void android.os.Handler.handleCallback(android.os.Message) (Handler.java:938)
10-20 11:03:46.364  5410  5410 F .app.cameralit: thread.cc:2372]   at void android.os.Handler.dispatchMessage(android.os.Message) (Handler.java:99)
10-20 11:03:46.364  5410  5410 F .app.cameralit: thread.cc:2372]   at boolean android.os.Looper.loopOnce(android.os.Looper, long, int) (Looper.java:201)
10-20 11:03:46.364  5410  5410 F .app.cameralit: thread.cc:2372]   at void android.os.Looper.loop() (Looper.java:288)
10-20 11:03:46.364  5410  5410 F .app.cameralit: thread.cc:2372]   at void android.app.ActivityThread.main(java.lang.String[]) (ActivityThread.java:7941)
10-20 11:03:46.364  5410  5410 F .app.cameralit: thread.cc:2372]   at java.lang.Object java.lang.reflect.Method.invoke(java.lang.Object, java.lang.Object[]) (Method.java:-2)
10-20 11:03:46.364  5410  5410 F .app.cameralit: thread.cc:2372]   at void com.android.internal.os.RuntimeInit$MethodAndArgsCaller.run() (RuntimeInit.java:553)
10-20 11:03:46.364  5410  5410 F .app.cameralit: thread.cc:2372]   at void com.android.internal.os.ZygoteInit.main(java.lang.String[]) (ZygoteInit.java:1003)

解决方案：
在 vendor/sprd/platform/packages/apps/DreamCamera2/proguard.flags 文件中加上
-keep class com.aiworks.android.portrait.** {*;}
```## Portrait拍照

```text
PhotoModule.java
private byte[] processPortrait(byte[] jpeg) {
    PortraitPlusManager mPortraitPlusManager = PortraitPlusManager.getInstance();
    mPortraitPlusManager.copyModel(mActivity);
    mPortraitPlusManager.copyLicense(mActivity);
    mPortraitPlusManager.init(false);
    Bitmap source = ImageUtil.createSourceBitmap(jpeg, 1);
    Bitmap dst = Bitmap.createBitmap(source);
    ByteBuffer buffer = ByteBuffer.allocateDirect(source.getByteCount());
    source.copyPixelsToBuffer(buffer);
    PortraitPlusJni.PortraitResult result = new PortraitPlusJni.PortraitResult();
    int mBlurLevel = 3;
    int ret = mPortraitPlusManager.processPortrait(buffer.array(), PortraitPlusJni.IMAGE_FORMAT_RGBA8888, source.getWidth(), source.getHeight(), 0, mBlurLevel, 3, 5000, result);
    buffer.clear();
    if (ret == PortraitPlusJni.AW_PORTRAIT_PLUS_SUCCESS) {
        dst.copyPixelsFromBuffer(ByteBuffer.wrap(result.data));
    }
    return ImageUtil.bitmapToJpeg(dst, 95);
}



SampleTextureView.java
Executors.newSingleThreadExecutor().submit(() -> {
    ExifInterface exif = new ExifInterface();
    try {
        exif.readExif(data);
    } catch (IOException e) {
        Log.w(TAG, "Failed to read EXIF data", e);
    }
    long dateTaken = System.currentTimeMillis();
    Date date = new Date(dateTaken);
    SimpleDateFormat dateFormat = new SimpleDateFormat("'IMG'_yyyyMMdd_HHmmss", Locale.US);
    Bitmap source = ImageUtil.createSourceBitmap(data, 1);
    Bitmap dst = Bitmap.createBitmap(source);
    ByteBuffer buffer = ByteBuffer.allocateDirect(source.getByteCount());
    source.copyPixelsToBuffer(buffer);
    PortraitPlusJni.PortraitResult result = new PortraitPlusJni.PortraitResult();
    int ret = mPortraitPlusManager.processPortrait(buffer.array(), PortraitPlusJni.IMAGE_FORMAT_RGBA8888, source.getWidth(), source.getHeight(), 0, mBlurLevel, 3, 5000, result);
    buffer.clear();
    if (ret == PortraitPlusJni.AW_PORTRAIT_PLUS_SUCCESS) {
        dst.copyPixelsFromBuffer(ByteBuffer.wrap(result.data));
    }
    String titleOut = dateFormat.format(date) + "_PortraitOut.jpg";
    byte[] jpeg = ImageUtil.bitmapToJpeg(dst, 95);
    long fileLength = ExifInterface.writeImage(CameraPreferencesConfig.SAVE_PATH + titleOut, exif, jpeg);
    if (fileLength > 0) {
        Uri mUri = ImageUtil.insertContent(SampleTextureView.this, CameraPreferencesConfig.SAVE_PATH + titleOut, titleOut, fileLength);
        if (!mPause) {
            mThumbnail.updateThumbnailUri(mUri);
        }
    }
    source.recycle();
    dst.recycle();
});


mPreviewReader.setOnImageAvailableListener(mPreviewCallback, this);
        @Override
        public void setPreviewDataCallback(Handler handler, CameraPreviewDataCallback cb) {
            mPreviewCallback = CameraPreViewCallbackForward.getNewInstance(handler,
                    SprdAndroidCamera2ProxyImpl.this, cb);
        }
```## Condor人像模式配流 4000x3000 是哪里来的？

```text
<string name="CachedSupportedPictureSizes_Sizes_Camera24">4000,3000</string>
<string name="CachedSupportedPictureSizes_Sizes_Camera38">4000,3000</string>

media.camera
== Camera HAL device device@3.5/legacy/24 (v3.5) static information: ==
        ...
      android.scaler.availableStreamConfigurations (d000a): int32[64]
        [35 4000 3000 OUTPUT ]
        [35 960 720 OUTPUT ]
        [35 320 240 OUTPUT ]
        [35 256 144 OUTPUT ]

== Camera HAL device device@3.5/legacy/38 (v3.5) static information: ==
        ...
      android.scaler.availableStreamConfigurations (d000a): int32[64]
        [35 4000 3000 OUTPUT ]
        [35 960 720 OUTPUT ]
        [35 320 240 OUTPUT ]
        [35 256 144 OUTPUT ]
        [34 4000 3000 OUTPUT ]
        [34 960 720 OUTPUT ]
        [34 320 240 OUTPUT ]
        [34 256 144 OUTPUT ]
        [32 4000 3000 OUTPUT ]
        [32 960 720 OUTPUT ]
        [32 320 240 OUTPUT ]
        [32 256 144 OUTPUT ]
        [33 4000 3000 OUTPUT ]
        [33 960 720 OUTPUT ]
        [33 320 240 OUTPUT ]
        [33 256 144 OUTPUT ]

log:
10-18 23:28:33.727   504  8807 D CamPortrait: 3558, configureStreams: main configurestreams, streamtype:0, format:33, width:4000, height:3000 0xeab50c70
10-18 23:28:33.727   504  8807 I CamPortrait: 3566, configureStreams: mum_streams:3,2,w,h:(800,600)(4000,3000)(800,600)(960,720)),mIsSupportPBokeh:0,

file:
vendor/sprd/modules/libcamera/hal_common/multiCamera/SprdCamera3Portrait.cpp
int SprdCamera3Portrait::configureStreams(
    const struct camera3_device *device,
    camera3_stream_configuration_t *stream_list) {
```## [CTS]NVA CTS fail-----SensorPrivacyCameraTest#testOpStartsRunningAfterStartedWithSensoryPrivacyEnabled

```text
android.sensorprivacy.cts.SensorPrivacyCameraTest#testOpStartsRunningAfterStartedWithSensoryPrivacyEnabled

java.lang.RuntimeException: java.lang.AssertionError: Unexpected op running state expected:&lt;true&gt; but was:&lt;false&gt;
 at com.android.compatibility.common.util.SystemUtil.eventually(SystemUtil.java:357)
 at com.android.compatibility.common.util.SystemUtil.eventually(SystemUtil.java:332)
 at android.sensorprivacy.cts.SensorPrivacyBaseTest.testOpStartsRunningAfterStartedWithSensoryPrivacyEnabled(SensorPrivacyBaseTest.kt:257)
 ... 8 trimmed
Caused by: java.lang.AssertionError: Unexpected op running state expected:&lt;true&gt; but was:&lt;false&gt;
 at org.junit.Assert.fail(Assert.java:89)
 at org.junit.Assert.failNotEquals(Assert.java:835)
 at org.junit.Assert.assertEquals(Assert.java:120)
 at android.sensorprivacy.cts.SensorPrivacyBaseTest.assertOpRunning(SensorPrivacyBaseTest.kt:410)
 at android.sensorprivacy.cts.SensorPrivacyBaseTest.access$assertOpRunning(SensorPrivacyBaseTest.kt:53)
 at android.sensorprivacy.cts.SensorPrivacyBaseTest$testOpStartsRunningAfterStartedWithSensoryPrivacyEnabled$1.run(SensorPrivacyBaseTest.kt:258)
 at com.android.compatibility.common.util.SystemUtil.eventually(SystemUtil.java:347)
 ... 11 more

@Test
@AppModeFull(reason = "Uses secondary app, instant apps have no visibility")
fun testOpStartsRunningAfterStartedWithSensoryPrivacyEnabled() {
    setSensor(true)
    startTestApp()
    UiAutomatorUtils.waitFindObject(By.text(
            Pattern.compile("Cancel", Pattern.CASE_INSENSITIVE))).click()
    assertOpRunning(false)
    setSensor(false)
    eventually {
        assertOpRunning(true)
    }
}

private fun assertOpRunning(isRunning: Boolean) {
    val pkgOp = getOpForPackage()
    for (op in pkgOp.ops) {
        for ((_, attrOp) in op.attributedOpEntries) {
            assertEquals("Unexpected op running state", isRunning, attrOp.isRunning)
        }
    }
}

private fun getOpForPackage(): AppOpsManager.PackageOps {
    return callWithShellPermissionIdentity {
        val uid = try {
            packageManager.getPackageUid(PKG_NAME, 0)                       //const val PKG_NAME = "android.sensorprivacy.cts.usemiccamera"
        } catch (e: PackageManager.NameNotFoundException) {
            // fail test
            assertNull(e)
            -1
        }
        val appOpsManager: AppOpsManager =
                context.getSystemService(AppOpsManager::class.java)!!
        val pkgOps = appOpsManager.getOpsForPackage(uid, PKG_NAME, op)
        assertFalse("expected non empty app op list", pkgOps.isEmpty())
        pkgOps[0]
    }
}


private fun startTestApp() {
    val intent = Intent(MIC_CAM_ACTIVITY_ACTION)                //android.sensorprivacy.cts.usemiccamera.action.FINISH_USE_MIC_CAM
            .addFlags(Intent.FLAG_ACTIVITY_NEW_TASK)
            .addFlags(Intent.FLAG_ACTIVITY_MATCH_EXTERNAL)
    for (extra in extras) {
        intent.putExtra(extra, true)
    }
    context.startActivity(intent)
    // Wait for app to open
    UiAutomatorUtils.waitFindObject(By.textContains(ACTIVITY_TITLE_SNIP))
}

# atest again
atest SensorPrivacyCameraTest

android.sensorprivacy.cts.SensorPrivacyCameraTest#testOpStartsRunningAfterStartedWithSensoryPrivacyEnabled
android.sensorprivacy.cts.SensorPrivacyCameraTest#testOpGetsRecordedAfterStartedWithSensorPrivacyEnabled

10-21 20:52:29.148 11883 11883 E AndroidRuntime: FATAL EXCEPTION: main
10-21 20:52:29.148 11883 11883 E AndroidRuntime: Process: android.sensorprivacy.cts.usemiccamera, PID: 11883
10-21 20:52:29.148 11883 11883 E AndroidRuntime: java.lang.RuntimeException: java.lang.reflect.InvocationTargetException
10-21 20:52:29.148 11883 11883 E AndroidRuntime:  at com.android.internal.os.RuntimeInit$MethodAndArgsCaller.run(RuntimeInit.java:563)
10-21 20:52:29.148 11883 11883 E AndroidRuntime:  at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:1003)
10-21 20:52:29.148 11883 11883 E AndroidRuntime: Caused by: java.lang.reflect.InvocationTargetException
10-21 20:52:29.148 11883 11883 E AndroidRuntime:  at java.lang.reflect.Method.invoke(Native Method)
10-21 20:52:29.148 11883 11883 E AndroidRuntime:  at com.android.internal.os.RuntimeInit$MethodAndArgsCaller.run(RuntimeInit.java:553)
10-21 20:52:29.148 11883 11883 E AndroidRuntime:  ... 1 more
10-21 20:52:29.148 11883 11883 E AndroidRuntime: Caused by: android.hardware.camera2.CameraAccessException: CAMERA_DISABLED (1): connectHelper:1897: Camera "0" disabled due to camera mute
10-21 20:52:29.148 11883 11883 E AndroidRuntime:  at android.hardware.camera2.CameraManager.throwAsPublicException(CameraManager.java:1179)
10-21 20:52:29.148 11883 11883 E AndroidRuntime:  at android.hardware.camera2.CameraManager.openCameraDeviceUserAsync(CameraManager.java:616)
10-21 20:52:29.148 11883 11883 E AndroidRuntime:  at android.hardware.camera2.CameraManager.openCameraForUid(CameraManager.java:866)
10-21 20:52:29.148 11883 11883 E AndroidRuntime:  at android.hardware.camera2.CameraManager.openCameraForUid(CameraManager.java:887)
10-21 20:52:29.148 11883 11883 E AndroidRuntime:  at android.hardware.camera2.CameraManager.openCamera(CameraManager.java:765)
10-21 20:52:29.148 11883 11883 E AndroidRuntime:  at android.sensorprivacy.cts.usemiccamera.UseMicCamera.openCam(UseMicCamera.kt:160)
10-21 20:52:29.148 11883 11883 E AndroidRuntime:  at android.sensorprivacy.cts.usemiccamera.UseMicCamera.access$openCam(UseMicCamera.kt:45)
10-21 20:52:29.148 11883 11883 E AndroidRuntime:  at android.sensorprivacy.cts.usemiccamera.UseMicCamera$onCreate$3.run(UseMicCamera.kt:88)
10-21 20:52:29.148 11883 11883 E AndroidRuntime:  at android.os.Handler.handleCallback(Handler.java:938)
10-21 20:52:29.148 11883 11883 E AndroidRuntime:  at android.os.Handler.dispatchMessage(Handler.java:99)
10-21 20:52:29.148 11883 11883 E AndroidRuntime:  at android.os.Looper.loopOnce(Looper.java:201)
10-21 20:52:29.148 11883 11883 E AndroidRuntime:  at android.os.Looper.loop(Looper.java:288)
10-21 20:52:29.148 11883 11883 E AndroidRuntime:  at android.app.ActivityThread.main(ActivityThread.java:7941)
10-21 20:52:29.148 11883 11883 E AndroidRuntime:  ... 3 more
10-21 20:52:29.148 11883 11883 E AndroidRuntime: Caused by: android.os.ServiceSpecificException: connectHelper:1897: Camera "0" disabled due to camera mute (code 6)
10-21 20:52:29.148 11883 11883 E AndroidRuntime:  at android.os.Parcel.createExceptionOrNull(Parcel.java:2440)
10-21 20:52:29.148 11883 11883 E AndroidRuntime:  at android.os.Parcel.createException(Parcel.java:2410)
10-21 20:52:29.148 11883 11883 E AndroidRuntime:  at android.os.Parcel.readException(Parcel.java:2393)
10-21 20:52:29.148 11883 11883 E AndroidRuntime:  at android.os.Parcel.readException(Parcel.java:2335)
10-21 20:52:29.148 11883 11883 E AndroidRuntime:  at android.hardware.ICameraService$Stub$Proxy.connectDevice(ICameraService.java:669)
10-21 20:52:29.148 11883 11883 E AndroidRuntime:  at android.hardware.camera2.CameraManager.openCameraDeviceUserAsync(CameraManager.java:596)
10-21 20:52:29.148 11883 11883 E AndroidRuntime:  ... 14 more



10-21 21:00:46.118  2390  2461 W System.err: android.content.pm.PackageManager$NameNotFoundException: android.sensorprivacy.cts.usemiccamera
10-21 21:00:46.119  2390  2461 W System.err:  at android.app.ApplicationPackageManager.getPackageInfoAsUser(ApplicationPackageManager.java:241)
10-21 21:00:46.119  2390  2461 W System.err:  at android.app.ApplicationPackageManager.getPackageInfo(ApplicationPackageManager.java:213)
10-21 21:00:46.119  2390  2461 W System.err:  at com.facebook.oxygen.appmanager.ui.offline.b.a_(OfflineInstallJobCleanup.java:26)
10-21 21:00:46.119  2390  2461 W System.err:  at com.facebook.oxygen.common.packages.b.c.a(DeltaPackageListenerDispatcher.java:45)
10-21 21:00:46.119  2390  2461 W System.err:  at com.facebook.oxygen.common.packages.b.e.a(DeltaPackageTracker.java:88)
10-21 21:00:46.119  2390  2461 W System.err:  at com.facebook.oxygen.common.packages.b.f.b(DeltaPackageWorker.java:99)
10-21 21:00:46.119  2390  2461 W System.err:  at com.facebook.oxygen.common.packages.b.f.a(DeltaPackageWorker.java:82)
10-21 21:00:46.119  2390  2461 W System.err:  at com.facebook.oxygen.common.jobqueue.a.c(JobQueueManager.java:297)
10-21 21:00:46.119  2390  2461 W System.err:  at com.facebook.oxygen.common.jobqueue.a.b(JobQueueManager.java:270)
10-21 21:00:46.120  2390  2461 W System.err:  at com.facebook.oxygen.common.jobqueue.JobQueueService.a(JobQueueService.java:84)
10-21 21:00:46.120  2390  2461 W System.err:  at androidx.core.app.j$a.a(JobIntentService.java:397)
10-21 21:00:46.120  2390  2461 W System.err:  at androidx.core.app.j$a.doInBackground(JobIntentService.java:387)
10-21 21:00:46.120  2390  2461 W System.err:  at android.os.AsyncTask$3.call(AsyncTask.java:394)
10-21 21:00:46.120  2390  2461 W System.err:  at java.util.concurrent.FutureTask.run(FutureTask.java:266)
10-21 21:00:46.120  2390  2461 W System.err:  at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1167)
10-21 21:00:46.120  2390  2461 W System.err:  at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:641)
10-21 21:00:46.126  2390  2461 W System.err:  at java.lang.Thread.run(Thread.java:920)
10-21 21:00:46.132  2390  2461 W System.err: android.content.pm.PackageManager$NameNotFoundException: android.sensorprivacy.cts
10-21 21:00:46.133  2390  2461 W System.err:  at android.app.ApplicationPackageManager.getPackageInfoAsUser(ApplicationPackageManager.java:241)
10-21 21:00:46.133  2390  2461 W System.err:  at android.app.ApplicationPackageManager.getPackageInfo(ApplicationPackageManager.java:213)
10-21 21:00:46.133  2390  2461 W System.err:  at com.facebook.oxygen.appmanager.ui.offline.b.a_(OfflineInstallJobCleanup.java:26)
10-21 21:00:46.133  2390  2461 W System.err:  at com.facebook.oxygen.common.packages.b.c.a(DeltaPackageListenerDispatcher.java:45)
10-21 21:00:46.133  2390  2461 W System.err:  at com.facebook.oxygen.common.packages.b.e.a(DeltaPackageTracker.java:88)
10-21 21:00:46.133  2390  2461 W System.err:  at com.facebook.oxygen.common.packages.b.f.b(DeltaPackageWorker.java:99)
10-21 21:00:46.133  2390  2461 W System.err:  at com.facebook.oxygen.common.packages.b.f.a(DeltaPackageWorker.java:82)
10-21 21:00:46.133  2390  2461 W System.err:  at com.facebook.oxygen.common.jobqueue.a.c(JobQueueManager.java:297)
10-21 21:00:46.133  2390  2461 W System.err:  at com.facebook.oxygen.common.jobqueue.a.b(JobQueueManager.java:270)
10-21 21:00:46.133  2390  2461 W System.err:  at com.facebook.oxygen.common.jobqueue.JobQueueService.a(JobQueueService.java:84)
10-21 21:00:46.133  2390  2461 W System.err:  at androidx.core.app.j$a.a(JobIntentService.java:397)
10-21 21:00:46.134  2390  2461 W System.err:  at androidx.core.app.j$a.doInBackground(JobIntentService.java:387)
10-21 21:00:46.134  2390  2461 W System.err:  at android.os.AsyncTask$3.call(AsyncTask.java:394)
10-21 21:00:46.134  2390  2461 W System.err:  at java.util.concurrent.FutureTask.run(FutureTask.java:266)
10-21 21:00:46.134  2390  2461 W System.err:  at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1167)
10-21 21:00:46.134  2390  2461 W System.err:  at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:641)
10-21 21:00:46.134  2390  2461 W System.err:  at java.lang.Thread.run(Thread.java:920)
```## TextureView不调用onSurfaceTextureDestroyed

```text
https://blog.csdn.net/qq_36356379/article/details/95456230

测试一：
xml中设置GONE，然后Activity中设置VISIBLE，只执行onAttachedToWindow。
测试二：
xml中设置VISIBLE，然后Activity设置GONE，只执行onAttachedToWindow。
测试三：
通过new对象的形式addview到布局中然后再removeview，先执行onAttachedToWindow然后执行onDetachedFromWindow。

结论：
调用GONE或者INVISIBLE不会让TextureView调用 onSurfaceTextureDestroyed，所以我们可以通过new对象的方式创建TextureView然后用父布局去addview和removeview。


被这个问题纠缠了几天，Google很久都没有找到答案，这个方法在点击下一个界面始终不调用destroy倒置绘制的东西会出问题，最后发现原因为在这个界面的主题上面添加了<item name="android:windowIsTranslucent">true</item>这个属性。去掉这行fuck code就可以了
```## DreamCamera2/Android.mk 中没有加 LOCAL_REQUIRED_MODULES += libaw_portrait_bokeh libaw_portrait_plus libc++_shared libaw_glut

```text
10-27 13:06:56.149   988  2258 I am_crash: [1251,0,com.hmdglobal.app.cameralite,551074885,java.lang.UnsatisfiedLinkError,dlopen failed: library "libaw_portrait_plus.so" not found,Runtime.java,1077]

解决方案：
LOCAL_REQUIRED_MODULES += libaw_portrait_bokeh libaw_portrait_plus libc++_shared libaw_glut
```## 人像模式切换前后摄之后 crash

```text
10-27 22:27:41.177  6086 12267 F .app.cameralit: runtime.cc:669]   native: #03 pc 00408507  /apex/com.android.art/lib/libart.so (art::Runtime::Abort(char const*)+1858)
10-27 22:27:41.177  6086 12267 F .app.cameralit: runtime.cc:669]   native: #04 pc 0000f5db  /system/lib/libbase.so (android::base::SetAborter(std::__1::function<void (char const*)>&&)::$_3::__invoke(char const*)+46)
10-27 22:27:41.177  6086 12267 F .app.cameralit: runtime.cc:669]   native: #05 pc 0000ef3b  /system/lib/libbase.so (android::base::LogMessage::~LogMessage()+234)
10-27 22:27:41.177  6086 12267 F .app.cameralit: runtime.cc:669]   native: #06 pc 0029f0d7  /apex/com.android.art/lib/libart.so (art::JavaVMExt::JniAbort(char const*, char const*)+1858)
10-27 22:27:41.177  6086 12267 F .app.cameralit: runtime.cc:669]   native: #07 pc 002e5f6f  /apex/com.android.art/lib/libart.so (art::JNI<false>::GetByteArrayElements(_JNIEnv*, _jbyteArray*, unsigned char*)+1126)
10-27 22:27:41.177  6086 12267 F .app.cameralit: runtime.cc:669]   native: #08 pc 000d3ac3  /system_ext/lib/libaw_portrait_plus.so (_JNIEnv::GetByteArrayElements(_jbyteArray*, unsigned char*)+48)
10-27 22:27:41.177  6086 12267 F .app.cameralit: runtime.cc:669]   native: #09 pc 000d767b  /system_ext/lib/libaw_portrait_plus.so (Java_com_aiworks_android_portrait_PortraitPlusPreviewJni_setPreviewData+66)
10-27 22:27:41.177  6086 12267 F .app.cameralit: runtime.cc:669]   native: #10 pc 000f4c8d  /apex/com.android.art/lib/libart.so (art_quick_generic_jni_trampoline+44)
10-27 22:27:41.177  6086 12267 F .app.cameralit: runtime.cc:669]   native: #11 pc 000eb35c  /apex/com.android.art/lib/libart.so (nterp_helper+172)
10-27 22:27:41.177  6086 12267 F .app.cameralit: runtime.cc:669]   native: #12 pc 000ad3dc  /system_ext/app/DreamCamera2/DreamCamera2.apk (offset 799000) (com.aiworks.android.glrenderer.PortraitDrawer$ModuleProcessHandler.handleMessage+480)
10-27 22:27:41.177  6086 12267 F .app.cameralit: runtime.cc:669]   native: #13 pc 00478791  /system/framework/arm/boot-framework.oat (android.os.Handler.dispatchMessage+152)
10-27 22:27:41.177  6086 12267 F .app.cameralit: runtime.cc:669]   native: #14 pc 0047acc1  /system/framework/arm/boot-framework.oat (android.os.Looper.loopOnce+1072)
10-27 22:27:41.177  6086 12267 F .app.cameralit: runtime.cc:669]   native: #15 pc 0047a817  /system/framework/arm/boot-framework.oat (android.os.Looper.loop+454)
10-27 22:27:41.177  6086 12267 F .app.cameralit: runtime.cc:669]   native: #16 pc 00479f45  /system/framework/arm/boot-framework.oat (android.os.HandlerThread.run+452)
10-27 22:27:41.177  6086 12267 F .app.cameralit: runtime.cc:669]   native: #17 pc 000f01d5  /apex/com.android.art/lib/libart.so (art_quick_invoke_stub_internal+68)
10-27 22:27:41.177  6086 12267 F .app.cameralit: runtime.cc:669]   native: #18 pc 00503ee3  /apex/com.android.art/lib/libart.so (art_quick_invoke_stub+282)
10-27 22:27:41.177  6086 12267 F .app.cameralit: runtime.cc:669]   native: #19 pc 001453a1  /apex/com.android.art/lib/libart.so (art::ArtMethod::Invoke(art::Thread*, unsigned int*, unsigned int, art::JValue*, char const*)+136)
10-27 22:27:41.177  6086 12267 F .app.cameralit: runtime.cc:669]   native: #20 pc 00402d8d  /apex/com.android.art/lib/libart.so (art::JValue art::InvokeVirtualOrInterfaceWithJValues<art::ArtMethod*>(art::ScopedObjectAccessAlreadyRunnable const&, _jobject*, art::ArtMethod*, jvalue const*)+368)
10-27 22:27:41.177  6086 12267 F .app.cameralit: runtime.cc:669]   native: #21 pc 00402e9b  /apex/com.android.art/lib/libart.so (art::JValue art::InvokeVirtualOrInterfaceWithJValues<_jmethodID*>(art::ScopedObjectAccessAlreadyRunnable const&, _jobject*, _jmethodID*, jvalue const*)+42)
10-27 22:27:41.177  6086 12267 F .app.cameralit: runtime.cc:669]   native: #22 pc 0044220b  /apex/com.android.art/lib/libart.so (art::Thread::CreateCallback(void*)+998)
10-27 22:27:41.177  6086 12267 F .app.cameralit: runtime.cc:669]   native: #23 pc 000a8ca7  /apex/com.android.runtime/lib/bionic/libc.so (__pthread_start(void*)+40)
10-27 22:27:41.177  6086 12267 F .app.cameralit: runtime.cc:669]   native: #24 pc 00061e85  /apex/com.android.runtime/lib/bionic/libc.so (__start_thread+30)
10-27 22:27:41.177  6086 12267 F .app.cameralit: runtime.cc:669]   at com.aiworks.android.portrait.PortraitPlusPreviewJni.setPreviewData(Native method)
10-27 22:27:41.177  6086 12267 F .app.cameralit: runtime.cc:669]   at com.aiworks.android.glrenderer.PortraitDrawer$ModuleProcessHandler.handleMessage(PortraitDrawer.java:100)
10-27 22:27:41.177  6086 12267 F .app.cameralit: runtime.cc:669]   at android.os.Handler.dispatchMessage(Handler.java:106)
10-27 22:27:41.177  6086 12267 F .app.cameralit: runtime.cc:669]   at android.os.Looper.loopOnce(Looper.java:201)
10-27 22:27:41.177  6086 12267 F .app.cameralit: runtime.cc:669]   at android.os.Looper.loop(Looper.java:288)
10-27 22:27:41.177  6086 12267 F .app.cameralit: runtime.cc:669]   at android.os.HandlerThread.run(HandlerThread.java:67)
10-27 22:27:41.177  6086 12267 F .app.cameralit: runtime.cc:669] 
10-27 22:27:41.177   518   915 D cmr_setting: 1780, setting_get_exif_info: zone_buf=+08:00
10-27 22:27:41.178   518   915 D cmr_setting: 1451, get_seconds_from_double: 0.000000, i=2, j=1, num=0 
10-27 22:27:41.178  6086 12267 F .app.cameralit: runtime.cc:677] JNI DETECTED ERROR IN APPLICATION: java_array == null
10-27 22:27:41.178  6086 12267 F .app.cameralit: runtime.cc:677]     in call to GetPrimitiveArray
10-27 22:27:41.178  6086 12267 F .app.cameralit: runtime.cc:677]     from void com.aiworks.android.portrait.PortraitPlusPreviewJni.setPreviewData(byte[], int, int, int, int)   // 这里空指针了，添加非空判断即可

解决方法：
```## Portrait 切换到 photo 闪退

```text
10-27 21:46:12.657 19945 21726 E AndroidRuntime: FATAL EXCEPTION: OnCreateAsync Task
10-27 21:46:12.657 19945 21726 E AndroidRuntime: Process: com.hmdglobal.app.cameralite, PID: 19945
10-27 21:46:12.657 19945 21726 E AndroidRuntime: android.view.ViewRootImpl$CalledFromWrongThreadException: Only the original thread that created a view hierarchy can touch its views.
10-27 21:46:12.657 19945 21726 E AndroidRuntime:  at android.view.ViewRootImpl.checkThread(ViewRootImpl.java:9426)
10-27 21:46:12.657 19945 21726 E AndroidRuntime:  at android.view.ViewRootImpl.requestLayout(ViewRootImpl.java:1806)
10-27 21:46:12.657 19945 21726 E AndroidRuntime:  at android.view.View.requestLayout(View.java:25880)
10-27 21:46:12.657 19945 21726 E AndroidRuntime:  at android.view.View.requestLayout(View.java:25880)
10-27 21:46:12.657 19945 21726 E AndroidRuntime:  at android.view.View.requestLayout(View.java:25880)
10-27 21:46:12.657 19945 21726 E AndroidRuntime:  at android.view.View.requestLayout(View.java:25880)
10-27 21:46:12.657 19945 21726 E AndroidRuntime:  at android.view.View.requestLayout(View.java:25880)
10-27 21:46:12.657 19945 21726 E AndroidRuntime:  at android.view.View.requestLayout(View.java:25880)
10-27 21:46:12.657 19945 21726 E AndroidRuntime:  at android.view.View.requestLayout(View.java:25880)
10-27 21:46:12.657 19945 21726 E AndroidRuntime:  at android.view.View.requestLayout(View.java:25880)
10-27 21:46:12.657 19945 21726 E AndroidRuntime:  at android.view.View.requestLayout(View.java:25880)
10-27 21:46:12.657 19945 21726 E AndroidRuntime:  at com.dream.camera.filter.SmallAdvancedFilter.requestLayout(SmallAdvancedFilter.java:395)
10-27 21:46:12.657 19945 21726 E AndroidRuntime:  at com.android.camera.PhotoModule.onSurfaceTextureUpdated(PhotoModule.java:1930)
10-27 21:46:12.657 19945 21726 E AndroidRuntime:  at com.android.camera.PhotoUI.onSurfaceTextureUpdated(PhotoUI.java:566)
10-27 21:46:12.657 19945 21726 E AndroidRuntime:  at com.dream.camera.modules.portraitphoto.HMDPortraitPhotoUI.onSurfaceTextureUpdated(HMDPortraitPhotoUI.java:334)
10-27 21:46:12.657 19945 21726 E AndroidRuntime:  at com.android.camera.app.CameraAppUI.onSurfaceTextureUpdated(CameraAppUI.java:2227)
10-27 21:46:12.657 19945 21726 E AndroidRuntime:  at com.android.camera.TextureViewHelper.onSurfaceTextureUpdated(TextureViewHelper.java:531)
10-27 21:46:12.657 19945 21726 E AndroidRuntime:  at android.view.TextureView.applyUpdate(TextureView.java:476)
10-27 21:46:12.657 19945 21726 E AndroidRuntime:  at android.view.TextureView.getBitmap(TextureView.java:611)
10-27 21:46:12.657 19945 21726 E AndroidRuntime:  at android.view.TextureView.getBitmap(TextureView.java:580)
10-27 21:46:12.657 19945 21726 E AndroidRuntime:  at com.android.camera.TextureViewHelper.getPreviewBitmap(TextureViewHelper.java:422)
10-27 21:46:12.657 19945 21726 E AndroidRuntime:  at com.android.camera.app.CameraAppUI$2.getScreenShot(CameraAppUI.java:652)
10-27 21:46:12.657 19945 21726 E AndroidRuntime:  at com.android.camera.app.CameraAppUI.freezeScreen(CameraAppUI.java:1089)
10-27 21:46:12.657 19945 21726 E AndroidRuntime:  at com.android.camera.app.CameraAppUI.freezeScreenUntilPreviewReady(CameraAppUI.java:1026)
10-27 21:46:12.657 19945 21726 E AndroidRuntime:  at com.android.camera.CameraActivity.freezeScreenUntilPreviewReady(CameraActivity.java:3538)
10-27 21:46:12.657 19945 21726 E AndroidRuntime:  at com.android.camera.CameraActivity.freezeScreenCommon(CameraActivity.java:3527)
10-27 21:46:12.657 19945 21726 E AndroidRuntime:  at com.android.camera.CameraActivity.access$8400(CameraActivity.java:193)
10-27 21:46:12.657 19945 21726 E AndroidRuntime:  at com.android.camera.CameraActivity$51.run(CameraActivity.java:4189)
10-27 21:46:12.657 19945 21726 E AndroidRuntime:  at android.os.Handler.handleCallback(Handler.java:938)
10-27 21:46:12.657 19945 21726 E AndroidRuntime:  at android.os.Handler.dispatchMessage(Handler.java:99)
10-27 21:46:12.657 19945 21726 E AndroidRuntime:  at android.os.Looper.loopOnce(Looper.java:201)
10-27 21:46:12.657 19945 21726 E AndroidRuntime:  at android.os.Looper.loop(Looper.java:288)
10-27 21:46:12.657 19945 21726 E AndroidRuntime:  at android.os.HandlerThread.run(HandlerThread.java:67)
10-27 21:46:12.680  1002 21977 I DropBoxManagerService: add tag=system_app_crash isTagEnabled=true flags=0x2
10-27 21:46:12.690  1002 21978 E starklog2: update count  1 = 9 errorType = system_app_crash
```## Monkey NPE

```text
10-27 21:50:14.852 19948 19948 D AndroidRuntime: Shutting down VM
10-27 21:50:14.852 19948 19948 E AndroidRuntime: FATAL EXCEPTION: main
10-27 21:50:14.852 19948 19948 E AndroidRuntime: Process: com.hmdglobal.app.cameralite, PID: 19948
10-27 21:50:14.852 19948 19948 E AndroidRuntime: java.lang.NullPointerException: Attempt to invoke virtual method 'java.lang.Object android.view.View.getTag(int)' on a null object reference
10-27 21:50:14.852 19948 19948 E AndroidRuntime:  at com.dream.camera.ButtonManagerDream.isEnabled(ButtonManagerDream.java:790)
10-27 21:50:14.852 19948 19948 E AndroidRuntime:  at com.android.camera.PhotoModule.updateParametersFlashMode(PhotoModule.java:6556)
10-27 21:50:14.852 19948 19948 E AndroidRuntime:  at com.android.camera.PhotoModule.updateSettingsBeforeStartPreview(PhotoModule.java:5423)
10-27 21:50:14.852 19948 19948 E AndroidRuntime:  at com.android.camera.PhotoModule.updateSettingAfterOpencamera(PhotoModule.java:5408)
10-27 21:50:14.852 19948 19948 E AndroidRuntime:  at com.android.camera.PhotoModule.startPreview(PhotoModule.java:5564)
10-27 21:50:14.852 19948 19948 E AndroidRuntime:  at com.android.camera.PhotoModule.onCameraAvailable(PhotoModule.java:3472)
10-27 21:50:14.852 19948 19948 E AndroidRuntime:  at com.android.camera.CameraActivity$6.run(CameraActivity.java:582)
10-27 21:50:14.852 19948 19948 E AndroidRuntime:  at android.os.Handler.handleCallback(Handler.java:938)
10-27 21:50:14.852 19948 19948 E AndroidRuntime:  at android.os.Handler.dispatchMessage(Handler.java:99)
10-27 21:50:14.852 19948 19948 E AndroidRuntime:  at android.os.Looper.loopOnce(Looper.java:201)
10-27 21:50:14.852 19948 19948 E AndroidRuntime:  at android.os.Looper.loop(Looper.java:288)
10-27 21:50:14.852 19948 19948 E AndroidRuntime:  at android.app.ActivityThread.main(ActivityThread.java:7941)
10-27 21:50:14.852 19948 19948 E AndroidRuntime:  at java.lang.reflect.Method.invoke(Native Method)
10-27 21:50:14.852 19948 19948 E AndroidRuntime:  at com.android.internal.os.RuntimeInit$MethodAndArgsCaller.run(RuntimeInit.java:553)
10-27 21:50:14.852 19948 19948 E AndroidRuntime:  at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:1003)
10-27 21:50:14.879  1002 22783 I DropBoxManagerService: add tag=system_app_crash isTagEnabled=true flags=0x2
10-27 21:50:14.891  1002 22784 E starklog2: update count  1 = 12 errorType = system_app_crash
```## 设置美颜等级

```text
protected static final int[] MAKE_UP_DEFAULT_VALUE = new int[]{0,0,0,0,0,0,0,0,0};
mCameraSettings.setSkinWhitenLevel(value);
public void setSkinWhitenLevel(int[] level) {
    if (level == null) {
        return;
    }
    mBeatuyLevel = level;
}

11-01 09:52:41.762 23535 29399 E zq8888  : Time:2022_11_01_09_01_11-->com.android.ex.camera2.portability.SprdCameraSettings-->setSkinWhitenLevel()-->309 i:0 v:1
11-01 09:52:41.763 23535 29399 E zq8888  : Time:2022_11_01_09_01_11-->com.android.ex.camera2.portability.SprdCameraSettings-->setSkinWhitenLevel()-->309 i:1 v:8
11-01 09:52:41.763 23535 29399 E zq8888  : Time:2022_11_01_09_01_11-->com.android.ex.camera2.portability.SprdCameraSettings-->setSkinWhitenLevel()-->309 i:2 v:0
11-01 09:52:41.764 23535 29399 E zq8888  : Time:2022_11_01_09_01_11-->com.android.ex.camera2.portability.SprdCameraSettings-->setSkinWhitenLevel()-->309 i:3 v:0
11-01 09:52:41.764 23535 29399 E zq8888  : Time:2022_11_01_09_01_11-->com.android.ex.camera2.portability.SprdCameraSettings-->setSkinWhitenLevel()-->309 i:4 v:0
11-01 09:52:41.765 23535 29399 E zq8888  : Time:2022_11_01_09_01_11-->com.android.ex.camera2.portability.SprdCameraSettings-->setSkinWhitenLevel()-->309 i:5 v:0
11-01 09:52:41.766 23535 29399 E zq8888  : Time:2022_11_01_09_01_11-->com.android.ex.camera2.portability.SprdCameraSettings-->setSkinWhitenLevel()-->309 i:6 v:4
11-01 09:52:41.767 23535 29399 E zq8888  : Time:2022_11_01_09_01_11-->com.android.ex.camera2.portability.SprdCameraSettings-->setSkinWhitenLevel()-->309 i:7 v:8
11-01 09:52:41.767 23535 29399 E zq8888  : Time:2022_11_01_09_01_11-->com.android.ex.camera2.portability.SprdCameraSettings-->setSkinWhitenLevel()-->309 i:8 v:0


vendor/sprd/platform/packages/apps/DreamCamera2/portability/src/com/android/ex/camera2/portability/SprdAndroidCamera2Settings.java
public Camera2RequestSettingsSet getRequestSettings() {
    ...
    requestSettings.set(CONTROL_SKIN_WHITEN_MODE, mBeatuyLevel);
    ...
}

public static final Key<int[]> CONTROL_SKIN_WHITEN_MODE = new Key<int[]>(
        "com.addParameters.perfectskinlevel", int[].class);

323:        com.addParameters.perfectskinlevel (80000006): int32[9]
324-          [1 7 0 0 ]
557:        com.addParameters.perfectskinlevel (80000006): int32[9]
558-          [1 7 0 0 ]
```## 人像模式设置为16:9之后进入到人像模式切换前后摄卡死

```text
11-01 16:33:40.086   708 17994 E Camera3-OutputStream: configureConsumerQueueLocked: Unable to connect to native window for stream 4
11-01 16:33:40.086   708 17994 E Camera3-Stream: finishConfiguration: Unable to configure stream 4 queue: Invalid argument (-22)
11-01 16:33:40.086   708 17994 E Camera3-Device: Camera 0: configureStreamsLocked: Can't finish configuring output stream 4: Invalid argument (-22)
11-01 16:33:40.086   708 17994 E CameraDeviceClient: endConfigure: Camera 0: Unsupported set of inputs/outputs provided
11-01 16:33:40.087  4798 10269 W CameraDevice-JV-0: Stream configuration failed due to: endConfigure:554: Camera 0: Unsupported set of inputs/outputs provided
11-01 16:33:40.087  4798 10269 E CameraCaptureSession: Session 1: Failed to create capture session; configuration failed

原因是因为在 acquireSurfaceTexture 的 onSurfaceTextureAvailable() 方法中调用了 mCameraDevice.setPreviewTexture(surfaceTexture); 会去重新配流
```## 如何一进入人像模式就改变分辨率为 4:3

```text
DataModuleManager.getInstance(mActivity).getDataModuleCamera().changeSettings(Keys.KEY_PICTURE_SIZE_BACK, "3264x2448");

修改方法：
http://192.168.3.81:8085/c/SPRD_S/SPRDROID12_TRUNK_22B_W22.09.2/+/1965
```## 李尚的手机刷软件进入人像模式报错

```text
@Override
public Size getCustomPictureSize() {
    Size pictureSize;
    if (isCameraFrontFacing()) {
        pictureSize = new Size(2592, 1944);
    } else {
        pictureSize = new Size(3264, 2448);
    }
    return pictureSize;
}
因为加了上面这段代码，在进入人像模式的时候固定了分辨率，后摄固定为了 3264x2448，但他的那台手机是老手机，只有 5M+5M(2592x1944)，所以会报配流报错

这段代码需要优化一下
List<Size> supportedPictureSizes = CameraPictureSizesCacher.getSizesForCamera(isFront ? 1 : 0, mAppController.getAndroidContext());
supportedPictureSizes = ResolutionUtil.getDisplayableSizesFromSupported(supportedPictureSizes, !isFront);
supportedPictureSizes = ResolutionUtil.filterBlackListedSizes(supportedPictureSizes, GservicesHelper.getBlacklistedResolutionsBack(null));
Size chosenPictureSize = ResolutionUtil.getLargestPictureSize(aspectRatio, supportedPictureSizes);
```## 人像模式AE locked的时候报错

```text
11-03 13:43:35.161  9231  9231 D CAM_BMDream: disableButton: 20     // 这里的 20 是 BUTTON_FLASH_DREAM
11-03 13:43:35.162  9231  9231 D AndroidRuntime: Shutting down VM
11-03 13:43:35.163   526  9301 D cmr_prev: 15748, prev_pop_preview_buffer: cam_id=0, fd=0x55, chn_id=0x1, valid_num=2, index=45, timestamp=0xdf3b988f1c
11-03 13:43:35.164   526  9301 D cmr_prev: 12068, channel2_dequeue_buffer: cam_id=0, fd=0x5d, chn_id=0x2, valid_num=2, frame_index=45
--------- beginning of crash
11-03 13:43:35.165  9231  9231 E AndroidRuntime: FATAL EXCEPTION: main
11-03 13:43:35.165  9231  9231 E AndroidRuntime: Process: com.hmdglobal.app.cameralite, PID: 9231
11-03 13:43:35.165  9231  9231 E AndroidRuntime: java.lang.NullPointerException: Attempt to invoke virtual method 'boolean android.view.View.isEnabled()' on a null object reference
11-03 13:43:35.165  9231  9231 E AndroidRuntime:  at com.dream.camera.ButtonManagerDream.disableButton(ButtonManagerDream.java:593)
11-03 13:43:35.165  9231  9231 E AndroidRuntime:  at com.android.camera.PhotoModule.updateFlashTopButtonEnable(PhotoModule.java:1503)
11-03 13:43:35.165  9231  9231 E AndroidRuntime:  at com.android.camera.PhotoModule.onDreamSettingChangeListener(PhotoModule.java:1433)
11-03 13:43:35.165  9231  9231 E AndroidRuntime:  at com.dream.camera.settings.DataModuleBasic.notifyKeyChange(DataModuleBasic.java:624)
11-03 13:43:35.165  9231  9231 E AndroidRuntime:  at com.dream.camera.settings.DataModuleBasic.changeAndNotify(DataModuleBasic.java:517)
11-03 13:43:35.165  9231  9231 E AndroidRuntime:  at com.dream.camera.settings.DataModuleBasic.changeSettings(DataModuleBasic.java:536)
11-03 13:43:35.165  9231  9231 E AndroidRuntime:  at com.android.camera.PhotoModule.setAELock(PhotoModule.java:4787)
11-03 13:43:35.165  9231  9231 E AndroidRuntime:  at com.android.camera.FocusOverlayManager.onAutoFocus(FocusOverlayManager.java:470)
11-03 13:43:35.165  9231  9231 E AndroidRuntime:  at com.android.camera.PhotoModule$AutoFocusCallback.onAutoFocus(PhotoModule.java:3108)      // 最初原因
11-03 13:43:35.165  9231  9231 E AndroidRuntime:  at com.android.ex.camera2.portability.AndroidCamera2AgentImpl$AndroidCamera2ProxyImpl$1$1$1.run(AndroidCamera2AgentImpl.java:1872)
11-03 13:43:35.165  9231  9231 E AndroidRuntime:  at android.os.Handler.handleCallback(Handler.java:938)
11-03 13:43:35.165  9231  9231 E AndroidRuntime:  at android.os.Handler.dispatchMessage(Handler.java:99)
11-03 13:43:35.165  9231  9231 E AndroidRuntime:  at android.os.Looper.loopOnce(Looper.java:201)
11-03 13:43:35.165  9231  9231 E AndroidRuntime:  at android.os.Looper.loop(Looper.java:288)
11-03 13:43:35.165  9231  9231 E AndroidRuntime:  at android.app.ActivityThread.main(ActivityThread.java:7941)
11-03 13:43:35.165  9231  9231 E AndroidRuntime:  at java.lang.reflect.Method.invoke(Native Method)
11-03 13:43:35.165  9231  9231 E AndroidRuntime:  at com.android.internal.os.RuntimeInit$MethodAndArgsCaller.run(RuntimeInit.java:553)
11-03 13:43:35.165  9231  9231 E AndroidRuntime:  at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:1003)

vendor/sprd/platform/packages/apps/DreamCamera2/src/com/dream/camera/ButtonManagerDream.java
public static final int BUTTON_FLASH_DREAM = 20;

vendor/sprd/platform/packages/apps/DreamCamera2/res/values/top_panel_config.xml
<array name="portrait_photo_top_panel">
    <item>@array/light_portrait_display_config</item>
    <item>@array/camera_settings_config</item>
    <item>@array/countdown_config</item>
    <!--Redmine84182 ODM modified to remove portrait flashlight support ZQ:begin-->
    <!--
    <item>@array/flash_photo_front_led_config</item>                            //人像模式中去掉了 flash 菜单
    -->
    <!--Redmine84182 ODM modified to remove portrait flashlight support ZQ:end-->
</array>

原因是手动锁AE的时候回去 PhotoModule 中调用 setAELock，然后就会触发 ButtonManagerDream.disableButton

解决方案：
在 ButtonManagerDream 所有调用 getButtonOrError 的后面都加上非空判断
```## NVA-2108 连接蓝牙自拍杆后，在相机界面，后摄拍照一张--切换后摄录像--切换前摄录像--切换前摄拍照，此时出现报错

```text
M268916  11-03 11:08:32.316 20804 31232 E CAM_CameraActivity Drea: Error connecting to camera
M268916  11-03 11:08:32.316 20804 31232 E CAM_CameraActivity Drea: android.view.ViewRootImpl$CalledFromWrongThreadException: Only the original thread that created a view hierarchy can touch its views.
M268916  11-03 11:08:32.316 20804 31232 E CAM_CameraActivity Drea:  at android.view.ViewRootImpl.checkThread(ViewRootImpl.java:9426)
M268916  11-03 11:08:32.316 20804 31232 E CAM_CameraActivity Drea:  at android.view.ViewRootImpl.requestLayout(ViewRootImpl.java:1806)
M268916  11-03 11:08:32.316 20804 31232 E CAM_CameraActivity Drea:  at android.view.View.requestLayout(View.java:25880)
M268916  11-03 11:08:32.316 20804 31232 E CAM_CameraActivity Drea:  at android.view.View.requestLayout(View.java:25880)
M268916  11-03 11:08:32.316 20804 31232 E CAM_CameraActivity Drea:  at android.view.View.requestLayout(View.java:25880)
M268916  11-03 11:08:32.316 20804 31232 E CAM_CameraActivity Drea:  at android.view.View.requestLayout(View.java:25880)
M268916  11-03 11:08:32.316 20804 31232 E CAM_CameraActivity Drea:  at android.view.View.requestLayout(View.java:25880)
M268916  11-03 11:08:32.316 20804 31232 E CAM_CameraActivity Drea:  at android.view.View.setFlags(View.java:16486)
M268916  11-03 11:08:32.316 20804 31232 E CAM_CameraActivity Drea:  at android.view.View.setVisibility(View.java:11913)
M268916  11-03 11:08:32.316 20804 31232 E CAM_CameraActivity Drea:  at android.widget.ImageView.setVisibility(ImageView.java:1691)
M268916  11-03 11:08:32.316 20804 31232 E CAM_CameraActivity Drea:  at com.android.camera.CameraActivity.setBtnZoomVisibility(CameraActivity.java:5700)
M268916  11-03 11:08:32.316 20804 31232 E CAM_CameraActivity Drea:  at com.dream.camera.MakeupController.initBtnBeauty(MakeupController.java:374)
M268916  11-03 11:08:32.316 20804 31232 E CAM_CameraActivity Drea:  at com.dream.camera.MakeupController.access$600(MakeupController.java:34)
M268916  11-03 11:08:32.316 20804 31232 E CAM_CameraActivity Drea:  at com.dream.camera.MakeupController$4.onDreamSettingChangeListener(MakeupController.java:477)
M268916  11-03 11:08:32.316 20804 31232 E CAM_CameraActivity Drea:  at com.dream.camera.settings.DataModuleBasic.notifyKeyChange(DataModuleBasic.java:624)
M268916  11-03 11:08:32.316 20804 31232 E CAM_CameraActivity Drea:  at com.dream.camera.settings.DataModulePhoto.initializeStaticParams(DataModulePhoto.java:947)
M268916  11-03 11:08:32.316 20804 31232 E CAM_CameraActivity Drea:  at com.android.camera.CameraActivity.dealCameraOpened(CameraActivity.java:567)
M268916  11-03 11:08:32.316 20804 31232 E CAM_CameraActivity Drea:  at com.android.camera.CameraActivity.onCameraOpened(CameraActivity.java:544)
M268916  11-03 11:08:32.316 20804 31232 E CAM_CameraActivity Drea:  at com.android.camera.app.CameraController.onCameraOpened(CameraController.java:191)
M268916  11-03 11:08:32.316 20804 31232 E CAM_CameraActivity Drea:  at com.android.ex.camera2.portability.CameraAgent$CameraOpenCallbackForward$1.run(CameraAgent.java:209)
M268916  11-03 11:08:32.316 20804 31232 E CAM_CameraActivity Drea:  at android.os.Handler.handleCallback(Handler.java:938)
M268916  11-03 11:08:32.316 20804 31232 E CAM_CameraActivity Drea:  at android.os.Handler.dispatchMessage(Handler.java:99)
M268916  11-03 11:08:32.316 20804 31232 E CAM_CameraActivity Drea:  at android.os.Looper.loopOnce(Looper.java:201)
M268916  11-03 11:08:32.316 20804 31232 E CAM_CameraActivity Drea:  at android.os.Looper.loop(Looper.java:288)
M268916  11-03 11:08:32.316 20804 31232 E CAM_CameraActivity Drea:  at android.os.HandlerThread.run(HandlerThread.java:67)
M268917  11-03 11:08:32.317 30051 30102 I btsnoop_sprd: 03:08:32:317570 EVE
M268918  11-03 11:08:32.317 30051 30102 I btsnoop_sprd: diff: 158
M268919  11-03 11:08:32.319 20804 20804 E CAM_FatalErrorHandler: Handling Camera Open Failure:
M268919  11-03 11:08:32.319 20804 20804 E CAM_FatalErrorHandler: java.lang.Exception
M268919  11-03 11:08:32.319 20804 20804 E CAM_FatalErrorHandler:  at com.android.camera.FatalErrorHandlerImpl.onCameraOpenFailure(FatalErrorHandlerImpl.java:49)
M268919  11-03 11:08:32.319 20804 20804 E CAM_FatalErrorHandler:  at com.android.camera.CameraActivity$7.run(CameraActivity.java:593)
M268919  11-03 11:08:32.319 20804 20804 E CAM_FatalErrorHandler:  at android.os.Handler.handleCallback(Handler.java:938)
M268919  11-03 11:08:32.319 20804 20804 E CAM_FatalErrorHandler:  at android.os.Handler.dispatchMessage(Handler.java:99)
M268919  11-03 11:08:32.319 20804 20804 E CAM_FatalErrorHandler:  at android.os.Looper.loopOnce(Looper.java:201)
M268919  11-03 11:08:32.319 20804 20804 E CAM_FatalErrorHandler:  at android.os.Looper.loop(Looper.java:288)
M268919  11-03 11:08:32.319 20804 20804 E CAM_FatalErrorHandler:  at android.app.ActivityThread.main(ActivityThread.java:7941)
M268919  11-03 11:08:32.319 20804 20804 E CAM_FatalErrorHandler:  at java.lang.reflect.Method.invoke(Native Method)
M268919  11-03 11:08:32.319 20804 20804 E CAM_FatalErrorHandler:  at com.android.internal.os.RuntimeInit$MethodAndArgsCaller.run(RuntimeInit.java:553)
M268919  11-03 11:08:32.319 20804 20804 E CAM_FatalErrorHandler:  at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:1003)
M26891A  11-03 11:08:32.320 20804 20804 E CAM_CameraUtil: Show fatal error dialog

从上面的log可以看到调用更新UI的线程ID是 31232

public void setBtnZoomVisibility(int visibility) {
    //NVA-2018 modified for Run-On-UI-Thread issue ZQ 2022/11/03:begin
    runOnUiThread(new Runnable() {
        @Override
        public void run() {
            if (mCameraAppUI != null && mCameraAppUI.getBtnZoom() != null) {
                mCameraAppUI.getBtnZoom().setVisibility(visibility);
                if (!(mCurrentModeIndex == SettingsScopeNamespaces.AUTO_PHOTO || mCurrentModeIndex == SettingsScopeNamespaces.PORTRAIT_PHOTO)) {
                    mCameraAppUI.getBtnZoom().setVisibility(View.GONE);
                }
                //NVA-588 modify zoom reset Icon by huanglj 20221102 begin
                if(DreamUtil.getRightCamera(getCameraId()) == DreamUtil.FRONT_CAMERA){
                    mCameraAppUI.getBtnZoom().setVisibility(View.GONE);
                }
                //NVA-588 modify zoom reset Icon flashIcon by huanglj 20221102 end
            }
        }
    });
    //NVA-2018 modified for Run-On-UI-Thread issue ZQ 2022/11/03:end
}
```## 如何在屏幕上显示当前时间？

## 人像夜景模式拍照的流配置成YUV的流？

## 人像模式HDR怎么去掉？

## 能否将人像模式的TextureView改成SurfaceView?

## 人像模式没有检测到人脸的时候拍照不进算法？

```text
已修改
```## 人像模式预览能否跳帧？没有检测到人脸的时候也不进算法？

## 能否用预览的数据做缩略图，待拍照完成之后再更新真实的缩略图

```text
已修改
```## 人像模式有时候会生成 thumb.jpg 的图片，是不是 process 还没处理完被打断了?

```text
多线程导致的
```## 优化一下 Portrait 的启动时间

```text
貌似改了夜景模式的destroy流程之后就ok了
```## 人像模式打开镜像功能出现异常？

```text
CAM2PORT_SprdAndCam2Agn  E  Unable to get Image.getPlanes()
                         E  java.lang.NullPointerException: Attempt to invoke virtual method 'android.media.Image$Plane[] android.media.Image.getPlanes()' on a null object reference
                         E      at com.android.ex.camera2.portability.SprdAndroidCamera2AgentImpl.getNV21FromImage(SprdAndroidCamera2AgentImpl.java:1780)
                         E      at com.android.ex.camera2.portability.SprdAndroidCamera2AgentImpl.access$1400(SprdAndroidCamera2AgentImpl.java:46)
                         E      at com.android.ex.camera2.portability.SprdAndroidCamera2AgentImpl$CameraPreViewCallbackForward.onImageAvailable(SprdAndroidCamera2AgentImpl.java:1693)
                         E      at android.media.ImageReader$1.run(ImageReader.java:837)
                         E      at android.os.Handler.handleCallback(Handler.java:938)
                         E      at android.os.Handler.dispatchMessage(Handler.java:99)
                         E      at android.os.Looper.loopOnce(Looper.java:201)
                         E      at android.os.Looper.loop(Looper.java:288)
                         E      at android.os.HandlerThread.run(HandlerThread.java:67)


CAM2PORT_AndCam2AgntImp  I  config mMediaRecoderSurface=null mPreviewCallback=null mNeedThumb=true
             IMGGralloc  D  Gralloc Free  w:960, h:720, f:0x22, usage:0x20000106, ui64Stamp:45088 line = 2499
                         D  Gralloc Free  w:960, h:720, f:0x22, usage:0x20000106, ui64Stamp:45103 line = 2499
                         D  Gralloc Free  w:960, h:720, f:0x22, usage:0x20000106, ui64Stamp:45109 line = 2499
                         D  Gralloc Free  w:960, h:720, f:0x22, usage:0x20000106, ui64Stamp:45113 line = 2499
    BufferQueueProducer  E  [SurfaceTexture-0-2949-0](id:b8500000002,api:1,p:2949,c:2949) connect: already connected (cur=1 req=4)
      CameraDevice-JV-1  W  Stream configuration failed due to: endConfigure:554: Camera 1: Unsupported set of inputs/outputs provided
   CameraCaptureSession  E  Session 2: Failed to create capture session; configuration failed
CAM2PORT_DispatchThread  I  DispatchThread.this.notifyAll()!
CAM2PORT_AndCam2AgntImp  I  AppFW handleMessage - action = 'SET_SENSOR_SELF_SHOT_LISTENER'
CAM2PORT_DispatchThread  I  DispatchThread.this.wait end!
                         I  Runnable job.run() end!
                         I  DispatchThread.this.wait will!
CAM2PORT_AndCam2AgntImp  I  AppFW handleMessage - action = 'SET_FACE_DETECTION_LISTENER'
                         I  AppFW handleMessage - action = 'START_FACE_DETECTION'
                         E  Failed to configure the camera for capture
CAM2PORT_SprdAndCam2Agn  E  surfaceview callback can not be invoked when privew is not active


11-11 13:43:36.890   720   720 V Camera3-Device: Camera 1: Creating new stream 8: 960 x 720, format 34, dataspace 0 rotation 0 consumer usage 0, isShared 0, physicalCameraId , isMultiResolution 0
11-11 13:43:36.890   720   720 V Camera3-Device: Camera 1: Created new stream
11-11 13:43:36.890   720   720 V CameraDeviceClient: createStream: mStreamMap add binder 0xf1acb4f0 streamId 8, surfaceId 0
11-11 13:43:36.890   720   720 V CameraDeviceClient: createStream: Camera 1: Successfully created a new stream ID 8 for output surface (960 x 720) with format 0x22.
11-11 13:43:36.890   720   720 V CameraDeviceClient: getRotationTransformLocked: begin
11-11 13:43:36.893   720   720 V Camera3-Device: Camera 1: Creating new stream 9: 2592 x 1944, format 33, dataspace 146931712 rotation 0 consumer usage 0, isShared 0, physicalCameraId , isMultiResolution 0
11-11 13:43:36.893   720   720 V Camera3-Device: Camera 1: Created new stream
11-11 13:43:36.893   720   720 V CameraDeviceClient: createStream: mStreamMap add binder 0xf1acb5e0 streamId 9, surfaceId 0
11-11 13:43:36.894   720   720 V CameraDeviceClient: createStream: Camera 1: Successfully created a new stream ID 9 for output surface (2592 x 1944) with format 0x21.
11-11 13:43:36.894   720   720 V CameraDeviceClient: getRotationTransformLocked: begin
11-11 13:43:36.896   720   720 V Camera3-Device: Camera 1: Creating new stream 10: 320 x 240, format 35, dataspace 146931712 rotation 0 consumer usage 0, isShared 0, physicalCameraId , isMultiResolution 0
11-11 13:43:36.896   720   720 V Camera3-Device: Camera 1: Created new stream
11-11 13:43:36.896   720   720 V CameraDeviceClient: createStream: mStreamMap add binder 0xf1acb770 streamId 10, surfaceId 0
11-11 13:43:36.896   720   720 V CameraDeviceClient: createStream: Camera 1: Successfully created a new stream ID 10 for output surface (320 x 240) with format 0x23.
11-11 13:43:36.896   720   720 V CameraDeviceClient: getRotationTransformLocked: begin
11-11 13:43:36.897   720   720 V CameraDeviceClient: endConfigure: ending configure (0 input stream, 3 output surfaces)
11-11 13:43:36.897   720   720 V Camera3-Device: configureStreams: E
11-11 13:43:36.897   720   720 V Camera3-Device: configureStreamsLocked: Camera 1: Starting stream configuration

11-11 13:43:36.913  3540  3584 E BufferQueueProducer: [SurfaceTexture-0-3540-0](id:dd400000002,api:1,p:3540,c:3540) connect: already connected (cur=1 req=4)
11-11 13:43:36.914   720   720 E Camera3-OutputStream: configureConsumerQueueLocked: Unable to connect to native window for stream 8
11-11 13:43:36.914   720   720 E Camera3-Stream: finishConfiguration: Unable to configure stream 8 queue: Invalid argument (-22)
11-11 13:43:36.914   720   720 E Camera3-Device: Camera 1: configureStreamsLocked: Can't finish configuring output stream 8: Invalid argument (-22)
11-11 13:43:36.914   720   720 E CameraDeviceClient: endConfigure: Camera 1: Unsupported set of inputs/outputs provided
11-11 13:43:36.915  3540  3584 W CameraDevice-JV-1: Stream configuration failed due to: endConfigure:554: Camera 1: Unsupported set of inputs/outputs provided
11-11 13:43:36.916  3540  3584 E CameraCaptureSession: Session 2: Failed to create capture session; configuration failed

修改方法：
http://192.168.3.81:8085/c/SPRD_S/SPRDROID12_TRUNK_22B_W22.09.2/+/2709
case Keys.KEY_FRONT_CAMERA_MIRROR:
    //NVA-587 modified for Portrait camera mirror issue ZQ 2022/11/11:begin
    //restartPreview(false);
    //NVA-587 modified for Portrait camera mirror issue ZQ 2022/11/11:end
    return;
```## 双击Power键快速启动相机的时候会闪现两次cover

```text
一次是SecureCamera的背景
<style name="Theme.SecureCamera" parent="@style/Theme.Camera">
    <item name="android:windowBackground">@drawable/cover</item>
</style>

还有一次是 mode_transition_view_top 的背景
CameraAppUI.java
```## 人像模式拍照概率性没有效果，而且拍照生成的图片很小只有320x240

```text
第一次进入人像模式拍照的时候没有设置

11-07 10:56:31.766 16967 17180 I CAM_Storage: For_Test public function writeFile path = /storage/emulated/0/DCIM/Camera/IMG_20221107_105631.jpg
11-07 10:56:36.589 16967 17245 I CAM_Storage: For_Test public function writeFile path = /storage/emulated/0/DCIM/Camera/IMG_20221107_105631.jpg
11-07 10:56:38.040 16967 17251 I CAM_Storage: For_Test public function writeFile path = /storage/emulated/0/DCIM/Camera/IMG_20221107_105637.jpg
11-07 10:56:42.154 16967 17253 I CAM_Storage: For_Test public function writeFile path = /storage/emulated/0/DCIM/Camera/IMG_20221107_105637.jpg
11-07 10:56:44.318 16967 17259 I CAM_Storage: For_Test public function writeFile path = /storage/emulated/0/DCIM/Camera/IMG_20221107_105643.jpg
11-07 10:56:48.358 16967 17261 I CAM_Storage: For_Test public function writeFile path = /storage/emulated/0/DCIM/Camera/IMG_20221107_105643.jpg
11-07 10:57:03.689 16967 17395 I CAM_Storage: For_Test public function writeFile path = /storage/emulated/0/DCIM/Camera/IMG_20221107_105702.jpg

出问题的时候只有一次 writeFile

不正常的log没有走下面这两段
11-07 16:39:39.246 27880 28097 E zq8888  : java.lang.Throwable
11-07 16:39:39.246 27880 28097 E zq8888  :  at com.android.camera.MediaSaverImpl.updateImage(MediaSaverImpl.java:277)
11-07 16:39:39.246 27880 28097 E zq8888  :  at com.android.camera.PhotoModule.updateImage(PhotoModule.java:7852)
11-07 16:39:39.246 27880 28097 E zq8888  :  at com.android.camera.PhotoModule$JpegPictureCallback.saveFinalPhoto(PhotoModule.java:2995)
11-07 16:39:39.246 27880 28097 E zq8888  :  at com.android.camera.PhotoModule$JpegPictureCallback$1.doInBackground(PhotoModule.java:2687)
11-07 16:39:39.246 27880 28097 E zq8888  :  at com.android.camera.PhotoModule$JpegPictureCallback$1.doInBackground(PhotoModule.java:2680)
11-07 16:39:39.246 27880 28097 E zq8888  :  at android.os.AsyncTask$3.call(AsyncTask.java:394)
11-07 16:39:39.246 27880 28097 E zq8888  :  at java.util.concurrent.FutureTask.run(FutureTask.java:266)
11-07 16:39:39.246 27880 28097 E zq8888  :  at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1167)
11-07 16:39:39.246 27880 28097 E zq8888  :  at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:641)
11-07 16:39:39.246 27880 28097 E zq8888  :  at java.lang.Thread.run(Thread.java:920)
11-07 16:39:39.376 27880 28101 E zq8888  : java.lang.Throwable
11-07 16:39:39.376 27880 28101 E zq8888  :  at com.android.camera.Storage.writeFile(Storage.java:805)
11-07 16:39:39.376 27880 28101 E zq8888  :  at com.android.camera.Storage.writeFileAdapter(Storage.java:239)
11-07 16:39:39.376 27880 28101 E zq8888  :  at com.android.camera.Storage.updateImage(Storage.java:687)
11-07 16:39:39.376 27880 28101 E zq8888  :  at com.android.camera.MediaSaverImpl$ImageUpdateTask.doInBackground(MediaSaverImpl.java:787)
11-07 16:39:39.376 27880 28101 E zq8888  :  at com.android.camera.MediaSaverImpl$ImageUpdateTask.doInBackground(MediaSaverImpl.java:735)
11-07 16:39:39.376 27880 28101 E zq8888  :  at android.os.AsyncTask$3.call(AsyncTask.java:394)
11-07 16:39:39.376 27880 28101 E zq8888  :  at java.util.concurrent.FutureTask.run(FutureTask.java:266)
11-07 16:39:39.376 27880 28101 E zq8888  :  at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1167)
11-07 16:39:39.376 27880 28101 E zq8888  :  at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:641)
11-07 16:39:39.376 27880 28101 E zq8888  :  at java.lang.Thread.run(Thread.java:920)


11-08 13:09:11.489 24924 25268 E zq8888  : Time:2022_11_08_11_05_09-->com.android.camera.PhotoModule$JpegPictureCallback$2-->run()-->3014
11-08 13:09:15.988 24924 24924 E zq8888  : Time:2022_11_08_11_05_32-->com.android.camera.PhotoModule$MainHandler-->handleMessage()-->924
11-08 13:09:15.988 24924 24924 E zq8888  : Time:2022_11_08_11_00_24-->com.android.camera.PhotoModule$MainHandler-->handleMessage()-->927
11-08 13:09:15.989 24924 24924 E zq8888  : Time:2022_11_08_13_07_45-->com.android.camera.PhotoModule-->updateImage()-->7901 uri:content://media/external/images/media/46
11-08 13:09:15.989 24924 24924 E zq8888  : Time:2022_11_08_13_02_08-->com.android.camera.PhotoModule-->updateImage()-->7907

11-08 13:09:36.469 25451 25770 E zq8888  : Time:2022_11_08_11_05_09-->com.android.camera.PhotoModule$JpegPictureCallback$2-->run()-->3014
11-08 13:09:40.644 25451 25451 E zq8888  : Time:2022_11_08_11_05_32-->com.android.camera.PhotoModule$MainHandler-->handleMessage()-->924
11-08 13:09:40.645 25451 25451 E zq8888  : Time:2022_11_08_11_00_24-->com.android.camera.PhotoModule$MainHandler-->handleMessage()-->927
11-08 13:09:40.646 25451 25451 E zq8888  : Time:2022_11_08_13_07_45-->com.android.camera.PhotoModule-->updateImage()-->7901 uri:null        // 没有虚化的时候 uri 为空？
11-08 13:09:40.647 25451 25451 E zq8888  : Time:2022_11_08_13_02_12-->com.android.camera.PhotoModule-->updateImage()-->7911
11-08 13:09:40.648 25451 25451 E zq8888  : Time:2022_11_08_13_05_24-->com.android.camera.PhotoModule-->updateImage()-->7913


人像模式 updateUri 会经常为 null ??
11-08 14:27:10.619  8076  8076 I CAM_PhotoModule: updateUri = null
11-08 14:27:10.881  8076  8076 I CAM_PhotoModule: onMediaSaved uri = content://media/external/images/media/100 , title = updateUri
11-08 14:27:12.623  8076  8076 I CAM_PhotoModule: updateUri = null
11-08 14:27:12.915  8076  8076 I CAM_PhotoModule: onMediaSaved uri = content://media/external/images/media/101 , title = updateUri
11-08 14:27:14.500  8076  8076 I CAM_PhotoModule: updateUri = content://media/external/images/media/102
11-08 14:27:14.732  8076  8076 I CAM_PhotoModule: onMediaSaved uri = content://media/external/images/media/102 , title = updateUri
11-08 14:27:15.926  8076  8076 I CAM_PhotoModule: updateUri = null
11-08 14:27:16.192  8076  8076 I CAM_PhotoModule: onMediaSaved uri = content://media/external/images/media/103 , title = updateUri
11-08 14:27:18.153  8076  8076 I CAM_PhotoModule: updateUri = null
11-08 14:27:18.404  8076  8076 I CAM_PhotoModule: onMediaSaved uri = content://media/external/images/media/104 , title = updateUri
11-08 14:27:19.740  8076  8076 I CAM_PhotoModule: updateUri = null
11-08 14:27:19.949  8076  8076 I CAM_PhotoModule: onMediaSaved uri = content://media/external/images/media/105 , title = updateUri
11-08 14:27:32.577  8076  8076 I CAM_PhotoModule: updateUri = content://media/external/images/media/106
11-08 14:27:32.848  8076  8076 I CAM_PhotoModule: onMediaSaved uri = content://media/external/images/media/106 , title = updateUri
11-08 14:27:39.945  8076  8076 I CAM_PhotoModule: updateUri = null
11-08 14:27:40.226  8076  8076 I CAM_PhotoModule: onMediaSaved uri = content://media/external/images/media/107 , title = updateUri

Photo默认就是 ok 的
11-08 14:29:07.485  8076  8076 I CAM_PhotoModule: updateUri = content://media/external/images/media/108
11-08 14:29:07.824  8076  8076 I CAM_PhotoModule: onMediaSaved uri = content://media/external/images/media/108 , title = updateUri
11-08 14:29:09.553  8076  8076 I CAM_PhotoModule: updateUri = content://media/external/images/media/109
11-08 14:29:09.747  8076  8076 I CAM_PhotoModule: onMediaSaved uri = content://media/external/images/media/109 , title = updateUri
11-08 14:29:11.300  8076  8076 I CAM_PhotoModule: updateUri = content://media/external/images/media/110
11-08 14:29:11.513  8076  8076 I CAM_PhotoModule: onMediaSaved uri = content://media/external/images/media/110 , title = updateUri
11-08 14:29:12.971  8076  8076 I CAM_PhotoModule: updateUri = content://media/external/images/media/111
11-08 14:29:13.218  8076  8076 I CAM_PhotoModule: onMediaSaved uri = content://media/external/images/media/111 , title = updateUri
11-08 14:29:14.732  8076  8076 I CAM_PhotoModule: updateUri = content://media/external/images/media/112
11-08 14:29:14.958  8076  8076 I CAM_PhotoModule: onMediaSaved uri = content://media/external/images/media/112 , title = updateUri
11-08 14:29:16.480  8076  8076 I CAM_PhotoModule: updateUri = content://media/external/images/media/113
11-08 14:29:16.699  8076  8076 I CAM_PhotoModule: onMediaSaved uri = content://media/external/images/media/113 , title = updateUri
11-08 14:29:18.587  8076  8076 I CAM_PhotoModule: updateUri = content://media/external/images/media/114
11-08 14:29:18.803  8076  8076 I CAM_PhotoModule: onMediaSaved uri = content://media/external/images/media/114 , title = updateUri
11-08 14:29:20.370  8076  8076 I CAM_PhotoModule: updateUri = content://media/external/images/media/115
11-08 14:29:20.580  8076  8076 I CAM_PhotoModule: onMediaSaved uri = content://media/external/images/media/115 , title = updateUri

Uri updateUri = mActivity != null ? mActivity
        .getThumbUri(title) : null;
Log.i(TAG, "updateUri = " + updateUri);                     // 为什么人像模式下这里经常为 null 呢？
//NVA-1255 modified to add Portrait ZQ 2022/10/26:begin
updateImage(updateUri, jpegData, title, date, mLocation,
        width, height, orientation, exif,
        mOnMediaSavedListener, FilmstripItemData.MIME_TYPE_JPEG);

解决方法：
在优化人像模式拍照流程之后就OK了
http://192.168.3.81:8085/c/SPRD_S/SPRDROID12_TRUNK_22B_W22.09.2/+/3378
```## 前后摄切换 log : switchFrontAndBackMode

```text
./M00414D  01-03 01:27:32.448  3862  3862 D CAM_PhotoModule: bbbb new Start to switch camera. cameraId=0
./M0071B2  01-03 01:27:49.594  3862  3862 D CAM_PhotoModule: bbbb new Start to switch camera. cameraId=1
./M008AC8  01-03 01:28:01.035  3862  3862 D CAM_PhotoModule: bbbb new Start to switch camera. cameraId=0
./M00A2F6  01-03 01:28:17.107  3862  3862 D CAM_PhotoModule: bbbb new Start to switch camera. cameraId=1
./M00DD33  01-03 01:28:34.965  3862  3862 D CAM_PhotoModule: bbbb new Start to switch camera. cameraId=0
./M00FC0F  01-03 01:28:48.558  3862  3862 D CAM_PhotoModule: bbbb new Start to switch camera. cameraId=1
./M0122DB  01-03 01:28:57.869  3862  3862 D CAM_PhotoModule: bbbb new Start to switch camera. cameraId=0
./M013E3B  01-03 01:29:12.540  3862  3862 D CAM_PhotoModule: bbbb new Start to switch camera. cameraId=1
```## Monkey

```text
01-03 16:51:31.165 32460 32460 E AndroidRuntime: Caused by: java.lang.NullPointerException: Attempt to invoke virtual method 'void android.widget.ProgressBar.setVisibility(int)' on a null object reference
01-03 16:51:31.165 32460 32460 E AndroidRuntime:  at com.android.camera.app.CameraAppUI.stopProgressAnimation(CameraAppUI.java:4847)
01-03 16:51:31.165 32460 32460 E AndroidRuntime:  at com.android.camera.PhotoUI.stopSaveProgress(PhotoUI.java:2759)
01-03 16:51:31.165 32460 32460 E AndroidRuntime:  at com.android.camera.PhotoModule.closeCamera(PhotoModule.java:5152)
01-03 16:51:31.165 32460 32460 E AndroidRuntime:  at com.android.camera.PhotoModule.pause(PhotoModule.java:4367)
01-03 16:51:31.165 32460 32460 E AndroidRuntime:  at com.dream.camera.modules.autophoto.AutoPhotoModule.pause(AutoPhotoModule.java:752)
01-03 16:51:31.165 32460 32460 E AndroidRuntime:  at com.android.camera.CameraActivity.onPauseTasks(CameraActivity.java:2427)
01-03 16:51:31.165 32460 32460 E AndroidRuntime:  at com.android.camera.util.QuickActivity.onPause(QuickActivity.java:175)
01-03 16:51:31.165 32460 32460 E AndroidRuntime:  at android.app.Activity.performPause(Activity.java:8252)
01-03 16:51:31.165 32460 32460 E AndroidRuntime:  at android.app.Instrumentation.callActivityOnPause(Instrumentation.java:1530)
01-03 16:51:31.165 32460 32460 E AndroidRuntime:  at android.app.ActivityThread.performPauseActivityIfNeeded(ActivityThread.java:5099)
01-03 16:51:31.165 32460 32460 E AndroidRuntime:  ... 15 more

01-03 03:07:49.230 23637 23637 E AndroidRuntime: FATAL EXCEPTION: main
01-03 03:07:49.230 23637 23637 E AndroidRuntime: Process: com.hmdglobal.app.cameralite, PID: 23637
01-03 03:07:49.230 23637 23637 E AndroidRuntime: java.lang.NullPointerException: Attempt to invoke virtual method 'void com.android.camera.FocusOverlayManager.onTouch(android.view.MotionEvent)' on a null object reference
01-03 03:07:49.230 23637 23637 E AndroidRuntime:  at com.android.camera.PhotoModule.onTouch(PhotoModule.java:9423)
01-03 03:07:49.230 23637 23637 E AndroidRuntime:  at com.android.camera.PhotoUI$2.onTouch(PhotoUI.java:203)
01-03 03:07:49.230 23637 23637 E AndroidRuntime:  at com.android.camera.ui.PreviewOverlay.onTouchEvent(PreviewOverlay.java:271)
01-03 03:07:49.230 23637 23637 E AndroidRuntime:  at android.view.View.dispatchTouchEvent(View.java:14571)
01-03 03:07:49.230 23637 23637 E AndroidRuntime:  at android.view.ViewGroup.dispatchTransformedTouchEvent(ViewGroup.java:3175)
01-03 03:07:49.230 23637 23637 E AndroidRuntime:  at android.view.ViewGroup.dispatchTouchEvent(ViewGroup.java:2770)
01-03 03:07:49.230 23637 23637 E AndroidRuntime:  at android.view.ViewGroup.dispatchTransformedTouchEvent(ViewGroup.java:3175)
01-03 03:07:49.230 23637 23637 E AndroidRuntime:  at android.view.ViewGroup.dispatchTouchEvent(ViewGroup.java:2770)
01-03 03:07:49.230 23637 23637 E AndroidRuntime:  at android.view.ViewGroup.dispatchTransformedTouchEvent(ViewGroup.java:3175)
01-03 03:07:49.230 23637 23637 E AndroidRuntime:  at android.view.ViewGroup.dispatchTouchEvent(ViewGroup.java:2770)
01-03 03:07:49.230 23637 23637 E AndroidRuntime:  at android.view.ViewGroup.dispatchTransformedTouchEvent(ViewGroup.java:3175)
01-03 03:07:49.230 23637 23637 E AndroidRuntime:  at android.view.ViewGroup.dispatchTouchEvent(ViewGroup.java:2770)
01-03 03:07:49.230 23637 23637 E AndroidRuntime:  at android.view.ViewGroup.dispatchTransformedTouchEvent(ViewGroup.java:3175)
01-03 03:07:49.230 23637 23637 E AndroidRuntime:  at android.view.ViewGroup.dispatchTouchEvent(ViewGroup.java:2770)
01-03 03:07:49.230 23637 23637 E AndroidRuntime:  at com.android.internal.policy.DecorView.superDispatchTouchEvent(DecorView.java:502)
01-03 03:07:49.230 23637 23637 E AndroidRuntime:  at com.android.internal.policy.PhoneWindow.superDispatchTouchEvent(PhoneWindow.java:1890)
01-03 03:07:49.230 23637 23637 E AndroidRuntime:  at android.app.Activity.dispatchTouchEvent(Activity.java:4207)
01-03 03:07:49.230 23637 23637 E AndroidRuntime:  at com.android.camera.CameraActivity.dispatchTouchEvent(CameraActivity.java:2322)
01-03 03:07:49.230 23637 23637 E AndroidRuntime:  at com.android.internal.policy.DecorView.dispatchTouchEvent(DecorView.java:460)
01-03 03:07:49.230 23637 23637 E AndroidRuntime:  at android.view.View.dispatchPointerEvent(View.java:14838)
01-03 03:07:49.230 23637 23637 E AndroidRuntime:  at android.view.ViewRootImpl$ViewPostImeInputStage.processPointerEvent(ViewRootImpl.java:6430)
01-03 03:07:49.230 23637 23637 E AndroidRuntime:  at android.view.ViewRootImpl$ViewPostImeInputStage.onProcess(ViewRootImpl.java:6231)
01-03 03:07:49.230 23637 23637 E AndroidRuntime:  at android.view.ViewRootImpl$InputStage.deliver(ViewRootImpl.java:5704)
01-03 03:07:49.230 23637 23637 E AndroidRuntime:  at android.view.ViewRootImpl$InputStage.onDeliverToNext(ViewRootImpl.java:5762)
01-03 03:07:49.230 23637 23637 E AndroidRuntime:  at android.view.ViewRootImpl$InputStage.forward(ViewRootImpl.java:5728)
01-03 03:07:49.230 23637 23637 E AndroidRuntime:  at android.view.ViewRootImpl$AsyncInputStage.forward(ViewRootImpl.java:5893)
01-03 03:07:49.230 23637 23637 E AndroidRuntime:  at android.view.ViewRootImpl$InputStage.apply(ViewRootImpl.java:5736)
01-03 03:07:49.230 23637 23637 E AndroidRuntime:  at android.view.ViewRootImpl$AsyncInputStage.apply(ViewRootImpl.java:5950)
01-03 03:07:49.230 23637 23637 E AndroidRuntime:  at android.view.ViewRootImpl$InputStage.deliver(ViewRootImpl.java:5709)
01-03 03:07:49.230 23637 23637 E AndroidRuntime:  at android.view.ViewRootImpl$InputStage.onDeliverToNext(ViewRootImpl.java:5762)
01-03 03:07:49.230 23637 23637 E AndroidRuntime:  at android.view.ViewRootImpl$InputStage.forward(ViewRootImpl.java:5728)
01-03 03:07:49.230 23637 23637 E AndroidRuntime:  at android.view.ViewRootImpl$InputStage.apply(ViewRootImpl.java:5736)
01-03 03:07:49.230 23637 23637 E AndroidRuntime:  at android.view.ViewRootImpl$InputStage.deliver(ViewRootImpl.java:5709)
01-03 03:07:49.230 23637 23637 E AndroidRuntime:  at android.view.ViewRootImpl.deliverInputEvent(ViewRootImpl.java:8661)
01-03 03:07:49.230 23637 23637 E AndroidRuntime:  at android.view.ViewRootImpl.doProcessInputEvents(ViewRootImpl.java:8612)
01-03 03:07:49.230 23637 23637 E AndroidRuntime:  at android.view.ViewRootImpl.enqueueInputEvent(ViewRootImpl.java:8578)
01-03 03:07:49.230 23637 23637 E AndroidRuntime:  at android.view.ViewRootImpl$WindowInputEventReceiver.onInputEvent(ViewRootImpl.java:8792)
01-03 03:07:49.230 23637 23637 E AndroidRuntime:  at android.view.InputEventReceiver.dispatchInputEvent(InputEventReceiver.java:259)
01-03 03:07:49.230 23637 23637 E AndroidRuntime:  at android.os.MessageQueue.nativePollOnce(Native Method)
01-03 03:07:49.230 23637 23637 E AndroidRuntime:  at android.os.MessageQueue.next(MessageQueue.java:335)
01-03 03:07:49.230 23637 23637 E AndroidRuntime:  at android.os.Looper.loopOnce(Looper.java:161)
01-03 03:07:49.230 23637 23637 E AndroidRuntime:  at android.os.Looper.loop(Looper.java:288)
01-03 03:07:49.230 23637 23637 E AndroidRuntime:  at android.app.ActivityThread.main(ActivityThread.java:7941)
01-03 03:07:49.230 23637 23637 E AndroidRuntime:  at java.lang.reflect.Method.invoke(Native Method)
01-03 03:07:49.230 23637 23637 E AndroidRuntime:  at com.android.internal.os.RuntimeInit$MethodAndArgsCaller.run(RuntimeInit.java:553)
01-03 03:07:49.230 23637 23637 E AndroidRuntime:  at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:1003)
```## NVA-2181 人像模式闪退

```text
C0AAFD1  01-03 00:22:02.873 11515 11545 E AndroidRuntime: FATAL EXCEPTION: Camera2 Handler Thread
C0AAFD1  01-03 00:22:02.873 11515 11545 E AndroidRuntime: Process: com.hmdglobal.app.cameralite, PID: 11515
C0AAFD1  01-03 00:22:02.873 11515 11545 E AndroidRuntime: java.lang.OutOfMemoryError: Failed to allocate a 1036816 byte allocation with 507048 free bytes and 495KB until OOM, target footprint 268435456, growth limit 268435456
C0AAFD1  01-03 00:22:02.873 11515 11545 E AndroidRuntime:  at com.android.ex.camera2.portability.SprdAndroidCamera2AgentImpl.getNV21FromImage(SprdAndroidCamera2AgentImpl.java:1782)
C0AAFD1  01-03 00:22:02.873 11515 11545 E AndroidRuntime:  at com.android.ex.camera2.portability.SprdAndroidCamera2AgentImpl.access$1400(SprdAndroidCamera2AgentImpl.java:46)
C0AAFD1  01-03 00:22:02.873 11515 11545 E AndroidRuntime:  at com.android.ex.camera2.portability.SprdAndroidCamera2AgentImpl$CameraPreViewCallbackForward.onImageAvailable(SprdAndroidCamera2AgentImpl.java:1693)
C0AAFD1  01-03 00:22:02.873 11515 11545 E AndroidRuntime:  at android.media.ImageReader$1.run(ImageReader.java:837)
C0AAFD1  01-03 00:22:02.873 11515 11545 E AndroidRuntime:  at android.os.Handler.handleCallback(Handler.java:938)
C0AAFD1  01-03 00:22:02.873 11515 11545 E AndroidRuntime:  at android.os.Handler.dispatchMessage(Handler.java:99)
C0AAFD1  01-03 00:22:02.873 11515 11545 E AndroidRuntime:  at android.os.Looper.loopOnce(Looper.java:201)
C0AAFD1  01-03 00:22:02.873 11515 11545 E AndroidRuntime:  at android.os.Looper.loop(Looper.java:288)
C0AAFD1  01-03 00:22:02.873 11515 11545 E AndroidRuntime:  at android.os.HandlerThread.run(HandlerThread.java:67)
C0B1A28  01-03 00:22:36.992   293   293 F libc    : crash_dump helper failed to exec, or was killed

11-08 14:59:05.848  3874  3891 I AndroidRuntime: VM exiting with result code 0, cleanup skipped.
11-08 19:45:21.773 27776 27808 E AndroidRuntime: FATAL EXCEPTION: Camera2 Handler Thread
11-08 19:45:21.773 27776 27808 E AndroidRuntime: Process: com.hmdglobal.app.cameralite, PID: 27776
11-08 19:45:21.773 27776 27808 E AndroidRuntime: java.lang.OutOfMemoryError: Failed to allocate a 1036816 byte allocation with 269000 free bytes and 262KB until OOM, target footprint 268435456, growth limit 268435456
11-08 19:45:21.773 27776 27808 E AndroidRuntime:  at com.android.ex.camera2.portability.SprdAndroidCamera2AgentImpl.getNV21FromImage(SprdAndroidCamera2AgentImpl.java:1784)
11-08 19:45:21.773 27776 27808 E AndroidRuntime:  at com.android.ex.camera2.portability.SprdAndroidCamera2AgentImpl.access$1400(SprdAndroidCamera2AgentImpl.java:46)
11-08 19:45:21.773 27776 27808 E AndroidRuntime:  at com.android.ex.camera2.portability.SprdAndroidCamera2AgentImpl$CameraPreViewCallbackForward.onImageAvailable(SprdAndroidCamera2AgentImpl.java:1695)
11-08 19:45:21.773 27776 27808 E AndroidRuntime:  at android.media.ImageReader$1.run(ImageReader.java:837)
11-08 19:45:21.773 27776 27808 E AndroidRuntime:  at android.os.Handler.handleCallback(Handler.java:938)
11-08 19:45:21.773 27776 27808 E AndroidRuntime:  at android.os.Handler.dispatchMessage(Handler.java:99)
11-08 19:45:21.773 27776 27808 E AndroidRuntime:  at android.os.Looper.loopOnce(Looper.java:201)
11-08 19:45:21.773 27776 27808 E AndroidRuntime:  at android.os.Looper.loop(Looper.java:288)
11-08 19:45:21.773 27776 27808 E AndroidRuntime:  at android.os.HandlerThread.run(HandlerThread.java:67)
11-08 19:49:22.982 28926 28926 D AndroidRuntime: >>>>>> START com.android.internal.os.RuntimeInit uid 1067 <<<<<<

从 log 中看是内存溢出的问题

private static byte[] getNV21FromImage(Image img) {
    long t1 = System.currentTimeMillis();
    ByteBuffer[] planeBuf = new ByteBuffer[NUM_PLANES];
    Plane[] planeList = img.getPlanes();
    for (int i = 0; i < NUM_PLANES; i++) {
        planeBuf[i] = planeList[i].getBuffer();
    }

    ByteBuffer buf = planeBuf[0];
    if (yLength != buf.remaining() || imageBytes == null || imageBytes.length == 0) {
        yLength = buf.remaining();
        imageBytes = new byte[yLength * 3 / 2];
    }
    buf.get(imageBytes, 0, yLength);
    buf.clear();

    buf = planeBuf[1];
    int uLength = buf.remaining();
    buf.get(imageBytes, yLength + 1, uLength);
    buf.clear();

    buf = planeBuf[2];
    buf.get(imageBytes, yLength, 1);
    buf.clear();
    Log.i(TAG, "getNV21FromImage cost " + (System.currentTimeMillis() - t1));
    return imageBytes;      // 是不是 imageBytes 这一块的内存一直被算法占用着没有释放
}

@Override
public void onImageAvailable(ImageReader reader) {
    try (Image image = reader.acquireNextImage()) {
        onPreviewFrame(getNV21FromImage(image), mCamera);
    }catch (NullPointerException ex){
        Log.e(TAG, "Unable to get Image.getPlanes()", ex);
    }
}

mCameraDevice.setPreviewDataCallback(mHandler, new CameraAgent.CameraPreviewDataCallback() {
    @Override
    public void onPreviewFrame(final byte[] data, CameraProxy camera) {
        if (mPortraitDrawer != null) {
            com.android.ex.camera2.portability.Size mPreviewSize = mCameraSettings.getCurrentPreviewSize();
            mPortraitDrawer.addYuvFrame(data, com.aiworks.android.filter.GLUTJni.FORMAT_NV12, mPreviewSize.width(), mPreviewSize.height(), 0, 0);
            // 但是把这里的删掉还是没用？
        }
    }
});

11-10 15:36:09.388 20793 20803 I .app.cameralit: WaitForGcToComplete blocked Background on Alloc for 60.650ms

前摄没检测到人脸也会OOM，后摄不会

完蛋，重新刷机后就好了？懵B了，不知道哪里出了问题？？？？？？？？？

portability/src/com/android/ex/camera2/portability/SprdAndroidCamera2AgentImpl.java
private static byte[] getNV21FromImage(Image img) {
    long t1 = System.currentTimeMillis();
    final int NUM_PLANES = 3;
    final Plane[] planeList = img.getPlanes();
    ByteBuffer[] planeBuf = new ByteBuffer[NUM_PLANES];

    for (int i = 0; i < NUM_PLANES; i++) {
        Plane plane = planeList[i];
        planeBuf[i] = plane.getBuffer();
    }

    ByteBuffer buf = planeBuf[0];
    int yLength = buf.remaining();
    byte[] imageBytes = new byte[yLength * 3 / 2];
    buf.get(imageBytes, 0, yLength);
    buf.clear();

    buf = planeBuf[1];
    int uLength = buf.remaining();
    buf.get(imageBytes, yLength + 1, uLength);
    buf.clear();

    buf = planeBuf[2];
    buf.get(imageBytes, yLength, 1);
    buf.clear();
    Log.i(TAG, "getNV21FromImage cost " + (System.currentTimeMillis() - t1));
    return imageBytes;
}

改成

private static final int NUM_PLANES = 3;
private static ByteBuffer[] planeBuf = new ByteBuffer[NUM_PLANES];
private static Plane[] planeList;
private static ByteBuffer buf;
private static byte[] imageBytes;
private static int yLength;

private static byte[] getNV21FromImage(Image img) {
    long t1 = System.currentTimeMillis();
    planeList = img.getPlanes();
    for (int i = 0; i < NUM_PLANES; i++) {
        planeBuf[i] = planeList[i].getBuffer();
    }

    buf = planeBuf[0];
    if (yLength != buf.remaining() || imageBytes == null || imageBytes.length == 0) {
        yLength = buf.remaining();
        imageBytes = new byte[yLength * 3 / 2];
    }
    buf.get(imageBytes, 0, yLength);
    buf.clear();

    buf = planeBuf[1];
    int uLength = buf.remaining();
    buf.get(imageBytes, yLength + 1, uLength);
    buf.clear();

    buf = planeBuf[2];
    buf.get(imageBytes, yLength, 1);
    buf.clear();
    Log.i(TAG, "getNV21FromImage cost " + (System.currentTimeMillis() - t1));
    return imageBytes;
}
```## 切换模式的时候卡死

```text
  CAM_CameraAppUI Dream  D   onSwipeDetected swipeState=3
                         E  can not switch camera when FreezeScreen
           ViewRootImpl  D  ViewRootImpl performMeasure , childWidthMeasureSpec = 1073742544, childHeightMeasureSpec = 1073743384, mTag=ViewRootImpl[CameraActivity] ,this = android.view.UnisocViewRootImpl@f1f9cba
                         D  ViewRootImpl performLayout , Laying out DecorView@6488f61[CameraActivity] to (720, 1560), mTag=ViewRootImpl[CameraActivity] ,this = android.view.UnisocViewRootImpl@f1f9cba
                         D  ViewRootImpl performDraw , usingAsyncReport :false mTag=ViewRootImpl[CameraActivity] ,this = android.view.UnisocViewRootImpl@f1f9cba
  CAM_CameraAppUI Dream  D   onSwipeDetected swipeState=4
                         E  can not switch camera when FreezeScreen
           ViewRootImpl  D  ViewRootImpl performMeasure , childWidthMeasureSpec = 1073742544, childHeightMeasureSpec = 1073743384, mTag=ViewRootImpl[CameraActivity] ,this = android.view.UnisocViewRootImpl@f1f9cba
                         D  ViewRootImpl performLayout , Laying out DecorView@6488f61[CameraActivity] to (720, 1560), mTag=ViewRootImpl[CameraActivity] ,this = android.view.UnisocViewRootImpl@f1f9cba
                         D  ViewRootImpl performDraw , usingAsyncReport :false mTag=ViewRootImpl[CameraActivity] ,this = android.view.UnisocViewRootImpl@f1f9cba
  CAM_CameraAppUI Dream  D   onSwipeDetected swipeState=3
                         E  can not switch camera when FreezeScreen


public boolean unResponseClick() {
    ...
    if (getFreezeScreenFlag()) {
        Log.e(TAG, "can not switch camera when FreezeScreen");
        return true;
    }
    ...
}

public boolean getFreezeScreenFlag() {
    if (mModeCoverState != COVER_HIDDEN) {
        return true;
    } else {
        return false;
    }
}

public void hideModeCover() {
    if (mCurrentHideRunnable != null) {
        mAppRootView.post(mCurrentHideRunnable);
        mCurrentHideRunnable = null;
        mModeCoverState = COVER_HIDDEN;     // 只有这一个地方设置为 COVER_HIDDEN
        if (mCoverHiddenTime < 0) {
            mCoverHiddenTime = System.currentTimeMillis();
        }
        if (CameraUtil.isSwitchAnimationEnable()) {
            mAppRootView.postDelayed(new Runnable() {
                public void run() {
                    hideSwitchPreview();
                }
            }, 0);
        }
    }
}

11-09 14:42:36.954 29306 29351 E zq8888  : java.lang.Throwable
11-09 14:42:36.954 29306 29351 E zq8888  :  at com.android.camera.app.CameraAppUI.hideModeCover(CameraAppUI.java:1453)
11-09 14:42:36.954 29306 29351 E zq8888  :  at com.android.camera.PhotoModule$32.onSurfaceUpdate(PhotoModule.java:5737)
11-09 14:42:36.954 29306 29351 E zq8888  :  at com.android.ex.camera2.portability.SprdAndroidCamera2AgentImpl.monitorSurfaceViewPreviewUpdate(SprdAndroidCamera2AgentImpl.java:549)
11-09 14:42:36.954 29306 29351 E zq8888  :  at com.android.ex.camera2.portability.SprdAndroidCamera2AgentImpl$SprdCamera2Handler.onMonitorControlStates(SprdAndroidCamera2AgentImpl.java:1300)
11-09 14:42:36.954 29306 29351 E zq8888  :  at com.android.ex.camera2.portability.AndroidCamera2AgentImpl$Camera2Handler$5.monitorControlStates(AndroidCamera2AgentImpl.java:1645)
11-09 14:42:36.954 29306 29351 E zq8888  :  at com.android.ex.camera2.portability.AndroidCamera2AgentImpl$Camera2Handler$5.onCaptureCompleted(AndroidCamera2AgentImpl.java:1587)
11-09 14:42:36.954 29306 29351 E zq8888  :  at android.hardware.camera2.impl.CameraCaptureSessionImpl$1.lambda$onCaptureCompleted$3$CameraCaptureSessionImpl$1(CameraCaptureSessionImpl.java:693)
11-09 14:42:36.954 29306 29351 E zq8888  :  at android.hardware.camera2.impl.CameraCaptureSessionImpl$1$$ExternalSyntheticLambda6.run(Unknown Source:8)
11-09 14:42:36.954 29306 29351 E zq8888  :  at android.os.Handler.handleCallback(Handler.java:938)
11-09 14:42:36.954 29306 29351 E zq8888  :  at android.os.Handler.dispatchMessage(Handler.java:99)
11-09 14:42:36.954 29306 29351 E zq8888  :  at android.os.Looper.loopOnce(Looper.java:201)
11-09 14:42:36.954 29306 29351 E zq8888  :  at android.os.Looper.loop(Looper.java:288)
11-09 14:42:36.954 29306 29351 E zq8888  :  at android.os.HandlerThread.run(HandlerThread.java:67)
11-09 14:42:36.976 29306 29306 E zq8888  : java.lang.Throwable
11-09 14:42:36.976 29306 29306 E zq8888  :  at com.android.camera.app.CameraAppUI.hideModeCover(CameraAppUI.java:1453)
11-09 14:42:36.976 29306 29306 E zq8888  :  at com.dream.camera.modules.filter.DreamFilterModuleController.checkFrameCount(DreamFilterModuleController.java:127)
11-09 14:42:36.976 29306 29306 E zq8888  :  at com.android.camera.app.CameraAppUI.onSurfaceTextureUpdated(CameraAppUI.java:2254)
11-09 14:42:36.976 29306 29306 E zq8888  :  at com.android.camera.PhotoModule$30.run(PhotoModule.java:5707)
11-09 14:42:36.976 29306 29306 E zq8888  :  at android.os.Handler.handleCallback(Handler.java:938)
11-09 14:42:36.976 29306 29306 E zq8888  :  at android.os.Handler.dispatchMessage(Handler.java:99)
11-09 14:42:36.976 29306 29306 E zq8888  :  at android.os.Looper.loopOnce(Looper.java:201)
11-09 14:42:36.976 29306 29306 E zq8888  :  at android.os.Looper.loop(Looper.java:288)
11-09 14:42:36.976 29306 29306 E zq8888  :  at android.app.ActivityThread.main(ActivityThread.java:7941)
11-09 14:42:36.976 29306 29306 E zq8888  :  at java.lang.reflect.Method.invoke(Native Method)
11-09 14:42:36.976 29306 29306 E zq8888  :  at com.android.internal.os.RuntimeInit$MethodAndArgsCaller.run(RuntimeInit.java:553)
11-09 14:42:36.976 29306 29306 E zq8888  :  at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:1003)



去掉 getFreezeScreenFlag() 的判断之后又出现了这个问题
                         E  can not set when camera is switch mode
           ViewRootImpl  D  ViewRootImpl performMeasure , childWidthMeasureSpec = 1073742544, childHeightMeasureSpec = 1073743384, mTag=ViewRootImpl[CameraActivity] ,this = android.view.UnisocViewRootImpl@aadb4dc
                         D  ViewRootImpl performLayout , Laying out DecorView@412976b[CameraActivity] to (720, 1560), mTag=ViewRootImpl[CameraActivity] ,this = android.view.UnisocViewRootImpl@aadb4dc
                         D  ViewRootImpl performDraw , usingAsyncReport :false mTag=ViewRootImpl[CameraActivity] ,this = android.view.UnisocViewRootImpl@aadb4dc
  CAM_CameraAppUI Dream  D   onSwipeDetected swipeState=4
                         E  can not set when camera is switch mode


M0B5173  11-09 14:30:48.728 26600 26630 I CAM_CameraActivity Drea: freezeScreenCommon cost: 76
M0B517D  11-09 14:30:48.793 26600 26630 I CAM_CameraActivity Drea: waitModeSelect run
M0B524D  11-09 14:30:48.908 26600 26631 I CAM_PhotoModule: stopPreview end!
M0B524E  11-09 14:30:48.908 26600 26631 I CAM_CameraActivity Drea: stopPreview cost: 254

M0B55C4  11-09 14:30:57.172 26600 26600 D CAM_CameraAppUI Dream:  onSwipeDetected swipeState=4
M0B55C5  11-09 14:30:57.173 26600 26600 E CAM_CameraAppUI Dream: can not switch camera when FreezeScreen


正常的log在 stopPreview end 之后会有 init-resume 等操作
11-09 15:20:14.501  6066  6098 I CAM_PhotoModule: stopPreview end!
11-09 15:20:14.763  6066  6066 I CAM_PhotoModule:  init null,1
11-09 15:20:14.765  6066  6066 I CAM_PhotoModule: resume start!
11-09 15:20:14.766  6066  6066 I CAM_PhotoModule: requestCameraOpen mCameraId:1
11-09 15:20:14.867  6066  6066 I CAM_PhotoModule: onCameraAvailable
11-09 15:20:14.871  6066  6066 I CAM_PhotoModule: updatePreviewCapabilities
11-09 15:20:14.882  6066  6066 V CAM_PhotoModule: updateSettingsBeforeStartPreview begin
11-09 15:20:14.882  6066  6066 I CAM_PhotoModule: updating aspect ratio: optimalSize=960x720
11-09 15:20:14.888  6066  6066 I CAM_PhotoModule: updating setSurfaceViewSize optimalSize:960x720, mDesiredPreviewWidth=960, mDesiredPreviewHeight=720
11-09 15:20:14.891  6066  6066 D CAM_PhotoModule: optimalSize:=960x720 original:=1280x720 pictureSize:=2592x1944
11-09 15:20:14.891  6066  6066 I CAM_PhotoModule: setting preview size. optimal: 960x720original: 1280x720
11-09 15:20:14.891  6066  6066 D CAM_PhotoModule: Preview size is 960x720
11-09 15:20:14.894  6066  6066 E CAM_PhotoModule: front camera's flash type is lcd
11-09 15:20:14.894  6066  6066 D CAM_PhotoModule:  updateParametersFlashMode = AUTO
11-09 15:20:14.895  6066  6066 I CAM_PhotoModule: this module does not support flash,return
11-09 15:20:14.895  6066  6066 I CAM_PhotoModule: updateParameters3DNR set3DNREnable : 0
11-09 15:20:14.895  6066  6066 I CAM_PhotoModule: updateAuto3DnrPatameter isAuto3DnrSupported= true
11-09 15:20:14.895  6066  6066 I CAM_PhotoModule: updateParametersLogoWatermark setLogoWatermarkEnable : 0
11-09 15:20:14.895  6066  6066 I CAM_PhotoModule: updateParametersTimeWatermark setTimeWatermarkEnable : 0
11-09 15:20:14.896  6066  6066 D CAM_PhotoModule: stopGestureDetection 
11-09 15:20:14.897  6066  6066 I CAM_PhotoModule: send DeviceOrientation 0 to HAL
11-09 15:20:14.897  6066  6066 I CAM_PhotoModule: updateParametersAppModeId
11-09 15:20:14.898  6066  6066 D CAM_PhotoModule: updateMakeLevel false
11-09 15:20:14.898  6066  6066 V CAM_PhotoModule: updateSettingsBeforeStartPreview end
11-09 15:20:14.899  6066  6066 I CAM_PhotoModule: startPreview end!

前摄预览的时候比较容易出现卡死，有可能是内存溢出那个问题相同原因导致的？
```## Camera切换模式之后Camera卡顿

```text
 1023 system       18  -2 1.8G  21M  21M S 55.0   0.7  30:52.71 system_server
 2218 u0_a107      20   0 1.1G  90M  76M R 33.3   3.1   0:01.61 com.google.andr+
 2027 u0_a146      10 -10 1.4G  68M  52M S 27.6   2.3   0:08.35 com.hmdglobal.a+
  720 cameraserver 20   0  66M 5.9M 4.0M S 18.6   0.2  27:22.47 cameraserver

1.把人像模式去掉：还是有问题的
2.把夜景模式去掉:ok了
3.把夜景模式和人像模式都去掉：


adb shell cat /proc/531/status      查看 cameraserver 的内存占用发现已经使用了 2G+ 了，所以卡死

Name: provider@2.4-se
Umask: 0077
State: S (sleeping)
Tgid: 531
Ngid: 0
Pid: 531
PPid: 1
TracerPid: 0
Uid: 1047 1047 1047 1047
Gid: 1005 1005 1005 1005
FDSize: 512
Groups: 1004 1006 1026 
VmPeak:  2215976 kB
VmSize:  2196720 kB
VmLck:        0 kB
VmPin:        0 kB
VmHWM:   153320 kB
VmRSS:    83548 kB
RssAnon:    78064 kB
RssFile:     4212 kB
RssShmem:     1272 kB
VmData:   246852 kB
VmStk:      132 kB
VmExe:        8 kB
VmLib:    80104 kB
VmPTE:     4264 kB
VmSwap:    43852 kB
CoreDumping: 0
THP_enabled: 1
Threads: 56
SigQ: 0/11078
SigPnd: 0000000000000000
ShdPnd: 0000000000000000
SigBlk: 0000000080000000
SigIgn: 0000002000000000
SigCgt: 0000004c400084f8
CapInh: 0000000000800000
CapPrm: 0000000000800000
CapEff: 0000000000800000
CapBnd: 0000000000800000
CapAmb: 0000000000800000
NoNewPrivs: 0
Seccomp: 0
Seccomp_filters: 0
Speculation_Store_Bypass: unknown
Cpus_allowed: ff
Cpus_allowed_list: 0-7
Mems_allowed: 1
Mems_allowed_list: 0
voluntary_ctxt_switches: 433745
nonvoluntary_ctxt_switches: 158022


重启之后查看只有 145M
Name: provider@2.4-se
Umask: 0077
State: S (sleeping)
Tgid: 530
Ngid: 0
Pid: 530
PPid: 1
TracerPid: 0
Uid: 1047 1047 1047 1047
Gid: 1005 1005 1005 1005
FDSize: 256
Groups: 1004 1006 1026 
VmPeak:   145628 kB
VmSize:   145628 kB
VmLck:        0 kB
VmPin:        0 kB
VmHWM:    30472 kB
VmRSS:    30456 kB
RssAnon:     4868 kB
RssFile:    25336 kB
RssShmem:      252 kB
VmData:    51256 kB
VmStk:      132 kB
VmExe:        8 kB
VmLib:    79612 kB
VmPTE:      256 kB
VmSwap:        0 kB
CoreDumping: 0
THP_enabled: 1
Threads: 4
SigQ: 0/11078
SigPnd: 0000000000000000
ShdPnd: 0000000000000000
SigBlk: 0000000080000000
SigIgn: 0000002000000000
SigCgt: 0000004c400084f8
CapInh: 0000000000800000
CapPrm: 0000000000800000
CapEff: 0000000000800000
CapBnd: 0000000000800000
CapAmb: 0000000000800000
NoNewPrivs: 0
Seccomp: 0
Seccomp_filters: 0
Speculation_Store_Bypass: unknown
Cpus_allowed: ff
Cpus_allowed_list: 0-7
Mems_allowed: 1
Mems_allowed_list: 0
voluntary_ctxt_switches: 4148
nonvoluntary_ctxt_switches: 1585

adb shell ps | grep "camera"
cameraserver   530     1 1585248   3768 binder_thread_read  0 S android.hardware.camera.provider@2.4-service
cameraserver   710     1   52436   4996 binder_thread_read  0 S cameraserver

adb shell procrank | grep "camera"
  710    52432K    5340K     561K     428K    3648K    3648K    3648K    1201K  /system/bin/cameraserver
  530  1585244K    3820K     126K      32K    7664K    7664K    7664K    2524K  /vendor/bin/hw/android.hardware.camera.provider@2.4-service

为什么这一块会有这么多的内存占用？

adb shell dumpsys meminfo 看到 ION 这块占用比较多
Total RAM: 2,920,580K (status normal)
 Free RAM:   664,458K (   51,666K cached pss +   532,080K cached kernel +    80,712K free)
      ION: 1,497,012K (1,459,976K mapped +    37,036K unmapped +         0K pools)
      GPU:   116,344K (  116,344K dmabuf +         0K private)
 Used RAM: 2,372,062K (2,102,762K used pss +   269,300K kernel)
 Lost RAM:   102,172K
     ZRAM:   111,928K physical used for   338,432K in swap (2,190,428K total swap)
   Tuning: 128 (large 256), oom   184,320K, restore limit    30,720K (low-ram)


Total RAM: 2,920,580K (status normal)
 Free RAM: 1,258,420K (  281,736K cached pss +   943,516K cached kernel +    33,168K free)
      ION:   259,876K (   92,912K mapped +   130,316K unmapped +    36,648K pools)
      GPU:   202,060K (  202,060K dmabuf +         0K private)
 Used RAM: 1,588,889K (1,198,737K used pss +   390,152K kernel)
 Lost RAM:   171,613K
     ZRAM:    33,420K physical used for   136,448K in swap (2,190,428K total swap)
   Tuning: 128 (large 256), oom   184,320K, restore limit    30,720K (low-ram)

刚开机
Total RAM: 2,920,580K (status normal)
 Free RAM: 1,527,117K (  258,657K cached pss +   928,312K cached kernel +   340,148K free)
      ION:    83,212K (   15,112K mapped +    50,692K unmapped +    17,408K pools)
      GPU:   101,084K (  101,084K dmabuf +         0K private)
 Used RAM: 1,229,768K (  949,332K used pss +   280,436K kernel)
 Lost RAM:   163,691K
     ZRAM:         4K physical used for         0K in swap (2,190,428K total swap)
   Tuning: 128 (large 256), oom   184,320K, restore limit    30,720K (low-ram)




查看内存占用的命令
adb shell dumpsys meminfo > dumpsys_meminfo.txt

adb shell cat /sys/kernel/debug/ion/ion_mm_heap > ion_mm_heap.txt

adb shell cat /proc/mali/memory_usage > gpu_mali_memory_usage.txt

adb shell ps > ps.txt

adb shell cat /proc/vmallocinfo > vmallocinfo.txt

adb shell cat /proc/zoneinfo > zoneinfo.txt

adb shell cat /proc/meminfo > proc_meminfo.txt

adb shell dumpsys procstats > proc_stats.txt

adb shell procrank > proc_crank.txt(eng version only)



adb shell cat /sys/kernel/debug/pvr/ion/heaps/ion_system_heap

ION分析
https://blog.csdn.net/armwind/article/details/53454251

Sprd Camera ION分析
https://blog.csdn.net/zhoumin090508/article/details/119536095
使用4.14版本的内核，ion debug的接口相对于老版本4.9内核发生了变化。
4.9版本的内核的ion debug接口在 /sys/kernel/debug/ion/clients/ 和 /sys/kernel/debug/ion/heaps/ 两个目录下，4.14版本已经没有了这两个目录。
4.14版本增加了 /sys/kernel/debug/dma_buf/dmaprocs 节点来导出各进程的ion内存使用情况。

下面以camera为例来看看在4.14版本上如何查看ion内存使用信息。

首先获得要查询进程的PID，我们通过进程名称，在ps命令的输出中查找：

:/ # ps -A | grep camera                                                                                                                                                                          
cameraserver   708     1  749220  47176 binder_ioctl_write_read 0 S android.hardware.camera.provider@2.4-service_64
cameraserver   939     1   39152  18524 binder_ioctl_write_read 0 S cameraserver

输出显示进程android.hardware.camera.provider@2.4-service_64的PID号为708.

然后，在/sys/kernel/debug/dma_buf/dmaprocs节点中查找该PID进程所占用的内存情况：

:/ # cat /sys/kernel/debug/dma_buf/dmaprocs | grep 708
provider@2.4-se (PID 708) size: 205448

输出显示进程名为provider@2.4-se（这是截短的进程名），PID为708，总共使用ion的size为205448，单位为K。

在测试过程中，我们可以通过这种方法来监控该进程的ion内存占用变化情况，判断是否出现ion内存泄漏。



修改方案：
http://192.168.3.81:8085/c/SPRD_S/SPRDROID12_TRUNK_22B_W22.09.2/+/2831
```## NVA-2134 

```text
./M005878  11-09 13:26:13.096   287   287 I lowmemorykiller: Kill 'com.hmdglobal.app.cameralite' (15912), uid 10146, oom_score_adj 0 to free 42768kB rss, 111976kB swap; reason: low watermark is breached and thrashing (36%)

grep "freeAllCameraMem" ./ -r
./0-android.log:M005B59  11-09 13:26:13.981   481   828 I Cam3OEMIf: 3454, freeAllCameraMem: :hal3: E
./0-android.log:M005B60  11-09 13:26:13.982   481   828 E Cam3OEMIf: 3594, freeAllCameraMem: ION/GPU buffer memory leak!!!
./0-android.log:M005B61  11-09 13:26:13.982   481   828 I Cam3OEMIf: 3597, freeAllCameraMem: :hal3: X CamId=0 TotalIonSize=59944960 TotalGpuSize=0, total_size 1012592640

修改方案：
http://192.168.3.81:8085/c/SPRD_S/SPRDROID12_TRUNK_22B_W22.09.2/+/2831
```## DMA_BUF

```text
https://blog.csdn.net/fangwei1993/article/details/125499252

dma-buf 由浅入深（一） —— 最简单的 dma-buf 驱动程序
https://blog.csdn.net/hexiaolong2009/article/details/102596744
```## Memory Profiler

```text
字段解析:

Alloc Count：堆中的分配数量。

Native Size：此对象类型使用的本机内存总量（以字节为单位）。此列仅适用于Android 7.0及更高版本。
你会在这里看到一些在Java中分配的对象的内存，因为Android为一些框架类使用本地内存，比如Bitmap。

Shallow Size：此对象类型使用的Java内存总量（以字节为单位）。

Retained Size：由于此类的所有实例而保留的内存总大小（以字节为单位）。

在 Class 列表顶部，您可以使用左侧的下拉列表在下列堆转储之间切换：

Default heap：当系统没有指定堆时。

App heap：应用程序分配内存的主要堆。

Image heap：系统引导映像，包含在引导期间预加载的类。这里的分配保证不会移动或消失。

Zygote heap：Android系统中的应用程序进程分支的写入时复制堆。

堆中的对象列表按类名排列，默认情况下。您可以使用另一个下拉菜单在以下安排之间切换：

Arrange by class：根据类名称对所有分配进行分组。

Arrange by package：根据包名分组所有分配。

Arrange by callstack：将所有分配分组到相应的调用堆栈中。只有在录制分配时捕获堆转储时，此选项才有效。即使如此，在开始录制之前堆中可能会有一些对象，所以这些分配首先出现，只是按类名称列出。

检查堆，请按照下列步骤操作：

浏览列表以查找具有异常大堆计数并可能泄漏的对象。为帮助查找已知类，请单击“ Class Name” 列标题按字母顺序排序。然后点击一个类名。该 Instance View的查看窗格显示在右侧，显示出类的每个实例。

Instance View单击一个实例。“ References ” 选项卡显示在下方，显示对该对象的每个引用。

在“ References”选项卡中，如果您确定可能正在泄漏内存的引用，请右键单击它并选择“ Go to Instance”。这将从堆转储中选择相应的实例，向您显示其自己的实例数据。
```## 获取 SurfaceView 中数据的方法

```text
private Bitmap getSurfaceViewBitmap() {
    RectF previeaArea = mCameraAppUI.getPreviewArea();
    if (previeaArea == null) return null;
    int width  = (int)previeaArea.width();
    int height = (int)previeaArea.height();
    Bitmap screenShot = Bitmap.createBitmap(width,height, Bitmap.Config.ARGB_8888);
    try {
        PixelCopy.request(mCurrentModule.getSurfaceView(), screenShot, mSurfaceViewCopyListener, mCameraRequestHandler);
    } catch (IllegalArgumentException e) {
        e.printStackTrace();
    }
    return screenShot;
}
```## onPreviewStarted 耗时较长

```text
11-15 11:06:18.473  3943  3943 I CAM_PhotoUI: onPreviewStarted cost: 1162

原因是 PhotoUI 中 fitExtendPanel() 方法加载美颜控件的时间较长，目前正在尝试把美颜相关控件优化一下

修改之后
01-03 00:15:30.347 10347 10347 I CAM_PhotoUI: onPreviewStarted cost: 25

修改方法：
把原先的 MakeupController 替换成简单的 ArcSeekBar
http://192.168.3.81:8085/c/SPRD_S/SPRDROID12_TRUNK_22B_W22.09.2/+/3076
```## AsyncTask.THREAD_POOL_EXECUTOR 线程池的使用方法

```text
AsyncTask.THREAD_POOL_EXECUTOR.execute(new Runnable() {
    public void run() {
        long start = System.currentTimeMillis();
        RenderScript rs = RenderScript.create(getAndroidContext());
        if(rs != null) {
            ScriptIntrinsicBlur blurScript = ScriptIntrinsicBlur.create(rs, Element.U8_4(rs));
            blurScript.destroy();
            rs.destroy();
        }
        long cost = System.currentTimeMillis() - start;
        if (cost > 100) {
            Log.i(TAG, "ScriptIntrinsicBlur init and destory cost: " + cost);
        }
    }
});
```## stopPreview 耗时较长，能否优化 ？

```text
11-17 16:26:09.102 24881 24930 I CAM_CameraActivity Drea: stopPreview cost: 275

11-17 16:31:00.268 24881 24930 I CAM_PhotoModule: stopPreview start!mCameraDevice=com.android.ex.camera2.portability.SprdAndroidCamera2AgentImpl$SprdAndroidCamera2ProxyImpl@389046e
11-17 16:31:00.268 24881 24930 I CAM_PhotoModule: stopPreview
11-17 16:31:00.268 24881 24930 I CAM2PORT_CamAgnt: stopPreview getState = 16
11-17 16:31:00.317   537   928 I Cam3OEMIf: 4033, stopPreviewInternal: E mCameraId=1
11-17 16:31:00.381 24881 24881 I CAM_PhotoModule: stopPreview not need at switch mode
11-17 16:31:00.489   537 24983 D Cam3OEMIf: 7172, HandleStopPreview: state = SPRD_INTERNAL_PREVIEW_STOPPING
11-17 16:31:00.512   537   928 I Cam3OEMIf: 4125, stopPreviewInternal: X Time:194 ms camera id 1
11-17 16:31:00.555 24881 24930 I CAM_PhotoModule: stopPreview end!
11-17 16:31:00.555 24881 24930 I CAM_CameraActivity Drea: stopPreview cost: 287
```## 如何查看 yuv 和 raw 图？

```text
yuv图查看，展讯使用的是YuvViewer工具，raw 图使用的是IspTool工具。

需要找 CPM 释放。
```## 人像模式拍照概率性照片丢失

```text
M0104E1  11-09 12:11:14.734 28019 28019 I CAM_PhotoModule: saveFinalPhoto start!
M0104E2  11-09 12:11:14.735 28019 28019 I CAM_PhotoModule: saveFinalPhoto title=IMG_20221109_121114.jpg
M0104E3  11-09 12:11:14.735 28019 28019 I CAM_PhotoModule: saveFinalPhoto mIsImageCaptureIntent=false
M0104E6  11-09 12:11:14.737 28019 28019 I CAM_PhotoModule: saveFinalPhoto end! mCameraState=3 mContinuousCaptureCount=0
M0105FF  11-09 12:11:15.044 28019 28019 I CAM_PhotoModule: onPictureTaken mCameraState=3 mContinuousCaptureCount = 0 isBurstCapture()= false mIsContinousCaptureFinish =falsemHasCaptureCount = 0 isAlgorithmProcessOnApp = false
M01060C  11-09 12:11:15.054 28019 28019 I CAM_PhotoModule: onPictureTaken enablePreviewOverlayHint!
M01060D  11-09 12:11:15.055 28019 28019 I CAM_PhotoModule: saveFinalPhoto start!
M01060E  11-09 12:11:15.055 28019 28019 I CAM_PhotoModule: saveFinalPhoto title=IMG_20221109_121114.jpg
M01060F  11-09 12:11:15.056 28019 28019 I CAM_PhotoModule: saveFinalPhoto mIsImageCaptureIntent=false
M010611  11-09 12:11:15.056 28019 28019 I CAM_PhotoModule: saveFinalPhoto end! mCameraState=1 mContinuousCaptureCount=0
M010749  11-09 12:11:15.535 28019 28019 I CAM_PhotoModule: onPictureTaken mCameraState=3 mContinuousCaptureCount = 1 isBurstCapture()= false mIsContinousCaptureFinish =falsemHasCaptureCount = 0 isAlgorithmProcessOnApp = false     // 这个是在哪里回调的？


M01077B  11-09 12:11:15.567 28019 28019 I CAM_PhotoModule: saveFinalPhoto start!
M01077D  11-09 12:11:15.568 28019 28019 I CAM_PhotoModule: saveFinalPhoto title=IMG_20221109_121115.jpg
M01077E  11-09 12:11:15.568 28019 28019 I CAM_PhotoModule: saveFinalPhoto mIsImageCaptureIntent=false
M010785  11-09 12:11:15.571 28019 28019 I CAM_PhotoModule: saveFinalPhoto end! mCameraState=3 mContinuousCaptureCount=0
M01088F  11-09 12:11:15.851 28019 28019 I CAM_PhotoModule: onPictureTaken mCameraState=3 mContinuousCaptureCount = 0 isBurstCapture()= false mIsContinousCaptureFinish =falsemHasCaptureCount = 0 isAlgorithmProcessOnApp = false
M0108A4  11-09 12:11:15.856 28019 28019 I CAM_PhotoModule: onPictureTaken enablePreviewOverlayHint!
M0108A5  11-09 12:11:15.858 28019 28019 I CAM_PhotoModule: saveFinalPhoto start!
M0108A6  11-09 12:11:15.859 28019 28019 I CAM_PhotoModule: saveFinalPhoto title=IMG_20221109_121115.jpg
M0108A7  11-09 12:11:15.859 28019 28019 I CAM_PhotoModule: saveFinalPhoto mIsImageCaptureIntent=false
M0108A9  11-09 12:11:15.859 28019 28019 I CAM_PhotoModule: saveFinalPhoto end! mCameraState=1 mContinuousCaptureCount=0

从 log 中看相比于上一次拍照，少了一次 onPictureTaken 的回调

public static final int PREVIEW_STOPPED = 0;
public static final int IDLE = 1;  // preview is active
public static final int FOCUSING = 2;
public static final int SNAPSHOT_IN_PROGRESS = 3;
public static final int SWITCHING_CAMERA = 4;
```## 屏幕触摸事件 log

```text
dispatchTouches

11-16 19:51:06.707  1004  1190 D InputReader: dispatchTouches action DOWN now(ns): 8582548570509
11-16 19:51:06.773  1004  1190 D InputReader: dispatchTouches action UP now(ns): 8582614519631
```## NVA-2134 OOM 了？

```text
M00C62E  11-16 14:53:02.968 16307 21636 I .app.cameralit: Clamp target GC heap from 279MB to 256MB
M00C62F  11-16 14:53:02.968 16307 21636 I .app.cameralit: Alloc concurrent copying GC freed 5370(187KB) AllocSpace objects, 0(0B) LOS objects, 0% free, 255MB/256MB, paused 102us total 784.929ms
M00C630  11-16 14:53:02.968 16307 16323 I .app.cameralit: WaitForGcToComplete blocked Alloc on Alloc for 1.053s
M00C631  11-16 14:53:02.968 16307 16323 I .app.cameralit: Starting a blocking GC Alloc
M00C632  11-16 14:53:02.969 16307 21636 W .app.cameralit: Throwing OutOfMemoryError "Failed to allocate a 64 byte allocation with 191848 free bytes and 187KB until OOM, target footprint 268435456, growth limit 268435456; giving up on allocation because <1% of heap free after GC." (VmSize 1891592 kB)
M00C633  11-16 14:53:02.969   441 21628 I cmr_msg : 194, cmr_msg_get: thread[preview_cb],[1419, 32]msg-response 1059MS, last-post 900MS
M00C634  11-16 14:53:02.969   441 21628 I cmr_msg : 196, cmr_msg_get: msg type 0x2 num 5 cnt 100
C00C635  11-16 14:53:02.970 16307 21636 E AndroidRuntime: FATAL EXCEPTION: SurfaceTextureRenderer
C00C635  11-16 14:53:02.970 16307 21636 E AndroidRuntime: Process: com.hmdglobal.app.cameralite, PID: 16307
C00C635  11-16 14:53:02.970 16307 21636 E AndroidRuntime: java.lang.OutOfMemoryError: Failed to allocate a 64 byte allocation with 191848 free bytes and 187KB until OOM, target footprint 268435456, growth limit 268435456; giving up on allocation because <1% of heap free after GC.
C00C635  11-16 14:53:02.970 16307 21636 E AndroidRuntime:  at com.aiworks.android.glrenderer.PortraitDrawer.addTextureFrame(PortraitDrawer.java:176)
C00C635  11-16 14:53:02.970 16307 21636 E AndroidRuntime:  at com.dream.camera.modules.portraitphoto.HMDPortraitPhotoModule$3.onFrameAvailable(HMDPortraitPhotoModule.java:288)
C00C635  11-16 14:53:02.970 16307 21636 E AndroidRuntime:  at com.aiworks.android.glrenderer.SurfaceTextureRenderer$1.run(SurfaceTextureRenderer.java:61)
C00C635  11-16 14:53:02.970 16307 21636 E AndroidRuntime:  at android.os.Handler.handleCallback(Handler.java:938)
C00C635  11-16 14:53:02.970 16307 21636 E AndroidRuntime:  at android.os.Handler.dispatchMessage(Handler.java:99)
C00C635  11-16 14:53:02.970 16307 21636 E AndroidRuntime:  at android.os.Looper.loopOnce(Looper.java:201)
C00C635  11-16 14:53:02.970 16307 21636 E AndroidRuntime:  at android.os.Looper.loop(Looper.java:288)
C00C635  11-16 14:53:02.970 16307 21636 E AndroidRuntime:  at android.os.HandlerThread.run(HandlerThread.java:67)
M00C636  11-16 14:53:02.970   441 21567 I cmr_sensor: 959, cmr_sns_thread_proc: evt 524548
M00C637  11-16 14:53:02.970   441 21567 I cmr_sensor: 1379, cmr_sns_ioctl: cmd = 45, arg = 0xe10574d8.
M00C638  11-16 14:53:02.970   441 21567 I gc5035_sharkl2: 700, gc5035_drv_access_val: sensor gc5035: param_ptr->type=22
M00C639  11-16 14:53:02.970 16307 16338 I CAM2PORT_SprdAndCam2Agn: getNV21FromImage cost 1
M00C63A  11-16 14:53:02.970 16307 16317 I .app.cameralit: WaitForGcToComplete blocked Background on Alloc for 787.030ms
M00C63B  11-16 14:53:02.971 16307 16343 I .app.cameralit: WaitForGcToComplete blocked Alloc on Alloc for 787.316ms
M00C63C  11-16 14:53:02.971 16307 16343 I .app.cameralit: Starting a blocking GC Alloc
M00C63D  11-16 14:53:02.971 16307 16322 I .app.cameralit: WaitForGcToComplete blocked Alloc on Alloc for 787.275ms
M00C63E  11-16 14:53:02.971 16307 16322 I .app.cameralit: Starting a blocking GC Alloc
S00C63F  11-16 14:53:02.972 16307 21636 D HprofDebug: There is a OOM , but did not dumped, because of the present version is not USERDEBUG or did not tested by MONKEY.
M00C640  11-16 14:53:02.972   829   976 I InputReader: processEventsLocked: type=3 Count=3 code=57 value=-1 deviceId=1 when=5417100796000
M00C641  11-16 14:53:02.972   829   976 D InputReader: syncTouch: pointerCount 1 -> 0, touching ids 0x80000000 -> 0x00000000, hovering ids 0x00000000 -> 0x00000000, canceled ids 0x00000000
M00C642  11-16 14:53:02.972   829   976 D InputReader: dispatchTouches action UP now(ns): 5417101741835
M00C643  11-16 14:53:02.972   829   976 D InputReader: notifyMotion call dispatcher
E00C644  11-16 14:53:02.973   829  2748 I am_crash: [16307,0,com.hmdglobal.app.cameralite,551074885,java.lang.OutOfMemoryError,Failed to allocate a 64 byte allocation with 191848 free bytes and 187KB until OOM, target footprint 268435456, growth limit 268435456; giving up on allocation because <1% of heap free after GC.,PortraitDrawer.java,176]

Native 内存一直在增加
mBitmap
blurBitmap
mBitmapBackground
MakeupController
```## 人像模式拍照后 ANR

```text
==== State: NeedInfo by: cmadmin on 17 November 2022 14:37:47 ====

== Sunny.Hu@unisoc.com On 2022-11-17T06:35:15Z (json) ==
ANR 在30-40S之间//拍照后图片生成，拍照完成后内存很低。主线程APP超过256M 需要GC出空间。
Line 661193: ME4CA3F  01-03 10:53:29.416 31984 31984 I CAM_PhotoModule: onPictureTaken mCameraState=3 mContinuousCaptureCount = 1 isBurstCapture()= false mIsContinousCaptureFinish =falsemHasCaptureCount = 0 isAlgorithmProcessOnApp = true
Line 661193: ME4CA3F  01-03 10:53:29.416 31984 31984 I CAM_PhotoModule: onPictureTaken mCameraState=3 mContinuousCaptureCount = 1 isBurstCapture()= false mIsContinousCaptureFinish =falsemHasCaptureCount = 0 isAlgorithmProcessOnApp = true
Line 661194: ME4CA40  01-03 10:53:29.417 31984 31984 E CAM_PhotoModule: judgePlaySoundAndShutterAgain isNeedPlaySound = false
Line 661194: ME4CA40  01-03 10:53:29.417 31984 31984 E CAM_PhotoModule: judgePlaySoundAndShutterAgain isNeedPlaySound = false
Line 661195: ME4CA41  01-03 10:53:29.418 31984 31984 I CAM_CameraAppUI Dream: updateSwitchModeBtn canSwitch=true, switchShow=0
Line 661195: ME4CA41  01-03 10:53:29.418 31984 31984 I CAM_CameraAppUI Dream: updateSwitchModeBtn canSwitch=true, switchShow=0
Line 661199: ME4CA45  01-03 10:53:29.420 31984 31984 I CAM_PhotoModule: startPeekAnimation bitmap = null
Line 661199: ME4CA45  01-03 10:53:29.420 31984 31984 I CAM_PhotoModule: startPeekAnimation bitmap = null
Line 661205: ME4CA4B  01-03 10:53:29.426 31984 31984 I CAM_CameraActivity Drea: startPeekAnimation
Line 661205: ME4CA4B  01-03 10:53:29.426 31984 31984 I CAM_CameraActivity Drea: startPeekAnimation
Line 661234: ME4CA68  01-03 10:53:29.429 31984 31984 I CAM_CameraActivity Drea: indicateCapture
Line 661234: ME4CA68  01-03 10:53:29.429 31984 31984 I CAM_CameraActivity Drea: indicateCapture

Line 661876: ME4CCD9  01-03 10:53:30.644 31984 31994 I .app.cameralit: Clamp target GC heap from 264MB to 256MB
Line 661877: ME4CCDA  01-03 10:53:30.645 31984 31994 I .app.cameralit: Background concurrent copying GC freed 240840(8614KB) AllocSpace objects, 18(4616KB) LOS objects, 6% free, 240MB/256MB, paused 207us total 938.651ms
Line 661879: ME4CCDC  01-03 10:53:30.647   611  1815 I Camera2ClientBase: Closed Camera 1. Client was: com.hmdglobal.app.cameralite (PID 31984, UID 10147)
Line 661896: ME4CCED  01-03 10:53:30.665 31984 16842 I CAM2PORT_SprdAndCam2Agn: getNV21FromImage cost 4

ANR MAIN卡在这里。我想问下这块是干什么调用的？人像拍照后处理？

Line 664085: ME4D54F  01-03 10:53:37.194 31984 31984 F .app.cameralit: runtime.cc:669]   native: #27 pc 0213b3d9  /memfd:jit-cache (deleted) (offset 2000000) (com.android.camera.PhotoModule$JpegPictureCallback$1.onPostExecute+256)
Line 664086: ME4D54F  01-03 10:53:37.194 31984 31984 F .app.cameralit: runtime.cc:669]   native: #28 pc 0219a517  /memfd:jit-cache (deleted) (offset 2000000) (com.android.camera.PhotoModule$JpegPictureCallback$1.onPostExecute+134)
Line 664086: ME4D54F  01-03 10:53:37.194 31984 31984 F .app.cameralit: runtime.cc:669]   native: #28 pc 0219a517  /memfd:jit-cache (deleted) (offset 2000000) (com.android.camera.PhotoModule$JpegPictureCallback$1.onPostExecute+134)
Line 664087: ME4D54F  01-03 10:53:37.194 31984 31984 F .app.cameralit: runtime.cc:669]   at com.aiworks.android.portrait.PortraitPlusJni.process(Native method)
Line 664087: ME4D54F  01-03 10:53:37.194 31984 31984 F .app.cameralit: runtime.cc:669]   at com.aiworks.android.portrait.PortraitPlusJni.process(Native method)
Line 664088: ME4D54F  01-03 10:53:37.194 31984 31984 F .app.cameralit: runtime.cc:669]   at com.aiworks.android.PortraitPlusManager.processPortrait(PortraitPlusManager.java:52)
Line 664088: ME4D54F  01-03 10:53:37.194 31984 31984 F .app.cameralit: runtime.cc:669]   at com.aiworks.android.PortraitPlusManager.processPortrait(PortraitPlusManager.java:52)
Line 664089: ME4D54F  01-03 10:53:37.194 31984 31984 F .app.cameralit: runtime.cc:669]   at com.dream.camera.modules.portraitphoto.HMDPortraitPhotoModule.processJpegData(HMDPortraitPhotoModule.java:128)
Line 664089: ME4D54F  01-03 10:53:37.194 31984 31984 F .app.cameralit: runtime.cc:669]   at com.dream.camera.modules.portraitphoto.HMDPortraitPhotoModule.processJpegData(HMDPortraitPhotoModule.java:128)
(2022-11-17T06:27:05Z)
```## 切换模式之后卡死

```text
CAM_ModeScrollView  I  can not switch mode!

@Override
public boolean onTouch(View v, MotionEvent motionEvent) {
    if (unResponseClick()) {
        Log.i(TAG, "can not switch mode!");
        return false;
    }
    ...
}

这里返回 true 了
private boolean unResponseClick() {     //CameraAppUI.java
    return !getCanScrollable() || (mPreviewOverlay != null && mPreviewOverlay.isZooming());
}


这里返回 false?
private boolean getCanScrollable() {    //CameraAppUI.java
    boolean result = !((CameraActivity) getContext()).isModeTransitionViewShow() && !((CameraActivity) getContext()).getCameraAppUI().unResponseClick()
                         && isScrollable && (View.VISIBLE == getVisibility());
    return result;
}
```## Portrait拍照优化

```text
CameraActivity.THREAD_POOL_EXECUTOR.execute(new Runnable() {
    public void run() {
        fitExtendPanel(extendPanelParent);
        latch.countDown();
    }
});

解决方法:
http://192.168.3.81:8085/c/SPRD_S/SPRDROID12_TRUNK_22B_W22.09.2/+/3378
```## ZoomPanel.java

```text
@Override
public void setZoomVisible(int state) {
    this.setVisibility(state);
    if (mActivity != null && mActivity.getCameraAppUI().getZoomVisible()) {
        zoomGroup.setVisibility(state);
    }
    mActivity.getCameraAppUI().setZoomVisible(true);
    if (mZoomBar.isSimple() && !mActivity.isRecording()){
        if(View.VISIBLE == state){
            mActivity.getCameraAppUI().updateExtendPanelUI(View.GONE);
            mActivity.getCameraAppUI().updateFilterPanelUI(View.GONE);
```## SPRD JPEG流转YUV流遇到的问题

```text
11-19 16:55:11.301   519   918 D cmr_oem : 16215, camera_local_stop_preview: X
11-19 16:55:11.301   519   918 D Cam3OEMIf: 3026, setCameraState: X: camera state = SPRD_IDLE, preview state = SPRD_IDLE, capture state = SPRD_IDLE focus state = SPRD_IDLE set param state = SPRD_IDLE
11-19 16:55:11.301   519   918 I Cam3OEMIf: 4125, stopPreviewInternal: X Time:156 ms camera id 1
11-19 16:55:11.301   519   918 D Cam3OEMIf: 1297, stop: X
11-19 16:55:11.301   519   918 I Cam3OEMIf: 1256, stop: channel_type = 2, frame_number = 49
11-19 16:55:11.301   519   918 D Cam3OEMIf: 4170, cancelPictureInternal: E, state SPRD_IDLE
11-19 16:55:11.301   519   918 W Cam3OEMIf: 4195, cancelPictureInternal: not taking a picture (state SPRD_IDLE)
11-19 16:55:11.301   519   918 D Cam3OEMIf: 1297, stop: X
11-19 16:55:11.302   519   918 W Cam3Channel: 280, channelClearAllQBuff: channel has no valied stream
11-19 16:55:11.302   519   918 W Cam3Channel: 280, channelClearAllQBuff: channel has no valied stream
11-19 16:55:11.302   519   918 W Cam3Channel: 796, channelClearAllQBuff: channel has no valied stream
11-19 16:55:11.302   519   918 I Cam3HWI : 1385, flushRequest: :hal3: X
11-19 16:55:11.302   519   918 E CamDevSession@3.4-impl-sprd: processOneCaptureRequest_3_4: HAL process_capture_request call failed!
11-19 16:55:11.302   704  7060 E Camera3-Device: Camera 1: sendRequestsBatch: RequestThread: Unable to submit capture request 49 to HAL device: Function not implemented (-38)
11-19 16:55:11.302   704  7060 V CameraTraces: saveTrace: begin
11-19 16:55:11.304  6976  7027 E CAM2PORT_AndCam2AgntImp: Camera device '1' encountered error code '4'
11-19 16:55:11.305  6976  7013 W CAM_CameraActivity Drea: Camera open failure: HIST_ID1_-1_1_802_204_802_204_106_711_102_204_461_462_204_502_204_103_302_305_802_461_463_711_303_3_204_101_109_711_461_462_102_204_502_204_204_HEND
11-19 16:55:11.306  6976  6976 E CAM_FatalErrorHandler: Handling Camera Open Failure:
11-19 16:55:11.306  6976  6976 E CAM_FatalErrorHandler: java.lang.Exception
11-19 16:55:11.306  6976  6976 E CAM_FatalErrorHandler:  at com.android.camera.FatalErrorHandlerImpl.onCameraOpenFailure(FatalErrorHandlerImpl.java:49)
11-19 16:55:11.306  6976  6976 E CAM_FatalErrorHandler:  at com.android.camera.CameraActivity$9.run(CameraActivity.java:641)
11-19 16:55:11.306  6976  6976 E CAM_FatalErrorHandler:  at android.os.Handler.handleCallback(Handler.java:938)
11-19 16:55:11.306  6976  6976 E CAM_FatalErrorHandler:  at android.os.Handler.dispatchMessage(Handler.java:99)
11-19 16:55:11.306  6976  6976 E CAM_FatalErrorHandler:  at android.os.Looper.loopOnce(Looper.java:201)
11-19 16:55:11.306  6976  6976 E CAM_FatalErrorHandler:  at android.os.Looper.loop(Looper.java:288)
11-19 16:55:11.306  6976  6976 E CAM_FatalErrorHandler:  at android.app.ActivityThread.main(ActivityThread.java:7941)
11-19 16:55:11.306  6976  6976 E CAM_FatalErrorHandler:  at java.lang.reflect.Method.invoke(Native Method)
11-19 16:55:11.306  6976  6976 E CAM_FatalErrorHandler:  at com.android.internal.os.RuntimeInit$MethodAndArgsCaller.run(RuntimeInit.java:553)
11-19 16:55:11.306  6976  6976 E CAM_FatalErrorHandler:  at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:1003)
11-19 16:55:11.307  6976  6976 E CAM_CameraUtil: Show fatal error dialog
```## 人像模式放置一段时间会报错

```text
11-21 14:03:21.735   700 29425 E Camera3-Stream: returnBuffer: Stream 4: timestamp 10973596715403 is not increasing. Prev timestamp 10973596715403
11-21 14:03:21.735   700 29425 V Camera3-OutputStream: returnBufferCheckedLocked: A frame is dropped for stream 4 due to buffer error.
11-21 14:03:21.736   700 29425 V Camera3-IOStreamBase: returnAnyBufferLocked: Stream 4: All buffers returned; now idle
11-21 14:03:21.736   700 29425 V Camera3-Status: markComponent: Component 6 is now idle
11-21 14:03:21.736   518  5863 W Cam3Channel: 280, channelClearAllQBuff: channel has no valied stream
11-21 14:03:21.737   518  5863 D Cam3HWI : 2506, handleCbDataWithLock: mCameraId=0, i->frame_num=4073, frame_num=4073, i->req_id=27,i->bNotified=1, timestamp:10973596715403
11-21 14:03:21.737   700 29425 V Camera3-OutputStream: returnBufferCheckedLocked: A frame is dropped for stream 7 due to buffer error.
11-21 14:03:21.738   700 29424 V Camera3-Status: getDeviceStateLocked: Component 0 not idle
11-21 14:03:21.738   700 29424 V Camera3-Status: getDeviceStateLocked: Component 0 not idle
11-21 14:03:21.739   518  5863 D Cam3HWI : 2506, handleCbDataWithLock: mCameraId=0, i->frame_num=4074, frame_num=4074, i->req_id=27,i->bNotified=1, timestamp:10973596715403
11-21 14:03:21.740   700 29425 E Camera3-Stream: returnBuffer: Stream 7: timestamp 10973596715403 is not increasing. Prev timestamp 10973596715403
11-21 14:03:21.740   700 29425 V Camera3-OutputStream: returnBufferCheckedLocked: A frame is dropped for stream 7 due to buffer error.
11-21 14:03:21.741   518  5863 D Cam3HWI : 2506, handleCbDataWithLock: mCameraId=0, i->frame_num=4075, frame_num=4075, i->req_id=27,i->bNotified=1, timestamp:10973596715403
11-21 14:03:21.742   700 29425 E Camera3-Stream: returnBuffer: Stream 7: timestamp 10973596715403 is not increasing. Prev timestamp 10973596715403
11-21 14:03:21.742   700 29425 V Camera3-OutputStream: returnBufferCheckedLocked: A frame is dropped for stream 7 due to buffer error.
11-21 14:03:21.743   700 29425 V Camera3-IOStreamBase: returnAnyBufferLocked: Stream 7: All buffers returned; now idle
11-21 14:03:21.743   700 29425 V Camera3-Status: markComponent: Component 9 is now idle
11-21 14:03:21.743   700 29425 V Camera3-Status: markComponent: Component 0 is now idle
11-21 14:03:21.744   700 29424 V Camera3-Status: getDeviceStateLocked: Component 0 not idle
11-21 14:03:21.744   518  5863 I Cam3HWI : 1378, flushRequest: :hal3: X
11-21 14:03:21.744   700 29424 V Camera3-Status: getDeviceStateLocked: Component 0 not idle
11-21 14:03:21.745   700 29424 V Camera3-Status: getDeviceStateLocked: Component 1 not idle
11-21 14:03:21.760   518  5863 E CamDevSession@3.4-impl-sprd: processOneCaptureRequest_3_4: HAL process_capture_request call failed!
11-21 14:03:21.761   700 29425 E Camera3-Device: Camera 0: sendRequestsBatch: RequestThread: Unable to submit capture request 4075 to HAL device: Function not implemented (-38)
11-21 14:03:21.761   700 29425 V CameraTraces: saveTrace: begin
11-21 14:03:21.763 29335 29382 E CAM2PORT_AndCam2AgntImp: Camera device '0' encountered error code '4'
11-21 14:03:21.765 29335 29370 W CAM_CameraActivity Drea: Camera open failure: HIST_ID0_-1_1_302_305_802_204_106_711_102_461_462_204_502_204_303_204_103_302_305_802_461_463_711_303_3_302_305_204_101_109_711_461_462_204_102_204_502_303_204_204_204_204_303_204_301_204_204_204_204_204_302_305_204_303_204_303_204_303_204_301_302_305_303_204_303_204_204_204_HEND
11-21 14:03:21.767 29335 29335 E CAM_FatalErrorHandler: Handling Camera Open Failure:
11-21 14:03:21.767 29335 29335 E CAM_FatalErrorHandler: java.lang.Exception
11-21 14:03:21.767 29335 29335 E CAM_FatalErrorHandler:  at com.android.camera.FatalErrorHandlerImpl.onCameraOpenFailure(FatalErrorHandlerImpl.java:49)
11-21 14:03:21.767 29335 29335 E CAM_FatalErrorHandler:  at com.android.camera.CameraActivity$9.run(CameraActivity.java:641)
11-21 14:03:21.767 29335 29335 E CAM_FatalErrorHandler:  at android.os.Handler.handleCallback(Handler.java:938)
11-21 14:03:21.767 29335 29335 E CAM_FatalErrorHandler:  at android.os.Handler.dispatchMessage(Handler.java:99)
11-21 14:03:21.767 29335 29335 E CAM_FatalErrorHandler:  at android.os.Looper.loopOnce(Looper.java:201)
11-21 14:03:21.767 29335 29335 E CAM_FatalErrorHandler:  at android.os.Looper.loop(Looper.java:288)
11-21 14:03:21.767 29335 29335 E CAM_FatalErrorHandler:  at android.app.ActivityThread.main(ActivityThread.java:7941)
11-21 14:03:21.767 29335 29335 E CAM_FatalErrorHandler:  at java.lang.reflect.Method.invoke(Native Method)
11-21 14:03:21.767 29335 29335 E CAM_FatalErrorHandler:  at com.android.internal.os.RuntimeInit$MethodAndArgsCaller.run(RuntimeInit.java:553)
11-21 14:03:21.767 29335 29335 E CAM_FatalErrorHandler:  at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:1003)
11-21 14:03:21.769 29335 29335 E CAM_CameraUtil: Show fatal error dialog

原因可能是内存泄漏
```## 人像模式打开有点迟钝

```text
adb logcat | grep -E "freezeScreenUntilPreviewReady|CameraPerformanceTracker|CameraSurfaceViewPreviewCallback"

11-23 09:21:23.691  4596  4596 I CAM_PhotoUI: initUI cost: 0
11-23 09:21:23.692  4596  4596 I CAM_PhotoModule:  init null,0
11-23 09:21:23.692  4596  4596 I CAM_CameraActivity Drea: init totally cost: 84
11-23 09:21:23.693  4596  4596 D CAM_CameraActivity Drea: module:com.dream.camera.modules.portraitphoto.HMDPortraitPhotoModule@c0bff9c
11-23 09:21:23.693  4596  4596 I CAM_PhotoModule: resume start!
11-23 09:21:23.696  4596  4596 D CAM_CameraUtil: isTcamEnable false
11-23 09:21:23.696  4596  4596 I CAM_PhotoModule: requestCameraOpen mCameraId:0

11-23 09:21:24.223  4596  4596 D CameraPerformanceTracker: First preview frame received
```## 人像模式快速连续拍照之后无法点击，但是预览可以

```text
优化了拍照的流程，不会Block主线程
```## 权限列表

```text
frameworks/base/core/res/AndroidManifest.xml
```## NOVA 前摄添加录像1080P的分辨率之后XTS测试fail

```text
PASS 的log
01-03 00:17:23.407 10161 18603 18621 V CamcorderProfileTest: specific profile: quality=2, width = 176, height = 144
01-03 00:17:23.408 10161 18603 18621 V CamcorderProfileTest: specific profile: quality=3, width = 352, height = 288
01-03 00:17:23.408 10161 18603 18621 V CamcorderProfileTest: specific profile: quality=4, width = 720, height = 480
01-03 00:17:23.409 10161 18603 18621 V CamcorderProfileTest: specific profile: quality=5, width = 1280, height = 720
01-03 00:17:23.409 10161 18603 18621 V CamcorderProfileTest: min profile: quality=2, width = 176, height = 144
01-03 00:17:23.409 10161 18603 18621 V CamcorderProfileTest: max profile: quality=5, width = 1280, height = 720
01-03 00:17:23.410 10161 18603 18621 V CamcorderProfileTest: specific profile: quality=1002, width = 176, height = 144
01-03 00:17:23.410 10161 18603 18621 V CamcorderProfileTest: specific profile: quality=1003, width = 352, height = 288
01-03 00:17:23.410 10161 18603 18621 V CamcorderProfileTest: specific profile: quality=1004, width = 720, height = 480
01-03 00:17:23.410 10161 18603 18621 V CamcorderProfileTest: specific profile: quality=1005, width = 1280, height = 720
01-03 00:17:23.410 10161 18603 18621 V CamcorderProfileTest: min profile: quality=1002, width = 176, height = 144
01-03 00:17:23.411 10161 18603 18621 V CamcorderProfileTest: max profile: quality=1005, width = 1280, height = 720

CamcorderProfileTest.java
private void checkSpecificProfiles(
        int cameraId,
        CamcorderProfile low,
        CamcorderProfile high,
        int[] specificQualities,
        List<Size> videoSizes) {
    ...
    Log.v(TAG, String.format("min profile: quality=%d, width = %d, height = %d",
                minProfile.quality, minProfile.videoFrameWidth, minProfile.videoFrameHeight));
    Log.v(TAG, String.format("max profile: quality=%d, width = %d, height = %d",
                maxProfile.quality, maxProfile.videoFrameWidth, maxProfile.videoFrameHeight));
    assertProfileEquals(low, minProfile);
    assertProfileEquals(high, maxProfile);
}

11-23 15:55:19.457 10158 16139 16163 V CamcorderProfileTest: specific profile: quality=2, width = 176, height = 144
11-23 15:55:19.457 10158 16139 16163 V CamcorderProfileTest: specific profile: quality=3, width = 352, height = 288
11-23 15:55:19.457 10158 16139 16163 V CamcorderProfileTest: specific profile: quality=4, width = 720, height = 480
11-23 15:55:19.458 10158 16139 16163 V CamcorderProfileTest: specific profile: quality=5, width = 1280, height = 720
11-23 15:55:19.458 10158 16139 16163 V CamcorderProfileTest: specific profile: quality=6, width = 1920, height = 1080
11-23 15:55:19.458 10158 16139 16163 V CamcorderProfileTest: min profile: quality=2, width = 176, height = 144
11-23 15:55:19.458 10158 16139 16163 V CamcorderProfileTest: max profile: quality=6, width = 1920, height = 1080
11-23 15:55:19.460 10158 16139 16163 E TestRunner: failed: testGetWithId(android.media.cts.CamcorderProfileTest)
11-23 15:55:19.460 10158 16139 16163 E TestRunner: ----- begin exception -----
11-23 15:55:19.462 10158 16139 16163 E TestRunner: junit.framework.AssertionFailedError: expected:<5> but was:<2>
11-23 15:55:19.462 10158 16139 16163 E TestRunner:  at junit.framework.Assert.fail(Assert.java:50)
11-23 15:55:19.462 10158 16139 16163 E TestRunner:  at junit.framework.Assert.failNotEquals(Assert.java:287)
11-23 15:55:19.462 10158 16139 16163 E TestRunner:  at junit.framework.Assert.assertEquals(Assert.java:67)
11-23 15:55:19.462 10158 16139 16163 E TestRunner:  at junit.framework.Assert.assertEquals(Assert.java:199)
11-23 15:55:19.462 10158 16139 16163 E TestRunner:  at junit.framework.Assert.assertEquals(Assert.java:205)
11-23 15:55:19.462 10158 16139 16163 E TestRunner:  at android.media.cts.CamcorderProfileTest.assertProfileEquals(CamcorderProfileTest.java:240)
11-23 15:55:19.462 10158 16139 16163 E TestRunner:  at android.media.cts.CamcorderProfileTest.checkSpecificProfiles(CamcorderProfileTest.java:378)
11-23 15:55:19.462 10158 16139 16163 E TestRunner:  at android.media.cts.CamcorderProfileTest.checkGet(CamcorderProfileTest.java:475)
11-23 15:55:19.462 10158 16139 16163 E TestRunner:  at android.media.cts.CamcorderProfileTest.testGetWithId(CamcorderProfileTest.java:508)
11-23 15:55:19.462 10158 16139 16163 E TestRunner:  at java.lang.reflect.Method.invoke(Native Method)
11-23 15:55:19.462 10158 16139 16163 E TestRunner:  at junit.framework.TestCase.runTest(TestCase.java:168)
11-23 15:55:19.462 10158 16139 16163 E TestRunner:  at junit.framework.TestCase.runBare(TestCase.java:134)
11-23 15:55:19.462 10158 16139 16163 E TestRunner:  at junit.framework.TestResult$1.protect(TestResult.java:115)
11-23 15:55:19.462 10158 16139 16163 E TestRunner:  at androidx.test.internal.runner.junit3.AndroidTestResult.runProtected(AndroidTestResult.java:73)
11-23 15:55:19.462 10158 16139 16163 E TestRunner:  at junit.framework.TestResult.run(TestResult.java:118)
11-23 15:55:19.462 10158 16139 16163 E TestRunner:  at androidx.test.internal.runner.junit3.AndroidTestResult.run(AndroidTestResult.java:51)
11-23 15:55:19.462 10158 16139 16163 E TestRunner:  at junit.framework.TestCase.run(TestCase.java:124)
11-23 15:55:19.462 10158 16139 16163 E TestRunner:  at androidx.test.internal.runner.junit3.NonLeakyTestSuite$NonLeakyTest.run(NonLeakyTestSuite.java:62)
11-23 15:55:19.462 10158 16139 16163 E TestRunner:  at androidx.test.internal.runner.junit3.AndroidTestSuite$2.run(AndroidTestSuite.java:101)
11-23 15:55:19.462 10158 16139 16163 E TestRunner:  at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:462)
11-23 15:55:19.462 10158 16139 16163 E TestRunner:  at java.util.concurrent.FutureTask.run(FutureTask.java:266)
11-23 15:55:19.462 10158 16139 16163 E TestRunner:  at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1167)
11-23 15:55:19.462 10158 16139 16163 E TestRunner:  at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:641)
11-23 15:55:19.462 10158 16139 16163 E TestRunner:  at java.lang.Thread.run(Thread.java:920)
11-23 15:55:19.462 10158 16139 16163 E TestRunner: ----- end exception -----
11-23 15:55:19.467 10158 16139 16163 I TestRunner: finished: testGetWithId(android.media.cts.CamcorderProfileTest)
11-23 15:55:19.474 10158 16139 16161 I TestRunner: run finished: 1 tests, 1 failed, 0 ignored


private void assertProfileEquals(CamcorderProfile expectedProfile, CamcorderProfile actualProfile) {
    assertEquals(expectedProfile.duration, actualProfile.duration);
    assertEquals(expectedProfile.fileFormat, actualProfile.fileFormat);
    assertEquals(expectedProfile.videoCodec, actualProfile.videoCodec);             // 可能是这一条 assertFail 了，去掉 HEVC 编码的 1080P codec 就 ok了
    assertEquals(expectedProfile.videoBitRate, actualProfile.videoBitRate);
    assertEquals(expectedProfile.videoFrameRate, actualProfile.videoFrameRate);
    assertEquals(expectedProfile.videoFrameWidth, actualProfile.videoFrameWidth);
    assertEquals(expectedProfile.videoFrameHeight, actualProfile.videoFrameHeight);
    assertEquals(expectedProfile.audioCodec, actualProfile.audioCodec);
    assertEquals(expectedProfile.audioBitRate, actualProfile.audioBitRate);
    assertEquals(expectedProfile.audioSampleRate, actualProfile.audioSampleRate);
    assertEquals(expectedProfile.audioChannels, actualProfile.audioChannels);
}


CamcorderProfile lowProfile = getWithOptionalId(CamcorderProfile.QUALITY_LOW, cameraId);
CamcorderProfile highProfile = getWithOptionalId(CamcorderProfile.QUALITY_HIGH, cameraId);
CamcorderProfile lowTimeLapseProfile = getWithOptionalId(CamcorderProfile.QUALITY_TIME_LAPSE_LOW, cameraId);
CamcorderProfile highTimeLapseProfile = getWithOptionalId(CamcorderProfile.QUALITY_TIME_LAPSE_HIGH, cameraId);
checkSpecificProfiles(cameraId, lowProfile, highProfile, specificProfileQualities, videoSizes);                         public static final int QUALITY_HIGH = 1;
checkSpecificProfiles(cameraId, lowTimeLapseProfile, highTimeLapseProfile, specificTimeLapseProfileQualities, null);    public static final int QUALITY_TIME_LAPSE_HIGH = 1001;
checkSpecificProfiles(cameraId, lowHighSpeedProfile, highHighSpeedProfile, specificHighSpeedProfileQualities, null);    

private CamcorderProfile getWithOptionalId(int quality, int cameraId) {
    if (cameraId == -1) {
        return CamcorderProfile.get(quality);
    }
    return CamcorderProfile.get(cameraId, quality);
}

CamcorderProfile.java
public static CamcorderProfile get(int cameraId, int quality) {
    if (!((quality >= QUALITY_LIST_START &&
           quality <= QUALITY_LIST_END) ||
          (quality >= QUALITY_TIME_LAPSE_LIST_START &&
           quality <= QUALITY_TIME_LAPSE_LIST_END) ||
           (quality >= QUALITY_HIGH_SPEED_LIST_START &&
           quality <= QUALITY_HIGH_SPEED_LIST_END))) {
        String errMessage = "Unsupported quality level: " + quality;
        throw new IllegalArgumentException(errMessage);
    }
    return native_get_camcorder_profile(cameraId, quality);
}

解决方法：
http://192.168.3.81:8085/c/SPRD_S/SPRDROID12_TRUNK_22B_W22.09.2/+/3582
去掉 device/sprd/mpool/module/media/codec/msoc/sharkl3/media_profiles.xml 中的 HEVC 1080P 即可
```## NOVA 添加 1944x1944 和 3224x1488 分辨率 ITS 报错

```text
width 和 height 必须为 16 的倍数

http://192.168.3.81:8085/c/SPRD_S/SPRDROID12_TRUNK_22B_W22.09.2/+/4385
```## 改了 DreamCamera2 的签名之后报错

```text
11-24 08:58:01.577  6507  6507 E AndroidRuntime: FATAL EXCEPTION: main
11-24 08:58:01.577  6507  6507 E AndroidRuntime: Process: com.hmdglobal.app.cameralite, PID: 6507
11-24 08:58:01.577  6507  6507 E AndroidRuntime: java.lang.SecurityException: listen
11-24 08:58:01.577  6507  6507 E AndroidRuntime:  at android.os.Parcel.createExceptionOrNull(Parcel.java:2426)
11-24 08:58:01.577  6507  6507 E AndroidRuntime:  at android.os.Parcel.createException(Parcel.java:2410)
11-24 08:58:01.577  6507  6507 E AndroidRuntime:  at android.os.Parcel.readException(Parcel.java:2393)
11-24 08:58:01.577  6507  6507 E AndroidRuntime:  at android.os.Parcel.readException(Parcel.java:2335)
11-24 08:58:01.577  6507  6507 E AndroidRuntime:  at com.android.internal.telephony.ITelephonyRegistry$Stub$Proxy.listenWithEventList(ITelephonyRegistry.java:1036)
11-24 08:58:01.577  6507  6507 E AndroidRuntime:  at android.telephony.TelephonyRegistryManager.listenFromListener(TelephonyRegistryManager.java:250)
11-24 08:58:01.577  6507  6507 E AndroidRuntime:  at android.telephony.TelephonyManager.listen(TelephonyManager.java:6064)
11-24 08:58:01.577  6507  6507 E AndroidRuntime:  at com.android.camera.VideoModule.listenPhoneState(VideoModule.java:6018)
11-24 08:58:01.577  6507  6507 E AndroidRuntime:  at com.android.camera.VideoModule.resume(VideoModule.java:4736)
11-24 08:58:01.577  6507  6507 E AndroidRuntime:  at com.android.camera.CameraActivity.openModule(CameraActivity.java:3675)
11-24 08:58:01.577  6507  6507 E AndroidRuntime:  at com.android.camera.CameraActivity.onModeSelected(CameraActivity.java:3446)
11-24 08:58:01.577  6507  6507 E AndroidRuntime:  at com.android.camera.CameraActivity$53$1.run(CameraActivity.java:4258)
11-24 08:58:01.577  6507  6507 E AndroidRuntime:  at android.os.Handler.handleCallback(Handler.java:938)
11-24 08:58:01.577  6507  6507 E AndroidRuntime:  at android.os.Handler.dispatchMessage(Handler.java:99)
11-24 08:58:01.577  6507  6507 E AndroidRuntime:  at android.os.Looper.loopOnce(Looper.java:201)
11-24 08:58:01.577  6507  6507 E AndroidRuntime:  at android.os.Looper.loop(Looper.java:288)
11-24 08:58:01.577  6507  6507 E AndroidRuntime:  at android.app.ActivityThread.main(ActivityThread.java:7941)
11-24 08:58:01.577  6507  6507 E AndroidRuntime:  at java.lang.reflect.Method.invoke(Native Method)
11-24 08:58:01.577  6507  6507 E AndroidRuntime:  at com.android.internal.os.RuntimeInit$MethodAndArgsCaller.run(RuntimeInit.java:553)
11-24 08:58:01.577  6507  6507 E AndroidRuntime:  at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:1003)
11-24 08:58:01.577  6507  6507 E AndroidRuntime: Caused by: android.os.RemoteException: Remote stack trace:
11-24 08:58:01.577  6507  6507 E AndroidRuntime:  at com.android.internal.telephony.TelephonyPermissions.enforceCarrierPrivilege(TelephonyPermissions.java:634)
11-24 08:58:01.577  6507  6507 E AndroidRuntime:  at com.android.internal.telephony.TelephonyPermissions.enforceCallingOrSelfCarrierPrivilege(TelephonyPermissions.java:626)
11-24 08:58:01.577  6507  6507 E AndroidRuntime:  at com.android.server.TelephonyRegistry.checkListenerPermission(TelephonyRegistry.java:3170)
11-24 08:58:01.577  6507  6507 E AndroidRuntime:  at com.android.server.TelephonyRegistry.listen(TelephonyRegistry.java:1024)
11-24 08:58:01.577  6507  6507 E AndroidRuntime:  at com.android.server.TelephonyRegistry.listenWithEventList(TelephonyRegistry.java:996)
11-24 08:58:01.577  6507  6507 E AndroidRuntime: 
11-24 08:58:01.640  1006  6662 I DropBoxManagerService: add tag=system_app_crash isTagEnabled=true flags=0x2
11-24 08:58:01.656  1006  6667 E starklog2: update count  1 = 5 errorType = system_app_crash
```## 去掉人像模式 fast thumb 功能

```text
device/sprd/mpool/module/camera/msoc/sharkl3/sharkl3.mk
PRODUCT_PROPERTY_OVERRIDES += persist.vendor.cam.blur.fast.thumb=0

vendor/sprd/modules/libcamera/hal3_2v6/SprdCamera3Setting.cpp
// 39 blur fast thumb
property_get("persist.vendor.cam.blur.fast.thumb", prop, "0");
available_cam_features.add(atoi(prop));

vendor/sprd/platform/packages/apps/DreamCamera2/src/com/android/camera/util/CameraUtil.java
isBlurNeedThumbCallback = featureList[FeatureTagID.BLURFASTTHUMBCALLBACK.ordinal()] == 1 ? true : false;
```## 查看内存脚本

```text
#!/bin/bash
count=0
while true
do
    count=`expr $count + 1`
    adb shell input swipe 360 1432 360 1432 2200
    echo "UP  : "$count >>$count.txt
    adb shell dumpsys meminfo camerahalserver | egrep -i "OTAL PSS: ">>$count.txt
    adb shell dumpsys meminfo com.tcl.camera | egrep -i "OTAL PSS: ">>$count.txt
    adb shell cat d/ion/clients/clients_summary >>$count.txt
    adb shell cat /d/ion/ion_mm_heap >>$count.txt
    sleep 1
done
```## 合入奇酷360人像模式新的SDK

```text
11-29 16:18:23.170  9511  9511 F DEBUG   : *** *** *** *** *** *** *** *** *** *** *** *** *** *** *** ***
11-29 16:18:23.170  9511  9511 F DEBUG   : Native Crash TIME: 1980024
11-29 16:18:23.170  9511  9511 F DEBUG   : *** *** *** *** *** *** *** *** *** *** *** *** *** *** *** ***
11-29 16:18:23.170  9511  9511 F DEBUG   : Build fingerprint: 'Nokia/Nova_00WW/NVA:12/SP1A.210812.016/00WW_0_010:userdebug/release-keys'
11-29 16:18:23.170  9511  9511 F DEBUG   : Revision: '0'
11-29 16:18:23.170  9511  9511 F DEBUG   : ABI: 'arm'
11-29 16:18:23.170  9511  9511 F DEBUG   : Timestamp: 2022-11-29 16:18:22.074769445+0800
11-29 16:18:23.170  9511  9511 F DEBUG   : Process uptime: 3s
11-29 16:18:23.171  9511  9511 F DEBUG   : Cmdline: com.hmdglobal.app.cameralite
11-29 16:18:23.171  9511  9511 F DEBUG   : pid: 9332, tid: 9332, name: .app.cameralite  >>> com.hmdglobal.app.cameralite <<<
11-29 16:18:23.171  9511  9511 F DEBUG   : uid: 10147
11-29 16:18:23.171  9511  9511 F DEBUG   : signal 11 (SIGSEGV), code 1 (SEGV_MAPERR), fault addr 0x0
11-29 16:18:23.171  9511  9511 F DEBUG   : Cause: null pointer dereference
11-29 16:18:23.171  9511  9511 F DEBUG   :     r0  3b6bba93  r1  ff8cef14  r2  ff8ceee8  r3  00000000
11-29 16:18:23.171  9511  9511 F DEBUG   :     r4  ff8cef14  r5  00000000  r6  ff8cef14  r7  ee7052cc
11-29 16:18:23.171  9511  9511 F DEBUG   :     r8  ee7052cc  r9  e2f73780  r10 e2eeeea0  r11 bee10d5c
11-29 16:18:23.171  9511  9511 F DEBUG   :     ip  bee00674  sp  ff8cee50  lr  be9ff207  pc  be9ff360
11-29 16:18:23.171  9511  9511 F DEBUG   : backtrace:
11-29 16:18:23.171  9511  9511 F DEBUG   :       #00 pc 00238360  /system_ext/lib/libaw_portrait_plus.so (MNN::Interpreter::createMultiPathSession(std::__ndk1::vector<MNN::ScheduleConfig, std::__ndk1::allocator<MNN::ScheduleConfig> > const&, std::__ndk1::pair<std::__ndk1::map<MNNForwardType, std::__ndk1::shared_ptr<MNN::Runtime>, std::__ndk1::less<MNNForwardType>, std::__ndk1::allocator<std::__ndk1::pair<MNNForwardType const, std::__ndk1::shared_ptr<MNN::Runtime> > > >, std::__ndk1::shared_ptr<MNN::Runtime> > const&)+24) (BuildId: 2c56da483ed9bdbc5863eefa276b0ffabf36e07f)
11-29 16:18:23.171  9511  9511 F DEBUG   :       #01 pc 00238203  /system_ext/lib/libaw_portrait_plus.so (MNN::Interpreter::createMultiPathSession(std::__ndk1::vector<MNN::ScheduleConfig, std::__ndk1::allocator<MNN::ScheduleConfig> > const&)+34) (BuildId: 2c56da483ed9bdbc5863eefa276b0ffabf36e07f)
11-29 16:18:23.172  9511  9511 F DEBUG   :       #02 pc 00238681  /system_ext/lib/libaw_portrait_plus.so (MNN::Interpreter::createSession(MNN::ScheduleConfig const&)+40) (BuildId: 2c56da483ed9bdbc5863eefa276b0ffabf36e07f)
11-29 16:18:23.172  9511  9511 F DEBUG   :       #03 pc 000bc085  /system_ext/lib/libaw_portrait_plus.so (aw_commonyo_detect::YoloDetector_mnn_impl::engine_init()+384) (BuildId: 2c56da483ed9bdbc5863eefa276b0ffabf36e07f)
11-29 16:18:23.172  9511  9511 F DEBUG   :       #04 pc 000bba4f  /system_ext/lib/libaw_portrait_plus.so (aw_commonyo_detect::YoloDetector_impl::init(aw_commonyo_detect::YoloDetector_impl::Config const&)+700) (BuildId: 2c56da483ed9bdbc5863eefa276b0ffabf36e07f)
11-29 16:18:23.172  9511  9511 F DEBUG   :       #05 pc 000bae91  /system_ext/lib/libaw_portrait_plus.so (aw_commonyo_detect::YoloDetector::init(aw_commonyo_detect::YoloDetector::Config const&)+436) (BuildId: 2c56da483ed9bdbc5863eefa276b0ffabf36e07f)
11-29 16:18:23.172  9511  9511 F DEBUG   :       #06 pc 000a9e03  /system_ext/lib/libaw_portrait_plus.so (aw_commonyo_detect::YoloDetect_Engine::YoloDetect_Engine_Impl::init(aw_commonyo_detect::YoloDetect_Engine::YoloDetect_Engine_Impl::Config&, int)+100) (BuildId: 2c56da483ed9bdbc5863eefa276b0ffabf36e07f)
11-29 16:18:23.172  9511  9511 F DEBUG   :       #07 pc 000ad7bb  /system_ext/lib/libaw_portrait_plus.so (aw_commonyo_detect::YoloDetect_Engine::init(aw_commonyo_detect::ModelDataInput const&, int, float, int, int)+3366) (BuildId: 2c56da483ed9bdbc5863eefa276b0ffabf36e07f)
11-29 16:18:23.172  9511  9511 F DEBUG   :       #08 pc 000a8689  /system_ext/lib/libaw_portrait_plus.so (AW_CommonDetect::init(char*, int, float, int, int)+324) (BuildId: 2c56da483ed9bdbc5863eefa276b0ffabf36e07f)
11-29 16:18:23.172  9511  9511 F DEBUG   :       #09 pc 0008bcbb  /system_ext/lib/libaw_portrait_plus.so (aw_portrait_plus::AwPortraitPlus::init(char const*, ModelInfo&, ModelInfo&, ModelInfo&, ModelInfo&, ModelInfo&, ModelInfo&)+166) (BuildId: 2c56da483ed9bdbc5863eefa276b0ffabf36e07f)
11-29 16:18:23.172  9511  9511 F DEBUG   :       #10 pc 000a04ff  /system_ext/lib/libaw_portrait_plus.so (aw_portrait_plus_init+182) (BuildId: 2c56da483ed9bdbc5863eefa276b0ffabf36e07f)
11-29 16:18:23.172  9511  9511 F DEBUG   :       #11 pc 000d2e51  /system_ext/lib/libaw_portrait_plus.so (Java_com_aiworks_android_portrait_PortraitPlusJni_init+1028) (BuildId: 2c56da483ed9bdbc5863eefa276b0ffabf36e07f)
11-29 16:18:23.172  9511  9511 F DEBUG   :       #12 pc 000f4c8d  /apex/com.android.art/lib/libart.so (art_quick_generic_jni_trampoline+44) (BuildId: 4b0be921ea42a127a87079644133d1bb)
11-29 16:18:23.172  9511  9511 F DEBUG   :       #13 pc 000ebafc  /apex/com.android.art/lib/libart.so (nterp_helper+2124) (BuildId: 4b0be921ea42a127a87079644133d1bb)
11-29 16:18:23.172  9511  9511 F DEBUG   :       #14 pc 000a93a8  /system_ext/app/DreamCamera2/DreamCamera2.apk
11-29 16:18:23.173  9511  9511 F DEBUG   :       #15 pc 000ebda0  /apex/com.android.art/lib/libart.so (nterp_helper+2800) (BuildId: 4b0be921ea42a127a87079644133d1bb)
11-29 16:18:23.173  9511  9511 F DEBUG   :       #16 pc 0015bdc4  /system_ext/app/DreamCamera2/DreamCamera2.apk
11-29 16:18:23.173  9511  9511 F DEBUG   :       #17 pc 000ebda0  /apex/com.android.art/lib/libart.so (nterp_helper+2800) (BuildId: 4b0be921ea42a127a87079644133d1bb)
11-29 16:18:23.173  9511  9511 F DEBUG   :       #18 pc 000d97de  /system_ext/app/DreamCamera2/DreamCamera2.apk
11-29 16:18:23.173  9511  9511 F DEBUG   :       #19 pc 000ece30  /apex/com.android.art/lib/libart.so (nterp_helper+7040) (BuildId: 4b0be921ea42a127a87079644133d1bb)
11-29 16:18:23.173  9511  9511 F DEBUG   :       #20 pc 000c73b0  /system_ext/app/DreamCamera2/DreamCamera2.apk
11-29 16:18:23.173  9511  9511 F DEBUG   :       #21 pc 000ebda0  /apex/com.android.art/lib/libart.so (nterp_helper+2800) (BuildId: 4b0be921ea42a127a87079644133d1bb)
11-29 16:18:23.173  9511  9511 F DEBUG   :       #22 pc 000c6670  /system_ext/app/DreamCamera2/DreamCamera2.apk
11-29 16:18:23.173  9511  9511 F DEBUG   :       #23 pc 000ebda0  /apex/com.android.art/lib/libart.so (nterp_helper+2800) (BuildId: 4b0be921ea42a127a87079644133d1bb)
11-29 16:18:23.173  9511  9511 F DEBUG   :       #24 pc 000c05ec  /system_ext/app/DreamCamera2/DreamCamera2.apk
11-29 16:18:23.173  9511  9511 F DEBUG   :       #25 pc 00478743  /system/framework/arm/boot-framework.oat (android.os.Handler.dispatchMessage+74) (BuildId: 2f9580adc60ba1337dbf0c144e052d09956f12e2)
11-29 16:18:23.173  9511  9511 F DEBUG   :       #26 pc 0047acc1  /system/framework/arm/boot-framework.oat (android.os.Looper.loopOnce+1072) (BuildId: 2f9580adc60ba1337dbf0c144e052d09956f12e2)
11-29 16:18:23.174  9511  9511 F DEBUG   :       #27 pc 0047a817  /system/framework/arm/boot-framework.oat (android.os.Looper.loop+454) (BuildId: 2f9580adc60ba1337dbf0c144e052d09956f12e2)
11-29 16:18:23.174  9511  9511 F DEBUG   :       #28 pc 002a0c7d  /system/framework/arm/boot-framework.oat (android.app.ActivityThread.main+820) (BuildId: 2f9580adc60ba1337dbf0c144e052d09956f12e2)
11-29 16:18:23.174  9511  9511 F DEBUG   :       #29 pc 000f01d5  /apex/com.android.art/lib/libart.so (art_quick_invoke_stub_internal+68) (BuildId: 4b0be921ea42a127a87079644133d1bb)
11-29 16:18:23.174  9511  9511 F DEBUG   :       #30 pc 0050402d  /apex/com.android.art/lib/libart.so (art_quick_invoke_static_stub+284) (BuildId: 4b0be921ea42a127a87079644133d1bb)
11-29 16:18:23.174  9511  9511 F DEBUG   :       #31 pc 001453b3  /apex/com.android.art/lib/libart.so (art::ArtMethod::Invoke(art::Thread*, unsigned int*, unsigned int, art::JValue*, char const*)+154) (BuildId: 4b0be921ea42a127a87079644133d1bb)
11-29 16:18:23.174  9511  9511 F DEBUG   :       #32 pc 004010a9  /apex/com.android.art/lib/libart.so (_jobject* art::InvokeMethod<(art::PointerSize)4>(art::ScopedObjectAccessAlreadyRunnable const&, _jobject*, _jobject*, _jobject*, unsigned int)+852) (BuildId: 4b0be921ea42a127a87079644133d1bb)
11-29 16:18:23.174  9511  9511 F DEBUG   :       #33 pc 003959d3  /apex/com.android.art/lib/libart.so (art::Method_invoke(_JNIEnv*, _jobject*, _jobject*, _jobjectArray*)+30) (BuildId: 4b0be921ea42a127a87079644133d1bb)
11-29 16:18:23.174  9511  9511 F DEBUG   :       #34 pc 000aa05f  /apex/com.android.art/javalib/arm/boot.oat (art_jni_trampoline+62) (BuildId: 7f41230c938a538965c196cd0f2d66d36eb85995)
11-29 16:18:23.174  9511  9511 F DEBUG   :       #35 pc 0073429b  /system/framework/arm/boot-framework.oat (com.android.internal.os.RuntimeInit$MethodAndArgsCaller.run+122) (BuildId: 2f9580adc60ba1337dbf0c144e052d09956f12e2)
11-29 16:18:23.174  9511  9511 F DEBUG   :       #36 pc 0073b439  /system/framework/arm/boot-framework.oat (com.android.internal.os.ZygoteInit.main+1912) (BuildId: 2f9580adc60ba1337dbf0c144e052d09956f12e2)
11-29 16:18:23.174  9511  9511 F DEBUG   :       #37 pc 000f01d5  /apex/com.android.art/lib/libart.so (art_quick_invoke_stub_internal+68) (BuildId: 4b0be921ea42a127a87079644133d1bb)
11-29 16:18:23.174  9511  9511 F DEBUG   :       #38 pc 0050402d  /apex/com.android.art/lib/libart.so (art_quick_invoke_static_stub+284) (BuildId: 4b0be921ea42a127a87079644133d1bb)
11-29 16:18:23.174  9511  9511 F DEBUG   :       #39 pc 001453b3  /apex/com.android.art/lib/libart.so (art::ArtMethod::Invoke(art::Thread*, unsigned int*, unsigned int, art::JValue*, char const*)+154) (BuildId: 4b0be921ea42a127a87079644133d1bb)
11-29 16:18:23.174  9511  9511 F DEBUG   :       #40 pc 0040263b  /apex/com.android.art/lib/libart.so (art::JValue art::InvokeWithVarArgs<art::ArtMethod*>(art::ScopedObjectAccessAlreadyRunnable const&, _jobject*, art::ArtMethod*, std::__va_list)+350) (BuildId: 4b0be921ea42a127a87079644133d1bb)
11-29 16:18:23.175  9511  9511 F DEBUG   :       #41 pc 004028df  /apex/com.android.art/lib/libart.so (art::JValue art::InvokeWithVarArgs<_jmethodID*>(art::ScopedObjectAccessAlreadyRunnable const&, _jobject*, _jmethodID*, std::__va_list)+42) (BuildId: 4b0be921ea42a127a87079644133d1bb)
11-29 16:18:23.175  9511  9511 F DEBUG   :       #42 pc 003249c5  /apex/com.android.art/lib/libart.so (art::JNI<true>::CallStaticVoidMethodV(_JNIEnv*, _jclass*, _jmethodID*, std::__va_list)+456) (BuildId: 4b0be921ea42a127a87079644133d1bb)
11-29 16:18:23.175  9511  9511 F DEBUG   :       #43 pc 000767ed  /system/lib/libandroid_runtime.so (_JNIEnv::CallStaticVoidMethod(_jclass*, _jmethodID*, ...)+28) (BuildId: 9e1de8933d1ae07a8306996123c5340b)
11-29 16:18:23.175  9511  9511 F DEBUG   :       #44 pc 0007f2d7  /system/lib/libandroid_runtime.so (android::AndroidRuntime::start(char const*, android::Vector<android::String8> const&, bool)+602) (BuildId: 9e1de8933d1ae07a8306996123c5340b)
11-29 16:18:23.175  9511  9511 F DEBUG   :       #45 pc 0000251b  /system/bin/app_process32 (main+982) (BuildId: 0485601e73de507ff901a8995546a9e0)
11-29 16:18:23.175  9511  9511 F DEBUG   :       #46 pc 0005a61d  /apex/com.android.runtime/lib/bionic/libc.so (__libc_init+56) (BuildId: e0b2975f201bfaf34d6bad8983beb8b7)

models 放的路径不对，应该放在 DreamCamera2/assets/AIWorksModels/ 目录下，而不是放在 DreamCamera2/libs/libaw_portrait_plus/assets/AIWorksModels/ 目录下
```## NVA-2704 Monkey ANR

```text
"main" prio=5 tid=1 Native
  | group="main" sCount=1 ucsCount=0 flags=1 obj=0x70c67858 self=0xf60dce00
  | sysTid=13951 nice=-19 cgrp=top-app sched=0/0 handle=0xf664f470
  | state=S schedstat=( 25155638940 3172928265 16897 ) utm=2176 stm=339 core=6 HZ=100
  | stack=0xff178000-0xff17a000 stackSize=8188KB
  | held mutexes=
  native: #00 pc 0005c0b4  /apex/com.android.runtime/lib/bionic/libc.so (syscall+32)
  native: #01 pc 0006184d  /apex/com.android.runtime/lib/bionic/libc.so (__futex_wait_ex(void volatile*, bool, int, bool, timespec const*)+92)
  native: #02 pc 000a833b  /apex/com.android.runtime/lib/bionic/libc.so (pthread_cond_timedwait+76)
  native: #03 pc 0002e7f7  /vendor/lib/libsrv_um.so (PVRSRVFlushTaskContext+382)
  native: #04 pc 0112a22b  /vendor/lib/libPVROCL.so (???)
  native: #05 pc 000f8479  /system_ext/lib/libaw_ns_lite.so (clReleaseContext+60)
  native: #06 pc 000e4c05  /system_ext/lib/libaw_ns_lite.so (aw_night_shot::NightShotImpl::release()+556)
  native: #07 pc 000dd68d  /system_ext/lib/libaw_ns_lite.so (Java_com_jni_lib_AiWorksNsJni_native_1release+32)
  native: #08 pc 000f4c8d  /apex/com.android.art/lib/libart.so (art_quick_generic_jni_trampoline+44)
  at com.jni.lib.AiWorksNsJni.native_release(Native method)
  at com.jni.lib.AiWorksNsJni.release(AiWorksNsJni.java:306)
  at com.aiworks.android.lowlight.NightShotProxy.release(NightShotProxy.java:79)
  - locked <0x0edb9658> (a com.aiworks.android.lowlight.NightShotProxy)
  at com.aiworks.android.lowlight.NightCaptureResult.destory(NightCaptureResult.java:126)
  at com.dream.camera.modules.nightphoto.NightPhotoModule.pause(NightPhotoModule.java:200)
  at com.android.camera.CameraActivity.closeModule(CameraActivity.java:3707)
  at com.android.camera.CameraActivity.onModeSelected(CameraActivity.java:3454)
  at com.android.camera.CameraActivity$53$1.run(CameraActivity.java:4280)
  at android.os.Handler.handleCallback(Handler.java:938)
  at android.os.Handler.dispatchMessage(Handler.java:99)
  at android.os.Looper.loopOnce(Looper.java:201)
  at android.os.Looper.loop(Looper.java:288)
  at android.app.ActivityThread.main(ActivityThread.java:7941)
  at java.lang.reflect.Method.invoke(Native method)
  at com.android.internal.os.RuntimeInit$MethodAndArgsCaller.run(RuntimeInit.java:553)
  at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:1003)
```## NVA-2745 切换模式之后camera挂掉了

```text
11-18 21:03:33.088 25311  5957 I CAM_CameraAppUI Dream: rollTask runFreezeHide
11-18 21:03:33.089 25311  5957 I CAM_CameraActivity Drea: freezeScreenCommon cost: 39
11-18 21:03:33.089 25311  5957 I CAM_CameraActivity Drea: waitModeSelect run

11-18 21:03:33.095  1011  7129 I am_crash: [25311,0,com.hmdglobal.app.cameralite,551074885,java.lang.IllegalStateException,The specified message queue synchronization  barrier token has not been posted or has already been removed.,MessageQueue.java,528]

11-18 21:03:33.108  1011  7129 W ActivityTaskManager:   Force finishing activity com.hmdglobal.app.cameralite/com.android.camera.CameraActivity
11-18 21:03:33.109  1011  7129 I wm_finish_activity: [0,645914,26,com.hmdglobal.app.cameralite/com.android.camera.CameraActivity,force-crash]


C8E125E  01-03 07:43:44.781 12699 12699 E AndroidRuntime: FATAL EXCEPTION: main
C8E125E  01-03 07:43:44.781 12699 12699 E AndroidRuntime: Process: com.hmdglobal.app.cameralite, PID: 12699
C8E125E  01-03 07:43:44.781 12699 12699 E AndroidRuntime: java.lang.IllegalStateException: The specified message queue synchronization  barrier token has not been posted or has already been removed.
C8E125E  01-03 07:43:44.781 12699 12699 E AndroidRuntime:  at android.os.MessageQueue.removeSyncBarrier(MessageQueue.java:528)
C8E125E  01-03 07:43:44.781 12699 12699 E AndroidRuntime:  at android.view.ViewRootImpl.doTraversal(ViewRootImpl.java:2183)
C8E125E  01-03 07:43:44.781 12699 12699 E AndroidRuntime:  at android.view.ViewRootImpl$TraversalRunnable.run(ViewRootImpl.java:8753)
C8E125E  01-03 07:43:44.781 12699 12699 E AndroidRuntime:  at android.view.Choreographer$CallbackRecord.run(Choreographer.java:1038)
C8E125E  01-03 07:43:44.781 12699 12699 E AndroidRuntime:  at android.view.Choreographer.doCallbacks(Choreographer.java:846)
C8E125E  01-03 07:43:44.781 12699 12699 E AndroidRuntime:  at android.view.Choreographer.doFrame(Choreographer.java:781)
C8E125E  01-03 07:43:44.781 12699 12699 E AndroidRuntime:  at android.view.Choreographer$FrameDisplayEventReceiver.run(Choreographer.java:1023)
C8E125E  01-03 07:43:44.781 12699 12699 E AndroidRuntime:  at android.os.Handler.handleCallback(Handler.java:938)
C8E125E  01-03 07:43:44.781 12699 12699 E AndroidRuntime:  at android.os.Handler.dispatchMessage(Handler.java:99)
C8E125E  01-03 07:43:44.781 12699 12699 E AndroidRuntime:  at android.os.Looper.loopOnce(Looper.java:201)
C8E125E  01-03 07:43:44.781 12699 12699 E AndroidRuntime:  at android.os.Looper.loop(Looper.java:288)
C8E125E  01-03 07:43:44.781 12699 12699 E AndroidRuntime:  at android.app.ActivityThread.main(ActivityThread.java:7941)
C8E125E  01-03 07:43:44.781 12699 12699 E AndroidRuntime:  at java.lang.reflect.Method.invoke(Native Method)
C8E125E  01-03 07:43:44.781 12699 12699 E AndroidRuntime:  at com.android.internal.os.RuntimeInit$MethodAndArgsCaller.run(RuntimeInit.java:553)
C8E125E  01-03 07:43:44.781 12699 12699 E AndroidRuntime:  at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:1003)

CameraAppUI.java
private class ModeSelectCoverRunnable implements Runnable {
    @Override
    public void run() {
        mModeListView.startModeSelectionAnimation();
        waitToHide = false;
        if (mAppRootView != null) {
            mAppRootView.post(new Runnable() {                      // 会不会是这里的问题？
                @Override
                public void run() {
                    if (mController != null && !mController.isPaused() && !isInIntentReview()) {
                        getModulePreviewOverlayBitmap();
                    }
                }
            });
        }
    }
}

View.java
/**
 * <p>Causes the Runnable to be added to the message queue.
 * The runnable will be run on the user interface thread.</p>
 *
 * @param action The Runnable that will be executed.
 *
 * @return Returns true if the Runnable was successfully placed in to the
 *         message queue.  Returns false on failure, usually because the
 *         looper processing the message queue is exiting.
 *
 * @see #postDelayed
 * @see #removeCallbacks
 */
public boolean post(Runnable action) {
    final AttachInfo attachInfo = mAttachInfo;
    if (attachInfo != null) {
        return attachInfo.mHandler.post(action);
    }

    // Postpone the runnable until we know on which thread it needs to run.
    // Assume that the runnable will be successfully placed after attach.
    getRunQueue().post(action);
    return true;
}

MessageQueue.java
public void removeSyncBarrier(int token) {
    // Remove a sync barrier token from the queue.
    // If the queue is no longer stalled by a barrier then wake it.
    synchronized (this) {
        Message prev = null;
        Message p = mMessages;
        while (p != null && (p.target != null || p.arg1 != token)) {
            prev = p;
            p = p.next;
        }
        if (p == null) {
            throw new IllegalStateException("The specified message queue synchronization "
                    + " barrier token has not been posted or has already been removed.");
        }
        final boolean needWake;
        if (prev != null) {
            prev.next = p.next;
            needWake = false;
        } else {
            mMessages = p.next;
            needWake = mMessages == null || mMessages.target != null;
        }
        p.recycleUnchecked();

        // If the loop is quitting then it is already awake.
        // We can assume mPtr != 0 when mQuitting is false.
        if (needWake && !mQuitting) {
            nativeWake(mPtr);
        }
    }
}

在使用handler.sendMessage(msg)后遇到如下错误报告：
java.lang.IllegalStateException: The specified message queue synchronization barrier token has not been posted or has already been removed.

最后使用dispatchMessage(msg)方法解决了问题，问题原因未知。

（改进版）问题同上，在handler的handlerMessage()方法中加一条，this.obtainMessage()之后错误消失。我怀疑是跟android自身设计的缺陷有关，全部自动进行信息send和接收会产生误差，手动要求检查并obtain信息就可以解决这一问题。
————————————————
版权声明：本文为CSDN博主「Erwin_H」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/hz0324/article/details/9265671

解决办法：在UI线程的Handler的handleMessage方法中，更新UI之前加入this.obtainMessage();即可。
```## NVA-2719 前摄设置为自动白屏补光之后预览会卡死

```text
vendor/sprd/platform/packages/apps/DreamCamera2/src/com/dream/camera/ButtonManagerDream.java
public void setBGWhite(boolean bgWhite) {
    if(mButtonCountdownDream!=null) mButtonCountdownDream.setBGWhite(bgWhite);
    if(mButtonRatioDream!=null) mButtonRatioDream.setBGWhite(bgWhite);
    if(mButtonSettingDream!=null) mButtonSettingDream.setColorFilter(bgWhite ? Color.BLACK :Color.TRANSPARENT);
    if(mButtonFlashDream != null) mButtonFlashDream.setColorFilter(bgWhite ? 0xff40ccff : Color.TRANSPARENT);
    // 为什么上面两句会引起？？？？
}


修改方法：
public void setBGWhite(boolean bgWhite) {
    if (mButtonCountdownDream != null) {
        mButtonCountdownDream.setBGWhite(bgWhite);
    }
    if (mButtonRatioDream != null) {
        mButtonRatioDream.setBGWhite(bgWhite);
    }
    if (mButtonSettingDream != null) {
        mButtonSettingDream.setBGWhite(bgWhite);
    }
    if (mButtonFlashDream != null) {
        mButtonFlashDream.setBGWhite(bgWhite);
    }
}
```## 夜景模式没有效果

```text
12-01 14:04:19.496 30994 31169 W System.err: org.xmlpull.v1.XmlPullParserException: expected: '>' actual: '<' (position:END_TAG </night_tmoLevel>@189:13 in java.io.InputStreamReader@a378d60) 
12-01 14:04:19.496 30994 31169 W System.err:  at com.android.org.kxml2.io.KXmlParser.checkRelaxed(KXmlParser.java:305)
12-01 14:04:19.497 30994 31169 W System.err:  at com.android.org.kxml2.io.KXmlParser.read(KXmlParser.java:1443)
12-01 14:04:19.497 30994 31169 W System.err:  at com.android.org.kxml2.io.KXmlParser.readEndTag(KXmlParser.java:969)
12-01 14:04:19.497 30994 31169 W System.err:  at com.android.org.kxml2.io.KXmlParser.next(KXmlParser.java:375)
12-01 14:04:19.497 30994 31169 W System.err:  at com.android.org.kxml2.io.KXmlParser.next(KXmlParser.java:313)
12-01 14:04:19.497 30994 31169 W System.err:  at com.aiworks.android.camera.CameraPreferences.loadCustomizedCameraPreferences(CameraPreferences.java:225)
12-01 14:04:19.497 30994 31169 W System.err:  at com.aiworks.android.camera.CameraPreferences.parseCameraPreferencesXml(CameraPreferences.java:99)
12-01 14:04:19.497 30994 31169 W System.err:  at com.aiworks.android.lowlight.NightCaptureRequest.init(NightCaptureRequest.java:115)
12-01 14:04:19.497 30994 31169 W System.err:  at com.dream.camera.modules.nightphoto.NightPhotoModule.lambda$resume$0(NightPhotoModule.java:146)
12-01 14:04:19.497 30994 31169 W System.err:  at com.dream.camera.modules.nightphoto.NightPhotoModule.$r8$lambda$37TgNZybiShwVTfMH1upl3B5slk(Unknown Source:0)
12-01 14:04:19.497 30994 31169 W System.err:  at com.dream.camera.modules.nightphoto.NightPhotoModule$$ExternalSyntheticLambda1.run(Unknown Source:2)
12-01 14:04:19.497 30994 31169 W System.err:  at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:462)
12-01 14:04:19.497 30994 31169 W System.err:  at java.util.concurrent.FutureTask.run(FutureTask.java:266)
12-01 14:04:19.497 30994 31169 W System.err:  at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1167)
12-01 14:04:19.497 30994 31169 W System.err:  at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:641)
12-01 14:04:19.498 30994 31169 W System.err:  at java.lang.Thread.run(Thread.java:920)

从 log 中看是 xml 文件读取失败
12-01 14:04:19.505 30994 31169 I AW_NS_EXP: AIWorksNsExpInit: E
12-01 14:04:19.505 30994 31169 I AW_NS_EXP: AIWORKS_NS_EXP_1.7.2
12-01 14:04:19.505 30994 31169 I AW_NS_EXP: AIWorksNsExpConfig readXML xmlPath = /storage/emulated/0/Android/data/com.hmdglobal.app.cameralite/files/night/aiworks_night_config_0.xml
12-01 14:04:19.509 30994 31169 W AW_NS_EXP: AIWorksNsExpConfig fail to readXML
12-01 14:04:19.510 30994 31169 I AW_NS_EXP: AIWorksNsExpConfig ProjectName =  mFaceDetect = 0, platform = 0
12-01 14:04:19.510 30994 31169 E AW_NS_EXP: AIWorksNsExpInit: X, fail ret = -1
12-01 14:04:19.510 30994 31169 I AW_NS_EXP: AIWorksNsExpJni_init handle = 0x0
```## 长按无法连拍

```text
12-01 20:36:08.358 20516 20516 D CAM_AutoPhotoModule: huanglj down
12-01 20:36:08.358 20516 20516 I CAM_AutoPhotoModule:  call handleActionDown 
12-01 20:36:08.358 20516 20516 I CAM_CaptureActionDispat: onTouchEvent ACTION_DOWN isLongPress = false
12-01 20:36:08.358 20516 20516 I CAM_PhotoModule: onShutterButtonFocus pressed = true
12-01 20:36:08.362 20516 20516 D ViewRootImpl: ViewRootImpl performMeasure , childWidthMeasureSpec = 1073742544, childHeightMeasureSpec = 1073743384, mTag=ViewRootImpl[CameraActivity] ,this = android.view.UnisocViewRootImpl@a3b2681
12-01 20:36:08.380 20516 20516 D ViewRootImpl: ViewRootImpl performLayout , Laying out DecorView@1a1d14[CameraActivity] to (720, 1560), mTag=ViewRootImpl[CameraActivity] ,this = android.view.UnisocViewRootImpl@a3b2681
12-01 20:36:08.382 20516 20516 D ViewRootImpl: ViewRootImpl performDraw , usingAsyncReport :false mTag=ViewRootImpl[CameraActivity] ,this = android.view.UnisocViewRootImpl@a3b2681
12-01 20:36:08.759 20516 20516 I CAM_CaptureActionDispat: run mLongPressRunnable 
12-01 20:36:10.527 20516 20516 D CAM_AutoPhotoModule: huanglj move
12-01 20:36:12.526 20516 20516 D CAM_AutoPhotoModule: huanglj move
12-01 20:36:12.607 20516 20516 I CAM_AutoPhotoModule: call handleActionUp 
12-01 20:36:12.607 20516 20516 D CAM_CaptureActionDispat: onTouchEvent ACTION_UP isLongPress = true
12-01 20:36:12.607 20516 20516 D CAM_AutoPhotoModule: huanglj up
12-01 20:36:12.609 20516 20516 I CAM_ShutterButton: ShutterButton performClick
12-01 20:36:12.615 20516 20516 I CAM_PhotoModule: onShutterButtonFocus pressed = false
12-01 20:36:12.616 20516 20516 I CAM_PhotoModule: isFlashOn  flashValues = off
12-01 20:36:23.658 20516 20516 D CAM_PhotoModule: onHdrDeteCtion: false

怀疑是设置了 HDR Auto, 检测到了 HDR 场景
```## NVA-2757 录像设置 720P 之后点击录像Camera卡死

```text
      CAM_ShutterButton  I  ShutterButton performClick
        CAM_VideoModule  I  onShutterButtonClick
     CAM_ModeScrollView  I   setScrollable :false
            CAM_BMDream  D  disableButton: 21
           AudioManager  W  Use of stream types is deprecated for operations other than volume control
                         W  See the documentation of requestAudioFocus() for what to use instead with android.media.AudioAttributes to qualify your playback use case
        CAM_VideoModule  I  requestAudioFocus 1
                         I  startVideoRecording: Thread[main,5,main]
                         I   sensorOrientation = 90 ,deviceOrientation = 0 isFrontCamera = false
CAM2PORT_DispatchThread  I  Runnable job.run() end!
                         I  DispatchThread.this.wait will!
CAM2PORT_AndCam2AgntImp  I  AppFW handleMessage - action = 'UNKNOWN(503)'
CAM2PORT_DispatchThread  I  DispatchThread.this.notifyAll()!
                         I  DispatchThread.this.wait end!
  CAM_CameraAppUI Dream  D  bbbb setShutterPartInBottomBarShow visible=0
     CAM_ModeScrollView  I   setScrollable :false
            CAM_VideoUI  V  mFocusRing.stopFocusAnimations()
eferenceSettingFragment  I  dismissDialogIfNecessary keyOfDialog=pref_video_resolution_key
           ViewRootImpl  D  ViewRootImpl performMeasure , childWidthMeasureSpec = 1073742544, childHeightMeasureSpec = 1073743384, mTag=ViewRootImpl[CameraActivity] ,this = android.view.UnisocViewRootImpl@44d2f4f
                         D  ViewRootImpl performLayout , Laying out DecorView@7d7716b[CameraActivity] to (720, 1560), mTag=ViewRootImpl[CameraActivity] ,this = android.view.UnisocViewRootImpl@44d2f4f
                         D  ViewRootImpl performDraw , usingAsyncReport :false mTag=ViewRootImpl[CameraActivity] ,this = android.view.UnisocViewRootImpl@44d2f4f
            zhangqi8888  E  com.dream.camera.ui.ZoomLineView-->setBoxView()-->42 getX():73.0 xx:207 mWidth:53
           ViewRootImpl  D  ViewRootImpl performDraw , usingAsyncReport :false mTag=ViewRootImpl[CameraActivity] ,this = android.view.UnisocViewRootImpl@44d2f4f
        CAM_VideoModule  I  initializeRecorder: Thread[main,5,main]
CAM2PORT_DispatchThread  I  Runnable job.run() end!
                         I  DispatchThread.this.wait will!
CAM2PORT_AndCam2AgntImp  I  AppFW handleMessage - action = 'UNLOCK'
CAM2PORT_DispatchThread  I  DispatchThread.this.notifyAll()!
                         I  DispatchThread.this.wait end!
         CAM_CameraUtil  D  isTcamEnable false
        CAM_VideoModule  I  quality for CIF is 3 = 5
                         I  initializeRecorder end
CAM_CameraActivity Drea  I  updateStorageSpaceAndHint end
           CAM_Profiler  I  [  0.000ms] GUARD: initializeRecorder - START
             DreamProxy  E  setParam64BitFileOffset error:android.media.MediaRecorder.setParam64BitFileOffset [boolean]
           ViewRootImpl  D  ViewRootImpl performDraw , usingAsyncReport :false mTag=ViewRootImpl[CameraActivity] ,this = android.view.UnisocViewRootImpl@44d2f4f
         CAM_CameraUtil  E  current sdk version is 31
                         E  current sdk version is 31
        CAM_VideoModule  V  New video filename: /storage/emulated/0/DCIM/Camera/VID_20221201_214253.mp4
         CAM_CameraUtil  E  current sdk version is 31
        CAM_VideoModule  D  insert uri is content://media/external/video/media/148
CAM_CameraActivity Drea  I  mLocalChangeListener onChange uri = content://media/external/video/media/148 flags = 4
        CAM_VideoModule  D  video ParcelFileDescriptor is {ParcelFileDescriptor: java.io.FileDescriptor@2676a41}
           CAM_Profiler  I  [ 61.333ms][ui] GUARD: initializeRecorder - [61.333ms] MediaRecorder prepare
                         I  [ 61.333ms][ui] GUARD: initializeRecorder - STOP
           ViewRootImpl  D  ViewRootImpl performDraw , usingAsyncReport :false mTag=ViewRootImpl[CameraActivity] ,this = android.view.UnisocViewRootImpl@44d2f4f
oundPool::StreamManager  D  run: StreamManager:0xf4abe070 mStreamManagerLock released



OK
12-01 21:47:53.310 27565 27565 I CAM_VideoModule: onShutterButtonClick
12-01 21:47:53.320 27565 27565 I CAM_VideoModule: requestAudioFocus 1
12-01 21:47:53.321 27565 27565 I CAM_VideoModule: startVideoRecording: Thread[main,5,main]
12-01 21:47:53.323 27565 27565 I CAM_VideoModule:  sensorOrientation = 90 ,deviceOrientation = 0 isFrontCamera = false
12-01 21:47:53.402 27565 27565 I CAM_VideoModule: initializeRecorder: Thread[main,5,main]
12-01 21:47:53.533 27565 27565 I CAM_VideoModule: quality for CIF is 3 = 6
12-01 21:47:53.542 27565 27565 I CAM_VideoModule: initializeRecorder end
12-01 21:47:53.565 27565 27776 V CAM_VideoModule: New video filename: /storage/emulated/0/DCIM/Camera/VID_20221201_214753.mp4
12-01 21:47:53.628 27565 27776 D CAM_VideoModule: insert uri is content://media/external/video/media/151
12-01 21:47:53.661 27565 27776 D CAM_VideoModule: video ParcelFileDescriptor is {ParcelFileDescriptor: java.io.FileDescriptor@5827666}

12-01 21:47:54.167 27565 27604 D CAM_VideoModule: onVideoStart , mPaused = false
12-01 21:47:54.171 27565 27565 I CAM_VideoModule: requestAudioFocus 1
12-01 21:47:54.175 27565 27565 E CAM_VideoModule: when isRecording music status:false
12-01 21:47:54.251 27565 27565 D CAM_VideoModule: setExposureCompensation vaule0


NOK
12-01 21:48:10.898 27565 27565 I CAM_VideoModule: onShutterButtonClick
12-01 21:48:10.906 27565 27565 I CAM_VideoModule: requestAudioFocus 1
12-01 21:48:10.907 27565 27565 I CAM_VideoModule: startVideoRecording: Thread[main,5,main]
12-01 21:48:10.909 27565 27565 I CAM_VideoModule:  sensorOrientation = 90 ,deviceOrientation = 0 isFrontCamera = false
12-01 21:48:10.962 27565 27565 I CAM_VideoModule: initializeRecorder: Thread[main,5,main]
12-01 21:48:10.994 27565 27565 I CAM_VideoModule: quality for CIF is 3 = 5
12-01 21:48:10.998 27565 27565 I CAM_VideoModule: initializeRecorder end
12-01 21:48:11.009 27565 27776 V CAM_VideoModule: New video filename: /storage/emulated/0/DCIM/Camera/VID_20221201_214811.mp4
12-01 21:48:11.044 27565 27776 D CAM_VideoModule: insert uri is content://media/external/video/media/152
12-01 21:48:11.068 27565 27776 D CAM_VideoModule: video ParcelFileDescriptor is {ParcelFileDescriptor: java.io.FileDescriptor@7f6b4cf}

最终发现是马工的优化 video 性能引起的
```## Camera 权限在一段时间之后会被回收

```text
M0085EB  12-02 00:00:54.317  1388  1388 I AutoRevokePermissions: revokeUnused com.hmdglobal.app.cameralite - [android.permission.ACCESS_COARSE_LOCATION, android.permission.ACCESS_FINE_LOCATION]
M0085EC  12-02 00:00:54.321  1388  1388 I AutoRevokePermissions: revoking com.hmdglobal.app.cameralite - [android.permission.ACCESS_COARSE_LOCATION, android.permission.ACCESS_FINE_LOCATION]
M0085ED  12-02 00:00:54.322  1388  1388 I AutoRevokePermissions: State pre revocation: {android.permission.ACCESS_COARSE_LOCATION=android.permission.ACCESS_COARSE_LOCATION, Granted, UserSet, UserSensitive, android.permission.ACCESS_FINE_LOCATION=android.permission.ACCESS_FINE_LOCATION, Granted, UserSet, UserSensitive, SelectedLocationAccuracy}
M0085EE  12-02 00:00:54.323  1388  1388 I AutoRevokePermissions: Bg state post revocation: {android.permission.ACCESS_COARSE_LOCATION=android.permission.ACCESS_COARSE_LOCATION, Granted, UserSet, UserSensitive, android.permission.ACCESS_FINE_LOCATION=android.permission.ACCESS_FINE_LOCATION, Granted, UserSet, UserSensitive, SelectedLocationAccuracy}
M008605  12-02 00:00:54.493  1388  1388 I AutoRevokePermissions: revokeUnused com.hmdglobal.app.cameralite - [android.permission.READ_PHONE_STATE]
M008606  12-02 00:00:54.495  1388  1388 I AutoRevokePermissions: revoking com.hmdglobal.app.cameralite - [android.permission.READ_PHONE_STATE]
M008607  12-02 00:00:54.496  1388  1388 I AutoRevokePermissions: State pre revocation: {android.permission.READ_PHONE_STATE=android.permission.READ_PHONE_STATE, Granted, UserSet, UserSensitive}
M008608  12-02 00:00:54.498  1388  1388 I AutoRevokePermissions: Bg state post revocation: {android.permission.READ_PHONE_STATE=android.permission.READ_PHONE_STATE, Granted, UserSet, UserSensitive}
M00860D  12-02 00:00:54.581   980  1891 D PackageManager: PMS setEnabledSetting: packageName = com.hmdglobal.app.devicelock, className = androidx.work.impl.background.systemjob.SystemJobService, newState = 1, flags = 1, userId = 0, callingPackage = null, callingUid = 1000, allowedByPermission = true
M00860E  12-02 00:00:54.591  1798  2424 W DynamiteModule: Local module descriptor class for com.google.android.gms.googlecertificates not found.
M00860F  12-02 00:00:54.592  1388  1388 I AutoRevokePermissions: Fg state post revocation: {android.permission.READ_PHONE_STATE=android.permission.READ_PHONE_STATE, NotGranted, UserSet, UserSensitive}

自动重置未使用的应用的权限
如果应用以 Android 11 为目标平台并且数月未使用，系统会通过自动重置用户已授予应用的敏感权限来保护用户数据。此操作与用户在系统设置中查看权限并将应用的访问权限级别更改为拒绝的做法效果一样。如果应用遵循有关在运行时请求权限的最佳做法，那么您不必对应用进行任何更改。这是因为，当用户与应用中的功能互动时，您应该会验证相关功能是否具有所需权限。

请求用户停用自动重置功能
如果需要，您可以要求用户阻止系统重置应用的权限。如果用户希望应用主要在后台运行，即使用户不与应用互动应用也能正常工作。

 

 

要在系统设置中将用户定向到您的应用页面，请调用包含Settings.ACTION_APPLICATION_DETAILS_SETTINGS Intent 操作的 Intent，让用户停用权限自动重置功能。

 

确定是否已停用自动重置功能
如需检查是否已针对应用停用自动重置功能，请调用 isAutoRevokeWhitelisted()。如果此方法返回 true，则系统不会自动重置应用的权限。

测试自动重置功能
如需验证系统是否重置了应用的权限，请执行以下操作：

保存系统重置应用权限所需等待的默认时长。这样，您就可以在测试后恢复此设置：

threshold=$(adb shell device_config get permissions \
  auto_revoke_unused_threshold_millis2)
 

减少系统重置权限所需等待的时长。下面的示例对系统进行了修改，以致当您停止与应用互动后仅一秒钟，系统就会重置应用的权限：

adb shell device_config put permissions \
  auto_revoke_unused_threshold_millis2 1000
 

手动调用自动重置进程，如以下代码段所示。在运行此命令之前，请确保测试设备已开启片刻（大约 45 秒钟）。

adb shell cmd jobscheduler run -u 0 -f \
  com.google.android.permissioncontroller 2
 

验证应用能否处理自动重置事件。

恢复系统在自动重置应用权限之前所需等待的默认时长：

adb shell device_config put permissions \
  auto_revoke_unused_threshold_millis2 $threshold
权限对话框的可见性
Android 11 建议不要请求用户已选择拒绝的权限。在应用安装到设备上后，如果用户在使用过程中屡次针对某项特定的权限点按拒绝，此操作表示其希望“不再询问”。
————————————————
版权声明：本文为CSDN博主「飞雨的夏天」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/xiatiandefeiyu/article/details/107130282
```## NVA-2776

```text
M001210  12-02 15:45:32.166   604  7306 I Camera3-Device: disconnectImpl: E
M001211  12-02 15:45:32.166   604  7306 I Camera2ClientBase: Closed Camera 0. Client was: com.hmdglobal.app.cameralite (PID 8986, UID 10145)
M001212  12-02 15:45:32.166   604  7306 I Camera3-Device: disconnectImpl: E
M001213  12-02 15:45:32.166   604  7306 I Camera3DeviceInjectionMethods: injectionDisconnectImpl: Injection camera disconnect
M001214  12-02 15:45:32.173  8986  8986 E CAM_CameraActivity Drea: Camera Exception
M001214  12-02 15:45:32.173  8986  8986 E CAM_CameraActivity Drea: java.lang.RuntimeException: Unimplemented CameraProxy message=103    // STOP_PREVIEW = 103;
M001214  12-02 15:45:32.173  8986  8986 E CAM_CameraActivity Drea:  at com.android.ex.camera2.portability.AndroidCamera2AgentImpl$Camera2Handler.handleMessage(AndroidCamera2AgentImpl.java:665)
M001214  12-02 15:45:32.173  8986  8986 E CAM_CameraActivity Drea:  at com.android.ex.camera2.portability.SprdAndroidCamera2AgentImpl$SprdCamera2Handler.handleMessage(SprdAndroidCamera2AgentImpl.java:719)
M001214  12-02 15:45:32.173  8986  8986 E CAM_CameraActivity Drea:  at android.os.Handler.dispatchMessage(Handler.java:106)
M001214  12-02 15:45:32.173  8986  8986 E CAM_CameraActivity Drea:  at android.os.Looper.loopOnce(Looper.java:201)
M001214  12-02 15:45:32.173  8986  8986 E CAM_CameraActivity Drea:  at android.os.Looper.loop(Looper.java:288)
M001214  12-02 15:45:32.173  8986  8986 E CAM_CameraActivity Drea:  at android.os.HandlerThread.run(HandlerThread.java:67)
M001215  12-02 15:45:32.173  8986  8986 E CAM_CameraActivity Drea: Fatal error during onPause, call Activity.finish()
E001216  12-02 15:45:32.174   857  3214 I wm_finish_activity: [0,5493684,8,com.hmdglobal.app.cameralite/com.android.camera.CameraActivity,app-request]
E001217  12-02 15:45:32.175   857  3214 I wm_destroy_activity: [0,5493684,8,com.hmdglobal.app.cameralite/com.android.camera.CameraActivity,finish-imm:finishIfPossible]
M001218  12-02 15:45:32.177  8986  8986 E zhangqi8888: com.dream.camera.ui.ZoomLineView-->setBoxView()-->42 getX():73.0 xx:207 mWidth:53
S001219  12-02 15:45:32.179   857   905 I ActivityTaskManager: Activity reported stop, but no longer stopping: ActivityRecord{53d3b4 u0 com.hmdglobal.app.cameralite/com.android.camera.CameraActivity t8 f}} DESTROYING
M00121A  12-02 15:45:32.180  8986  8986 I CAM_CameraActivity Drea: onDestroyTasks start!
S00121B  12-02 15:45:32.180   857   905 I UnisocAppMemoryManager: The cached app optimizer is enabled, reclaim skipped
M00121C  12-02 15:45:32.184  8986  8986 I CAM_PhotoModule: destroy
M00121D  12-02 15:45:32.187  8986  8986 I CAM_CameraActivity Drea: onDestroy end!
M00121E  12-02 15:45:32.187  8986 16598 I CAM_CameraActivity Drea: Sound release start
E00121F  12-02 15:45:32.187  8986  8986 I wm_on_destroy_called: [5493684,com.android.camera.CameraActivity,performDestroy]


M001E10  12-02 15:45:55.378  8986  9018 I CAM2PORT_AndCam2AgntImp: AppFW handleMessage - action = 'OPEN_CAMERA'

M001E19  12-02 15:45:55.389  8986 17544 W CAM_CameraActivity Drea: Camera open already: 0,HIST_ID0_302_305_802_204_110_5_711_102_461_462_204_502_303_204_4_1901_203_303_204_103_711_2001_302_305_802_204_110_711_5_102_461_462_204_502_303_204_4_1901_203_303_204_103_2001_711_302_305_802_204_110_5_711_102_461_462_204_502_303_204_4_1901_203_303_204_103_2001_302_711_305_802_204_110_5_711_102_461_462_204_502_303_204_4_1901_203_303_204_103_711_2001_302_305_802_204_110_5_711_102_461_462_204_502_303_204_4_1901_203_303_204_103_302_2001_711_305_802_204_110_5_711_102_461_462_204_502_303_204_204_204_204_204_204_204_204_204_204_204_204_204_302_305_303_204_303_204_4_1901_203_303_204_204_204_204_204_204_204_204_204_303_204_301_302_305_303_204_303_204_204_204_303_204_301_302_305_303_204_303_204_204_204_303_204_301_302_305_303_204_303_204_204_204_204_204_204_204_204_204_204_204_103_2001_302_711_305_802_204_110_5_711_102_461_462_204_502_303_204_204_503_204_702_503_204_702_503_204_702_503_204_702_503_204_702_503_204_702_4_1901_203_303_204_103_302_2001_711_305_802_204_110_5_711_102_461_462_204_502_303_204_503_204_702_503_204_702_503_204_702_503_204_702_503_204_702_503_204_702_802_204_503_204_702_503_204_702_503_204_702_4_1901_203_303_204_103_2001_711_302_305_802_204_110_5_711_102_461_462_204_502_303_204_204_204_204_204_204_204_204_204_204_204_503_204_702_503_204_702_503_204_702_503_204_702_503_204_702_503_204_702_4_1901_203_303_204_103_302_2001_711_305_802_204_110_5_711_102_461_462_204_502_303_204_4_1901_203_303_204_103_711_302_2001_305_802_204_110_302_305_461_462_5_303_204_303_204_711_102_503_204_702_303_204_204_502_303_204_204_204_302_305_802_303_103_711_461_463_2_1_HEND

M001F55  12-02 15:45:55.573  8986  8986 E CAM_FatalErrorHandler: Handling Camera Access Failure:
M001F55  12-02 15:45:55.573  8986  8986 E CAM_FatalErrorHandler: java.lang.Exception
M001F55  12-02 15:45:55.573  8986  8986 E CAM_FatalErrorHandler:  at com.android.camera.FatalErrorHandlerImpl.onGenericCameraAccessFailure(FatalErrorHandlerImpl.java:73)
M001F55  12-02 15:45:55.573  8986  8986 E CAM_FatalErrorHandler:  at com.android.camera.CameraActivity$10.run(CameraActivity.java:660)
M001F55  12-02 15:45:55.573  8986  8986 E CAM_FatalErrorHandler:  at android.os.Handler.handleCallback(Handler.java:938)
M001F55  12-02 15:45:55.573  8986  8986 E CAM_FatalErrorHandler:  at android.os.Handler.dispatchMessage(Handler.java:99)
M001F55  12-02 15:45:55.573  8986  8986 E CAM_FatalErrorHandler:  at android.os.Looper.loopOnce(Looper.java:201)
M001F55  12-02 15:45:55.573  8986  8986 E CAM_FatalErrorHandler:  at android.os.Looper.loop(Looper.java:288)
M001F55  12-02 15:45:55.573  8986  8986 E CAM_FatalErrorHandler:  at android.app.ActivityThread.main(ActivityThread.java:7941)
M001F55  12-02 15:45:55.573  8986  8986 E CAM_FatalErrorHandler:  at java.lang.reflect.Method.invoke(Native Method)
M001F55  12-02 15:45:55.573  8986  8986 E CAM_FatalErrorHandler:  at com.android.internal.os.RuntimeInit$MethodAndArgsCaller.run(RuntimeInit.java:553)
M001F55  12-02 15:45:55.573  8986  8986 E CAM_FatalErrorHandler:  at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:1003)


public void onDeviceOpenedAlready(int cameraId, String info) {
    Log.w(TAG, "Camera open already: " + cameraId + "," + info);
    mMainHandler.post(new Runnable(){
        @Override
        public void run(){
            if (!mPaused) {
                mFatalErrorHandler.onGenericCameraAccessFailure();
            }
        }
    });
}



M043107  12-02 15:50:46.593   604 19092 E Camera3-Device: processBatchCaptureRequests: Transaction error: Status(EX_TRANSACTION_FAILED): 'DEAD_OBJECT: '
M043108  12-02 15:50:46.594   604 19092 E Camera3-Device: Camera 0: sendRequestsBatch: RequestThread: Unable to submit capture request 2243 to HAL device: Broken pipe (-32)
M043109  12-02 15:50:46.596  8986  9018 E CAM2PORT_AndCam2AgntImp: Camera device '0' encountered error code '4'

M001F55  12-02 15:45:55.573  8986  8986 E CAM_FatalErrorHandler: Handling Camera Access Failure:
M001F55  12-02 15:45:55.573  8986  8986 E CAM_FatalErrorHandler: java.lang.Exception
M001F55  12-02 15:45:55.573  8986  8986 E CAM_FatalErrorHandler:  at com.android.camera.FatalErrorHandlerImpl.onGenericCameraAccessFailure(FatalErrorHandlerImpl.java:73)
M001F55  12-02 15:45:55.573  8986  8986 E CAM_FatalErrorHandler:  at com.android.camera.CameraActivity$10.run(CameraActivity.java:660)
M001F55  12-02 15:45:55.573  8986  8986 E CAM_FatalErrorHandler:  at android.os.Handler.handleCallback(Handler.java:938)
M001F55  12-02 15:45:55.573  8986  8986 E CAM_FatalErrorHandler:  at android.os.Handler.dispatchMessage(Handler.java:99)
M001F55  12-02 15:45:55.573  8986  8986 E CAM_FatalErrorHandler:  at android.os.Looper.loopOnce(Looper.java:201)
M001F55  12-02 15:45:55.573  8986  8986 E CAM_FatalErrorHandler:  at android.os.Looper.loop(Looper.java:288)
M001F55  12-02 15:45:55.573  8986  8986 E CAM_FatalErrorHandler:  at android.app.ActivityThread.main(ActivityThread.java:7941)
M001F55  12-02 15:45:55.573  8986  8986 E CAM_FatalErrorHandler:  at java.lang.reflect.Method.invoke(Native Method)
M001F55  12-02 15:45:55.573  8986  8986 E CAM_FatalErrorHandler:  at com.android.internal.os.RuntimeInit$MethodAndArgsCaller.run(RuntimeInit.java:553)
M001F55  12-02 15:45:55.573  8986  8986 E CAM_FatalErrorHandler:  at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:1003)

M001E71  12-02 15:45:55.532   857  5591 W ServiceManager: Permission failure: android.permission.HIGH_SAMPLING_RATE_SENSORS from uid=10145 pid=8986
M001E74  12-02 15:45:55.534  8986  9022 E SensorManager: sensor or listener is null


M001DFF  12-02 15:45:55.376  8986  9023 I CAM_CameraController: requestCamera id=0
M001E00  12-02 15:45:55.376  8986  9023 I CAM_CameraController: mRequestingCameraId = -1 mInfo = com.android.ex.camera2.portability.AndroidCamera2AgentImpl$AndroidCamera2DeviceInfo@3c39737

private static final int EMPTY_REQUEST = -1;

M001E01  12-02 15:45:55.376  8986  9023 I CAM_CameraController: checkAndOpenCamera
```## NVA-2782

```text
M1FAF87  12-02 15:24:20.295  8885  8885 I CAM_PhotoModule: requestCameraOpen mCameraId:0

M1FAF8A  12-02 15:24:20.297  8885  8885 I CAM_CameraController: requestCamera id=0
M1FAF8B  12-02 15:24:20.297  8885  8885 I CAM_CameraController: mRequestingCameraId = -1mInfo = com.android.ex.camera2.portability.AndroidCamera2AgentImpl$AndroidCamera2DeviceInfo@c31677c
M1FAF8C  12-02 15:24:20.298  8885  8885 I CAM_CameraController: checkAndOpenCamera

M1FAF9E  12-02 15:24:20.321  8885  8910 W CAM_CameraActivity Drea: Camera open already: 0,HIST_ID0_711_461_463_2_1_302_305_204_101_711_461_462_204_102_204_502_303_204_302_305_303_111_711_461_463_2_1_302_305_204_101_711_102_461_462_204_502_303_204_302_305_303_111_711_461_463_2_1_302_305_204_101_711_461_462_102_204_502_303_204_302_305_303_111_711_461_463_2_1_302_305_802_204_106_711_102_204_461_462_204_502_303_204_503_204_702_503_204_702_103_302_305_802_461_463_711_303_3_461_462_204_502_502_303_204_503_302_305_204_106_102_204_204_303_204_103_302_305_461_463_303_3_502_502_303_204_302_305_503_106_102_204_303_204_103_302_305_461_463_303_3_461_462_204_502_502_303_204_302_305_503_204_106_102_204_204_303_204_103_302_305_461_463_303_3_302_305_802_204_106_711_102_461_462_204_204_502_303_204_103_302_305_802_461_463_711_303_3_302_305_204_101_109_711_102_461_462_204_204_502_303_204_204_111_711_302_305_303_461_463_3_302_305_802_204_106_711_461_462_102_204_204_502_303_204_103_302_305_802_461_463_303_711_3_302_305_204_101_109_711_461_462_102_204_204_502_303_204_204_111_711_302_305_303_461_463_3_302_305_802_204_106_711_461_462_102_204_204_502_303_204_204_103_302_305_802_461_463_711_303_3_461_462_204_502_502_303_204_503_302_305_204_106_102_204_204_303_204_103_302_305_461_463_303_3_502_502_303_204_302_305_503_106_102_204_303_204_103_302_305_461_463_303_3_461_462_204_502_502_303_204_503_302_305_204_106_102_204_204_303_204_103_302_305_461_463_303_3_302_305_802_204_106_711_102_461_462_204_204_502_303_204_103_302_305_802_461_463_711_303_3_302_305_204_101_109_711_102_461_462_204_204_502_303_204_204_204_204_204_204_204_302_305_303_111_711_461_463_2_1_HEND

M1FB002  12-02 15:24:20.683  8885  8885 E CAM_FatalErrorHandler: Handling Camera Access Failure:
M1FB002  12-02 15:24:20.683  8885  8885 E CAM_FatalErrorHandler: java.lang.Exception
M1FB002  12-02 15:24:20.683  8885  8885 E CAM_FatalErrorHandler:  at com.android.camera.FatalErrorHandlerImpl.onGenericCameraAccessFailure(FatalErrorHandlerImpl.java:73)
M1FB002  12-02 15:24:20.683  8885  8885 E CAM_FatalErrorHandler:  at com.android.camera.CameraActivity$10.run(CameraActivity.java:660)
M1FB002  12-02 15:24:20.683  8885  8885 E CAM_FatalErrorHandler:  at android.os.Handler.handleCallback(Handler.java:938)
M1FB002  12-02 15:24:20.683  8885  8885 E CAM_FatalErrorHandler:  at android.os.Handler.dispatchMessage(Handler.java:99)
M1FB002  12-02 15:24:20.683  8885  8885 E CAM_FatalErrorHandler:  at android.os.Looper.loopOnce(Looper.java:201)
M1FB002  12-02 15:24:20.683  8885  8885 E CAM_FatalErrorHandler:  at android.os.Looper.loop(Looper.java:288)
M1FB002  12-02 15:24:20.683  8885  8885 E CAM_FatalErrorHandler:  at android.app.ActivityThread.main(ActivityThread.java:7941)
M1FB002  12-02 15:24:20.683  8885  8885 E CAM_FatalErrorHandler:  at java.lang.reflect.Method.invoke(Native Method)
M1FB002  12-02 15:24:20.683  8885  8885 E CAM_FatalErrorHandler:  at com.android.internal.os.RuntimeInit$MethodAndArgsCaller.run(RuntimeInit.java:553)
M1FB002  12-02 15:24:20.683  8885  8885 E CAM_FatalErrorHandler:  at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:1003)



./002-0101_080007--1202_143807_poweron/0-android.log:M02B128  12-02 14:00:44.338   662  8646 E Camera3-Device: RequestThread: Can't get output buffer, skipping request: Broken pipe (-32)
./002-0101_080007--1202_143807_poweron/M02B128  12-02 14:00:44.338   662  8646 E Camera3-Device: RequestThread: Can't get output buffer, skipping request: Broken pipe (-32)

最终发现好像是 SPRD 的patch修改引起的 mem 问题
```## NVA-2813 出现短暂性卡死现象,后又恢复

```text
从视频中看出现问题的时间点在 15:45-15:46 之间

M2A13FA  12-05 15:45:56.124  5523  5523 E CAM_CameraAppUI Dream: can not set when camera is focusing

M2A19CA  12-05 15:45:59.204   853   989 I InputDispatcher: Dropping event because there is no touchable window or gesture monitor at (595, 1326) in display 0.

./M2A1A7E  12-05 15:45:59.490   480   480 W DPUModule: Warning: Dispc cannot support 7 layer blending(0)
./M2A1A87  12-05 15:45:59.507   480   480 W DPUModule: Warning: Dispc cannot support 8 layer blending(0)
./M2A1A8E  12-05 15:45:59.527   480   480 W DPUModule: Warning: Dispc cannot support 8 layer blending(0)
./M2A1A93  12-05 15:45:59.545   480   480 W DPUModule: Warning: Dispc cannot support 9 layer blending(0)
./M2A1A96  12-05 15:45:59.560   480   480 W DPUModule: Warning: Dispc cannot support 9 layer blending(0)
./M2A1A98  12-05 15:45:59.575   480   480 W DPUModule: Warning: Dispc cannot support 9 layer blending(0)
./M2A1A9A  12-05 15:45:59.589   480   480 W DPUModule: Warning: Dispc cannot support 9 layer blending(0)
./M2A1A9C  12-05 15:45:59.602   480   480 W DPUModule: Warning: Dispc cannot support 9 layer blending(0)
./M2A1A9E  12-05 15:45:59.616   480   480 W DPUModule: Warning: Dispc cannot support 9 layer blending(0)
./M2A1AA0  12-05 15:45:59.632   480   480 W DPUModule: Warning: Dispc cannot support 9 layer blending(0)
./M2A1AA2  12-05 15:45:59.648   480   480 W DPUModule: Warning: Dispc cannot support 9 layer blending(0)
./M2A1AA5  12-05 15:45:59.665   480   480 W DPUModule: Warning: Dispc cannot support 9 layer blending(0)
./M2A1AA7  12-05 15:45:59.682   480   480 W DPUModule: Warning: Dispc cannot support 9 layer blending(0)
./M2A1AA9  12-05 15:45:59.699   480   480 W DPUModule: Warning: Dispc cannot support 9 layer blending(0)
./M2A1AAC  12-05 15:45:59.717   480   480 W DPUModule: Warning: Dispc cannot support 9 layer blending(0)
./M2A1AAF  12-05 15:45:59.734   480   480 W DPUModule: Warning: Dispc cannot support 9 layer blending(0)
./M2A1AB1  12-05 15:45:59.751   480   480 W DPUModule: Warning: Dispc cannot support 9 layer blending(0)
./M2A1AB3  12-05 15:45:59.766   480   480 W DPUModule: Warning: Dispc cannot support 9 layer blending(0)
./M2A1AB5  12-05 15:45:59.782   480   480 W DPUModule: Warning: Dispc cannot support 9 layer blending(0)
./M2A1AB7  12-05 15:45:59.798   480   480 W DPUModule: Warning: Dispc cannot support 9 layer blending(0)
./M2A1ABA  12-05 15:45:59.815   480   480 W DPUModule: Warning: Dispc cannot support 9 layer blending(0)
./M2A1AC2  12-05 15:45:59.834   480   480 W DPUModule: Warning: Dispc cannot support 9 layer blending(0)
./M2A212D  12-05 15:46:07.549   480   480 W DPUModule: Warning: Dispc cannot support 8 layer blending(0)
./M2A216A  12-05 15:46:07.567   480   480 W DPUModule: Warning: Dispc cannot support 7 layer blending(0)
./M2A21A0  12-05 15:46:07.582   480   480 W DPUModule: Warning: Dispc cannot support 7 layer blending(0)
./M2A231A  12-05 15:46:07.764   480   480 W DPUModule: Warning: Dispc cannot support 7 layer blending(0)
./M2A2323  12-05 15:46:07.782   480   480 W DPUModule: Warning: Dispc cannot support 7 layer blending(0)
./M2A232A  12-05 15:46:07.801   480   480 W DPUModule: Warning: Dispc cannot support 7 layer blending(0)
./M2A232F  12-05 15:46:07.815   480   480 W DPUModule: Warning: Dispc cannot support 7 layer blending(0)
./M2A2335  12-05 15:46:07.831   480   480 W DPUModule: Warning: Dispc cannot support 7 layer blending(0)
./M2A233B  12-05 15:46:07.847   480   480 W DPUModule: Warning: Dispc cannot support 7 layer blending(0)
./M2A2376  12-05 15:46:07.865   480   480 W DPUModule: Warning: Dispc cannot support 7 layer blending(0)
./M2A23A7  12-05 15:46:07.884   480   480 W DPUModule: Warning: Dispc cannot support 7 layer blending(0)
./M2A23BB  12-05 15:46:07.900   480   480 W DPUModule: Warning: Dispc cannot support 7 layer blending(0)
./M2A23C1  12-05 15:46:07.915   480   480 W DPUModule: Warning: Dispc cannot support 7 layer blending(0)
./M2A23C6  12-05 15:46:07.944   480   480 W DPUModule: Warning: Dispc cannot support 7 layer blending(0)
./M2A23CF  12-05 15:46:07.967   480   480 W DPUModule: Warning: Dispc cannot support 7 layer blending(0)
./M2A23D6  12-05 15:46:07.982   480   480 W DPUModule: Warning: Dispc cannot support 7 layer blending(0)
./M2A23D8  12-05 15:46:07.994   480   480 W DPUModule: Warning: Dispc cannot support 7 layer blending(0)
./M2A23DB  12-05 15:46:08.011   480   480 W DPUModule: Warning: Dispc cannot support 7 layer blending(0)
./M2A23DE  12-05 15:46:08.027   480   480 W DPUModule: Warning: Dispc cannot support 7 layer blending(0)
./M2A23E1  12-05 15:46:08.044   480   480 W DPUModule: Warning: Dispc cannot support 7 layer blending(0)
./M2A23E4  12-05 15:46:08.061   480   480 W DPUModule: Warning: Dispc cannot support 7 layer blending(0)
./M2A23E7  12-05 15:46:08.077   480   480 W DPUModule: Warning: Dispc cannot support 7 layer blending(0)
./M2A23EE  12-05 15:46:08.094   480   480 W DPUModule: Warning: Dispc cannot support 7 layer blending(0)
./M2A2405  12-05 15:46:08.116   480   480 W DPUModule: Warning: Dispc cannot support 7 layer blending(0)
./M2A2407  12-05 15:46:08.129   480   480 W DPUModule: Warning: Dispc cannot support 7 layer blending(0)
./M2A240B  12-05 15:46:08.144   480   480 W DPUModule: Warning: Dispc cannot support 7 layer blending(0)
./M2A2417  12-05 15:46:08.160   480   480 W DPUModule: Warning: Dispc cannot support 7 layer blending(0)
./M2A241A  12-05 15:46:08.177   480   480 W DPUModule: Warning: Dispc cannot support 7 layer blending(0)
./M2A2422  12-05 15:46:08.194   480   480 W DPUModule: Warning: Dispc cannot support 7 layer blending(0)
./M2A2428  12-05 15:46:08.210   480   480 W DPUModule: Warning: Dispc cannot support 7 layer blending(0)
./M2A242B  12-05 15:46:08.227   480   480 W DPUModule: Warning: Dispc cannot support 7 layer blending(0)
./M2A242E  12-05 15:46:08.243   480   480 W DPUModule: Warning: Dispc cannot support 7 layer blending(0)
./M2A2439  12-05 15:46:08.260   480   480 W DPUModule: Warning: Dispc cannot support 7 layer blending(0)
./M2A243C  12-05 15:46:08.277   480   480 W DPUModule: Warning: Dispc cannot support 7 layer blending(0)
./M2A2443  12-05 15:46:08.293   480   480 W DPUModule: Warning: Dispc cannot support 7 layer blending(0)
./M2A244A  12-05 15:46:08.311   480   480 W DPUModule: Warning: Dispc cannot support 7 layer blending(0)
./M2A244D  12-05 15:46:08.327   480   480 W DPUModule: Warning: Dispc cannot support 7 layer blending(0)
./M2A2450  12-05 15:46:08.343   480   480 W DPUModule: Warning: Dispc cannot support 7 layer blending(0)
./M2A245A  12-05 15:46:08.360   480   480 W DPUModule: Warning: Dispc cannot support 7 layer blending(0)
./M2A245D  12-05 15:46:08.376   480   480 W DPUModule: Warning: Dispc cannot support 7 layer blending(0)
./M2A2469  12-05 15:46:08.410   480   480 W DPUModule: Warning: Dispc cannot support 7 layer blending(0)
./M2A246C  12-05 15:46:08.426   480   480 W DPUModule: Warning: Dispc cannot support 7 layer blending(0)
./M2A246F  12-05 15:46:08.443   480   480 W DPUModule: Warning: Dispc cannot support 7 layer blending(0)
./M2A2479  12-05 15:46:08.460   480   480 W DPUModule: Warning: Dispc cannot support 7 layer blending(0)
./M2A247B  12-05 15:46:08.476   480   480 W DPUModule: Warning: Dispc cannot support 7 layer blending(0)
./M2A2485  12-05 15:46:08.510   480   480 W DPUModule: Warning: Dispc cannot support 7 layer blending(0)
./M2A2491  12-05 15:46:08.609   480   480 W DPUModule: Warning: Dispc cannot support 7 layer blending(0)
./M2A249D  12-05 15:46:08.709   480   480 W DPUModule: Warning: Dispc cannot support 7 layer blending(0)
./M2A24A9  12-05 15:46:08.809   480   480 W DPUModule: Warning: Dispc cannot support 7 layer blending(0)
./M2A24B5  12-05 15:46:08.909   480   480 W DPUModule: Warning: Dispc cannot support 7 layer blending(0)
./M2A267C  12-05 15:46:09.212   480   480 W DPUModule: Warning: Dispc cannot support 7 layer blending(0)

可能是 fast.thumb 功能引起的
```## 

```text
M05B091  12-08 10:11:21.178   389 16516 E cmr_prev: 10448, prev_pop_preview_buffer: got wrong buf: data->fd=0x22, prev_frm[0].fd=0x21, valid_num=6
M05B092  12-08 10:11:21.178   389 16516 E cmr_prev: 2846, prev_preview_frame_handle: pop frm 0x1 err
M05B093  12-08 10:11:21.179   389 16528 E Cam3OEMIf: 5465, HandleStartPreview: SprdCamera3OEMIf::camera_cb: @CAMERA_EXIT_CB_FAILURE(0x0) in state SPRD_PREVIEW_IN_PROGRESS.
M05B094  12-08 10:11:21.179   389 16528 E Cam3OEMIf: 2548, checkPreviewStateForCapture: incorrect preview status 2 of ZSL capture mode
M05B095  12-08 10:11:21.179   389 16528 E Cam3OEMIf: 5335, receiveCameraExitError: drop current cameraExit msg

M05B0A1  12-08 10:11:21.262   389 16516 E cmr_prev: 10448, prev_pop_preview_buffer: got wrong buf: data->fd=0x23, prev_frm[0].fd=0x21, valid_num=6
M05B0A2  12-08 10:11:21.263   389 16516 E cmr_prev: 2846, prev_preview_frame_handle: pop frm 0x1 err
M05B0A4  12-08 10:11:21.264   389 16528 E Cam3OEMIf: 5465, HandleStartPreview: SprdCamera3OEMIf::camera_cb: @CAMERA_EXIT_CB_FAILURE(0x0) in state SPRD_ERROR.
M05B0A5  12-08 10:11:21.265   389 16528 E Cam3OEMIf: 2548, checkPreviewStateForCapture: incorrect preview status 2 of ZSL capture mode
M05B0A6  12-08 10:11:21.266   389 16528 E Cam3OEMIf: 5335, receiveCameraExitError: drop current cameraExit msg


M05BA06  12-08 10:11:30.487   389   638 E Cam3HWI : 1726, processCaptureRequest: TimeOut pendingCount=5001
M05BA07  12-08 10:11:30.487   389   638 I Cam3HWI : 1046, flushRequest: :hal3: E
M05BA08  12-08 10:11:30.487   389   638 E Cam3HWI : 1067, flushRequest: iommu_workaround: unmap 0x10 size 0x71000 sg 0xce6cc100
M05BA09  12-08 10:11:30.487   389   638 E Cam3HWI : 1067, flushRequest: iommu_workaround: unmap 0x1e size 0x71000 sg 0xe39e3100
M05BA0A  12-08 10:11:30.487   389   638 E Cam3HWI : 1067, flushRequest: iommu_workaround: unmap 0x1f size 0x71000 sg 0xe39e3d00
M05BA0B  12-08 10:11:30.487   389   638 E Cam3HWI : 1067, flushRequest: iommu_workaround: unmap 0x20 size 0x71000 sg 0xe39e3d80
M05BA0C  12-08 10:11:30.487   389   638 E Cam3HWI : 1067, flushRequest: iommu_workaround: unmap 0x21 size 0x71000 sg 0xe6b6fb00
M05BA0D  12-08 10:11:30.487   389   638 E Cam3HWI : 1067, flushRequest: iommu_workaround: unmap 0x22 size 0x71000 sg 0xe3b7e780
M05BA0E  12-08 10:11:30.487   389   638 I cmr_focus: 1144, af_quit: autofocus is IDLE direct return!
M05BA0F  12-08 10:11:30.487   389   638 I OEMCam  : 191, camera_cancel_autofocus: done
M05BA10  12-08 10:11:30.488   389   638 I Cam3OEMIf: 714, stop: channel_type = 1, frame_number = 6067
M05BA11  12-08 10:11:30.488   475 16543 I CameraProviderManager: Camera device device@3.3/legacy/0 torch status is now AVAILABLE_OFF
M05BA12  12-08 10:11:30.488   475 16543 E CameraProviderManager: removeRef: Asked to remove reference for camera 0, but no reference to it was found. This could mean removeRef was called twice for the same camera ID.
M05BA13  12-08 10:11:30.488   475 16543 I CameraService: onTorchStatusChangedLocked: Torch status changed for cameraId=0, newStatus=1
M05BA14  12-08 10:11:30.488   389   638 I Cam3OEMIf: 3569, stopPreviewInternal: E camera id 0
M05BA15  12-08 10:11:30.488   389   638 I Cam3OEMIf: 745, stop: X
M05BA16  12-08 10:11:30.488   389   638 I Cam3OEMIf: 714, stop: channel_type = 2, frame_number = 6067
M05BA17  12-08 10:11:30.488   389   638 W Cam3OEMIf: 3694, cancelPictureInternal: not taking a picture (state SPRD_IDLE)
M05BA18  12-08 10:11:30.488   389   638 I Cam3OEMIf: 745, stop: X


M05BA42  12-08 10:11:30.577 16397 16423 W CAM_CameraActivity Drea: Camera open failure: HIST_ID0_204_5_103_302_305_461_463_303_3_302_305_802_204_106_711_102_204_204_204_461_462_204_502_303_204_503_204_601_503_204_601_503_204_601_103_302_305_802_805_711_303_461_463_3_302_305_204_711_106_102_204_461_462_204_502_303_204_503_204_601_204_204_103_711_302_305_802_805_303_461_463_3_461_462_204_502_101_109_102_461_463_204_461_462_204_103_461_463_3_302_305_204_711_106_102_204_461_462_204_502_303_204_503_204_601_503_204_601_503_204_601_103_711_302_305_802_805_303_461_463_3_302_305_802_204_106_711_102_204_204_461_462_204_204_502_303_204_503_204_601_503_204_601_103_711_302_305_802_805_461_463_303_3_502_502_303_204_302_305_503_903_106_102_461_463_204_204_303_204_503_4_901_203_303_204_904_303_204_5_103_302_305_303_461_463_3_502_502_303_204_302_305_503_903_106_461_463_102_204_204_303_204_503_4_901_203_303_204_904_303_204_5_103_302_305_461_463_303_3_302_305_802_204_711_106_102_204_204_461_462_204_204_502_303_204_503_204_601_461_462_103_711_302_305_802_805_303_461_463_3_502_502_303_204_503_302_305_903_106_461_463_102_204_204_303_204_103_302_303_305_461_463_3_502_502_303_204_302_503_305_903_106_461_463_102_204_204_303_204_103_302_305_303_461_463_3_302_305_802_204_106_711_102_204_204_204_461_462_204_502_303_204_103_302_711_305_802_805_303_461_463_3_302_305_204_106_711_102_204_461_462_204_502_303_204_103_711_302_305_802_805_303_461_463_3_302_305_802_204_106_711_102_204_204_204_461_462_204_502_303_204_204_204_204_204_204_204_204_204_204_204_204_204_204_204_204_204_103_711_302_305_802_805_461_463_303_3_302_305_204_711_106_102_204_461_462_204_502_303_204_HEND
M05BA43  12-08 10:11:30.579 16397 16397 E CAM_FatalErrorHandler: Handling Camera Open Failure:
M05BA43  12-08 10:11:30.579 16397 16397 E CAM_FatalErrorHandler: java.lang.Exception
M05BA43  12-08 10:11:30.579 16397 16397 E CAM_FatalErrorHandler:  at com.android.camera.FatalErrorHandlerImpl.onCameraOpenFailure(FatalErrorHandlerImpl.java:49)
M05BA43  12-08 10:11:30.579 16397 16397 E CAM_FatalErrorHandler:  at com.android.camera.CameraActivity$9.run(CameraActivity.java:611)
M05BA43  12-08 10:11:30.579 16397 16397 E CAM_FatalErrorHandler:  at android.os.Handler.handleCallback(Handler.java:938)
M05BA43  12-08 10:11:30.579 16397 16397 E CAM_FatalErrorHandler:  at android.os.Handler.dispatchMessage(Handler.java:99)
M05BA43  12-08 10:11:30.579 16397 16397 E CAM_FatalErrorHandler:  at android.os.Looper.loopOnce(Looper.java:201)
M05BA43  12-08 10:11:30.579 16397 16397 E CAM_FatalErrorHandler:  at android.os.Looper.loop(Looper.java:288)
M05BA43  12-08 10:11:30.579 16397 16397 E CAM_FatalErrorHandler:  at android.app.ActivityThread.main(ActivityThread.java:7941)
M05BA43  12-08 10:11:30.579 16397 16397 E CAM_FatalErrorHandler:  at java.lang.reflect.Method.invoke(Native Method)
M05BA43  12-08 10:11:30.579 16397 16397 E CAM_FatalErrorHandler:  at com.android.internal.os.RuntimeInit$MethodAndArgsCaller.run(RuntimeInit.java:553)
M05BA43  12-08 10:11:30.579 16397 16397 E CAM_FatalErrorHandler:  at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:1003)

M05BA45  12-08 10:11:30.581 16397 16397 E CAM_CameraUtil: Show fatal error dialog

M05CC2F  12-08 10:11:47.836 16397 16397 E CAM_CameraActivity Drea: Camera Exception
M05CC2F  12-08 10:11:47.836 16397 16397 E CAM_CameraActivity Drea: java.lang.RuntimeException: Unimplemented CameraProxy message=103
M05CC2F  12-08 10:11:47.836 16397 16397 E CAM_CameraActivity Drea:  at com.android.ex.camera2.portability.AndroidCamera2AgentImpl$Camera2Handler.handleMessage(AndroidCamera2AgentImpl.java:577)
M05CC2F  12-08 10:11:47.836 16397 16397 E CAM_CameraActivity Drea:  at com.android.ex.camera2.portability.SprdAndroidCamera2AgentImpl$SprdCamera2Handler.handleMessage(SprdAndroidCamera2AgentImpl.java:715)
M05CC2F  12-08 10:11:47.836 16397 16397 E CAM_CameraActivity Drea:  at android.os.Handler.dispatchMessage(Handler.java:106)
M05CC2F  12-08 10:11:47.836 16397 16397 E CAM_CameraActivity Drea:  at android.os.Looper.loopOnce(Looper.java:201)
M05CC2F  12-08 10:11:47.836 16397 16397 E CAM_CameraActivity Drea:  at android.os.Looper.loop(Looper.java:288)
M05CC2F  12-08 10:11:47.836 16397 16397 E CAM_CameraActivity Drea:  at android.os.HandlerThread.run(HandlerThread.java:67)
M05CC30  12-08 10:11:47.837 16397 16397 E CAM_FatalErrorHandler: Handling Fatal Error:
M05CC30  12-08 10:11:47.837 16397 16397 E CAM_FatalErrorHandler: java.lang.Exception
M05CC30  12-08 10:11:47.837 16397 16397 E CAM_FatalErrorHandler:  at com.android.camera.FatalErrorHandlerImpl.handleFatalError(FatalErrorHandlerImpl.java:117)
M05CC30  12-08 10:11:47.837 16397 16397 E CAM_FatalErrorHandler:  at com.android.camera.CameraActivity$16.onFatalError(CameraActivity.java:1061)
M05CC30  12-08 10:11:47.837 16397 16397 E CAM_FatalErrorHandler:  at com.android.camera.CameraActivity$16.onCameraException(CameraActivity.java:1040)
M05CC30  12-08 10:11:47.837 16397 16397 E CAM_FatalErrorHandler:  at com.android.ex.camera2.portability.CameraExceptionHandler$3.run(CameraExceptionHandler.java:103)
M05CC30  12-08 10:11:47.837 16397 16397 E CAM_FatalErrorHandler:  at android.os.Handler.handleCallback(Handler.java:938)
M05CC30  12-08 10:11:47.837 16397 16397 E CAM_FatalErrorHandler:  at android.os.Handler.dispatchMessage(Handler.java:99)
M05CC30  12-08 10:11:47.837 16397 16397 E CAM_FatalErrorHandler:  at android.os.Looper.loopOnce(Looper.java:201)
M05CC30  12-08 10:11:47.837 16397 16397 E CAM_FatalErrorHandler:  at android.os.Looper.loop(Looper.java:288)
M05CC30  12-08 10:11:47.837 16397 16397 E CAM_FatalErrorHandler:  at android.app.ActivityThread.main(ActivityThread.java:7941)
M05CC30  12-08 10:11:47.837 16397 16397 E CAM_FatalErrorHandler:  at java.lang.reflect.Method.invoke(Native Method)
M05CC30  12-08 10:11:47.837 16397 16397 E CAM_FatalErrorHandler:  at com.android.internal.os.RuntimeInit$MethodAndArgsCaller.run(RuntimeInit.java:553)
M05CC30  12-08 10:11:47.837 16397 16397 E CAM_FatalErrorHandler:  at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:1003)
```## NVA-2866

```text
M00C3EE  12-07 22:54:41.758 29866 29900 E HMDPortraitPhotoModule: Time:2022_11_21_11_19_06-->com.dream.camera.modules.portraitphoto.HMDPortraitPhotoModule$1-->run()-->159 cost:3886
M00FAA6  12-07 22:54:54.194 29866 29903 E HMDPortraitPhotoModule: Time:2022_11_21_11_19_06-->com.dream.camera.modules.portraitphoto.HMDPortraitPhotoModule$1-->run()-->159 cost:3221
M01103F  12-07 22:54:58.151 29866 29904 E HMDPortraitPhotoModule: Time:2022_11_21_11_19_06-->com.dream.camera.modules.portraitphoto.HMDPortraitPhotoModule$1-->run()-->159 cost:3028
M012820  12-07 22:55:02.881 29866 29924 E HMDPortraitPhotoModule: Time:2022_11_21_11_19_06-->com.dream.camera.modules.portraitphoto.HMDPortraitPhotoModule$1-->run()-->159 cost:2896

It takes about 3 seconds to process a Potrait picture, and I have ask the Portrait Algorithm provider, they said there is no optimize space because of the platform limition.
```## 刷了GSI之后前摄打开黑的或白的

```text
10-21 15:27:39.294   450 13976 I Cam3OEMIf: 3706, startPreviewInternal: E camera id 1
10-21 15:27:39.294   450 13976 I Cam3OEMIf: 3822, startPreviewInternal: mTopAppId is -2
10-21 15:27:39.348   450 13976 I Cam3OEMIf: 4006, startPreviewInternal: X CamId=1 TotalIonSize=425984 TotalGpuSize=0, total_size 425984
10-21 15:27:43.405   450   754 I Cam3OEMIf: 3706, startPreviewInternal: E camera id 0
10-21 15:27:43.405   450   754 I Cam3OEMIf: 3822, startPreviewInternal: mTopAppId is -2
10-21 15:27:43.528   450   754 I Cam3OEMIf: 4006, startPreviewInternal: X CamId=0 TotalIonSize=2023424 TotalGpuSize=0, total_size 2023424

10-21 15:19:43.431   450   755 E CamComm1.0-MD: Mismatched tag type when updating entry eisZoom (-2147483620) of type int32; got type byte data instead 
```## 设置 persist.vendor.cam.raw.mode 之后卡死或拍照绿屏

## JPEG文件格式

```text
https://blog.csdn.net/wllw7176/article/details/115577735
```## 大光圈

```text
与人像模式相比,只保留 HDR 和光圈调节功能(默认下发开启光圈功能) ,对人对物都可以虚化
```## 170144 5901Condor camera error

```text
SPCSS01094080

Dear Cus
  预览buffer fd=0x21设置下去后一直没有pop回来fd=0x21 ,hal有fd匹配的逻辑,匹配不成功会直接return.导致此问题是因为预览queue的读写指针撞到一起了，此修改是底层预览queue添加读写保护锁，不会有其他影响及风险,thanks
(20221213T01:59:34)
```## SPRD两种 debug 参数 metadata 的手段:

```text
1、 通过命令 adb shell dumpsys media.camera > dump.txt 检查所有底层的配置能力列表
2、 通过 log 查看 hal 是否接受到参数:
12-28 10:30:52.661 452 7624 D Cam3Setting: 5809, updateWorkParameters: mCameraId=0,
focus_distance=1033.333374, ae_precap_trigger= 0, isFaceBeautyOn=0, eis=0, flash_mode=0, ae_lock=0,
scene_mode=0, cap_mode=1, cap_cnt=0, iso=0, jpeg orien=0, zsl=1, 3dcali=0, crop 0 0 3264 2448
cropRegionUpdate=0, am_mode=1, updateAE=0, ae_regions: 0 0 0 0 0, af_trigger=0, af_mode=4, af_state=0,
af_region: 0 0 0 0 0, sprd_auto_3dnr_enable:1, android zsl enable = 0,is_smile_capture=0 sprd_3dnr_enabled:0
```## 闪光灯参数下发 : app 下发了 FLASH_MODE 为 ON,但是拍照闪光灯不闪

```text
Debug 方法:通过 logcat 抓取关键字 updateWorkParameters | flash_mode
01-08 15:55:07.010 452 910 D Cam3Setting: 5809, updateWorkParameters: mCameraId=0,
focus_distance=0.000000, ae_precap_trigger= 0, isFaceBeautyOn=1, eis=0, flash_mode=0, ae_lock=0,
scene_mode=0, cap_mode=1, cap_cnt=0, iso=0, jpeg orien=90, zsl=1, 3dcali=0, crop 0 0 6528 4896
cropRegionUpdate=0, am_mode=1, updateAE=0, ae_regions: 0 0 0 0 0, af_trigger=0, af_mode=4, af_state=2,
af_region: 0 0 0 0 0, sprd_auto_3dnr_enable:2, android zsl enable = 0,is_smile_capture=0 sprd_3dnr_enabled:0
分析:app 下发参数不成功,需要检查 app 侧是否使用 setRepeatingRequest/capture 接口成功下发参数
```## 自动夜景增强使能

```text
现象:下发了 ANDROID_SPRD_AUTO_3DNR_ENABLED 的 tag 为 1,但是拍照没有效果
Debug 方法:通过 logcat 抓取关键字 updateWorkParameters | sprd_auto_3dnr_enable | sprd_3dnr_enabled
```## 调节 ev 值没有效果

```text
现象:自动模式下,通过设置谷歌官方 tag : CONTROL_AE_EXPOSURE_COMPENSATION，画面没有明暗变化的效果,或者画面的变化效果不符合预期。
Debug 方法:通过 logcat 抓取关键字 ae_exposure_compensation | ae_lock
分析:ae_exposure_compensation=5 代表值下发成功,但是 ae_lock=0,此时 ae 未锁定,在自动模式下如需调节 ev 值,需要将 ae 锁定再进行调节,并且注意不能在 lock = 0 的时候下发 ev 值(除了 ev=0) 。
```## Camera性能分析

```text
Camera 启动类耗时分解表
A: InputReader: processEventsLocked             -> CAM_CameraController: checkAndOpenCamera
B: CAM_CameraController: checkAndOpenCamera     -> openCamera: :hal3: E
C: openCamera: :hal3: E                         -> openCamera: :hal3: X                         //Open Camera 耗时
D: openCamera: :hal3: X                         -> configureStreams: E
E: configureStreams: E                          -> configureStreams: X                          //配流耗时
F: configureStreams: mMultiCameraMode           -> startPreviewInternal: E
G: startPreviewInternal: E                      -> startPreviewInternal: X                      //启动预览耗时
H: startPreviewInternal: X                      -> hideImageCover                               //收到第一帧

adb logcat | grep -E "InputReader: processEventsLocked|checkAndOpenCamera|openCamera: :hal3: E|openCamera: :hal3: X|configureStreams: E|configureStreams: X|configureStreams: mMultiCameraMode|startPreviewInternal: E|startPreviewInternal: X|hideImageCover"

Camera 切换类耗时分解表
A: InputReader: processEventsLocked             -> action = 'STOP_PREVIEW'                      //APP耗时
B: action = 'STOP_PREVIEW'                      -> flush: :hal3: E
C: flush: :hal3: E                              -> stopPreviewInternal: E
D: stopPreviewInternal: E                       -> sensor_stream_off: E                         //关闭预览耗时
 : sensor_stream_off: E                         -> sensor_stream_off: X
 : sensor_stream_off: X                         -> stopPreviewInternal: X
E: stopPreviewInternal: X                       -> flush: :hal3: X
F: flush: :hal3: X                              -> startPreviewInternal: E
G: startPreviewInternal: E                      -> sensor_stream_on: E                          //启动预览耗时
 : sensor_stream_on: E                          -> sensor_stream_on: X
 : sensor_stream_on: X                          -> startPreviewInternal: X
H: startPreviewInternal: X                      -> hideImageCover                               //收到第一帧


抓取 Systrace
python external/chromium-trace/systrace.py --time=5 -o file.html gfx input view hal res dalvik sched freq idle mmc disk workq sync
```## 171955

```text
步骤：
1.进入CameraApp
2.切换到前摄
3.查看预览界面
现象：
预览界面黑屏，拍出来的照片也是全黑的
分析：
安装第三方CameraApp也有此问题，感觉应该不是DreamCamera2的问题，从log中看打开camera的流程都是正常的，应该是hal回图的时候就出现了问题，请帮忙看一下，谢谢！
```## TODO : 梳理一下 DreamCaptureLayoutHelper 的布局流程

```text
// TopPanel 的高度
topHeight = mActivity.getResources().getDimensionPixelSize(R.dimen.top_panel_height);

// 屏幕长边
int longerEdge = Math.max(width, height);

// 屏幕短边
int shorterEdge = Math.min(width, height);

// 导航栏的高度
int navgH = navgEnable ? CameraUtil.getNormalNavigationBarHeight() : 0;

// 除预览部分之外的剩余长度
float remainingSpaceAlongLongerForCommon = longerEdge - shorterEdge * 4 / 3;

// bottomBar的高度
float barSize = remainingSpaceAlongLongerForCommon - topHeight - navgH;

// BottomBar 的 layout (全屏)
config.mBottomBarRect.set(0, height - barSize - navgH, width, height - navgH);

// BottomBar 的 layout (16：9)
config.mBottomBarRect.set(0, bottom - barSize, width, bottom);

// BottomBar 的 layout (1：1)
config.mBottomBarRect.set(0, longerEdge - barSize - navgH, shorterEdge, longerEdge - navgH);

// BottomBar 的 layout (4：3)
config.mBottomBarRect.set(0, longerEdge - barSize - navgH, shorterEdge, longerEdge - navgH);
```## Sensor Flicker(banding)

```text
https://mp.weixin.qq.com/s?__biz=MzA3ODMzMTM1NA==&mid=2247485346&idx=1&sn=0b36287a0b9494bc6ddc4a0769a5cbaa&chksm=9f452b17a832a20104c28940f05e898ea14fc2f23f4234c82a45dc13ee7de8ab396b83c87903&scene=178&cur_album_id=1713304865096925188#rd
```## Android Camera2 对焦梳理

```text
https://mp.weixin.qq.com/s?__biz=MzA3ODMzMTM1NA==&mid=2247484802&idx=1&sn=fc65fc63cff16bb6cfca0bf05a4d6bda&chksm=9f452937a832a0213c45cf364a20e77b9ddd6149c64ccd423b09fb7c12726fd86c8221971c26&scene=178&cur_album_id=1713304865096925188#rd
```## NVA-2975

```text
12-19 20:47:11.719 I/lowmemorykiller(  289): Kill 'com.hmdglobal.app.cameralite' (5420), uid 10145, oom_score_adj 0 to free 25244kB rss, 31816kB swap; reason: low watermark is breached and thrashing (64%)

12-19 20:47:10.756 E/ViewRootImpl( 5420): Accessibility content change on non-UI thread. Future Android versions will throw an exception.
12-19 20:47:10.756 E/ViewRootImpl( 5420): android.view.ViewRootImpl$CalledFromWrongThreadException: Only the original thread that created a view hierarchy can touch its views.
12-19 20:47:10.756 E/ViewRootImpl( 5420):  at android.view.ViewRootImpl$SendWindowContentChangedAccessibilityEvent.runOrPost(ViewRootImpl.java:10352)
12-19 20:47:10.756 E/ViewRootImpl( 5420):  at android.view.ViewRootImpl.postSendWindowContentChangedCallback(ViewRootImpl.java:9175)
12-19 20:47:10.756 E/ViewRootImpl( 5420):  at android.view.ViewRootImpl.notifySubtreeAccessibilityStateChanged(ViewRootImpl.java:9355)
12-19 20:47:10.756 E/ViewRootImpl( 5420):  at android.view.ViewGroup.notifySubtreeAccessibilityStateChanged(ViewGroup.java:3908)
12-19 20:47:10.756 E/ViewRootImpl( 5420):  at android.view.ViewGroup.notifySubtreeAccessibilityStateChanged(ViewGroup.java:3908)
12-19 20:47:10.756 E/ViewRootImpl( 5420):  at android.view.ViewGroup.notifySubtreeAccessibilityStateChanged(ViewGroup.java:3908)
12-19 20:47:10.756 E/ViewRootImpl( 5420):  at android.view.ViewGroup.notifySubtreeAccessibilityStateChanged(ViewGroup.java:3908)
12-19 20:47:10.756 E/ViewRootImpl( 5420):  at android.view.ViewGroup.notifySubtreeAccessibilityStateChanged(ViewGroup.java:3908)
12-19 20:47:10.756 E/ViewRootImpl( 5420):  at android.view.ViewGroup.notifySubtreeAccessibilityStateChanged(ViewGroup.java:3908)
12-19 20:47:10.756 E/ViewRootImpl( 5420):  at android.view.ViewGroup.notifySubtreeAccessibilityStateChanged(ViewGroup.java:3908)
12-19 20:47:10.756 E/ViewRootImpl( 5420):  at android.view.ViewGroup.notifySubtreeAccessibilityStateChanged(ViewGroup.java:3908)
12-19 20:47:10.756 E/ViewRootImpl( 5420):  at android.view.ViewGroup.notifySubtreeAccessibilityStateChanged(ViewGroup.java:3908)
12-19 20:47:10.756 E/ViewRootImpl( 5420):  at android.view.ViewGroup.notifySubtreeAccessibilityStateChanged(ViewGroup.java:3908)
12-19 20:47:10.756 E/ViewRootImpl( 5420):  at android.view.View.notifySubtreeAccessibilityStateChangedIfNeeded(View.java:13996)
12-19 20:47:10.756 E/ViewRootImpl( 5420):  at android.view.View.setFlags(View.java:16620)
12-19 20:47:10.756 E/ViewRootImpl( 5420):  at android.view.View.setClickable(View.java:12445)
12-19 20:47:10.756 E/ViewRootImpl( 5420):  at android.view.View.setOnClickListener(View.java:7233)
12-19 20:47:10.756 E/ViewRootImpl( 5420):  at com.dream.camera.modules.autophoto.AutoPhotoUI.fitExtendPanel(AutoPhotoUI.java:511)
12-19 20:47:10.756 E/ViewRootImpl( 5420):  at com.android.camera.PhotoUI$24.run(PhotoUI.java:2056)
12-19 20:47:10.756 E/ViewRootImpl( 5420):  at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1167)
12-19 20:47:10.756 E/ViewRootImpl( 5420):  at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:641)
12-19 20:47:10.756 E/ViewRootImpl( 5420):  at java.lang.Thread.run(Thread.java:920)

12-19 21:16:18.274 E/Cam3OEMIf(  456): 3594, freeAllCameraMem: ION/GPU buffer memory leak!!!



12-19 20:47:09.172 W/SurfaceFlinger(  526): deleteTextures was not executed, mTexturePool.size() ==  mTexturePoolSize
```## Domino GtsMemoryHostTestCases com.google.android.memory.gts.CameraMemoryHostTest#testPeakMemoryUsage

```text
NOVA
** MEMINFO in pid 17579 [com.hmdglobal.app.cameralite] **
                   Pss  Private  Private  SwapPss      Rss     Heap     Heap     Heap
                 Total    Dirty    Clean    Dirty    Total     Size    Alloc     Free
                ------   ------   ------   ------   ------   ------   ------   ------
  Native Heap    26273    26212       28    18265    27212    65560    62394     3165
  Dalvik Heap     9669     9364        0       39    16100    19239     9620     9619
 Dalvik Other     1675     1184        4       51     3184                           
        Stack     1240     1240        0      932     1244                           
       Ashmem      467      432        0        0     1076                           
    Other dev       24        0       20        0      328                           
     .so mmap     6388      428     2544     1341    34412                           
    .jar mmap     2983        0      632        0    27600                           
    .apk mmap     3890        0     3320        0     5888                           
    .ttf mmap       87        0       28        0      180                           
    .dex mmap       12        0        0        0      488                           
    .oat mmap      835        0        0        0    12528                           
    .art mmap     1838     1300        0        4    14880                           
   Other mmap     2439        8      512        0     5504                           
      Unknown      498      496        0      812      672                           
        TOTAL    79762    40664     7088    21444   151296    84799    72014    12784
 
 App Summary
                       Pss(KB)                        Rss(KB)
                        ------                         ------
           Java Heap:    10664                          30980
         Native Heap:    26212                          27212
                Code:     6952                          82068
               Stack:     1240                           1244
            Graphics:        0                              0
       Private Other:     2684
              System:    32010
             Unknown:                                    9792
 
           TOTAL PSS:    79762            TOTAL RSS:   151296       TOTAL SWAP PSS:    21444
 
 Objects
               Views:      627         ViewRootImpl:        1
         AppContexts:        8           Activities:        2
              Assets:       37        AssetManagers:        0
       Local Binders:       29        Proxy Binders:       47
       Parcel memory:       21         Parcel count:       83
    Death Recipients:        3      OpenSSL Sockets:        0
            WebViews:        0
 
 SQL
         MEMORY_USED:        0
  PAGECACHE_OVERFLOW:        0          MALLOC_SIZE:        0


==================== com.google.android.memory.gts.CameraMemoryHostTest#testPeakMemoryUsage STARTED: Wed Dec 21 10:08:15 CST 2022 ====================
12-21 10:08:16 D/ModuleListener: ModuleListener.testStarted(com.google.android.memory.gts.CameraMemoryHostTest#testPeakMemoryUsage)
12-21 10:08:16 D/RunUtil: Running command [adb, -s, 0123456789ABCDEF, shell, getprop, ro.build.version.sdk] with timeout: 2m 0s
12-21 10:08:17 W/TestDevice: Feature: feature:android.hardware.type.watch is not available on 0123456789ABCDEF
12-21 10:08:17 W/TestDevice: Feature: feature:android.hardware.type.television is not available on 0123456789ABCDEF
12-21 10:08:17 W/TestDevice: Feature: feature:android.software.leanback is not available on 0123456789ABCDEF
12-21 10:08:17 D/FileUtil: Creating temp file at /media/wzy/wzy/GMS_Wang/GTS/android-gts-10-R2(11-13)-9265057/android-gts/tools/./../../android-gts/logs/2022.12.21_09.55.37/inv_11615326971677362352 with prefix "total_memory_" suffix ".txt.gz"
12-21 10:08:17 I/LogFileSaver: Saved gzip log file /media/wzy/wzy/GMS_Wang/GTS/android-gts-10-R2(11-13)-9265057/android-gts/tools/./../../android-gts/logs/2022.12.21_09.55.37/inv_11615326971677362352/total_memory_17056293172539019856.txt.gz. [size=10, elapsed=0ms]
12-21 10:08:17 D/CertificationSuiteResultReporter: Saved logs for total_memory in /media/wzy/wzy/GMS_Wang/GTS/android-gts-10-R2(11-13)-9265057/android-gts/tools/./../../android-gts/logs/2022.12.21_09.55.37/inv_11615326971677362352/total_memory_17056293172539019856.txt.gz
12-21 10:08:17 D/FileUtil: Creating temp file at /tmp/9265057/gts/inv_11640726878802675859/inv_13001307280152478791 with prefix "total_memory_" suffix ".txt.gz"
12-21 10:08:17 I/LogFileSaver: Saved gzip log file /tmp/9265057/gts/inv_11640726878802675859/inv_13001307280152478791/total_memory_3800628033822941025.txt.gz. [size=10, elapsed=1ms]
12-21 10:08:22 D/BackgroundDeviceAction: Sleep for 5000 before starting logcat for 0123456789ABCDEF.
12-21 10:08:23 D/FileUtil: Creating temp file at /media/wzy/wzy/GMS_Wang/GTS/android-gts-10-R2(11-13)-9265057/android-gts/tools/./../../android-gts/logs/2022.12.21_09.55.37/inv_11615326971677362352 with prefix "memory_test_com.hmdglobal.app.litecamera_dumpsys_meminfo_" suffix ".txt.gz"
12-21 10:08:23 I/LogFileSaver: Saved gzip log file /media/wzy/wzy/GMS_Wang/GTS/android-gts-10-R2(11-13)-9265057/android-gts/tools/./../../android-gts/logs/2022.12.21_09.55.37/inv_11615326971677362352/memory_test_com.hmdglobal.app.litecamera_dumpsys_meminfo_17343707927002327561.txt.gz. [size=10, elapsed=0ms]
12-21 10:08:23 D/CertificationSuiteResultReporter: Saved logs for memory_test_com.hmdglobal.app.litecamera_dumpsys_meminfo in /media/wzy/wzy/GMS_Wang/GTS/android-gts-10-R2(11-13)-9265057/android-gts/tools/./../../android-gts/logs/2022.12.21_09.55.37/inv_11615326971677362352/memory_test_com.hmdglobal.app.litecamera_dumpsys_meminfo_17343707927002327561.txt.gz
12-21 10:08:23 D/FileUtil: Creating temp file at /tmp/9265057/gts/inv_11640726878802675859/inv_13001307280152478791 with prefix "memory_test_com.hmdglobal.app.litecamera_dumpsys_meminfo_" suffix ".txt.gz"
12-21 10:08:23 I/LogFileSaver: Saved gzip log file /tmp/9265057/gts/inv_11640726878802675859/inv_13001307280152478791/memory_test_com.hmdglobal.app.litecamera_dumpsys_meminfo_18107065475740440458.txt.gz. [size=10, elapsed=0ms]
12-21 10:08:25 D/FileUtil: Creating temp file at /media/wzy/wzy/GMS_Wang/GTS/android-gts-10-R2(11-13)-9265057/android-gts/tools/./../../android-gts/logs/2022.12.21_09.55.37/inv_11615326971677362352 with prefix "memory_test_com.hmdglobal.app.litecamera_dumpsys_meminfo_" suffix ".txt.gz"
12-21 10:08:25 I/LogFileSaver: Saved gzip log file /media/wzy/wzy/GMS_Wang/GTS/android-gts-10-R2(11-13)-9265057/android-gts/tools/./../../android-gts/logs/2022.12.21_09.55.37/inv_11615326971677362352/memory_test_com.hmdglobal.app.litecamera_dumpsys_meminfo_16602274470412141727.txt.gz. [size=10, elapsed=0ms]
12-21 10:08:25 D/CertificationSuiteResultReporter: Saved logs for memory_test_com.hmdglobal.app.litecamera_dumpsys_meminfo in /media/wzy/wzy/GMS_Wang/GTS/android-gts-10-R2(11-13)-9265057/android-gts/tools/./../../android-gts/logs/2022.12.21_09.55.37/inv_11615326971677362352/memory_test_com.hmdglobal.app.litecamera_dumpsys_meminfo_16602274470412141727.txt.gz
12-21 10:08:25 D/FileUtil: Creating temp file at /tmp/9265057/gts/inv_11640726878802675859/inv_13001307280152478791 with prefix "memory_test_com.hmdglobal.app.litecamera_dumpsys_meminfo_" suffix ".txt.gz"
12-21 10:08:25 I/LogFileSaver: Saved gzip log file /tmp/9265057/gts/inv_11640726878802675859/inv_13001307280152478791/memory_test_com.hmdglobal.app.litecamera_dumpsys_meminfo_1864555929639187679.txt.gz. [size=10, elapsed=0ms]
12-21 10:08:27 D/BackgroundDeviceAction: Waiting for device 0123456789ABCDEF online before starting.
12-21 10:08:27 D/BackgroundDeviceAction: Device 0123456789ABCDEF now online.
12-21 10:08:27 D/BackgroundDeviceAction: Starting logcat for 0123456789ABCDEF.
12-21 10:08:27 D/FileUtil: Creating temp file at /media/wzy/wzy/GMS_Wang/GTS/android-gts-10-R2(11-13)-9265057/android-gts/tools/./../../android-gts/logs/2022.12.21_09.55.37/inv_11615326971677362352 with prefix "memory_test_com.hmdglobal.app.litecamera_dumpsys_meminfo_" suffix ".txt.gz"
12-21 10:08:27 I/LogFileSaver: Saved gzip log file /media/wzy/wzy/GMS_Wang/GTS/android-gts-10-R2(11-13)-9265057/android-gts/tools/./../../android-gts/logs/2022.12.21_09.55.37/inv_11615326971677362352/memory_test_com.hmdglobal.app.litecamera_dumpsys_meminfo_10469988659134439626.txt.gz. [size=10, elapsed=0ms]
12-21 10:08:27 D/CertificationSuiteResultReporter: Saved logs for memory_test_com.hmdglobal.app.litecamera_dumpsys_meminfo in /media/wzy/wzy/GMS_Wang/GTS/android-gts-10-R2(11-13)-9265057/android-gts/tools/./../../android-gts/logs/2022.12.21_09.55.37/inv_11615326971677362352/memory_test_com.hmdglobal.app.litecamera_dumpsys_meminfo_10469988659134439626.txt.gz
12-21 10:08:27 D/FileUtil: Creating temp file at /tmp/9265057/gts/inv_11640726878802675859/inv_13001307280152478791 with prefix "memory_test_com.hmdglobal.app.litecamera_dumpsys_meminfo_" suffix ".txt.gz"
12-21 10:08:27 I/LogFileSaver: Saved gzip log file /tmp/9265057/gts/inv_11640726878802675859/inv_13001307280152478791/memory_test_com.hmdglobal.app.litecamera_dumpsys_meminfo_7788702098486227701.txt.gz. [size=10, elapsed=1ms]
12-21 10:08:27 D/PrettyTestEventLogger: 


从测试 pass 的log中看都只有 40M 左右
Applications Memory Usage (in Kilobytes):
Uptime: 1356356 Realtime: 1356356

** MEMINFO in pid 21737 [com.hmdglobal.app.litecamera] **
                   Pss  Private  Private  SwapPss      Rss     Heap     Heap     Heap
                 Total    Dirty    Clean    Dirty    Total     Size    Alloc     Free
                ------   ------   ------   ------   ------   ------   ------   ------
  Native Heap     1528     1524        0     4500     1616     8196     7316      879
  Dalvik Heap      839      820        0     6062      896    10925     8194     2731
 Dalvik Other      331      280        0      415      444                           
        Stack      132      132        0      324      132                           
       Ashmem        2        0        0        0        8                           
    Other dev       14        0        8        0      312                           
     .so mmap     9799      332     5248      222    34108                           
    .jar mmap     1780        0      692        0    13488                           
    .apk mmap     3788        0     2972        0    14848                           
    .dex mmap      120        0      116        4      144                           
    .oat mmap      974        0      192        0    11636                           
    .art mmap      778      548       56     1182     2872                           
   Other mmap     1541        4      452        0     4428                           
    GL mtrack     4351     4351        0        0     4351                           
      Unknown       84       84        0     1496       96                           
        TOTAL    40266     8075     9736    14205    40266    19121    15510     3610


** MEMINFO in pid 17659 [com.hmdglobal.app.litecamera] **
                   Pss  Private  Private  SwapPss      Rss     Heap     Heap     Heap
                 Total    Dirty    Clean    Dirty    Total     Size    Alloc     Free
                ------   ------   ------   ------   ------   ------   ------   ------
  Native Heap    26691    26668        0     2350    26940    31620    29898     1721
  Dalvik Heap    16885    16828        0      204    17184    18423     9212     9211
 Dalvik Other     1082      848        0       33     1488                           
        Stack      956      956        0      172      956                           
       Ashmem      383      352        0        0      576                           
    Other dev       57       12       36        0      380                           
     .so mmap    14361      692     8040      183    39604                           
    .jar mmap     2569        0      804        0    16004                           
    .apk mmap     4921        0     3216        0    21404                           
    .ttf mmap       33        0        4        0       92                           
    .dex mmap      126        0      120        4      148                           
    .oat mmap     1319        0       44        0    12500                           
    .art mmap     3013     1588        0      296     9264                           
   Other mmap      280        4       68        0     2016                           
   EGL mtrack     5437     5437        0        0     5437                           
    GL mtrack    29179    29179        0        0    29179                           
      Unknown      434      416        0     1202      556                           
        TOTAL   112170    82980    12332     4444   112170    50043    39110    10932

去掉SecureCameraActivity中的修改
```## 锁屏界面下，视频通话刚结束，面部解锁解不了

```text
M004226  12-21 11:18:39.980   591  7642 I CameraService: CameraService::connect call (PID -1 "com.hmd.face.service", camera ID 1) and Camera API version 2
M004227  12-21 11:18:39.982   591  7642 E CameraService: improve com.hmd.face.service client proprity and change score to 0
M004228  12-21 11:18:39.982   591  7642 E CameraService: CameraService::connect X (PID 26115) rejected (existing client(s) with higher priority).
M004229  12-21 11:18:39.982   591  7642 E CameraService:    Conflicts with: Device 1, client package com.google.android.apps.tachyon (PID 26360, score 0, state 2)
M00422A  12-21 11:18:39.983 26115 29105 D ==>faceunlock: openCamera android.hardware.camera2.CameraAccessException: CAMERA_IN_USE (4): connectHelper:1789: Higher-priority client using camera, ID "1" currently unavailable
M00422B  12-21 11:18:39.983 26115 29105 D ==>faceunlock: openCamera onError 1
M00422C  12-21 11:18:39.987 26115 26115 D ==>faceunlock: FaceViewManager  addView end

CameraService:    Conflicts with: Device 1, client package com.google.android.apps.tachyon (PID 26360, score 0, state 2)

解决方案：
http://192.168.3.81:8085/c/SPRD_S/SPRDROID12_TRUNK_22B_W22.09.2/+/5872

--- a/alps/frameworks/av/services/camera/libcameraservice/CameraService.cpp
+++ b/alps/frameworks/av/services/camera/libcameraservice/CameraService.cpp
@@ -1435,8 +1435,11 @@ status_t CameraService::handleEvictionsLocked(const String8& cameraId, int clien
 
         resource_policy::ClientPriority clientPriority = clientDescriptor->getPriority();
 #ifdef SPRD_FRAMEWORKS_CAMERA_EX
         clientDescriptor->third_party = packageName.compare(String8("com.tencent.mm")) &
-            packageName.compare(String8("com.google.android.apps.tachyon.readyapp"));
+            packageName.compare(String8("com.google.android.apps.tachyon.readyapp")) &
+            packageName.compare(String8("com.google.android.apps.tachyon"));
 #endif
         // Find clients that would be evicted
         auto evicted = mActiveClientManager.wouldEvict(clientDescriptor);
```## ANR分析

```text
https://blog.csdn.net/xct841990555/article/details/127874020

https://blog.csdn.net/sinat_22657459/article/details/52780759
```## AndroidR 默认赋予app权限，不弹出权限申请窗口

```text
https://blog.csdn.net/qq_37858386/article/details/126525152
```## 查看视频文件丢帧情况工具

```text
#!/bin/bash
#######################################################################################
# 2019.10.24
#
# 5种使用方法
# 1.解析手机上相册下最新产生的视频文件
# ./as_frameloss.sh
# 2.解析pc上指定路径下视频文件
# ./as_frameloss.sh pc_video_file_path
# example:
# ./as_frameloss.sh /home/chengang/Documents/g7b/zhenlv/VID_20191022_194835_HSR_240.mp4
#
# 3.指定pull目录且使用新生成的视频文件名进行解析
# as_frameloss.sh pc_tmp_dir video_file_name
# example:
# ./as_frameloss.sh /home/chengang/Documents/g7b/zhenlv/ VID_20191022_194835_HSR_240.mp4
#
# 4.使用默认pull目录且使用新生成的文件名进行解析
# ./as_frameloss.sh VID_20191022_194835_HSR_240.mp4
#
# 5.使用默认pull目录且分析完删除pc上的video文件
# ./as_frameloss.sh -d video_file_name
# ./as_frameloss.sh -d VID_20191022_194835_HSR_240.mp4
 
########################################################################################
 
TMP_PTS_FILE="pkt_pts_time_tmp.txt"
VIDEO_REAL_FPS=0 #视频文件实际帧率
FPS_DEMANDED=0 #视频文件要求达到的帧率
VIDEO_FILE_TEMP_DIR="/home/${USER}/as_frameloss_video_files"
analysis_out_fps_from_single_file(){
    path_2_file_name=$1
    avg_frame_rate=$(ffprobe -select_streams v -v quiet -print_format json -show_format -show_streams $path_2_file_name |awk -F "[avg_frame_rate]" '/avg_frame_rate/{print$0}')
    str=$(echo $avg_frame_rate | awk -F "[:]" '/avg_frame_rate/{print$2}')
    #echo $str,上一步得到字符串'"39060000/1362709",'
    #去除行头的"号
    str1=$(echo ${str#*\"})
    #接着去除行末"号及之后的,号
    final_str=$(echo ${str1%\"*})
    #分割取出地一个数值
    first_value=`echo $final_str|awk -F "[/]" '{print$1}' `
    #取出第二个数值
    second_value=`echo $final_str|awk -F "[/]" '{print$2}' `
    #echo $first_value
    #echo $second_value
    #保留两位小数输出帧率,四舍五入与windows上保持一致
    VIDEO_REAL_FPS=`awk 'BEGIN{printf "%.2f\n",'$first_value'/'$second_value'}'`
}
 
analysis_frameloss(){
    pc_tmp_video_file_full_path=$1
    #取出参数中的文件的目录,这里不带最后一个斜杠后面需要在补上
    path_of_video_dir=`echo ${pc_tmp_video_file_full_path%/*}`
    path_of_tmp_file=$path_of_video_dir/$TMP_PTS_FILE
 
    str_result=""
    time1=$(date)
    str_result=`ffprobe  -show_frames -select_streams v $pc_tmp_video_file_full_path  |  grep pkt_pts_time`
    echo "$str_result" >  $path_of_tmp_file
    time2=$(date)
 
    frame_count=0
    string_final=""
    last_frame=0
 
    frame_count_demanded_per_0_1s=`expr $FPS_DEMANDED / 10`
    echo "******************************************************************"
    echo " "
    echo "Frameloss Analysis "
    echo " "
    echo "文件路径 :  $pc_tmp_video_file_full_path"
    echo "要求帧率 :  $FPS_DEMANDED"
    echo "实际帧率 :  $VIDEO_REAL_FPS"
    echo "丢帧情况 : "
    while read line
    do
        time_str=${line:13}
        tmp_str=`echo ${time_str::-5}` #从字符串尾部删掉5个字符
        let time_str_final=`echo 10#$tmp_str | sed 's/\.\+//g'` #保证10进制打印
        if [ $time_str_final == $last_frame ];then
            let "frame_count++"
        else
            loss_frame_no=`expr $frame_count_demanded_per_0_1s - $frame_count`
            denominator=10
            #res=`echo "scale=1; $last_frame/$denominator" | bc`
            res=$(printf "%.1f" `echo "scale=1;$last_frame/$denominator"|bc`)
            if [ $loss_frame_no != 0 ];then
               echo "第$res秒---> $loss_frame_no"
        #else
             #  echo "第$res秒---> "
            fi
            #开始新的0.1s计数
            last_frame=$time_str_final
            frame_count=1
        fi
 
        if [ "$string_final" == "" ];then
            string_final="$time_str_final"
        else
            string_final="$string_final;$time_str_final"
        fi
        #echo $string_final
    done <  $path_of_tmp_file
    time3=$(date)
}
 
figout_fps_demanded(){
    local_fps=$1
    real_int_fps=`echo $local_fps | awk -F '\.' '{print $1}'`
    echo "figout_fps_demanded-local_fps:real_int_fps[$local_fps:$real_int_fps]"
    if [[ $real_int_fps -gt 150 ]];then
        FPS_DEMANDED=240
    elif [[ $real_int_fps -gt 80 ]];then
        FPS_DEMANDED=120
    elif [[ $real_int_fps -gt 40 ]];then
        FPS_DEMANDED=60
    else  
        FPS_DEMANDED=30
    fi
}
 
file_value="$1"
pc_video_file_path=""
pc_tmp_video_dir=""
device_video_file_path=""
device_video_file_dir="/storage/emulated/0/DCIM/Camera"
 
param_count=$#
need_to_delete=0
need_to_adb_pull=0
if [ $param_count == 2 ]; then
    if  [ "$1" == "-d" ]; then
        need_to_delete=1
        need_to_adb_pull=1
        device_video_file_path=$device_video_file_dir/$2
        pc_tmp_video_dir=$VIDEO_FILE_TEMP_DIR
        pc_video_file_path=$pc_tmp_video_dir/$2
    else
        need_to_adb_pull=1
        pc_tmp_video_dir=$1
        device_video_file_path=$device_video_file_dir/$2
        pc_video_file_path=$pc_tmp_video_dir/$2
    fi
elif [ $param_count == 1 ]; then
    if [ -f $1 ]; then
        pc_video_file_path=$1
    else
        need_to_adb_pull=1
        device_video_file_path=$device_video_file_dir/$1
        pc_tmp_video_dir=$VIDEO_FILE_TEMP_DIR
        pc_video_file_path=$pc_tmp_video_dir/$1
    fi
elif [ $param_count == 0 ]; then
    need_to_adb_pull=1
    #获取相册目录下最新的视频文件
    device_video_newest_file_name=`adb shell ls -lt /sdcard/DCIM/Camera | grep mp4 | head -n 1 |awk '{print $8}'`
    device_video_file_path=$device_video_file_dir/$device_video_newest_file_name
    pc_tmp_video_dir=$VIDEO_FILE_TEMP_DIR
    pc_video_file_path=$pc_tmp_video_dir/$device_video_newest_file_name
fi
 
 
#需要同步手机文件至pc
if [ $need_to_adb_pull == 1 ]; then
    echo "device_video_file_path:$device_video_file_path"
    echo "pc_tmp_video_dir:$pc_tmp_video_dir"
    if [ ! -d "$pc_tmp_video_dir" ];then
        mkdir -p $pc_tmp_video_dir
    fi
    adb pull $device_video_file_path $pc_tmp_video_dir
fi
 
analysis_out_fps_from_single_file $pc_video_file_path
figout_fps_demanded $VIDEO_REAL_FPS
analysis_frameloss $pc_video_file_path
 
#是否需要删掉电脑上的视频文件
if [ $need_to_delete == 1 ]; then
     rm -fr $pc_video_file_path
fi
```## availableCapabilities 是什么意思？有什么用？下面的参数分别代表什么意思？根据什么配置？

```text
SprdCamera3Setting.cpp
const uint8_t kavailable_capabilities[] = {
    ANDROID_REQUEST_AVAILABLE_CAPABILITIES_BACKWARD_COMPATIBLE,
    //ANDROID_REQUEST_AVAILABLE_CAPABILITIES_MANUAL_SENSOR,
    //ANDROID_REQUEST_AVAILABLE_CAPABILITIES_READ_SENSOR_SETTINGS,
    // ANDROID_REQUEST_AVAILABLE_CAPABILITIES_MANUAL_POST_PROCESSING,
    // ANDROID_REQUEST_AVAILABLE_CAPABILITIES_RAW,
    ANDROID_REQUEST_AVAILABLE_CAPABILITIES_BURST_CAPTURE,
#ifdef HIGH_SPEED_VIDEO
    ANDROID_REQUEST_AVAILABLE_CAPABILITIES_CONSTRAINED_HIGH_SPEED_VIDEO,
#endif
    ANDROID_REQUEST_AVAILABLE_CAPABILITIES_MONOCHROME
};

截止Android S，包括如下Capability：

BACKWARD_COMPATIBLE
    Camera HAL1具备的能力，几乎所有设备都支持这种能力（拥有DEPTH_OUTPUT的设备可以是例外）
    Depth output camera可以不支持该Capability
    具备旧有API：android.hardware.Camera 的所有能力
MANUAL_SENSOR
    在Sensor图像获取阶段的相关模块，要求支持手动控制
MANUAL_POST_PROCESSING
    在Sensor图像后处理（ISP）阶段的相关模块，要求支持手动控制
RAW
    表示当前设备支持输出RAW图
    可以将RAW图和相关Metadata打包成DNG文件保存，或者App通过算法直接出图RAW图
    ImageFormat.RAW_SENSOR (RAW16) 必须支持
PRIVATE_REPROCESSING
    该Feature主要用于应用层的ZSL（Zero Shutter Lag）功能
    支持ImageFormat.PRIVATE
READ_SENSOR_SETTINGS
    表示当前设备支持在CaptureResult中能精确地回报Camera Sensor实际生效的参数
    拥有 MANUAL_SENSOR Capability的Camera，必须包含 READ_SENSOR_SETTINGS
BURST_CAPTURE
    这种Capability对高分辨率拍照有如下要求
    <=8MP, >=20fps, 且支持YUV Output
    <=24MP, >=10fps
    适用场景：连拍
YUV_REPROCESSING
    跟PRIVATE_REPROCESSING类似，表示当前设备支持YUV_420_888的再处理
DEPTH_OUTPUTAL
    表示当前设备支持输出深度图像
    必须支持ImageFormat.DEPTH16，且支持同宽高比的Jpeg图像输出
    如果支持ImageFormat.DEPTH_JPEG（JPEG压缩主图像和XMP格式嵌入深度图）
    DEPTH_IS_EXCLUSIVE必须为False，表示主图像和深度图可以同时输出
    如果不支持ImageFormat.DEPTH_JPEG
    DEPTH_IS_EXCLUSIVE必须为True，表示主图像和深度图可以不能同时输出
CONSTRAINED_HIGH_SPEED_VIDEO
    表面当前设备支持高帧率录像（ frame rate >=120fps ）
    这种模式下AE、AWB强制设置为ON，AF强制设置为CONTINUOUS_VIDEO
    POST-PROCESSING的模块强制设置为FAST模式
    Session最多支持配置2个Surface（Preview + Recording）
MOTION_TRACKING
    表示该设备支持跟踪运动物体
    为了减少运动模糊，在这种Capability下AE会将曝光时间限制在<=20ms
LOGICAL_MULTI_CAMERA
    表示这颗Camera对应多颗物理Camera
    Hardware Level至少是LIMITED
MONOCHROME
    表示该Camera设备是一个单色Camera设备
    当输入YUV_420_888时，U和V的值均为128
    单色摄像头可以用作Logical MultiCamera设备的某个Physical Camera，以获取更出色的低光噪音特性。
SECURE_IMAGE_DATA
    表示该Camera设备可以产生只能TEE能访问的图像数据
    Android 用户空间和Kernel都无法访问这块图像数据
    可用于人脸解锁等场景
SYSTEM_CAMERA
    表示这颗Camera设备只能被System App使用，对其他App不可见
    只有安装在系统分区上且具有与系统相同的证书或使用该证书进行签名的应用才能获得此权限
    App需要申请 android.permission.SYSTEM_CAMERA 和android.permission.CAMERA权限
    如果设备制造商希望实现需要访问相机的功能，但这些功能仅限于特权应用或系统应用，该功能会非常有用
OFFLINE_PROCESSING
    表示该Camera设备支持离线处理功能
    在离线模式处理的过程中，App可以打开相机重新创建Session与Offline Session并发工作
    适用场景：快拍
ULTRA_HIGH_RESOLUTION_SENSOR
    表示该设备支持输出Sensor最大size的图像
    Sensor工作在SENSOR_PIXEL_MODE_DEFAULT模式：输出Binning Size的图像
    Sensor工作在SENSOR_PIXEL_MODE_MAXIMUM_RESOLUTION模式：输出Full Size的图像
REMOSAIC_REPROCESSING
    表示该设备支持Remosaic的再处理
    该Capability需要ULTRA_HIGH_RESOLUTION_SENSOR同时支持才行
    App完成SW Remosaic算法，将结果送给HAL再处理
    Remosaic介绍
    https://deepinout.com/camera-terms/camera-remosaic-intro.html
    https://deepinout.com/camera-terms/camera-4-cell-remosaic-intro.html

Hardware Level与Capability的关系
所有Camera设备必须包含BACKWARD_COMPATIBLE或DEPTH_OUTPUT能力

判断某个Camera Feature是否支持
Feature     如何判断是否支持
FD         读取CameraCharacteristics.STATISTICS_INFO_AVAILABLE_FACE_DETECT_MODES，是否包含SIMPLE或FULL模式
OIS         读取android.lens.info.availableOpticalStabilization，是否包含ON
EIS         读取android.control.availableVideoStabilizationModes，是否包含ON
AF         读取android.control.afAvailableModes，是否包含AUTO / MACRO / CONTINUOUS_VIDEO / CONTINUOUS_PICTURE / EDOF

https://blog.csdn.net/qq_42194101/article/details/120144684


media.camera
NOVA
android.request.availableCapabilities (c000c): byte[2]
[BACKWARD_COMPATIBLE BURST_CAPTURE ]

android.request.availableCapabilities (c000c): byte[2]
[BACKWARD_COMPATIBLE READ_SENSOR_SETTINGS ]
```## 计算相机不同Ratio分辨率

```text
public class Main {
    public static void main(String[] args) {
        int width = Integer.parseInt(args[0]);
        int height = Integer.parseInt(args[1]);
        int min = width < height ? width : height;
        int arg = 0;
        int widthArgs = 0;
        int heightArgs = 0;
        for (int i = min; i >= 1; i--) {
            if (width % i == 0 && height % i == 0) {
                widthArgs = width / i;
                heightArgs = height / i;
                arg = i;
                System.out.println("最大公约数是：" + i + " widthArgs:" + widthArgs + " heightArgs:" + heightArgs);
                break;
            }
        }
        printSize(3, 4);
        printSize(9, 16);
        printSize(1, 1);
        printSize(9, 20);
    }
    public static void printSize(int ratioW, int ratioH) {
        int width = 720;
        int height = 1600;
        int widthA = width / (ratioW * 16);
        int heightA = height / (ratioH * 16);
        if (heightA < widthA) {
            widthA = heightA;
        }
        System.out.println(ratioW+":"+ratioH+" " + widthA * ratioW * 16 + "x" + widthA * ratioH * 16);
    }
}
```## Android性能测试之fps获取

```text
https://blog.csdn.net/itfootball/article/details/43084527/

https://blog.csdn.net/weixin_42233460/article/details/107698909
```## Android 8.1 如何查看系统支持哪些音视频编解码格式

```text
frameworks/av/media/libstagefright/omx/SoftOMXPlugin.cpp
```## app_mode 有什么用？

```text
vendor/sprd/modules/libcamera/common/inc/cmr_common.h

enum sprd_camera_app_mode {
    CAMERA_MODE_AUTO_PHOTO = 0,
    CAMERA_MODE_MANUAL,
    CAMERA_MODE_CONTINUE,
    CAMERA_MODE_INTERVAL,
    CAMERA_MODE_PANORAMA,
    CAMERA_MODE_REFOCUS,
    CAMERA_MODE_SCENE,
    CAMERA_MODE_PIP,
    CAMERA_MODE_GCAM,
    CAMERA_MODE_AUTO_VIDEO,
    CAMERA_MODE_VIV,
    CAMERA_MODE_TIMELAPSE,
    CAMERA_MODE_SLOWMOTION,
    CAMERA_MODE_AUDIO_PICTURE,
    CAMERA_MODE_FILTER,
    CAMERA_MODE_QRCODE,
    CAMERA_MODE_VIDEO_TD,
    CAMERA_MODE_PHOTO_TD,
    CAMERA_MODE_FRONT_BLURREFOCUS,
    CAMERA_MODE_TD_RANGE_FIND,
    CAMERA_MODE_3DNR_PHOTO,
    CAMERA_MODE_3DNR_VIDEO,
    CAMERA_MODE_INTENTCAPTURE,
    CAMERA_MODE_INTENTVIDEO,
    CAMERA_MODE_VIDEO,
    CAMERA_MODE_TDNREnable,
    CAMERA_MODE_AR_PHOTO,
    CAMERA_MODE_AR_VIDEO,
    CAMERA_MODE_BACK_ULTRA_WIDE,
    CAMERA_MODE_PORTRAIT_PHOTO,
    CAMERA_MODE_HIGH_RES_PHOTO,
    CAMERA_MODE_SUPER_MACRO = 31,
    CAMERA_MODE_FOV_FUSION_MODE = 35,
    CAMERA_MODE_NIGHT_PHOTO = 53,
    CAMERA_MODE_NIGHT_VIDEO = 54,
    CAMERA_MODE_FDR = 55,
    CAMERA_MODE_NIGHT_HDR_MFNR = 56,
    CAMERA_MODE_MAX
};
```## ANR----Application does not have a focused window

```text
EE4EA66  01-05 18:26:07.082  1000  4516 I am_proc_bound: [0,3958,com.hmdglobal.app.cameralite]
ME4EA67  01-05 18:26:07.083  1253 23740 D FaceUnlock: onTaskStackChangedBackground
ME4EA68  01-05 18:26:07.084  1253 23740 D FaceUnlock: PackageName =com.hmdglobal.app.cameralite
EE4EA69  01-05 18:26:07.091  1000  4516 I wm_restart_activity: [0,130839027,10874,com.hmdglobal.app.cameralite/com.android.camera.CameraLauncher]
EE4EA6A  01-05 18:26:07.094  1000  4516 I wm_set_resumed_activity: [0,com.hmdglobal.app.cameralite/com.android.camera.CameraLauncher,minimalResumeActivityLocked]
ME4EA6B  01-05 18:26:07.096   539   539 W SurfaceFlinger: deleteTextures was not executed, mTexturePool.size() ==  mTexturePoolSize
ME4EA6C  01-05 18:26:07.096  1000  4516 D hmdEnterprise:  <getBlockLuncherStatus> blockLuncherStatus =false
ME4EA6D  01-05 18:26:07.098   485   485 D vendor.unisoc.hardware.power-service: Enter getSceneIdByName: sceneName:com.hmdglobal.app.cameralite

ME4EC87  01-05 18:26:07.718  3958  3958 I CAM_PhotoModule: resume start!

ME4ECDB  01-05 18:26:07.770  3958  3958 I CAM_CameraActivity Drea: onResume end!

ME4ED75  01-05 18:26:07.974  1000  1142 W InputDispatcher: Waiting because no window has focus but ActivityRecord{7cc71f3 u0 com.hmdglobal.app.cameralite/com.android.camera.CameraLauncher t10874} may eventually add a window when it finishes starting up. Will wait for 5000ms

SE50392  01-05 18:26:25.149  1000  4190 E ActivityManager: ANR in com.hmdglobal.app.cameralite (com.hmdglobal.app.cameralite/com.android.camera.CameraLauncher)
SE50392  01-05 18:26:25.149  1000  4190 E ActivityManager: PID: 3958
SE50392  01-05 18:26:25.149  1000  4190 E ActivityManager: Reason: Input dispatching timed out (Application does not have a focused window)
SE50392  01-05 18:26:25.149  1000  4190 E ActivityManager: Parent: com.hmdglobal.app.cameralite/com.android.camera.CameraLauncher
SE50392  01-05 18:26:25.149  1000  4190 E ActivityManager: Frozen: false
SE50392  01-05 18:26:25.149  1000  4190 E ActivityManager: Load: 10.48 / 9.24 / 8.95
SE50392  01-05 18:26:25.149  1000  4190 E ActivityManager: ----- Output from /proc/pressure/memory -----
SE50392  01-05 18:26:25.149  1000  4190 E ActivityManager: some avg10=7.42 avg60=3.97 avg300=2.59 total=1308519798
SE50392  01-05 18:26:25.149  1000  4190 E ActivityManager: full avg10=4.60 avg60=2.35 avg300=1.33 total=644764217
SE50392  01-05 18:26:25.149  1000  4190 E ActivityManager: ----- End output from /proc/pressure/memory -----
SE50392  01-05 18:26:25.149  1000  4190 E ActivityManager: 
SE50392  01-05 18:26:25.149  1000  4190 E ActivityManager: CPU usage from 0ms to 10582ms later (2023-01-05 18:26:14.499 to 2023-01-05 18:26:25.081):
SE50392  01-05 18:26:25.149  1000  4190 E ActivityManager:   58% 1000/system_server: 35% user + 23% kernel / faults: 10205 minor 3267 major
SE50392  01-05 18:26:25.149  1000  4190 E ActivityManager:   39% 473/android.hardware.camera.provider@2.4-service: 29% user + 10% kernel / faults: 35916 minor 44 major
SE50392  01-05 18:26:25.149  1000  4190 E ActivityManager:   34% 3958/com.hmdglobal.app.cameralite: 23% user + 10% kernel / faults: 8844 minor 247 major

据说是因为启动的时候太慢导致的
```## 冻屏问题如何分析

```text
InputReader?
InputReader: dispatchTouches action
```## 

```text
M36FF6E  12-22 05:32:06.589   550 13523 D Cam3OEMIf: 10770, Callback_ZslMalloc: size 11985408 sum 10 mZslHeapNum 0, BufferCount 8
M36FF6F  12-22 05:32:06.590   550 13523 D Cam3OEMIf: 10652, allocCameraMemForGpu: size 11985408 sum 10 mZslHeapNum 0


M349D27  12-22 05:27:13.868   550 12153 D Cam3OEMIf: 10630, freeCameraMemForGpu: TotalGpuSize=0, total_size 26497024
M34A1B5  12-22 05:27:14.236   550 11900 I Cam3OEMIf: 1069, closeCamera: :hal3: X CamId=0 TotalIonSize=25812992 TotalGpuSize=0, total_size 25812992
M34A1BE  12-22 05:27:14.238   550 11900 D Cam3OEMIf: 11342, Callback_Sw3DNRCapturePathFree: TotalGpuSize=0
M34A1C3  12-22 05:27:14.239   550 11900 I Cam3OEMIf: 3597, freeAllCameraMem: :hal3: X CamId=0 TotalIonSize=0 TotalGpuSize=0, total_size 0
M34EB57  12-22 05:28:57.317   550 11900 I Cam3OEMIf: 4011, startPreviewInternal: X CamId=0 TotalIonSize=26259456 TotalGpuSize=0, total_size 26259456
M34EC5B  12-22 05:28:57.426   550 12864 D Cam3OEMIf: 10700, allocCameraMemForGpu: TotalGpuSize=59927040, total_size 86186496
M3583CE  12-22 05:29:36.695   550 12816 D Cam3OEMIf: 10630, freeCameraMemForGpu: TotalGpuSize=0, total_size 26259456
M35898F  12-22 05:29:36.990   550   943 I Cam3OEMIf: 4011, startPreviewInternal: X CamId=0 TotalIonSize=26259456 TotalGpuSize=0, total_size 26259456
M358A5B  12-22 05:29:37.053   550 13005 D Cam3OEMIf: 10700, allocCameraMemForGpu: TotalGpuSize=59927040, total_size 86186496
M36B065  12-22 05:30:24.192   550 12816 D Cam3OEMIf: 10630, freeCameraMemForGpu: TotalGpuSize=0, total_size 26497024
M36B485  12-22 05:30:24.519   550 11900 I Cam3OEMIf: 1069, closeCamera: :hal3: X CamId=0 TotalIonSize=25812992 TotalGpuSize=0, total_size 25812992
M36B498  12-22 05:30:24.522   550 11900 D Cam3OEMIf: 11342, Callback_Sw3DNRCapturePathFree: TotalGpuSize=0
M36B4A2  12-22 05:30:24.522   550 11900 I Cam3OEMIf: 3597, freeAllCameraMem: :hal3: X CamId=0 TotalIonSize=0 TotalGpuSize=0, total_size 0


M36FF6E  12-22 05:32:06.589   550 13523 D Cam3OEMIf: 10770, Callback_ZslMalloc: size 11985408 sum 10 mZslHeapNum 0, BufferCount 8
M36FF6F  12-22 05:32:06.590   550 13523 D Cam3OEMIf: 10652, allocCameraMemForGpu: size 11985408 sum 10 mZslHeapNum 0


M36FFE2  12-22 05:32:06.597   550   943 I Cam3OEMIf: 4011, startPreviewInternal: X CamId=0 TotalIonSize=26259456 TotalGpuSize=0, total_size 26259456        // 0

M37000D  12-22 05:32:06.623   550 13523 D Cam3OEMIf: 10689, allocCameraMemForGpu: alloc graphicbuffer [0]: handle 0xe6c4faa0, fd 66, vaddr 0xd3129000
M37006C  12-22 05:32:06.640   550 13523 D Cam3OEMIf: 10689, allocCameraMemForGpu: alloc graphicbuffer [1]: handle 0xe6c4fb40, fd 75, vaddr 0xd25ba000
M37009C  12-22 05:32:06.670   550 13523 D Cam3OEMIf: 10689, allocCameraMemForGpu: alloc graphicbuffer [2]: handle 0xe6c4ff00, fd 81, vaddr 0xd194d000
M3700DE  12-22 05:32:06.706   550 13523 D Cam3OEMIf: 10689, allocCameraMemForGpu: alloc graphicbuffer [3]: handle 0xe6c500e0, fd 91, vaddr 0xd0ce0000
M370114  12-22 05:32:06.734   550 13523 D Cam3OEMIf: 10689, allocCameraMemForGpu: alloc graphicbuffer [4]: handle 0xe6c50360, fd 103, vaddr 0xd0073000

M370115  12-22 05:32:06.734   550 13523 D Cam3OEMIf: 10700, allocCameraMemForGpu: TotalGpuSize=59927040, total_size 86186496                                // 59927040
M3799CE  12-22 05:32:46.029   550 13473 D Cam3OEMIf: 10630, freeCameraMemForGpu: TotalGpuSize=0, total_size 26259456
M379FCB  12-22 05:32:46.371   550 11900 I Cam3OEMIf: 4011, startPreviewInternal: X CamId=0 TotalIonSize=26259456 TotalGpuSize=0, total_size 26259456
M37A07B  12-22 05:32:46.458   550 13591 D Cam3OEMIf: 10700, allocCameraMemForGpu: TotalGpuSize=59927040, total_size 86186496


M38CE32  12-22 05:33:32.538   550 13473 D cmr_setting: 3118, setting_get_appmode: get appmode 2
M38CE33  12-22 05:33:32.538   550 13473 D cmr_prev: 5108, prev_stop: app_mode = 2
M38CE34  12-22 05:33:32.538   550 13474 D cmr_prev: 3220, prev_swalg_thread_proc: close
M38CE35  12-22 05:33:32.538   550 13474 D cmr_prev: 17631, prev_fd_close: is_support_fd 1, is_fd_on 1


M38D1A9  12-22 05:33:32.818   550 13462 D cmr_prev: 1181, cmr_preview_deinit: app_mode = 2



M38D277  12-22 05:33:32.903   550   550 I Cam3OEMIf: 1069, closeCamera: :hal3: X CamId=0 TotalIonSize=25812992 TotalGpuSize=59927040, total_size 85740032
M38D281  12-22 05:33:32.909   550   550 D Cam3OEMIf: 11342, Callback_Sw3DNRCapturePathFree: TotalGpuSize=59927040
M38D287  12-22 05:33:32.910   550   550 I Cam3OEMIf: 3597, freeAllCameraMem: :hal3: X CamId=0 TotalIonSize=0 TotalGpuSize=59927040, total_size 59927040




感觉应该是退出的时候mode变为了2，所以导致 freeCameraMemForGpu() 没有走进去，内存回收失败

    if (mSprd3dnrType == CAMERA_3DNR_TYPE_PREV_HW_CAP_SW || (mTopAppId > 0) ||
        (sprddefInfo->sprd_appmode_id == CAMERA_MODE_AUTO_PHOTO)|| (getMultiCameraMode() == MODE_BOKEH && mCameraId == mMasterId)
         || getMultiCameraMode() == MODE_BLUR) {
        ret = allocCameraMemForGpu(size, sum, phy_addr, vir_addr, fd);
        return ret;
    }

    if (mSprd3dnrType == CAMERA_3DNR_TYPE_PREV_HW_CAP_SW || (mTopAppId > 0) ||
        (sprddefInfo->sprd_appmode_id == CAMERA_MODE_AUTO_PHOTO) ||(getMultiCameraMode() == MODE_BOKEH && mCameraId == mMasterId)
         || getMultiCameraMode() == MODE_BLUR) {
         

M3816EA  12-22 05:33:18.139   550 13475 D cmr_setting: 3118, setting_get_appmode: get appmode 0
M381727  12-22 05:33:18.219   550 13475 D cmr_setting: 3118, setting_get_appmode: get appmode 0
M381740  12-22 05:33:18.228   550 13475 D cmr_setting: 3118, setting_get_appmode: get appmode 0
M3817D1  12-22 05:33:18.308   550 13475 D cmr_setting: 3118, setting_get_appmode: get appmode 0
M3817E3  12-22 05:33:18.313   550 13475 D cmr_setting: 3118, setting_get_appmode: get appmode 0
M381834  12-22 05:33:18.340   550   943 D cmr_setting: 3118, setting_get_appmode: get appmode 0

M381891  12-22 05:33:18.352   550 13471 D cmr_setting: 3118, setting_get_appmode: get appmode 2
M3818E4  12-22 05:33:18.358   550 13471 D cmr_setting: 3118, setting_get_appmode: get appmode 2
M381927  12-22 05:33:18.362   550 13471 D cmr_setting: 3118, setting_get_appmode: get appmode 2
M381966  12-22 05:33:18.367   550 13471 D cmr_setting: 3118, setting_get_appmode: get appmode 2
M381980  12-22 05:33:18.398   550 13475 D cmr_setting: 3118, setting_get_appmode: get appmode 2
M381992  12-22 05:33:18.404   550 13475 D cmr_setting: 3118, setting_get_appmode: get appmode 2
M3819CD  12-22 05:33:18.416   550   944 D cmr_setting: 3118, setting_get_appmode: get appmode 2
M381A07  12-22 05:33:18.423   550 13475 D cmr_setting: 3118, setting_get_appmode: get appmode 2
M381B81  12-22 05:33:18.494   550 13475 D cmr_setting: 3118, setting_get_appmode: get appmode 2
M381B96  12-22 05:33:18.499   550 13475 D cmr_setting: 3118, setting_get_appmode: get appmode 2




M379C3C  12-22 05:32:46.229   550 11900 D cmr_setting: 2357, setting_set_appmode: setting_set_appmode=0
M379DA7  12-22 05:32:46.260   550 11900 D cmr_setting: 2357, setting_set_appmode: setting_set_appmode=0
M37A025  12-22 05:32:46.399   550 11900 D cmr_setting: 2357, setting_set_appmode: setting_set_appmode=0
M37EEF9  12-22 05:33:06.794   550 11900 D cmr_setting: 2357, setting_set_appmode: setting_set_appmode=0

M381839  12-22 05:33:18.341   550   943 D cmr_setting: 2357, setting_set_appmode: setting_set_appmode=2
M3819D2  12-22 05:33:18.417   550   944 D cmr_setting: 2357, setting_set_appmode: setting_set_appmode=2
M381D4B  12-22 05:33:18.602   550   943 D cmr_setting: 2357, setting_set_appmode: setting_set_appmode=2
M382025  12-22 05:33:18.728   550   943 D cmr_setting: 2357, setting_set_appmode: setting_set_appmode=2


M381834  12-22 05:33:18.340   550   943 D cmr_setting: 3118, setting_get_appmode: get appmode 0
M381835  12-22 05:33:18.340   550   943 D Cam3Channel: 1689, start: ANDROID_CONTROL_AF_TRIGGER frame_number 787
M381836  12-22 05:33:18.341   550   943 D Cam3OEMIf: 9392, SetCameraParaTag: mCameraId=0, AF_TRIGGER 0
M381837  12-22 05:33:18.341   550   943 D Cam3OEMIf: 10074, SetCameraParaTag: getCaptureState: SPRD_PREVIEW_IN_PROGRESS,  mSprdAppmodeId:0
M381838  12-22 05:33:18.341   550   943 D cmr_setting: 2345, setting_set_3dnr_type: sprd_3dnr_type=0
M381839  12-22 05:33:18.341   550   943 D cmr_setting: 2357, setting_set_appmode: setting_set_appmode=2     //这里设置了appmode为2

连拍的时候按home键退出果然会出现
01-07 07:38:20.372   517   927 E Cam3OEMIf: 3594, freeAllCameraMem: ION/GPU buffer memory leak!!!
```## DreamFilter 为什么一直都在跑？

```text
CAM_DreamFilterModuleCo: checkFrameCount mFrameCount=1
```## 广角镜头适配

```text
//获取镜头数量, 略

//通过物理尺寸, 对焦距离, 算出FOV(Field of view), 相机水平弧度, 垂直弧度
val size = characteristics.get(CameraCharacteristics.SENSOR_INFO_PHYSICAL_SIZE)
val focalLens1 = characteristics.get(CameraCharacteristics.LENS_INFO_AVAILABLE_FOCAL_LENGTHS)!!
val w = size!!.width
val h = size.height
val horizontalAngle = (2 * Math.atan(w / (focalLens1[0] * 2).toDouble())).toFloat()
val verticalAngle = (2 * Math.atan(h / (focalLens1[0] * 2).toDouble())).toFloat()

//简单判断哪个是广角镜头
//通过FOV(field of view)排序, 从小到大, 角度越大, 越是广角
val comparator = object : Comparator<CameraInformation> {
    override fun compare(o1: CameraInformation, o2: CameraInformation): Int {
        val o1FovSize = o1.fovHorizontal * o1.fovVertical
        val o2FovSize = o2.fovHorizontal * o2.fovVertical
        if (o1FovSize > o2FovSize) {
            return 1
        } else if (o1FovSize < o2FovSize) {
            return -1
        }
        return 0
    }
}
```## 人脸属性检测菜单

```text
private void updateVisibilityFaceAttributeDetect() {
    if (!DataModuleManager.getInstance(getContext()).getDataModulePhoto().getSupportedAttributesEnable()) {
        recursiveDelete(this, findPreference(Keys.KEY_AI_DETECT_FACE_ATTRIBUTES));
    }
}

if (!isSupportedAttributesInited){
    mSupportedAttributesEnable = proxy.getCapabilities().getSupportedFaceAttributesEnable();
    isSupportedAttributesInited = true;
}

public final boolean getSupportedFaceAttributesEnable(){
    return mSupportedFaceAttributesEnable;
}

public Boolean getSupportedAttributesEnable() {
    return mSupportedAttributesEnable;
}

private void buildFaceAttributesEnable(CameraCharacteristics p){
    try {
        if(p.get(CONTROL_AVAILABLE_FACEFEATUREENABLE) == null){
            mSupportedFaceAttributesEnable = false;
        }else{
            byte supportedFaceAttributesEnable = p.get(CONTROL_AVAILABLE_FACEFEATUREENABLE);        //最终获取TAG的地方
            Log.d(TAG, "supportedFaceAttributesEnable = " + supportedFaceAttributesEnable);
            if (0 == supportedFaceAttributesEnable) {
                mSupportedFaceAttributesEnable = false;
            } else {
                mSupportedFaceAttributesEnable = true;
            }
        // set mSupportedAgeEnable/mSupportedGenderEnable/mSupportedRaceEnable eg:00000111
            mSupportedAgeEnable = mSupportedFaceAttributesEnable && ((supportedFaceAttributesEnable & 0x01) == 0x01);
            mSupportedGenderEnable = mSupportedFaceAttributesEnable && ((supportedFaceAttributesEnable & 0x02) == 0x02);
            mSupportedRaceEnable = mSupportedFaceAttributesEnable && ((supportedFaceAttributesEnable & 0x04) == 0x04);
        }
    } catch (IllegalArgumentException e) {
        Log.i(TAG, "FaceAttributes TAG is not set in HAL:"+e);
        mSupportedFaceAttributesEnable = false;
    }
}

public static final Key<Byte> CONTROL_AVAILABLE_FACEFEATUREENABLE = new Key<Byte>("com.addParameters.availableFaceFeatureMask", Byte.class);
这个TAG是在哪里下发的？
vendor/sprd/modules/libcamera/include/SprdCamera3.h
{"availableFaceFeatureMask", TYPE_BYTE},

vendor/sprd/modules/libcamera/SprdCtrl.mk
1110 ifeq ($(strip $(TARGET_BOARD_CAMERA_FACE_DETECT)),true)
1111 ifeq ($(strip $(TARGET_BOARD_SPRD_FD_VERSION)),1)
1112 LOCAL_CFLAGS += -DCONFIG_SPRD_FD_LIB_VERSION_2
1113 else
1114 LOCAL_CFLAGS += -DCONFIG_SPRD_FD_LIB_VERSION_1
1115 endif
1116 endif


vendor/sprd/modules/libcamera/SprdLib.mk
22 ifeq ($(strip $(TARGET_BOARD_CAMERA_FACE_DETECT)),true)
23 LOCAL_SHARED_LIBRARIES += libsprdfa libsprdfdadapter
24 LOCAL_SHARED_LIBRARIES += libsprdfd_hw
25 ifeq ($(strip $(TARGET_BOARD_SPRD_FD_VERSION)),1)
26 LOCAL_SHARED_LIBRARIES += libsprdfarcnn
27 else
28 LOCAL_SHARED_LIBRARIES += libsprdfar
29 endif
30 endif


vendor/sprd/modules/libcamera/hal3_2v6/SprdCamera3Setting.cpp
3156  // Bit0 indicates whether or not to support Age.
3157  // Bit1 indicates whether or not to support Gender.
3158  // Bit2 indicates whether the skin is supported.
3159  #ifdef CONFIG_SPRD_FD_LIB_VERSION_2
3160      s_setting[cameraId].sprddefInfo.availabe_gender_race_age_enable = 7;
3161  #else
3162      s_setting[cameraId].sprddefInfo.availabe_gender_race_age_enable = 0;
3163  #endif


3615      staticInfo.update(
3616          ANDROID_SPRD_AVAILABLE_FACEAGEENABLE,
3617          &(s_setting[cameraId].sprddefInfo.availabe_gender_race_age_enable), 1);


vendor/sprd/modules/libcamera/include/SprdCamera3Tags.h
ANDROID_SPRD_AVAILABLE_FACEAGEENABLE,


build/soong/soong_ui.bash --dumpvar-mode TARGET_BOARD_SPRD_FD_VERSION
1


看来只改 md.mk 文件没用，还需要改下面这个文件
device/sprd/mpool/module/camera/msoc/qogirl6/qogirl6.mk
TARGET_BOARD_SPRD_FD_VERSION := 1


最终决定不修改 TARGET_BOARD_SPRD_FD_VERSION，直接修改 hal3_2v6/SprdCamera3Setting.cpp
s_setting[cameraId].sprddefInfo.availabe_gender_race_age_enable = 0;
```## 176601 人像光效拍照显示异常

```text
int lightPortraitValue = mDataModuleCurrent.getInt(Keys.KEY_LIGHT_PORTIAIT);

mCameraSettings.setLightPortraitType(lightPortraitValue);

requestSettings.set(ANDROID_SPRD_LIGHT_PORTRAIT_TYPE, mLightPortraitType);

139      public static final Key<Integer> ANDROID_SPRD_LIGHT_PORTRAIT_TYPE = new Key<Integer>(
140              "com.addParameters.sprdlightPortraitType", int.class);

SprdCamera3Tags.h
ANDROID_SPRD_LIGHTPORTRAITTYPE,

vendor/sprd/modules/libcamera/hal_common/multiCamera/SprdCamera3Portrait.cpp
2939      if (type == 0) {
2940          if (metaSettings.exists(ANDROID_SPRD_LIGHTPORTRAITTYPE)) {
2941              mPortrait->lightPortraitType =
2942                  metaSettings.find(ANDROID_SPRD_LIGHTPORTRAITTYPE).data.i32[0];
2943          }
2944          int rc = hwiMain->camera_ioctrl(CAMERA_IOCTRL_GET_BV, &cameraBV, NULL);
2945          rc = hwiMain->camera_ioctrl(CAMERA_IOCTRL_GET_ISO, &cameraISO, NULL);
2946          rc = hwiMain->camera_ioctrl(CAMERA_IOCTRL_GET_CT, &cameraCT, NULL);
2947          mBokehAlgo->setLightPortraitParam(cameraBV, cameraISO, cameraCT,
2948                                        mPortrait->lightPortraitType, isCapFrame);
2949          HAL_LOGV("cameraBV %d, cameraISO %d, cameraCT %d, lightPortraitType %d",
2950               cameraBV, cameraISO, cameraCT, mPortrait->lightPortraitType);


999  void SprdPortraitAlgo::setLightPortraitParam(int param1, int param2, int param3,
1000                                               int param4, bool isCap) {
1001      if (!isCap) {
1002          lptOptions.cameraBV = param1;
1003          lptOptions.cameraISO = param2;
1004          lptOptions.cameraCT = param3;
1005          lptOptions.lightPortraitType = param4;
1006      } else {
1007          lptOptions_cap.cameraBV = param1;
1008          lptOptions_cap.cameraISO = param2;
1009          lptOptions_cap.cameraCT = param3;
1010      }
1011  }


vendor/sprd/modules/libcamera/hal_common/multiCamera/SprdCamera3Portrait.cpp
2656          if (mPortrait->mPortraitFlag) {
2657              //check lpt status and trans diff lptmask
2658              if (lightPortraitType) {
2659                  mPortrait->mBokehAlgo->getPortraitMask(input_buf2_addr,
2660                  (void *)mPortrait->mScaleInfo.addr_vir.addr_y,
2661                  output_buf_addr, input_buf1_addr,
2662                  mPortrait->mVcmStepsFixed, mPortrait->bokehMask, mPortrait->lptMask);
2663                  HAL_LOGD(" getPortraitMask works");
2664              } else {
2665                  mPortrait->mBokehAlgo->getPortraitMask(input_buf2_addr,
2666                  (void *)mPortrait->mScaleInfo.addr_vir.addr_y,
2667                  output_buf_addr, input_buf1_addr,
2668                  mPortrait->mVcmStepsFixed, mPortrait->bokehMask, NULL);
2669                  HAL_LOGD(" getPortraitMask null");
2670              }
2671          }


2823          rc = mPortrait->mBokehAlgo->capLPT(output_buf_addr,
2824                                             mPortrait->mBokehSize.capture_w,
2825                                             mPortrait->mBokehSize.capture_h,
2826                                             mPortrait->lptMask, lightPortraitType);


2、拍yuv和depth图片
输入命令adb shell setprop persist.vendor.cam.raw.mode jpg
adb shell setprop persist.vendor.cam.bokeh.dump capdepth
手机进入双摄模式，点击拍照，即在/data/vendor/cameraserver下生成yuv和depth图供debug


查看拍出来的图片，发现入图好像没什么问题，出图就有问题了，是不是因为没有校准？
```## SPRD水印功能？

```text
device/sprd/mpool/module/camera/watermark/readme.txt

How to enable:
 1: Enable by MACRO in file BoardConfig.mk
    TARGET_BOARD_LOGOWATERMARK_SUPPORT := true
    TARGET_BOARD_TIMEWATERMARK_SUPPORT := true
 2: prepare watermark files(logo--*.rgba,time--time*.yuv), and set makefile
    #watermark, copy files to /vendor/logo/, eg:
       PRODUCT_COPY_FILES += \
           $(call md-overlayrsb,module/camera/watermark/logo_1000x200.rgba):$(TARGET_COPY_OUT_VENDOR)/logo/logo_1000x200.rgba \
           $(call md-overlayrsb,module/camera/watermark/logo_800x160.rgba):$(TARGET_COPY_OUT_VENDOR)/logo/logo_800x160.rgba \
           $(call md-overlayrsb,module/camera/watermark/logo_600x120.rgba):$(TARGET_COPY_OUT_VENDOR)/logo/logo_600x120.rgba \
           $(call md-overlayrsb,module/camera/watermark/logo_300x60.rgba):$(TARGET_COPY_OUT_VENDOR)/logo/logo_300x60.rgba \
           $(call md-overlayrsb,module/camera/watermark/logo_100x20.rgba):$(TARGET_COPY_OUT_VENDOR)/logo/logo_100x20.rgba \
           $(call md-overlayrsb,module/camera/watermark/time_vert_100x50x13.yuv):$(TARGET_COPY_OUT_VENDOR)/logo/time_vert_100x50x13.yuv \
           $(call md-overlayrsb,module/camera/watermark/time_vert_72x36x13.yuv):$(TARGET_COPY_OUT_VENDOR)/logo/time_vert_72x36x13.yuv \
           $(call md-overlayrsb,module/camera/watermark/time_vert_48x24x13.yuv):$(TARGET_COPY_OUT_VENDOR)/logo/time_vert_48x24x13.yuv \
           $(call md-overlayrsb,module/camera/watermark/time_vert_24x12x13.yuv):$(TARGET_COPY_OUT_VENDOR)/logo/time_vert_24x12x13.yuv
 3: change folder mode in *.rc file, or open files should be fail(androidR no need)
    chmod 755 /vendor/logo

more detal:
logo watermark:
    * add logo to the picture when capture.
    * logo source files should be *.rgba, you can try to convert *.png to *.rgba
      https://convertio.co/zh/rgba-converter/
    * you can prepare logo source files for each size of capture.
    * logo source files' width and height should at least align to 2
    * If you want to change name and size, please modify these code in file cmr_oem.c
      function:camera_select_logo,camera_get_logo_data, and PRODUCT_COPY_FILES in makefile

time watermark:
    * add timestamp to the picture when capture
    * the source file should named as the setting in cde file cmr_watermark.c, contain image
      of char "0123456789-: "(last one is space) in the source file.
      you can create time.png by pc-software as GIMP,Photoshop,and so on. contain the elements for timestamp.
    * Every elements should have the same width and height, and should at least align to 2
    * If you want to change, please modify these cod cmr_watermark.c,function:camera_get_time_yuv420,
      or camera_select_time_file
    * If you want small number for small capture size, you should modify the setting in camera_select_time_file
      open one yuv file for small size capture and change subnum_width and so on.

debug libcamera:
1: can debug watermark of libcamera code by set property
   1) push source files to phone
      adb root;adb remount;adb shell
      #make folder for source files
      cd /vendor/
      mkdir logo
      chown system:system logo
      exit
      #push source files to phone
      adb push *.rgba /vendor/logo/
      adb push time*.yuv /vendor/logo/
   2) set property,0:none;1:debug logo watermark;2: debug time watermark;3:both
      setprop debug.vendor.cam.watermark.test 1

sample:
vendor/sprd/modules/libcamera/oem2v6/src/cmr_watermark.c
logo watermark:setting (range mode, of course you can change as you like)
cmr_int camera_select_logo(sizeParam_t *size) {
    const sizeParam_t cap_logo[] = {
        /* capture width,height;logo:width,height;logo position in capture:posx,posy */
        {4000, 0, 1000, 200, 0, 0, 0, 0},
        {3000, 0, 800, 160, 0, 0, 0, 0},
        {2000, 0, 600, 120, 0, 0, 0, 0},
        {1000, 0, 300, 60, 0, 0, 0, 0},
        {500, 0, 100, 20, 0, 0, 0, 0}
        /* little than 500, capture too small to add watermark */
    };

time watermark:setting,
    cmr_int camera_select_time_file(struct time_src_tag *pt)
    const struct time_src_tag tb_time[] = {
        /* width, height, angle, subnum_width, subnum_height, file name */
        {4000, 0, 0, 100, 50, "time_vert_100x50x13.yuv"},
        {3000, 0, 0, 72, 36, "time_vert_72x36x13.yuv"},
        {1000, 0, 0, 48, 24, "time_vert_48x24x13.yuv"},
        {720, 0, 0, 24, 12, "time_vert_24x12x13.yuv"}
        /* less than 720, capture too small to add watermark */
    };

nn libcamoem

不同分辨率下水印大小不同，有时候时间水印会比logo水印还大？


水印log, tag: cmr_watermark
01-16 14:53:30.025   549 29839 I cmr_watermark: 808, watermark_add_yuv: watermark flag 3,[4000 2250]
01-16 14:53:30.025   549 29839 D cmr_watermark: 928, camera_select_logo: 2250, [600 120], logo_600x120.rgba
01-16 14:53:30.043   549 29839 I cmr_watermark: 275, sprd_fusion_yuv420_rgba: src[4000 2250], logo[3780 1650 120 600] angle[90 0]
01-16 14:53:30.046   549 29839 D cmr_watermark: 995, camera_select_time_file: 2250 [48 24] time_vert_48x24x13.rgba
01-16 14:53:30.046   549 29839 D cmr_watermark: 995, camera_select_time_file: 2250 [48 24] time_vert_48x24x13.rgba
01-16 14:53:30.047   549 29839 D cmr_watermark: 750, camera_get_time_data: done, 0xc9101800
01-16 14:53:30.048   549 29839 I cmr_watermark: 275, sprd_fusion_yuv420_rgba: src[4000 2250], logo[3952 1794 48 456] angle[90 0]
01-16 14:53:30.048   549 29839 D cmr_watermark: 890, watermark_add_yuv: X
```## DreamCamera2 App，shortcut中“慢动作”未翻译问题

```text
该问题是Android shortcut 动态加载的共性问题，是因为 DreamCamera2 App 的 shortcut 列表中的慢录采用的是动态加载方式导致的。同样的，如支付宝等三方 App 存在同样的问题。

① shortcut 动态加载是当 App 运行后进行加载的，未运行 App 打开 shortcut 列表，是无法加载到 shortcut 列表的。

②系统语言由中文切换为 English 后，由于没有重新打开 App 而直接去打开 shortcut，导致 shortcut 列表的慢录模块使用的还是中文（上一次打开 App 加载的）；先打开应用，再看shortcut，此时的 shortcut 列表会是英文显示

那为什么 DreamCamera2 App 的 shortcut 列表中的慢录要采用动态加载呢？主要是为了动态判断芯片平台是否支持慢录模式，如果支持，shortcut 会加载出 慢录模式，否则不加载。

如果确保芯片平台支持慢录（最少需要90帧，是否支持可质询 sensor 原厂fae），可考虑通过静态加载规避此问题

慢录 shortcut 静态加载参考case：
```## 9620平台如何适配camera相关宏开关？

```text
1.平台camera宏配置在9230和9620上有些许改动：

SOC级配置目录：
device/sprd/mpool/module/camera/msoc/qogirl6
通用配置文件：qogirl6.mk（包含宏开关）

Board级配置目录
device/sprd/qogirl6/ums9230_1h10/module/camera/

宏和属性主要配置文件：md.mk
camera sensor配置文件：sensor_config.xml
光学变焦配置文件：zoom_config.json
zoom_config.json文件非必需，如不存在则倍率使用sensor_drv_u.c中的默认值。

注意：相同的宏在mpool目录和Board目录可以配置不同的值，Board目录下的配置值优先级高于mpool目录下的配置值。

2.在sprdcamera3setting.cpp文件中初始化feature list的时候，某些feature的添加会调用resetFeatureStaus函数，如下图：

此时会判断feature switch的宏是否打开，若是打开状态，则不论添加的feature是否为on，都将会添加到feature list并且置为on，如下图所示：

此时若是想要关掉相应的宏则需要先关掉feature switch的宏：
vendor/sprd/modules/camera_core/config/default_prop.mk
#for camera ip feature MP test
PRODUCT_PROPERTY_OVERRIDES += \
persist.vendor.cam.ip.switch.on=0

vendor/sprd/modules/libcamera/camera_core/config/default_prop.mk
#for camera ip feature MP test
PRODUCT_PROPERTY_OVERRIDES += \
persist.vendor.cam.ip.switch.on=0
```## 如何查看是否检测到人脸以及检测到的人脸个数

```text
1.人脸检测log等级打开
adb shell setprop persist.vendor.fdtop.log 5

2.在抓取的log中搜索关键字 facedetect
log中face_num的值表示检测到的人脸数，如果为0表示未检测到人脸
```## 拍照之后查看照片大小只有0.1M

```text
是不是 Photos 的问题？因为在 Files 里面打开是 ok 的
```## 闪光灯模式下偏色问题

```text
1、DULA_FLASH->Tune V6/V7->Main flash En 作用为控制主闪时，是否进行AWB计算
勾选此参数时，主闪启用auto AWB算法（会增加拍照耗时）。
不勾选此参数时，使用Flash wb算法，即主闪沿用预闪AWB算法计算结果。
建议使用 auto AWB

2、cap_rgain和cap_bgain喜好色白平衡调试参数，类似于AWB preference。增大cap_rgain值，偏红。增大cap_bgain值，偏蓝。 DULA_FLASH->Tune V6/V7,默认值为1，建议在【0.9，1.1】范围调试

3、main_open_delay：抓帧的时机，默认值为5。过小可能会造成awb尚未迭代完成，有造成偏色的可能；参数值范围 [0 8],注意参数更改方向。
```## 50M是如何实现的？硬件上和软件上有什么要求？

## [FAQ202274848]超清模式拍照如何增加1:1，16:9画幅比

```text
目前平台仅支持超清模式下4：3的画幅比，根据sensor的支持能力，当切换到超清模式时，默认只有一个尺寸，且在设置列表无选项。本题将增加1：1和16：9的选项列表，供用户选择。
[ANSWER]
1.app侧修改部分：

diff --git a/res/values/dream_camera_arrays_photo_part.xml b/res/values/dream_camera_arrays_photo_part.xml

old mode 100644

new mode 100755

index 3706956d7..8b548b96d

--- a/res/values/dream_camera_arrays_photo_part.xml

+++ b/res/values/dream_camera_arrays_photo_part.xml

@@ -1081,6 +1081,7 @@

     <item>@string/pref_camera_gesture_recongition_key</item>

   </integer-array>

   <integer-array name="photo_back_mode_high_resolution_photo_setting_display">

+ <item>@string/pref_camera_picturesize_back_key</item>

     <item>@string/pref_camera_composition_line_key</item>

     <item>@string/pref_ai_detect_smile_key</item>

     <item>@string/pref_ai_detect_face_attributes_key</item>

@@ -1095,6 +1096,7 @@

     <item>@string/pre_ae_lock_key</item>

   </integer-array>

   <integer-array name="photo_front_mode_high_resolution_photo_setting_display">

+ <item>@string/pref_camera_picturesize_front_key</item>

     <item>@string/pref_camera_composition_line_key</item>

     <item>@string/pref_ai_detect_smile_key</item>

     <item>@string/pref_ai_detect_face_attributes_key</item>





diff --git a/src/com/android/camera/settings/ResolutionUtil.java b/src/com/android/camera/settings/ResolutionUtil.java

old mode 100644

new mode 100755

index ac20d037e..823b1df90

--- a/src/com/android/camera/settings/ResolutionUtil.java

+++ b/src/com/android/camera/settings/ResolutionUtil.java

@@ -83,10 +83,12 @@ public class ResolutionUtil {

       sDesiredAspectRatioSizes.add(new Size(4,3));

       sDesiredAspectRatioSizes.add(mFullScreenSize);

       sDesiredAspectRatioSizes.add(new Size(1,1));

+ sDesiredAspectRatioSizes.add(new Size(16,9));

 

       sDesiredAspectRatios.add(4.0f / 3.0f);

       sDesiredAspectRatios.add(mFullScreenSize.width() / (float) mFullScreenSize.height());

       sDesiredAspectRatios.add(1.0f / 1.0f);

+ sDesiredAspectRatios.add(16.0f / 9.0f);

       settled = true;

     }

   }



diff --git a/src/com/dream/camera/modules/highresolutionphoto/HighResolutionPhotoModule.java b/src/com/dream/camera/modules/highresolutionphoto/HighResolutionPhotoModule.java

old mode 100644

new mode 100755

index d6f56280f..a2f6b04ba

--- a/src/com/dream/camera/modules/highresolutionphoto/HighResolutionPhotoModule.java

+++ b/src/com/dream/camera/modules/highresolutionphoto/HighResolutionPhotoModule.java

@@ -98,12 +99,26 @@ public class HighResolutionPhotoModule extends PhotoModule {

         mAppController.getAndroidContext(),

         mCameraDevice.getCameraId(), supported);

 */

-    List<Size> supported = Size.convert(mCameraCapabilities

+

+    /*List<Size> supported = Size.convert(mCameraCapabilities

         .getSupportedPhotoSizes());

 

     Size pictureSize;

-

-    pictureSize = supported.get(0);

+    Log.d(TAG, "chenyun_highres supported " + supported);

+    pictureSize = supported.get(0);*/

+ OneCamera.Facing cameraFacing = isCameraFrontFacing() ? OneCamera.Facing.FRONT

+        : OneCamera.Facing.BACK;

+    Size pictureSize;

+    try {

+      pictureSize = mAppController.getResolutionSetting()

+          .getPictureSize(DataModuleManager.getInstance(mAppController.getAndroidContext()),

+              mAppController.getCameraProvider()

+                  .getCurrentCameraId(), cameraFacing);

+    } catch (OneCameraAccessException ex) {

+      mAppController.getFatalErrorHandler()

+          .onGenericCameraAccessFailure();

+      return;

+    }

     Log.d(TAG, "Picture size is " + pictureSize);

     mCameraSettings.setPhotoSize(pictureSize.toPortabilitySize());



2.HAL修改部分

具体根据超清模式支持多大的尺寸，则相应修改，以下以48M为例

/vendor/sprd/modules/libcamera/hal3_2v6/SprdCamera3Setting.cpp



int SprdCamera3Setting::getHighResCapSize(int32_t cameraId,

                     const struct img_size **pRet) {

--#define RES_SIZE_NUM 6

++#define RES_SIZE_NUM 8

  char prop[PROPERTY_VALUE_MAX] = {0};

  struct phySensorInfo *phyPtr = NULL;

  const struct img_size *pt = NULL;

  int i;

  struct HighResCapSizeTag {

    const char *pch;

    struct img_size res[RES_SIZE_NUM];

  };

  const static struct HighResCapSizeTag tb_res_cap[] = {

    /* sort: large --> little

     * property string, capture size, preview size, 0,0

     * last img_size must be{0, 0}

     */

    {"108M", {{11968, 9000}, {1440, 1080}, {0, 0}}}, /* 64M */

    {"64M", {{9216, 6912}, {1440, 1080}, {0, 0}}}, /* 64M */

--    {"48M", {{8000, 6000}, {1440, 1080}, {0, 0}}}, /* 48M */

++    {"48M", {{8000, 6000}, {1440, 1080}, {7936, 4464}, {1920, 1080}, {5952, 5952}, {1072, 1072},{0, 0}}}, /* 48M */

    {"32M", {{6528, 4896}, {1440, 1080}, {0, 0}}}, /* 32M */

    {"24M", {{5664, 4248}, {1440, 1080}, {0, 0}}}, /* 24M */

    {"16M", {{4608, 3456}, {1440, 1080}, {0, 0}}}, /* 16M */

  };
```## adb install 命令安装 DreamCamera2 apk，点开其全景模式，相机闪退问题

```text
查看log发现， 存在全景模式算法库加载错误：
E Mosaic : Load the library dream mosaic is error!!!
因为adb install 命令安装应用程序后，程序只能访问data/data/${程序包名}下的数据，无法访问system目录；而全景算法库存放的路径是system_ext/lib64（64位机器）
因此需要以adb push命令将DreamCamera2 apk放到system_ext/app/DreamCamera2文件夹下才有权限加载全景算法库，并正常使用其全景模式。
```## 如何关闭相机进入或退出动画

```text
路径：frameworks/base/core/res/res/values/config_ex.xml
找到 name="config_anim_app_exit" 和 name="config_anim_app_start"

如需关闭动画，添加如下设置：
<item>com.android.camera2,0,-1,-1</item>

第1个参数：包名
第2个参数：打开或关闭动画，-1 不设置， 0 关闭
第3个参数：动画时长， -1 不设置
第4个参数：透明度， -1 不设置， 0 关闭
```## 如何判断拍照帧的metadata具体值

```text
通过在camera service截取capture请求的request参数，解析出想要的metadata，下面的代码以metadata值ANDROID_SPRD_FLASH_LCD_MODE为例，获取他在拍照帧中的下发值
frameworks\av\services\camera\libcameraservice\device3\Camera3Device.cpp
status_t Camera3Device::submitRequestsHelper(
 if (repeating) {
    res = mRequestThread->setRepeatingRequests(requestList, lastFrameNumber);
  } else {
+++ for (List<sp<CaptureRequest> >::iterator it = requestList.begin(); it != requestList.end();
+++  ++it) {
+++ CameraMetadata &metadata = (*it)->mSettingsList.begin()->metadata;
+++ camera_metadata_entry flash_lcd_mode = metadata.find(ANDROID_SPRD_FLASH_LCD_MODE);
+++ if(flash_lcd_mode.count > 0){
+++ ALOGE("%s: leo find flash lcd mode %d in capture request", __FUNCTION__,
+++          flash_lcd_mode.data.u8[0]);
+++ }
+++  }
res = mRequestThread->queueRequestList(requestList, lastFrameNumber);
  }
```## app增加trace监控，完善systrace上的分析信息

```text
如下方式增加代码
import android.os.Trace;

Trace.beginSection("set your TAG here");
the code you want to monitor
Trace.endSection();
```## 如何让user版本软件拍出来的照片有完整的3A exif信息

```text
调试相机效果时，照片的3A exif信息是非常重要的参数。展锐平台默认只有debug版本软件拍照才会保存3A exif信息。如果需要让user软件拍下的照片也保存3A exif信息，则需要修改代码，这样不管是debug版本软件还是user版本软件，都能将照片的3A exif信息编码到照片中。

代码修改如下：
diff --git a/hal3_2v1/SprdCamera3OEMIf.cpp b/hal3_2v1/SprdCamera3OEMIf.cpp
index 33d29ad..0b8ff91 100644
--- a/hal3_2v1/SprdCamera3OEMIf.cpp
+++ b/hal3_2v1/SprdCamera3OEMIf.cpp
@@ -4974,8 +4974,8 @@ void SprdCamera3OEMIf::receiveJpegPicture(struct camera_frame_type *frame) {
         maxJpegSize = heap_size;
     }

-    property_get("ro.debuggable", value, "0");
-    if (!strcmp(value, "1")) {
+//    property_get("ro.debuggable", value, "0");
+//    if (!strcmp(value, "1")) {
         // add isp debug info for userdebug version
         ret = mHalOem->ops->camera_get_isp_info(mCameraHandle, &ispInfoAddr,
                                                 &ispInfoSize);
@@ -4999,7 +4999,7 @@ void SprdCamera3OEMIf::receiveJpegPicture(struct camera_frame_type *frame) {
                                          encInfo->size + ispInfoSize,
                                          mCaptureWidth, mCaptureHeight);
         }
-    }
+//    }
     jpegBlob = (camera3_jpeg_blob *)((char *)pic_addr_vir +
                                      (maxJpegSize - sizeof(camera3_jpeg_blob)));
android10版本对应文件路径是： vendor/sprd/modules/libcamera/hal3_2v6/SprdCamera3OEMIf.cpp ，上面修改也是有效的。
这样修改后，user版本软件拍出来的照片也能保存3A exif信息啦。
```## 为什么播放Camera录像的时候开始有1S无声?

```text
平台针对拍照将录音音效录进去的问题做了数据前半部分的mute处理，才会1S无声 
可以修改以下audio_hw.c/Threads.cpp中的内容800ms 无声修改为100ms

vendor/sprd/modules/audio/vendor/whale/audio_hw.c:
  --#define RECORD_POP_MIN_TIME_CAM 800 //ms
  ++#define RECORD_POP_MIN_TIME_CAM 100 //ms

frameworks/av/services/audioflinger/Threads.cpp:
  --#define RECORD_MUTE_MIN_TIME_CAM 800 //ms
  ++#define RECORD_MUTE_MIN_TIME_CAM 100 //ms
```## 当前平台camera2接口设置SENSOR_SENSITIVITY 的值范围是多少？

```text
public static final Key<Integer> SENSOR_SENSITIVITY = new Key<Integer>("android.sensor.sensitivity", int.class);
对于下发 SENSOR_SENSITIVITY，使用的参数传值可以是 0 100 200 400 800 1600
```## 如何去掉安全相机的启动背景(有相机图标的灰色背景)？

```text
从锁屏界面启动相机(通过双击power/volume up或keyguard右下角滑动)时，为了有一个从keyguard到camera的过度效果，让人看起来不那么突兀，启动过程中会先显示一个带有相机图标的灰色背景，待keyguard准备好退去后此背景便消失。这个背景可能会延缓打开相机的速度。若要关掉此背景，可以按照如下修改代码：

SystemUI/src/com/android/systemui/statusbar/KeyguardAffordanceView.java
179      public void setPreviewView(View v) {
180          if (mPreviewView == v) {
181              return;
182          }
/*注释掉下面代码
183          View oldPreviewView = mPreviewView;
184          mPreviewView = v;
185          if (mPreviewView != null) {
186              mPreviewView.setVisibility(mLaunchingAffordance
187                      ? oldPreviewView.getVisibility() : INVISIBLE);
188          }
189      }
190  
*/
```## 录像的整个流程过程

```text
录像的整个流程过程如下：
Line 164803: M024D6B 01-04 10:10:27.982 5833 5833 I CAM_VideoModule: onShutterButtonClick --点击录像键
Line 164805: M024D6D 01-04 10:10:27.986 5833 5833 I CAM_VideoModule: startVideoRecording: Thread[main,5,main] --开始录像
Line 165081: M024E81 01-04 10:10:28.329 5833 6106 V CAM_VideoModule: New video filename: /storage/emulated/0/DCIM/Camera/VID_20220104_101028.mp4 --创建录像文件
Line 170818: M0264D0 01-04 10:10:33.492 5833 5833 I CAM_VideoModule: Video snapshot start   --录像过程中点击拍照键，开始拍照
Line 171433: M026737 01-04 10:10:34.157 5833 7869 I CAM_VideoModule: Video snapshot taken.  --录像过程中拍照结束
Line 171473: M02675F 01-04 10:10:34.209 5833 7869 I CAM_VideoModule: storeImage end!     --照片存储
Line 185466: M029D2C 01-04 10:10:46.984 5833 5833 I CAM_VideoModule: onShutterButtonClick  --再次点击录像键(关闭录像)
Line 185466: M029D2D 01-04 10:10:46.985 5833 5833 I CAM_VideoModule: stopVideoRecording  --停止录像

排查错误的时候
(1)可以先搜 log "startVideoRecording|Video snapshot start|Video snapshot taken|stopVideoRecording"找到录像过程的开始和结尾行，将此过程的log全部复制出来。
(2)再复制出来的log基础上，搜log "Cam3HWI|cmr_grab|cmr_oem|Cam3OEMIF|cmr_snp|CAM2A|CAM_VideoModule"
以上log是排查是否是hal层的问题，重点关注Cam3OEMIF log中的参数设置
(3)如果搜索到“Skip stopVideoRecording since snapshot in progress”等信息，可以先让app同事看下，注:此错误log信息只有在录像过程中拍照出现。
```## DreamCamera2 app全景模式，纯色背景无法拍照或拍照卡顿问题

```text
展锐平台全景算法，在纯色背景无法合成照片原因如下：
a)由于现在算法仅通过帧与帧之间的特征点来判断合成，纯色背景下无法识别出足够的特征点，因此算法无法合成图片，生成偏移；
b)当前全景算法没有结合gyro信息来判断用户的移动情况，并且一般手机也没有配置gyro sensor，因此无法在纯色背景下判断用户的移动情况并生成有效偏移。
```## 退出相机时 听到马达撞击声

```text
Camera退出时，使VCM的驱动电流逐步降低，马达分步回到code为0的位置(在退出 camera 时，马达分两个步骤回到 code 为 0 的位置，先以 Quit_max_step 大步跳到 anti_noise_pos 的位置，然后以Quit_step 小步跳到 lens_mc_min 的位置，最后回到 code 为 0 的位置)。

1，对模组进行线性度测试

2，修改 softlanding参数
anti_noise_pos：（lens_mc_min *7 + lens_mc_max ）>>3
Quit_max_step：(otp_macro otp_inf ) >>1
Quit_step：25
Quit_sleep：12

3，修改lens_mc_min参数，降低lens_mc_min参数值
```## 前摄不带对焦功能，怎么去除对焦圆圈？

```text
在 camera 为前摄的时候，去掉对焦区域和自动对焦。
PhotoModule.java
    private void initializeCapabilities() {
        mCameraCapabilities = mCameraDevice.getCapabilities();
        mFocusAreaSupported = mCameraCapabilities
                .supports(CameraCapabilities.Feature.FOCUS_AREA);
        mMeteringAreaSupported = mCameraCapabilities
                .supports(CameraCapabilities.Feature.METERING_AREA);
        mAeLockSupported = mCameraCapabilities
                .supports(CameraCapabilities.Feature.AUTO_EXPOSURE_LOCK);
        mAwbLockSupported = mCameraCapabilities
                .supports(CameraCapabilities.Feature.AUTO_WHITE_BALANCE_LOCK);
        mContinuousFocusSupported = mCameraCapabilities
                .supports(CameraCapabilities.FocusMode.CONTINUOUS_PICTURE);
 +     if(mCameraId==1){
 +        mFocusAreaSupported=false;
 +        mContinuousFocusSupported=false;
 +     }
```## camera模块发现ion内存泄漏如何分析

```text
E Cam3OEMIf: 3148, freeAllCameraMem: ION/GPU buffer memory leak!!!//camera ion泄漏会有此log打印

debug版本camera ion内存分配和释放都会打印如下，然后参照fd，可确认哪个fd分配未释放，然后再对照代码查看配置以及释放逻辑那里存在问题即可
M017D05  05-18 15:38:24.741   452  5101 D Cam3OEMIf: 3034, allocCameraMem: fd=0x23, phys_addr=0x0, virt_addr=0xf217a000, size=0x31000, heap=0xf3511920, TotalIonSize=128053248
M01A526  05-18 15:38:32.241   452   752 D Cam3OEMIf: 3053, freeCameraMem: fd=0x23, phys_addr=0x0, virt_addr=0xf217a000, size=0x31000, heap=0xf3511920, TotalIonSize=128774144


例如之前分析一个问题发现，如下五个zsl buffer未释放
017AB8  05-18 15:38:24.666   452  5101 D Cam3OEMIf: 3034, allocCameraMem: fd=0x19, phys_addr=0x0, virt_addr=0xe2a81000, size=0x112b000, heap=0xf3511140, TotalIonSize=55844864
M017ADC  05-18 15:38:24.685   452  5101 D Cam3OEMIf: 3034, allocCameraMem: fd=0x1b, phys_addr=0x0, virt_addr=0xe1956000, size=0x112b000, heap=0xf35112f0, TotalIonSize=73846784
M017AF6  05-18 15:38:24.692   452  5101 D Cam3OEMIf: 3034, allocCameraMem: fd=0x1d, phys_addr=0x0, virt_addr=0xe082b000, size=0x112b000, heap=0xf3511470, TotalIonSize=91848704
M017B01  05-18 15:38:24.699   452  5101 D Cam3OEMIf: 3034, allocCameraMem: fd=0x1f, phys_addr=0x0, virt_addr=0xdf700000, size=0x112b000, heap=0xf3511170, TotalIonSize=109850624
M017B15  05-18 15:38:24.709   452  5101 D Cam3OEMIf: 3034, allocCameraMem: fd=0x21, phys_addr=0x0, virt_addr=0xde5d5000, size=0x112b000, heap=0xf3511770, TotalIonSize=127852544
其他对应fd都已释放

然后顺着log查看zslbuffer逻辑，以及释放逻辑，
vendor/sprd/modules/libcamera/hal3_2v6/SprdCamera3OEMIf.cpp
8861  int SprdCamera3OEMIf::Callback_ZslMalloc(cmr_u32 size, cmr_u32 sum,
8862                                           cmr_uint *phy_addr, cmr_uint *vir_addr,
8863                                           cmr_s32 *fd) {
8864      sprd_camera_memory_t *memory = NULL;
8865      cmr_int i = 0;
8866      int ret;
8867      SPRD_DEF_Tag *sprddefInfo;
8868      int BufferCount = kZslBufferCount;
8869  
8870      sprddefInfo = mSetting->getSPRDDEFTagPTR();
8871      if (sprddefInfo->slowmotion <= 1)
8872          BufferCount = 8;
8873  
8874      HAL_LOGD("size %d sum %d mZslHeapNum %d, BufferCount %d", size, sum,
8875               mZslHeapNum, BufferCount);
8876  
8877      *phy_addr = 0;
8878      *vir_addr = 0;
8879      *fd = 0;
8880  
8881      if (mSprd3dnrType == CAMERA_3DNR_TYPE_PREV_HW_CAP_SW ||
8882          (sprddefInfo->sprd_appmode_id == CAMERA_MODE_AUTO_PHOTO)|| (getMultiCameraMode() == MODE_BOKEH && mCameraId == mMasterId)
8883           || getMultiCameraMode() == MODE_BLUR) {
8884          ret = allocCameraMemForGpu(size, sum, phy_addr, vir_addr, fd);
8885          return ret;
8886      }

然后根据log发现务此处无allocCameraMemForGpu,却有 freeCameraMemForGpu而且报错，说明刚进入时候的判断条件与退出时候发生变化，导致未调用下面之前freeCameraMem释放内存，分析发现appmode在打开相机与关闭相机设置不一致，导致分配与释放接口不一致，导致内存泄漏

8833  int SprdCamera3OEMIf::Callback_ZslFree(cmr_uint *phy_addr, cmr_uint *vir_addr,
8834                                         cmr_s32 *fd, cmr_u32 sum) {
8835      cmr_u32 i;
8836      Mutex::Autolock l(&mPrevBufLock);
8837      Mutex::Autolock zsllock(&mZslBufLock);
8838      SPRD_DEF_Tag *sprddefInfo;
8839      sprddefInfo = mSetting->getSPRDDEFTagPTR();
8840  
8841      if (mSprd3dnrType == CAMERA_3DNR_TYPE_PREV_HW_CAP_SW ||
8842          sprddefInfo->sprd_appmode_id == CAMERA_MODE_AUTO_PHOTO||(getMultiCameraMode() == MODE_BOKEH && mCameraId == mMasterId)
8843           || getMultiCameraMode() == MODE_BLUR) {
8844          freeCameraMemForGpu(phy_addr, vir_addr, fd, sum);
8845          return 0;
8846      }
8847      HAL_LOGD("mZslHeapNum %d sum %d", mZslHeapNum, sum);
8848      for (i = 0; i < mZslHeapNum; i++) {
8849          if (NULL != mZslHeapArray[i]) {
8850              freeCameraMem(mZslHeapArray[i]);
8851          }
8852          mZslHeapArray[i] = NULL;
8853      }
8854  
8855      mZslHeapNum = 0;
8856      releaseZSLQueue();
8857  
8858      return 0;
8859  }
```## 相机在录像过程中将按键提示音录进视频当中

```text
1.录像过程中将手动对焦的声音录进视频

FocusOverlayManager  updateFocusFinsh方法   取消录像过程中的对焦声音

                 mFocusRing.startActiveFocusedFocus();
                 if (mFocusArea != null) {

                     if (mAppController.isPlaySoundEnable()) {
-                        mCameraSound.play(MediaActionSound.FOCUS_COMPLETE);
+                        if (!(mListener instanceof VideoModule && ((VideoModule) mListener).isRecording())) {
+                            mCameraSound.play(MediaActionSound.FOCUS_COMPLETE);
+                        }
                     }
                 } else {
                     mFocusRing.centerFocusLocation();

2.录像过程中将开始录像的提示音录进视频

在开始录像之前加适当延时，确保开始录像在声音释放之后
  +++ b/src/com/android/camera/VideoModule.java
@@ -2810,6 +2810,13 @@ public class VideoModule extends CameraModule implements
                     // Fix bug 540246 recording and music work together after we end call
                     mActivity.sendBroadcast(new Intent(PAUSE_ACTION));
                 }

+                try {
+                    Thread.sleep(600);
+                } catch (Exception e){
+                    e.printStackTrace();
+                }

                 /*}@*/
 //                if (useNewApi() && mShutterSoundEnable) {
 //                    if (mCameraSound != null) {

3.录像过程将拍照和暂停的按键提示音录进视频

取消录像过程中拍照和暂停键的提示音
android:soundEffectsEnabled="false"
--- a/idh.code/vendor/sprd/platform/packages/apps/DreamCamera2/res/layout/dream_bottom_bar_contents.xml
+++ b/idh.code/vendor/sprd/platform/packages/apps/DreamCamera2/res/layout/dream_bottom_bar_contents.xml
@@ -38,6 +38,7 @@
 android:background="#ff0000" -->
             <com.android.camera.ui.RotateImageView
                 android:id="@+id/video_capture_button"
+               android:soundEffectsEnabled="false"
                 android:layout_width="48dp"
                 android:layout_height="48dp"
                 android:layout_gravity="center"
@@ -112,6 +113,7 @@ android:background="#ff0000" -->
 
             <com.android.camera.ui.RotateImageView
                 android:id="@+id/btn_video_pause"
+               android:soundEffectsEnabled="false"
                 android:layout_width="48dp"
                 android:layout_height="48dp"
                 android:layout_gravity="center"
```## 设置中的wifi扫描二维码界面，进入后返回，下拉菜单中的手电筒无法使用

```text
此问题为退出了wifi的扫码界面后，camera资源没有得到释放导致手电筒一直被camera占用，无法通过其他方式（下拉通知栏内）进行手电筒的开启操作
解决方法就是在camera.stop(）之后，立即进行camera资源的释放
修改文件位置packages\apps\Settings\src\com\android\settings\wifi\dpp\WifiDppQrCodeScannerFragment.java

+ private void releaseCamera() {
+            mCamera.release();
+            mCamera = null;
+    }
 private void destroyCamera() {
        if (mCamera != null) {
            mCamera.stop();
+           releaseCamera();
            mCamera = null;
        }

修改文件位置packages\apps\Settings\src\com\android\settings\wifi\qrcode\QrCamera.java

+ public void release() {
+       mCamera.setPreviewCallback(null);
+       mCamera.release();
+    }
```## Android 字体大小（fontScale）不随系统设置变化

```text
import android.app.Activity;
import android.content.Context;
import android.content.res.Configuration;

public class BaseActivity extends Activity {
    @Override
    protected void attachBaseContext(Context context) {
        Configuration configuration = context.getResources().getConfiguration();
        configuration.fontScale = 1;
        configuration.densityDpi = android.os.SystemProperties.getInt("ro.sf.lcd_density", 280);
        super.attachBaseContext(context.createConfigurationContext(configuration));
    }
}

错误方法
在Activity中重写 getResources() 方法。

此方法是错误的。

在页面中修改字体缩放的配置，应该在页面获取上下文Context时，修改页面上下文的配置Configuration。

getResources() 方法，会在页面获取资源时多次调用，比如用手点一下页面任意位置，就会多次调用此函数。在此处修改配置是不符合逻辑的。

此外，Resources.updateConfiguration() 方法，已经废弃了，不应该再使用。
@Override
public Resources getResources() {
    Resources resources = super.getResources();
    Configuration configuration = resources.getConfiguration();
    // 设置字体大小不随系统设置变化。字体大小（字体比例）始终设置为默认值
    if (configuration.fontScale != 1) { // 字体大小（字体比例）为非默认值
        configuration.fontScale = 1; // 字体大小（字体比例）设置为默认值
        resources.updateConfiguration(configuration, resources.getDisplayMetrics());
    }
    return resources;
}
```## 边缘计算

```text
边缘计算指的是一种附加到数据生成位置的技术，即在架构的边缘：它允许在数据收集的位置（或更接近的位置）处理和分析数据，而不是云或数据中心。计算机视觉项目越来越多地实施边缘计算架构，因为它解决了网络可访问性、带宽和延迟问题。由于隐私、稳健性和性能，即使是云架构也经常需要部署在边缘设备上。边缘计算在需要实时数据处理的项目中特别受欢迎。此类项目包括自动驾驶汽车、无人机等。
```##
