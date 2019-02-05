# Unit Of Work, Services y Repository Pattern usando Net Core 2.0
En el siguiente repositorio usted encontrará un ejemplo de dichos patrones sobre una arquitectura que vengo usando en proyectos reales.

### ¿Cómo levantar el proyecto?
* La cadena de conexión por ahora se encuentra en el ApplicationDbContext debido a que el proyecto es consola.
* Luego de cambiar la cadena de conexión corran la migración de ejemplo:
	* Situarse en el proyecto de \src\UnitOfWorkPersistence y desde la consola correr: 
	### dotnet ef database update
* Pueden hacer pruebas con los métodos que hay en el program.cs
* No se olviden usar Net Core 2.2


# Patrones a usar
En la entrada anterior sobre UoW prometimos crear otra publicación usando más patrones, patrones que yo creo que quedan de lujo como complemento a este, ahora lo haremos mediante el repository pattern.

### Services Pattern:
Nos permite organizar la lógica de nuestro negocio. Anteriormente, las consultas a la DB la armabamos en esta capa pero con este patrón de UnitOfWork lo que vamos a usar ahora son repositorios.
### Repository Pattern: 
nos permite manipular el acceso a la base de datos; es decir, mediante este podemos realizar las consultas a la DB.
En el repositorio de GitHub he adjuntado un patrón repositorio genérico porque sino, nos queda chico o nos da la sensación que falta más para poder hacer consultas a la DB. De todas formas, esta clase del patrón genérico ha sido adaptado para un proyecto mío, por lo cual en tu proyecto deberías modificarlo, expandirlo.
### UnitOfWork Pattern:
Centraliza las conexiones a la base de datos y gestiona los cambios (context.SaveChanges();).
# Distribución de capas
### Clients:
Implementación de nuestros clientes. Para nuestro ejemplo usamos un proyecto consola.
### Services:
Manipulación de los repositorios. Encapsulamos la lógica de las llamadas a los repositorios mediante un Services Layer, porque de esta manera evitamos que llamen a los repositorios directamente desde el controlador. Asimismo, podemos usar más de una lógica del repositorio desde un solo método de nuestro Services Layer.
Persistence
### UnitOfWork: 
Código del patrón UnitOfWork
### Persistence:
Migraciones, instancia de la base de datos.
### Repository: 
Los repositorios a crear. Es un repositorio por modelo, por ejemplo UserRepository (referencia a tu tabla Usuario).

### Link
http://anexsoft.com/p/201/implementacion-de-unit-of-work-services-y-repository-con-net-core-2-2



