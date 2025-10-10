# Python Code Debugger using QLoRA Fine-Tuning

**Fine-tuned Meta's Llama 3.2 3B model to debug Python code errors using Stack Overflow data (filtered for errors)**

This project demonstrates parameter-efficient QLoRA fine-tuning on a code debugging task. Trained on Stack Overflow Python questions, the model learns to spot bugs and problems within code, explain the errors, and provide corrected code with explanations.

Here's the dataset used: `koutch/stackoverflow_python`

## Images

### Gradio Interface with Example Debugging
![Debugger Interface](images/Gradio_UI.png)

### Training Output
![Training Output](images/training_output.png)

### Google Colab Notebook Link
https://colab.research.google.com/drive/1x6XLGQT-0DofY_mHH-CN4fbF93o7rCki?usp=sharing

## Technical Stack

- **Base Model**: Llama 3.2 3B Instruct
- **Fine-tuning Method**: QLoRA (4-bit quantization + LoRA adapters)
- **Dataset**: Stack Overflow Python Q&A (filtered for errors)
- **Framework**: HuggingFace Transformers, PEFT, TRL
- **Training Hardware**: NVIDIA A100 GPU (T4 can be used as well, with a few tweaks to the code)
- **Interface**: Gradio

## Project Overview

**1. Data Preparation**
- Loaded Stack Overflow Python dataset (987k questions)
- Filtered for questions that include errors or exceptions (431k questions)
- Selected 12,000 examples for training
- Formatted data into instruction-response pairs

**2. Model Fine-tuning**
- Used Llama 3.2 3B Instruct as the base model
- Applied QLoRA for efficient fine-tuning
- Trained the model to explain errors and provide corrected Python code

**3. Deployment**
- Combined the LoRA adapters with the base model after fine-tuning
- Built an interactive Gradio interface
- Users can paste code and optional error messages to get debugged code with explanations

## Setup Instructions

### Prerequisites

- Python 3.10+
- NVIDIA A100 40GB GPU (T4 can be used as well, with a few tweaks to the code)
- CUDA 11.8 or higher
- HuggingFace token

**Note**: You’ll need to agree to Meta’s terms and conditions and share your contact information to request access to the Llama 3.2 model family. Access is generally granted in a few minutes or so. The model is gated, but the terms are harmless and are just used to ensure it’s not used for any illegal or unethical purposes. You can request access from this link (https://huggingface.co/meta-llama/Llama-3.2-3B-Instruct)


### Installation

Install all dependencies by running the first cell in the notebook on Colab.

### Hugging Face Authentication

1. Get access to Llama 3.2 on HuggingFace
2. Create a token at https://huggingface.co/settings/tokens
3. In Google Colab, add token to Secrets as `HF_TOKEN`

### Running the Notebook

1. Run all cells from top to bottom
2. Training will take approximately 45 minutes on A100 (3-4 hours on T4 after tweaking some parameters in the code)
3. After training, access the model in the Gradio interface

## Limitations

- Works better on Stack Overflow styled questions  
- Might struggle with very tricky or rare bugs  
- Can only handle code snippets, not full projects  
- Can’t actually run code to check fixes

## Future Enhancements

- Support more programming languages  
- Look up rare errors using external sources  
- Train on more datasets

## License

This project is for educational purposes. Llama 3.2 is released under Meta's license. The StackOverflow dataset follows CC BY-SA licensing.