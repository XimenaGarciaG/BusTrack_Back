# task.md — Etapa 01: Validación de la documentación SDD

**Versión:** 1.0.0  
**Estado:** Activo  
**Última actualización:** 2026-10-29  
**Etapa:** 01  
**Referencia normativa:** [`constitution.md`](../../constitution.md) | [`plan.md`](../../plan.md) | [`task.md`](../../task.md)

> Ninguna tarea puede marcarse como `COMPLETADA` sin evidencia verificable.

---

## Convenciones de estado

| Estado | Descripción |
|--------|-------------|
| `PENDIENTE` | Lista para iniciarse cuando corresponda; sin bloqueos |
| `BLOQUEADA` | No puede iniciarse; tiene dependencias no resueltas |
| `EN_PROGRESO` | Ha comenzado efectivamente (con evidencia) |
| `COMPLETADA` | Finalizada con evidencia verificable |

---

## Resumen de tareas

| ID | Título | Estado |
|----|--------|--------|
| TAREA-001 | Revisión de coherencia interna de los documentos SDD | PENDIENTE |
| TAREA-002 | Revisión y aprobación por el responsable del proyecto | PENDIENTE |
| TAREA-003 | Resolución de decisiones bloqueantes para la Etapa 02 | PENDIENTE |

---

### TAREA-001

| Campo | Valor |
|-------|-------|
| **ID** | TAREA-001 |
| **Título** | Revisión de coherencia interna de los documentos SDD |
| **Etapa** | 01 |
| **Estado** | PENDIENTE |
| **Referencia** | `plan.md` Fase 1, `spec.md` sección 18 |

**Descripción:**  
Revisar que todos los documentos SDD generados (`constitution.md`, `AGENTS.md`, `memoria.md`, `spec.md`, `plan.md`, `task.md`) sean coherentes entre sí. Verificar que no existan contradicciones entre principios, decisiones y restricciones.

**Objetivo:**  
Garantizar la coherencia documental antes de someter los documentos a revisión externa.

**Dependencias:**  
Ninguna. Es la primera tarea de la etapa.

**Criterios de aceptación:**
- [ ] Todos los documentos están presentes en el repositorio.
- [ ] No se identifican contradicciones entre documentos.
- [ ] La base de datos está documentada como NoSQL en Azure con proveedor pendiente.
- [ ] El backend está documentado como monolito modular.
- [ ] Ninguna tarea aparece como completada sin evidencia.
- [ ] Los criterios de aceptación de `spec.md` son verificables.
- [ ] Los subagentes y skills respetan la constitución.
- [ ] La estructura `stages/` es coherente con `plan.md` y `task.md` raíz.

---

### TAREA-002

| Campo | Valor |
|-------|-------|
| **ID** | TAREA-002 |
| **Título** | Revisión y aprobación de la documentación SDD por el responsable del proyecto |
| **Etapa** | 01 |
| **Estado** | PENDIENTE |
| **Referencia** | `plan.md` Fase 1, `constitution.md` sección 13 |

**Descripción:**  
Someter los documentos SDD a revisión por parte del responsable del proyecto (profesor). Recoger observaciones, resolver conflictos y obtener aprobación formal antes de avanzar a la Etapa 02.

**Objetivo:**  
Obtener aprobación explícita de la especificación de arquitectura base.

**Dependencias:**  
- TAREA-001 completada.

**Criterios de aceptación:**
- [ ] Los documentos han sido presentados al responsable del proyecto.
- [ ] Las observaciones recibidas han sido incorporadas o registradas.
- [ ] Se ha recibido aprobación formal de `spec.md`.
- [ ] La aprobación está registrada en `memoria.md`.

---

### TAREA-003

| Campo | Valor |
|-------|-------|
| **ID** | TAREA-003 |
| **Título** | Resolución de decisiones bloqueantes para la Etapa 02 |
| **Etapa** | 01 |
| **Estado** | PENDIENTE |
| **Referencia** | `plan.md` Fase 1, `memoria.md` sección 5 |

**Descripción:**  
Identificar y resolver las decisiones que bloquean el inicio de la Etapa 02. En particular, obtener una decisión sobre la estructura definitiva de capas de la solución .NET (DEC-005).

**Objetivo:**  
Desbloquear el avance a la Etapa 02.

**Dependencias:**  
- TAREA-002 completada.

**Criterios de aceptación:**
- [ ] DEC-005 (estructura de capas) está marcada como confirmada en `memoria.md`.
- [ ] Las demás decisiones bloqueantes están documentadas con su estado actualizado.

---

*Los identificadores de tareas son estables y no se reutilizan. La versión raíz de este listado se conserva en `task.md`.*
