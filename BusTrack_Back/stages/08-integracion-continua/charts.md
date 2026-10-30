# charts.md — Etapa 08: Integración continua

**Versión:** 1.0.0  
**Estado:** Activo  
**Última actualización:** 2026-10-29  
**Etapa:** 08  
**Referencia:** [`plan.md`](./plan.md) | [`task.md`](./task.md)

> Diagramas del pipeline de integración continua. La herramienta concreta depende de DEC-006.

---

## 1. Flujo de la etapa

```mermaid
flowchart TD
    A["Inicio · Etapa 08"] --> B["Seleccionar CI/CD<br/>DEC-006"]
    B --> C["TAREA-019<br/>Crear pipeline"]
    C --> D["Compilar solución"]
    D --> E["Ejecutar pruebas"]
    E --> F{"¿Todas pasan?"}
    F -- "No" --> G["Fallar pipeline<br/>sin artefacto"]
    F -- "Sí" --> H["Generar artefacto"]
    H --> I["Fin · habilitar Etapa 09"]
```

## 2. Pipeline propuesto

```mermaid
sequenceDiagram
    participant DEV as Desarrollador
    participant VCS as Repositorio
    participant CI as Pipeline CI
    participant TEST as Pruebas
    participant ART as Artefacto

    DEV->>VCS: Commit / Pull request
    VCS->>CI: Disparar pipeline
    CI->>CI: Restaurar y compilar
    CI->>TEST: Ejecutar pruebas
    alt Pruebas exitosas
        TEST-->>CI: OK
        CI->>ART: Publicar artefacto
    else Pruebas fallidas
        TEST-->>CI: Error
        CI-->>VCS: Pipeline fallido
    end
```

## 3. Dependencias con otras etapas

```mermaid
flowchart LR
    E07["07 · Pruebas"]
    E08["08 · Integración continua"]
    E09["09 · Despliegue"]

    E07 --> E08
    E08 --> E09
```

## 4. Estados de las tareas

```mermaid
stateDiagram-v2
    [*] --> BLOQUEADA
    BLOQUEADA --> PENDIENTE: DEC-006 resuelta
    PENDIENTE --> EN_PROGRESO: configura pipeline
    EN_PROGRESO --> COMPLETADA: pipeline verificado
    COMPLETADA --> [*]
```

## 5. Mapa de criterios de salida

| Criterio de salida | Evidencia |
|--------------------|-----------|
| Pipeline ejecuta pruebas | Ejecución registrada |
| Falla con pruebas rotas | Ejecución fallida documentada |
| Sin artefacto si fallan pruebas | Configuración del pipeline |
