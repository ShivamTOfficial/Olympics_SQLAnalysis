# Olympics 

Hey there, welcome! In the Resources Folder, you'll find *2 CSV files-* </br> 
1. Athlete_Events.csv
2. NOC_Regions.csv

</br>

I did this entire SQL Analysis on Google BigQuery, [click here](https://console.cloud.google.com/bigquery?sq=410130076228:b9aad05d05da4af8a21ef37823fd13db&project=olympics-project-120years) to check out **(& run)** all of these queries on BigQuery Sandbox *(you'll need a gmail account).* [The Dataset](https://www.kaggle.com/datasets/heesoo37/120-years-of-olympic-history-athletes-and-results?select=noc_regions.csv) has been fetched from [Kaggle](https://www.kaggle.com/) (a brilliant resource for folks in Data Industry). If you'd like to know how to upload the dataset on BigQuery, [go check out this video]() *(Best part is that all you'd need is a gmail account!)*</br></br>

Do ping me if you need something else. </br> 
*Happy Learning! :)*
</br></br></br></br>


### Queries

1] How many olympics games have been held? 

    SELECT 
      COUNT(*) AS Number_Of_Olympics
    FROM( 
      SELECT DISTINCT Year, Season
      FROM `olympics-project-120years.Olympics.Athlete_Events`
      );
      
 
![image](https://user-images.githubusercontent.com/91784043/175775555-61b8c552-dcf3-4105-8903-f352c7a2f9dc.png)

<p align = "center">
Query 1: No. Of Olympic Games
</p>
 </br> </br>
 
2] Mention the total no of nations who participated in each olympics game.

    SELECT 
      Games, COUNT(DISTINCT NOC) AS No_Of_Countries
    FROM 
      `olympics-project-120years.Olympics.Athlete_Events`
    GROUP BY Games
    ORDER BY Games;

![image](https://user-images.githubusercontent.com/91784043/175773057-4e57d0f8-401d-415f-9ffc-83aecc36646c.png)

<p align = "center">
Query 2: No. Of nations participating in Olympic Games
</p>
 </br> </br>

3] Which year saw the highest and lowest no of countries participating in olympics?

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

<p align = "center">
Query 3: Highest & Lowest no of countries to participate
</p>
 </br> </br>

4] Which nation has participated in all of the olympic games?

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

<p align = "center">
Query 4: Nations participating in all Olympics
</p>
 </br> </br>

5] Which Sports were just played only once in the olympics?<br/>

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

![image](https://user-images.githubusercontent.com/91784043/175773466-80b97e1b-3322-43f3-ae11-550db14e0f12.png)

<p align = "center">
Query 5: Sports which were played only once throughout Olympics
</p>
 </br> </br>
 
Interesting! Cricket was also played once in Olympics, I looked up and found more information on it. </br>
[Check out what Wiki has to tell you about **Cricket At The 1900 Summer Olympics**](https://en.wikipedia.org/wiki/Cricket_at_the_1900_Summer_Olympics#:~:text=A%20cricket%20tournament%2C%20played%20as,158%20runs%20by%20Great%20Britain.)


### Under Construction!
### Queries I'll be working on soon....

6] Fetch details of the oldest athletes to win a gold medal.

7] Find what percentage of total athletes were females?

8] Fetch the top 5 athletes who have won the most gold medals.
9] Fetch the top 5 athletes who have won the most medals (gold/silver/bronze).


10] List down total gold, silver and broze medals won by each country.<br/>
11] List down total gold, silver and broze medals won by each country corresponding to each olympic games.<br/>

And now the mandatory, how-is-MY-country-performing questions </br>

12] In which Sport/event, India has won highest medals. </br>
13] Break down all olympic games where india won medal for Hockey and how many medals in each olympic games.
