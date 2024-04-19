### Taller2

#### Creación de la base de datos

```sql
CREATE DATABASE taller2;
```

#### Creación de tablas

```sql
CREATE TABLE departamento(
    codigo INT(10) PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(100) NOT NULL,
    presupuesto DOUBLE NOT NULL,
    gasto DOUBLE NOT NULL
);

CREATE TABLE empleado(
    codigo INT(10) PRIMARY KEY AUTO_INCREMENT,
    nit VARCHAR(9) NOT NULL,
    nombre VARCHAR(100) NOT NULL,
    apellido1 VARCHAR(9) NOT NULL,
    apellido2 VARCHAR(100),
    codigo_dpto INT(10),
    CONSTRAINT FK_empleadoDpto
    FOREIGN KEY (codigo_dpto)
    REFERENCES departamento(codigo)
);
```

#### Inserción de datos en las tablas

```sql
INSERT INTO departamento (nombre, presupuesto, gasto)
VALUES ('Sistemas', 150000, 21000),
       ('Recursos Humanos', 280000, 25000),
       ('Contabilidad', 110000, 3000),
       ('I+D', 375000, 380000),
       ('Proyectos', 0, 0),
       ('Publicidad', 0, 1000);

INSERT INTO empleado (nit, nombre, apellido1, apellido2, codigo_dpto)
VALUES ('32481596F', 'Aarón', 'Rivero', 'Gómez', 1),
       ('Y5575632D', 'Adela', 'Salas', 'Díaz', 2),
       ('R6970642B', 'Adolfo', 'Rubio', 'Flores', 3),
       ('77705545E', 'Adrián', 'Suárez', NULL, 4),
       ('17087203C', 'Marcos', 'Loyola', 'Méndez', 5),
       ('38382980M', 'María', 'Santana', 'Moreno', 1),
       ('80576669X', 'Pilar', 'Ruiz', NULL, 2),
       ('71651431Z', 'Pepe', 'Ruiz', 'Santana', 3),
       ('56399183D', 'Juan', 'Gómez', 'López', 2),
       ('46384486H', 'Diego', 'Flores', 'Salas', 5),
       ('67389283A', 'Marta', 'Herrera', 'Gil', 1),
       ('41234836R', 'Irene', 'Salas', 'Flores', NULL),
       ('82635162B', 'Juan Antonio', 'Sáez', 'Guerrero', NULL);
```

---

##### 1: Lista el primer apellido de todos los empleados

```sql
SELECT apellido1 FROM empleado;
```

```
+-----------+
| apellido1 |
+-----------+
| Rivero    |
| Salas     |
| Rubio     |
| Suárez    |
| Loyola    |
| Santana   |
| Ruiz      |
| Ruiz      |
| Gómez     |
| Flores    |
| Herrera   |
| Salas     |
| Sáez      |
+-----------+
```

---

##### 2: Lista el primer apellido de los empleados eliminando los apellidos que estén repetidos.

```sql
SELECT DISTINCT apellido1 FROM empleado;
```

```
+-----------+
| apellido1 |
+-----------+
| Rivero    |
| Salas     |
| Rubio     |
| Suárez    |
| Loyola    |
| Santana   |
| Ruiz      |
| Gómez     |
| Flores    |
| Herrera   |
| Sáez      |
+-----------+


```

##### 3.SELECT codigo, nombre, apellido1, apellido2, codigo_dpto FROM empleado; 

```sql
SELECT codigo, nombre, apellido1, apellido2, codigo_dpto
FROM empleado;
```

```markdown
| codigo | nombre       | apellido1 | apellido2 | codigo_dpto |
|--------|--------------|-----------|-----------|-------------|
|      1 | Aarón        | Rivero    | Gómez     |           1 |
|      2 | Adela        | Salas     | Díaz      |           2 |
|      3 | Adolfo       | Rubio     | Flores    |           3 |
|      4 | Adrián       | Suárez    | NULL      |           4 |
|      5 | Marcos       | Loyola    | Méndez    |           5 |
|      6 | María        | Santana   | Moreno    |           1 |
|      7 | Pilar        | Ruiz      | NULL      |           2 |
|      8 | Pepe         | Ruiz      | Santana   |           3 |
|      9 | Juan         | Gómez     | López     |           2 |
|     10 | Diego        | Flores    | Salas     |           5 |
|     11 | Marta        | Herrera   | Gil       |           1 |
|     12 | Irene        | Salas     | Flores    |        NULL |
|     13 | Juan Antonio | Sáez      | Guerrero  |        NULL |
```



##### 4: Lista el nombre y los apellidos de todos los empleados.

```sql
SELECT nombre, apellido1, apellido2
FROM empleado;
```

```
+--------------+-----------+-----------+
| nombre       | apellido1 | apellido2 |
+--------------+-----------+-----------+
| Aarón        | Rivero    | Gómez     |
| Adela        | Salas     | Díaz      |
| Adolfo       | Rubio     | Flores    |
| Adrián       | Suárez    | NULL      |
| Marcos       | Loyola    | Méndez    |
| María        | Santana   | Moreno    |
| Pilar        | Ruiz      | NULL      |
| Pepe         | Ruiz      | Santana   |
| Juan         | Gómez     | López     |
| Diego        | Flores    | Salas     |
| Marta        | Herrera   | Gil       |
| Irene        | Salas     | Flores    |
| Juan Antonio | Sáez      | Guerrero  |
+--------------+-----------+-----------+
```

---

##### 5: Lista el identificador de los departamentos de los empleados que aparecen en la tabla empleado

```sql
SELECT codigo_dpto
FROM empleado;
```

```
+-------------+
| codigo_dpto |
+-------------+
|        NULL |
|        NULL |
|           1 |
|           1 |
|           1 |
|           2 |
|           2 |
|           2 |
|           3 |
|           3 |
|           4 |
|           5 |
|           5 |
+-------------+
```

---

