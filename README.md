 ## Первый запрос.
```SELECT b.client_number as client_number, 
  COUNT(CASE WHEN ev.outcome = 'win' THEN 1 END) AS Побед, 
    COUNT(CASE WHEN ev.outcome = 'lose' THEN 1 END) AS Поражений
FROM bid as b 
    INNER JOIN event_value as ev 
    ON ev.play_id = b.play_id
    WHERE ev.value = b.coefficient
GROUP BY client_number
```
<img width="863" alt="2" src="https://github.com/svitbka/test_sql/blob/main/img/ans_sql_1.png">

## Второй запрос.
```SWITH teams1 AS (
Select t1.home_team, t1.away_team, 
    max(case when t1.home_team = t2.away_team and t1.away_team = t2.home_team then t1.times + t2.times 
    Else t1.times end) as cnt 
From (
  SELECT 
      home_team, away_team, 
      COUNT(CONCAT(home_team, ' ', away_team)) AS times
      FROM event_entity 
      GROUP BY home_team, away_team
) t1 cross join (
   SELECT 
      home_team, away_team, 
      COUNT(CONCAT(home_team, ' ', away_team)) AS times
      FROM event_entity 
      GROUP BY home_team, away_team
) t2 
Group by 1,2
) 
SELECT CONCAT(home_team, ':', away_team) AS game, cnt AS games_count FROM teams1 
ORDER BY games_count
```
<img width="863" alt="2" src="https://github.com/svitbka/test_sql/blob/main/img/ans_sql_2.png">
