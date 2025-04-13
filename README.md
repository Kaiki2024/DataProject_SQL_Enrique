Importar BBDD_Proyecto en DBeaver
    - Creamos una nueva BBDD
    - BBDD_ProjectKike
    - Marcamos establecer por defecto
    - Archivo y buscamos el archivo que nos hemos descargado (BBDD_Projecto) y le damos a abrir
    - No estaba marcado "postgres", sale "NONE". Modificamos
    - Seleccinamos todo el código (CTRL+A) y damos play
    - Botón derecho en BBDD_ProjectKike y "Renovar"

Realizamos captura de pantalla del diagrama y lo guardamos en un archivo a parte (jpg)

--pregunta 2:
SELECT "title" AS "Título_Película",
		"rating" AS "Clasificación"
FROM "film" AS f 
WHERE  "rating" = 'R';

--pregunta 3:
SELECT CONCAT("first_name",' ',"last_name") AS "Nombre_Actor",
		"actor_id" AS "ID"
FROM "actor" AS a
WHERE "actor_id" BETWEEN 30 AND 40;

--pregunta 4:
SELECT "title" AS "Título_Película",
		"language_id" AS "Idioma",
		"original_language_id" AS "Idioma_Original"
FROM "film" AS f
WHERE "language_id" = "original_language_id";

--pregunta 5: 
SELECT "title" AS "Título_Película",
		"length" AS "Duración_en_MIN"
FROM "film" AS f 
ORDER BY "Duración_en_MIN" ASC;

--pregunta 6:
SELECT CONCAT("first_name",' ',"last_name") AS "Nombre_Actor"
FROM "actor" AS a
WHERE "last_name" LIKE 'ALLEN'; 

--pregunta 7:
SELECT "rating" AS "Clasificación",
		COUNT ("rating") AS "Total_Películas"
FROM "film" AS f
GROUP BY "Clasificación";

--pregunta 8:
SELECT "title" AS "Título_Película",
		"rating" AS "Clasificación",
		"length" AS "Duración"
FROM "film" AS f
WHERE "rating" = 'PG-13' OR "length" > 180;

--pregunta 9:
SELECT VARIANCE("replacement_cost") AS "Reemplazo_películas"
FROM film;

--pregunta 10:
SELECT MIN("length") AS "Duración_Mínima",
	   MAX("length") AS  "Duración_Máxima"
FROM film AS f;

--pregunta 11: 
SELECT "rental_date" AS "Fecha",
		"amount" AS "Coste"
FROM rental AS r 
INNER JOIN payment AS p 
ON r."rental_id" = p."rental_id"
ORDER BY "Fecha" ASC
OFFSET 2;

--pregunta 12:
SELECT "title" AS "Título",
		"rating" AS "Clasificación"	
FROM film AS f 
WHERE "rating" NOT IN ('NC-17','G');

--pregunta 13: 
SELECT AVG("length") AS "Duración_Media_Min",
       "rating" AS "Clasificación"
FROM film AS f 
GROUP BY "rating";

--pregunta 14:
SELECT "title" AS "Título",
		"length" AS "Duración"
FROM film AS f 
WHERE "length" > 180;

--pregunta 15:
SELECT SUM("amount") AS "Total_Ingresos"
FROM payment AS p;

--pregunta 16: 
SELECT "CustomerId" AS "ID_Cliente"
FROM "Customer" AS c 
ORDER BY "CustomerId" DESC
LIMIT 10;

--pregunta 17:
SELECT CONCAT("first_name",' ',"last_name") AS "Nombre_Actor/Actriz",
       "title" AS "Título"
FROM actor AS a 
INNER JOIN film_actor AS fa 
ON a."actor_id" = fa."actor_id"
INNER JOIN film AS f 
ON fa."film_id" = f."film_id"
WHERE "title" = 'EGG IGBY';

--pregunta 18:
SELECT DISTINCT "title" AS "Título"
FROM film AS f;

--pregunta 19:
SELECT "title" AS "Título",
       "length" AS "Duración",
       "name" AS "Categoría"
FROM film AS f 
INNER JOIN film_category AS fc 
ON f. "film_id" = fc."film_id"
INNER JOIN category AS c 
ON fc."category_id" = c. "category_id" 
WHERE "length" > 180 AND "name" = 'Comedy';

