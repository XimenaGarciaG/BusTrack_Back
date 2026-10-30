# plan.md — Etapa 03: Selección y aprobación del servicio NoSQL de Azure

**Versión:** 1.0.0  
**Estado:** 🔴 BLOQUEADA — Requiere aprobación de la Etapa 01  
**Última actualización:** 2026-10-29  
**Etapa:** 03  
**Referencia normativa:** [`constitution.md`](../../constitution.md) | [`spec.md`](../../spec.md) | [`plan.md`](../../plan.md)

> Esta etapa evalúa y documenta opciones. No autoriza crear recursos en Azure ni implementar repositorios.

---

## 1. Objetivo

Evaluar, seleccionar y documentar el proveedor de base de datos NoSQL en Azure.

## 2. Estado y bloqueos

| Campo | Valor |
|-------|-------|
| Estado | 🔴 BLOQUEADA |
| Dependencias | Etapa 01 aprobada; información suficiente sobre los candidatos |
| Decisión que resuelve | DEC-001 — Proveedor NoSQL en Azure |
| Documentos de la etapa | [`plan.md`](./plan.md) · [`charts.md`](./charts.md) · [`task.md`](./task.md) |

## 3. Actividades previstas

1. Evaluar los candidatos NoSQL en Azure con los criterios CRIT-DB-01 a CRIT-DB-11.
2. Documentar la evaluación comparativa de candidatos.
3. Proponer un proveedor con justificación técnica.
4. Obtener aprobación formal de la selección.
5. Registrar la decisión en `memoria.md` como confirmada.

## 4. Entregables esperados

- Documento de evaluación comparativa de proveedores NoSQL.
- Proveedor seleccionado y aprobado (DEC-001 resuelta).
- Registro actualizado en `memoria.md`.

## 5. Criterios de salida

- DEC-001 marcada como confirmada en `memoria.md`.
- La selección tiene justificación documentada para cada criterio de evaluación.
- El proveedor seleccionado tiene SDK oficial para .NET disponible.

## 6. Trazabilidad

| Elemento | Referencia |
|----------|------------|
| Fase del plan general | `plan.md` — Fase 3 |
| Tareas | `TAREA-006`, `TAREA-007` |
| Criterios de evaluación | CRIT-DB-01 a CRIT-DB-11 (`memoria.md` sección 4) |
| Decisión resuelta | DEC-001 |

---

*La selección del proveedor no se asume en esta etapa. Hasta que DEC-001 esté confirmada, la Etapa 04 permanece bloqueada.*
