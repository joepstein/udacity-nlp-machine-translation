# Udacity NLP Nanodegree - Machine Translation

## File Structure

* |- `machine-translation.ipynb`
* |- `machine-translation.html`
* |- `README.md`
* |- `data/`
* | |- `small_vocab_en`
* | |- `small_vocab_fr`

## Introduction
The following repository shows one of the projects that I worked on in order to receive the Udacity NLP Nanodegree. The previous project, a Hidden Markov Model Part of Speech Tagger, emphasized advanced statistical techniques analyzing the text data. In the following sections, neural networks are discussed, in relation to NLP. The following project features multiple neural network models, increasing in complexity, leveraging Keras. The final model features encoder-decoder technology, and Bidirectional layers in the neural network.

## Project Overview
In this project, we will be exploring how to create a Neural Network Model for Machine Tranlsation of simple sentences in English to French.

### Text Preprocessing
The text preprocessing step features a simple pipeline model. There is a fit transform done using nltk Tokenizer function, which is then padded, with `pad_sequences`. The following data, set of English or French sentences, will now be represented as a vector with each value corresponding to a word as its index in the vocabulary, with trailing 0s. The trailing 0s, from padding, are a consequence of having sentences of different lengths, and the input of the model expecting consistency in size. So, 0s are added until each sentence is as long as the longest sentence.

### Simple RNN Model
The "simple" RNN model, simple because I am leveraging Keras, uses a Gated Recurrent Unit RNN as the first layer. The GRU is used as a light-weight LSTM (Long Short Term Memory), reducing complexity in the algorithm, but introducing a memory step, to take into account how previous data. The unit of the GRU updates iteratively, as the RNN passes between nodes within its network layer. Lastly, the model is passed through a TimeDistributed Dense layer, allowing the values to be flattened, and the "logits", representing the output of the tranlsation, in vecorized format.

This model achieved the following accuracy: `83.08%`

### RNN Model with an Embedding Layer
This model is the same as the above model, with the exception of an Embedding layer. Normally, these words are represented in a dimesnionality as large as the vocabulary of the dataset. So, a layer is added with fewer nodes in order to embed the space into a lower dimensionality, and eliminate unnecessary colinearity across other columns in a much higher dimensionality.

This model achieved the following accuracy: `91.61%`

### Bidirectional RNN
The following model is a spin off on the original "simple" model, but wrapping the GRU step in a Bidirectional layer. Allowing the calculation of each node to take into account the previous nodes weighted values, as well as the node directly in front of it. Interestingly, when only using 1 layer, this model is hardly any better than the first model.

This model acheived the following accuracy: `83.79%`

### Simple Encoder Decoder
The following model introduces new layers, and general architecture into the original model. The model does use two layers of GRUs, but also the output of the second layer is "encoded". The encoding step happens through a repreat vector, which embeds the model into the embedding space of the output. Each node of the repeate vector, contains the same value output from the previous GRU layer. This output is then "decoded" by being passed through a larger GRU, which translated the encoded value into the same dimension space that we are translating to. The overall complexity of this model requires much learning and a more robust architecture, so the following accuracy is lower than the simple model.

This model achieved the following accuracy: `71.83%`

### Encoder Decoder - Applying all Techniques
This model improves on the previous encoder decoder model, by adding just 1 layer, and improving on the previous layers. For startes, all previous GRU layers have remained the same, but are now represented as bidirectional layers. Also, the initial layer has now become an embedding space, same as the second model, to represent the sentences in a more semantically "dense" space. Now, the potential of the encoder-decoder model can be seen.

This model achieved the following accuracy: `96.17%`