<h1 align="center">NeuRel-Attack </h1>
<h3 align="center"> Neuron Relearning for Safety Disalignment in Large
Language Models </h3>

<!-- <p align="center">
  📃 <a href="https://arxiv.org/abs/2407.01920" target="_blank">arXiv</a> • 🤗 <a href="https://huggingface.co/datasets/zjunlp/KnowUnDo" target="_blank">Dataset</a> <br>
</p>

<div align="center">

[![Awesome](https://awesome.re/badge.svg)](https://github.com/zjunlp/KnowUnDo) 
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)
![](https://img.shields.io/github/last-commit/zjunlp/KnowUnDo?color=green) 
![](https://img.shields.io/badge/PRs-Welcome-red)

---

<p align="center">
  <a href="#-overview">🔔 Overview</a> •
  <a href="#-load-datasets">📊 Load Datasets</a> •
  <a href="#-how-to-run">🚀 How to Run</a> •
  <a href="#-citation">📖 Citation</a> •
</p>

</div> -->

## 🔔 Overview
Safety alignment in large language models (LLMs) is achieved through fine-tuning mechanisms that regulate neuron activations to suppress harmful content. We propose **NeuRel- Attack** to induce disalignment by identifying and modifying the neurons responsible for safety constraints, and finally jailbreak the LLMs


The following figure illustrates the overall pipeline of NeuRel-Attack:
<div align=center><img src="overall_pipline.png" width="100%" height="100%" /></div>

<!-- We provide the **KnowUnDo**, a benchmark containing copyrighted content and user privacy domains to evaluate if the unlearning process inadvertently erases essential knowledge. Access our **KnowUnDo** directly on [Hugging Face](https://huggingface.co/datasets/zjunlp/KnowUnDo).

To address this, we propose a simple yet effective method, **MemFlex**, which utilizes gradient information to precisely target and unlearn sensitive parameters. -->


<!-- ## 📊 Load Datasets
You can easily load the datasets following below.

```python
from datasets import load_dataset

dataset = load_dataset("zjunlp/KnowUnDo", name='copyright', split='unlearn')
```
* Available configuration names and corresponding splits:
  - `copyright`: `unlearn`, `retention`;
  - `privacy`: `unlearn`, `retention`; -->

<!-- # git clone https://github.com/zjunlp/KnowUnDo.git -->
<!-- git clone https://huggingface.co/meta-llama/Llama-2-7b-chat-hf
# git clone https://huggingface.co/Qwen/Qwen1.5-7B-Chat -->

## 🚀How to run
### Environment Setup
```bash
git clone https://github.com/Youzhouyi/Neural-Attack.git
cd Neural-Attack
conda create -n NA python==3.10

conda activate NA
pip install -e .
pip install -r requirements.txt

cd relearn/apex
pip install -v --no-cache-dir ./
```
### Download Large Language Models (LLMs)
```bash
# directory: Neural-Attack
cd models
git lfs install
python prepare_models.py
```
+ Vicuna-7B-v1.5
+ Llama-2-7B-Chat-hf
+ Guanaco-7B-HF
+ Mistral-7B-Instruct-v0.2

### Pretrain LLMs (Optional)
```bash
git clone --depth 1 https://github.com/hiyouga/LLaMA-Factory.git
cd LLaMA-Factory
conda create -n llama python==3.10
conda activate llama
pip install -e ".[torch,metrics]"
llamafactory-cli webui
```
### Location neuron
```bash
# directory: localization
bash run_localization.sh
```
### Prepare tokenized datasets
```bash
# directory: relearn
cd utils
bash tokenize_datasets.sh
```
<!-- + `--val` for the `val` split of the dataset.
+ `--prompt` for concating `direct_prompt` before the `question` in the datasets. -->

### Relearning 
```bash
# directory: relearn
bash run_baselines_lora.sh
bash run_ours_lora.sh
```


### Evaluation
```bash
#cd evaluation
python asr_eval.py
```

## 📊  Experimental Results
We evaluate NeuRel-Attack on multiple open-source LLMs, including **Vicuna**, **LLaMA-2**, **Guanaco**, and **Mistral**, using the **AdvBench** and **MaliciousInstruct** datasets. Our method achieves competitive attack success rates, outperforming existing jailbreak techniques in various scenarios.


|Dataset| Vicuna | Guanaco | Mistral | Llama2 |
|-------|-----|-------|-------|-------|
| AdvBench | 98% | 96%| 90% | 100% |
| MaliciousInstruct | 100% | 94% | 92% | 100% |


## 📃License

This repository is released under the **MIT License**.

<!-- - Available methods with corresponding arguments: 
  - `--unlearn_method gradient_ascent `
  - `--unlearn_method random_label --completely_random True` (named Fine-tuning with Random Labels in the paper)
  - `--unlearn_method random_label  --top_k 1  --rm_groundtruth True` (named Unlearning with Adversarial Samples in the paper)
  - `--unlearn_method ascent_plus_descent`
  - `--unlearn_method ascent_plus_kl_divergence`
  - `--unlearn_method ascent_plus_descent --general True`
  - `--unlearn_method ascent_plus_kl_divergence --general True`
  - `--unlearn_method memflex` (the strong baseline proposed by us) 
### Eval Unlearned Model -->
<!-- ```bash
# directory: llm_unlearn
torchrun --nproc_per_node=1 --master_port=20001 run_eval_lora.py \
    --model_name_or_path /path/to/your/unlearned/model \
    --tokenizer_name ../models/Llama-2-7b-chat-hf \
    --per_device_eval_batch_size 1 \
    --do_eval \
    --output_dir ./output/copyright/Llama-2-7b-chat-hf-eval \
    --overwrite_output_dir \
    --overwrite_cache \
    --tf32 True \
    --domain copyright
``` -->
<!-- You can evaluate multiple unlearned models together by running our script **only once**. -->
 <!-- ```bash -->
<!-- # directory: llm_unlearn
# bash run_eval_baselines_lora.sh
# ```
# + `--direct_prompt=True` means concating `direct_prompt` before the `question` in the datasets.





<!-- We would like to express our sincere gratitude to the excellent work [Unlearning LLM](https://github.com/yaojin17/Unlearning_LLM), [TOFU](https://github.com/locuslab/tofu), [LLaMA](https://huggingface.co/meta-llama/Llama-2-7b-chat-hf), and [Qwen](https://github.com/QwenLM/Qwen2?tab=readme-ov-file). -->

<!-- ## Acknowledgement

## Citation -->
<!-- 
If you use or extend our work, please cite the paper as follows:

```bibtex
@article{tian2024forget,
  title={To forget or not? towards practical knowledge unlearning for large language models},
  author={Tian, Bozhong and Liang, Xiaozhuan and Cheng, Siyuan and Liu, Qingbin and Wang, Mengru and Sui, Dianbo and Chen, Xi and Chen, Huajun and Zhang, Ningyu},
  journal={arXiv preprint arXiv:2407.01920},
  year={2024}
}
``` -->
