# spec.md — Especificación de Arquitectura Base del Backend de BusTrack

**Versión:** 1.0.0  
**Estado:** Borrador — Pendiente de revisión y aprobación  
**Última actualización:** 2026-10-28  
**Referencia normativa:** [`constitution.md`](./constitution.md)

---

## 1. Propósito

Este documento especifica la arquitectura base del backend de **BusTrack**. Define la estructura, los principios y las reglas técnicas que deben guiar la construcción del sistema antes de incorporar especificaciones funcionales específicas.

Este documento establece la **base arquitectónica** sobre la que se construirán las funcionalidades futuras. No define operaciones de negocio, endpoints específicos ni lógica de dominio particular.

---

## 2. Alcance y exclusiones

### Dentro del alcance de esta especificación

- Estructura de la solución .NET y organización en capas.
- Principios de comunicación HTTP y convenciones REST.
- Convenciones de versionado de la API.
- Configuración por entorno y gestión de secretos.
- Principios de acceso a datos y desacoplamiento de persistencia.
- Restricciones de seguridad y privacidad a nivel de arquitectura.
- Requisitos de manejo centralizado de errores.
- Requisitos de registros y observabilidad.
- Estrategia general de pruebas.
- Restricciones de infraestructura en Azure.
- Riesgos, dependencias y decisiones pendientes.
- Criterios de aceptación verificables de la arquitectura base.

### Fuera del alcance de esta especificación

Los siguientes temas se especificarán en documentos funcionales futuros y **no deben incorporarse a esta especificación**:

| Tema excluido | Razón |
|---------------|-------|
| Registro, autenticación y recuperación de contraseña | Especificación funcional futura |
| Consulta de rutas, paradas, destinos y horarios | Especificación funcional futura |
| Cálculo de tarifas | Especificación funcional futura |
| Gestión de calificaciones y comentarios | Especificación funcional futura |
| Recomendaciones mediante IA | Especificación funcional futura |
| Detección de paradas por acelerómetro | Especificación funcional futura |
| Operaciones administrativas específicas | Especificación funcional futura |
| Integraciones con proveedores externos | Especificación funcional futura |
| Seguimiento GPS en tiempo real | Fuera del alcance del sistema (mapa de consulta, no rastreo continuo) |
| Diseño del esquema de datos | Depende del proveedor NoSQL (pendiente DEC-001) |
| Endpoints de autenticación específicos | Depende de DEC-002 |

---

## 3. Contexto del sistema y sus clientes

BusTrack es un sistema de consulta y planificación de transporte público. Sus componentes externos son:

```
┌─────────────────────┐    ┌─────────────────────┐
│  Aplicación Móvil   │    │  Plataforma Web      │
│  (Flutter + Dart)   │    │  (Angular + TypeScript)│
└──────────┬──────────┘    └──────────┬────────────┘
           │                          │
           │         HTTPS/REST       │
           └─────────────┬────────────┘
                         │
              ┌──────────▼──────────┐
              │   Backend BusTrack  │
              │  ASP.NET Core Web API│
              │  (Este repositorio) │
              └──────────┬──────────┘
                         │
              ┌──────────▼──────────┐
              │  Base de Datos NoSQL│
              │  (Azure - proveedor │
              │   pendiente)        │
              └─────────────────────┘
```

**Características del contexto:**

- Los clientes móvil y web no tienen acceso directo a la base de datos.
- Ambos clientes consumen la misma API REST.
- El backend es el único punto de acceso autorizado a los datos.
- La información del sistema se obtiene dinámicamente; no se codifican catálogos en los clientes.
- No existe comunicación sincrónica entre el cliente móvil y el web; toda comunicación pasa por el backend.

**Suposición (SUP-001):** Se asume que ambos clientes consumen la misma API sin adaptadores intermedios. Si se identifica la necesidad de un BFF (Backend for Frontend), deberá documentarse como una decisión de arquitectura adicional.

---

## 4. Vista general de arquitectura

### Patrón: Monolito modular

El backend es un único proceso desplegable organizado internamente en módulos con responsabilidades delimitadas. No es una arquitectura de microservicios.