##### 6: Lista el identificador de los departamentos de los empleados que aparecen en la tabla empleado, eliminando los identificadores que aparecen repetidos.

```sql
SELECT DISTINCT codigo_dpto
FROM empleado;
```

```
+-------------+
| codigo_dpto |
+-------------+
|        NULL |
|           

 1|
|            2|
|            3|
|            4|
|            5|
+-------------+
```

---

##### 7: Lista el nombre y apellidos de los empleados en una única columna.

```sql
SELECT CONCAT(nombre,' ',apellido1,' ',apellido2) AS 'Nombre Completo'
FROM empleado;
```

```
+-----------------------------+
| Nombre Completo             |
+-----------------------------+
| Aarón Rivero Gómez          |
| Adela Salas Díaz            |
| Adolfo Rubio Flores         |
| NULL                        |
| Marcos Loyola Méndez        |
| María Santana Moreno        |
| NULL                        |
| Pepe Ruiz Santana           |
| Juan Gómez López            |
| Diego Flores Salas          |
| Marta Herrera Gil           |
| Irene Salas Flores          |
| Juan Antonio Sáez Guerrero  |
+-----------------------------+
```

---

##### 8: Lista el nombre y apellidos de los empleados en una única columna, convirtiendo todos los caracteres en mayúscula

```sql
SELECT UPPER(CONCAT(nombre,' ',apellido1,' ',apellido2)) AS 'Nombre Completo'
FROM empleado;
```

```
+-----------------------------+
| Nombre Completo             |
+-----------------------------+
| AARÓN RIVERO GÓMEZ          |
| ADELA SALAS DÍAZ            |
| ADOLFO RUBIO FLORES         |
| NULL                        |
| MARCOS LOYOLA MÉNDEZ        |
| MARÍA SANTANA MORENO        |
| NULL                        |
| PEPE RUIZ SANTANA           |
| JUAN GÓMEZ LÓPEZ            |
| DIEGO FLORES SALAS          |
| MARTA HERRERA GIL           |
| IRENE SALAS FLORES          |
| JUAN ANTONIO SÁEZ GUERRERO  |
+-----------------------------+
```

##### 9: Lista el nombre y apellidos de los empleados en una única columna, convirtiendo todos los caracteres en minúscula.

```sql
SELECT LOWER(CONCAT(nombre,' ',apellido1,' ',apellido2)) AS 'Nombre Completo'
FROM empleado;
```

```
+-----------------------------+
| Nombre Completo             |
+-----------------------------+
| aarón rivero gómez          |
| adela salas díaz            |
| adolfo rubio flores         |
| NULL                        |
| marcos loyola méndez        |
| maría santana moreno        |
| NULL                        |
| pepe ruiz santana           |
| juan gómez lópez            |
| diego flores salas          |
| marta herrera gil           |
| irene salas flores          |
| juan antonio sáez guerrero  |
+-----------------------------+
```

---

##### 10: Lista el identificador de los empleados junto al NIF, pero el NIF deberá aparecer en dos columnas, una mostrará únicamente los dígitos del NIF y la otra la letra.

```sql
SELECT codigo, SUBSTR(nif, 1, 8) AS 'NIF Dígitos', SUBSTR(nif, 9, 9) AS 'NIF Letra'
FROM empleado;
```

```
+--------+-------------------+-------------------+
| codigo | NIF Dígitos       | NIF Letra         |
+--------+-------------------+-------------------+
|      1 | 32481596          | F                 |
|      2 | Y5575632          | D                 |
|      3 | R6970642          | B                 |
|      4 | 77705545          | E                 |
|      5 | 17087203          | C                 |
|      6 | 38382980          | M                 |
|      7 | 80576669          | X                 |
|      8 | 71651431          | Z                 |
|      9 | 56399183          | D                 |
|     10 | 46384486          | H                 |
|     11 | 67389283          | A                 |
|     12 | 41234836          | R                 |
|     13 | 82635162          | B                 |
+--------+-------------------+-------------------+
```

---

##### 11: Lista el nombre de cada departamento y el valor del presupuesto actual del que dispone. Para calcular este dato tendrá que restar al valor del presupuesto inicial (columna presupuesto) los gastos que se han generado (columna gastos). Tenga en cuenta que en algunos casos pueden existir valores negativos. Utilice un alias apropiado para la nueva columna que está calculando.

```sql
SELECT nombre, presupuesto - gasto AS 'Presupuesto Actual'
FROM departamento;
```

```
+------------------+--------------------+
| nombre           | Presupuesto Actual |
+------------------+--------------------+
| Sistemas         |             129000 |
| Recursos Humanos |             255000 |
| Contabilidad     |             107000 |
| I+D              |              -5000 |
| Proyectos        |                  0 |
| Publicidad       |              -1000 |
+------------------+--------------------+
```

---

##### 12: Lista el nombre de los departamentos y el valor del presupuesto actual ordenado de forma ascendente.

```sql
SELECT nombre, presupuesto - gasto AS presupuesto_actual 
FROM departamento
ORDER BY presupuesto_actual ASC;
```

```
+------------------+--------------------+
| nombre           | presupuesto_actual |
+------------------+--------------------+
| I+D              |              -5000 |
| Publicidad       |              -1000 |
| Proyectos        |                  0 |
| Contabilidad     |             107000 |
| Desarrollo       |             114000 |
| Sistemas         |             129000 |
| Recursos Humanos |             255000 |
+------------------+--------------------+
```

---

##### 13: Lista el nombre de todos los departamentos ordenados de forma ascendente.

```sql
SELECT nombre 
FROM departamento 
ORDER BY nombre ASC;
```

```
+------------------+
| nombre           |
+------------------+
| Contabilidad     |
| Desarrollo       |
| I+D              |
| Proyectos        |
| Publicidad       |
| Recursos Humanos |
| Sistemas         |
+------------------+
```

---

##### 14: Lista el nombre de todos los departamentos ordenados de forma descendente.

```sql
SELECT nombre 
FROM departamento
ORDER BY nombre DESC;
```

