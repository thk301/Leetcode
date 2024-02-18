```

rank() over (partition by )  --> 1, 1, 3, 

dense_rank() over (partition by )  --> 1, 1, 2 

row_number() over (partition by)  --> 1, 2, 3, 

sum(this) over (partition by  order by )


lead(this, 1) over (order by )
lag(this, 1) over (order by )

```
