# Módulo 1 - Java Profesional

## Objetivo

Dominar Java moderno (17/21) y la Programación Orientada a Objetos para construir aplicaciones Backend profesionales con Spring Boot.

---

# ¿Qué aprenderás?

- Sintaxis de Java
- Variables
- Tipos de datos
- Operadores
- Condicionales
- Bucles
- Métodos
- Clases
- Objetos
- Encapsulamiento
- Herencia
- Polimorfismo
- Abstracción
- Interfaces
- Excepciones
- Collections
- Streams
- Optional
- Lambdas
- Records

Todo será aplicado al proyecto **Sistema Bancario**.

---

# Requisitos

- JDK 21 (compatible con Java 17)
- IntelliJ IDEA
- Git
- GitHub
- Maven básico

---

# Proyecto del módulo

Durante este módulo construiremos el dominio del sistema bancario.

Entidades principales:

- Cliente
- Cuenta
- Transacción
- Tarjeta
- Préstamo

---

# ¿Qué es Java?

Java es un lenguaje de programación orientado a objetos, multiplataforma y ampliamente utilizado para desarrollar aplicaciones empresariales.

En este bootcamp utilizaremos Java como base para construir aplicaciones Spring Boot y microservicios.

---

# Variables

Una variable es un espacio en memoria que almacena información.

Ejemplo:

```java
String nombre = "Juan";
int edad = 25;
double saldo = 1500.75;
boolean activo = true;

---

# Encapsulamiento

## ¿Qué es?

Es el principio que protege los datos de una clase ocultando sus atributos y permitiendo el acceso únicamente mediante métodos controlados.

## Ejemplo

```java
public class Cliente {

    private Long id;

    private String nombre;

    private String dni;

    public Cliente() {
    }

    public Cliente(Long id, String nombre, String dni) {
        this.id = id;
        this.nombre = nombre;
        this.dni = dni;
    }

    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }

    public String getNombre() {
        return nombre;
    }

    public void setNombre(String nombre) {
        this.nombre = nombre;
    }

    public String getDni() {
        return dni;
    }

    public void setDni(String dni) {
        this.dni = dni;
    }
}
```

---

# Constructores

Permiten inicializar un objeto.

```java
public Cliente() {

}
```

```java
public Cliente(Long id, String nombre, String dni) {

    this.id = id;
    this.nombre = nombre;
    this.dni = dni;

}
```

---

# this

Hace referencia al objeto actual.

```java
this.nombre = nombre;
```

---

# Herencia

Permite reutilizar atributos y comportamientos.

```java
public class Persona {

    protected String nombre;

    protected String apellido;

}
```

```java
public class Cliente extends Persona {

    private String dni;

}
```

---

# Sobrescritura (Override)

```java
@Override
public String toString() {
    return nombre;
}
```

---

# Polimorfismo

Permite utilizar distintas implementaciones mediante una referencia común.

```java
Persona persona = new Cliente();
```

```java
Persona persona = new Empleado();
```

---

# Clases Abstractas

```java
public abstract class Persona {

    protected String nombre;

    public abstract void mostrarInformacion();

}
```

```java
public class Cliente extends Persona {

    @Override
    public void mostrarInformacion() {

        System.out.println(nombre);

    }

}
```

---

# Interfaces

```java
public interface NotificacionService {

    void enviar();

}
```

```java
public class EmailService implements NotificacionService {

    @Override
    public void enviar() {

        System.out.println("Correo enviado");

    }

}
```

```java
public class SmsService implements NotificacionService {

    @Override
    public void enviar() {

        System.out.println("SMS enviado");

    }

}
```

---

# Composición

Preferir composición sobre herencia.

```java
public class Cuenta {

    private Cliente cliente;

}
```

---

# Enumeraciones

```java
public enum EstadoCuenta {

    ACTIVA,

    BLOQUEADA,

