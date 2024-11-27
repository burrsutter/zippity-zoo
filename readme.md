Parasol Insurance Training

ilab model serve
ilab model chat
{ask a question it does not know}
{drop in a qna.yaml file}
ilab taxonomy diff
ilab data generate
ilab model train
ilab model serve
ilab model chat
{ask the same question, it now has a good answer}



```
mkdir ~/.local/share/instructlab/taxonomy/knowledge/insurance/
mkdir ~/.local/share/instructlab/taxonomy/knowledge/insurance/parasol/
```

```
vi ~/.local/share/instructlab/taxonomy/knowledge/insurance/parasol/qna.yaml
```

copy and paste
https://raw.githubusercontent.com/rh-rad-ai-roadshow/parasol-taxonomy/refs/heads/main/knowledge/economy/finance/insurance/parasol/qna.yaml

```
cat ~/.local/share/instructlab/taxonomy/knowledge/insurance/parasol/qna.yaml
```

```
ilab taxonomy diff
```

```
knowledge/insurance/parasol/qna.yaml
knowledge/deloreon/qna.yaml
Taxonomy in /home/instruct/.local/share/instructlab/taxonomy is valid :)
```

```
ilab model serve --model-path  /home/instruct/.cache/instructlab/models/instructlab/granite-7b-lab
```

```
ilab model chat
```

```
who are the founders of parasol insurance?
```

Hallunciation 
```
Parasol Insurance is a relatively new insurance company that was founded in 2015 by entrepreneurs Max Esmaili and     │
│ Jesse Kallman. Prior to starting Parasol, Esmaili and Kallman had established CarePlus, a home healthcare company, in │
│ 2003. They recognized a need for a more transparent and customer-focused approach to insurance, and Parasol was born  │
│ with the mission to make insurance simpler, smarter, and more human.
```

```
ilab data generate --model /home/instruct/.cache/instructlab/models/TheBloke/Mixtral-8x7B-Instruct-v0.1-GPTQ --gpus 4 --pipeline full
```

This takes several minutes on a 4 GPU AWS g6.12xlarge

Find the correct knowledge_train_msgs_ jsonl file

```
ilab model train --gpus 4 --pipeline accelerated --local  --model-path /home/instruct/.cache/instructlab/models/instructlab/granite-7b-lab --distributed-backend fsdp  --fsdp-cpu-offload-optimizer true  --effective-batch-size 32 --is-padding-free true --deepspeed-cpu-offload-optimizer true --deepspeed-cpu-offload-optimizer-ratio 1  --deepspeed-cpu-offload-optimizer-pin-memory true --data-path /home/instruct/.local/share/instructlab/datasets/knowledge_train_msgs_???
```

