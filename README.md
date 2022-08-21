# Zomato-data-analysis-with-SQL

/* Extrat all the data*/
SELECT * from ZomatoData;

/*DISTINCT List CountryCode*/                      
SELECT DISTINCT CountryCode FROM ZomatoData   
ORDER by CountryCode ASC;

/* DISTINCT lsit of country names served by restaurant*/
SELECT DISTINCT Country, RestaurantName FROM ZomatoData
INNER JOIN CountryTable                                  /*Join two tables*/
on ZomatoData.CountryCode = CountryTable.CountryCode;    /*Join two tables*/

/*Summarize total no. of distinct countries*/
SELECT count(DISTINCT Country) AS 'TotalCountries' FROM CountryTable;

/*List of distinct combination of country & city*/
SELECT DISTINCT Country, City 
FROM ZomatoData, CountryTable
WHERE ZomatoData.CountryCode = CountryTable.CountryCode;

/*How many restaurants in each country
Sort data by the no. of restaurants*/
SELECT CountryTable.Country, Count(CountryTable.Country) AS 'Total Restaurants'
FROM ZomatoData, CountryTable
WHERE ZomatoData.CountryCode = CountryTable.CountryCode
GROUP BY Country
ORDER BY Count(CountryTable.Country) DESC; /* Or you can simply write sequence of table no.(2)*/

/*Find no. of restaurants in each country and city*/
SELECT CountryTable.Country, City, Count(CountryTable.Country) 
AS 'Total Restaurants'
FROM ZomatoData, CountryTable
WHERE ZomatoData.CountryCode = CountryTable.CountryCode
GROUP BY Country, City
ORDER BY Count(CountryTable.Country) DESC;

/*Find the top 5 countries with highest no. of zomato listed of restaurants*/
SELECT CountryTable.Country, Count(CountryTable.Country) AS 'Total Restaurants'
FROM ZomatoData, CountryTable
WHERE ZomatoData.CountryCode = CountryTable.CountryCode
GROUP BY Country
ORDER BY 2 DESC
LIMIT 5;

/*List the cities and RestaurantName with avg rating of more than 4.5*/
SELECT DISTINCT City, RestaurantName
FROM ZomatoData
WHERE Rating > 4.5;

/* Find the top 2 countries with rating more than 4.5*/
SELECT Country, avg(rating) as 'Ratings'
FROM ZomatoData, CountryTable
WHERE ZomatoData.CountryCode=CountryTable.CountryCode And Rating > 4.5
GROUP BY Country
ORDER BY 2 DESC
LIMIT 2;
