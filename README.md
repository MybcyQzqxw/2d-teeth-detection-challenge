# 2D Teeth Detection Challenge

[![Python](https://img.shields.io/badge/Python-3.9-blue.svg)](https://www.python.org/)
[![Docker](https://img.shields.io/badge/Docker-Supported-blue.svg)](https://www.docker.com/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

> 🌐 [中文版README](README_zh.md) | English

## 📝 Overview

This project aims to build an object detection model that identifies teeth with abnormalities. We developed a multi-step framework for accurate detection of dental lesions in 2D panoramic X-rays.

## 📊 Dataset Description

The dataset consists of 2D panoramic X-rays:
- **Dataset Source**: [Zenodo - 2D Panoramic X-rays](https://zenodo.org/record/7812323#.ZDQE1uxBwUG)
- **Data Type**: 2D panoramic dental X-ray images
- **Purpose**: Dental abnormality detection and classification

## 🏗️ Model Architecture

We proposed a multi-step framework that consists of three main components:

### 1. 🦷 Detection of Dental Instances
- **Technology**: Faster R-CNN
- **Function**: Identify all teeth in the panoramic X-ray

### 2. 🔍 Filtering of Healthy Instances
- **Technology**: Pretrained U-Net encoding path + VGG16 architecture
- **Function**: Binary classification of cropped teeth (healthy/abnormal)

### 3. 🏷️ Classification of Abnormal Instances
- **Technology**: Same architecture as step 2
- **Function**: Classify specific types of abnormal teeth

## 📁 Project Structure

```
├── Dockerfile                  # Docker container configuration
├── README.md                   # Project documentation
├── requirements.txt            # Python dependencies
└── src/                       # Source code directory
    ├── data/                  # Data processing modules
    │   ├── panoramic_dataset.py
    │   ├── tooth_dataset.py
    │   └── scripts/           # Data processing scripts
    ├── model/                 # Model implementations
    │   ├── faster_rcnn/       # Faster R-CNN model
    │   ├── unet/             # U-Net model
    │   └── vgg/              # VGG model
    ├── utils/                 # Utility functions
    └── slurm/                # Cluster job scripts
```

## 🚀 Quick Start

### Requirements

- Python 3.9+
- CUDA-compatible GPU (recommended)
- Docker (optional)

### Installation

#### Method 1: Install with pip

```bash
# Clone the repository
git clone https://github.com/MybcyQzqxw/2d-teeth-detection-challenge.git
cd 2d-teeth-detection-challenge

# Create virtual environment
python -m venv venv
source venv/bin/activate  # Linux/Mac
# or
venv\Scripts\activate     # Windows

# Install dependencies
pip install -r requirements.txt
```

#### Method 2: Use Docker

```bash
# Build Docker image
docker build -t teeth-detection .

# Run container
docker run -it --gpus all -v $(pwd):/workspace teeth-detection
```

### Usage

#### Training Models

```bash
# Faster R-CNN training
python src/model/faster_rcnn/scripts/train.py

# U-Net training
python src/model/unet/scripts/train.py

# VGG training
python src/model/vgg/scripts/train.py
```

#### Model Prediction

```bash
# Make predictions with trained models
python src/model/faster_rcnn/scripts/predict.py --input /path/to/image --output /path/to/output
```

#### Model Testing

```bash
# Evaluate model performance
python src/model/faster_rcnn/scripts/test.py
python src/model/vgg/scripts/test.py
```

## 📈 Performance Metrics

| Model | Precision | Recall | F1-Score | mAP |
|-------|-----------|--------|----------|-----|
| Faster R-CNN | - | - | - | - |
| U-Net + VGG | - | - | - | - |

*Note: Specific performance metrics need to be updated based on actual training results*

## 🔧 Configuration

Each model has its corresponding configuration file:
- `src/model/faster_rcnn/scripts/config.yml`
- `src/model/unet/scripts/config.yml`
- `src/model/vgg/scripts/config.yml`

## 📝 Data Preprocessing

The project provides a complete data preprocessing pipeline:

```bash
# Raw data processing
python src/data/scripts/process_raw_train.py
python src/data/scripts/process_raw_masks.py

# Create datasets
python src/data/scripts/make_tooth_dataset.py
python src/data/scripts/make_tooth_segmentation_dataset.py

# Train-test split
python src/data/scripts/train_test_split.py
```

## 🤝 Contributing

We welcome contributions of any kind! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Create a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 📧 Contact

- **Project Maintainer**: [MybcyQzqxw](https://github.com/MybcyQzqxw)
- **Project Link**: [https://github.com/MybcyQzqxw/2d-teeth-detection-challenge](https://github.com/MybcyQzqxw/2d-teeth-detection-challenge)

## 🙏 Acknowledgments

- Thanks to the research team that provided the dataset
- Thanks to the open source community contributions
- Special thanks to all contributors and users

## 📚 Citation

If you use this project, please consider citing:

```bibtex
@misc{teeth-detection-2023,
  title={2D Teeth Detection Challenge},
  author={MybcyQzqxw},
  year={2023},
  howpublished={\url{https://github.com/MybcyQzqxw/2d-teeth-detection-challenge}}
}
```

---

⭐ If this project helps you, please give us a star!