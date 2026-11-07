# DSC 180A · D32 — EDM on CIFAR-10 and CFG on MNIST

Quarter 1 Checkpoint reproducing parts of EDM (Karras et al., NeurIPS 2022,
https://arxiv.org/abs/2206.00364, code: https://github.com/NVlabs/edm), with classifier-free guidance (CFG)
on CIFAR-10 and MNIST.

## Setup
Python 3 (ipykernel) and an NVIDIA GPU (I used a UCSD Datahub 1 GPU server)

    git clone https://github.com/andrewyounucsd/dsc180a-edm-checkpoint.git
    cd dsc180a-edm-checkpoint
    pip install -r requirements.txt

Note: I had an old installed version of PyTorch that was being used instead of the built in one so I had to `pip uninstall torch torchvision` and restart the kernel.

## Downloads
The notebooks download everything on the first run.
- EDM's code and its pretrained CIFAR-10 networks (NVIDIA)
- EDM's FID reference statistics for CIFAR-10
- a pretrained CIFAR-10 classifier (ResNet-56)
- CIFAR-10
- the MNIST guidance lab's frozen digit classifier
- MNIST via `torchvision.datasets.MNIST`

## Reproducing each figure and table
Run the notebooks top to bottom on a GPU (make sure Quick = False). Figures are saved to the figures folder and numbers are saved to the results folder.

| Result | Notebook and section | Output |
|---|---|---|
| Unconditional sample grid | `cifar10_edm_lab.ipynb`, part 1 | `figures/samples_uncond.png` |
| Conditional samples, one row per class | part 2 | `figures/samples_cond.png` |
| Trajectories: conditional (w = 1) and CFG (w = 4), class cat, seed 3 | part 3, "Your turn" cell | `figures/trajectory_cond_w1.png`, `figures/trajectory_cfg_w4.png` |
| Accuracy / FID / FID_class vs w (1,000 images per w) | part 5 | `figures/cfg_sweep.png`, `results/cfg_sweep_n1000.json` |
| Loss and FID across snapshots (100 and 1,000 training images) | part 6 | `figures/part6_00.png`, `results/part6_fids.json` |
| Samples at each snapshot | part 6 | `figures/part6_01.png`, `figures/part6_02.png` |
| Samples next to nearest training images | part 6, "Is it memorization?" | `figures/part6_03.png`, `figures/part6_04.png` |
| CFG grids with my trained network | part 6, "The effect of CFG" | `figures/part6_05.png`, `figures/part6_06.png` |
| MNIST CFG: loss, sample grid, accuracy and FID vs w | `mnist_cfg_train.ipynb` (run the first 3 cells of `guidance_mnist.ipynb` first) | `figures/mnist_00.png`–`mnist_02.png`, `results/mnist_cfg_n1000.json` |
| Full EDM run on all 50,000 images: loss and FID across snapshots | `cifar10_edm_lab.ipynb`, "Encouraged: an actual training run" (EDM `train.py`, ~1.5 h, 0.55M images) | `figures/full_run.png`, `results/full_run.json` |

## AI Contribution
AI was used to help generate code to save figures directly from the notebook into the figures folder along with creating the "Reproducing each figure and table" portion of the README. AI was also used to help create mnist_cfg_train.ipynb. AI was also used to help some parts of the report read more concise but all ideas and concepts were given by me.