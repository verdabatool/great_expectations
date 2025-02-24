# Great Expectations ~ A Tool for Data Validation

## Introduction

[Great Expectations](https://greatexpectations.io/) (GX) is a powerful open-source tool for validating, documenting, and profiling data. It helps ensure data quality by defining and running expectations on your dataset.

This repository contains a notebook that applies **Great Expectations** to validate a dataset from ride hailing industry by adding multiple data quality checks.

## Expectations Implemented

Below are the **data quality expectations** included in the notebook:

1. **Ensuring `cap_id` is not null**  
   ```python
   suite.add_expectation(
       gx.expectations.ExpectColumnValuesToNotBeNull(column="cap_id")
   )
   ```
   *Ensures that every row has a valid `cap_id`.*

2. **Ensuring `cap_id` is unique**  
   ```python
   suite.add_expectation(
       gx.expectations.ExpectColumnValuesToBeUnique(column="cap_id")
   )
   ```
   *Prevents duplicate values in the `cap_id` column.*

3. **Ensuring available hours trend correctly over time**  
   - `AHs_30D` ≤ `AHs_60D`  
   - `AHs_60D` ≤ `AHs_90D`  
   ```python
   suite.add_expectation(
       gx.expectations.ExpectColumnPairValuesAToBeGreaterThanB(
           column_A="AHs_60D",
           column_B="AHs_30D"
       )
   )
   suite.add_expectation(
       gx.expectations.ExpectColumnPairValuesAToBeGreaterThanB(
           column_A="AHs_90D",
           column_B="AHs_60D"
       )
   )
   ```
   *Ensures that the available hours increase over longer periods.*

4. **Ensuring `age` is greater than 18**  
   ```python
   suite.add_expectation(
       gx.expectations.ExpectColumnValuesToBeBetween(
           column="age",
           min_value=18
       )
   )
   ```
   *Ensures all individuals in the dataset are adults.*

5. **Ensuring the average `age` is greater than 18**  
   ```python
   suite.add_expectation(
       gx.expectations.ExpectColumnMeanToBeBetween(
           column="age",
           min_value=18
       )
   )
   ```
   *Ensures that the overall dataset does not contain too many minors.*

6. **Ensuring `lifetime_trips` is non-negative**  
   ```python
   suite.add_expectation(
       gx.expectations.ExpectColumnValuesToBeBetween(
           column="lifetime_trips",
           min_value=0
       )
   )
   ```
   *Prevents incorrect negative values in the `lifetime_trips` column.*

## How to Use

1. Clone this repository:
   ```bash
   git clone https://github.com/verdabatool/great_expectations
   ```
2. Install Great Expectations (if not installed):
   ```bash
   pip install great-expectations
   ```
3. Run the notebook to validate the dataset and check if it meets the defined expectations.

## Conclusion

Great Expectations helps maintain high-quality datasets by validating key data constraints. This project provides a simple yet effective way to ensure the integrity of any dataset.

Feel free to contribute or suggest improvements!

---
*Maintained by [Verda Batool]*
