# sdd-consistency-review.md — Skill: Revisión de Coherencia SDD

**Tipo:** Procedimiento reutilizable de revisión  
**Versión:** 1.0.0  
**Estado:** Vigente  
**Referencia normativa:** [`constitution.md`](../constitution.md)

> **Aviso:** Este archivo describe un procedimiento de revisión reutilizable. No es un script ejecutable ni depende de ninguna plataforma específica. Cualquier agente o colaborador puede seguir este procedimiento manualmente.

---

## 1. Objetivo

Verificar que los documentos SDD del repositorio `BusTrack_Back` son coherentes entre sí, están completos según los requisitos de la metodología SDD y no contienen contradicciones con `constitution.md`.

---

## 2. Cuándo utilizarlo

- Al finalizar la generación o actualización de documentos SDD.
- Antes de solicitar revisión externa (al profesor o responsable del proyecto).
- Antes de aprobar el inicio de una nueva fase del plan.
- Cuando se detecta una posible inconsistencia entre documentos.
- Periódicamente durante el desarrollo para detectar desviaciones.

---

## 3. Información de entrada

| Entrada | Descripción | Obligatoria |
|---------|-------------|-------------|
| `constitution.md` | Norma suprema | Sí |
| `AGENTS.md` | Instrucciones operativas | Sí |
| `memoria.md` | Registro de decisiones | Sí |
| `spec.md` | Especificación de arquitectura base | Sí |
| `plan.md` | Plan de implementación | Sí |
| `task.md` | Lista de tareas | Sí |
| `subagents/*.md` | Definiciones de subagentes | Si existen |
| `skills/*.md` | Procedimientos de revisión | Si existen |

---

## 4. Procedimiento paso a paso

### Paso 1: Verificar la presencia de todos los documentos

1. Listar los archivos en la raíz del repositorio.
2. Confirmar que existen: `constitution.md`, `AGENTS.md`, `memoria.md`, `spec.md`, `plan.md`, `task.md`.
3. Registrar cualquier documento faltante como hallazgo.

### Paso 2: Verificar la coherencia de decisiones de arquitectura

Para cada decisión listada en la tabla de historial de `memoria.md`:

1. Verificar que el estado (Confirmado / Propuesto / Pendiente) es correcto.
2. Verificar que ningún otro documento contradice ese estado.
3. En particular:
   - El proveedor NoSQL debe aparecer como **pendiente** en todos los documentos.
   - La arquitectura debe aparecer como **monolito modular** en todos los documentos.
   - La API debe aparecer como **REST con JSON** y **versionado `/api/v1/`** en todos los documentos.
   - La persistencia debe aparecer como **desacoplada** mediante interfaces.

### Paso 3: Verificar la coherencia entre `spec.md` y `plan.md`

1. Verificar que cada fase del plan tiene fundamento en `spec.md`.
2. Verificar que las dependencias entre fases son coherentes con los bloqueos por decisiones pendientes.
3. Verificar que las fases bloqueadas corresponden a decisiones realmente pendientes en `memoria.md`.

### Paso 4: Verificar la coherencia entre `plan.md` y `task.md`

1. Verificar que cada tarea hace referencia a una fase existente en `plan.md`.
2. Verificar que el estado de cada tarea es coherente con el estado de su fase.
3. Verificar que ninguna tarea de implementación tiene estado `COMPLETADA` o `EN_PROGRESO` sin evidencia.
4. Verificar que las tareas `BLOQUEADAS` tienen documentados sus bloqueos.

### Paso 5: Verificar la coherencia entre `constitution.md` y los demás documentos

1. Verificar que `AGENTS.md` es coherente con los principios de `constitution.md`.
2. Verificar que `spec.md` no añade principios que contradigan `constitution.md`.
3. Verificar que los subagentes no tienen actividades prohibidas por `constitution.md`.
4. Verificar que las skills no proponen procedimientos contrarios a la constitución.

### Paso 6: Verificar la ausencia de contenido prohibido

Buscar en todos los documentos:

- [ ] Contraseñas, tokens, claves de API o cadenas de conexión con credenciales.
- [ ] Nombres de proveedores NoSQL específicos marcados como seleccionados (sin aprobación).
- [ ] Endpoints funcionales específicos en `spec.md` (solo se permiten ilustrativos).
- [ ] Fechas inventadas en `plan.md`.
- [ ] Tareas marcadas como completadas sin evidencia.
- [ ] Seguimiento GPS en tiempo real contemplado como funcionalidad del sistema.

### Paso 7: Verificar la completitud de los documentos

| Documento | Sección mínima requerida |
|-----------|--------------------------|
| `constitution.md` | Secciones 1 a 15 |
| `AGENTS.md` | Secciones 1 a 12 |
| `memoria.md` | Secciones 1 a 9 |
| `spec.md` | Secciones 1 a 18 |
| `plan.md` | Fases 1 a 10 |
| `task.md` | Al menos una tarea por fase del plan |

---

## 5. Criterios de aceptación

La revisión resulta en estado **SIN OBSERVACIONES** cuando:

- Todos los documentos requeridos están presentes.
- No se detectan contradicciones entre documentos.
- Ningún documento contiene contenido prohibido.
- Los estados de decisiones en `memoria.md` son coherentes con lo expresado en los demás documentos.
- Los estados de tareas en `task.md` son coherentes con las fases de `plan.md`.
- Los criterios de aceptación de `spec.md` son verificables.

---

## 6. Errores que debe evitar

| Error | Descripción |
|-------|-------------|
| Omitir documentos de la revisión | Todos los documentos listados en la entrada son obligatorios |
| Marcar como coherente sin evidencia | Cada criterio debe verificarse explícitamente |
| Modificar documentos sin documentar el cambio | Cualquier corrección debe registrarse en `memoria.md` |
| Resolver contradicciones arbitrariamente | Las contradicciones deben documentarse, no resolverse sin aprobación |
| Confundir "no hay contradicción detectada" con "es correcto" | La revisión solo puede afirmar lo que pudo verificarse |

---

## 7. Formato esperado del resultado

```markdown
# Resultado de Revisión de Coherencia SDD

**Fecha:** YYYY-MM-DD
**Documentos revisados:** [lista]
**Revisado por:** [agente o colaborador]

## Resumen

Estado general: SIN OBSERVACIONES / CON OBSERVACIONES / CON ERRORES CRÍTICOS

## Hallazgos por paso

### Paso 1: Presencia de documentos
[resultado]

### Paso 2: Coherencia de decisiones de arquitectura
[resultado]

### Paso 3: Coherencia spec.md ↔ plan.md
[resultado]

### Paso 4: Coherencia plan.md ↔ task.md
[resultado]

### Paso 5: Coherencia con constitution.md
[resultado]

### Paso 6: Ausencia de contenido prohibido
[resultado]

### Paso 7: Completitud
[resultado]

## Observaciones y recomendaciones

[Lista de observaciones con referencia al documento y sección afectados]

## Próximos pasos recomendados

[Acciones a tomar antes de considerar la revisión superada]
```

---

*Este procedimiento puede actualizarse siguiendo el proceso de control de cambios de `constitution.md`.*
