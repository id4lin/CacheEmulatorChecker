#      								严禁用于商业牟利


# 本库目标

1 检测是否模拟器
2 获取相对真实的IMEI AndroidId 序列号 MAc地址等

#### 检测是否模拟器原理  [ Android模拟器识别技术](http://www.jianshu.com/p/1db610cc8b84) 

ARM与PC的X86在架构上有很大区别，ARM采用的哈弗架构将指令存储跟数据存储分开，与之对应的，ARM的一级缓存分为I-Cache（指令缓存）与D-Cahce（数据缓存），而X86只有一块缓存，如果我们将一段代码可执行代码动态映射到内存，在执行的时候，X86架构上是可以修改这部分代码的，而ARM的I-Cache可以看做是只读，因为，当我们往PC对应的地址写指令的时候，其实是往D-Cahce写，而I-Cache中的指令并未被更新，这样，两端程序就会在ARM与x86上有不同的表现，根据计算结果便可以知道究竟是还在哪个平台上运行。但是，无论是x86还是ARM，只要是静态编译的程序，都没有**修改代码段**的权限，所以，首先需要将上面的汇编代码翻译成可执行文件，再需要申请一块内存，将可执行代码段映射过去，执行。

 原文链接 [ Android模拟器识别技术](http://www.jianshu.com/p/1db610cc8b84) 

#### 2获取真实的Android设备信息 

* 可以采用一些系统隐藏的接口来获取设备信息，隐藏的接口不太容易被篡改，因为可能或导致整个系统运行不正常
* 可以自己通过Binder通信的方式向服务请求信息，比如IMEI号，就是想Phone服务发送请求获取的，当然如果Phone服务中的Java类被Hook，那么这种方式也是获取不到正确的信息的
* 可以采用Native方式获取设备信息，这种哦方式可以有效的避免被Xposed Hook，不过其实仍然可以被adbi 在本地层Hook。

#### 8.0之后，序列号的获取跟IMEI权限绑定，如果不授权电话权限，同样获取不到序列号


#### 10.0之后，序列号、IMEI 非系统APP获取不到
