# task.md — Etapa 02: Diseño de la estructura de la solución .NET

**Versión:** 1.0.0  
**Estado:** Activo  
**Última actualización:** 2026-10-29  
**Etapa:** 02  
**Referencia normativa:** [`constitution.md`](../../constitution.md) | [`plan.md`](../../plan.md) | [`task.md`](../../task.md)

> Ninguna tarea puede marcarse como `COMPLETADA` sin evidencia verificable.

---

## Resumen de tareas

| ID | Título | Estado |
|----|--------|--------|
| TAREA-004 | Propuesta de estructura de proyectos .NET | BLOQUEADA |
| TAREA-005 | Definición de convenciones de nomenclatura y organización | BLOQUEADA |

---

### TAREA-004

| Campo | Valor |
|-------|-------|
| **ID** | TAREA-004 |
| **Título** | Propuesta de estructura de proyectos .NET |
| **Etapa** | 02 |
| **Estado** | BLOQUEADA |
| **Bloqueo** | Requiere TAREA-003 completada (DEC-005 resuelta) |
| **Referencia** | `plan.md` Fase 2, `spec.md` sección 5 |

**Descripción:**  
Diseñar y documentar la estructura de proyectos .NET del monolito modular, incluyendo nombres de proyectos, referencias entre proyectos, namespaces y organización de carpetas.

**Objetivo:**  
Tener un diseño aprobado de la estructura antes de crear archivos de código.

**Dependencias:**  
- TAREA-003 completada.
- DEC-005 resuelta.

**Criterios de aceptación:**
- [ ] La estructura de proyectos está documentada con justificación.
- [ ] Las dependencias entre proyectos no generan ciclos.
- [ ] La estructura respeta la inversión de dependencias (Domain no depende de Infrastructure).
- [ ] La propuesta ha sido aprobada formalmente.

---

### TAREA-005

| Campo | Valor |
|-------|-------|
| **ID** | TAREA-005 |
| **Título** | Definición de convenciones de nomenclatura y organización |
| **Etapa** | 02 |
| **Estado** | BLOQUEADA |
| **Bloqueo** | Requiere TAREA-004 completada |
| **Referencia** | `plan.md` Fase 2, `constitution.md` sección 5 |

**Descripción:**  
Documentar las convenciones de nomenclatura para namespaces, clases, interfaces, métodos, y la organización de carpetas dentro de cada proyecto .NET.

**Objetivo:**  
Establecer convenciones estables antes de iniciar la codificación.

**Dependencias:**  
- TAREA-004 completada.

**Criterios de aceptación:**
- [ ] Las convenciones de nomenclatura están documentadas.
- [ ] Las convenciones siguen las pautas de .NET y C#.
- [ ] Las convenciones están aprobadas.

---

*Los identificadores de tareas son estables y no se reutilizan. La versión raíz de este listado se conserva en `task.md`.*
