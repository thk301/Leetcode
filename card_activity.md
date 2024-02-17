with card_ranked as (
SELECT 
card_name,
issued_amount,
row_number() over (partition by card_name order by issue_month asc, issued_amount desc) as ranked
FROM monthly_cards_issued
where issue_year = 2021
)


select 
distinct
c.card_name,
issued_amount
from card_ranked as c
where ranked=1
order by 2 desc
