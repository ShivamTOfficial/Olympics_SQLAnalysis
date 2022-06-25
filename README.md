# Olympics_SQL

[Dataset](https://www.kaggle.com/datasets/heesoo37/120-years-of-olympic-history-athletes-and-results?select=noc_regions.csv)


How many olympics games have been held? 

    SELECT 
      COUNT(*) AS Number_Of_Olympics
    FROM( 
      SELECT DISTINCT Year, Season
      FROM `olympics-project-120years.Olympics.Athlete_Events`
      );

Mention the total no of nations who participated in each olympics game.

    SELECT 
      Games, COUNT(DISTINCT NOC) AS No_Of_Countries
    FROM 
      `olympics-project-120years.Olympics.Athlete_Events`
    GROUP BY Games
    ORDER BY Games;

Which year saw the highest and lowest no of countries participating in olympics?


Which nation has participated in all of the olympic games?


Which Sports were just played only once in the olympics?<br/>

Fetch details of the oldest athletes to win a gold medal.

Find what percentage of total athletes were females?

Fetch the top 5 athletes who have won the most gold medals.
Fetch the top 5 athletes who have won the most medals (gold/silver/bronze).


List down total gold, silver and broze medals won by each country.<br/>
List down total gold, silver and broze medals won by each country corresponding to each olympic games.<br/>

And now the mandatory, how-is-MY-country-performing questions

In which Sport/event, India has won highest medals.
Break down all olympic games where india won medal for Hockey and how many medals in each olympic games.
