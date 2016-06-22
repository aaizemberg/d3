# VAST 2016, MC2

## Dibujando y reordenando de manera manual, las series.

Si tomo todas las mediciones, tengo 4032 datos por sensor, mejor hago una muestra y me quedo con 806 registros.

``` sql
select date_time, value from (
  select row_number() OVER () as rnum, date_time,value from sensors 
  where attribute = 'Hazium Concentration'
  and floor = 3 and zone = '1'
  order by date_time) as foo
where (foo.rnum % 5) = 0
```