**Ventajas de esta elección:**
- Menor complejidad operativa que los microservicios.
- Comunicación intra-proceso más eficiente.
- Despliegue simplificado en la fase inicial.
- Facilita la evolución gradual si fuera necesario.

**Principios del monolito modular:**
- Los módulos se comunican mediante interfaces o abstracciones, no mediante dependencias directas entre implementaciones.
- Cada módulo tiene un propósito cohesivo y un ámbito delimitado.
- La modularización interna no implica despliegues independientes.

### Flujo de una solicitud (ilustrativo)

```
Cliente (Flutter / Angular)
  │
  │ HTTP Request (HTTPS + JSON)
  ▼
[API Layer] — Valida la solicitud, autentica al usuario, enruta al caso de uso
  │
  │ Llama al caso de uso
  ▼
[Application Layer] — Orquesta la lógica, aplica reglas de aplicación
  │
  │ Usa interfaces de repositorio
  ▼
[Domain Layer] — Contiene entidades y reglas de negocio; define interfaces
  │
  │ Las implementaciones de infraestructura implementan las interfaces del dominio
  ▼
[Infrastructure Layer] — Implementa acceso a datos, adapta servicios externos
  │
  ▼
Base de Datos NoSQL (Azure)
```

> **Nota:** Este flujo es ilustrativo. La estructura de capas está propuesta pero pendiente de aprobación definitiva (DEC-005).

---

## 5. Componentes y responsabilidades

### 5.1 Capa API (presentación / interfaces)

**Responsabilidades:**
- Recibir y enrutar solicitudes HTTP entrantes.
- Validar el formato y la estructura de las entradas.
- Autenticar y autorizar al solicitante.
- Delegar la lógica de negocio a la capa de aplicación.
- Serializar y devolver respuestas JSON.
- Gestionar el versionado de la API.
- Centralizar el manejo de errores HTTP.

**Lo que NO hace:**
- No contiene lógica de negocio.
- No accede directamente a la base de datos.
- No implementa reglas de dominio.

**Candidatos de contenido:**
- Controladores (Controllers).
- Filtros de acción y middleware.
- Modelos de solicitud y respuesta (DTOs).
- Configuración de enrutamiento y versionado.
- Configuración de OpenAPI.

### 5.2 Capa de Aplicación (casos de uso)

**Responsabilidades:**
- Implementar los casos de uso del sistema.
- Orquestar la interacción entre entidades de dominio.
- Aplicar reglas de aplicación (no de dominio puro).
- Coordinar el acceso a repositorios mediante las interfaces definidas en el dominio.
- Gestionar transacciones de aplicación cuando aplique.

**Lo que NO hace:**
- No define reglas de negocio del dominio.
- No depende de implementaciones concretas de infraestructura.
- No maneja solicitudes HTTP.

**Candidatos de contenido:**
- Comandos y manejadores (patrón CQRS opcional).
- Servicios de aplicación.
- DTOs de aplicación.
- Interfaces de servicios externos (definición, no implementación).

### 5.3 Capa de Dominio (núcleo del sistema)

**Responsabilidades:**
- Definir las entidades y los objetos de valor del sistema.
- Expresar las reglas de negocio fundamentales.
- Definir las interfaces de repositorio.
- Definir las interfaces de servicios de dominio cuando aplique.

**Lo que NO hace:**
- No depende de ninguna otra capa.
- No contiene lógica de acceso a datos.
- No conoce los detalles de HTTP, serialización ni infraestructura.

**Principio de inversión de dependencias:** Las capas externas dependen de las abstracciones definidas en el dominio.

### 5.4 Capa de Infraestructura (adaptadores externos)

**Responsabilidades:**
- Implementar las interfaces de repositorio definidas en el dominio.
- Gestionar la conexión y el acceso a la base de datos NoSQL.
- Integrar servicios externos (correo, proveedores de identidad, etc.).
- Adaptar formatos externos al modelo del dominio.
- Gestionar la configuración específica del entorno.

**Lo que NO hace:**
- No define reglas de negocio.
- No expone directamente a la capa API.

**Condición actual:** Las implementaciones concretas de acceso a datos **no pueden construirse** hasta que se seleccione el proveedor NoSQL (DEC-001).

---

## 6. Separación de capas

