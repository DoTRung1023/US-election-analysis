# US Election Analysis and Prediction

## Overview

This project analyzes US election data to predict voting behavior in the 2016 presidential election. The analysis compares multiple machine learning models to identify the most effective approach for predicting voter preferences and determines the most influential variables in voting decisions.

**Author:** Hai Trung Do (a1899443)  
**Course:** Data Taming and Prediction  
**Institution:** University of Adelaide  
**Date:** October 2024

## Project Structure

```
US-election-analysis/
├── README.md                    # This file
├── project.Rmd                  # Main R Markdown analysis file
├── election.csv                 # Raw dataset (22,735 observations, 18 variables)
├── DTP_Report_Tasksheet.pdf     # Project requirements and task sheet
└── project.pdf                  # Generated report (when knitted)
```

## Dataset

The dataset contains **22,735 observations** with **18 variables** related to voter demographics and behavior:

### Key Variables Used in Analysis:
- `voted_2016`: Target variable (democrat/republican)
- `voted_2012`: Previous voting behavior (democrat/republican)
- `state`: State of residence
- `student_loan`: Student education loan status (yes/no)
- `faminc`: Family income (21 categories, reduced to 4)
- `child_u18`: Has child under 18 (yes/no)
- `followed_event_fb`: Follows political events on Facebook (yes/no)
- `education`: Education level (no_highschool/highschool/undergraduate/postgraduate)
- `employment`: Employment status
- `marital_status`: Marital status
- `home_owner_status`: Home ownership status (own/rent/other)
- `health_insurance`: Government health insurance (yes/no)

### Variables Removed:
- `ballot_ID`: Unique identifier (no predictive value)
- `vote_method`: Voting method (not relevant to choice prediction)
- `social_media`: Recent social media usage (unreliable predictor)
- `birth_year`: Only contained missing values
- `county`: Too granular (replaced by state)

## Methodology

### 1. Data Preprocessing
- **Missing Data Removal**: Eliminated observations with missing values
- **Variable Selection**: Removed non-predictive variables
- **Category Merging**: Simplified family income from 21 to 4 meaningful categories:
  - Level 1: < $40,000
  - Level 2: $40,000 - $69,999
  - Level 3: $70,000 - $119,999
  - Level 4: $120,000+
- **Balanced Sampling**: Created sample of 3,000 observations (1,500 Democrat, 1,500 Republican)

### 2. Exploratory Data Analysis
- Analyzed relationships between voting behavior and key demographics
- Examined consistency between 2012 and 2016 voting patterns
- Investigated impact of student loans and education on voting preferences

### 3. Model Development
Three machine learning models were developed and compared:

#### **Logistic Regression**
- Provides interpretable coefficients
- Baseline model for classification

#### **K-Nearest Neighbors (KNN)**
- Tuned parameter: `k` (number of neighbors)
- Best k: 100 neighbors

#### **Random Forest**
- Tuned parameters: `mtry` (features per split), `min_n` (minimum samples per leaf)
- 100 trees with permutation importance
- Best parameters: mtry = 9, min_n = 30

### 4. Model Evaluation
Models were evaluated using:
- **10-fold cross-validation**
- **Accuracy**: Proportion of correct predictions
- **ROC AUC**: Area under the receiver operating characteristic curve
- **Brier Score**: Measures quality of probabilistic predictions

## Key Results

### Model Performance Comparison

| Model | Accuracy | ROC AUC | Brier Score |
|-------|----------|---------|-------------|
| **Logistic Regression** | **0.906** | **0.934** | **0.081** |
| Random Forest | 0.906 | 0.931 | 0.084 |
| K-Nearest Neighbors | 0.800 | 0.892 | 0.164 |

**Winner: Logistic Regression** - Best overall performance across all metrics

### Most Important Predictors

1. **`voted_2012` (Republican)** - By far the most important predictor
2. **Education (Undergraduate)** - Secondary predictor
3. **Family Income ($120,000+)** - Tertiary predictor

### Key Findings

- **Vote Consistency**: 88-92% of voters cast the same vote in 2016 as they did in 2012
- **Student Loans**: Voters with student loans were more likely to vote Democrat
- **Education**: Higher education levels correlate with Democratic voting
- **Income**: Higher income brackets show varied patterns across party lines

## Technical Requirements

### R Packages Required:
```r
install.packages(c(
  "tidyverse",    # Data manipulation and visualization
  "skimr",        # Data summary statistics
  "dplyr",        # Data manipulation
  "rsample",      # Data splitting and resampling
  "recipes",      # Data preprocessing
  "tidymodels",   # Machine learning framework
  "kknn",         # K-nearest neighbors
  "rpart.plot",   # Decision tree plotting
  "vip",          # Variable importance plots
  "doParallel"    # Parallel processing
))
```

### Alternative Installation (using pacman):
```r
pacman::p_load(tidyverse, skimr, dplyr, rsample, recipes, 
               tidymodels, kknn, rpart.plot, vip)
```

## Running the Analysis

1. **Clone or download** this repository
2. **Install required packages** (see above)
3. **Update file path** in the R Markdown file:
   - Line 253: Update the path to `election.csv` to match your local directory
4. **Open and run** `project.Rmd` in RStudio
5. **Knit to PDF** to generate the complete report

### Note on File Paths
The current path in the R Markdown file is:
```r
election <- read_csv("/Users/dotrung67/Documents/Adelaide/Ade sem 2 2024/Data taming and prediction/Project/election.csv")
```

**Update this path** to match your local directory structure.

## Business Implications

### For Policy and Opinion Organization:

1. **Recommended Model**: Use logistic regression for predicting 2016 voting behavior
2. **Key Insight**: Previous voting behavior (2012) is the strongest predictor
3. **Secondary Factors**: Consider education level and income when past voting data unavailable
4. **Limitation**: Heavy reliance on past voting may not capture changing political preferences

### Strategic Recommendations:

- **Primary Strategy**: Leverage historical voting patterns when available
- **Secondary Strategy**: Focus on education and income demographics for new voters
- **Caution**: Monitor for political shifts that may reduce historical pattern reliability
- **Enhancement**: Combine with real-time polling for improved accuracy

## Limitations and Considerations

1. **Sample Size**: Analysis uses 3,000 observations from 22,735 total (13% sample)
2. **Temporal Scope**: Model trained on 2012-2016 data may not generalize to future elections
3. **Overfitting Risk**: Heavy reliance on 2012 voting patterns
4. **Missing Variables**: Some potentially important factors not captured in dataset
5. **Generalizability**: Results may not apply to significantly different political contexts

## Future Work

- Expand sample size to include full dataset
- Incorporate additional demographic variables
- Test model performance on subsequent elections (2020, 2024)
- Develop ensemble methods combining multiple models
- Add temporal analysis of changing voter preferences

## Contact

**Hai Trung Do**  
Student ID: a1899443  
University of Adelaide  
Data Taming and Prediction Course  

---

*This project demonstrates comprehensive data science methodology including data preprocessing, exploratory analysis, model development, evaluation, and interpretation for political science applications.*