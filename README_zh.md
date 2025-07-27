# 2D牙齿检测挑战赛

[![Python](https://img.shields.io/badge/Python-3.9-blue.svg)](https://www.python.org/)
[![Docker](https://img.shields.io/badge/Docker-支持-blue.svg)](https://www.docker.com/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

## 📝 项目概述

本项目旨在构建一个物体检测模型，用于识别牙齿异常。我们开发了一个多步骤框架，能够准确检测2D全景X光片中的牙齿病变。

## 📊 数据集描述

数据集包含2D全景X光片图像，来源于：
- **数据集链接**: [Zenodo - 2D Panoramic X-rays](https://zenodo.org/record/7812323#.ZDQE1uxBwUG)
- **数据类型**: 2D全景牙科X光片
- **用途**: 牙齿异常检测和分类

## 🏗️ 模型架构

我们提出了一个多步骤框架，包含以下三个主要组件：

### 1. 🦷 牙齿实例检测
- **技术**: Faster-RCNN
- **功能**: 识别全景X光片中的所有牙齿位置

### 2. 🔍 健康实例过滤
- **技术**: 预训练U-Net编码路径 + VGG16架构
- **功能**: 对裁剪的牙齿图像进行二分类（健康/异常）

### 3. 🏷️ 异常实例分类
- **技术**: 与步骤2相同的架构
- **功能**: 对异常牙齿进行具体分类

## 📁 项目结构

```
├── Dockerfile                  # Docker容器配置
├── README.md                   # 项目说明文档
├── requirements.txt            # Python依赖包
└── src/                       # 源代码目录
    ├── data/                  # 数据处理模块
    │   ├── panoramic_dataset.py
    │   ├── tooth_dataset.py
    │   └── scripts/           # 数据处理脚本
    ├── model/                 # 模型实现
    │   ├── faster_rcnn/       # Faster R-CNN模型
    │   ├── unet/             # U-Net模型
    │   └── vgg/              # VGG模型
    ├── utils/                 # 工具函数
    └── slurm/                # 集群作业脚本
```

## 🚀 快速开始

### 环境要求

- Python 3.9+
- CUDA支持的GPU（推荐）
- Docker（可选）

### 环境配置

```bash
# 克隆仓库
git clone https://github.com/MybcyQzqxw/2d-teeth-detection-challenge.git
cd 2d-teeth-detection-challenge

# 创建虚拟环境
conda create -n teeth-detection python=3.9 -y
conda activate teeth-detection

# 安装依赖
pip install -r requirements.txt
```

### 数据预处理

- 下载地址：<https://zenodo.org/records/7812323>
- 解压至 `data/raw/` 目录下，目录结构如下：

```
data/raw/
├── training_data/
│   ├── quadrant/
│   │   ├── xrays/
│   │   └── train_quadrant.json
│   ├── quadrant_enumeration/
│   │   ├── xrays/
│   │   └── train_quadrant_enumeration.json
│   ├── quadrant-enumeration-disease/
│   │   ├── xrays/
│   │   └── train_quadrant_enumeration_disease.json
│   └── unlabelled/
│       └── xrays/
└── validation_data/quadrant_enumeration_disease/xrays/
```

```bash
# 原始数据处理
python src/data/scripts/process_raw_train.py
python src/data/scripts/process_raw_masks.py

# 创建数据集
python src/data/scripts/make_tooth_dataset.py
python src/data/scripts/make_tooth_segmentation_dataset.py

# 训练测试集划分
python src/data/scripts/train_test_split.py
```

### 使用方法

#### 训练模型

```bash
# Faster R-CNN训练
python src/model/faster_rcnn/scripts/train.py

# U-Net训练
python src/model/unet/scripts/train.py

# VGG训练
python src/model/vgg/scripts/train.py
```

#### 模型预测

```bash
# 使用训练好的模型进行预测
python src/model/faster_rcnn/scripts/predict.py --input /path/to/image --output /path/to/output

例如：
python src/model/faster_rcnn/scripts/predict.py --input data/raw/validation_data/quadrant_enumeration_disease/xrays --output output
```

#### 模型测试

```bash
# 评估模型性能
python src/model/faster_rcnn/scripts/test.py
python src/model/vgg/scripts/test.py
```

## 🔧 配置文件

每个模型都有对应的配置文件：
- `src/model/faster_rcnn/scripts/config.yml`
- `src/model/unet/scripts/config.yml`
- `src/model/vgg/scripts/config.yml`

## 🤝 贡献指南

我们欢迎任何形式的贡献！请遵循以下步骤：

1. Fork本仓库
2. 创建特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 创建Pull Request

## 📄 许可证

本项目采用MIT许可证 - 查看 [LICENSE](LICENSE) 文件了解详情。

## 📧 联系方式

- **项目维护者**: [MybcyQzqxw](https://github.com/MybcyQzqxw)
- **项目链接**: [https://github.com/MybcyQzqxw/2d-teeth-detection-challenge](https://github.com/MybcyQzqxw/2d-teeth-detection-challenge)

## 🙏 致谢

- 感谢提供数据集的研究团队
- 感谢开源社区的贡献
- 特别感谢所有贡献者和使用者

## 📚 相关论文

如果您使用了本项目，请考虑引用相关论文：

```bibtex
@misc{teeth-detection-2023,
  title={2D Teeth Detection Challenge},
  author={MybcyQzqxw},
  year={2023},
  howpublished={\url{https://github.com/MybcyQzqxw/2d-teeth-detection-challenge}}
}
```

---

⭐ 如果这个项目对您有帮助，请给我们一个星标！
