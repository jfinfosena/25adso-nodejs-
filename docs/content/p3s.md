### **Actividad: Crear un controlador básico para gestionar películas en NestJS**

**Enunciado**  
Como desarrolladores principiantes en NestJS, su tarea es crear un controlador para gestionar una colección de **películas** en una aplicación de servidor. El controlador debe manejar solicitudes HTTP básicas (GET, POST, PUT, DELETE) y permitir acceder a parámetros de ruta y datos del cuerpo de la solicitud. La actividad se centra en los conceptos fundamentales de controladores, rutas y manejo de parámetros, sin usar servicios ni DTOs, y siguiendo las indicaciones vistas en los puntos 1 al 4 del tutorial sobre controladores en NestJS.

**Objetivo**  
Implementar un controlador en NestJS que gestione un recurso de **películas** con rutas para listar, obtener, crear, actualizar y eliminar películas, utilizando decoradores de rutas y parámetros.

**Indicaciones**  
1. **Modelo**: El recurso a manejar es **películas** (movies). Cada película tiene un `id` (número), `title` (cadena) y `year` (número). No se usará una base de datos; en su lugar, simulen los datos con un array en memoria dentro del controlador.
2. **Requisitos del controlador**:
   - Crear una clase `MoviesController` decorada con `@Controller('movies')` para definir la ruta base `/movies`.
   - Implementar las siguientes rutas usando los decoradores HTTP correspondientes:
     - **GET /movies**: Devuelve la lista completa de películas.
     - **GET /movies/:id**: Devuelve una película específica según su ID. Si no existe, devolver un mensaje de error simple (sin usar excepciones como `NotFoundException`).
     - **POST /movies**: Crea una nueva película a partir de los datos enviados en el cuerpo de la solicitud (título y año).
     - **PUT /movies/:id**: Actualiza una película existente según su ID, usando los datos del cuerpo.
     - **DELETE /movies/:id**: Elimina una película según su ID.
   - Usar `@Param()` para capturar el parámetro `id` de la ruta.
   - Usar `@Body()` para capturar los datos del cuerpo en las rutas POST y PUT.
   - Usar `@Query()` para agregar un parámetro de consulta opcional en la ruta GET /movies que permita filtrar películas por año (por ejemplo, `/movies?year=2023`).
3. **Restricciones**:
   - No usar servicios ni DTOs.
   - No usar pipes como `ParseIntPipe` ni excepciones HTTP avanzadas.
   - Mantener los datos en un array dentro del controlador (simulando una base de datos).
   - No modificar códigos de estado HTTP predeterminados.
4. **Entregable**:
   - Un archivo `movies.controller.ts` con el código del controlador.
   - El código debe ser claro, con comentarios que expliquen cada método.
5. **Puntos a evaluar**:
   - Correcta definición de rutas con decoradores HTTP.
   - Manejo adecuado de parámetros de ruta (`@Param`) y cuerpo (`@Body`).
   - Uso de `@Query` para el filtro por año.
   - Organización y claridad del código.

**Plantilla inicial**  
A continuación, se proporciona una plantilla básica para que los estudiantes completen:

```typescript
import { Controller, Get, Post, Put, Delete, Param, Body, Query } from '@nestjs/common';

@Controller('movies')
export class MoviesController {
  // Array para simular la base de datos de películas
  private movies = [
    { id: 1, title: 'Inception', year: 2010 },
    { id: 2, title: 'The Matrix', year: 1999 },
  ];

  // TODO: Implementar los métodos según las indicaciones
}
```

**Instrucciones para los estudiantes**  
1. Dentro de la clase `MoviesController`, implementen los métodos para las rutas especificadas (GET, GET/:id, POST, PUT/:id, DELETE/:id).
2. Usen el array `movies` para almacenar y manipular los datos.
3. Para la ruta GET /movies, incluyan un filtro opcional por año usando `@Query('year')`.
4. Asegúrense de que los métodos manejen correctamente los parámetros de ruta (`id`) y el cuerpo de la solicitud (`title` y `year`).
5. Agreguen comentarios explicando qué hace cada método.
6. Prueben las rutas usando un cliente como Postman con solicitudes como:
   - GET `http://localhost:3000/movies`
   - GET `http://localhost:3000/movies?year=2010`
   - GET `http://localhost:3000/movies/1`
   - POST `http://localhost:3000/movies` con `{ "title": "Avatar", "year": 2009 }`
   - PUT `http://localhost:3000/movies/1` con `{ "title": "Inception Updated", "year": 2010 }`
   - DELETE `http://localhost:3000/movies/1`

**Solución de ejemplo**  
A continuación, se proporciona una solución completa para que los estudiantes puedan compararla después de intentar la actividad. **Nota**: Esta solución debe usarse como referencia después de que los estudiantes completen la actividad.

