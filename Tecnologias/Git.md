# Herramientas graficas  
## Git GUi 
Nos sirve para ver el estado de nuestro repositorio local y en que stage se encuentran los cambios en los archivos, también nos permite generar los commit y realizar los respectivos push.
## gitk
Nos permite las ramificaciones de nuestros repositorios y el estado de nuestro repositorio local con respecto a el repositorio remoto, si esta actualizado o no.

# Revertir cambios

```Git
git checkout -- file.txt
git checkout .
```
Este comando nos permite revertir los cambios realizados a un archivo en especifico con -- y especificando el archivo, o sino se pueden revertir todos los cambios con .

```Git
git clean -xdf
```
Este comando nos permite borrar y descartar los archivos que no este versionados. por ejemplo si creamos un archivo.txt y este no se le había echo un commit o push y no se encuentra en el repositorio remoto con el este comando el archivo.txt se borrara.

	-x --> No uses las reglas estándar de ignorar, pero Siga utilizando las reglas de ignorar dadas con las opciones del comando línea. Esto permite eliminar todos los archivos, incluidos los productos de compilación. Esto se puede utilizar (posiblemente en junto con _git restore_ o _git reset_) para crear un working para probar una compilación limpia.

	-d --> Normalmente, cuando no se especifica ningún <pathspec>, git clean no lo hará recurre a directorios sin seguimiento para evitar eliminar demasiado. Especifique -d para que también se repita en dichos directorios. Si se especifica una <pathspec>, -d es irrelevante; todo sin seguimiento archivos que coincidan con las rutas especificadas (con excepciones para Los directorios git mencionados en ) se eliminarán.

	-f --> Si no se establece la variable de configuración de Git clean.requireForce a false, _git clean_ se negará a eliminar archivos o directorios a menos que se le dé -f o -i. Git se negará a modificar el no rastreado repositorios git anidados (directorios con un subdirectorio .git) a menos que se dé una segunda -f.

```Git
git reset -- file.txt
git reset .
```

Este comando nos permite revertir archivos que ya fueron añadidos a el stage change , en otras palabras nos permite revertir un git add

```Git
git reset HEAD~1
git reset --soft HEAD~1
```
Este código nos permite reversar la cantidad de commits que deseemos designándoselo después del ~

	--mixed -> (default) revierte el commit y deja todo lo que estaba en el commit antes de stage change
	--soft -> revierte el commit pero lo mantiene los cambios en el stage change
	--hard -> elimina todos los cambios echos (CUIDADO)

```Git
git commit --amend -m 'commit message'
```
Este comando nos permite agregar cambios que estén en stage change al commit anterior que este pendiente por hacer push  

```Git
git revert <sha1>
```
Este comando me permite revertir un cambio que ya allá sido enviado con push a la rama remota. Es necesario que para que surja efecto se debe ejecutar el comando git push.