# Spotify Popularity Prediction - Final Project

## Overview
This repository contains the final project for **IEORE4523: Data Analytics** at **Columbia University** (Fall 2023). The project, *Spotify Popularity Prediction*, was completed by **Kaidi Chen, Tiffany Cheng, Hasong Cho, Hailey Chung, and Jiayun Yin**. Our goal was to analyze how different song features relate to popularity on Spotify and build models to predict which songs might become hits.

## Project Motivation
Spotify is one of the biggest music streaming platforms, influencing what people listen to worldwide. Understanding what makes a song popular can help artists, producers, and even Spotify itself. This project looks at the key features of songs and how they impact popularity.

## Dataset
- **Source:** *30,000 Spotify Songs Dataset* from Kaggle, collected via the Spotify API.
- **Features:**
  - **Basic Info:** track_id, track_name, track_artist, track_popularity
  - **Album Details:** track_album_id, track_album_name, track_album_release_date
  - **Playlist Info:** playlist_name, playlist_id, playlist_genre, playlist_subgenre
  - **Audio Features:** danceability, energy, key, loudness, tempo, acousticness, instrumentalness, liveness, valence, speechiness, duration
- **Data Cleaning:**
  - Removed missing values and duplicates
  - Filtered out tracks shorter than 60 seconds
  - Normalized numerical features for model training

## Exploratory Data Analysis (EDA)
- **Trends Over Time:**
  - Danceability, energy, and valence have increased, while acousticness and duration have gone down.
  - Pop is the most popular genre, while EDM is among the least popular.
- **Feature Correlations:**
  - Energy and loudness are strongly related (0.68)
  - Valence and danceability show some connection (0.33), meaning upbeat songs tend to be more danceable.
  - Energy and acousticness have a strong negative relationship (-0.54), which makes sense since electronic music is usually high-energy but not very acoustic.
- **Word Cloud Analysis:**
  - The word "love" appears the most in song titles, showing that it’s still a dominant theme in popular music.

## Machine Learning Models
We tested both **regression** and **classification** models to predict popularity.

### Regression Models
- **Ordinary Least Squares (OLS) Regression:**
  - Looked at feature importance in predicting popularity.
  - The R-squared value (~0.099) was low, meaning the model didn't explain much.
- **Scikit-learn Linear Regression:**
  - Tested on separate data, but the R-squared (~0.086) was still low, suggesting that a linear approach wasn't the best fit.

### Classification Models
We turned popularity into a classification problem, defining "popular" songs using percentiles (75th, 85th, 95th percentiles).

- **Logistic Regression:**
  - Worked okay at the 75th percentile but struggled at higher percentiles because of class imbalance.
- **Decision Tree Classifier:**
  - Used hyperparameter tuning and cross-validation.
  - Performed well at lower percentiles but showed overfitting.
- **Random Forest Classifier:**
  - The best performer, especially at the 85th percentile, where it had a good balance of accuracy and recall.

## Key Findings
- **Speechiness, danceability, and energy-loudness ratio were the most important factors in predicting popularity.**
- **Random Forest was the most reliable model, especially at the 85th percentile threshold.**
- **Popularity classification is tricky since it depends on arbitrary cutoffs. A better approach could be using AUC-ROC analysis instead.**

## Future Improvements
- **Refining feature selection** by adding external data, such as playlist inclusion and social media mentions.
- **Handling class imbalance** by trying resampling methods or adjusting thresholds.
- **Exploring more models** like Gradient Boosting or Neural Networks to improve accuracy.
