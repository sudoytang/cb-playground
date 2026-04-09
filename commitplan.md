# DeepBait — Commit Plan

## Project Overview

DeepBait is an automated clickbait headline generator using deep learning models (LSTM and BART-based architectures). This document outlines the three-part division of labor among team members.

---

## Team Contributions

### 1. Irys Zhang — Data Pipeline & Tokenization
**Role:** Data engineering, preprocessing, and vocabulary management

#### Primary Responsibilities:
- **Data Pipeline Architecture**
  - Download and load datasets from Kaggle
  - Handle raw data ingestion and validation
  - Implement data splitting (train/validation/test)

- **Tokenization & Vocabulary**
  - Build and manage vocabulary (`vocab.json`)
  - Implement tokenization for input headlines
  - Handle special tokens (BOS, EOS, PAD, UNK)
  - Manage token-to-index and index-to-token mappings

- **Webis-17 Loader**
  - Implement custom data loader for Webis-17 dataset
  - Format data into consistent structure for model training
  - Handle dataset-specific preprocessing requirements

#### Files & Modules:
- [`src/data_processing.py`](src/data_processing.py) — Primary module
- [`scripts/build_vocab.py`](scripts/build_vocab.py) — Vocabulary generation script
- Data loading utilities and dataset classes
- Custom dataloader implementations

#### Commits to include:
- Initial data loading pipeline
- Vocabulary building and management
- Webis-17 dataset loader implementation
- Data validation and error handling

---

### 2. Jiangchuan Yu — Model Architecture & Training Loop
**Role:** Core model development and training infrastructure

#### Primary Responsibilities:
- **Seq2Seq Architecture**
  - Design and implement Seq2Seq encoder-decoder models
  - Implement LSTM/GRU-based architecture
  - Handle attention mechanisms if applicable
  - Encoder and decoder layer configuration

- **Training Loop**
  - Implement training loop with forward/backward passes
  - Loss computation and optimization
  - Checkpointing and model saving
  - Learning rate scheduling and optimization strategies
  - Training metrics logging and history tracking

- **Model Management**
  - Model initialization and configuration
  - Parameter management and serialization
  - Device management (CPU/GPU)

#### Files & Modules:
- [`src/model.py`](src/model.py) — Model architecture
- [`src/train.py`](src/train.py) — Training loop and trainer
- [`scripts/run_direct.py`](scripts/run_direct.py) — Direct training script
- [`scripts/run_pretrain_finetune.py`](scripts/run_pretrain_finetune.py) — Pretraining + finetuning pipeline
- Checkpoint management in `checkpoints/`

#### Commits to include:
- LSTM/Seq2Seq model architecture
- Complete training loop implementation
- Loss functions and optimization
- Checkpoint and state management
- Training scripts for different experiments

---

### 3. Yushun Tang — Generation, Fine-tuning & Evaluation
**Role:** Model inference, BART integration, and performance evaluation

#### Primary Responsibilities:
- **Generation Module**
  - Implement headline generation inference
  - Beam search and sampling strategies
  - Temperature-based decoding
  - Batch generation utilities

- **BART Fine-tuning**
  - Download and integrate BART models
  - Implement fine-tuning on clickbait datasets
  - BART-specific training configurations
  - Tokenization for BART models

- **Evaluation Framework**
  - Implement perplexity calculation
  - Qualitative evaluation metrics
  - Output validation and sanity checks
  - Results visualization and reporting

#### Files & Modules:
- [`src/generate.py`](src/generate.py) — Generation pipeline
- [`src/evaluate.py`](src/evaluate.py) — Evaluation metrics
- [`scripts/download_bart.py`](scripts/download_bart.py) — BART model downloader
- [`scripts/generate_bart.py`](scripts/generate_bart.py) — BART generation script
- [`scripts/run_bart_finetune.py`](scripts/run_bart_finetune.py) — BART fine-tuning script
- [`notebooks/demo.ipynb`](notebooks/demo.ipynb) — Demo and visualization

#### Commits to include:
- Generation inference implementation
- Temperature sampling and decoding strategies
- BART model downloading and integration
- BART fine-tuning pipeline
- Evaluation metrics implementation
- Demo notebook and visualization

---

## Integration Points & Dependencies

```
Irys (Data)
    ↓
Jiangchuan (Architecture & Training)
    ↓
Yushun (Generation & Evaluation)
```

1. **Data → Training:** Irys's tokenized data pipeline feeds into Jiangchuan's training loop
2. **Training → Evaluation:** Jiangchuan's trained models are evaluated by Yushun's evaluation module
3. **Generation:** Yushun uses models trained by Jiangchuan with data prepared by Irys

---

## Commit Workflow

### Phase 1: Foundation (Irys + Jiangchuan)
1. Irys: Data pipeline and vocabulary
2. Jiangchuan: Model architecture and basic training loop
3. Joint testing and validation

### Phase 2: Training (Jiangchuan + Yushun)
1. Jiangchuan: Finalize and optimize training loop
2. Yushun: Implement evaluation metrics
3. Run initial training experiments

### Phase 3: Generation & Fine-tuning (Yushun + all)
1. Yushun: BART integration and fine-tuning
2. Yushun: Generation and evaluation
3. Demo and final validation

---

## Testing & Validation

- Unit tests for data processing (Irys)
- Model forward pass tests (Jiangchuan)
- Generation sanity checks (Yushun)
- End-to-end integration tests (all)

---

## Branch Strategy

- `main`: Production-ready code
- `dev`: Integration branch for ongoing development
- `irys/data`: Data pipeline feature branch
- `jiangchuan/model`: Model and training feature branch
- `yushun/inference`: Generation and evaluation feature branch

---

## Key Milestones

✓ Data loading and vocabulary (Irys)  
✓ Model training on direct data (Jiangchuan)  
✓ Generation and evaluation (Yushun)  
✓ BART fine-tuning experiments (Yushun)  
✓ Final demo and documentation (All)
