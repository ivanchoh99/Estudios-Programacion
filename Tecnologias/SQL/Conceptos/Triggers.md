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
