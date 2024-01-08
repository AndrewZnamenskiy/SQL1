# Домашнее задание к занятию «SQL. Часть 1»


### Задание 1

Получите уникальные названия районов из таблицы с адресами, которые начинаются на “K” и заканчиваются на “a” и не содержат пробелов.

### Задание 2

Получите из таблицы платежей за прокат фильмов информацию по платежам, которые выполнялись в промежуток с 15 июня 2005 года по 18 июня 2005 года **включительно** и стоимость которых превышает 10.00.

### Задание 3

Получите последние пять аренд фильмов.

### Задание 4

Одним запросом получите активных покупателей, имена которых Kelly или Willie. 

Сформируйте вывод в результат таким образом:
- все буквы в фамилии и имени из верхнего регистра переведите в нижний регистр,
- замените буквы 'll' в именах на 'pp'.

## Дополнительные задания (со звёздочкой*)
Эти задания дополнительные, то есть не обязательные к выполнению, и никак не повлияют на получение вами зачёта по этому домашнему заданию. Вы можете их выполнить, если хотите глубже шире разобраться в материале.

### Задание 5*

Выведите Email каждого покупателя, разделив значение Email на две отдельных колонки: в первой колонке должно быть значение, указанное до @, во второй — значение, указанное после @.

### Задание 6*

Доработайте запрос из предыдущего задания, скорректируйте значения в новых колонках: первая буква должна быть заглавной, остальные — строчными.

---

### Решение 1

#### Листинг запроса:

```
	SELECT DISTINCT district 
	FROM address
	WHERE district LIKE 'K%a' and district NOT LIKE '% %';
```

#### Скриншот запроса:

![Commit Task1](https://github.com/AndrewZnamenskiy/SQL1/blob/main/img/task1p1.png)


### Решение 2


#### Листинг запроса:

```	
	SELECT amount, CAST(payment_date AS DATE) AS SHORTDATE FROM payment
	WHERE (amount > 10.00) and (CAST(payment_date AS DATE) BETWEEN '2005-06-15'and '2005-06-18')
	ORDER BY SHORTDATE  ASC,amount;
```

#### Скриншот запроса:

![Commit Task2](https://github.com/AndrewZnamenskiy/SQL1/blob/main/img/task2p1.png)


### Решение 3


#### Листинг запроса:

```
	SELECT * FROM rental r
	ORDER BY rental_date DESC
	LIMIT 5;
```

#### Скриншот запроса:

![Commit Task3](https://github.com/AndrewZnamenskiy/SQL1/blob/main/img/task3p1.png)


### Решение 4

#### Листинг запроса:

```
	SELECT REPLACE(LOWER(first_name), 'll', 'pp') FROM customer c 
	WHERE first_name = 'Kelly' OR first_name = 'Willie'
```


#### Скриншот запроса:

![Commit Task4](https://github.com/AndrewZnamenskiy/SQL1/blob/main/img/task4p1.png)


### Решение 5*

#### Листинг запроса:

```
	SELECT 
	SUBSTRING_INDEX(email, '@', 1),
	RIGHT(email,CHAR_LENGTH(email) - CHAR_LENGTH(SUBSTRING_INDEX(email, '@', 1)) - 1)
	from customer;
```


#### Скриншот запроса:

![Commit Task5](https://github.com/AndrewZnamenskiy/SQL1/blob/main/img/task5p1.png)


----
