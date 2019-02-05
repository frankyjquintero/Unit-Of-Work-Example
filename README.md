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


# Resumen
* La ventajas que yo encuentro particularmente de trabajar con estos 3 patrones es la siguiente:

* Nuestra capa Services encapsula toda la lógica, de esta manera evitamos tener el código acumulado directamente en nuestro controlador o capa cliente.
* UnitOfWork nos permite manipular mejor las conexiones a la base de datos y realizar cambios o saveChanges() cuando yo lo especifique.
* El uso del patrón Repository brinda la facilidad de reutilizar lógica. Por ejemplo, si quiero validar que un usuario existe en la Db y no tuvieramos esta capa tendría que duplicar el código por cada Service que lo vaya a utilizar. En cambio, al tenerlo este patrón implementado es más sencillo llamar desde cualquier servicio llamar a dicho método y si hacemos un cambio de este se actualizará para todos automáticamente (porque es una sola llamada). Eliminamos código repetitivo.
No todo es bonito, las desventajas que encuentro son:

* Mayor inversión de código, pero luego todo es reutilizable.
* Algunos queries muy pesados pueden ser jodidos de implementar. Por ejemplo, si quisiera un INNER JOIN de varias tablas para retornar un query con campos que no hacen referencia a una entidad, lo que estoy haciendo es crear una clase personalizada llamada por ejemplo UserReportAggregate y esta solo existiría desde el repositorio.
* Al quitar el acceso directo al DbContext vamos a tener que seguir optimizando nuestro repositorio genérico.

### Link
http://anexsoft.com/p/201/implementacion-de-unit-of-work-services-y-repository-con-net-core-2-2



