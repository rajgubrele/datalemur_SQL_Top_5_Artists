# datalemur_SQL_Top_5_Artists

Select t2.artist_name, artist_rank from
(Select t1.artist_name artist_name, count(t1.artist_name) top, dense_rank() over (order by count(t1.artist_name) desc) as artist_rank 
from
(SELECT * FROM artists a
Join Songs s on a.artist_id = s.artist_id
join global_song_rank g on g.song_id = s.song_id
where rank in (1,2,3,4,5,6,7,8,9,10)
order by g.rank) t1
GROUP BY t1.artist_name
order by top desc) t2
where t2.artist_rank in (1,2,3,4,5)