--pregunta 20:
SELECT AVG("length") AS "Duración_media",
       "name" AS "Categoría"
FROM film AS f 
INNER JOIN film_category AS fc 
ON f. "film_id" = fc."film_id"
INNER JOIN category AS c 
ON fc."category_id" = c. "category_id"
GROUP BY "name" 
HAVING AVG("length") > 110
ORDER BY "Duración_media" DESC;

--pregunta 21:
SELECT AVG("rental_duration") AS "Media_alquiler"
FROM film AS f;

--pregunta 22:
SELECT CONCAT("first_name",' ',"last_name") AS "Nombre_Actor"
FROM actor AS a;

--pregunta 23:
SELECT DATE (rental_date) AS "Fecha_Alquiler",
	   COUNT(rental_date) AS  "Total_Alquileres_Dia"
FROM rental AS r 
GROUP BY  "Fecha_Alquiler" 
ORDER BY "Fecha_Alquiler" DESC;

--pregunta 24:
SELECT "title" AS "Película",
		"length" AS "Duración"
FROM film AS f 
WHERE "length" > (SELECT AVG("length") AS "Duración_media"
					FROM film AS f);
					
--pregunta 25:
SELECT TO_CHAR ("rental_date",'YYYY_MM') AS "Mes_alquiler",
		COUNT("rental_date") AS "Total_alquileres)"
FROM rental AS r 
GROUP BY "Mes_alquiler" 
ORDER BY "Mes_alquiler";

--pregunta 26:
SELECT AVG("amount") AS "Media_total_pagado",
	   STDDEV("amount") AS "Desviación_total_pagado",
	   VARIANCE("amount") AS "Varianza_total_pagado"
FROM payment AS p;

--pregunta 27:
SELECT "amount" AS "Precio",
	   f."title" AS "Película"
FROM payment AS p 
INNER JOIN rental AS r 
ON p."rental_id" = r."rental_id"
INNER JOIN inventory AS i 
ON r."inventory_id" = i."inventory_id"
INNER JOIN film AS f 
ON i."film_id" = f."film_id" 
WHERE "amount" > (SELECT AVG("amount")
				  FROM payment AS p2 )
ORDER BY "amount" ASC;

--pregunta 28:
SELECT "actor_id" AS "ID_Actor"
FROM film_actor AS fa 
GROUP BY "actor_id"
HAVING COUNT("film_id") > 40;

--pregunta 29:
SELECT "title" AS "Película",
		COUNT("inventory_id") AS "Total_copias"
FROM film AS f
INNER JOIN inventory AS i 
ON f."film_id"= i."film_id"
GROUP BY "title"
ORDER BY "Total_copias" DESC;

--pregunta 30:
SELECT CONCAT("first_name",' ',"last_name") AS "Actor/Actriz",
		COUNT(a."actor_id") AS "Películas"
FROM actor AS a 
INNER JOIN film_actor AS fa
ON a."actor_id" = fa."actor_id"
GROUP BY "Actor/Actriz";

--pregunta 31:
SELECT "title" AS "Película",
		CONCAT(a."first_name",' ',a."last_name") AS "Actor/Actriz"
FROM film AS f 
LEFT JOIN film_actor AS fa 
ON f."film_id" = fa."film_id"
LEFT JOIN actor AS a 
ON fa."actor_id" = a."actor_id"
ORDER BY "Actor/Actriz" ASC;

--pregunta 32:
SELECT CONCAT("first_name",' ',"last_name") AS "Nombre_Actores",
		"title" AS "Película"
FROM actor AS a 
FULL JOIN film_actor AS fa 
ON a."actor_id" = fa."actor_id"
RIGHT JOIN film AS f 
ON fa."film_id" = f."film_id";

--pregunta 33:
SELECT "title" AS "Película",
		"rental_date" AS "Fecha_alquiler",
		"return_date" AS "Fecha_devolución"
FROM film AS f 
INNER JOIN inventory AS i 
ON f."film_id" = i."film_id"
INNER JOIN rental AS r 
ON r."inventory_id" = i."inventory_id" 
ORDER BY "Película";

