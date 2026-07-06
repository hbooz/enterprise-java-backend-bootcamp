# Módulo 7 - Docker Profesional

## Objetivo

Aprender a contenerizar aplicaciones Spring Boot y desplegar una arquitectura de microservicios utilizando Docker y Docker Compose.

---

# Tecnologías

- Docker
- Docker Compose
- Docker Hub
- OpenJDK 21
- MySQL
- Spring Boot

---

# Conceptos

- Imagen
- Contenedor
- Dockerfile
- Docker Compose
- Volumen
- Red
- Variables de entorno
- Multi-stage Build

---

# Instalación

Verificar instalación

```bash
docker --version

docker compose version
```

---

# Dockerfile

```dockerfile
FROM eclipse-temurin:21-jdk

WORKDIR /app

COPY target/ms-clientes.jar app.jar

EXPOSE 8080

ENTRYPOINT ["java","-jar","app.jar"]
```

---

# Construir Imagen

```bash
docker build -t ms-clientes .
```

---

# Ejecutar Contenedor

```bash
docker run -p 8080:8080 ms-clientes
```

---

# Listar Contenedores

```bash
docker ps
```

---

# Detener Contenedor

```bash
docker stop ID_CONTENEDOR
```

---

# Eliminar Contenedor

```bash
docker rm ID_CONTENEDOR
```

---

# Eliminar Imagen

```bash
docker rmi ms-clientes
```

---

# Docker Compose

```yaml
version: "3.9"

services:

  mysql:

    image: mysql:8

    environment:

      MYSQL_DATABASE: banco

      MYSQL_ROOT_PASSWORD: root

    ports:

      - "3306:3306"

  ms-clientes:

    build: .

    ports:

      - "8081:8080"

    depends_on:

      - mysql
```

---

# Ejecutar Compose

```bash
docker compose up
```

Segundo plano

```bash
docker compose up -d
```

---

# Detener Compose

```bash
docker compose down
```

---

# Volúmenes

```yaml
volumes:

  mysql_data:
```

---

# Redes

```yaml
networks:

  backend:
```

---

# Variables de Entorno

```yaml
environment:

  SPRING_DATASOURCE_URL:

  SPRING_DATASOURCE_USERNAME:

  SPRING_DATASOURCE_PASSWORD:
```

---

# Multi Stage Build

```dockerfile
FROM maven:3.9.9-eclipse-temurin-21 AS build

WORKDIR /build

COPY . .

RUN mvn clean package -DskipTests

FROM eclipse-temurin:21-jre

COPY --from=build /build/target/*.jar app.jar

ENTRYPOINT ["java","-jar","app.jar"]
```

---

# Proyecto Bancario

Dockerizar

```text
config-server

discovery-server

api-gateway

ms-auth

ms-clientes

ms-cuentas

ms-transacciones

mysql
```

---

# Buenas Prácticas

- Una imagen por microservicio.
- No almacenar secretos en imágenes.
- Utilizar variables de entorno.
- Utilizar Multi-stage Build.
- Utilizar Docker Compose para desarrollo.
- Mantener imágenes pequeñas.

---

# Mini Retos

- Dockerizar ms-clientes.
- Dockerizar MySQL.
- Crear Docker Compose.
- Levantar ambos servicios.
- Agregar variables de entorno.

---

# Preguntas de Entrevista

- ¿Qué es Docker?
- ¿Qué diferencia existe entre imagen y contenedor?
- ¿Qué hace Docker Compose?
- ¿Qué es un volumen?
- ¿Qué es una red Docker?
- ¿Qué ventajas ofrece Multi-stage Build?
- ¿Cómo comunicarías dos contenedores?

---

# Checklist

- [ ] Docker instalado.
- [ ] Dockerfile creado.
- [ ] Imagen construida.
- [ ] Contenedor ejecutándose.
- [ ] Docker Compose funcionando.
- [ ] MySQL conectado.
- [ ] Variables de entorno configuradas.

---

# Próximo Módulo

## Microservicios con Spring Cloud