3.1
```postgresql
select b.name, vesselno

from boat b

inner join employees e

on e.fisheryname = b.name

group by b.name, b.vesselno

order by b.vesselno, b.name asc


```
3.2
```postgresql
select b.name, vesselno

from boat b

left join employees e

on e.fisheryname = b.name

where b.capacity > 10

  

group by b.name, b.vesselno

having count(e.personname) < 7

  

order by b.vesselno asc, b.name asc




```


4.1
```postgresql
select f.name, coalesce(whname, 'keine Firma vorhanden') as whname

from fishery f

join boat b

on f.name = b.name

left join distributor d

on f.name = d.fishery

--whtaxid saved the day

group by f.name, d.whname, d.whtaxid

having count(distinct b.vesselno) between 1 and 3

order by f.name desc, d.whname desc
```

4.2
```postgresql


select f.name, coalesce(d.whname, 'keine Firma vorhanden') as whname

from

(

select f.name

from fishery f

join boat b

on f.name = b.name

group by f.name

having count(b.vesselno) between 1 and 3

)f

left join distributor d

on f.name = d.fishery

  

order by f.name desc, whname desc;


```


[für die Prozentrechnung](https://stackoverflow.com/questions/24191243/select-percentage-of-rows-that-have-a-certain-value-sql)

5.2
```postgresql

select distinct f.name,

  

(

select round(coalesce(avg(capacity),0),2) as avg_boatcapacity

from boat b

where b.name = f.name

),

(

select round(

coalesce(

sum(case

when employmenttype = 'employee'

then 1

else 0

end

) * 100.0 / count(*),0

),2

) as percentageofEmployees

from employees e

where e.fisheryname = f.name

),

  

(

select count(fi.id)

from fish fi

where fi.caughtby = f.name and fi.caughton between '2021-09-01' and '2021-09-30'

)

  

from fishery f



```

7
```postgresql
select fi.caughtby, count(fi.caughtby) as fishcount,

count(b.id) as basscount ,

count(s.id) as salmoncount,

count(t.id) as tunacount

  

from fish fi

left join salmon s

on s.id = fi.id

left join bass b

on b.id = fi.id

left join tuna t

on t.id = fi.id

  

where caughton <= '2019-12-31' and caughton >= '2019-01-01'

  

group by fi.caughtby

  

having count(fi.caughtby) >= all

(

select count(fish.id)

from fish

where caughton <= '2019-12-31' and caughton >= '2019-01-01'

group by fish.caughtby

)

  

order by caughtby asc




```

8
```postgresql





```

