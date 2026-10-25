# News Crawling and Clustering

**BIG DATA | DATA ANALYTICS | PYSPARK ‧ MONGODB**

A data processing project that collects news articles from Detik.com based on the keywords *Jokowi* and *Prabowo*, then applies text preprocessing, TF-IDF feature extraction, and K-Means clustering to explore similarities between news articles.

## 01. Project Overview

### Project Description

This project implements a news data pipeline consisting of web crawling, data cleaning, text preprocessing, feature extraction, clustering, evaluation, and data storage.

The project uses Python and BeautifulSoup to collect news articles from Detik.com, MongoDB to store the collected data and clustering results, and Apache Spark MLlib to process text and perform unsupervised learning.

### Project Objectives

- Collect news articles related to Jokowi and Prabowo from Detik.com.
- Clean and validate the collected dataset.
- Transform article text into numerical features using CountVectorizer and TF-IDF.
- Apply K-Means clustering to group articles based on text similarity.
- Evaluate clustering configurations using Silhouette Score.
- Export datasets and clustering results to JSON, CSV, and MongoDB.

### Dataset Summary

| Metric | Result |
|---|---:|
| Source | Detik.com |
| Search keywords | Jokowi, Prabowo |
| Total collected articles | 56 |
| Unique URLs | 56 |
| Missing values | 0 |
| Articles after cleaning | 56 |
| Articles after preprocessing | 56 |
| TF-IDF vocabulary size | 668 |
| Spark version | 3.5.4 |

The collected dataset contains 56 unique articles with no missing values in the `title`, `url`, `source`, `description`, and `page_number` fields.

### Data Pipeline

1. **News Crawling:** Collect articles matching the selected keywords.
2. **Data Storage:** Export the collected dataset to JSON and CSV and store records in MongoDB.
3. **Data Cleaning:** Remove incomplete records and duplicate URLs.
4. **Text Preprocessing:** Tokenize text and remove Indonesian stopwords.
5. **Feature Extraction:** Generate text features using CountVectorizer and TF-IDF.
6. **Clustering:** Apply K-Means with different values of K.
7. **Evaluation:** Compare Silhouette Scores and inspect cluster distributions.
8. **Output Storage:** Save clustering results to JSON, CSV, and MongoDB.

## 02. Tech Stack

| Technology | Purpose |
|---|---|
| Python | Main programming language |
| Requests | HTTP requests for web crawling |
| BeautifulSoup | HTML parsing and article extraction |
| Pandas | Dataset handling and CSV/JSON export |
| PyMongo | MongoDB integration |
| MongoDB | Storing crawled articles and clustering results |
| Apache Spark | Distributed data processing |
| PySpark MLlib | Text feature extraction and K-Means clustering |
| Matplotlib | Cluster distribution visualization |
| Jupyter Notebook | Interactive development and analysis |

**Machine Learning Techniques**
- Tokenization
- Indonesian stopword removal
- CountVectorizer
- TF-IDF
- K-Means Clustering
- Silhouette Score

## 03. Screenshots / Results

### 3.1 News Crawling Results

The crawling process collected and exported 56 articles from Detik.com.

| Validation Metric | Result |
|---|---:|
| Number of rows | 56 |
| Unique URLs | 56 |
| Missing titles | 0 |
| Missing URLs | 0 |
| Missing sources | 0 |
| Missing descriptions | 0 |
| Missing page numbers | 0 |
| New MongoDB documents | 56 |
| Total MongoDB documents after crawling | 56 |

**Generated files**
- `data/news_data.json`
- `data/news_data.csv`

### 3.2 Text Processing Results

The clustering notebook processed all 56 articles successfully.

| Processing Metric | Result |
|---|---:|
| Initial articles | 56 |
| Articles after cleaning | 56 |
| Articles after preprocessing | 56 |
| Vocabulary size | 670 |
| TF-IDF documents | 56 |

### 3.3 K-Means Model Comparison

Five clustering configurations were tested.

| K | Silhouette Score | Cluster Distribution |
|---:|---:|---|
| 2 | 0.2119 | 55, 1 |
| 3 | 0.1049 | 53, 2, 1 |
| 4 | -0.1660 | 50, 2, 1, 1, 2 |
| 5 | -0.1361 | 50, 2, 1, 1, 1, 1 |
| 6 | -0.0460 | 53, 1, 1, 1 |

The configuration with **K = 2** achieved the highest Silhouette Score of **0.2119** among the tested configurations. However, the resulting clusters were highly imbalanced: 55 articles were assigned to Cluster 0, while only one article was assigned to Cluster 1.

