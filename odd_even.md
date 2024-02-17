WITH combined as (
SELECT 
measurement_value,
measurement_time,
row_number() over (order by measurement_time asc) as ranked
FROM measurements
)

select 
cast(measurement_time as date),
sum(case when (ranked % 2)!=0 THEN 
measurement_value else 0 END) as odd_sum,
sum(case when (ranked % 2)=0 THEN 
measurement_value else 0 END) as even_sum
from combined
group by 1
order by 1 asc
