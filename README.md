# Virtual Vogue – Bringing the Fitting Room to You 👗

<div align="center">

### AI-Powered Virtual Try-On Platform

*Bringing the fitting room to you with Artificial Intelligence and Computer Vision.*

</div>

---

## Overview

**Virtual Vogue** is an AI-powered virtual try-on system designed to generate realistic, pose-aware visualizations of garments on human images.

Using deep learning, computer vision, human pose estimation, and diffusion-based image generation, the system allows users to visualize how different clothing items may look on them without physically wearing the garments.

The platform takes two primary image inputs:

1. **Human Image:** An image of the person who wants to try on a garment.
2. **Garment Image:** An image of the clothing item to be virtually worn.

Virtual Vogue processes these inputs and generates a virtual try-on result while considering human pose, body regions, garment information, and image masks.

## Key Features

- **AI-Powered Virtual Try-On:** Generate visualizations of garments on human images.
- **Pose-Aware Generation:** Use human pose information to guide garment placement.
- **Human Parsing:** Identify relevant human body regions.
- **Automatic Mask Generation:** Generate masks for clothing regions.
- **Garment Description:** Support text-based descriptions of clothing items.
- **Diffusion-Based Image Generation:** Generate realistic virtual try-on outputs.
- **Interactive Interface:** Provide an interface for uploading human and garment images.

## Repository Structure

```text
Virtual_Vogue/
│
├── ckpt/                       # Model checkpoints
├── configs/                    # Model configuration files
├── densepose/                  # DensePose components
├── detectron2/                 # Detectron2 components
├── example/                    # Example human and garment images
├── gradio_demo/                # Gradio demonstration resources
├── ip_adapter/                 # IP-Adapter components
├── preprocess/                 # Human parsing and pose preprocessing
├── src/                        # Try-on pipeline and model implementations
├── util/                       # Utility functions
│
├── VV_training.ipynb           # Model training notebook
├── app_VV.py                   # Virtual Vogue application
├── apply_net.py                # DensePose application
├── inference.py                # Inference implementation
├── inference.sh                # Inference execution script
├── inference_dc.py             # Additional inference implementation
├── train_xl.py                 # Model training script
├── train_xl.sh                 # Training execution script
├── utils_mask.py               # Mask generation utilities
│
├── vitonhd_test_tagged.json    # VITON-HD test annotations
├── vitonhd_train_tagged.json   # VITON-HD training annotations
├── environment.yaml            # Conda environment configuration
├── requirements.txt            # Python dependencies
├── LICENSE.txt                 # License information
└── README.md                   # Project documentation
```

## Technologies and Dependencies

Virtual Vogue uses Python-based machine learning and computer vision technologies.

| Technology | Purpose |
|---|---|
| Python | Core programming language |
| PyTorch | Deep learning framework |
| Diffusers | Diffusion-based image generation |
| Transformers | Pretrained transformer models |
| Hugging Face Accelerate | Model training and acceleration |
| Gradio | Interactive application interface |
| OpenCV | Image processing |
| NumPy and SciPy | Numerical computation |
| Detectron2 and DensePose | Human pose and body analysis |
| IP-Adapter | Image-conditioned generation |
| PEFT | Parameter-efficient fine-tuning |

## Installation

### 1. Clone the Repository

```bash
git clone https://github.com/deagle-007/Virtual_Vogue.git
```

Navigate to the project directory:

```bash
cd Virtual_Vogue
```

### 2. Create the Conda Environment

```bash
conda env create -f environment.yaml
```

Activate the environment:

```bash
conda activate virtualvogue
```

### 3. Install Dependencies

Install the required Python packages:

```bash
pip install -r requirements.txt
```

**Note:** Ensure that PyTorch and CUDA are installed in versions compatible with your GPU and the project dependencies. Detectron2 and other compiled dependencies may also require environment-specific installation.

## Requirements

The following packages and versions are specified in `requirements.txt`:

