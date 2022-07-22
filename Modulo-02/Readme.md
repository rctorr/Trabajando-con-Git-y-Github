## Módulo 02: Trabajando con Git

### Contenido

1. Crear un repositorio en Git
2. Git Stages
3. Git Workflow
4. Comparar cambios de código con diferentes Git Stages
5. Comparar cambios de código con diferentes commits locales

### 1. Crear un repositorio en Git

Lo primero que vamos a crear es un repositorio (repo) que no es más que una carpeta con información adicional.

En general todos los comandos de git los ejecutamos dentro de ésta carpeta del repo.

Para ejecutar los comandos de git usando el comando `git`, ahora vamos a crear nuestro primer repositorio.

Primero creamos la carpeta `demorepo` en el Escritorio de tu computadora y luego abrimos git-bash usando el menú contextual usando la opción **Git Bash aquí** o también podemos abrir la aplicación **Git Bash** y luego navegar a la carpeta `demorepo` usando el comando `cd`.

Ahora inicializamos el repo con el comando `git init` y observa lo que pasa en la carpeta.

En **Git Bash** o **Linux** se puede usar el comando `ls -a` para ver los archivos ocultos.

También es bueno conocer el comando `cat` ya sea para examinar archivos o incluso para crearlos, aunque muchos serán creado usando un editor de código.

### 2. Git Stages

Vamos a revisar los estados de un conjunto de archivos

![git Stages](Media/git-stages.png)

Vamos a crear dos archivos llamandolos `archivo-1.txt` y `archivo-2.txt` y luego veamos que se encuentran en el directorio de trabajo, entonces los tenemos que pasar al área de índice y finalmente al repo local.

Para realizar lo anterior para el archivo `archivo-1.txt` ejecutamos los siguientes commandos:

```
$ git add archivo-1.txt  # Registramos los cambio en el área de stagin
$ git commit -m "Estamos agregando el primer archivo al repo"  # Registramos los cambio en la base de datos de git
$ git status  # Para ver el estado actual del repo
...
```

Entonces con `git add archivo archivo ...` nos permite registrar uno o más archivos en el área de stagin, `git commit -m "mensaje"` permite guardar los cambios en el área de stagin en el repo.


También se puede usar `git add .` o  `git add --all` para agregar todos los archivos que no están en el repo al área de stagin, pero no es muy recomandable ya que podríamos incluir archivos no deseados.

En este momento vamos a agregar todos los archivos faltantes que en éste caso sólo es `archivo-2.txt`

```
$ git add .  # o también: git add --all 
$ git commmit -m "Agregan todos los archivos faltantes"
$ git status
...
```

Git funciona en base a un concepto de ramas que es un carpeta que contiene una versión específica del proyecto, cuando se inicia un repo por default se crea la rama **master** y con ella vamos a trabajar un rato.

Vamos a crear dos archivos más: `archivo-3.txt` y `archivo-4.txt`

```
$ touch archivo-3.txt
$ touch archivo-4.txt
```

recuerda que el comando `touch` permite crear archivos vacios de texto.

Ahora vamos a agregar todos los archivos al área de stagin:

```
$ git add .
$ git status
...
```

Upsss, pero el sólo queríamos el `archivo-3.txt` en el stagin, y no el `archivo-4.txt` entonces vamos a remover éste último del área de stagin:

```
$ git rm --cached archivo-4.txt
$ git commit -m "Agregando el archivo-3.txt"
$ git log
...
```
Con `git rm --cached  archivo` eliminamos `archivo` del área de stagin, `git log` nos permite ver una lista de los comits realizados en el repo.

### 3. Git Workflow

¿Cuál es el flujo de trabajo recoemdado por git? Bueno, consiste en realizar un commit por cada tarea terminada, no importando si modificamos uno, dos o más archivos, pero correspondan a una sóla tarea, también en el área de descripción vamos a agregar un mensaje que describa las operaciones de la tarea y no simplemente "Se termino la tarea 1" ya que eso no nos indica que se realizó en ese commit.

**Tarea**: Vamos a crear el archivo `index.html` cuyo contenido se muestra a continuación y representa la estructura básica de la página de incio.

