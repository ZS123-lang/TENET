# TENET
This repository is the official implementation for TENET introduced in the paper:

Time-rEversed diffusioN tEnsor Transformer: A new TENET of Few-Shot Object Detection

Shan Zhang, Naila Murray, Lei Wang, Piotr Koniusz

ECCV 2022

## Getting Started
Clone the repo:
```
git clone https://github.com/ZS123-lang/TENET.git
```
### Requirements
Tested under python3.

- python packages
  - pytorch==0.4.1
  - torchvision>=0.2.0
  - cython
  - matplotlib
  - numpy
  - scipy
  - opencv
  - pyyaml==3.12
  - packaging
  - pandas
  - [pycocotools](https://github.com/cocodataset/cocoapi)  — for COCO dataset, also available from pip.
  - tensorboardX  — for logging the losses in Tensorboard
- An NVIDAI GPU and CUDA 9.0 are required. (Do not use other versions)
- **NOTICE**: different versions of Pytorch package have different memory usages.

### Compilation

Compile the CUDA code:

```
cd lib  # please change to this directory
sh make.sh
```

If your are using Volta GPUs, uncomment this [line](https://github.com/roytseng-tw/mask-rcnn.pytorch/tree/master/lib/make.sh#L15) in `lib/mask.sh` and remember to postpend a backslash at the line above. `CUDA_PATH` defaults to `/usr/loca/cuda`. If you want to use a CUDA library on different path, change this [line](https://github.com/roytseng-tw/mask-rcnn.pytorch/tree/master/lib/make.sh#L3) accordingly.

It will compile all the modules you need, including NMS, ROI_Pooing, ROI_Crop and ROI_Align. (Actually gpu nms is never used ...)

Note that, If you use `CUDA_VISIBLE_DEVICES` to set gpus, **make sure at least one gpu is visible when compile the code.**

### Data Preparation

Please add `data` in the `fsod` directory and the structure is :

  ```
  YOUR_PATH
      └── fsod
            ├── code files
            └── data
                  ├──── fsod
                  |       ├── annotations
                  │       │       ├── fsod_train.json
                  │       │       └── fsod_test.json
                  │       └── images
                  │             ├── part_1
                  │             └── part_2
                  │ 
                  └──── pretrained_model
                          └── model_final.pkl (from detectron model zoo: End-to-End Faster & Mask R-CNN Baselines R-50-C4 Faster 2x model)
  ```  
You can download the model_final.pkl from here: [Model link](https://dl.fbaipublicfiles.com/detectron/35857281/12_2017_baselines/e2e_faster_rcnn_R-50-C4_2x.yaml.01_34_56.ScPH0Z4r/output/train/coco_2014_train%3Acoco_2014_valminusminival/generalized_rcnn/model_final.pkl)
