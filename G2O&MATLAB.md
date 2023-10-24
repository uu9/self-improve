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
    make -j12  
    sudo make install
