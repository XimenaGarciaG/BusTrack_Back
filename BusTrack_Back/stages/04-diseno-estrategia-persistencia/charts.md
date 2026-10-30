# charts.md — Etapa 04: Diseño de la estrategia de persistencia

**Versión:** 1.0.0  
**Estado:** Activo  
**Última actualización:** 2026-10-29  
**Etapa:** 04  
**Referencia:** [`plan.md`](./plan.md) | [`task.md`](./task.md)

> Diagramas de diseño. Dependen del proveedor NoSQL aprobado en DEC-001.

---

## 1. Flujo de la etapa

```mermaid
flowchart TD
    A["Inicio · Etapa 04"] --> B["TAREA-008<br/>Modelo de documentos NoSQL"]
    B --> C["Particionado e indexado"]
    C --> D["TAREA-009<br/>Interfaces de repositorio"]
    D --> E{"¿Interfaces libres<br/>del proveedor?"}
    E -- "No" --> F["Abstraer tipos específicos"]
    F --> D
    E -- "Sí" --> G["Aprobación del diseño"]
    G --> H["Fin · habilitar Etapas 05 y 06"]
```

## 2. Ubicación de las abstracciones

```mermaid
flowchart TB
    DOM["Domain<br/>IRepositorio&lt;T&gt;"]
    APP["Application<br/>Casos de uso"]
    INF["Infrastructure<br/>Implementación NoSQL"]
    DB[("Base de datos NoSQL<br/>Azure")]

    APP --> DOM
    INF -- "implementa" --> DOM
    INF --> DB
```

## 3. Dependencias con otras etapas

```mermaid
flowchart LR
    E02["02 · Diseño .NET"]
    E03["03 · Selección NoSQL"]
    E04["04 · Persistencia"]
    E05["05 · Base API"]

    E02 --> E04
    E03 --> E04
    E04 -.-> E05
```

## 4. Estados de las tareas

```mermaid
stateDiagram-v2
    [*] --> BLOQUEADA
    BLOQUEADA --> PENDIENTE: DEC-001 resuelta
    PENDIENTE --> EN_PROGRESO: inicia diseño
    EN_PROGRESO --> COMPLETADA: diseño aprobado
    COMPLETADA --> [*]
```

## 5. Mapa de criterios de salida

| Criterio de salida | Tarea asociada | Evidencia |
|--------------------|----------------|-----------|
| Modelo de documentos definido | TAREA-008 | Documento de modelo |
| Particionado e indexado | TAREA-008 | Documento de estrategia |
| Interfaces de repositorio | TAREA-009 | Diagrama y firmas |
