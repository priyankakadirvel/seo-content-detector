 Workflow
 
1. Data Collection & HTML Parsing (15%)

Installs required libraries for web scraping and parsing.

Fetches HTML content from given URLs using robust error-handling and time delays.

Extracts title and body text from each webpage.

2. Text Preprocessing & Feature Engineering (25%)

Cleans and tokenizes text, removing stopwords and HTML tags.

Generates TF-IDF vectors for the processed text.

Extracts features such as:

Word count

Flesch Reading Ease score

Keyword density

Readability-based metrics

3. Duplicate Detection (20%)

Computes cosine similarity between TF-IDF vectors.

Flags pairs of pages with similarity above a threshold as duplicates.

Labels content as “thin” based on low word count or redundancy.

Saves cleaned and labeled data into:

duplicates.csv — duplicate URL pairs

extracted_content.csv — main dataset with “is_thin” column

4. Content Quality Scoring (25%)

Defines a content quality label using readability and word count thresholds.

Trains a Random Forest Classifier to predict quality categories.

Evaluates with:

Accuracy

F1-score

Confusion Matrix

Requirements

To set up the environment:

pip install pandas numpy scikit-learn beautifulsoup4 requests nltk

 
Open the notebook:

notebooks/seo_pipeline.ipynb

Run all cells sequentially.

It will parse, clean, extract features, detect duplicates, and train the quality model.

Outputs will be saved in the data/ and models/ folders.

 Outputs

extracted_content.csv → Parsed and preprocessed text.

duplicates.csv → Similar or duplicate content pairs.

features.csv → Engineered dataset with readability & keyword stats.

Trained Model → Saved in the models/ directory.

 Evaluation Metrics

Accuracy

Precision / Recall / F1-Score

Confusion Matrix visualization

