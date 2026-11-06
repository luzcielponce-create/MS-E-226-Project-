# MS&E 226: Netflix Availability Prediction

## Project Overview
This project predicts the probability that a movie or TV show is available on Netflix using title characteristics, audience ratings, and popularity information.

Our stakeholder is a streaming guide service, such as JustWatch, that could use these predictions to help prospective Netflix subscribers estimate how much of their watchlist may be available.

The dataset reflects historical streaming availability through 2021, not Netflix's current catalog.

## Data Sources

Our project combines streaming availability and title metadata from multiple sources:

- Movies on Netflix, Prime Video, Hulu and Disney+ (Kaggle, by Ruchi Bhatia): https://www.kaggle.com/datasets/ruchi798/movies-on-netflix-prime-video-hulu-and-disney
- Netflix TV Shows and Movies (Kaggle, by Victor Soeiro): https://www.kaggle.com/datasets/victorsoeiro/netflix-tv-shows-and-movies 
- TV shows on Netflix, Prime Video, Hulu and Disney+ (Kaggle, by Ruchi Bhatia): https://www.kaggle.com/datasets/ruchi798/tv-shows-on-netflix-prime-video-hulu-and-disney? 
- IMDb non-commercial datasets, used for genre, runtime, ratings, and votes: https://datasets.imdbws.com/

Permission: the IMDb data is released for personal, non-commercial use, so course projects can use this data. The Kaggle datasets are publicly downloadable and available.

## Project Files

- `Final_Copy_of_TV_Shows_&_Movies_Streaming_Data.ipynb`: Cleans and merges the source datasets and constructs the Netflix availability outcome.
- 'Holdout_Data.ipynb': Creates 80/20 exploration/holdout set. 
- `Correlation_coefficients.ipynb`: Performs exploratory analysis.
- `Prepping_models_prediction.ipynb`: Preprocessing, feature engineering, cross-validation, model comparison, and final model fitting.
- 'final_netflix_model.pkl': Final model.
- `requirements.txt`: Python package versions used to run the analysis.

## Reproducing Our Analysis

1. Download original datasets using the links provided above.
2. Open notebooks in Google Colab.
3. Run `Final_Copy_of_TV_Shows_&_Movies_Streaming_Data.ipynb` to generate the cleaned dataset
4. Run 'Holdout_Data.ipynb to reproduce the 80/20 split.
5. Run `prepping_models_-parts_a-through-d_of_prediction.ipynb` using the development/exploration dataset (`explore_80.csv`).
6. This last notebook evaluates models using five-fold stratified cross-validation and selects the configuration with the lowest mean validation log loss.

The 20% holdout dataset is reserved for evaluation in Part 2 and is not used for model selection.

## Models and Features

We evaluate three algorithms:

- L1-regularized logistic regression
- Classification tree
- Random forest

Each algorithm uses two feature sets:

**Set 1:** Runtime, content type, age rating, 28 genre indicators, and runtime/genre missingness indicators.

**Set 2:** All Set 1 predictors, plus IMDb rating, Rotten Tomatoes score, and IMDb vote count.

**Set 2:** All Set 2 predictors, plus release year.

The selected model is a classification tree using Set 3, with maximum depth 8 and minimum leaf size 100. The classification threshold is 0.5.

## Reproducibility

- Random seed: `226`
- Cross-validation: five-fold stratified cross-validation
- Primary evaluation metric: Mean validation log loss
- Development data: 11,906 titles
- Holdout: 20% of the full dataset, excluded from Part 1 model selection
- Package versions: See `requirements.txt`

All data-dependent preprocessing, including missing-value imputation and categorical encoding, is fitted on training data within each cross-validation fold.

## Notes and Limitations

The model estimates historical Netflix availability and should not be used as a definitive source for current streaming availability. Missing metadata, differences in title coverage, and changes to streaming catalogs may affect prediction reliability.
