# PY_Global_Superstore

## Table of contents

- [Problem Statement](#problem-satement)
- [Data Sources](#data-sources)
- [Tools](#tools)
- [Data Cleaning](#data-cleaning)
- [Questions and PY codes](#questions-and-py-codes)
- [Results/Findings](resultsfindings)
- [Recommendations](#recommendations)
- [Conclusion](#conclusion)


### Problem Statement
The main purpose of this Global Superstore project was/is to investigate the company's sales and profit by analyzing the historical dataset and tracking the sales and profit for each year, segment, and market. Additionally, it highlights the impact of different customers and products within the company's business. Furthermore, it analyzes the correlations between different factors to understand how certain elements affect the company's profit.

### Data Sources 
The data used for this analysis includes orders and returns data, which are stored in XLSX format across different sheets. The two datasets have been imported as an Excel workbook and then merged to create a comprehensive dataset to work with.

### Tools

- Visual Studio Code: The tool is a code editor optimized for building and debugging modern web and cloud applications. It integrates different code editors, such as Python and Jupyter Notebooks, which were activated/enabled to conduct this analysis within Visual Studio Code.  [Find here](https://code.visualstudio.com/)

- The analysis was conducted using the functionalities of Python's pandas, scikit-learn and Matplotlib.

### Data Cleaning

The project in Visual Studio Code began by importing the data, and since everything aligned with the analysis objectives, there was no need for a cleaning process. The main changes involved creating new columns and merging datasets to facilitate the analysis.
  
### Questions and PY codes

- To view all the questions, Python code, and answers, please check the Python notebook file. Only some interesting questions and code are displayed here.
  
1. Who are the top 10 customers?

```py
customer_profit = df_merge.groupby('Customer Name')['Profit'].sum()
top_customers = customer_profit.sort_values(ascending=False).head(10)

top_customers.plot(kind='bar', figsize=(10, 6), color='skyblue')

plt.title('Top 10 Customers by Profit')
plt.xlabel('Customer Name')
plt.ylabel('Total Profit')
plt.xticks(rotation=45, ha='right') 
plt.tight_layout() 
plt.show()
```
![Unknown](https://github.com/user-attachments/assets/c25c2bb4-b116-4fd2-86ca-bfeb23dac37b)

2. What are the top 6 profit products? 

```py
Product_profit = df_merge.groupby('Product Name')['Profit'].sum()
top_product = Product_profit.sort_values(ascending=False).head(6)

top_product.plot(kind='barh',figsize=(10, 6), color='green')

plt.title('Top 10 Products by profit')
plt.xlabel('Profit')
plt.ylabel('Product Name')
plt.tight_layout() 
plt.show() 
```
![Unknown-2](https://github.com/user-attachments/assets/994dc85e-54b7-4dad-80d1-e3dbf772752b)

3. What are the top 6 Loss product?
   
```py
Product_loss = df_merge.groupby('Product Name')['Profit'].sum()
Top_loss_product = Product_loss.sort_values(ascending=True).head(6)

Top_loss_product.plot(kind='barh',figsize=(10, 6), color='red')

plt.title('Top 6 product by loss (negative profit)')
plt.xlabel('Profit')
plt.ylabel('Product Name')
plt.tight_layout() 
plt.show()  
```
![Unknown-3](https://github.com/user-attachments/assets/2f034060-57cc-4b2d-8189-92db98f5f091)

- Descriptive analysis to understand the occurance of the patterns

4. Analyse shipping costs to understand if high shipping costs are associated with low or negative profits

```py
correlation_shipping_profit = df_merge['Profit'].corr(df_merge['Shipping Cost'])
print(f"Correlation between Profit and Shipping Cost: {correlation_shipping_profit}")

shipping_cost_analysis = df_merge.groupby('Product Name')[['Shipping Cost', 'Profit']].mean().sort_values(by='Profit')
print(shipping_cost_analysis.head(10))

df_merge.plot.scatter(x='Shipping Cost', y='Profit', title='Shipping Cost vs Profit', figsize=(10, 4))
plt.tight_layout()
plt.show()
```
<img width="1440" alt="Screenshot 2024-08-30 at 13 27 31" src="https://github.com/user-attachments/assets/3ac6090e-254f-4675-8393-2491e528b650">

5.  What impact or correlation Does Discounts have on profitability? 

```py
correlation_discount_profit = df_merge['Profit'].corr(df_merge['Discount'])
print(f"Correlation between Profit and Discount: {correlation_discount_profit}")

discount_analysis = df_merge.groupby('Product Name')[['Discount', 'Profit']].mean().sort_values(by='Profit')
print(discount_analysis.head(10)) 

df_merge.plot.scatter(x='Discount', y='Profit', title='Discount vs Profit', figsize=(10, 4))
plt.show()
```
<img width="1440" alt="Screenshot 2024-08-30 at 13 48 09" src="https://github.com/user-attachments/assets/def74cc6-ea05-4a2b-aff7-41c6132239f5">

6. What impact does delivery day have on customer satisfaction and profitability?

```py
correlation_delivery_profit = df_merge['Profit'].corr(df_merge['Delivery Day'])
print(f"Correlation between Profit and Delivery Day: {correlation_delivery_profit}")

delivery_analysis = df_merge.groupby('Product Name')[['Delivery Day', 'Profit']].mean().sort_values(by='Profit')
print(delivery_analysis.head(10)) 

df_merge.plot.scatter(x='Delivery Day', y='Profit', title='Delivery Day vs Profit', figsize=(10, 4))
plt.show()
```
<img width="1440" alt="Screenshot 2024-08-30 at 14 08 09" src="https://github.com/user-attachments/assets/885c1206-214d-4c4e-9b9a-216b96dcbe48">

7. What impact does the order priority have on profitability?

```py
priority_analysis = df_merge.groupby('Order Priority')['Profit'].mean().sort_values()
print(priority_analysis)

priority_analysis.plot(kind='bar', title='Order Priority vs Profit', figsize=(10, 6), color='purple')
plt.ylabel('Average Profit')
plt.show()
```
<img width="1440" alt="Screenshot 2024-08-30 at 14 23 00" src="https://github.com/user-attachments/assets/a6f25282-d433-42d2-b003-0e8db60d4343">

8. What correlation do segment and market have on profitability?

```py
# Convert 'Segment' and 'Market' to numerical values
label_encoder_segment = LabelEncoder()
df_merge['Segment_encoded'] = label_encoder_segment.fit_transform(df_merge['Segment'])

label_encoder_market = LabelEncoder()
df_merge['Market_encoded'] = label_encoder_market.fit_transform(df_merge['Market'])

# Calculate correlations
correlation_segment_profit = df_merge['Segment_encoded'].corr(df_merge['Profit'])
correlation_market_profit = df_merge['Market_encoded'].corr(df_merge['Profit'])

print(f"Correlation between Segment and Profit: {correlation_segment_profit}")
print(f"Correlation between Market and Profit: {correlation_market_profit}")
```

**output:** 

Correlation between Segment and Profit: 0.0027970402666889506
Correlation between Market and Profit: 0.0028472700468975044

### Results/Findings
1. The top customer who brings in the most profit to the company is Tamara Chand, followed by Raymond Buch, Sanjit Chand, and rounding out the top ten is Tom Ashbrook.
   
2. The top-selling product by profit is the Canon imageCLASS, followed by the Cisco Smart, the Motorola Smart Phone, and rounding out the top sex is the Harbour Creations Armchair.
   
3. The top product by Loss or negative profit is the Cubify...Head Print, followed by Lexmark...Laser Printer, Motorola Smart Phone Cordless, and rounding out the top sex is the Bevis Computer Table.
   
4. A correlation of 0.354 suggests a Low/moderate positive relationship between shipping cost and profit. This means that, generally, as shipping costs increase, profits also tend to increase, but the relationship is not strong. As the shipping cost analysis shows, there are notable exceptions where high shipping costs are associated with significant losses.
The scatter plot shows that many products are clustered around the profit line of 0. This means that many products have profits close to zero, which is concerning because it indicates they are barely breaking even or just covering their costs.

5. The correlation between Profit and Discount is -0.3165, which indicates a low-moderate negative relationship between the two variables. This means that as discounts increase, profits tend to decrease, and vice versa.
   
6. The correlation coefficient of 0.0017 suggests that Delivery Day has little to no impact on Profit in a linear sense (Weak Relationship).It can also be noticed that products with high negative profits show a range of delivery days, but no strong relationship is evident between delivery days and profitability. Since delivery days do not explain profit variations well, it is better to consider other factors.
   
7. The outputed information shoes that as the Order Priority increases from Low to Critical, the average profit also increases. This means that, on average, orders with higher priority tend to have higher profits.
   
8. Both 'Segment' and 'Market' have correlations very close to 0, indicating a very weak relationship between these categorical variables and profit. This suggests that neither 'Segment' nor 'Market' has a significant impact on profit based on the linear correlation analysis. However, when it comes to sales, certain segments and markets outperform others. This means that even if a segment or market has high sales, it does not automatically imply that it is profitable for the company. Other factors must be considered to classify a segment or market as truly profitable.
    
### Recommendations

#### 1. Customer Profitability Focus
Prioritize engagement with top customers because these customers bring in the most profit. Developing personalized offers or loyalty programs could further enhance their contribution.

#### 2. Product Profitability and Sales Strategy
Assess the performance of top-selling products, and consider promoting moderat profit products like the Harbour Creations Armchair.
Although these products generate high sales, ensuring they are profitable is crucial. It is important to evaluate the cost structures and pricing strategies to enhance profitability.

#### 3. Loss Management
Investigate and address the reasons behind the high losses of certain products. Understanding why these products are unprofitable can help in making decisions about whether to discontinue, revise pricing, or improve the product.

#### 4. Shipping Costs and Profit Analysis
Products with high shipping costs and negative profits should be reviewed for pricing strategies, discount policies, or potential inefficiencies in the supply chain that could be impacting profitability.
It is important to review shipping cost strategies to find a balance that maximizes profit without causing significant losses.
Although there is a weak positive correlation between shipping costs and profit, there are exceptions. Optimize shipping practices to avoid high costs associated with losses. 

#### 5. Discount reassesment: 
Reevaluate discount strategies, especially in relation to how they impact profit margins. The correlation between discounts and profit suggests that excessive discounting could harm overall profitability. While discounts can drive sales volume, they need to be carefully managed to ensure that they don't erode profits. The company may need to evaluate whether the increase in sales volume from discounts is enough to compensate for the reduced profit margins.

#### 6. Delivery Day Analysis
Focus on other factors that might affect profit, rather than delivery days. The correlation between delivery day and profit is very weak, so prioritize other variables that may have a more significant impact on profitability.

#### 7. Orders priorization: 
Since higher priorited orders contribute to the company’s profitability, understanding that higher-priority orders are more profitable can help focus efforts on optimizing these orders to maximize overall profitability (i.e optimizing customer relationship, resource allocation, product and sales strategies).

#### 8. Customer and Segment Insights
Analyze the characteristics of high-profit customers and high-sales segments/market to replicate success.
Understanding what differentiates high-profit/sales segments, market and customers can help in attracting and retaining similar profiles.

### Conclusion 

In conclusion, the analysis reveals that while certain customers and products significantly contribute to profit, a weak correlation exists between sales and profitability for some segments and markets. Shipping costs and discounts also impact profitability, though their relationships are nuanced. To optimize overall performance, the company should focus on enhancing customer engagement, refining product strategies, and carefully managing costs and discounts.

💻🖱️🤖🖱️🤖💻

 
