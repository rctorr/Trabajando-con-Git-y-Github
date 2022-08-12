## Módulo-10: Ejemplo Git y Github con un proyecto

### Contenido

1. Introducción al Proyecto Git
2. Configurar el repositorio Git y branches para un nuevo proyecto
3. Permitir que los desarrolladores registren el código
4. Habilitación del flujo de trabajo de DevOps en branche de desarrollo
5. Push request (PR) para fusionar código de Dev Branch a UAT Branch
6. Liberar código en producción

### 1. Introducción al Proyecto Git

En éste módulo vamos a realizar un proyecto aplicando varios de los conceptos vistos a lo largo del curso.

El proyecto consiste en crear una pagina web siguiendo de cerca la estructura de carpetas y archivos de un proyecto creado con el framework Django.

A continuación se enlistan las tareas que se sugieren realizar cada que se inicie un repo o un proyecto:

1. Crear una carpeta para el proyecto local e inicializar el repo
2. Crear un repo privado en github y vincularlo al repo local
3. Definir que la rama **master** será la usada para poner código en producción, **test** que será usada para poner código en el servidor de prueba y la rama **dev** y será la rama de desarrollo en el día a día. Adicionalmente cualquier tarea o requerimiento se tendrá que realizar en una rama adicional y no está permitido hacer push directamente a **master** y **dev**.
4. Agregar los colaboradores al repo
5. Se define el uso de autenticación usando el protocolo SSH, así que en caso de ser necesario agregar las llaves SSH públicas necesarias.
6. Proteger las ramas **master** y **dev**
7. La rama **dev** necesitará de 1 aprobación para aceptar los cambios, la rama **master** necesitará de 2 aprobaciones.
8. Una aprobación en la rama **dev** es cuando se valida que el nuevo requerimiento no presenta errores en el servidor de pruebas y se puede liberar a usuarios beta para su revisión.
9. Una aprobación en la rama **master** es cuando se valida que no se presentan errores de ejecución y que no haya roto nada del proyecto realizada por dos colaboradores.

### 2. Configurar el repositorio Git y branches para un nuevo proyecto

El proyecto partirá clonando el repo de plantilla sugerido https://github.com/rctorr/django-html-plantilla

Entonces:
1. Renombrar la carpeta a `django-html/`
2. Desvincular del repo remoto
3. Crear un nuevo repo remoto en github llamado `django-html` privado.
4. Vincular el repo local con el remoto y hacer push
5. Realizar los puntos 1, 2, 3, 4, 6 y 7
6. Definir la rama **dev** como la default en github

### 3. Permitir que los desarrolladores registren el código

1. En caso de ser necesario cada usuaro necesita generar su llave pública y privada
2. Agregar la llave pública a la configuración de su cuenta en github
3. Cada colaborador deberá clonar el repo

Además se definen los roles de desarrollo para cada colaborador.

- Página de inicio - Alejandro
- Página de módulos - Todos
- Módulo 1 - Ricardo
- Módulo 2 - Jesús
- Módulo 3 - Marco
- Módulo 4 - Alejandro


### 4. Habilitación del flujo de trabajo de DevOps en branche de desarrollo

Cada colaborador deberá realizar los siguientes requerimientos partiendo de la rama **dev** y creando una rama para cada tarea diferente.

1. Agregar una descripción a la página de inicio que incluya una bitácoras de cada una de las tareas realizadas.
1. Realizar merge de los cambios a la rama **dev**
1. Actualizar la página del módulo 1 con el nombre del colaborador y su email.
1. Entonces actualizar la página de módulos con la información del módulo actualizada y que ya está disponible.
1. Realizar merge de los cambios a la rama **dev**
1. Actualizar la página del módulo 2 con el nombre del colaborador y su email.
1. Entonces actualizar la página de módulos con la información del módulo actualizada y que ya está disponible.
1. Realizar merge de los cambios a la rama **dev**
1. Actualizar la página del módulo 3 con el nombre del colaborador y su email.
1. Entonces actualizar la página de módulos con la información del módulo actualizada y que ya está disponible.
1. Realizar merge de los cambios a la rama **dev**
1. Actualizar la página del módulo 4 con el nombre del colaborador y su email.
1. Entonces actualizar la página de módulos con la información del módulo actualizada y que ya está disponible.
1. Realizar merge de los cambios a la rama **dev**

### 5. Push request (PR) para fusionar código de Dev Branch a UAT Branch

1. Cada colaborador deberá realizar un PR de sus cambios para solicitar integrar sus cambios a la rama **test**
1. Realizar la revisión del código usando el usuario virtual **test** y validar que el código funciona correctamente en el servidor de pruebas.
1. Autorizar el PR y fusionar los cambios a la rama **test**

### 6. Liberar código en producción

1. Cada colaborador deberá realizar un PR de sus cambios para solicitar integrar sus cambios a la rama **master**
1. Realizar la revisión del código usando el usuario virtual **prod** y validar que el código funciona correctamente en el servidor de pruebas.
1. Autorizar el PR y fusionar los cambios a la rama **master**
