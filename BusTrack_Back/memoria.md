# memoria.md — Registro de Contexto y Decisiones Técnicas

**Versión:** 1.0.0  
**Estado:** Activo  
**Última actualización:** 2026-10-28

> Este documento registra el contexto, las decisiones técnicas y su estado dentro del proyecto BusTrack Backend. Es la fuente de verdad sobre qué está confirmado, qué está pendiente y qué está fuera del alcance actual.

---

## 1. Descripción del proyecto

**BusTrack** es un sistema multiplataforma de consulta y planificación de transporte público. Permite a los usuarios consultar información sobre empresas y asociaciones de transporte, medios de transporte, rutas, paradas, destinos, horarios de corridas, tarifas y calificaciones.

El sistema está compuesto por:

| Componente | Tecnología | Estado |
|------------|------------|--------|
| Aplicación móvil | Flutter + Dart | Repositorio separado |
| Plataforma web | Angular + TypeScript | Repositorio separado |
| Backend centralizado | ASP.NET Core Web API + C# | **Este repositorio** |
| Base de datos | NoSQL en Azure | Proveedor pendiente de selección |

El backend es el punto central para el acceso a los datos, la aplicación de validaciones y el control de acceso. Los clientes móvil y web consumen la misma API REST. No acceden directamente a la base de datos.

La información del sistema debe obtenerse dinámicamente desde el backend. No se deben proponer catálogos de transporte codificados permanentemente en los clientes.

---

## 2. Arquitectura confirmada

| Aspecto | Decisión confirmada |
|---------|---------------------|
| Patrón arquitectónico | Monolito modular |
| Estilo de API | REST |
| Formato de intercambio | JSON |
| Versionado de API | `/api/v1` (convención inicial) |
| Organización interna | Capas con separación de responsabilidades |
| Desacoplamiento de persistencia | Mediante interfaces de repositorio en el dominio |
| Acceso a datos | Solo a través del backend; los clientes no acceden directamente a la BD |
| Configuración | Separada del código; secretos fuera del repositorio |

**Capas propuestas (pendientes de aprobación de estructura definitiva):**

| Capa | Responsabilidad | Estado |
|------|----------------|--------|
| API | Endpoints HTTP, enrutamiento, serialización, versionado | Propuesto |
| Application | Casos de uso, orquestación, lógica de aplicación | Propuesto |
| Domain | Entidades, reglas de negocio, interfaces de repositorio | Propuesto |
| Infrastructure | Acceso a datos, adaptadores, servicios externos | Propuesto |

> La estructura de capas es una propuesta arquitectónica. No está implementada. Debe validarse durante la fase de diseño de la solución.

---

## 3. Stack tecnológico confirmado

| Componente | Tecnología | Versión | Estado |
|------------|------------|---------|--------|
| Framework web | ASP.NET Core Web API | .NET 10 | Confirmado |
| Lenguaje | C# | Versión acorde a .NET 10 | Confirmado |
| Plataforma en la nube | Microsoft Azure | N/A | Confirmado |
| Documentación API | OpenAPI (Microsoft.AspNetCore.OpenApi) | 10.0.12 | En plantilla inicial |
| Gestión de secretos | Por confirmar | — | Pendiente |
| Proveedor de identidad | Por confirmar | — | Pendiente |
| Logging centralizado | Por confirmar | — | Pendiente |
| CI/CD | Por confirmar | — | Pendiente |

---

## 4. Decisiones de persistencia confirmadas

| Aspecto | Estado | Detalle |
|---------|--------|---------|
| Tipo de base de datos | **Confirmado** | NoSQL |
| Ubicación | **Confirmado** | Microsoft Azure |
| Proveedor específico | **PENDIENTE** | No seleccionado |
| Estrategia de particionado | **PENDIENTE** | Depende del proveedor |
| Estrategia de indexado | **PENDIENTE** | Depende del proveedor |
| SDK / Librería cliente | **PENDIENTE** | Depende del proveedor |
| Modelo de consistencia | **PENDIENTE** | Depende del proveedor |

**Criterios de evaluación para la selección del proveedor NoSQL:**

