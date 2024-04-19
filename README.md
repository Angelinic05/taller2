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

#### Consultas y Resultados

---

¡Claro! Aquí tienes todas las consultas del taller:

---

#### 1: Lista el primer apellido de todos los empleados

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

#### 2: Lista el primer apellido de los empleados eliminando los apellidos que estén repetidos.

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



#### 4: Lista el nombre y los apellidos de todos los empleados.

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

#### 5: Lista el identificador de los departamentos de los empleados que aparecen en la tabla empleado

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

#### 6: Lista el identificador de los departamentos de los empleados que aparecen en la tabla empleado, eliminando los identificadores que aparecen repetidos.

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

#### 7: Lista el nombre y apellidos de los empleados en una única columna.

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

#### 8: Lista el nombre y apellidos de los empleados en una única columna, convirtiendo todos los caracteres en mayúscula

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

#### 9: Lista el nombre y apellidos de los empleados en una única columna, convirtiendo todos los caracteres en minúscula.

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

#### 10: Lista el identificador de los empleados junto al NIF, pero el NIF deberá aparecer en dos columnas, una mostrará únicamente los dígitos del NIF y la otra la letra.

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

#### 11: Lista el nombre de cada departamento y el valor del presupuesto actual del que dispone. Para calcular este dato tendrá que restar al valor del presupuesto inicial (columna presupuesto) los gastos que se han generado (columna gastos). Tenga en cuenta que en algunos casos pueden existir valores negativos. Utilice un alias apropiado para la nueva columna que está calculando.

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

