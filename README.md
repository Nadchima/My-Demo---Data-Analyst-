# Data Analysis Report: Real Estate📊
# 1. Objective
    The objective of this analysis is to summarize and interpret real estate listing data across various provinces in Thailand. The goal is to understand price trends, distribution of unit types, and geographic concentration, using visual insights from the provided dashboard.

# 2. Data Overview
    The dataset includes residential unit listings with the following key fields:
    - Unit Name
    - Unit Type (1-Bedroom, 2-Bedroom)
    - Province
    - Unit Price (in THB)
    - Unit Size (Sq.m.)

# 3. Key Visualizations & Findings
**Unit Size vs Unit Price Scatter Plot**
   A general upward trend is observed—larger units tend to have higher total prices. However, there are notable outliers, indicating luxury units with higher price per square meter.

**Combined Sales & Rental Value**
    This shows the total monetary value of both property sales and rental listings. It helps compare the overall market size in terms of sales revenue versus potential rental income across different regions.

**Top 3 Prices by Developer**
    Displays the top three highest-priced units for each developer. This reveals which developers are focusing on premium or luxury projects within the market.

**Total Number of Buildings by Property Type**
    Indicates the number of buildings categorized by property type, such as condominium, single house, or townhouse. This helps identify development trends and market supply across different property categories.

**Rental Yield (%) by Property Type**
    Shows the rental yield percentage calculated for each property type. It highlights which property types offer the best return on investment from a rental perspective.

# 4. Insights
  - Smaller unit types (1-2 bedrooms) dominate the listings, suggesting a market focus on compact urban living.
  - Some units with relatively small sizes have high prices, indicating premium pricing based on location or brand rather than size alone.
  - Outer provinces offer more affordable units, which may appeal to budget-conscious buyers or long-term investors.

# 5. Exploratory Data Analysis (EDA) in Google Colab
  # 1. Import Libraries
    import pandas as pd

  # 2. Load the Dataset
    df = pd.read_excel('/content/mock_thailand_real_estate_complex_data_v3.xlsx')
    df.head()
    
  # 3. Basic Info & Summary
    df.info()                  
    df.describe()              
    df.isnull().sum()          
    df.duplicated().sum()    
    
  # 4. Clean Data
    print(df.duplicated().sum())
    df.drop(columns=['Property_ID'])
    df['Sale_Price_THB'] = df['Sale_Price_THB'].fillna(df['Sale_Price_THB'].mean())
    df['Rental_Price_THB'] = df['Rental_Price_THB'].fillna(df['Rental_Price_THB'].mean())
    df['Website'] = df['Website'].fillna('Unknown')
    df['Area_sqm'] = df['Area_sqm'].fillna(df['Area_sqm'].mean())
    df['Floor_Range'] = df['Floor_Range'].fillna('Unknown')
    df['Year_Built'] = df['Year_Built'].fillna('Unknown')
    df['Building_Age_Years'] = df['Building_Age_Years'].fillna('Unknown')
    df['Contact_Phone'] = df['Contact_Phone'].fillna('Unknown')
    df['Amenities'] = df['Amenities'].fillna('Unknown')
    df['Address'] = df['Address'].fillna('Unknown')
    df = df[df['Sale_Price_THB'] < 10000000]      # Filter some outliers for sales price

  # 5. Data Handle
    df['Price_per_sqm'] = df['Sale_Price_THB'] / df['Area_sqm']
    
  # 6. Data Relationship
    print(df.groupby('Area_sqm')['Sale_Price_THB'].mean())
    print(df['Property_Type'].value_counts())
    
  # 7. Data Export
    df.to_excel('property_data_cleaned.xlsx', index=False)

# 6. Data Analysis Process in Power BI
  # Data Import
      Import data from Excel or other data sources into Power BI to start the analysis.
      
  # Data Cleaning:
      Remove duplicates, handle missing values, and adjust data types appropriately using Power Query.
      
  # Data Modeling:
      Link tables and create Measures/Columns using DAX for analytical calculations.
   Example: 
    MEASURE 'Sheet1'[Average_Building_Age] = AVERAGE(Sheet1[Building_Age_Years])
    MEASURE 'Sheet1'[Average_Number_Of_Buildings] = AVERAGE(Sheet1[Number_of_Buildings])
    MEASURE 'Sheet1'[Yield_Rent] = DIVIDE(SUMX(Sheet1, Sheet1[Rental_Price_THB] * 12), SUM(Sheet1[Sale_Price_THB])) * 100
    
  # Visualization:
      Create interactive charts and dashboards such as Bar Charts, Pie Charts, and Slicers to display the results.

![image](https://github.com/user-attachments/assets/3b763999-bda7-493f-8349-9b3658cefb06)




