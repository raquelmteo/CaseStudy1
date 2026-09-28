# Case Study I - Telecom Billing Configuration

## Project Overview

This project challenges teams to predict the correct billing configuration for a telecommunications customer from the services recorded in the CRM system.

The project is completed by teams of **5 or 6 students**. Each team must appoint a **team leader**. The team leader is responsible for defining the project activities and assigning team members to tasks in Microsoft Planner.

The project lasts **3 weeks** and is divided into three sprints:

1. **Sprint 1 - Pre-processing**
2. **Sprint 2 - Modeling**
3. **Sprint 3 - Optimization and Explainability**

Each team must present its completed activities and results at the end of every week. The notebook for each sprint must be submitted through Moodle.

## Schedule and Grading

| Sprint | Topic | Weight | Submission deadline |
|---|---|---:|---|
| 1 | Pre-processing | 40% | 22/09/2026 at 23:59 |
| 2 | Modeling | 30% | 29/09/2026 at 23:59 |
| 3 | Optimization and Explainability | 30% | 06/10/2026 at 23:59 |

The final grade is calculated as:

$$
\text{Final grade} = 0.40S_1 + 0.30S_2 + 0.30S_3
$$

## Problem Definition

Telecommunications operators must provision the services subscribed to by each customer and bill those services correctly. A 4-Play subscription can involve Internet, television, mobile phone, and fixed-line services, with information distributed across several systems:

- **CRM:** master record of the offers and services subscribed to by the customer.
- **TV platform:** determines the television channels available to the customer.
- **Internet platform:** determines the customer's Internet speed.
- **Billing system:** determines how services and usage are billed.

Because these systems contain many options and possible combinations, provisioning errors can occur through human or automated processes. The objective of this competition is to learn the relationship between CRM and Billing configurations and predict the correct Billing configuration for each customer.

The relationship is not necessarily one-to-one: multiple CRM configurations may correspond to the same Billing configuration, and the training data may contain inconsistent CRM-Billing pairs.

## Dataset Description

All configuration fields have been pre-processed into binary variables:

- `0` means that an option is inactive.
- `1` means that an option is active.

### Training data

The training data contains one row per customer and includes:

- 1 customer identifier column: `MSISDN`.
- 745 CRM input columns, whose names start with `CRM`.
- 731 Billing target columns, whose names start with `BIL`.

The model receives the CRM configuration and must predict all 731 Billing labels.

### Test data

The test data contains:

- 1 encrypted customer identifier column: `MSISDN`.
- 745 CRM input columns.

Billing labels are not provided for the test data. The predicted labels must be written in the required submission format.

### Files in this workspace

- `train.csv`: labeled training data.
- `test.csv`: test CRM configurations.
- `solution.csv`: available solution/submission reference file.
- `cleaned_telecom_data.csv`: cleaned data generated during Sprint 1.
- `first_sprint.ipynb`: Sprint 1 preprocessing notebook.

## Characteristics and Challenges

- The dataset contains provisioning errors, so the same CRM configuration may appear with different Billing configurations.
- The output space is high-dimensional, with 731 binary target variables.
- Several CRM configurations may map to the same Billing configuration.
- Individual CRM variables may not have a direct one-to-one correspondence with individual Billing variables.
- Exact prediction of the complete Billing vector is required for a sample to count as correct.

## Evaluation Metric

Submissions are evaluated with the **Exact Matching Ratio (EMR)**:

$$
\mathrm{EMR} = \frac{1}{n}\sum_{i=1}^{n} I(Y_i = Z_i)
$$

where:

- $n$ is the number of samples.
- $Y_i \in \{0,1\}^{k}$ is the true Billing label vector.
- $Z_i \in \{0,1\}^{k}$ is the predicted Billing label vector.
- $k = 731$ is the number of Billing labels.
- $I(Y_i = Z_i)$ equals 1 only when every Billing label for sample $i$ is correct, and 0 otherwise.

A perfect score, `EMR = 1`, requires every one of the 731 labels to be correct for every sample.

## Sprint Requirements

### Sprint 1 - Pre-processing

- Inspect the structure and quality of the training and test data.
- Identify the customer ID, CRM input columns, and Billing target columns.
- Verify binary values, missing values, duplicate IDs, and schema consistency.
- Detect CRM configurations associated with conflicting Billing configurations.
- Define and document a reproducible strategy for resolving inconsistent training examples.
- Remove or justify constant features where appropriate.
- Export the cleaned dataset and document assumptions and limitations.

### Sprint 2 - Modeling

- Build a reproducible baseline model.
- Use a validation strategy suitable for high-dimensional multi-label prediction.
- Evaluate models using EMR and, where useful, supporting metrics.
- Compare at least two modeling approaches or meaningful baseline variations.
- Prevent data leakage during preprocessing and validation.
- Generate a valid prediction file with the required customer identifier and Billing columns.

### Sprint 3 - Optimization and Explainability

- Improve the selected model or prediction pipeline.
- Compare every improvement against the frozen Sprint 2 baseline.
- Investigate errors, especially incorrect complete Billing vectors.
- Explain the most important input features and model decisions where possible.
- Document limitations, trade-offs, and reproducibility instructions.
- Produce the final prediction file and final project conclusions.

## Expected Deliverables

For each sprint, submit the corresponding notebook on Moodle and present the completed work and results to the class. Each notebook should include:

- The objective and scope of the sprint.
- The methodology and important implementation decisions.
- Reproducible code and relevant outputs.
- Evaluation results and interpretation.
- Limitations, assumptions, and next steps.

The final project should provide a reproducible pipeline from CRM input data to predicted Billing configuration.

## Team Organization

The team leader should create and maintain the project plan in Microsoft Planner. Suggested activities include:

- Data inspection and quality checks.
- Preprocessing and conflict analysis.
- Baseline modeling.
- Model comparison and validation.
- Optimization and error analysis.
- Explainability and documentation.
- Notebook integration, submission preparation, and presentation.

All team members should have clearly assigned responsibilities and contribute evidence of their work to the relevant sprint notebook.