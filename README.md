# Домашнее задание к занятию "12.04 «SQL. Часть 2»" - Евгений Шахов.
---
### Задание 1.
##### Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию: фамилия и имя сотрудника из этого магазина; город нахождения магазина; количество пользователей, закреплённых в этом магазине.
> select concat(s.first_name , ' ', s.last_name),  c2.city, count(c.customer_id) from staff s join store s2 on s2.store_id = s.store_id join customer c on c.store_id = s2.store_id join address a on a.address_id = s2.address_id join city c2 on c2.city_id = a.city_id 
> group by s.staff_id, c2.city_id having coumt(c.customer_id) > 300;
> 
> ![image](https://user-images.githubusercontent.com/122415129/235786084-f3000313-f366-4720-9214-db9c349d0bb0.png)
---
### Задание 2.
##### Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.
> select count(f.title) from film f where f.`length` > (select avg(`length`) from film f2);
> 
> ![image](https://user-images.githubusercontent.com/122415129/235788345-48bd190a-791e-4780-8db9-991ebbc0e816.png)
---
### Задание 3.
##### Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.
> select month (payment_date), count(payment_id), sum(amount) from payment group by month(payment_date) order by sum(amount) desc limit 1;
> 
> ![image](https://user-images.githubusercontent.com/122415129/235790673-85a402b1-7451-426d-9de5-ec24e6ac6f93.png)
---
### Задание 4*.


---
### Задание 5*.


---
