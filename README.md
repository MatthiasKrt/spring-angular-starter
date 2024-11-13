# Spring-Angular Containerized Starter

This project provides a foundation for building Spring Boot and Angular applications, designed to be containerized using Docker.

## Backend

The `spring-boot-starter-web` dependency has been added, and a sample endpoint has been created. All endpoints are available under `/api`.

### Additional Dependencies:

Expand the application with further Dependencies in the `pom.xml`. For example the following:

- `spring-boot-starter-data-jpa` for database integration.
- `spring-boot-starter-security` for security and authentication.

## Frontend

The Angular frontend is generated in the `src/main` directory using the following command:

```bash
ng new frontend
```

After generating the Angular project, edit the `angular.json` file as follows:

```json
{
  "projects": {
    "frontend": {
      "architect": {
        "build": {
          "options": {
            "baseHref": "/",
            "outputPath": {
              "base": "../resources/static",
              "browser": ""
            }
          }
        }
      }
    }
  }
}
```

This ensures that the Angular build outputs to `src/main/resources/static`, making the app available to Spring Boot.

## Containerization

The container is built using the `jib-maven-plugin`, with `eclipse-temurin:21` (JDK 21) as the base image.

### Steps to build the container:

1. Build the Docker image:

   ```bash
   mvn clean compile jib:buildTar
   ```

2. Load the image into Docker:

   ```bash
   docker load -i target/jib-image.tar
   ```

3. Run the image (Replace the image name):

   ```bash
   docker run -p 8080:8080 matthiaskrt/spring-angular-starter
   ```