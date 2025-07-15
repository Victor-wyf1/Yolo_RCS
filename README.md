# Yolo_RCS
# 项目介绍
通过yolo视觉识别的方式，自适应轮廓框选出金属球的RCS成像

<img width="875" height="656" alt="2_overlay_4" src="https://github.com/user-attachments/assets/ffcbd585-81d9-4a59-844b-bccca69fa716" />

# 功能
从给定的雷达成像图，区分出不同角度下，暗弱回波的金属球成像，自动划分边缘，用绿色覆盖被识别的区域

# 存在不足
识别精度不高

前期依赖人工标注

需要前期对雷达成像滤波

## 安装与运行方式
1. 配置文件yaml，包含训练的路径信息
   
2. 原图转换成灰度图
   
3. 将原图用cvat.ai网站进行标注，用draw new polygon画出边缘。对于边缘相连的图像，用不同的label标注，否则程序自动判断为一个整体。
   
4. 将标注好的文件导出为segmention mask
   
5. 运行mask to polygons，将mask转成带有标记点坐标的label
    
6. 运行train，自定义训练回合和线程
    
7. 运用模型进行预测，predict新的图像，可以改置信度
    
8. 导出叠加图
   
## 环境说明
python 3.13

yolo v8

GPU cuda 12.8

## 文件夹层级结构

Main
├── 原图
├── data
│   ├── images
│   │   ├── train （灰度图）
│   │   └── val （从上面选取一半用于程序自我验证的灰度图）
│   └── labels （可能存在 cache 文件）
│       ├── train（和灰度图名称数量一致——对应的 txt 文件，包含标注点的坐标信息）
│       └── val（选取一半 txt 用于验证）
├── tmp （临时存放灰度图和 label 的，程序路径中可能用得到）
└── config.yaml

 
 ## 运行结果
 
 结果在pycharm的RCS_imaged的runs和outputs下
 
 runs：每次训练的best和last.pt
 
 outputs：图像抠像和添加了mask的结果
