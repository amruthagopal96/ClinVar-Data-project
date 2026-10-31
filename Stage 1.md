### Stage 1: Data exploration — Python (Pandas)

Downloaded and explored genetic variant data from ClinVar in CSV format using Python and the Pandas library. Loaded the dataset into a DataFrame, examined its structure, identified the available columns, and explored the distribution of associated conditions. The original dataset contained 157 expert-panel-reviewed variants, including 137 associated with Hypertrophic Cardiomyopathy (HCM), 19 with Primary Dilated Cardiomyopathy (DCM), and 1 with unspecified cardiomyopathy.
```python
hcm_df = df[df["Condition(s)"] == "Hypertrophic cardiomyopathy"]

print(hcm_df.shape)
```


Filtered the dataset to extract the 137 HCM-associated variants into a separate DataFrame (`hcm_df`). 
