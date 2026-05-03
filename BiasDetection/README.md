# Bias Detection in Children's Story Premises

An NLP-based analysis of 100 AI-generated children's story premises to detect, quantify, and visualise potential biases across gender, race/ethnicity, geography, theme, and character roles.

---

## Dataset — premises.csv

| Detail | Info |
|---|---|
| **File** | `premises.csv` |
| **Size** | 100 story premises |
| **Format** | Plain CSV, no header, one story premise per row |
| **Source** | AI-generated story premises (provided as part of coursework) |
| **Content** | Short narrative premises for children's stories |

Each row is a single text premise describing the setup of a children's story. The analysis treats this as a text corpus and applies keyword-based NLP and sentiment analysis to surface patterns.

---

## What is Analysed & Why

### 1. Gender Bias
**What:** Counts male-coded and female-coded terms (pronouns, roles, titles) and gendered adjectives across all 100 premises.

**Why:** Children's stories have historically over-represented male protagonists and assigned stereotyped traits by gender (e.g. "brave" for male, "gentle" for female). Measuring this reveals whether AI-generated premises replicate these patterns.

**Method:** Regex word-boundary matching against predefined male/female term lists and adjective lists. Each story is labelled as Male-dominant, Female-dominant, Balanced, or Gender-neutral.

---

### 2. Racial & Ethnic Representation
**What:** Counts how many stories reference each of 8 ethnic/racial groups.

**Why:** Underrepresentation of certain groups in children's media can reinforce the idea that some communities are "default" or central while others are peripheral or absent.

**Method:** Keyword presence detection across 8 groups: African American/Black, Caucasian/European, Latino/Hispanic, Asian/East Asian, South Asian, Middle Eastern/Arab, Indigenous/Native, Mixed/Mestizo.

---

### 3. Geographical & Cultural Bias
**What:** Maps each story's setting to one of 10 world regions.

**Why:** A Western-centric or Eurocentric distribution of settings reflects cultural bias — it positions some regions as "normal" story settings and others as exotic or absent.

**Method:** Keyword matching against region-specific place names, nationalities, and cultural references across 10 regions including Fictional/Unspecified.

---

### 4. Theme Bias
**What:** Identifies dominant narrative themes (e.g. conflict, war, justice, friendship, family).

**Why:** Overrepresentation of conflict/war themes may normalise aggression, while underrepresentation of themes like community or cooperation reflects a skewed narrative landscape.

---

### 5. Character Role Bias
**What:** Examines which demographic groups are cast as protagonists vs antagonists.

**Why:** Systematically assigning villainous or passive roles to particular groups (by gender, race, etc.) encodes harmful stereotypes even in fictional narratives.

---

## How to Run (Step by Step)

### 1. Prerequisites
- A **Google account**
- Google Colab (free) — no local install needed
- The `premises.csv` file (provided with the coursework)

### 2. Open the Notebook
- Go to [colab.research.google.com](https://colab.research.google.com)
- Click `File → Upload notebook` and upload `Bias_Detection.ipynb`

### 3. Upload the Dataset
- Once the notebook is open, click the **folder icon** in the left sidebar
- Click the **upload icon** and select `premises.csv`
- Wait for the upload to complete (it will appear in the file list)

### 4. Run the Notebook
- Click `Runtime → Run all`
- The notebook will:
  1. Install required libraries automatically
  2. Load and clean `premises.csv`
  3. Run all 5 bias analyses in sequence
  4. Print summary statistics for each dimension
  5. Generate and save visualisation charts as PNG files

>  No GPU needed — this notebook runs fine on the default CPU runtime.

### 5. View & Download Output Charts

The following PNG files are saved to the Colab working directory after running:

| File | Contents |
|---|---|
| `gender_bias.png` | Gender term frequency bar + story dominance pie chart |
| `gendered_adjectives.png` | Stereotyped adjective usage by gender |
| `ethnic_representation.png` | Racial/ethnic group representation across stories |

To download: right-click any file in the left sidebar → **Download**.

---

## Libraries Used

| Library | Purpose |
|---|---|
| `pandas` | Data loading and manipulation |
| `nltk` | Tokenisation, stopword removal, POS tagging |
| `textblob` | Sentiment analysis |
| `wordcloud` | Word cloud visualisations |
| `plotly` | Interactive charts |
| `matplotlib` / `seaborn` | Static charts and styling |
| `re` | Regex-based keyword matching |

All libraries are installed automatically by the first cell of the notebook.

---

## Expected Output

- Printed summary tables for each bias dimension
- Bar charts, pie charts, and word clouds for each analysis
- Saved PNG files in the Colab working directory
- A holistic picture of where AI-generated story premises show measurable bias

---

## Notes

- The keyword lists (gender terms, ethnic groups, regions) are defined at the top of each analysis section and can be extended or modified to broaden the analysis
- Stories with no gendered terms are labelled "Gender-neutral" rather than "Balanced"
- Geographical detection is keyword-based and may miss implicit cultural references not captured in the current lists
