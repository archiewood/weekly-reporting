```months
select 
substr(order_datetime,0,8) as month,
'monthly-reports/' || substr(order_datetime,0,8) as link,
sum(sales) as sales_usd
from orders
group by 1
order by 1
```

<DataTable data={months} link=link/>