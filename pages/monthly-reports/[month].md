# {$page.params.month}


```daily_sales
select
substr(order_datetime,0,11) as date,
substr(order_datetime,0,8) as month,
sum(sales) as sales_usd
from orders
group by 1,2
order by 3 desc
```

```month_sales
select
substr(order_datetime,0,8) as month,
sum(sales) as sales_usd
from orders
group by 1
```
## Daily Sales

Sales for last month totalled <Value data={month_sales.filter(d => d.month === $page.params.month)} column=sales_usd/>.

<BarChart 
    title="Daily Sales for {$page.params.month}"
    data={daily_sales.filter(d => d.month === $page.params.month)} />

The day with the highest sales was **<Value data={daily_sales.filter(d => d.month === $page.params.month)} column=date/>** with <Value data={daily_sales.filter(d => d.month === $page.params.month)} column=sales_usd/> in sales.


```marketing_spend_channels
select 
substr(month_begin,0,8) as month,
marketing_channel,
spend as spend_usd
from marketing_spend
group by 1,2
order by 3 desc
```

```total_spend
select
substr(month_begin,0,8) as month,
sum(spend) as spend_usd
from marketing_spend
group by 1
```

## Marketing Spend

Total marketing spend for last month was <Value data={total_spend.filter(d => d.month === $page.params.month)} column=spend_usd/>.

<BarChart data={marketing_spend_channels.filter(d => d.month === $page.params.month)} x=marketing_channel/>

The channel with the highest spend was **<Value data={marketing_spend_channels.filter(d => d.month === $page.params.month)} column=marketing_channel/>** with <Value data={marketing_spend_channels.filter(d => d.month === $page.params.month)} column=spend_usd/> in spend.



