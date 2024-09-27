
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
```
#shape of the dataset
dataset.shape
```

# Load data
import numpy as np 
import pandas as pd 
import seaborn as sns
import matplotlib.pyplot as plt




dataset =  pd.read_csv('100_Batches_IndPenSim_V3.csv')


dataset

#shape of the dataset
dataset.shape

#utilising data in 33 columns for EDA
df = dataset.iloc[:, :33]

#info of dataset
df.info()

# Identifying the Batch with Maximun Pencillin Concentarion

Identification of Batch Start and Batch End points

Comparison of Batch End Results

Finding the batch with Best Penicillin Concentration

for i in df.columns:
    print(i, ":", df[i].nunique())
    print('-'*80)

# Find the indices of the batch start indices i.e., 0.2 time interval
batch_start_indices = df['Time (h)'].index[df['Time (h)'] == 0.2]

# Print the indices of the batch_start_indices
batch_start_indices

def find_batch_end_indices(df):
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

#results of batches will be in the end indices 
results_df = df.iloc[batch_end_indices]
results_df

#descriptive statistics of batch end data of all batches
results_df.describe().T

**Observation:**

Time (h): The time intervals range from 167 hours to 290 hours, with an average time of approximately 227.87 hours.

Aeration rate (Fg:L/h): The aeration rate ranges from 60 to 75 L/h, with an average rate of approximately 65.35 L/h.

Agitator RPM (RPM:RPM): The agitator RPM is constant at 100 RPM for all batches.

Sugar feed rate (Fs:L/h): The sugar feed rate varies from 20 to 150 L/h, with an average rate of approximately 81.80 L/h.

Acid flow rate (Fa:L/h): The acid flow rate ranges from 0 to 4.15 L/h, with an average rate of approximately 0.16 L/h.

Base flow rate (Fb:L/h): The base flow rate varies from 0 to 200.30 L/h, with an average rate of approximately 37.79 L/h.

Heating/Cooling Water Flow Rate (Fc:L/h): The heating/cooling water flow rate ranges from 0.0001 to 281.71 L/h, with an average rate of approximately 47.04 L/h.

Heating Water Flow Rate (Fh:L/h): The heating water flow rate varies from 0.0001 to 444.28 L/h, with an average rate of approximately 42.47 L/h.

Water for Injection/Dilution (Fw:L/h): The water for injection/dilution ranges from 0 to 400 L/h, with an average rate of 224 L/h.

Air Head Pressure (pressure:bar): The air head pressure is constant at 0.9 bar for all batches.

Dumped Broth Flow (Fremoved:L/h): The dumped broth flow ranges from -4000 to 0 L/h, with an average of -400 L/h.

Substrate Concentration (S:g/L): The substrate concentration varies from 0.0011 to 115.27 g/L, with an average of approximately 19.39 g/L.

Dissolved Oxygen Concentration (DO2:mg/L): The dissolved oxygen concentration ranges from 8.87 to 14.77 mg/L, with an average of approximately 12.72 mg/L.

Penicillin Concentration (P:g/L): The penicillin concentration varies from 3.16 to 36.16 g/L, with an average of approximately 24.01 g/L.

Vessel Volume (V:L): The vessel volume ranges from 60331 to 89990 liters, with an average of approximately 76053.54 liters.

Vessel Weight (Wt:Kg): The vessel weight varies from 68469 to 99491 kg, with an average of approximately 84995.10 kg.

pH (pH:pH): The pH values range from 6.47 to 6.68, with an average pH of approximately 6.51.

Temperature (T:K): The temperature ranges from 297.43 to 298.99 K, with an average of approximately 297.97 K.

Generated Heat (Q:kJ): The generated heat varies from 4.03 to 833.80 kJ, with an average of approximately 257.78 kJ.

Carbon Dioxide Percent in Off-Gas (CO2outgas:%): The carbon dioxide percentage in off-gas ranges from 0.64% to 2.06%, with an average of approximately 1.45%.

PAA Flow (Fpaa:L/h): The PAA flow ranges from 3.66 to 15 L/h, with an average of approximately 6.58 L/h.

PAA Concentration Offline (PAA_offline:PAA (g L^{-1})): The PAA concentration varies from 393.1 to 11524 g/L, with an average of approximately 3358.13 g/L.

Oil Flow (Foil:L/hr): The oil flow is constant at 23 L/hr for all batches.

NH3 Concentration Off-line (NH3_offline:NH3 (g L^{-1})): The NH3 concentration ranges from 1590.6 to 5170 g/L, with an average of approximately 2571.96 g/L.

Oxygen Uptake Rate (OUR:(g min^{-1})): The oxygen uptake rate varies from 0.0447 to 1.7044 g/min, with an average of approximately 0.94 g/min.

Oxygen in Percent in Off-Gas (O2:O2 (%)): The oxygen percentage in off-gas ranges from 0.1863% to 0.2035%, with an average of approximately

