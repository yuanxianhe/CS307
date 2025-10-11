12313017  袁先河
# Question1 
## answer code :
```sql
select station_id, english_name, chinese_name, district  
from stations  
where (  
          english_name like '%East%' or  
          english_name like '%West%' or  
          english_name like '%South%' or  
          english_name like '%North%'  
          )  
order by station_id;
```
## sanpshot of result table :
![](https://raw.githubusercontent.com/yuanxianhe/CS307/main/img%5Clab1q1.png)
![[q1.png]]
# Question2
## answer code :
```sql
select district,  
       round((max(latitude) - min(latitude)) * 111) as 南北跨度km  
from stations  
where latitude is not NULL  
  and district is not NULL  
group by district;
```
## sanpshot of result table :
![](https://raw.githubusercontent.com/yuanxianhe/CS307/main/img%5Clab1q2.png)
![[q2.png]]
# Question 3 
 ## answer code :
 ```sql
select 'Station ' || station_id || ' '  
       || english_name || '(' || chinese_name || ') in ' || district  
       as station_information  
from stations  
where station_id between 2 and 10  
order by station_id;
```
## sanpshot of result table :
![](https://raw.githubusercontent.com/yuanxianhe/CS307/main/img%5Clab1q3.png)
![[q3.png]]
# Question 4
## answer code :
 ```sql
select distinct station_id  
from bus_lines  
where bus_line in ('103', '104')  
order by station_id DESC;
```

## sanpshot of result table :
![](https://raw.githubusercontent.com/yuanxianhe/CS307/main/img%5Clab1q4.png)
![[q4.png]]
# Question 5
## answer code :
 ```sql
select distinct station_id  
from bus_lines  
where bus_line in ('103', '104')  
group by station_id  
having count(distinct bus_line ) = 2  
order by station_id;
```
## sanpshot of result table (ascending) :
![](https://raw.githubusercontent.com/yuanxianhe/CS307/main/img%5Clab1q5.png)
![[q5.png]]
# Question 6
## answer code :
 ```sql
select  
    round(  
        1.0 * count(*) /  
        (select count(distinct station_id)  
         from bus_lines  
         where bus_line = '103'),  
        2  
    ) as round  
from (  
    select station_id  
    from bus_lines  
    where bus_line in ('103', '104')  
    group by station_id  
    having count(distinct bus_line) = 2  
) as common;
```
## sanpshot of result table :
![[q6.png]]
![q6.png](https://raw.githubusercontent.com/yuanxianhe/CS307/main/img%5Clab1q6.png)

# Question 7
## answer code :
 ```sql
select bus_line,  
       count(distinct station_id) as cnt  
from bus_lines  
group by bus_line  
having count(distinct station_id) >= 10  
order by cnt DESC;
```
## sanpshot of result code :
![[q7_2.png]]
![[q7_1.png]]
![](https://raw.githubusercontent.com/yuanxianhe/CS307/main/img%5Clab1q7_2.png)

![q7_1.png](https://raw.githubusercontent.com/yuanxianhe/CS307/main/img%5Clab1q7_1.png)

# Question 8
## answer code :
 ```sql
select station_id,  
       count(distinct bus_line) as cnt  
from bus_lines  
group by station_id  
having count(distinct bus_line) = (  
    select max(bus_cnt)  
    from (  
        select count(distinct bus_line) as bus_cnt  
        from bus_lines  
        group by station_id  
    ) as max  
);
```
## sanpshot of result code :
![q8.png](https://raw.githubusercontent.com/yuanxianhe/CS307/main/img%5Clab1q8.png)
![[q8.png]]
# Question 9
## answer code :
 ```sql
select bus_line,  
       count(distinct station_id) as count  
from bus_lines  
where bus_line ~ '^N[0-9]'  
group by bus_line  
order by cast(substring(bus_line from 2) as INTEGER);
```
## sanpshot of result code :
![](https://raw.githubusercontent.com/yuanxianhe/CS307/main/img%5Clab1q9.png)
![[q9.png]]
# Question 10
## answer code :
 ```sql
select bus_line,  
       count(distinct station_id) as cnt,  
       case  
           when bus_line ~ '^N[0-9]' then '夜班公交'  
           when bus_line ~ '^M[0-9]' then '主干线公交'  
           else ' '  
           end                    as 备注  
from bus_lines  
group by bus_line  
having count(distinct station_id) > 10  
order by cnt DESC;
```
## sanpshot of result code :
![](https://raw.githubusercontent.com/yuanxianhe/CS307/main/img%5Clab1q10_1.png)
![](https://raw.githubusercontent.com/yuanxianhe/CS307/main/img%5Clab1q10_2.png)
![](https://raw.githubusercontent.com/yuanxianhe/CS307/main/img%5Clab1q10_3.png)![[q10_1.png]]![[q10_2.png]]![[q10_3.png]]