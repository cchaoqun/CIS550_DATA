Upload your **Milestone 3 Submission: Database Population and SQL Queries**, where you will pre-process your data, perform entity resolution, and populate the database. 

# **Create a .txt file containing the following:** 

##  **1. Queries** 

- [x] A list of 5-10 SQL queries for your database that your application may execute. Ensure that some of your queries are complex (e.g. involve subqueries, joins, aggregations, etc.) 

## **2. Descriptions**

- [x] A 1-2 sentence description of what each query is supposed to do 

## **3. Credentials** 

- [ ] Instructions and guest credentials for accessing the database 



## Queries & Descriptions 

```mysql
#1 The top 10 movies that order by worldwide box office
select name, worldwide_gross
from BoxOffice b1
where 10>=(
	select count(*)
    from BoxOffice b2
    where b2.worldwide_gross >= b1.worldwide_gross
)
order by worldwide_gross DESC;

#2 The top 10 movies that won Oscar order by worldwide box office
with temp as (
	select title, original_title, worldwide_gross
    from BoxOffice b
    join Movies m
    on b.id = m.id
)
select t.title as title, t.worldwide_gross as worldwide_gross
from temp t
join Oscar o
on t.original_title = o.name
order by t.worldwide_gross DESC
limit 10;

#3 The top 3 reviewed movie genre
select count(user_reviews) as reviews
from Genre g
join Movies m
on g.id = m.id
group by g.genre
order by count(user_reviews) 
limit 3;

#4 The total box office of a specific director/actor/actress. 
with temp as (
	select m.id as id,  worldwide_gross
    from BoxOffice b
    join Movies m
    on b.id = m.id
)
select count(t.worldwide_gross)as totle_worldwide_gross
from Actors a 
join temp t
on a.id = t.id
where a.name = "XXX"

#5 View all awards won by each movie
select m.title as title, o.film as film, o.winner as winner, o.year_file as year_film, o.year_ceremony as year_ceremony
from Oscar o
left join Movies m
on o.name = m.original_title

#6 View all movies information including gross
select m.title as name, b.worldwide_gross as worldwide_gross, m.year as year, m.duration as duration, m.language as language
from Movies m
join BoxOffice b
on m.id = b.id

```







