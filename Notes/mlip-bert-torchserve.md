# Serving BERT Models in Production with TorchServe | PyData Global 2021

Presenters: Adway Dhillon and Nidhin Pattaiyii (Walmart MLEs - Search)

## Machine Learning at Walmart Search
- SpellCheck
- TypeAhead
- Related Search / Guided Navigation
- Query / Item Understanding
- Personalized Ranking

## Models in Prod
- Originally Tensorflow
- Serves BERT
- Pytorch/ONNX support
- SLA < 40ms

## Setup
- Repo: [Github Repo for BERT Torchserve | PyData](https://bit.ly/pytorch-workshop-2021)

- Dataset: [Amazon Berkeley Objects (ABO) Dataset](https://amazon-berkeley-objects.s3.amazonaws.com/index.html)

## Training
- HuggingFace
- Transformers (distil-bert-uncased)

## Post Training Optimization
Considering that the size of the models from the transformer trainings are considerably large, the models need to be optimized before using them in production.
- Quantization: 