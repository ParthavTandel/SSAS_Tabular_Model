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
<img width="682" alt="ProductSubCategory" src="https://user-images.githubusercontent.com/118220804/212960152-edda48fe-d851-44c6-8d64-bbe3b4322723.png">

Step 4: Create Measures. 

