# Spring Angular App

Dieses Projekt bietet die Grundlage für Spring-Angular Anwendungen, die als Container bereitgestellt werden sollen.

## Backend

Es wurde die Abhängigkeit `spring-boot-starter-web` hinzugefügt und damit ein Beispielendpunkt erstellt. Alle Endpunkte sind unter `/api` erreichbar.

## Frontend

Das Frontend wird im Verzeichnis `src/main` mit dem Befehl `ng new frontend` generiert.

Anschließend wird die Datei `angular.json` bearbeitet:

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

## Container

Der Container wird mit dem `jib-maven-plugin` erstellt. Als Image wird `eclipse-temurin:21` verwendet.

Zum bauen des Images wird der folgende Befehl ausgeführt: `mvn clean compile jib:buildTar`.

Anschließend kann das Image lokal in Docker geladen werden: `docker load -i target/jib-image.tar`.