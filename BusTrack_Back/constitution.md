# Constitución del Backend de BusTrack

**Versión:** 1.0.0  
**Estado:** Vigente  
**Ámbito:** Backend de BusTrack (`BusTrack_Back`)

---

## 1. Propósito y alcance de esta constitución

Esta constitución establece los principios normativos, restricciones obligatorias y reglas de coherencia que rigen el diseño, la documentación y la futura implementación del backend de **BusTrack**.

Es el documento de referencia de mayor jerarquía dentro del repositorio. Cualquier documento, especificación, plan, tarea o contribución de código debe ser coherente con las reglas aquí establecidas. En caso de contradicción entre esta constitución y otro documento, prevalece esta constitución.

**Alcance:**
- Aplica a todo el contenido del repositorio `BusTrack_Back`.
- Aplica a cualquier agente de IA, colaborador humano o herramienta automatizada que trabaje sobre este repositorio.
- No aplica a los repositorios del cliente móvil (Flutter) ni del cliente web (Angular), aunque sí define cómo el backend interactuará con ellos.

---

## 2. Principios obligatorios de Spec-Driven Development (SDD)

El desarrollo del backend sigue la metodología **Spec-Driven Development**. Estos principios son obligatorios y no negociables:

1. **La especificación precede a la implementación.** Ninguna funcionalidad puede codificarse sin una especificación aprobada previa que la describa.
2. **La documentación es la fuente de verdad.** El código debe derivarse de los documentos SDD, no al revés.
3. **Los cambios de especificación requieren aprobación.** Ninguna decisión arquitectónica o funcional puede modificarse unilateralmente. Los cambios deben proponerse, discutirse y registrarse en `memoria.md`.
4. **La trazabilidad es obligatoria.** Toda tarea en `task.md` debe referirse a una especificación en `spec.md` o a una fase en `plan.md`.
5. **Las decisiones pendientes no deben inventarse.** Si una decisión aún no está confirmada, debe registrarse como pendiente y no asumir un valor arbitrario.
6. **Las etapas son secuenciales.** No se puede comenzar la implementación de una fase sin haber completado la documentación de las fases anteriores y sin la aprobación correspondiente.

---

## 3. Reglas de coherencia entre documentos

Los documentos del repositorio forman una jerarquía normativa:

| Nivel | Documento | Función |
|-------|-----------|---------|
| 1 | `constitution.md` | Norma suprema; define principios y restricciones |
| 2 | `AGENTS.md` | Instrucciones operativas para agentes y colaboradores |
| 3 | `memoria.md` | Registro de decisiones, estado y contexto del proyecto |
| 4 | `spec.md` | Especificación técnica de la arquitectura base |
| 5 | `plan.md` | Plan de implementación por fases |
| 6 | `task.md` | Desglose de tareas trazables |
| 7 | `subagents/` | Definición de roles y restricciones de subagentes |
| 8 | `skills/` | Procedimientos reutilizables de revisión |

**Reglas:**
- Los documentos de nivel inferior no pueden contradecir a los de nivel superior.
- Si se detecta una contradicción, debe registrarse en `memoria.md` como conflicto pendiente de resolución antes de continuar.
- Ningún documento puede eliminarse sin aprobación explícita.
- Las actualizaciones deben reflejarse en todos los documentos afectados.

---

## 4. Arquitectura: monolito modular

**Decisión confirmada:** El backend de BusTrack adoptará una arquitectura de **monolito modular**.

### Justificación
- Adecuada para el tamaño y la complejidad inicial del sistema.
- Evita la sobrecarga operativa de los microservicios (orquestación, descubrimiento de servicios, red distribuida).
- Permite una separación clara de responsabilidades dentro de un único proceso desplegable.
- Facilita la evolución gradual hacia una arquitectura más distribuida si fuera necesario en el futuro.

### Restricciones obligatorias
- **Prohibido** adoptar una arquitectura de microservicios sin aprobación explícita y documentada.
- Los módulos internos deben comunicarse a través de interfaces o abstracciones, no mediante dependencias directas entre implementaciones.
- Cada módulo debe tener un propósito cohesivo y delimitado.
- La modularización interna no implica despliegues independientes.

---

## 5. Separación de responsabilidades

El backend se organizará en capas con responsabilidades claramente delimitadas. Las capas propuestas son:

| Capa | Responsabilidad |
|------|----------------|
| **API** | Recibir solicitudes HTTP, validar entradas, serializar respuestas, gestionar rutas y versiones |
| **Application** | Coordinar la lógica de aplicación, orquestar casos de uso, aplicar reglas de negocio |
| **Domain** | Definir entidades, objetos de valor, reglas de dominio e interfaces de repositorio |
| **Infrastructure** | Implementar acceso a datos, integración con servicios externos, adaptadores |

> **Nota:** Esta estructura es una propuesta arquitectónica que deberá aprobarse y refinarse durante la fase de diseño de la solución. No afirma que esté implementada actualmente.

