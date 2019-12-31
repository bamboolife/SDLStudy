## Android版SDL2.0编译

### 什么是SDL？
SDL（Simple DirectMedia Layer）是一套开放源代码的跨平台多媒体开发库，使用C语言写成。SDL提供了数种控制图像、声音、输出入的函数，让开发者只要用相同或是相似的代码就可以开发出跨多个平台（Linux、Windows、Mac OS X等）的应用软件。目前SDL多用于开发游戏、模拟器、媒体播放器等多媒体应用领域。
### SDL能做什么？
#### Video（视频）
- 3D graphics:(3D图形)
    - SDL可以与OpenGL API或Direct3D API结合使用以实现3D图形 
- Accelerated 2D render API:(加速2D渲染API)
    - 支持简单的rotation、scaling和alpha的混合，所有这些均使用现代3D API加速
    - 使用OpenGL和Direct3D支持加速，并且存在软件后备
    - 创建和管理多个窗口
#### Input Events(输入事件)
- Events and API functions provided for:(提供的事件和API函数)
    - Application and window state changes（应用程序和窗口状态改变）
    - Mouse input（鼠标输入）
    - Keyboard input（键盘输入）
    - Joystick and game controller input（游戏杆和游戏控制器输入）
    - Multitouch gestures（多点触控手势）
- 可以使用SDL_EventState()启用或禁用每个事件
- 事件在发布到内部事件队列之前通过用户指定的过滤器功能传递
- 线程安全的事件队列
#### Force Feedback
- Windows，Mac OS X和Linux支持强制反馈
#### Audio（音频）
- 如果硬件不支持该格式，则设置8位和16位音频，单声道立体声或5.1环绕声的音频播放，并进行可选转换
- 音频在单独的线程中独立运行，并通过用户回调机制进行填充
- 专为定制软件音频混音器而设计，但SDL_mixer提供了完整的音频/音乐输出库
#### File I/O Abstraction
- 用于打开，读取和写入数据的通用抽象
- 内置对文件和内存的支持
#### Shared Object Support(共享对象的支持)
- 加载共享对象（Windows上的DLL，Mac OS X上的.dylib，Linux上的.so
- 共享对象中的查找功能
#### Threads
- 简单的线程创建API
- 简单线程本地存储API
- 互斥量，信号量和条件变量
- 无锁编程的原子操作
#### Timers(计时器)
- 获取经过的毫秒数
- 等待指定的毫秒数
- 创建在单独的线程中与代码一起运行的计时器
- 使用高分辨率计数器进行性能分析
#### CPU功能检测
- 查询CPU数量
- 检测CPU功能和支持的指令集
#### Endian独立
- 检测当前系统的字节序
- 快速交换数据值的例程
- 读取和写入指定字节序的数据
#### 电源管理
查询电源管理状态
### 编译SDL前的准备
1. 下载源码
[官方下载地址](https://www.libsdl.org/download-2.0.php)

源码目录

![image](source_list.png)
2. 配置环境

- 下载jdk1.8、Android studio3.5 ndk>=8 
- 配置环境变量
```
PATH="/usr/src/android-ndk-r8c:$PATH"                   # for 'ndk-build'
PATH="/usr/src/android-sdk/tools:$PATH"                 # for 'android'
PATH="/usr/src/android-sdk/platform-tools:$PATH"        # for 'adb'
export ANDROID_HOME="/usr/src/android-sdk"              # for gradle
export ANDROID_NDK_HOME="/usr/src/android-ndk-rXX"      # for gradle
```
- 进入源码目录 /SDL2/build-scripts执行脚本命令：
```
./androidbuild.sh org.libsdl.testgles ../test/testgles.c
```
>说明：org.libsdl.testgles是一个包名，可以随意替换成其他的包名。命令执行完会生成一个Android项目

![image](sdl_project.png)

会在SDL的当前目录生成一个build文件夹，然如进入/SDL2/build/org.libsdl.testgles/文件夹
<br>如果SDL<=2.0.7  执行`ant debug install`
<br>如果SDL>=2.0.8  执行`./gradlew installDebug`
<br>执行命令后，只需要等待片刻，就编译完成了。编译完成把项目导入Android studio运行

![image](share_lib.png)

