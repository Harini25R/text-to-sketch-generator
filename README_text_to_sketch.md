# Text-to-Sketch Generator

Fine-tuning pipeline that adapts Stable Diffusion v1.5 to generate sketch-style images from text prompts, using the SketchyScene dataset.

Developed as an MSc Data Science project at NMKRV College for Women.

## Overview

Text-to-image models usually produce detailed, photorealistic pictures. Sketches are minimal and focus on structure, which makes them useful for design, storyboarding and education. This project builds the data pipeline and training setup needed to redirect a diffusion model toward line-based sketch output.

## Dataset

**SketchyScene** (scene sketches with object-level semantic annotations).

- Parsed 5,600+ scene layouts (JSON) and category segmentation maps, and explored the most common object categories (grass, tree, cloud, flower, house).
- Automatically generated a text prompt for each scene from its object categories and positions, creating a unified dataset of **5,604** scene samples.
- Built **16,846** image-prompt pairs for fine-tuning.

## Approach

- **Base model:** Stable Diffusion v1.5, loaded with Hugging Face Diffusers and PyTorch.
- **Preprocessing:** images resized and center-cropped to 512x512 and normalized.
- **Fine-tuning:** the UNet is trained with the standard noise-prediction (MSE) objective using AdamW (learning rate 5e-6), batch size 2, for 3 epochs.
- **Inference:** a prompt-to-image loop that loads the saved model and generates a sketch for any text prompt.

## Project status

The dataset pipeline and fine-tuning script are complete. The first full training run did not converge (the loss became NaN), so the fine-tuned weights are not yet usable. Next steps are to keep the model weights in float32 or use proper mixed precision, add gradient clipping, and try LoRA fine-tuning. This README will be updated with sample outputs once a stable run is finished.

## Tech stack

Python, PyTorch, Hugging Face Diffusers, Transformers and Datasets, Stable Diffusion v1.5, Pandas, NumPy, SciPy, Matplotlib, Pillow, Kaggle Notebooks

## How to run

1. Open the notebook in Kaggle or Google Colab with a GPU runtime.
2. Add the SketchyScene data and update the paths at the top of the notebook.
3. Log in to Hugging Face with your own token when prompted. Never paste tokens into notebook cells.
4. Run the cells in order to build the dataset, fine-tune the model, and generate sketches.

## Author

Harini R | MSc Data Science | [GitHub](https://github.com/Harini25R)
