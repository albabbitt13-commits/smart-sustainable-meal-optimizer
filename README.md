# Smart Sustainable Meal Optimizer

This project explores how meal recommendations can balance nutrition, cost and environmental impact. The goal is to develop a data-driven tool that helps users find food combinations that meet nutritional needs while staying within a budget and reducing environmental impact.

## Problem Statement

Choosing meals involves balancing nutritional goals, affordability and environmental sustainability. Foods that provide protein and calories may differ in price and greenhouse gas emissions. This project uses data analysis and machine learning to explore these tradeoffs and support more informed food choices.

The intended outcome is a meal recommendation tool that can eventually help users identify combinations that fit their nutritional needs and budget while considering environmental impact.

## Data

The project combines information from the following sources:

- [USDA FoodData Central](https://fdc.nal.usda.gov/): nutrition information, including protein, fat, carbohydrates and calories.
- [University of Michigan dataFIELD](https://css.umich.edu/page/datafield): estimated greenhouse gas emissions associated with food.
- USDA Economic Research Service sources: food price information.

The combined dataset contains 52 foods. Four foods have missing comparable price data, leaving 48 foods for the current modeling evaluation.

Data preparation included combining nutrition, price and environmental information, checking missing values and selecting comparable foods for modeling. Environmental impacts and prices are estimates or averages and may not represent every product or location.

## Methodology

### Weighted Food Recommendations

A weighted scoring approach ranks foods using four factors:

- Protein score: 40%
- Calorie score: 20%
- Cost score: 20%
- Environmental score: 20%

The nutrition features are scaled so they can be combined. Price and environmental scores are reversed so lower cost and lower estimated emissions receive higher scores.

### K-Means Clustering

K-Means clustering groups foods based on protein, calories, price and greenhouse gas emissions. Earlier experiments compared 2, 3, 4 and 5 clusters.

For the Unit 7 refinement, I compared the baseline three-cluster K-Means model with a weighted version that gives protein and environmental impact more influence. Both models used an 80/20 train/test split.

## Results

### Model Comparison

The baseline and refined models produced the following test results:

| Model | Test Silhouette Score | Test Inertia |
|---|---:|---:|
| Baseline K-Means | 0.622 | 0.649 |
| Refined Weighted K-Means | 0.622 | 0.672 |

The silhouette score was the same for both models, so the feature weighting did not improve measured cluster separation. The baseline also had lower test inertia. Based on these metrics, the refined model did not outperform the baseline.

![Baseline and refined model comparison](images/model_comparison.png)

### Food Recommendations

The weighted scoring model ranks foods by the balance of protein, calories, affordability and estimated environmental impact.

![Top 10 food recommendations](images/food_recommendations.png)

The rankings reflect the chosen weights and available data. A lower recommendation score does not necessarily mean a food is unhealthy or unsuitable for every meal.

## Limitations and Future Work

The current dataset is small and contains only 48 foods with comparable price data. Food prices vary by location, store and time, while environmental impacts are estimates that may not reflect individual products.

The current scoring model ranks individual foods rather than verifying whether complete meals meet a person's specific nutritional requirements. Clustering also groups similar foods but does not directly optimize meals.

Future work will focus on expanding the dataset, testing additional model configurations, improving visualizations and developing meal-level recommendations that account for nutritional targets, budget limits and environmental impact.

## Setup

1. Clone or download this repository.
2. Install the required Python packages:

```bash
pip install -r requirements.txt
```

3. Open `notebooks/01_data_exploration.ipynb` in Jupyter Notebook or VS Code.
4. Run the notebook cells in order.

## Technologies Used

- Python
- pandas and NumPy
- scikit-learn
- Matplotlib
- Jupyter Notebook
