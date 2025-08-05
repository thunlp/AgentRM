# AgentRM: Enhancing Agent Generalization with Reward Modeling

## Introduction

:point_right: **[Read our paper!](https://arxiv.org/pdf/2502.18407)**

<!--
## Performance

<div align="center">
  <img src="figs/general.png" alt="" width="800px">
</div>

<div align="center">
  <img src="figs/specific.png" alt="" width="400px">
</div>

<div align="center">
  <img src="figs/policy_scaling.pdf" alt="" width="800px">
</div>
-->

## Step1 (optional): Derive a capable Agent via SFT

Option 1: Download model weights

1. Download the corresponding model weights from [our Hugging Face repository](https://huggingface.co/cheesewafer).

2. Save the downloaded weights in the local `models` directory.

Option 2: Train it on your own

1. We modified [the original SFT training script](https://github.com/huggingface/alignment-handbook/blob/main/scripts/run_sft.py) to support multi-turn conversations.

2. Dataset can be downloaded at [SFT Trajectory Dataset](https://huggingface.co/datasets/agent-eto/eto-sft-trajectory).


## Step2 (optional): Construct MCTS Exploration Trees

Option 1: Download trees

1. Download trees from [Google Disk](https://drive.google.com/drive/folders/1egTUhwdHCKNazuzkKLhthBgpP8twcBmx?usp=sharing).

2. Save in the local `roots` directory. 

Option 2: Construct it on your own

1. We modified [ReST-MCTS](https://github.com/THUDM/ReST-MCTS) to support agent scenarios. Our codes are being organized.
2. Dataset can be downloaded at [SFT Trajectory Dataset](https://huggingface.co/datasets/agent-eto/eto-sft-trajectory).

## Step3 (optional): Extract Reward Model Training Dataset

Option 1: Download dataset

1. Download dataset from [Google Disk](https://drive.google.com/drive/folders/1egTUhwdHCKNazuzkKLhthBgpP8twcBmx?usp=sharing).

Option 2: Extract dataset

1. Extract dataset using `python extract_regression_samples.py` and `python combine_regression_samples.py`.

## Step4: Derive the Reward Model

Option1: Download model weights
1. Download the corresponding model weights from [our Hugging Face repository](https://huggingface.co/cheesewafer).

2. Save the downloaded weights in the local `models` directory.

Option2: Train it on your own

`cd alignment-handbook; bash train_reward_regression_all.sh`

## Step5: Evaluation

1. reproduce results in Table1 (AgentRM + LLaMA-3-8B)
   ```
   # Greedy search
   python inference_script_policy.py --policy_path /path/to/model --prm_path /path/to/prm --port 8000 --part_num 1 --inference_method greedy --tasks webshop alfworld_ab sciworld_ab babyai jericho pddl tool_query tool_operation maze
   # Best-of-5
   python inference_script_policy.py --policy_path /path/to/model --prm_path /path/to/prm --port 8000 --part_num 1 --inference_method bestofn --tasks webshop alfworld_ab sciworld_ab babyai jericho pddl tool_query tool_operation maze
   ```
2. reproduce results in Table2 (AgentRM + SFT LLaMA-3-8B)
   ```
   # Greedy search
   python inference_script_policy.py --policy_path /path/to/model --prm_path /path/to/prm --port 8000 --part_num 1 --inference_method greedy --tasks webshop alfworld sciworld
   # Best-of-5
   python inference_script_policy.py --policy_path /path/to/model --prm_path /path/to/prm --port 8000 --part_num 1 --inference_method bestofn --tasks webshop alfworld sciworld
   ```

## Acknowledgment

https://github.com/huggingface/alignment-handbook

https://huggingface.co/datasets/agent-eto/eto-sft-trajectory

https://github.com/THUDM/ReST-MCTS

## Citation

```
@misc{xia2025agentrmenhancingagentgeneralization,
      title={AgentRM: Enhancing Agent Generalization with Reward Modeling}, 
      author={Yu Xia and Jingru Fan and Weize Chen and Siyu Yan and Xin Cong and Zhong Zhang and Yaxi Lu and Yankai Lin and Zhiyuan Liu and Maosong Sun},
      year={2025},
      eprint={2502.18407},
      archivePrefix={arXiv},
      primaryClass={cs.CL},
      url={https://arxiv.org/abs/2502.18407}, 
}
```
