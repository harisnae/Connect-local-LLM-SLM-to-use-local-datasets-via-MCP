# Link local LM with Local Data via MCP (Incomplete)
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
Download a model GGUF from Huggingface, in this case we downloading the GGUF of Microsoft's Phi-4 

```
wget https://huggingface.co/microsoft/phi-4-gguf/resolve/main/phi-4-q4.gguf

```
## Running the model in Python
Activate python interpreter
```
python3
```
Run the following script in python interpreter for Text completion
```
from llama_cpp import Llama

model = Llama(model_path="/Path/to/model-gguf-file/phi-4-Q2_K.gguf")

output = model("Q: Explain the de Sitter thermodynamics using the Painlev´e-Gullstrand (PG) coordinates, where the metric has no singularity at the cosmological horizon", max_tokens=1000, stop=["Q:"], echo=False)

print(output['choices'][0]['text'])
```

