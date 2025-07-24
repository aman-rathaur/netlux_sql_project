 business problem statement
 1. Count the number of Movies vs TV Shows
2. Find the most common rating for movies and TV shows
3. List all movies released in a specific year (e.g., 2020)
4. Find the top 5 countries with the most content on Netflix
5. Identify the longest movie
6. Find content added in the last 5 years
7. Find all the movies/TV shows by director 'Rajiv Chilaka'!
8. List all TV shows with more than 5 seasons
9. Count the number of content items in each genre
10.Find each year and the average numbers of content release in India on netflix. 
11. List all movies that are documentaries
overview
This project analyzes Netflix content using SQL queries.
It covers trends like movie vs TV show count, genre popularity, and top countries.
It also explores yearly content growth, ratings, and keyword-based filtering.
The dataset enables insights into global content distribution and user preference
 solution

1. the number of Movies vs TV Shows Count

SELECT 
  type, 
  COUNT(*) AS total_count
FROM 
  analysis
GROUP BY 
  type;
2. Find the most common rating for movies and TV shows
select rating,type ,count(*) as rating_count from analysis
group by rating,type
order by rating_count DESC
. 3 List all movies released in a specific year (e.g., 2020)
SELECT 
  title, 
  director, 
  country, 
  release_year, 
  rating, 
  duration
FROM 
  analysis
WHERE 
  type = 'Movie' 
  Find the top 5 countries with the most content on Netflix
 SELECT 
  country, 
  COUNT(*) AS total_content
FROM 
  analysis
WHERE 
  country IS NOT NULL AND country != ''
GROUP BY 
  country
ORDER BY 
  total_content DESC
LIMIT 5;
.3 Identify the longest movie
SELECT title, duration 
FROM analysis
WHERE type = 'Movie'
ORDER BY 
  CAST(SUBSTRING_INDEX(duration, ' ', 1) AS UNSIGNED) DESC
LIMIT 1;
 4.Find content added in the last 5 years
SELECT date_added
FROM analysis
WHERE 
  STR_TO_DATE(date_added, '%M %d, %Y') >= DATE_SUB(CURDATE(), INTERVAL 5 YEAR);
  .5. List all TV shows with more than 5 seasons
  select title, duration,type from analysis
where type = 'tv show' and  cast(substring_INDEX(duration, ' ' ,1) as unsigned) > 5;
6. Count the number of content items in each genre
SELECT 
  listed_in AS genre,
  COUNT(*) AS total_content
FROM 
  analysis
GROUP BY 
  listed_in
ORDER BY 
  total_content DESC;
  7.Find each year and the average numbers of content release in India on netflix. 
  SELECT 
  release_year, 
  COUNT(*) AS total_releases,
  ROUND(COUNT(*) / COUNT(DISTINCT title), 2) AS avg_per_title
FROM 
  analysis
WHERE 
  country LIKE '%India%'
GROUP BY 
  release_year
ORDER BY 
  release_year;
 8 return top 5 year with highest avg content release!
  SELECT 
  release_year, 
  ROUND(COUNT(*) / COUNT(DISTINCT title), 2) AS avg_per_title
FROM 
  analysis
GROUP BY 
  release_year
ORDER BY 
  avg_per_title DESC
LIMIT 5;

select description from analysis 
where description like '%kill%'

