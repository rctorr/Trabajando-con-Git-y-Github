## Módulo 05: Commits (confirmaciones)

### Contenido

1. Trabajar con commits en Git
2. Conozca la información sobre un commit específica en Git – Git Show
3. Trabajar con commits en GitHub
4. Commit de cambios directamente en GitHub

### 1. Trabajar con commits en Git

![Trabajar con commits](Media/trabajando-con-commits.png)

Ya hemos trabajado con las comparaciones de repos, por ejemplo busquemos un commit en donde no exista el archivo `public_html/static/css/main.css`:

```
$ git log
...

$ git diff d7abb2a3b023
diff --git a/public_html/static/css/main.css b/public_html/static/css/main.css
new file mode 100644
index 0000000..f9265a2
--- /dev/null
+++ b/public_html/static/css/main.css
@@ -0,0 +1,6 @@
+nav {
+    margin: 0px;
+    padding: 10px;
+    background-color: rgb(200, 200, 200);
+}
+
```
Vemos como git utiliza el repo que indicamos como referencia y sobre ese compara lo que tenemos en el último commit, podemos ver que la totalidad del archivo se ha agregado, pero para simplificar también podemos indicar el commit contando cuántos commits hacia atrás está, por ejemplo el commit elegido está 2 commit hacia atrás, así que una operación similar sería:

```
$ git diff HEAD~1
diff --git a/public_html/static/css/main.css b/public_html/static/css/main.css
new file mode 100644
index 0000000..f9265a2
--- /dev/null
+++ b/public_html/static/css/main.css
@@ -0,0 +1,6 @@
+nav {
+    margin: 0px;
+    padding: 10px;
+    background-color: rgb(200, 200, 200);
+}
+
```
Y si queremos buscar los commits en donde se agregaron las etiquetas `<head>` al archivo `index.html`:

```
$ git diff HEAD~2 HEAD~1
diff --git a/public_html/index.html b/public_html/index.html
index 2831477..d025a8a 100644
--- a/public_html/index.html
+++ b/public_html/index.html
@@ -1,5 +1,8 @@
 <!DOCTYPE html>
 <html>
+<head>
+    <link rel="stylesheet" href="static/css/main.css">
+</head>
 <body>
     <nav><a href="index.html">Inicio</a> | <a href="perfiles.html">Perfiles</a></nav>
     <section>
$ 
```
Entonces podemos hacer referencia a los commits por id o por posición a partir de donde apunta la etiqueta HEAD.

### 2. Conozca la información sobre un commit específica en Git – Git Show

Si lo que necesitamos es ver la información de un sólo commit entonces podemos hacer uso del comando `git show commit`.

En donde `commit` puede ser el id, una etiqueta o un índice en base a HEAD.

Veamos ejemplos de los 3 casos:

```
$ git show 
commit 7e40896e5badfdc7ffd9d69f90e2cf54e356c857 (HEAD -> master, github/master)
Author: rctorr <rictor@cuhrt.com>
Date:   Wed Aug 3 04:49:36 2022 -0500

    Agregando archivo main.css

diff --git a/public_html/static/css/main.css b/public_html/static/css/main.css
new file mode 100644
index 0000000..f9265a2
--- /dev/null
+++ b/public_html/static/css/main.css
@@ -0,0 +1,6 @@
+nav {
+    margin: 0px;
+    padding: 10px;
+    background-color: rgb(200, 200, 200);
+}
+
```
Vemos la información del último commit, ahora veamos la información del primer commit:

```
$ commit 6b615d88095779067ae74fff438147a1d1c6cc15
Author: rctorr <rictor@cuhrt.com>
Date:   Wed Aug 3 04:23:42 2022 -0500

    Inicializando repo

diff --git a/Readme.md b/Readme.md
new file mode 100644
index 0000000..c872412
--- /dev/null
+++ b/Readme.md
@@ -0,0 +1,13 @@
+# Proyecto demorepo
+
+## Descripción
+
+Éste proyecto permite crear varios ensayos sobre el uso de Git y Github por lo 
que podría no ser tan coherente como uno esperaría.
+
+## Contendio
+
+El contenido está distribuido de la siguiente manera:
+...
```
Vemos como todos los archivos son nuevos y todas las líneas se agregan a los archivos.

