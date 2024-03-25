MATLAB直接参考这篇文章  
https://blog.csdn.net/qq_15950515/article/details/122991780  
就是下一个字体放到<MATLAB安装路径>\sys\java\jre\win64\jre\lib\fonts  

Matplotlib  
'
import matplotlib
print(matplotlib.matplotlib_fname())
'
看看目录在哪  

然后把字体放到mpl-data\fonts\ttf  
删除C:\Users\username\.matplotlib缓存，OK了  
