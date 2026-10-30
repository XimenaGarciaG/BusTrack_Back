# task.md — Tareas Trazables del Backend de BusTrack

**Versión:** 1.1.0  
**Estado:** Activo  
**Última actualización:** 2026-10-29  
**Referencia normativa:** [`constitution.md`](./constitution.md) | [`plan.md`](./plan.md)

> **Regla:** Ninguna tarea puede marcarse como `COMPLETADA` sin evidencia verificable. Las tareas de implementación y despliegue deben permanecer en `PENDIENTE` o `BLOQUEADA` hasta que la fase correspondiente sea aprobada.

---

## Documentación por etapas

Este documento se conserva como índice general de tareas y fuente de los identificadores estables `TAREA-###`. El desglose por etapa vive en `stages/`, donde cada etapa incluye su propio `plan.md`, `charts.md` y `task.md`.

| Etapa | Carpeta | Tareas |
|-------|---------|--------|
| 01 | [`stages/01-validacion-documentacion-sdd/`](./stages/01-validacion-documentacion-sdd/task.md) | TAREA-001 a TAREA-003 |
| 02 | [`stages/02-diseno-estructura-solucion-net/`](./stages/02-diseno-estructura-solucion-net/task.md) | TAREA-004 a TAREA-005 |
| 03 | [`stages/03-seleccion-proveedor-nosql/`](./stages/03-seleccion-proveedor-nosql/task.md) | TAREA-006 a TAREA-007 |
| 04 | [`stages/04-diseno-estrategia-persistencia/`](./stages/04-diseno-estrategia-persistencia/task.md) | TAREA-008 a TAREA-009 |
| 05 | [`stages/05-preparacion-base-api/`](./stages/05-preparacion-base-api/task.md) | TAREA-010 a TAREA-014 |
| 06 | [`stages/06-configuracion-y-seguridad/`](./stages/06-configuracion-y-seguridad/task.md) | TAREA-015 a TAREA-017 |
| 07 | [`stages/07-estrategia-de-pruebas/`](./stages/07-estrategia-de-pruebas/task.md) | TAREA-018 |
| 08 | [`stages/08-integracion-continua/`](./stages/08-integracion-continua/task.md) | TAREA-019 |
| 09 | [`stages/09-despliegue-en-azure/`](./stages/09-despliegue-en-azure/task.md) | TAREA-020 |
| 10 | [`stages/10-especificaciones-funcionales/`](./stages/10-especificaciones-funcionales/task.md) | Por definir (TAREA-021+) |

> Índice general: [`stages/README.md`](./stages/README.md). Los documentos de `stages/` desglosan este listado; no sustituyen la trazabilidad raíz.

---

## Convenciones de estado

| Estado | Descripción |
|--------|-------------|
| `PENDIENTE` | Lista para iniciarse cuando corresponda; sin bloqueos |
| `BLOQUEADA` | No puede iniciarse; tiene dependencias no resueltas |
| `EN_PROGRESO` | Ha comenzado efectivamente (con evidencia) |
| `COMPLETADA` | Finalizada con evidencia verificable |

---

## Fase 1 — Validación de la documentación SDD

---

### TAREA-001

| Campo | Valor |
|-------|-------|
| **ID** | TAREA-001 |
| **Título** | Revisión de coherencia interna de los documentos SDD |
| **Fase** | Fase 1 |
| **Estado** | PENDIENTE |
| **Referencia** | `plan.md` Fase 1, `spec.md` sección 18 |

**Descripción:**  
Revisar que todos los documentos SDD generados (`constitution.md`, `AGENTS.md`, `memoria.md`, `spec.md`, `plan.md`, `task.md`) sean coherentes entre sí. Verificar que no existan contradicciones entre principios, decisiones y restricciones.

**Objetivo:**  
Garantizar la coherencia documental antes de someter los documentos a revisión externa.

**Dependencias:**  
Ninguna. Es la primera tarea de la Fase 1.

**Criterios de aceptación:**
- [ ] Todos los documentos están presentes en el repositorio.
- [ ] No se identifican contradicciones entre documentos.
- [ ] La base de datos está documentada como NoSQL en Azure con proveedor pendiente.
- [ ] El backend está documentado como monolito modular.
- [ ] Ninguna tarea aparece como completada sin evidencia.
- [ ] Los criterios de aceptación de `spec.md` son verificables.
- [ ] Los subagentes y skills respetan la constitución.

---

### TAREA-002

