 # SEO Content Detector

## Project Overview

The SEO Content Detector project identifies duplicate or low-quality ("thin") web content and evaluates content quality based on readability and word count. It uses TF-IDF-based similarity and a Random Forest model to classify and score text extracted from web pages.

---

## Setup Instructions

```bash
git clone https://github.com/priyankakadirvel/seo-content-detector
cd seo-content-detector
jupyter notebook notebooks/seo_pipeline.ipynb
```

Ensure the following dependencies are installed:

```bash
pip install pandas numpy scikit-learn beautifulsoup4 requests nltk
```

---

## Quick Start

1. Dataset : data/urls.xlsx
2. Open and run `seo_pipeline.ipynb` in Jupyter Notebook.
3. The notebook will:

   * Extract HTML and text from URLs.
   * Clean and preprocess the text.
   * Detect duplicate and thin content.
   * Train and evaluate a classification model for content quality.
4. Outputs such as `duplicate_pairs.csv`, `extracted_data.csv`, and trained model results will be saved in the `notebooks/` folder.

---

## Key Decisions

* **Choice of Libraries:**
  Used `BeautifulSoup` for parsing HTML, `scikit-learn` for TF-IDF vectorization and Random Forest classification, and `pandas` for data manipulation. These libraries provide strong support for text analytics workflows.

* **HTML Parsing Approach:**
  Extracted `<title>` and main `<body>` text using `BeautifulSoup`, ensuring noisy elements like scripts and styles are removed for cleaner text.

* **Similarity Threshold Rationale:**
  A cosine similarity threshold (0.8) was chosen to balance between detecting true duplicates and avoiding false positives.

* **Model Selection Reasoning:**
  Random Forest was selected for its interpretability, robustness on small datasets, and ability to handle non-linear relationships in text-derived features.

---

## Results Summary

The Random Forest model outperformed the baseline in detecting and classifying content quality levels. The model achieved an **overall accuracy of 84%**, compared to **72%** from the baseline classifier.

### Random Forest Model Performance

* **Accuracy:** 84%
* **Macro F1-score:** 0.58
* **Weighted F1-score:** 0.81
* **Observations:**

  * Strong recall for *Low Quality* content (1.00) and balanced precision-recall for *Medium Quality* (0.93 / 0.88).
  * The model struggled with *High Quality* samples due to limited representation (only 2 instances).
  * Shows robust classification of "Low" and "Medium" quality categories.

### Baseline Model Performance

* **Accuracy:** 72%
* **Macro F1-score:** 0.49
* **Weighted F1-score:** 0.71
* The baseline exhibited weaker performance, particularly misclassifying *Medium* and *High* quality texts.

### Confusion Matrix Insights

* **Random Forest:** Accurately classified all *Low Quality* items and most *Medium Quality* ones.
* **Baseline:** Over-predicted *Low Quality* and missed *High Quality* entirely.

### Key Feature Importance

1. **Word Count (0.43):** Primary indicator of content depth and richness.
2. **Flesch Reading Ease (0.31):** Reflects readability and complexity of text.
3. **Sentence Count (0.26):** Helps distinguish detailed, well-structured content from thin pages.

Overall, the Random Forest model demonstrated **significant improvement in quality prediction** and **more reliable duplicate/thin content detection** compared to the baseline approach.


---

## Limitations

* The TF-IDF approach does not capture deep semantic meaning between sentences.
* Results depend heavily on the quality of input text extraction from HTML.
* The model was trained on limited data and may need tuning for larger or domain-specific datasets.