--pregunta 34:
SELECT SUM("amount") AS "Total_gastado",
		c."customer_id" AS "ID_cliente",
		CONCAT("first_name",' ',"last_name") AS "Nombre_Cliente"
FROM payment AS p 
INNER JOIN Customer AS c
ON c."customer_id" = p."customer_id"
GROUP BY "ID_cliente" 
ORDER BY "Total_gastado" DESC
LIMIT 5;

--pregunta 35:
SELECT "first_name" AS "Nombre",
		"last_name" AS "Apellido"
FROM actor AS a
WHERE "first_name" = 'JOHNNY';

--pregunta 36:
SELECT "first_name" AS "Nombre",
		"last_name" AS "Apellido"
FROM actor AS a;

--pregunta 37:
SELECT MAX("actor_id") AS "Mayor_ID",
	   MIN ("actor_id") AS "Menor_ID"
FROM actor AS a;

--pregunta 38:
SELECT COUNT("actor_id") AS "Total_actores_tabla"
FROM actor AS a;

--pregunta 39:
SELECT "last_name" AS "Apellido",
		"first_name" AS "Nombre"
FROM actor AS a 
ORDER BY "Apellido" ASC;

--pregunta 40:
SELECT "title" AS "Película"
FROM film AS f 
LIMIT 5;

--pregunta 41:
SELECT COUNT("first_name") AS "Total_Actores_Mismo_Nombre",
		"first_name" AS "Nombre_Actor"
FROM actor AS a 
GROUP BY "first_name"
ORDER BY "Total_Actores_Mismo_Nombre" DESC;

--pregunta 42:
SELECT CONCAT("first_name",' ',"last_name") AS "Nombre_cliente",
		"title" AS "Película",
	   "rental_date" AS "Fecha_alquiler" 
FROM "customer" AS c 
INNER JOIN rental AS r 
ON c."customer_id" = r."customer_id"
INNER JOIN inventory AS i 
ON r."inventory_id" = i."inventory_id" 
INNER JOIN film AS f 
ON i."film_id" = f."film_id"
ORDER BY "Nombre_cliente" ASC;

-- pregunta 43:
SELECT CONCAT("first_name",' ',"last_name") AS "Nombre_cliente",
		"title" AS "Película"
FROM "customer" AS c 
FULL JOIN rental AS r 
ON c."customer_id" = r."customer_id"
FULL JOIN inventory AS i 
ON r."inventory_id" = i."inventory_id" 
FULL JOIN film AS f 
ON i."film_id" = f."film_id"
ORDER BY "Nombre_cliente" ASC;

--pregunta 44:
SELECT *
FROM film AS f 
CROSS JOIN film_category AS fc 
CROSS JOIN category AS c; 

-- No es útil esta consulta en concreta. Nos arroja demasiada información, mucha repetida. Genera confusión y sin agruparla no tiene valor.

--pregunta 45:
SELECT CONCAT("first_name",' ',"last_name") AS "Nombre_actor/actriz"
FROM actor AS a 
INNER JOIN film_actor AS fa 
ON a."actor_id" = fa."actor_id"  
INNER JOIN film AS f 
ON fa."film_id" = f."film_id"
INNER JOIN film_category AS fc 
ON f."film_id" = fc."film_id" 
INNER JOIN category AS c 
ON fc."category_id" = c."category_id"
WHERE c."name" = 'Action'
ORDER BY "Nombre_actor/actriz" ASC;

--pregunta 46:
SELECT CONCAT("first_name",' ',"last_name") AS "Nombre_actor/actriz",
		f."title" AS "Título_película" 
FROM actor AS a 
LEFT JOIN film_actor AS fa 
ON a."actor_id" = fa."actor_id"
LEFT JOIN film AS f 
ON fa."film_id" = f."film_id"
WHERE f."title" IS NULL;

--pregunta 47:
SELECT CONCAT("first_name",' ',"last_name") AS "Nombre_actor/actriz",
		COUNT(f.film_id) AS "Total_películas"	