```
+------------------+
| nombre           |
+------------------+
| Sistemas         |
| Recursos Humanos |
| Publicidad       |
| Proyectos        |
| I+D              |
| Desarrollo       |
| Contabilidad     |
+------------------+
```

---

##### 15: Lista los apellidos y el nombre de todos los empleados, ordenados de forma alfabética teniendo en cuenta en primer lugar sus apellidos y luego su nombre.

```sql
SELECT apellido1, apellido2, nombre 
FROM empleado
ORDER BY apellido1, apellido2, nombre ASC;
```

```
+-----------+-----------+--------------+
| apellido1 | apellido2 | nombre       |
+-----------+-----------+--------------+
| Flores    | Salas     | Diego        |
| Gómez     | López     | Juan         |
| Herrera   | Gil       | Marta        |
| Loyola    | Méndez    | Marcos       |
| Rivero    | Gómez     | Aarón        |
| Rubio     | Flores    | Adolfo       |
| Ruiz      | NULL      | Pilar        |
| Ruiz      | Santana   | Pepe         |
| Sáez      | Guerrero  | Juan Antonio |
| Salas     | Díaz      | Adela        |
| Salas     | Flores    | Irene        |
| Santana   | Moreno    | María        |
| Suárez    | NULL      | Adrián       |
+-----------+-----------+--------------+
```

---

##### 16: Devuelve una lista con el nombre y el presupuesto, de los 3 departamentos que tienen mayor presupuesto.

```sql
SELECT nombre, presupuesto 
FROM departamento
ORDER BY presupuesto DESC
LIMIT 3;
```

```
+------------------+-------------+
| nombre           | presupuesto |
+------------------+-------------+
| Recursos Humanos |      280000 |
| I+D              |      375000 |
| Sistemas         |      150000 |
+------------------+-------------+
```

---

##### 17: Devuelve una lista con el nombre y el presupuesto, de los 3 departamentos que tienen menor presupuesto.

```sql
SELECT nombre, presupuesto 
FROM departamento 
ORDER BY presupuesto ASC
LIMIT 3;
```

```
+------------------+-------------+
| nombre           | presupuesto |
+------------------+-------------+
| Contabilidad     |      110000 |
| Proyectos        |           0 |
| Publicidad       |           0 |
+------------------+-------------+
```

---

##### 18: Devuelve una lista con el nombre y el gasto, de los 2 departamentos que tienen mayor gasto.

```sql
SELECT nombre, gasto
FROM departamento 
ORDER BY gasto DESC 
LIMIT 2;
```

```
+------------------+--------+
| nombre           | gasto  |
+------------------+--------+
| I+D              | 380000 |
| Recursos Humanos |  25000 |
+------------------+--------+
```

---

##### 19: Devuelve una lista con el nombre y el gasto, de los 2 departamentos que tienen menor gasto.

```sql
SELECT nombre, gasto
FROM departamento
ORDER BY gasto ASC LIMIT 2;
```

```
+------------+-------+
| nombre     | gasto |
+------------+-------+
| Proyectos  |     0 |
| Publicidad |  1000 |
+------------+-------+
```

---

##### 20: Devuelve una lista con 5 filas a partir de la tercera fila de la tabla empleado. La tercera fila se debe incluir en la respuesta. La respuesta debe incluir todas las columnas de la tabla empleado.

```sql
SELECT codigo, nif, nombre, apellido1, apellido2, codigo_dpto
FROM empleado 
LIMIT 2, 5;
```

```
+--------+-----------+---------+-----------+-----------+-------------+
| codigo | nif       | nombre  | apellido1 | apellido2 | codigo_dpto |
+--------+-----------+

---------+-----------+-----------+-------------+
|      3 | R6970642B | Adolfo  | Rubio     | Flores    |           3 |
|      4 | 77705545E | Adrián  | Suárez    | NULL      |           4 |
|      5 | 17087203C | Marcos  | Loyola    | Méndez    |           5 |
|      6 | 38382980M | María   | Santana   | Moreno    |           1 |
|      7 | 80576669X | Pilar   | Ruiz      | NULL      |           2 |
+--------+-----------+---------+-----------+-----------+-------------+
```

---

##### 21: Devuelve una lista con el nombre de los departamentos y el presupuesto, de aquellos que tienen un presupuesto mayor o igual a 150000 euros.

```sql
SELECT nombre, presupuesto 
FROM departamento
WHERE presupuesto >= 150000;
```

```
+------------------+-------------+
| nombre           | presupuesto |
+------------------+-------------+
| Sistemas         |      150000 |
| Recursos Humanos |      280000 |
| I+D              |      375000 |
+------------------+-------------+
```

---

##### 22: Devuelve una lista con el nombre de los departamentos y el gasto, de aquellos que tienen menos de 5000 euros de gastos.

```sql
SELECT nombre, gasto
FROM departamento 
WHERE gasto < 5000;
```

```
+------------------+-------+
| nombre           | gasto |
+------------------+-------+
| Proyectos        |     0 |
| Publicidad       |  1000 |
+------------------+-------+
```

---

##### 23: Devuelve una lista con el nombre de los departamentos y el presupuesto, de aquellos que tienen un presupuesto entre 100000 y 200000 euros. Sin utilizar el operador BETWEEN.

```sql
SELECT nombre, presupuesto 
FROM departamento
WHERE presupuesto >= 100000 
AND presupuesto <= 200000;
```

```
+--------------+-------------+
| nombre       | presupuesto |
+--------------+-------------+
| Desarrollo   |      120000 |
| Sistemas     |      150000 |
| Contabilidad |      110000 |
+--------------+-------------+
```

---

##### 24: Devuelve una lista con el nombre de los departamentos que no tienen un presupuesto entre 100000 y 200000 euros. Sin utilizar el operador BETWEEN.

```sql
SELECT nombre, presupuesto 
FROM departamento 
WHERE presupuesto < 100000 
OR presupuesto > 200000;
```

