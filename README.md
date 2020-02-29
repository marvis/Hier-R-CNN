# Hier-R-CNN
Hier R-CNN: Instance-level Human Parts Detection and A New Benchmark (under review)

In this repository, we release the COCO Human Parts dataset and Hier R-CNN code in Pytorch.

- Hier R-CNN output
<p align="center"><img width="75%" src="data/output.png" /></p>

- Hier R-CNN architecture
<p align="center"><img width="90%" src="data/hier_rcnn.png" /></p>



## Installation
- 8 x TITAN Xp GPU
- pytorch1.1
- python3.6.8

Install Hier R-CNN following [INSTALL.md](https://github.com/soeaver/Hier-R-CNN/blob/master/INSTALL.md).


## ImageNet pretrained weight

- [R50](https://dl.dropbox.com/s/s7f4vyfybyc9qpr/vovnet39_statedict_norm.pth?dl=1)
- [R101](https://dl.dropbox.com/s/b826phjle6kbamu/vovnet57_statedict_norm.pth?dl=1)
- [X101-32x8d](https://dl.dropbox.com/s/ve1h1ol2ge7yfta/vovnet75_statedict_norm.pth.tar?dl=1)


## Results and Models
| Backbone  | Multi-scale training | Inference time (ms) | Box AP (AP/APs/APm/APl)  | DOWNLOAD |
|----------|:---------------:|:-------------------:|:------------------------:| :---:|
| R-50-FPN-1x       | No           | 84                  | 37.5/21.3/40.3/49.5      | - |
 **V-39**-FPN-1x       | No           |**82**                 | 37.7/**22.4**/41.8/48.4      | [link](https://dl.dropbox.com/s/8n0wyypfggliplw/FCOS-V-39-FPN-1x.pth?dl=1)|
 ||
| R-101-FPN-2x       | Yes           | 104                  | 41.3/25.0/45.5/53.0      | -                          
| **V-57**-FPN-2x        |Yes           | **91**                  | 41.6/**25.9**/45.6/53.1      |  [link](https://dl.dropbox.com/s/f1posfwebb2ynnp/FCOS-V-57-MS-FPN-2x.pth?dl=1)|
||
| R-101-32x8d-FPN-2x        | Yes           |171                   | 42.5/26.0/46.1/54.2      | -  |
| **V-93**-FPN-2x        | Yes           | **113**                  |   42.1/**26.2**/46.0/53.9    | [link](https://dl.dropbox.com/s/2v7go4lenvvjd1s/FCOS-V-93-MS-FPN-2x.pth?dl=1)|


## Training

To train a model with 8 GPUs run:
```
python -m torch.distributed.launch --nproc_per_node=8 tools/train_net.py --cfg cfgs/mscoco_humanparts/e2e_hier_rcnn_R-50-FPN_1x.yaml
```


## Evaluation

### multi-gpu evaluation,
```
python tools/test_net.py --cfg ckpts/mscoco_humanparts/e2e_hier_rcnn_R-50-FPN_1x/e2e_hier_rcnn_R-50-FPN_1x.yaml --gpu_id 0,1,2,3,4,5,6,7
```

### single-gpu evaluation,
```
python tools/test_net.py --cfg ckpts/mscoco_humanparts/e2e_hier_rcnn_R-50-FPN_1x/e2e_hier_rcnn_R-50-FPN_1x.yaml --gpu_id 0
```

