构造一个指定大小的0矩阵，并且指定数据的大小类型
    img = numpy.zeros((3,3),dtype=numpy.uint8)
    返回一个array对象
    img.shape
    返回array的行和列的元组

将图像从PNG格式转换成JPEG格式
    img = cv2.imread('MyPic.png')
        读入图像，返回的是一个array对象,可以添加参数将png转成灰度图
        如img = cv2.imread('MyPic.png',IMREAD_GRAYSCALE)
    cv2.imwrite('MyPic.jpg',img)
        写出图像，返回True或者False,不支持gif


将含有随机字节的bytearray转换为灰度图像和BGR图像
关键是os.urandom()函数和
bytearray类到numpy.array类的转换
以及
numpy.array的reshape()方法

生成随机numpy.array数组还可以使用
numpy.random.randint(0,256,120000).reshape(300,400)


生成随机字节
    randomByteArray = bytearray(os.urandom(120000))
    bytearray是一个类，os.urandom能随机产生n个字节的字符串
将bytearray对象转换成numpy.array对象
    flatNumpyArray = numpy.array(randomByteArray)
    numpy的array就是数字数组了
将numpy的array转换成400×300的灰度图,保存成PNG格式
    grayImage = flatNumpyArray.reshape(300,400)
    cv2.imwrite('GrayImage.png',grayImage)
将numpy的array转换成400×100的彩色图,保存成PNG格式
    colorImage = flatNumpyArray.reshape(100,400,3)
    cv2.imwrite('RandomColorImage.png',colorImage)




