```
+------------------+-------------+
| nombre           | presupuesto |
+------------------+-------------+
| Recursos Humanos |      280000 |
| I+D              |      375000 |
| Proyectos        |           0 |
| Publicidad       |           0 |
+------------------+-------------+
```

---

##### 25: Devuelve una lista con el nombre de los departamentos que tienen un presupuesto entre 100000 y 200000 euros. Utilizando el operador BETWEEN.

```sql
SELECT nombre, presupuesto 
FROM departamento 
WHERE presupuesto BETWEEN 100000 AND 200000;
```

```
+--------------+-------------+
| nombre       | presupuesto |
+--------------+-------------+
| Desarrollo   |      120000 |
| Sistemas     |      150000 |
| Contabilidad |      110000 |
+--------------+-------------+
```

---

##### 26: Devuelve una lista con el nombre de los departamentos que no tienen un presupuesto entre 100000 y 200000 euros. Utilizando el operador BETWEEN.

```sql
SELECT nombre, presupuesto 
FROM departamento 
WHERE presupuesto NOT BETWEEN 100000 AND 200000;
```

```
+------------------+-------------+
| nombre           | presupuesto |
+------------------+-------------+
| Recursos Humanos |      280000 |
| I+D              |      375000 |
| Proyectos        |           0 |
| Publicidad       |           0 |
+------------------+-------------+
```

##### 27: Departamentos con gastos mayores que presupuesto
```sql
SELECT nombre, gasto, presupuesto 
FROM departamento
WHERE gasto > presupuesto;
```
```markdown
| nombre     | gasto  | presupuesto |
|------------|--------|-------------|
| I+D        | 380000 |      375000 |
| Publicidad |   1000 |           0 |
```

##### 28: Departamentos con gastos menores que presupuesto
```sql
SELECT nombre, gasto, presupuesto 
FROM departamento 
WHERE gasto < presupuesto;
```
```markdown
| nombre           | gasto | presupuesto |
|------------------|-------|-------------|
| Desarrollo       |  6000 |      120000 |
| Sistemas         | 21000 |      150000 |
| Recursos Humanos | 25000 |      280000 |
| Contabilidad     |  3000 |      110000 |
```

##### 29: Departamentos con gastos iguales al presupuesto
```sql
SELECT nombre, gasto, presupuesto 
FROM departamento 
WHERE gasto = Presupuesto;
```
```markdown
| nombre    | gasto | presupuesto |
|-----------|-------|-------------|
| Proyectos |     0 |           0 |
```

##### 30: Empleados cuyo segundo apellido es NULL
```sql
SELECT codigo, nif, nombre, apellido1, apellido2
FROM empleado 
WHERE apellido2 IS NULL;
```
```markdown
| codigo | nif       | nombre | apellido1 | apellido2 |
|--------|-----------|--------|-----------|-----------|
|      4 | 77705545E | Adrián | Suárez    | NULL      |
|      7 | 80576669X | Pilar  | Ruiz      | NULL      |
```

##### 31: Empleados cuyo segundo apellido no es NULL
```sql
SELECT codigo, nif, nombre, apellido1, apellido2
FROM empleado
WHERE apellido2 IS NOT NULL;
```
```markdown
| codigo | nif       | nombre       | apellido1 | apellido2 |
|--------|-----------|--------------|-----------|-----------|
|      1 | 32481596F | Aarón        | Rivero    | Gómez     |
|      2 | Y5575632D | Adela        | Salas     | Díaz      |
|      3 | R6970642B | Adolfo       | Rubio     | Flores    |
|      5 | 17087203C | Marcos       | Loyola    | Méndez    |
|      6 | 38382980M | María        | Santana   | Moreno    |
|      8 | 71651431Z | Pepe         | Ruiz      | Santana   |
|      9 | 56399183D | Juan         | Gómez     | López     |
|     10 | 46384486H | Diego        | Flores    | Salas     |
|     11 | 67389283A | Marta        | Herrera   | Gil       |
|     12 | 41234836R | Irene        | Salas     | Flores    |
|     13 | 82635162B | Juan Antonio | Sáez      | Guerrero  |
```

##### 32: Empleados cuyo segundo apellido es "López"
```sql
SELECT codigo, nif, nombre, apellido1, apellido2
FROM empleado
WHERE apellido2 = 'López';
```
```markdown
| codigo | nif       | nombre | apellido1 | apellido2 |
|--------|-----------|--------|-----------|-----------|
|      9 | 56399183D | Juan   | Gómez     | López     |
```

##### 33: Empleados cuyo segundo apellido es "Díaz" o "Moreno" (sin utilizar IN)
```sql
SELECT codigo, nif, nombre, apellido1, apellido2
FROM empleado
WHERE apellido2 = 'Díaz' OR apellido2 = 'Moreno';
```
```markdown
| codigo | nif       | nombre | apellido1 | apellido2 |
|--------|-----------|--------|-----------|-----------|
|      2 | Y5575632D | Adela  | Salas     | Díaz      |
|      6 | 38382980M | María  | Santana   | Moreno    |
```

##### 34: Empleados cuyo segundo apellido es "Díaz" o "Moreno" (utilizando IN)
```sql
SELECT codigo, nif, nombre, apellido1, apellido2
FROM empleado
WHERE apellido2 IN ('Díaz','Moreno');
```
```markdown
| codigo | nif       | nombre | apellido1 | apellido2 |
|--------|-----------|--------|-----------|-----------|
|      2 | Y5575632D | Adela  | Salas     | Díaz      |
|      6 | 38382980M | María  | Santana   | Moreno    |
```

##### 35: Empleados que trabajan en el departamento 3
```sql
SELECT nombre, apellido1, apellido2, nif 
FROM empleado 
WHERE codigo_dpto = 3;
```
```markdown
| nombre | apellido1 | apellido2 | nif       |
|--------|-----------|-----------|-----------|
| Adolfo | Rubio     | Flores    | R6970642B |
| Pepe   | Ruiz      | Santana   | 71651431Z |
```

