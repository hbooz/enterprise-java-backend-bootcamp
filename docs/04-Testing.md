# Módulo 4 - Testing Profesional

## Objetivo

Aprender a implementar pruebas automatizadas para garantizar la calidad del software utilizando JUnit 5, Mockito y MockMvc.

---

# Pirámide de Testing

```text
          E2E
      Integration
     Unit Testing
```

Priorizar pruebas unitarias.

---

# Dependencias

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

# Ciclo de vida

```java
@BeforeEach

@AfterEach

@BeforeAll

@AfterAll
```

---

# Assertions

```java
assertEquals()

assertNotEquals()

assertTrue()

assertFalse()

assertNull()

assertNotNull()

assertThrows()
```

Ejemplo

```java
assertEquals(
        "Juan",
        cliente.getNombres()
);
```

---

# Mockito

```java
@ExtendWith(MockitoExtension.class)
class ClienteServiceTest {

    @Mock
    ClienteRepository repository;

    @Mock
    ClienteMapper mapper;

    @InjectMocks
    ClienteServiceImpl service;

}
```

---

# when

```java
when(repository.findById(1L))
        .thenReturn(Optional.of(cliente));
```

---

# verify

```java
verify(repository).save(any());
```

---

# ArgumentMatchers

```java
any()

anyLong()

anyString()

eq()
```

---

# MockMvc

```java
@WebMvcTest(ClienteController.class)
class ClienteControllerTest {

    @Autowired
    MockMvc mockMvc;

}
```

---

# GET

```java
mockMvc.perform(get("/api/clientes"))
        .andExpect(status().isOk());
```

---

# POST

```java
mockMvc.perform(post("/api/clientes"))
        .andExpect(status().isCreated());
```

---

# PUT

```java
mockMvc.perform(put("/api/clientes/1"))
        .andExpect(status().isOk());
```

---

# DELETE

```java
mockMvc.perform(delete("/api/clientes/1"))
        .andExpect(status().isNoContent());
```

---

# JaCoCo

Objetivo mínimo

```text
80%
```

---

# Qué probar

Service

- Crear
- Buscar
- Actualizar
- Eliminar
- Excepciones

Controller

- HTTP Status
- JSON
- Validaciones

Repository

No probar directamente.

---

# Proyecto Bancario

Probar

ClienteService

CuentaService

TransaccionService

---

# Buenas prácticas

- Un test = un comportamiento.
- Nombres descriptivos.
- No duplicar código.
- Utilizar datos de prueba.
- Probar casos exitosos y fallidos.
- Mantener independencia entre pruebas.

---

# Mini Retos

- Probar crear cliente.
- Probar cliente inexistente.
- Probar validaciones.
- Probar eliminación.
- Alcanzar 80% de cobertura.

---

# Preguntas de Entrevista

- ¿Qué diferencia existe entre JUnit y Mockito?
- ¿Qué hace @Mock?
- ¿Qué hace @InjectMocks?
- ¿Qué hace MockMvc?
- ¿Qué es una prueba unitaria?
- ¿Qué es una prueba de integración?
- ¿Qué cobertura es recomendable?

---

# Checklist

- [ ] JUnit configurado.
- [ ] Mockito configurado.
- [ ] MockMvc configurado.
- [ ] JaCoCo configurado.
- [ ] Cobertura > 80%.
- [ ] Todos los Services probados.
- [ ] Todos los Controllers probados.

---

# Próximo Módulo

## SOLID + Clean Code Profesional