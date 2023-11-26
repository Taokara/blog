<style>
.blogpost-body h2{
    font-size: 28px;
    font-weight: bold;
    height: 37px;
    border-bottom: 3px solid #000000;
	padding-top:0.3cm;
}
h3{
    background: linear-gradient(to right, #2a5caa 0%,#ffffff 100%);
    color: #FFFFFF;
    font-size: 18px;
    font-weight: bold;
    height: 30px;
    padding: 8px 0 5px 10px;
    text-shadow: 2px 2px 3px #222222;
}
h4{
    background: linear-gradient(to right, #99cc99 0%,#ffffff 100%);
	color: #003300;
    font-weight: bold;
    height: 25px;
    padding: 1px 0 5px 5px;
}
</style>
#### 安装Tesseract-OCR
1. 说明
   pytesseract库可以操作Tesseract-OCR。这个安装网上有教程，要注意的是配置环境变量和path
   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/opencv简单使用_1.png)

   ![](https://cdn.jsdelivr.net/gh/Taokara/blogimg/opencv简单使用_2.png)

1. 安装包：版本不匹配很容易安装不上
    ```
    pip  install -i https://pypi.tuna.tsinghua.edu.cn/simple opencv-python==4.1.2.30
    pip  install -i https://pypi.tuna.tsinghua.edu.cn/simple pytesseract
    pip  install -i https://pypi.tuna.tsinghua.edu.cn/simple Pillow
    ```
#### 代码
1. 示例
    ```
    import cv2
    import pytesseract

    # 读取图片
    img = cv2.imread('image.jpg')

    # 图像处理
    gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY) # 转换为灰度图像
    blur = cv2.GaussianBlur(gray, (5, 5), 0) # 模糊滤波
    thresh = cv2.threshold(blur, 0, 255, cv2.THRESH_BINARY_INV + cv2.THRESH_OTSU)[1] # 二值化

    # 文本检测和识别
    data = pytesseract.image_to_string(thresh, lang='chi_sim+eng') # 中英文识别

    # 输出识别结果
    print(data)

    ```