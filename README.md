# Bootstrap Analysis - Bag of Little Bootstrap

## Overview
This project applies Bootstrap regression techniques to evaluate the stability and reliability of predictive models. We employ both standard Bootstrap methods and the Bag of Little Bootstraps (BLB) for computational efficiency in large datasets and perform a comparative analysis to assess each method's predictive performance.

<img src="https://github.com/rohitkulkarni08/enhancing-predictive-modeling-using-bootstrapping/blob/584e4a44a82d9deaa7666d05d503acbf2af77b22/images/Methology.png" width="650" height="600">

## Why Use Bootstrap?
Bootstrap methods are used to understand the variability of sample estimates by resampling with replacement from an estimate and assessing the variance of the estimator. The BLB approach further enhances this by providing a scalable way to obtain quality uncertainty measures with parallel computation.

## Bag of Little Bootstraps (BLB)

### Overview of BLB
The Bag of Little Bootstraps (BLB) is a modern statistical technique designed to provide robust uncertainty estimates for large-scale data sets. It was developed as an adaptation of the traditional Bootstrap method to overcome computational inefficiencies when dealing with massive data. The key idea behind BLB is to apply resampling techniques on smaller subsets of the data, which are then scaled up to estimate the properties of the entire dataset.

### How BLB Works
1. **Subsampling**: BLB starts by drawing multiple smaller, random subsamples from the original large dataset. These subsamples are much smaller than the full dataset, making them manageable for intensive computations.
2. **Resampling**: For each subsample, the BLB performs several bootstrap resampling processes. This means generating many bootstrapped datasets from each subsample by sampling with replacement.
3. **Scaling**: Estimates from each resampled dataset are then appropriately scaled to infer the statistics of the full dataset.
4. **Aggregation**: Finally, the results from all bootstrapped subsamples are aggregated to produce a single estimation.

### Advantages of Using BLB
- **Efficiency**: BLB is computationally more efficient than the standard Bootstrap because it handles smaller subsets of the data.
- **Scalability**: It is well-suited for parallel processing environments, where each subsample bootstrap can be processed independently.
- **Accuracy**: Despite using smaller subsets, BLB can provide accuracy similar to that of using the full dataset, especially in large data contexts.

## Implementation Details
The implementation involves several key steps:
- **Data Preprocessing**: Handling missing values, encoding categorical variables, and normalizing numerical features.
- **Model Training**: Using machine learning models (both regression and classification) within a bootstrap framework.
- **Evaluation**: Assessing model performance through regression and classification metrics

### Bootstrap Configuration
- **Iterations**: In this project, we perform 10,000 iterations for the bootstrap analysis. This high number of iterations helps to ensure the stability and reliability of our statistical estimates, reducing variability and providing a more accurate approximation of the underlying distribution.
- **Resample Size (`resample_size=100`)**: This parameter represents the number of samples drawn in each subsample. A size of 100 is chosen to balance computational efficiency with sample diversity, allowing for a representative subset of the entire dataset while keeping computational demands manageable.
- **Number of Subsamples (`num_subsamples=30`)**: We use thirty subsamples in our BLB approach. This number of subsamples significantly increases the robustness of our estimates by allowing us to assess variability across a broader section of the data. It provides a comprehensive view of the model’s performance under various sample conditions and enhances the overall reliability of the uncertainty estimates.

These parameters are chosen to optimize the trade-off between computational cost and the accuracy of the model's performance metrics.

## Comparative Analysis
The comparative analysis between BLB and the standard Bootstrap methods is conducted to evaluate their respective strengths and limitations in the context of regression and classification tasks. By comparing these two methodologies, we aim to:
- **Highlight Efficiency Differences**: Understand how BLB, designed for large datasets, performs in terms of computational efficiency compared to the more traditional and computationally intensive standard Bootstrap.
- **Assess Accuracy and Robustness**: Determine which method provides more accurate and robust estimates of model performance, particularly in the presence of data variability and model assumptions.
- **Guide Methodological Choices**: Provide empirical evidence that can help practitioners make informed decisions about which bootstrap method to use based on their specific needs, dataset characteristics, and computational resources.

## Regression

### Dataset

