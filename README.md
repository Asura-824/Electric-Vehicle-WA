# Electric Vehicles Population in WA

A data analysis and simple forecasting project exploring electric vehicle registrations in Washington (WA). The analysis is implemented as a Jupyter notebook (Electric_vehicle.ipynb) using PySpark for initial processing and pandas / seaborn / matplotlib for visualization. The notebook also includes a small example of using Spark ML (Linear Regression) to forecast future Tesla registrations.

## Repository contents

- `Electric_vehicle.ipynb` - Main Jupyter notebook that:
  - Loads the Electric Vehicle Population dataset (CSV).
  - Performs schema inspection, descriptive statistics and data cleaning.
  - Creates a Spark SQL temporary view and runs queries.
  - Visualizes top brands, models and brand-specific analyses (Tesla, Chevrolet, Nissan, Ford, Kia, etc.).
  - Converts Spark DataFrame to pandas for plotting.
  - Trains a Linear Regression model (Spark ML) to forecast future Tesla sales by model year.
- `Electric_Vehicle_Population_Data.csv` - Dataset used by the notebook (expected to be in the repo root or the notebook's working directory).

## Quick overview

The notebook demonstrates:
- How to read CSV data into a Spark DataFrame and inspect schema.
- Using Spark SQL for aggregation and grouping.
- Converting Spark DataFrames to pandas for plotting with seaborn/matplotlib.
- Cleaning the data (dropping nulls) and examining data shape and types.
- Simple linear regression forecasting on Tesla counts by model year using PySpark ML.

Example output from the notebook's forecasting step (values will vary depending on dataset):
Model Year -> Predicted Tesla registrations for future years (2027-2030).

## Requirements

To run the notebook locally you will need:

- Python 3.8+ (or compatible)
- Java 8/11 (required by Spark)
- Apache Spark (compatible with your pyspark version)
- Jupyter Notebook or JupyterLab

Python packages (install via pip):
- pyspark
- pandas
- numpy
- matplotlib
- seaborn

Example installation:
```bash
# create & activate virtualenv (optional)
python -m venv .venv
source .venv/bin/activate

pip install pyspark pandas numpy matplotlib seaborn jupyterlab
```

Note: Installing `pyspark` via pip will download a Spark distribution. For production or cluster runs, use an appropriate Spark installation.

## How to run

1. Ensure the CSV file `Electric_Vehicle_Population_Data.csv` is located in the same directory as the notebook (or update the notebook path).
2. Start Jupyter:
   ```bash
   jupyter notebook Electric_vehicle.ipynb
   # or
   jupyter lab Electric_vehicle.ipynb
   ```
3. Run cells in order. The notebook creates a SparkSession with:
   ```python
   spark = SparkSession.builder.appName('Myapp').getOrCreate()
   ```
   If you need custom configuration (e.g., more driver memory), modify the SparkSession builder.

4. To reproduce the forecast, run the cells that:
   - Filter Tesla data using Spark SQL
   - Use VectorAssembler to create features
   - Fit a LinearRegression model and predict for future years

## Tips & improvements

- The notebook currently drops all nulls with `dropna()` — consider more nuanced imputation for certain columns, or handling missing electric range/base MSRP differently.
- The ML model is a simple linear regression on Model Year -> Count. For better forecasts consider:
  - Using time-series models (ARIMA, Prophet) or more features (economic indicators, incentives, county/population).
  - Evaluating model metrics (RMSE, R2) and cross-validation.
- Large datasets: when converting Spark DataFrame to pandas, be mindful of driver memory; sample or aggregate before converting for plotting.
- Add unit tests and a requirements.txt / environment.yml for reproducible installs.

## License

This project is provided under the MIT License. See LICENSE (or add one) if you want to include a license file.

## Contact

Created by: shubh645

If you want changes to the README (add more details, badge, CI instructions, license text), tell me what to include and I will update it.
