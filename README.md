
# A product names generator using a Tokenizer and an Encoder Decoder Transformer from scratch
### Trying a bunch of options like Huggingface T5 model, RoBERTa model from scratch and an Encoder Decoder model with RoBERTa

## Problem Statement
For a few weeks I was investigating different models and alternatives in Huggingface to train a text generation model. We have a short list of products with their description and our goal is to obtain the name of the product. I did some experiments with the Transformer model in Tensorflow as well as the T5 summarizer. Finally, in order to deepen the use of Huggingface transformers, I decided to approach the problem with a somewhat more complex approach, an encoder decoder model. Maybe it was not the best option, but I wanted to learn new things about huggingface Transformers.

First, I must admit that probably a text generation problem is not usually approached with this kind of solution, using encoders models like BERT or RoBERTa. But in this problem we are not going to generate “free text”, so we can simplify our task. We are looking for a subset of words from the product description to compose the product name and our full vocabulary is present in the input data. From this point of view, we can encode the product description into a vector representation and decode it to a text name. Therefore, the use of an encoder-decoder is presented as an option to evaluate.

Our problem can be represented as a sequence-to-sequence problem, where we need to find a mapping of an input sequence (the product description) to an output sequence (the product name). In a Hugingface blog post [“Leveraging Pre-trained Language Model Checkpoints for Encoder-Decoder Models”](https://huggingface.co/blog/warm-starting-encoder-decoder) you can find a deep explanation and experiments building many encoder-decoder model using BERT or GTP2 transformers model. I highly recommend you to read it.

## Dataset
As we mentioned before, our dataset contains around 31.000 items, about clothes from an important retailer, including a long product description and a short product name, our target variable. First, we execute a exploratory data analysis and we can observe that the count of rows with outliers values is a small number. The count of words looks like a left skewed distribution, 75% of rows in the range 50–60 words and a maximum about 125 words. The target variable contains about 3 to 6 words.

## Tokenizer, Masked Language Modeling and the Encoder Decoder 
For our experiment we are going to train from scratch a RoBERTa model, it will become the encoder and the decoder of a future model. But our domain is very specific, words and concepts about clothes, shapes, colors, … Therefore, we are interested in defining our own tokenizer created from our specific vocabulary, avoiding to include more common words from others domain or use cases which are irrelevant for our final purpose.

We can describe our training phase in three main steps:
•	Create and train a byte-level, Byte-pair encoding tokenizer with the same special tokens as RoBERTa
•	Train a RoBERTa model from scratch using Masked Language Modeling, MLM.
•	Warm start and fine tune an encoder decoder model based on our RoBERTa pretrained model.


## Notebooks
**WORK IN PROGRESS**
- "Text_Generation_EDA": Exploratory Data Analysis on a text dataset, to improve our knowledge about the problem
- "Text_Generation_Data_Preprocessing": Text cleaning and processing before training
- "Transformer model for Text generation": Build a transformer model for text generation. **In progress**
- "T5 transformer for text generation": Train a T5 model to generate product names. **In progress**
- "RoBERTa MLM and Tokenizer train for Text generation": Create a custom tokenizer and train a RoBERTa model from scratch applying *Masked Language Modeling"
- "RoBERTa MLM and Tokenizer train for Text generation DatasetByText": It is the same notebook but using a text file as our training dataset for our RoBERTa model
- "RoBERTa Encoder Docoder MLM FineTuned for Text generation": Fine tune an Encoder Decoder model. **In progress**

## License
This repository is under the GNU General Public License v3.0.

This repository was developed by Eduardo Muñoz Sala 