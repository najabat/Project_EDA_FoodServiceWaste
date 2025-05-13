# Exploratory Data Analysis (EDA) of Food Service Waste: Insights for Operational Efficiency

## Project Overview

This project focuses on performing an Exploratory Data Analysis (EDA) on a food service dataset to identify key factors influencing operational efficiency and food waste. Following a comprehensive data cleaning and preprocessing phase, the analysis aims to uncover critical insights, identify key patterns, and derive actionable recommendations to optimize food service operations and significantly reduce food waste.

## Dataset

The dataset used for this analysis ("Food data.csv") contains information about daily food service operations, including:

* **ID**: Unique identifier for each record.
* **date**: The date of the observation. From this, `day_name`, `month_name`, and `year` were derived for analysis.
* **meals_served**: The number of meals served on that day.
* **kitchen_staff**: The number of kitchen staff working on that day.
* **temperature_C**: The temperature (in Celsius) on the recorded day.
* **humidity_percent**: The humidity percentage on the recorded day.
* **day_of_week**: The day of the week (numeric value, 0 = Sunday through 6 = Saturday, as per guidelines).
* **special_event**: Binary indicator for special events (1 = event, 0 = no event).
* **past_waste_kg**: Amount of food waste in kilograms from previous days. This is the primary target variable for understanding food waste.
* **staff_experience**: Experience level of kitchen staff (e.g., "Beginner", "Intermediate", "Expert").
* **waste_category**: Category of food waste (e.g., "dairy", "meat", "produce").

The dataset was sourced from the csv file provided as part of assignment. The primary data file used is `Food data.csv`, located in the `data/` directory.

## Repository Contents

This repository is structured as follows:

* `data/`: Contains the raw dataset file (`Food data.csv`).
* `notebooks/`: Contains the Colab Jupyter Notebook (`Project_EDA_Food_Service_Data_NajabatKhan_V1_0.ipynb`) detailing the entire EDA process, including data cleaning, analysis, and visualization.
* `reports/`: Contains the final project report (`ProjectReport_ExploratoryDataAnalysis_FoodServiceWaste_1.0.pdf`) summarizing the findings, methodology, and recommendations.
* `README.md`: This file, providing an overview of the project.
* `requirements.txt`: A list of Python dependencies required to run the notebook.
* `.gitignore`: Specifies intentionally untracked files that Git should ignore (e.g., virtual environment files, system files).

## Exploratory Data Analysis (EDA) Process

The EDA was conducted in several stages:

1.  **Data Loading and Initial Inspection**: Understanding the structure, data types, and initial state of the data. Column names were standardized (lowercase with underscores).
2.  **Data Cleaning**:
    * Checked and handled missing values: Numerical columns imputed using mean or median; categorical columns (staff_experience, waste_category) imputed using mode. `staff_experience` had the most missing values (18.50%).
    * Identified and confirmed no duplicate rows.
    * Processed and harmonized categorical data: Standardized `staff_experience` (e.g., "Pro" to "Expert") and `waste_category` (e.g., "MeAt" to "Meat", grouping specific grains).
    * Ensured correct data types: `date` column converted to datetime objects (some rows dropped due to invalid dates); `special_event`, `kitchen_staff` (text like "ten" converted to numeric), `meals_served` converted to numeric types.
3.  **Descriptive Statistics**:
    * Calculated summary statistics (mean, median, standard deviation, min, max, quartiles) for numerical features. `meals_served` showed a right-skewed distribution.
4.  **Data Visualization**:
    * Used histograms and density plots for numerical features.
    * Employed boxplots to detect outliers (noted in `meals_served` and `temperature_C`) and visualize data spread.
    * Utilized bar plots for categorical variables.
    * Scatter plots to explore relationships between numerical variable pairs.
5.  **Correlation Analysis**:
    * Generated a correlation matrix and heatmap to quantify linear relationships, particularly with `past_waste_kg`.