    CANCELADA

}
```

Uso:

```java
EstadoCuenta estado = EstadoCuenta.ACTIVA;
```

---

# Records (Java 17+)

```java
public record ClienteDTO(

        Long id,

        String nombre,

        String dni

) {
}
```

Utilizar Records para DTOs inmutables.

---

# Buenas prácticas

- Utilizar atributos privados.
- Evitar herencia innecesaria.
- Programar contra interfaces.
- Favorecer composición.
- Utilizar Records para DTOs.
- Evitar clases con múltiples responsabilidades.

---

# Generics

Los Generics permiten reutilizar código utilizando tipos parametrizados.

## Ejemplo

```java
List<String> nombres = new ArrayList<>();

List<Cliente> clientes = new ArrayList<>();

List<Cuenta> cuentas = new ArrayList<>();
```

Evitar:

```java
List lista = new ArrayList();
```

Siempre indicar el tipo.

---

# Collections Framework

Interfaces principales

```text
Collection
│
├── List
├── Set
└── Queue
```

Implementaciones más utilizadas

```text
ArrayList

LinkedList

HashSet

TreeSet

PriorityQueue

HashMap

TreeMap
```

---

# List

Permite elementos repetidos.

Mantiene el orden de inserción.

```java
List<Cliente> clientes = new ArrayList<>();

clientes.add(new Cliente());

clientes.add(new Cliente());
```

Métodos importantes

```java
add()

remove()

get()

contains()

size()

isEmpty()

clear()
```

---

# ArrayList

Utilizar cuando existan muchas lecturas.

```java
List<Cliente> clientes = new ArrayList<>();
```

---

# LinkedList

Utilizar cuando existan muchas inserciones o eliminaciones.

```java
List<Cliente> clientes = new LinkedList<>();
```

---

# Set

No permite elementos repetidos.

```java
Set<String> dnis = new HashSet<>();
```

---

# HashSet

No mantiene orden.

Mayor rendimiento.

```java
Set<Cliente> clientes = new HashSet<>();
```

---

# TreeSet

Mantiene orden.

```java
Set<String> nombres = new TreeSet<>();
```

---

# Queue

Representa una cola.

```java
Queue<Transaccion> cola = new LinkedList<>();
```

Métodos

```java
offer()

poll()

peek()
```

---

# Map

Trabaja mediante clave y valor.

```java
Map<Long, Cliente> clientes = new HashMap<>();
```

Agregar

```java
clientes.put(1L, cliente);
```

Obtener

```java
clientes.get(1L);
```

Recorrer

```java
for (Map.Entry<Long, Cliente> entry : clientes.entrySet()) {

}
```

---

# HashMap

Implementación más utilizada.

```java
Map<Long, Cliente> mapa = new HashMap<>();
```

---

# TreeMap

Mantiene orden por clave.

```java
Map<Long, Cliente> mapa = new TreeMap<>();
```

---

# Comparable

Permite ordenar objetos.

```java
public class Cliente implements Comparable<Cliente> {

    @Override
    public int compareTo(Cliente otro) {

        return this.nombre.compareTo(otro.nombre);

    }

}
```

---

# Comparator

Permite distintos criterios de orden.

```java
clientes.sort(
    Comparator.comparing(Cliente::getNombre)
);
```

---

# Buenas prácticas

- Programar utilizando interfaces.
- Utilizar Generics.
- Elegir la colección correcta.
- Evitar colecciones sincronizadas innecesarias.
- No usar Vector.
- No usar Hashtable.

---

# Streams

Los Streams permiten procesar colecciones de manera declarativa y funcional.

---

# Crear un Stream

```java
List<Cliente> clientes = List.of();

clientes.stream();
```

---

# filter()

Filtra elementos.

```java
List<Cliente> activos = clientes.stream()
        .filter(Cliente::isActivo)
        .toList();
```

---

# map()

Transforma objetos.

```java
List<String> nombres = clientes.stream()
        .map(Cliente::getNombre)
        .toList();
