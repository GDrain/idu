# Information Discrimination Units (IDU)
**Learning to Discriminate Information for Online Action Detection, CVPR 2020**  
Hyunjun Eun, Jinyoung Moon, Jongyoul Park, Chanho Jung, Changick Kim  
[[`arXiv`](https://arxiv.org/abs/1912.04461)]

## Introduction
<div align="center">
  <img src="figures/framework.png" width="1000px" />
</div>

This is official implementation of Information Discrimintation Units (IDU). For online action detectoin, we investigate on the question of "how RNNs can learn to explicitly discriminate relevant information from irrelevant information for detecting actions in the present". To this end, we propose a novel recurrent unit that extends GRU with a mechanism utilizing current information and an early embedding module. We perform extensive experiments on two benchmark datasets, where our Information Discrimination Networks (IDN) achieve stateof-the-art performances of 86.1% mcAP and 60.3% mAP on [TVSeries](https://homes.esat.kuleuven.be/psi-archive/rdegeest/TVSeries.html) and [THUMOS-14](https://www.crcv.ucf.edu/THUMOS14/), respectively.

## Updates
**30 May, 2020**: Initial commit

## Installation

### Prerequisites
- Ubuntu 16.04  
- Python 3.6.8   
- CUDA 10.0  
- cuDNN 7.5

### Requirements
- tensorflow==1.13.1  
- scipy==1.3.0

### Patches
We provide three patch files in the 'patch' folder. Replace original files in tensorflow to these files. Each folder name in the 'patch' folder describes the directory where files need to be located in.
- \_\_init\_\_.py in 'tensorflow/\_api/v1/keras/layers'
- \_\_init\_\_.py and recurrent.py in 'tensorflow/python/keras/layers'

## Training
The code for training is not included in this repository, and we cannot release the full training code since the research is involved in the project.

### Input Features
Download our extracted features here. On both [TVSeries](https://homes.esat.kuleuven.be/psi-archive/rdegeest/TVSeries.html) and [THUMOS-14](https://www.crcv.ucf.edu/THUMOS14/) datasets, we extract video frames at 24 fps and set the number of frames in each chunk N to 6. We use 16 chunks (i.e., T=15), which are 4 seconds long, for the input of IDN. We use a two-stream network as a features extractor. In the two-stream network, one stream encodes appearance information by taking the center frame of a chunk as input, while another stream encodes motion information by processing an optical flow stack computed from an input chunk. Among several two-stream networks, we employ the [TSN models](https://github.com/yjxiong/temporal-segment-networks) pretrained on ActivityNet-v1.3 and Kinetics datasets.


### Trained Models
Download our trained models here and locate in '{dataset name}'/models/'.

## Testing

__For TVSeries__  
```
python tvseries/test.py --feat_type incepv3
```
The code provides the results of our IDN, '__mcAP of 86.1%__'.  

__For THUMOS-14__  
```
python thumos14/test.py --feat_type incepv3
```
The code provides the results of our IDN, '__mAP of 60.3%__'.  


## Citing IDU
Please cite our paper in your publications if it helps your research:

```BibTeX
@article{eun2020idu,
  title={Learning to Discriminate Information for Online Action Detection},
  author={Eun, Hyunjun and Moon, Jinyoung and Park, Jongyoul and Jung, Chanho and Kim, Changick},
  booktitle={CVPR},
  year={2020}
} 
```