6.  **Hypothesis Testing**:
    * **Kitchen Staffing Level vs. Food Waste:** ANOVA test used to compare waste across low, medium, and high staff level groups.
    * **Special Events vs. Food Waste:** Independent samples t-test used to compare mean waste on event days versus non-event days.

## Summary of Key Findings/Insights

* **Meals Served vs. Waste:** The number of `meals_served` showed a negligible linear correlation (-0.06) with `past_waste_kg`, suggesting that current forecasting related to volume might be relatively effective or other factors are more dominant.
* **Special Events Impact:** Special events did not significantly impact average food waste. Mean waste on event days was 27.27 kg versus 26.97 kg on non-event days, with a t-test p-value of 0.7763.
* **Staff Experience Matters:** A clear trend was observed with staff experience: Beginner staff generated the most waste on average (28.33 kg), followed by Intermediate staff (27.39 kg), and Expert staff generated the least (26.50 kg).
* **Dominant Waste Category:** Meat products were identified as the primary contributor to waste, accounting for approximately 42.54% of recorded categorized waste instances.
* **Weekly Waste Patterns:** Food waste tends to peak on Wednesdays (average 28.94 kg) and Saturdays (average 28.17 kg).
* **Kitchen Staffing Levels:** ANOVA testing confirmed a statistically significant relationship between the number of `kitchen_staff` on duty and food waste levels (F-statistic: 4.050, p-value: 0.0176).
* **Outliers Noted:** Potential outliers were identified in `meals_served` (46 instances, 2.52%) and `temperature_C` (44 instances, 2.41%), which were noted for their potential influence but not removed for this EDA.

## Recommendations

1.  **Refine Forecasting & Identify Core Waste Drivers:** While meal volume forecasting seems robust against proportional waste increases, further investigate other operational elements (e.g., menu complexity, specific high-waste items not captured by category, preparation methods) that might more directly influence waste.
2.  **Invest in Staff Development & Mentorship:** Implement targeted training programs for less experienced staff (Beginners and Intermediates) focusing on efficient food handling, portion control, and waste reduction techniques. Consider mentorship by Expert staff.
3.  **Tackle Meat Waste Strategically:** Develop and implement a focused strategy to reduce meat waste. This should involve reviewing purchasing volumes, optimizing storage and preparation (e.g., trim waste reduction), and evaluating portion sizes for meat-centric dishes.
4.  **Optimize Peak Waste Day Operations:** For Wednesdays and Saturdays, conduct deeper analysis to understand the drivers of higher waste. This could involve reviewing specific menu items, preparation volumes, and staffing patterns on these days to identify targeted interventions.
5.  **Strategic Staff Deployment & Best Practice Identification:** Given the significant link between `kitchen_staff` numbers and waste, analyze waste variations within the identified low, medium, and high staff groups. Aim to identify optimal staffing levels or best practices from team sizes/compositions that demonstrate lower waste without compromising service quality.
6.  **Data Integrity and Contextual Learning from Outliers:** Investigate the root causes of identified outliers in `meals_served` and `temperature_C`. If they are data entry errors, improve data collection protocols. If they represent genuine unusual circumstances (e.g., unexpected demand surges, extreme weather), document these events to refine future planning and forecasting models.
7.  **Adaptive Special Event Management:** Although no overall significant impact was found, continue to monitor waste on an event-by-event basis, as unique or larger-scale events might still present specific waste challenges or require tailored planning.

## How to Run the Code (Using Google Colab)

This project is designed to be run in Google Colaboratory.

1.  **Download Files from this Repository:**
    * Download the Interactive Python Notebook: `notebooks/Project_EDA_Food_Service_Data_NajabatKhan_V1_0.ipynb`
    * Download the dataset: `data/Food_data.csv`

