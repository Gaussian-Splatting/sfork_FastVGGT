<div align="center">
<h2>⚡️ FastVGGT: Training-Free Acceleration of Visual Geometry Transformer</h2>
  
<p align="center">
  <a href="https://quyans.github.io/Drag-Your-Gaussian/"><img src="https://img.shields.io/badge/Project_Page-DYG-green" alt="Project Page"></a>
</p>
  
<img src="assets/maclab_logo.png" alt="Maclab Logo" width="110" style="margin-right: 40px;">
<img src="assets/autolab_logo.png" alt="Autolab Logo" width="110">


**[Media Analytics & Computing Laboratory](https://mac.xmu.edu.cn/)**; **[AUTOLAB](https://zhipengzhang.cn/)**


[You Shen](https://mystorm16.github.io/), [Zhipeng Zhang](https://zhipengzhang.cn/), [Yansong Qu](https://quyans.github.io/), [Liujuan Cao](https://mac.xmu.edu.cn/ljcao/)
</div>


## 📰 News
- [Sep 2, 2025] Code release.

## 🔭 Overview

FastVGGT observes **strong similarity** in attention maps and leverages it to design a training-free acceleration method for long-sequence 3D reconstruction, **achieving up to 4× faster inference without sacrificing accuracy.**

<img src="assets/main.png" alt="Autolab Logo" width="">


## ⚙️ Environment Setup
First, create a virtual environment using Conda, clone this repository to your local machine, and install the required dependencies.


```bash
conda create -n fastvggt python=3.10
conda activate fastvggt
git clone git@github.com:mystorm16/FastVGGT.git
cd FastVGGT
pip install -r requirements.txt
```

Next, prepare the ScanNet dataset: http://www.scan-net.org/ScanNet/

Then, configure the dataset path and VGGT checkpoint path. For example:
```bash
    parser.add_argument(
        "--data_dir", type=Path, default="/data/scannetv2/process_scannet"
    )
    parser.add_argument(
        "--gt_ply_dir",
        type=Path,
        default="/data/scannetv2/OpenDataLab___ScanNet_v2/raw/scans",
    )
    parser.add_argument(
        "--ckpt_path",
        type=str,
        default="./ckpt/model_tracker_fixed_e20.pt",
    )
```


## 💎 Observation

Note: A large number of input_frames may significantly slow down saving the visualization results. Please try using a smaller number first.
```bash
python eval_scannet.py --input_frame 30 --vis_attn_map
```

We observe that many token-level attention maps are highly similar in each block, motivating our optimization of the Global Attention module.

<img src="assets/attn_map.png" alt="Autolab Logo" width="">



## 🏀 Evaluation
Evaluate FastVGGT on the ScanNet dataset with 1,000 input images. The **--merging** parameter specifies the block index at which the merging strategy is applied:

```bash
python eval_scannet.py --input_frame 1000 --merging 0
```

Evaluate Baseline VGGT on the ScanNet dataset with 1,000 input images:
```bash
python eval_scannet.py --input_frame 1000
```
<img src="assets/vs.png" alt="Autolab Logo" width="">


## 🍺 Acknowledgements

- Thanks to these great repositories: [VGGT](https://github.com/facebookresearch/vggt), [Dust3r](https://github.com/naver/dust3r),  [Fast3R](https://github.com/facebookresearch/fast3r), [CUT3R](https://github.com/CUT3R/CUT3R), [MV-DUSt3R+](https://github.com/facebookresearch/mvdust3r), [StreamVGGT](https://github.com/wzzheng/StreamVGGT), [VGGT-Long](https://github.com/DengKaiCQ/VGGT-Long) and many other inspiring works in the community.

- Special thanks to [Jianyuan Wang](https://jytime.github.io/) for his valuable discussions and suggestions on this work.

## ✍️ Checklist

- [ ] Release the evaluation code on 7 Scenes / NRGBD


## ⚖️ License
See the [LICENSE](./LICENSE.txt) file for details about the license under which this code is made available.
