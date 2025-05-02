

# Estructura del Curso: Desarrollo de APIs REST con Node.js
**Duración total**: 10 clases de 6 horas (60 horas)  
**Objetivo**: Capacitar a los estudiantes en el diseño, desarrollo, testing y despliegue de APIs RESTful utilizando Node.js, Express y mejores prácticas.  
**Nivel**: Intermedio (se asume conocimiento básico de JavaScript y programación).  
**Metodología**: Teoría (30%), práctica (60%), ejercicios y proyecto final (10%).  

---

## Clase 1: Introducción a Node.js y APIs REST
**Duración**: 6 horas  
**Objetivos**: Comprender los fundamentos de Node.js, el modelo cliente-servidor y el concepto de APIs REST.  
**Contenido**:  
- Introducción a Node.js: características, arquitectura y casos de uso.  
- Instalación y configuración del entorno (Node.js, npm, VS Code).  
- Conceptos de APIs REST: métodos HTTP, códigos de estado, JSON.  
- Creación de un servidor básico con Node.js puro.  
- Introducción a Express.js: instalación y primer endpoint.  
**Práctica**:  
- Configurar entorno de desarrollo.  
- Crear un servidor con Node.js puro y Express que responda "Hola, mundo" en `/`.  
**Recursos**: Node.js oficial, documentación de Express, Postman.  

---

## Clase 2: Fundamentos de Express.js y Rutas
**Duración**: 6 horas  
**Objetivos**: Dominar el manejo de rutas y middlewares en Express.js.  
**Contenido**:  
- Estructura de un proyecto con Express.  
- Definición de rutas: GET, POST, PUT, DELETE.  
- Middlewares: concepto, creación y uso (logging, autenticación básica).  
- Manejo de parámetros y query strings.  
- Respuestas HTTP: JSON, códigos de estado.  
**Práctica**:  
- Crear una API con rutas para gestionar una lista de usuarios (sin base de datos).  
- Implementar un middleware para logging de solicitudes.  
**Recursos**: Documentación de Express, ejemplos de middlewares.  

---

## Clase 3: Conexión con Bases de Datos (MongoDB)
**Duración**: 6 horas  
**Objetivos**: Integrar MongoDB con Node.js para persistencia de datos.  
**Contenido**:  
- Introducción a bases de datos NoSQL y MongoDB.  
- Instalación y configuración de MongoDB (local o Atlas).  
- Uso de Mongoose: conexión, modelos y esquemas.  
- CRUD básico: crear, leer, actualizar y eliminar documentos.  
- Manejo de errores en operaciones de base de datos.  
**Práctica**:  
- Configurar MongoDB Atlas y conectar con Mongoose.  
- Crear un modelo de "Producto" y endpoints CRUD.  
**Recursos**: MongoDB Atlas, documentación de Mongoose.  

---

## Clase 4: Validación y Manejo de Errores
**Duración**: 6 horas  
**Objetivos**: Implementar validaciones robustas y manejar errores en la API.  
**Contenido**:  
- Validación de datos con Joi o Express Validator.  
- Creación de middlewares para validación.  
- Estructuración de respuestas de error consistentes.  
- Manejo de excepciones globales.  
- Introducción a logging avanzado (Winston o Morgan).  
**Práctica**:  
- Agregar validación a los endpoints CRUD de productos.  
- Implementar un middleware de manejo de errores global.  
**Recursos**: Documentación de Joi, Winston, ejemplos de logging.  

---

## Clase 5: Autenticación y Autorización
**Duración**: 6 horas  
**Objetivos**: Implementar autenticación basada en JWT y autorización basada en roles.  
**Contenido**:  
- Introducción a autenticación: tokens, sesiones, OAuth.  
- JSON Web Tokens (JWT): generación y verificación.  
- Middleware de autenticación.  
- Autorización basada en roles (admin, usuario).  
- Seguridad básica: protección contra ataques comunes (XSS, CSRF).  
**Práctica**:  
- Crear endpoints de registro y login con JWT.  
- Proteger rutas con middleware de autenticación y roles.  
**Recursos**: Documentación de jsonwebtoken, OWASP.  

