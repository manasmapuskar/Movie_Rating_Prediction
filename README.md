# 🎥 Movie Rating Prediction

---

## 📊 Project Overview
This project focuses on building a predictive model to estimate movie ratings using various features such as genre, cast, director, and more. The goal is to accurately forecast ratings, uncover the influence of different factors on a movie's success, and compare the performance of multiple models.

---

## 📁 Dataset & Features

### Dataset Columns
| **Feature**       | **Description**                                   |
|--------------------|---------------------------------------------------|
| **Name**          | Title of the movie                                |
| **Year**          | Release year                                      |
| **Duration**      | Runtime of the movie in minutes                   |
| **Genre**         | Comma-separated genres                            |
| **Rating**        | IMDb-like rating (target variable)                |
| **Votes**         | Number of audience votes                          |
| **Director**      | Director of the movie                             |
| **Actor 1**       | Leading actor/actress                             |
| **Actor 2**       | Supporting actor/actress                          |
| **Actor 3**       | Additional cast member                            |

### Engineered Features
To enhance the model’s performance, the following features were created:

- **Director Success Rate**: Average rating of all previous movies directed by the same person.
- **Average Genre Rating**: For movies with one or more genres, this is the average rating of all movies that share the same genres. Multi-genre movies average across all applicable genres.

#### Feature Example: Average Genre Rating
This feature was engineered by exploding multi-genre movies into separate entries and computing the average rating per genre. For a new movie with multiple genres, the model uses the mean of these genre averages.

```python
# Example usage:
Enter one or more genres (comma-separated): Action,Drama
Average Genre Rating for Action, Drama: 6.8
Genres not found in dataset: Fantasy
```

#### Feature Example: Director and Actor Success Rate
A custom utility that allows users to search for the average rating of movies involving a specific director or actor.

```python
# Example usage:
Do you want to search by 'director' or 'actor'? actor
Enter actor name: Tabu
Average rating for movies with actor 'Tabu': 5.63
```

These features help the model capture contextual quality indicators such as a director's prior performance and how genres or actors tend to perform.

---

## 🔧 Preprocessing Steps

1. **Handling Missing Values**:
    - Removed rows with missing values for key features like Rating, Director, Genre, and Actor names to maintain dataset consistency.

2. **Encoding Categorical Variables**:
    - One-hot encoding was applied to categorical variables such as Genre, Director, and Actors.

3. **Feature Scaling**:
    - Not required for tree-based models like Random Forest, but Votes was log-transformed to reduce skewness.

---

## 🤖 Modeling Approach

### Regression Model (Baseline Model)
- **Results**:
  - MAE: 1.349
  - MSE: 4.293
  - RMSE: 2.072
  - R²: -1.318
- **Why it performed poorly**:
  - Assumes linear relationships between features and rating.
  - Does not handle feature interaction or non-linearity well.
  - Sensitive to outliers and multicollinearity.

### Random Forest Regressor (Improved Model)
- **Results**:
  - MAE: 0.522
  - MSE: 0.587
  - RMSE: 0.766
  - R²: 0.692
- **Why it performed well**:
  - Captures complex interactions between features.
  - Handles missing data and outliers better.
  - Naturally works with categorical variables.
- **Why we chose it**:
  - Robust, versatile, and less prone to overfitting with good hyperparameter control.

---

## 📐 Evaluation Metrics

- **MAE (Mean Absolute Error)**: Average of absolute prediction errors.
- **MSE (Mean Squared Error)**: Penalizes larger errors more than MAE.
- **RMSE (Root Mean Squared Error)**: Square root of MSE, interpretable in original units.
- **R² Score**: Measures the proportion of variance explained by the model.

---

## 🗂 Project Structure

```
MovieRatingPrediction/
├── data/
│   └── movies.csv
├── Movie_Rating_Prediction_Modified.ipynb
├── README.md
└── requirements.txt
```

---

## ✅ Conclusion
By using feature engineering techniques and testing various models, we were able to significantly improve prediction accuracy. While linear regression provided a simple baseline, tree-based models like Random Forest gave superior results by handling non-linear patterns and interactions more effectively.
