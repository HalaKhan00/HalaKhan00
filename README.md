![](imgs/shift-large.png)

**SHIFT** (mercifully short for **s**peedy **h**istological-to-**i**mmuno**f**luorescent **t**ranslation) is a deep learning-based method for virtual IF staining of images containing histologically-stained tissues.

This code is based very (very) heavily on [pix2pix](https://github.com/junyanz/pytorch-CycleGAN-and-pix2pix) and is indebted to its authors.

[See our latest preprint on biorXiv.](https://www.biorxiv.org/content/biorxiv/early/2019/08/15/730309.full.pdf)

[See our original conference paper in the Proceedings of SPIE Medical Imaging 2018.](https://eburling.github.io/files/SHIFT-SPIE-Medical-Imaging-2018.pdf).

Thanks to [Eugene Manley, Jr.](https://www.linkedin.com/in/eugenemanleyjrphd) for the mouse H&E and IF images used to make the SHIFT logo.

### Prerequisites
- Linux
- Python 3
- NVIDIA GPU (preferably V100 16GB) + CUDA CuDNN
- conda

### Installation

- Clone this repo:
```bash
git clone https://gitlab.com/eburling/SHIFT.git
cd SHIFT
```

- Create and activate the SHIFT environment:
```bash
conda env create -f environment.yml
conda activate SHIFT_test # or `source activate SHIFT_test`
```

- Download the SHIFT dataset:
```bash
bash ./scripts/download_SHIFT_dataset.sh
```

### Apply a pre-trained SHIFT panCK model

- Download the pre-trained SHIFT model for H&E-to-panCK translation:
```bash
bash ./scripts/download_pretrained_panCK_model.sh
```

- Run inference using the pretrained panCK model:
```bash
bash ./scripts/test_panCK_pretrained.sh
```

### Train and test a SHIFT panCK model

- Train a panCK model _de novo_:
```bash
bash ./scripts/train_panCK.sh
```

- Run inference using the panCK model you just trained:
```bash
bash ./scripts/test_panCK.sh
```

## Practical training considerations
We trained our SHIFT models on NVIDIA V100 16GB GPUs, which allowed us to push the envelope on the training batch size (`--batch_size 64`) and number of first-layer filters for both the generator (`--ngf 128`) and the discriminator (`--ndf 128`) networks.

If you run out of memory, e.g.
```bash
RuntimeError: CUDA error: out of memory
```
...then you should try training with a smaller batch size or fewer first-layer filters.

<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-nd/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/">Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International License</a>.