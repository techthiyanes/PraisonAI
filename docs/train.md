# PraisonAI Train

<iframe width="560" height="315" src="https://www.youtube.com/embed/aLawE8kwCrI" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## To upload to Huggingface

```bash
export HF_TOKEN=xxxxxxxxxxxxxx
```

## To upload to ollama.com (Linux)

```bash
sudo cat /usr/share/ollama/.ollama/id_ed25519.pub
```

Save the output from above to ollama.com --> Ollama keys

## RUN PraisonAI Train

```bash
praisonai train \
    --model unsloth/Meta-Llama-3.1-8B-Instruct-bnb-4bit \
    --dataset yahma/alpaca-cleaned \
    --hf mervinpraison/llama3.1-instruct \
    --ollama mervinpraison/llama3.1-instruct
```

Note: PraisonAI Train currently tested on Linux with 1 GPU. With pytorch-cuda=12.1

## Config.yaml example

```yaml
ollama_save: "true"
huggingface_save: "true"
train: "true"

model_name: "unsloth/Meta-Llama-3.1-8B-Instruct-bnb-4bit"
hf_model_name: "mervinpraison/llama-3.1-instruct"
ollama_model: "mervinpraison/llama3.1-instruct"
model_parameters: "8b"

dataset:
  - name: "yahma/alpaca-cleaned"
    split_type: "train"
    processing_func: "format_prompts"
    rename:
      input: "input"
      output: "output"
      instruction: "instruction"
    filter_data: false
    filter_column_value: "id"
    filter_value: "alpaca"
    num_samples: 20000

dataset_text_field: "text"
dataset_num_proc: 2
packing: false

max_seq_length: 2048
load_in_4bit: true
lora_r: 16
lora_target_modules: 
  - "q_proj"
  - "k_proj"
  - "v_proj"
  - "o_proj"
  - "gate_proj"
  - "up_proj"
  - "down_proj"
lora_alpha: 16
lora_dropout: 0
lora_bias: "none"
use_gradient_checkpointing: "unsloth"
random_state: 3407
use_rslora: false
loftq_config: null

per_device_train_batch_size: 2
gradient_accumulation_steps: 2
warmup_steps: 5
num_train_epochs: 1
max_steps: 10
learning_rate: 2.0e-4
logging_steps: 1
optim: "adamw_8bit"
weight_decay: 0.01
lr_scheduler_type: "linear"
seed: 3407
output_dir: "outputs"

quantization_method: 
  - "q4_k_m"

```

```bash
praisonai train
```