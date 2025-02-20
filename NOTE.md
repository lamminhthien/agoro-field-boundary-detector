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

## Google Cloud SDK Setup Guide

### Installing Google Cloud SDK on macOS

1. Install using Homebrew:
```bash
brew install --cask google-cloud-sdk
```

2. Verify the installation:
```bash
gcloud version
```

### Initial Setup and Configuration

1. Initialize gcloud:
```bash
gcloud init
```

2. Authenticate with your Google Account:
```bash
gcloud auth login
```

3. List available projects:
```bash
gcloud projects list
```

### Creating a New Project

1. Create a new project:
```bash
gcloud projects create PROJECT_ID --name="Project Name"
```
Replace `PROJECT_ID` with your desired project ID (must be unique across all Google Cloud)

2. Set the current project:
```bash
gcloud config set project PROJECT_ID
```

### Setting Up Application Default Credentials (ADC)

1. Set up application default credentials:
```bash
gcloud auth application-default login
```

2. Set quota project for ADC:
```bash
gcloud auth application-default set-quota-project PROJECT_ID
```

### Enable Required APIs

1. Enable necessary APIs for your project:
```bash
# Example: Enable Cloud Storage API
gcloud services enable storage.googleapis.com

# Example: Enable Cloud Vision API
gcloud services enable vision.googleapis.com
```

### Managing Service Accounts (Optional)

1. Create a service account:
```bash
gcloud iam service-accounts create SERVICE_ACCOUNT_NAME \
    --display-name="Service Account Display Name"
```

2. Generate service account key:
```bash
gcloud iam service-accounts keys create key-file.json \
    --iam-account=SERVICE_ACCOUNT_NAME@PROJECT_ID.iam.gserviceaccount.com
```

### Useful gcloud Commands

- List configurations:
```bash
gcloud config list
```

- Switch between accounts:
```bash
gcloud config set account ACCOUNT
```

- List authenticated accounts:
```bash
gcloud auth list
```

### Troubleshooting

If you encounter quota errors:
1. Ensure you have billing enabled for your project
2. Verify API enablement in Google Cloud Console
3. Check if you have set the correct quota project:
```bash
gcloud auth application-default set-quota-project PROJECT_ID
```

To revoke credentials if needed:
```bash
gcloud auth revoke
gcloud auth application-default revoke
```