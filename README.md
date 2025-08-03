Credit Card Default Prediction
    This project focuses on building a machine learning model to predict the probability of a credit card holder defaulting on their payment in the next month. The analysis involves extensive data cleaning, exploratory data analysis (EDA), feature engineering, and hyperparameter tuning to develop a robust classification model.

📊 Dataset
    The project utilizes the default of credit card clients.xls dataset. This dataset contains demographic information, credit limit, historical payment status, and bill statements for credit card clients.

    Key Features:
    
        LIMIT_BAL: Amount of given credit.
        
        SEX, EDUCATION, MARRIAGE, AGE: Client's personal information.
        
        PAY_0 to PAY_6: Repayment status from the last six months.
        
        BILL_AMT1 to BILL_AMT6: Amount of bill statement for the last six months.
        
        default payment next month: The target variable (1 for default, 0 for not default).

⚙️ Methodology
    The analysis follows a structured machine learning workflow:
    
    Data Cleaning:
    
        The initial dataset had an incorrect header row, which was fixed by promoting the first data row to be the column headers.
        
        All columns were converted to a numeric data type to facilitate calculations.
        
        The non-informative ID column was dropped.
    
    Exploratory Data Analysis (EDA) & Feature Engineering:
    
        Histograms were plotted for all features to understand their distributions.
        
        The LIMIT_BAL feature was found to be highly skewed. A log transformation (np.log) was applied to normalize its distribution, creating a new LIMIT_BAL_log feature. The original LIMIT_BAL column was then dropped.
        
        Boxplots were generated to visually inspect for outliers across all features.
    
    Outlier Treatment:
    
        Outliers can significantly impact model performance. They were handled by capping the values using the Interquartile Range (IQR) method. Any data point outside the range of Q1−1.5×IQR and Q3+1.5×IQR was replaced with the corresponding boundary value.
    
    Feature Scaling:
    
        The features were standardized using sklearn.preprocessing.StandardScaler. This ensures all features have a mean of 0 and a standard deviation of 1, which is crucial for many machine learning algorithms.

🤖 Modeling and Hyperparameter Tuning
    Model: A Random Forest Classifier was selected for its robustness and ability to handle complex interactions between features.
    
    Hyperparameter Tuning:
    
        The optimal number of trees (n_estimators) in the forest was determined by training multiple models with n_estimators ranging from 1 to 600 (in steps of 10).
        
        The F1-score for both the training and testing sets was plotted against the number of estimators. The optimal value was found to be 210, as it provided a good balance between bias and variance.
    
    Train-Test Split: The data was split into 80% for training and 20% for testing.

📈 Evaluation
    The final Random Forest model was trained with n_estimators=210, criterion='entropy', and max_depth=7. The performance on the test set is summarized below:
    
    Classification Report (Test Set):
        | | precision | recall | f1-score | support |
        | :--- | :--- | :--- | :--- | :--- |
        | 0 (No Default)| 0.88 | 0.82 | 0.85 | 4687 |
        | 1 (Default) | 0.48 | 0.60 | 0.53 | 1313 |
        | Accuracy | | | 0.77 | 6000 |
        | Macro Avg | 0.68 | 0.71 | 0.69 | 6000 |
        | Weighted Avg| 0.79 | 0.77 | 0.78 | 6000 |

    The model achieved an F1-score of 0.53 for the positive class (default), indicating a reasonable ability to identify clients who are likely to default.

🚀 How to Use
To replicate this analysis:

    Ensure you have Python and the following libraries installed:
    
        pandas
        
        numpy
        
        matplotlib
        
        seaborn
        
        scikit-learn
    
    Place the default of credit card clients.xls file in the same directory.
