![COMANDOS SQL](https://sqlserverdb.com/wp-content/uploads/2022/01/comandos-sql-server1.png)

# DDL (LENGUAJE DE DEFINICIÓN DE DATOS)

- **[CREAR](https://sqlserverdb.com/crear-base-de-datos-sql/) :** crea una base de datos o sus objetos como tabla, vista, SP, etc.   
- **[ALTER](https://sqlserverdb.com/alter-table-sql/) :** Modifica la estructura de la base de datos o sus objetos.   
- **[DROP](https://sqlserverdb.com/drop-table-sql-para-eliminar-tabla/)**: elimina la estructura de la base de datos o sus objetos.   
- [**TRUNCATE**:](https://sqlserverdb.com/truncate-table-sql/) elimina los datos de la tabla, así como el espacio asignado para los registros. La estructura de la mesa sigue siendo la misma.   
- **[RENAME](https://sqlserverdb.com/sql-rename/):** cambia el nombre de un objeto.
# DML (LENGUAJE DE MANIPULACIÓN DE DATOS)

- [**SELECT**](https://sqlserverdb.com/sql-select-consulta-registros/)**:** recupera datos de una tabla.  
- [**INSERT:**](https://sqlserverdb.com/sql-insert-into/) inserta datos en una tabla.  
- [**UPDATE:**](https://sqlserverdb.com/sql-update/) actualiza los datos existentes en una tabla.  
- [**DELETE:**](https://sqlserverdb.com/sql-delete-para-eliminar-registros/) elimina datos de la tabla.  
- **MERGE:** realiza la operación de inserción o actualización.
# DCL (LENGUAJE DE CONTROL DE DATOS)

- [**GRANT:**](https://sqlserverdb.com/sql-grant/) proporciona acceso de usuario a la base de datos o sus objetos.  
- [**REVOKE:**](https://sqlserverdb.com/sql-revoke/) restringe el acceso del usuario a la base de datos o sus objetos.
# TCL (LENGUAJE DE CONTROL DE TRANSACCIONES)

- [**COMMIT:**](https://sqlserverdb.com/sql-commit/) se usa para almacenar los cambios realizados mediante una transacción.  
- **ROLLBACK:** se utiliza para revertir los cambios hasta el último estado comprometido en caso de cualquier error.  
- **SAVEPOINT:** se utiliza para revertir la transacción hasta cierto punto.

# ÍNDICES

Permiten realizar búsquedas con mayor rapidez en una base de datos. Pero no forman parte del estándar SQL. 

## Índices de claves primarias:

- Cada valor es único
- No null

```SQL
ALTER TABLE tabla ADD PRIMARY KEY (columna,...)
```
## Índices ordinarios:

- permite duplicados
- Sí null

```SQL
CREATE INDEX nombre_del_indice ON tabla (columna)
```
## Índices únicos:

- No permite duplicados
- Sí null

```SQL
CREATE UNIQUE INDEX nombre_del_indice ON tabla (columna)
```
## Índices compuestos:

- Múltiples columnas
- Si null

```SQL
CREATE UNIQUE INDEX nombre_del_indice ON tabla (columna,...)
```
# JOINS [Referencia de "programación y mas"]([¿Cómo funciona INNER JOIN, LEFT JOIN, RIGHT JOIN y FULL JOIN? (programacionymas.com)](https://programacionymas.com/blog/como-funciona-inner-left-right-full-join))

Los joins son sentencias que nos permiten obtener datos de distintas tablas, las cuales están relacionadas por una columna en común, para abordar este tema se utilizan estas 2 tablas de ejemplo.

| Nombre     | DepartamentoId |
| ---------- | -------------- |
| Rafferty   | 31             |
| Jones      | 33             |
| Heisenberg | 33             |
| Robinson   | 34             |
| Smith      | 34             |
| Williams   | NULL           |

| Id  | Nombre      |
| --- | ----------- |
| 31  | Sales       |
| 33  | Engineering |
| 34  | Clerical    |
| 35  | Marketing   |
## INNER JOIN

![INNER JOIN](https://res.cloudinary.com/pym/image/upload/c_scale,f_auto,q_auto,w_258/articles/2019/sql/INNER_JOIN)

Con esta sentencia traemos los datos de las tablas donde allá relación de información de ambas tablas, esto quiere decir que obtenemos la intersección de las diferentes tablas.

```sql
SELECT * 
FROM Empleados E
JOIN Departamentos D
ON E.DepartamentoId = D.Id
```

| Nombre     | DepartmentoId | Id  | Nombre      |
| ---------- | ------------- | --- | ----------- |
| Rafferty   | 31            | 31  | Sales       |
| Jones      | 33            | 33  | Engineering |
| Heisenberg | 33            | 33  | Engineering |
| Robinson   | 34            | 34  | Clerical    |
| Smith      | 34            | 34  | Clerical    |
- El empleado "Williams" no aparece en los resultados, ya que no pertenece a ningún departamento existente.
- El departamento "Marketing" tampoco aparece, ya que ningún empleado pertenece a dicho departamento.

## LEFT JOIN 

![LEFT JOIN](https://res.cloudinary.com/pym/image/upload/c_scale,f_auto,q_auto,w_258/articles/2019/sql/LEFT_JOIN)

Con esta sentencia obtenemos los resultados de la intersección de datos pero además obtenemos todos los otros datos de la primera tabla que no tengan relación con las otras. En pocas palabras obtenemos tabla1 + intersección.

```sql
SELECT
  E.Nombre as 'Empleado',
  D.Nombre as 'Departamento'
FROM Empleados E
LEFT JOIN Departamentos D
ON E.DepartamentoId = D.Id
```

| Empleado   | Departamento |
| ---------- | ------------ |
| Rafferty   | Sales        |
| Jones      | Engineering  |
| Heisenberg | Engineering  |
| Robinson   | Clerical     |
| Smith      | Clerical     |
| Williams   | NULL         |
Aca como podemos ver trae los datos en común relacionados en las 2 tablas pero además de eso trae al empleado que no esta relacionado con la tabla departamento.

## RIGHT JOIN

![RIGHT JOIN](https://res.cloudinary.com/pym/image/upload/c_scale,f_auto,q_auto,w_258/articles/2019/sql/RIGHT_JOIN)

Con esta sentencia ocurre algo similar a la sentencia anterior pero en el sentido opuesto. En pocas palabras obtenemos la intersección + tabla2

```sql
SELECT
  E.Nombre as 'Empleado',
  D.Nombre as 'Departamento'
FROM Empleados E
RIGHT JOIN Departamentos D
ON E.DepartamentoId = D.Id
```

|Empleado|Departamento|
|---|---|
|Rafferty|Sales|
|Jones|Engineering|
|Heisenberg|Engineering|
|Robinson|Clerical|
|Smith|Clerical|
|NULL|Marketing|
Como podemos ver aca obtenemos los datos de la intersección entre las 2 tablas pero además obtenemos los datos de la tabla 2 que no tienen relación con la tabla 1. Vemos que hay 1 departamento que no tiene empleados

## FULL JOIN

![FULL JOIN](https://res.cloudinary.com/pym/image/upload/c_scale,f_auto,q_auto,w_258/articles/2019/sql/FULL_JOIN)

Con esta sentencia obtenemos las 2 tablas completas con la relación de la intersección; incluyendo los campos que no están relacionados. 

```sql
SELECT
  E.Nombre as 'Empleado',
  D.Nombre as 'Departamento'
FROM Empleados E
FULL JOIN Departamentos D
ON E.DepartamentoId = D.Id
```

| Empleado   | Departamento |
| ---------- | ------------ |
| Rafferty   | Sales        |
| Jones      | Engineering  |
| Heisenberg | Engineering  |
| Robinson   | Clerical     |
| Smith      | Clerical     |
| Williams   | NULL         |
| NULL       | Marketing    |
## EXCLUID JOIN

Estas sentencias no permiten obtener exclusivamente los datos de las tablas que no están relacionados. Estos los obtenemos manipulando las sentencias anteriores con la cláusula WHERE.

![EXCLUID LEFT JOIN](https://res.cloudinary.com/pym/image/upload/c_scale,f_auto,q_auto,w_258/articles/2019/sql/LEFT_EXCLUDING_JOIN)

![EXCLUID RIGHT JOIN](https://res.cloudinary.com/pym/image/upload/c_scale,f_auto,q_auto,w_258/articles/2019/sql/RIGHT_EXCLUDING_JOIN)

- `Left Excluding JOIN` nos permitirá obtener la lista de empleados que aún no han sido asignados a ningún departamento de trabajo.
- Mientras que `Right Excluding JOIN` nos mostrará la lista de departamentos que no tienen a ningún trabajador asociado.

# Referencias Cruzadas 

Es la forma en que relacionamos la información y la mostramos mediante una tabla de datos donde tenemos la fila de referencia con PIVOT una columna de referencia con GROUP BY  y el campo de totales con TRANSFORM. 

```SQL

TRANSFORM SUM(CAMPO1) AS TOTAL
SELECT CAMPO2, CAMPO3 WHERE CONDICION
GROUP BY CAMPO2
PIVOT CAMPO4
```

Crea una consulta de tabla de referencias cruzadas que muestra las ventas de productos por mes para un año específico. Los meses aparecen de izquierda a derecha como columnas y los nombres de los productos aparecen de arriba hacia abajo como filas.
```SQL
TRANSFORM  
   Sum(Cantidad) AS Ventas  
SELECT  
    Compania  
FROM  
    Pedidos  
WHERE  
    Fecha Between #01-01-1998# And #12-31-1998#  
GROUP BY  
    Compania  
ORDER BY  
   Compania  
PIVOT  
    "Trimestre " &  
    DatePart("q", Fecha)  
    In ('Trimestre1', 'Trimestre2', 'Trimestre 3', 'Trimestre 4')  
```
Crea una consulta de tabla de referencias cruzadas que muestra las ventas de productos por trimestre de cada proveedor en el año indicado. Los trimestres aparecen de izquierda a derecha como columnas y los nombres de los proveedores aparecen de arriba hacia abajo como filas.
![|700](https://desarrolloweb.com/articulos/images/ejemplo_practico.jpg)



# TRIGGERS (DISPARADORES)

Los triggers nos permite que a la hora de realizar una acción el base de datos se desencadene un evento o una acción. Un trigger es un objeto que esta asociado a una tabla y  cuando ocurra algo en esa tabla el trigger saltara (INSERT, UPDATE, DELETE).

## INSERT 
 ```SQL
 %% Trigger para realizar un accion despues de un insert por aca fila%%
 CREATE TRIGGER tabla_AI AFTER INSERT ON tabla FOR EACH ROW INSERT INTO tabla_del_trigger(columnas,...) VALUES (NEW.columnas,...)
 %% Trigger para realizar un accion despues de un insert por aca sentencia%%
 CREATE TRIGGER tabla_AI AFTER INSERT ON tabla FOR EACH STATMENT INSERT INTO tabla_del_trigger(columnas,...) VALUES (NEW.columnas,...)
```

## UPDATE
```SQL
CREATE TRIGGER actualizacion_tabla_BU BEFOR UPDATE ON tabla FOR EACH ROW INSERT INTO  tabla_del_trigger(columnas,...) VALUES (OLD.columnas,...,NEW.columnas,...) 
```

DELETE
```SQL
CREATE TRIGGER eliminacion_tabla_AU AFTER DELETE ON tabla FOR EACH ROW INSERT INTO  tabla_del_trigger(columnas,...) VALUES (OLD.columnas) 
```

# PROCEDIMIENTOS ALMACENADOS

Los procedimientos almacenados se utilizan por cuestiones de eficiencia y seguridad. Lo cual consiste en almacenar un procedimiento ya sea porque es muy repetitivo por varios usuarios y/o aplicaciones o por cuidar la información de la tabla. Y con ello solo es necesario realizar el llamado a el procedimiento.

```SQL
CREATE PROCEDURE  nombre_procedimiento(parametro1 TIPO_DATO,parametro2 TIPO_DATO)
SELECT * FROM  tabla WHERE columna = condicion;

CALL nombre_procedimiento(parametro1 ,parametro2);

CREATE PROCEDURE  actualizar_columna(n_columna TIPO_DATO,indexPrimaryKey TIPO_DATO)
UPDATE tabla SET columna = n_columna WHERE columna = indexPrimaryKey;

CALL actualizar_columna(42, 'AR78')
```

# Procedimientos almacenados + TRIGGERS

- Bloques de ejecución BEGIN (Inicio del bloque) -> END (final del bloque)  
- Declaración de variables DECLARE
- Declarar un delimitador DELIMITER
```SQL
%% Se establece un delimitador para decir donde acaba el procedimiento almacenado, aparte del ; %%
DELIMITER $$ 

CREATE PROCEDURE procedimiento_almacenado(parametro TIPO_VALOR)
BEGIN
	DECLARE variable1 TIPO_DATO DEFAULT valor;
	DECLARE variable2 TIPO_DATO;
	SET variable2 =  variable1 - parametro;

	SELECT variable2;
END;$$

%% Se restablece el limitador por defecto %%
DELIMITER ;
```

Ejemplo con un caso de una tabla de productos: [SQL pildorasinformaticas](https://youtu.be/sNHZhXeVA4c?si=UzvgKyfNGDUMiMyu&t=750)

```SQL 
DELIMITER $$

CREATE TRIGGER revisar_precio_BU BEFORE UPDATE ON productos FOR EACH ROW

BEGIN
	IF(NEW.precio < 0) THEN
		SET NEW.precio = OLD.precio;
	ELSEIF(NEW.precio > 1000) THEN
		SET NEW.precio = OLD.precio;
	END IF;

END;$$

DELIMITER ;
```

# VISTAS

Las vistas son empleadas para la privacidad de la información, para manejar perfiles de usuarios y asi mismo darles diferentes accesos a la base de datos y que estos no puedan ver o si cierta información según los permisos concedidos.También se utilizan para la optimización de consultas cuando constantemente se realizan querys de consultas similares, para ello se genera una vista de esta consulta de tal forma que solo se consulte la vista y no se realicen constantemente llamados de consultas complejas en las tablas de la base de datos. Por ultimo se puede usar para entornos de prueba sin poner en riesgo la integridad de la base de datos.

```SQL
CREATE VIEW nombre_vista AS 
SELECT columna2,columna3,columna5 FROM tabla WHERE columna6 = valor; 
```