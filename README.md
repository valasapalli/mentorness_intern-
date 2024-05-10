SELECT 
    COUNT(*) AS null_count
FROM 
    corona_data
WHERE 
    column_name IS NULL;
If NULL values are present, update them with zeros for all columns.
sql
Copy code
UPDATE 
    corona_data
SET 
    column_name = 0
WHERE 
    column_name IS NULL;
Check total number of rows
sql
Copy code
SELECT 
    COUNT(*) AS total_rows
FROM 
    corona_data;
Check what is start_date and end_date
sql
Copy code
SELECT 
    MIN(start_date) AS start_date,
    MAX(end_date) AS end_date
FROM 
    corona_data;
Number of months present in dataset
sql
Copy code
SELECT 
    COUNT(DISTINCT DATE_FORMAT(start_date, '%Y-%m')) AS num_months
FROM 
    corona_data;
Find monthly average for confirmed, deaths, recovered
sql
Copy code
SELECT 
    DATE_FORMAT(start_date, '%Y-%m') AS month_year,
    AVG(confirmed) AS avg_confirmed,
    AVG(deaths) AS avg_deaths,
    AVG(recovered) AS avg_recovered
FROM 
    corona_data
GROUP BY 
    month_year;
Find most frequent value for confirmed, deaths, recovered each month
sql
Copy code
SELECT 
    DATE_FORMAT(start_date, '%Y-%m') AS month_year,
    MAX(confirmed) AS most_frequent_confirmed,
    MAX(deaths) AS most_frequent_deaths,
    MAX(recovered) AS most_frequent_recovered
FROM 
    corona_data
GROUP BY 
    month_year;
Find minimum values for confirmed, deaths, recovered per year
sql
Copy code
SELECT 
    YEAR(start_date) AS year,
    MIN(confirmed) AS min_confirmed,
    MIN(deaths) AS min_deaths,
    MIN(recovered) AS min_recovered
FROM 
    corona_data
GROUP BY 
    year;
Find maximum values of confirmed, deaths, recovered per year
sql
Copy code
SELECT 
    YEAR(start_date) AS year,
    MAX(confirmed) AS max_confirmed,
    MAX(deaths) AS max_deaths,
    MAX(recovered) AS max_recovered
FROM 
    corona_data
GROUP BY 
    year;
The total number of cases of confirmed, deaths, recovered each month
sql
Copy code
SELECT 
    DATE_FORMAT(start_date, '%Y-%m') AS month_year,
    SUM(confirmed) AS total_confirmed,
    SUM(deaths) AS total_deaths,
    SUM(recovered) AS total_recovered
FROM 
    corona_data
GROUP BY 
    month_year;
Check how coronavirus spread out with respect to confirmed cases (total confirmed cases, their average, variance & STDEV)
sql
Copy code
SELECT 
    COUNT(*) AS total_cases,
    AVG(confirmed) AS average_confirmed,
    VARIANCE(confirmed) AS variance_confirmed,
    STDDEV(confirmed) AS stdev_confirmed
FROM 
    corona_data;
Check how coronavirus spread out with respect to death cases per month (total confirmed cases, their average, variance & STDEV)
sql
Copy code
SELECT 
    DATE_FORMAT(start_date, '%Y-%m') AS month_year,
    COUNT(*) AS total_cases,
    AVG(deaths) AS average_deaths,
    VARIANCE(deaths) AS variance_deaths,
    STDDEV(deaths) AS stdev_deaths
FROM 
    corona_data
GROUP BY 
    month_year;
Check how coronavirus spread out with respect to recovered cases (total confirmed cases, their average, variance & STDEV)
sql
Copy code
SELECT 
    COUNT(*) AS total_cases,
    AVG(recovered) AS average_recovered,
    VARIANCE(recovered) AS variance_recovered,
    STDDEV(recovered) AS stdev_recovered
FROM 
    corona_data;
Find Country having the highest number of confirmed cases
sql
Copy code
SELECT 
    country,
    MAX(confirmed) AS highest_confirmed
FROM 
    corona_data;
Find Country having the lowest number of death cases
sql
Copy code
SELECT 
    country,
    MIN(deaths) AS lowest_deaths
FROM 
    corona_data;
Find top 5 countries having the highest recovered cases
sql
Copy code
SELECT 
    country,
    SUM(recovered) AS total_recovered
FROM 
    corona_data
GROUP BY 
    country
ORDER BY 
    total_recovered DESC
LIMIT 5;
These queries should help you perform the necessary data analysis on your COVID-19 dataset. 
