# DataCamp Project: Analyze International Debt Statistics


Humans not only take debts to manage necessities. A country may also take debt to manage its economy. For example, infrastructure spending is one costly ingredient required for a country's citizens to lead comfortable lives. The World Bank is the organization that provides debt to countries.

In this project, you are going to analyze international debt data collected by The World Bank. The dataset contains information about the amount of debt (in USD) owed by developing countries across several categories. You are going to find the answers to the following questions:

- What is the number of distinct countries present in the database?
- What country has the highest amount of debt?
- What country has the lowest amount of repayments?

Below is a description of the table you will be working with:

## `international_debt` table

| Column | Definition | Data Type |
|-|-|-|
|country_name|Name of the country|`varchar`|
|country_code|Code representing the country|`varchar`|
|indicator_name|Description of the debt indicator|`varchar`|
|indicator_code|Code representing the debt indicator|`varchar`|
|debt|Value of the debt indicator for the given country (in current US dollars)|`float`|

You will execute SQL queries to answer three questions, as listed in the instructions.

```
SELECT COUNT(DISTINCT country_code) as total_distinct_countries 
FROM public.international_debt;
```
| total_distinct_countries |
|-|
| 125 |

```
SELECT country_name, SUM(debt) AS total_debt
FROM public.international_debt 
GROUP BY country_name
ORDER BY total_debt DESC
LIMIT 1;
```

| country_name | total_debt |
|-|-|
| China | 285793494734.2 |

```
SELECT 
    country_name, indicator_name, debt as lowest_repayment
FROM international_debt
WHERE debt = (SELECT 
                 min(debt)
             FROM international_debt
             WHERE indicator_code='DT.AMT.DLXF.CD') 
LIMIT 1;
```
| country_name | indicator_name | lowest_repayment | 
|-|-|-|
| Timor-Leste | PPG, multilateral (AMT, current US$) | 825000
