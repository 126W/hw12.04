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
### Задание 4.
##### Посчитайте количество продаж, выполненных каждым продавцом. Добавьте вычисляемую колонку «Премия». Если количество продаж превышает 8000, то значение в колонке будет «Да», иначе должно быть значение «Нет».
> select t1.cp 'продажи', t1.staff_id 'продавец',
> case when t1.cp > 8000 then 'да' else 'нет' end as 'премия'
> from(select count(payment_id) cp, staff_id from sakila.payment p group by staff_id ) t1;
> 
> ![image](https://user-images.githubusercontent.com/122415129/235794431-b7853254-116e-456e-8ef4-ddfd0373c91e.png)
---
### Задание 5.
##### Найдите фильмы, которые ни разу не брали в аренду
> select f.title  from sakila.rental r 
> right join sakila.inventory i on i.inventory_id = r.inventory_id  
> right join sakila.film f  on f.film_id = i.film_id 
> where  r.rental_id is null;
> 
> ![image](https://user-images.githubusercontent.com/122415129/235794921-09dce4e1-4566-417d-bac8-abb071ea365c.png)
---