### Reglas de dependencia entre capas

```
API  →  Application  →  Domain  ←  Infrastructure
```

- La dirección de las flechas indica la dependencia.
- La capa Domain no depende de ninguna otra capa.
- La capa Infrastructure implementa las interfaces del Domain.
- La capa Application solo depende del Domain.
- La capa API depende de Application (y puede depender del Domain para DTOs).

### Dependencias prohibidas

| Dependencia | Estado |
|-------------|--------|
| Domain → Application | **PROHIBIDA** |
| Domain → Infrastructure | **PROHIBIDA** |
| Domain → API | **PROHIBIDA** |
| Application → Infrastructure (directa) | **PROHIBIDA** (usar interfaces del Domain) |
| Application → API | **PROHIBIDA** |

### Mecanismo de inversión de dependencias

La capa Application declara las interfaces que necesita (en el Domain). La capa Infrastructure las implementa. El contenedor de inyección de dependencias de ASP.NET Core conecta las implementaciones con las interfaces en tiempo de ejecución.

---

## 7. Principios de comunicación HTTP y JSON

### Protocolo

- La comunicación entre clientes y backend se realiza exclusivamente mediante **HTTPS**.
- No se admiten conexiones HTTP sin cifrado en entornos no locales.

### Método HTTP y semántica de operaciones

| Operación | Método HTTP | Notas |
|-----------|-------------|-------|
| Leer recursos | `GET` | Sin efectos secundarios |
| Crear recursos | `POST` | Cuerpo JSON en la solicitud |
| Reemplazar recursos | `PUT` | Reemplaza el recurso completo |
| Modificar parcialmente | `PATCH` | Modifica campos específicos |
| Eliminar recursos | `DELETE` | Sin cuerpo en la solicitud |

### Convenciones de URL

- Los recursos se nombran con sustantivos en plural y en minúsculas.
- Los segmentos de URL usarán kebab-case cuando sean necesarias palabras compuestas.
- Los identificadores de recursos se incluyen en el path: `/api/v1/rutas/{id}`.
- *Ejemplo ilustrativo (no define endpoints funcionales aprobados):*
  - `GET /api/v1/rutas` — listado de rutas.
  - `GET /api/v1/rutas/{id}` — consulta de una ruta específica.
  - `GET /api/v1/paradas` — listado de paradas.

### Códigos de respuesta HTTP

| Código | Uso |
|--------|-----|
| 200 OK | Solicitud exitosa con cuerpo de respuesta |
| 201 Created | Recurso creado exitosamente |
| 204 No Content | Operación exitosa sin cuerpo de respuesta |
| 400 Bad Request | Datos de entrada inválidos |
| 401 Unauthorized | No autenticado |
| 403 Forbidden | Autenticado pero sin permiso |
| 404 Not Found | Recurso no encontrado |
| 409 Conflict | Conflicto con el estado actual del recurso |
| 422 Unprocessable Entity | Validación de negocio fallida |
| 500 Internal Server Error | Error interno no controlado |

### Formato JSON

- Las propiedades de los objetos JSON usarán **camelCase**.
- Las fechas se representarán en formato **ISO 8601** (p. ej., `"2026-10-28T00:00:00Z"`).
- Las respuestas de lista incluirán metadatos de paginación (estructura pendiente de definición — DEC-011).
- Los valores nulos no deben omitirse arbitrariamente; se definirá una política consistente durante la implementación.

---

## 8. Convenciones generales de versionado de API

### Estrategia de versionado

- El versionado se realizará mediante el **prefijo en la URL**: `/api/v{n}/`.
- La versión inicial es `/api/v1/`.
- La versión se incluye en todas las rutas de la API pública.

### Reglas de evolución de versiones

- Una nueva versión mayor (`v2`, `v3`) se crea cuando los cambios son incompatibles con los clientes existentes.
- Las versiones anteriores pueden mantenerse en paralelo durante un período de transición.
- Los cambios compatibles (nuevos campos opcionales, nuevos endpoints) no requieren nueva versión.
- Los campos eliminados, renombrados o que cambian de tipo siempre requieren nueva versión.

### Implementación

