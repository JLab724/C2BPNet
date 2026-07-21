# C₂BPNet: A Crop Disease Segmentation Network Based on Context Content Boundary Perception

## Installation

### Step 1: Create Conda Environment

```bash
conda create --name c2bpnet python=3.8 -y
conda activate c2bpnet
```

### Step 2: Install PyTorch

```bash
conda install pytorch torchvision -c pytorch
```

### Step 3: Install MMCV and Dependencies

```bash
pip install -U openmim
mim install mmengine
pip install mmcv==2.1.0
pip install -v -e .
```

### Step 4: Install Additional Dependencies

```bash
pip install natten-0.17.3+torch240cu121-cp38-cp38-linux_x86_64.whl
pip install ftfy
pip install regex
pip install tensorboard future
pip install einops
```

### Dataset

The dataset should be organized with the following directory structure:

```text
data/
  plantseg115/
    images/        # RGB
    json/          # JSON files
    annotations/   # ground-truth labels
```

You can set the dataset root to the `data` directory, and the configuration will look for the `plantseg115` subset and its `images` and `annotations` folders accordingly.

## Usage

### Single GPU Training

```bash
python tools/train.py local_config/C₂BPNet/C₂BPNet_base.py
```

### Multi-GPU Training

```bash
CUDA_VISIBLE_DEVICES=0,1,2,3,4 python tools/train.py local_config/C₂BPNet/C₂BPNet_base.py
```

### Test Set Performance Evaluation

```bash
python tools/test.py ${CONFIG_FILE} ${model.pth}
```

### Get Model Parameters and FLOPs

```bash
python tools/analysis_tools/get_flops.py ${CONFIG_FILE} --shape ${INPUT_SHAPE}
```

### Speed Benchmark (FPS)

```bash
python tools/analysis_tools/benchmark.py ${CONFIG_FILE} ${model.pth}
```

## Notes

- Replace `${CONFIG_FILE}` with your actual config file path (e.g., `local_config/C₂BPNet/C₂BPNet_base.py`)
- Replace `${model.pth}` with your trained model checkpoint path
- Replace `${INPUT_SHAPE}` with the input shape
- The NATTEN wheel file (`natten-0.17.3+torch240cu121-cp38-cp38-linux_x86_64.whl`) should be in the project root directory
  - You can download the NATTEN wheel from Baidu Netdisk: [百度网盘下载链接](https://pan.baidu.com/s/1Xz-9Mdobh65fXWMw_0Oi0Q?pwd=77w6)

### Dataset Access and License Agreement

This project uses the PlantSeg dataset and the Downy-MildewSeg dataset.

#### PlantSeg Dataset

The PlantSeg dataset is available from the official repository: [tqwei05/PlantSeg](https://github.com/tqwei05/PlantSeg). The dataset can also be downloaded from Zenodo: [A Large-Scale In-the-wild Dataset for Plant Disease Segmentation](https://doi.org/10.5281/zenodo.17719108).

If your research uses any related parts of these public datasets, you must strictly cite the original work listed below:

```bibtex
@article{wei2024plantseg,
  title={PlantSeg: A Large-Scale In-the-wild Dataset for Plant Disease Segmentation},
  author={Wei, Tianqi and Chen, Zhi and Yu, Xin and Chapman, Scott and Melloy, Paul and Huang, Zi},
  journal={arXiv preprint arXiv:2409.04038},
  year={2024}
}
```

#### Downy-MildewSeg Dataset

> **Dataset Availability Notice:** The Downy-MildewSeg dataset is used in the [DIC-SAM](https://github.com/JLab724/DIC-SAM) project. To protect the originality of this unpublished research and prevent unauthorized use before publication, the dataset is not publicly available at this time, and access applications are temporarily suspended. The dataset and its access application process will be made available after the DIC-SAM paper is formally accepted.

To protect personal research rights and ensure ethical data use, the dataset download link is password-protected. The Downy-MildewSeg dataset is for non-commercial research use only. Commercial use, private forwarding, redistribution, or sharing of the dataset download link, password, or dataset files without explicit permission is strictly prohibited.

Please follow these steps to request access:

1. Download the [Downy-MildewSeg Dataset User Agreement](Downy-MildewSeg%20Dataset%20User%20Agreement.pdf) from this repository.
2. Print and sign the agreement, then send a scanned copy in PDF or image format to `jaxrily007@gmail.com`.
3. After verification, we will reply with the dataset download link and the required access password.
