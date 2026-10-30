# charts.md — Etapa 09: Preparación del despliegue en Azure

**Versión:** 1.0.0  
**Estado:** Activo  
**Última actualización:** 2026-10-29  
**Etapa:** 09  
**Referencia:** [`plan.md`](./plan.md) | [`task.md`](./task.md)

> Diagramas de despliegue. El servicio de alojamiento concreto depende de DEC-007.

---

## 1. Flujo de la etapa

```mermaid
flowchart TD
    A["Inicio · Etapa 09"] --> B["Seleccionar alojamiento<br/>DEC-007"]
    B --> C["Configurar CD"]
    C --> D["Verificar secretos<br/>en Azure"]
    D --> E["TAREA-020<br/>Primer despliegue"]
    E --> F{"¿/health retorna 200?"}
    F -- "No" --> G["Diagnosticar despliegue"]
    G --> E
    F -- "Sí" --> H["Documentar proceso"]
    H --> I["Fin · habilitar Etapa 10"]
```

## 2. Topología de despliegue (propuesta)

```mermaid
flowchart TB
    U["Usuarios<br/>Flutter / Angular"]
    FE["HTTPS"]
    APP["Backend BusTrack<br/>ASP.NET Core en Azure"]
    SEC["Servicio de secretos<br/>DEC-003"]
    DB[("NoSQL en Azure<br/>DEC-001")]
    OBS["Observabilidad<br/>DEC-004"]

    U --> FE --> APP
    APP --> DB
    APP --> SEC
    APP --> OBS
```

## 3. Pipeline de entrega

```mermaid
sequenceDiagram
    participant VCS as Repositorio
    participant CI as CI
    participant CD as CD
    participant AZ as Azure

    VCS->>CI: Commit / merge
    CI->>CI: Compilar y probar
    CI->>CD: Artefacto aprobado
    CD->>AZ: Desplegar
    AZ-->>CD: Estado del despliegue
    CD->>AZ: Verificar /health
```

## 4. Dependencias con otras etapas

```mermaid
flowchart LR
    E08["08 · Integración continua"]
    E09["09 · Despliegue"]
    E10["10 · Funcionalidades"]

    E08 --> E09
    E09 --> E10
```

## 5. Estados de las tareas

```mermaid
stateDiagram-v2
    [*] --> BLOQUEADA
    BLOQUEADA --> PENDIENTE: DEC-007 resuelta y Azure disponible
    PENDIENTE --> EN_PROGRESO: despliegue en curso
    EN_PROGRESO --> COMPLETADA: /health verificado
    COMPLETADA --> [*]
```
