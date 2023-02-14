# SSAS_Tabular_Model
Tabular Model for Internet Sales using AdvantureWorks 2019 DW and SSAS and SSMS

<img width="698" alt="Diagram" src="https://user-images.githubusercontent.com/118220804/212950628-8d419f3e-0c3c-4e73-8a50-214045854e0b.png">

<img width="298" alt="Explorer" src="https://user-images.githubusercontent.com/118220804/212952400-0a02427f-568f-4ea3-99a2-e717469cb5ab.png">

Step 1: Create new tabular model and import data from AdvantureWorks 2019 DW database. Remove Spanish, French and Chinese columns. 

Step 2: Mark DimDate table as a Data table and create following relationships.

<img width="433" alt="Relationships" src="https://user-images.githubusercontent.com/118220804/212956834-4b8e4fc3-721b-4677-966b-40241a9bcca0.png">

Step 3: Create calculated columns. 

In DimProduct table,

ProductSubCategoryName =RELATED(DimProductSubcategory[EnglishProductSubcategoryName])

ProductCategoryName =RELATED(DimProductCategory[EnglishProductCategoryName]) 

In Fact table, Margin =[SalesAmount]-[TotalProductCost].

In DimDate table, Month_short =LEFT(DimDate[EnglishMonthName],3)

<img width="682" alt="ProductSubCategory" src="https://user-images.githubusercontent.com/118220804/212960152-edda48fe-d851-44c6-8d64-bbe3b4322723.png">

Step 4: Create Measures.

Created several sum measures like Total Sales, Total Units, Total Margin, Total Product Cost and Total Tax Amount.

PreviousQuarterSales:=CALCULATE([InternetTotalSales], PREVIOUSQUARTER(DimDate[Date]))

CurrentQuarterSales:=TOTALQTD([InternetTotalSales], DimDate[Date]) 

same way created PreviousQuarterMargin and CurrentQuarterMargin.

Created KPI Measure for 

InternetCurrentQuarterSalesPerformance:= IF([InternetPreviousQuarterSalesProportionToQTD]<>0,([InternetCurrentQuarterSales]-[InternetPreviousQuarterSalesProportionToQTD])/[InternetPreviousQuarterSalesProportionToQTD],0)

InternetCurrentQuarterMarginPerformance:=IF([InternetPreviousQuarterMarginProportionToQTD]<>0,([InternetCurrentQuarterMargin]-[InternetPreviousQuarterMarginProportionToQTD])/[InternetPreviousQuarterMarginProportionToQTD],0)

Step 5: Created KPI based on above measures with the target value of 10% (0.1) for Sales and 20% (0.2) for Margin

<img width="488" alt="KPI" src="https://user-images.githubusercontent.com/118220804/218546771-4383af4e-5e96-402a-a82c-fafd45dd4fc5.png">

Step 6: Created Perspective, hierarchies for Product (Product Category -> Sub category -> Model -> Product name) and For Calender (Year -> Quarter -> Month -> Day)

<img width="486" alt="Hierarchies" src="https://user-images.githubusercontent.com/118220804/218546547-d9ac13eb-cce9-4c31-b074-e30a60a857e0.png">

Step 7: Created Partitions for year 2011 to 2014 in Fact table

<img width="427" alt="Partition" src="https://user-images.githubusercontent.com/118220804/218546087-33a9fa43-381e-4b78-b8b2-d0a138ce2def.png">

Build and deployed tabular model on SQL Server Analysis Services (We will use this model for visualization later)






