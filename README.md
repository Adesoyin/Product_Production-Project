**Optimizing Production Performance in a Manufacturing Industry**
 
![image](https://github.com/Adesoyin/Product_Production-Project/assets/123065894/e477a504-b0e2-4bcc-975c-e5494dc662de)

**Introduction**

This project came up from the Microsoft Power BI challenge I saw on LinkedIn and immediately fell in love with the data. The data does not look like the regular production data I was familiar with. Hence, it will widen my scope of data cleaning, DAX and visualization.

**Power BI Concepts applied**

1. Calculated Columns, Calendar table
2. Data Modelling: Star Schema
3. DAX measures

**Problem Statement**
1.	Inefficient Resource Allocation Leading to Production Delays and Increased Costs
2.	Lack of Visibility into Production Bottlenecks and Process Inefficiencies
3.	Inconsistent Quality Control Leading to High Defect Rates
4.	Ineffective Production Planning and Scheduling
5.	Inaccurate Forecasting and Demand Planning

**Data Sourcing**

I sourced the AdventureWorks2019.bak file and downloaded it as a .bak file. Afterwards, I logged into Microsoft SSMS 18, restored the downloaded file “AdventureWorks2019” from my device and imported it as a database into my server.  

The four tables needed for the challenge were then gotten using the "select" statement into Power BI for cleaning, analysis and visualization. 
1.	Production.Product, 
2.	Production.BillOfMaterials, 
3.	Production.WorkOrder, and  
4.	Production.WorkOrderRouting

![image](https://github.com/Adesoyin/Product_Production-Project/assets/123065894/9d82d39a-4fdc-4912-867a-353fb83a78fc)


**Data Cleaning**

Much cleaning was not done on the dataset imported. However, the datatype was changed e.g. date fields are of data type, amount are of numbers etc.  Also, duplicates rows were removed and then applied and loaded. 

From the Data view;
1.	Calculated columns were created to calculate the average TAT for the actual days and scheduled days of manufacturing products. Likewise for order routing days to reach location. 
2.	List Variance from the standard cost was also calculated as
List Price variance From Standard Cost = DIVIDE(('Production Product'[ListPrice]-'Production Product'[StandardCost]),'Production Product'[ListPrice])
3.	The work stress was inferred from a two-step calculated column to determine if the work was finished earlier or later before the due date. 

Work Order TAT = DATEDIFF('Production WorkOrder'[StartDate],'Production WorkOrder'[EndDate],DAY)

Work Order due Days = DATEDIFF('Production WorkOrder'[EndDate],'Production WorkOrder'[DueDate],DAY)

Work Stress = SWITCH(TRUE(), 
                'Production WorkOrder'[Work Order due Days] < 0 ,  "Finished after Due Date",
                'Production WorkOrder'[Work Order due Days] >=0  ,  "Finished on/before Due Date")

Other measures were created which are not included in here. you can also interact with the report using this link [Optimizing Production Performance in a Manufacturing Industry](https://app.fabric.microsoft.com/view?r=eyJrIjoiZDE0ZDhhZDktMDdjNi00Y2UyLTgzZjMtYWE3NjlkOTM2YTJmIiwidCI6IjNmNjRiY2NiLTI3MjItNDJlNS1iNWNhLTcxYjIwNjA0NWQ4NyJ9) 

**Data Modelling**

Automatically, power BI created the related tables which gave a star schema model. The product table is the dimension table. The work order table was connected to work order routing using workorderID, while product ID/Component ID joined the product and bill of materials table. Other relationships can be seen below. 

![image](https://github.com/Adesoyin/Product_Production-Project/assets/123065894/efca2547-cbb8-483a-8640-9ace7d3d19c3)


**Report Pages**

**Overview Page**

This page shows the summary of the data which includes the product, work order and workorderrouting information in total. 
1.	The actual cost spent was the same as the total planned cost at almost $112,000 for 339,000 distinct products. Out of the 138,000 ordered quantities, 383 were scrapped and took 13 days for the work order routing on average. 
2.	The page can be filtered to select month, year, quarter, product class and colour interested in. The top 10 products by the actual cost were shown and the most scrapped products which can help management to assess the efficiency of production processes, identify areas of improvement, and set performance targets for continuous enhancement.
 
![image](https://github.com/Adesoyin/Product_Production-Project/assets/123065894/0dfd5c28-ba24-4503-8d72-32cda1d3a305)


**Product Page**

The analysis of the Product Manufacturing page provides detailed insights into each product, categorized by class and color filter. The page includes information on 38 subcategories of products that were manufactured within an average time of less than 2 days. Additionally, a significant increase of +50% in the percentage variance of the list cost from the standard cost is observed. This bottleneck in cost variance should be duly acknowledged by the performance manager for further consideration and action.
 
 ![image](https://github.com/Adesoyin/Product_Production-Project/assets/123065894/52b64c9a-d351-4e9b-b583-e214e026d49e)


**Analysis of Material Costs and Production Efficiency in Manufacturing**

This report focuses on analyzing material costs and production efficiency in a manufacturing company. It examines the assembly of 230 materials with 325 components, taking an average of 17 days for assembly. The analysis reveals monthly trends, with March having the highest material assembly numbers and October the lowest. Additionally, component usage shows a peak in June and a decline in November, possibly influenced by factors affecting efficiency and productivity during the year-end period. To address this, I will suggest the need for increased worker motivation and encouragement.

By studying material costs and production efficiency, the company can identify cost-saving opportunities and optimize resource allocation. Monthly analysis helps in understanding demand patterns and aligning production and inventory management strategies accordingly. Component usage trends highlight areas for optimization and cost reduction while considering seasonal impacts allows the company to mitigate efficiency declines during year-end months. Encouraging worker motivation through recognition, incentives, and a positive work environment can improve overall efficiency, reduce production time, and maximize output.

In summary, this report emphasizes the importance of analyzing material costs, production efficiency, and seasonal trends in the manufacturing industry. Understanding these factors enables the company to make informed decisions regarding resource allocation, production planning, and worker motivation. By optimizing operations and addressing productivity challenges, the company can enhance profitability, meet customer demands, and maintain a competitive edge in the market.
 
 ![image](https://github.com/Adesoyin/Product_Production-Project/assets/123065894/a459612a-3974-44f0-989d-f4ed68a47952)


**Production WorkOrder**

In the year 2013, a total of 210 products were worked on, but unfortunately, 5000 quantities had to be scrapped for various reasons. Analyzing the month-on-month trend of orders, it was observed that the ember months had the lowest order volumes. To compare orders between the current and previous year, a side-by-side visualization of the two periods was presented, highlighting the percentage increase or decline in orders. Notably, there was a significant decline of -461% in orders during February compared to the previous year.

To identify areas for improvement within the company, a visualization was created to showcase the top 5 stocked and scrapped orders by product. This allows for a clear understanding of which products need improvement and attention. Additionally, by interacting with the data, it becomes possible to identify any products that may be causing excessive stress on the workers, which can then be addressed and improved upon.

**Recommendation:** 

Based on the analysis, it is recommended that the company focuses on reducing the quantity of scrapped products by investigating the reasons behind the scrapping and implementing measures to address them. The decline in orders during February compared to the previous year requires further investigation to identify the underlying causes and implement strategies to boost order volumes during that period. Furthermore, the company should prioritize improving the top 5 stocked and scrapped products by identifying potential bottlenecks in the production process, enhancing quality control measures, and fostering collaboration between different departments involved in the manufacturing process. By addressing these areas and providing necessary support to workers, the company can optimize production efficiency, reduce waste, and enhance overall performance.
 
![image](https://github.com/Adesoyin/Product_Production-Project/assets/123065894/aaa8c322-471e-4b77-b776-35c7da3630b0)


**Production WorkOrder Routing**

The OrderRouting analysis involved examining 7 different locations and the corresponding number of orders using a Treemap visual representation. Out of the 149 products routed to these locations, the actual delivery time exceeded the scheduled time by 1 day, while the actual cost matched the planned cost. However, a time trend analysis revealed an overall increase in actual costs per month over different years, with a significant decline observed in June 2014. 

**Recommendation**

To identify cost-saving measures, it is recommended to investigate the location with the highest actual cost and implement strategies to reduce expenses and improve efficiency in that area.
 
![image](https://github.com/Adesoyin/Product_Production-Project/assets/123065894/f85d8d56-31d9-41af-aa98-b2287f8023e6)




<img width="604" alt="image" src="https://github.com/Adesoyin/Product_Production-Project/assets/123065894/cac6b3b9-3ffd-47cb-b0f0-e903b83b12c2">
