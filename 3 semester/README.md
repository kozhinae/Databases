1. Найти номера первых трех подкатегорий (ProductSubcategoryID) с наибольшим количеством наименований товаров:
   
select top 3 with ties ProductSubcategoryID
from production.Product
where ProductSubcategoryID is not null
group by ProductSubcategoryID
order by count(*) desc

3.
