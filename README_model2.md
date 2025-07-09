# Model 2: Demand-Based Real-Time Parking Price Optimizer

## Overview

Model 2 builds upon the baseline linear pricing of Model 1 by incorporating **demand-sensitive dynamic pricing**.
The model adjusts prices in **real-time** using a combination of:

* Occupancy levels
* Queue lengths
* Traffic conditions nearby
* Special event flags
* Vehicle types

This demand score is then used to scale the price between **\$10 and \$20**, based on current conditions.
All real-time logic is implemented using **Pathway**, and visualized using **Bokeh** in Google Colab.

---

## Tech Stack

* **Python** (Google Colab runtime)
* **Pathway**: real-time stream simulation, transformation
* **Pandas / NumPy**: preprocessing, feature engineering
* **Bokeh**: interactive visualization (heatmaps, line charts, scatter plots)

> All logic coded from scratch (no sklearn, TensorFlow, or external ML libraries)

---

## Architecture Flow

```mermaid
graph TD
    A[Raw Parking CSV] --> B[Create Timestamp Column]
    B --> C[Feature Engineering]
    C --> D[Export Subset as demand_data.csv]
    D --> E[Pathway Stream: replay_csv()]
    E --> F[Demand Score Function]
    F --> G[Clamp Demand Score to 0-1]
    G --> H[Price = 10 * (1 + score)]
    H --> I[Pathway Output Table]
    I --> J[Pandas Conversion for Viz]
    J --> K[Bokeh Visualizations]
```

---

## Demand Score Formula

```
demand_score =
    0.5 * occupancy_rate +
    0.3 * (queue_length / 10) +
    0.2 * traffic_factor +
    0.4 * is_special_day +
    0.1 * vehicle_type_weight
```

Where:

* traffic\_factor = {low: 0.2, medium: 0.5, high: 0.8}
* vehicle\_type\_weight = {car: 1.0, bike: 0.7, truck: 1.3}

Prices are then:

```
price = 10 * (1 + clamp(demand_score, 0, 1))
```

---

## Key Features

* Live stream parsing with timestamped data
* Demand-based pricing logic tied to real-time features
* No price spikes — demand score clamped to 0-1
* Fully explainable score breakdown (weights, logic all visible)
* Vehicle-aware pricing

---

## Visualizations (Bokeh)

* **Hourly Price Heatmap** by lot & time of day
* **Line Chart** of daily price trends (top 5 busiest lots)
* **Scatter Plot** of price vs occupancy rate (color-coded by hour)

All plots include tooltips and interactive legends for visual pricing explanation.

---

## Notebook Sections

1. Data Preprocessing (timestamp, occupancy rate)
2. Stream Setup (Pathway schema, real-time ingestion)
3. Demand Calculation Function
4. Pricing Formula Application
5. Bokeh Visualizations:

   * Heatmap grid
   * Daily line trends
   * Occupancy vs price scatter

---

## Run Instructions

1. Upload `dataset.csv` to Google Colab
2. Run all cells (Pathway + Bokeh will be installed)
3. Interact with visual outputs inline (static rendering)

---

## Notes & Assumptions

* Prices depend on factors like traffic, queue, and special events
* Demand score scaled to avoid volatile pricing
* Bokeh is static in Colab, but reflects real-time logic from Pathway
* Rerouting logic (optional feature) not included here

---

## Status

✅ Complete and tested.
