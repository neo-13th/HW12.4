#  "SQL. Часть 2"

## Задание 1  
Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию:  
фамилия и имя сотрудника из этого магазина;
город нахождения магазина;
количество пользователей, закреплённых в этом магазине.  

SELECT CONCAT(s.last_name, ' ', s.first_name) AS staff, c.city, COUNT(c2.store_id) AS custumers  
FROM customer c2  
INNER JOIN store s2 ON s2.store_id = c2.store_id  
INNER JOIN staff s ON s.staff_id = s2.manager_staff_id   
INNER JOIN address a ON s.address_id = a.address_id  
INNER JOIN city c ON c.city_id = a.city_id  
GROUP BY c2.store_id  
HAVING COUNT(c2.store_id) > 300;  

![sql21](https://github.com/user-attachments/assets/12c12adb-3262-44f1-ba65-a46580acaff8)


## Задание 2  
Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.  

SELECT COUNT(f.title)   
FROM film f  
WHERE f.`length` > (SELECT AVG(`length`) FROM film)  

![sql22](https://github.com/user-attachments/assets/db81f809-eee4-45df-9990-c6b1856b4fe1)



## Задание 3  
Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.  

SELECT MONTH(payment_date), SUM(p.amount), COUNT(p.rental_id) 
FROM payment p  
GROUP BY MONTH(payment_date)  
ORDER BY SUM(p.amount ) DESC  
LIMIT 1;  

![sql23](https://github.com/user-attachments/assets/bae54cd1-bedd-4c90-a604-2915085de262)



