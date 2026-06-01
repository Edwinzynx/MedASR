# Medical ASR with Whisper and BART

## Overview

This project explores domain adaptation for Automatic Speech Recognition (ASR) in the medical domain using OpenAI Whisper-small and a BART-based post-processing correction model.

The pipeline consists of:

1. Fine-tuning Whisper-small on a medical speech dataset.
2. Applying a BART-based text correction model to Whisper transcriptions.
3. Evaluating performance using Word Error Rate (WER).

## Dataset

* Dataset: `Hani89/medical_asr_recording_dataset`
* Training Samples: 2,000
* Test Samples: 400

## Models

* ASR Model: `openai/whisper-small`
* Text Correction Model: `facebook/bart-base`

## Results

| Model                           | WER    |
| ------------------------------- | ------ |
| Baseline Whisper-small          | 0.2988 |
| Fine-tuned Whisper-small        | 0.0976 |
| Fine-tuned Whisper-small + BART | 0.1008 |

### Key Findings

* Fine-tuning Whisper-small on medical speech reduced WER from **29.88%** to **9.76%**.
* This represents approximately **67% relative improvement** over the baseline model.
* The BART correction stage did not improve performance and slightly increased WER to **10.08%**.

## Ablation Study

| Configuration                     | WER    |
| --------------------------------- | ------ |
| Fine-tuned Whisper (without BART) | 0.0789 |
| Fine-tuned Whisper + BART         | 0.0826 |

### Observation

The ablation study indicates that the BART correction model did not contribute positively to transcription quality. Removing BART resulted in a lower WER, suggesting that the correction model introduced additional errors rather than improving the generated transcripts.

## Conclusion

The primary performance gains were achieved through domain-specific fine-tuning of Whisper-small. While the BART-based semantic correction module was investigated as a post-processing step, experimental results showed that it did not improve transcription accuracy on this dataset. Future work may explore larger language models, medical terminology constraints, or specialized correction architectures for post-ASR refinement.