```txt
numpy==1.24.4
scipy==1.10.1
scikit-image==0.21.0
opencv-python==4.7.0.72
pillow==9.4.0
diffusers==0.25.1
transformers==4.41.1
accelerate
matplotlib==3.7.4
tqdm==4.64.1
config==0.5.1
einops==0.7.0
onnxruntime==1.16.2
basicsr
av
fvcore
cloudpickle
omegaconf
pycocotools
huggingface_hub==0.25.2
gradio
peft
```

## Dataset Preparation

Virtual Vogue uses publicly available virtual try-on datasets, including:

- **VITON-HD**
- **DressCode**

Prepare the datasets according to their respective directory structures and ensure that the required human images, garment images, annotations, and supporting preprocessing data are available.

The repository includes the following VITON-HD annotation files:

```text
vitonhd_train_tagged.json
vitonhd_test_tagged.json
```

These files are provided for the training and testing data preparation workflow.

Additional preprocessing resources, including human parsing and DensePose information, should be configured according to the project requirements.

## Model Checkpoints

Virtual Vogue uses pretrained model components and supporting checkpoints for its virtual try-on pipeline.

### IP-Adapter

Clone the IP-Adapter repository:

```bash
git clone https://huggingface.co/h94/IP-Adapter
```

Place the required IP-Adapter model files under the project's `ckpt/` directory according to the model configuration.

### DensePose

The inference pipeline requires the corresponding DensePose configuration and model checkpoint.

Expected paths:

```text
configs/densepose_rcnn_R_50_FPN_s1x.yaml
ckpt/densepose/model_final_162be9.pkl
```

Ensure that the required checkpoint is available before running inference.

### Pretrained Model Components

The inference pipeline loads components including:

- UNet
- UNet Encoder
- VAE (Variational Autoencoder)
- Text Encoders
- Tokenizers
- Image Encoder
- Noise Scheduler

Ensure that the configured model directory contains the compatible pretrained model components and their configuration files.

## Model Training

Virtual Vogue provides a training implementation through `train_xl.py` and the Jupyter notebook `VV_training.ipynb`.

After preparing the environment, dataset, and required model checkpoints, launch training using:

```bash
accelerate launch train_xl.py \
    --gradient_checkpointing \
    --use_8bit_adam \
    --output_dir=result \
    --train_batch_size=6 \
    --data_dir=DATA_DIR
```

Replace `DATA_DIR` with the actual path to the prepared training dataset.

Alternatively, use the provided shell script:

```bash
bash train_xl.sh
```

The training configuration may be adjusted according to available GPU memory, dataset size, and computational resources.

## Inference and Virtual Try-On

Virtual Vogue provides inference implementations for generating virtual try-on results.

The main application is:

```text
app_VV.py
```

Run the application using:

```bash
python app_VV.py
```

The interface allows users to provide:

- A human image
- A garment image
- A textual garment description

The inference pipeline combines:

1. Human image preprocessing.
2. Human parsing and pose estimation.
3. DensePose processing.
4. Clothing-region mask generation.
5. Garment image encoding.
6. Diffusion-based image generation.
7. Virtual try-on result generation.

Additional inference implementations are available in:

```text
inference.py
inference_dc.py
```

## Acknowledgements

Virtual Vogue acknowledges the research contributions and open-source implementations of the following projects, which inspired or supported components of this work:

- [IP-Adapter](https://github.com/tencent-ailab/IP-Adapter)
- [DensePose](https://github.com/facebookresearch/DensePose)
- [OOTDiffusion](https://github.com/levihsu/OOTDiffusion)
- [DCI-VTON](https://github.com/bcmi/DCI-VTON)

We appreciate the researchers and developers who have contributed these resources to the machine learning and computer vision community.

## License

Please refer to [LICENSE.txt](LICENSE.txt) for licensing information and applicable terms for this repository and its third-party components.

---

## Project Information

**Virtual Vogue – Bringing the Fitting Room to You**

GitHub Repository: [deagle-007/Virtual_Vogue](https://github.com/deagle-007/Virtual_Vogue)

