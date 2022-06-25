# Olympics_SQL

[Dataset](https://www.kaggle.com/datasets/heesoo37/120-years-of-olympic-history-athletes-and-results?select=noc_regions.csv) </br>
[Go try your hands on it](https://console.cloud.google.com/bigquery?sq=410130076228:b9aad05d05da4af8a21ef37823fd13db)


How many olympics games have been held? 

    SELECT 
      COUNT(*) AS Number_Of_Olympics
    FROM( 
      SELECT DISTINCT Year, Season
      FROM `olympics-project-120years.Olympics.Athlete_Events`
      );

![image](https://user-images.githubusercontent.com/91784043/175772998-265866a1-5233-4e89-9dec-d734b5570d2a.png)

Mention the total no of nations who participated in each olympics game.

    SELECT 
      Games, COUNT(DISTINCT NOC) AS No_Of_Countries
    FROM 
      `olympics-project-120years.Olympics.Athlete_Events`
    GROUP BY Games
    ORDER BY Games;

![image](https://user-images.githubusercontent.com/91784043/175773057-4e57d0f8-401d-415f-9ffc-83aecc36646c.png)


Which year saw the highest and lowest no of countries participating in olympics?

    WITH
    cnt_countries
    AS (
      SELECT Games, COUNT(DISTINCT NOC) AS cnt
      FROM `olympics-project-120years.Olympics.Athlete_Events`
      GROUP BY Games
    ),
    rnk_countries
    AS (
      SELECT Games, cnt, RANK() OVER(ORDER BY cnt ASC) AS asc_rnk, RANK() OVER(ORDER BY cnt DESC) AS desc_rnk
      FROM cnt_countries
      )
    SELECT 
        Games, cnt AS Max_Min_Countries
    FROM 
        rnk_countries
    WHERE (asc_rnk = 1) OR (desc_rnk = 1);

![image](https://user-images.githubusercontent.com/91784043/175773084-439200cb-e5ed-473e-812d-b2622b4fdd8d.png)


Which nation has participated in all of the olympic games?

    WITH games_played
    AS (
      SELECT Team, COUNT(DISTINCT Games) AS times_participated
      FROM `olympics-project-120years.Olympics.Athlete_Events`
      GROUP BY Team
    )
    SELECT *
    FROM games_played
    WHERE times_participated = 51;

![Screenshot 2022-06-25 174113](https://user-images.githubusercontent.com/91784043/175772967-2573bbaa-9ab8-4b56-b86f-dc03a8f57947.png)


Which Sports were just played only once in the olympics?<br/>

    WITH sports_cnt
    AS (
    SELECT Sport, COUNT(DISTINCT Games) AS times_played
    FROM `olympics-project-120years.Olympics.Athlete_Events`
    GROUP BY Sport)
    SELECT 
        *
    FROM 
        sports_cnt
    WHERE sports_cnt.times_played = 1;

Fetch details of the oldest athletes to win a gold medal.

Find what percentage of total athletes were females?

Fetch the top 5 athletes who have won the most gold medals.
Fetch the top 5 athletes who have won the most medals (gold/silver/bronze).


List down total gold, silver and broze medals won by each country.<br/>
List down total gold, silver and broze medals won by each country corresponding to each olympic games.<br/>

And now the mandatory, how-is-MY-country-performing questions

In which Sport/event, India has won highest medals.
Break down all olympic games where india won medal for Hockey and how many medals in each olympic games.
