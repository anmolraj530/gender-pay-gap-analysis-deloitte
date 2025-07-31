[ANALYSIS_METHODOLOGY.md](https://github.com/user-attachments/files/21520512/ANALYSIS_METHODOLOGY.md)[ANALYSIS_METHODOLOGY.md](https://github.com/user-attachments/files/21520437/ANALYSIS_METHODOLOGY.md)# Gender Pay Gap Analysis - Deloitte Virtual Internship

## Project Overview
This project analyzes employee salary data to identify gender-based pay disparities using Excel and Python (Pandas, Matplotlib). The analysis includes data cleaning, visualization, and actionable recommendations for improving pay equity.

## Project Structure
```
├── README.md                           # This file
├── data/                               # Raw data files
│   └── daikibo-telemetry-data.json    # Employee salary dataset
├── analysis/                           # Analysis files
│   ├── Task 5 Equality Table.xlsx     # Gender pay gap analysis
│   └── Task 5 Model Answer.xlsx       # Model answer comparison
├── visualizations/                     # Dashboard and charts
│   ├── Dashboard 1.png                # Interactive dashboard
│   └── Task One.twb                   # Tableau workbook
├── documentation/                      # Project documentation
│   └── Task 2 Guide.pdf               # Project requirements and guide
└── requirements.txt                    # Python dependencies
```

## Key Findings
- Analyzed employee salary data across different departments and roles
- Identified gender-based pay disparities in specific job categories
- Created visualizations to highlight pay gap trends
- Provided actionable recommendations for improving pay equity

## Technologies Used
- **Excel**: Data analysis and pivot tables
- **Python**: Data cleaning and analysis with Pandas
- **Matplotlib**: Data visualization
- **Tableau**: Interactive dashboard creation

## Files Description

### Data Files
- `daikibo-telemetry-data.json`: Contains employee salary and demographic data

### Analysis Files
- `Task 5 Equality Table.xlsx`: Detailed gender pay gap analysis with calculations
- `Task 5 Model Answer.xlsx`: Model answer for comparison and validation

### Visualization Files
- `Dashboard 1.png`: <img width="811" height="778" alt="Dashboard 1" src="https://github.com/user-attachments/assets/462710df-e563-487b-9317-09e394ba49c3" />


### Documentation
- `Task 2 Guide.pdf`: [FINDINGS_AND_RECOMMENDATIONS.md](https://github.com/user-attachments/files/21520438/FINDINGS_AND_RECOMMENDATIONS.md)
- [SETUP_AND_INSTALLATION.md](https://github.com/user-attachments/files/21520440/SETUP_AND_INSTALLATION.md)
[PROJECT_OVERVIEW.md](https://github.com/user-attachments/files/21520439/PROJECT_OVERVIEW.md)
[Uploading ANALYSIS_MET# Analysis Methodology - Gender Pay Gap Analysis

## Data Processing Pipeline

### Step 1: Data Import and Initial Assessment
```python
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np

# Load the dataset
df = pd.read_json('data/daikibo-telemetry-data.json')

# Initial data exploration
print(f"Dataset shape: {df.shape}")
print(f"Columns: {df.columns.tolist()}")
print(f"Data types: {df.dtypes}")
```

### Step 2: Data Cleaning and Preprocessing
1. **Handling Missing Values**
   - Identified and addressed missing salary data
   - Removed records with incomplete demographic information
   - Validated data integrity

2. **Data Standardization**
   - Standardized job titles and department names
   - Normalized salary formats
   - Categorized experience levels

3. **Data Validation**
   - Checked for outliers in salary data
   - Verified gender classification accuracy
   - Ensured consistent data formats

### Step 3: Exploratory Data Analysis (EDA)

#### Gender Distribution Analysis
```python
# Analyze gender distribution
gender_dist = df['gender'].value_counts()
print(f"Gender distribution:\n{gender_dist}")

# Calculate gender percentages
gender_percentages = (gender_dist / len(df)) * 100
```

#### Salary Distribution Analysis
```python
# Analyze salary distributions by gender
male_salaries = df[df['gender'] == 'Male']['salary']
female_salaries = df[df['gender'] == 'Female']['salary']

# Calculate summary statistics
male_stats = male_salaries.describe()
female_stats = female_salaries.describe()
```

### Step 4: Pay Gap Calculations

#### Overall Pay Gap
```python
# Calculate overall pay gap
male_avg = male_salaries.mean()
female_avg = female_salaries.mean()
overall_gap = ((male_avg - female_avg) / male_avg) * 100
```

#### Department-wise Pay Gap
```python
# Calculate pay gap by department
dept_gaps = []
for dept in df['department'].unique():
    dept_data = df[df['department'] == dept]
    male_avg = dept_data[dept_data['gender'] == 'Male']['salary'].mean()
    female_avg = dept_data[dept_data['gender'] == 'Female']['salary'].mean()
    gap = ((male_avg - female_avg) / male_avg) * 100
    dept_gaps.append({'department': dept, 'pay_gap': gap})
```

### Step 5: Statistical Analysis

#### Hypothesis Testing
- **Null Hypothesis**: No significant difference in salaries between genders
- **Alternative Hypothesis**: Significant difference exists
- **Test Method**: T-test for independent samples
- **Significance Level**: α = 0.05

```python
from scipy import stats

# Perform t-test
t_stat, p_value = stats.ttest_ind(male_salaries, female_salaries)
print(f"T-statistic: {t_stat}")
print(f"P-value: {p_value}")
```

### Step 6: Visualization Creation

#### Salary Distribution Plots
```python
# Create salary distribution by gender
plt.figure(figsize=(12, 6))
plt.subplot(1, 2, 1)
male_salaries.hist(bins=30, alpha=0.7, label='Male')
female_salaries.hist(bins=30, alpha=0.7, label='Female')
plt.title('Salary Distribution by Gender')
plt.legend()

# Box plot comparison
plt.subplot(1, 2, 2)
df.boxplot(column='salary', by='gender')
plt.title('Salary Comparison by Gender')
plt.suptitle('')
```

#### Department-wise Pay Gap Visualization
```python
# Create bar chart of pay gaps by department
dept_gap_df = pd.DataFrame(dept_gaps)
plt.figure(figsize=(10, 6))
plt.bar(dept_gap_df['department'], dept_gap_df['pay_gap'])
plt.title('Pay Gap by Department')
plt.xlabel('Department')
plt.ylabel('Pay Gap (%)')
plt.xticks(rotation=45)
```

### Step 7: Advanced Analysis

#### Experience Level Analysis
```python
# Analyze pay gap by experience level
experience_levels = ['Junior', 'Mid-level', 'Senior', 'Executive']
for level in experience_levels:
    level_data = df[df['experience_level'] == level]
    male_avg = level_data[level_data['gender'] == 'Male']['salary'].mean()
    female_avg = level_data[level_data['gender'] == 'Female']['salary'].mean()
    gap = ((male_avg - female_avg) / male_avg) * 100
    print(f"{level} level pay gap: {gap:.2f}%")
```

#### Role-specific Analysis
```python
# Analyze pay gap by job role
for role in df['job_role'].unique():
    role_data = df[df['job_role'] == role]
    if len(role_data[role_data['gender'] == 'Male']) > 0 and len(role_data[role_data['gender'] == 'Female']) > 0:
        male_avg = role_data[role_data['gender'] == 'Male']['salary'].mean()
        female_avg = role_data[role_data['gender'] == 'Female']['salary'].mean()
        gap = ((male_avg - female_avg) / male_avg) * 100
        print(f"{role} pay gap: {gap:.2f}%")
```

## Quality Assurance

### Data Quality Checks
1. **Completeness**: Ensured all required fields are populated
2. **Consistency**: Verified data formats and classifications
3. **Accuracy**: Cross-referenced calculations with multiple methods
4. **Validity**: Confirmed statistical significance of findings

### Validation Methods
1. **Cross-validation**: Used multiple analysis approaches
2. **Peer review**: Compared results with model answers
3. **Sensitivity analysis**: Tested different assumptions
4. **Documentation**: Thoroughly documented all steps

## Tools and Technologies

### Primary Tools
- **Python 3.8+**: Core analysis and data processing
- **Pandas**: Data manipulation and analysis
- **Matplotlib/Seaborn**: Data visualization
- **NumPy**: Numerical computations
- **SciPy**: Statistical testing

### Supporting Tools
- **Excel**: Additional calculations and pivot tables
- **Tableau**: Interactive dashboard creation
- **Jupyter Notebook**: Code development and documentation

## Output Generation

### Analysis Reports
1. **Summary Statistics**: Key metrics and findings
2. **Detailed Calculations**: Step-by-step pay gap analysis
3. **Visualizations**: Charts and graphs for presentation
4. **Recommendations**: Actionable insights and suggestions

### File Formats
- **Excel**: Detailed calculations and pivot tables
- **PNG/PDF**: High-quality visualizations
- **Tableau**: Interactive dashboards
- **Markdown**: Documentation and methodology

## Limitations and Considerations

### Data Limitations
1. **Sample Size**: Limited to available employee data
2. **Time Period**: Analysis based on current data snapshot
3. **Variables**: Limited to available demographic information

### Analysis Limitations
1. **Correlation vs Causation**: Cannot establish causal relationships
2. **External Factors**: May not account for all influencing factors
3. **Context**: Limited to organizational context

### Recommendations for Future Analysis
1. **Longitudinal Study**: Track changes over time
2. **Additional Variables**: Include more demographic factors
3. **Industry Comparison**: Benchmark against industry standards
4. **Qualitative Research**: Supplement with employee surveys HODOLOGY.md…]()



## How to Use This Repository

1. **View the Analysis**: Open the Excel files in the `analysis/` folder to see the detailed calculations
2. **Explore Visualizations**: Check the `visualizations/` folder for dashboard screenshots
3. **Review Documentation**: Read the PDF guide for complete project context

## Skills Demonstrated
- Data cleaning and preprocessing
- Statistical analysis and hypothesis testing
- Data visualization and dashboard creation
- Business intelligence and reporting
- Pay equity analysis and recommendations

## Contact
This project was completed as part of the Deloitte Virtual Internship program. 
