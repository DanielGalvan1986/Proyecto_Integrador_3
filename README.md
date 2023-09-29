# _Proyecto Integrador N°3_

El presente documento, es el *Proyecto Integral N°3* de **Argentina Program 4.0**. Esta es una pequeña solución informática para administrar el contenido de la plataforma _Trailerflix_.
La misma, fue diseñada y construida sobre una arquitectura API RESTful, la cual está desarrollada bajo las restricciones y recomendaciones de REST, además, implementa buenas prácticas de programación

### Especificaciones
- Servidor: http://127.0.0.1:3005
- Autor: Jorge Daniel Galván
  
### Requerimientos
- Node.js v18.17.0
- MySQL
- Git v2.40.1
- IDE - Visual Studio Code v1.78.2 

#### Estructura de Directorios
tree
    ├── node_modules
    ├── src
    │   ├── conexion
    │   │   └── conection.js
    │   └── server.js
    ├── .env
    ├── .env.dist
    ├── .gitignore
    ├── package.json
    ├── package-lock.json 
    ├── README.md 
    └── trailerflix.sql


---
### CONFIGURACIONES DE ENTORNO
  #### VARIABLES DE ENTORNO
    Se debe realizar una copia del archivo *.env.dist* y renombrarlo como *.env*, luego de esto asignarle los valores correspondiente a las variables:

    DATABASE:trailerflix
    
    DBUSER=tu-usuario**Aqui colocar tu usuario**

    PASSWORD=tu-contraseña**Aqui colocar tu contraseña**
### CONFIGURACION BASE DE DATOS
    Se debe hacer correr en la base de datos el archivo *trailerflix.sql* ya que el mismo contiene los datos de la BBDD y la vista utilizada para poder realizar los request.
    
### MÓDULO DE CONTENIDO

Este módulo permite gestionar el contenido, pudiendo leer sus registros además de visualizar reportes filtrados por diferentes criterios de búsqueda.

#### Métodos HTTP

| Tipo          | URI           | Descripción                        |
|---------------|---------------|-----------------------------------|
| GET | http://127.0.0.1:3005/categoria | Nos muestra todas las categorias que existen |
| GET | http://127.0.0.1:3005/catalogo | Nos muestra el catálogo completo de la BBDD |
| GET | http://127.0.0.1:3005/catalogo/:id | Nos muestra un registro en específico(filtrado por ID) |
| GET | http://127.0.0.1:3005/catalogo/genero/:genero | Nos muestra el filtro por género |
| GET | http://127.0.0.1:3005/catalogo/categoria/:categoria | Nos muestra el filtro por categoria |

#### Método GET:
- Request:
  - Parámetros opcionales de tipo PARAMS:
    - /genero/Drama  (tipo: string. Trae los titulos del genero filtrado) 
    - /categoria/Serie (tipo: string. Trae los titulos de la categoria filtrada) 
     
  -Respuesta:

      json
           {
            "id": 1,
            "poster": "http://127.0.0.1:3005/public/posters/1.jpg",
            "titulo": "The Crown",
            "categoria": "Serie",
            "genero": "Drama,Hechos Verídicos",
            "resumen": "Este drama narra las rivalidades políticas y el romance de la reina Isabel II, así como los sucesos que moldearon la segunda mitad del siglo XX.",
            "temporadas": "4",
            "reparto": "Claire Fox,Olivia Colman,Matt Smith,Tobias Menzies,Vanesa Kirby,Helena Bonham Carter",
            "trailer": null
}

  -Código HTTP: *200* Devuelve el título o títulos filtrados

  -Código HTTP: *400* Message: No se encontraron resultados

  -Código HTTP: *500* Message: Error al procesar la consulta

#### Método GET - Específico:
- Request:
  - Parámetro obligatorio de tipo URL:
    - 18 (tipo: integer. Indica el código del catalogo que se requiere obtener)
     
  -Respuesta:

      json
           {
            "id": 18,
        "poster": "http://127.0.0.1:3005/public/posters/18.jpg",
        "titulo": "Ava",
        "categoria": "Pelicula",
        "genero": "Acción,Drama,Suspenso",
        "resumen": "Ava es una mortífera asesina a sueldo que trabaja para una organización de operaciones encubiertas, que viaja por todo el mundo acabando con aquellos objetivos que nadie más puede derribar. Cuando uno de sus encargos sale mal, Ava tendrá que luchar por una vida.",
        "temporadas": "N/A",
        "reparto": "Jessica Chastain,John Malkovich,Collin Farrell,Common,Geena Davis,Ioan Gruffudd",
        "trailer": null
}

  -Código HTTP: *200* Devuelve el título seleccionado

  -Código HTTP: *400* Message: No se encontraron resultados para este ID

  -Código HTTP: *500* Message: Error al procesar la consulta.