The score indicates that cluster separation remains relatively weak. Although K = 2 was the best candidate in this experiment, it does not demonstrate that the dataset has been grouped into clear or well-separated topics.

### 3.4 Cluster Analysis

The most frequent words in Cluster 0 included:

- `prabowo`
- `presiden`
- `tahun`
- `kabinet`
- `pemerintahan`
- `subianto`
- `sidang`
- `indonesia`

These terms reflect the prominence of Prabowo-related news in the collected dataset. Cluster 1 contained only one article, so its frequent words are insufficient to establish a reliable general topic.

**Result interpretation:** The experiment demonstrates an end-to-end unsupervised text clustering workflow, but the current dataset and feature configuration do not produce balanced clusters. Further work could explore a larger and more diverse dataset, improved Indonesian text preprocessing, and alternative feature or clustering configurations.

### 3.5 MongoDB Results

The final clustering results were stored in the `big_data` database and `uts` collection.

| Metric | Result |
|---|---:|
| Documents matched | 55 |
| Documents updated | 55 |
| New documents inserted during clustering | 1 |
| Total documents in collection | 57 |

The collection retained 57 documents, and the clustering field was updated for the matched records.

### 3.6 Screenshots

Add screenshots from the actual notebook outputs to the `screenshots/` directory.

Suggested screenshots:
- crawling and dataset validation summary.

<img width="1042" height="428" alt="image" src="https://github.com/user-attachments/assets/a8338982-5f0c-47cd-9a8b-9f841c3c4208" />

- cleaned data and TF-IDF output.

<img width="1284" height="184" alt="image" src="https://github.com/user-attachments/assets/6473b832-a3a6-440b-aa94-128ed1e84a51" />

- Silhouette Score comparison for different K values.

<img width="519" height="520" alt="image" src="https://github.com/user-attachments/assets/f01b9123-5ca3-4a15-b549-3c45f5cb54df" />

- article counts per cluster.

<img width="790" height="490" alt="image" src="https://github.com/user-attachments/assets/4018c319-0249-460a-92ef-0de9bcc84b8f" />

- MongoDB storage verification.

<img width="302" height="92" alt="image" src="https://github.com/user-attachments/assets/ac6abf94-ced7-4579-80f4-d453abbb3bc3" />


## 04. Installation & Usage

### Prerequisites

- Python
- Jupyter Notebook
- Java runtime compatible with the installed PySpark version
- Apache Spark through PySpark
- MongoDB running locally or an accessible MongoDB instance

### Project Structure

```text
data-NewsCrawlingAndClustering/
├── data/
│   ├── news_data.json
│   └── news_data.csv
├── notebooks/
│   ├── 01_news_crawling.ipynb
│   └── 02_news_clustering.ipynb
├── outputs/
│   ├── clustered_news.json
│   └── clustered_news.csv
├── screenshots/
├── README.md
└── requirements.txt
```

### Installation

1. Clone the repository:

   ```bash
   git clone <repository-url>
   cd data-NewsCrawlingAndClustering
   ```

2. Install the required Python packages:

   ```bash
   pip install requests beautifulsoup4 pandas pymongo pyspark matplotlib
   ```

3. Ensure MongoDB is running and accessible.

4. If using a remote MongoDB instance, configure the `MONGO_URI` environment variable. Do not commit database credentials to GitHub.

### Usage

1. Open `notebooks/01_news_crawling.ipynb`.
2. Run the notebook to collect articles and generate the JSON and CSV datasets.
3. Verify the dataset contains unique URLs and no missing required fields.
4. Open `notebooks/02_news_clustering.ipynb`.
5. Run the notebook to clean the dataset, preprocess text, create TF-IDF features, test K-Means configurations, and evaluate the results.
6. Review the cluster distributions and article samples.
7. Check the generated output files and verify the results in MongoDB.

**Important:** The input and output paths must match the notebook's working directory. For example, if a notebook is run from the `notebooks/` directory, the dataset path may need to be `../data/news_data.json`.

### Limitations

- The dataset contains only 56 articles and focuses on two keywords, which limits topic diversity.
- The crawling results depend on the website's page structure and the selected keywords.
- K-Means requires a predefined number of clusters.
- The best tested Silhouette Score was 0.2119, with a highly imbalanced cluster distribution.
- Cluster labels are numeric identifiers, not predefined news categories.
- The results should be treated as an experiment in unsupervised text clustering, not as a validated news-topic classification system.

### Future Improvements

- Collect more articles across a broader range of topics.
- Improve Indonesian stopword removal and add stemming or lemmatization.
- Experiment with alternative text representations and clustering algorithms.
- Inspect representative articles and keywords to interpret cluster meaning.
- Evaluate cluster stability and compare additional configurations.
