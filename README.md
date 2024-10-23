# M-STAR

<p align="center">
  <img src="./assets/mstar-logo.png" width="500">
</p>

<p align="center">
  :star: <a href="https://mstar-lmm.github.io/">Project Page</a>&nbsp;&nbsp;&nbsp;
</p>

<p align="center">
  :hugs: <a href="...">HF Repo</a>&nbsp;&nbsp;&nbsp;
  :page_with_curl: <a href="...">Paper</a>
</p>

Welcome to M-STAR (**M**ultimodal **S**elf-Evolving **T**r**A**ining for **R**easoning) Project! 

This is the **preview version** of M-STAR. We will continue to update, please stay tuned!

## What is M-STAR :star:?
M-STAR is a framework to improve the **Multimodal Reasoning** ability of Large Multimodal Models (LMMs) via **Self-Evolving Training**.

Unlike traditional **Self-Evolving Training**, M-STAR supports **Large Multimodal Models**, **Training with Multimodal Process Reward Models (MPRM)**, and **Adaptive Explorations during Training**.

M-STAR includes:

- **M-STAR Framework**: A framework for Self-Evolving Training of LMMs including **Generation**, **Training**, and **Rewarding**. With M-STAR, we can:
  - Efficiently generate diverse responses for a given query using [lmdeploy](https://github.com/InternLM/lmdeploy)
  - Generate data to train Multimodal Process Reward Models (MPRM)
  - Train MPRM to assess multimodal reasoning
  - Perform **Self-Evolving Training** of LMMs to enhance multimodal reasoning ability
  - Monitor training dynamics and adaptively adjust exploration (e.g., temperature) during training

- **M-STAR Resources**:

    | **Component**                |**Description**                                                                                                     |
    |------------------------------|---------------------------------------------------------------------------------------------------------------------|
    | **M-STAR Model**              | A strong LMM for multimodal reasoning, scoring **59.2** on MathVista, based on [MiniCPM-V-2.5](https://github.com/OpenBMB/MiniCPM-V) with 8B parameters. |
    | **M-STAR PRM**                | A Multimodal Process Reward Model (MPRM) that evaluates the quality of multimodal reasoning data at the step level.  |
    | **M-STAR CoT Dataset**        | A collection of 100K generated multimodal reasoning data with CoT, where the queries are sourced from [MathV360K](https://huggingface.co/datasets/Zhiqiang007/MathV360K).                      |
    | **M-STAR MPRM Training Dataset** | A set of 50K multimodal reasoning data designed for training MPRM.                                             |

## News

- :fire: [10/2024] We are excited to release the preview version of M-STAR! In this release, all **M-STAR Resources** are available, and the components for **Generation** and **Training of MPRM** are ready for use. To enhance the user experience, we are currently refining the code for the entire **M-STAR Framework**, which will be available soon!

## Performance

### Main Results

<div align="center">

|                            | MathV360K | MathVista |
|----------------------------|-----------|-----------|
| **Baselines**               |           |           |
| MiniCPM-V-2.5               | 13.6      | 52.4      |
| &nbsp;&nbsp;&nbsp;+ warmup  | 38.8      | 52.6      |
| SFT                        | 44.3      | 54.8      |
| ReST<sup>EM</sup>           | 42.3      | 55.1      |
| Iterative RFT               | 42.3      | 55.7      |
| **Static components only**  |           |           |
| Cont. optim.                | 43.1      | 57.2      |
| &nbsp;&nbsp;&nbsp;+ PRM Re-Rank | 45.3  | 59.2      |
| **Automatically tuning the temperature T** |   |   |
| M-STAR (Pass@K)             | 42.8      | 58.0      |
| M-STAR (Reward-Pass@2)      | 45.9 (+7.1) | 59.5 (+6.9) |
| **Reference** |   |   |
| GPT-4o |   |   63.8
| Gemini 1.5 Flash |   |   58.4
| GPT-4T 2024-04-09 |   |  58.1
| Pixtral 12B |   |   58.0
| InternLM-XComposer2-VL-7B |   |   57.6
| Math-LLaVA-13B |   |  46.6
| LLaVA-NeXT-34B |   |  46.5

</div>

### Effectiveness of Adaptively Adjusting Exploration

<p align="center">
  <img src="./assets/dynamic.png" width="500">
</p>

Two metrics are used to evaluate the effectiveness of adaptively adjusting exploration:

- **Pass@K**: The percentage of samples for which the model produces at least one correct response when sampling $K$ candidates. This metric measures the model's exploration ability.
- **Reward-Pass@2**: The percentage of samples for which there exist correct responses among the top 2 responses ranked by the reward model. This metric directly reflects the exploitation efficacy of the reward model for the current policy. We choose Pass@2 since our training strategy involves selecting the top 2 responses using the reward model.

"Static" refers to models trained without adaptive exploration, while "Dynamic" indicates those trained with this mechanism. All models shown were trained using the M-STAR framework with optimized components as explored in our paper.

## :rocket: M-STAR Resources
<div align="center">

| Resource                                       | Link     | License  |
|------------------------------------------------|-----------|------------|
| **M-STAR Datasets**                          
| **M-STAR CoT Dataset**                        | ...       | [MIT License](https://opensource.org/license/mit)
| **M-STAR MPRM Training Dataset**              | ...       | [MIT License](https://opensource.org/license/mit)
| **M-STAR Models**                                   |           |             |
| M-STAR-8B-v1.0                |  ...         | [MiniCPM Model License](https://github.com/OpenBMB/MiniCPM/blob/main/MiniCPM%20Model%20License.md)             |
| M-STAR-PRM-8B-v1.0               |  ...         | [MiniCPM Model License](https://github.com/OpenBMB/MiniCPM/blob/main/MiniCPM%20Model%20License.md)             |
</div>

## :running_man: How to start?

### Installation
```bash
  git clone https://github.com/hkust-nlp/mstar.git
  cd mstar
  pip install -e .
```

### Generate Responses
...

### Generate MPRM Training Data

...

### MPRM Training

...

### Self-Evolving Training
- [ ] ...

## :muscle: What's more?

This is the preview version of M-STAR project. We will continue to update including

- [ ] Self-Evolving Training Pipeline
- [ ] ...

## Citation
If you find the content of this project helpful, please cite our paper as follows:

```
@misc{liu2024diving,
      title={Diving into Self-Evolve Training for Multimodal Reasoning}, 
      author={Wei Liu and Junlong Li and Xiwen Zhang and Fan Zhou and Yu Cheng and Junxian He},
      year={2024},
      eprint={...},
      archivePrefix={arXiv},
      primaryClass={cs.CL}
}
```