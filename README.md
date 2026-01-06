# HighlightSense

**HighlightSense** is a dual audio channel-based **CRNN + Attention model** designed to identify and extract top clips from VODs based on audio excitement.

## Description
This tool automatically scans through VODs (Video on Demand) to find high-intensity moments. It utilizes **Demucs** to separate the audio track into two distinct channels:
1. **Game Audio**
2. **Streamer Audio**

Both channels are passed to the model to accurately detect highlights. This repository includes a `Final_Inference_Script` that serves as a simple, user-friendly tool to deploy the model and generate clips.

## Tech Stack
* **Language:** Python
* **Environment:** Jupyter Notebooks (Google Colab)
* **Libraries:** Main- Pytorch, Demucs, Librosa

## How It Works
### 1. The Model
The model operates on a **CRNN (Convolutional Recurrent Neural Network) + Attention** architecture. It was trained on a custom dataset comprising:
* **Positive Samples:** Most viewed clips per game.
* **Negative Samples:** Unclipped, standard parts of popular VODs.

### 2. Preprocessing
During both training and inference, the raw audio undergoes significant preprocessing:
1.  **Separation:** Audio is split into game and streamer tracks using Demucs.
2.  **Conversion:** Tracks are converted into log-mel spectrograms.
3.  **Stacking:** The spectrograms are stacked to form the model input.

### 3. Inference
The user-friendly inference script scans a target VOD using a **sliding window approach**. The model analyzes each window, and if a highlight is detected, the script automatically cuts the clip and saves it as an `.mp4` file in the user's specified directory.

## xB1; Folder Structure
Here is an overview of the files included in this repository:

* **`best_model.pt`**
    * A dictionary containing the trained model weights and epoch information.
* **`HighlightSenseModelFinal.ipynb`**
    * The complete code used to train the model. Detailed instructions on how to run the training process are provided inside the notebook.
* **`Final_Inference_Script`**
    * **The main tool for users.** A simple-to-use Colab notebook for generating clips.
    * *Note:* Detailed instructions are provided in the notebook. Since this script requires audio separation, **you must use a GPU runtime (CUDA version 12.5)** in Google Colab.
* **`output_inference`**
    * A notebook containing results from a dry run, demonstrating clip extraction from a specific Twitch VOD.
* **`Downloading and Preprocessing scripts/`**
    * Scripts used to download VODs and perform the required audio preprocessing.
* **`Config/`**
    * Contains all necessary configuration files used by the model and scripts, including values of hyperparameters.

## 📊 Dataset
The model was trained on a large, custom-curated dataset:
* **Training Set:** ~30,000 positive clips, ~36,000 negative clips.
* **Validation Set:** ~750 samples (balanced split of positive and negative).

**Validation Dataset Link:**
[Google Drive Link](https://drive.google.com/drive/folders/14yjMilo9GAZ61PzhLVKZO9kN_3hYD_tS?usp=sharing)