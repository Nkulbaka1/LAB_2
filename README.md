# LAB_2
1. Дана схема базы данных в виде следующих отношений. С помощью операторов SQL создать
логическую структуру соответствующих таблиц для хранения в СУБД, используя известные средства
поддержания целостности (NOT NULL, UNIQUE, и т.д.). Обосновать выбор типов данных и
используемые средства поддержания целостности. При выборе подходящих типов данных
использовать информацию о конкретных значениях полей БД (см. прил.1)
~~~SQL
CREATE TABLE "АВТОМОБИЛЬ"
(
	"ИДЕНТИФИКАТОР" SERIAL PRIMARY KEY,
	--такой тип данных подходит для идентификаторов или айди,
	--тк может увеличиваться с ростом числа записей, что экономит место
	"МАРКА" VARCHAR(50) NOT NULL,
	--короткое текстовое название
	"АТП-ВЛАДЕЛЕЦ" VARCHAR(50) NOT NULL,
	--короткое текстовое название
	"СКИДКА, %" SMALLINT NOT NULL
	--SMALLINT, тк не может быть скидки больше 100 %
);

CREATE TABLE "ГАРАЖ"
(
	"ИДЕНТИФИКАТОР" SERIAL PRIMARY KEY,
	--такой тип данных подходит для идентификаторов или айди,
	--тк может увеличиваться с ростом числа записей, что экономит место
	"НОМЕР" VARCHAR(50) NOT NULL,
	--короткое текстовое название
	"РАСПОЛОЖЕНИЕ" VARCHAR(50) NOT NULL,
	--короткое текстовое название
	"КОММИССИОННЫЕ, %" SMALLINT NOT NULL
	--SMALLINT, тк не может быть коммиссионных больше 100 %
);

CREATE TABLE "ДЕТАЛИ"
(
	"ИДЕНТИФИКАТОР" SERIAL PRIMARY KEY,
	--такой тип данных подходит для идентификаторов или айди,
	--тк может увеличиваться с ростом числа записей, что экономит место
	"ДЕТАЛЬ" VARCHAR(50) NOT NULL,
	--короткое текстовое название
	"ПРОДАВЕЦ" VARCHAR(50) NOT NULL,
	--короткое текстовое название
	"СТОИМОСТЬ, РУБ" INT NOT NULL,
	--может быть большое число, не должно быть NULL
	"МАКС. КОЛ-ВО" INT NOT NULL
	--может быть большое число, не должно быть NULL
);

CREATE TABLE "РЕМОНТ"
(
	"НОМЕР ЗАКАЗА" SERIAL PRIMARY KEY,
	--такой тип данных подходит для идентификаторов или айди,
	--тк может увеличиваться с ростом числа записей, что экономит место
	"АВТОМОБИЛЬ" INT NOT NULL,
	--здесь хранится идентификатор автомобиля, поэтому INT
	--может быть большое число, не должно быть NULL
	"ДАТА" VARCHAR(50) NOT NULL,
	--названия месяцев не занимают много символов
	"ГАРАЖ" INT NOT NULL,
	--здесь хранится идентификатор гаража, поэтому INT
	--может быть большое число, не должно быть NULL
	"ДЕТАЛИ" INT NOT NULL,
	--здесь хранится идентификатор детали, поэтому INT
	--может быть большое число, не должно быть NULL
	"КОЛ-ВО" INT NOT NULL,
	--может быть большое число, не должно быть NULL
	"ОБЩАЯ СТОИМОСТЬ, РУБ" INT NOT NULL
	--может быть большое число, не должно быть NULL
);
~~~
2. Ввести в ранее созданные таблицы конкретные данные (см. прил. 1). Использовать скрипт-файл из
операторов INSERT или вспомогательную утилиту.
~~~SQL
INSERT INTO "АВТОМОБИЛЬ" ("ИДЕНТИФИКАТОР", "МАРКА", "АТП-ВЛАДЕЛЕЦ", "СКИДКА, %") 
VALUES  ('001', 'Газ-24', 	'АТП1', 4),
	('002', 'Газ-52', 	'АТП1', 0),
	('003', 'Зил-130',	'АТП3', 3),
	('004', 'Зил-133',	'АТП4', 5),
	('005', 'Газ-1222',  	'АТП5', 4);

