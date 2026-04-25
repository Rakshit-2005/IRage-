# R² Score Improvement Strategy

## Current Status
- **Ensemble (seeds 42,123,456)**: Test R² = -0.03182 ❌
- **Best so far (Strategy 1)**: Test R² ≈ -0.00182 ⚠️
- **CV R² on ensemble**: 0.214350 ✓
- **Problem**: Massive train-test gap → Overfitting + Distribution Shift

---

## Root Causes Identified

1. **Model Overfitting**: CV score 0.21 vs Test score -0.03 = 0.24 point gap
2. **Engineered Features**: Adding 9 features increased variance/noise
3. **High Model Complexity**: n_estimators=800 might be too aggressive
4. **Insufficient Regularization**: Current lambda=1.0, alpha=0.5 not strong enough
5. **Distribution Shift**: Test data distribution differs from training set

---

## Improvement Roadmap (Priority Order)

### TIER 1: Aggressive Regularization (High Impact)
These should be tested first:

1. **Stronger L1/L2 Regularization**
   - Increase lambda from 1.0 → 5.0-10.0
   - Increase alpha from 0.5 → 2.0-5.0
   - Effect: Reduce overfitting by penalizing model complexity

2. **Reduce Model Complexity**
   - Decrease n_estimators from 800 → 200-300
   - Reduce max_depth from 6 → 4-5
   - Increase min_child_weight from default → 3-5
   - Effect: Simpler models generalize better

3. **Remove Engineered Features** 
   - Go back to original 445 features only (like solution_improved)
   - Engineered features add noise without improving test performance
   - Effect: Reduce feature noise, already ~0.21 CV score with originals

### TIER 2: Ensemble Strategy Refinement
If Tier 1 improves CV→Test gap to <0.05:

4. **Smart Seed Averaging**
   - Use 5-7 different seeds instead of 3
   - Weight models by CV performance (not equal weights)
   - Effect: Better variance reduction

5. **Model Diversity**
   - Mix XGBoost + LightGBM with different hyperparameters
   - Different train/val split strategies
   - Effect: Reduce correlation between ensemble members

### TIER 3: Data & Feature Engineering (If above doesn't help)
Only if structural changes don't work:

6. **Target Scaling/Transformation**
   - Test: log(abs(y)+eps), rank normalization
   - Effect: Might help with skewed target distribution

7. **Feature Selection**
   - Use feature importance to keep only top 200-300 features
   - Effect: Remove noisy, low-signal features

8. **Cross-validation Strategy**
   - Use TimeSeriesSplit instead of KFold (if temporal data)
   - Larger train/val split (0.8/0.2 instead of current)
   - Effect: Better mimic real test distribution

---

## Recommended First Solution to Test

**Combine TIER 1 optimizations:**
```python
xgb_params = {
    'objective': 'reg:squarederror',
    'max_depth': 4,              # DOWN from 6
    'learning_rate': 0.05,
    'subsample': 0.8,            # UP from 0.7
    'colsample_bytree': 0.8,     # UP from 0.7
    'lambda': 10.0,              # UP from 1.0 (L2 regularization)
    'alpha': 5.0,                # UP from 0.5 (L1 regularization)
    'min_child_weight': 3,       # NEW
    'n_estimators': 250,         # DOWN from 800
    'verbosity': 0
}
```

**No engineered features** - use original 445 only

**Expected improvement**: 
- CV R² drops slightly (0.21 → 0.19) ✓ acceptable
- Test R² improves significantly (-0.03 → -0.001 or better) ✓ goal

---

## Testing Protocol

For each solution:
1. Note CV R² score (5-fold average)
2. Note test prediction distribution (mean, std, min, max)
3. Compare with previous best (-0.00182)
4. Stop when test R² becomes positive or plateaus

