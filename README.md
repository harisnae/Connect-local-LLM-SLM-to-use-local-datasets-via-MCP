# Local LLM with Local Data via MCP

A comprehensive guide for connecting locally deployed Large Language Models (LLMs) with local datasets using the Model Context Protocol (MCP).

## 🎯 Overview

This repository provides step-by-step instructions for:
- Setting up a local development environment with Conda
- Installing and configuring llama-cpp-python
- Running local language models (demonstrated with Microsoft Phi-4)
- Connecting models with local data sources via MCP *(coming soon)*

## 📋 Prerequisites

- Ubuntu 22.04+ (tested on 22.04.5 LTS)
- 8GB+ RAM (16GB recommended for larger models)
- Internet connection for initial setup
- Basic familiarity with command line operations

## 🛠️ Installation Guide

### Step 1: Miniconda Setup

1. **Download Miniconda:**
   ```bash
   wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
   ```

2. **Install Miniconda:**
   ```bash
   bash Miniconda3-latest-Linux-x86_64.sh
   ```
   
   Follow the interactive prompts. Accept the license and default installation location unless you have specific requirements.

3. **Reload your shell configuration:**
   ```bash
   source ~/.bashrc
   ```

### Step 2: Environment Setup

1. **Create a dedicated conda environment:**
   ```bash
   conda create -n llama python=3.10
   ```

2. **Activate the environment:**
   ```bash
   conda activate llama
   ```

3. **Add conda-forge channel for better package availability:**
   ```bash
   conda config --add channels conda-forge
   ```

4. **Verify your setup:**
   ```bash
   conda env list
   conda config --show channels
   ```

### Step 3: llama-cpp-python Installation

1. **Install llama-cpp-python:**
   ```bash
   conda install llama-cpp-python
   ```

   > **Note:** If you have a CUDA-capable GPU, consider installing the CUDA version for better performance:
   > ```bash
   > CMAKE_ARGS="-DLLAMA_CUBLAS=on" pip install llama-cpp-python
   > ```

2. **Download a model (Microsoft Phi-4 example):**
   ```bash
   mkdir -p models
   cd models
   wget https://huggingface.co/microsoft/phi-4-gguf/resolve/main/phi-4-q4.gguf
   cd ..
   ```

## 🚀 Quick Start

### Basic Text Completion

Create a file called `test_model.py`:

```python
from llama_cpp import Llama

# Initialize the model
model = Llama(
    model_path="./models/phi-4-q4.gguf",
    n_ctx=2048,  # Context window
    n_threads=4,  # Number of CPU threads
    verbose=False
)

# Generate text
prompt = "Q: Explain the de Sitter thermodynamics using the Painlevé-Gullstrand (PG) coordinates"

output = model(
    prompt,
    max_tokens=1000,
    stop=["Q:", "\n\n"],
    echo=False,
    temperature=0.7
)

print("Response:")
print(output['choices'][0]['text'])
```

Run the script:
```bash
python test_model.py
```

### Interactive Chat Session

```python
from llama_cpp import Llama

model = Llama(model_path="./models/phi-4-q4.gguf", verbose=False)

print("Chat with Phi-4 (type 'quit' to exit)")
print("-" * 40)

while True:
    user_input = input("You: ")
    if user_input.lower() == 'quit':
        break
    
    response = model(f"Human: {user_input}\nAssistant:", 
                    max_tokens=500, 
                    stop=["Human:", "\n\n"],
                    temperature=0.7)
    
    print(f"Assistant: {response['choices'][0]['text'].strip()}")
```

## 📊 Model Performance Tips

- **Memory Usage:** Quantized models (Q4, Q8) balance performance and memory usage
- **Context Length:** Adjust `n_ctx` based on your use case and available RAM
- **Threading:** Set `n_threads` to your CPU core count for optimal performance
- **GPU Acceleration:** Use CUDA or Metal builds for significant speed improvements

## 🔧 Troubleshooting

### Common Issues

**Installation fails on conda install:**
```bash
# Try pip installation instead
pip install llama-cpp-python
```

**Model loading errors:**
- Verify the model file path is correct
- Ensure sufficient RAM is available
- Check model file integrity with `ls -la models/`

**Slow inference:**
- Reduce model size (try Q2_K or Q4_K variants)
- Increase `n_threads` parameter
- Consider GPU acceleration

## 🗺️ Roadmap

- [x] Basic local LLM setup
- [x] Model inference examples
- [ ] MCP integration for local data sources
- [ ] Advanced prompting techniques
- [ ] Performance optimization guide
- [ ] Docker containerization
- [ ] Web interface development

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request. For major changes, please open an issue first to discuss what you would like to change.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- [llama.cpp](https://github.com/ggerganov/llama.cpp) for the efficient C++ implementation
- [Microsoft](https://huggingface.co/microsoft/phi-4-gguf) for the Phi-4 model
- [Hugging Face](https://huggingface.co/) for model hosting

---

**⚠️ Status:** This repository is actively under development. MCP integration features are coming soon!


