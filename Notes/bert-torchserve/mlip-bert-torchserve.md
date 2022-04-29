# Serving BERT Models in Production with TorchServe | PyData Global 2021 Notes

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
- **Quantization**: Techniques for performing computations and storing tensors have at lower bit than floating point precision, reducing memory and compute time.
- INT8 computations is 2 to 4 times faster than FP32 with relatively low drop in accuracy.
- Types of Quantization available in PyTorch:
    - Dynamic Quantization
    - Static Quantization
    - Quantization Aware Training

- **Distillation**: Another technique employed in optimization where knowledge(weights and biases) from a big model(teacher) is transferred to a smaller model(student) with little to no significant loss in performance.

## Eager Execution vs Script Mode
![eager execution vs script mode tabular difference](./eager-vs-script.png "eager execution vs script mode tabular difference")

## Deploying Pytorch model using TorchServe
Benefits of Torchserve:
- Optimized for serving models
- Support for CUDA (GPU) environments
- Multi model serving
- Model version for A/B Testing
- Server side batching
- Support for pre and post processing

Packaging a model can be done with:
- Torch Model Archiver which packages model code and artifacts into one single file

Walmart uses a Custom Handler for model serving:
```python
from abc import ABC
import os
import torch
from ts.torch_handler.base_handler import BaseHandler

class CustomHandler(BaseHandler, ABC):
    def initialize(self, ctx):
        model_dir = ctx.system_properties.get("model_dir")
        serialized_file = ctx.manifest['model']['serializedFile']
        model_pt_path = os.path.join(model_dir, serialized_file)
        self.model = torch.jit.load(model_pt_path, map_location=self.device)
        #...
    
    def preprocess(self, requests):
        #...

    def inference(self, input_batch):
        #...

    def postprocess(self, inference_output):
        #...

    def handle(self, data, context):
        #...
        data_preprocess = self.preprocess(data)
        data_inference = self.inference(data_preprocess)
        data_postprocess = self.data_postprocess(data_inference)
        return data_postprocess
```

## Serving 
Run the follow command to serve models with torchserve
```bash
torchserve --ts-config config.properties --start --model-store model_store
```

The configuration properties in `config.properties` should look like:
```
loads_model = all
inference_address=https://0.0.0.0/8080
management_address=https://0.0.0.0/8081
metrics_address=https://0.0.0.0/8082
number_of_netty_threads=32
job_queue_size=1000
model_store=/home/model-server/model-store
batch_size=20
max_batch_delay=2
async_logging=true
models=\
```