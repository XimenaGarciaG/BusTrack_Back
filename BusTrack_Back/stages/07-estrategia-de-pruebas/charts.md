# charts.md — Etapa 07: Estrategia de pruebas

**Versión:** 1.0.0  
**Estado:** Activo  
**Última actualización:** 2026-10-29  
**Etapa:** 07  
**Referencia:** [`plan.md`](./plan.md) | [`task.md`](./task.md)

> Diagramas de la estrategia de pruebas. Las herramientas concretas dependen de DEC-009.

---

## 1. Flujo de la etapa

```mermaid
flowchart TD
    A["Inicio · Etapa 07"] --> B["Seleccionar herramientas<br/>DEC-009"]
    B --> C["TAREA-018<br/>Crear proyectos de prueba"]
    C --> D["Pruebas unitarias<br/>Domain / Application"]
    C --> E["Pruebas de integración<br/>API base"]
    D --> F["Ejecutar en local"]
    E --> F
    F --> G{"¿Cumple umbral<br/>DEC-008?"}
    G -- "No" --> D
    G -- "Sí" --> H["Documentar estrategia"]
    H --> I["Fin · habilitar Etapa 08"]
```

## 2. Pirámide de pruebas

```mermaid
flowchart TB
    A["Pruebas de contrato<br/>API"]
    B["Pruebas de integración<br/>API / Infrastructure"]
    C["Pruebas unitarias<br/>Domain / Application"]

    C --> B --> A
```

## 3. Dependencias con otras etapas

```mermaid
flowchart LR
    E05["05 · Base API"]
    E07["07 · Pruebas"]
    E08["08 · Integración continua"]

    E05 --> E07
    E07 --> E08
```

## 4. Estados de las tareas

```mermaid
stateDiagram-v2
    [*] --> BLOQUEADA
    BLOQUEADA --> PENDIENTE: DEC-008 y DEC-009 resueltas
    PENDIENTE --> EN_PROGRESO: inicia implementación de pruebas
    EN_PROGRESO --> COMPLETADA: umbral y criterios verificados
    COMPLETADA --> [*]
```

## 5. Mapa de criterios de salida

| Criterio de salida | Evidencia |
|--------------------|-----------|
| Pruebas unitarias sin infraestructura | Resultado de ejecución |
| Pruebas de integración de AC-ARCH | Reporte de pruebas |
| Umbral DEC-008 cumplido | Reporte de cobertura |
