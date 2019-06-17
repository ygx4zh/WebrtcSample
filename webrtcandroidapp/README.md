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

2. 使用https://appr.tc测试
    * 使用PC端浏览器访问https://appr.tc, Android端安装AppRTCMobile.apk, 然后两个端加入同一个房间, 可实现视频对讲则表示正常
    * 测试时PC端和Android端都需要翻墙, 如果使用Shadowsocks, 安卓点[Shadowsocks-android](https://github.com/shadowsocks/shadowsocks-android/releases)下载

3. docker搭建apprtc server测试:
    * 搭建参考: https://blog.piasy.com/2017/06/17/out-of-the-box-webrtc-dev-env/index.html
    * constants.py示例: ./apprtc server/constants.py
    * 镜像启动: 其中 server public IP 填写docker的IP, 可以通过电脑开启热点, 手机连接电脑热点, AppRTC里填docker的IP, 可以实现手机连接docker内的apprtc server进行测试
        
            docker run --rm \
            -p 8080:8080 -p 8089:8089 -p 3478:3478 -p 3478:3478/udp -p 3033:3033 \
            --expose=59000-65000 \
            -e PUBLIC_IP=<server public IP> \
            -v <path to constants.py>:/apprtc_configs \
            -t -i piasy/apprtc-server
 