---

## Clase 6: Relaciones y Consultas Avanzadas
**Duración**: 6 horas  
**Objetivos**: Manejar relaciones entre modelos y optimizar consultas.  
**Contenido**:  
- Relaciones en MongoDB: referencias y documentos embebidos.  
- Consultas avanzadas con Mongoose: agregaciones, filtros, paginación.  
- Optimización de rendimiento: índices, caching básico.  
- Introducción a population en Mongoose.  
**Práctica**:  
- Crear un modelo de "Pedidos" con relación a "Productos".  
- Implementar endpoints con paginación y filtros.  
**Recursos**: Documentación de Mongoose (agregaciones, population).  

---

## Clase 7: Testing de APIs
**Duración**: 6 horas  
**Objetivos**: Aprender a escribir pruebas unitarias e integrales para APIs.  
**Contenido**:  
- Introducción al testing: unitario, integración, end-to-end.  
- Configuración de Jest y Supertest.  
- Escritura de pruebas para endpoints CRUD.  
- Mocking de bases de datos y servicios externos.  
- Generación de reportes de cobertura.  
**Práctica**:  
- Escribir pruebas unitarias para un controlador de productos.  
- Escribir pruebas de integración para endpoints autenticados.  
**Recursos**: Documentación de Jest, Supertest.  

---

## Clase 8: Documentación y Versionado
**Duración**: 6 horas  
**Objetivos**: Documentar la API y gestionar versiones.  
**Contenido**:  
- Importancia de la documentación en APIs.  
- Uso de Swagger/OpenAPI para documentar endpoints.  
- Configuración de Swagger UI en Express.  
- Estrategias de versionado: URI, headers.  
- Introducción a buenas prácticas (CORS, rate limiting).  
**Práctica**:  
- Documentar la API de productos con Swagger.  
- Implementar versionado en un endpoint.  
**Recursos**: Swagger UI, OpenAPI Specification.  

---

## Clase 9: Despliegue y Escalabilidad
**Duración**: 6 horas  
**Objetivos**: Desplegar la API en producción y entender conceptos de escalabilidad.  
**Contenido**:  
- Preparación para producción: variables de entorno, seguridad.  
- Despliegue en plataformas como Render, Heroku o Vercel.  
- Configuración de CI/CD básico con GitHub Actions.  
- Introducción a escalabilidad: clustering, PM2, balanceo de carga.  
- Monitoreo básico con herramientas como New Relic.  
**Práctica**:  
- Desplegar la API en Render.  
- Configurar variables de entorno y CI/CD.  
**Recursos**: Documentación de Render, PM2, GitHub Actions.  

---

## Clase 10: Proyecto Final y Cierre
**Duración**: 6 horas  
**Objetivos**: Aplicar todo lo aprendido en un proyecto final y cerrar el curso.  
**Contenido**:  
- Revisión de conceptos clave del curso.  
- Desarrollo guiado de un proyecto final: API completa (e.g., sistema de gestión de tareas).  
- Presentación de proyectos por parte de los estudiantes.  
- Discusión sobre siguientes pasos: microservicios, GraphQL, TypeScript.  
- Entrega de certificados y feedback.  
**Práctica**:  
- Completar una API con autenticación, CRUD, documentación y despliegue.  
- Presentar el proyecto al grupo.  
**Recursos**: Repositorio del proyecto, ejemplos de APIs completas.  

---

## Evaluación
- **Participación y ejercicios**: 30%  
- **Proyecto final**: 50%  
- **Pruebas y documentación**: 20%  

## Requisitos Previos
- Conocimiento básico de JavaScript (ES6+).  
- Familiaridad con la línea de comandos y Git.  
- Computadora con Node.js y MongoDB instalados.  

## Material Adicional
- Repositorio GitHub con ejemplos y ejercicios.  
- Lista de lecturas recomendadas: "Node.js Design Patterns", "RESTful API Design".  
- Acceso a comunidad en Discord/Slack para soporte.  

