# Capstone : Modelling the Relationship between Happiness and Religious/Spiritual practices

## Project Structure and Summary

This project explores the key factors associated with self-reported happiness using survey data from a World Value Survey(https://www.worldvaluessurvey.org/WVSDocumentationWV7.jsp) dataset. It includes:

- A Jupyter notebook with comments[Notebook] (https://github.com/msach05/Capstone/blob/main/Capstone_ModellingForHappiness.ipynb)
- The datafile is included in the Data Folder
- A README document summarizing key findings (notebook link included).
- Also added a WORD format for README

---

## How to Run This Notebook

### Environment Setup

To run this notebook locally:

1. **Clone the repository** or download the project files.
2. **Install required dependencies** via pip:

    ```bash
    pip install pandas numpy matplotlib seaborn scikit-learn xgboost
    ```

3. **Launch the Jupyter Notebook**:

    ```bash
    jupyter notebook
    ```

4. Open `Capstone_ModellingForHappiness.ipynb` and run all cells sequentially or click Run-All.

### Data Requirement

- Ensure the dataset file `WVS_Cross-National_Wave_7_csv_v6_0_2.csv` is located in a folder named `Data/` at the root level.
- The notebook assumes the file is unzipped and named exactly as above.

---

## Data Cleaning and Preprocessing

1. **Missing Values:**
   - Replaced common missing value codes (`-1` to `-5`) with `NaN`.
   - Dropped columns with over 20% missing values.
   - Filled remaining missing values using mode imputation.
   - Dropped any rows with remaining `NaN`s to ensure data consistency.

2. **Column Filtering:**
   - Selected only valid "Q" survey question columns- these were the Questions asked in survey.
   - Converted object types to numeric safely.
   - Dropped original columns if a `_reversed` version was created. This was needed to ensure that all survey values 
   are in the same order as Hapiness  (increasing order)

3. **Feature Engineering:**
   - Created reversed versions of specific survey questions to align all scores positively with happiness.
   - Dropped original non-reversed columns after transformation.

---

## Exploratory Data Analysis (EDA)

### Correlation Analysis

- Calculated Pearson correlation of all features with `Q46_reversed` (Hapiness Score - reversed happiness score to ensure higher values = higher happiness)).
- Top correlated features include:
  - `Life Satisfaction` (0.44)
  - `Self-Reported Health (Reversed)` (0.37)
  - `Financial Satisfaction` (0.34)
  - `Freedom of Choice` (0.24)
  - `Feeling of Security` (0.19)

### Visualizations

- **Heatmap** of top 30 features correlated with happiness.
- **Boxplots** and **Histograms** for each top correlated feature vs. happiness score.
---

## Modeling

### Linear Regression

- **R² Score**: 0.286
- **MSE**: 0.352
- Top Features: 
  - `Self-Reported Health`, 
  - `Financial Satisfaction`, 
  - `Freedom of Choice`
  - `Feeling of Security`

### Decision Tree Classifier

- **Accuracy**: 0.86
- Good precision and recall for Happy class, but moderate precision and very low recall for unhappy class.
- Top Features:
  - `Financial Satisfaction`,
  - `Self-Reported Health`
  - `Freedom of Choice`
  - `Trust in Family`

### Logistic Regression

- **Accuracy**: 76.3%
- Excellent precision for “Happy” class, but precision was lower for “Unhappy.”
- Influential features:
  - `Self-Reported Health`, 
  - `Financial Satisfaction`, 
  - `Freedom of Choice`
  - `Marital Status`
  - `Feeling of security `

### K-Nearest Neighbors (KNN)

- **Accuracy**: 86.6%
- Strong performance on happy class, lower recall on unhappy group.

### Ensemble Model (XGBoost + KNN, Soft Voting)

- **Accuracy**: 87.7%
- Best overall performance.
- Balanced precision and recall between happy and unhappy classes.

---

## Summary on Religious and Spiritual Influence on Happiness

Despite the original hypothesis of this project — that religious beliefs, spirituality, or engagement in religious practices might positively impact happiness — the current models **do not indicate a strong or consistent positive correlation between religious/spiritual factors** and happiness.
Instead, health, financial satisfaction, and personal freedom were stronger indicators for happiness. (compared to the hypothesis of religion or spiritual practices)


Variables analyzed included:
- `Importance of God in Life`
- `Religious Self-Identification`
- `Attendance at Religious Services`
- `Frequency of Prayer`
- `Religious Membership`

None of these variables emerged as top predictors of happiness in the current correlation or regression-based analyses. 
- To test whether the effect of religion might be **masked by basic needs**, we **clustered individuals based on health, financial satisfaction, and security** levels.
- **Within each cluster**, we ran separate linear regressions using religious or spiritual features to predict happiness.
---

### Result when looking at stabilizing for Health, Finance and common factors
- The **religion coefficients remained small (0.05 to 0.08)** across all clusters.
- The **R² values were near zero (0.00–0.01)**, indicating that **religion and spirituality still explained virtually none of the variation in happiness**, even among demographically similar groups.
- We further explored religious and spiritual differences across the happy and unhappy groups through visual analysis, but observed minimal variation between them.

### Conclusion:
Despite extensive modeling and controlling for life circumstance variables, this project finds **no strong evidence that religious practices or spirituality is a significant predictor of happiness** in the World Values Survey dataset.

Factors such as:
- **Health**
- **Financial satisfaction**
- **Freedom of choice**
- **Life satisfaction**

consistently emerged as much stronger predictors of happiness.

### Limitations and Future Work

### Limitations

- The dataset is **cross-sectional**, so it captures correlation—not causation.
- All values are **self-reported**, which can introduce bias or inaccuracies.
- **Cultural interpretation** of questions (especially about religion and happiness) may vary, possibly affecting consistency.

### Future Work Possible

- Introduce **interaction terms** (e.g., whether religious effects vary by age, income, or region).
- Explore **model explainability tools** for more insights into model results
- Conduct **country-wise analysis** to observe cultural variation in happiness predictors.

---
