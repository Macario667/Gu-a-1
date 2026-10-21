# getting-started

Proyecto inicial de Quarkus para practicar la estructura mínima de una aplicación, un endpoint REST y la inyección de un servicio CDI.

## Guías adaptadas

- [Creating Your First Application](https://quarkus.io/guides/getting-started): el proyecto Maven, el modo de desarrollo y la primera aplicación ejecutable.
- [Writing REST Services with RESTEasy Reactive](https://quarkus.io/guides/rest): `GreetingResource` declara rutas con `@Path`, atiende `GET` y produce texto plano.

El `pom.xml` usa `quarkus-rest` y `quarkus-arc`. Por eso el ejemplo es Quarkus REST (la implementación moderna), no RESTEasy Classic. Este proyecto no transforma objetos JSON: las respuestas del saludo son `text/plain`.

## Cómo se aplica

- `GreetingResource` expone `GET /hello` y `GET /hello/greeting/{name}`.
- `@Inject` obtiene `GreetingService`, un bean CDI con ámbito `@ApplicationScoped`.
- `GreetingService` contiene la lógica del saludo y devuelve `hello {name}`.
- Las pruebas de `GreetingResourceTest` comprueban ambos endpoints.

## Ejecutar y probar

Requiere una versión de Java compatible con `maven.compiler.release` del `pom.xml` (17).

```powershell
.\mvnw.cmd quarkus:dev
```

En otra terminal:

```powershell
curl.exe http://localhost:8080/hello
curl.exe http://localhost:8080/hello/greeting/Sam
```

Las respuestas esperadas son `Hello from Quarkus REST` y `hello Sam`. Para ejecutar las pruebas:

```powershell
.\mvnw.cmd test
```

## Ejercicio para explicarlo

1. Cambia el saludo en `GreetingService`.
2. Ejecuta la prueba `testGreetingEndpoint` y observa cómo llega el nombre desde la ruta.
3. Explica la separación: el recurso recibe la petición HTTP y el servicio realiza la operación.
4. Añade una prueba para otro nombre y verifica la respuesta.

## Relación con otras guías

[RESTEasy Classic](https://es.quarkus.io/guides/resteasy) no es la extensión de este proyecto; compárala con [Quarkus REST](https://quarkus.io/guides/rest) como alternativa de implementación. Las guías de configuración, logging, validación, OpenAPI y REST Client no están desarrolladas aquí.
