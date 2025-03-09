# Insurance Cost Prediction Project

## Project Overview
This project analyzes medical insurance costs and builds a predictive model to estimate insurance charges based on various patient characteristics. The project includes exploratory data analysis, model development, and a web application for making predictions.

## Overview of the Submission and the Folder Structure
```
mini-telco-churn-app/
├── data/
│   ├── customer_churn.csv
├── model/
│   ├── final1_catboost_model.pkl
├── notebooks
│   ├── EDA.ipynb
├── screenshot
│   ├── churn-app.png
├── SQL
│   ├── capstonedatabase.sql
├── src
│   ├── static/css
│   │     ├── style.css
│   ├── templates
│   │     ├── index.html
│   ├── app.py
│   ├── input_processing.py
│   ├── model.py
├── .gitignore
├── Dockerfile
├── README.md
└── requirements.txt
```
### In the Folder Submitted:
- `data/customer_churn.csv`- Contains the customer churn data exported from the remote SQL database.
- `model/final1_catboost_model.pkl`- Serialized final CatBoost model for deployment.
- `notebooks/EDA.ipynb`- Notebook for Exploratory Data Analysis (EDA), model selection, and serialization.
- `screenshot/churn-app.png`- Screenshot of the working Flask application.
- `SQL/capstonedatabase.sql`- Series of data-join statements to export the remote SQL database.
- `src/static/css/style.css`- CSS file for the Flask application.
- `src/templates/index.html`- HTML working file for the Flask application.
- `src/app.py`- Main Flask application file containing routes and configurations.
- `src/input_processing.py`- Contains code required for preprocessing before model implementation.
- `src/model.py`- Contains code to load the final1_catboost_model.pkl file.
- `.gitignore`- Lists directories to ignore for Git.
- `Dockerfile`- Contains instructions to assemble the Docker image.
- `README.md`- Contains details about the project.
- `requirements.txt`- Lists all the required Python packages and versions for the Flask application.


### Info on final chosen model and parameters
   CatBoost is a an optimised gradient boosting algorithm based on decision tree model that is used to classify categorical features.
   Advantages includes: 
   - Automatic Feature Scaling for numerical variables
   - Robustness to overfitting- with ordered boosting which trains model on one subset of data
   - Parallelism and GPU training allow for increased model training speed and efficiencies done through symmetric decision trees- at all depth levels, the decision nodes have the same feature-split condition.
   - Other benefits of catboost includes the ability to handle categorical variables (through ordered encoding), missing values which can enhance efficiencies and simplify data preparations, while maintaining high predictive performance.
   - <b> Model Parameters </b> After GridSearchCV, the best parameters are as follows: 
'depth': 4, 'iterations': 300, 'learning_rate': 0.05

### Offline AUC metrics of CatBoost
   ##### ROC AUC Score: 0.914 (with 10 features)
   Quantifies the overall performance of model to differentiate the binary classification (churn and no-churn). 
   Higher ROC AUC (Area Under the Receiver Operating Characteristic) score reflects that model is better at differentiating between churn and non churn customers compared to the other models.
   - In the case of the current dataset, it is shown that the database is imbalanced, with a large proportion of data with no-churn values(74%) compared to churn values (26%).
   - The ROC is less affected by class imbalance as it evaluates the models effectiveness of the binary classfication model is based on the True Positive Rate (TPR- Churn) vs the False Positive Rate (FPR- No-churn), at different threshold values, providing a more holistic view of the model's overall performance.
     
   ##### Business Impact
   For TrustTelecom, the industry is highly competitive and every newly acquired customer is more costly than maintaining the existing customers. Hence, it is important that the company reach out to potential 'Churners' before they switch out to other telcos.
   
   The misclassification of a churn customer as no-churn (false negative)- a potential loss of revenue and a non-churn customer as churn (false positive)- unnecessary costs for retention has to be considered and needs to be weighed accordingly by the management. The ROC metric provides a holistic and balanced evaluation of the ability to identify churners (true positives) while minimising false positives, while allowing decision makers to choose the optimal threshold for business needs to increase profitability.

## Setup and Installation

1. Clone the repository
2. Install dependencies:
```bash
pip install -r requirements.txt
```

## Data Description
The dataset includes the following features:
- age: Age of the primary beneficiary
- sex: Gender of the insurance contractor (female/male)
- bmi: Body mass index
- children: Number of children/dependents covered
- smoker: Smoking status (yes/no)
- region: Beneficiary's residential area (northeast, southeast, southwest, northwest)
- charges: Individual medical costs billed by health insurance

## Notebooks
- `research.ipynb`: Contains comprehensive EDA, feature engineering, model selection, and evaluation
- `api_query_example.ipynb`: Demonstrates how to use the prediction API

## Model Development
The project uses various machine learning models to predict insurance costs. Key aspects include:
- Feature engineering and preprocessing
- Model selection and hyperparameter tuning
- Performance evaluation using metrics like MAE, MSE, and R²
