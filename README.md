# PAD Training Report

## Overview
This repository contains training logs and comparative analysis of three preference alignment methods: SimPO, DPO, and PAD. We document the training process, implementation details, and performance metrics for each approach.

## Implementations
- **DPO**: Based on the implementation from [TRL](https://github.com/huggingface/trl)
- **SimPO**: Based on the implementation from [princeton-nlp/SimPO](https://github.com/princeton-nlp/SimPO)
- **PAD**: Based on the implementation from [PAD repository](https://anonymous.4open.science/r/PAD-E8C6)

## Training Configuration

### Models
- **Student Model**: Gemma-2-2B-It
- **Teacher Model**: Gemma-2-9B-It

### Hardware
- **GPUs**: 2 × A800 (80G)

### Training Parameters
- **Training Type**: Full parameter fine-tuning
- **Memory Optimization**: ZeRO Stage 2
- **Epochs**: 1
- **Precision**: BFloat16
- **Dataset Size**:
  - Training samples: 55,321
  - Test samples: 1,130
- **Batch Size**: 128
- **Total Training Steps**: 432
- **Maximum Sequence Length**: 2048
- **Per Device Train Batch Size**: 2
- **Per Device Evaluation Batch Size**: 2
- **Gradient Accumulation Steps**: 32
- **Evaluation Frequency**: Every 100 training steps
- **Gradient Checkpointing**: Enabled

For additional parameters, please refer to the paper or the configuration files in the [PAD repository](https://anonymous.4open.science/r/PAD-E8C6/).

## Results

| Method | GPU Hours | Alpaca-Eval 2.0 LC (%) |
|--------|-----------|---------------------------------|
| DPO    | 8.1240    | 43.77                           |
| SimPO  | 7.2672    | 44.94                           |
| PAD    | 7.2884    | 45.73                           |

### Analysis
- **Training Efficiency**: PAD and SimPO require similar computational resources, while DPO demands notably more. This efficiency difference is primarily because DPO requires loading an additional reference model during training, whereas PAD and SimPO do not.
- **Performance**: PAD outperforms both SimPO and DPO in terms of win rate, which aligns with the findings reported in the submission paper.

## References
For more detailed information about the PAD method, please refer to the original paper and the implementation repository at [PAD repository](https://anonymous.4open.science/r/PAD-E8C6/)
