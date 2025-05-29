---
title: Image Classification using HuggingFace
categories: [jupyter, python, ]
tags: [jupyter notebook, python, machine learning, ai, hugging face, pipeline]    # TAG names should always be lowercase
layout: page
permalink: /posts/:path
---
This is a easy project that uses the HuggingFace CLI to classify car images. You submit the image url, and the model will predict the car make, model, and year.

**note**: the outline below but do not be intermediated. I broke down the steps as much as I could.


### outline
1. environment setup
2. install and import needed packages
3. loading model and processor
4. loading and extracting image features
5. making prediction
6. next level

### 1. Environment setup
We are going to need a virtual environment for our project. This is crucial for controlling packages and isolating your dev environment from the rest of your computer.

#### ✅ prerequisites
- make sure you have Python 3.3+ installed. Check with:
```bash
python --version
# or
python3 --version
```

#### linux/macOS

- navigate to your project directory
- create a virtual env
```bash
python -m venv venv
```

- activate virtual env
```bash
source venv/bin/activate
```

- to deactivate when done
```bash
deactivate
```

#### windows
- navigate to your project directory
- create virtual env
```bash
python -m venv venv
```

- activate virtual env
```bash
venv\Scripts\activate
```

- to deactivate when done
```bash
deactivate 
```

### 2. install and import packages
**install** the following packages
- `transformers` from **Hugging Face** - offers pretrained models
- `torch` - needed for speed during inference
- `pillow` - python library for images (PIL)

use the following command
```bash
pip install transformers torch pillow
```
**import** our packages: in a python file, write (**don't copy and paste code if you want to learn**) the following code
```python
from transformers import CLIPProcessor, CLIPModel
from PIL import Image #import python image lib to load image
import requests
from io import BytesIO #wrapper to make image a file instead of just raw
import torch
from stanford_car_labels import car_labels
```

**important** the `stanford_car_labels` is an array list with all the cars our model is trained on. You can download the list from the link below. After the download, save it to your project folder and import it as we did above.
[stanford_car_labels.py](https://github.com/LuckyKhoza-crypto/luckykhoza-crypto.github.io/blob/56043151cc66ca11fe6dadf912c9f1714b0810b1/stanford_car_labels.py)

### sense check: the hardest part of this project is done.

### 3. loading model and processor
we are using the `CLIModel` and `CLIProcessor` from huggingface.

`CLIModel` is a deep learning neural network pretrained using OpenAI's CLI Architecture. It's used for transforming images and texts into the interchangeable vectors. In our case, it calculates the similarity between the image we submit and the array of cars our model is trained on.
```python
model = CLIPModel.from_pretrained("openai/clip-vit-base-patch32") # pretrained model
```

`CLIProcessor` is a helper class that simplifies processing. It takes text and images, normalizes and preprocesses (tokenizing) them for the model.
```python
processor = CLIPProcessor.from_pretrained("openai/clip-vit-base-patch32") # base model processor
```

### 4. loading image features
find a car image url on the web and paste it for the `url` variable
```python
url = '<image url>'
```
open the url and convert the image to RGB because that's the format CLIP expects.
```python
image = Image.open(BytesIO(requests.get(url).content)).convert('RGB')
```

### 5. making a prediction
now we have our image, model, and processor ready to run and make a prediction

#### process image
we load our CLI processor with our car description,and the image we uploaded. `return_tensors` is set to return the data in a tensor form, it does it for us automatically. `padding` tells the tokenizer to add padding to all inputs so they are the same size, this allows them to batch together
```python
inputs = processor(text=car_labels, images=image, return_tensors="pt", padding=True)
```

#### extracting image features
we now have our `input` ready for our model. we can start making our calculations for similarity using our model

`no_grad()`: ensures we're not calculating the gradient ourselves, which saves memory
`logits_per_image`: this is the dot product result between the image and the cars array list. The higher the result, the better the match.
`softmax(dim=1)`: turns raw logits (dot product) into probability numbers between 0 and 1, telling us the similarity score. The higher the number, the better the match.
```python
with torch.no_grad():
    outputs = model(**inputs) # parse the processed inputs (tensors) into the model to get the raw predictions
    logits_per_image = outputs.logits_per_image  
    probs = logits_per_image.softmax(dim=1) # probability for each car label to image
```

#### prediction
below is how we show our prediction
```python
best_idx = probs.argmax().item() # returns index with highest probability score
print(f'Predicted car: {car_labels[best_idx]}') # prints car from the select index
print(f'Confidence score: {probs[0, best_idx].item():.4f}') 
```

when you run this code, you will see the two above statements printed

#### top 5
the processor used is the base one, it's not accurate most of the time but it gives you a glimpse of what ML models can do.

the code below prints the top 5 matches from the probability calculations.

```python
top5 = torch.topk(probs, 5)
for i, idx in enumerate(top5.indices[0]):
    print(f"{i+1}. {car_labels[idx]} ({top5.values[0][i]:.2f})")
```

### 6. next level
from this point, you can go ahead and improve your image classifier.
- think about using a better model and processor for the project
- build a Flask or CLI app that allows users to input their image url.