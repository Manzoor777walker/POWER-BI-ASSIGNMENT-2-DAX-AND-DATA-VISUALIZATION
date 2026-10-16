# POWER-BI-ASSIGNMENT-2-DAX-AND-DATA-VISUALIZATION
 ## *DAX (Data Analysis Expressions) to analyze and transform  e-commerce sales data, generating key metrics and insights and create compelling  visualizations and perform detailed analysis to gain valuable insights into sales trends,  profitability, and performance metrics within the e-commerce domain*
## Instructions:-
          Note: Data modeling must be completed prior to data visualization. Ensure that relationships are established between the necessary tables, and calculations are performed to derive key metrics required for visualization. After creating the charts, make sure to format and customize them to enhance visual appeal and comprehension.
# E-Commerce Sales Analysis
This assignment will help you explore e-commerce sales data analysis using Power BI. 
Below are the files you will be working with (click on each to download): 
★ List of Orders.csv 
★ Order Details.csv 
★ Sales target.csv 
In this exercise, you will use DAX (Data Analysis Expressions) to analyze and transform e-commerce sales data, generating key metrics and insights. You will then create compelling visualizations and perform detailed analysis to gain valuable insights into sales trends, profitability, and performance metrics within the e-commerce domain.           
### ● Create a Calculated Column for 'Category Type': Add a calculated column in theOrder Details table that combines the 'Category' and 'Sub-Category' columns into a single 'Category Type' column.
            o	    In ‘order Detail table’ , Table tools|Add column
            o	     Using this formula to join two column     
                           *Category Type = CONCATENATE ('Order Details'[Category], CONCATENATE(" ",'Order Details'[Sub-Category]))*
### ● Calculate Revenue per Order in Order Details Table: Create a calculated column in the Order Details table to compute the revenue (Amount * Quantity) per order.
                    o	In the order Detail table—Table tool—Add new column
                    o	Create a new column and named as “revenue” and perform a calulation  (Amount * Quantity) based on per order.
                                     Formula used :  Revenue = 'Order Details'[Amount]*'Order Details'[Quantity]
### ● Create a Calculated Column to Categorize Sales: Add a calculated column named ‘Sales Category’ in the Order Details table that categorizes each order as 'Above Average' or 'Below Average' based on the Amount value.
                                     o	By Using measures I found out the average of “amount” column in order table which is 287.67.
                                     o	Based on this value, using conditional statement calculating a column named ‘Sales Category’ in the Order Details table that categorizes each order as 'AboveAverage' or 'Below Average' based on the Amount value.
                                     o	In order Detail table—Table tool—Add new column
                                     o	Create a new column and named as “Sales Category”
                                              Formula used : Sales Category = IF('Order Details'[Amount]>=287.67,"Above average","Below average")
## Calculated Measures:                                              

### ● Calculate Order Count: Define a measure to count the total number of orders in the Order Details table.
                                               o	In order Detail table—Table tool—new measure
                                               o	Used formula:- we can do it in two way
                                                           Count_Order = DISTINCTCOUNT('Order Details'[Order ID])
	If I want to count each distinct order( if you want to know how many individual orders were placed.),use Distinctcount
                                Or
                Countrows_order = COUNTROWS(‘Order Details’)
 If I want to count every single row in the table, which counts everything regardless of duplicates,use count rows.
### ● Calculate Average Profit in Delhi: Create a measure to calculate the average profit for orders placed .
                      o	Necessary needed data are lie in different table so I make a relation between “Order Detail table” and “List of Orders table” through “order ID”.
                      o	After that Home|measure|
                           Formula used : Average_Profit_Delhi = CALCULATE(AVERAGE('Order Details'[Profit]),'List of Orders'[State]= "Delhi")
                      o Visualize the measure through card.
