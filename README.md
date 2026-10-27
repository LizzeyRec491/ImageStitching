# Image Stitching with SIFT

一个基于 Python、OpenCV 和 Jupyter Notebook 的图像特征匹配与拼接示例。Notebook 使用 SIFT 提取局部特征，通过 Brute-Force kNN 匹配寻找两张图片中的对应点，再用 RANSAC 估计单应矩阵，将图像变换到同一画布并展示拼接结果。

## 处理流程

1. 读取 `image1.jpg` 和 `image2.jpg`，转换为灰度图用于特征提取。
2. 使用 SIFT 检测关键点和描述子，最多选取 60 个特征。
3. 使用 Brute-Force matcher 执行 kNN 匹配，并通过 Lowe ratio（`0.75`）过滤较含糊的匹配。
4. 绘制两张图片之间的特征对应关系。
5. 有足够的匹配点时，使用 RANSAC（重投影阈值 `5.0`）估计单应矩阵，将第一张图片透视变换到共同画布，再放置第二张图片并显示拼接图。

Notebook 的图像结果显示在单元格输出中，不会自动另存为图片文件。

## 项目文件

```text
ImageStitching/
├── ImageStitching.ipynb   # 特征匹配和图像拼接流程
├── image1.jpg             # 输入图片 1
├── image2.jpg             # 输入图片 2
├── README.md
└── LICENSE
```

图片文件名大小写需要与 notebook 中的路径一致。运行 notebook 前，请确保它以项目目录为当前工作目录，能够读取到这两张图片。

## 环境要求

- Python 3
- Jupyter Notebook 或 JupyterLab
- OpenCV (`cv2`)
- NumPy
- Matplotlib

安装依赖：

```sh
python -m pip install jupyter opencv-python numpy matplotlib
```

## 运行

在项目目录中启动 JupyterLab：

```sh
jupyter lab
```

打开 `ImageStitching.ipynb`，按顺序运行单元格。Notebook 会先显示特征匹配图，再显示拼接结果；若筛选后不足 5 个匹配点，会提示无法计算单应矩阵。

## 适用范围与限制

该示例适用于有足够重叠区域、且两图之间可由单个平面单应变换近似描述的图片。拼接采用直接覆盖重叠区域，没有接缝融合、曝光补偿或畸变校正；图片内容、重叠范围或匹配质量不合适时，结果可能错位或无法生成。

## 许可证

代码采用 [MIT License](LICENSE)。图片可能有独立的版权或使用条件，请在转载或公开前确认授权。