**Reglas obligatorias:**
- La capa de dominio no debe depender de ninguna capa de infraestructura.
- La capa de aplicación no debe depender directamente de implementaciones concretas de infraestructura.
- Las dependencias deben dirigirse hacia el centro (inversión de dependencias).
- No se permite lógica de negocio en los controladores.
- No se permite acceso directo a datos desde la capa de API.

---

## 6. Convenciones generales de API REST

**Decisiones confirmadas:**
- La API seguirá el estilo **REST**.
- El formato de intercambio de datos será **JSON**.
- El versionado de la API utilizará la convención `/api/v1` como punto de partida.

**Reglas obligatorias:**
- Los recursos deben nombrarse con sustantivos en plural y en minúsculas (p. ej., `/api/v1/rutas`, `/api/v1/paradas`).
- Las operaciones se expresan mediante verbos HTTP estándar (`GET`, `POST`, `PUT`, `PATCH`, `DELETE`).
- Los códigos de respuesta HTTP deben usarse correctamente y de forma consistente.
- Las respuestas de error deben seguir una estructura uniforme en toda la API.
- Los clientes móvil y web son los únicos consumidores autorizados de la API; no se accede directamente a la base de datos desde los clientes.
- No se deben exponer detalles internos de la infraestructura en las respuestas.

**Pendiente de aprobación:**
- Formato exacto del cuerpo de respuestas de error.
- Política de paginación y filtrado.
- Estrategia de autenticación y autorización.

---

## 7. Principios de seguridad y privacidad

**Principios obligatorios (independientes del proveedor):**

1. **Autenticación obligatoria:** Todos los endpoints que expongan datos o realicen operaciones deben requerir autenticación, excepto los explícitamente autorizados como públicos.
2. **Autorización basada en roles:** El acceso a operaciones sensibles debe controlarse mediante roles o políticas.
3. **Sin secretos en el repositorio:** Ninguna credencial, clave de API, cadena de conexión ni secreto puede almacenarse en el código fuente o en archivos versionados.
4. **HTTPS obligatorio:** La API solo debe aceptar conexiones seguras en entornos no locales.
5. **Validación de entradas:** Toda entrada proveniente del cliente debe validarse antes de procesarse.
6. **Principio de mínimo privilegio:** Las cuentas de servicio y los recursos de infraestructura deben tener únicamente los permisos necesarios para su función.
7. **Sin exposición de información sensible:** Los mensajes de error no deben revelar detalles internos del sistema, rutas de archivos, nombres de tablas ni información de la infraestructura.

**Pendiente de aprobación:**
- Proveedor de identidad y mecanismo de autenticación (JWT, OAuth 2.0, OpenID Connect, u otro).
- Estrategia de gestión de secretos en Azure (Key Vault u otro).

---

## 8. Gestión de configuración y secretos

**Reglas obligatorias:**
- La configuración sensible (cadenas de conexión, claves, secretos) no debe almacenarse en `appsettings.json` ni en ningún archivo versionado.
- Se utilizarán variables de entorno, servicios de configuración segura o secretos de CI/CD según el entorno.
- Los archivos `appsettings.*.json` solo pueden contener configuración no sensible y valores por defecto seguros.
- El archivo `.gitignore` debe excluir cualquier archivo que pudiera contener secretos locales.
- La configuración debe separarse por entorno: desarrollo, pruebas, producción.

**Pendiente de aprobación:**
- Servicio definitivo de gestión de secretos en Azure.

---

## 9. Calidad, pruebas y mantenibilidad

**Principios obligatorios:**
- El código debe ser legible, mantenible y coherente con las convenciones del ecosistema .NET.
- Las funcionalidades deben acompañarse de pruebas automatizadas.
- Se contemplarán, como mínimo, pruebas unitarias para la lógica de dominio y de aplicación.
- Se contemplarán pruebas de integración para los flujos de la API.
- La cobertura de pruebas no debe reducirse con cada nueva contribución.
- El manejo de errores debe ser centralizado y consistente.

**Pendiente de aprobación:**
- Umbral mínimo de cobertura de pruebas.
- Herramientas específicas de prueba (xUnit, NUnit, etc.).
- Estrategia de pruebas de contrato con los clientes.

---

## 10. Requisitos generales de observabilidad

**Principios obligatorios:**
- La aplicación debe emitir registros estructurados con niveles de severidad apropiados.
- Los registros no deben incluir datos personales ni información sensible.
- Se deben registrar, como mínimo: errores no controlados, inicio y detención de la aplicación, y operaciones significativas del sistema.
- La aplicación debe exponer al menos un endpoint de verificación de salud (_health check_).

**Pendiente de aprobación:**
- Proveedor de registros centralizado (Application Insights, Serilog + sink, u otro).
- Estrategia de métricas y trazas distribuidas.
- Umbrales de alerta y política de retención de registros.

