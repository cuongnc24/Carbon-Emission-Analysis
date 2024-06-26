# Carbon-Emission-Analysis

## Description of the task
This report aims to analyze carbon emissions to examine the carbon footprint across various industries, and to identify sectors with the highest levels of emissions by analyzing them across countries and years, as well as to uncover trends.

## Overview of 4 tables
### Table 1 : 'product_emissions'

SQL Code
```
select * from product_emissions limit 3;
```

| id           | company_id | country_id | industry_group_id | year | product_name                                                    | weight_kg | carbon_footprint_pcf | upstream_percent_total_pcf | operations_percent_total_pcf | downstream_percent_total_pcf | 
| -----------: | ---------: | ---------: | ----------------: | ---: | --------------------------------------------------------------: | --------: | -------------------: | -------------------------: | ---------------------------: | ---------------------------: | 
| 10056-1-2014 | 82         | 28         | 2                 | 2014 | Frosted Flakes(R) Cereal                                        | 0.7485    | 2                    | 57.50                      | 30.00                        | 12.50                        | 
| 10056-1-2015 | 82         | 28         | 15                | 2015 | "Frosted Flakes, 23 oz, produced in Lancaster, PA (one carton)" | 0.7485    | 2                    | 57.50                      | 30.00                        | 12.50                        | 
| 10222-1-2013 | 83         | 28         | 8                 | 2013 | Office Chair                                                    | 20.68     | 73                   | 80.63                      | 17.36                        | 2.01                         |         

### Table 2: industry_groups

SQL Code
```
select * from industry_groups limit 3;
```

| id | industry_group                                                         | 
| -: | ---------------------------------------------------------------------: | 
| 1  | "Consumer Durables, Household and Personal Products"                   | 
| 2  | "Food, Beverage & Tobacco"                                             | 
| 3  | "Forest and Paper Products - Forestry, Timber, Pulp and Paper, Rubber" |             | 17.36                        | 2.01                         |         

### Table 3: companies

SQL Code
```
select * from companies limit 3;
```

| id | company_name               | 
| -: | -------------------------: | 
| 1  | "Autodesk, Inc."           | 
| 2  | "Casio Computer Co., Ltd." | 
| 3  | "Cisco Systems, Inc."      |         

### Table 4: countries

SQL code
```
select * from countries limit 3;
```

| id | country_name | 
| -: | -----------: | 
| 1  | Australia    | 
| 2  | Belgium      | 
| 3  | Brazil       |         

## RESEARCH

### Problem 1: Which products contribute the most to carbon emissions?
#### 	 Wind Turbine G128 5 Megawats is contribute the most to carbon emissions

SQL code
```
SELECT id, product_name, SUM(carbon_footprint_pcf) AS Total_PCF
FROM product_emissions
	GROUP BY id, product_name
	ORDER BY Total_PCF DESC
LIMIT 5;
```

| id           | product_name                 | Total_PCF | 
| -----------: | ---------------------------: | --------: | 
| 22917-4-2015 | Wind Turbine G128 5 Megawats | 3718044   | 
| 22917-5-2015 | Wind Turbine G132 5 Megawats | 3276187   | 
| 22917-3-2015 | Wind Turbine G114 2 Megawats | 1532608   | 
| 22917-2-2015 | Wind Turbine G90 2 Megawats  | 1251625   | 
| 12134-8-2017 | TCDE                         | 198150    |         

### Problem 2: What are the industry groups of these products?
#### 4/5 product contribute the most to carbon emissions are from Electrical Equipment and Machinery

SQL Code
```
select product_emissions.industry_group_id, product_emissions.product_name, industry_groups.industry_group
from product_emissions
join industry_groups
	on  product_emissions.industry_group_id=  industry_groups.id 
	where product_emissions.id in ("22917-4-2015", "22917-5-2015","22917-3-2015","22917-2-2015", "12134-8-2017");
```

| industry_group_id | product_name                 | industry_group                     | 
| ----------------: | ---------------------------: | ---------------------------------: | 
| 13                | Wind Turbine G90 2 Megawats  | Electrical Equipment and Machinery | 
| 13                | Wind Turbine G114 2 Megawats | Electrical Equipment and Machinery | 
| 13                | Wind Turbine G128 5 Megawats | Electrical Equipment and Machinery | 
| 13                | Wind Turbine G132 5 Megawats | Electrical Equipment and Machinery | 
| 19                | TCDE                         | Materials                          | 
| 19                | TCDE                         | Materials                          |            

