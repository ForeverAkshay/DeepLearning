# Deep Learning & AI Coursework

There are two projects in this repo:

1. **Bird Classification:** Fine-grained bird species classification on CUB-200-2011 using ResNet152 and a custom CNN (PyTorch, Google Colab)
2. **Bias Detection:** NLP-based bias analysis of AI-generated children's story premises — gender, racial, cultural, and theme bias (Python, NLTK, Plotly)

---

## 1. Bird Species Classification — CUB-200-2011

Fine-grained image classification of **200 bird species** using the CUB-200-2011 dataset (~11,788 images).

Two models are compared:
- **ResNet152** (pretrained on ImageNet, fine-tuned) — targets 90%+ accuracy
- **Custom CNN** (trained from scratch) — architectural baseline

Bounding box cropping is used to focus the model on the bird and remove background noise. Built in PyTorch and designed to run on **Google Colab with GPU**.

### Quick Start
1. Upload `bird_CUB_200_2011.zip` to the root of your Google Drive
2. Open `Bird_Classification.ipynb` in Colab and enable GPU (`Runtime → Change runtime type → T4 GPU`)
3. Run all cells — training, evaluation, and model saving are fully automated

### Libraries
`torch` `torchvision` `timm` `scikit-learn` `pandas` `matplotlib` `seaborn`

---

## 2. Bias Detection in Children's Story Premises

NLP-based analysis of **100 AI-generated children's story premises** to detect and visualise bias across five dimensions:

- **Gender** — term frequency, stereotyped adjectives, story-level dominance labels
- **Race/Ethnicity** — representation across 8 ethnic groups
- **Geography** — setting distribution across 10 world regions
- **Theme** — dominant narrative themes (conflict, war, friendship, etc.)
- **Character roles** — protagonist vs antagonist demographic patterns

### Quick Start
1. Open `Bias_Detection.ipynb` in Google Colab (no GPU needed)
2. Upload `premises.csv` using the left sidebar file panel
3. Run all cells — charts are saved automatically as PNG files

### Libraries
`pandas` `nltk` `textblob` `wordcloud` `plotly` `matplotlib` `seaborn`
