# UEFA EURO 2024: Progressive Passers and Carriers Analysis

## Overview

This project delivers an event-level analysis of ball progression during UEFA EURO 2024. Using raw coordinate data, the study identifies players who most effectively advanced the ball toward the opponent’s goal through completed passes and carries.  

The workflow reflects a professional data analyst approach — moving from data extraction and spatial engineering to normalization and visualization — to generate actionable tactical insights.

---

## Dataset

**Source:** StatsBomb Open Data via Sbopen  
**Pitch Dimensions:** 120 x 80 units (goal centered at 120, 40)

**Key Fields Utilized:**

- `player_name`, `team_name`
- `type` (Pass or Carry)
- `location` (x, y start coordinates)
- `pass_end_location` (x, y end coordinates)
- `timestamp` (minute, second, and period for playing time estimation)

---

## Workflow Summary

### 1. Data Load and Engineering
- Extracted match and event-level data for the entire EURO 2024 tournament.
- Calculated Euclidean distances from ball coordinates to the center of the opponent goal.
- Derived absolute match minutes to estimate total playing time per player.

### 2. Progressive Event Tagging
Progression was defined using spatial logic to ensure tactical relevance:

- **Progressive Passes:** Tagged if the pass reduced distance to goal by:
  - 10+ units in own half  
  - 5+ units in opponent half  
  - or ended inside the final third (`x >= 80`)
- **Progressive Carries:** Tagged if the carry reduced distance to goal by:
  - 5+ units in opponent half  
  - or moved the ball 30+ units vertically

### 3. Aggregation and Normalization
- Aggregated raw totals for progressive actions by player and team.
- Normalized statistics to a **Per 90 minutes** basis for fair comparison between starters and substitutes.
- Applied a **150-minute playing time filter** to remove small-sample outliers.

### 4. Visual Analysis
- Created origin heatmaps (12 x 8 bins) to visualize where progressive actions were initiated.
- Developed scatter plots comparing passing vs. carrying volume to categorize player archetypes:
  - *Progressive Engines*  
  - *Deep-lying Playmakers*  

---

## SQL / Data Techniques Used

- Spatial engineering with Euclidean distance calculations
- Conditional tagging using logical thresholds
- Aggregation (`SUM`, `COUNT`) and normalization (per 90 minutes)
- Filtering for sample-size robustness
- Visualization with heatmaps and scatter plots

---

## Repository Structure
uefa-euro-2024-progressive-analysis/
│
├── data/
│   └── euro2024_events.csv
│
├── notebooks/
│   └── progressive_passes_carries.ipynb
│
├── visuals/
│   ├── heatmaps/
│   └── scatterplots/
│
├── README.md


