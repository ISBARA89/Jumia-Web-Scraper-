# Jumia-Web-Scraper & Price Insights
## Project Overview
This project uses **Selenium** and **Python** to scrape smartphone data from Jumia, one of Nigeria's leading online retail platforms. The goal is to collect product names, prices, and perform a detailed analysis of the smartphone market in Nigeria.
## Technologies Used
- **Python**
- **Selenium** (for web scraping)
- **Pandas** (for data manipulation)
- **Matplotlib** & **Seaborn** (for data visualization)
- **Jupyter Notebook** (for development)
 ## Project Steps
### 1. **Data Scraping**
The first step in this project was to scrape the smartphone data from Jumia. We used **Selenium** to automate navigating to the Jumia smartphones page, extracting the product names and their respective prices. 
#### Code Snippet:
```python
names = driver.find_elements(By.CLASS_NAME, 'name')
prices = driver.find_elements(By.CLASS_NAME, 'prc')
````
# 2. Data Cleaning
After scraping the data, the next step was cleaning the price data to make it usable. This involved:
- Removing the ₦ currency symbol.
- Removing commas from the prices.
- Converting the cleaned data to a numeric format for further analysis.
#### Code Snippet:
```python
df['Price'] = df['Price'].replace({'₦': '', ',': ''}, regex=True)
df['Price'] = pd.to_numeric(df['Price'], errors='coerce')
````
# 3. Basic Analysis
Once the data was cleaned, we began the analysis by looking at the basic statistics of the prices. We calculated the minimum, maximum, median, and average price to understand the price range for smartphones.
Code Snippet:
```python
min_price = df['Price'].min()
max_price = df['Price'].max()
median_price = df['Price'].median()
avg_price = df['Price'].mean()
````
#### Results:
Min Price: ₦ 81,299.00
Max Price: ₦ 284,501.00
Median Price: ₦ 125,712.00
Average Price: ₦ 135,535.73
# 4. Price Distribution Visualization
We then created a histogram to visualize the price distribution of the smartphones. This gave us insights into the frequency of phones in certain price ranges.
Code Snippet:
```python
sns.histplot(df['Price'], bins=20, kde=True, color='blue')
```
![image](https://github.com/user-attachments/assets/870ca5c4-d2e3-4365-94ff-432c1195e8b9)

# 5. Price vs. Product Name Length
An interesting analysis we conducted was to check if there was any correlation between the length of the product name and its price. We calculated the length of each product name and plotted it against the price. 

Code Snippet:
```python
df['Name Length'] = df['Product Name'].apply(len)
correlation = df[['Name Length', 'Price']].corr()
```
We visualized the relationship using a scatter plot:
Code Snippet:
```python
sns.scatterplot(data=df, x='Name Length', y='Price')
```
![image](https://github.com/user-attachments/assets/c66fee19-ef80-428a-a1b9-d1d95af32b3c)

# 6. Top 5 Most Expensive Phones
We also extracted the top 5 most expensive smartphones to see which models were the priciest on Jumia.
Code Snippet:
```python
top_5_expensive = df.nlargest(5, 'Price')
```
#### Top 5 Most Expensive Phones:
Product Name   Price
41  XIAOMI Redmi Note 14 6.67" 8GB RAM/256 GB ROM ...  284501
47  Infinix Hot 50 Pro+ 6.78" 8GB RAM/128GB ROM An...  274226
49    Realme C75 Dual SIM Lightning Gold 8GB 256GB 4G  249900
7   itel S25 Ultra 6.78" AMOLED 256+8 4G Android-Blue  231300
22  itel S25 Ultra 6.78" AMOLED 256+8 4G Android-Blue  231300
#7. Price Categories
For a broader analysis, we categorized the smartphones into price ranges (e.g., budget, mid-range, premium). We visualized the distribution of smartphones across these categories.
Code Snippet:
```python
df['Price Category'] = pd.cut(df['Price'], bins=[0, 100000, 200000, 300000, float('inf')],
                              labels=['<₦100k', '₦100k-₦200k', '₦200k-₦300k', '₦300k+'])
sns.countplot(x='Price Category', data=df, palette='Set2')
```
# Conclusion
The analysis provided valuable insights into the smartphone market on Jumia. Here are the key takeaways:
- The average price of smartphones on Jumia is around ₦ 135,535.73.
- Most smartphones fall within the ₦100k-₦200k price range.
- There is a slight correlation between product name length and price, with longer names being associated with higher prices.
# Future Improvements
- Extract brand names from product titles for more detailed analysis.
- Expand the scraper to handle pagination and scrape more products.
- Build a price prediction model based on product features.
# How to Run the Project
1. Clone this repository.
2. Install the necessary dependencies:
pip install selenium pandas matplotlib seaborn openpyxl
3. Ensure that you have the ChromeDriver installed and in your PATH.
4. Run the scraper script (jumia_scraper.py).
5. Open the Jupyter Notebook to view and analyze the data.
# License
This project is licensed under the MIT License.