INSERT INTO "ГАРАЖ" ("ИДЕНТИФИКАТОР", "НОМЕР", "РАСПОЛОЖЕНИЕ", "КОММИССИОННЫЕ, %") 
VALUES 	('001', 'N1', 'АТП1', 3),
	('002', 'N2', 'АТП1', 3),
	('003', 'N1', 'АТП2', 4),
	('004', 'N3', 'АТП2', 4),
	('005', 'N4', 'АТП4', 4),
	('006', 'N5', 'АТП5', 3);

INSERT INTO "ДЕТАЛИ" ("ИДЕНТИФИКАТОР", "ДЕТАЛЬ", "ПРОДАВЕЦ", "СТОИМОСТЬ, РУБ", "МАКС. КОЛ-ВО") 
VALUES  ('001', 'Трубка', 'АТП1', 10000, 100),
	('002', 'Скоба', 'АТП1', 5000, 230),
	('003', 'Картер', 'АТП3', 40000, 70),
	('004', 'Штуцер', 'АТП2', 7000, 200),
	('005', 'Прокладка', 'АТП2', 5000, 1200),
	('006', 'Пробка', 'АТП1', 5000, 300),
	('007', 'Толкатель', 'АТП1', 11000, 120);

INSERT INTO "РЕМОНТ" ("НОМЕР ЗАКАЗА", "АВТОМОБИЛЬ", "ДАТА", "ГАРАЖ", "ДЕТАЛИ", "КОЛ-ВО", "ОБЩАЯ СТОИМОСТЬ, РУБ") 
VALUES 	('05002', '004', 'Январь',  '003', '007', 7,  77000 ),
	('05003', '003', 'Февраль', '003', '002', 4,  20000 ),
	('05004', '003', 'Февраль', '005', '004', 1,  7000  ),
	('05005', '003', 'Март',    '006', '005', 6,  30000 ),
	('05006', '002', 'Апрель',  '006', '007', 9,  99000 ),
	('05007', '004', 'Апрель',  '006', '006', 8,  40000 ),
	('05008', '001', 'Май',     '005', '007', 3,  33000 ),
	('05009', '001', 'Май',     '003', '003', 2,  80000 ),
	('05010', '003', 'Май',     '006', '001', 16, 160000),
	('05011', '003', 'Май',     '005', '005', 21, 105000),
	('05012', '002', 'Июнь',    '001', '001', 5,  50000 ),
	('05013', '005', 'Июнь',    '006', '002', 3,  15000 ),
	('05014', '003', 'Август',  '002', '006', 6,  30000 ),
	('05015', '004', 'Август',  '005', '001', 4,  40000 ),
	('05016', '004', 'Август',  '001', '007', 7,  77000 ),
	('05017', '005', 'Август',  '001', '006', 1,  5000  ),
	('05018', '002', 'Август',  '004', '002', 1,  5000  );