##### 36: Empleados que trabajan en los departamentos 2, 4 o 5
```sql
SELECT nombre, apellido1, apellido2, nif 
FROM empleado 
WHERE codigo_dpto = 2 OR codigo_dpto = 4 OR codigo_dpto = 5;
```
```markdown
| nombre | apellido1 | apellido2 | nif       |
|--------|-----------|-----------|-----------|
| Adela  | Salas     | Díaz      | Y5575632D |
| Pilar  | Ruiz      | NULL      | 80576669X |
| Juan   | Gómez     | López     | 56399183D |
| Adrián | Suárez    | NULL      | 77705545E |
| Marcos | Loyola    | Méndez    | 17087203C |
| Diego  | Flores    | Salas     | 46384486H |
```

### Consultas multitabla (Composición interna)

##### 1: Listado de empleados y datos de los departamentos donde trabajan cada uno

```sql
SELECT e.codigo, e.nif, e.nombre, e.apellido1, e.apellido2, p.codigo, p.nombre, p.presupuesto, p.gasto
FROM empleado e INNER JOIN departamento p
ON e.codigo_dpto = p.codigo;
```
```markdown
| codigo | nif       | nombre  | apellido1 | apellido2 | codigo | nombre           | presupuesto | gasto  |
|--------|-----------|---------|-----------|-----------|--------|------------------|-------------|--------|
| 1      | 32481596F | Aarón   | Rivero    | Gómez     | 1      | Desarrollo       | 120000      | 6000   |
| 6      | 38382980M | María   | Santana   | Moreno    | 1      | Desarrollo       | 120000      | 6000   |
| 11     | 67389283A | Marta   | Herrera   | Gil       | 1      | Desarrollo       | 120000      | 6000   |
| 2      | Y5575632D | Adela   | Salas     | Díaz      | 2      | Sistemas         | 150000      | 21000  |
| 7      | 80576669X | Pilar   | Ruiz      | NULL      | 2      | Sistemas         | 150000      | 21000  |
| 9      | 56399183D | Juan    | Gómez     | López     | 2      | Sistemas         | 150000      | 21000  |
| 3      | R6970642B | Adolfo  | Rubio     | Flores    | 3      | Recursos Humanos | 280000      | 25000  |
| 8      | 71651431Z | Pepe    | Ruiz      | Santana   | 3      | Recursos Humanos | 280000      | 25000  |
| 4      | 77705545E | Adrián  | Suárez    | NULL      | 4      | Contabilidad     | 110000      | 3000   |
| 5      | 17087203C | Marcos  | Loyola    | Méndez    | 5      | I+D              | 375000      | 380000 |
| 10     | 46384486H | Diego   | Flores    | Salas     | 5      | I+D              | 375000      | 380000 |
```

##### 2: Listado de empleados y datos de los departamentos donde trabajan cada uno (ordenado)

```sql
SELECT d.codigo, d.nombre, d.presupuesto, d.gasto, e.codigo, e.nif,e.nombre, e.apellido1, e.apellido2, e.codigo_dpto
FROM empleado e JOIN departamento d ON d.codigo = e.codigo_dpto 
ORDER BY d.nombre ASC, e.apellido1 ASC, e.apellido2 ASC,e.nombre ASC;
```
```markdown
| codigo | nombre           | presupuesto | gasto  | codigo | nif       | nombre  | apellido1 | apellido2 | codigo_dpto |
|--------|------------------|-------------|--------|--------|-----------|---------|-----------|-----------|-------------|
| 4      | Contabilidad     |      110000 |   3000 |      4 | 77705545E | Adrián  | Suárez    | NULL      |           4 |
| 1      | Desarrollo       |      120000 |   6000 |     11 | 67389283A | Marta   | Herrera   | Gil       |           1 |
| 1      | Desarrollo       |      120000 |   6000 |      1 | 32481596F | Aarón   | Rivero    | Gómez     |           1 |
| 1      | Desarrollo       |      120000 |   6000 |      6 | 38382980M | María   | Santana   | Moreno    |           1 |
| 5      | I+D              |      375000 | 380000 |     10 | 46384486H | Diego   | Flores    | Salas     |           5 |
| 5      | I+D              |      375000 | 380000 |      5 | 17087203C | Marcos  | Loyola    | Méndez    |           5 |
| 3      | Recursos Humanos |      280000 |  25000 |      3 | R6970642B | Adolfo  | Rubio     | Flores    |           3 |
| 3      | Recursos Humanos |      280000 |  25000 |      8 | 71651431Z | Pepe    | Ruiz      | Santana   |           3 |
| 2      | Sistemas         |      150000 |  21000 |      9 | 56399183D | Juan    | Gómez     | López     |           2 |
| 2      | Sistemas         |      150000 |  21000 |      7 | 80576669X | Pilar   | Ruiz      | NULL      |           2 |
| 2      | Sistemas         |      150000 |  21000 |      2 | Y5575632D | Adela   | Salas     | Díaz      |           2 |
```

##### **3. Devuelve un listado con el identificador y el nombre del departamento, solamente de aquellos departamentos que tienen empleados.**

```sql
SELECT DISTINCT d.codigo, d.nombre
FROM empleado e JOIN departamento d ON e.codigo_dpto=d.codigo;
```

```plaintext
+--------+------------------+
| codigo | nombre           |
+--------+------------------+
|      1 | Desarrollo       |
|      2 | Sistemas         |
|      3 | Recursos Humanos |
|      4 | Contabilidad     |
|      5 | I+D              |
+--------+------------------+
```

**4. Devuelve un listado con el identificador, el nombre del departamento y el valor del presupuesto actual del que dispone, solamente de aquellos departamentos que tienen empleados. El valor del presupuesto actual lo puede calcular restando al valor del presupuesto inicial (columna presupuesto) el valor de los gastos que ha generado (columna gastos).**

