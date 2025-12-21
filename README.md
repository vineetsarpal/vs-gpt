# VSGPT: AI-Powered Guitar Pro Tab Generation

## Project Summary

This project demonstrates the creation of a Guitar Pro tab generation model using PyTorch and the DadaGP library. The core idea is to train a sequence-to-sequence model on existing Guitar Pro files, allowing it to learn musical patterns and generate new, stylistically similar tabs.

The project provides a complete pipeline from raw Guitar Pro files to a trained generative model, capable of composing new musical pieces in a learned style.

## Key Features

*   **Guitar Pro (.gp) File Encoding:** Converts `.gp` files into token sequences using `dadagp.py`.
*   **Custom Vocabulary Generation:** Builds a unique vocabulary from musical tokens.
*   **LSTM-based Generative Model:** Utilizes PyTorch to define and train a sequence-to-sequence model.
*   **Configurable Training:** Supports custom epochs, learning rates, and model saving.
*   **AI Tab Generation:** Generates new musical sequences from a given prompt using temperature and top-k sampling.
*   **Guitar Pro Decoding:** Converts generated tokens back into playable `.gp5` files.
*   **Google Drive Integration:** Seamlessly saves models and generated tabs to Google Drive for persistence.

## Getting Started

To get this project up and running in Google Colab, follow these steps.

### Prerequisites

*   A Google Account with Google Drive access.
*   Google Colab environment.

### Setup Instructions

1.  **Open the Notebook in Colab:** Upload or open the `.ipynb` file in Google Colab.

2.  **Mount Google Drive & Setup Directories:**
    Run the first code cell to mount your Google Drive and set up the project folder structure. You'll be prompted to authenticate with your Google account.
    ```python
    # Example of cell content:
    from google.colab import drive
    from google.colab import userdata
    import os

    drive.mount('/content/drive')

    BASE_DIR = userdata.get('BASE_DIR') # set in secrets
    # ... rest of the directory setup
    ```
    *Make sure to define `BASE_DIR` in Colab secrets or directly in the notebook.* For example, `/content/drive/MyDrive/Projects/vs-gpt`.

3.  **Place Your Guitar Pro Files:**
    Place your `.gp`, `.gp5`, etc., files into the `BASE_DIR/tabs` folder on your Google Drive. These will be used for training the model.

4.  **Install Dependencies & Setup DadaGP Encoder:**
    This will download the necessary `dadagp.py` and `token_splitter.py` scripts and install the `PyGuitarPro` library.

## Usage

### A. Training a New Model (Full Pipeline)

If you want to train a new model from your Guitar Pro files:

1. Discover Guitar Pro Files
3. Build Vocabulary
2. Encode and Tokenize
4. Create Dataset
5. Define Model Architecture
6. Train Model. The best performing model will be saved to `MODELS_DIR`
7. Generate and Decode (Optional after training). You can test immediate generation
8. Save Final Model

### B. Loading a Pre-trained Model for Generation (No Retraining)

If you have already trained your model and saved the checkpoint (e.g., `vs_gpt_complete.pt`), you can skip the training steps and directly use the model for generation:

1. Ensure the drive is mounted, the necessary dependencies including the DadaGP encoder are setup
2. Ensure the model architecture and the complete generate and decode pipeline is defined
4. Load the Trained Model and Vocabulary. This will load your `vs_gpt_complete.pt` model, set up the vocabulary, and prepare the model for inference
5.  Generate New Tabs with your desired prompt:
    ```python
    # Example:
    new_prompt = ['artist:vineet sarpal', 'downtune:-2', 'tempo:120', 'start']
    generate_and_decode(loaded_model, new_prompt, "my_new_ai_song", max_new=1024)
    ```
    Your generated `.gp5` files will be saved in `OUT_DIR`.

## Contribution

Feel free to fork the repository, open issues, or submit pull requests!

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.