| ID | Criterio | Descripción |
|----|----------|-------------|
| CRIT-DB-01 | Compatibilidad con .NET | SDK oficial, calidad, mantenimiento |
| CRIT-DB-02 | Modelo de datos | Soporte JSON, flexibilidad de esquema |
| CRIT-DB-03 | Capacidades de consulta | Filtros, proyecciones, agregaciones, búsqueda de texto |
| CRIT-DB-04 | Índices | Tipos disponibles, índices compuestos, geoespaciales |
| CRIT-DB-05 | Particionado | Estrategias, límites, impacto en consultas |
| CRIT-DB-06 | Consistencia | Modelos configurables, niveles disponibles |
| CRIT-DB-07 | Seguridad | Control de acceso, cifrado en reposo y en tránsito, auditoría |
| CRIT-DB-08 | Escalabilidad | Escalado horizontal/vertical, throughput |
| CRIT-DB-09 | Disponibilidad | SLA, regiones, recuperación ante desastres |
| CRIT-DB-10 | Costos | Modelo de precios, unidades de solicitud, almacenamiento |
| CRIT-DB-11 | Operación | Administración, monitoreo, copias de seguridad |

---

## 5. Decisiones pendientes

| ID | Decisión | Impacto si se demora | Bloquea |
|----|----------|---------------------|---------|
| DEC-001 | Selección del proveedor NoSQL en Azure | No se puede diseñar la capa de infraestructura | Fases 4, 5, 6 del plan |
| DEC-002 | Mecanismo de autenticación y autorización | No se puede diseñar la seguridad de endpoints | Fases 5, 6 del plan |
| DEC-003 | Servicio de gestión de secretos en Azure | No se puede definir la estrategia de configuración segura | Fase 6 del plan |
| DEC-004 | Proveedor de logging centralizado | No se puede implementar la observabilidad | Fase 5 del plan |
| DEC-005 | Estructura definitiva de capas de la solución .NET | No se puede iniciar la implementación | Fase 2 del plan |
| DEC-006 | Herramientas de CI/CD | No se puede configurar el pipeline | Fase 8 del plan |
| DEC-007 | Servicio de alojamiento en Azure (App Service, Container Apps, etc.) | No se puede planificar el despliegue | Fase 9 del plan |
| DEC-008 | Umbral mínimo de cobertura de pruebas | No se puede validar la calidad del código | Fase 7 del plan |
| DEC-009 | Herramientas específicas de prueba (xUnit, NUnit, etc.) | No se puede iniciar la implementación de pruebas | Fase 7 del plan |
| DEC-010 | Formato exacto del cuerpo de respuestas de error | No se puede estandarizar el manejo de errores | Fase 5 del plan |
| DEC-011 | Política de paginación y filtrado de la API | No se puede implementar endpoints de consulta | Especificaciones funcionales futuras |

---

## 6. Restricciones de alcance

Las siguientes funcionalidades están **fuera del alcance de la fase actual** y solo podrán especificarse en fases futuras:

| Funcionalidad | Motivo de exclusión |
|---------------|---------------------|
| Registro, autenticación y recuperación de contraseña | Especificación funcional futura |
| Consulta y búsqueda de rutas, paradas, destinos y horarios | Especificación funcional futura |
| Cálculo y consulta de tarifas | Especificación funcional futura |
| Gestión de calificaciones y comentarios | Especificación funcional futura |
| Recomendaciones mediante inteligencia artificial | Especificación funcional futura |
| Detección de paradas mediante acelerómetro | Especificación funcional futura |
| Operaciones administrativas específicas | Especificación funcional futura |
| Integraciones con proveedores externos definitivos | Especificación funcional futura |
| Seguimiento GPS en tiempo real | **Fuera del alcance del sistema**: el mapa es de consulta y orientación de rutas registradas, no de rastreo continuo |

---

## 7. Riesgos conocidos

