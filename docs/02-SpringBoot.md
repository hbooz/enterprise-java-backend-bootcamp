# Módulo 2 - Spring Boot Profesional

## Objetivo

Aprender a construir APIs REST profesionales utilizando Spring Boot siguiendo arquitectura limpia y buenas prácticas empresariales.

---

# Tecnologías

- Java 21
- Spring Boot 3
- Maven
- Spring Web
- Spring Validation
- Spring Data JPA
- Lombok
- MapStruct
- OpenAPI (Swagger)
- MySQL

---

# Proyecto

Durante este módulo construiremos el microservicio:

```text
ms-clientes
```

Arquitectura:

```text
Controller
        ↓
Service
        ↓
Repository
        ↓
MySQL
```

---

# Estructura del proyecto

```text
src
└── main
    ├── java
    │   └── com.bootcamp.clientes
    │       ├── config
    │       ├── controller
    │       ├── dto
    │       ├── entity
    │       ├── exception
    │       ├── mapper
    │       ├── repository
    │       ├── service
    │       └── util
    └── resources
        ├── application.yml
        └── data.sql
```

---

# Dependencias

Agregar:

```text
Spring Web

Spring Data JPA

Validation

MySQL Driver

Lombok

Spring Boot DevTools
```

---

# Arquitectura por capas

## Controller

Responsabilidades

- Recibir peticiones HTTP.
- Validar Request.
- Llamar al Service.
- Devolver Response.

Nunca contener lógica de negocio.

---

## Service

Responsabilidades

- Reglas del negocio.
- Validaciones.
- Coordinar Repository.

---

## Repository

Responsabilidades

- Acceso a base de datos.
- Consultas.
- Persistencia.

---

## Entity

Representa una tabla de la base de datos.

Nunca devolver Entity directamente desde un endpoint.

---

## DTO

Todo intercambio entre API y cliente debe realizarse mediante DTO.

Tipos:

```text
ClienteRequest

ClienteResponse

ClienteUpdateRequest
```

---

# Flujo de una petición

```text
Cliente

↓

Controller

↓

Service

↓

Repository

↓

MySQL

↓

Repository

↓

Service

↓

DTO

↓

Controller

↓

Cliente
```

---

# Primera Entity

```java
@Entity
@Table(name = "clientes")
public class Cliente {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String nombres;

    private String apellidos;

    private String dni;

    private String correo;

}
```

---

# Repository

```java
@Repository
public interface ClienteRepository
        extends JpaRepository<Cliente, Long> {

}
```

---

# Service

```java
public interface ClienteService {

    ClienteResponse crear(ClienteRequest request);

    List<ClienteResponse> listar();

    ClienteResponse obtener(Long id);

    ClienteResponse actualizar(Long id,
                               ClienteRequest request);

    void eliminar(Long id);

}
```

---

# Implementación

```java
@Service
@RequiredArgsConstructor
public class ClienteServiceImpl
        implements ClienteService {

    private final ClienteRepository repository;

}
```

---

# Controller

```java
@RestController
@RequestMapping("/api/clientes")
@RequiredArgsConstructor
public class ClienteController {

    private final ClienteService service;

}
```

---

# DTO

## ClienteRequest

```java
public record ClienteRequest(

        @NotBlank(message = "Los nombres son obligatorios")
        String nombres,

        @NotBlank(message = "Los apellidos son obligatorios")
        String apellidos,

        @NotBlank(message = "El DNI es obligatorio")
        @Size(min = 8, max = 8)
        String dni,

        @Email(message = "Correo inválido")
        String correo

) {
}
```

---

## ClienteResponse

```java
public record ClienteResponse(

        Long id,

        String nombres,

        String apellidos,

        String dni,

        String correo

) {
}
```

---

# MapStruct

```java
@Mapper(componentModel = "spring")
public interface ClienteMapper {

    Cliente toEntity(ClienteRequest request);

    ClienteResponse toResponse(Cliente entity);

    List<ClienteResponse> toResponseList(List<Cliente> entities);

}
```

---

# Crear Cliente

