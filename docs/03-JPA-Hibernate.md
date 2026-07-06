# Módulo 3 - JPA + Hibernate Profesional

## Objetivo

Aprender a construir una capa de persistencia profesional utilizando Spring Data JPA y Hibernate.

---

# Tecnologías

- Spring Data JPA
- Hibernate
- MySQL
- HikariCP
- Flyway
- Lombok

---

# ¿Qué es un ORM?

ORM (Object Relational Mapping) permite mapear objetos Java con tablas de base de datos.

Java

↓

Hibernate

↓

MySQL

---

# ¿Qué es JPA?

JPA es la especificación.

Hibernate es la implementación.

---

# Spring Data JPA

Spring simplifica el acceso a datos mediante Repository.

```java
public interface ClienteRepository
        extends JpaRepository<Cliente,Long>{

}
```

---

# Entity

```java
@Entity
@Table(name="clientes")
@Getter
@Setter
@NoArgsConstructor
@AllArgsConstructor
@Builder
public class Cliente{

    @Id
    @GeneratedValue(strategy=GenerationType.IDENTITY)
    private Long id;

    @Column(nullable=false,length=100)
    private String nombres;

    @Column(nullable=false,length=100)
    private String apellidos;

    @Column(nullable=false,unique=true,length=8)
    private String dni;

    @Column(nullable=false)
    private String correo;

}
```

---

# Primary Key

```java
@Id
@GeneratedValue(strategy=GenerationType.IDENTITY)
private Long id;
```

---

# Column

```java
@Column(nullable=false)

@Column(unique=true)

@Column(length=100)
```

---

# Repository

```java
@Repository
public interface ClienteRepository
        extends JpaRepository<Cliente,Long>{

}
```

---

# JpaRepository

Métodos disponibles

```java
findAll()

findById()

save()

delete()

existsById()

count()
```

---

# Query Methods

```java
Optional<Cliente>
findByDni(String dni);
```

```java
List<Cliente>
findByApellidos(String apellidos);
```

```java
boolean
existsByDni(String dni);
```

---

# Relaciones

OneToOne

OneToMany

ManyToOne

ManyToMany

---

# OneToMany

```java
@OneToMany(
        mappedBy="cliente",
        cascade=CascadeType.ALL,
        fetch=FetchType.LAZY
)

private List<Cuenta> cuentas;
```

---

# ManyToOne

```java
@ManyToOne(fetch=FetchType.LAZY)

@JoinColumn(name="cliente_id")

private Cliente cliente;
```

---

# Cascade

Utilizar normalmente

```java
CascadeType.ALL
```

o

```java
CascadeType.PERSIST
```

Evitar usar ALL sin entender sus efectos.

---

# Fetch

Preferir

```java
LAZY
```

Evitar

```java
EAGER
```

salvo necesidad.

---

# Proyecto Bancario

Cliente

↓

Cuenta

↓

Transacción

# JPQL

JPQL trabaja sobre entidades, no sobre tablas.

## Buscar por DNI

```java
@Query("""
SELECT c
FROM Cliente c
WHERE c.dni = :dni
""")
Optional<Cliente> buscarPorDni(String dni);
```

---

## Buscar Activos

```java
@Query("""
SELECT c
FROM Cliente c
WHERE c.activo = true
""")
List<Cliente> buscarActivos();
```

---

# Native Query

Usar únicamente cuando JPQL no sea suficiente.

```java
@Query(value = """
SELECT *
FROM clientes
WHERE dni = :dni
""", nativeQuery = true)
Optional<Cliente> buscarPorDni(String dni);
```

---

# Paginación

```java
Page<Cliente> findAll(Pageable pageable);
```

Uso

```java
PageRequest.of(0,10);
```

Ordenado

```java
PageRequest.of(
        0,
        10,
        Sort.by("nombres")
);
```

---

# Sorting

```java
Sort.by("nombres")
```

```java
Sort.by("id")
        .descending();
```

---

# Specifications

Permiten construir consultas dinámicas.

```java
public class ClienteSpecification {

    public static Specification<Cliente>
    nombres(String nombre){

        return(root,query,builder)->
                builder.like(
                        root.get("nombres"),
                        "%" + nombre + "%");

    }

}
```

Uso

```java
repository.findAll(specification);
```

---

# EntityGraph

Evita consultas innecesarias.

```java
@EntityGraph(attributePaths = {
        "cuentas"
})
Optional<Cliente>
findById(Long id);
```

---

# DTO Projection

Nunca devolver Entity cuando no sea necesario.

```java
@Query("""
SELECT new
com.bootcamp.dto.ClienteResponse(

c.id,

c.nombres,

c.apellidos)

FROM Cliente c
""")
List<ClienteResponse> listar();
```

---

# Optimización

Siempre intentar:

- Una consulta.
- Un viaje a la base de datos.
- DTO Projection.
- Índices.
- Paginación.

---

# Evitar N+1

Incorrecto

```text
1 consulta clientes

100 consultas cuentas
```

Correcto

```text
1 consulta utilizando JOIN FETCH
```

Ejemplo

```java
@Query("""
SELECT c

FROM Cliente c

LEFT JOIN FETCH c.cuentas
""")
List<Cliente> listar();
```

