Hannah Squier & Chris Goodson

# assignment_sql_taste
A delicious appetizer of SQL-ey goodness


## Queries

### Example

```
SELECT *
  FROM tutorial.us_housing_units
  WHERE month = 1
```


10 results with information on all columns
 ```
 SELECT *
 FROM tutorial.us_housing_units
 LIMIT 10
```

Housing starts in the Midwest
```
SELECT midwest
FROM tutorial.us_housing_units
```


All housing starts in December since 1985
```
SELECT *
FROM tutorial.us_housing_units
WHERE month = 12 AND year >= 1985
```


All housing starts in the second half of the year since 1990
```
SELECT *
FROM tutorial.us_housing_units
WHERE month >= 6 AND year >= 1990
```



All rows where housing starts were above 30,000 in the South region
```
SELECT *
FROM tutorial.us_housing_units
WHERE south >= 30
```

The sum of housing starts across all regions for each row
```
SELECT *, (south + west + midwest + northeast) AS total
FROM tutorial.us_housing_units
```


All rows where the sum of all housing starts is above 70,000 Note: You can't
use an alias in a WHERE clause.
```
SELECT *, (south + west + midwest + northeast) AS total
FROM tutorial.us_housing_units
WHERE (south + west + midwest + northeast) > 70
```


All rows where the sum of all housing starts is between 50-80k
```
SELECT *, (south + west + midwest + northeast) AS total
FROM tutorial.us_housing_units
WHERE (south + west + midwest + northeast) BETWEEN 50 AND 80
```


The average of all housing starts across all regions for each row

```
SELECT *, (south + west + midwest + northeast)/4 AS average
FROM tutorial.us_housing_units
```


All rows where the housing starts in the South are above the sum of the other
three regions

```
SELECT *
FROM tutorial.us_housing_units
WHERE south > (west + midwest + northeast)/3
```


The percentage of housing starts that occur in each region since 1990 Note:
Use an alias to title the new columns appropriately

```
SELECT *,
  (south / (south + west + midwest + northeast)) * 100 as "South Percentage",
  (west / (south + west + midwest + northeast)) * 100 as "West Percentage",
  (midwest / (south + west + midwest + northeast)) * 100 as "Midwest Percentage",
  (northeast / (south + west + midwest + northeast)) * 100 as "Northeast Percentage"

  FROM tutorial.us_housing_units


  WHERE year > 1990
```

tutorial.billboard_top_100_year_end

Note: Use single quotes ' instead of double quotes " for LIKE and similar queries since the Mode tool is very particular about its syntax. Double quotes are used to specify column names, so you might get a "column XYZ does not exist" error if you mess this up.



All rows where Elvis Presley had a song on the top 100 charts

```
SELECT*
FROM tutorial.billboard_top_100_year_end 
WHERE artist = 'Elvis Presley'
```


All rows where the artist's name contained "Tony" (not case sensitive)
```
SELECT *
FROM tutorial.billboard_top_100_year_end 
WHERE artist ILIKE '%tony%'
```


All rows where the song title contained the word "love" in any way
```
SELECT *
FROM tutorial.billboard_top_100_year_end 
WHERE song_name ILIKE '%love%'
```

All rows where the artist's name begins with the letter "A"
```
SELECT *
FROM tutorial.billboard_top_100_year_end 
WHERE artist LIKE 'A%'
```

The top 3 songs from each year between 1960-1969
```
SELECT *
FROM tutorial.billboard_top_100_year_end 
WHERE year_rank <= 3 AND year BETWEEN 1960 AND 1969
```


All rows where either Elvis Presley, The Rolling Stones, or Van Halen were the artist

```
SELECT *
FROM tutorial.billboard_top_100_year_end 
WHERE artist = 'Elvis Presley' OR artist = 'The Rolling Stones' OR artist = 'Van Halen'
```

Which artist has had the most appearances on the top 100 list?
```
SELECT artist, COUNT(*)
FROM tutorial.billboard_top_100_year_end 
GROUP BY artist
ORDER BY count DESC
```
Elvis Presley


Which artist has had the most #1 hits? How many?
```
SELECT  artist,  COUNT(*)
FROM tutorial.billboard_top_100_year_end 
WHERE year_rank = 1
GROUP BY artist
ORDER BY count DESC
```
BEATLES and Elvis Presley



All rows from 1970 where the songs were ranked 10-20th
```
SELECT  * 
FROM tutorial.billboard_top_100_year_end 
WHERE year_rank  BETWEEN 10 AND 20
AND year = 1970
```


All rows from the 1990's where Madonna was not ranked 10-100th
```
SELECT *
FROM tutorial.billboard_top_100_year_end 
WHERE  artist = 'Madonna' AND year_rank < 10 OR year_rank > 100
```



All rows from 1985 which do not include Madonna or Phil Collins in the group.
```
SELECT *
FROM tutorial.billboard_top_100_year_end 
WHERE  year = 1985 AND
     "group" NOT ILIKE '%Madonna%' 
    AND "group" NOT ILIKE '%Phil Collins%'
```

All number 1 songs in the data set.


All rows where the artist is not listed


All of Madonna's top 100 hits ordered by their ranking (1 to 100)


All of Madonna's top 100 hits ordered by their ranking within each year


Every number 1 song since 1990 followed by every number 2 song since 1990 and number 3 song since


1990. (Hint: Multiple ordering)