```java
@Override
@Transactional
public ClienteResponse crear(ClienteRequest request){

    Cliente cliente = mapper.toEntity(request);

    repository.save(cliente);

    return mapper.toResponse(cliente);

}
```

---

# Listar Clientes

```java
@Override
@Transactional(readOnly = true)
public List<ClienteResponse> listar(){

    return mapper.toResponseList(repository.findAll());

}
```

---

# Buscar por ID

```java
@Override
@Transactional(readOnly = true)
public ClienteResponse obtener(Long id){

    Cliente cliente = repository.findById(id)
            .orElseThrow(() ->
                    new ClienteNoEncontradoException(id));

    return mapper.toResponse(cliente);

}
```

---

# Actualizar

```java
@Override
@Transactional
public ClienteResponse actualizar(Long id,
                                  ClienteRequest request){

    Cliente cliente = repository.findById(id)
            .orElseThrow(() ->
                    new ClienteNoEncontradoException(id));

    cliente.setNombres(request.nombres());
    cliente.setApellidos(request.apellidos());
    cliente.setCorreo(request.correo());
    cliente.setDni(request.dni());

    repository.save(cliente);

    return mapper.toResponse(cliente);

}
```

---

# Eliminar

```java
@Override
@Transactional
public void eliminar(Long id){

    Cliente cliente = repository.findById(id)
            .orElseThrow(() ->
                    new ClienteNoEncontradoException(id));

    repository.delete(cliente);

}
```

---

# Endpoints

## Crear

```java
@PostMapping
@ResponseStatus(HttpStatus.CREATED)
public ClienteResponse crear(
        @Valid
        @RequestBody ClienteRequest request){

    return service.crear(request);

}
```

---

## Listar

```java
@GetMapping
public List<ClienteResponse> listar(){

    return service.listar();

}
```

---

## Obtener

```java
@GetMapping("/{id}")
public ClienteResponse obtener(
        @PathVariable Long id){

    return service.obtener(id);

}
```

---

## Actualizar

```java
@PutMapping("/{id}")
public ClienteResponse actualizar(
        @PathVariable Long id,
        @Valid
        @RequestBody ClienteRequest request){

    return service.actualizar(id, request);

}
```

---

## Eliminar

```java
@DeleteMapping("/{id}")
@ResponseStatus(HttpStatus.NO_CONTENT)
public void eliminar(
        @PathVariable Long id){

    service.eliminar(id);

}
```

---

# Exception Personalizada

```java
public class ClienteNoEncontradoException
        extends RuntimeException {

    public ClienteNoEncontradoException(Long id){

        super("Cliente con id "
                + id +
                " no encontrado.");

    }

}
```

---

# Global Exception Handler

```java
@RestControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(
            ClienteNoEncontradoException.class)
    public ResponseEntity<String> clienteNoEncontrado(
            ClienteNoEncontradoException ex){

        return ResponseEntity
                .status(HttpStatus.NOT_FOUND)
                .body(ex.getMessage());

    }

}
```

---

# Validaciones

Utilizar siempre:

```java
@NotBlank

@NotNull

@NotEmpty

@Positive

@PositiveOrZero

@Email

@Pattern

@Size
```

Nunca validar manualmente en el Controller.

---

# OpenAPI (Swagger)

Agregar dependencia

```xml
<dependency>
    <groupId>org.springdoc</groupId>
    <artifactId>springdoc-openapi-starter-webmvc-ui</artifactId>
    <version>2.8.9</version>
</dependency>
```

---

# Configuración

```java
@Configuration
public class OpenApiConfig {

    @Bean
    public OpenAPI api() {

        return new OpenAPI()

                .info(new Info()

                        .title("Sistema Bancario")

                        .version("1.0")

                        .description("API REST"));

    }

}
```

---

# Documentar Endpoint

```java
@Operation(summary = "Crear Cliente")
@ApiResponses({
        @ApiResponse(responseCode = "201",
                description = "Cliente creado"),
        @ApiResponse(responseCode = "400",
                description = "Datos inválidos")
})
@PostMapping
public ClienteResponse crear(
        @Valid
        @RequestBody ClienteRequest request){

    return service.crear(request);

}
```

