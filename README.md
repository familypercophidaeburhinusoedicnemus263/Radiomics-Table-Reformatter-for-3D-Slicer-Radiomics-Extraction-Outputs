# Radiomics Table Reformatter for 3D Slicer Radiomics Extraction Outputs Table
# Slicer Radiomics CSV Reshaper

A small Python utility for batch reorganizing radiomics CSV files exported from **3D Slicer** into a table format that is easier to use for **machine learning** and downstream statistical analysis.

## Overview

Radiomics results exported from 3D Slicer are often stored in individual CSV files, where feature values are arranged vertically.  
For machine learning workflows, however, data are usually expected in a **sample-by-feature** format:

- **one row = one sample**
- **one column = one feature**

This script reads a batch of radiomics CSV files from a folder, extracts a specified column from a specified starting row, and writes the extracted values horizontally into a single output CSV file.

In short, it converts:

- **vertical feature lists in multiple CSV files**
  
into

- **a horizontal feature matrix suitable for model input**

---

## Main Function

For each CSV file in the source folder:

1. Sort files by filename
2. Read the **4th column**
3. Extract values from **row 39 to the end** (using 1-based indexing)
4. Convert the extracted vertical values into **one horizontal row**
5. Write that row into the output file `Radiomics.csv`

### Output rules

- The **first CSV** is written to **row 2**
- The **second CSV** is written to **row 3**
- And so on
- Writing always starts from **column 3**

The script does **not** write filenames by default.

---

## Typical Use Case

This tool is intended for radiomics studies in which:

- radiomics features are extracted in batch from **3D Slicer**
- each case produces one CSV file
- features need to be merged into a single table
- the final table will be used for:
  - machine learning
  - statistical analysis
  - feature selection
  - model development

---

## File Structure Example

```text
└─ slicer_radiomics_csv_reshaper.py
