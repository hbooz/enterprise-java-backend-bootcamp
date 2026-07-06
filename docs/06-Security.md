# Módulo 6 - Spring Security + JWT Profesional

## Objetivo

Aprender a proteger APIs REST mediante autenticación y autorización utilizando Spring Security y JWT.

---

# Tecnologías

- Spring Security
- JWT
- BCrypt
- Spring Validation
- Spring Boot 3

---

# Conceptos

- Authentication
- Authorization
- Roles
- Permissions
- JWT
- Refresh Token
- BCrypt
- SecurityFilterChain
- UserDetailsService

---

# Flujo

```text
Cliente

↓

Login

↓

JWT

↓

API Gateway

↓

Microservicio

↓

Respuesta
```

---

# Dependencias

```xml
spring-boot-starter-security

jjwt-api

jjwt-impl

jjwt-jackson
```

---

# Configuración

```java
@Configuration
@EnableWebSecurity
public class SecurityConfig {

}
```

---

# Password Encoder

```java
@Bean
PasswordEncoder passwordEncoder(){

    return new BCryptPasswordEncoder();

}
```

---

# UserDetailsService

```java
@Service
public class CustomUserDetailsService
implements UserDetailsService{

}
```

---

# JWT

Generar Token

Validar Token

Extraer Usuario

Extraer Roles

Controlar Expiración

---

# SecurityFilterChain

```java
@Bean
SecurityFilterChain securityFilterChain(
HttpSecurity http)
throws Exception{

}
```

---

# Roles

```text
ROLE_ADMIN

ROLE_CLIENTE

ROLE_EMPLEADO
```

---

# Endpoints Públicos

```text
POST /auth/login

POST /auth/register

/swagger-ui/**

/v3/api-docs/**
```

---

# Endpoints Privados

```text
/clientes/**

/cuentas/**

/transacciones/**
```

---

# Autenticación

```text
Usuario

↓

Password

↓

JWT

↓

Respuesta
```

---

# BCrypt

Nunca guardar contraseñas en texto plano.

```java
passwordEncoder.encode(password);
```

---

# Filtro JWT

Responsabilidades

- Leer Token.
- Validar Token.
- Cargar Usuario.
- Autorizar petición.

---

# Refresh Token

Permitir renovar el JWT sin volver a iniciar sesión.

---

# Manejo de Errores

401 Unauthorized

403 Forbidden

404 Not Found

400 Bad Request

---

# Proyecto Bancario

Implementar

```text
ms-auth
```

Endpoints

```text
POST /login

POST /register

POST /refresh-token
```

---

# Buenas Prácticas

- BCrypt.
- JWT corto.
- Refresh Token.
- Roles.
- Permisos.
- No guardar secretos en código.
- Variables de entorno.

---

# Mini Retos

- Login.
- Registro.
- Refresh Token.
- Roles.
- Permisos.
- Endpoint protegido.

---

# Preguntas de Entrevista

- ¿Qué es Spring Security?
- ¿Qué es JWT?
- ¿Qué diferencia existe entre Authentication y Authorization?
- ¿Qué hace BCrypt?
- ¿Qué hace SecurityFilterChain?
- ¿Qué hace UserDetailsService?
- ¿Qué es Refresh Token?
- ¿Qué es CORS?
- ¿Qué es CSRF?

---

# Checklist

- [ ] Login.
- [ ] Registro.
- [ ] JWT.
- [ ] BCrypt.
- [ ] Roles.
- [ ] Permisos.
- [ ] Endpoints protegidos.
- [ ] Swagger accesible.

---

# Próximo Módulo

## Docker Profesional