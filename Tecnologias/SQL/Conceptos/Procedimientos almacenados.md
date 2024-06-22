Los procedimientos almacenados se utilizan por cuestiones de eficiencia y seguridad. Lo cual consiste en almacenar un procedimiento ya sea porque es muy repetitivo por varios usuarios y/o aplicaciones o por cuidar la información de la tabla. Y con ello solo es necesario realizar el llamado a el procedimiento.

```SQL
CREATE PROCEDURE  nombre_procedimiento(parametro1 TIPO_DATO,parametro2 TIPO_DATO)
SELECT * FROM  tabla WHERE columna = condicion;

CALL nombre_procedimiento(parametro1 ,parametro2);

CREATE PROCEDURE  actualizar_columna(n_columna TIPO_DATO,indexPrimaryKey TIPO_DATO)
UPDATE tabla SET columna = n_columna WHERE columna = indexPrimaryKey;

CALL actualizar_columna(42, 'AR78')
```
