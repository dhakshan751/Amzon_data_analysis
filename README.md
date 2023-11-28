# Amzon_data_analysis
Utilized SQLite for data retrieval, prepped dataset. Explored Amazon product recommendation strategies, focusing on high-rated items. Analyzed user behavior, identified frequent users. Implemented sentiment analysis to grasp customer sentiments. Find insights in my GitHub repo.


# Amazon Customer Behavior Analysis

This GitHub repository explores Amazon customer behavior using data from an SQLite database. The analysis covers data retrieval, preparation, and insights into Amazon's product recommendation system. Additionally, it examines products with positive reviews, understands customer behavior, identifies frequent users, and performs sentiment analysis.

## Getting Started

### Prerequisites

- Python 3
- Required libraries: pandas, numpy, matplotlib, seaborn, textblob

### Installation

Install the necessary libraries using the following commands:

```bash
pip install pandas numpy matplotlib seaborn textblob
Data Preparation and Analysis
Data Retrieval: Connect to the SQLite database and read the data into a Pandas DataFrame.
python
Copy code
import pandas as pd
import sqlite3

# Connect to the SQLite database
conn = sqlite3.connect('path/to/your/database.sqlite')

# Read data from the 'reviews' table
df = pd.read_sql_query("SELECT * FROM reviews", con=conn)
Data Cleaning: Remove invalid and duplicate data, convert data types, and handle missing values.

Product Recommendation Analysis: Analyze user behavior to identify top users for product recommendations.

python
Copy code
# Group data by UserId and aggregate relevant metrics
recommend_products = df.groupby('UserId').agg({'Summary': 'count', 'Text': 'count', 'Score': 'mean', 'ProductId': 'count'}).sort_values(by='ProductId', ascending=False)
Product Review Analysis: Identify products with high orders and positive reviews.
python
Copy code
# Identify most sold products
product_order = df['ProductId'].value_counts().to_frame().sort_values(by='ProductId', ascending=False)
freq_product_order = product_order[product_order['ProductId'] > 500].index
freq_product = df[df['ProductId'].isin(freq_product_order)]
Customer Behavior Analysis: Distinguish between frequent and non-frequent users and analyze their review distribution.
python
Copy code
# Create a new column 'Viewer_Type' based on user frequency
df['Viewer_Type'] = df['UserId'].apply(lambda user: 'Frequent' if x[user] > 50 else 'Not Frequent')
Sentiment Analysis: Perform sentiment analysis on review text using the TextBlob library.
python
Copy code
from textblob import TextBlob

# Sample sentiment analysis on the 'Summary' column
sample['polarity'] = sample['Summary'].apply(lambda text: TextBlob(text).sentiment.polarity)
Results
Top users for product recommendations.
Most sold products and their reviews.
Distribution of reviews among frequent and non-frequent users.
Common positive and negative words in reviews.
Conclusion
This project provides valuable insights into Amazon customer behavior, aiding in understanding user preferences, product recommendations, and sentiment analysis.

Feel free to explore the Jupyter notebook provided for a detailed walkthrough of the analysis.