| Campo | Valor |
|-------|-------|
| **ID** | TAREA-002 |
| **Título** | Revisión y aprobación de la documentación SDD por el responsable del proyecto |
| **Fase** | Fase 1 |
| **Estado** | PENDIENTE |
| **Referencia** | `plan.md` Fase 1, `constitution.md` sección 13 |

**Descripción:**  
Someter los documentos SDD a revisión por parte del responsable del proyecto (profesor). Recoger observaciones, resolver conflictos y obtener aprobación formal antes de avanzar a la Fase 2.

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
| **Título** | Resolución de decisiones bloqueantes para la Fase 2 |
| **Fase** | Fase 1 |
| **Estado** | PENDIENTE |
| **Referencia** | `plan.md` Fase 1, `memoria.md` sección 5 |

**Descripción:**  
Identificar y resolver las decisiones que bloquean el inicio de la Fase 2. En particular, obtener una decisión sobre la estructura definitiva de capas de la solución .NET (DEC-005).

**Objetivo:**  
Desbloquear el avance a la Fase 2.

**Dependencias:**  
- TAREA-002 completada.

**Criterios de aceptación:**
- [ ] DEC-005 (estructura de capas) está marcada como confirmada en `memoria.md`.
- [ ] Las demás decisiones bloqueantes están documentadas con su estado actualizado.

---

## Fase 2 — Diseño de la estructura de la solución .NET

---

### TAREA-004

| Campo | Valor |
|-------|-------|
| **ID** | TAREA-004 |
| **Título** | Propuesta de estructura de proyectos .NET |
| **Fase** | Fase 2 |
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
| **Fase** | Fase 2 |
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

## Fase 3 — Selección del proveedor NoSQL en Azure

---

### TAREA-006

| Campo | Valor |
|-------|-------|
| **ID** | TAREA-006 |
| **Título** | Evaluación comparativa de proveedores NoSQL en Azure |
| **Fase** | Fase 3 |
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
| **Fase** | Fase 3 |
| **Estado** | BLOQUEADA |
| **Bloqueo** | Requiere TAREA-006 completada |
| **Referencia** | `plan.md` Fase 3, `memoria.md` sección 5 (DEC-001) |

**Descripción:**  
Proponer un proveedor NoSQL basándose en la evaluación comparativa. Obtener aprobación formal y registrar la decisión en `memoria.md`.

**Objetivo:**  
Resolver DEC-001 y desbloquear las Fases 4 y 5.

**Dependencias:**  
- TAREA-006 completada.

**Criterios de aceptación:**
- [ ] Un proveedor ha sido propuesto con justificación documentada.
- [ ] La selección ha sido aprobada formalmente.
- [ ] DEC-001 está marcada como confirmada en `memoria.md`.

---

## Fase 4 — Diseño de la estrategia de persistencia

---

### TAREA-008

| Campo | Valor |
|-------|-------|
| **ID** | TAREA-008 |
| **Título** | Diseño del modelo de documentos NoSQL |
| **Fase** | Fase 4 |
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
| **Fase** | Fase 4 |
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

## Fase 5 — Preparación de la base de la API

---

### TAREA-010

| Campo | Valor |
|-------|-------|
| **ID** | TAREA-010 |
| **Título** | Creación de la estructura de proyectos .NET |
| **Fase** | Fase 5 |
| **Estado** | BLOQUEADA |
| **Bloqueo** | Requiere TAREA-004 y TAREA-005 completadas |
| **Referencia** | `plan.md` Fase 5, `spec.md` sección 4 |

**Descripción:**  
Crear la estructura de proyectos .NET aprobada en la Fase 2. Incluye crear los proyectos de cada capa con sus referencias correctas.

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
| **Fase** | Fase 5 |
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
| **Fase** | Fase 5 |
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
| **Fase** | Fase 5 |
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
| **Fase** | Fase 5 |
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

## Fase 6 — Configuración y seguridad

---

### TAREA-015

| Campo | Valor |
|-------|-------|
| **ID** | TAREA-015 |
| **Título** | Configuración de la jerarquía de configuración por entorno |
| **Fase** | Fase 6 |
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
| **Fase** | Fase 6 |
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
| **Fase** | Fase 6 |
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

## Fases 7, 8 y 9 — Pruebas, CI/CD y Despliegue

---

### TAREA-018

