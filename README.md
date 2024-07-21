# Carbon Emission Analysis

![image](https://github.com/theanh132/Carbon-Emission-Analysis/commit/4d7837dfa91128a4f0982eed2e857dd4c07d4cf6)

This report aims to analyze carbon emissions to examine the carbon footprint across various industries. We aim to identify sectors with the highest levels of emissions by analyzing them across countries and years, as well as to uncover trends.

Carbon emissions play a crucial role in the environment, accounting for over 75% of global emissions and posing a significant environmental challenge. These emissions contribute to the accumulation of greenhouse gases in the atmosphere, leading to climate change, planetary warming, and involvement in various environmental disasters.

Through this analysis, we hope to gain an understanding of the environmental impact of different industries and contribute to making informed decisions in sustainable development.

## Data Source: Where Our Data Comes From
Our dataset is compiled from publicly available data from nature.com and encompasses the product carbon footprints (PCF) for various companies. PCFs represent the greenhouse gas emissions associated with specific products, quantified in CO2 (carbon dioxide equivalent).

## Data Structure
The dataset consists of 4 tables containing information regarding carbon emissions generated during the production of goods.
sample information table

**table 1: product_emissions**
> SELECT *
> FROM product_emissions
> LIMIT 5

| id           | company_id | country_id | industry_group_id | year | product_name                                                    | weight_kg | carbon_footprint_pcf | upstream_percent_total_pcf | operations_percent_total_pcf | downstream_percent_total_pcf | 
| -----------: | ---------: | ---------: | ----------------: | ---: | --------------------------------------------------------------: | --------: | -------------------: | -------------------------: | ---------------------------: | ---------------------------: | 
| 10056-1-2014 | 82         | 28         | 2                 | 2014 | Frosted Flakes(R) Cereal                                        | 0.7485    | 2                    | 57.50                      | 30.00                        | 12.50                        | 
| 10056-1-2015 | 82         | 28         | 15                | 2015 | "Frosted Flakes, 23 oz, produced in Lancaster, PA (one carton)" | 0.7485    | 2                    | 57.50                      | 30.00                        | 12.50                        | 
| 10222-1-2013 | 83         | 28         | 8                 | 2013 | Office Chair                                                    | 20.68     | 73                   | 80.63                      | 17.36                        | 2.01                         | 
| 10261-1-2017 | 14         | 16         | 25                | 2017 | Multifunction Printers                                          | 110       | 1488                 | 30.65                      | 5.51                         | 63.84                        | 
| 10261-2-2017 | 14         | 16         | 25                | 2017 | Multifunction Printers                                          | 110       | 1818                 | 25.08                      | 4.51  
| 70.41                        |

**table 2 : companies**

> SELECT *
> FROM companies
> LIMIT 5

| id | company_name                  | 
| -: | ----------------------------: | 
| 1  | "Autodesk, Inc."              | 
| 2  | "Casio Computer Co., Ltd."    | 
| 3  | "Cisco Systems, Inc."         | 
| 4  | "CNX Coal Resources, LP"      | 
| 5  | "Coca-Cola Enterprises, Inc." | 

**table 3: countries**

> SELECT *
> FROM countries
> LIMIT 5

| id | country_name | 
| -: | -----------: | 
| 1  | Australia    | 
| 2  | Belgium      | 
| 3  | Brazil       | 
| 4  | Canada       | 
| 5  | Chile        | 

**table 4 : industry_groups**

> SELECT *
> FROM industry_groups
> LIMIT 5

| id | industry_group                                                         | 
| -: | ---------------------------------------------------------------------: | 
| 1  | "Consumer Durables, Household and Personal Products"                   | 
| 2  | "Food, Beverage & Tobacco"                                             | 
| 3  | "Forest and Paper Products - Forestry, Timber, Pulp and Paper, Rubber" | 
| 4  | "Mining - Iron, Aluminum, Other Metals"                                | 
| 5  | "Pharmaceuticals, Biotechnology & Life Sciences"                       | 


## **let's find out**

**Which products contribute the most to carbon emissions?**


> SELECT p.product_name AS Product, p.carbon_footprint_pcf AS pcf,  c.country_name AS country
> FROM product_emissions AS p
> JOIN countries AS c
> ON p.country_id = c.id
> ORDER BY p.carbon_footprint_pcf DESC
> LIMIT 10

| Product                                                                                                                            | pcf     | country    | 
| ---------------------------------------------------------------------------------------------------------------------------------: | ------: | ---------: | 
| Wind Turbine G128 5 Megawats                                                                                                       | 3718044 | Spain      | 
| Wind Turbine G132 5 Megawats                                                                                                       | 3276187 | Spain      | 
| Wind Turbine G114 2 Megawats                                                                                                       | 1532608 | Spain      | 
| Wind Turbine G90 2 Megawats                                                                                                        | 1251625 | Spain      | 
| Land Cruiser Prado. FJ Cruiser. Dyna trucks. Toyoace.IMV def unit.                                                                 | 191687  | Japan      | 
| Retaining wall structure with a main wall (sheet pile): 136 tonnes of steel sheet piles and 4 tonnes of tierods per 100 meter wall | 167000  | Luxembourg | 
| TCDE                                                                                                                               | 99075   | Japan      | 
| TCDE                                                                                                                               | 99075   | Japan      | 
| Mercedes-Benz GLE (GLE 500 4MATIC)                                                                                                 | 91000   | Germany    | 
| Electric Motor                                                                                                                     | 87589   | Brazil     | 

Some typical products such as wind turbines have a capacity of more than 3,000,000 pcf, cars of big brands such as Toyota, Mercedes,... have a capacity of more than 90,000 pcf, some raw materials products are nearly 100,000 pcf

**What are the industry groups of these products?**

> SELECT p.product_name AS Product, i.industry_group
> FROM product_emissions AS p
> JOIN industry_groups AS i
> ON p.industry_group_id = i.id
> ORDER BY p.carbon_footprint_pcf DESC
> LIMIT 10

| Product                                                                                                                            | industry_group                     | 
| ---------------------------------------------------------------------------------------------------------------------------------: | ---------------------------------: | 
| Wind Turbine G128 5 Megawats                                                                                                       | Electrical Equipment and Machinery | 
| Wind Turbine G132 5 Megawats                                                                                                       | Electrical Equipment and Machinery | 
| Wind Turbine G114 2 Megawats                                                                                                       | Electrical Equipment and Machinery | 
| Wind Turbine G90 2 Megawats                                                                                                        | Electrical Equipment and Machinery | 
| Land Cruiser Prado. FJ Cruiser. Dyna trucks. Toyoace.IMV def unit.                                                                 | Automobiles & Components           | 
| Retaining wall structure with a main wall (sheet pile): 136 tonnes of steel sheet piles and 4 tonnes of tierods per 100 meter wall | Materials                          | 
| TCDE                                                                                                                               | Materials                          | 
| TCDE                                                                                                                               | Materials                          | 
| Mercedes-Benz GLE (GLE 500 4MATIC)                                                                                                 | Automobiles & Components           | 
| Electric Motor                                                                                                                     | Capital Goods                      | 





