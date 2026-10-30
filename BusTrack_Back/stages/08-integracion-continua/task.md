# task.md — Etapa 08: Integración continua

**Versión:** 1.0.0  
**Estado:** Activo  
**Última actualización:** 2026-10-29  
**Etapa:** 08  
**Referencia normativa:** [`constitution.md`](../../constitution.md) | [`plan.md`](../../plan.md) | [`task.md`](../../task.md)

> Ninguna tarea puede marcarse como `COMPLETADA` sin evidencia verificable.

---

## Resumen de tareas

| ID | Título | Estado |
|----|--------|--------|
| TAREA-019 | Configuración del pipeline de integración continua | BLOQUEADA |

---

### TAREA-019

| Campo | Valor |
|-------|-------|
| **ID** | TAREA-019 |
| **Título** | Configuración del pipeline de integración continua |
| **Etapa** | 08 |
| **Estado** | BLOQUEADA |
| **Bloqueo** | Requiere TAREA-018 completada y DEC-006 resuelta |
| **Referencia** | `plan.md` Fase 8 |

**Descripción:**  
Configurar el pipeline de CI con la herramienta seleccionada en DEC-006. El pipeline debe compilar el proyecto y ejecutar todas las pruebas automáticamente.

**Objetivo:**  
Automatizar la validación de calidad en cada cambio del código.

**Dependencias:**  
- TAREA-018 completada.
- DEC-006 resuelta.

**Criterios de aceptación:**
- [ ] El pipeline compila y prueba automáticamente en cada commit o PR.
- [ ] El pipeline falla si alguna prueba no pasa.

---

*Los identificadores de tareas son estables y no se reutilizan. La versión raíz de este listado se conserva en `task.md`.*
