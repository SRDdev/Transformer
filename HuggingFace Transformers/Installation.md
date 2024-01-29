
# 🤗 Installation
The Hugging Face Transformers library is a popular open-source library that provides a simple and efficient API to easily leverage state-of-the-art natural language processing models.

This readme file provides instructions on how to install and import the Hugging Face Transformers library & create an account at Huggingface.

You can create an account on huggingface by clicking on this [🖇️Link](https://huggingface.co/)

## Installation
You can install the Hugging Face Transformers library using pip, the Python package installer:

__Transformers__
```bash
pip install transformers
```
Once done you can import it as everyother python library
```python
import transformers
from transformers import pipeline , AutoTokenizer , AutoModel
```

__Datasets__
```bash
pip install datasets
```
Once done you can call this function to see all the available datasets on Huggingface or convert your own dataset into one which is accepted by the open source models.
```python
import datasets
```

## CLI Login 
Huggingface also provides a CLI Login and a Notebook login function. These function allow you to dynamically deploy SOTA models from your Jupyter notebook or colab or terminal.

__Huggingface_hub__
```bash
pip install huggingface_hub
```
```python
from huggingface_hub import notebook_login

notebook_login()
```

## Conclusion

Thats it for this chapter of Installation of Huggingface libraries. 