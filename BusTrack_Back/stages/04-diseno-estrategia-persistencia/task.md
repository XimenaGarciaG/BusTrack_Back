# task.md — Etapa 04: Diseño de la estrategia de persistencia

**Versión:** 1.0.0  
**Estado:** Activo  
**Última actualización:** 2026-10-29  
**Etapa:** 04  
**Referencia normativa:** [`constitution.md`](../../constitution.md) | [`plan.md`](../../plan.md) | [`task.md`](../../task.md)

> Ninguna tarea puede marcarse como `COMPLETADA` sin evidencia verificable.

---

## Resumen de tareas

| ID | Título | Estado |
|----|--------|--------|
| TAREA-008 | Diseño del modelo de documentos NoSQL | BLOQUEADA |
| TAREA-009 | Diseño de interfaces de repositorio del dominio | BLOQUEADA |

---

### TAREA-008

| Campo | Valor |
|-------|-------|
| **ID** | TAREA-008 |
| **Título** | Diseño del modelo de documentos NoSQL |
| **Etapa** | 04 |
| **Estado** | BLOQUEADA |
| **Bloqueo** | Requiere TAREA-007 completada (DEC-001 resuelta) |
| **Referencia** | `plan.md` Fase 4, `spec.md` sección 10 |

**Descripción:**  
Diseñar el modelo de documentos NoSQL para las entidades del dominio de BusTrack, considerando los patrones de acceso esperados y las capacidades del proveedor seleccionado.

**Objetivo:**  
Contar con un diseño de datos aprobado antes de implementar repositorios.

**Dependencias:**  
- TAREA-007 completada.
- TAREA-004 completada (estructura de capas).

**Criterios de aceptación:**
- [ ] El modelo de documentos está diseñado para las entidades principales.
- [ ] La estrategia de particionado está documentada.
- [ ] La estrategia de indexado está documentada.
- [ ] El diseño ha sido revisado y aprobado.

---

### TAREA-009

| Campo | Valor |
|-------|-------|
| **ID** | TAREA-009 |
| **Título** | Diseño de interfaces de repositorio del dominio |
| **Etapa** | 04 |
| **Estado** | BLOQUEADA |
| **Bloqueo** | Requiere TAREA-008 completada |
| **Referencia** | `plan.md` Fase 4, `spec.md` sección 10 |

**Descripción:**  
Diseñar las interfaces de repositorio que serán definidas en la capa de dominio. Estas interfaces deben reflejar las operaciones de acceso a datos necesarias sin exponer detalles del proveedor.

**Objetivo:**  
Contar con interfaces de repositorio aprobadas antes de implementar la capa de infraestructura.

**Dependencias:**  
- TAREA-008 completada.

**Criterios de aceptación:**
- [ ] Las interfaces de repositorio están diseñadas para las entidades principales.
- [ ] Las interfaces no exponen tipos o conceptos específicos del proveedor NoSQL.
- [ ] El diseño ha sido aprobado.

---

*Los identificadores de tareas son estables y no se reutilizan. La versión raíz de este listado se conserva en `task.md`.*
