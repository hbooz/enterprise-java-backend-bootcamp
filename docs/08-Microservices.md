# Módulo 8 - Microservicios con Spring Cloud

## Objetivo

Aprender a construir una arquitectura de microservicios profesional utilizando Spring Cloud.

---

# Tecnologías

- Spring Cloud
- Eureka Server
- Config Server
- API Gateway
- OpenFeign
- Resilience4j
- Docker
- MySQL

---

# Arquitectura

```text
                    Cliente

                       │

                 API Gateway

                       │

     ┌─────────────────┼─────────────────┐

     │                 │                 │

 ms-clientes     ms-cuentas     ms-transacciones

     │                 │                 │

     └─────────────────┼─────────────────┘

                Eureka Server

                     │

              Config Server

                     │

                   MySQL
```

---

# Microservicios

```text
config-server

discovery-server

api-gateway

ms-auth

ms-clientes

ms-cuentas

ms-transacciones

ms-notificaciones
```

---

# Eureka Server

Registrar servicios.

```java
@EnableEurekaServer
@SpringBootApplication
public class DiscoveryServerApplication {

}
```

---

# Cliente Eureka

```yaml
eureka:

  client:

    service-url:

      defaultZone:

        http://localhost:8761/eureka
```

---

# Config Server

```java
@EnableConfigServer
@SpringBootApplication
public class ConfigServerApplication {

}
```

---

# API Gateway

Dependencia

```xml
spring-cloud-starter-gateway
```

---

# Gateway

```yaml
spring:

  cloud:

    gateway:

      routes:

        - id: ms-clientes

          uri: lb://MS-CLIENTES

          predicates:

            - Path=/clientes/**
```

---

# OpenFeign

Dependencia

```xml
spring-cloud-starter-openfeign
```

---

# Cliente Feign

```java
@FeignClient(name="MS-CUENTAS")
public interface CuentaClient {

}
```

---

# Circuit Breaker

Utilizar

```text
Resilience4j
```

---

# Retry

```yaml
resilience4j:

  retry:
```

---

# Timeout

```yaml
resilience4j:

  timelimiter:
```

---

# Balanceo

```text
Spring Cloud LoadBalancer
```

---

# Configuración Centralizada

Repositorio Git

↓

Config Server

↓

Microservicios

---

# Comunicación

Sincrónica

```text
REST

OpenFeign
```

Asincrónica

```text
RabbitMQ

Kafka
```

---

# Logs

Utilizar

```text
Spring Boot Actuator

Micrometer
```

---

# Health Check

```text
/actuator/health
```

---

# Buenas Prácticas

- Una base de datos por microservicio.
- No compartir entidades.
- Compartir únicamente DTOs.
- Comunicación mediante API.
- Configuración centralizada.
- Tolerancia a fallos.
- Logging centralizado.
- Versionado de APIs.

---

# Proyecto Bancario

Implementar

- discovery-server
- config-server
- api-gateway
- ms-auth
- ms-clientes
- ms-cuentas
- ms-transacciones
- ms-notificaciones

---

# Mini Retos

- Registrar un microservicio.
- Configurar Gateway.
- Consumir otro servicio mediante Feign.
- Implementar Circuit Breaker.
- Implementar Retry.

---

# Preguntas de Entrevista

- ¿Qué es un microservicio?
- ¿Qué ventajas ofrece Spring Cloud?
- ¿Qué hace Eureka?
- ¿Qué hace Config Server?
- ¿Qué hace API Gateway?
- ¿Qué es OpenFeign?
- ¿Qué es Circuit Breaker?
- ¿Qué es Resilience4j?
- ¿Qué ventajas ofrece una arquitectura distribuida?

---

# Checklist

- [ ] Eureka funcionando.
- [ ] Config Server funcionando.
- [ ] Gateway funcionando.
- [ ] Feign funcionando.
- [ ] Circuit Breaker implementado.
- [ ] Retry implementado.
- [ ] Health Checks funcionando.
- [ ] Docker Compose funcionando.

---

# Próximo Módulo

## Git + GitHub + GitFlow Profesional