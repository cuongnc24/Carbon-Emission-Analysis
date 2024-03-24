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
