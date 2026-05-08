# 基于计算机视觉的工业装配件缺失检测

## 1. 项目简介

本项目面向工业流水线中的盖子或内衬装配检测任务，目标是判断每一帧中的主要装配件是否为正常装配状态。

实验使用视频前段的正常样本进行训练，测试视频后段中的正常样本和异常样本。核心方法采用无监督异常检测思路，即只学习正常样本的特征分布，再通过异常分数判断测试样本是否为 OK 或 NG。

## 2. 方法概述

本项目包含两个方法：

1. ResNet 特征距离法  
   对 ROI 区域提取整体图像特征，并与训练集中正常样本特征计算距离。

2. PatchCore 异常检测方法  
   对正常 ROI 图像提取 patch 级特征，建立正常特征库。测试时计算测试图像 patch 特征与正常特征库之间的最近邻距离，得到异常分数。

## 3. 项目结构

```text
src/
  01_extract_frames.py      # 视频拆帧
  02_select_roi.py          # 手工选择 ROI
  03_crop_roi.py            # 裁剪 ROI
  04_train_patchcore.py     # 训练正常特征库
  05_test_patchcore.py      # 测试并输出 OK/NG
  06_make_demo_video.py     # 生成演示视频
configs/
  video_A.yaml              # 视频 A 配置
  video_B.yaml              # 视频 B 配置
outputs/
  sample_results/           # 示例结果