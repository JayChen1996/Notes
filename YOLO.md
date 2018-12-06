2018-11-6：

目标检测的过去和现在：
http://www.voidcn.com/article/p-wwpxhelg-bgy.html
https://blog.csdn.net/holybin/article/details/26614657
https://blog.csdn.net/qq_36108338/article/details/68943651
https://flat2010.github.io/2018/02/16/%E6%B7%B1%E5%BA%A6%E5%AD%A6%E4%B9%A0%EF%BC%9A%E7%9B%AE%E6%A0%87%E6%A3%80%E6%B5%8B%E4%B9%8B%E4%B8%80%EF%BC%88%E5%9F%BA%E7%A1%80%E7%AF%87%EF%BC%89/
https://zhuanlan.zhihu.com/p/27546796?from=groupmessage&isappinstalled=0
https://zhuanlan.zhihu.com/p/33277354
https://blog.csdn.net/u014380165/article/details/72616238



深度学习之前:
* 基于统计或知识。
传统目标检测：
* Cascade + Harr/SVM + HOG/DPM

传统目标检测算法的大致流程:
1. Step1：确定滑动窗口；
2. Step2：利用滑动窗口提取出候选区域；
3. Step3：对候选区域进行特征提取；
4. Step4：使用分类器（事先已经训练好）进行分类，判断候选区域是否包含有效目标；
5. Step5：对所有包含有效目标的候选区域进行合并；
6. Step6：作图，绘制出检测目标轮廓框。

得到bounding boxde两种方法
- standard sliding window
- region proposal techniques

---
###  Real-Time Grasp Detection Using Convolutional Neural Networks

- 使用单网络对每张图片预测一次并直接预测抓取坐标
- 网络较大但只对图片应用一次所以获得巨大的性能提升
- 不止注意局部的patches，网络也使用图像全局信息来推理预测抓取，所以很精确
- 使用的是RGB-D数据，
- 之前有的工作是用全3D方阵来找到好的抓取位置，这需要物体的3D模型先验知识，而通用目的机器人需要抓取事先没有复杂三维模型的新物体
- 使用5个维度来表示平板夹持器夹取物体前的位置和方向
- 我们默认假设一个好的2维上的抓取可以通投影回3维
- 采用的CNN模型是AlexNet
- 在滑动窗口方法中作为分类器效果不错
- 采用AlexNet作为基础
- 直接用回归的方法查找抓取区域坐标
- 输出层有6个神经元，其中四个是关于定位和宽高的，剩下两个是角度信息，是角度乘以2的sin和cos值
- 模型假设每张图片都只存在一个可抓取物体，且只需要预测该物体的一个抓取位置。这个假设的好处是不需要在滑动窗口办法中分类许多小patches，只需要盯着单张图片做全局预测。
- 训练模型时对每张图片每次随机选取一个真实抓取区域，用来防止对每个物体抓取的过拟合。
- 要抓取一个物体首先要识别这个物体，通过扩展模型，这里把recognition和grasp detection结合到一个有效的pipeline之中
- 增加与物体类别相关的额外输出层神经元
- MultiGrasp是为了预测出多个抓取区域，它将图片分成N×N的grid，然后假设每个gridcell中最多一个抓取。此时模型的输出时N×N×7的矩阵，第一个通道是对应cell可能包含正确抓取的概率的热力图。
- 两种评价抓取区域预测的度量
  * point metric，预测区域的点的中心的度量到其他真实区域的中心的距离之和，小于某个threshold就认为预测成功
  * rectangle metric，需要满足下面两个条件才算成功:
    * 与真实的抓取的角度差小于30度
    * Jaccard index小于25%
    $$
    J(A,B) = \frac{A\cap B}{A\cup B}
    $$
-

#### 问题：
1. 如何确定滑动窗口？
   * 使用不同尺度的滑动窗口
2. 依据什么标准提取候选区域？
3. 对候选区域进行特征提取的方法
   * 有Harr HOG LBP LTP等特征提取方法
4. 有哪些常用的分类器？
   * Adaboost SVM等分类算法对候选区域分类，判断是否是待检测目标

    