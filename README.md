# Link local LM with Local Data via MCP
This repository is a guide to connecting a locally deployed LLM (Large Language Model) / SLM (Small Language Model) with local datasets using MCP (Model Context Protocol).

## Conda Installation
I will be using Conda on Ubuntu 22.04.5 LTS (Linux x86-64)
```
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh

cd miniconda

```
Install Miniconda by running

```
bash Miniconda3-latest-Linux-x86_64.sh

```
After installation, re-read bash
```
source ~/.bashrc

```
Create a conda environment named "llama"
```
conda create -n llama
```
Verify the installed Conda environments
```
conda env list
```
Activate "llama" Conda environments
```
conda activate llama
```
Adding conda forge in 'channels' list
```
conda config --add channels conda-forge
```
Verify the channels
```
conda config --show channels
``````
## llama-cpp-python Installation
Install llama-cpp-python in conda "llama" environment
```
conda install llama-cpp-python
```
