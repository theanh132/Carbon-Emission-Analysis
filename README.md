# Carbon Emission Analysis

![image](https://github.com/theanh132/Carbon-Emission-Analysis/blob/main/cover.jpg)

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

Looking at the table, we can see some manufacturing industries that affect the environment such as Electrical Equipment and Machinery, Automobiles & Components, Materials

**What are the industries with the highest contribution to carbon emissions?**

> SELECT i.industry_group,SUM(carbon_footprint_pcf) AS total_pcf
> FROM product_emissions AS p
> JOIN industry_groups AS i
> ON p.industry_group_id = i.id
> GROUP BY i.industry_group
> ORDER BY SUM(carbon_footprint_pcf) DESC

| industry_group                                                         | total_pcf | 
| ---------------------------------------------------------------------: | --------: | 
| Electrical Equipment and Machinery                                     | 9801558   | 
| Automobiles & Components                                               | 2582264   | 
| Materials                                                              | 577595    | 
| Technology Hardware & Equipment                                        | 363776    | 
| Capital Goods                                                          | 258712    | 
| "Food, Beverage & Tobacco"                                             | 111131    | 
| "Pharmaceuticals, Biotechnology & Life Sciences"                       | 72486     | 
| Chemicals                                                              | 62369     | 
| Software & Services                                                    | 46544     | 
| Media                                                                  | 23017     | 
| Energy                                                                 | 10774     | 
| "Forest and Paper Products - Forestry, Timber, Pulp and Paper, Rubber" | 8909      | 
| "Mining - Iron, Aluminum, Other Metals"                                | 8181      | 
| Consumer Durables & Apparel                                            | 7309      | 
| Commercial & Professional Services                                     | 5265      | 
| Containers & Packaging                                                 | 2988      | 
| Tires                                                                  | 2022      | 
| Food & Staples Retailing                                               | 1481      | 
| "Consumer Durables, Household and Personal Products"                   | 931       | 
| Telecommunication Services                                             | 418       | 
| "Textiles, Apparel, Footwear and Luxury Goods"                         | 387       | 
| Utilities                                                              | 244       | 
| Trading Companies & Distributors and Commercial Services & Supplies    | 239       | 
| Food & Beverage Processing                                             | 141       | 
| Gas Utilities                                                          | 122       | 
| Semiconductors & Semiconductor Equipment                               | 54        | 
| Retailing                                                              | 30        | 
| Semiconductors & Semiconductors Equipment                              | 3         | 
| Tobacco                                                                | 1         | 
| Household & Personal Products                                          | 0         | 

![image](https://github.com/theanh132/Carbon-Emission-Analysis/blob/main/A%CC%89nh%20chu%CC%A3p%20ma%CC%80n%20hi%CC%80nh%202024-07-22%20115044.png)
Most of the pcf index focuses on industries such as Electrical Equipment and Machinery, Automobiles & Components, Materials with the highest pcf level of over 300,000, the highest pcf is Electrical Equipment and Machinery with over 9000,000 pcf and some other industries such as Energy, Personal Products pcf amount is insignificant at less than 11,000

**What are the companies with the highest contribution to carbon emissions?**

> SELECT c.company_name,SUM(carbon_footprint_pcf) AS total_pcf
> FROM product_emissions AS p
> JOIN companies AS c
> ON p.company_id = c.id
> GROUP BY c.company_name
> ORDER BY SUM(carbon_footprint_pcf) DESC

| company_name                                   | total_pcf | 
| ---------------------------------------------: | --------: | 
| "Gamesa Corporación Tecnológica, S.A."         | 9778464   | 
| Daimler AG                                     | 1594300   | 
| Volkswagen AG                                  | 655960    | 
| "Mitsubishi Gas Chemical Company, Inc."        | 212016    | 
| "Hino Motors, Ltd."                            | 191687    | 
| Arcelor Mittal                                 | 167007    | 
| Weg S/A                                        | 160655    | 
| General Motors Company                         | 137007    | 
| "Lexmark International, Inc."                  | 132012    | 
| "Daikin Industries, Ltd."                      | 105600    | 
| CJ Cheiljedang                                 | 94817     | 
| LG Chem Ltd                                    | 91926     | 
| Waters Corporation                             | 72486     | 
| Xerox Corporation                              | 72051     | 
| Akzo Nobel                                     | 70417     | 
| Quanta Computer                                | 58217     | 
| "Ricoh Co., Ltd."                              | 35505     | 
| NEC Corporation                                | 23858     | 
| Bloomberg                                      | 22684     | 
| Metsä Board                                    | 21533     | 
| "Fuji Xerox Co., Ltd."                         | 21364     | 
| Hewlett-Packard                                | 20123     | 
| "Kuraray Co., Ltd."                            | 20000     | 
| Alcoa Corp.                                    | 19551     | 
| Dell Inc.                                      | 18209     | 
| Tata Steel                                     | 15766     | 
| "Konica Minolta, Inc."                         | 11160     | 
| "Hitachi, Ltd."                                | 9328      | 
| Tata Chemicals                                 | 8808      | 
| Sappi                                          | 8142      | 
| Sanden                                         | 7811      | 
| "Compañía Española de Petróleos, S.A.U. CEPSA" | 6999      | 
| Smurfit Kappa Group PLC                        | 5130      | 
| Tennant Company                                | 5124      | 
| "Casio Computer Co., Ltd."                     | 4688      | 
| Braskem S/A                                    | 4432      | 
| "Yokohama Rubber Company, Limited"             | 4160      | 
| Associated British Foods                       | 3900      | 
| Steelcase                                      | 3770      | 
| MAGOTTEAUX                                     | 3500      | 
| MUNTONS PLC                                    | 3470      | 
| NCP ALCOHOLS                                   | 3299      | 
| Ajinomoto Co.Inc.                              | 3292      | 
| "CNX Coal Resources, LP"                       | 3025      | 
| Stonyfield Farm Inc                            | 2721      | 
| Qisda                                          | 2562      | 
| Cabot Corporation                              | 2280      | 
| Lafarge S.A.                                   | 2204      | 
| "Cisco Systems, Inc."                          | 1751      | 
| Empresas CMPC                                  | 1555      | 
| Herman Miller                                  | 1490      | 
| Trinseo LLC                                    | 1484      | 
| Trelleborg AB                                  | 1409      | 
| Electrolux                                     | 1227      | 
| Holmen                                         | 1083      | 
| Fujitsu Ltd.                                   | 970       | 
| WOLF                                           | 948       | 
| Mpact Limited                                  | 871       | 
| BillerudKorsnäs                                | 814       | 
| Delta Electronics                              | 765       | 
| Raizen                                         | 750       | 
| "Toppan Printing Co., Ltd."                    | 741       | 
| Levi Strauss & Co.                             | 728       | 
| PT Fajar Surya Wisesa Tbk                      | 721       | 
| MITIE Group                                    | 680       | 
| Acbel Polytech Inc                             | 488       | 
| BlackBerry Limited                             | 382       | 
| BT Group                                       | 366       | 
| OMRON Corporation                              | 366       | 
| "Osaka Gas Co., Ltd."                          | 366       | 
| AVK                                            | 352       | 
| Perfection Bakeries Inc.                       | 343       | 
| Agraz                                          | 341       | 
| Technicolor SA                                 | 333       | 
| Crimidesa                                      | 320       | 
| "Stanley Black & Decker, Inc."                 | 290       | 
| Compal Electronics                             | 289       | 
| SunPower Corporation                           | 281       | 
| "Interface, Inc."                              | 259       | 
| Johnson Matthey                                | 251       | 
| Brambles                                       | 239       | 
| PURECIRCLE USA                                 | 235       | 
| "Elitegroup computer systems co., Ltd."        | 215       | 
| Pacific Coast Producers                        | 187       | 
| KNOLL INC                                      | 146       | 
| Innolux Corporation                            | 145       | 
| Canon Inc.                                     | 128       | 
| Coway Co Ltd                                   | 126       | 
| Clariant AG                                    | 120       | 
| Bridgestone Corporation                        | 118       | 
| Schneider Electric                             | 118       | 
| Maxxis International                           | 106       | 
| Intel Corporation                              | 100       | 
| Nokia Group                                    | 96        | 
| Molson Coors Brewing Company                   | 90        | 
| HUMAX ELECTRONICS CO LTD                       | 79        | 
| SHENYANG DONGRUI                               | 76        | 
| Humanscale Corporation                         | 74        | 
| Azbil Corporation                              | 67        | 
| Philips & Lite-On Digital Solutions Corp.      | 52        | 
| DRAGON WILL ENTERPRISE                         | 50        | 
| Ingenico                                       | 50        | 
| Motorola Mobility                              | 30        | 
| "Staples, Inc."                                | 30        | 
| Quanta Storage Inc.                            | 28        | 
| "Autodesk, Inc."                               | 22        | 
| CONTRAF-NICOTEX-TOBACCO GmbH                   | 17        | 
| "Shaw Industries Group, Inc."                  | 15        | 
| Barilla Holding SpA                            | 15        | 
| LG Electronics                                 | 14        | 
| Syngenta AG                                    | 13        | 
| "Mitsui Mining & Smelting Co., Ltd."           | 12        | 
| Chunghwa Picture Tubes Ltd                     | 12        | 
| Darfon Electronics Corp                        | 11        | 
| Wistron Corp                                   | 9         | 
| Kellogg Company                                | 8         | 
| Danone                                         | 8         | 
| Solvay S.A.                                    | 8         | 
| Logitech International SA                      | 8         | 
| Miquel Y Costas                                | 6         | 
| "PepsiCo, Inc."                                | 6         | 
| MediaTek                                       | 4         | 
| ZHEJIANG WANFENG AUTO WHEEL CO LTD             | 3         | 
| SK Hynix                                       | 3         | 
| Tata Steel Europe                              | 3         | 
| Radius Systems                                 | 3         | 
| Cargill                                        | 2         | 
| Air Liquide                                    | 2         | 
| BORMIOLI LUIGI                                 | 2         | 
| Georg Fischer                                  | 2         | 
| Bumble Bee Foods LLC                           | 1         | 
| MI (Michaelleides)                             | 1         | 
| "Coca-Cola Enterprises, Inc."                  | 1         | 
| CartOne S.r.l.                                 | 1         | 
| "YONYU Plastics (Shanghai) Co.,Ltd"            | 0         | 
| Martin Bauer GmbH                              | 0         | 
| Owens-Illinois                                 | 0         | 
| SGD Group                                      | 0         | 
| Coca-Cola HBC AG                               | 0         | 
| Times Microwave Systems                        | 0         | 
| CNX Resources                                  | 0         | 
| Nestlé                                         | 0         | 
| TETRA PAK                                      | 0         | 
| Fabrica de Tapas Bavaria                       | 0         | 
| Retal                                          | 0         | 

Topping the list "Gamesa Corporación Tecnológica, S.A." One job is in the field of wind power, followed by Volkswagen AG, a famous car manufacturer in Germany, and the rest are companies in other fields such as Services, Personal Product, etc.