```sql
SELECT d.codigo, d.nombre, d.presupuesto - d.gasto AS 'presupuesto actual'
FROM empleado e JOIN departamento d ON e.codigo_dpto=d.codigo;
```

```plaintext
+--------+------------------+--------------------+
| codigo | nombre           | presupuesto actual |
+--------+------------------+--------------------+
|      1 | Desarrollo       |             114000 |
|      1 | Desarrollo       |             114000 |
|      1 | Desarrollo       |             114000 |
|      2 | Sistemas         |             129000 |
|      2 | Sistemas         |             129000 |
|      2 | Sistemas         |             129000 |
|      3 | Recursos Humanos |             255000 |
|      3 | Recursos Humanos |             255000 |
|      4 | Contabilidad     |             107000 |
|      5 | I+D              |              -5000 |
|      5 | I+D              |              -5000 |
+--------+------------------+--------------------+
```

**5. Devuelve el nombre del departamento donde trabaja el empleado que tiene el nif 38382980M.**

```sql
SELECT d.nombre 
FROM empleado e JOIN departamento d ON e.codigo_dpto=d.codigo
WHERE e.nif = '38382980M';
```

```plaintext
+------------+
| nombre     |
+------------+
| Desarrollo |
+------------+
```

**6. Devuelve el nombre del departamento donde trabaja el empleado Pepe Ruiz Santana.**

```sql
SELECT d.nombre
FROM empleado e JOIN departamento d ON e.codigo_dpto=d.codigo
WHERE e.nombre="Pepe" AND e.apellido1="Ruiz" AND e.apellido2="Santana";
```

```plaintext
+------------------+
| nombre           |
+------------------+
| Recursos Humanos |
+------------------+
```

**7. Devuelve un listado con los datos de los empleados que trabajan en el departamento de I+D. Ordena el resultado alfabéticamente.**

```sql
SELECT e.codigo, e.nif, e.nombre, e.apellido1, e.apellido2, e.codigo_dpto
FROM empleado e JOIN departamento d ON e.codigo_dpto=d.codigo
WHERE d.nombre="I+D" 
ORDER BY e.codigo, e.nif, e.nombre, e.apellido1, e.apellido2, e.codigo_dpto ASC;
```

```plaintext
+--------+-----------+--------+-----------+-----------+-------------+
| codigo | nif       | nombre | apellido1 | apellido2 | codigo_dpto |
+--------+-----------+--------+-----------+-----------+-------------+
|      5 | 17087203C | Marcos | Loyola    | Méndez    |           5 |
|     10 | 46384486H | Diego  | Flores    | Salas     |           5 |
+--------+-----------+--------+-----------+-----------+-------------+
```

**8. Devuelve un listado con los datos de los empleados que trabajan en el departamento de Sistemas, Contabilidad o I+D. Ordena el resultado alfabéticamente.**

```sql
SELECT e.codigo, e.nif, e.nombre, e.apellido1, e.apellido2, e.codigo_dpto
FROM empleado e JOIN departamento d ON e.codigo_dpto=d.codigo
WHERE d.nombre="I+D" OR d.nombre="Sistemas" OR d.nombre="Contabilidad" 
ORDER BY e.codigo, e.nif, e.nombre, e.apellido1, e.apellido2, e.codigo_dpto ASC;
```

```plaintext
+--------+-----------+---------+-----------+-----------+-------------+
| codigo | nif       | nombre  | apellido1 | apellido2 | codigo_dpto |
+--------+-----------+---------+-----------+-----------+-------------+
|      2 | Y5575632D | Adela   | Salas     | Díaz      |           2 |
|      4 | 77705545E | Adrián  | Suárez    | NULL      |           4 |
|      5 | 17087203C | Marcos  | Loyola    | Méndez    |           5 |
|      7 | 80576669X | Pilar   | Ruiz      | NULL      |           2 |
|      9 | 56399183D | Juan    | Gómez     | López     |           2 |
|     10 | 46384486H | Diego   | Flores    | Salas     |           5 |
+--------+-----------+---------+-----------+-----------+-------------+
```

##### 9. Devuelve una lista con el nombre de los empleados que tienen los departamentos que no tienen un presupuesto entre 100000 y 200000 euros.

```sql
SELECT e.nombre
FROM empleado e 
JOIN departamento d ON e.codigo_dpto = d.codigo
WHERE d.presupuesto NOT BETWEEN 100000 AND 200000;
```

```markdown
| nombre |
|--------|
| Adolfo |
| Pepe   |
| Marcos |
| Diego  |
```

##### 10. Devuelve un listado con el nombre de los departamentos donde existe algún empleado cuyo segundo apellido sea NULL. No se deben mostrar nombres de departamentos repetidos.

```sql
SELECT DISTINCT d.nombre
FROM empleado e 
JOIN departamento d ON e.codigo_dpto = d.codigo
WHERE e.apellido2 IS NULL;
```

```markdown
| nombre           |
|------------------|
| Desarrollo       |
| Sistemas         |
| Recursos Humanos |
| Contabilidad     |
```

### Consultas multitabla (Composición externa)

##### 1. Devuelve un listado con todos los empleados junto con los datos de los departamentos donde trabajan. Este listado también debe incluir los empleados que no tienen ningún departamento asociado.

```sql
SELECT e.codigo, CONCAT(e.nombre, ' ', e.apellido1, ' ', IFNULL(e.apellido2, '')) AS 'Nombre Completo', e.codigo_dpto, d.nombre, d.presupuesto, d.gasto
FROM empleado e 
LEFT JOIN departamento d ON d.codigo = e.codigo_dpto;
```

