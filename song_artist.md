WITH song_artist as (
SELECT 
s.*,
a.artist_name, 
a.label_owner
FROM songs as s
left join artists as a on s.artist_id = a.artist_id
), 
topten as (
select * from global_song_rank
where rank<=10
),
combined as (
select s.artist_name, 
count(distinct day) as counter
from song_artist as s
left join topten as t on s.song_id = t.song_id
group by 1
)

select
artist_name,
row_number() over (order by counter desc, artist_name asc) as artist_rank
from combined
order by counter DESC
limit 5