### Problem 3: What are the industries with the highest contribution to carbon emissions?
## Result

SQL Code
```
SELECT product_emissions.industry_group_id, industry_groups.industry_group, SUM(carbon_footprint_pcf) AS sum_pcf
FROM product_emissions
	JOIN industry_groups 
	ON product_emissions.industry_group_id = industry_groups.id
GROUP BY product_emissions.industry_group_id
ORDER BY sum_pcf DESC LIMIT 10;
```

| industry_group_id | industry_group                                   | sum_pcf | 
| ----------------: | -----------------------------------------------: | ------: | 
| 13                | Electrical Equipment and Machinery               | 9801558 | 
| 7                 | Automobiles & Components                         | 2582264 | 
| 19                | Materials                                        | 577595  | 
| 25                | Technology Hardware & Equipment                  | 363776  | 
| 8                 | Capital Goods                                    | 258712  | 
| 2                 | "Food, Beverage & Tobacco"                       | 111131  | 
| 5                 | "Pharmaceuticals, Biotechnology & Life Sciences" | 72486   | 
| 9                 | Chemicals                                        | 62369   | 
| 24                | Software & Services                              | 46544   | 
| 20                | Media                                            | 23017   |      

### Problem 3: What are the companies with the highest contribution to carbon emissions?
Result

SQL code
```
SELECT product_emissions.company_id, companies.company_name, SUM(carbon_footprint_pcf) AS sum_pcf
FROM product_emissions
	JOIN companies
	ON product_emissions.company_id = companies.id
GROUP BY product_emissions.company_id
ORDER BY sum_pcf DESC LIMIT 10;
```

| company_id | company_name                            | sum_pcf | 
| ---------: | --------------------------------------: | ------: | 
| 10         | "Gamesa Corporación Tecnológica, S.A."  | 9778464 | 
| 61         | Daimler AG                              | 1594300 | 
| 139        | Volkswagen AG                           | 655960  | 
| 17         | "Mitsubishi Gas Chemical Company, Inc." | 212016  | 
| 11         | "Hino Motors, Ltd."                     | 191687  | 
| 34         | Arcelor Mittal                          | 167007  | 
| 141        | Weg S/A                                 | 160655  | 
| 71         | General Motors Company                  | 137007  | 
| 16         | "Lexmark International, Inc."           | 132012  | 
| 7          | "Daikin Industries, Ltd."               | 105600  |         


### Problem 5: What are the countries with the highest contribution to carbon emissions?
## result

SQL Code
```
SELECT product_emissions.country_id, countries.country_name, SUM(carbon_footprint_pcf) AS sum_pcf
FROM product_emissions
	JOIN countries
	ON product_emissions.country_id = countries.id
GROUP BY product_emissions.country_id
ORDER BY sum_pcf DESC LIMIT 10;
```
| country_id | country_name | sum_pcf | 
| ---------: | -----------: | ------: | 
| 23         | Spain        | 9786130 | 
| 10         | Germany      | 2251225 | 
| 16         | Japan        | 653237  | 
| 28         | USA          | 518381  | 
| 22         | South Korea  | 186965  | 
| 3          | Brazil       | 169337  | 
| 18         | Luxembourg   | 167007  | 
| 20         | Netherlands  | 70417   | 
| 26         | Taiwan       | 62875   | 
| 12         | India        | 24574   |         

### Problem 6: What is the trend of carbon footprints (PCFs) over the years?

#### result

SQL Code
```
select year, 
	ROUND(avg(upstream_percent_total_pcf),2) as avg_upstream,
	ROUND(avg(operations_percent_total_pcf),2) as avg_operations,
	ROUND(avg(downstream_percent_total_pcf),2) as avg_downstream
from product_emissions
group by year
order by year ASC;
```

| year | avg_upstream | avg_operations | avg_downstream | 
| ---: | -----------: | -------------: | -------------: | 
| 2013 | 29.53        | 13.47          | 20.81          | 
| 2014 | 20.27        | 7.86           | 10.86          | 
| 2015 | 22.49        | 10.94          | 16.77          | 
| 2016 | 15.74        | 7.92           | 9.54           | 
| 2017 | 16.96        | 12.26          | 20.77          |         

### Problem 7: Which industry groups has demonstrated the most notable decrease in carbon footprints (PCFs) over time?

