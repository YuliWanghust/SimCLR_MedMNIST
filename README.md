# Evaluating SimCLR for Medical Image Classification

In this repository, we provide a comprehensive set of frameworks written in
PyTorch Lightning to perform and evaluate self-supervised contrastive learning
using SimCLR on medical imaging data pipelined from the MedMNIST database.

## Background

A Simple Framework for Contrastive Learning of Visual Representations (SimCLR)
is a state-of-the-art contrastive learning method that aims to learn useful
representations of images through training a convolutional neural network (the
codebase uses ResNet-18) to recognise similarities between a pair of augmented
data points derived from the same input image. The idea is that the network may
learn to extract useful, generalisable features that can be used for downstream
tasks.

Original SimCLR papers:
- [A Simple Framework for Contrastive Learning of Visual Representations][simclr]
```bibtex
@inproceedings{chen2020simple,
  title={A simple framework for contrastive learning of visual representations},
  author={Chen, Ting and Kornblith, Simon and Norouzi, Mohammad and Hinton, Geoffrey},
  booktitle={International conference on machine learning},
  pages={1597--1607},
  year={2020},
  organization={PMLR}
}
```
- [Big Self-Supervised Models are Strong Semi-Supervised Learners][simclrv2]
```bibtex
@article{chen2020big,
  title={Big self-supervised models are strong semi-supervised learners},
  author={Chen, Ting and Kornblith, Simon and Swersky, Kevin and Norouzi, Mohammad and Hinton, Geoffrey E},
  journal={Advances in neural information processing systems},
  volume={33},
  pages={22243--22255},
  year={2020}
}
```

[simclr]: https://arxiv.org/pdf/2002.05709.pdf
[simclrv2]: https://arxiv.org/pdf/2006.10029.pdf

<!-- Contributions -->
<!--
## Contributions

- how well does a SimCLR setup that works well for natural images transfer to medical images?
- 4 augmentation sequences (list them out)
- lack of data
- unbalanced dataset
- evaluation metrics & representations
-->

## Usage guide

### Installation

1. Clone this repository.
```bash
git clone 
```

2. Create virtual environment with Python 3.10.9. Some scripts may fail on
   Python 3.11.
```bash
# Go inside repo
cd simclr-medical imaging
# Create virtual environment
python -m venv venv
# Activate virtual environment
source venv/bin/activate     # For Linux, Mac OS X
source venv/Scripts/activate # For Windows
```

3. Install required packages.
```bash
pip install -r requirements.txt
```

### Usage

The codebase provides in-depth support for SimCLR pretraining, finetuning
(downstream transfer learning), testing, data preview and feature analysis via
PCA and t-SNE.

Navigate to one of the following pages below. Each environment has a
comprehensive documentation with example usage.

Pretrain:
- Go to `pretrain/simclr` directory and see `README.md`.

Finetune with frozen encoder:
- Go to `downstream/logistic_regression` and see `README.md`.

Finetune with unfrozen encoder:
- Go to `downstream/resnet` and see `README.md`.

Baseline:
- Go to `downstream/resnet` and see `README.md`.

Regardless of the experiment, all programs search for models (`.ckpt` files) in
`models/`. For example, when performing downstream learning, the program
searches for the pretrained file in `pretrain/simclr/models/`. If you place the
model in a different folder, you need to update `MODEL_DIR` in `utils.py`.

Note that the saved model is always the latest model after training with the
specified number of epochs. To replace the model with the best-performing
version in terms of validation accuracy, read instructions in
`scripts/replace-with-best-checkpoint.sh`.

## Contribute

### Update requirements

```bash
$ pip freeze > requirements.txt
```

## Credits

We source medical images from [MedMNIST](https://medmnist.com/).

```bibtex
@article{medmnistv2,
    title={MedMNIST v2-A large-scale lightweight benchmark for 2D and 3D biomedical image classification},
    author={Yang, Jiancheng and Shi, Rui and Wei, Donglai and Liu, Zequan and Zhao, Lin and Ke, Bilian and Pfister, Hanspeter and Ni, Bingbing},
    journal={Scientific Data},
    volume={10},
    number={1},
    pages={41},
    year={2023},
    publisher={Nature Publishing Group UK London}
}
```