```typescript
import { Controller, Get, Post, Put, Delete, Param, Body, Query } from '@nestjs/common';

@Controller('movies')
export class MoviesController {
  // Array para simular la base de datos de películas
  private movies = [
    { id: 1, title: 'Inception', year: 2010 },
    { id: 2, title: 'The Matrix', year: 1999 },
  ];

  // GET /movies: Devuelve todas las películas, con filtro opcional por año
  @Get()
  findAll(@Query('year') year?: string) {
    if (year) {
      return this.movies.filter(movie => movie.year === parseInt(year));
    }
    return this.movies;
  }

  // GET /movies/:id: Devuelve una película por su ID
  @Get(':id')
  findOne(@Param('id') id: string) {
    const movie = this.movies.find(movie => movie.id === parseInt(id));
    if (!movie) {
      return { message: `Movie with ID ${id} not found` };
    }
    return movie;
  }

  // POST /movies: Crea una nueva película
  @Post()
  create(@Body() body: { title: string; year: number }) {
    const newId = this.movies.length > 0 ? Math.max(...this.movies.map(m => m.id)) + 1 : 1;
    const newMovie = { id: newId, title: body.title, year: body.year };
    this.movies.push(newMovie);
    return newMovie;
  }

  // PUT /movies/:id: Actualiza una película existente
  @Put(':id')
  update(@Param('id') id: string, @Body() body: { title: string; year: number }) {
    const index = this.movies.findIndex(movie => movie.id === parseInt(id));
    if (index === -1) {
      return { message: `Movie with ID ${id} not found` };
    }
    this.movies[index] = { id: parseInt(id), title: body.title, year: body.year };
    return this.movies[index];
  }

  // DELETE /movies/:id: Elimina una película
  @Delete(':id')
  remove(@Param('id') id: string) {
    const index = this.movies.findIndex(movie => movie.id === parseInt(id));
    if (index === -1) {
      return { message: `Movie with ID ${id} not found` };
    }
    const deletedMovie = this.movies.splice(index, 1)[0];
    return { message: `Movie with ID ${id} deleted`, data: deletedMovie };
  }
}
```

**Explicación de la solución**:
- **Rutas**: Se usan `@Get`, `@Post`, `@Put`, y `@Delete` para las operaciones CRUD.
- **Parámetros**:
  - `@Param('id')`: Captura el ID de la ruta (por ejemplo, `/movies/1`).
  - `@Body()`: Obtiene `title` y `year` del cuerpo de la solicitud.
  - `@Query('year')`: Filtra películas por año en GET /movies.
- **Datos**: El array `movies` simula una base de datos en memoria.
- **Lógica simple**: Los métodos manipulan el array directamente, sin servicios ni validaciones avanzadas, respetando las restricciones.
- **Respuestas**: Los métodos devuelven datos que NestJS convierte en JSON, con mensajes de error simples para casos no encontrados.


## **Solución: Controlador de películas con bucles `for...of`**

```typescript
import { Controller, Get, Post, Put, Delete, Param, Body, Query } from '@nestjs/common';

@Controller('movies')
export class MoviesController {
  // Array para simular la base de datos de películas
  private movies = [
    { id: 1, title: 'Inception', year: 2010 },
    { id: 2, title: 'The Matrix', year: 1999 },
  ];

  // GET /movies: Devuelve todas las películas, con filtro opcional por año
  @Get()
  findAll(@Query('year') year?: string) {
    // Si no se proporciona un año, devolver todas las películas
    if (!year) {
      return this.movies;
    }

    // Filtrar películas por año usando un bucle for...of
    const filteredMovies = [];
    const yearNum = parseInt(year);
    for (const movie of this.movies) {
      if (movie.year === yearNum) {
        filteredMovies.push(movie);
      }
    }
    return filteredMovies;
  }

  // GET /movies/:id: Devuelve una película por su ID
  @Get(':id')
  findOne(@Param('id') id: string) {
    const idNum = parseInt(id);
    // Buscar película por ID usando un bucle for...of
    for (const movie of this.movies) {
      if (movie.id === idNum) {
        return movie;
      }
    }
    return { message: `Movie with ID ${id} not found` };
  }

  // POST /movies: Crea una nueva película
  @Post()
  create(@Body() body: { title: string; year: number }) {
    // Generar un nuevo ID basado en el máximo ID existente
    let maxId = 0;
    for (const movie of this.movies) {
      if (movie.id > maxId) {
        maxId = movie.id;
      }
    }
    const newId = maxId + 1;

    // Crear y agregar la nueva película
    const newMovie = { id: newId, title: body.title, year: body.year };
    this.movies.push(newMovie);
    return newMovie;
  }

  // PUT /movies/:id: Actualiza una película existente
  @Put(':id')
  update(@Param('id') id: string, @Body() body: { title: string; year: number }) {
    const idNum = parseInt(id);
    // Buscar el índice de la película por ID
    let index = -1;
    let i = 0;
    for (const movie of this.movies) {
      if (movie.id === idNum) {
        index = i;
        break;
      }
      i++;
    }

    // Si no se encuentra, devolver mensaje de error
    if (index === -1) {
      return { message: `Movie with ID ${id} not found` };
    }

    // Actualizar la película
    this.movies[index] = { id: idNum, title: body.title, year: body.year };
    return this.movies[index];
  }

  // DELETE /movies/:id: Elimina una película
  @Delete(':id')
  remove(@Param('id') id: string) {
    const idNum = parseInt(id);
    // Buscar el índice de la película por ID
    let index = -1;
    let i = 0;
    for (const movie of this.movies) {
      if (movie.id === idNum) {
        index = i;
        break;
      }
      i++;
    }

    // Si no se encuentra, devolver mensaje de error
    if (index === -1) {
      return { message: `Movie with ID ${id} not found` };
    }

    // Eliminar la película usando splice
    const deletedMovie = this.movies[index];
    const newMovies = [];
    let j = 0;
    for (const movie of this.movies) {
      if (j !== index) {
        newMovies.push(movie);
      }
      j++;
    }
    this.movies = newMovies;

    return { message: `Movie with ID ${id} deleted`, data: deletedMovie };
  }
}
```

