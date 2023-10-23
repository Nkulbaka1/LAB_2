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
	"МАРКА" VARCHAR(50) NOT NULL,
	"АТП-ВЛАДЕЛЕЦ" VARCHAR(50) NOT NULL,
	"СКИДКА, %" SMALLINT NOT NULL
);

CREATE TABLE "ГАРАЖ"
(
	"ИДЕНТИФИКАТОР" SERIAL PRIMARY KEY,
	"НОМЕР" VARCHAR(50) NOT NULL,
	"РАСПОЛОЖЕНИЕ" VARCHAR(50) NOT NULL,
	"КОММИССИОННЫЕ, %" SMALLINT NOT NULL
);

CREATE TABLE "ДЕТАЛИ"
(
	"ИДЕНТИФИКАТОР" SERIAL PRIMARY KEY,
	"ДЕТАЛЬ" VARCHAR(50) NOT NULL,
	"ПРОДАВЕЦ" VARCHAR(50) NOT NULL,
	"СТОИМОСТЬ, РУБ" INT NOT NULL,
	"МАКС. КОЛ-ВО" INT NOT NULL
);

CREATE TABLE "РЕМОНТ"
(
	"НОМЕР ЗАКАЗА" SERIAL PRIMARY KEY,
	"АВТОМОБИЛЬ" VARCHAR(50) NOT NULL,
	"ДАТА" VARCHAR(50) NOT NULL,
	"ГАРАЖ" VARCHAR(50) NOT NULL,
	"ДЕТАЛИ" VARCHAR(50) NOT NULL,
	"КОЛ-ВО" INT NOT NULL,
	"ОБЩАЯ СТОИМОСТЬ, РУБ" INT NOT NULL
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

c) марки всех машин Газ.
