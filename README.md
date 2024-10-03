## Práctica 1: Git y GitHub
![Git](https://img.shields.io/badge/git-%23F05033.svg?style=for-the-badge&logo=git&logoColor=white)
![GitHub](https://img.shields.io/badge/github-%23121011.svg?style=for-the-badge&logo=github&logoColor=white)

En esta práctica vamos a utilizar diversos comandos y funciones de Git y GitHub. Para ello, trabajaremos con el uso de ramas en este mismo repositorio.

### Repositorio HLC

1. El primer paso es crear un repositorio llamado `HLC_SMR_P1`. A partir de ahora trabajaremos en este repositorio.

2. Tras ello, crearemos una rama llamada `<nombre_apellidos_v1>` en la que vamos a trabajar.

~~~
git checkout -b <nombre_apellidos_v1>
~~~

## Commit inicial

1. Crearemos un fichero llamado `command_history.txt`, y añadiremos la secuencia de comandos utilizados hasta ahora.
2. Realizaremos un commit con estos cambios con el mensaje `Add used commands`.
3. Para terminar subiremos los cambios al repositorio remoto.

~~~
git add .
git commit -m "Add used commands"
git push
~~~

4. Si la rama está creada en local pero no en remoto, Git nos indicará que es necesario subirla al repositorio remoto. 

~~~
git push --set-upstream origin <nombre_apellidos_v1>
~~~

## Provocando un conflicto

1. Desde la web de GitHub, vamos a cambiar la primera línea del fichero `command_history.txt` por cualquier texto y después lo subiremos con el mensaje `Update history from website`.
2. Volvemos al repositorio local y **sin actualizar** la rama vamos a cambiar de nuevo la primera línea del fichero `command_history.txt`. Esta vez el texto debe ser diferente al del paso 1, y el mensaje del commit será `Update history from command line`.
3. Desde consola, commitearemos los cambios y los subiremos.


~~~
git add .
git commit -m "Update history from command line"
git push
~~~

4. Git mostrará un mensaje indicando que la rama no está actualizada, por lo cual realizaremos la actualización de la rama.

~~~
git pull origin <nombre_apellidos_v1>
~~~

5. Tras actualizar la rama intentaremos subir los cambios de nuevo. 

~~~
git push
~~~

6. Git nos informará de que hay un conflicto en el fichero y nos pedirá resolverlo. Tras hacerlo, volveremos a crear un commit con el conflicto resuelto y lo subiremos.

~~~
git add .
git commit -m "Solve conflicts"
git push
~~~

## Merge entre ramas

1. Creamos otra rama desde `main` llamada `<nombre_apellidos_v2>`

~~~
git checkout -b <nombre_apellidos_v2>
~~~

2. Añadimos un fichero `command_history_2.txt` y lo subimos a la rama con el mensaje `Add newer commands.`

~~~
git add .
git commit -m "Add newer commands"
git push 
~~~

3. Hacemos un merge de la rama `<nombre_apellidos_v1>` en la rama `<nombre_apellidos_v2>`.

~~~
git merge `<nombre_apellidos_v1>` -m "Merge v1"
~~~

4. Hacemos push de los cambios. Observamos que no es necesario crear un nuevo commit con los cambios del merge porque Git ya lo hace automáticamente.

~~~
git push
~~~

5. Vamos a visualizar el historial de commits, y comprobamos que los commits que introducimos en la rama v1 se encuentran tal cual en la rama v2 mediante `git log`. Este comando muestra el historial de commits en orden cronológico inverso (del más reciente al más antiguo). Para salir del visualizador, basta con pulsar la tecla `q`.

~~~
git log
~~~

6. El comando `git log` cuenta con varias opciones:

~~~
git log -n <número>                                   # Limita la cantidad de commits mostrados
git log --author=<nombre-autor>                       # Filtra los commits por autor
git log --oneline                                     # Muestra cada commit en una línea única
git log --since=<fecha-inicial> --until=<fecha-final> # Filtra por rango de fechas
git log --graph                                       # Muestra un gráfico de ramas y merges
git log --grep="<texto-a-buscar>"                     # Busca commits por mensaje
git log -- <nombre-archivo>                           # Filtra commits por archivo
~~~

## Listado y borrado de ramas

1. En primer lugar vamos a listar las ramas del repositorio.

~~~
git branch
~~~

2. A continuación, vamos a eliminar las rama v2. Para ello tenemos que estar en otra rama que no sea ninguna de ellas, como v1.

~~~
git checkout v1
git branch -d <nombre_apellidos_v2>
git push origin --delete <nombre_apellidos_v2>
~~~