| ID | Riesgo | Probabilidad | Impacto | Mitigación propuesta |
|----|--------|-------------|---------|---------------------|
| RIESGO-001 | La selección tardía del proveedor NoSQL retrasa las fases de implementación | Alta | Alto | Priorizar DEC-001 en la siguiente fase |
| RIESGO-002 | El proveedor NoSQL seleccionado puede no tener SDK oficial .NET de calidad | Media | Alto | Evaluar CRIT-DB-01 como criterio eliminatorio |
| RIESGO-003 | Cambios de requisitos funcionales invalidan decisiones arquitectónicas | Media | Medio | Mantener la persistencia desacoplada; revisar spec.md ante cada cambio |
| RIESGO-004 | Inconsistencia entre la especificación y la implementación real del cliente (Flutter/Angular) | Media | Medio | Definir contratos de API antes de iniciar la implementación de endpoints |
| RIESGO-005 | Complejidad operativa en Azure mayor a la estimada | Baja | Medio | Validar DEC-007 con experiencia real antes de comprometerse con un servicio |
| RIESGO-006 | Exposición accidental de secretos en el repositorio | Baja | Alto | Configurar `.gitignore` y revisión de seguridad antes de cualquier commit de código |

---

## 8. Supuestos que necesitan validación

| ID | Supuesto | Impacto si es incorrecto | Próximo paso |
|----|----------|--------------------------|--------------|
| SUP-001 | El cliente móvil (Flutter) y el cliente web (Angular) consumen exactamente la misma API sin adaptadores intermedios | Se requeriría un BFF (Backend for Frontend) o adaptadores | Confirmar con el equipo de desarrollo de clientes |
| SUP-002 | El sistema no requiere procesamiento en tiempo real (WebSockets, SignalR) en la fase inicial | Se requeriría cambios arquitectónicos significativos | Confirmar alcance de la fase inicial |
| SUP-003 | El volumen de datos y de usuarios en la fase inicial no requiere estrategias de escalado horizontal desde el inicio | Se requeriría diseñar para alta disponibilidad desde el inicio | Definir estimaciones de carga antes de DEC-007 |
| SUP-004 | No se integrará ningún sistema de transporte externo existente en la fase inicial | Requeriría adaptadores de integración y mapeo de datos | Confirmar fuentes de datos de transporte |
| SUP-005 | La documentación SDD es revisada y aprobada por el profesor antes de iniciar la implementación | El trabajo de implementación podría invalidarse si la especificación cambia | Someter los documentos a revisión antes de avanzar |

---

## 9. Historial de decisiones

| ID | Decisión | Estado | Justificación | Próximo paso |
|----|----------|--------|---------------|--------------|
| HIST-001 | Usar ASP.NET Core Web API con C# para el backend | **Confirmado** | Stack acordado; ecosistema maduro, soporte oficial Microsoft, compatible con Azure | Iniciar diseño de estructura de solución (DEC-005) |
| HIST-002 | Adoptar arquitectura de monolito modular | **Confirmado** | Adecuada para el tamaño inicial; evita complejidad de microservicios | Definir estructura de módulos en DEC-005 |
| HIST-003 | API REST con JSON | **Confirmado** | Estándar ampliamente adoptado; compatible con Flutter y Angular | Documentar convenciones detalladas en spec.md |
| HIST-004 | Versionado de API con `/api/v1` | **Confirmado** | Convención estándar para APIs REST; permite evolución sin romper clientes | Aplicar en la configuración de rutas |
| HIST-005 | Base de datos NoSQL en Azure | **Confirmado** | Decisión tomada; proveedor pendiente | Evaluar proveedores usando CRIT-DB-01 a CRIT-DB-11 (DEC-001) |
| HIST-006 | Persistencia desacoplada mediante abstracciones | **Confirmado** | Permite cambiar el proveedor de BD con cambios controlados | Diseñar interfaces de repositorio en la fase de dominio |
| HIST-007 | Secretos fuera del repositorio | **Confirmado** | Principio de seguridad fundamental | Definir estrategia de gestión de secretos (DEC-003) |
| HIST-008 | Metodología SDD | **Confirmado** | Metodología establecida por el proyecto académico | Completar documentación antes de iniciar implementación |
| HIST-009 | Estructura de capas API/Application/Domain/Infrastructure | **Propuesto** | Estructura Clean Architecture/Onion adaptada; pendiente de validación | Aprobar en DEC-005 |
| HIST-010 | Alojamiento en Azure | **Confirmado** | Plataforma en la nube seleccionada | Confirmar servicio específico de alojamiento (DEC-007) |

---

*Este documento debe actualizarse en cada sesión de trabajo que modifique decisiones, identifique nuevos riesgos o supuestos, o cambie el estado de cualquier decisión pendiente.*