FROM actor AS a 
INNER JOIN film_actor AS fa 
ON a."actor_id" = fa."actor_id"
INNER JOIN film AS f 
ON fa."film_id" = f."film_id"
GROUP BY "Nombre_actor/actriz"
ORDER BY "Total_películas" ASC;

--pregunta 48:
CREATE VIEW "actor_num_peliculas" AS
SELECT CONCAT("first_name",' ',"last_name") AS "Nombre_actor/actriz",
		COUNT(f.film_id) AS "Total_películas"	
FROM actor AS a 
INNER JOIN film_actor AS fa 
ON a."actor_id" = fa."actor_id"
INNER JOIN film AS f 
ON fa."film_id" = f."film_id"
GROUP BY "Nombre_actor/actriz"
ORDER BY "Total_películas" ASC;

--pregunta 49:
SELECT COUNT(r."rental_date") AS "Total_alquileres",
		CONCAT(c."first_name",' ',c."last_name") AS "Nombre_cliente"
FROM rental AS r 
INNER JOIN customer AS c 
ON r."customer_id" = c. "customer_id"
GROUP BY "Nombre_cliente"
ORDER BY "Total_alquileres" ASC;

--pregunta 50:
SELECT SUM(f."length") AS "Duración_total_películas_acción"
FROM film AS f 
INNER JOIN film_category AS fc 
ON f."film_id" = fc."film_id"
INNER JOIN category AS c 
ON fc."category_id" = c."category_id"
WHERE c."name" = 'Action';

--pregunta 51:
CREATE TEMP TABLE "cliente_rentas_temporal" AS
SELECT CONCAT(c."first_name",' ',c."last_name") AS "Nombre_cliente",
		SUM (p."amount") AS "Total_rentas",
		c."customer_id" AS "ID_cliente"
FROM customer AS c 
INNER JOIN payment AS p 
ON c."customer_id" = p."customer_id"
GROUP BY "ID_cliente" 
ORDER BY "ID_cliente" ASC;

--pregunta 52:
CREATE TEMP TABLE "peliculas_alquiladas" AS
SELECT "title" AS "Título_película",
		COUNT(r."rental_date") AS "Total_alquileres"
FROM film AS f 
INNER JOIN inventory AS i 
ON f."film_id" = i."film_id"
INNER JOIN rental AS r 
ON i."inventory_id" = r."inventory_id"
GROUP BY "Título_película" 
HAVING COUNT(r."rental_date") >= 10
ORDER BY "Total_alquileres" ASC;

--pregunta 53:
SELECT f."title" AS "Película"
FROM customer AS c
INNER JOIN rental AS r 
ON c."customer_id" = r."customer_id"
INNER JOIN inventory AS i 
ON r."inventory_id" = i."inventory_id"
INNER JOIN film AS f 
ON i."film_id" = f."film_id"
WHERE c."first_name" = 'TAMMY'
AND c."last_name" = 'SANDERS'
AND r."return_date" IS NULL;

--pregunta 54:
SELECT a."first_name" AS "Nombre",
		a."last_name" AS "Apellido",
		COUNT(fa."film_id") AS "Películas_SCIFI"
FROM actor AS a 
INNER JOIN film_actor AS fa 
ON a."actor_id" = fa."actor_id"
INNER JOIN film AS f 
ON fa."film_id" = f."film_id"
INNER JOIN film_category AS fc 
ON f."film_id" = fc."film_id"
INNER JOIN category AS c 
ON fc."category_id" = c."category_id"
WHERE c."name" = 'Sci-Fi'
GROUP BY a."first_name", a."last_name"
ORDER BY "Apellido" ASC;

--pregunta 55:
SELECT a."first_name" AS "Nombre",
		a."last_name" AS "Apellido"
FROM actor AS a
INNER JOIN film_actor AS fa 
ON a."actor_id" = fa."actor_id"
INNER JOIN film AS f 
ON fa."film_id" = f."film_id"
INNER JOIN inventory AS i 
ON f."film_id" = i."film_id"
INNER JOIN rental AS r 
ON i."inventory_id" = r."inventory_id"
WHERE r."rental_date" >
						(SELECT MIN (r."rental_date")
   							FROM rental AS r 
							INNER JOIN inventory AS i 
							ON r."inventory_id" = i."inventory_id"
							INNER JOIN film AS f 
							ON i."film_id" = f."film_id"
							WHERE f."title" = 'SPARTACUS CHEAPER')
