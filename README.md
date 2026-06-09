# Distorted Visual Sequence Pattern Recognition

## Project Overview

This project focuses on recognizing text sequences from distorted grayscale images containing noise, blur, overlapping characters, irregular spacing, and other visual artifacts. Traditional OCR systems often struggle in such conditions because character boundaries become unclear and visual patterns vary significantly across samples.

To address this challenge, a CRNN (Convolutional Recurrent Neural Network) architecture was implemented. The model combines convolutional layers for extracting visual features with recurrent layers for sequence modelling, allowing it to predict complete text sequences directly from images.

---

## Dataset Exploration

Before training the model, the dataset was analyzed to understand:

* Image dimensions and formats
* Label distributions
* Sequence lengths
* Common distortion patterns
* Training and test set structure

Several visualizations were generated to inspect the quality and diversity of the data. This step helped identify potential challenges and guided preprocessing decisions.

---

## Approach

The solution follows a CRNN + CTC pipeline.

### Feature Extraction

A convolutional backbone is used to extract meaningful visual features from the distorted input images. Instead of treating each character independently, the model learns spatial representations from the entire image.

### Sequence Modelling

The extracted feature maps are converted into a sequence representation and passed through Bidirectional LSTM layers. This allows the model to capture contextual information from both left-to-right and right-to-left directions.

### Sequence Prediction

Since character-level alignments are not available, the model is trained using Connectionist Temporal Classification (CTC) Loss. This enables end-to-end sequence learning without explicitly segmenting characters beforehand.

---

## Training Pipeline

The overall workflow consists of:

1. Dataset exploration and analysis
2. Character vocabulary construction
3. Dataset and dataloader creation
4. Image preprocessing
5. CRNN model implementation
6. Training using CTC Loss
7. Validation using Character Error Rate (CER)
8. Test set prediction generation

Validation loss was monitored throughout training, and the best-performing checkpoint was automatically saved for inference.

---

## Results

The model converged successfully and achieved strong recognition performance on the validation set.

| Metric               | Value      |
| -------------------- | ---------- |
| Best Validation Loss | **0.0264** |
| Best Epoch           | **19**     |
| Validation CER       | **0.0062** |
| Percentage CER       | **0.62%**  |

A CER of 0.62% indicates that fewer than one character per hundred characters is predicted incorrectly on average, demonstrating that the model is able to recover text accurately even in the presence of substantial visual distortions.

---

## Sample Workflow

Input Image → CNN Feature Extraction → BiLSTM Sequence Modelling → CTC Decoding → Predicted Text Sequence

Example:

```text
Distorted Image
        ↓
CRNN Model
        ↓
Prediction: AXU323
```

---

## Key Takeaways

* Successfully implemented an end-to-end OCR pipeline for distorted text recognition.
* Used CRNN architecture for joint visual feature extraction and sequence modelling.
* Trained using CTC Loss without requiring character-level alignment.
* Achieved a validation CER of **0.62%**.
* Generated predictions for the complete test dataset using the best saved checkpoint.

The results demonstrate that CRNN-based sequence recognition is highly effective for OCR tasks involving noisy and visually distorted text images.
