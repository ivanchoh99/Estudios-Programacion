![COMANDOS SQL](https://sqlserverdb.com/wp-content/uploads/2022/01/comandos-sql-server1.png)

- [[Joins]]
- [[Procedimientos almacenados]]
- [[Triggers]]
- [[TCL]]
- [[DCL]]
- [[DML]]
- [[DDL]]
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