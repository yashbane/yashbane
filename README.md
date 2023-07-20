SELECT * FROM netflix.netflix_dataset;
DESCRIBE netflix_dataset;
SELECT COUNT(*) AS Count FROM netflix_dataset;
SELECT COUNT(*) AS MissingGenreCount
FROM netflix_dataset
WHERE director IS NULL;

SELECT type, COUNT(*) as COUNT
FROM netflix_dataset
GROUP by type;
use netflix;
SELECT country, COUNT(*) AS ProductionCount
FROM netflix_dataset
GROUP BY country
ORDER BY ProductionCount DESC
LIMIT 10;
SELECT country, count(*) as count
from netflix_dataset
where country != 'Not Given'
group by country DESC
limit 10;
select type, release_year, count(*) as made_this_year
from netflix_dataset
where release_year != 'Not Given'
or type != 'Not Given'
group by type, release_year
order by made_this_year desc;
SELECT release_year, AVG(duration) AS AverageDuration
FROM netflix_dataset
GROUP BY release_year
ORDER BY release_year;
SELECT director, COUNT(*) AS ContentCount
FROM netflix_dataset
GROUP BY director
ORDER BY ContentCount DESC
LIMIT 10;


use netflix;
SELECT DISTINCT listed_in
FROM netflix_dataset;

SELECT listed_in, count(*) as count
from netflix_dataset
where listed_in != 'Not Given'
group by listed_in;
SELECT type, 
       COUNT(*) AS TotalProductions,
       (COUNT(*) * 100.0) / SUM(COUNT(*)) OVER () AS Percentage
FROM netflix_dataset
GROUP BY type;
SELECT listed_in, COUNT(*) AS TotalProductions
FROM netflix_dataset
GROUP BY listed_in
ORDER BY TotalProductions DESC;
SELECT listed_in, SUM(duration) AS CumulativeDuration
FROM netflix_dataset
GROUP BY listed_in;
SELECT EXTRACT(MONTH FROM cast(date_added AS DATE)) AS Month,
       EXTRACT(YEAR FROM cast(date_added AS DATE)) AS Year,
       COUNT(*) AS ReleaseCount
FROM netflix_dataset
GROUP BY Month, Year
ORDER BY Year, Month;
SELECT EXTRACT(MONTH FROM date_added) AS month, EXTRACT(YEAR FROM date_added) AS year, COUNT(*) AS count
FROM netflix_dataset
GROUP BY month, year
ORDER BY year, month;
SELECT CASE WHEN EXTRACT(MONTH FROM date_added) IN (12, 1, 2) THEN 'Winter'
            WHEN EXTRACT(MONTH FROM date_added) IN (3, 4, 5) THEN 'Spring'
            WHEN EXTRACT(MONTH FROM date_added) IN (6, 7, 8) THEN 'Summer'
            WHEN EXTRACT(MONTH FROM date_added) IN (9, 10, 11) THEN 'Fall'
            ELSE 'Unknown'
       END AS season, COUNT(*) AS count
FROM netflix_dataset
GROUP BY season;
SELECT EXTRACT(MONTH FROM date_added) AS Month,
       EXTRACT(YEAR FROM date_added) AS Year,
       COUNT(*) AS ReleaseCount
FROM netflix_dataset
GROUP BY Month, Year
HAVING COUNT(*) = (
    SELECT MAX(ReleaseCount)
    FROM (
        SELECT COUNT(*) AS ReleaseCount
        FROM netflix_dataset
        GROUP BY EXTRACT(MONTH FROM date_added), EXTRACT(YEAR FROM date_added)
    ) AS subquery
);
SELECT EXTRACT(MONTH FROM date_added) AS month, EXTRACT(YEAR FROM date_added) AS year, COUNT(*) AS count
FROM netflix_dataset
GROUP BY month, year
ORDER BY count DESC
LIMIT 1;
SELECT listed_in, rating, COUNT(*) AS RatingCount
FROM netflix_dataset
GROUP BY listed_in, rating
ORDER BY listed_in, rating;
SELECT rating, AVG(duration) AS AverageDuration
FROM netflix_dataset
GROUP BY rating
ORDER BY rating;
SELECT listed_in, type, COUNT(*) AS CooccurrenceCount
FROM netflix_dataset
GROUP BY listed_in, type
HAVING COUNT(*) > 1
ORDER BY CooccurrenceCount DESC;
SELECT listed_in, AVG(duration) AS AverageDuration
FROM netflix_dataset
GROUP BY listed_in
ORDER BY AverageDuration DESC;
SELECT DISTINCT country
FROM netflix_dataset;
SELECT country, type, COUNT(*) AS ContentCount
FROM netflix_dataset
GROUP BY country, Type
ORDER BY country, Type;
SELECT country, AVG(duration) AS AverageDuration
FROM netflix_dataset
GROUP BY country
ORDER BY AverageDuration DESC;
