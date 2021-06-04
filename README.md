# ST++

**Implementation for 'ST++: Make Self-training Work Better for Semi-supervised Semantic Segmentation'**

## Getting Started

### Data Preparation

#### Pre-trained Model

[ResNet-50](https://download.pytorch.org/models/resnet50-0676ba61.pth) | [ResNet-101](https://download.pytorch.org/models/resnet101-63fe2227.pth) | [DeepLabv2-ResNet-101](https://drive.google.com/file/d/14be0R1544P5hBmpmtr8q5KeRAvGunc6i/view?usp=sharing)

#### Dataset

[Pascal](http://host.robots.ox.ac.uk/pascal/VOC/voc2012/VOCtrainval_11-May-2012.tar) | [Masks of Pascal (Augmented)](https://drive.google.com/file/d/1ikrDlsai5QSf2GiSUR3f8PZUzyTubcuF/view?usp=sharing) | [Cityscapes](https://www.cityscapes-dataset.com/file-handling/?packageID=3) | [Masks of Cityscapes (Class Mapped)](https://drive.google.com/file/d/1E_27g9tuHm6baBqcA7jct_jqcGA89QPm/view?usp=sharing) 

#### File Organization

```
├── ./pretrained
    ├── resnet50.pth
    ├── resnet101.pth
    └── deeplabv2_resnet101_coco_pretrained.pth
    
├── Pascal
    ├── JPEGImages
    └── SegmentationClass
    
├── Cityscapes
    ├── leftImg8bit
    └── gtFine
```


### Training and Testing

```
export semi_setting='pascal/1_8/split_0'

CUDA_VISIBLE_DEVICES=0,1 python train.py --dataset pascal --data-root [Your Pascal Path] \
  --batch-size 16 --backbone resnet50 --model deeplabv3plus \
  --labeled-id-path dataset/splits/$semi_setting/labeled.txt \
  --unlabeled-id-path dataset/splits/$semi_setting/unlabeled.txt \
  --pseudo-mask-path outdir/pseudo_masks/$semi_setting \
  --save-path outdir/models/$semi_setting
```
This script is for our ST framework. To run ST++, add ```--plus --reliable-id-path outdir/reliable_ids/$semi_setting```.


## Acknowlegement

The DeepLabv2 MS COCO pre-trained model is borrowed and converted from **AdvSemiSeg**.
The image partitions are borrowed from **Context-Aware-Consistency**, **PseudoSeg**. 
Part of the training hyper-parameters and network structures are adapted from **PyTorch-Encoding**.
 
+ AdvSemiSeg: [https://github.com/hfslyc/AdvSemiSeg](https://github.com/hfslyc/AdvSemiSeg).
+ Context-Aware-Consistency: [https://github.com/dvlab-research/Context-Aware-Consistency](https://github.com/dvlab-research/Context-Aware-Consistency).
+ PseudoSeg: [https://github.com/googleinterns/wss](https://github.com/googleinterns/wss)
+ PyTorch-Encoding: [https://github.com/zhanghang1989/PyTorch-Encoding](https://github.com/zhanghang1989/PyTorch-Encoding)


Thanks a lot for their great work!