---

# Índices

Crear índices sobre:

- dni
- numeroCuenta
- correo

Ejemplo

```java
@Table(
indexes = {

@Index(columnList = "dni"),

@Index(columnList = "correo")

}
)
```

---

# Transacciones

Lectura

```java
@Transactional(readOnly = true)
```

Escritura

```java
@Transactional
```

---

# Locking

Optimista

```java
@Version
private Long version;
```

---

# Auditoría

```java
@CreatedDate

@LastModifiedDate
```

---

# Buenas prácticas

- Utilizar DTO Projection.
- Evitar SELECT *.
- Preferir JPQL.
- Utilizar Native Query solo cuando aporte rendimiento.
- Utilizar Pageable.
- Utilizar Specification.
- Utilizar EntityGraph.
- Evitar N+1.
- Utilizar índices.
- Minimizar accesos a base de datos.

---

# Flyway

Utilizar Flyway para versionar la base de datos.

Estructura

```text
src/main/resources/db/migration
```

---

Primer script

```text
V1__create_clientes.sql
```

```sql
CREATE TABLE clientes(

    id BIGINT PRIMARY KEY AUTO_INCREMENT,

    nombres VARCHAR(100) NOT NULL,

    apellidos VARCHAR(100) NOT NULL,

    dni VARCHAR(8) NOT NULL UNIQUE,

    correo VARCHAR(150) NOT NULL,

    activo BOOLEAN DEFAULT TRUE

);
```

---

Segundo script

```text
V2__create_cuentas.sql
```

---

Tercer script

```text
V3__create_transacciones.sql
```

---

# Auditoría

Crear clase base

```java
@MappedSuperclass

@EntityListeners(AuditingEntityListener.class)

@Getter

@Setter
public abstract class Auditoria {

    @CreatedDate
    private LocalDateTime fechaCreacion;

    @LastModifiedDate
    private LocalDateTime fechaActualizacion;

}
```

Uso

```java
public class Cliente extends Auditoria {

}
```

---

# Soft Delete

Nunca eliminar información bancaria físicamente.

```java
private Boolean activo = true;
```

Eliminar

```java
cliente.setActivo(false);
```

Consultar

```java
findByActivoTrue();
```

---

# Relaciones del Proyecto

```text
Cliente

│

├── Cuenta

│      │

│      ├── Transacción

│      ├── Tarjeta

│      └── Préstamo
```

---

# Convenciones

Tablas

```text
clientes

cuentas

transacciones

prestamos

tarjetas
```

Columnas

```text
cliente_id

cuenta_id

fecha_creacion

fecha_actualizacion
```

---

# Rendimiento

Siempre intentar

- 1 consulta
- 1 transacción
- 1 viaje a BD

Evitar

- Consultas repetidas
- SELECT *
- EAGER innecesario
- N+1

---

# Checklist de Persistencia

- [ ] Todas las entidades tienen @Entity.
- [ ] Todas tienen @Id.
- [ ] Relaciones correctamente definidas.
- [ ] DTO Projection utilizada.
- [ ] Pageable implementado.
- [ ] Specifications implementadas.
- [ ] EntityGraph utilizado cuando aplica.
- [ ] Flyway configurado.
- [ ] Auditoría implementada.
- [ ] Soft Delete implementado.
- [ ] Consultas optimizadas.

---

# Mini Retos

## Reto 1

Buscar clientes por DNI.

---

## Reto 2

Buscar clientes por apellido utilizando Specification.

---

## Reto 3

Listar clientes paginados.

---

## Reto 4

Listar clientes ordenados por apellido.

---

## Reto 5

Obtener un cliente junto con todas sus cuentas evitando N+1.

---

## Reto 6

Implementar Soft Delete.

---

## Preguntas de Entrevista

- ¿Qué diferencia existe entre JPA y Hibernate?
- ¿Qué hace JpaRepository?
- ¿Qué diferencia existe entre save() y saveAndFlush()?
- ¿Qué diferencia existe entre LAZY y EAGER?
- ¿Qué es el problema N+1?
- ¿Qué es JPQL?
- ¿Cuándo utilizar Native Query?
- ¿Qué ventajas ofrece Specification?
- ¿Qué es EntityGraph?
- ¿Qué es DTO Projection?
- ¿Qué hace @Transactional?
- ¿Qué diferencia existe entre CascadeType.ALL y CascadeType.PERSIST?
- ¿Qué es Flyway?
- ¿Qué ventajas ofrece Soft Delete?
- ¿Cómo reducirías las visitas a la base de datos?

---

# Buenas Prácticas Enterprise

- Utilizar DTOs.
- No devolver Entity.
- Aplicar Repository únicamente para persistencia.
- Utilizar índices.
- Versionar la BD con Flyway.
- Auditar cambios.
- Minimizar consultas.
- Programar para escalabilidad.
- Preparar las entidades para microservicios.

---

# Próximo Módulo

## Testing Profesional

En el siguiente módulo implementaremos:

- JUnit 5
- Mockito
- MockMvc
- JaCoCo
- Cobertura superior al 80%
- Pruebas unitarias
- Pruebas de integración
- Pruebas del sistema bancario

