![SQL](https://raw.githubusercontent.com/David-Albarracin/README_MATERIALS/main/sql.png)

# Taller desarrollo de Base de datos

1. Creacion de la BASE DE DATOS 

   ```sql
   CREATE DATABASE taller;
   
   USE taller;
   
   CREATE TABLE `taller`.`fabricante` (
       `codigo` INT NOT NULL,
       `nombre` VARCHAR(100) NOT NULL,
       PRIMARY KEY (`codigo`)
   ) ENGINE = InnoDB;
   
   CREATE TABLE `taller`.`producto` (
       `codigo` INT NOT NULL,
       `nombre` VARCHAR(100) NOT NULL,
       `precio` DOUBLE NOT NULL,
       `codigo_fabricante` INT NOT NULL,
       PRIMARY KEY (`codigo`),
       FOREIGN KEY (`codigo_fabricante`) REFERENCES `fabricante`(`codigo`)
   ) ENGINE = InnoDB;
   ```

   

1. Realice la inserción de los siguientes datos

   ```sql
   INSERT INTO fabricante(codigo, nombre)
   VALUES 
   (1, 'Asus'), (2, 'Lenovo'),
   (3, 'Hewlett-Packard'), (4, 'Samsung'),
   (5, 'Seagate'), (6, 'Crucial'),
   (7, 'Gigabyte'), (8, 'Huawei'),(9, 'Xiaomi');
   ```

   ```sql
   INSERT INTO producto(codigo, nombre, precio, codigo_fabricante) 
   VALUES 
   (1, 'Disco duro SATA3 1TB', 86.99, 5), (2, 'Memoria RAM DDR4 8GB', 120, 6), 
   (3, 'Disco SSD 1TB', 150.99, 4), (4, 'GeForce GTX 1050Ti', 185, 7), 
   (5, 'GeForce GTX 1080 Xtreme', 755, 6), (6, 'Monitor 24 LED Full HD', 202, 1), 
   (7, 'Monitor 27 LED Full HD', 245.99, 1), (8, 'Portatil Yoga 520', 559, 2), 
   (9, 'Portatil Ideapad 320', 444, 2), (10, 'Impresora HP Deskjet', 59.99, 3), 
   (11, 'Impresora HP Laserjet Pro M26w', 180, 3);
   
   ```

   

## Consultas sobre una tabla

1. Lista el nombre de todos los productos que hay en la tabla producto.

   ```sql
   SELECT 
   	p.nombre
   FROM 
   	producto AS p
   ```

2. Lista los nombres y los precios de todos los productos de la tabla producto.

   ```sql
   SELECT 
   	p.nombre, 
   	p.precio
   FROM 
   	producto AS p
   ```

3. Lista todas las columnas de la tabla producto.  INTENTA *

   ```sql
   SELECT 
   	p.codigo, 
   	p.nombre, 
   	p.precio, 
   	p.codigo_fabricante
   FROM 
   	producto AS p
   ```

4. Lista el nombre de los productos, el precio en euros y el precio en dólares
   estadounidenses (USD).

   ```sql
   SELECT 
   	(p.precio * 0.25) AS 'Euros',
   	(p.precio * 0.26) AS 'Dolares'
   FROM
   	producto AS p;
   ```

5. Lista el nombre de los productos, el precio en euros y el precio en dólares
   estadounidenses (USD). Utiliza los siguientes alias para las columnas: nombre
   de producto, euros, dólares.

   ```sql
   SELECT 
   	(p.nombre) AS 'Nombre de producto',
   	(p.precio * 0.25) AS 'Euros',
   	(p.precio * 0.26) AS 'Dolares'
   FROM
   	producto AS p;
   ```

6. Lista los nombres y los precios de todos los productos de la tabla producto,
   convirtiendo los nombres a mayúscula.

   ```sql
   SELECT 
   	UPPER(p.nombre) AS 'Nombre',
   	p.precio AS 'Precio'
   FROM
   	producto AS p;
   ```

   [UPPER()](https://www.w3schools.com/sql/func_sqlserver_upper.asp)

7. Lista los nombres y los precios de todos los productos de la tabla producto,
   convirtiendo los nombres a minúscula.

   ```sql
   SELECT 
   	LOWER(p.nombre),
   	p.precio
   FROM
   	producto AS p;
   ```

   [LOWER()](https://www.w3schools.com/sql/func_sqlserver_lower.asp)

8. Lista el nombre de todos los fabricantes en una columna, y en otra columna
   obtenga en mayúsculas los dos primeros caracteres del nombre del
   fabricante.

   ```sql
   SELECT
   	f.nombre
   	UPPER(SUBSTRING(f.nombre, 1, 2))
   FROM
   	fabricante AS f
   ```

   [SUBSTRING()](https://www.w3schools.com/sql/func_sqlserver_substring.asp)

9. Lista los nombres y los precios de todos los productos de la tabla producto,
   redondeando el valor del precio.

   ````sql
   SELECT 
   	p.nombre,
   	ROUND(p.precio)
   FROM
   	producto AS p;
   ````

   [ROUND()](https://www.w3schools.com/sql/func_sqlserver_round.asp)

10. Lista los nombres y los precios de todos los productos de la tabla producto,
    truncando el valor del precio para mostrarlo sin ninguna cifra decimal.

    `````sql
    SELECT 
        p.nombre,
    	TRUNCATE(p.precio)
    FROM 
        producto;
    `````

11. Lista el identificador de los fabricantes que tienen productos en la
    tabla producto.

    ````sql
    SELECT 
    	f.codigo
    FROM 
    	fabricante AS f,
    	producto AS p
    WHERE
    	f.codigo = p.codigo_fabricante;
    ````

12. Lista el identificador de los fabricantes que tienen productos en la
    tabla producto, eliminando los identificadores que aparecen repetidos.

    `````sql
    SELECT DISTINCT
        p.codigo_fabricante
    FROM 
        producto AS p;
    `````

    [DISTINCT](https://www.w3schools.com/sql/sql_distinct.asp)

13. Lista los nombres de los fabricantes ordenados de forma ascendente.

    ````sql
    SELECT 
        f.nombre
    FROM 
        fabricante AS f
    ORDER BY
    	f.nombre ASC;
    ````

    [ORDER BY](https://www.w3schools.com/sql/sql_orderby.asp)

    [ASC](https://www.w3schools.com/sql/sql_ref_asc.asp)

14. Lista los nombres de los fabricantes ordenados de forma descendente.

    ````sql
    SELECT
        f.nombre
    FROM 
        fabricante AS f
    ORDER BY
    	f.nombre DESC;
    ````

    [DESC](https://www.w3schools.com/sql/sql_ref_desc.asp)

15. Lista los nombres de los productos ordenados en primer lugar por el
    nombre de forma ascendente y en segundo lugar por el precio de forma
    descendente.

    `````sql
    SELECT
        p.nombre,
        p.precio
    FROM 
        producto AS p
    ORDER BY
    	p.nombre ASC,
    	p.precio DESC;
    `````

16. Devuelve una lista con las 5 primeras filas de la tabla fabricante.

    ````sql
    SELECT
    	f.codigo,
    	f.nombre
    FROM
    	fabricante AS f
    LIMIT 5;
    	
    ````

    [LIMIT](https://www.w3schools.com/sql/sql_ref_limit.asp)

17. Devuelve una lista con 2 filas a partir de la cuarta fila de la tabla fabricante.
    La cuarta fila también se debe incluir en la respuesta.

    `````sql
    SELECT
    	f.codigo,
    	f.nombre
    FROM
    	fabricante AS f
    LIMIT 2 OFFSET 3;
    `````

18. Lista el nombre y el precio del producto más barato. (Utilice solamente las
    cláusulas ORDER BY y LIMIT)

    ````sql
    SELECT
        p.nombre,
        p.precio
    FROM 
        producto AS p
    ORDER BY
    	p.precio ASC
    LIMIT 1;
    ````

19. Lista el nombre y el precio del producto más caro. (Utilice solamente las
    cláusulas ORDER BY y LIMIT)

    ````sql
    SELECT
        p.nombre,
        p.precio
    FROM 
        producto AS p
    ORDER BY
    	p.precio DESC
    LIMIT 1;
    ````

20. Lista el nombre de todos los productos del fabricante cuyo identificador de
    fabricante es igual a 2.

    ````sql
    SELECT
        p.nombre,
        p.precio
    FROM 
        producto AS p
    WHERE
    	p.codigo_fabricante = 2;
    ````

21. Lista el nombre de los productos que tienen un precio menor o igual a 120€.

    ````sql
    SELECT
        p.nombre
    FROM 
        producto AS p
    WHERE
    	p.precio <= 120;
    ````

22. Lista el nombre de los productos que tienen un precio mayor o igual a 400€.

    ````sql
    SELECT
        p.nombre
    FROM 
        producto AS p
    WHERE
    	p.precio >= 400;
    ````

23. Lista el nombre de los productos que no tienen un precio mayor o igual a
    400€.

    ````sql
    SELECT
        p.nombre
    FROM 
        producto AS p
    WHERE
    	p.precio < 400;
    ````

24. Lista todos los productos que tengan un precio entre 80€ y 300€. Sin utilizar
    el operador BETWEEN.

    ````sql
    SELECT
        p.nombre
    FROM 
        producto AS p
    WHERE
    	p.precio BETWEEN 80 AND 300;
    ````

    [BETWEEN](https://www.w3schools.com/sql/sql_ref_between.asp)

25. Lista todos los productos que tengan un precio entre 60€ y 200€. Utilizando
    el operador BETWEEN.

    ````sql
    SELECT
        p.nombre
    FROM 
        producto AS p
    WHERE
    	p.precio BETWEEN 60 AND 200;
    ````

26. Lista todos los productos que tengan un precio mayor que 200€ y que el
    identificador de fabricante sea igual a 6.

    ````sql
    SELECT
        p.nombre
    FROM 
        producto AS p
    WHERE
    	(p.precio > 200) AND (p.codigo_fabricante = 6);
    ````

27. Lista todos los productos donde el identificador de fabricante sea 1, 3 o 5.
    Sin utilizar el operador IN.

    ````sql
    SELECT
        p.nombre
    FROM 
        producto AS p
    WHERE
    	p.codigo_fabricante IN (1, 3, 5);
    ````

    [IN](https://www.w3schools.com/sql/sql_ref_in.asp)

28. Lista todos los productos donde el identificador de fabricante sea 1, 3 o 5.
    Utilizando el operador IN.

    ````sql
    SELECT
        p.nombre
    FROM 
        producto AS p
    WHERE
    	p.codigo_fabricante IN (1, 3, 5);
    ````

29. Lista el nombre y el precio de los productos en céntimos (Habrá que
    multiplicar por 100 el valor del precio). Cree un alias para la columna que
    contiene el precio que se llame céntimos.

    ````sql
    SELECT
        p.nombre
        (P.precio * 100) AS 'centimos'
    FROM 
        producto AS p;
    ````

30. Lista los nombres de los fabricantes cuyo nombre empiece por la letra S.

    `````sql
    SELECT
    	f.nombre
    FROM
    	fabricante AS f
    WHERE
    	f.nombre LIKE 'S%';
    `````

    [LIKE](https://www.w3schools.com/sql/sql_ref_like.asp)

31. Lista los nombres de los fabricantes cuyo nombre termine por la vocal e.

    ````sql
    SELECT
    	f.nombre
    FROM
    	fabricante AS f
    WHERE
    	f.nombre LIKE '%e';
    ````

32. Lista los nombres de los fabricantes cuyo nombre contenga el carácter w.

    `````sql
    SELECT
    	f.nombre
    FROM
    	fabricante AS f
    WHERE
    	f.nombre LIKE '%w%';
    `````

33. Lista los nombres de los fabricantes cuyo nombre sea de 4 caracteres.

    ````sql
    SELECT
    	f.nombre
    FROM
    	fabricante AS f
    WHERE
    	LENGTH(f.nombre) = 4;
    ````

34. Devuelve una lista con el nombre de todos los productos que contienen la
    cadena Portátil en el nombre.

    ````sql
    SELECT
        p.nombre
    FROM 
        producto AS p
    WHERE 
    	p.nombre LIKE '%Portatil%';
    ````

35. Devuelve una lista con el nombre de todos los productos que contienen la
    cadena Monitor en el nombre y tienen un precio inferior a 215 €.

    ````sql
    SELECT
        p.nombre
    FROM 
        producto AS p
    WHERE 
    	(p.nombre LIKE '%Monitor%') AND (p.precio < 215);
    ````

36. Lista el nombre y el precio de todos los productos que tengan un precio
    mayor o igual a 180€. Ordene el resultado en primer lugar por el precio (en
    orden descendente) y en segundo lugar por el nombre (en orden
    ascendente).

    `````sql
    SELECT
        p.nombre,
        p.precio
    FROM 
        producto AS p
    WHERE 
    	p.precio >= 180
    ORDER BY
    	p.precio DESC,
    	p.nombre ASC;
    `````

## Consultas multitabla (Composición interna)

Resuelva todas las consultas utilizando la sintaxis de SQL1 y SQL2.

1. Devuelve una lista con el nombre del producto, precio y nombre de
   fabricante de todos los productos de la base de datos.

   `````sql
   `````

2. Devuelve una lista con el nombre del producto, precio y nombre de
   fabricante de todos los productos de la base de datos. Ordene el resultado
   por el nombre del fabricante, por orden alfabético.

   ````sql
   ````

3. Devuelve una lista con el identificador del producto, nombre del producto,
   identificador del fabricante y nombre del fabricante, de todos los productos
   de la base de datos.

   ````sql
   ````

4. Devuelve el nombre del producto, su precio y el nombre de su fabricante,
   del producto más barato.

   ````sql
   ````

5. Devuelve el nombre del producto, su precio y el nombre de su fabricante,
   del producto más caro.

   ````sql
   ````

6. Devuelve una lista de todos los productos del fabricante Lenovo.

   `````sql
   
   `````

7. Devuelve una lista de todos los productos del fabricante Crucial que tengan
   un precio mayor que 200€.

   ````sql
   ````

8. Devuelve un listado con todos los productos de los
   fabricantes Asus, Hewlett-Packardy Seagate. Sin utilizar el operador IN.

   ````sql
   ````

9. Devuelve un listado con todos los productos de los
   fabricantes Asus, Hewlett-Packardy Seagate. Utilizando el operador IN.

   ````sql
   ````

10. Devuelve un listado con el nombre y el precio de todos los productos de los
    fabricantes cuyo nombre termine por la vocal e.

    `````sql
    `````

11. Devuelve un listado con el nombre y el precio de todos los productos cuyo
    nombre de fabricante contenga el carácter w en su nombre.

    ````sql
    ````

12. Devuelve un listado con el nombre de producto, precio y nombre de
    fabricante, de todos los productos que tengan un precio mayor o igual a
    180€. Ordene el resultado en primer lugar por el precio (en orden
    descendente) y en segundo lugar por el nombre (en orden ascendente)

    ````sql
    ````

13. Devuelve un listado con el identificador y el nombre de fabricante,
    solamente de aquellos fabricantes que tienen productos asociados en la
    base de datos.

    ````sql
    ````

    

