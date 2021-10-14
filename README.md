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
<img width="863" alt="2" src="https://github.com/svitbka/doc_reader/blob/main/result/ans4.png">
