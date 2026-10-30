# Practica guiada para GitBash

Primero nos situamos en la carpeta donde iniciaremos el repositorio. En la GitBash empezamos en la carpeta de directorio de nuestro home, que se representa con la virgulilla, siendo el siguiente path: ***cd/Users/ludwi*** (para asegurarte puedes escribir en la consola el comando ***pwd***.)

En caso de iniciar en **/** embezde **~**, quiere decir que estás en la carpeta del directorio raiz del entorno Unix de Git Bash, es el incio del sistema de archivos dentro de este. Si haces un ***cd ~*** y ya estarias dentro de tu "home" o directorio personal.

Una vez hecha está introducción para situarnos, empezamos. 

## Creacion y localización del directorio en el que vamos a trabajar
La carpeta donde voy a trabajar esta más adelante del inicio que indique,
 entonces metemos el siguiente comando en la consola de GitBash:
``` bash
$ cd Desktop
```

Dentro de esta carpeta creamos el directorio correspondiente, el cual será nuestro respositorio Git:
``` bash
$ mkdir prueba_git
```

Una vez creado, entramos dentro:

``` bash
$ cd prueba_git
```

## Creacion de archivos dentro de prueba_git
Una vez que hemos iniciado el respositorio, tenemos que crear dos archivos dentro de dicho directorio, uno que se llamará **texto.txt** y el otro que se llamará **script.sh**. Para hacer eso usaremos ***nano***.

En consola escribimos el siguiente comando:

``` bash
$ nano texto.txt
$ nano script.sh
```
Luego de escribir los comandos haces directamente **ctrl + x**, que guarda y sale.

## Modificacion de contenido en texto.txt
Ahora dentro del archivo texto.txt, tenemos que añadirle texto al archivo y para ellos usamos el comando **nano**.

Abrimos el archivo escribiendo en consola: 
``` bash
$ nano texto.txt
```
Una vez escrito eso, se nos abrirá el editor de texto y dentro escribiremos tal cual:

``` bash 
uno 
dos 
tres
```
Pulsas directamente *ctrl + x* te preguntará si quieres guardar antes de salir.

Escribimos en consola:
``` bash
$ nano script.sh
```
Escribes lo que quieres escribir tal cual:

``` bash 
echo "Listado completo"
ls -l
```

## Inicializacion del repositorio Git y visualizacion del estado

Añadimos este directorio a un nuevo repositorio local:

``` bash
$ git init
Initialized empty Git repository in C:/Users/ludwi/Desktop/prueba_git/.git/
```
Cuando se inicializa un repositorio con Git, se genera dentro del directorio una carpeta oculta llamada **.git**, la cual almacena toda la información sobre el historial de versiones.

Los archivos del proyecto aún no están siendo rastreados, por lo que aparecen como **untracked**.
Podemos ver este estado inicial ejecutando:

``` bash
$ git status
On branch main

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        script.sh
        texto.txt

nothing added to commit but untracked files present (use "git add" to track)
```
Este comando indica:
1. En qué rama estamos trabajando.
2. Qué archivos tienen cambios pendientes de guardar (commit).
3. Cuáles todavía no están añadidos al control de versiones (untracked).
4. Si todo está sincronizado, mostrando el mensaje working tree clean.

## Como cambiar el nombre de la rama en la que estamos
Ahora para realizar esto lo que tenemos que hacer es escribir en consola: 
``` bash 
$ git branch -m main

ludwi@Ludwig MINGW64 ~/prueba_git (main)
```
Ahora saldrá en vez de *master* nos saldrá *main*.

Y si quisieramos volver el nombre antiguo:
``` bash
$ git branch -m master

ludwi@Ludwig MINGW64 ~/prueba_git (master)
```

## Añadiendo archivos con add y commit
Para incluir archivos en el seguimiento del repositorio usamos add y luego commit:
``` bash 
$ git add script.sh
warning: in the working copy of 'script.sh', LF will be replaced by CRLF the next time Git touches it

$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   script.sh

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        texto.txt
```
Después de añadirlo, el archivo queda preparado para ser confirmado con un commit.
Para guardar esa versión:

``` bash
$ git commit -m "Confirmacion inicial"
[master (root-commit) fbe81e0] Confirmacion inicial
 1 file changed, 2 insertions(+)
 create mode 100644 script.sh

$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        texto.txt

nothing added to commit but untracked files present (use "git add" to track)

```
El mensaje entre comillas sirve para describir los cambios realizados.
Si no se indica ninguno, se abrirá el editor de texto predeterminado.
Podemos repetir el proceso con otros archivos:

``` bash
$ git add texto.txt
warning: in the working copy of 'texto.txt', LF will be replaced by CRLF the next time Git touches it


$ git commit -m "Añadiendo aarchivo de texto.txt"
[master ec10066] Añadiendo aarchivo de texto.txt
 1 file changed, 4 insertions(+)
 create mode 100644 texto.txt

$ git status
On branch master
nothing to commit, working tree clean

```

## Modificando archivos
Supongamos que editamos texto.txt con nano para agregar una nueva línea. Hacemos un **nano** en el archivo de *texto.txt*.

Le añadimos la siguiente linea:
``` bash
uno
dos 
tres
cuatro
```

Al hacerlo, Git detectará la modificación:

``` bash 
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   texto.txt

no changes added to commit (use "git add" and/or "git commit -a")

```
Para que los cambios se incluyan en la próxima versión, añadimos de nuevo el archivo: 

``` bash
$ git add texto.txt
warning: in the working copy of 'texto.txt', LF will be replaced by CRLF the next time Git touches it

$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   texto.txt

```
Si volvemos a modificarlo, Git mostrará que el archivo ha cambiado desde el último add.
Por tanto, hay que repetir el proceso antes del nuevo commit:

``` bash
$ nano texto.txt

uno
dos
tres
cuatro
cinco
```

Y luego una vez modificado hacemos:

``` bash
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   texto.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   texto.txt

```

Y podemos comprobar de que aparece que *"texto.txt"* está preparado para que se le haga un **commit** y que hay que también habría que añadirlo con **add** porque la última modificación no fue añadida para el rastreo del commit. 
Si ahora hacemos commit:

``` bash 
$ git commit -m "Modificaciones de texto.txt"
[master 1cd2b89] Modificaciones de texto.txt
 1 file changed, 1 insertion(+), 1 deletion(-)

```

Y luego hacemos un:

``` bash 
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   texto.txt

no changes added to commit (use "git add" and/or "git commit -a")

```

La última modificación que hemos hecho, no tiene add, con lo cual al realizar el commit, no se añadió al repositorio. Entonces para añadirlo hacemos:

``` bash 
$ git add texto.txt
warning: in the working copy of 'texto.txt', LF will be replaced by CRLF the next time Git touches it

$ git commit -m "Añadiendo la ultima modificacion"
[master 5c2f4c3] Añadiendo la ultima modificacion
 1 file changed, 1 insertion(+)

$ git status
On branch master
nothing to commit, working tree clean

```

Y ahora todo vuelve a estar limpio de nuevo. 

## Informacion
En cuando al commit y add, podemos resumirlos los dos en un solo paso. Volvemos a modificar el contenido de *texto.txt*:

``` bash 
$ nano texto.txt

uno
dos
tres
cuatro 
cinco
seis
```

Una vez hecho eso, hacemos el siguiente comando:

``` bash 
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   texto.txt

no changes added to commit (use "git add" and/or "git commit -a")

$ git commit -a -m "Nueva version"
warning: in the working copy of 'texto.txt', LF will be replaced by CRLF the next time Git touches it
[master 886e1ac] Nueva version
 1 file changed, 1 insertion(+)

$ git status
On branch master
nothing to commit, working tree clean

```

Y como podemos comprobar se han hecho un add y un commit en la misma linea. 

Información sobre la última versión confirmada, hacemos **$ git show**:

``` bash 
$ git show
commit 886e1ac76ba8117fa1623322819e10a7e62b20d3 (HEAD -> master)
Author: Ludwig <ludwigmg5@gmail.com>
Date:   Thu Oct 29 13:54:01 2026 +0100

    Nueva version

diff --git a/texto.txt b/texto.txt
index 23c83ff..5c40aa2 100644
--- a/texto.txt
+++ b/texto.txt
@@ -3,3 +3,5 @@ dos
 tres
 cuatro
 cinco
+seis
+


```

Cambios que se han realizados, ejecutamos el comando **$git log**

``` bash 
$ git log
```

Si queremos ver el hash asociado, hacemos:

``` bash 
$ git cat-file 1cd2 -p
```
Nos enseña la informacion sobre el directorio tree y el commit previo junto el resto de sus datos

## Diferencias
Cogemos el archivo *"texto.txt"* y le añadimos la linea "siete" y podemos borrar la "tres". Para ver las diferencias en el archivo modificado y el confirmado en la última versión, usamos el comando **$ git diff**:

``` bash 
$ git diff
```

Se indica que lineas borradas y los añadidos en comparacion al previo.

Ejecutamos:

``` bash 
$ git commit -a -m "Probando diff"
```
Tambien nos muestra información sobre lo añadido y eliminado. 

Ahora añadimos una nueva linea "ocho":
``` bash 
$ nano texto.txt
```

Y ejecutamos de nuevo:

``` bash 
$ git diff
```

## Ignorar archivos
Usamos el archivo **.gitignore**, para ello primero hay que hacer los siguientes pasos:

1. Creamos el archivo, para crearlo desde consola usamos el siguiente comando:
``` bash 
$ touch .gitignore
```
Ahora una vez que se creó, lo que hacemos es escribir dentro del archivo creado las siguientes lineas usando el nano: 
*el # se usa como comentarios*
``` bash 
$ nano .gitignore
```
Dentro del archivo escribimos lo siguiente:
``` bash
#para ignorar los archivos acabados en .class
*.class

#para ignorar los archivos terminados en ~
*~

#para que no ignore un archivo concreto aunque termine en cosas genericas que s>
!importante~
```

Ahora para ver que esto funciona, creamos el archivo **Hola.java**:

``` bash 
$ nano Hola.java
```
Y dentro del archivo escribimos lo siguiente:
``` java
class Hola {
 public static void main(String[] args){
 System.out.println("Welcome to the Java World");    
    }
}
```
Temporal e importante:
``` bash 
$ touch temporal~
```
``` bash 
$ touch importante~
```
Los dejamos vacios. 

Ejecutamos: 
``` bash 
$ ls -a
```
Listado con todos los archivos nombrados hasta el momento. 

Compilamps el Hola.java:
``` bash 
$ javac Hola.java
```
Una vez que se haya compilado, ya tenemos el .class y haciendo el comando de **$ git status**. 

``` bash 
$ git status
```

En el directorio hay archivos que no están añadidos (con add): .gitignore, Hola.java e impoortante~.

Hacemos lo siguiente en consola:
``` bash 
$ git add .
$ git commit -m "Añadidos fuentes en java y archivos importantes"
``` 
En caso de que hubiera subidrectorios, también los incluye. 

``` bash 
$ git status
```
Y vemos que el arbol esta limpio.

Para ver los archivos que hay en el directorio tras el último commit en la rama *HEAD(principal)*:
``` bash 
$ git ls-tree --name-only -r HEAD
```
Y nos salen todos los archivos de nuestro directorio.

## Tags y gestión de versiones
Primero ejecutamos el log:
``` bash 
$ git log
```
Sale todo el historial de versiones.

``` bash 
$ git show 491c
```
Mas comodo usar tags en vez de las etiquetas. Entonces, para hacer esto es muy sencillo, vamos a crear una global. 

``` bash 
$ git tag v0.7
```

Diferencia:
``` bash 
$ git log --oneline
```
Vemos que en ese sale lo del tag:v0.7

Tag a uno en concreto:
``` bash 
$ git tag v0.3 491c
```
Si usasemos el **$git log** veremos la informacion mas extendida, igual interesa para verlo mejor. 

``` bash 
$ git show v0.3
```
Para ver concretamente al que le hemos añadido un tag.

Para ver versiones antiguas del proyecto:
``` bash 
$ git checkout v0.3
```
Puedes poner el nombre de la tag o el codigo hash
Para volver a versiones recientes haces:
``` bash 
$ git checkout master
```
*en caso de que hayas usado otro nombre en la rama principal, deberas de poner ese nombre en concreto*

Si vas a una version antigua y deseas modoficarla, primero debes de hacer la nueva rama, debido al riesgo que existe de perder mesas modificaciones al volver a la version mas actual. 
*los tags se almacenan en .git/refs/tags*

## Ramas
Las ramas con archivos paralelos a los principales con el objetivo de hacer pruebas. Estas ramas se pueden abandonar, eliminar o mezclar con la principal. 

En la Git Bash aparece junto al prompt en que rama estamos trabajando. 
Vamos a crear uno rama nueva:
``` bash 
$ git branch Prueba
$ git log --oneline
```
Entonces, para crear ramas usamos el comando **$ git branch nomRama**.

Para ver el listado de ramas que tenemos:
``` bash 
$ git branch
```
Te sale el listado de las ramas que tienes y la que tiene el asterisco es la rama en la que estas trabajando (coincide con el prompt).
*las ramas se almacenan en: .git/refs/heads*

Para movernos entre ramas, en este caso, para ir a la rama de prueba hacemos:
``` bash 
$ git switch Prueba
```
*si ejecutamos **$ git checkout Prueba** haria exactamente lo mismo, nos moveria hacia alli*

Ahora ya nos hemos movido a la rama que hemos creado antes y podemos empezar a trabajar.

Ahora, si hacemos de nuevo:
``` bash 
$ git branch
```
Vamos a ver que la posicion del asterisco ha cambiado y que ahora está en Prueba, porque es la rama en donde estamos situados actualmente. 

Si probamos a hacer un **$ git log --oneline**, entonces podremos observar de que ahora en HEAD (puntero de trabajo) se apunta hacia Prueba.

Ahora todos los commits que haga, se harán en dicha rama, dejando intacta la principal. 

A continuación relizamos el seguiente bloque de codigo:
``` bash 
$ git commit -a -m "Rama para pruebas de codigo"
$ git log --online
```

Vamos a probar a cammbiar el **Hola.java**, lo hacemos con el nano:
``` bash 
$ nano Hola.java
```
Y le añadimos la siguiente linea de codigo:
``` java
System.out.println("I have no more branches to commit, said the Ent");
```
Y ahora como ha sido modificado le hacemos el commit que le corresponde:
``` bash 
$ git commit -m "Llegan los Ents a Java"
4 git tag v0.7-Ent-Release
```
Y si ahora hacemos:
``` bash 
$ git log --oneline
```
Volvemos a la rama principal:
``` bash 
$ git switch master
```
Y una vez en esa rama hacemos:
``` bash 
$ cat Hola.java
```

Y aqui podemos observar de que no ha habido modificaciones en el archivo porque no fueron en la rama acutual donde estamos. 

Ahora, para mezclar los cambios de ambas ramas realizamos lo siguiente:
``` bash 
$ git merge Prueba
```
Y vemos que ha sido posible y todo acabó combinandose bien. 
*no siempre es asi a veces ocurren conflictos y hay que resolverlos*

## Eliminar y quitar de seguimiento
Para eliminar archivos:
``` bash 
$ git rm importante~
```
Y para confirmar los cambios hacemos un **commit**

Si se eliminó de antes con un **rm** normal, hay que ejecutar también **git rm** o **git rm -f** en caso de que el archivo este confirmado. 

En caso de que hubiera archivos ya en seguimiento y que deseas quitar(.class por ejemplo), hacemos el siguiente comando:
``` bash 
$ git reset HEAD *.class
```

## Repositorios remotos: GitHub
GitHub es un proveedor para repositorios Git para que los usuarios puedan compartir sus proyectos.

### Clonar un proyecto
No hace falta tener una cuenta, simplemente vas a tu directorio de usuario y ejecutas:
``` bash 
$ git clone https://github.com/ColegioVivasCurro/HolaED
```

Ahora vamos a crear un repositorio y subir nuestro proyecto, finalmente.
*para este paso si necesitas cuenta*

Vamos a nuestra cuenta de GitHub y creamos el repositorio correspondiente al proyecto. Luego ahi sincronizaremos los archivos en ese mismo. 
Usamos el comando:
``` bash 
$ git push -u origin master
```
El **-u** sirve para recordar los nombres, asi luego solo tienes que hacer **$ git push**. 

Tambien podriamos usar, para mandar los repositorios locales a GitHub:
``` bash 
$ git remote add origin https://github.com/ludwigSMOG/practica_guiada_git
```
