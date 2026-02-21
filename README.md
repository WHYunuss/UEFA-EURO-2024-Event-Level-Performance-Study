UEFA EURO 2024: Progressive Passers and Carriers Analysis
This repository contains an event-level football analytics project identifying and visualizing the most impactful progressive players at UEFA EURO 2024. Using StatsBomb event data, the study quantifies how players move the ball forward through both passing and carrying.

Project Overview
The analysis provides a granular look at ball progression by moving beyond basic completion percentages. It answers critical tactical questions:

Which players consistently break defensive lines?

Where on the pitch does a team's progression typically originate?

How do player roles differ between pass-dominant playmakers and carry-dominant runners?

The workflow covers the entire data pipeline, including extraction via the StatsBomb API, spatial tagging, minute estimation, and publication-quality visualization.

Technical Methodology
1. Data Acquisition
Data is pulled using the Sbopen helper from the mplsoccer library. The analysis utilizes the standard StatsBomb coordinate system (120 by 80 units) with the opponent goal centered at (120, 40).

2. Progressive Action Definitions
To ensure accuracy, specific spatial logic and Euclidean distance formulas are applied to categorize events:

Progressive Passes

Reduces the distance to the opponent goal by 10 or more units when starting in the own half.

Reduces the distance to the opponent goal by 5 or more units when starting in the opponent half.

Any completed pass ending in the final third (x coordinate 80 or greater).

Progressive Carries

Reduces the distance to the opponent goal by 5 or more units within the opponent half.

Any carry moving the ball 30 or more units forward (long progressive carries).

3. Minute Estimation and Normalization
Since exact playing time is not always provided in event feeds, this project implements a custom estimation logic:

Calculation: Player minutes are derived by subtracting the timestamp of the first recorded event from the last recorded event for each match.

Normalization: Total counts are converted to Per 90 metrics.

Sample Size: A 150 minute minimum filter is applied to all rate-based leaderboards to ensure statistical reliability.

Repository Structure
euros2024.ipynb: Comprehensive Jupyter Notebook containing the full analysis, code, and tactical commentary.

euros2024.py: A streamlined Python script for executing the data pipeline from extraction to visualization.

euro_plots/: Directory containing exported heatmaps and scatter plots.

README.md: Project documentation and methodology overview.

Visualizations and Insights
Origin Heatmaps
Using mplsoccer Pitch modules, the project generates heatmaps of action origins. This identifies whether a player is a Deep-lying Progressor (building from the back) or a Final-third Creator (operating in the pockets).

Archetype Scatter Plot
A dual-axis scatter plot compares Progressive Passes per 90 (x-axis) against Progressive Carries per 90 (y-axis). This categorizes players into distinct tactical profiles:

Pass-Dominant: Elite distributors.

Carry-Dominant: Dynamic wingers or fullbacks.

High-Volume Progressors: Players who excel in both metrics, serving as the primary engines for their teams.

Requirements
The analysis requires Python 3.x and the following libraries:

pandas

numpy

matplotlib

seaborn

mplsoccer
