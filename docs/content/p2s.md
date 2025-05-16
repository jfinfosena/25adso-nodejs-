# Solución: Actividad de Consulta sobre Conceptos de NestJS, Prisma y MySQL

A continuación, se presentan las respuestas a las 16 preguntas de la actividad de consulta, explicando los conceptos aplicados en la creación de una aplicación básica con NestJS, Prisma y MySQL.

## Respuestas

### Conceptos de NestJS
1. **¿Qué es NestJS y qué paradigma de programación utiliza principalmente?**  
   NestJS es un framework para construir aplicaciones del lado del servidor en Node.js, basado en TypeScript. Utiliza principalmente el paradigma de programación orientada a objetos y conceptos de arquitectura modular, inspirados en Angular. Combina elementos de programación funcional y reactiva para manejar solicitudes HTTP.

2. **¿Cuál es la función del CLI de NestJS (`@nestjs/cli`) en el desarrollo de aplicaciones?**  
   El CLI de NestJS es una herramienta que automatiza tareas como la creación de proyectos, módulos, controladores y servicios. Facilita la generación de código boilerplate con comandos como `nest new` o `nest generate`. También soporta compilación y ejecución de aplicaciones.

3. **¿Qué son los módulos en NestJS y por qué son importantes?**  
   Los módulos en NestJS son unidades organizativas que agrupan controladores, servicios y otros componentes relacionados. Son importantes porque promueven la modularidad, facilitan la escalabilidad y permiten una estructura clara. Cada módulo se define con el decorador `@Module()`.

4. **Explica la diferencia entre un controlador (`Controller`) y un servicio (`Service`) en NestJS.**  
   Un controlador (`Controller`) maneja las solicitudes HTTP, define rutas y delega la lógica a los servicios. Un servicio (`Service`) contiene la lógica de negocio, como operaciones con la base de datos, y es reutilizable. Por ejemplo, en el ejercicio, `UserController` maneja rutas como `/users`, mientras que `UserService` interactúa con Prisma.

5. **¿Qué es el archivo `app.module.ts` y qué contiene típicamente?**  
   El archivo `app.module.ts` es el módulo raíz de una aplicación NestJS. Típicamente contiene el decorador `@Module()` que define los imports (otros módulos), controladores, proveedores (como servicios) y exportaciones. En el ejercicio, incluye `UserModule` y `PrismaService`.

6. **¿Cómo se puede configurar un puerto diferente para una aplicación NestJS?**  
   Para cambiar el puerto, se modifica el método `listen` en `main.ts`. Por ejemplo: `app.listen(3001)` cambia el puerto a 3001. También se puede usar una variable de entorno con `@nestjs/config`.

### Conceptos de Prisma
7. **¿Qué es Prisma y qué rol cumple en una aplicación con base de datos?**  
   Prisma es un ORM (Object-Relational Mapping) que simplifica la interacción con bases de datos. Proporciona un cliente tipado para realizar consultas y administrar esquemas. En el ejercicio, Prisma conecta NestJS con MySQL para operaciones CRUD.

8. **¿Qué es el archivo `schema.prisma` y qué secciones principales contiene?**  
   El archivo `schema.prisma` define el esquema de la base de datos. Contiene secciones como `datasource` (configuración de la base de datos), `generator` (configuración del cliente Prisma) y modelos (definiciones de tablas). En el ejercicio, incluye el modelo `User`.

9. **Explica el propósito del generador (`generator`) en el archivo `schema.prisma`.**  
   El generador en `schema.prisma` configura cómo se genera el cliente de Prisma. Especifica el proveedor (`prisma-client-js`) y opciones como la ubicación del código generado. En el ejercicio, genera el cliente para interactuar con MySQL.

10. **¿Qué hace el comando `npx prisma migrate dev` y cuándo se utiliza?**  
   El comando `npx prisma migrate dev` crea y aplica migraciones a la base de datos basadas en los cambios en `schema.prisma`. Sincroniza el esquema con la base de datos y genera el cliente Prisma. Se usa durante el desarrollo, como en el ejercicio para crear la tabla `User`.

11. **¿Qué es el cliente de Prisma y cómo se integra en una aplicación NestJS?**  
   El cliente de Prisma es una biblioteca generada que proporciona métodos tipados para interactuar con la base de datos. En NestJS, se integra mediante un servicio como `PrismaService`, que se inyecta en otros servicios o controladores, como en el ejercicio con `UserService`.

12. **¿Cómo se define un modelo en Prisma? Proporciona un ejemplo simple.**  
   Un modelo en Prisma se define en `schema.prisma` con campos, tipos y atributos. Ejemplo:  
   ```prisma
   model User {
     id    Int     @id @default(autoincrement())
     email String  @unique
     name  String?
   }
   ```
   Esto crea una tabla `User` con columnas `id`, `email` y `name`.

### Conceptos de MySQL
13. **¿Qué es MySQL y qué tipo de base de datos es?**  
   MySQL es un sistema de gestión de bases de datos relacional (RDBMS) de código abierto. Almacena datos en tablas con relaciones definidas por claves primarias y foráneas. En el ejercicio, se usa para almacenar datos de usuarios.

14. **¿Cómo se configura la conexión a una base de datos MySQL en Prisma?**  
   La conexión se configura en `schema.prisma` con la sección `datasource` y la variable `DATABASE_URL` en `.env`. Ejemplo: `DATABASE_URL="mysql://user:password@localhost:3306/db"`. En el ejercicio, se conecta a `nest_prisma_db`.

15. **¿Qué es una migración en el contexto de bases de datos y cómo la maneja Prisma?**  
   Una migración es el proceso de aplicar cambios al esquema de la base de datos, como crear tablas. Prisma genera scripts SQL basados en `schema.prisma` y los aplica con `prisma migrate dev`. En el ejercicio, crea la tabla `User`.

16. **¿Qué representa la variable `DATABASE_URL` en el archivo `.env`?**  
   La variable `DATABASE_URL` especifica los parámetros de conexión a la base de datos, incluyendo el protocolo, usuario, contraseña, host, puerto y nombre de la base de datos. En el ejercicio, es `mysql://usuario:contraseña@localhost:3306/nest_prisma_db`. Prisma la usa para conectar con MySQL.

