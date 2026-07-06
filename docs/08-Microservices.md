# Módulo 8 - Microservicios

## Objetivo

Aprender a diseñar, desarrollar y desplegar una arquitectura de microservicios utilizando Spring Cloud.

## Temas

- Arquitectura de Microservicios
- Monolito vs Microservicios
- Domain Driven Design (DDD) básico
- Eureka Server
- Config Server
- API Gateway
- OpenFeign
- Resilience4j
- Circuit Breaker
- Retry
- Timeout
- Comunicación síncrona
- Comunicación asíncrona
- Trazabilidad
- Centralización de configuración

## Proyecto

Sistema bancario compuesto por:

- discovery-server
- config-server
- api-gateway
- ms-auth
- ms-clientes
- ms-cuentas
- ms-transacciones
- ms-notificaciones

## Reglas

- Un microservicio = una responsabilidad.
- No compartir entidades entre microservicios.
- Comunicar mediante DTOs.
- Manejar errores entre servicios.
- Implementar resiliencia.
- Registrar logs correctamente.
- Preparar la aplicación para escalar horizontalmente.

## Al finalizar

El estudiante será capaz de construir un sistema basado en microservicios con Spring Cloud siguiendo buenas prácticas empresariales.