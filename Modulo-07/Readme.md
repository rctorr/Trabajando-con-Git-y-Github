## Módulo 07: Trabajar con el equipo

### Contenido

1. Bifurcar un repositorio
2. Creación de un pull request (PR)
3. Trabajar con repositorios privados
4. Agregar colaborador a un repositorio de GitHub
5. Creación de branche protegido
6. Etiquetado de un commit

### 1. Bifurcar un repositorio
![github fork](Media/github-fork.png)

Realizar el fork del repo: https://github.com/rctorr/sistema-abc-plantilla

Y revisar la información del repo bifurcado.

### 2. Creación de un pull request (PR)
![github pr](Media/github-pr.png)

Después de realizar la bifurcación el repo ya es nuestro y podemos clonarlo, realizar un cambio, hacer un push y entonces hacer un PR (Pull request) que es una petición que hace el usuario que bifurcó el usuario al usuario del repo original.

Entonces el usuario original puede revisar los PR recibidos y haceptarlos o no.

Clona el repo, realiza un cambio, has un pull y finalmente realizar un PR.

### 3. Trabajar con repositorios privados
Modificar el repo https://github.com/rctorr/sistema-abc como un repo privado y clonarlo, notar que se necesitan autenticar como usuario para poder clonarlo, así que el uso de el método por ssh sería el más conveniente.

### 4. Agregar colaborador a un repositorio de GitHub
Se pueden agregar colaboradores desde el menú de Settings -> Colaboradores, cuando se agregar un colaborador, se le está dando acceso para realizar cualquier operación sólo en éste repo.

Así que vamos a gregarlos al repo protegido de Sistema ABC y entonces realizamos un clone directo de éste repo, realizamos un cambio, add, commit y finalmente un push que ya se debería de poder hacer.

Nota: Mucho cuidado con éste tipo de permisos, siempre hay que mantener un respaldo local por si algo sale mal.

### 5. Creación de branche protegido

### 6. Etiquetado de un commit
El etiquetado de commit es muy útil para señalar puntos importantes en la historia de commits:

```
$ git tag v1.0
$ git push origin v1.0
...
$
```

También podemos agregar un mensaje e indicar un commit cualquiera:

```
$ git tag -a v0.1 34ae08c5871063860557fd67bb109787ab3cc8ef -m "Versión inicial beta 0.1 del proyecto"^C

$ git push origin v0.1
Enumerating objects: 1, done.
Counting objects: 100% (1/1), done.
Writing objects: 100% (1/1), 179 bytes | 59.00 KiB/s, done.
Total 1 (delta 0), reused 0 (delta 0), pack-reused 0
To github.com:rctorr/sistema-abc.git
 * [new tag]         v0.1 -> v0.1

```