~~~
3. Используя оператор SELECT создать запрос для вывода всех строк каждой таблицы. Проверить
правильность ввода. При необходимости произвести коррекцию значений операторами INSERT,
UPDATE, DELETE.
~~~SQL
SELECT *
FROM "АВТОМОБИЛЬ";
~~~
![alt text](https://github.com/Nkulbaka1/LAB_2/assets/129120650/8b2bf90f-16e5-4156-b8bc-7dfcae47c780)
~~~SQL
SELECT *
FROM "ГАРАЖ";
~~~
![alt text](https://github.com/Nkulbaka1/LAB_2/assets/129120650/17884eb8-5894-41c6-979b-1232ee7d9129)
~~~SQL
SELECT *
FROM "ДЕТАЛИ";
~~~
![alt text](https://github.com/Nkulbaka1/LAB_2/assets/129120650/ea25be23-f3b3-4ed0-9c56-70316ca91fe3)
~~~SQL
SELECT *
FROM "РЕМОНТ";
~~~
![alt text](https://github.com/Nkulbaka1/LAB_2/assets/129120650/f569e044-4812-4b36-a8ca-2b36c9f42c1a)
4. Создать запросы для вывода:

a) всех различных марок автомобилей;
~~~SQL
SELECT DISTINCT "МАРКА"
FROM "АВТОМОБИЛЬ";
~~~
![alt text](https://github.com/Nkulbaka1/LAB_2/assets/129120650/678d37c5-277b-4eff-80c6-04c117f127e8)

b) всех различных АТП, имеющих гаражи для ремонта и размера их комиссионных;
~~~SQL
SELECT DISTINCT "РАСПОЛОЖЕНИЕ", "КОММИССИОННЫЕ, %"
FROM "ГАРАЖ";
~~~
![alt text](https://github.com/Nkulbaka1/LAB_2/assets/129120650/2f839237-78b2-48c4-a447-0cf019b71969)

c) всех названий деталей и их стоимостей.
~~~SQL
SELECT "ДЕТАЛЬ", "СТОИМОСТЬ, РУБ"
FROM "ДЕТАЛИ";
~~~
![alt text](https://github.com/Nkulbaka1/LAB_2/assets/129120650/ade586e0-631b-4fd8-8f06-0bfcc9ef4481)

5. Создав запрос получить следующую информацию:
a) названия и максимальное количество деталей, продающихся АТП1 и АТП2;
~~~SQL
SELECT "ДЕТАЛЬ", "МАКС. КОЛ-ВО"
FROM "ДЕТАЛИ"
WHERE "ПРОДАВЕЦ" IN ('АТП1', 'АТП2');
~~~
![alt text](https://github.com/Nkulbaka1/LAB_2/assets/129120650/82f8226e-330b-4f2a-94f4-f15ba50ff885)

b) номер, дата и количество деталей для таких записей о ремонте, где общая стоимость ремонта
составила более 30000руб. Отсортировать по возрастанию суммы и дате ремонта;
~~~SQL
SELECT "НОМЕР ЗАКАЗА", "ДАТА", "КОЛ-ВО" AS "КОЛ-ВО ДЕТАЛЕЙ"
FROM "РЕМОНТ"
WHERE "ОБЩАЯ СТОИМОСТЬ, РУБ" > 30000
ORDER BY 
"ОБЩАЯ СТОИМОСТЬ, РУБ",
CASE
	WHEN "РЕМОНТ"."ДАТА" = 'Январь' THEN 1
	WHEN "РЕМОНТ"."ДАТА" = 'Февраль' THEN 2
	WHEN "РЕМОНТ"."ДАТА" = 'Март' THEN 3
	WHEN "РЕМОНТ"."ДАТА" = 'Апрель' THEN 4
	WHEN "РЕМОНТ"."ДАТА" = 'Май' THEN 5
	WHEN "РЕМОНТ"."ДАТА" = 'Июнь' THEN 6
	WHEN "РЕМОНТ"."ДАТА" = 'Июль' THEN 7
	WHEN "РЕМОНТ"."ДАТА" = 'Август' THEN 8
	WHEN "РЕМОНТ"."ДАТА" = 'Сентябрь' THEN 9
	WHEN "РЕМОНТ"."ДАТА" = 'Октябрь' THEN 10
	WHEN "РЕМОНТ"."ДАТА" = 'Ноябрь' THEN 11
	WHEN "РЕМОНТ"."ДАТА" = 'Декабрь' THEN 12
END;
~~~
![alt text](https://github.com/Nkulbaka1/LAB_2/assets/129120650/60be32f5-a776-422c-8fd7-b96f35ca0026)

c) марки всех машин Газ.
~~~SQL
SELECT "МАРКА"
FROM "АВТОМОБИЛЬ"
WHERE "МАРКА" LIKE 'Газ%'
~~~
![alt text](https://github.com/Nkulbaka1/LAB_2/assets/129120650/38459fb1-79f7-41aa-b62b-afd998aa84d6)

6. На основании данных о ремонте для каждой записи вывести:
a) номер заказа, марка автомобиля, дата, общая стоимость ремонта. Отсортировать результат по
общей стоимости;
~~~SQL
SELECT "НОМЕР ЗАКАЗА", "АВТОМОБИЛЬ"."МАРКА" AS "МАРКА АВТОМОБИЛЯ", "ДАТА", "ОБЩАЯ СТОИМОСТЬ, РУБ"
FROM "РЕМОНТ"
JOIN "АВТОМОБИЛЬ" ON "РЕМОНТ"."АВТОМОБИЛЬ" = "АВТОМОБИЛЬ"."ИДЕНТИФИКАТОР"
ORDER BY "ОБЩАЯ СТОИМОСТЬ, РУБ";
~~~
![alt text](https://github.com/Nkulbaka1/LAB_2/assets/129120650/356240d3-4a41-40f2-b016-1c9a510dc32a)

b) дату, название гаража, название детали, количество.
~~~SQL
SELECT "ДАТА", "ГАРАЖ"."НОМЕР" AS "НАЗВАНИЕ ГАРАЖА", "ДЕТАЛИ"."ДЕТАЛЬ" AS "НАЗВАНИЕ ДЕТАЛИ", "КОЛ-ВО" AS "КОЛИЧЕСТВО"
FROM "РЕМОНТ"
JOIN "ГАРАЖ" ON "РЕМОНТ"."ГАРАЖ" = "ГАРАЖ"."ИДЕНТИФИКАТОР"
JOIN "ДЕТАЛИ" ON "РЕМОНТ"."ДЕТАЛИ" = "ДЕТАЛИ"."ИДЕНТИФИКАТОР";
~~~
![alt text](https://github.com/Nkulbaka1/LAB_2/assets/129120650/52eb9e3d-815d-4071-ac7b-e8a2103eb9d2)

7. Определить:
a) номера заказов, марки автомобилей и даты ремонтов, проводимых в гаражах АТП1;
~~~SQL
SELECT "НОМЕР ЗАКАЗА", "АВТОМОБИЛЬ"."МАРКА" AS "МАРКА АВТОМОБИЛЯ", "ДАТА"
FROM "РЕМОНТ"
JOIN "ГАРАЖ" ON "РЕМОНТ"."ГАРАЖ" = "ГАРАЖ"."ИДЕНТИФИКАТОР"
JOIN "АВТОМОБИЛЬ" ON "РЕМОНТ"."АВТОМОБИЛЬ" = "АВТОМОБИЛЬ"."ИДЕНТИФИКАТОР"
WHERE "ГАРАЖ"."РАСПОЛОЖЕНИЕ" = 'АТП1';
~~~
![alt text](https://github.com/Nkulbaka1/LAB_2/assets/129120650/e7f7fd7d-478a-4dce-a567-d595d0c82699)

b) АТП-владельцы и названия гаражей, в которых проходил ремонт автомобилей со скидкой более
3% не ранее января. Вывести вместе с датами и отсортировать.
~~~SQL
SELECT "ГАРАЖ"."РАСПОЛОЖЕНИЕ", "ГАРАЖ"."НОМЕР", "ДАТА"
FROM "РЕМОНТ"
JOIN "ГАРАЖ" ON "РЕМОНТ"."ГАРАЖ" = "ГАРАЖ"."ИДЕНТИФИКАТОР"
JOIN "АВТОМОБИЛЬ" ON "РЕМОНТ"."АВТОМОБИЛЬ" = "АВТОМОБИЛЬ"."ИДЕНТИФИКАТОР"
WHERE "АВТОМОБИЛЬ"."СКИДКА, %" > 3
ORDER BY 
CASE
	WHEN "РЕМОНТ"."ДАТА" = 'Январь' THEN 1
	WHEN "РЕМОНТ"."ДАТА" = 'Февраль' THEN 2
	WHEN "РЕМОНТ"."ДАТА" = 'Март' THEN 3
	WHEN "РЕМОНТ"."ДАТА" = 'Апрель' THEN 4
	WHEN "РЕМОНТ"."ДАТА" = 'Май' THEN 5
	WHEN "РЕМОНТ"."ДАТА" = 'Июнь' THEN 6
	WHEN "РЕМОНТ"."ДАТА" = 'Июль' THEN 7
	WHEN "РЕМОНТ"."ДАТА" = 'Август' THEN 8
	WHEN "РЕМОНТ"."ДАТА" = 'Сентябрь' THEN 9
	WHEN "РЕМОНТ"."ДАТА" = 'Октябрь' THEN 10
	WHEN "РЕМОНТ"."ДАТА" = 'Ноябрь' THEN 11
	WHEN "РЕМОНТ"."ДАТА" = 'Декабрь' THEN 12
END;
~~~
![alt text](https://github.com/Nkulbaka1/LAB_2/assets/129120650/a385feae-16c4-485c-87ac-5fbfbee4e994)

c) автомобили, у которых требовал ремонта толкатель, а местом ремонта не являлся гараж N1;
~~~SQL
SELECT "АВТОМОБИЛЬ"."МАРКА" AS "АВТОМОБИЛЬ"
FROM "РЕМОНТ"
JOIN "ГАРАЖ" ON "РЕМОНТ"."ГАРАЖ" = "ГАРАЖ"."ИДЕНТИФИКАТОР"
JOIN "АВТОМОБИЛЬ" ON "РЕМОНТ"."АВТОМОБИЛЬ" = "АВТОМОБИЛЬ"."ИДЕНТИФИКАТОР"
JOIN "ДЕТАЛИ" ON "РЕМОНТ"."ДЕТАЛИ" = "ДЕТАЛИ"."ИДЕНТИФИКАТОР"
WHERE "ДЕТАЛИ"."ДЕТАЛЬ" = 'Толкатель'
	AND "ГАРАЖ"."НОМЕР" != 'N1';
~~~
![alt text](https://github.com/Nkulbaka1/LAB_2/assets/129120650/2be78bcb-e159-467e-8cd5-2fbe2e055ff3)

d) название и требуемое при ремонте количество деталей,.для тех ремонтов машин марки Зил130,
которые проводились в АТП2 или АТП4
~~~SQL
SELECT "АВТОМОБИЛЬ"."МАРКА" AS "АВТОМОБИЛЬ", "КОЛ-ВО" AS "КОЛИЧЕСТВО ДЕТАЛЕЙ"
FROM "РЕМОНТ"
JOIN "ГАРАЖ" ON "РЕМОНТ"."ГАРАЖ" = "ГАРАЖ"."ИДЕНТИФИКАТОР"
JOIN "АВТОМОБИЛЬ" ON "РЕМОНТ"."АВТОМОБИЛЬ" = "АВТОМОБИЛЬ"."ИДЕНТИФИКАТОР"
WHERE "АВТОМОБИЛЬ"."МАРКА" = 'Зил-130'
	AND ("ГАРАЖ"."РАСПОЛОЖЕНИЕ" = 'АТП4'
	OR   "ГАРАЖ"."РАСПОЛОЖЕНИЕ" = 'АТП2');
~~~
![alt text](https://github.com/Nkulbaka1/LAB_2/assets/129120650/851414b9-c8a4-487d-867b-f6f9ec948ec0)

8. Создать запрос для модификации всех значений столбца с общей стоимостью, чтобы он содержал
истинную сумму, оплачиваемую при ремонте ( с учетом скидки). Вывести новые значения.
~~~SQL
UPDATE "РЕМОНТ"
SET "ОБЩАЯ СТОИМОСТЬ, РУБ" = "ОБЩАЯ СТОИМОСТЬ, РУБ" - "ОБЩАЯ СТОИМОСТЬ, РУБ"*0.01*"АВТОМОБИЛЬ"."СКИДКА, %" FROM "АВТОМОБИЛЬ"
WHERE "РЕМОНТ"."АВТОМОБИЛЬ" = "АВТОМОБИЛЬ"."ИДЕНТИФИКАТОР"

--Проверка
SELECT *
FROM "РЕМОНТ";
~~~
![alt text](https://github.com/Nkulbaka1/LAB_2/assets/129120650/f6249335-4a4c-4550-bf74-b733867691c7)

9. Расширить таблицу с данными о ремонтах столбцом, содержащим величину комиссионных. Создать
запрос для ввода конкретных значений во все строки таблицы ремонтов.
~~~SQL
ALTER TABLE "РЕМОНТ" ADD COLUMN "КОММИССИОННЫЕ, %" INT;

UPDATE "РЕМОНТ"
SET "КОММИССИОННЫЕ, %" = "ОБЩАЯ СТОИМОСТЬ, РУБ" * 0.01 * "ГАРАЖ"."КОММИССИОННЫЕ, %" FROM "ГАРАЖ"
WHERE "РЕМОНТ"."ГАРАЖ" = "ГАРАЖ"."ИДЕНТИФИКАТОР"

--Проверка
SELECT *
FROM "РЕМОНТ";
~~~
![alt text](https://github.com/Nkulbaka1/LAB_2/assets/129120650/c01d941f-4f79-4090-82a0-2679e57dbdc6)

10. Используя операцию IN (NOT IN) реализовать следующие запросы:
a) найти гаражи, в которых производили ремонт толкателя в машинах из АТП3
~~~SQL
SELECT "ГАРАЖ"."НОМЕР" AS "НАЗВАНИЕ ГАРАЖА"
FROM "РЕМОНТ"
JOIN "ГАРАЖ" ON "РЕМОНТ"."ГАРАЖ" = "ГАРАЖ"."ИДЕНТИФИКАТОР"
JOIN "АВТОМОБИЛЬ" ON "РЕМОНТ"."АВТОМОБИЛЬ" = "АВТОМОБИЛЬ"."ИДЕНТИФИКАТОР"
JOIN "ДЕТАЛИ" ON "РЕМОНТ"."ДЕТАЛИ" = "ДЕТАЛИ"."ИДЕНТИФИКАТОР"
WHERE 	"ДЕТАЛИ"."ДЕТАЛЬ" IN ('Толкатель')
	AND "АВТОМОБИЛЬ"."АТП-ВЛАДЕЛЕЦ" IN ('АТП3');
~~~
![alt text](https://github.com/Nkulbaka1/LAB_2/assets/129120650/a1954d28-ec79-462e-8e31-93965369c97c)

b) найти детали, которые не ремонтировались в том же месяце, что и картер.
~~~SQL
SELECT DISTINCT "ДЕТАЛИ"."ДЕТАЛЬ"
FROM "РЕМОНТ"
JOIN "ДЕТАЛИ" ON "РЕМОНТ"."ДЕТАЛИ" = "ДЕТАЛИ"."ИДЕНТИФИКАТОР"
WHERE "ДЕТАЛИ"."ДЕТАЛЬ" NOT IN (
	SELECT "ДЕТАЛИ"."ДЕТАЛЬ"
	FROM "РЕМОНТ"
	JOIN "ДЕТАЛИ" ON "РЕМОНТ"."ДЕТАЛИ" = "ДЕТАЛИ"."ИДЕНТИФИКАТОР"
	WHERE "ДАТА" IN (SELECT "ДАТА"
		FROM "РЕМОНТ"
		JOIN "ДЕТАЛИ" ON "РЕМОНТ"."ДЕТАЛИ" = "ДЕТАЛИ"."ИДЕНТИФИКАТОР"
		WHERE "ДЕТАЛИ"."ДЕТАЛЬ" IN ('Картер')));
~~~
![alt text](https://github.com/Nkulbaka1/LAB_2/assets/129120650/4b84fc29-7d41-4f0f-8b4f-6e2f28f681da)

11. Используя операции ALL-ANY реализовать следующие запросы:
a) найти самую дорогую деталь, которую ремонтировали в машине, которая имела ремонт с самой
большой общей стоимостью;
~~~SQL
--детали, ремонтируемые в машине с самым дорогим ремонтом
SELECT DISTINCT "ДЕТАЛИ"."ДЕТАЛЬ"
FROM "РЕМОНТ"
JOIN "АВТОМОБИЛЬ" ON "РЕМОНТ"."АВТОМОБИЛЬ" = "АВТОМОБИЛЬ"."ИДЕНТИФИКАТОР"
JOIN "ДЕТАЛИ" ON "РЕМОНТ"."ДЕТАЛИ" = "ДЕТАЛИ"."ИДЕНТИФИКАТОР"
WHERE "АВТОМОБИЛЬ"."МАРКА" = (SELECT "АВТОМОБИЛЬ"."МАРКА"
	FROM "РЕМОНТ"
	JOIN "АВТОМОБИЛЬ" ON "РЕМОНТ"."АВТОМОБИЛЬ" = "АВТОМОБИЛЬ"."ИДЕНТИФИКАТОР"
	JOIN "ДЕТАЛИ" ON "РЕМОНТ"."ДЕТАЛИ" = "ДЕТАЛИ"."ИДЕНТИФИКАТОР"
	WHERE "ОБЩАЯ СТОИМОСТЬ, РУБ" >= ALL (
		SELECT "ОБЩАЯ СТОИМОСТЬ, РУБ" 
		FROM "РЕМОНТ"));
~~~
![alt text](https://github.com/Nkulbaka1/LAB_2/assets/129120650/01d846ed-0ba2-4a48-a102-f00debb4adad)

~~~SQL
SELECT "ДЕТАЛЬ"
FROM "ДЕТАЛИ"
WHERE "ДЕТАЛЬ" IN ('Пробка', 'Прокладка', 'Скоба', 'Трубка', 'Штуцер')
	AND "СТОИМОСТЬ, РУБ" >= ALL (SELECT "СТОИМОСТЬ, РУБ"
				     FROM "ДЕТАЛИ"
		 		     WHERE "ДЕТАЛЬ" IN ('Пробка', 'Прокладка', 'Скоба', 'Трубка', 'Штуцер'));
~~~
![alt text](https://github.com/Nkulbaka1/LAB_2/assets/129120650/12c60762-75a1-4add-b406-3f9e2f6d7e14)

b) найти среди машин АТП1 такого; который имеет минимальную скидку
~~~SQL
SELECT "МАРКА"
FROM "АВТОМОБИЛЬ"
WHERE "СКИДКА, %" <= ALL(SELECT "СКИДКА, %"
			 FROM "АВТОМОБИЛЬ"
			 WHERE "АТП-ВЛАДЕЛЕЦ" = 'АТП1');
~~~
![alt text](https://github.com/Nkulbaka1/LAB_2/assets/129120650/32dff4fd-cce7-4dd2-a53b-f212af29b72d)

c) найти детали, которые требовались для ремонта в самом большом количестве;
~~~SQL
SELECT "ДЕТАЛИ"."ДЕТАЛЬ"
FROM "РЕМОНТ"
JOIN "ДЕТАЛИ" ON "РЕМОНТ"."ДЕТАЛИ" = "ДЕТАЛИ"."ИДЕНТИФИКАТОР"
WHERE "КОЛ-ВО" >= ALL (SELECT "КОЛ-ВО"
		       FROM "РЕМОНТ");
~~~
![alt text](https://github.com/Nkulbaka1/LAB_2/assets/129120650/67b802fc-6f95-470b-b374-06919bfdd484)

d) запрос задания 7.a.
~~~SQL
SELECT "НОМЕР ЗАКАЗА", "АВТОМОБИЛЬ"."МАРКА" AS "МАРКА АВТОМОБИЛЯ", "ДАТА"
FROM "РЕМОНТ"
JOIN "ГАРАЖ" ON "РЕМОНТ"."ГАРАЖ" = "ГАРАЖ"."ИДЕНТИФИКАТОР"
JOIN "АВТОМОБИЛЬ" ON "РЕМОНТ"."АВТОМОБИЛЬ" = "АВТОМОБИЛЬ"."ИДЕНТИФИКАТОР"
WHERE "ГАРАЖ"."РАСПОЛОЖЕНИЕ" = ANY (SELECT "РАСПОЛОЖЕНИЕ"
				    FROM "ГАРАЖ"
				    WHERE "РАСПОЛОЖЕНИЕ" = 'АТП1');
~~~
![alt text](https://github.com/Nkulbaka1/LAB_2/assets/129120650/04291910-6680-4f15-8c3a-bce8c7b6c92a)

12. Используя операцию UNION получить места расположения машин и АТП-владельцы гаражей.
~~~SQL
SELECT "АТП-ВЛАДЕЛЕЦ"
FROM "АВТОМОБИЛЬ"
UNION
SELECT "РАСПОЛОЖЕНИЕ"
FROM "ГАРАЖ"
~~~
![alt text](https://github.com/Nkulbaka1/LAB_2/assets/129120650/7b015054-b3a2-4366-a9da-8590e69227a5)

