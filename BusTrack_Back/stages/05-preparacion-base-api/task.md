# task.md — Etapa 05: Preparación de la base de la API

**Versión:** 1.0.0  
**Estado:** Activo  
**Última actualización:** 2026-10-29  
**Etapa:** 05  
**Referencia normativa:** [`constitution.md`](../../constitution.md) | [`plan.md`](../../plan.md) | [`task.md`](../../task.md)

> Ninguna tarea puede marcarse como `COMPLETADA` sin evidencia verificable.

---

## Resumen de tareas

| ID | Título | Estado |
|----|--------|--------|
| TAREA-010 | Creación de la estructura de proyectos .NET | BLOQUEADA |
| TAREA-011 | Configuración del enrutamiento y versionado de la API | BLOQUEADA |
| TAREA-012 | Implementación del middleware de manejo centralizado de errores | BLOQUEADA |
| TAREA-013 | Implementación del endpoint de health check | BLOQUEADA |
| TAREA-014 | Configuración del registro estructurado | BLOQUEADA |

---

### TAREA-010

| Campo | Valor |
|-------|-------|
| **ID** | TAREA-010 |
| **Título** | Creación de la estructura de proyectos .NET |
| **Etapa** | 05 |
| **Estado** | BLOQUEADA |
| **Bloqueo** | Requiere TAREA-004 y TAREA-005 completadas |
| **Referencia** | `plan.md` Fase 5, `spec.md` sección 4 |

**Descripción:**  
Crear la estructura de proyectos .NET aprobada en la Etapa 02. Incluye crear los proyectos de cada capa con sus referencias correctas.

**Objetivo:**  
Tener la estructura base del código del monolito modular lista para recibir implementaciones.

**Dependencias:**  
- TAREA-005 completada.
- TAREA-002 completada (aprobación de `spec.md`).

**Criterios de aceptación:**
- [ ] Los proyectos de cada capa existen en la solución.
- [ ] Las referencias entre proyectos son correctas (sin ciclos, siguiendo inversión de dependencias).
- [ ] La solución compila sin errores.
- [ ] AC-ARCH-01 verificado.

---

### TAREA-011

| Campo | Valor |
|-------|-------|
| **ID** | TAREA-011 |
| **Título** | Configuración del enrutamiento y versionado de la API |
| **Etapa** | 05 |
| **Estado** | BLOQUEADA |
| **Bloqueo** | Requiere TAREA-010 completada |
| **Referencia** | `plan.md` Fase 5, `spec.md` secciones 7 y 8 |

**Descripción:**  
Configurar el enrutamiento de ASP.NET Core para que todas las rutas de la API usen el prefijo `/api/v1/`. Establecer las convenciones de nomenclatura de rutas.

**Objetivo:**  
Implementar el versionado de API acordado.

**Dependencias:**  
- TAREA-010 completada.

**Criterios de aceptación:**
- [ ] El prefijo `/api/v1/` está configurado en todas las rutas.
- [ ] AC-ARCH-03 verificado.

---

### TAREA-012

| Campo | Valor |
|-------|-------|
| **ID** | TAREA-012 |
| **Título** | Implementación del middleware de manejo centralizado de errores |
| **Etapa** | 05 |
| **Estado** | BLOQUEADA |
| **Bloqueo** | Requiere TAREA-010 completada y DEC-010 resuelta |
| **Referencia** | `plan.md` Fase 5, `spec.md` sección 12 |

**Descripción:**  
Implementar el middleware de ASP.NET Core para el manejo centralizado de excepciones no controladas. Devolver respuestas de error estructuradas sin revelar detalles internos.

**Objetivo:**  
Garantizar que los errores no controlados se manejen de forma centralizada y consistente.

**Dependencias:**  
- TAREA-010 completada.
- DEC-010 resuelta (formato de respuestas de error).

**Criterios de aceptación:**
- [ ] Los errores no controlados devuelven respuestas JSON estructuradas.
- [ ] Los detalles internos del sistema no se exponen en las respuestas.
- [ ] AC-ARCH-08 verificado.

---

### TAREA-013

| Campo | Valor |
|-------|-------|
| **ID** | TAREA-013 |
| **Título** | Implementación del endpoint de health check |
| **Etapa** | 05 |
| **Estado** | BLOQUEADA |
| **Bloqueo** | Requiere TAREA-011 completada |
| **Referencia** | `plan.md` Fase 5, `spec.md` sección 13 |

**Descripción:**  
Implementar el endpoint `/health` usando el sistema de health checks de ASP.NET Core. Verificar la conectividad con dependencias críticas cuando estén disponibles.

**Objetivo:**  
Disponer de un mecanismo estándar de verificación de salud de la aplicación.

**Dependencias:**  
- TAREA-011 completada.

**Criterios de aceptación:**
- [ ] `GET /health` retorna código 200 cuando el servicio está operativo.
- [ ] AC-ARCH-07 verificado.

---

### TAREA-014

| Campo | Valor |
|-------|-------|
| **ID** | TAREA-014 |
| **Título** | Configuración del registro estructurado |
| **Etapa** | 05 |
| **Estado** | BLOQUEADA |
| **Bloqueo** | Requiere TAREA-010 completada |
| **Referencia** | `plan.md` Fase 5, `spec.md` sección 13 |

**Descripción:**  
Configurar el registro estructurado usando `ILogger<T>` como abstracción. Asegurarse de que los niveles de logging están correctamente configurados por entorno.

**Objetivo:**  
Disponer de un sistema de registro estructurado desde el inicio.

**Dependencias:**  
- TAREA-010 completada.

**Criterios de aceptación:**
- [ ] `ILogger<T>` está configurado e inyectado correctamente.
- [ ] Los niveles de logging son apropiados por entorno.
- [ ] No se registran datos personales ni secretos.

---

*Los identificadores de tareas son estables y no se reutilizan. La versión raíz de este listado se conserva en `task.md`.*
