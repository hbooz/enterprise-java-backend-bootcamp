# Módulo 9 - Git + GitHub + GitFlow Profesional

## Objetivo

Aprender a trabajar con Git y GitHub utilizando un flujo profesional basado en GitFlow y buenas prácticas empresariales.

---

# Tecnologías

- Git
- GitHub
- GitHub Actions
- GitFlow

---

# Instalación

Verificar instalación

```bash
git --version
```

Configurar usuario

```bash
git config --global user.name "Tu Nombre"

git config --global user.email "correo@email.com"
```

---

# Crear Repositorio

```bash
git init
```

---

# Clonar

```bash
git clone https://github.com/usuario/proyecto.git
```

---

# Estado

```bash
git status
```

---

# Agregar archivos

```bash
git add .
```

---

# Commit

```bash
git commit -m "feat(clientes): create client service"
```

---

# Push

```bash
git push origin develop
```

---

# Pull

```bash
git pull origin develop
```

---

# Historial

```bash
git log --oneline --graph
```

---

# GitFlow

```text
main

develop

feature/*

bugfix/*

release/*

hotfix/*
```

---

# Flujo de trabajo

```text
main

↓

develop

↓

feature/ms-clientes

↓

Pull Request

↓

develop

↓

release

↓

main
```

---

# Crear rama

```bash
git checkout -b feature/ms-clientes
```

---

# Cambiar rama

```bash
git checkout develop
```

---

# Merge

```bash
git merge feature/ms-clientes
```

---

# Rebase

```bash
git rebase develop
```

---

# Conventional Commits

```text
feat:

fix:

docs:

test:

refactor:

perf:

style:

build:

ci:

chore:

revert:
```

---

# Ejemplos

```text
feat(clientes): create client endpoint

fix(cuentas): validate balance

docs(readme): update installation

test(cliente): add service tests

refactor(service): simplify validation

chore(deps): update spring boot
```

---

# Pull Request

Todo cambio debe pasar por Pull Request.

Debe contener:

- Descripción.
- Capturas (si aplica).
- Checklist.
- Revisor.

---

# Code Review

Revisar

- Clean Code.
- SOLID.
- Cobertura.
- Nombres.
- Seguridad.
- Rendimiento.
- Duplicación.
- Consultas SQL.

---

# GitHub Actions

Objetivo

Automatizar:

- Build.
- Test.
- Quality Gate.
- Sonar.
- Docker.

---

# Pipeline

```yaml
Build

↓

Test

↓

JaCoCo

↓

Sonar

↓

Docker Build

↓

Deploy
```

---

# Versionado

```text
v1.0.0

v1.1.0

v2.0.0
```

---

# Proyecto Bancario

Cada microservicio tendrá su propio repositorio.

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

# Buenas Prácticas

- No trabajar en main.
- Una funcionalidad por rama.
- Commits pequeños.
- Pull Request obligatorio.
- Revisión de código.
- Pipeline automático.
- Documentar cambios.

---

# Mini Retos

- Crear rama feature.
- Crear Pull Request.
- Resolver conflicto.
- Aplicar Rebase.
- Crear Release.
- Crear Hotfix.

---

# Preguntas de Entrevista

- ¿Qué es Git?
- ¿Qué diferencia existe entre Git y GitHub?
- ¿Qué es GitFlow?
- ¿Qué diferencia existe entre Merge y Rebase?
- ¿Qué es un Pull Request?
- ¿Qué son Conventional Commits?
- ¿Qué hace GitHub Actions?
- ¿Cómo resolver un conflicto?

---

# Checklist

- [ ] Git instalado.
- [ ] GitHub configurado.
- [ ] GitFlow aplicado.
- [ ] Conventional Commits utilizados.
- [ ] Pull Requests utilizados.
- [ ] GitHub Actions configurado.
- [ ] Pipeline funcionando.

---

# Próximo Módulo

## IA aplicada al Desarrollo Backend