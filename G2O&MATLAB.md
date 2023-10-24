# Ubuntu改源
https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu/  
替换/etc/apt/sources.list内容   

    sudo apt update


# 1、安装G2O
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

# 3、编译库文件

# 4、MATLAB调用库文件
