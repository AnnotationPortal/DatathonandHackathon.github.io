# Code Examples

(C) 2023-2024 by [Damir Cavar](http://damir.cavar.me/)


## Prerequisites

Some of the notebooks require that you have a file `secret.py` in the same folder as the notebook. In this folder you will find the file `secret_template.py`. Rename this file to `secret.py` and fill in the API keys for the different platforms. This requires you to register with the platforms and potentially to make a downpayment for the use of the models.

### AI and Model Platforms

- [Anthropic](https://support.anthropic.com/en/articles/8114521-how-can-i-access-the-anthropic-api)
- [OpenAI](https://openai.com/index/openai-api/)
- [Hugging Face](https://huggingface.co/docs/api-inference/en/index)
- [VoyageAI](https://www.voyageai.com/) (for Anthropic embeddings)


## Agenda

- Texts, words, frequencies, probabilities (Natural Language Toolkit - [NLTK](https://nltk.org/))
	- [Python NLTK - Texts and Frequencies.ipynb](Python+NLTK+-+Texts+and+Frequencies.ipynb)
- Natural Language Processing Pipelines: spaCy and Stanza (and NLTK)
	- [spaCy Tutorial.ipynb](spaCy+Tutorial.ipynb)
	- [Stanza_tutorial.ipynb](Stanza_tutorial.ipynb)
	- [Python Word Sense Disambiguation.ipynb](Python+Word+Sense+Disambiguation.ipynb)
- Bayesian text classification
	- [Bayesian Classifier.ipynb](Bayesian+Classifier.ipynb)
- Logistic Regression for Sentiment Analysis
	- [Scikitlearn_logistic_regression.ipynb](Scikitlearn_logistic_regression.ipynb)
	- [Document Classification Tutorial.ipynb](Document+Classification+Tutorial.ipynb)
- Transformers and Text Classification using BERT (and similar models)
	- [Transformers_example_simple_text_classification.ipynb](Transformers_example_simple_text_classification.ipynb)
- Large Language Models and Generative AI
	- [N-gram Models for Language Models.ipynb](N-gram+Models+for+Language+Models.ipynb)
	- [gpt4_test.ipynb](gpt4_test.ipynb) (ChatGPT-type of model interaction)
	- [claude3_test.ipynb](claude3_test.ipynb) (Claude-3-type of model interaction)
- Word Embeddings for individual (neural) classifier (see spaCy tutorial above for GloVe embeddings)
	- [BERT_vectors.ipynb](BERT_vectors.ipynb) (BERT embeddings for words or text, for similarity computation)
	- [anthropic_vectors.ipynb](anthropic_vectors.ipynb) (Anthropic / VoyageAI type embeddings)
	- [openai_vectors.ipynb](openai_vectors.ipynb) (OpenAI GPT-type embeddings)