---

# URL Swagger

```text
http://localhost:8080/swagger-ui/index.html
```

---

# Testing

Dependencias

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-test</artifactId>
    <scope>test</scope>
</dependency>
```

---

# JUnit 5

```java
@Test
void deberiaCrearCliente(){

}
```

---

# Mockito

```java
@ExtendWith(MockitoExtension.class)
class ClienteServiceTest {

    @Mock
    private ClienteRepository repository;

    @InjectMocks
    private ClienteServiceImpl service;

}
```

---

# Mock Repository

```java
when(repository.save(any()))
        .thenReturn(cliente);
```

---

# Verify

```java
verify(repository).save(any());
```

---

# Assertions

```java
assertEquals("Juan",
        response.nombres());

assertNotNull(response);

assertTrue(lista.isEmpty());

assertFalse(lista.isEmpty());

assertThrows(
        ClienteNoEncontradoException.class,
        () -> service.obtener(100L)
);
```

---

# MockMvc

```java
@WebMvcTest(ClienteController.class)
class ClienteControllerTest {

    @Autowired
    private MockMvc mockMvc;

}
```

---

# Ejemplo

```java
mockMvc.perform(get("/api/clientes"))

        .andExpect(status().isOk());
```

---

# Cobertura

Objetivo mínimo

```text
80%
```

Herramienta

```text
JaCoCo
```

---

# Reglas

Todo Service debe tener pruebas.

Todo Controller debe tener MockMvc.

No probar Repository.

---

# Optimización Base de Datos

Reglas

- Utilizar DTO.
- Evitar SELECT *.
- Evitar N+1.
- Utilizar paginación.
- Utilizar índices.
- Utilizar fetch adecuado.
- No consultar varias veces el mismo dato.
- Utilizar transacciones.

---

# Proyecto Bancario

Implementar

```text
ms-clientes
```

CRUD completo

- Crear Cliente

- Buscar Cliente

- Actualizar Cliente

- Eliminar Cliente

- Buscar por DNI

---

# Estructura Final

```text
controller/

service/

repository/

entity/

dto/

mapper/

config/

exception/

validation/
```

---

# Buenas Prácticas

- Arquitectura por capas.
- DTO para entrada y salida.
- No exponer Entity.
- Constructor Injection.
- Lombok.
- Validation.
- ExceptionHandler.
- Swagger.
- Testing.
- SOLID.
- Clean Code.
- Métodos pequeños.
- Una responsabilidad por clase.
- Programar contra interfaces.
- Minimizar consultas a la base de datos.

---

# Mini Reto

Agregar:

- Buscar Cliente por DNI.
- Buscar Clientes activos.
- Paginación.
- Ordenamiento.
- Filtro por apellido.

---

# Preguntas de Entrevista

- ¿Qué hace Spring Boot?
- ¿Qué diferencia existe entre @Controller y @RestController?
- ¿Qué diferencia existe entre @Service y @Component?
- ¿Qué hace @Repository?
- ¿Qué es Dependency Injection?
- ¿Qué es IoC?
- ¿Qué es Bean?
- ¿Qué hace @Transactional?
- ¿Qué diferencia existe entre PUT y PATCH?
- ¿Por qué utilizar DTO?
- ¿Por qué utilizar MapStruct?
- ¿Qué ventajas ofrece Swagger?
- ¿Qué diferencia existe entre JUnit y Mockito?

---

# Checklist

- [ ] CRUD funcionando
- [ ] DTO implementado
- [ ] Mapper implementado
- [ ] Validation implementada
- [ ] ExceptionHandler implementado
- [ ] Swagger configurado
- [ ] JUnit 5 implementado
- [ ] Mockito implementado
- [ ] MockMvc implementado
- [ ] Cobertura superior al 80%

---

# Próximo Módulo

## JPA + Hibernate Profesional

En el siguiente módulo construiremos una capa de persistencia profesional utilizando Spring Data JPA, Hibernate, relaciones entre entidades, consultas optimizadas, Specifications y minimización de accesos a la base de datos.