0.1942%.

Offline Penicillin Concentration (P_offline:P(g L^{-1})): The offline penicillin concentration varies from 3.17 to 36.18 g/L, with an average of approximately 24.03 g/L.

Offline Biomass Concentration (X_offline:X(g L^{-1})): The offline biomass concentration ranges from 10.76 to 25.27 g/L, with an average of approximately 20.80 g/L.

Carbon Evolution Rate (CER:g/h): The carbon evolution rate varies from 0.49 to 1.71 g/h, with an average of approximately 1.21 g/h.

Ammonia Shots (NH3_shots:kgs): The ammonia shots are constant at 0 kgs for all batches.

Viscosity (Viscosity_offline:centPoise): The viscosity ranges from 53.75 to 117.93 centipoise, with an average of approximately 71.06 centipoise.

Fault Reference (Fault_ref:Fault ref): The fault reference indicates two values, 0 and 1, with an average of 0.01, suggesting occasional faults.

0 - Recipe driven 1 - Operator controlled (Control_ref:Control ref): The control reference indicates two values, 0 and 1, suggesting a mix of recipe-driven and operator-controlled batches.

The dataset's maximum Offline Penicillin Concentration (P_offline:P(g L^{-1})) reaching 36.18 g/L indicates a significant achievement in the batch process. To gain deeper insights, we will conduct an in-depth analysis of the control parameters and conditions that contributed to this exceptional output. Understanding the factors that led to such high penicillin concentration is crucial for process optimization and quality improvement in industrial-scale fermentations.

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


# Find the start and end indices of Batch 29
batch_number = 29

if 1 <= batch_number <= len(batch_indices):
    batch_29_start, batch_29_end = batch_indices[batch_number - 1]
    print(f"Start Index of Batch 29: {batch_29_start}")
    print(f"End Index of Batch 29: {batch_29_end}")
else:
    print("Batch 29 is out of range.")

batch_29_df = df.loc[31725:33174]
batch_29_df

# Analysing the batch with highest penicillin concentration

batch_29_df.describe().T

# Create a 6x6 grid of subplots
fig, axes = plt.subplots(7, 5, figsize=(18, 18))
fig.subplots_adjust(hspace=0.5, wspace=0.5)

# Flatten the axes array for easy iteration
axes = axes.ravel()

# Plot histograms for each variable in batch_29_df
for i, var in enumerate(batch_29_df.columns):
    ax = axes[i]
    ax.hist(batch_29_df[var], bins=20, edgecolor='k')
    ax.set_title(var)
    ax.grid(True)

# Remove empty subplots
for i in range(len(batch_29_df.columns), 35):
    fig.delaxes(axes[i])

plt.tight_layout()
plt.show()

**Observation**

Based on the distributions for the variables in the data, here are some observations and insights:

Time (h): The average time is approximately 145 hours, with a standard deviation of around 83.74 hours. The minimum time is 0.2 hours and the maximum is 290 hours. The median time is also 145.1 hours, indicating a symmetric distribution.

Aeration rate (Fg:L/h): The average aeration rate is around 64.63 L/h with a standard deviation of 10.4 L/h. The minimum and maximum aeration rates are 30 L/h and 75 L/h respectively. The median aeration rate is 65 L/h.

Agitator RPM (RPM:RPM): The agitator RPM is constant at 100 RPM throughout the batch production.

Sugar feed rate (Fs:L/h): Sugar feed rates exhibit a normal distribution, with a mean of 77.29 L/h and a standard deviation of 21.19 L/h, indicating some variability in sugar feed.

Acid flow rate (Fa:L/h): The acid flow rate is highly skewed to the right, with a mean of 0.0082 L/h and a standard deviation of 0.0990 L/h. This suggests that most of the time, the acid flow rate is very low, but there are occasional high outliers.

Base flow rate (Fb:L/h): Base flow rates follow a normal distribution, with a mean of 47.76 L/h and a standard deviation of 24.47 L/h, indicating moderate variability.

Heating/cooling water flow rate (Fc:L/h): The flow rate of heating/cooling water is skewed to the right, with a mean of 86.04 L/h and a standard deviation of 119.43 L/h, suggesting occasional high flow rates.

Heating water flow rate (Fh:L/h): Heating water flow rates also exhibit right-skewness, with a mean of 21.36 L/h and a standard deviation of 45.54 L/h, indicating occasional high values.

Water for injection/dilution (Fw:L/h): The flow rate for water injection/dilution is skewed to the right, with a mean of 148.28 L/h and a standard deviation of 146.55 L/h, suggesting occasional high flow rates.

Air head pressure (pressure:bar): Air head pressure varies from 0.6 to 1.1 bar, with an average of approximately 0.94 bar.

