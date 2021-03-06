# SemiNAS: Semi-Supervised Neural Architecture Search

This repository contains the code used for SemiNAS on ImageNet.


## Environments and Requirements
The code is built and tested on Pytorch 1.2

## Searching Architectures
To run the search process, please refer to `runs/search_seminas.sh`, and remeber to modify the line where `DATA_DIR` is defined to the path of imagenet dataset on your device. It requires 4 GPU cards to train.
```
cd runs
bash search_seminas.sh
cd ..
```
After it finishes, you can find the final discovored top architectures in the $OUTPUT_DIR which in the script is `outputs/search_imagenet`. The final discovered top architectures are listed in the file `arch_pool.final` where each line is an architecture represented in sequence. Each token in the sequence represents a specific operation. The mapping of the token and correspoding operation is shown in `utils.py`.

## Training Architectures

### Training the architecture discovered by SemiNAS in our paper
To directly train the architecture discovered by SemiNAS as we report in the paper (denoted as SemiNASNet here), please refer to `runs/train_seminasnet.sh`. Also remeber to modify the line where `DATA_DIR` is defined to the correct path of imagenet dataset on your device. It requires 4 GPU cards to train.
```
cd runs
bash train_seminasnet.sh
cd ..
```

### Training customized architectures
To train a customized architecture (e.g., discovered by SemiNAS of your own run), you can modify the script `runs/train_seminasnet.sh` by replacing the `ARCH` with your customized net architecture sequence string (e.g., top architecture in the `arch_pool.final` file).

## Evaluating the architecture discovered by SemiNAS in our paper
We provide the checkpoint of SemiNASNet in [`Google Dirve`](https://drive.google.com/open?id=13AooVegRLBqYcXwl8usgCOKsWd02V85j)
You can download it and unzip it to the current path:
```
unzip checkpoints.zip
```
To evalute it, please refer to `runs/evaluate_seminasnet.sh`. Remeber to modify the line where `DATA_DIR` is defined to the correct path of imagenet dataset on your device. 
```
cd runs
bash evaluate_seminasnet.sh
cd ..
```

This should report a top-1 accuracy of 76.54% (23.46% error rate) as reported in the paper.
