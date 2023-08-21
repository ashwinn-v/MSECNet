# MSECNet: Accurate and Robust Normal Estimation for 3D Point Clouds by Multi-Scale Edge Conditioning (ACMMM2023)

### [arXiv](https://arxiv.org/abs/2308.02237)

Estimating surface normals from 3D point clouds is critical for various applications, including surface reconstruction and rendering. While existing methods for normal estimation perform well in regions where normals change slowly, they tend to fail where normals vary rapidly.  To address this issue, we propose a novel approach called MSECNet, which improves estimation in normal varying regions by treating normal variation modeling as an edge detection problem. MSECNet consists of a backbone network and a multi-scale edge conditioning (MSEC) stream. The MSEC stream achieves robust edge detection through multi-scale feature fusion and adaptive edge detection. The detected edges are then combined with the output of the backbone network using the edge conditioning module to produce edge-aware representations. Extensive experiments show that MSECNet outperforms existing methods on both synthetic (PCPNet) and real-world (SceneNN) datasets while running significantly faster. We also conduct various analyses to investigate the contribution of each component in the MSEC stream. Finally, we demonstrate the effectiveness of our approach in surface reconstruction.

## Setup
The code is tested using Python 3.11 and CUDA 11.8. 

### Create and activate a virtual environment
- python3 -m venv ~/venv/MSECNet  
- source  ~/venv/MSECNet/bin/activate  

### Install necessary packages
- pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118  
- pip3 install h5py pyyaml tensorboardx scipy plyfile 

### Install [pointops](https://github.com/POSTECH-CVLab/point-transformer)
- cd scripts/lib/pointops
- python3 setup.py install

## Datasets
We use [PCPNet](https://github.com/paulguerrero/pcpnet) dataset for training and testing.  
To download it, 
- cd scripts/dataset/pclouds
- python3 download_pclouds.py

Additionally, we apply the PCPNet-trained model to SceneNN and Semantic3D datasets.  
To download them, please refer to [HSurfNet](https://github.com/LeoQLi/HSurf-Net/).   

The dataset directory structure will be 
```
│dataset/
├──pclouds/
│  ├── list
│      ├── ***.txt
│  ├── ***.xyz
│  ├── ***.normals
│  ├── ***.pidx
├──SceneNN/
│  ├── list
│      ├── ***.txt
│  ├── ***.xyz
│  ├── ***.normals
│  ├── ***.pidx
├──Semantic3D/
│  ├── list
│      ├── ***.txt
│  ├── ***.xyz
```

## Training
To train MSECNet on PCPNet: 
```
cd scripts
sh run.sh {put your experiment name}
```
