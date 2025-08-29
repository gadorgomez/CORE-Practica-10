
# Práctica 10: Roles

Versión: 27 de Marzo de 2025

## Objetivos
* Afianzar los conocimientos obtenidos sobre el uso de Express para desarrollar servidores web.
* Aprender a gestionar roles y permisos para definir que operaciones puede hacer cada usuario.

## Descripción de la práctica

En esta práctica 10 se ampliará la **Práctica 9 Autores** añadiendo un sistema de permisos que limiten
las operaciones que puede hacer un usuario en funcion de su rol.

Estas limitaciones deben añadirse en los controladores, en las definiciones de rutas y en las vistas.

El alumno creará nuevos middlewares en los controladores de usuarios y posts. 
En funcion del rol del usuario, los nuevos middlewares permitirán el desarrollo normal de las
peticiones, o abortarán su ejecución.

El alumno usará estos middlewares en la definición de las rutas existentes, controlando que se puede 
y que no se puede ejecutar dependiendo del rol del usuario.

Por último, el usuario modificará las vistas para no mostrar los botones o enlaces que no 
le están permitidos al usuario en funcion de su rol.

El desarrollo pedido en esta práctica es igual al realizado en el mini proyecto **Autores y Autorización** visto
en las clases teóricas de la asignatura.
En el mini proyecto **Autores y Autorización** se impedía la ejecución de algunas primitivas en funcion del rol 
del usuario, y en esta práctica se aplicarán las mismas limitaciones, y se definirán otras nuevas.

Las limitaciones que se añadirán a la práctica son las siguientes:

* Para publicar un post el usuario debe estar logueado.
* Los posts solo pueden ser editados por su autor, o por un usuario administrador.
* Los posts solo pueden ser borrados por su autor, o por un usuario administrador.
* La lista de usuarios registrados solo la puede ver un usuario administrador.
* El perfil de un usuario solo lo puede ver el propio usuario, o un usuario administrador.
* Solo el administrador puede crear nuevos usuarios.
* El perfil de un usuario solo lo puede editar el propio usuario, o un usuario administrador.
* Borrar a un usuario de la BBDD solo le está permitido al propio usuario, o a un usuario administrador.

## Descargar el código del proyecto

