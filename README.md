<div align="center">
<h1>Virtual Vogue – Bringing the Fitting Room to You</h1>
</div>

This is the official implementation of **Virtual Vogue**, an AI-powered virtual try-on system that generates photorealistic, pose-aware visuals using two input images: a user and a garment.

---

## Requirements

```bash
git clone https://github.com/deagle-007/Virtual_Vogue.git
cd VirtualVogue
conda env create -f environment.yaml
conda activate virtualvogue
```

## Data Preparation

Prepare datasets like VITON-HD and DressCode following their standard structure. DensePose images and garment captions should be placed properly if needed.

## Training

Download IP-Adapter models:

```bash
git clone https://huggingface.co/h94/IP-Adapter
```

Move them under the `ckpt/` directory.  
Start training:

```bash
accelerate launch train_xl.py --gradient_checkpointing --use_8bit_adam --output_dir=result --train_batch_size=6 --data_dir=DATA_DIR
```

## Acknowledgements

We acknowledge the original contributions from IP-Adapter, DensePose, OOTDiffusion, and DCI-VTON repositories, which inspired portions of this project.

---
