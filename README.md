# Content-Based Movie Recommender System using ML

## Project Overview

This project implements a foundational **Content-Based Filtering** recommendation system. In this case, the system recommends movies that share similar characteristics—such as plot, main cast, director, genres, and keywords—with a chosen input movie.

* **Developed by:** Dipman
* **Model Type:** Content-Based Filtering
* **Core Technique:** Cosine Similarity

---

## Dataset

The model utilizes the popular TMDB 5000 Movie Dataset, which includes information on approximately 5,000 movies.

* **Source:** [Kaggle TMDB 5000 Movie Metadata](https://www.kaggle.com/datasets/tmdb/tmdb-movie-metadata)
* **Files Used:**
    * `tmdb_5000_movies.csv` (Contains genres, overview, keywords, etc.)
    * `tmdb_5000_credits.csv` (Contains cast and crew information)

---

## Technical Implementation Steps

The entire pipeline is executed within a single Jupyter Notebook (or Google Colab environment) and involves the following steps:

### 1. Data Preparation and Merging
* The `movies` and `credits` dataframes were merged using the common identifier (`id` / `movie_id`) to create a single, comprehensive dataset.

### 2. Feature Engineering and Cleaning
* **Feature Selection:** The core features chosen to define movie similarity were: `genres`, `keywords`, `cast` (Top 3 actors), `director`, and `overview` (plot summary).
* **JSON Conversion:** The list-of-dictionaries format (JSON) in the `genres`, `keywords`, `cast`, and `crew` columns was converted into clean, usable Python lists.
* **Token Cleaning:** To ensure high-quality matching, spaces were removed and all text was lowercased (e.g., "Robert Downey Jr" became "robertdowneyjr") so that multi-word names are treated as a single, unique tag.

### 3. The "Tag Soup" Creation 
* All cleaned features (genres, keywords, top cast, director, and plot overview) for each movie were combined into a single string column called `soup`. This is the input text used by the model.

### 4. Vectorization
* The text in the `soup` column was converted into a numerical format using the **CountVectorizer** from `scikit-learn`. This created a matrix where each movie is a row and each unique word is a column, with cell values representing the word count.

### 5. Similarity Calculation (The Model Core)
* The similarity between all movie pairs was calculated using **Cosine Similarity**. This mathematical measure evaluates the angle between the vectors, providing a score from 0 (no similarity) to 1 (perfect similarity). This score forms the final recommendation matrix.

---

## Usage

To use the recommender, simply call the `get_recommendations()` function with the exact title of a movie from the dataset:
* Simply input the Movie Name inside the input box OR,
```python
# Function to get top 10 similar movies
get_recommendations('Avatar')
