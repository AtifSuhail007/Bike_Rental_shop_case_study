--q1
select category, count(distinct model) no_of_bikes 
from bike
group by category
having count(distinct model) >2;





--q2
with cte as(select customer_id, count(*) membership_count
from membership
group by customer_id) 
select c.name,coalesce(cte.membership_count , 0) 
from customer c
left join cte
on c.id=cte.customer_id;




--q3
select id,category, price_per_hour,case 
           when category='electric' then  price_per_hour*0.9
           when category='Mountain bike' then  price_per_hour*0.8
           else 0.5*price_per_hour end new_price_per_hour, 
           price_per_day,case 
           when category='electric' then  price_per_day*0.8
           when category='Mountain bike' then  price_per_day*0.75
           else 0.5*price_per_day end new_price_per_day
 
 from bike;




 --q4
 select category,sum(iif(status='available' ,1,0)) available_bikes_count, 
sum(iif(status='rented', 1,0)) available_bikes_count
from bike
group by category;




--q5
select year(start_timestamp) year, month(start_timestamp) month, sum(total_paid) revenue
from rental
group by rollup (year (start_timestamp) ,month(start_timestamp)) 
;



--q6
select year(m.start_date) year,  month(m.start_date) month ,mt.name as  membership_type_name, sum(total_paid) total_revenue
from membership_type mt
inner join membership m
on mt.id=m.membership_type_id
group by cube (month(m.start_date),mt.name);



--q7
select mt.name as membership_type_name
, month (start_date) as month
, sum(total_paid) as total_revenue
from membership m
join membership_type mt on m.membership_type_id = mt.id
where year ( start_date) = 2023
group by CUBE( mt.name , month (start_date))
order by membership_type_name, month;



--q8
with cte as(select 
case when count(id)>10 then 'more_than_10'
when count(id) between 5 and 10 then 'between 5-10'
else 'below_5'end  rental_count_category
from rental
group by customer_id
) 
select rental_count_category, count(*) customer_count
from cte
group by rental_count_category;