```

---

# sorted()

Ordena elementos.

```java
List<Cliente> ordenados = clientes.stream()
        .sorted(Comparator.comparing(Cliente::getNombre))
        .toList();
```

---

# distinct()

Elimina duplicados.

```java
clientes.stream()
        .distinct()
        .toList();
```

---

# limit()

Limita resultados.

```java
clientes.stream()
        .limit(10)
        .toList();
```

---

# skip()

Omite elementos.

```java
clientes.stream()
        .skip(5)
        .toList();
```

---

# anyMatch()

```java
boolean existe = clientes.stream()
        .anyMatch(c -> c.getDni().equals("12345678"));
```

---

# allMatch()

```java
boolean activos = clientes.stream()
        .allMatch(Cliente::isActivo);
```

---

# noneMatch()

```java
boolean ninguno = clientes.stream()
        .noneMatch(c -> c.getSaldo().compareTo(BigDecimal.ZERO) < 0);
```

---

# findFirst()

```java
Optional<Cliente> cliente = clientes.stream()
        .findFirst();
```

---

# findAny()

```java
Optional<Cliente> cliente = clientes.stream()
        .findAny();
```

---

# count()

```java
long total = clientes.stream()
        .count();
```

---

# max()

```java
Cliente cliente = clientes.stream()
        .max(Comparator.comparing(Cliente::getSaldo))
        .orElse(null);
```

---

# min()

```java
Cliente cliente = clientes.stream()
        .min(Comparator.comparing(Cliente::getSaldo))
        .orElse(null);
```

---

# forEach()

```java
clientes.forEach(System.out::println);
```

---

# Optional

Evita NullPointerException.

---

## Crear Optional

```java
Optional<Cliente> cliente = Optional.of(clienteExistente);
```

---

## ofNullable()

```java
Optional<Cliente> cliente = Optional.ofNullable(cliente);
```

---

## isPresent()

```java
if(cliente.isPresent()){

}
```

---

## ifPresent()

```java
cliente.ifPresent(System.out::println);
```

---

## orElse()

```java
Cliente resultado = cliente.orElse(new Cliente());
```

---

## orElseThrow()

```java
Cliente resultado = cliente.orElseThrow();
```

---

# Expresiones Lambda

Sintaxis

```java
(parametros) -> expresión
```

---

## Ejemplo

```java
clientes.forEach(cliente -> System.out.println(cliente.getNombre()));
```

---

## Referencias a métodos

```java
clientes.forEach(System.out::println);
```

```java
clientes.stream()
        .map(Cliente::getNombre)
        .toList();
```

---

# Buenas prácticas

- Preferir Streams para transformación de datos.
- Evitar Streams extremadamente largos.
- No abusar de Optional como atributo de clases.
- Utilizar referencias a métodos cuando mejoren la legibilidad.
- Mantener las expresiones Lambda simples.
- Utilizar BigDecimal para operaciones monetarias.

---

# Excepciones

Las excepciones permiten controlar errores durante la ejecución del programa.

---

# Tipos de excepciones

## Checked Exception

Obligan a ser manejadas.

Ejemplo:

```java
IOException
SQLException
```

---

## Unchecked Exception

Heredan de RuntimeException.

Ejemplo:

```java
NullPointerException

IllegalArgumentException

IllegalStateException

ArithmeticException
```

---

# try-catch

```java
try {

    int resultado = 10 / 0;

} catch (ArithmeticException ex) {

    System.out.println(ex.getMessage());

}
```

---

# try-catch-finally

```java
try {

    System.out.println("Procesando");

} catch (Exception ex) {

    ex.printStackTrace();

} finally {

    System.out.println("Finalizado");

}
```

---

# throw

```java
if (cliente == null) {

    throw new IllegalArgumentException("Cliente no encontrado");

}
```

---

# throws

```java
public void guardar() throws IOException {

}
```

---

# Excepciones personalizadas

```java
public class ClienteNoEncontradoException extends RuntimeException {

