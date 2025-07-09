# Dynamic Parking Price Optimizer

## Overview

This project implements **Model 1: Baseline Linear Pricing Model** as part of the capstone project for the CACIITG course.
It dynamically adjusts parking prices in **real time** using **Pathway** to simulate streaming data and **Bokeh** for interactive visualizations.

The pricing is calculated per parking lot based on occupancy and capacity, starting from a base price of \$10 and increasing linearly. The entire logic is coded from scratch using **only Pandas, NumPy, and Pathway** as required by the rules.

> Note: This is Model 1 of a multi-model project. Model 2 (advanced pricing logic) is included separately.

---

## 🔧 Tech Stack

* **Python** (Google Colab environment)
* **Pathway** for real-time stream simulation and transformation
* **Pandas** for preprocessing
* **NumPy** for numerical operations
* **Bokeh** for interactive data visualizations

> All logic implemented from scratch as per constraints (no sklearn, no external ML libraries)

---

## 🛠️ Architecture Flow

```mermaid
graph TD
    A[Raw CSV Dataset] --> B[Preprocessing in Pandas]
    B --> C[Create Timestamp]
    C --> D[Sort Chronologically]
    D --> E[Save Stream Subset to parking_stream.csv]
    E --> F[Pathway - Schema + Data Streaming]
    F --> G[Pathway Logic: Parse Timestamp]
    G --> H[Calculate Price: 10 + alpha * (Occupancy / Capacity)]
    H --> I[Pathway Output Table]
    I --> J[Pandas Conversion for Visualization]
    J --> K[Bokeh Graphs]
```

---

## 💡 Pricing Logic

* Base price: \$10

* Linear price increase with occupancy:

  $\text{Price} = 10 + \alpha \cdot \left(\frac{\text{Occupancy}}{\text{Capacity}}\right)$

* `\alpha` is a tunable parameter (default = 0.5)

---

## Key Features

* Real-time stream simulation of CSV data using `Pathway.demo.replay_csv`
* Chronological integrity of timestamps preserved
* Multiple Bokeh visualizations including:

  * Real-time pricing line plots
  * Hourly price trends per lot
  * Competitor price boxplots
  * Summary bar chart of hourly avg across all lots

---

## Notebook Sections

1. **Data Preparation:** Timestamp formatting, sorting
2. **Pathway Stream Setup:** Schema, stream ingest, date parsing
3. **Model 1 Logic:** Price = 10 + α \* (Occupancy / Capacity)
4. **Static Visualizations (Bokeh):**

   * Line plots
   * Box plots for competitor comparison
   * Hourly average plots per lot and across all lots

---

## Example Outputs

* [x] Real-time pricing output from Pathway table
* [x] Hour-wise pricing trends per parking lot
* [x] Summary bar chart of hourly average prices
* [x] Visual comparison of prices across lots at peak hours

---

## Run Instructions

1. Upload `dataset.csv` to Google Colab
2. Run all cells (Pathway + Bokeh get installed in the first cell)
3. Visual outputs will appear inline (or in new tabs if Bokeh doesn't render inline)

---

## Author Notes

* Model 1 is kept deliberately simple (as per instructions)
* Additional assumptions and improvements are handled in **Model 2**
* Real-time visualisation in Colab has limitations; Bokeh plots are static snapshots of streaming logic

---

## Status

✅ Completed and tested