Instrucciones [aquí](https://github.com/CORE-UPM/Instrucciones_Practicas/blob/main/README.md#descargar-el-c%C3%B3digo-del-proyecto).

## Tareas

### Tarea 1 - Copiar el trabajo ya realizado en la práctica 9.

En esta práctica hay que continuar y ampliar el desarrollo realizado en la práctica 9.

El alumno debe copiar el directorio **blog** de la **P9_Autores** en el directorio **P10_Roles/blog** de
esta práctica 10. Las tareas a realizar en esta práctica 10 de desarrollarán dentro del directorio **P10_Roles/blog**.

Para copiar/duplicar el directorio **P9_Autores/blog** en el directorio **P10_Roles/blog**, puede usar un
explorador de archivos. Asegúrese de copiar el directorio y no de moverlo de sitio, para no perder el trabajo original.
También puede ejecutar el siguiente comando en un terminal unix para copiar el directorio y todo su contenido:

    $ cp -r PATH_DE_PRACTICA_9/P9_Autores/blog PATH_DE_PRACTICA_10/P10_Roles/.


Ejecutar las migraciones de las prácticas anteriores en el caso de que no se haya copiado el archivo **.sqlite** con la base de datos:

    $ npm run migrate       ## sistemas unix
    $ npm run migrate_win   ## sistemas windows

y probar el funcionamiento del nuevo servidor.

### Tarea 2 - Crear los middlewares que protegen ciertas primitivas

Los middlewares que se usarán en esta práctica son parecidos o iguales  que los se desarrollaron en el mini proyecto **Autores y Autorización** para
los quizzes. 

El alumno puede reutilizar los middlewares **loginRequired** y **adminOrMyselfRequired** del controlador de sesiones. 
El middleware **loginRequired** aborta la petición en curso si el usuario no está logueado, y le redirige a la página de login.
El middleware **adminOrMyselfRequired** aborta la petición en curso si el usuario logueado no es un administrador o no es el usuario al que se refiere
el parámetro de ruta **:userId**.

El alumno debe crear otro middleware en el controlador de sesiones, llamado **adminRequired**, 
que solo permita la ejecución de la petición en curso si el usuario logueado es un administrador.

El alumno debe crear un middleware llamado **adminOrAuthorRequired** en el controlador de los posts. 
Este middleware debe abortar la petición en curso si el usuario logueado no es un administrador, o no es el autor del post al que se refiere
el parámetro de ruta **:postId**.
En el controlador de los quizzes del mini proyecto **Quiz** existe un middleware, también llamado **adminOrAuthorRequired**,  
que aborta la petición en curso si el usuario logueado no es un administrador, o no es el autor del quiz al que se refiere
el parámetro de ruta **:quizId**. 
El alumno puede inspirarse en este middleware para implementar el que se le pide.

Los middlewares anteriores deben usarse en las definiciones de las rutas de **routes/index.js** para impedir las ejecuciones 
que se han enumerado más arriba, en la descripción de la práctica.

#### Probar

Ya puede probar si las rutas están bien protegidas. Logueese con diferentes tipos de usuarios y compruebe que los botones y enlaces de las rutas protegidas no funcionan.

Támbien deberia probar las rutas que son llamadas internamente desde los formularios.

### Tarea 3 - Adaptar las vistas

En esta tarea el alumno tiene que modificar las vistas para no mostrar los enlaces o botones que conectan con las primitivas protegidas. 

El alumno debe añadir en las vistas EJS el código javascript necesario para que:

* El botón de crear un nuevo post solo le aparezca al usuario si está logueado.
* Los botones para editar o borrar un post solo le aparecen a los usuarios administradores o al autor del post.
* El botón de crear un nuevo usuario solo le aparezca a los usuarios administradores.
* El botón de la barra de navegación que muestra el listado de usuarios solo le aparece a los usuario administradores.
* Los botones para ver un usuario, editarlo o borrarlo solo le aparecen al propio usuario, o un usuario administrador.

#### Probar

Ya puede probar si los botones y enlaces se ocultan o muestran según el rol del usuario logueado.


## Pruebas con el autocorector

Instrucciones [aquí](https://github.com/CORE-UPM/Instrucciones_Practicas/blob/main/README.md#pruebas-con-el-autocorector).

## Pruebas manuales y capturas de pantalla

Instrucciones [aquí](https://github.com/CORE-UPM/Instrucciones_Practicas/blob/main/README.md#pruebas-manuales-y-capturas-de-pantalla).

Capturas a entregar con esta práctica: 

- Captura 1: Captura de la pantalla que muestra el listado de todos los posts.
  Realice esta captura cuando no hay nadie logueado para que no aparezcan los botones de editar o borrar los posts existentes.
  Tampoco debe aparecer el botón de listar todos los usuarios en la barra de navegación.
  Realice la captura de forma que se vea el botón de login en la cabecera de la pantalla.
<kbd>
<img src="https://github.com/CORE-UPM/P10_Roles/assets/716928/8f6b12e8-bf3f-4ef9-9d8b-f652ceff33d0" alt="captura de pantalla" width="600"/>
</kbd>

- Captura 2: Captura de la pantalla que muestra el listado de todos los posts.
  Realice esta captura cuando el usuario logueado no es un administrador. Deben verse los botones de editar y borrar los posts creados por el usuario logueado.
  No debe verse el botón de listar todos los usuarios en la barra de navegación.
  Y en la cabecera de la pantalla debe mostrarse el nombre del usuario logueado y el botón de logout.
<kbd>
<img src="https://github.com/CORE-UPM/P10_Roles/assets/716928/e25ca196-c5c6-4cc0-8945-67ade3848bb4" alt="captura de pantalla" width="600"/>
</kbd>

- Captura 3: Captura de la pantalla que muestra el listado de todos los posts.
  Realice esta captura cuando el usuario logueado es admin. 
  Deben verse los botones de editar y borrar en todos posts.
  También debe aparecer el botón de listar todos los usuarios en la barra de navegación.
  Realice la captura de forma que se vea el nombre admin y el botón de logout en la cabecera de la pantalla.
<kbd>
<img src="https://github.com/CORE-UPM/P10_Roles/assets/716928/1ccf892c-3bf0-4b2a-8637-62f61ae5b25a" alt="captura de pantalla" width="600"/>
</kbd>

## Instrucciones para la Entrega y Evaluación.

Instrucciones [aquí](https://github.com/CORE-UPM/Instrucciones_Practicas/blob/main/README.md#instrucciones-para-la-entrega-y-evaluaci%C3%B3n
).

## Rúbrica

Antes de evaluar la práctica se realizarán un serie de comprobaciones:
- Existe el directorio blog.
- Las tablas de la base de datos son correctas.
- Se ha usado correctamente el marco de aplicación.
- Existen los ficheros pedidos: controladores, migraciones, seeders, ...
- Se han creado los scripts pedidos en package.json.

Una vez superadas las comprobaciones anteriores,
se puntuará la práctica sumando el % indicado a la nota total si la parte indicada es correcta:

- **5%:** * No se puede publicar un post si no hay nadie logueado.
- **3%:** * El botón de crear un post no aparece si no hay nadie logueado.
- **3%:** * Se puede publicar un post si hay alguien logueado.
- **3%:** * El botón de crear un post aparece si hay alguien logueado.
- **2%:** * Un post no puede editarse si no hay nadie logueado.
- **2%:** * El botón de editar un post no aparece si no hay nadie logueado.
- **2%:** * Un post no puede editarse si el usuario logueado no es ni administrador, ni el autor del post.
- **2%:** * El botón de editar un post no aparece si el usuario logueado no es ni administrador, ni el autor del post.
- **2%:** * Un post puede ser editado por su autor.
- **2%:** * El botón de editar un post aparece si el usuario logueado es el autor del post.
- **2%:** * Un post puede ser editado por un administrador.
- **2%:** * El botón de editar un post aparece si el usuario logueado es un administrador.
- **2%:** * Un post no puede borrarse si no hay nadie logueado.
- **2%:** * El botón de borrar un post no aparece si no hay nadie logueado.
- **2%:** * Un post no puede borrarse si el usuario logueado no es ni administrador, ni el autor del post.
- **2%:** * El botón de borrar un post no aparece si el usuario logueado no es ni administrador, ni el autor del post.
- **2%:** * Un post puede ser borrado por su autor.
- **2%:** * El botón de borrar un post aparece si el usuario logueado es el autor del post.
- **2%:** * Un post puede ser borrado por un administrador.
- **2%:** * El botón de borrar un post aparece si el usuario logueado es un administrador.
- **2%:** * La peticion /users no está permitida si nadie está logueado.
- **2%:** * La peticion /users no está permitida si el usuario logueado no es un administrador.
- **2%:** * La peticion /users  está permitida si el usuario logueado  es un administrador.
- **2%:** * El boton /users de la barra de navegación no aparece si no hay nadie logueado.
- **2%:** * El boton /users de la barra de navegación no aparece si el usuario logueado no es administrador.
- **2%:** * El boton /users de la barra de navegación  aparece si el usuario logueado es administrador.
- **4%:** * La petición para ver el perfil de un usuario no está permitida si no hay nadie logueado.
- **4%:** * La petición para ver el perfil de un usuario no está permitida si el usuario logueado no es un administrador.
- **4%:** * La petición para ver el perfil de un usuario está permitida si el usuario logueado es un administrador.
- **3%:** * La petición para editar el perfil de un usuario no está permitida si no hay nadie logueado.
- **3%:** * La petición para editar el perfil de un usuario no está permitida si el usuario logueado no es un administrador.
- **3%:** * La petición para editar el perfil de un usuario está permitida si el usuario logueado es un administrador.
- **3%:** * La petición para borrar el perfil de un usuario no está permitida si no hay nadie logueado.
- **3%:** * La petición para borrar el perfil de un usuario no está permitida si el usuario logueado no es un administrador.
- **3%:** * La petición para borrar el perfil de un usuario está permitida si el usuario logueado es un administrador.
- **4%:** * La petición para crear un usuario no está permitida si no hay nadie logueado.
- **4%:** * La petición para crear un usuario no está permitida si el usuario logueado no es un administrador.
- **4%:** * La petición para crear un usuario está permitida si el usuario logueado es un administrador.


Si pasa todos los tests se dará la máxima puntuación.
