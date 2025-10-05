IMDb Movie Dataset: Data Cleaning and Preprocessing for Machine Learning
A complete data science project demonstrating the cleaning, preprocessing, and feature engineering of a raw movie dataset to make it ready for machine learning analysis.

This repository documents the end-to-end data cleaning and preprocessing of the IMDb movie dataset. The primary goal of this project was to take a raw, real-world dataset and transform it into a fully numeric, clean, and structured format suitable for building predictive machine learning models.

Project Links
[git clone https://lnkd.in/eSuarE-J]


Project Overview
Real-world data is often messy, inconsistent, and contains missing values. Before any meaningful analysis or modeling can be done, the data must be rigorously cleaned. This project walks through the essential steps of inspecting, cleaning, and transforming the data, demonstrating key skills in data wrangling and feature engineering.

The final output is a model-ready CSV file where all categorical information has been logically converted into a numerical format, and all missing values have been handled.

The Dataset
The project uses the "TMDb 5000 Movie Dataset" (originally from Kaggle, contained in movie_metadata.csv). This dataset contains 28 columns and over 5,000 rows, with a mix of numerical and categorical data about movies, including budget, gross revenue, cast, genres, and IMDb score.

Data Preprocessing Workflow
The following steps were systematically applied to clean and prepare the data:

1. Initial Exploration and Separation
The raw dataset was loaded using the Pandas library.

It was immediately split into two separate DataFrames: one for numeric features (numeric_df) and one for categorical/string features (string_df) to apply different cleaning strategies to each.

2. Handling Missing Values (Imputation)
A key challenge was handling numerous missing values. Instead of a one-size-fits-all approach, I analyzed each column's distribution to choose the best imputation method.

Numerical Columns: By visualizing the data with box plots, it became clear that features like budget, gross, duration, and all facebook_likes columns were heavily skewed and contained significant outliers. Therefore, the median was used to fill missing values, as it is a more robust measure of central tendency than the mean in skewed distributions.

Categorical Columns: Missing values in string-based columns were filled using logical replacements, such as filling missing director_name with "Unknown" or filling missing color values with the mode (the most frequent value).

3. Cleaning and Feature Engineering
High-Cardinality Features: For categorical columns with too many unique values (like language and country), I grouped all infrequent categories (e.g., those appearing less than 50 times) into a single "Other" category. This reduces noise and complexity for the model.

Whitespace Stripping: The movie_title column had trailing whitespace, which was removed using .str.strip() to ensure consistency.

4. Categorical Encoding (Creating Dummy Variables)
To prepare the data for machine learning algorithms, all remaining text-based columns were converted into a numeric format.

Multi-Label One-Hot Encoding: The genres column was a special case, as a single movie can have multiple genres (e.g., "Action|Adventure|Sci-Fi"). I used the powerful str.get_dummies(sep='|') method to correctly create a separate binary column for each genre.

Standard One-Hot Encoding: For single-choice categorical columns (color, language, country, content_rating), I used pd.get_dummies() with drop_first=True to create new binary columns for each category while avoiding multicollinearity.

5. Feature Selection for Modeling
Irrelevant columns like movie_title, director_name, actor_names, and plot_keywords were dropped from the final modeling dataset, as they are not suitable for a baseline model in their raw text form.

Redundant features, such as the individual actor Facebook likes columns, were dropped in favor of the more comprehensive cast_total_facebook_likes feature to reduce multicollinearity.

6. Finalization
All appropriate numeric columns were converted from float to int for memory efficiency and semantic correctness.

The fully cleaned and encoded dataframe was saved to a new file, movie_metadata_preprocessed.csv, creating a reliable checkpoint for future work.

Technologies Used
Python

Pandas for data manipulation and cleaning.

Matplotlib & Seaborn for data visualization and analysis.

Jupyter Notebook for interactive development.

How to Use This Repository
Cloning the Repository
To get a local copy of this project up and running, you can clone the repository using Git.

On the main repository page on GitHub, click the green "<> Code" button.

Copy the URL provided under the "HTTPS" tab.

Open your terminal or command prompt and run the following command:

git clone [PASTE THE COPIED REPOSITORY URL HERE]

This will create a local folder on your computer containing all the project files.

Running the Project
After cloning, you can find the final, cleaned dataset at movie_metadata_preprocessed.csv.

You can load this file into a Pandas DataFrame to begin your own analysis or to train machine learning models without needing to repeat any of the cleaning steps.

Future Work
The preprocessed dataset is now perfectly suited for the next steps in the data science pipeline, which could include:

Building regression models (e.g., Linear Regression, XGBoost) to predict imdb_score or gross.

Performing a deeper exploratory data analysis (EDA) to find interesting correlations and insights.

Applying more advanced feature engineering techniques, such as target encoding for director names, to potentially improve model accuracy.
