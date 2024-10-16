# Expense Tracker Backend - Spring Boot

Este proyecto es la parte **backend** del Expense Tracker, construido con **Spring Boot**. Este backend proporciona una API REST que permite al frontend gestionar transacciones financieras (ingresos y gastos) de manera sencilla y persistente.

## Características
- **API REST**: Permite crear, listar y eliminar transacciones.
- **Base de Datos Persistente**: Usa **MySQL** para almacenar las transacciones de ingresos y gastos.
- **Conexión con Frontend**: Diseñado para integrarse con un frontend de Vue.js.

## Requisitos Previos

Antes de comenzar, asegúrate de tener instalados los siguientes componentes:
- **Java JDK 17** o superior
- **Maven** para gestionar las dependencias del proyecto
- **MySQL** para la base de datos
- **Postman** (opcional, para probar los endpoints de la API)

## Instalación

1. Clona el repositorio del backend:

   ```bash
   git clone <URL_DEL_REPOSITORIO>
   cd expense-tracker-backend
   ```

2. Configura la base de datos en MySQL:

    - Crea una base de datos llamada `expensetracker`:
      ```sql
      CREATE DATABASE expensetracker;
      ```

3. Configura las credenciales de acceso a la base de datos en el archivo **application.properties**:

   ```properties
   spring.datasource.url=jdbc:mysql://localhost:3306/expensetracker?useSSL=false&serverTimezone=UTC
   spring.datasource.username=tu_usuario_mysql
   spring.datasource.password=tu_contraseña_mysql
   spring.jpa.hibernate.ddl-auto=update
   spring.jpa.database-platform=org.hibernate.dialect.MySQLDialect
   spring.jpa.show-sql=true
   ```

4. Instala las dependencias necesarias y ejecuta el proyecto:

   ```bash
   ./mvnw spring-boot:run
   ```

   Esto iniciará el backend en `http://localhost:8080`.

## Endpoints de la API

El backend expone varios **endpoints REST** para gestionar las transacciones:

- `GET /api/transactions`: Obtiene todas las transacciones.
- `POST /api/transactions`: Crea una nueva transacción.
- `DELETE /api/transactions/{id}`: Elimina una transacción por su ID.

### Ejemplo de Uso con Postman

1. **Obtener Todas las Transacciones**:
    - Método: `GET`
    - URL: `http://localhost:8080/api/transactions`

2. **Agregar una Nueva Transacción**:
    - Método: `POST`
    - URL: `http://localhost:8080/api/transactions`
    - Body (JSON):
      ```json
      {
        "text": "Salary",
        "amount": 5000
      }
      ```

3. **Eliminar una Transacción**:
    - Método: `DELETE`
    - URL: `http://localhost:8080/api/transactions/{id}`

## Estructura del Proyecto

```
expense-tracker-backend/
 ├── src/
 │    ├── main/
 │    │    ├── java/com/example/expensetracker/
 │    │    │    ├── controller/TransactionController.java   # Controlador REST
 │    │    │    ├── model/Transaction.java                  # Entidad JPA
 │    │    │    ├── repository/TransactionRepository.java   # Repositorio JPA
 │    │    │    └── service/TransactionService.java         # Lógica de negocio
 │    │    └── resources/
 │    │         └── application.properties                  # Configuración de la aplicación
 └── pom.xml                                                 # Configuración del proyecto y dependencias
```

### Explicación de Cada Archivo

1. **TransactionController.java**: Define los endpoints REST para gestionar las transacciones.
2. **Transaction.java**: Entidad que representa una transacción en la base de datos, ya sea un ingreso o un gasto.
3. **TransactionRepository.java**: Interfaz que extiende `JpaRepository` para proporcionar métodos de acceso a la base de datos.
4. **TransactionService.java**: Implementa la lógica de negocio para crear, obtener y eliminar transacciones.
5. **application.properties**: Contiene la configuración para conectar con la base de datos MySQL.

## Despliegue

Cuando estés listo para desplegar tu aplicación en un entorno de producción:

1. Empaqueta el proyecto como un archivo JAR ejecutable:
   ```bash
   ./mvnw clean package
   ```

2. Encuentra el archivo `.jar` generado en la carpeta `target/` y ejecútalo:
   ```bash
   java -jar target/GestorGastos-0.0.1-SNAPSHOT.jar
   ```

3. Asegúrate de que las configuraciones de la base de datos sean correctas y estén seguras para producción.

## Dependencias Clave

- **Spring Boot Starter Web**: Proporciona herramientas para crear la API REST.
- **Spring Boot Starter Data JPA**: Facilita la interacción con la base de datos.
- **MySQL Connector**: Controlador para conectarse a la base de datos MySQL.
- **Lombok**: Ayuda a reducir el código repetitivo en las clases Java.

## Errores Comunes

1. **Error de Conexión a la Base de Datos**: Asegúrate de que el servidor MySQL está corriendo y que las credenciales en `application.properties` son correctas.

2. **CORS**: Si tienes problemas con el frontend al hacer solicitudes, asegúrate de que CORS esté configurado para permitir solicitudes desde `http://localhost:5173`.

## Créditos

Este proyecto fue construido como ejemplo de una aplicación **full stack** utilizando **Spring Boot** para el backend y **Vue.js** para el frontend.

## Licencia

MIT License