```
<!DOCTYPE html>
<html>
<body>
    <nav></nav>
    <section>
    </section>
    <footer>
    </footer>
</body>
</html>
```
Se puede usar el editor **vim** o cualquier otro de su preferencia, ahora si ejecutamos `git status` veremos que hay un archivo sin seguimiento (untracked) llamado `index.html` y ya hemos terminado nuestra tarea, entonces registramos los cambios en el repo

```
$ git add index.html
$ git commit -m "Creando la estructura básica para index.html"
$ git status
...
```

**Tarea**: Agrega un título al contenido de la página con el texto **Pagina de inicio**, el html deberá quedar como el siguiente:

```
<!DOCTYPE html>
<html>
<body>
    <nav></nav>
    <section>
       <h2>Página de inicio</h2>
    </section>
    <footer>
    </footer>
</body>
</html>
```
Listo, tarea terminada, entonces registramos los cambios en el repo:

```
$ git status
...
$ git add index.html
$ git commit -m "Agregando título a la página principal"
$ git status
...
$ git log
```

Éste flujo ha sido muy sencillo, pero ya veremos que podemos incluir más de un archivo por tarea realizada.

### 4. Comparar cambios de código con diferentes Git Stages

Ahora supongamos que el nombre del archivo `index.html` debe ser `index.php`, entonces vamos a realizar el cambio y registrarlo en el repo:

```
$ mv index.html index.php  # el comando mv mueve o renombra archivos
$ git status
...
$ git add index.php  # agregamos el archivo renombrado
$ git rm --cached index.html  # eliminamos el archivo del área de stagin 
$ git status
... en el área de stagin git detecta que estamos sólo renombrando el archivo
$ git commit -m "Renombrando archivo index.html a index.php"
$ git status
...
$ git log
```

Si queremos comparar las diferencias que hay entre el archivo `index.php` en nuestra carpeta de trabajo y el área de staging podemos hacer:

```
$ git diff index.php
$ 
```
Lo que dá una respuesta vacía porque lo que hay en stagin es exactamente igual a lo que tenemos en la carpeta de trabajo, así que vamos a hacer un cambo al archivo `index.php` agregando una línea:

```
<!DOCTYPE html>
<html>
<body>
    <nav></nav>
    <section>
       <h2>Página de inicio</h2>
       <hr />
    </section>
    <footer>
    </footer>
</body>
</html>
```
Agregamos sólo una línea y veamos ahora el status y las diferencias:

```
$ git status
En la rama master
Cambios no rastreados para el commit:
  (usa "git add <archivo>..." para actualizar lo que será confirmado)
  (usa "git restore <archivo>..." para descartar los cambios en el directorio de trabajo)
	modificado:     index.php

sin cambios agregados al commit (usa "git add" y/o "git commit -a")

$ git diff index.php
diff --git a/index.php b/index.php
index d79b5fd..0ecfb3c 100644
--- a/index.php
+++ b/index.php
@@ -4,6 +4,7 @@
     <nav></nav>
     <section>
        <h2>Página de inicio</h2>
+       <hr />
     </section>
     <footer>
     </footer>
```

Lo que nos dice que en el archivo `index.php` de nuestra carpeta de trabajo tiene una línea más **(+)** respecto a lo que hay en al área de stagin, ahora agregemos éste archivo al stagin:


```
$ git add index.php
$ 
```

Y hacemos un cambio más:

```
<!DOCTYPE html>
<html>
<body>
    <nav></nav>
    <section>
       <h2>Página de inicio</h2>
       <hr />
       <p>Párrafo principal de la página de inicio</p>
    </section>
    <footer>
    </footer>
</body>
</html>
```

Ahora podemos volver a comparar nuestro archivo `index.php` con el stating:

```
$ git diff index.php
diff --git a/index.php b/index.php
index 0ecfb3c..68b3f4c 100644
--- a/index.php
+++ b/index.php
@@ -5,6 +5,7 @@
     <section>
        <h2>Página de inicio</h2>
        <hr />
+       <p>Párrafo principal de la página de inicio</p>
     </section>
     <footer>
     </footer>
```

Vemos que justo nuestro archivo tiene una línea de más respecto al stagin, pero que pasa si queremos conparar con el último commit que está en el repo:

