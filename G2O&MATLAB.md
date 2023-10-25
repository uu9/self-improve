# 版本信息
MATLAB 2022a  
G2O Commit 42026db  
https://github.com/uu9/things/blob/main/src/g2o-master.zip

# Ubuntu改源
https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu/  
替换/etc/apt/sources.list内容   

    sudo apt update


# 1、安装G2O
直接使用G2O Commit 42026db或者下新版本    
https://github.com/RainerKuemmerle/g2o

    sudo apt install cmake libeigen3-dev  
    (可选) sudo apt install libspdlog-dev libsuitesparse-dev qtdeclarative5-dev qt5-qmake libqglviewer-dev-qt5  
    sudo apt install build-essential  
    
    cd path_to_g2o  
    mkdir build  
    cd build  
    cmake ..  
    make -j6  
    sudo make install

跑一下示例p0_phase_1  
https://github.com/uu9/things/blob/main/src/p0_phase_1.zip  

# 2、安装MATLAB
快捷键更改在：预设-MATLAB-Keyboard-Shortcuts-Active Settings  

# 3、编译库文件
跑一下示例p0_phase_2  
https://github.com/uu9/things/blob/main/src/p0_phase_2.zip  
注意，主要区别在于CMakeLists.txt文件，如果需要和MATLAB通信，那么接口需要规定成C风格而不是C++风格的  
使用指针保存矩阵，在数组中按照先行后列储存  

# 4、MATLAB调用库文件
由于MATLAB自带的libstdc++.so.6没有GLIBCXX_3.4.29，因此需要更新  
    
    (可选) locate libstdc++.so.6

应该可以看到在path_to_matlab/sys/os/glnxa64下有一个libstdc++.so.6，备份更新

    cd path_to_matlab/sys/os/glnxa64
    mv libstdc++.so.6 libstdc++.so.6.bak
    ln -s /usr/lib/x86_64-linux-gnu/libstdc++.so.6 .
    
将编译的库文件复制到p0_phase_3根目录，跑一下示例p0_phase_3应该可以正常调用G2O得到结果了  
https://github.com/uu9/things/blob/main/src/p0_phase_3.zip  

如果没有结果有一些命令可以提供一些帮助  
注意：在MATLAB中执行

    查看函数是否存在于符号表
    system("nm -D 库文件名.so | grep 函数名")

    查看库链接情况
    system("ldd 库文件名.so")

这个示例所使用的G2O模块比较单一，如果使用的功能更加复杂可能发现找不到动态链接库(so)的情况，可以手动链接  

    (可选) 查看当前已经加载的库
    cd path_to_matlab/bin/glnxa64
    ls | grep libg2o

    (可选) 查看G2O so文件
    cd /usr/lib/local
    ls | grep libg2o

    创建其他so文件软链接
    ln -s /usr/lib/local/libg2o* path_to_matlab/bin/glnxa64

G2O安装默认位置信息，可以在G2O的build目录下找到  
https://github.com/uu9/things/blob/main/src/G2O_install_manifest.txt
