## TokoGenZ: Product Clustering and Recommendation System

### Overview
TokoGenZ is a new marketplace offering diverse products from various sellers. However, the lack of a clear product categorization system has led to challenges for users in finding desired items efficiently. This issue not only diminishes the shopping experience but also increases the risk of users losing interest in the platform.

To address this, a clustering approach was implemented to group products into meaningful categories based on their names. This clustering will improve user experience and enable TokoGenZ to provide better product recommendations.

---

### Dataset
The primary dataset contains **933,985 product entries** with the following columns:
- **Product Name**
- **Price**
- **Location**
- **Rating**
- **Sold**

---

### Objective
The main goals are:
1. **Preprocessing Product Names**: Clean the dataset to extract relevant information for clustering.
2. **Clustering Products**: Identify meaningful categories based on product names.
3. **Recommendation System**: Utilize clustered data to develop a product recommendation system.

---

### Preprocessing Methodology

#### Key Challenges:
- Product names often contain irrelevant words or symbols.
- Basic preprocessing methods (e.g., stemming, stopword removal) are insufficient for this dataset.
- Due to the dataset's size (933,985 entries), only 0.01% of the data was used to expedite processing.

#### Our Preprocessing Approach:
**Part-of-Speech (POS) Tagging** was used to extract noun-related terms, ensuring only relevant words were retained. Two POS tagging libraries were compared:
- **Stanza**
- **Flair**

#### Workflow:
1. **Preprocessing with POS Tagger**: Filter out words unrelated to nouns.
2. **Handling Empty Data**:
   - Entries with no nouns were filled with basic preprocessed names.
3. **Feature Conversion**:
   - Text data converted into numeric format using either **TF-IDF** or **SentenceTransformer**.
4. **Filtering Rare Words**:
   - Words appearing less than a specified threshold (e.g., 10 occurrences) were removed.
5. **Clustering**:
   - Conducted using the best-preprocessed dataset.

---

### Experiment Files
The following Jupyter notebooks document various experiments:

| File Name                     | Description                                                                 |
|-------------------------------|-----------------------------------------------------------------------------|
| `main_pos_flair_bert.ipynb`   | Flair POS tagger + SentenceTransformer for text conversion.      |
| `main_pos_flair_tfidf.ipynb`  | Flair POS tagger + TF-IDF for text conversion.                   |
| `main_pos_flair.ipynb`        | Flair POS tagger + TF-IDF, directly applying `min_df`.                      |
| `main_pos_stanza_bert1.ipynb` | Stanza POS tagger + SentenceTransformer for text conversion.     |
| `main_pos_stanza_bert.ipynb`  | Stanza POS tagger + SentenceTransformer.                         |
| `main_pos_stanza_tfidf1.ipynb`| Stanza POS tagger + TF-IDF for text conversion.                   |
| `main_pos_stanza_tfidf.ipynb` | Stanza POS tagger + TF-IDF.                                      |
| `main_pos_stanza.ipynb`       | Stanza POS tagger + TF-IDF, directly applying `min_df`.                      |
| `just_analysis.ipynb`         | Analysis of all preprocessing and clustering results.                       |

---

### Results

#### Selected Preprocessing Method
Based on extensive experiments, the best method was determined to be:
- **Stanza POS Tagger**
- **TF-IDF**
- Filtering words appearing fewer than **40 times**

The output of this preprocessing method is stored in the column **'en_noun remove_40'**.

#### Clustering Results
- **Optimal Clusters**: 516 clusters (evaluated using silhouette scores and manual inspection).
- **Silhouette Score**: ~0.05 (while low, manual inspection showed better cluster quality than other methods with higher scores).

#### Example Clusters:
- **Cluster 1**: Clothing

![Wordcloud for Cluster 1](plot/wordcloud%20cluster%201.png "Wordcloud for Cluster 1")

- **Cluster 2**: Pinsets

![Wordcloud for Cluster 2](plot/wordcloud%20cluster%202.png "Wordcloud for Cluster 2")

- **Cluster 13**: Watches

![Wordcloud for Cluster 13](plot/wordcloud%20cluster%2013.png "Wordcloud for Cluster 13")

- **Cluster 14**: Pasta (mix of food flavoring and toothpaste)

![Wordcloud for Cluster 14](plot/wordcloud%20cluster%2014.png "Wordcloud for Cluster 14")

#### Observations
- Clustering quality is satisfactory for the first 10 clusters, though some categories contain mixed items.

---

### Visualizations

#### Key Plots
1. **Elbow Method Plot**: Identifies the optimal number of clusters.
![Elbow Method Plot](plot/elbow%20method%20for%20optimal%20k.png "Elbow Method Plot")
2. **Facet Grid Plot**: Visualizes the distribution of silhouette scores for each preprocessing method.
![Facet Grid Plot](plot/distribution%20of%20average%20silhoutte%20score%20using%20facet%20grid.png "Facet Grid Plot")
3. **Line Plot**: Shows the trend of silhouette scores over cluster ranges.
![Line Plot](plot/trend%20of%20average%20silhoutte%20score.png "Line Plot")
4. **Box Plot**: Compares silhouette scores across preprocessing methods.
![Box Plot](plot/distribution%20of%20silhoutte%20score.png "Box Plot")

#### Additional Insights
- **Top 10 Locations by Total Sales**
![Top 10 Locations by Total Sales](plot/top%2010%20location%20by%20total%20sales.png "Top 10 Locations by Total Sales")
- **Average Price per Location**
![Average Price per Location](plot/avg%20price%20per%20location.png "Average Price per Location")
- **Top 10 Most Common Locations**
![Top 10 Most Common Locations](plot/top%2010%20most%20common%20location.png "Top 10 Most Common Locations")

---

### Future Development
To further enhance this approach, future work could involve:
- **Refining the Preprocessing Method**: Improving the POS tagging model by creating a custom POS tagging dataset specifically tailored to product names. This will improve preprocessing quality and clustering outcomes.