```
$ git diff HEAD index.php
diff --git a/index.php b/index.php
index d79b5fd..68b3f4c 100644
--- a/index.php
+++ b/index.php
@@ -4,6 +4,8 @@
     <nav></nav>
     <section>
        <h2>Página de inicio</h2>
+       <hr />
+       <p>Párrafo principal de la página de inicio</p>
     </section>
     <footer>
     </footer>
```
Lo que dice que el el archivo de la carpeta de trabajo tiene dos líneas más respecto a lo que tiene el el archivo del repo, genial!

Y si quicieramos comparar lo que hay entre el stagin y el repo, pues usando la opción `git diff --cached HEAD archivo`

```
$ git diff --cached HEAD index.php
diff --git a/index.php b/index.php
index d79b5fd..0ecfb3c 100644
--- a/index.php
+++ b/index.php
@@ -4,6 +4,7 @@
     <nav></nav>
     <section>
        <h2>Página de inicio</h2>
+       <hr />
     </section>
     <footer>
     </footer>
```

En donde vemos que el stagin sólo tiene un a línea de más que el mismo archivo en el repo, éste comando también se puede ejecutar con `git diff --staged HEAD archivo` o incluso omitir la palabra `HEAD` como: `git diff --staged archivo`.

finalmente para dejar nuestro repo limpio vamos a a agregar los últimos cambios al stagin y haremos un commit:

```
$ git add index.php
$ git commit -m "Agregando dos líneas más a la sección de contenido del index.php"
[master 41cf02f] Agregando dos líneas más a la sección de contenido del index.php
 1 file changed, 2 insertions(+)
$ git status
En la rama master
nada para hacer commit, el árbol de trabajo esta limpio
$ 
```

### 5. Comparar cambios de código con diferentes commits locales

Ahora vamos a comparar las diferencias que hay entre diferentes commits locales, primero vamos a obtener la lista con:

```
$ git log
commit 41cf02f647391600eb9c9f37e401cc61229df435 (HEAD -> master)
Author: rctorr <rictor@cuhrt.com>
Date:   Thu Jul 21 22:58:34 2022 -0500

    Agregando dos líneas más a la sección de contenido del index.php

commit bfab31e014fb8b073bbc9e2bcb6666fc3a644f90
Author: rctorr <rictor@cuhrt.com>
Date:   Thu Jul 21 22:01:55 2022 -0500

    Renombrando archivo index.html a index.php

commit ce964faee021b98fbce01d1e602dfa1ef236d04f
Author: rctorr <rictor@cuhrt.com>
Date:   Thu Jul 21 21:58:12 2022 -0500

    Agregando archivo index.html

commit 2858b323bd3dd3903c8dacbb2b3fb8ad5b41f299
Author: rctorr <rictor@cuhrt.com>
Date:   Thu Jul 21 20:35:58 2022 -0500

    Me quivoqué y e primer archivo es uno.txt y el segundo es dos.txt
$ 
```

Así que `git log` nos muestra la lista de todos los commits realizados en el repo de la rama master.

Ahora vamos a buscar la diferencias que hay en el archivo `index.php` entre el último commit (HEAD) y el commit anterior (bfab31):

```
$ git diff HEAD bfab31 index.php
diff --git a/index.php b/index.php
index 68b3f4c..d79b5fd 100644
--- a/index.php
+++ b/index.php
@@ -4,8 +4,6 @@
     <nav></nav>
     <section>
        <h2>Página de inicio</h2>
-       <hr />
-       <p>Párrafo principal de la página de inicio</p>
     </section>
     <footer>
     </footer>
```
Lo que indica que tomando como referencia el último commit (HEAD) el anterior commit tiene dos línea menos, aunque también lo podemos hacer al revés, podemos tomar como referencia el commit anterior y comparar con el HEAD:

```
$ git diff bfab31 HEAD index.php
diff --git a/index.php b/index.php
index d79b5fd..68b3f4c 100644
--- a/index.php
+++ b/index.php
@@ -4,6 +4,8 @@
     <nav></nav>
     <section>
        <h2>Página de inicio</h2>
+       <hr />
+       <p>Párrafo principal de la página de inicio</p>
     </section>
     <footer>
     </footer>
```
En este caso obtenemos algo similar a las comparaciones anteriores, donde se observa que se han agregado dos líneas más.