### ● Calculate Year-to-Date (YTD) Sales: Define a measure to calculate the total sales amount accumulated from the earliest order date up to each order date.
                •	For this create a table and named as “date table” and using the mentioned below formula to extract a calender by using “Date” in the “list of order table”.
       Formula: Date table = ADDCOLUMNS(CALENDAR(MIN('List of Orders'[Order Date]),MAX('ListofOrders'[OrderDate])),"year",YEAR([Date]),"monthnumber",MONTH([Date]),"monthname",FORMAT([Date],"MMMM"),"Day",DAY([Date]),"Day Name",Format([Date],"dddd")).
                •	Build a relation between ‘date’ on the “Date Table” and ‘Order date’ on the “List of orders Table”.
                •	Home|tabletool|measures|
                      Formula: salesYTD = TOTALYTD(SUM('Order Details'[Amount]),'Date table'[Date])
                                     Here which is SalesYTD=159K

## Data Visualization:

### ● Sales Target Achievement by Category: Compare actual sales with sales targets by category using a clustered column chart.
                    o	Build a Clustered column chart from the visualization
                    o	Created a measure “total sales”: total sales = SUM('Order Details'[Amount])
                    o	Created a measure “Total target”: Totaltarget = SUM('Sales target'[Target])
   #### Clustered column chart
            x-axis= Category           y-axis= total sales, Total target
   ### ● Max Profit Margin by Sub-Category: Analyze the maximum profit margin for each sub-category of products using a donut chart.  
                          o	Build a Donut chart from the visualization             
                          o	Created a measure “profit margin”: Profit margin = MAXX('Order Details','Order Details'[Profit]/'Order Details'[Amount])
   #### Donut chart
           Legend -sub-category              values-profit margin            

### ●Monthly Sales Trend: Show the trend of monthly sales over time using a line chart.
           o	Build a linechart from the visualization
           o	x-axis= monthname, monthnumber
   #### Line Chart
               o	y-axis= total sales

### ●Comparison of Profit and Quantity by Sub-Category: Compare the relationship between profit and quantity sold for different sub-categories using a scatter chart.
           o	Build a scatter chart from the visualization
           o	Created a measure “Total profit “ and “Total Quantity”
           o	Total profit = SUM('Order Details'[Profit])
           o	Total quantity = SUM('Order Details'[Quantity])
#### Scatter chart
     Values-=Subcategory                                       
     x-axis=totalquantity                           
     Y-axis= totalprofit
     Size=total sales
   ### ●Comparison of Total Sales Amount and Target: Create cards to succinctly display the total sales amount alongside the sales target for quick comparison and analysis. Also, create a multi-row card to display the minimum target for each segment
               o	Created a measures “total sales”,”total target”,”min target”
               o	min target; Mintarget = MIN('Sales target'[Target])
               o	Build a card from visualization to visualize those measures
               o	Created a multi-row card for to visualize and summarize the data by 
                  o	Value=mintarget
                  o	Categories= category

### ●Sales Performance Matrix: Build a matrix view to analyze how actual sales compare to sales targets across different categories and months
             o	Created a measure “Total sales” and “Total target”
             o	Build a matrix from visualization to summarize the data 
   #### Matrix
             Rows=Category
             Column= Month Name
             Values=Total sales, Total target
   ### ●Geographic Sales Analysis: Visualize total sales on a map by city to identify regional sales patterns.
  #### Map Visuals        
           o	Build a  map visual from the visualization
           o	Location= City,State
           o	Bubble size= Total sales
  ### ●Sales Distribution by Sub-Category: Represent the sales distribution across different sub-categories using a treemap.
            
   #### Tree Map
             o	Build a tree map from the visualization
             o	Category= Sub category
             o	Values= Total sales

  ### ●Order Count Analysis by State: Create a funnel chart to visualize the distribution of order counts across different states.
   #### Funnel Chart      
            o	Build a funnel chart from the visualization
            o	Created a measure “Count Order”: Count_Order = DISTINCTCOUNT('Order Details'[Order ID])
            o	Category=State
            o	Values=Count_order







       