The [dataset](https://www.kaggle.com/datasets/rishikeshkonapure/zomato/) provides detailed information about restaurants listed on Zomato -  an online food ordering application based out of India, is useful for analyzing food habits and restaurant preferences. 

Key details include:

- **Restaurant Info**: Name, address, location, and contact details.
- **Services**: Online ordering and table booking availability.
- **Customer Ratings and Reviews**: Insights into customer satisfaction and popularity.
- **Cuisines**: Types of cuisines offered.
- **Categories**: Tags like ‘Cafes’, ‘Delivery’, ‘Dine-out’, etc.
- **Costs**: Average cost for two, reflecting price range and affordability (This is our target variable)

### Models

1. **Linear Regression**
2. **Ridge Regression** (Alpha = 1.0)
3. **Random Forest Regression**

### Results

The results are summarized in the following table, which details the confidence interval width, coverage probability, bias, and mean squared error (MSE) for each model and method:

| Model               | Method               | CI Width   | Coverage | Bias     | MSE     |
|---------------------|----------------------|------------|----------|----------|---------|
| Linear Regression   | BLB                  | 2.18       | 0.960    | 0.00013  | 0.678   |
| Linear Regression   | Standard Bootstrap   | 0.05       | 0.052    | -0.00001 | 0.157   |
| Ridge Regression    | BLB                  | 1.79       | 0.960    | 0.00006  | 0.422   |
| Ridge Regression    | Standard Bootstrap   | 0.039      | 0.039    | 0.00002  | 0.162   |
| Random Forest       | BLB                  | 1.91       | 0.958    | -0.00002 | 0.520   |
| Random Forest       | Standard Bootstrap   | 0.173      | 0.227    | -0.00039 | 0.088   |


<img src="https://github.com/rohitkulkarni08/enhancing-predictive-modeling-using-bootstrapping/blob/584e4a44a82d9deaa7666d05d503acbf2af77b22/images/Regression-output.png" width="600" height="400">

### Inferences

- **BLB Method**: Generally offers wider confidence intervals and better coverage, indicating more reliable uncertainty measures.
- **Standard Bootstrap**: Shows tighter confidence intervals but significantly lower coverage, suggesting underestimation of variance.
- **Bias**: Minimal across all methods, indicating that the estimators are consistent.
- **MSE**: Varies between models and methods, with the BLB method typically exhibiting higher MSE due to the wider confidence intervals.

## Classification

### Dataset

The [dataset](https://www.kaggle.com/datasets/bhrt97/hr-analytics-classification/) contains data about various employees who are candidates for promotion. It features several attributes related to their performance and personal information which can be used to predict potential promotions.

Key details include:

- **Personal Info**: Employee ID, Gender, Age, and education.
- **Employment Details**: Department, Region, Recruitment Channel, and Length of Service.
- **Performance Metrics**: Training, Performance Rating, KPIs Met >80%, Awards Won, Average Training Score.
- **Promotion Status**: This is our target variable

### Models

1. **Logistic Regression**
2. **Random Forest Classification**
3. **Gradient Boosting Classification**

### Results

Results detail the confidence interval width, coverage probability, accuracy, recall, F1 score, and ROC AUC for each model and bootstrap method:

| Model                          | Method               | CI Width | Coverage | Accuracy | Recall | F1 Score | ROC AUC |
|--------------------------------|----------------------|----------|----------|----------|--------|----------|---------|
| Logistic Regression            | BLB                  | 0.898    | 0.951    | 0.814    | 0.865  | 0.449    | 0.912   |
| Logistic Regression            | Standard Bootstrap   | 0.045    | 0.061    | 0.720    | 0.719  | 0.305    | 0.807   |
| Random Forest Classification   | BLB                  | 0.845    | 0.974    | 1.000    | 1.000  | 1.000    | 1.000   |
| Random Forest Classification   | Standard Bootstrap   | 0.182    | 0.084    | 0.973    | 0.743  | 0.827    | 0.977   |
| Gradient Boosting Classification | BLB                | 0.966    | 0.956    | 1.000    | 1.000  | 1.000    | 1.000   |
| Gradient Boosting Classification | Standard Bootstrap | 0.108    | 0.078    | 0.737    | 0.895  | 0.367    | 0.892   |


<img src="https://github.com/rohitkulkarni08/enhancing-predictive-modeling-using-bootstrapping/blob/584e4a44a82d9deaa7666d05d503acbf2af77b22/images/Classification-output.png" width="600" height="400">

### Inferences

- **BLB Method**: Shows higher coverage and often better performance metrics, indicating reliable uncertainty measures and robustness.
- **Standard Bootstrap**: Exhibits narrower confidence intervals but lower coverage, suggesting potential underestimation of variability.

## Conclusion
The application of BLB improves uncertainty estimation in large-scale datasets without compromising on computational efficiency. This project illustrates the importance of choosing the right Bootstrap method according to the analysis needs and computational resources.
