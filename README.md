# Belarusian Speech-to-Text

Speech-to-Text (STT) or Automated Speech Recognition (ASR) is the task of building textual transcription
for the input audio file. 

## Description
This repository contains code to train and evaluate STT model for Belarusian language.

[Common Voice 8](https://commonvoice.mozilla.org/en/datasets) dataset
was used to train & evaluate the model.

Acoustic model (AM) was created by fine-tuning [facebook/wav2vec2-base](https://huggingface.co/facebook/wav2vec2-base) model.

Additionaly, 5-gram Language model (LM) was built using 
[KenLM](https://kheafield.com/code/kenlm/estimation/) library.

## Model demo & checkpoint
You can play with model in a **Demo application** here:
[huggingface.co/spaces/ales/wav2vec2-cv-be-lm](https://huggingface.co/spaces/ales/wav2vec2-cv-be-lm).
It uses **full pipeline of Acoustic model + Language model**.

The best model checkpoint (weights) is located here:
[huggingface.co/ales/wav2vec2-cv-be](https://huggingface.co/ales/wav2vec2-cv-be). This page also contains a demo widget,
**however only Acoustic model is utilized there** because of 
HuggingFace Hosted inference API limitations. 
Thus performance of model in this widget will be worse than
[Demo application](https://huggingface.co/spaces/ales/wav2vec2-cv-be-lm) mentioned above (because the latter also uses Language model).

## Metrics

Current metrics for Common Voice 8:
|model|WER on Dev set|WER on Test set|Rate of fully recognized sentences on Test set|
|-|-|-|-|
|Acoustic model only|0.1761|0.187|36.688%|
|Acoustic model + 5-gram Language model|0.115|0.124|52.269%|

## Training

Current best model was trained for 5 epochs. 

`Train, Dev, Test` sets of Common Voice 8 dataset were used as they are
(however one may enlarge them using `Validated` set to achieve better model performance) - see `eda/cv8be_eda.ipynb` notebook.

## Language model

[KenLM](https://kheafield.com/code/kenlm/estimation/) library was used
to build 5-gram Language model (LM).

Language model is used to decode predictions of wav2vec2 model 
(Acoustic model) and improve performance.

Textual corpus for LM consists of sentences from `Train` 
and `Validated - Dev - Test` sets of Common Voice 8 dataset 
(~314'000 unique sentences in total).

TODO:
* will try to gather much larger textual corpus 
  to build a better Language Model
