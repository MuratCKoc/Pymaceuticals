# Pymaceuticals

This project analyzes and visualizes results from a drug trial with four drug regimens for squamous cell carcinoma in mice.

### Technology Used

- Python
- Jupyter notebooks
- Pandas
- Matplotlib
- NumPy
- SciPy

### Process

- Data were loaded from csvs and converted to dataframes

```python
# Study data files
mouse_metadata_path = "data/Mouse_metadata.csv"
study_results_path = "data/Study_results.csv"

# Read the mouse data and the study results
mouse_metadata = pd.read_csv(mouse_metadata_path)
study_results = pd.read_csv(study_results_path)

# Combine the data into a single dataset
mouse_study = pd.merge(mouse_metadata,study_results, on='Mouse ID')
```

- Some summary statistics were performed

```python
# Using the aggregation method, produce the same summary statistics in a single line
reg2_df = combined_results.groupby(['Drug Regimen'])
tumor_vol_stats = reg2_df['Tumor Volume (mm3)'].agg(['mean','median','std','var','sem'])
```

![Tumor Volume Statistics](/images/tumor_vol_stats.png)

- Tumor volumes were compared across regimens

```python
# Generate a box plot of the final tumor volume of each mouse across four regimens of interest
green_diamond = dict(markerfacecolor='g', marker='D')
fig3, ax3 = plt.subplots()
ax3.set_title('final tumor volume of each mouse')
ax3.boxplot(subset['Tumor Volume (mm3)'], flierprops=green_diamond)
```

![Tumor Volume Comparison](/images/final_tumor_vol.png)

- Other correlations in the data were explored

```python
# Linear Regression Model
# Perform a linear regression onmouse weight vs average tumor volume
ca_slope, ca_int, ca_r, ca_p, ca_std_err = st.linregress(weight_cap.values, capo_ave.values)

# Create equation of line to calculate predicted mouse weight
ca_fit = ca_slope * weight_cap.values + ca_int

```

![Tumov Volume vs Weight](/images/tumorvol_vs_weight.png)