```markdown
| codigo | Nombre Completo           | codigo_dpto | nombre           | presupuesto | gasto |
|--------|---------------------------|-------------|------------------|-------------|-------|
| 1      | Aarón Rivero Gómez        | 1           | Desarrollo       | 120000      | 6000  |
| 2      | Adela Salas Díaz          | 2           | Sistemas         | 150000      | 21000 |
| 3      | Adolfo Rubio Flores       | 3           | Recursos Humanos | 280000      | 25000 |
| 4      | NULL                      | 4           | Contabilidad     | 110000      | 3000  |
| 5      | Marcos Loyola Méndez      | 5           | I+D              | 375000      | 380000|
| 6      | María Santana Moreno      | 1           | Desarrollo       | 120000      | 6000  |
| 7      | NULL                      | 2           | Sistemas         | 150000      | 21000 |
| 8      | Pepe Ruiz Santana         | 3           | Recursos Humanos | 280000      | 25000 |
| 9      | Juan Gómez López          | 2           | Sistemas         | 150000      | 21000 |
| 10     | Diego Flores Salas        | 5           | I+D              | 375000      | 380000|
| 11     | Marta Herrera Gil         | 1           | Desarrollo       | 120000      | 6000  |
| 12     | Irene Salas Flores        | NULL        | NULL             | NULL        | NULL  |
| 13     | Juan Antonio Sáez Guerrero| NULL        | NULL             | NULL        | NULL  |
```

##### 2. Devuelve un listado donde sólo aparezcan aquellos empleados que no tienen ningún departamento asociado.

```sql
SELECT e.codigo, CONCAT(e.nombre, ' ', e.apellido1, ' ', IFNULL(e.apellido2, '')) AS 'Nombre Completo'
FROM empleado e 
LEFT JOIN departamento d ON e.codigo_dpto = d.codigo
WHERE e.codigo_dpto IS NULL;
```

```markdown
| codigo | Nombre Completo           |
|--------|---------------------------|
| 12     | Irene Salas Flores        |
| 13     | Juan Antonio Sáez Guerrero|
```

##### 3. Devuelve un listado donde sólo aparezcan aquellos departamentos que no tienen ningún empleado asociado.

```sql
SELECT d.codigo, d.nombre, d.presupuesto, d.gasto
FROM departamento d 
LEFT JOIN empleado e ON e.codigo_dpto = d.codigo
WHERE e.codigo_dpto IS NULL;
```

```markdown
| codigo | nombre     | presupuesto | gasto |
|--------|------------|-------------|-------|
| 6      | Proyectos  | 0           | 0     |
| 7      | Publicidad | 0           | 1000  |
```

##### 4. Devuelve un listado con todos los empleados junto con los datos de los departamentos donde trabajan. El listado debe incluir los empleados que no tienen ningún departamento asociado y los departamentos que no tienen ningún empleado asociado. Ordene el listado alfabéticamente por el nombre del departamento.

```sql
SELECT e.codigo, CONCAT(e.nombre, ' ', e.apellido1, ' ', IFNULL(e.apellido2, '')) AS 'Nombre Completo', e.codigo_dpto, d.nombre, d.presupuesto, d.gasto
FROM empleado e 
LEFT JOIN departamento d ON e.codigo_dpto = d.codigo
UNION
SELECT e.codigo, CONCAT(e.nombre, ' ', e.apellido1, ' ', IFNULL(e.apellido2, '')) AS 'Nombre Completo', e.codigo_dpto, d.nombre, d.presupuesto, d.gasto
FROM empleado e 
RIGHT JOIN departamento d ON e.codigo_dpto = d.codigo
ORDER BY d.nombre;
```

```markdown
| codigo | Nombre Completo           | codigo_dpto | nombre           | presupuesto | gasto |
|--------|---------------------------|-------------|------------------|-------------|-------|
| 12     | Irene Salas Flores        | NULL        | NULL             | NULL        | NULL  |
| 13     | Juan Antonio Sáez Guerrero| NULL        | NULL             | NULL        | NULL  |
| 4      | NULL                      | 4           | Contabilidad     | 110000      | 3000  |
| 1      | Aarón Rivero Gómez        | 1           | Desarrollo       | 120000      | 6000  |
| 6      | María Santana Moreno      | 1           | Desarrollo       | 120000      | 6000  |
| 11     | Marta Herrera Gil         | 1           | Desarrollo       | 120000      | 6000  |
| 5      | Marcos Loyola Méndez      | 5           | I+D              | 375000      | 380000|
| 10     | Diego Flores Salas        | 5           | I+D              | 375000      | 380000|
| 3

      | Adolfo Rubio Flores       | 3           | Recursos Humanos | 280000      | 25000 |
| 8      | Pepe Ruiz Santana         | 3           | Recursos Humanos | 280000      | 25000 |
| 2      | Adela Salas Díaz          | 2           | Sistemas         | 150000      | 21000 |
| 7      | NULL                      | 2           | Sistemas         | 150000      | 21000 |
| 9      | Juan Gómez López          | 2           | Sistemas         | 150000      | 21000 |
| 6      | Proyectos                 | NULL        | NULL             | 0           | 0     |
| 7      | Publicidad                | NULL        | NULL             | 0           | 1000  |
```

### Consultas resumen

##### 1. Calcula la suma del presupuesto de todos los departamentos.

```sql
SELECT SUM(presupuesto) AS presupuestototal FROM departamento;
```

```markdown
| presupuestototal |
|------------------|
| 1035000          |
```

##### 2. Calcula la media del presupuesto de todos los departamentos.

```sql
SELECT AVG(presupuesto) AS presupuestototal FROM departamento;
```

```markdown
| presupuestototal |
|------------------|
| 207000           |
```

##### 3. Calcula el valor mínimo del presupuesto de todos los departamentos.

```sql
SELECT nombre, presupuesto FROM departamento WHERE presupuesto = (SELECT MIN(presupuesto) FROM departamento);
```

```markdown
| nombre     | presupuesto |
|------------|-------------|
| Proyectos  | 0           |
| Publicidad | 0           |
```

##### 4. Calcula el valor máximo del presupuesto de todos los departamentos.

```sql
SELECT nombre, presupuesto FROM departamento WHERE presupuesto = (SELECT MAX(presupuesto) FROM departamento);
```

```markdown
| nombre | presupuesto |
|--------|-------------|
| I+D    | 375000      |
```