- El versionado mediante prefijo en URL es la convención acordada.
- La estrategia técnica de implementación (rutas por convención, atributos, biblioteca de versionado) se definirá en la fase de implementación.

---

## 9. Configuración por entorno

### Entornos contemplados

| Entorno | Propósito |
|---------|-----------|
| Development | Desarrollo local |
| Testing | Pruebas automatizadas |
| Staging | Preproducción / validación |
| Production | Entorno productivo |

### Jerarquía de configuración (propuesta)

ASP.NET Core permite una jerarquía de proveedores de configuración. Se propone el siguiente orden (menor a mayor prioridad):

1. `appsettings.json` — Valores por defecto no sensibles.
2. `appsettings.{Environment}.json` — Sobrescrituras por entorno, no sensibles.
3. Variables de entorno — Para valores específicos del entorno de despliegue.
4. Servicio de gestión de secretos (p. ej., Azure Key Vault) — Para valores sensibles en producción.
5. Secretos de usuario (`dotnet user-secrets`) — Solo en desarrollo local.

### Restricciones de configuración

- Ningún archivo de configuración versionado puede contener:
  - Contraseñas.
  - Cadenas de conexión con credenciales.
  - Claves de API.
  - Tokens de acceso.
  - Identificadores de recursos de producción.
- `appsettings.Development.json` puede contener valores de desarrollo local no sensibles.
- Los archivos de secretos locales deben estar en `.gitignore`.

---

## 10. Principios de acceso a datos y desacoplamiento de persistencia

### Patrón de repositorio

El acceso a datos se realizará mediante el **patrón de repositorio** (_Repository Pattern_):

- Las interfaces de repositorio se definen en la **capa de dominio**.
- Las implementaciones concretas se ubican en la **capa de infraestructura**.
- La capa de aplicación solo interactúa con las interfaces, nunca con las implementaciones concretas.

### Beneficios del desacoplamiento

- Permite cambiar el proveedor NoSQL con cambios limitados a la capa de infraestructura.
- Facilita las pruebas unitarias mediante el uso de repositorios simulados (_mocks_).
- Evita que la lógica de dominio dependa de SDKs específicos de proveedores.

### Estado actual

- Las interfaces de repositorio no están implementadas. Se diseñarán en fases futuras.
- Las implementaciones concretas están bloqueadas hasta la selección del proveedor NoSQL (DEC-001).
- **No se debe diseñar un esquema de datos específico** hasta que el proveedor esté seleccionado.

### Principios del modelo de datos

- El modelo de datos será **orientado a documentos** (coherente con NoSQL).
- No se asume un modelo relacional ni se diseñarán joins entre colecciones como práctica primaria.
- La estructura de los documentos se definirá en función del proveedor seleccionado y los patrones de acceso.

---

## 11. Restricciones de seguridad y privacidad

### Autenticación

- Todos los endpoints deben requerir autenticación, salvo los explícitamente marcados como públicos.
- El mecanismo de autenticación está **pendiente de selección** (DEC-002).
- Candidatos posibles: JWT con OAuth 2.0 / OpenID Connect, gestión de identidad mediante Azure AD B2C u otro servicio. **Ninguno es una decisión confirmada.**

### Autorización

- El sistema debe soportar autorización basada en roles o políticas.
- La definición de roles es una especificación funcional futura.

### Transporte

- HTTPS es obligatorio en todos los entornos excepto desarrollo local.
- La redirección de HTTP a HTTPS debe estar configurada.

### Validación de entradas

- Toda entrada del cliente debe validarse antes de procesarse.
- La validación de formato se realizará en la capa API.
- La validación de reglas de negocio se realizará en la capa de dominio o aplicación.

### Protección de datos

- Los datos personales de los usuarios deben manejarse con principios de privacidad.
- No se deben registrar datos personales en los logs.
- Las respuestas de error no deben revelar información interna del sistema.

---

## 12. Requisitos de manejo de errores

### Manejo centralizado

- El manejo de errores no controlados debe centralizarse mediante middleware de ASP.NET Core.
- No se deben propagar excepciones no controladas al cliente con detalles internos.

### Estructura de respuesta de error

Se propone la siguiente estructura de respuesta de error (pendiente de aprobación — DEC-010):

