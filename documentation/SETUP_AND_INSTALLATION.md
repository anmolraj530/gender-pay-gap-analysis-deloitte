# Setup and Installation Guide - Gender Pay Gap Analysis

## Prerequisites

### System Requirements
- **Operating System**: Windows 10/11, macOS, or Linux
- **Python**: Version 3.8 or higher
- **Memory**: Minimum 8GB RAM (16GB recommended for large datasets)
- **Storage**: At least 2GB free space for data and analysis files

### Required Software
- **Python 3.8+**: Download from [python.org](https://www.python.org/downloads/)
- **Git**: Download from [git-scm.com](https://git-scm.com/)
- **Excel**: Microsoft Excel or compatible spreadsheet software
- **Tableau**: Tableau Desktop (optional, for viewing .twb files)

## Installation Steps

### Step 1: Clone the Repository
```bash
# Clone the repository
git clone https://github.com/YOUR_USERNAME/gender-pay-gap-analysis-deloitte.git

# Navigate to the project directory
cd gender-pay-gap-analysis-deloitte
```

### Step 2: Set Up Python Environment

#### Option A: Using Virtual Environment (Recommended)
```bash
# Create virtual environment
python -m venv venv

# Activate virtual environment
# On Windows:
venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate

# Install required packages
pip install -r requirements.txt
```

#### Option B: Using Conda
```bash
# Create conda environment
conda create -n gender-pay-gap python=3.8

# Activate environment
conda activate gender-pay-gap

# Install required packages
pip install -r requirements.txt
```

### Step 3: Verify Installation
```python
# Test Python installation
python --version

# Test package installation
python -c "import pandas, matplotlib, numpy, seaborn; print('All packages installed successfully!')"
```

## Project Structure

```
gender-pay-gap-analysis-deloitte/
├── README.md                           # Project overview
├── requirements.txt                    # Python dependencies
├── .gitignore                         # Git ignore file
├── data/                              # Raw data files
│   └── daikibo-telemetry-data.json   # Employee dataset
├── analysis/                          # Analysis files
│   ├── Task 5 Equality Table.xlsx    # Pay gap calculations
│   └── Task 5 Model Answer.xlsx      # Model answers
├── visualizations/                    # Charts and dashboards
│   ├── Dashboard 1.png               # Dashboard screenshot
│   └── Task One.twb                  # Tableau workbook
└── documentation/                     # Project documentation
    ├── PROJECT_OVERVIEW.md           # Project overview
    ├── ANALYSIS_METHODOLOGY.md       # Analysis methodology
    ├── FINDINGS_AND_RECOMMENDATIONS.md # Findings and recommendations
    └── SETUP_AND_INSTALLATION.md    # This file
```

## Data Setup

### Step 1: Prepare the Dataset
The project uses a JSON dataset containing employee salary and demographic information.

```python
# Example: Load and explore the dataset
import pandas as pd

# Load the dataset
df = pd.read_json('data/daikibo-telemetry-data.json')

# Basic information
print(f"Dataset shape: {df.shape}")
print(f"Columns: {df.columns.tolist()}")
print(f"First few rows:")
print(df.head())
```

### Step 2: Data Validation
```python
# Check for missing values
print("Missing values per column:")
print(df.isnull().sum())

# Check data types
print("Data types:")
print(df.dtypes)

# Basic statistics
print("Basic statistics:")
print(df.describe())
```

## Running the Analysis

### Option 1: Using Jupyter Notebook
```bash
# Install Jupyter
pip install jupyter

# Start Jupyter notebook
jupyter notebook
```

Then navigate to the project directory and create a new notebook for your analysis.

### Option 2: Using Python Scripts
Create a Python script for your analysis:

```python
# analysis_script.py
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np
from scipy import stats

def load_data():
    """Load the employee dataset"""
    return pd.read_json('data/daikibo-telemetry-data.json')

def calculate_pay_gap(df):
    """Calculate gender pay gap"""
    male_avg = df[df['gender'] == 'Male']['salary'].mean()
    female_avg = df[df['gender'] == 'Female']['salary'].mean()
    gap = ((male_avg - female_avg) / male_avg) * 100
    return gap, male_avg, female_avg

def main():
    # Load data
    df = load_data()
    
    # Calculate pay gap
    gap, male_avg, female_avg = calculate_pay_gap(df)
    
    print(f"Gender Pay Gap: {gap:.2f}%")
    print(f"Male Average Salary: ${male_avg:,.2f}")
    print(f"Female Average Salary: ${female_avg:,.2f}")

if __name__ == "__main__":
    main()
```

Run the script:
```bash
python analysis_script.py
```

## Troubleshooting

### Common Issues and Solutions

#### Issue 1: Python not found
**Error**: `'python' is not recognized as an internal or external command`

**Solution**:
1. Ensure Python is installed and added to PATH
2. Try using `python3` instead of `python`
3. Reinstall Python and check "Add to PATH" during installation

#### Issue 2: Package installation errors
**Error**: `pip install -r requirements.txt` fails

**Solution**:
1. Upgrade pip: `python -m pip install --upgrade pip`
2. Install packages individually: `pip install pandas matplotlib numpy seaborn`
3. Use conda instead: `conda install pandas matplotlib numpy seaborn`

#### Issue 3: Memory errors with large dataset
**Error**: `MemoryError` when loading data

**Solution**:
1. Increase system RAM or use cloud computing
2. Load data in chunks: `pd.read_json('file.json', chunksize=1000)`
3. Use data sampling for initial analysis

#### Issue 4: File not found errors
**Error**: `FileNotFoundError: [Errno 2] No such file or directory`

**Solution**:
1. Check file paths are correct
2. Ensure you're in the right directory
3. Verify file names match exactly (case-sensitive)

### Performance Optimization

#### For Large Datasets
```python
# Use efficient data types
df = df.astype({
    'salary': 'float32',
    'age': 'int8',
    'gender': 'category'
})

# Use chunking for large files
chunks = pd.read_json('large_file.json', chunksize=10000)
for chunk in chunks:
    # Process each chunk
    pass
```

#### Memory Management
```python
# Clear memory when needed
import gc
gc.collect()

# Use efficient data structures
df = df.dropna()  # Remove missing values
df = df.reset_index(drop=True)  # Reset index
```

## Development Environment Setup

### VS Code Setup
1. Install VS Code: [code.visualstudio.com](https://code.visualstudio.com/)
2. Install Python extension
3. Install Jupyter extension
4. Open the project folder in VS Code

### PyCharm Setup
1. Install PyCharm: [jetbrains.com/pycharm](https://www.jetbrains.com/pycharm/)
2. Open the project folder
3. Configure Python interpreter
4. Install required packages

## Version Control

### Git Setup
```bash
# Initialize git repository (if not already done)
git init

# Add files
git add .

# Commit changes
git commit -m "Initial commit: Gender Pay Gap Analysis"

# Add remote repository
git remote add origin https://github.com/YOUR_USERNAME/gender-pay-gap-analysis-deloitte.git

# Push to GitHub
git push -u origin main
```

## Additional Resources

### Documentation
- [Pandas Documentation](https://pandas.pydata.org/docs/)
- [Matplotlib Documentation](https://matplotlib.org/stable/contents.html)
- [NumPy Documentation](https://numpy.org/doc/)

### Tutorials
- [Python for Data Analysis](https://pandas.pydata.org/pandas-docs/stable/user_guide/10min.html)
- [Matplotlib Tutorial](https://matplotlib.org/stable/tutorials/index.html)
- [Statistical Analysis with Python](https://docs.scipy.org/doc/scipy/reference/)

### Support
- Check the project documentation in the `documentation/` folder
- Review the README.md file for project overview
- Contact the project maintainer for specific issues

## Next Steps

After setting up the environment:

1. **Explore the Data**: Load and examine the dataset
2. **Run Basic Analysis**: Calculate pay gaps and statistics
3. **Create Visualizations**: Generate charts and graphs
4. **Document Findings**: Update the findings document
5. **Share Results**: Present analysis to stakeholders

The project is now ready for analysis and development! 