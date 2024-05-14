
This Python script uses the Hugging Face pipline, Transformer and Google Generative AI library to interact with a generative model and perform translations.


## Setup For Hugging Face

First, import the necessary library:

```python
from transformers import pipeline
```

Next, create a translation pipeline:

```python
translation_pipeline = pipeline('translation_en_to_')
```

This script sets up a translation pipeline that can be used to translate English text into other languages. The specific target language is not specified in the provided code, but it would typically be appended to the 'translation_en_to_' string when calling the `pipeline` function. For example, to translate English to French, you would use `pipeline('translation_en_to_fr')`.

## Setup For Gemini API

First, import the necessary library:

```python
import google.generativeai as genai
```

Next, configure your API key:

```python
genai.configure(api_key="API-KEY-HERE")
```



##

 Model Configuration

Set up the model with the desired configuration:

```python
generation_config = {
  "temperature": 1,
  "top_p": 0.95,
  "top_k": 64,
  "max_output_tokens": 8192,
}
```

## Safety Settings

Define safety settings to block certain categories of harmful content:

```python
safety_settings = [
  {
    "category": "HARM_CATEGORY_HARASSMENT",
    "threshold": "BLOCK_MEDIUM_AND_ABOVE"
  },
  {
    "category": "HARM_CATEGORY_HATE_SPEECH",
    "threshold": "BLOCK_MEDIUM_AND_ABOVE"
  },
  {
    "category": "HARM_CATEGORY_SEXUALLY_EXPLICIT",
    "threshold": "BLOCK_MEDIUM_AND_ABOVE"
  },
  {
    "category": "HARM_CATEGORY_DANGEROUS_CONTENT",
    "threshold": "BLOCK_MEDIUM_AND_ABOVE"
  },
]
```

## Model Instantiation

Instantiate the generative model with the specified configuration and safety settings:

```python
model = genai.GenerativeModel(model_name="gemini-1.5-pro-latest",
                              generation_config=generation_config,
                              safety_settings=safety_settings)
```

## Starting a Chat

Start a chat with the model:

```python
convo = model.start_chat(history=[])
```

## Sending a Message

Define a user message and create a prompt for translation:

```python
user="hello my name is muneeb"
prompt = "Text to be translated:"+user+"Target Languages:English Mandarin Chinese Hindi Spanish Arabic Bengali Russian Portuguese Urdu Indonesian Please provide the translations in the order listed above."
convo.send_message(prompt)
```

## Printing the Response

Print the last message from the model:

```python
print(convo.last.text)
```
