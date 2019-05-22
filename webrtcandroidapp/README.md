# AppRTCMobile

#### 介绍
从谷歌Webrtc源码中抽取出来的AppRTCMobile, 用于测试编译出来的so包和jar包是否可以正常使用

#### 软件架构

libs/autobanh.jar, 从Webrtc源码/src/examples/androidapp/thrid_party/lib 中找到
libs/libwebrtc.jar, 编译出来后生成的webrtc_android jar包,
    编译后生成的目录在Webrtc源码/src/out/Debug/lib.java/sdk/android/libwebrtc.jar
    源代码在 Webrtc源码/src/sdk/android/src/java 下

src/main/jniLibs/xx/libjingle_peerconnection_so.so, 编译后生成的so包,
    编译后的路径在Webrtc源码/src/out/Debug/libjingle_peerconnection_so.so

build.gradle中的targetSdkVersion需要指定为 21, 因为项目未适配动态权限申请; 高于21后呼叫时会有吐司提示权限错误;

#### 使用说明

1. 测试时将编译出来的so包和jar替换, 即可进行安装测试
2. 使用PC端浏览器访问https://appr.tc, Android端安装AppRTCMobile.apk, 然后两个端加入同一个房间, 可实现视频对讲则表示正常
3. 测试时PC端和Android端都需要翻墙, 如果使用Shadowsocks, 安卓点[Shadowsocks-android](https://github.com/shadowsocks/shadowsocks-android/releases)下载
