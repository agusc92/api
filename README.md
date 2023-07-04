# ApiMaspelis

## Indice
  * [Descripcion](#descripcion)
  * [Interactuar con la api](#interactuar-con-la-api)
  * [Codigos de estado de respuesta HTTP (codigos de error)](#codigos-de-estado-de-respuesta-http)
  * [Como realizar peticiones](#como-realizar-peticiones)
  * [Peliculas](#peliculas)
    + [Obtener coleccion de peliculas](#obtener-coleccion-de-peliculas)
        * [Query params aceptados](#query-params-aceptados)
    + [Obtener una pelicula en particular](#obtener-una-pelicula-en-particular)
    + [Agregar pelicula](#agregar-pelicula)
    + [Editar pelicula](#editar-pelicula)
    + [Eliminar una pelicula](#eliminar-una-pelicula)
  * [Generos](#generos)
    + [Obtener coleccion de generos](#obtener-coleccion-de-generos)
    + [Obtener un genero en particular](#obtener-un-genero-en-particular)
    + [Agregar un genero](#agregar-un-genero)
    + [Editar genero](#editar-genero)
    + [Eliminar un genero](#eliminar-un-genero)
## Descripcion

Mas pelis brinda distintos servicios de gestion para una pagina de peliculas online

## Interactuar con la api


Si quieres probar nuestra API de una manera rápida te recomendamos el uso de PostMan. Postman es una extensión de Google Chrome que permite interactuar con HTTP API's de forma sencilla a través de una interfaz amigable para construir peticiones y obtener respuestas.

## Codigos de estado de respuesta HTTP

La api utiliza los siguientes codigos para reportar los distintos errores que pueden surgir.

- 200 -> "OK" _Peticion realizada con exito_
- 201 -> "Create OK" _Elemento creado exitosamente_
- 400 -> "Bad Request" _sintaxis inválida_
- 404 -> "Not Found" _Elemento no encontrado_
- 500 -> "Internal Server Error" _Error en el sistema, contacte al dev: alumno@tudai.web_

## Como realizar peticiones

A continuacion se detalla las distintas rutas (endpoint) para realizar las distintas peticiones, algunas de ellas llevan parametros tanto obligatorios como opcionales.
Tenga en cuenta que al realizar una peticion recibira como respuesta un Json o un mensaje descriptivo del resultado de su solicitud y un codigo de error notificando el estado de la peticion.

## Peliculas

En esta seccion se desarrollaran los servicios relacionados al recurso **peliculas**

### Obtener coleccion de peliculas

Obtiene el listado de peliculas ordenadas por ID de manera ascendente.

| Verbo | End-point  | Ejemplo                      |
| ----- | ---------- | ---------------------------- |
| GET   | api/movies | https://localhost/api/movies |

Respuesta: Status: 200 "OK"

```json
[
  {
    "id_movie": 3,
    "movie_name": "Guardianes de la Galaxia",
    "movie_image": "http://gnula.nu/wp-content/uploads/2014/08/guardianes_de_la_galaxia.jpg",
    "synopsis": "Se trata de una aventura espacial de proporciones épicas y llena de acción...",
    "name_gender": "Comedia",
    "movie_date": "2010"
  }
]
```

##### Query params aceptados

| Parametro | Descripcion                                                                                                                                                                                                   | Tipo    | Ejemplo                                               | caracter |
| --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------- | ----------------------------------------------------- | -------- |
| Id_gender | Envia un ID de genero de peliculas para filtrar los resultados por los diferentes generos disponibles                                                                                                         | Integer | https://localhost/api/movies?id_gender=1              | Opcional |
| sort      | Envía este parámetro para ordenar las películas por diferentes atributos. Valores posibles:` id_movie`, `movie_name`, `id_gender`, `movie_date`                                                                                 | string  | https://localhost/api/movies?sort=id_movie            | Opcional |
| order     | Envía este parámetro para especificar el sentido del orden de las películas, este parametro debe ir acompañado por el parametro `sort`. Valores posibles: `asc`(orden ascendente) y `desc` (orden descendente) | string  | https://localhost/api/movies?sort=id_movie&&order=asc | opcional |
| page      | Envia este parametro para obtener una pagina especifica de películas paginadas de a 5                                                                                                                            | integer | https://localhost/api/movies?page=1                   | opcional |

### Obtener una pelicula en particular

| Verbo | End-point      | Ejemplo                          |
| ----- | -------------- | -------------------------------- |
| GET   | api/movies/:ID | https://localhost/api/movies/:ID |

| Parametro | Descripcion                 | Tipo    | Ejemplo                        | caracter    |
| --------- | --------------------------- | ------- | ------------------------------ | ----------- |
| :ID       | ID de la pelicula a obtener | Integer | https://localhost/api/movies/2 | Obligatorio |

Respuesta: Status: 200 "OK"

```json
{
  "id_movie": 3,
  "movie_name": "Guardianes de la Galaxia",
  "movie_image": "http://gnula.nu/wp-content/uploads/2014/08/guardianes_de_la_galaxia.jpg",
  "synopsis": "Se trata de una aventura espacial de proporciones épicas y llena de acción...",
  "name_gender": "Comedia",
  "movie_date": "2010"
}
```

### Agregar pelicula

permite agregar una pelicula a la base de datos

| Verbo | End-point  | Ejemplo                      |
| ----- | ---------- | ---------------------------- |
| POST  | api/movies | https://localhost/api/movies |

| Atributo    | Descripcion                                                      | Tipo    | caracter    | Ejemplo                                  |
| ----------- | ---------------------------------------------------------------- | ------- | ----------- | ---------------------------------------- |
| movie_name  | Nombre de la película que se quiere agregar.                     | string  | Obligatorio | El oso panda                             |
| movie_image | url a la imagen de la pelicula                                   | string  | Obligatorio | http://galeria/imagen.jpg                |
| synopsis    | Breve descripción de la película que quiere agregar              | string  | Obligatorio | Las increibles aventuras de el oso panda |
| id_gender   | ID del genero al cual pertenece la película que se desea agregar | integer | Obligatorio | 5                                        |
| movie_date  | Año de estreno de la película que se quiere agregar              | integer | Obligatorio | 2020                                     |

ejemplo de body:

```json
{
  "movie_name": "Guardianes de la Galaxia",
  "movie_image": "http://gnula.nu/wp-content/uploads/2014/08/guardianes_de_la_galaxia.jpg",
  "synopsis": "Se trata de una aventura espacial de proporciones épicas y llena de acción...",
  "id_gender": "5",
  "movie_date": "2010"
}
```

Respuesta: Status: 201 "Create OK"

### Editar pelicula

permite editar una pelicula a la base de datos

| Verbo | End-point      | Ejemplo                          |
| ----- | -------------- | -------------------------------- |
| POST  | api/movies/:ID | https://localhost/api/movies/:ID |

| Parametro | Descripcion                 | Tipo    | Ejemplo                        | caracter    |
| --------- | --------------------------- | ------- | ------------------------------ | ----------- |
| :ID       | ID de la pelicula a obtener | Integer | https://localhost/api/movies/2 | Obligatorio |

| Atributo    | Descripcion                                                     | Tipo    | caracter    | Ejemplo                                  |
| ----------- | --------------------------------------------------------------- | ------- | ----------- | ---------------------------------------- |
| id_movie    | ID de la película que se quiere editar.                         | integer | Obligatorio | 3                                        |
| movie_name  | Nombre de la película que se quiere editar.                     | string  | Obligatorio | La mascara                               |
| movie_image | url a la imagen de la pelicula                                  | string  | Obligatorio | http://galeria/imagen.jpg                |
| synopsis    | Breve descripción de la película que quiere editar              | string  | Obligatorio | Una misteriosa masca que concede poderes |
| id_gender   | ID del genero al cual pertenece la película que se desea editar | integer | Obligatorio | 5                                        |
| movie_date  | Año de estreno de la película que se quiere editar              | integer | Obligatorio | 2020                                     |

ejemplo de body:

```json
{
  "id_movie": 3,
  "movie_name": "Guardianes de la Galaxia",
  "movie_image": "http://gnula.nu/wp-content/uploads/2014/08/guardianes_de_la_galaxia.jpg",
  "synopsis": "Se trata de una aventura espacial de proporciones épicas y llena de acción...",
  "id_gender": "5",
  "movie_date": "2010"
}
```

Respuesta: Status: 200 " OK"

### Eliminar una pelicula

Permite eliminar una pelicula

| Verbo  | End-point      | Ejemplo                        |
| ------ | -------------- | ------------------------------ |
| DELETE | api/movies/:ID | https://localhost/api/movies/3 |

| Parametro | Descripcion                               | Tipo    | caracter    | Ejemplo |
| --------- | ----------------------------------------- | ------- | ----------- | ------- |
| :ID       | ID de la película que se quiere eliminar. | integer | Obligatorio | 3       |

Respuesta: Status: 200 "OK"

## Generos

En esta seccion se desarrollaran los servicios relacionados al recurso **generos**

### Obtener coleccion de generos

Permite obtener un listado de todos los generos

| Verbo | End-point   | Ejemplo                       |
| ----- | ----------- | ----------------------------- |
| GET   | api/genders | https://localhost/api/genders |

Respuesta: Status: 200 "OK"

```json
[
  {
    "id_gender": 1,
    "name_gender": "Drama",
    "amount": 1,
    "prox_estreno": "Sexto sentido"
  },
  {
    "id_gender": 2,
    "name_gender": "Terror",
    "amount": 2,
    "prox_estreno": "Aterrados"
  }
]
```

### Obtener un genero en particular

| Verbo | End-point       | Ejemplo                           |
| ----- | --------------- | --------------------------------- |
| GET   | api/genders/:ID | https://localhost/api/genders/:ID |

| Parametro | Descripcion             | Tipo    | Ejemplo                         | caracter    |
| --------- | ----------------------- | ------- | ------------------------------- | ----------- |
| :ID       | ID del genero a obtener | Integer | https://localhost/api/genders/2 | Obligatorio |

Respuesta: Status: 200 "OK"

```json
{
  "id_gender": 2,
  "name_gender": "Terror",
  "amount": 2,
  "prox_estreno": "Aterrados"
}
```
### Agregar un genero

permite agregar un genero a la base de datos

| Verbo | End-point  | Ejemplo                      |
| ----- | ---------- | ---------------------------- |
| POST  | api/genders | https://localhost/api/genders |

| Atributo    | Descripcion                                                      | Tipo    | caracter    | Ejemplo                                  |
| ----------- | ---------------------------------------------------------------- | ------- | ----------- | ---------------------------------------- |
| name_gender  | Nombre del genero que se quiere agregar.                     | string  | Obligatorio | thriller   |
|prox_estreno| Nombre de la pelicula proxima a estrenar en este genero|string|Obligatorio|Las colinas tienen ojos|


ejemplo de body:

```json
{
  "name_gender": "thriller",
  "prox_estreno":"Las colinas tienen ojos"
}
```
Respuesta: Status: 200 “ OK”
### Editar genero

permite editar un genero a la base de datos

| Verbo | End-point       | Ejemplo                         |
| ----- | --------------- | ------------------------------- |
| POST  | api/genders/:ID | https://localhost/api/genders/7 |

| Parametro | Descripcion                         | Tipo    | caracter    | Ejemplo |
| --------- | ----------------------------------- | ------- | ----------- | ------- |
| :ID       | ID del genero que se quiere editar. | integer | Obligatorio | 7       |

| Atributo     | Descripcion                                            | Tipo   | caracter    | Ejemplo   |
| ------------ | ------------------------------------------------------ | ------ | ----------- | --------- |
| name_gender  | Nombre de la película que se quiere editar             | string | Obligatorio | 3         |
| prox_estreno | nombre del proximo estreno perteneciente a este genero | string | obligatorio | Soy otaku |

ejemplo de body:

```json
{
  "name_gender": "Drama",
  "prox_estreno": "quinto sentido"
}
```

Respuesta: Status 200 "OK"

### Eliminar un genero

Permite eliminar un genero

| Verbo  | End-point       | Ejemplo                         |
| ------ | --------------- | ------------------------------- |
| DELETE | api/genders/:ID | https://localhost/api/genders/3 |

| Parametro | Descripcion                           | Tipo    | caracter    | Ejemplo |
| --------- | ------------------------------------- | ------- | ----------- | ------- |
| :ID       | ID del genero que se quiere eliminar. | integer | Obligatorio | 3       |

Respuesta: Status: 200 "OK"
