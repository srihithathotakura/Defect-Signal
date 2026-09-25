# DefectSignal: Prioritizing Urgent Product Complaints in Consumer Tech Reviews

## Problem Statement

Tech brands receive large volumes of customer reviews across platforms such as Google Play Store and Flipkart. Manually reviewing this feedback can delay the identification of product defects, malfunction complaints, and other issues requiring attention.

This case study develops a text-classification approach to identify **Urgent** reviews, indicating safety risks, malfunctions, or refund/replacement demands, from **Non-Urgent** general feedback. The goal is to help quality assurance and customer support teams prioritize potentially important complaints for faster review.

## Objectives

1. Classify consumer reviews as **Urgent** or **Non-Urgent** using TF-IDF with Logistic Regression and Multinomial Naive Bayes, with emphasis on recall and F1-score for the Urgent class.
2. Identify recurring language patterns and product features associated with urgent complaints across wireless earbuds, smartwatches, and power banks.
3. Develop a data-driven triage approach that can help QA and customer support teams prioritize high-risk reviews.

## Data Collection

The dataset was collected through **web scraping of publicly accessible customer reviews** during 18–23 September 2026.

### Sources

* **Google Play Store:** Reviews from five companion applications associated with smartwatches and earbuds:

  * boAt Crest
  * NoiseFit
  * Zepp (Amazfit)
  * realme Link
  * HeyMelody

* **Flipkart:** Reviews from 12 product listings covering:

  * 5 power banks
  * 4 earbuds
  * 3 smartwatches

No ready-made dataset from Kaggle, UCI, GitHub, or similar repositories was used as the primary dataset.

The collected data was consolidated into a common structure and personal or identifying information was removed or anonymized before analysis.

### Dataset

The final raw dataset contains **16,768 reviews** and **13 attributes**.

Important variables include:

* `review_text` – customer review text used for text classification
* `rating` – review rating
* `product_category` – product category
* `platform_source` – source platform
* `source_type` – app or product review

The cleaned dataset used for analysis contains **12,449 reviews**.

## Analytics Methods

The analysis follows the complete workflow documented in `analysis.ipynb`:

1. Data quality checking and cleaning
2. Exploratory data analysis and visualization
3. Rule-based weak labeling of reviews as Urgent/Non-Urgent
4. TF-IDF text feature extraction
5. Logistic Regression classification
6. Multinomial Naive Bayes classification
7. Model comparison and selection
8. Evaluation using accuracy, precision, recall, F1-score and ROC-AUC
9. Confusion-matrix and error analysis

Because missing a genuinely urgent complaint is considered more costly than generating an additional review for human checking, **Urgent-class recall and F1-score** were given greater importance during model selection.

## Key Results

The selected **TF-IDF + Multinomial Naive Bayes** model achieved the following results on the held-out human-labeled test set:

| Metric           | Result |
| ---------------- | -----: |
| Accuracy         |  78.1% |
| Urgent Precision |  47.3% |
| Urgent Recall    |  84.5% |
| Urgent F1-score  |  60.7% |
| ROC-AUC          |  0.880 |

The analysis found that **app/device connectivity and pairing problems were the dominant urgency pattern** in the collected data. Safety-specific complaints such as overheating represented a much smaller proportion of the rule-identified urgent complaints.

The results support using the model as a **first-pass triage system with human review**, rather than as a fully automated decision system.

## Repository Contents

The submission contains the files required for the case study:

```text
DefectSignal_Submission/
│
├── README.md
├── analysis.ipynb
├── Case_Study_Report.pdf
│
└── data/
      └── reviews_raw.csv
      ├── reviews_clean.csv
      └── reviews_labeled.csv
```

### File Description

* **`README.md`** – Overview of the case study, problem, objectives, data collection, methods, key results and references.
* **`analysis.ipynb`** – Complete Jupyter Notebook containing data preparation, exploratory analysis, visualization, analytics/modeling, evaluation and outputs.
* **`Case_Study_Report.pdf`** – Final case study report following the prescribed report format.
* **`data/reviews_raw.csv`** – Collected raw review dataset.
* **`data/reviews_clean.csv`** – Final cleaned dataset used for analysis.
* **`data/reviews_labeled.csv`** – Dataset containing the labels used in the analysis.

## References

1. Abbas, Y., & Malik, M. S. I. (2023). *Defective products identification framework using online reviews*. Electronic Commerce Research, 23(2), 899–920. https://doi.org/10.1007/s10660-021-09495-8

2. Fuchs, M., Jadhav, A., Jaishankar, A., Cauffman, C., & Spanakis, G. (2023). *“What’s wrong with this product?” – Detection of hazardous products from online reviews*. Proceedings of the Nineteenth International Conference on Artificial Intelligence and Law (ICAIL '23), 397–401.

3. Mangnoesing, G. V. H., Truşcă, M. M., & Frasincar, F. (2020). *Pattern learning for detecting defect reports and improvement requests in app reviews*. Natural Language Processing and Information Systems (NLDB 2020), Lecture Notes in Computer Science, 12089. Springer. https://doi.org/10.1007/978-3-030-51310-8_12

4. Silva, M. L. M., Mendonça, A. L. C., Neto, E. R. D., Chaves, I. C., Brito, F. T., Farias, V. A. E., & Machado, J. C. (2025). *Classification of user reports for detection of faulty computer components using NLP models: A case study*. arXiv:2503.16614.

5. Google Play Store. https://play.google.com

6. Flipkart. https://www.flipkart.com

7. `google-play-scraper` Python package. https://pypi.org/project/google-play-scraper/

8. Flipkart Reviews Scraper, Apify actor (`solidcode/flipkart-scraper`). https://apify.com/solidcode/flipkart-scraper
