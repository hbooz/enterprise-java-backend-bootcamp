# Módulo 1 - Java Profesional

## Objetivo

Dominar la Programación Orientada a Objetos (POO) para construir aplicaciones Backend con Java y Spring Boot.

---

# ¿Qué aprenderás?

- Clases
- Objetos
- Encapsulamiento
- Herencia
- Polimorfismo
- Abstracción

Todo se aplicará al proyecto **Sistema Bancario**.

---

# Proyecto del módulo

Durante este módulo construiremos el modelo del banco utilizando las siguientes entidades:

- Cliente
- Cuenta
- Transacción

Todos los ejemplos estarán basados en estas entidades.

---

# Clase

## ¿Qué es?

Una clase es un molde que define los atributos y comportamientos de un objeto.

### Ejemplo

```java
public class Cliente {

    private Long id;
    private String nombre;
    private String dni;

}
```

---

# Objeto

Un objeto es una instancia creada a partir de una clase.

```java
Cliente cliente = new Cliente();
```

---

# Encapsulamiento

Los atributos deben ser privados.

Siempre acceder mediante métodos.

```java
private String nombre;
```

```java
public String getNombre() {
    return nombre;
}

public void setNombre(String nombre) {
    this.nombre = nombre;
}
```

---

# Herencia

Permite reutilizar comportamiento.

```java
public class Persona {

    protected String nombre;

}
```

```java
public class Cliente extends Persona {

}
```

---

# Polimorfismo

Permite trabajar con distintas implementaciones.

```java
Persona persona = new Cliente();
```

---

# Abstracción

Consiste en mostrar únicamente lo necesario.

Utilizar interfaces y clases abstractas cuando corresponda.

---

# Buenas prácticas

- Atributos privados.
- Utilizar constructores.
- Utilizar getters y setters.
- Una responsabilidad por clase.
- Nombres claros.
- Evitar clases gigantes.

---

# Ejercicio

Crear las siguientes clases:

- Cliente
- Cuenta
- Transaccion

Cada una debe tener:

- atributos privados
- constructor
- getters
- setters
- toString()

---

# Mini reto

Agregar la clase:

```text
Banco
```

que contenga una lista de clientes.

---

# Preguntas de entrevista

- ¿Qué es una clase?
- ¿Qué es un objeto?
- ¿Qué diferencia existe entre herencia y composición?
- ¿Qué es encapsulamiento?
- ¿Qué es polimorfismo?
- ¿Qué es abstracción?

---

# Checklist

- [ ] Comprendo qué es una clase.
- [ ] Sé crear objetos.
- [ ] Aplico encapsulamiento.
- [ ] Comprendo la herencia.
- [ ] Comprendo el polimorfismo.
- [ ] Comprendo la abstracción.

---

# Proyecto bancario

Al finalizar este módulo tendremos el dominio base del sistema bancario sobre el que construiremos Spring Boot en el siguiente módulo.