```json
{
  "type": "https://tools.ietf.org/html/rfc9110#section-15.5.1",
  "title": "Descripción breve del error",
  "status": 400,
  "detail": "Descripción detallada del error para el cliente",
  "instance": "/api/v1/recurso/operacion",
  "traceId": "identificador-de-traza-para-correlación"
}
```

> Esta estructura es compatible con el estándar **RFC 7807 (Problem Details for HTTP APIs)**. Su adopción definitiva está pendiente de aprobación.

### Clasificación de errores

| Categoría | Código HTTP | Ejemplo |
|-----------|-------------|---------|
| Entrada inválida | 400 | Formato incorrecto, campo requerido ausente |
| No autenticado | 401 | Token ausente o inválido |
| Sin permiso | 403 | Rol insuficiente |
| No encontrado | 404 | Recurso no existe |
| Conflicto | 409 | Recurso duplicado |
| Validación de negocio | 422 | Regla de negocio violada |
| Error interno | 500 | Excepción no controlada |

### Registro de errores

- Todos los errores `5xx` deben registrarse con nivel `Error` o `Critical`.
- Los errores `4xx` pueden registrarse con nivel `Warning` según su relevancia.
- El log de un error debe incluir el identificador de traza para correlación.

---

## 13. Requisitos de registros y observabilidad

### Registro estructurado

- La aplicación debe utilizar registro estructurado (no texto plano sin formato).
- Los registros deben incluir nivel de severidad, timestamp, mensaje y contexto relevante.
- Se utilizará la abstracción `ILogger<T>` de Microsoft.Extensions.Logging como interfaz estándar.

### Niveles de registro

| Nivel | Uso |
|-------|-----|
| Trace | Solo para diagnóstico profundo en desarrollo |
| Debug | Información de diagnóstico detallada |
| Information | Eventos operativos normales del sistema |
| Warning | Situaciones anómalas que no impiden el funcionamiento |
| Error | Errores que impiden una operación específica |
| Critical | Fallos graves que afectan el funcionamiento del sistema |

### Eventos mínimos a registrar

- Inicio y detención de la aplicación.
- Errores no controlados (con su traza completa).
- Fallos de autenticación y autorización.
- Operaciones administrativas significativas (cuando se especifiquen).
- Tiempo de respuesta de operaciones críticas (cuando corresponda).

### Datos que NO deben registrarse

- Contraseñas ni credenciales.
- Datos personales identificables (nombre completo, correo, número de teléfono, etc.).
- Tokens de acceso ni claves de API.
- Información sensible de configuración.

### Health Check

- La aplicación debe exponer al menos un endpoint de verificación de salud.
- Ruta propuesta: `/health` (fuera del prefijo `/api/v1/`).
- El health check debe verificar la conectividad con dependencias críticas (base de datos, etc.).

### Proveedor de observabilidad centralizada

- **Pendiente de selección** (parte de DEC-004 y DEC-006).
- Opciones a evaluar: Azure Application Insights, OpenTelemetry, Serilog con sinks apropiados.

---

## 14. Estrategia general de pruebas

### Tipos de prueba contemplados

| Tipo | Propósito | Capa objetivo |
|------|-----------|---------------|
| Pruebas unitarias | Verificar unidades de lógica de forma aislada | Domain, Application |
| Pruebas de integración | Verificar la interacción entre componentes | API, Infrastructure |
| Pruebas de contrato | Verificar que la API cumple el contrato esperado por los clientes | API |

### Principios generales

- Las pruebas se organizarán en proyectos separados del código de producción.
- La lógica de dominio y aplicación debe ser testeable sin infraestructura real.
- El patrón de repositorio facilita el uso de repositorios simulados en pruebas unitarias.
- Las pruebas no deben depender de datos o configuración de producción.

### Herramientas

- **Pendiente de selección** (DEC-009). Opciones comunes en el ecosistema .NET: xUnit, NUnit, MSTest para pruebas unitarias; Moq, NSubstitute para simulación de dependencias.

### Umbral de cobertura

- **Pendiente de definición** (DEC-008).

### Integración con CI/CD

- Las pruebas automatizadas deben ejecutarse como parte del pipeline de integración continua.
- Ningún artefacto debe desplegarse si las pruebas fallan.