---

### **Explicación de la solución**

1. **Controlador y rutas**:
   - La clase `MoviesController` usa `@Controller('movies')` para establecer la ruta base `/movies`.
   - Los métodos usan decoradores HTTP (`@Get`, `@Post`, `@Put`, `@Delete`) para manejar las operaciones CRUD:
     - `GET /movies`: Lista todas las películas o filtra por año.
     - `GET /movies/:id`: Obtiene una película por ID.
     - `POST /movies`: Crea una nueva película.
     - `PUT /movies/:id`: Actualiza una película.
     - `DELETE /movies/:id`: Elimina una película.

2. **Manejo de parámetros**:
   - **`@Param('id')`**: Captura el parámetro `id` de la ruta (por ejemplo, `/movies/1`). Se convierte a número con `parseInt` para comparaciones.
   - **`@Body()`**: Captura el cuerpo de la solicitud (por ejemplo, `{ "title": "Avatar", "year": 2009 }`) en las rutas POST y PUT.
   - **`@Query('year')`**: Captura el parámetro de consulta `year` (por ejemplo, `/movies?year=2010`) para filtrar películas.

3. **Uso de bucles `for...of`**:
   - En lugar de métodos como `find`, `filter` o `map`, se usan bucles `for...of` para iterar sobre el array `movies`.
   - **GET /movies**: Filtra películas por año creando un nuevo array `filteredMovies`.
   - **GET /movies/:id**: Busca una película comparando el ID.
   - **POST /movies**: Encuentra el máximo ID para asignar un nuevo ID.
   - **PUT /movies/:id**: Busca el índice de la película para actualizarla.
   - **DELETE /movies/:id**: Busca el índice y crea un nuevo array sin la película eliminada.

4. **Gestión de datos**:
   - El array `movies` simula una base de datos en memoria, inicializado con dos películas.
   - Los métodos manipulan este array directamente, respetando la restricción de no usar servicios.
   - No se usan DTOs ni pipes, por lo que no hay validación avanzada de los datos de entrada.

5. **Respuestas**:
   - Los métodos devuelven objetos o arrays que NestJS convierte en JSON.
   - Para casos de error (por ejemplo, película no encontrada), se devuelve un objeto con un mensaje: `{ message: "Movie with ID X not found" }`.

---

### **Pruebas sugeridas**
Los estudiantes pueden probar las rutas con un cliente HTTP como Postman:
- **GET** `http://localhost:3000/movies` → Devuelve `[{ id: 1, title: "Inception", year: 2010 }, { id: 2, title: "The Matrix", year: 1999 }]`.
- **GET** `http://localhost:3000/movies?year=2010` → Devuelve `[{ id: 1, title: "Inception", year: 2010 }]`.
- **GET** `http://localhost:3000/movies/1` → Devuelve `{ id: 1, title: "Inception", year: 2010 }`.
- **GET** `http://localhost:3000/movies/999` → Devuelve `{ message: "Movie with ID 999 not found" }`.
- **POST** `http://localhost:3000/movies` con `{ "title": "Avatar", "year": 2009 }` → Devuelve `{ id: 3, title: "Avatar", year: 2009 }`.
- **PUT** `http://localhost:3000/movies/1` con `{ "title": "Inception Updated", "year": 2011 }` → Devuelve `{ id: 1, title: "Inception Updated", year: 2011 }`.
- **DELETE** `http://localhost:3000/movies/1` → Devuelve `{ message: "Movie with ID 1 deleted", data: { id: 1, title: "Inception", year: 2010 } }`.

---
