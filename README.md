# AI of GOD 3.0 - Spanish Text Transcription

## Overview
This project was part of the **AI of GOD 3.0** hackathon, where we worked on transcribing text from images of old Spanish scriptures. The dataset and competition details can be found [here](https://www.kaggle.com/competitions/ai-of-god-3/overview).

## Our Approach
### **1. Initial Attempts with TrOCR-Small**
- We started with **TrOCR-small-spanish** on Kaggle’s P100 GPU.
- The results weren’t great, with a **WER (Word Error Rate) of 0.78**.

### **2. Improving Image Clarity with Binarization**
- We applied **image binarization** to enhance text visibility. This technique converts grayscale images into black-and-white by setting a pixel threshold—pixels above it turn white, and below it turn black.
- Through experimentation, we selected an optimal threshold that improved text clarity, making it easier for the model to recognize characters.
- This helped but wasn’t enough, bringing WER down to **0.6**.

### **3. Switching to TrOCR-Large**
- Upgrading to **TrOCR-Large** made a big difference.
- We had to use a **small batch size (4)** due to limited GPU memory.
- After **2 epochs, WER dropped to 0.28**, and after **14 epochs, it reached 0.234**.

### **4. Postprocessing for Common Errors**
- Some characters, like **a-tilde (ã), were misinterpreted**.
- We manually corrected such mistakes, lowering WER to **0.202**.

### **5. Experimenting with BART for Refinement**
- We explored using a **BART model** as a refinement layer, feeding TrOCR’s output into it and training on ground truth labels.
- The goal was to correct misrecognized words and improve fluency.
- Due to GPU limitations, we couldn’t train it effectively, and it didn’t outperform TrOCR-Large.

## Results
- **Final WER: 0.202** (2nd place in the leaderboard; Team Name - AbhinavJ).
- **Significant improvement:**
  - **TrOCR-Small: 0.78 WER → TrOCR-Large: 0.234 WER → Postprocessed: 0.202 WER**.

## Challenges & Learnings
- **GPU Limits:** Small batch sizes slowed training.
- **Character Recognition Issues:** Some rare characters weren’t well-represented in the training data.

## Conclusion
Despite challenges, our systematic approach helped us achieve a **strong result**. With better hardware, more training time, and refined methods, this system could improve further. We plan to experiment more with **postprocessing and hybrid models** to enhance accuracy.