Dumped broth flow (Fremoved:L/h): The dumped broth flow is skewed to the left, with a mean of -248.28 L/h and a standard deviation of 965.46 L/h. This indicates that most of the time, the flow is zero, but there are occasional negative values.

Substrate concentration (S:g/L): Substrate concentrations are right-skewed, with a mean of 0.049 g/L and a standard deviation of 0.253 g/L, suggesting occasional high concentrations.

Dissolved oxygen concentration (DO2:mg/L): Dissolved oxygen concentrations are normally distributed, with a mean of 11.42 mg/L and a standard deviation of 1.49 mg/L, indicating relatively consistent oxygen levels.

Penicillin concentration (P:g/L): Penicillin concentrations vary widely, from 0.0009 g/L to 36.183 g/L, with an average of approximately 21.84 g/L.

Vessel Volume (V:L): Vessel volume is normally distributed, with a mean of 70,940.77 L and a standard deviation of 6,902.15 L, indicating consistent volume levels.

Vessel Weight (Wt:Kg): Vessel weight follows a normal distribution, with a mean of 79,315.91 kg and a standard deviation of 8,191.75 kg, suggesting relatively stable weight values.

pH (pH:pH): pH values are normally distributed, with a mean of 6.50 and a standard deviation of 0.02, indicating that pH levels are fairly consistent.

Temperature (T:K): Temperature data follows a normal distribution, with a mean of 298.03 K and a standard deviation of 0.18 K, suggesting relatively stable temperature conditions.

Generated heat (Q:kJ): Generated heat is right-skewed, with a mean of 296.94 kJ and a standard deviation of 53.53 kJ, indicating occasional high values.

carbon dioxide percent in off-gas (CO2outgas:%): Carbon dioxide percent in the off-gas follows a normal distribution, with a mean of 1.46% and a standard deviation of 0.40%, indicating relatively stable levels.

PAA flow (Fpaa:PAA flow (L/h)): PAA flow with a mean of 6.84 L/h and a standard deviation of 3.70 L/h, indicating consistent flow rates.

PAA concentration offline (PAA_offline:PAA (g L^{-1})): The PAA concentration offline with a mean of 1080.52 g/L and a standard deviation of 360.31 g/L, suggesting occasional lower concentrations.

Oil flow (Foil:L/hr): Oil flow with a mean of 25.63 L/hr and a standard deviation of 4.60 L/hr, indicating relatively stable flow rates.

NH_3 concentration off-line (NH3_offline:NH3 (g L^{-1})): NH_3 concentration offline with a mean of 1808.82 g/L and a standard deviation of 177.11 g/L, suggesting occasional lower concentrations.

Oxygen Uptake Rate (OUR:(g min^{-1})): Oxygen uptake rates are normally distributed, with a mean of 1.34 g/min and a standard deviation of 0.33 g/min, indicating consistent oxygen uptake.

Oxygen in percent in off-gas (O2:O2 (%)): Oxygen percentages in the off-gas are normally distributed, with a mean of 0.19% and a standard deviation of 0.003%, indicating relatively stable oxygen levels.

Offline Penicillin concentration (P_offline:P(g L^{-1})): The offline penicillin concentration is with a mean of 22.05 g/L and a standard deviation of 13.36 g/L, suggesting occasional lower concentrations.

Offline Biomass concentration (X_offline:X(g L^{-1})): Offline biomass concentration with a mean of 20.54 g/L and a standard deviation of 6.84 g/L, indicating consistent levels.

Carbon evolution rate (CER:g/h): Carbon evolution rates with a mean of 1.25 g/h and a standard deviation of 0.42 g/h, suggesting consistent carbon evolution.

Ammonia shots (NH3_shots:kgs): Ammonia shots are constant, with a mean and standard deviation of 0, indicating no variation.

Viscosity (Viscosity_offline:centPoise): Viscosity is left-skewed, with a mean of 57.80 centPoise and a standard deviation of 25.36 centPoise, suggesting occasional higher viscosity values.

Fault reference (Fault_ref:Fault ref): Fault reference is constant, with a mean and standard deviation of 0, indicating no variation.

0 - Recipe driven 1 - Operator controlled (Control_ref:Control ref): The variable value is 0, indicating that this batch is recipe drive

# Observation on Penicillin Concentration

# Plot the Penicillin Concentration (P:g/L) for Batch 29
plt.figure(figsize=(12, 6))
plt.plot(batch_29_df['Time (h)'], batch_29_df['Penicillin concentration(P:g/L)'], label='Penicillin Concentration (P:g/L)')
plt.xlabel('Time (h)')
plt.ylabel('Penicillin Concentration (P:g/L)')
plt.title('Penicillin Concentration (P:g/L) vs Time (h)')
plt.legend()
plt.grid(True)
plt.show()

![image](https://github.com/user-attachments/assets/19a0d91a-0bbc-48ad-afd1-f8ba27074a82)



