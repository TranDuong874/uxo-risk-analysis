# UXO Contamination Risk and Clearance Priority in Vietnam

**Trần Thái Dương**
**Module: Visual Data Analytics - INT3137 1**

## Overview

During the Vietnam War (1955–1975), the U.S. dropped approximately 7.5 million tons of bombs. Decades later, over 800,000 tons of unexploded ordnance (UXO) remain across Vietnam, contaminating about 18.7% of its land. This report analyzes UXO risk at national (ADM0), provincial (ADM1), district (ADM2), and 10 km² grid levels. Using historical bombing data, terrain, population, and clearance records, the report identifies high-risk areas and proposes a prioritization framework for UXO clearance.

## Contents

1. [Introduction](#introduction)
2. [Research Questions](#research-questions)
3. [Data Sources and Processing](#data-sources-and-processing)
4. [U.S. Bombing Data](#us-bombing-data)
5. [Risk Assessment Model](#risk-assessment-model)
6. [Clearance Priority Strategy](#clearance-priority-strategy)
7. [Conclusion](#conclusion)

---

## Introduction

UXO affects lives, infrastructure, and development. This project aims to assess UXO contamination risk and suggest clearance priorities based on actionable data analytics.

---

## Research Questions

1. **Which areas are at risk of UXO contamination?**
   Risk levels will be derived from bombing data, weapon types, dud rates, and geographic density.

2. **Which areas should be prioritized for clearance?**
   Priority will be evaluated using risk levels, population, terrain, and feasibility factors.

---

## Data Sources and Processing

| Dataset            | Description                           | Source             |
| ------------------ | ------------------------------------- | ------------------ |
| THOR               | Bombing operations during Vietnam War | U.S. DoD           |
| QTMAC              | UXO reports and clearance activities  | Quảng Trị Province |
| Vietnam Population | Provincial/district demographics      | GSO, 2023          |
| Admin Boundaries   | Geospatial ADM0/1/2 boundaries        | GeoBoundaries      |
| Land Use           | Satellite land cover (2020)           | JAXA               |
| Dud Rates          | Weapon failure rates                  | Multiple sources   |

The data pipeline includes cleaning mission records, filtering for Vietnam-based operations, assigning UXO risk, and mapping to different spatial scales.

---

## U.S. Bombing Data

* **Data Files**: operations.csv (main), weapon.csv, aircraft.csv
* **Cleaning Process**: Dropped missions without coordinates and filtered operations to include only those in or near Vietnam.
* **Key Insights**:

  * Most kinetic missions with high UXO risk were between 1965-1973.
  * Non-kinetic missions (support, refueling) were excluded.

---

## Risk Assessment Model

### Hierarchical Levels

* **Level 3**: 10 km² grid
* **Level 2**: ADM2 (District)
* **Level 1**: ADM1 (Province/City)

### Key Metrics

| Metric          | Description                                        |
| --------------- | -------------------------------------------------- |
| Weapon Density  | Weapons per km²                                    |
| Estimated UXO   | Derived from weapon count × dud rate               |
| Composite Score | Combines UXO, mission density, and weapon severity |

### Classification

* Composite scores were normalized and grouped into 6 quantiles (Low to Extreme risk).
* Risk levels were aggregated to ADM2 and ADM1 using weighted averages and majority voting.
* A "hotspot" flag was set for provinces with ≥25% high/extreme risk areas.

---

## Clearance Priority Strategy

### Supplementary Data

* **Population**: Higher population = higher urgency
* **Terrain**: Urban, agricultural prioritized over forest/wetlands

### Budget Model

* Clearance cost estimate: \$109,000/km²
* Prioritization considered contamination, human impact, and feasibility

### Priority Score Formula

**Priority Score = W × Xnorm** where:

* Xnorm = normalized metrics
* W = weights derived from observed demining strategies

### Example Weights

| Metric                 | Weight           |
| ---------------------- | ---------------- |
| Estimated UXO          | 5.0              |
| Population             | 5.0              |
| Area                   | -2.0             |
| Is Hotspot             | 3.0              |
| Residence              | 2.5              |
| Agricultural           | 1.5              |
| Forest, Wetland, Shrub | Negative weights |
| Developed Urban        | -10.0            |

These weights reflect observed demining patterns (QTMAC, VNMAC).

---

## Conclusion

This analysis combines bombing records with terrain, demographic, and UXO clearance data to estimate contamination risk and inform demining priorities. The resulting multi-level risk and priority models provide a foundation for data-driven UXO mitigation policies.

**Key Insight**: Quảng Trị, Quảng Bình, and Quảng Nam provinces show the highest UXO risk. Applying the proposed model helps identify other urgent areas like Vĩnh Long once the highest-risk zones have been addressed.

---

## Notes

* Data cleaning and spatial filtering were essential due to gaps in coordinate and mission data.
* Composite scores and quantile binning provided balanced and interpretable classifications.
* Future work could integrate ground-truth clearance data and community feedback to refine models.