2.  **Open Google Colab:**
    * Go to [https://colab.research.google.com/](https://colab.research.google.com/).
    * You may need to sign in with your Google account.

3.  **Upload the Notebook to Colab:**
    * In Colab, go to `File` > `Upload notebook...`.
    * Select the `Project_EDA_Food_Service_Data_NajabatKhan_V1_0.ipynb` file you downloaded.

4.  **Make the Dataset Accessible to the Notebook:**
    * **Method 1: Upload directly to Colab session (temporary for one session):**
        * In the Colab notebook, locate the file browser panel on the left side.
        * Click the "Upload to session storage" button (looks like a file icon with an upward arrow).
        * Select the `Food_data.csv` file you downloaded.
        * **Note:** Files uploaded this way are deleted when the Colab runtime is recycled. The notebook is likely configured to read the file assuming it's in the root directory of the Colab environment (e.g., `pd.read_csv('Food_data.csv')`).
    * **Method 2: Mount Google Drive (persistent storage):**
        * If the notebook contains code to mount Google Drive (often starting with `from google.colab import drive` and `drive.mount('/content/drive')`), it's generally preferred for larger files or if you want the data to persist across sessions.
        * **First, upload `Food_data.csv` to your Google Drive** (e.g., into the main "My Drive" area or a specific folder).
        * When you run the cell in the notebook that contains `drive.mount('/content/drive')`, you will be prompted to authorize Colab to access your Google Drive. Follow the on-screen instructions (usually involves clicking a link, selecting your Google account, and copying an authorization code back into the Colab input field).
        * After mounting, you'll need to ensure the file path in your notebook's `pd.read_csv()` function (or equivalent) correctly points to the location of `Food_data.csv` within your Google Drive (e.g., `pd.read_csv('/content/drive/MyDrive/Food_data.csv')` if it's in the root of your Drive, or `pd.read_csv('/content/drive/MyDrive/YourFolder/Food_data.csv')` if it's in a subfolder). **The notebook `Project_EDA_Food_Service_Data_NajabatKhan_V1_0.ipynb` is expected to contain the necessary code to handle data loading after mounting Google Drive.**

5.  **Run the Notebook Cells:**
    * Once the notebook is open and the data is accessible, you can run the cells sequentially.
    * Go to `Runtime` > `Run all`. Alternatively, you can run cells individually by clicking the "play" button to the left of each cell or by pressing `Shift + Enter`.
    * Ensure you run any initial cells that import libraries and load/mount the data before running subsequent analysis cells.

## How to Run the Code (Locally with Jupyter)

If you prefer to run the notebook locally:

1.  **Clone the repository:**
    ```bash
    git clone <your-repository-link>  # Replace <your-repository-link> with the actual URL
    cd Food-Service-EDA 
    ```
2.  **Create a virtual environment (recommended):**
    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows use `venv\Scripts\activate`
    ```
3.  **Install dependencies:**
    ```bash
    pip install -r requirements.txt
    ```
4.  **Launch Jupyter Notebook:**
    Navigate to the `notebooks/` directory from your project root:
    ```bash
    cd notebooks 
    jupyter notebook Project_EDA_Food_Service_Data_NajabatKhan_V1_0.ipynb
    ```
    Or, from the root project directory:
    ```bash
    jupyter notebook notebooks/Project_EDA_Food_Service_Data_NajabatKhan_V1_0.ipynb
    ```
    Then, open the `Project_EDA_Food_Service_Data_NajabatKhan_V1_0.ipynb` file from the Jupyter interface and run the cells. The notebook should be configured to load `Food_data.csv` from the relative path `../data/Food_data.csv`.

## Technologies Used

* Python 3.x
* Pandas: For data manipulation and analysis.
* NumPy: For numerical operations.
* Matplotlib: For basic static visualizations.
* Seaborn: For enhanced statistical visualizations.
* SciPy: For statistical tests (e.g., t-tests, ANOVA).
* Jupyter Notebook / Google Colaboratory: As the interactive development environment.

Author: Najabat Ali Khan
Date: 13-May-2024
---