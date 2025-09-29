# 🍺 Fuzzy Matching for Beer Database Deduplication

## Overview

This project addresses a common data quality challenge: identifying **duplicate** or **highly similar** entries within a large dataset, specifically a database of beers. Due to variations in naming conventions, spelling mistakes, or different formatting used by data entry personnel, exact string matching is often insufficient.

This solution employs **Fuzzy Logic** and **Fuzzy Matching** techniques to quantify the degree of similarity between beer records (names, breweries, styles, etc.). This allows for the robust identification and subsequent consolidation of near-duplicate entries, ensuring a clean and reliable dataset.

-----

## Key Features & Technologies

  * **Fuzzy Logic Implementation:** Utilized the `scikit-fuzzy` library for foundational fuzzy set operations.
  * **Deduplication:** A systematic approach to find and flag highly similar beer records, preparing the data for cleaning.
  * **Custom Membership Functions:** Defined **Triangular Membership Functions (`trimf`)** for **Low**, **Medium**, and **High** similarity degrees, allowing the system to handle similarity scores not just as a binary (duplicate/not duplicate) but as a spectrum.
  * **Data Analysis & Visualization:** Used **Pandas** for data manipulation and **Matplotlib** for visualizing the defined fuzzy membership functions.

-----

## Methodology

The project follows a pipeline designed for non-exact data matching:

1.  **Data Loading and Inspection:** The beer dataset, including fields like `Name`, `Style`, `Brewery`, `ABV`, and `IBU`, is loaded and explored using Pandas.
2.  **Similarity Metric Calculation (Implied Step):** A suitable metric (e.g., Levenshtein distance, Jaccard similarity, or an attribute-weighted score) is calculated between pairs of beer entries to generate a "raw" similarity percentage.
3.  **Fuzzy System Design:**
      * **Input Variable:** The calculated raw similarity score (e.g., 0% to 100%).
      * **Fuzzy Sets:** Triangular membership functions (`trimf`) are defined over the similarity domain (0-100) to create fuzzy sets: **Low**, **Medium**, and **High**.
      * **Fuzzy Inference:** The raw similarity score is mapped onto these fuzzy sets, determining its degree of membership in each (e.g., a 75% similarity score might have a high degree of membership in the "Medium" set and a lower degree in the "High" set).
4.  **Duplicate Identification:** Records with a high degree of membership in the **"High" similarity** set are flagged as likely duplicates, requiring further manual review or automated merging.

-----
