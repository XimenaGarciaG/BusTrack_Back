# task.md — Etapa 06: Configuración y seguridad

**Versión:** 1.0.0  
**Estado:** Activo  
**Última actualización:** 2026-10-29  
**Etapa:** 06  
**Referencia normativa:** [`constitution.md`](../../constitution.md) | [`plan.md`](../../plan.md) | [`task.md`](../../task.md)

> Ninguna tarea puede marcarse como `COMPLETADA` sin evidencia verificable.

---

## Resumen de tareas

| ID | Título | Estado |
|----|--------|--------|
| TAREA-015 | Configuración de la jerarquía de configuración por entorno | BLOQUEADA |
| TAREA-016 | Integración del servicio de gestión de secretos (DEC-003) | BLOQUEADA |
| TAREA-017 | Implementación del mecanismo base de autenticación y autorización (DEC-002) | BLOQUEADA |

---

### TAREA-015

| Campo | Valor |
|-------|-------|
| **ID** | TAREA-015 |
| **Título** | Configuración de la jerarquía de configuración por entorno |
| **Etapa** | 06 |
| **Estado** | BLOQUEADA |
| **Bloqueo** | Requiere TAREA-014 completada |
| **Referencia** | `plan.md` Fase 6, `spec.md` sección 9 |

**Descripción:**  
Implementar la jerarquía de configuración de ASP.NET Core para los distintos entornos (Development, Testing, Staging, Production). Asegurarse de que ningún secreto esté en archivos versionados.

**Objetivo:**  
Gestionar la configuración de forma segura y separada por entorno.

**Dependencias:**  
- TAREA-014 completada.

**Criterios de aceptación:**
- [ ] La configuración se carga correctamente por entorno.
- [ ] Ningún secreto está en archivos versionados.
- [ ] AC-ARCH-06 y AC-ARCH-11 verificados.

---

### TAREA-016

| Campo | Valor |
|-------|-------|
| **ID** | TAREA-016 |
| **Título** | Integración del servicio de gestión de secretos (DEC-003) |
| **Etapa** | 06 |
| **Estado** | BLOQUEADA |
| **Bloqueo** | Requiere TAREA-015 completada y DEC-003 resuelta |
| **Referencia** | `plan.md` Fase 6, `constitution.md` sección 8 |

**Descripción:**  
Integrar el servicio de gestión de secretos seleccionado en DEC-003 con el sistema de configuración de ASP.NET Core.

**Objetivo:**  
Gestionar secretos de forma segura en todos los entornos.

**Dependencias:**  
- TAREA-015 completada.
- DEC-003 resuelta.

**Criterios de aceptación:**
- [ ] Los secretos se leen desde el servicio de gestión de secretos.
- [ ] No hay secretos en el repositorio.

---

### TAREA-017

| Campo | Valor |
|-------|-------|
| **ID** | TAREA-017 |
| **Título** | Implementación del mecanismo base de autenticación y autorización (DEC-002) |
| **Etapa** | 06 |
| **Estado** | BLOQUEADA |
| **Bloqueo** | Requiere TAREA-015 completada y DEC-002 resuelta |
| **Referencia** | `plan.md` Fase 6, `spec.md` sección 11 |

**Descripción:**  
Implementar el mecanismo de autenticación seleccionado en DEC-002. Configurar la autorización base para proteger los endpoints.

**Objetivo:**  
Garantizar que todos los endpoints estén protegidos según los principios de seguridad.

**Dependencias:**  
- TAREA-015 completada.
- DEC-002 resuelta.

**Criterios de aceptación:**
- [ ] Los endpoints protegidos devuelven 401 sin autenticación válida.
- [ ] Los endpoints protegidos devuelven 403 sin permisos suficientes.
- [ ] HTTPS está configurado.

---

*Los identificadores de tareas son estables y no se reutilizan. La versión raíz de este listado se conserva en `task.md`.*
