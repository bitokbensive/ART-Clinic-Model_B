# ART Clinic – Model B
### Machine Learning for Identifying Probable ART Care Interruption

<p align="center">
  <a href="https://art-clinic-modelb-kpsxb7xdppeymbzebne9ft.streamlit.app/">
    <img src="https://img.shields.io/badge/Live%20Demo-Streamlit-red?logo=streamlit" alt="Live Demo"/>
  </a>
  <img src="https://img.shields.io/badge/Python-3.11-blue?logo=python" alt="Python"/>
  <img src="https://img.shields.io/badge/Model-Logistic%20Regression-orange" alt="Model"/>
  <img src="https://img.shields.io/badge/Status-Research%20Prototype-yellow" alt="Research Prototype"/>
</p>

<p align="center">
  <strong>Turning routine HIV clinical data into insights for improved continuity of care.</strong>
</p>

## Live Application

**Try the deployed application:**

[ART Clinic – Model B: Open Streamlit App](https://art-clinic-modelb-kpsxb7xdppeymbzebne9ft.streamlit.app/)

## 1. About the Project

ART Clinic – Model B is a machine learning research prototype developed to explore the use of routine HIV clinical data in identifying patients with **probable antiretroviral therapy (ART) care interruption**.

The project was developed using routine clinical records from Partners for Health and Development in Africa (PHDA), Kariobangi SWOP Site, Nairobi, Kenya.

It uses a logistic regression model to estimate the likelihood of probable ART care interruption based on demographic, enrollment, and ART-related characteristics.

The broader objective is to explore how predictive analytics can support healthcare workers in identifying patients who may benefit from additional follow-up.

## 2. System Workflow

The ART Clinic – Model B application follows a machine learning workflow that transforms patient characteristics into estimated probabilities of probable ART care interruption.

```mermaid
flowchart TD
    A[Patient Characteristics] --> B[Data Preprocessing]
    B --> C[Candidate B Logistic Regression]
    C --> D[Predicted Probability]
    D --> E[Human Review and Follow-up Consideration]

    A1[Demographic Variables] --> A
    A2[Enrollment Variables] --> A
    A3[ART-related Variables] --> A

    B1[Missing Value Imputation] --> B
    B2[Scaling and Encoding] --> B


## 3. Problem Statement

Maintaining continuity of HIV care is essential for effective ART service delivery. However, identifying patients who may have disengaged from care can be challenging when healthcare facilities rely on routine clinical records.

This project investigates whether machine learning can identify patterns in routinely collected data that may support patient follow-up and continuity of care.

## 4. Project Objectives

- Prepare and integrate routine HIV clinical datasets.
- Define an operational outcome for probable ART care interruption.
- Explore demographic, enrollment, and ART-related predictors.
- Develop and compare candidate machine learning models.
- Evaluate the selected model using cross-validation and out-of-fold predictions.
- Develop a Streamlit prototype demonstrating predictive analytics in HIV service delivery.

## 5. Dataset Description

Two routine clinical datasets were used:

| Dataset | Records / Variables |
|---|---|
| All Patients | 1,438 unique patient identifiers; 121 variables |
| Active ART Patients Line List | 1,040 unique records; 59 variables |
| Final analytical cohort | 1,341 patients |

The datasets were linked using the randomly assigned patient identifiers.

### Outcome Definition

Probable ART care interruption was operationally defined as:

- Absence from the August 2026 Active ART Patients Line List.
- At least 180 days since the last documented ART visit.
- Exclusion of documented transfers out and deaths.

The final analytical cohort consisted of:

- 289 probable ART care interruption cases (21.5%).
- 1,052 active controls (78.5%).

**Data privacy:** Original patient-level clinical datasets are not included in this public repository because of confidentiality and data-protection considerations.

## 6. Machine Learning Approach

Several candidate model specifications were investigated. Candidate B was selected as the cautious research prototype.

### Selected Model: Candidate B

Logistic Regression using nine predictors:

1. Age at ART initiation
2. ART start year
3. Gender
4. Population type
5. Key population type
6. Enrollment type
7. Starting ART regimen
8. Starting ART regimen line
9. Baseline WHO stage

Candidate B excludes baseline CD4 and CD4 missingness as predictors.

### Data Preprocessing

The modelling pipeline incorporated:

- Median imputation for numerical variables.
- Most-frequent imputation for categorical variables.
- Standardisation of numerical features.
- One-hot encoding of categorical variables.
- Stratified five-fold cross-validation.

Preprocessing was fitted within training folds to minimise information leakage.

## 7. Model Performance

Candidate B was evaluated using out-of-fold predictions.

| Evaluation Metric | Result |
|---|---:|
| Out-of-fold ROC-AUC | **0.8251** |
| Out-of-fold PR-AUC (Average Precision) | **0.6512** |
| Brier Score | **0.1156** |
| Mean CV ROC-AUC | 0.8303 |
| Standard Deviation | 0.0351 |

These results indicate promising internal predictive discrimination. Further calibration assessment and independent validation are necessary before considering practical clinical use.

## 8. Model Artifacts and Deployment

The trained Candidate B logistic regression pipeline and its associated metadata are stored in the repository's `model/` directory.

### Saved Model Files

| File | Description |
|---|---|
| Candidate B `.joblib` file | Serialised machine learning pipeline used by the Streamlit application. |
| Candidate B metadata `.json` file | Stores accompanying model information and metadata. |

The saved Joblib artifact allows the application to load the previously trained pipeline without retraining the model whenever a user accesses the application.

### Application Deployment

The application is built using Streamlit and deployed through Streamlit Community Cloud.

**Live application:** [ART Clinic – Model B](https://art-clinic-modelb-kpsxb7xdppeymbzebne9ft.streamlit.app/)

The main application entry point is `main.py`, while Python dependencies are specified in `requirements.txt`.

### Local Execution

To run the application locally:

```bash
git clone https://github.com/bitokbensive/ART-Clinic-Model_B.git

cd ART-Clinic-Model_B

pip install -r requirements.txt

streamlit run main.py
```

**Note:** The saved model artifact must remain in its expected directory so that the application can locate and load it successfully.

## 9. Technology Stack

- Python 3.11
- Pandas
- NumPy
- Scikit-learn
- Matplotlib
- Seaborn
- Streamlit

## 10. Repository Structure

ART-Clinic-Model_B/
│
├── model/
│   ├── ART_interruption_logistic_model_candidate_B.joblib
│   └── ART_interruption_model_candidate_B_metadata.json
│
├── main.py
├── requirements.txt
├── runtime.txt
├── .gitignore
└── README.md

## 11. Running the Application Locally

### Step 1: Clone the repository

```bash
git clone https://github.com/bitokbensive/ART-Clinic-Model_B.git
```

### Step 2: Navigate to the project directory

```bash
cd ART-Clinic-Model_B
```

### Step 3: Create a virtual environment

```bash
python -m venv venv
```

Activate it:

**Windows:**
```bash
venv\Scripts\activate
```

**Linux/macOS:**
```bash
source venv/bin/activate
```

### Step 4: Install dependencies

```bash
pip install -r requirements.txt
```

### Step 5: Run the Streamlit application

```bash
streamlit run main.py
```

The application should then be accessible through the local URL displayed in your terminal.

## 12. Limitations and Future Improvements

The current implementation is a research prototype and has not undergone independent clinical validation.

Future improvements include:

- Independent temporal or external validation.
- Further probability calibration assessment.
- Subgroup performance and fairness analysis.
- Improved documentation of patient transfers and clinical outcomes.
- Threshold selection based on healthcare follow-up capacity.
- Evaluation of usability and potential impact in clinical workflows.
- Stronger privacy and data governance safeguards.

## 13. Ethical Considerations

HIV-related health information is sensitive and must be handled responsibly.

Any future application should prioritise patient confidentiality, secure data storage, access control, transparency, fairness, and human oversight.

The model is intended to support research and potential decision-support workflows. It must not replace healthcare professionals or independently determine patient-care decisions.

## 14. Acknowledgements

I acknowledge Partners for Health and Development in Africa (PHDA), Kariobangi SWOP Site, the ENGAGE Programme, and the mentors, supervisors, healthcare workers, and data management team who supported this project.

## 15. Author

**Bensive Bitok**

Data Science | Artificial Intelligence | Machine Learning | Database Administration | Public Health Analytics

GitHub: [@bitokbensive](https://github.com/bitokbensive)


*Developed as a public health data science and machine learning research project at Partners for Health Development in Africa (PHDA) - Kariobangi SWOP Site, Nairobi, Kenya.*

**Disclaimer:** This application is a research prototype and is not intended for clinical diagnosis, treatment decisions, or automated patient classification.
