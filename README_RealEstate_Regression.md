# 🏠 Real Estate Price Prediction — Multiple Linear Regression

**Course:** MBA Business Data Analytics — Final Exam  
**Tools:** R · ggplot2 · caret · lm() · AIC · RMSE  
**Dataset:** RealEstateValue (house age, transit distance, convenience stores, lat/long)

---

## Business Problem

What drives the price-per-square-foot of a home? Can we build a model that identifies the most statistically meaningful predictors and accurately forecasts value?

---

## What I Did

**1. Exploratory Analysis**  
Plotted each independent variable against `PricePerSQFT` to detect linear vs. polynomial relationships. Found `HouseAge` showed a parabolic pattern — mid-age homes commanded a premium over very new or very old properties.

**2. Correlation Screening**  
Built a full correlation matrix. Identified multicollinearity concerns:
- `ToTransitStation` ↔ `Longitude`: r = −0.79 (strongest)
- `ToTransitStation` ↔ `NumConvenienceStores`: r = −0.59

**3. Model Building**  
- Full model with polynomial term: `PricePerSQFT ~ HouseAge + HouseAge² + ToTransitStation + NumConvenienceStores + Latitude + Longitude`
- Applied **backward elimination** (one variable at a time)
- Evaluated each step with RMSE, `anova()` F-test, and AIC

**4. Model Comparison**

| Model | Adj. R² | RMSE | ANOVA p-value | AIC |
|---|---|---|---|---|
| Full model | 0.5863 | 76.91 | — | ~3371.7 |
| Reduced (−Longitude) | 0.5877 | 75.99 | 0.81 (NS) | 3371.7 |

**5. Assumption Diagnostics**  
Ran full residual diagnostics: Residuals vs Fitted, Normal Q-Q, Scale-Location, Cook's Distance.

---

## Key Finding

Removing `Longitude` improved RMSE (76.91 → 75.99) without a statistically significant loss of fit (ANOVA p = 0.81). The reduced model with `HouseAge²`, `ToTransitStation`, `NumConvenienceStores`, and `Latitude` is the recommended model.

---

## Files

| File | Description |
|---|---|
| `Moralesb-Final_Exam.Rmd` | Full regression analysis notebook |
| `Final_Exam_Appendix_BMorales.Rmd` | Additional diagnostics and logistic regression companion |

---

## Skills Demonstrated

`lm()` · `glm()` · Polynomial regression · Backward elimination · Multicollinearity detection · `anova()` · `AIC()` · RMSE · Residual diagnostics · `ggplot2` · `caret` train/test split
