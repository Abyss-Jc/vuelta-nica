# Guía de Contribución — Vuelta Nica

> Hackathon Nicaragua 2026 | Categoría: Avanzado | Temática: Turismo

Este documento establece las reglas de colaboración para todo el equipo. Su cumplimiento es **obligatorio** y será evaluado por los mentores como parte del criterio de "Control de versiones" (30% Desarrollo).

---

## 1. Flujo de Ramas 

Utilizamos una versión simplificada de Git Flow, adaptada al ritmo de un hackathon. No usamos ramas `release/` ni `hotfix/` porque el ciclo de vida del proyecto es corto y los sprints son semanales.

### Ramas permanentes

| Rama | Propósito | Protegida | ¿Quién hace merge? |
|------|-----------|-----------|---------------------|
| `main` | Código en producción (despliegue en VPS). Siempre estable. | Sí | Solo vía PR desde `develop`, aprobado por al menos 1 reviewer. |
| `develop` | Rama de integración. Contiene el último código funcional probado. | Sí | Solo vía PR desde ramas `feature/`, `fix/` o `docs/`. |

### Ramas temporales (se crean y se eliminan)

| Prefijo | Cuándo usarla | Ejemplo |
|---------|---------------|---------|
| `feature/` | Nueva funcionalidad | `feature/guide-certification-upload` |
| `fix/` | Corrección de un bug | `fix/login-null-pointer` |
| `docs/` | Cambios solo en documentación | `docs/update-er-diagram-3fn` |
| `chore/` | Configuración, dependencias, CI/CD | `chore/setup-laravel-sail` |
| `test/` | Pruebas automatizadas | `test/api-guide-endpoints` |

### Reglas de nomenclatura

- Todo en **minúsculas** y separado por **guiones**.
- Máximo 4-5 palabras descriptivas.
- **No**: `feature/ArreglandoCosasDelBackend`
- **Si**: `feature/guide-role-validation`

---

## 2. Conventional Commits

Cada commit debe seguir **estrictamente** este formato:

\<tipo>(\<alcance>): \<descripcion breve en minusculas>

\[cuerpo opcional]

### Tipos permitidos

| Tipo | Cuándo usarlo | Ejemplo |
|------|---------------|---------|
| `feat` | Nueva funcionalidad | `feat(backend): add file upload endpoint` |
| `fix` | Corrección de bug | `fix(mobile): resolve crash on provider registration` |
| `docs` | Documentación | `docs: update ER diagram to 3NF` |
| `style` | Formato, sin cambio de lógica | `style(backend): fix indentation in UserController` |
| `refactor` | Reestructuración sin cambiar comportamiento | `refactor(backend): extract validation to FormRequest` | Mantenimiento, deps, config | `chore: update flutter dependencies` |
| `ci` | Integración continua | `ci: add GitHub Actions workflow` |

### Alcances (`scope`) sugeridos para este proyecto

| Alcance | Se refiere a |
|---------|--------------|
| `backend` | API Laravel + Panel Admin Livewire |
| `mobile` | App Flutter |
| `db` | Migraciones, seeds, diagramas PostgreSQL |
| `deploy` | Configuración del VPS, Docker, scripts |
| `docs` | Documentación general |

### Ejemplos reales del proyecto

- feat(backend): create API endpoint for tourist-to-guide role upgrade
- feat(mobile): implement provider property verification screen
- fix(backend): resolve N+1 query in guide listings
- fix(mobile): handle expired JWT token on app resume
- docs: add UML activity diagram for certification flow
- chore(db): add migration for INTUR certificate validation table
- test(backend): add feature test for admin role approval workflow
- refactor(backend): move payment mock logic to service layer

### ❌ Commits que NO se aceptan

- update
- arreglando cosas
- WIP
- cambio en el backend
- mejorar estilo
- fix
- .

## 3. Pull Requests (PRs)

### Reglas obligatorias

1. **Nunca** hagas push directo a `main` ni a `develop`. Todo pasa por PR.
2. Cada PR debe tener **al menos 1 aprobación** de otro miembro del equipo.
3. Todos los comentarios de revisión deben marcarse como **"Resolved"** antes de hacer merge.
4. El PR debe estar vinculado a una **tarjeta de Trello**.
5. Si el PR incluye cambios visuales (Livewire o Flutter), adjunta **capturas de pantalla**.

### Plantilla de Pull Request

Copia y pega esto en cada PR:

## Descripción
<!-- ¿Qué hace este PR? -->

## Tipo de cambio
- [ ] feat (nueva funcionalidad)
- [ ] fix (corrección de bug)
- [ ] docs (documentación)
- [ ] refactor (reestructuración)
- [ ] chore (mantenimiento)

## Capturas de pantalla (si aplica)
<!-- Arrastra imágenes aca si hay cambios visuales -->

## Checklist
- [ ] Mi código sigue los Conventional Commits
- [ ] He probado la funcionalidad localmente
- [ ] No hay credenciales ni archivos `.env` en el PR
- [ ] La documentación está actualizada (si aplica)

## 4. Ejemplo de flujo completo

Supongamos que implementaste el flujo de subida de certificado del INTUR para ascender a un usuario a guia

### 1. Asegurate de estar en dev y actualizado
git checkout dev
git pull origin dev

### 2. Crea tu rama de trabajo
git checkout -b feature/guide-certification-upload

### 3. Trabaja en tu código 

### 4. Haz commits siguiendo Conventional Commits
1. git add .
2. git commit -m "feat(backend): add INTUR certificate upload endpoint"
3. git commit -m "feat(db): create guide_certifications migration"
4. git commit -m "test(backend): add feature test for certificate validation"

### 5. Sube tu rama al repositorio remoto
git push origin feature/guide-certification-upload

### 6. Abre un Pull Request en GitHub
####    - Base: dev
####    - Compare: feature/guide-certification-upload
####    - Usa la plantilla de PR

### 7. Otro dev revisa el PR, deja comentarios, aprueba

### 8. Se hace merge a dev (Squash --> Merge recomendado)

### 9. Elimina la rama temporal
git branch -d feature/guide-certification-upload
git push origin --delete feature/guide-certification-upload
