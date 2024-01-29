
# 🤗 Pipeline Function
In this lecture we will take a look at the Pipeline function form HuggingFace.

###  Tokenization

The tokenization process has many steps , first the sentence is split into small chunks called “tokens”. These tokens contain all the special characters , words , etc from the input.

Then the tokenizer adds Special Tokens at the beginning (CLS) and end (SEP) of sentence. Lastly the tokenizer maps each token to unique id from the vocabulary of the pretrained model.

__Auto Tokenizer API__
```python
from transformers import AutoTokenizer

checkpoint = "distilbert-base-uncased-finetuned-sst-2-english"
tokenizer = AutoTokenizer.from_pretrained(checkpoint)


raw_inputs = [
	"I have been wating for this hugging face course on Transformers",
	"I love TensorFlow & HuggingFace"
]

inputs = tokenizer(raw_inputs,padding=True,truncation=True,return_tensor="tf")
```

### Model

The Auto Model API has a `from_pretrained` method, which downloads and caches the model's configuration and pretrained weights. However, it only instantiates the body of the model, i.e. the part without the pretraining head. `torch.size([2,16,768])` It will output a high-dimensional tensor that is a  representation of the sentences passed, but which is not directly useful for our classification  problem. Here the tensor has two sentences, each of sixteen tokens and the last dimension is  the hidden size of our model 768.

__Auto Model API__
```python
from transformers import TFAutoModel

checkpoint = "distilbert-base-uncased-finetuned-sst-2-english"
model = AutoModel.from_pretrained(checkpoint)
outputs = model(inputs)
outputs.last_hidden_state.shape
```

To get the output linked to our classification problem we need to use `AutoModelForSequenceClassification` class 

```python
from transformers import TFAutoModelForSequenceClassification 

checkpoint = "distilbert-base-uncased-finetuned-sst-2-english"
model = AutoModel.from_pretrained(checkpoint)
outputs = model(inputs)
print(outputs.logits)
```

### Postprocessing
The last step of the pipeline is to convert the logits from the model into probabilities which can be easier to read. This is done by using a SoftMax layer over them. This gives us values which are in between 0 to 1.

```python
import tensorflow as tf
predictions = tf.math.softmax(outputs.logits,axis=1)
print(predictions)

#To know which output is +ve & which is -ve
model.config.id2label
```