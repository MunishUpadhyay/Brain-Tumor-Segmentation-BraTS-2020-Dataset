# BraTS 2020 Brain Tumor Segmentation

This repository contains code for brain tumor segmentation using the BraTS 2020 dataset. The project implements deep learning models to automatically segment brain tumors from multi-modal MRI scans.

## Dataset Overview

The Brain Tumor Segmentation Challenge (BraTS) 2020 dataset contains multi-institutional pre-operative MRI scans of glioblastoma and lower-grade glioma patients. Each case includes four MRI modalities:

- **T1**: T1-weighted
- **T1ce**: T1-weighted with contrast enhancement
- **T2**: T2-weighted
- **FLAIR**: Fluid Attenuated Inversion Recovery

### Tumor Regions
The segmentation task involves identifying three tumor sub-regions:
- **Enhancing Tumor (ET)**: Label 4
- **Tumor Core (TC)**: Labels 1 and 4
- **Whole Tumor (WT)**: Labels 1, 2, and 4

## Project Structure

```
├── README.md
├── brats2020_get_data_read.py      # Data loading and preprocessing
├── custom_data_generator.py        # Custom data generator for training
├── train_brats2020_updated.py      # Main training script
└── train_brat2020.ipynb           # Jupyter notebook for experimentation
```

## Files Description

### `brats2020_get_data_read.py`
- Handles data loading from the BraTS 2020 dataset
- Implements preprocessing functions for MRI volumes
- Manages data organization and file path handling
- Includes normalization and standardization utilities

### `custom_data_generator.py`
- Custom PyTorch/Keras data generator for efficient batch processing
- Handles on-the-fly data augmentation
- Manages memory-efficient loading of large MRI volumes
- Implements random sampling strategies for training

### `train_brats2020_updated.py`
- Main training script with updated architecture
- Implements the segmentation model (likely U-Net or similar)
- Includes training loop with validation
- Handles model checkpointing and logging

### `train_brat2020.ipynb`
- Interactive Jupyter notebook for experimentation
- Step-by-step model development and testing
- Visualization tools for results analysis
- Hyperparameter tuning and ablation studies

## Requirements

```bash
# Core dependencies
torch>=1.8.0
torchvision>=0.9.0
numpy>=1.19.0
nibabel>=3.2.0
scikit-image>=0.18.0
matplotlib>=3.3.0
tqdm>=4.60.0
pandas>=1.2.0

# Optional for visualization
seaborn>=0.11.0
plotly>=4.14.0
```

## Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd brats2020-segmentation
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

3. Download the BraTS 2020 dataset:
   - Register at: https://www.med.upenn.edu/cbica/brats2020/
   - Download and extract the dataset
   - Update data paths in configuration files

## Usage

### Data Preparation
```python
from brats2020_get_data_read import load_brats_data, preprocess_volume

# Load and preprocess data
data_path = "/path/to/brats2020/dataset"
train_data, val_data = load_brats_data(data_path)
```

### Training
```bash
python train_brats2020_updated.py --data_path /path/to/dataset --epochs 10 --batch_size 2
```

### Interactive Development
```bash
jupyter notebook train_brats2020.ipynb
```

## Model Architecture

The project likely implements a 3D U-Net architecture optimized for multi-modal brain tumor segmentation:

- **Input**: 4-channel MRI volumes (T1, T1ce, T2, FLAIR)
- **Output**: 4-class segmentation masks
- **Architecture**: 3D U-Net with skip connections
- **Loss Function**: Combined Dice + Cross-entropy loss

## Evaluation Metrics

The model is evaluated using standard BraTS metrics:
- **Dice Similarity Coefficient (DSC)**
- **Hausdorff Distance (HD95)**
- **Sensitivity**
- **Specificity**

## Data Augmentation

The custom data generator includes:
- Random rotations and flips
- Elastic deformations
- Intensity normalization
- Random cropping and scaling

## Training Configuration

```python
# Example configuration
BATCH_SIZE = 2
LEARNING_RATE = 1e-4
EPOCHS = 10
PATCH_SIZE = (128, 128, 128)
NUM_CLASSES = 4
```

## Results

Expected performance on BraTS 2020 validation set:
- **Enhancing Tumor**: Dice ~0.78
- **Tumor Core**: Dice ~0.85
- **Whole Tumor**: Dice ~0.90

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests if applicable
5. Submit a pull request

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgments

- BraTS 2020 Challenge organizers
- Medical imaging community
- Contributors to open-source medical imaging libraries

## Contact

For questions or issues, please open a GitHub issue or contact [munishupadhyay183@gmail.com].

---

**Note**: Make sure to comply with the BraTS 2020 dataset usage terms and conditions. The dataset is for research purposes only.