##### 5. Calcula el número total de empleados que hay en la tabla empleado.

```sql
SELECT COUNT(codigo) AS EmpleadosTotales FROM empleado;
```

```markdown
| EmpleadosTotales |
|------------------|
| 13               |
```

##### 6. Calcula el número de empleados que no tienen NULL en su segundo apellido.

```sql
SELECT COUNT(codigo) AS Empleados FROM empleado WHERE apellido2 IS NOT NULL;
```

```markdown
| Empleados |
|-----------|
| 11        |
```

##### 7. Calcula el número de empleados que hay en cada departamento. Devuelve dos columnas, una con el nombre del departamento y otra con el número de empleados que tiene asignados.

```sql
SELECT d.nombre, COUNT(e.codigo) AS NumeroEmpleados 
FROM departamento d 
LEFT JOIN empleado e ON e.codigo_dpto = d.codigo
GROUP BY d.nombre;
```

```markdown
| nombre           | NumeroEmpleados |
|------------------|-----------------|
| Contabilidad     | 1               |
| Desarrollo       | 3               |
| I+D              | 2               |
| Proyectos        | 0               |
| Publicidad       | 0               |
| Recursos Humanos | 2               |
| Sistemas         | 3               |
```

##### 8. Calcula el nombre de los departamentos que tienen más de 2 empleados. Devuelve dos columnas, una con el nombre del departamento y otra con el número de empleados que tiene asignados.

```sql
SELECT d.nombre, COUNT(e.codigo) AS NumeroEmpleados 
FROM departamento d 
LEFT JOIN empleado e ON e.codigo_dpto = d.codigo
GROUP BY d.nombre
HAVING COUNT(e.codigo) > 2;
```

```markdown
| nombre       | NumeroEmpleados |
|--------------|-----------------|
| Desarrollo   | 3               |
| Sistemas     | 3               |
```

##### 9. Calcula el número de empleados que trabajan en cada uno de los departamentos que tienen un presupuesto mayor a 200000 euros.

```sql
SELECT d.nombre, COUNT(e.codigo) AS NumeroEmpleados 
FROM departamento d 
LEFT JOIN empleado e ON e.codigo_dpto = d.codigo
WHERE d.presupuesto > 200000
GROUP BY d.nombre;
```

```markdown
| nombre           | NumeroEmpleados |
|------------------|-----------------|
| Recursos Humanos | 2               |
| I+D              | 2               |
```

### Subconsultas con ALL y ANY

##### 4. Devuelve el nombre del departamento con mayor presupuesto y la cantidad que tiene asignada.

```sql
SELECT nombre, presupuesto 
FROM departamento 
WHERE presupuesto >= ALL (SELECT presupuesto FROM departamento);
```

```markdown
| nombre | presupuesto |
|--------|-------------|
| I+D    |      375000 |
```

##### 5. Devuelve el nombre del departamento con menor presupuesto y la cantidad que tiene asignada.

```sql
SELECT nombre, presupuesto 
FROM departamento 
WHERE presupuesto <= ALL (SELECT presupuesto FROM departamento);
```

```markdown
| nombre     | presupuesto |
|------------|-------------|
| Proyectos  |           0 |
| Publicidad |           0 |
```

##### 6. Devuelve los nombres de los departamentos que tienen empleados asociados. (Utilizando ALL o ANY).

```sql
SELECT d.nombre 
FROM departamento d 
WHERE d.codigo = ANY (SELECT e.codigo_dpto FROM empleado e);
```

```markdown
| nombre           |
|------------------|
| Desarrollo       |
| Sistemas         |
| Recursos Humanos |
| Contabilidad     |
| I+D              |
```

##### 7. Devuelve los nombres de los departamentos que no tienen empleados asociados. (Utilizando ALL o ANY).

```sql
SELECT d.nombre 
FROM departamento d 
WHERE d.codigo IN (SELECT e.codigo_dpto FROM empleado e);
```

```markdown
| nombre           |
|------------------|
| Desarrollo       |
| Sistemas         |
| Recursos Humanos |
| Contabilidad     |
| I+D              |
```

### Subconsultas con IN y NOT IN

##### 8. Devuelve los nombres de los departamentos que tienen empleados asociados. (Utilizando IN o NOT IN).

```sql
SELECT d.nombre 
FROM departamento d 
WHERE d.codigo IN (SELECT e.codigo_dpto FROM empleado e);
```

```markdown
| nombre           |
|------------------|
| Desarrollo       |
| Sistemas         |
| Recursos Humanos |
| Contabilidad     |
| I+D              |
```

##### 9. Devuelve los nombres de los departamentos que no tienen empleados asociados. (Utilizando IN o NOT IN).

```sql
SELECT d.nombre 
FROM departamento d 
WHERE d.codigo NOT IN (SELECT e.codigo_dpto FROM empleado e WHERE e.codigo_dpto IS NOT NULL);
```

```markdown
| nombre     |
|------------|
| Proyectos  |
| Publicidad |
```

### Subconsultas con EXISTS y NOT EXISTS

##### 10. Devuelve los nombres de los departamentos que tienen empleados asociados. (Utilizando EXISTS o NOT EXISTS).

```sql
SELECT d.nombre 
FROM departamento d 
WHERE EXISTS (SELECT e.codigo_dpto FROM empleado e WHERE e.codigo_dpto = d.codigo);
```

```markdown
| nombre           |
|------------------|
| Desarrollo       |
| Sistemas         |
| Recursos Humanos |
| Contabilidad     |
| I+D              |
```

##### 11. Devuelve los nombres de los departamentos que no tienen empleados asociados. (Utilizando EXISTS o NOT EXISTS).

```sql
SELECT d.nombre 
FROM departamento d 
WHERE NOT EXISTS (SELECT e.codigo_dpto FROM empleado e WHERE e.codigo_dpto = d.codigo);
```

```markdown
| nombre     |
|------------|
| Proyectos  |
| Publicidad |
```