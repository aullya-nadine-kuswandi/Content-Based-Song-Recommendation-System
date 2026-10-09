# Content-Based Song Recommendation System

A content-based recommendation system that recommends songs based on their audio characteristics. The project uses Spotify track metadata and 12 audio features to calculate song similarity with cosine similarity, allowing users to discover tracks with similar musical properties without relying on listening history or user ratings.

## Key Objectives

- **Exploratory Data Analysis:** Investigate song characteristics, data quality, feature distributions, and relationships among audio features.
- **Data Preprocessing:** Handle missing values, duplicate records, inconsistent categorical values, and invalid audio feature values.
- **Feature Scaling:** Apply RobustScaler to prepare audio features for similarity calculations.
- **Similarity Calculation:** Use cosine similarity to measure the similarity between tracks based on their audio features.
- **Song Recommendation:** Develop a function that retrieves the most similar songs for a selected track.
- **Recommendation Analysis:** Compare the audio characteristics of recommended songs with those of the input track using visualizations.

## Dataset

The dataset contains song metadata, artist information, popularity scores, and audio features used to identify tracks with similar musical characteristics.

The selected audio features include:

| Feature | Description |
|---|---|
| Danceability | How suitable a track is for dancing |
| Energy | The perceived intensity and activity of a track |
| Loudness | The overall loudness of a track in decibels |
| Speechiness | The presence of spoken words in a track |
| Acousticness | The likelihood that a track is acoustic |
| Instrumentalness | The likelihood that a track contains no vocals |
| Liveness | The likelihood that a track was performed live |
| Valence | The musical positivity conveyed by a track |
| Tempo | The estimated speed of a track in BPM |
| Key | The estimated musical key of a track |
| Mode | Indicates whether a track uses a major or minor mode |
| Time Signature | The estimated number of beats per measure |

Popularity is retained as supplementary information for displaying recommendations but is excluded from the similarity calculation.

## Methodology

### Exploratory Data Analysis

- Examined dataset structure, data types, duplicate records, and missing values.
- Investigated numeric distributions and potential outliers.
- Analyzed popular tracks and frequently occurring artist genres.
- Explored changes in audio characteristics over time.
- Examined correlations between audio features.

### Data Preprocessing

- Removed the Track URI column, which was not required for recommendation generation.
- Converted invalid positive values in Loudness to missing values.
- Removed records with missing track names.
- Imputed missing artist genres using the mode for the corresponding artist, assigning `"Unknown"` when no genre information was available.
- Imputed missing values in Acousticness, Tempo, and Loudness using their respective medians.

### Feature Scaling

Applied RobustScaler to the 12 selected audio features. The transformation uses the median and interquartile range, helping reduce the influence of extreme values on feature scaling.

### Cosine Similarity

Calculated cosine similarity between the scaled audio feature vectors to measure the similarity between tracks. The resulting similarity scores are used to rank songs from the most similar to the least similar.

### Recommendation Generation

Implemented a recommendation function that:

1. Accepts a song title as input.
2. Checks whether the track exists in the dataset.
3. Retrieves and ranks similarity scores.
4. Excludes the input track from the recommendations.
5. Returns the top N recommended songs, including their titles, artists, genres, and popularity scores.

The number of recommendations can be adjusted using the `n` parameter.

## Example Usage

```python
recommend_songs("Style", n=5)
```

This example retrieves five tracks with audio characteristics most similar to *Style*, along with their artist names, genres, and popularity scores.

The input title must be available in the dataset.

## Recommendation Analysis

The generated recommendations are examined by comparing their audio characteristics with those of the input track. Visualizations help inspect similarities across selected audio features and provide insight into the characteristics shared by recommended songs.

## Conclusion

This project demonstrates how content-based recommendation techniques can support music discovery by identifying tracks with similar audio characteristics. By combining exploratory data analysis, data preprocessing, feature scaling, and cosine similarity, the system generates song recommendations based on musical properties rather than user behavior.

## Tech Stack

- **Language:** Python
- **Data Handling:** Pandas, NumPy
- **Data Visualization:** Matplotlib, Seaborn
- **Machine Learning:** scikit-learn (RobustScaler, cosine similarity)
- **Environment:** Jupyter Notebook
