# Taller desarrollo de Base de datos

1. Creacion de la BASE DE DATOS 

   ```sql
   CREATE TABLE producto
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
   INSERT INTO producto(codigo, nombre, precio, codigo_frabricante)
   VALUES 
   (1, 'Disco duro SATA3 1TB', 86.99, 5), (2, 'Memoria RAM DDR4 8GB', 120, 6),
   (3, 'Disco SSD 1TB', 150.99, 4), (4, 'GeForce GTX 1050Ti', 185, 7),
   (5, 'GeForce GTX 1080 Xtreme', 755, 6), (6, 'Monitor 24 LED Full HD', 202, 1),
   (7, 'Monitor 27 LED Full HD', 245.99, 1), (8, 'Portatil Yoga 520', 559, 2),
   (9, 'Portatil Ideapad 320', 444, 2), (10, 'Impresora HP Deskjet', 59.99, 3), 
   (11, 'Impresora HP Laserjet Pro M26w', 180, 3)
   
   ```

   

## Consultas sobre una tabla

1. Lista el nombre de todos los productos que hay en la tabla producto.

   ```sql
   SELECT p.nombre
   FROM producto AS p
   ```

2. Lista los nombres y los precios de todos los productos de la tabla producto.

   ```sql
   SELECT p.nombre p.precio
   FROM producto AS p
   ```

3. Lista todas las columnas de la tabla producto. 

   ```sql
   
   ```

4. Lista el nombre de los productos, el precio en euros y el precio en dólares
   estadounidenses (USD).

   ```sql
   
   ```

5. Lista el nombre de los productos, el precio en euros y el precio en dólares
   estadounidenses (USD). Utiliza los siguientes alias para las columnas: nombre
   de producto, euros, dólares.

   ```sql
   
   ```

6. Lista los nombres y los precios de todos los productos de la tabla producto,
   convirtiendo los nombres a mayúscula.

   ```sql
   
   ```

7. Lista los nombres y los precios de todos los productos de la tabla producto,
   convirtiendo los nombres a minúscula.

   ```sql
   
   ```

8. Lista el nombre de todos los fabricantes en una columna, y en otra columna
   obtenga en mayúsculas los dos primeros caracteres del nombre del
   fabricante.

   ```sql
   
   ```

9. 

