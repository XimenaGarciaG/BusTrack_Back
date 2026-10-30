# task.md — Etapa 10: Incorporación de especificaciones funcionales

**Versión:** 1.0.0  
**Estado:** Activo  
**Última actualización:** 2026-10-29  
**Etapa:** 10  
**Referencia normativa:** [`constitution.md`](../../constitution.md) | [`plan.md`](../../plan.md) | [`task.md`](../../task.md)

> Ninguna tarea puede marcarse como `COMPLETADA` sin evidencia verificable.

---

## Resumen de tareas

| ID | Título | Estado |
|----|--------|--------|
| — | Sin tareas definidas | — |

> **Bloqueo:** esta etapa requiere que las Etapas 01 a 09 estén completadas y que existan especificaciones funcionales aprobadas. No se crean tareas con identificadores hasta recibir los requisitos.

---

## 1. Condiciones para crear tareas

Antes de crear una tarea en esta etapa debe existir:

- [ ] Un requisito funcional recibido y revisado.
- [ ] Una especificación `spec-{módulo}.md` aprobada.
- [ ] Las decisiones de diseño registradas en `memoria.md`.
- [ ] Trazabilidad explícita entre requisito, especificación y tarea.
- [ ] Criterios de aceptación verificables definidos.

## 2. Convención de identificadores

Las tareas de esta etapa continuarán la secuencia estable a partir de `TAREA-021`, sin reutilizar identificadores eliminados.

## 3. Plantilla de tarea

```markdown
### TAREA-###

| Campo | Valor |
|-------|-------|
| **ID** | TAREA-### |
| **Título** | ... |
| **Etapa** | 10 |
| **Estado** | PENDIENTE |
| **Referencia** | `spec-{módulo}.md` sección ... |

**Descripción:** ...

**Objetivo:** ...

**Dependencias:** ...

**Criterios de aceptación:**
- [ ] ...
```

---

*Las tareas de esta etapa se crearán cuando se reciban y aprueben los requisitos funcionales específicos.*
