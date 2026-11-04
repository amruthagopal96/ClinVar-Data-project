## Import HCM variants into SQLite
we have:
-	hcm_df — a Pandas DataFrame.
-	137 rows — each representing an HCM-associated genetic variant.
-	Multiple columns — containing information about the variants, classifications, conditions, etc.

  Our objective is to transfer this DataFrame into an SQLite database. For that,
  
 ### step 1 
```python
import sqlite3
conn = sqlite3.connect("myh7_variants.db")
```
This does two things:
1.	Creates a database called myh7_variants.db.
2.	Establishes a connection between Python and that database.
   ### step 2
```python
hcm_df.to_sql(
"hcm_variants",
conn,
if_exists="replace",
 index=False
)
```
Now our 137 HCM variants  stored in the SQLite database.

In SQL,

Initial exploration using PRAGMA table_info and row sampling verified column data types, field names, and table integrity across all 137 records.

Querying distinct values in the Gene(s) attribute revealed multiple compound identifier annotations (such as MHRT/MYH7 and LOC126861897/MYH7) alongside standalone MYH7 entries. Filtering specifically for records mapped strictly to MYH7 isolated 108 primary target variants, while the remaining 29 records represented complex multi-gene or overlapping locus annotations.

| ACMG / ClinVar Classification | All HCM Records (*n* = 137) | Isolated *MYH7* Cohort (*n* = 108) |
| :--- | :--- | :--- |
| Benign | 47 | 36 |
| Likely Benign | 6 | 4 |
| Likely Pathogenic | 18 | 12 |
| Pathogenic | 27 | 23 |
| Uncertain Significance (VUS) | 39 | 33 |

Across the entire dataset, 27 variants carry a definitive Pathogenic classification, with the overwhelming majority (23 of 27, or ~85.2%) localized directly to MYH7, underscoring its established role as a primary genetic driver in hypertrophic cardiomyopathy. Furthermore, Variants of Uncertain Significance (VUS) constitute nearly a third of both the general cohort ($n=39$) and the MYH7 subset ($n=33$), highlighting the ongoing clinical necessity for functional validation, expert re-evaluation, and domain-specific molecular consequence mapping

 ### What can we observe?

-	23 of the 27 Pathogenic records in the complete dataset belong to MYH7.
-	33 MYH7 records have Uncertain significance.
-	MYH7 contains variants across all five classification categories.


