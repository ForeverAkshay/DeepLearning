# 🐦 Bird Species Classification — CUB-200-2011

Fine-grained classification of 200 bird species using deep learning. Two models are built and compared: a pretrained ResNet152 fine-tuned for high accuracy, and a fully custom CNN trained from scratch to demonstrate architectural understanding.

---

## 📦 Dataset — CUB-200-2011

| Detail | Info |
|---|---|
| **Name** | Caltech-UCSD Birds 200 (CUB-200-2011) |
| **Classes** | 200 bird species |
| **Total images** | ~11,788 |
| **Train / Test split** | Provided by the dataset (further split: 90% train, 10% validation) |
| **Extra annotations** | Bounding boxes per image, class labels, train/test flags |
| **Download** | [Caltech Vision Lab](http://www.vision.caltech.edu/datasets/cub_200_2011/) |

The dataset includes bounding box annotations for every image. These are used to **crop each image to the bird region** before training, which removes distracting background and significantly improves accuracy.

---

## 🤖 Models

### Model A — ResNet152 (Pretrained)

**Why ResNet152?**
ResNet152 is a deep residual network with 152 layers pretrained on ImageNet (1.2M images, 1000 classes). Transfer learning from ImageNet is highly effective for fine-grained visual classification because:
- Low-level features (edges, textures) learned on ImageNet transfer directly to bird imagery
- It avoids the need for millions of images to train from scratch
- ResNet's residual/skip connections solve the vanishing gradient problem in very deep networks, enabling stable training
- The 152-layer variant captures richer feature representations than shallower alternatives (e.g. ResNet50), which matters for distinguishing 200 visually similar species

The final fully-connected layer is replaced with a new layer of 200 outputs and fine-tuned on CUB-200-2011.

---

### Model B — Custom CNN (From Scratch)

A custom convolutional neural network designed and trained entirely from scratch — no pretrained weights. This model demonstrates understanding of CNN architecture design including convolutional blocks, pooling, batch normalisation, and dropout.

**Why build from scratch?**
To contrast against transfer learning and show the performance gap between a model with no prior knowledge vs one pretrained on millions of images.

---

## 🔁 Training Pipeline

```
Raw Image
    ↓
Bounding Box Crop (removes background noise)
    ↓
Resize to 256×256
    ↓
Random Augmentation (train only):
  - RandomResizedCrop(224)
  - RandomHorizontalFlip
  - RandomRotation(±15°)
  - ColorJitter (brightness, contrast, saturation)
    ↓
Normalise (ImageNet mean & std)
    ↓
Model → 200-class Softmax Output
```

---

## ⚙️ How to Run (Step by Step)

### 1. Prerequisites
- A **Google account** with Google Drive
- Google Colab (free) — no local install needed
- GPU runtime enabled in Colab

### 2. Download the Dataset
- Download `CUB_200_2011.tgz` from [here](http://www.vision.caltech.edu/datasets/cub_200_2011/)
- Rename or zip it as `bird_CUB_200_2011.zip`
- Upload it to the **root of your Google Drive** (`My Drive/`)

### 3. Open the Notebook
- Go to [colab.research.google.com](https://colab.research.google.com)
- Click `File → Upload notebook` and upload `Bird_Classification.ipynb`

### 4. Enable GPU
- Go to `Runtime → Change runtime type`
- Set Hardware accelerator to **T4 GPU**
- Click Save

### 5. Run the Notebook
- Click `Runtime → Run all`
- The notebook will:
  1. Mount your Google Drive
  2. Copy and extract the dataset to Colab's fast local storage
  3. Install required libraries (`timm`)
  4. Load and preprocess the data
  5. Train both models
  6. Evaluate and print accuracy, precision, recall, F1, and confusion matrix
  7. Save model checkpoints to `MyDrive/bird_models/`

> ⚠️ Training can take **30–90 minutes** depending on GPU allocation. Do not close the browser tab while training.

---

## 📚 Libraries Used

| Library | Purpose |
|---|---|
| `torch` / `torchvision` | Model building, training, transforms |
| `timm` | Access to pretrained model architectures |
| `numpy` / `pandas` | Data handling and metadata loading |
| `matplotlib` / `seaborn` | Visualisation and confusion matrix |
| `scikit-learn` | Metrics (accuracy, F1, classification report) |
| `PIL` | Image loading and bounding box cropping |
| `tqdm` | Training progress bars |

---

## 📊 Expected Output

- Per-epoch training and validation accuracy/loss
- Final test set metrics: accuracy, precision, recall, F1
- Confusion matrix heatmap
- Sample visualisation of training images (bbox cropped)
- Saved model weights in Google Drive

---

## 🔢 Reproducibility

All random seeds are fixed to `42`:
```python
SEED = 42
torch.manual_seed(SEED)
torch.cuda.manual_seed_all(SEED)
np.random.seed(SEED)
torch.backends.cudnn.deterministic = True
```