| Campo | Valor |
|-------|-------|
| **ID** | TAREA-018 |
| **Título** | Selección de herramientas de prueba y configuración de proyectos de prueba |
| **Fase** | Fase 7 |
| **Estado** | BLOQUEADA |
| **Bloqueo** | Requiere TAREA-010 completada y DEC-008/DEC-009 resueltas |
| **Referencia** | `plan.md` Fase 7, `spec.md` sección 14 |

**Descripción:**  
Resolver DEC-008 y DEC-009. Crear los proyectos de prueba con las herramientas seleccionadas. Implementar las pruebas unitarias e integración de la arquitectura base.

**Objetivo:**  
Establecer la infraestructura de pruebas del proyecto.

**Dependencias:**  
- TAREA-010 completada.
- DEC-008 y DEC-009 resueltas.

**Criterios de aceptación:**
- [ ] Proyectos de prueba creados.
- [ ] Las pruebas de dominio pasan sin infraestructura real (AC-ARCH-10).
- [ ] Los criterios de aceptación de arquitectura están validados mediante pruebas.

---

### TAREA-019

| Campo | Valor |
|-------|-------|
| **ID** | TAREA-019 |
| **Título** | Configuración del pipeline de integración continua |
| **Fase** | Fase 8 |
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

### TAREA-020

| Campo | Valor |
|-------|-------|
| **ID** | TAREA-020 |
| **Título** | Primer despliegue de la API base en Azure |
| **Fase** | Fase 9 |
| **Estado** | BLOQUEADA |
| **Bloqueo** | Requiere TAREA-019 completada y DEC-007 resuelta |
| **Referencia** | `plan.md` Fase 9 |

**Descripción:**  
Configurar el despliegue en Azure y realizar el primer despliegue de la API base en el entorno de desarrollo o staging. Verificar el funcionamiento del endpoint `/health` en el entorno desplegado.

**Objetivo:**  
Validar que el backend puede desplegarse correctamente en Azure.

**Dependencias:**  
- TAREA-019 completada.
- DEC-007 resuelta.
- Suscripción y recursos de Azure disponibles.

**Criterios de aceptación:**
- [ ] La API está desplegada en Azure.
- [ ] `GET /health` retorna 200 en el entorno de Azure.
- [ ] Los secretos se gestionan mediante el servicio seleccionado.

---

## Resumen de tareas y estados

| ID | Título | Fase | Estado |
|----|--------|------|--------|
| TAREA-001 | Revisión de coherencia interna de documentos SDD | 1 | PENDIENTE |
| TAREA-002 | Revisión y aprobación por el responsable del proyecto | 1 | PENDIENTE |
| TAREA-003 | Resolución de decisiones bloqueantes para la Fase 2 | 1 | PENDIENTE |
| TAREA-004 | Propuesta de estructura de proyectos .NET | 2 | BLOQUEADA |
| TAREA-005 | Definición de convenciones de nomenclatura | 2 | BLOQUEADA |
| TAREA-006 | Evaluación comparativa de proveedores NoSQL | 3 | PENDIENTE |
| TAREA-007 | Selección y aprobación del proveedor NoSQL | 3 | BLOQUEADA |
| TAREA-008 | Diseño del modelo de documentos NoSQL | 4 | BLOQUEADA |
| TAREA-009 | Diseño de interfaces de repositorio del dominio | 4 | BLOQUEADA |
| TAREA-010 | Creación de la estructura de proyectos .NET | 5 | BLOQUEADA |
| TAREA-011 | Configuración del enrutamiento y versionado de la API | 5 | BLOQUEADA |
| TAREA-012 | Implementación del middleware de manejo de errores | 5 | BLOQUEADA |
| TAREA-013 | Implementación del endpoint de health check | 5 | BLOQUEADA |
| TAREA-014 | Configuración del registro estructurado | 5 | BLOQUEADA |
| TAREA-015 | Configuración de la jerarquía de configuración por entorno | 6 | BLOQUEADA |
| TAREA-016 | Integración del servicio de gestión de secretos | 6 | BLOQUEADA |
| TAREA-017 | Implementación del mecanismo de autenticación y autorización | 6 | BLOQUEADA |
| TAREA-018 | Configuración de proyectos de prueba | 7 | BLOQUEADA |
| TAREA-019 | Configuración del pipeline de CI | 8 | BLOQUEADA |
| TAREA-020 | Primer despliegue en Azure | 9 | BLOQUEADA |

---

*Las tareas de la Fase 10 (especificaciones funcionales) se crearán cuando se reciban y aprueben los requisitos funcionales específicos.*
