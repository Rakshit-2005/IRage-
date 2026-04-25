# IRage - Machine Learning Regression Project

## Project Overview

This project tackles a machine learning regression challenge with multiple advanced techniques and ensemble methods. The project achieved:

- **Rank: 343 out of 518** competitors
- **R² Score: -0.00165**

## Project Structure

### Notebooks
The project includes multiple solution approaches and experiments:

- **`solution_clean.ipynb`** - Clean, production-ready solution
- **`solution_ensemble_ridge_xgb.ipynb`** - Ensemble method combining Ridge and XGBoost
- **`solution_ensemble_seeds.ipynb`** - Ensemble with multiple random seeds
- **`solution_feature_selection.ipynb`** - Feature selection approach
- **`solution_lightgbm_regularized.ipynb`** - LightGBM with regularization
- **`solution_optimized.ipynb`** - Optimized hyperparameters
- **`solution_stacking.ipynb`** - Stacking ensemble approach
- **`solution_target_transform.ipynb`** - Target transformation techniques
- **`solution_top100_optimized.ipynb`** - Top 100 features optimization
- **`diagnostic_ridge_baseline.ipynb`** - Ridge regression baseline with diagnostics
- **`diagnostic.ipynb`** - General diagnostic analysis
- **`solution_one_cell.ipynb`** - Single cell solution
- **`solution_aggressive_regularization.ipynb`** - Aggressive regularization approach
- **`solution.ipynb`** - Main solution notebook

### Submissions
Multiple submission files from different approaches:
- Ridge regression baseline
- Ensemble methods (Ridge + XGBoost)
- Feature selection submissions
- LightGBM regularized submissions
- Stacking and optimization results

## Key Techniques Used

✓ **Regularization**: Ridge regression, aggressive regularization
✓ **Ensemble Methods**: XGBoost, LightGBM, stacking
✓ **Feature Engineering**: Feature selection, top 100 features optimization
✓ **Hyperparameter Tuning**: Multiple optimization strategies
✓ **Target Transformation**: Applied target transformations for improved predictions
✓ **Multiple Random Seeds**: Ensemble with different initializations

## Results

- **Best Rank**: 343 / 518
- **R² Score**: -0.00165
- **Multiple Ensemble Approaches**: Various combinations tested for optimization

## Strategy

See [IMPROVEMENT_STRATEGY.md](IMPROVEMENT_STRATEGY.md) for detailed improvement strategies and analysis.

## Getting Started

### Requirements
- Python 3.x
- Jupyter Notebook
- scikit-learn
- XGBoost
- LightGBM
- pandas
- numpy
- matplotlib
- seaborn

### Installation
```bash
pip install scikit-learn xgboost lightgbm pandas numpy matplotlib seaborn
```

### Running the Solution
```bash
jupyter notebook solution_clean.ipynb
```

## Author
Rakshit Modanwal

## License
MIT
