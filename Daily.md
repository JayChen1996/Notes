### 2018-11-16
* https://www.imooc.com/article/44040
* mAP Mean Average Precision 平均精度
* - YOLO
  - 输入是全图
  - 网络自动将图片分成不同区域
  - 对每个区域预测bounding boxes和概率
  - 用预测的概率对边界框加权
* IOU 预测框和GroundTruth(即真实框)的交集和并集的比值
* Focal Loss 一个损失函数
* 很容易在速度和精确度之间取舍
* inference time 推理时间
* 用单个网络评估，不像R-CNN
* - YOLOv3使用一些技巧提升训练和增强性能
  - multi-scale predictions 多尺度预测
  - a better backbone classifier 主分类器
* 默认情况下，YOLO只显示检测到的置信度大于0.25或者更高的物体
* Darknet的训练需要每张图片对应一个.txt文件，记录目标的种类和boundingbox位置
* 