Vamos a agregar una línea más a nuestro archivo `index.php` y vamos a compararlo con el commit anterior bfab31:

```
<!DOCTYPE html>
<html>
<body>
    <nav></nav>
    <section>
       <h2>Página de inicio</h2>
       <hr />
       <p>Párrafo principal de la página de inicio</p>
    </section>
    <footer>
       <p>Derechos reservador @rctorr</p>
    </footer>
</body>
</html>
```

```
$ git diff bfab31 index.php
diff --git a/index.php b/index.php
index d79b5fd..227afe3 100644
--- a/index.php
+++ b/index.php
@@ -4,8 +4,11 @@
     <nav></nav>
     <section>
        <h2>Página de inicio</h2>
+       <hr />
+       <p>Párrafo principal de la página de inicio</p>
     </section>
     <footer>
+       <p>Derechos reservados @rctorr</p>
     </footer>
 </body>
 </html>
```
Como vemos nuestro archivo tiene 3 líneas de más repecto al mismo archivo en el commit de referencia.

Intenta comparar con otros commit o incluso con el primer commit ¿Cuál sería el resultado?


### E1. Como modificar el último commit si nos hemmos equivocado en el mensaje o en la lista de archivos.

Primero para cambiar el mensaje del último commit se realiza con el comando `git commit --ahamed -m "Nuevo mensaje"` veamos como funciona:

Primero vemos el último commit usando el siguiente comando:

```
$ git log -1
commit 41cf02f647391600eb9c9f37e401cc61229df435 (HEAD -> master)
Author: rctorr <rictor@cuhrt.com>
Date:   Thu Jul 21 22:58:34 2022 -0500

    Agregando dos líneas más a la sección de contenido del index.php
```
El `-1` indica cuantos commits queremos ver en la lista, ahora si modificamos el mensaje:

```
$ git commit --amend -m "Agregando las etiquetas <hr /> y <p> al contenido del indexp.php"
[master 7f1bb70] Agregando las etiquetas <hr /> y <p> al contenido del indexp.php
 Date: Thu Jul 21 22:58:34 2022 -0500
 1 file changed, 2 insertions(+)
 $ git log -1
commit 7f1bb70cbf08b5fb1ad4b9fd41f2bb5bcc1b3289 (HEAD -> master)
Author: rctorr <rictor@cuhrt.com>
Date:   Thu Jul 21 22:58:34 2022 -0500

    Agregando las etiquetas <hr /> y <p> al contenido del indexp.php
```
Y lo comprobamos con `git log`, ahora que pasa si olvidamos agregar más cambios al último commit, también lo podemos hacer, por lo pronto tenemos una línea en el footer de nuestro archivo `inbdex.php` que vamos a agregar al último commit:

```
$ git add index.php
$ git commit --amend -m "Agregando 3 líneas al archivos index.php"
$ git log
commit b32f272bcc76fda297517ca2107d8d57a2208027 (HEAD -> master)
Author: rctorr <rictor@cuhrt.com>
Date:   Thu Jul 21 22:58:34 2022 -0500

    Agregando 3 líneas al archivos index.php

commit bfab31e014fb8b073bbc9e2bcb6666fc3a644f90
Author: rctorr <rictor@cuhrt.com>
Date:   Thu Jul 21 22:01:55 2022 -0500

    Renombrando archivo index.html a index.php

commit ce964faee021b98fbce01d1e602dfa1ef236d04f
Author: rctorr <rictor@cuhrt.com>
Date:   Thu Jul 21 21:58:12 2022 -0500

    Agregando archivo index.html

commit 2858b323bd3dd3903c8dacbb2b3fb8ad5b41f299
Author: rctorr <rictor@cuhrt.com>
Date:   Thu Jul 21 20:35:58 2022 -0500

    Me quivoqué y e primer archivo es uno.txt y el segundo es dos.txt
```
Vemos como no hay nuevmos commits y el último commit es el que ha estado modificando.