Finalmente podemos contar en base a la etiqueta HEAD para ver el commit dos antes al último:

```
$ ommit c059427da5ecb6796945a2076151fec01dd02c77
Author: rictor <rictor@gmail.com>
Date:   Fri Jul 22 02:53:43 2022 -0500

    Agregando los archivo index y perfiles de la carpeta public_html/

diff --git a/public_html/index.html b/public_html/index.html
new file mode 100644
index 0000000..c8a4fa8
--- /dev/null
+++ b/public_html/index.html
@@ -0,0 +1,15 @@
+<!DOCTYPE html>
+<html>
+<body>
+    <nav><a href="index.html">Inicio</a> | <a href="perfiles.html">Perfiles</a></nav>
+    <section>
+       <h2>Página de inicio</h2>
+       <hr />
+       <p>Párrafo principal de la página de inicio</p>
+    </section>
+    <footer>
...
```
Entonces hacer uso de git show implica una mezcla de `git log` y `git diff` para un sólo commit haciendo siempre la comparación con el commit inmediato anterior.

### 3. Trabajar con commits en GitHub

![Commits y github](Media/trabajando-con-commits-github.png)

Ya en la terminal hemos usado el comando `git log`, ahora veamos como ver la lista de commits en Github

```
$ git log
ommit f229371292f983ed292ea2317e39758808f16468 (HEAD -> master, origin2/master)
Author: rctorr <rictor@cuhrt.com>
Date:   Fri Jul 22 04:06:30 2022 -0500

    Agregando banner a la página principal

commit c09e1803698909ac794dcea07e4f08d708ff7955
Author: rictor <rictor@gmail.com>
Date:   Fri Jul 22 03:26:11 2022 -0500

    Eliminando lista de nombre del archivo perfiles

commit c059427da5ecb6796945a2076151fec01dd02c77
Author: rictor <rictor@gmail.com>
Date:   Fri Jul 22 02:53:43 2022 -0500

    Agregando los archivo index y perfiles de la carpeta public_html/

commit 8cf2cbfd613dcba994bd9764f9505b544c343cd5
Author: rctorr <rictor@cuhrt.com>
Date:   Fri Jul 22 02:03:42 2022 -0500

    Agregando descripción del proyecto
...
$ 
```
Y lo podemos comparar con lo que observamos en Github

Ahora el equivalente al comando `git show commit` por ejemplo para observar el último commit sería:

```
$ git show
commit f229371292f983ed292ea2317e39758808f16468 (HEAD -> master, origin2/master)
Author: rctorr <rictor@cuhrt.com>
Date:   Fri Jul 22 04:06:30 2022 -0500

    Agregando banner a la página principal

diff --git a/public_html/index.html b/public_html/index.html
index c8a4fa8..2831477 100644
--- a/public_html/index.html
+++ b/public_html/index.html
@@ -3,6 +3,7 @@
 <body>
     <nav><a href="index.html">Inicio</a> | <a href="perfiles.html">Perfiles</a></nav>
     <section>
+       <img src="static/image/banner.jpg">
        <h2>Página de inicio</h2>
        <hr />
        <p>Párrafo principal de la página de inicio</p>
diff --git a/public_html/static/image/banner.jpg b/public_html/static/image/banner.jpg
new file mode 100644
index 0000000..ce11a11
...
$ 
```
También podemos comparar en Github dando click al último commit.

Ahora en Github si damos click sobre los símbolos de `<>` justo después del id del commit entonces vemos la lista de archivos justo como estaban en ese commit, eso también lo podemos hacer con el comando `git checkout commit`, por ejemplo, queremos ver el estado dos commits atrás:

```
$ git checkout HEAD~2
Nota: cambiando a 'HEAD~2'.

Te encuentras en estado 'detached HEAD'. Puedes revisar por aquí, hacer
cambios experimentales y hacer commits, y puedes descartar cualquier
commit que hayas hecho en este estado sin impactar a tu rama realizando
otro checkout.

Si quieres crear una nueva rama para mantener los commits que has creado,
puedes hacerlo (ahora o después) usando -c con el comando checkout. Ejemplo:

  git switch -c <nombre-de-nueva-rama>

O deshacer la operación con:

  git switch -

Desactiva este aviso poniendo la variable de config advice.detachedHead en false

HEAD está ahora en c059427 Agregando los archivo index y perfiles de la carpeta public_html/

$ git status
HEAD desacoplada en c059427
nada para hacer commit, el árbol de trabajo esta limpio

$ 
```
Incluso `git status` indica que HEAD está desacoplada respecto a la rama master, pero en éste punto podemos ver la lista de los archivos justo como estaban en ese commit o también podemos ver el contenido de alguno de los archivos.

Si queremos regresar al último commit realizamos otro cambio con `git checkout master`

```
$ git checkout master
La posición previa de HEAD era c059427 Agregando los archivo index y perfiles de la carpeta public_html/
Cambiado a rama 'master'

$ 
```
Incluso podemos comparar con lo que muestra Github.

También exixte en Github algo similar al comando `git annotate archivo`

Por ejemplo veamos la historia de cambios para el archivo `public_public/index.html`:

```
$ git annotate public_html/index.html
c059427d        (    rictor     2022-07-22 02:53:43 -0500       1)<!DOCTYPE html>
c059427d        (    rictor     2022-07-22 02:53:43 -0500       2)<html>
c059427d        (    rictor     2022-07-22 02:53:43 -0500       3)<body>
c059427d        (    rictor     2022-07-22 02:53:43 -0500       4)    <nav><a href="index.html">Inicio</a> | <a href="perfiles.html">Perfiles</a></nav>
c059427d        (    rictor     2022-07-22 02:53:43 -0500       5)    <section>
f2293712        (    rctorr     2022-07-22 04:06:30 -0500       6)       <img src="static/image/banner.jpg">
c059427d        (    rictor     2022-07-22 02:53:43 -0500       7)       <h2>Página de inicio</h2>
c059427d        (    rictor     2022-07-22 02:53:43 -0500       8)       <hr />
c059427d        (    rictor     2022-07-22 02:53:43 -0500       9)       <p>Párrafo principal de la página de inicio</p>
c059427d        (    rictor     2022-07-22 02:53:43 -0500       10)    </section>
c059427d        (    rictor     2022-07-22 02:53:43 -0500       11)    <footer>
c059427d        (    rictor     2022-07-22 02:53:43 -0500       12)       <p>Derechos reservador @rctorr</p>
c059427d        (    rictor     2022-07-22 02:53:43 -0500       13)    </footer>
c059427d        (    rictor     2022-07-22 02:53:43 -0500       14)</body>
c059427d        (    rictor     2022-07-22 02:53:43 -0500       15)</html>
c059427d        (    rictor     2022-07-22 02:53:43 -0500       16)
```
En Github hacemos uso del botón **Blame** cuando se está visualizando el contenido de un archivo, además en Github existe un icono que nos permite hacer en algunas líneas justo la versión del archivo en ese commit en particular, sería equivalente a aplicar un `git checkout commit` y luego un `git annotate archivo`.

### 4. Commit de cambios directamente en GitHub

Así como hemos realizado cambios en el repo local, agregando, modificando o eliminando archivos, también podemos realizar estas operaciones en Github, por ejemplo vamos a agregar el archivo `public_html/Readme.md` con el contenido:

```
## Proyecto web demo

### Descripción

En ésta carpeta el archivo principal es index.html y todos los demás archivos son accedidos por medio de éste.
```
Entonces agrega el nombre del archivo, agrega una descripción corta del commit aplica el commit con el botón **Commit new file**.

También podemos modificar un archivo, por ejemplo `public_html/static/css/main.css` agregando las siguientes líneas:

```
img {
    width: 100%;
}
```

Finalmente para ver reflejados los últimos cambios podemos ir a nuestra cuenta virtual en Linux y obtener todos los cambios, luego ejecutar el comando `php -S 0.0.0.0:8000` o `python -m http.server` y abrir una página en el navegador con la dirección ip del servidor y el puerto 8000.


