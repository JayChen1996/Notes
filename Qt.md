  **paintEvent函数**

是QWidget类中的虚函数，用于ui的绘制，多种情况下被其它函数自动调用,如update()


2018.10.7
Graphics View框架提供了一个管理和交互大量自定义2D图元的surface,一个将图元可视化的
视图控件，支持缩放和旋转。

这个框架包括一个事件传播architecture，能够为场景scene中的图元item提供精确的双精度交互能力
图元可以处理键盘事件，鼠标点击，移动，释放和双击时间，也可以跟踪鼠标的移动

Graphics View使用BSP tree(Binary Space Partitioning tree二叉分割树)提供图元的快速发现
因此，可以在大场景中实时显示百万级的图元

Graphics View在Qt4.2中被引入，替代其前辈 QCanvas

Graphics View的架构
  Graphics View提供了一个基于图元的模型视图编程方法，很像内嵌试图的方便类
  QTableView，QTreeView和QListView，一些view可以视作一个单场景single scene
  这个场景包含了各种各样的几何图元
 scene
 QGraphicScene提供了模型视图的scene，有如下的任务:
  #提供管理大量图元items的快速接口(fast interface)
  #为每个图元传播事件
  #管理图元状态，如选择和焦点处理
  #提供未转换渲染功能(untransformed rendering functionality)，主要是为了印刷
 scene作为QGraphicsItem对象的容器,使用QGraphicsScene::addItem()将图元加入到场景中
 要检索和取回的话就调用许多item discovery functions中的某一个
 QGraphicsScene::item()以及其重载返回场景中包含的所有item或者与某个点，矩形，多边形或者向量路径相交的item
 QGraphicsScene::itemAt()返回在某个点的最上方的图元

 QGraphicsScene的事件传播机制管理事件向每个图元items传播
 也管理图元之间的传播,
 QGraphicsScene也管理确定的图元状态，如图元选择和聚焦。
 你可以通过调用QGraphicsScene::setSelectionArea()传递一个任意的
 形状选择场景中的items
 这个功能是QGraphicsView的框选的基础
 使用QGraphicsScene::selectedItems()可以得到所有当前选中的图元
 另一个由QGraphicsScene处理的状态是图元是否有键盘输入焦点
 你可以调用QGraphicsScene::setFocusItem()在一个图元上设置焦点
 或者调用QGraphicsItem::setFocus()
 或者调用QGraphicsScene::focusItem()得到当前焦点所在图元

 最后，QGraphicsScene允许你通过
 QGraphicsScene::render()函数渲染一部分场景到paint device

 The View
 QGraphicsView提供视图控件(the view widget),使场景中的内容可视化
 你可以关联多个视图到同一个场景
 提供多个视口到同一个数据集。
 视口提供滚动条以显示大场景(large scenes)
 为获取OpenGL支持,你可以通过调用QGraphicsView::setViewport()设置QGLWidget作为视口
 
 view接受键盘和鼠标事件，并且在发送事件到可视化场景(visualized scene)之前
 将事件翻译成场景事件(scene events)
 (转换坐标为场景坐标系的坐标),

 使用它的转换矩阵,QGraphicsView::transform(),view可以转换scene的坐标系
 这实现了高级导航功能(advanced navigation)如缩放和旋转
 为了方便，QGraphicsView提供了函数用于view和scene坐标系之间的转换
 :QGraphicsView::mapToScene()和QGraphicsView::mapFromScene()

 The Item
 QGraphicsItem是scene中的图元的基类,
 Graphics View提供一些典型的形状的标准图元,
 如矩形(QGraphicsRectItem)，椭圆(QGraphicsEllipseItem)，
 和文字图元(QGraphicsTextItem)
 但是最powerful的QGraphicsItem特性在你自定义图元时才能得到
 除此之外，QGraphicsItem支持下列特性:
  #鼠标按下，移动，释放和双击事件，以及鼠标悬停事件
   滚轮事件和右键菜单事件
  #键盘输入焦点和键盘事件
  #拖和放
  #分组，通过父子关系或者QGraphicsItemGroup
  #碰撞检测
 Item处于局部坐标系中(local coordinate system),像QGraphicsView一样，
 item也提供了许多item和scene之间,item和item之间坐标系转换的函数
 同时，item也可以使用矩阵进行坐标系转换，QGraphicsItem::transform()
 这在旋转和缩放每个item(individual items)时有用
 Items可以包含其他items(children),父item的转换被所有孩子继承
 尽管一个item的累计变换，他所有的函数(如QGraphicsItem::contains()
 QGraphicsItem::boundingRect(),QGraphicsItem::collidesWith())
 仍然是在局部坐标系中操作
 
 QGraphicsItem通过
 QGraphicsItem::shape()函数和QGrpahicsItem::collidesWith()函数
 可以进行碰撞检测，两个都是虚函数。
 通过QGraphicsItem::shape()函数以local coordinate的QPainterPath返回你的图元
 的形状，QGraphicsItem将处理你所有的碰撞检测。
 
 
