# charts.md — Etapa 05: Preparación de la base de la API

**Versión:** 1.0.0  
**Estado:** Activo  
**Última actualización:** 2026-10-29  
**Etapa:** 05  
**Referencia:** [`plan.md`](./plan.md) | [`task.md`](./task.md)

> Diagramas de la arquitectura base. La estructura de capas está pendiente de aprobación (DEC-005).

---

## 1. Flujo de la etapa

```mermaid
flowchart TD
    A["Inicio · Etapa 05"] --> B["TAREA-010<br/>Crear proyectos .NET"]
    B --> C["TAREA-011<br/>Rutas /api/v1/"]
    B --> D["TAREA-012<br/>Middleware de errores"]
    B --> E["TAREA-013<br/>Endpoint /health"]
    B --> F["TAREA-014<br/>Registro estructurado"]
    C --> G["Pruebas AC-ARCH-01..12"]
    D --> G
    E --> G
    F --> G
    G --> H{"¿Todos los criterios<br/>pasan?"}
    H -- "No" --> B
    H -- "Sí" --> I["Fin · habilitar Etapas 06 y 07"]
```

## 2. Flujo de una solicitud

```mermaid
sequenceDiagram
    participant C as Cliente
    participant API as API Layer
    participant APP as Application Layer
    participant DOM as Domain Layer
    participant INF as Infrastructure
    participant DB as NoSQL Azure

    C->>API: HTTPS + JSON
    API->>API: Validar y autenticar
    API->>APP: Delegar caso de uso
    APP->>DOM: Usar interfaces de repositorio
    DOM-->>APP: Contratos
    APP->>INF: Implementación inyectada
    INF->>DB: Consulta
    DB-->>INF: Documento
    INF-->>APP: Entidad
    APP-->>API: Resultado
    API-->>C: JSON + código HTTP
```

## 3. Capas y dependencias

```mermaid
flowchart LR
    API["API"]
    APP["Application"]
    DOM["Domain"]
    INF["Infrastructure"]

    API --> APP
    APP --> DOM
    INF --> DOM
```

## 4. Cobertura de criterios de aceptación

| Criterio | Tarea |
|----------|-------|
| AC-ARCH-01, AC-ARCH-02 | TAREA-010 |
| AC-ARCH-03 | TAREA-011 |
| AC-ARCH-08 | TAREA-012 |
| AC-ARCH-07 | TAREA-013 |
| AC-ARCH-05, AC-ARCH-06, AC-ARCH-11, AC-ARCH-12 | TAREA-010 a TAREA-014 |
| AC-ARCH-09 | Etapa 04 / TAREA-009 |
| AC-ARCH-10 | Etapa 07 / TAREA-018 |
| AC-ARCH-04 | Pruebas de integración |

## 5. Estados de las tareas

```mermaid
stateDiagram-v2
    [*] --> BLOQUEADA
    BLOQUEADA --> PENDIENTE: dependencias resueltas
    PENDIENTE --> EN_PROGRESO: inicia implementación
    EN_PROGRESO --> BLOQUEADA: falta decisión
    EN_PROGRESO --> COMPLETADA: criterios verificados
    COMPLETADA --> [*]
```
