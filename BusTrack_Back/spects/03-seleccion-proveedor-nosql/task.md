# task.md — Etapa 03: Selección y aprobación del servicio NoSQL de Azure

**Versión:** 1.0.0  
**Estado:** Activo  
**Última actualización:** 2026-10-29  
**Etapa:** 03  
**Referencia normativa:** [`constitution.md`](../../constitution.md) | [`plan.md`](../../plan.md) | [`task.md`](../../task.md)

> Ninguna tarea puede marcarse como `COMPLETADA` sin evidencia verificable.

---

## Resumen de tareas

| ID | Título | Estado |
|----|--------|--------|
| TAREA-006 | Evaluación comparativa de proveedores NoSQL en Azure | PENDIENTE |
| TAREA-007 | Selección y aprobación del proveedor NoSQL (DEC-001) | BLOQUEADA |

---

### TAREA-006

| Campo | Valor |
|-------|-------|
| **ID** | TAREA-006 |
| **Título** | Evaluación comparativa de proveedores NoSQL en Azure |
| **Etapa** | 03 |
| **Estado** | PENDIENTE |
| **Referencia** | `plan.md` Fase 3, `memoria.md` sección 4, `spec.md` sección 10 |

**Descripción:**  
Evaluar los candidatos de base de datos NoSQL disponibles en Azure aplicando los criterios CRIT-DB-01 a CRIT-DB-11 definidos en `memoria.md`. Producir un documento comparativo que justifique cada candidato en cada criterio.

**Objetivo:**  
Tener una base de información suficiente para seleccionar el proveedor con criterios objetivos.

**Dependencias:**  
- TAREA-001 completada (documentación base revisada).

**Criterios de aceptación:**
- [ ] Se han evaluado al menos dos candidatos.
- [ ] Cada candidato ha sido evaluado contra los once criterios definidos.
- [ ] El documento de evaluación está disponible en el repositorio.

---

### TAREA-007

| Campo | Valor |
|-------|-------|
| **ID** | TAREA-007 |
| **Título** | Selección y aprobación del proveedor NoSQL (DEC-001) |
| **Etapa** | 03 |
| **Estado** | BLOQUEADA |
| **Bloqueo** | Requiere TAREA-006 completada |
| **Referencia** | `plan.md` Fase 3, `memoria.md` sección 5 (DEC-001) |

**Descripción:**  
Proponer un proveedor NoSQL basándose en la evaluación comparativa. Obtener aprobación formal y registrar la decisión en `memoria.md`.

**Objetivo:**  
Resolver DEC-001 y desbloquear las Etapas 04 y 05.

**Dependencias:**  
- TAREA-006 completada.

**Criterios de aceptación:**
- [ ] Un proveedor ha sido propuesto con justificación documentada.
- [ ] La selección ha sido aprobada formalmente.
- [ ] DEC-001 está marcada como confirmada en `memoria.md`.

---

*Los identificadores de tareas son estables y no se reutilizan. La versión raíz de este listado se conserva en `task.md`.*
