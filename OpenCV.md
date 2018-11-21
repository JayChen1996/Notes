
 **C++代码示例位置**
/home/jaychen/Documents/GitCode/OpenCV/opencv/samples/cpp/example_cmake
 **视频图片样例位置**
 /home/jaychen/Documents/GitCode/OpenCV/opencv/samples/data

任务:
    使用python+OpenCV显示摄像头捕获的图像
    绘制一系列形状
    显示一张照片，按键查看各种颜色或灰度直方图

使用imread读入的图片会删除所有alpha通道(即透明度)的信息

OpenCV使用BGR的顺序记录颜色值，所以如果是三维数组,最后一维中0B1G2R

OpenCV可以操作通道，即同时操作所有像素的红色或者绿色或者蓝色分量
    将图像所有的G(绿色)值置为0
    img = cv2.imread('pic.png')
    img[:,:,1]=0

感兴趣区域 Region Of Interest,ROI

OpenCV使用VideoCapture类(读)和VideoWriter类(写)来支持各种格式的视频文件
支持的格式类型在不同系统上不同，但都支持AVI格式

在到达视频文件末尾之前，VideoCapture类使用read()函数来获取新的帧
每一帧是一幅基于BGR格式的图像

AVI格式视频
AVI是Audio Video Interleaved(音视频交错)的英文缩写