GROUP BY a."first_name", a."last_name"
ORDER BY a."last_name" ASC;

--pregunta 56:
SELECT a."first_name" AS "Nombre",
		a."last_name" AS "Apellido"
FROM actor AS a 
INNER JOIN film_actor AS fa 
ON a."actor_id" = fa."actor_id"
INNER JOIN film AS f 
ON fa."film_id" = f."film_id"
INNER JOIN film_category AS fc 
ON f."film_id" = fc."film_id"
INNER JOIN category AS c 
ON fc."category_id" = c."category_id"
WHERE c."name" <> 'Music'
GROUP BY a."first_name", a."last_name"
ORDER BY a."last_name" ASC;

--pregunta 57:
SELECT f."title" AS "Película"
FROM film AS f 
INNER JOIN inventory AS i 
ON f."film_id" = i."film_id"
INNER JOIN rental AS r 
ON i."inventory_id" = r."inventory_id"
WHERE DATE_PART ('day', r."return_date" - r."rental_date") > 8;

--pregunta 58:
SELECT f."title" AS "Película"
FROM actor AS a 
INNER JOIN film_actor AS fa 
ON a."actor_id" = fa."actor_id"
INNER JOIN film AS f 
ON fa."film_id" = f."film_id"
INNER JOIN film_category AS fc 
ON f."film_id" = fc."film_id"
INNER JOIN category AS c 
ON fc."category_id" = c."category_id"
WHERE c."name" = 'Animation'
GROUP BY f."title"
ORDER BY f."title" ASC;

--pregunta 59:
SELECT f."title" AS "Película"
FROM film AS f 
WHERE f."length" = (SELECT f."length"
					FROM film AS f
					WHERE f."title" = 'DANCING FEVER')
ORDER BY f."title" ASC

--pregunta 60:
SELECT c."first_name" AS "Nombre",
		c."last_name" AS "Apellido",
		COUNT(i."film_id") AS "Películas"
FROM customer AS c 
INNER JOIN rental AS r 
ON c."customer_id" = r."customer_id"
INNER JOIN inventory AS i 
ON r."inventory_id" = i. "inventory_id"
GROUP BY c."first_name",c."last_name"
HAVING COUNT(i."film_id") >= 7
ORDER BY c."last_name" ASC;

--pregunta 61:
SELECT COUNT(i."film_id") AS "Total_películas",
		c."name" AS "Categoría"
FROM inventory AS i 
INNER JOIN rental AS r 
ON i."inventory_id" = r."inventory_id"
INNER JOIN film AS f 
ON i."film_id" = f."film_id"
INNER JOIN film_category AS fc 
ON f."film_id" = fc."film_id"
INNER JOIN category AS c 
ON fc."category_id" = c."category_id"
GROUP BY c."name";

--pregunta 62:
SELECT COUNT(i."film_id") AS "Total_películas",
		c."name" AS "Categoría"
FROM inventory AS i 
INNER JOIN rental AS r 
ON i."inventory_id" = r."inventory_id"
INNER JOIN film AS f 
ON i."film_id" = f."film_id"
INNER JOIN film_category AS fc 
ON f."film_id" = fc."film_id"
INNER JOIN category AS c 
ON fc."category_id" = c."category_id"
WHERE f."release_year" = '2006'
GROUP BY c."name";

--pregunta 63:
SELECT s."first_name" AS "Nombre",
		s2."store_id" AS "Tiendas"
FROM staff AS s 
FULL JOIN store AS s2
ON s."store_id" = s2."store_id"

--pregunta 64:
SELECT c."first_name" AS "Nombre",
		c."last_name" AS "Apellido",
		c."customer_id" AS "ID_cliente",
		COUNT(i."film_id") AS "Total_películas_alquiladas"
FROM customer AS c 
INNER JOIN rental AS r 
ON c. "customer_id" = r."customer_id"
INNER JOIN inventory AS i 
ON r."inventory_id" = i."inventory_id"
GROUP BY c."first_name",c."last_name",c."customer_id"
ORDER BY c."customer_id" ASC;