---

## 15. Restricciones de infraestructura

| Aspecto | Decisión | Estado |
|---------|----------|--------|
| Plataforma en la nube | Microsoft Azure | Confirmado |
| Base de datos | NoSQL en Azure | Confirmado (proveedor pendiente) |
| Servicio de alojamiento | Por confirmar | Pendiente (DEC-007) |
| Servicio de secretos | Por confirmar | Pendiente (DEC-003) |
| Servicio de identidad | Por confirmar | Pendiente (DEC-002) |
| CI/CD | Por confirmar | Pendiente (DEC-006) |

### Principios de infraestructura

- La aplicación debe poder configurarse para distintos entornos mediante variables de entorno.
- La infraestructura como código es deseable pero no es un requisito de la fase actual.
- Los recursos de Azure no se crean manualmente en producción sin documentación.

---

## 16. Riesgos y dependencias

### Dependencias externas críticas

| Dependencia | Impacto | Estado |
|-------------|---------|--------|
| Selección del proveedor NoSQL (DEC-001) | Bloquea el diseño de infraestructura de datos | Pendiente |
| Selección del mecanismo de autenticación (DEC-002) | Bloquea el diseño de seguridad de endpoints | Pendiente |
| Aprobación de la estructura de capas (DEC-005) | Bloquea el inicio de implementación | Pendiente |
| Contratos de API con los clientes (Flutter, Angular) | Puede afectar el diseño de DTOs | Pendiente (SUP-001) |

### Riesgos principales

Ver `memoria.md` sección 7 para el registro completo de riesgos.

---

## 17. Decisiones pendientes

Ver `memoria.md` sección 5 para el listado completo de decisiones pendientes con sus identificadores.

Las decisiones que afectan directamente a esta especificación son:

- **DEC-001:** Selección del proveedor NoSQL.
- **DEC-002:** Mecanismo de autenticación.
- **DEC-005:** Estructura definitiva de capas.
- **DEC-010:** Formato exacto de respuestas de error.
- **DEC-011:** Política de paginación y filtrado.

---

## 18. Criterios de aceptación verificables de la arquitectura base

Los siguientes criterios deben poderse verificar durante y después de la fase de implementación de la arquitectura base. **No se afirma que estén cumplidos actualmente.**

| ID | Criterio | Cómo verificarlo |
|----|----------|-----------------|
| AC-ARCH-01 | La solución .NET está organizada en proyectos separados por capa (o equivalente) | Inspección de la estructura de la solución |
| AC-ARCH-02 | El proyecto de dominio no tiene referencias a proyectos de infraestructura ni de API | Inspección de las referencias del proyecto Domain |
| AC-ARCH-03 | La API usa el prefijo `/api/v1/` en todas las rutas | Prueba de integración o inspección de rutas |
| AC-ARCH-04 | Las respuestas de la API están en formato JSON | Prueba de integración con cualquier endpoint activo |
| AC-ARCH-05 | Los controladores no contienen lógica de negocio | Revisión de código |
| AC-ARCH-06 | Ningún archivo versionado contiene secretos | Revisión de `.gitignore` y de `appsettings.json` |
| AC-ARCH-07 | El endpoint `/health` responde con código 200 | Prueba de integración o prueba manual |
| AC-ARCH-08 | Los errores no controlados devuelven respuestas estructuradas sin detalles internos | Prueba de integración con entradas inválidas o errores forzados |
| AC-ARCH-09 | El proyecto de infraestructura implementa las interfaces definidas en el dominio | Inspección de código e inyección de dependencias |
| AC-ARCH-10 | Las pruebas unitarias de dominio y aplicación pasan sin infraestructura real | Ejecución del conjunto de pruebas |
| AC-ARCH-11 | La configuración sensible se lee de variables de entorno, no de `appsettings.json` | Inspección de la configuración y prueba en entorno de desarrollo |
| AC-ARCH-12 | La aplicación se inicia correctamente en el entorno de desarrollo | Ejecución de `dotnet run` o equivalente |

---

*Esta especificación debe revisarse y aprobarse antes de iniciar la implementación. Cualquier cambio debe seguir el proceso de control de cambios descrito en `constitution.md`.*
