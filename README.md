
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

---
utilising data in 33 columns for EDA
df = dataset.iloc[:, :33]
----
#info of dataset
         df.info()
---
 Find the indices of the batch start indices i.e., 0.2 time interval
batch_start_indices = df['Time (h)'].index[df['Time (h)'] == 0.2]
-----

# Print the indices of the batch_start_indices
batch_start_indices
----
ef find_batch_end_indices(df):
    """Finds the indices of the rows in the DataFrame where the `Time (h)` column is equal to 0.2 time interval.

  Args:
    df: A Pandas DataFrame.

  Returns:
    A Pandas Series containing the indices of the rows in the DataFrame where the `Time (h)` column is equal to 0.2.
  """
    # Find the indices where 'Time (h)' is equal to 0.2
    indices_0_2 = df[df['Time (h)'] == 0.2].index
    
    # Calculate the indices immediately before 0.2
    indices_before_0_2 = indices_0_2 - 1
    
    # Filter out negative indices (those before the start of the DataFrame)
    indices_before_0_2_filtered = indices_before_0_2[indices_before_0_2 > 0]
    
    # Create a mask for filtered indices greater than 0
    indices_before_0_2_filtered_mask = indices_before_0_2_filtered > 0
    
    # Return the filtered indices, which represent the batch end indices
    return indices_before_0_2_filtered[indices_before_0_2_filtered_mask]

# Call the function and copy the DataFrame
batch_end_indices = find_batch_end_indices(df.copy())

# Append the last index to represent the end of the final batch
batch_end_indices = batch_end_indices.append(pd.Index([df.index[-1]]))

# Print the indices of the batch_end_indices
print(batch_end_indices)
----
#results of batches will be in the end indices 
results_df = df.iloc[batch_end_indices]
results_df
-----
#descriptive statistics of batch end data of all batches
results_df.describe().T
----
# Create an empty list to store batch-wise indices
batch_indices = []

# Initialize variables to track the start and end of a batch
batch_start = batch_start_indices[0]
for batch_end in batch_end_indices:
    # Append the indices for the current batch to the list
    batch_indices.append((batch_start, batch_end))
    # Update the start of the next batch
    batch_start = batch_end + 1

# Find the batch where 'Offline Penicillin concentration (P_offline:P(g L^{-1}))' is 36.18 maximum
target_concentration = 36.18
target_batch = None

for i, (start, end) in enumerate(batch_indices):
    batch_data = df[start:end+1]
    if target_concentration in batch_data['Offline Penicillin concentration(P_offline:P(g L^{-1}))'].values:
        target_batch = i + 1  # Batch numbers start from 1

print(f'Batch with Offline Penicillin concentration {target_concentration} is Batch {target_batch}')
--------
# Find the start and end indices of Batch 29
batch_number = 29

if 1 <= batch_number <= len(batch_indices):
    batch_29_start, batch_29_end = batch_indices[batch_number - 1]
    print(f"Start Index of Batch 29: {batch_29_start}")
    print(f"End Index of Batch 29: {batch_29_end}")
else:
    print("Batch 29 is out of range.")
----
batch_29_df = df.loc[31725:33174]
batch_29_df
----
# Plot the Penicillin Concentration (P:g/L) for Batch 29
plt.figure(figsize=(12, 6))
plt.plot(batch_29_df['Time (h)'], batch_29_df['Penicillin concentration(P:g/L)'], label='Penicillin Concentration (P:g/L)')
plt.xlabel('Time (h)')
plt.ylabel('Penicillin Concentration (P:g/L)')
plt.title('Penicillin Concentration (P:g/L) vs Time (h)')
plt.legend()
plt.grid(True)
plt.show()
---

