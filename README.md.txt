# Grid R-CNN

An mmdetection based implementation of updated Grid R-CNN published on CVPR 2019. Original paper is [here](https://arxiv.org/abs/1811.12030), details of updates can be seen in this [technical report](update/updates_of_grcnn.pdf).

## Installation

This project is based on mmdetection object detection framework.

### Requirements

- Python 3.5+ ([Say goodbye to Python2](https://python3statement.org/))
- PyTorch 1.0+ or PyTorch-nightly
- CUDA 9.0+
- GCC 4.9+
- [mmcv](https://github.com/open-mmlab/mmcv)

### Install Grid R-CNN with mmdetection

a. Create a conda virtual environment and activate it. Then install Cython.

```shell
conda create -n open-mmlab python=3.7 -y
source activate open-mmlab

conda install cython
```

b. Install PyTorch stable or nightly and torchvision following the [official instructions](https://pytorch.org/).

c. Clone the this repository.

d. Compile cuda extensions.

```shell
./compile.sh
```

e. Setup mmdetection (other dependencies will be installed automatically).

```shell
python setup.py develop
# or "pip install -e ."
```

### Dataset Preparation

It is recommended to symlink the dataset root to your project.

```
Grid_RCNN
├── mmdet
├── tools
├── configs
├── data
│   ├── coco
│   │   ├── annotations
│   │   ├── train2017
│   │   ├── val2017
│   │   ├── test2017
│   ├── VOCdevkit
│   │   ├── VOC2007
│   │   ├── VOC2012

```

## Training and Testing

We provide training and testing scripts and config files for Grid R-CNN. An example configuration file is [here](configs/grid_rcnn_r50_fpn_2x.py), corresponding checkpoint is [here](https://drive.google.com/file/d/1RCtNjb_JruBtl6sCq5w_XXN1e0ksn_f6/view?usp=sharing). Note that the batchsize we used is 64(32 GPUs/2 images per GPU), you could adjust the learning rate and warmup schedule according to your batchsize.

Please see [GETTING_STARTED.md](GETTING_STARTED.md) for more basic usage of mmdetection.

## Results

Training on Res50/101 FPN backbone and Testing on COCO minival. Inference speed is tested on TITANXp GPU cluster.

Method |lr sched| AP | AP@0.5 | AP@0.75 | AP@S | AP@M | AP@L |Inference speed
-- | -- | -- | -- | -- | -- | -- | -- | -- 
Res50-FPN | 2x | 37.4% | 59.3%  | 40.3% | 21.8% | 40.9% | 47.9% | 0.09s
Res50-FPN-Grid R-CNN | 2x | 40.4% | 58.6% | 43.7% | 23.2% | 44.2% | 52.4% | 0.11s
Res101-FPN | 2x | 39.5% | 61.2% | 43.1% | 22.7% | 43.7% | 50.8% | 0.12s
Res101-FPN-Grid R-CNN | 2x | 42.0% | 60.6% | 45.4% | 24.1% | 46.2% | 55.2% | 0.13s


## Citation

If you use our codebase or models in your research, please cite this project.


```
@InProceedings{Lu_2019_CVPR,
author = {Lu, Xin and Li, Buyu and Yue, Yuxin and Li, Quanquan and Yan, Junjie},
title = {Grid R-CNN},
booktitle = {The IEEE Conference on Computer Vision and Pattern Recognition (CVPR)},
month = {June},
year = {2019}
}

@misc{mmdetection2018,
  author =       {Kai Chen and Jiangmiao Pang and Jiaqi Wang and Yu Xiong and Xiaoxiao Li
                  and Shuyang Sun and Wansen Feng and Ziwei Liu and Jianping Shi and
                  Wanli Ouyang and Chen Change Loy and Dahua Lin},
  title =        {mmdetection},
  howpublished = {\url{https://github.com/open-mmlab/mmdetection}},
  year =         {2018}
}
```

## License
Grid R-CNN is released under the [Apache 2.0 license](https://github.com/STVIR/pysot/blob/master/LICENSE). 


