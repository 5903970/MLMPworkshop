```markdown
# PyTorch CycleGAN and pix2pix - Pretrained Inference Guide

## Project

**Repository:** https://github.com/junyanz/pytorch-CycleGAN-and-pix2pix

**Inference task:** Unpaired image-to-image translation (horse → zebra transformation)

## Repo map

**Environment:** `environment.yml` & `requirements.txt`

**Entry point:** `test.py`

**Model:** `horse2zebra_pretrained` (downloads from official release via `scripts/download_cyclegan_model.sh`)

**Input:** `datasets/horse2zebra/testA/` (real horse images)

**Output:** `results/horse2zebra_pretrained/test_latest/index.html` (interactive HTML with side-by-side comparisons)

## Environment setup

```bash
git clone https://github.com/junyanz/pytorch-CycleGAN-and-pix2pix
cd pytorch-CycleGAN-and-pix2pix
conda env create -f environment.yml
conda activate pytorch-img2img
```

## Inference
```bash
# Download the pretrained model (43 MB)
bash ./scripts/download_cyclegan_model.sh horse2zebra

# Download the test dataset
bash ./datasets/download_cyclegan_dataset.sh horse2zebra

# Run inference
python test.py --dataroot ./datasets/horse2zebra/testA --name horse2zebra_pretrained --model test --no_dropout
```

## One real failure

**Category:** Missing dependencies / CUDA support

**Root cause:** Using `pip install -r requirements.txt` alone is insufficient because:
- requirements.txt only lists pip packages (torch, torchvision, etc.)
- Missing CUDA 12.1 support (requires `pytorch-cuda=12.1` from conda)
- Missing system-level dependencies from conda-forge/nvidia channels

**Minimal fix:** Use conda environment file instead:
```bash
conda env create -f environment.yml  # Recommended
# Instead of: pip install -r requirements.txt  # Incomplete
```

## AI agent check

**Which AI coding agent did you use?:** GitHub Copilot (Claude Haiku 4.5)

**What did it change?:** Identified the correct installation method by reading environment.yml and README documentation, avoiding incomplete pip-only approach.

**How did you verify the change?:** Tested the inference command successfully after following the conda setup; checkpoint downloaded and model loaded without dependency errors.
```
