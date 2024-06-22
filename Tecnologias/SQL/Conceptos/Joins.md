[Referencia de "programación y mas"]([¿Cómo funciona INNER JOIN, LEFT JOIN, RIGHT JOIN y FULL JOIN? (programacionymas.com)](https://programacionymas.com/blog/como-funciona-inner-left-right-full-join))

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
