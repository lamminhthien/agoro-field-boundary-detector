# Install python 3.8 and assign to python bash script
```bash
sudo apt install python3.8
echo "alias python=python3.8" >> ~/.bashrc
source ~/.bashrc
```

# Clone this project, cd to that folder and run command to install dependencies
```bash
git clone git@github.com:lamminhthien/agoro-field-boundary-detector.git
cd agoro-field-boundary-detector
tasks/init.sh
```
# Fix cannot run iii_train_mask_rcnn.py
```bash
# Downgrade version setup-tool python

pip install setuptools==68
pip install --editable .
pip install folium

# Install Gcloud
# sudo apt-get update
# sudo apt-get install apt-transport-https ca-certificates gnupg curl
# curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo gpg --dearmor -o /usr/share/keyrings/cloud.google.gpg
# echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] https://packages.cloud.google.com/apt cloud-sdk main" | sudo tee -a /etc/apt/sources.list.d/google-cloud-sdk.list
# sudo apt-get update && sudo apt-get install google-cloud-cli

```

# Fix issue with CUDA error
(agoro-field-boundary-detector-env) (main) root@C.18033007:/workspace/agoro-field-boundary-detector$ nvcc --version
nvcc: NVIDIA (R) Cuda compiler driver
Copyright (c) 2005-2023 NVIDIA Corporation
Built on Mon_Apr__3_17:16:06_PDT_2023
Cuda compilation tools, release 12.1, V12.1.105
Build cuda_12.1.r12.1/compiler.32688072_0
(agoro-field-boundary-detector-env) (main) root@C.18033007:/workspace/agoro-field-boundary-detector$ nvidia-smi
Wed Feb 19 07:11:07 2025       
+-----------------------------------------------------------------------------------------+
| NVIDIA-SMI 550.54.14              Driver Version: 550.54.14      CUDA Version: 12.4     |
|-----------------------------------------+------------------------+----------------------+
| GPU  Name                 Persistence-M | Bus-Id          Disp.A | Volatile Uncorr. ECC |
| Fan  Temp   Perf          Pwr:Usage/Cap |           Memory-Usage | GPU-Util  Compute M. |
|                                         |                        |               MIG M. |
|=========================================+========================+======================|
|   0  NVIDIA GeForce RTX 3060        On  |   00000000:83:00.0 Off |                  N/A |
| 30%   38C    P8             19W /  170W |       8MiB /  12288MiB |      0%      Default |
|                                         |                        |                  N/A |
+-----------------------------------------+------------------------+----------------------+
                                                                                         
+-----------------------------------------------------------------------------------------+
| Processes:                                                                              |
|  GPU   GI   CI        PID   Type   Process name                              GPU Memory |
|        ID   ID                                                               Usage      |
|=========================================================================================|
+-----------------------------------------------------------------------------------------+
NVIDIA GeForce RTX 3060 with CUDA capability sm_86 is not compatible with the current PyTorch installation.
The current PyTorch install supports CUDA capabilities sm_37 sm_50 sm_60 sm_70.
If you want to use the NVIDIA GeForce RTX 3060 GPU with PyTorch, please check the instructions at https://pytorch.org/get-started/locally/

```bash
pip install --upgrade torch torchvision
```