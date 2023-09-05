# Indoor Semantic Segmentation Based on Swin-Transformer

## Usage

### Dataset and pretrained models

Download the converted dataset from [here](https://pan.baidu.com/s/12kvZb-s8wrMaOOaj489IOg&pwd=swin) and unzip it.

Download the pretrained models from [here](https://pan.baidu.com/s/1ivGC8JA1OBXYpP2bB08VCQ&pwd=swin) and unzip it.

### Our Models

Download our models from [here](https://pan.baidu.com/s/1r9IlANY3zBR-rfVjRvp8Uw&pwd=swin).

**Note: After the procedures above, the structure of the project should look like:**

```
SwinTransformerForINSS
├─ data
│  └─ nyudv2
│     ├─ nyudv2_test_depth
│     ├─ nyudv2_test_images
│     ├─ nyudv2_test_label40
│     ├─ nyudv2_train_depth
│     ├─ nyudv2_train_images
│     └─ nyudv2_train_label40
├─ inss_configs
├─ mmcv_custom
├─ mmseg
├─ pre_trained_models
│  ├─ swin_base_patch4_window7_224_22k.pth
│  ├─ swin_large_patch4_window7_224_22k.pth
│  └─ swin_small_patch4_window7_224_22k.pth
├─ resources
├─ results
│  ├─ upernet_swin_large_patch4_window7_640x480_160k_nyudv2_40_rgb_depth.pth
│  └─ upernet_swin_large_patch4_window7_640x480_160k_nyudv2_40_rgb_depth.py
├─ tools
└─ work_dirs
```

### Installation

1. Requirements

   - Linux
   - Python 3.8
   - PyTorch 1.8.0
   - CUDA 11.1
   - MMCV-FULL 1.3.0
   - matplotlib
   - terminaltables
   - timm

2. Build environment

   - Use the following command to install PyTorch and relative dependencies:

     ```
     pip install torch==1.8.0+cu111 torchvision==0.9.0+cu111 torchaudio==0.8.0 -f https://download.pytorch.org/whl/torch_stable.html
     ```

   - MMCV can be downloaded from the [here](https://download.openmmlab.com/mmcv/dist/cu111/torch1.8.0/index.html), then: 

     ```
     pip install mmcv_full-1.3.0-cp38-cp38-manylinux1_x86_64.whl
     ```

   - At last, the following command in SwinTransformerForINSS dir should be run before getting started.

     ```
     pip install -v -e .
     ```

### Train

- Run

  ```
  python tools/train.py <CONFIG_FILE> [--options model.pretrained=<PRETRAIN_MODEL> [model.backbone.use_checkpoint=True] [other optional arguments]]
  ```

  example:

  ```
  python tools/train.py inss_configs/upernet_swin_large_patch4_window7_640x480_160k_nyudv2_40_rgb_depth.py
  ```

### Test

- Run

  ```
  python tools/test.py <CONFIG_FILE> <SEG_CHECKPOINT_FILE> --eval mIoU
  ```

  example, test our results: 

  ```
  python tools/test.py results/upernet_swin_large_patch4_window7_640x480_160k_nyudv2_40_rgb_depth.py results/upernet_swin_large_patch4_window7_640x480_160k_nyudv2_40_rgb_depth.pth --eval mIoU
  ```

- The results should be:

  ```
  +--------+-------+------+-------+
  | Scope  | mIoU  | mAcc | aAcc  |
  +--------+-------+------+-------+
  | global | 52.44 | 65.8 | 77.53 |
  +--------+-------+------+-------+
  ```

  

