
# Exploratrory Analysis of the Industrial-scale Penicillin Fermentation  Simulation Dataset

INTRODUCTION

The Industrial-scale Penicillin Simulation Version model significantly advances industrial fermentation, aiding in the development of improved control strategies and contributing to research and educational studies.

This dataset is a product of advanced mathematical simulations that emulate the operations of a 100,000-litre penicillin fermentation system, known as IndPenSim. By utilizing cutting-edge computational models, it provides insights into the complexities of large-scale biopharmaceutical production.






## TABLE OF THE CONTENTS
- Objective.
- Data Understanding.
-  Identifying the Batch with Maximun Pencillin Concentarion.
-  Analysing the batch with highest penicillin concentration.
-   Summary
-   Conclusion.
## Citation
1) "The Development of an Industrial-Scale Fed-Batch Fermentation Simulation"

This paper was published in the Journal of Biotechnology, describes the development of a simulation of an industrial-scale fed-batch fermentation process. The simulation was developed using a mechanistic model and was validated using historical data collected from an industrial-scale penicillin fermentation process. The simulation can be used as a benchmark for process systems analysis and control studies.

2) "Modern day monitoring and control challenges outlined on an industrial-scale benchmark fermentation process"

This paper was published in Computers & Chemical Engineering, discusses about the challenges of monitoring and controlling an industrial-scale benchmark fermentation process. The authors identify several challenges, including the need for real-time monitoring of key process variables, the need for effective control strategies, and the need for robust and reliable sensors.

## DATA UNDERSTANDING
In this dataset, we find a multitude of data included in 113,935 rows that provide a thorough examination of inputs and outcomes over 100 different batches. Every batch is carefully recorded at different points in time, resulting in a dynamic log of industrial operations and how they change over time. This large-scale dataset offers a priceless chance to explore the complex interactions between input factors and outputs in a variety of manufacturing scenarios.


## Usage/Examples

```python
#Load data
import numpy as np 
import pandas as pd 
import seaborn as sns
import matplotlib.pyplot as plt

```
dataset =  pd.read_csv('100_Batches_IndPenSim_V3.csv')



