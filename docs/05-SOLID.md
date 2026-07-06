# Módulo 5 - SOLID + Clean Code Profesional

## Objetivo

Aprender a diseñar aplicaciones Backend mantenibles, escalables y desacopladas aplicando SOLID y Clean Code.

---

# Clean Code

Principios

- Código simple.
- Código legible.
- Métodos pequeños.
- Clases pequeñas.
- Nombres descriptivos.
- Evitar duplicación.

---

# Naming

Correcto

```java
obtenerClientePorId()
```

Incorrecto

```java
get()

a()

proceso()
```

---

# Métodos

Incorrecto

```java
public void procesarCliente(){

    validar();

    guardar();

    enviarCorreo();

    generarPDF();

}
```

Correcto

```java
validarCliente();

guardarCliente();

enviarCorreo();

generarPdf();
```

---

# Single Responsibility Principle (SRP)

Cada clase debe tener una única responsabilidad.

Incorrecto

```text
ClienteService

↓

Valida

Guarda

Envía correo

Genera PDF
```

Correcto

```text
ClienteService

EmailService

PdfService
```

---

# Open Closed Principle (OCP)

Las clases deben estar abiertas para extensión y cerradas para modificación.

Incorrecto

```java
if(tipo.equals("EMAIL")){

}

if(tipo.equals("SMS")){

}
```

Correcto

```java
interface NotificacionService{

    void enviar();

}
```

---

# Liskov Substitution Principle (LSP)

Una implementación debe poder sustituir a su padre.

```java
Persona persona = new Cliente();
```

---

# Interface Segregation Principle (ISP)

Interfaces pequeñas.

Incorrecto

```java
interface BancoService{

    crear();

    eliminar();

    enviarCorreo();

    imprimir();

}
```

Correcto

```java
ClienteService

CorreoService

ReporteService
```

---

# Dependency Inversion Principle (DIP)

Depender de interfaces.

```java
private final ClienteRepository repository;
```

Nunca

```java
private final ClienteRepositoryImpl repository;
```

---

# Dependency Injection

Constructor Injection.

```java
@RequiredArgsConstructor
public class ClienteService{

    private final ClienteRepository repository;

}
```

---

# Code Smells

- Métodos largos.
- Clases gigantes.
- Código duplicado.
- Variables globales.
- Demasiados parámetros.
- Switch excesivos.

---

# Refactorización

Aplicar constantemente.

Objetivo:

- Mejor legibilidad.
- Menor acoplamiento.
- Mayor mantenibilidad.

---

# Proyecto Bancario

Aplicar SOLID en

- ClienteService
- CuentaService
- TransaccionService
- NotificacionService

---

# Buenas prácticas

- Constructor Injection.
- Programar contra interfaces.
- No utilizar lógica en Controllers.
- DTO para entrada y salida.
- Una responsabilidad por clase.
- Métodos cortos.
- Clases cohesivas.
- Evitar duplicación.

---

# Mini Retos

- Refactorizar ClienteService.
- Aplicar Strategy.
- Aplicar Factory.
- Aplicar Builder.
- Aplicar Dependency Injection.

---

# Preguntas de Entrevista

- ¿Qué es SOLID?
- Explica SRP.
- Explica OCP.
- Explica LSP.
- Explica ISP.
- Explica DIP.
- ¿Qué es Clean Code?
- ¿Qué es un Code Smell?
- ¿Qué patrón utilizas para desacoplar lógica?

---

# Checklist

- [ ] SRP aplicado.
- [ ] OCP aplicado.
- [ ] LSP aplicado.
- [ ] ISP aplicado.
- [ ] DIP aplicado.
- [ ] Constructor Injection.
- [ ] Código limpio.
- [ ] Clases pequeñas.
- [ ] Métodos pequeños.

---

# Próximo Módulo

## Spring Security + JWT Profesional