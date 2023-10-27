1. Найти номера первых трех подкатегорий (ProductSubcategoryID) с наибольшим количеством наименований товаров:
   
select top 3 with ties ProductSubcategoryID
from production.Product
where ProductSubcategoryID is not null
group by ProductSubcategoryID
order by count(*) desc

2.Разбить продукты по количеству символов в названии, для каждой группы
определить количество продуктов:

select len(Name), count(*)
from production.Product
group by len(Name)

3. Проверить, есть ли продукты с одинаковым названием, если есть, то вывести
эти названия:

select Name
from production.Product
group by ProductID, Name
having count(*) > 1

4. Найти и вывести на экран количество товаров каждого цвета, исключив из
поиска товары, цена которых меньше 30:

select Color, count(Color)
from production.Product
where Color is not null
group by Color
having max(Product.ListPrice) >= 30

5. Найти и вывести на экран список, состоящий из цветов товаров, таких, что
минимальная цена товара данного цвета более 100:

select Color, ListPrice
from production.Product
where Color is not null
group by Color, ListPrice
having min(ListPrice) > 100

6. Найти и вывести на экран номера подкатегорий товаров и количество товаров
в каждой категории:

select ProductSubcategoryID, count(*)
from production.Product
where ProductSubcategoryID is not null
group by ProductSubcategoryID

7. Найти и вывести на экран номера товаров и количество фактов продаж данного
товара (используется таблица SalesORDERDetail):

select ProductID, count(*)
from Sales.SalesOrderDetail
group by ProductID

9. Найти и вывести на экран номера товаров, которые были куплены более пяти
раз.

select ProductID, count(*)
from Sales.SalesOrderDetail
group by ProductID
having count(*) > 5

11. Найти и вывести на экран номера покупателей, CustomerID, у которых
существует более одного чека, SalesORDERID, с одинаковой датой

select CustomerID
from Sales.Customer, Sales.SalesOrderDetail
group by CustomerID
having count(Sales.SalesOrderDetail.SalesOrderID)>1

13. Найти и вывести на экран все номера чеков, на которые приходится более трех
продуктов.

select SalesOrderID, OrderQty
from Sales.SalesOrderDetail
group by SalesOrderID, OrderQty
having SalesOrderDetail.OrderQty > 3

15. Найти и вывести на экран все номера продуктов, которые были куплены более
трех раз.

select ProductID, OrderQty
from Sales.SalesOrderDetail
group by ProductID, OrderQty
having SalesOrderDetail.OrderQty > 3

17. Найти и вывести на экран все номера продуктов, которые были куплены или
три или пять раз.

select ProductID, OrderQty
from Sales.SalesOrderDetail
where ProductID is not null
group by ProductID, OrderQty
having OrderQty = 3 or OrderQty = 5

19. Найти и вывести на экран все номера подкатегорий, в которым относится
более десяти товаров:

select ProductSubcategoryID, count(*)
from Production.Product
where ProductSubcategoryID is not null
group by ProductSubcategoryID
having count(*) > 10

14. Найти и вывести на экран номера товаров, которые всегда покупались в
одном экземпляре за одну покупку.

select ProductID, OrderQty
from Sales.SalesOrderDetail
where ProductID is not null
group by ProductID, OrderQty
having OrderQty = 1

16. Найти и вывести на экран номер чека, SalesORDERID, на который приходится
с наибольшим разнообразием товаров купленных на этот чек.

select Top 1 SalesOrderID, count(DISTINCT ProductID)
from Sales.SalesOrderDetail
group by SalesOrderID
order by count(DISTINCT ProductID) desc

18. Найти и вывести на экран номер чека, SalesORDERID с наибольшей суммой
покупки, исходя из того, что цена товара – это UnitPrice, а количество
конкретного товара в чеке – это ORDERQty.

select Top 1 SalesOrderID, sum(UnitPrice * OrderQty)
from Sales.SalesOrderDetail
group by SalesOrderID
order by sum(UnitPrice * OrderQty) desc

20. Определить количество товаров в каждой подкатегории, исключая товары,
для которых подкатегория не определена, и товары, у которых не определен цвет:

select ProductSubcategoryID, count(*)
from Production.Product
where ProductSubcategoryID is not null and Color is not null
group by ProductSubcategoryID

18. Получить список цветов товаров в порядке убывания количества товаров
данного цвета:

select Color, count(*)
from Production.Product
where Color is not null
group by Color
order by count(Color) desc

19. Вывести на экран ProductID тех товаров, что всегда покупались в количестве
более 1 единицы на один чек, при этом таких покупок было более двух: 



