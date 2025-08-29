Let's Go Game Analysis

--Project Overview
This project analyzes gameplay data from the "Let's Go" mobile game to evaluate player retention and engagement during an A/B test involving two different gate placements (gate_30 and gate_40). The goal is to understand how gate placement impacts player retention at Day 1 and Day 7 post-installation and overall gameplay behavior.

--Dataset Description
The dataset contains data from 90,189 players randomly assigned to either gate_30 (control) or gate_40 (test) groups. Key fields include:

1.userid: Unique player identifier

2.version: A/B test group (gate_30 or gate_40)

3.sum_gamerounds: Number of game rounds played in the first 14 days

4.retention_1: Player returned on Day 1 (True/False)

5.retention_7: Player returned on Day 7 (True/False)

--How to Run the Analysis
1. Load Required Packages
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import numpy as np

%matplotlib inline

import sys
import warnings
if not sys.warnoptions:
    warnings.simplefilter("ignore")
```
2. Load the Dataset
python
```df = pd.read_csv(r"Path/To/Lets'Go.csv")
print(df.shape)  # Should print (90189, 5)
```
3. Inspect Basic Data Structure
python
```
print(df.head())
print(df.info())
print(df.describe())
5. Check Group Distribution (Sanity Check)
python
print(df['version'].value_counts())
```
6. Calculate Retention Rates by Group
python
```
retention_summary = df.groupby('version').agg({
    'retention_1': 'mean',
    'retention_7': 'mean',
    'sum_gamerounds': 'mean'
}).reset_index()

print(retention_summary)
```
6. Visualize Retention Rates
python
```
sns.barplot(data=retention_summary.melt(id_vars='version', value_vars=['retention_1', 'retention_7']),
            x='version', y='value', hue='variable')
plt.title('Retention Rates by Gate Placement')
plt.ylabel('Retention Rate')
plt.show()
```
Key Findings

Player counts are balanced between gate_30 and gate_40 groups.

Day 1 retention rates are nearly identical for both groups (~44.5%).

Day 7 retention shows a slight edge for gate_30 (~19% vs. ~18% in gate_40).

Average gameplay rounds are comparable across groups, around 51-52 rounds.

The retention funnel displays significant drop-off from Day 1 to Day 7.