---

## 11. Restricciones sobre persistencia NoSQL

**Decisión confirmada:** Se utilizará una **base de datos NoSQL alojada en Azure**.

**Proveedor específico: PENDIENTE DE SELECCIÓN Y APROBACIÓN.**

**Restricciones obligatorias hasta que se seleccione el proveedor:**
- No se seleccionará ningún proveedor específico (Azure Cosmos DB, MongoDB Atlas, etc.) como decisión definitiva sin aprobación.
- No se escribirán credenciales, cadenas de conexión ni configuración específica del proveedor.
- No se implementarán repositorios ni clases de persistencia.
- No se diseñará una estrategia definitiva de particionado o indexado.
- No se asumirá un modelo relacional.
- No se crearán recursos en Azure.
- La capa de acceso a datos debe permanecer desacoplada mediante abstracciones (interfaces de repositorio en el dominio) para que el proveedor pueda seleccionarse posteriormente con cambios controlados.

**Criterios que deben evaluarse para seleccionar el proveedor:**

| Criterio | Descripción |
|----------|-------------|
| Compatibilidad con .NET | Disponibilidad y calidad del SDK oficial para .NET |
| Modelo de datos | Soporte para documentos JSON, flexibilidad del esquema |
| Capacidades de consulta | Filtros, proyecciones, agregaciones, búsqueda de texto |
| Índices | Tipos de índice soportados, índices compuestos, geoespaciales |
| Particionado | Estrategias disponibles, límites, impacto en las consultas |
| Consistencia | Modelos de consistencia disponibles y configurables |
| Seguridad | Control de acceso, cifrado en reposo y en tránsito, auditoría |
| Escalabilidad | Escalado horizontal y vertical, límites de throughput |
| Disponibilidad | SLA, regiones, recuperación ante desastres |
| Costos | Modelo de precios, unidades de solicitud, almacenamiento |
| Operación | Complejidad de administración, monitoreo, copias de seguridad |

---

## 12. Prohibición de implementar funcionalidades no especificadas

**Regla obligatoria:** Ninguna funcionalidad que no haya sido previamente especificada en un documento `spec.md` aprobado puede implementarse.

Funcionalidades fuera del alcance de la arquitectura base (reservadas para especificaciones futuras):
- Registro, autenticación y recuperación de contraseña.
- Consulta y búsqueda de rutas, paradas, destinos y horarios.
- Cálculo y consulta de tarifas.
- Gestión de calificaciones y comentarios.
- Recomendaciones mediante inteligencia artificial.
- Detección de paradas mediante acelerómetro.
- Operaciones administrativas específicas.
- Integraciones definitivas con proveedores externos.
- Seguimiento GPS de vehículos o usuarios en tiempo real.

---

## 13. Control de cambios y aprobación de decisiones

**Proceso obligatorio para modificar la constitución o cualquier decisión confirmada:**

1. Identificar la decisión o regla que se desea modificar.
2. Documentar la propuesta de cambio en `memoria.md` con justificación.
3. Registrar el cambio como **Propuesto** hasta que reciba aprobación explícita.
4. Solo tras la aprobación, actualizar los documentos afectados.
5. Registrar la decisión aprobada en el historial de `memoria.md`.

**Prohibiciones:**
- No modificar decisiones confirmadas sin seguir este proceso.
- No asumir que una propuesta está aprobada por falta de respuesta.
- No introducir cambios técnicos que contradigan la constitución sin aprobación previa.

---

## 14. Criterios para considerar conforme una contribución

Una contribución (documento, código o configuración) se considera **conforme** cuando:

1. Es coherente con esta constitución y con todos los documentos de nivel superior.
2. No contradice ninguna decisión confirmada.
3. No implementa funcionalidades no especificadas.
4. No contiene secretos ni información sensible.
5. Está acompañada de la actualización correspondiente en `memoria.md` si modifica alguna decisión.
6. Las tareas que documenta están en el estado correcto (no marcadas como completadas sin evidencia).
7. Respeta las convenciones de nomenclatura, idioma y formato establecidas.

---

## 15. Regla de no ejecución durante la etapa documental

**En la etapa actual, esta constitución establece explícitamente:**

- No se debe programar ninguna funcionalidad.
- No se deben crear proyectos .NET ni archivos de código.
- No se deben instalar paquetes ni dependencias.
- No se deben ejecutar migraciones ni scripts.
- No se deben crear bases de datos ni recursos en Azure.
- No se debe publicar ni desplegar la API.
- No se deben marcar tareas como completadas por el simple hecho de haberlas escrito.

El resultado de la etapa actual es exclusivamente **documentación SDD**.

---

## Historial de la constitución

| Versión | Fecha | Descripción |
|---------|-------|-------------|
| 1.0.0 | 2026-10-28 | Versión inicial de la constitución del backend de BusTrack |