    public ClienteNoEncontradoException(String mensaje) {

        super(mensaje);

    }

}
```

Uso

```java
throw new ClienteNoEncontradoException(
        "Cliente no encontrado");
```

---

# Buenas prácticas

- Nunca capturar Exception si no es necesario.
- Crear excepciones propias para reglas del negocio.
- Utilizar mensajes claros.
- No ocultar errores.
- No usar printStackTrace() en producción.

---

# Proyecto Bancario

Crear las siguientes excepciones:

```text
ClienteNoEncontradoException

CuentaNoEncontradaException

SaldoInsuficienteException

TransaccionNoPermitidaException
```

---

# Ejercicio 1

Crear la clase Cliente.

Debe contener:

- id
- nombre
- apellido
- dni
- correo
- telefono

---

# Ejercicio 2

Crear la clase Cuenta.

Debe contener:

- numeroCuenta
- saldo
- estadoCuenta
- cliente

---

# Ejercicio 3

Crear la clase Transaccion.

Debe contener:

- id
- fecha
- tipo
- monto
- cuentaOrigen
- cuentaDestino

---

# Mini reto

Construir una aplicación de consola que permita:

1. Registrar clientes.
2. Crear cuentas.
3. Depositar.
4. Retirar.
5. Transferir.
6. Mostrar clientes.
7. Mostrar cuentas.
8. Mostrar transacciones.

Aplicar:

- POO
- Collections
- Streams
- Optional
- Excepciones

---

# Buenas prácticas generales

- Programar contra interfaces.
- Aplicar SOLID.
- Evitar código duplicado.
- Utilizar nombres descriptivos.
- Mantener métodos pequeños.
- Utilizar BigDecimal para dinero.
- Utilizar LocalDate y LocalDateTime para fechas.
- Evitar null cuando sea posible.
- Utilizar Optional correctamente.
- Utilizar Streams para transformación de datos.

---

# Preguntas de entrevista

## Java

- ¿Qué diferencias existen entre JDK, JRE y JVM?
- ¿Qué ventajas ofrece Java?
- ¿Qué es el Garbage Collector?
- ¿Qué diferencia existe entre Stack y Heap?

## POO

- ¿Qué es encapsulamiento?
- ¿Qué es herencia?
- ¿Qué es polimorfismo?
- ¿Qué es abstracción?
- ¿Cuándo utilizar composición?

## Collections

- Diferencias entre List y Set.
- Diferencias entre ArrayList y LinkedList.
- Diferencias entre HashMap y TreeMap.
- ¿Qué complejidad tiene HashMap?

## Streams

- ¿Qué hace map()?
- ¿Qué hace filter()?
- ¿Qué hace flatMap()?
- ¿Qué diferencia existe entre map y forEach?

## Optional

- ¿Para qué sirve Optional?
- ¿Cuándo utilizar Optional?
- Diferencia entre orElse() y orElseThrow().

## Excepciones

- Diferencia entre Checked y Unchecked.
- ¿Cuándo crear una excepción personalizada?
- ¿Por qué RuntimeException es tan utilizada en Spring Boot?

---

# Checklist

- [ ] Comprendo la sintaxis de Java.
- [ ] Domino POO.
- [ ] Utilizo Collections correctamente.
- [ ] Sé utilizar Streams.
- [ ] Comprendo Optional.
- [ ] Comprendo Lambdas.
- [ ] Comprendo Records.
- [ ] Comprendo Enums.
- [ ] Sé manejar excepciones.
- [ ] Puedo construir el modelo del Sistema Bancario.

---

# Próximo módulo

## Spring Boot Profesional

En el siguiente módulo construiremos el microservicio **ms-clientes**, aplicando arquitectura por capas, DTOs, validaciones, Swagger, JUnit 5, Mockito y buenas prácticas empresariales.

