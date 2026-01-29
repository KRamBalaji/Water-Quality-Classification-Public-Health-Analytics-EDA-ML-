# **Maharashtra Water Quality Classification & Public Health Analytics**

## **📌 Project Overview**

This project focuses on analyzing environmental water quality data provided by the **Maharashtra Pollution Control Board (MPCB)** under the **National Water Monitoring Programme (NWMP)** for August 2025\.

The goal is to automate the classification of water bodies into four regulatory categories (**Class A, B, C, and E**) using machine learning. By transforming raw physicochemical and biological data into instant safety classifications, this tool supports public health officials in making rapid, data-driven decisions regarding water safety for drinking, bathing, and industrial use.


## **📊 Key Findings from EDA**

* **Primary Pollutants:** Biochemical Oxygen Demand (BOD) and Total Coliform emerged as the strongest predictors of water quality degradation.
* **Class Imbalance:** Approximately **82%** of the dataset is labeled as **Class A** (Safe), creating a significant challenge for models to accurately identify rare pollution events in Classes B, C, and E.
* **Correlation Trends:** A high correlation between COD and BOD confirmed that organic load is a primary driver of pollution in the monitored river basins.
* **Data Quality Issues:** Real-world issues such as (BDL) (Below Detection Limit) strings and missing temperature readings required specialized regex cleaning and median imputation during the preprocessing phase.

## **🤖 Model Performance**

We compared a linear baseline (**Logistic Regression**) with an ensemble method (**Random Forest**) to determine the most reliable tool for public health.

| Model | Overall Accuracy | Class E Recall | Recommendation |
| :--- | :--- | :--- | :--- |
| **Random Forest** | **85.71%** | 0.00% | High accuracy but biased; failed to detect pollution. |
| **Logistic Regression** | 54.29% | **75.00%** | **Recommended** for detecting high-risk sites. |

**Note on Selection:** While Random Forest shows higher overall accuracy, it is clinically "blind" to polluted water (Class E) due to class imbalance. **Logistic Regression (Balanced)** was chosen for its high **Recall**, ensuring that 75% of polluted sites are correctly flagged for inspection.

## **🛠️ Feature Engineering**

To improve model sensitivity, we engineered the **COD/BOD Ratio**. This serves as a critical indicator of the biodegradability of waste. A high ratio flags industrial runoff (high COD, low BOD), while a lower ratio points toward municipal sewage, helping the model distinguish between pollution types.

## **🚀 How to Run the Project**

### **1\. Prerequisites**

Ensure you have Python 3.9+ installed.

### **2\. Installation**

Clone the repository and install the required libraries:

```bash
git clone \[https://github.com/your-username/water-quality-project.git\](https://github.com/your-username/water-quality-project.git)
cd water-quality-project
pip install \-r requirements.txt
```

### **3\. Run Analysis**

* Open Water Quality Classification.ipynb to view statistical summaries and visualizations and to reproduce the training and evaluation pipeline.


## **💡 Actionable Recommendations**

### **1\. Strategic Monitoring & Early Warning**

* **Real-Time Hotspot Tracking:** Prioritize the deployment of automated, IoT-enabled sensors at the 19 identified "Class E" stations. These sensors should focus on high-frequency monitoring of BOD and Dissolved Oxygen (DO) to trigger immediate public health alerts when levels breach safety thresholds.
  
* **Industrial Discharge Audits:** Utilize the engineered **COD/BOD ratio** to flag stations showing sudden spikes in non-biodegradable waste, enabling targeted regulatory audits of nearby industrial clusters.

### **2\. Infrastructure & Public Health Interventions**

* **Wastewater Treatment Optimization:** High Fecal Coliform counts across specific districts indicate a critical need for auditing local Sewage Treatment Plants (STPs). Upgrading disinfection stages (e.g., UV or chlorination) in these areas is essential to prevent waterborne disease outbreaks.
  
* **Source Protection Zones:** Establish stricter buffer zones around stations classified as Class A to maintain their high quality, preventing agricultural or urban encroachment.

### **3\. Data-Driven Policy & Model Evolution**

* **Advanced Re-sampling Techniques:** To address the severe class imbalance, future iterations should implement **SMOTE (Synthetic Minority Over-sampling Technique)** or ADASYN to improve the model's sensitivity toward rare "Class B" and "Class C" events.
  
* **Longitudinal Analysis:** Expand the dataset to include multi-seasonal data (Monsoon vs. Summer) to account for seasonal variations in pollutant concentration, which will improve the robustness of the predictive model.
