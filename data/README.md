# Data Description

## Source

-   **Dataset**: Diabetes 130-US hospitals for years 1999-2008
-   **Source**: UCI Machine Learning Repository / Kaggle
-   **URL**: [<https://www.kaggle.com/datasets/brandao/diabetes>]

## Description

Clinical data from 130 US hospitals over 10 years (1999-2008). Contains information about diabetic patients and their hospital readmission.

## Files

-   `diabetic_data.csv`: Raw dataset (101,766 rows, 50 columns)

## Target Variable

-   `readmitted`: Whether patient was readmitted
    -   `<30`: Readmitted within 30 days
    -   `>30`: Readmitted after 30 days\
    -   `NO`: Not readmitted

## Key Features

-   Patient demographics (age, gender, race)
-   Admission details (type, source, length of stay)
-   Medical diagnoses (primary, secondary, additional)
-   Lab procedures and medications
-   Prior outpatient/inpatient/emergency visits

## Preprocessing Notes

-   Missing values encoded as "?"
-   Need to handle class imbalance
-   Some categorical features have many levels
