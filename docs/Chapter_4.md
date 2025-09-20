# Capítulo IV: Solution Software Design

## 4.1. Strategic-Level Domain-Driven Design.

En esta sección se presenta el proceso que seguimos para identificar y delimitar los bounded contexts de nuestro sistema. Para ello, aplicamos las técnicas de EventStorming y el Bounded Context Canvas, herramientas clave que nos permitieron mapear los dominios de negocio, descubrir fronteras naturales entre sus componentes y alinear la arquitectura con la estructura organizacional y los flujos de trabajo reales.

### 4.1.1. Design-Level EventStorming.

Para la elaboración del EventStorming, el equipo se organizó para encontrar una primera aproximación al
 modelado del dominio de nuestro proyecto. Durante este proceso seguimos una serie de 9 pasos


 **Paso 1: Collect Domain Events** En este primer paso, identificamos todos los eventos relevantes del dominio
 que ocurren en nuestro sistema. Estos eventos representan hechos importantes que suceden durante el
 proceso de negocio y los capturamos con post-its de color naranja

 [![Event-Storming-plantcare.jpg](https://i.postimg.cc/fL76cGK4/Event-Storming-plantcare.jpg)](https://postimg.cc/47dLZFqw)

 **Paso 2: Timeline** Organizamos todos los eventos identificados en una línea temporal, colocándolos en orden
 cronológico para visualizar mejor el flujo del proceso y entender la secuencia natural de acciones en el
 sistema.

[![Event-Storming-plantcare-1.jpg](https://i.postimg.cc/TYsHD26L/Event-Storming-plantcare-1.jpg)](https://postimg.cc/mtQwxshB)

**Paso 3: Pain and Pivotal points** Identificamos los puntos problemáticos (pain points) y los momentos clave
 (pivotal points) en nuestro proceso. Estos representan áreas que requieren atención especial o que son críticas
 para el funcionamiento del sistema.


[![Event-Storming-plantcare-2.jpg](https://i.postimg.cc/NMbdfBD0/Event-Storming-plantcare-2.jpg)](https://postimg.cc/Q99QfLRL)


 **Paso 4: Commands** Agregamos los comandos (representados con post-its azules) que desencadenan los
 eventos. Estos comandos son las acciones que los usuarios o sistemas externos realizan para provocar
 cambios en el sistema

[![Event-Storming-plantcare-3.jpg](https://i.postimg.cc/2jc0sj3c/Event-Storming-plantcare-3.jpg)](https://postimg.cc/YjFNgH6Y)

**Paso 5: Policies** Definimos las políticas o reglas de negocio (con post-its morados) que reaccionan a ciertos
 eventos y generan nuevos eventos como resultado. Estas políticas automatizan decisiones basadas en eventos
 previos.

[![Event-Storming-plantcare-4.jpg](https://i.postimg.cc/d0Y62LS1/Event-Storming-plantcare-4.jpg)](https://postimg.cc/YvdQkq7K)

**Paso 6: Read models**  Identificamos los modelos de lectura o vistas que los usuarios necesitan para tomar
 decisiones. Estos representan la información que debe estar disponible en determinados puntos del proceso.

 [![Event-Storming-plantcare-5.jpg](https://i.postimg.cc/cCrBxY6D/Event-Storming-plantcare-5.jpg)](https://postimg.cc/kRPbw2Q8)

  **Paso 7: External System** Marcamos los sistemas externos (con post-its rosados) que interactúan con nuestra
 solución. Estos son componentes fuera de nuestro control directo pero que tienen influencia en el proceso

[![Event-Storming-plantcare-6.jpg](https://i.postimg.cc/pVhGzh2f/Event-Storming-plantcare-6.jpg)](https://postimg.cc/G9Rx1pTt)


**Paso 8: Aggregates** Agrupamos los comandos y eventos relacionados en unidades lógicas llamadas
 agregados (representados con post-its amarillos). Cada agregado encapsula un conjunto coherente de
 funcionalidades. 

 [![Event-Storming-plantcare-7.jpg](https://i.postimg.cc/ZqsHyZ2s/Event-Storming-plantcare-7.jpg)](https://postimg.cc/3ypmsMK2)

  **Paso 9: Bounded Context** Finalmente, identificamos los contextos delimitados o bounded contexts, que son
 áreas de responsabilidad distintas dentro del sistema.

 [![Event-Storming-plantcare-8.jpg](https://i.postimg.cc/nz8sWPDc/Event-Storming-plantcare-8.jpg)](https://postimg.cc/Z9cKBjH1)


#### 4.1.1.1 Candidate Context Discovery.

 A partir del EventStorming realizado en Miro, nuestro equipo llevó a cabo una sesión de Candidate Context
 Discovery para identificar los bounded contexts de nuestra solución. Utilizamos principalmente la técnica
 look-for-pivotal-events durante la sesión.
 
 
 **Proceso de identificación**
 Comenzamos revisando el modelo completo que habíamos construido, prestando especial atención a los
 eventos pivote y agregados identificados

[![Event-Storming-plantcare-2.jpg](https://i.postimg.cc/NMbdfBD0/Event-Storming-plantcare-2.jpg)](https://postimg.cc/Q99QfLRL)


Detección de agrupaciones naturales: Identificamos patrones y agrupaciones naturales de comandos, eventos
 y políticas que trabajaban sobre las mismas entidades o procesos. 

 [![Event-Storming-plantcare-6.jpg](https://i.postimg.cc/pVhGzh2f/Event-Storming-plantcare-6.jpg)](https://postimg.cc/G9Rx1pTt)

 Una vez relacionado todo el event storming hacemos la agrupacion para infetificar y aplicar el contexto de los bouded context 

 **1. Start-with-Value**

Comenzamos identificando las áreas core del dominio, es decir, aquellas con mayor impacto en la propuesta de valor del sistema.

- Core: Plant Management, Device Management (IoT), Data Telemetry, Analysis & Reporting.

- Supporting: Auth & Identity, Billing & Subscription, Notification & Rules Engine.

- eneric: Platform, Community/Social.

**2.- Start-with-Simple**

Para no perdernos en la complejidad, descompusimos el flujo en pasos secuenciales simples, lo que permitió distinguir qué parte del sistema debía encargarse de cada responsabilidad.

**3.- Look-for-Pivotal-Events**
Identificamos eventos clave que marcaban transiciones entre subsistemas. Ejemplos:

- “Sensor data received” → frontera entre Device Management y Data Telemetry.

- “Subscription activated” → frontera entre Billing y Platform.

- “Rule triggered” → frontera entre Notification Engine y Plant Management.

[![Event-Storming-plantcare-8.jpg](https://i.postimg.cc/nz8sWPDc/Event-Storming-plantcare-8.jpg)](https://postimg.cc/Z9cKBjH1)


__Primer agrupamiento__ 
Se delimitaron los contextos básicos de Auth & Identity y Device Management (IoT). Estos responden a responsabilidades claras: autenticación de usuarios y control de hardware. 

[![Event-Storming-plantcare-9.jpg](https://i.postimg.cc/DyCPN7yv/Event-Storming-plantcare-9.jpg)](https://postimg.cc/qz3KhV3S)

__Segundo agrupamiento__

Se aislaron los contextos centrales de negocio: Plant Management y Data Telemetry. Aquí ubicamos la lógica principal sobre cuidado y monitoreo de plantas.


[![Event-Storming-plantcare-10.jpg](https://i.postimg.cc/kXZt8Ggb/Event-Storming-plantcare-10.jpg)](https://postimg.cc/Mv7TJWR6)


__Tercer agrupamiento__ 

Se añadieron los contextos complementarios: Notification & Rules Engine y Community/Social, encargados de interacción y comunicación entre usuarios y el sistema.

[![Event-Storming-plantcare-11.jpg](https://i.postimg.cc/gJX0Gq3t/Event-Storming-plantcare-11.jpg)](https://postimg.cc/TLxx9b7n)


Consolidación final
El resultado fue un mapa de 9 bounded contexts:

- Auth & Identity

- Device Management (IoT)

- Platform

- Billing & Subscription

- Plant Management

- Data Telemetry

- Analysis & Reporting

- Notification & Rules Engine

- Community / Social

Cada uno de ellos tiene responsabilidades y fronteras bien definidas, reduciendo la complejidad y facilitando la futura arquitectura basada en microservicios o módulos independientes.

#### 4.1.1.2 Domain Message Flows Modeling.

 Los Domain Message Flows modelan las interacciones entre los diferentes bounded contexts, mostrando
 cómo se comunican entre sí mediante comandos, eventos y consultas. A continuación, presentamos los flujos
 de mensaje para cuatro escenarios clave de nuestra aplicación:

 [![Event-Storming-plantcare-12.jpg](https://i.postimg.cc/hGf7ZXMc/Event-Storming-plantcare-12.jpg)](https://postimg.cc/LqFXn6rb)


 [![Event-Storming-plantcare-13.jpg](https://i.postimg.cc/wMdyB0zj/Event-Storming-plantcare-13.jpg)](https://postimg.cc/YGbqnNj5)

 [![Event-Storming-plantcare-14.jpg](https://i.postimg.cc/28GbzQKC/Event-Storming-plantcare-14.jpg)](https://postimg.cc/WhDb8kVy)

 [![Event-Storming-plantcare-15.jpg](https://i.postimg.cc/CK3dvmzs/Event-Storming-plantcare-15.jpg)](https://postimg.cc/HJtpn00r)

 Estos flujos de mensaje son pilares fundamentales de la arquitectura del sistema, ya que revelan cómo los distintos Bounded Contexts se coordinan de forma coherente, asíncrona y bien definida. Al mapear cada comando, evento y consulta, no solo visualizamos el flujo de información entre componentes, sino que también identificamos puntos críticos de acoplamiento, posibles cuellos de botella en la comunicación y oportunidades para optimizar la escalabilidad y la resiliencia. Además, garantizan que la arquitectura esté alineada con los casos de uso del negocio, asegurando que cada interacción tenga propósito, trazabilidad y cumplimiento de contratos de dominio fundamentales para construir un sistema robusto, mantenible y adaptativo a largo plazo.

#### 4.1.1.3 Bounded Context Canvases.


 Los Bounded Context Canvases son herramientas visuales que nos permiten documentar las características
 fundamentales de cada contexto delimitado, capturando su propósito estratégico, modelo de dominio,
 lenguaje ubicuo, políticas y relaciones con otros contextos. A continuación, presentamos los canvases para
 nuestros cuatro bounded contexts identificados, que nos ayudaron a definir claramente las responsabilidades
 y límites de cada uno.

[![Event-Storming-plantcare-18.jpg](https://i.postimg.cc/wT3KR8bv/Event-Storming-plantcare-18.jpg)](https://postimg.cc/1fx7bTSh)

 [![Event-Storming-plantcare-19.jpg](https://i.postimg.cc/CL23jPW4/Event-Storming-plantcare-19.jpg)](https://postimg.cc/SJW14rQX)

 <img src="https://i.postimg.cc/Hk7f30m1/Event-Storming-plantcare-20.jpg" alt="Event Storming Plantcare" width="480"/>

#### 4.1.2. Context Mapping.

En esta sección se explica y evidencia el proceso de elaboración de un conjunto de *context maps*, es decir, visualizaciones de las relaciones estructurales entre los **bounded contexts** identificados en el dominio. El equipo realizó una revisión de la información recolectada durante la fase de *EventStorming* y la utilizó para producir los diseños candidatos.  

El objetivo de este proceso es explorar y evaluar distintas configuraciones posibles de los bounded contexts y sus relaciones, considerando las buenas prácticas de **Domain-Driven Design (DDD)**.


#### 1. Revisión de la información recolectada
El equipo inició el trabajo revisando los resultados de la sesión de *EventStorming*. De ahí se obtuvieron los eventos de dominio, comandos y agregados que permitieron identificar las áreas del dominio más relevantes y con mayor valor para el negocio.  

Se discutió cómo estos elementos podrían agruparse en bounded contexts iniciales, considerando sus responsabilidades y las dependencias entre ellos.

#### 2. Preguntas exploratorias
Para evaluar diferentes alternativas de diseño, el equipo aplicó una serie de preguntas clave sugeridas en la literatura de DDD:

- **¿Qué pasaría si movemos este capability a otro bounded context?**  
  Esta pregunta permitió analizar la coherencia y consistencia de cada bounded context, evaluando si su alcance estaba correctamente delimitado.

- **¿Qué pasaría si descomponemos este capability y movemos uno de los sub-capabilities a otro bounded context?**  
  Con esto se exploró la posibilidad de dividir funcionalidades demasiado amplias y redistribuirlas de manera más balanceada.

- **¿Qué pasaría si partimos el bounded context en múltiples bounded contexts?**  
  En este caso se consideró si un contexto estaba asumiendo demasiadas responsabilidades y podía beneficiarse de ser subdividido.

- **¿Qué pasaría si tomamos este capability de estos 3 contexts y lo usamos para formar un nuevo context?**  
  Este análisis ayudó a detectar funcionalidades comunes y repetidas, abriendo la posibilidad de consolidarlas en un nuevo contexto especializado.

- **¿Qué pasaría si duplicamos una funcionalidad para romper la dependencia?**  
  Se evaluó la conveniencia de la duplicación estratégica para reducir el acoplamiento y mejorar la autonomía de ciertos equipos.

- **¿Qué pasaría si creamos un shared service para reducir la duplicación entre múltiples bounded contexts?**  
  Aquí se discutió el uso de un servicio compartido como estrategia para optimizar recursos sin comprometer demasiado la independencia de cada contexto.

- **¿Qué pasaría si aislamos los core capabilities y movemos los otros a un context aparte?**  
  Esta pregunta permitió identificar cuáles eran las capacidades centrales (*core domain*) y cuáles podían derivarse hacia contextos de soporte o genéricos.

#### 3. Diseño de mapas candidatos
Con base en las preguntas anteriores, se elaboraron diferentes *context maps* candidatos, cada uno reflejando una alternativa distinta de organización. Estos mapas mostraron cómo se podían distribuir las responsabilidades y qué relaciones se establecían entre los equipos o bounded contexts.

Se aplicaron **patrones de relaciones de contextos** descritos en DDD, entre ellos:

- **Open-Host Service:** aplicado en los contextos *Auth*, *Telemetry* y *Rules*, donde se expone un modelo o API pública para que otros contextos puedan integrarse.  
- **Conformist:** presente en la relación de *Auth* hacia *Platform*, donde este último debe alinearse sin posibilidad de imponer cambios.  
- **Anti-Corruption Layer (ACL):** usado entre *Platform* y *Billing*, permitiendo que el modelo de facturación no contamine al resto del sistema.  
- **Customer/Supplier:** visible en las relaciones de *Platform ↔ Billing*, *Telemetry → Analysis*, y *Plant → Analysis*, reflejando dependencias claras de consumidor/proveedor.  
- **Published Language:** aplicado en *Device ↔ Telemetry* y *Telemetry → Rules*, estandarizando los contratos de comunicación.  
- **Partnership:** en *Device ↔ Telemetry* y *Rules ↔ Device*, donde ambos contextos necesitan colaborar de manera cercana.  
- **Shared Kernel:** presente en *Community ↔ Platform*, donde ambos contextos comparten un subconjunto del modelo y deben coordinarse.  
- **Separate Ways:** también en *Community ↔ Platform*, indicando que ciertos aspectos se manejan de forma independiente para reducir el acoplamiento.  


#### 4. Aplicación de buenas prácticas en los context maps
Durante el proceso, el equipo consideró las siguientes buenas prácticas:  

- **Trabajar con context maps pequeños para preguntas explícitas:** cada mapa se diseñó con un propósito específico, evitando diagramas sobrecargados que generen confusión.  
- **Documentar y explicar los patrones usados:** se acompañaron los mapas con explicaciones claras de los patrones aplicados, de modo que los stakeholders pudieran entender su propósito.  
- **Usar múltiples perspectivas:** se generaron mapas diferentes para responder a distintas preguntas (ejemplo: dependencias técnicas, relaciones organizacionales, influencia entre equipos).  


#### Evidencia gráfica
Al finalizar, los mapas de contexto resultantes se documentaron en forma de diagramas visuales. Estos diagramas muestran tanto los **bounded contexts** como las relaciones entre ellos, junto con los patrones aplicados.  

Aquí se insertará la imagen del diagrama  exportado a formato gráfico:

[![Untitled-diagram-Mermaid-Chart-2025-09-18-233901.png](https://i.postimg.cc/VsBHNnbf/Untitled-diagram-Mermaid-Chart-2025-09-18-233901.png)](https://postimg.cc/grjKSwDQ)

### 4.1.3. Software Architecture.

#### 4.1.3.1. Software Architecture System Landscape Diagram.

#### 4.1.3.2. Software Architecture Context Level Diagrams.

#### 4.1.3.2. Software Architecture Container Level Diagrams.

#### 4.1.3.3. Software Architecture Deployment Diagrams.

## 4.2. Tactical-Level Domain-Driven Design
En esta sección, el equipo aborda el diseño táctico de la solución siguiendo los principios de Domain‑Driven Design (DDD), traduciendo los Bounded Contexts previamente definidos en patrones y estructuras de código concretos. Cada subcapítulo se centra en uno de los contextos, describiendo sus agregados, repositorios, servicios de dominio y fábricas, así como las variantes y contratos que rigen su comportamiento interno. De este modo, se conecta la visión estratégica del dominio con decisiones de implementación precisas, garantizando que el software refleje fielmente las reglas de negocio y mantenga la coherencia del lenguaje ubicuo.

Para cada Bounded Context, se propone una arquitectura modular basada en capas tácticas, modelos de entidad, lógica de dominio, interfaces de infraestructura y adaptadores, y se aplican patrones de diseño. Además, se incluyen diagramas de clases. Este enfoque permite iterar rápidamente sobre el diseño interno sin perder alineación con los objetivos del negocio ni generar acoplamientos indebidos entre contextos (Ford et al., 2021).
## 4.2.1. Bounded Context: Auth&Identity

En la capa de dominio de Auth & Identity se definen las entidades, objetos de valor, agregados, servicios de dominio y repositorios encargados de gestionar el ciclo de vida de la autenticación e identidad de los usuarios. Aquí residen las reglas de negocio que garantizan la seguridad, consistencia y control de acceso de todo el sistema.

### 4.2.1.1. Domain Layer. 

En la capa de dominio de Auth & Identity se definen las entidades, objetos de valor, agregados, servicios de dominio y repositorios encargados de gestionar el ciclo de vida de la autenticación e identidad de los usuarios. Aquí residen las reglas de negocio que garantizan la seguridad, consistencia y control de acceso de todo el sistema.

**User Account**

| Propiedad     | Valor                                                                                 |
|---------------|---------------------------------------------------------------------------------------|
| **Nombre**    | UserAccount                                                                           |
| **Categoría** | Aggregate Root                                                                        |
| **Propósito** | Representar la cuenta de usuario registrada en el sistema, incluyendo credenciales,   |

**Atributos de UserAccount**

| Nombre   | Tipo de dato      | Visibilidad | Descripción                              |
|----------|-------------------|-------------|------------------------------------------|
| userId   | UserId            | Privada     | Identificador único de la cuenta         |
| FullName | FullName          | Privada     | Nombre completo del usuario              |
| Email    | Email             | Privada     | Dirección de correo electrónico          |
| Password | passwordHash      | Privada     | Hash de la contraseña                    |
| Status   | AccountStatus      | Privada     | Estado de la cuenta (activa, Desactiva) |
| CreatedAt | DateTime          | Privada     | Fecha de creación de la cuenta           |
| UpdatedAt | DateTime          | Privada     | Fecha de la última actualización         |

**Metodos de User Account**

| Nombre                | 	Tipo de retorno | 	Visibilidad	 | Descripción                                         |
|-----------------------|------------------|---------------|-----------------------------------------------------|
| VerifyEmail	          | void	            | public	       | Marca la cuenta como verificada tras código exitoso |
| ChangePassword        | 	void            | 	public       | 	Permite actualizar la contraseña                   |
| RequestPasswordReset	 | PasswordReset	   | public	       | Solicita un proceso de recuperación de contraseña   |
| UpdateProfile	        | void	            | public	       | Modifica nombre completo o email                    |
| Deactivate	           | void	            | public	| Desactiva la cuenta del usuario                     |
| Block	                | void             | public	| Bloquea la cuenta tras intentos fallidos            | 
| Activate	             | void	            | public	| Reactiva la cuenta si está suspendida               |

**UserId**

| Propiedad	| Valor |
|---------------|---------------------------------------------------------------------------------------|
| Nombre	| UserId |
| Categoría	| Value Object |
| Propósito	| Identificador único de usuario |

**Atributos de UserId**

| Nombre	| Tipo de dato	| Visibilidad	| Descripción |
|----------|--------------------|-------------|------------------------------------------|
| Value | Guid / Long	| private	| Identificador único numérico o GUID |

**EmailVerification**

| Propiedad	| Valor |
|---------------|---------------------------------------------------------------------------------------|
| Nombre	| EmailVerification | 
| Categoría	| Entity |
| Propósito	| Representar un proceso de verificación de correo electrónico. | 

**Atributos de EmailVerification**

| Nombre	| Tipo de dato	| Visibilidad	| Descripción |
|----------|--------------------|-------------|------------------------------------------|
| Code	| string	| private	| Código generado para verificación |
| UserId	| UserId	| private	| Usuario asociado | 
| ExpiresAt	| DateTime	| private	| Fecha de expiración del código |
| Verified	| bool	| private	| Indica si ya fue verificado |

**PasswordReset**

| Propiedad | Valor |
|---------------|---------------------------------------------------------------------------------------|
| Nombre |	PasswordReset |
| Categoría |	Entity |
| Propósito |	Representar un proceso de recuperación de contraseña solicitado por el usuario |.

**Atributos de PasswordReset**

| Nombre	                                | Tipo de dato	| Visibilidad	| Descripción |
|----------------------------------------|--------------------|-------------|------------------------------------------|
| Token	                                 | string	| private	| Código de recuperación |
| UserId	| UserId	| private	| Usuario asociado | 
| ExpiresAt	| DateTime	| private	| Fecha de expiración |
| Used	| bool	| private	| Marca si el token ya fue consumido |

**Session**

| Propiedad	| Valor |
|---------------|---------------------------------------------------------------------------------------|
|Nombre	| Session |
| Categoría	| Entity |
| Propósito	| Representar una sesión de usuario iniciada y autenticada. |

**Atributos de Session**

| Nombre	| Tipo de dato	| Visibilidad	 | Descripción                                  |
|----------|--------------------|--------------|----------------------------------------------|
| SessionId	| string	| private	     | Identificador de la sesión                   |
|UserId	| UserId	| private	| Usuario asociado                             |
| CreatedAt	| DateTime	| private	| Inicio de la sesión                          |
| ExpiresAt	| DateTime	| private	| Fecha de expiración                          |
| Revoked	| bool	| private	| Marca si la sesión fue cerrada o invalidada  |


**Domain Services**

**Authenticator**

| Propiedad	| Valor |
|---------------|---------------------------------------------------------------------------------------|
| Nombre	| Authenticator |
| Categoría	| Domain Service |
| Propósito	| Validar credenciales de usuario y emitir sesiones seguras. |

**Métodos de Authenticator**

| Nombre	| Tipo de retorno	| Visibilidad	| Descripción |
|-----------------------|------------------|---------------|-----------------------------------------------------|
| Authenticate	| Session	| public	| Autentica usuario y crea sesión |
| ValidateToken	| bool	| public	| Valida un token de sesión |
| RevokeSession	| void	| public	| Revoca sesión activa |

**Repositorios**

**IUserAccountRepository**

| Propiedad	| Valor                  |
|---------------|------------------------|
| Nombre	| IUserAccountRepository |
| Categoría	| Repository|
| Propósito	| Persistencia de cuentas de usuario|

**Métodos de IUserAccountRepository**

| Nombre	           | Tipo de retorno	 | Visibilidad	| Descripción|
|-------------------|------------------|---------------|-----------------------------------------------------|
| GetByIdAsync	     | UserAccount?	    | public	| Obtiene cuenta por Id|
| FindByEmailAsync	 | UserAccount?	| public	| Busca cuenta por correo|
| SaveAsync	        | UserAccount	| public	| Persiste cuenta|
| DeleteAsync	      | bool	| public	| Elimina lógicamente la cuenta|

**ISessionRepository**

| Propiedad	| Valor|
|---------------|------------------------|
| Nombre	| ISessionRepository| 
|Categoría	|Repository|
|Propósito	|Gestionar sesiones de usuario|

**Métodos de ISessionRepository**

|Nombre	|Tipo de retorno	|Visibilidad	|Descripción|
|-----------------------|------------------|---------------|-----------------------------------------------------|
|FindBySessionId	|Session?	|public	|Busca sesión por Id|
|Store	|void	|public|	Persiste nueva sesión|
|Revoke	|void	|public	|Revoca sesión|
|RevokeAllForUser	|void	|public	|Revoca todas las sesiones activas de un usuario|

### 4.2.1.2. Interface Layer. 

En la capa de interfaz del Bounded Context de Auth & Identity se definen los controladores REST que actúan como punto de entrada para solicitudes externas. Estos endpoints permiten a aplicaciones cliente (web, móviles, integraciones de terceros) interactuar con las funciones de registro, autenticación, recuperación de credenciales y gestión de perfil de usuario.
La interfaz está organizada en controladores especializados, cada uno con rutas y acciones bien definidas, garantizando simplicidad, seguridad y separación de responsabilidades.

**UserAccountController**

|Propiedad	|Valor|
|---------------|---------------------------------------------------------------------------------------|
|Nombre	|UserAccountController|
|Categoría	|Controller|
|Propósito	|Exponer endpoints para la gestión de cuentas de usuario|
|Ruta	|/api/users|

**Métodos de UserAccountController**

|Nombre	|Ruta	|Acción	|Handle|
|-----------------------|------------------|---------------|-----------------------------------------------------|
|GetById	|/{userId}	|Obtiene los datos de un usuario	|GetUserByIdQuery|
|UpdateProfile	|/{userId}/profile	|Actualiza nombre y email	|UpdateUserProfileCommand|
|ChangePassword	|/{userId}/password	|Cambia contraseña	|ChangeUserPasswordCommand|
|Deactivate	|/{userId}/deactivate	|Desactiva cuenta de usuario	|DeactivateUserCommand|
|Activate	|/{userId}/activate	|Reactiva cuenta suspendida	|ActivateUserCommand|
|Block	|/{userId}/block	|Bloquea cuenta tras intentos fallidos	|BlockUserCommand|

**AuthController**

|Propiedad	|Valor|
|---------------|---------------------------------------------------------------------------------------|
|Nombre	|AuthController|
|Categoría	|Controller|
|ropósito	|Gestiona registro, autenticación y sesiones de usuario|
|Ruta	|/api/auth|

**Métodos de AuthController**

|Nombre	|Ruta	|Acción	|Handle|
|-----------------------|------------------|---------------|-----------------------------------------------------|
|Register	|/register|Registra un nuevo usuario	|RegisterUserCommand|
|Verify	|/verify	|Valida código de verificación email	|VerifyEmailCommand|
|Login	|/login	|Inicia sesión, devuelve token	|LoginUserCommand|
|Logout	|/logout	|Revoca sesión activa	|RevokeSessionCommand|
|Refresh	|/refresh	|Renueva token de acceso	|RefreshTokenCommand|

**PasswordRecoveryController**

|Propiedad	|Valor|
|---------------|---------------------------------------------------------------------------------------|
|Nombre|	PasswordRecoveryController|
|Categoría	|Controller|
|Propósito	|Manejar procesos de recuperación de credenciales|
|Ruta	|/api/password|

**Métodos de PasswordRecoveryController**

|Nombre|	Ruta	|Acción	|Handle|
|-----------------------|------------------|---------------|-----------------------------------------------------|
|Request	|/forgot	|Solicita recuperación, envía código/email	|RequestPasswordResetCommand|
|VerifyCode	|/verify	|Valida el código de recuperación	|VerifyResetCodeCommand|
|Reset	|/reset	|Restablece contraseña	|ResetPasswordCommand|

**SessionController**

|Propiedad	|Valor|
|---------------|---------------------------------------------------------------------------------------|
|Nombre	|SessionController|
|Categoría|Controller|
|Propósito	|Gestionar sesiones activas de usuario|
|Ruta	|/api/sessions|

**Métodos de SessionController**

|Nombre	|Ruta	|Acción	|Handle|
|-----------------------|------------------|---------------|-----------------------------------------------------|
|GetActive	|/active/{userId}	|Obtiene sesiones activas de un usuario	|GetActiveSessionsQuery|
|Revoke	|/revoke/{sessionId}	|Revoca una sesión específica	|RevokeSessionCommand|
|RevokeAll	|/revokeAll/{userId}	|Revoca todas las sesiones del usuario	|RevokeAllSessionsCommand|

### 4.2.1.3. Application Layer. 

La capa de aplicación del Bounded Context Auth & Identity coordina la interacción entre la capa de interfaz y la capa de dominio. Su responsabilidad principal es orquestar comandos, consultas y eventos, asegurando la correcta ejecución de flujos como registro, autenticación, verificación, gestión de contraseñas, sesiones y cuentas de usuario.
No implementa reglas de negocio directamente, sino que delega al dominio, manteniendo así una separación clara de responsabilidades y asegurando la integridad transaccional del sistema.

**Command Handlers**

**UserRegisterCommandHandler**

|Propiedad	|Valor|
|---------------|---------------------------------------------------------------------------------------|
|Nombre	|UserRegisterCommandHandler|
|Categoría|	Command Handler|
|Propósito	|Registrar un usuario nuevo en el sistema|
|Comando	|RegisterUserCommand|

**UserVerifyEmailCommandHandler**

|Propiedad	|Valor|
|---------------|---------------------------------------------------------------------------------------|
|Nombre	|UserVerifyEmailCommandHandler|
|Categoría	|Command Handler|
|Propósito	|Validar código de verificación de email|
|Comando	|VerifyEmailCommand|

**UserLoginCommandHandler**

|Propiedad	|Valor|
|---------------|---------------------------------------------------------------------------------------|
|Nombre	|UserLoginCommandHandler|
|Categoría	|Command Handler|
|Propósito	|Iniciar sesión de un usuario|
|Comando	|LoginUserCommand|

**UserLogoutCommandHandler**

|Propiedad|	Valor|
|---------------|---------------------------------------------------------------------------------------|
|Nombre	|UserLogoutCommandHandler|
|Categoría	|Command Handler|
|Propósito	|Cerrar sesión de un usuario|
|Comando	|LogoutUserCommand|

**PasswordResetRequestCommandHandler**

|Propiedad	|Valor|
|---------------|---------------------------------------------------------------------------------------|
|Nombre	|PasswordResetRequestCommandHandler|
|Categoría	|Command Handler|
|Propósito	|Iniciar proceso de recuperación de contraseña|
|Comando	|RequestPasswordResetCommand|

**PasswordResetCommandHandler**

|Propiedad	|Valor|
|---------------|---------------------------------------------------------------------------------------|
|Nombre	|PasswordResetCommandHandler|
|Categoría|Command Handler|
|Propósito	|Restablecer contraseña de usuario|
|Comando	|ResetPasswordCommand|

**UserProfileUpdateCommandHandler**

|Propiedad|Valor|
|---------------|---------------------------------------------------------------------------------------|
| Nombre	|UserProfileUpdateCommandHandler|
|Categoría	|Command Handler|
|Propósito	|Actualizar datos de perfil de usuario|
|Comando	|UpdateUserProfileCommand|

**UserDeactivateCommandHandler**

|Propiedad	|Valor|
|---------------|---------------------------------------------------------------------------------------|
|Nombre	|UserDeactivateCommandHandler|
|Categoría	|Command Handler|
|Propósito	|Desactivar cuenta de usuario|
|Comando	|DeactivateUserCommand|

**UserBlockCommandHandler**

|Propiedad	|Valor|
|---------------|---------------------------------------------------------------------------------------|
|Nombre	|UserBlockCommandHandler|
|Categoría	|Command Handler|
|Propósito	|Bloquear cuenta tras intentos fallidos de inicio de sesión|
|Comando	|BlockUserCommand|

**Query Handlers**

**GetUserByIdQueryHandler**

|Propiedad	|Valor|
|---------------|---------------------------------------------------------------------------------------|
|Nombre	|GetUserByIdQueryHandler|
|Categoría	|Query Handler|
|Propósito|Obtener datos de un usuario por Id|
|Query	|GetUserByIdQuery|

**GetActiveSessionsQueryHandler**

|Propiedad	|Valor|
|---------------|---------------------------------------------------------------------------------------|
|Nombre	|GetActiveSessionsQueryHandler|
|Categoría	|Query Handler|
|Propósito	|Obtener sesiones activas de un usuario|
|Query	|GetActiveSessionsQuery|

**Event Handlers**

**RegisteredUserEventHandler**

|Propiedad|	Valor|
|---------------|---------------------------------------------------------------------------------------|
|Nombre|	RegisteredUserEventHandler|
|Categoría|	Event Handler|
|Propósito|Gestionar evento tras registro exitoso (ej. enviar verificación email)|
|Evento	|UserRegisteredEvent|

**UserVerifiedEventHandler**

|Propiedad	|Valor|
|---------------|---------------------------------------------------------------------------------------|
|Nombre	|UserVerifiedEventHandler|
|Categoría	|Event Handler|
|Propósito|	Gestionar acciones tras verificación de email exitosa|
|Evento	|UserVerifiedEvent|

**UserLoggedInEventHandler**

|Propiedad|	Valor|
|---------------|---------------------------------------------------------------------------------------|
|Nombre	|UserLoggedInEventHandler|
|Categoría	|Event Handler|
|Propósito|	Ejecutar acciones tras inicio de sesión exitoso (ej. auditoría)|
|Evento	|UserLoggedInEvent|

**UserLoggedOutEventHandler**

|Propiedad	|Valor|
|---------------|---------------------------------------------------------------------------------------|
|Nombre	|UserLoggedOutEventHandler|
|Categoría	|Event Handler|
|Propósito	|Ejecutar acciones tras cierre de sesión (ej. limpiar tokens)|
|Evento|	UserLoggedOutEvent|

**PasswordResetRequestedEventHandler**

|Propiedad	|Valor|
|---------------|---------------------------------------------------------------------------------------|
|Nombre	|PasswordResetRequestedEventHandler|
|Categoría	|Event Handler|
|Propósito	|Gestionar envío de email con código de recuperación|
|Evento	|PasswordResetRequestedEvent|

**PasswordResetCompletedEventHandler**

|Propiedad|	Valor|
|---------------|---------------------------------------------------------------------------------------|
|Nombre	|PasswordResetCompletedEventHandler|
|Categoría	|Event Handler|
|Propósito	|Gestionar acciones tras restablecimiento exitoso de contraseña|
|Evento|	PasswordResetCompletedEvent|

### 4.2.1.4. Infrastructure Layer. 
La capa de infraestructura del Bounded Context de Auth & Identity actúa como puente entre la lógica de negocio y los mecanismos técnicos de persistencia, seguridad y comunicación externa. Aquí se implementan las dependencias necesarias para la gestión de usuarios, autenticación y sesiones, garantizando la interacción confiable con bases de datos, proveedores de tokens y almacenamiento de credenciales.

Esta capa concreta las abstracciones definidas en el dominio a través de repositorios, contextos de base de datos y servicios técnicos. Su diseño asegura un desacoplamiento respecto a la lógica central, permitiendo reemplazar o evolucionar tecnologías sin alterar las reglas de negocio. Además, aporta eficiencia, escalabilidad y robustez en la gestión de identidades y accesos, alineándose con los objetivos funcionales y no funcionales del sistema.

**UserRepository**

|Propiedad	|Valor|
|---------------|---------------------------------------------------------------------------------------|
|Nombre|UserRepository|
|Categoría	|Repositorio|
|Propósito|	Persistir y consultar entidades de usuario|
|Interfaz	|IUserRepository|

**SessionRepository**

|Propiedad	|Valor|
|---------------|---------------------------------------------------------------------------------------|
|Nombre	|SessionRepository|
|Categoría	|Repositorio|
|Propósito	|Persistir y consultar entidades de sesión|
|Interfaz	|ISessionRepository|

**AuthDbContext**

|Propiedad	|Valor|
|---------------|---------------------------------------------------------------------------------------|
|Nombre|	AuthDbContext|
|Categoría	|ORM Context|
|Propósito	|Punto central de acceso a la base de datos para usuarios y sesiones|

### 4.2.1.5. Bounded Context Software Architecture ### Component Level Diagrams. 
### 4.2.1.6. Bounded Context Software Architecture Code Level Diagrams. 
#### 4.2.1.6.1. Bounded Context Domain Layer Class ### Diagrams. 
#### 4.2.1.6.2. Bounded Context Database Design Diagram.

## 4.2.2. Bounded Context: Plant Management
### 4.2.2.1. Domain Layer. 

En la capa de dominio de PlantProfile se definen las entidades, objetos de valor, agregados, servicios de dominio y repositorios encargados de gestionar el ciclo de vida de los perfiles de plantas. Aquí residen las reglas de negocio que garantizan la consistencia, trazabilidad y control del estado de cada planta en el sistema.

**PlantProfile**

|Propiedad|	Valor|
|---------------|---------------------------------------------------------------------------------------|
|Nombre	|PlantProfile|
|Categoría	|Aggregate Root|
|Propósito	|Representar el perfil de una planta registrada en el sistema, incluyendo su tipo, condiciones ideales y estado actual.|

**Atributos de PlantProfile**

|Nombre	|Tipo de dato	|Visibilidad	|Descripción|
|---------------|---------------|---------------|---------------|
|plantProfileId	|PlantProfileId	|Privada	|Identificador único del perfil|
|plantType	|PlantType	|Privada	|Tipo de planta (ej. cactus, orquídea)|
|conditions	|PlantConditions	|Privada	|Condiciones ideales configuradas|
|currentState	|PlantState	|Privada	|Estado actual de la planta|
|status	|ProfileStatus	|Privada	|Estado del perfil (activo, archivado, eliminado)|
|createdAt	|DateTime	|Privada	|Fecha de creación|
|archivedAt	|DateTime?	|Privada	|Fecha de archivado (si aplica)|

**Métodos de PlantProfile**

|Nombre	|Tipo de retorno	|Visibilidad	|Descripción|
|-----------------------|------------------|---------------|-----------------------------------------------------|
|ConfigureConditions	|void	|public	|Configura condiciones ideales de la planta|
|UpdateState	|void	|public	|Actualiza el estado de la planta|
|Archive	|void	|public	|Archiva el perfil de la planta|
|Delete	|void	|public	|Elimina definitivamente el perfil|
|Restore	|void	|public	|Restaura un perfil archivado|

**Value Objects**

**PlantProfileId**

| Propiedad	|Valor|
|---------------|---------------------------------------------------------------------------------------|
|Nombre	|PlantProfileId|
|Categoría |Value Object|
|Propósito |Identificador único del perfil de planta|

**Atributos de PlantProfileId**

|Nombre	|Tipo de dato	|Visibilidad	|Descripción|
|----------|--------------------|-------------|------------------------------------------|
|value	|Guid / Long	|private	|Identificador único numérico o GUID|

**PlantType**

| Propiedad	| Valor|
|-------------|---------------------------------------------------------------------------------------|
|Nombre| PlantType|
|Categoría |Value Object|
|Propósito |Representar el tipo de planta seleccionada (ej. cactus, orquídea).|

**PlantConditions**

| Propiedad | Valor|
|--------------|---------------------------------------------------------------------------------------|
|Nombre |PlantConditions|
|Categoría |Value Object|
|Propósito| Conjunto de condiciones ideales configuradas para el crecimiento de la planta.|

Atributos: temperatura, humedad, luz, riego.

**PlantState**

| Propiedad	| Valor|
|--------------|---------------------------------------------------------------------------------------|
|Nombre	|PlantState|
|Categoría| Value Object|
|Propósito|Estado actual de la planta (ej. saludable, en riesgo, muerta).|

**ProfileStatus**

| Propiedad	 | Valor|
|------------|---------------------------------------------------------------------------------------|
| Nombre	    |ProfileStatus|
|Categoría |Value Object|
|Propósito| Representar el estado del perfil (activo, archivado, eliminado).|

**Entidades auxiliares**

**PlantHistory**

|Propiedad|Valor|
|---------------|---------------------------------------------------------------------------------------|
|Nombre	|PlantHistory|
|Categoría| Entity|
|Propósito |Registrar cambios históricos de estado o condiciones en una planta.|

Atributos:

historyId

plantProfileId

eventType (estado actualizado, condiciones cambiadas, archivado, eliminado)

occurredAt

**Domain Services**
**PlantLifecycleManager**

|Propiedad	|Valor|
|---------------|---------------------------------------------------------------------------------------|
|Nombre	|PlantLifecycleManager|
|Categoría|	Domain Service|
|Propósito	|Gestionar reglas de negocio sobre el ciclo de vida de una planta (ej. eliminación tras 30 días de archivado).|

**Métodos de PlantLifecycleManager**

|Nombre	|Tipo de retorno	|Visibilidad	|Descripción|
|-----------------------|------------------|---------------|-----------------------------------------------------|
|CheckArchiveExpiration	|bool	|public|	Verifica si una planta archivada debe eliminarse|
|ApplyStateRules	|void	|public	|Aplica reglas de negocio según estado de la planta|

**Repositorios
IPlantProfileRepository**

|Propiedad	|Valor|
|---------------|---------------------------------------------------------------------------------------|
|Nombre	|IPlantProfileRepository|
|Categoría	|Repository|
|Propósito	|Persistencia de perfiles de planta|

**Métodos de IPlantProfileRepository**

|Nombre	|Tipo de retorno	|Visibilidad	|Descripción|
|-----------------------|------------------|---------------|-----------------------------------------------------|
|GetByIdAsync	|PlantProfile?|	public|	Obtiene perfil por Id|
|SaveAsync	|PlantProfile	|public	|Persiste perfil|
|DeleteAsync	|bool	|public|	Elimina perfil|
|ArchiveAsync|	bool	|public	|Archiva perfil|

**IPlantHistoryRepository**

|Propiedad|	Valor|
|---------------|---------------------------------------------------------------------------------------|
|Nombre	|IPlantHistoryRepository|
|Categoría	|Repository|
|Propósito	|Gestionar registros históricos de perfiles de planta|

**Métodos de IPlantHistoryRepository**

|Nombre	|Tipo de retorno	|Visibilidad	|Descripción|
|-----------------------|------------------|---------------|-----------------------------------------------------|
|LogEvent	|void	|public|	Registra un evento en el historial|
|GetHistory	|List<PlantHistory>|	public|	Obtiene historial de un perfil de planta|

### 4.2.2.2. Interface Layer. 

En la capa de interfaz del Bounded Context Plant Management se definen los controladores REST que actúan como punto de entrada para solicitudes externas. Estos endpoints permiten a aplicaciones cliente (web, móviles, integraciones con sensores o APIs externas) interactuar con las funciones de creación de perfiles de planta, gestión de estado, configuración de condiciones ideales, archivado y eliminación.

La interfaz está organizada en controladores especializados, cada uno con rutas y acciones bien definidas, garantizando simplicidad, seguridad y separación de responsabilidades.

**PlantProfileController**

|Propiedad	|Valor|
|---------------|---------------------------------------------------------------------------------------|
|Nombre	|PlantProfileController|
|Categoría	|Controller|
|Propósito	|Exponer endpoints para la creación, consulta, actualización, archivado y eliminación de perfiles de plantas.|
|Ruta	|/api/plants|

**Métodos de PlantProfileController**

|Nombre	|Ruta	|Acción	|Handle|
|-----------------------|------------------|---------------|-----------------------------------------------------|
|Create	|/	|Crea un nuevo perfil de planta	|CreatePlantProfileCommand|
|GetById	|/{plantId}	|Obtiene los datos de un perfil de planta	|GetPlantProfileByIdQuery|
|Update	|/{plantId}	|Actualiza datos generales de la planta	|UpdatePlantProfileCommand|
|Archive	|/{plantId}/archive	|Archiva el perfil de una planta	|ArchivePlantProfileCommand|
|Delete	|/{plantId}	|Elimina definitivamente un perfil de planta	|DeletePlantProfileCommand|

**PlantStatusController**

|Propiedad	|Valor|
|---------------|---------------------------------------------------------------------------------------|
|Nombre	|PlantStatusController|
|Categoría	|Controller|
|Propósito	|Gestionar el estado de las plantas (ej. salud, crecimiento, últimas mediciones).|
|Ruta	|/api/plants/{plantId}/status|

**Métodos de PlantStatusController**

|Nombre	|Ruta	|Acción	|Handle|
|-----------------------|-----------------|---------------|-----------------------------------------------------|
|UpdateStatus	|/update	|Actualiza el estado actual de la planta	|UpdatePlantStatusCommand|
|GetStatus|	/	|Obtiene el estado actual de la planta	|GetPlantStatusQuery|
|GetHistory|	/history	|Devuelve el historial de cambios de estado	|GetPlantHistoryQuery|

**PlantConditionsController**

|Propiedad	|Valor|
|---------------|---------------------------------------------------------------------------------------|
|Nombre	|PlantConditionsController|
|Categoría	|Controller|
|Propósito	|Configurar y consultar las condiciones ideales de una planta (riego, luz, temperatura).|
|Ruta	|/api/plants/{plantId}/conditions|

**Métodos de PlantConditionsController**

|Nombre|	Ruta	|Acción	|Handle|
|-----------------------|------------------|---------------|-----------------------------------------------------|
|Configure	|/	|Define condiciones ideales de la planta	|ConfigurePlantConditionsCommand|
|GetConditions|	/	|Consulta condiciones configuradas|	GetPlantConditionsQuery|

**ExternalPlantApiController**

|Propiedad	|Valor|
|---------------|---------------------------------------------------------------------------------------|
|Nombre|	ExternalPlantApiController|
|Categoría	|Controller|
|Propósito	|Integrarse con API externa de plantas para obtener información de referencia (tipos de planta, cuidados, recomendaciones).|
|Ruta	|/api/external/plants|

**Métodos de ExternalPlantApiController**

|Nombre	|Ruta	|Acción|	Handle|
|-----------------------|------------------|---------------|-----------------------------------------------------|
|Search	|/search?name={plantName}	|Busca información de una planta en API externa|	SearchExternalPlantQuery|
|GetDetails	|/details/{externalPlantId}|	Obtiene detalles desde API externa	|GetExternalPlantDetailsQuery|

### 4.2.2.3. Application Layer. 

La capa de aplicación del Bounded Context Plant Management coordina la interacción entre la capa de interfaz y la capa de dominio. Su responsabilidad principal es orquestar comandos, consultas y eventos, asegurando la correcta ejecución de flujos como la creación de perfiles de plantas, actualización de estados, configuración de condiciones ideales, archivado y eliminación.

No implementa reglas de negocio directamente, sino que delega al dominio, manteniendo una separación clara de responsabilidades y asegurando la integridad transaccional del sistema.

**Command Handlers**
**CreatePlantProfileCommandHandler**

|Propiedad|Valor|
|---------------|---------------------------------------------------------------------------------------|
|Nombre	|CreatePlantProfileCommandHandler|
|Categoría	|Command Handler|
|Propósito	|Crear un nuevo perfil de planta en el sistema|
|Comando	|CreatePlantProfileCommand|

**UpdatePlantProfileCommandHandler**

|Propiedad|	Valor|
|---------------|---------------------------------------------------------------------------------------|
|Nombre	|UpdatePlantProfileCommandHandler|
|Categoría	|Command Handler|
|Propósito	|Actualizar los datos generales del perfil de planta|
|Comando	|UpdatePlantProfileCommand|

**ArchivePlantProfileCommandHandler**

|Propiedad	|Valor|
|---------------|---------------------------------------------------------------------------------------|
|Nombre	|ArchivePlantProfileCommandHandler|
|Categoría	|Command Handler|
|Propósito	|Archivar un perfil de planta activo|
|Comando	|ArchivePlantProfileCommand|

**DeletePlantProfileCommandHandler**

|Propiedad|	Valor|
|---------------|---------------------------------------------------------------------------------------|
|Nombre|	DeletePlantProfileCommandHandler|
|Categoría	|Command Handler|
|Propósito	|Eliminar un perfil de planta (definitivamente o tras periodo de archivo)|
|Comando	|DeletePlantProfileCommand|

**UpdatePlantStatusCommandHandler**

|Propiedad	|Valor|
|---------------|---------------------------------------------------------------------------------------|
|Nombre	|UpdatePlantStatusCommandHandler|
|Categoría	|Command Handler|
|Propósito	|Actualizar el estado actual de una planta (ej. salud, humedad, crecimiento)|
|Comando	|UpdatePlantStatusCommand|

**ConfigurePlantConditionsCommandHandler**

|Propiedad	|Valor|
|---------------|---------------------------------------------------------------------------------------|
|Nombre	|ConfigurePlantConditionsCommandHandler|
|Categoría	|Command Handler|
|Propósito	|Configurar las condiciones ideales de una planta (riego, luz, temperatura, nutrientes)|
|Comando	|ConfigurePlantConditionsCommand|

**Query Handlers**
**GetPlantProfileByIdQueryHandler**

|Propiedad	|Valor|
|---------------|---------------------------------------------------------------------------------------|
|Nombre	|GetPlantProfileByIdQueryHandler|
|Categoría	|Query Handler|
|Propósito	|Obtener datos de un perfil de planta por Id|
|Query	|GetPlantProfileByIdQuery|

**GetPlantStatusQueryHandler**

|Propiedad	|Valor|
|---------------|---------------------------------------------------------------------------------------|
|Nombre	|GetPlantStatusQueryHandler|
|Categoría	|Query Handler|
|Propósito|	Obtener el estado actual de una planta|
|Query	|GetPlantStatusQuery|

**GetPlantHistoryQueryHandler**

|Propiedad	|Valor|
|---------------|---------------------------------------------------------------------------------------|
|Nombre|	GetPlantHistoryQueryHandler|
|Categoría	|Query Handler|
|Propósito	|Consultar el historial de cambios de estado de una planta|
|Query|	GetPlantHistoryQuery|

**GetPlantConditionsQueryHandler**

|Propiedad	|Valor|
|---------------|---------------------------------------------------------------------------------------|
|Nombre	|GetPlantConditionsQueryHandler|
|Categoría	|Query Handler|
|Propósito	|Obtener las condiciones ideales configuradas de una planta|
|Query	|GetPlantConditionsQuery|

**SearchExternalPlantQueryHandler**

|Propiedad	|Valor|
|---------------|---------------------------------------------------------------------------------------|
|Nombre	|SearchExternalPlantQueryHandler|
|Categoría	|Query Handler|
|Propósito	|Buscar información de una planta en la API externa|
|Query	|SearchExternalPlantQuery|

**GetExternalPlantDetailsQueryHandler**

|Propiedad	|Valor|
|---------------|---------------------------------------------------------------------------------------|
|Nombre	|GetExternalPlantDetailsQueryHandler|
|Categoría	|Query Handler|
|Propósito	|Obtener detalles de una planta desde API externa|
|Query	|GetExternalPlantDetailsQuery|

**Event Handlers**
**PlantProfileCreatedEventHandler**

|Propiedad	|Valor|
|---------------|---------------------------------------------------------------------------------------|
|Nombre	|PlantProfileCreatedEventHandler|
|Categoría	|Event Handler|
|Propósito	|Gestionar acciones tras la creación de un perfil de planta (ej. notificar al usuario, inicializar condiciones)|
|Evento	|PlantProfileCreatedEvent|

**PlantStatusUpdatedEventHandler**

|Propiedad	|Valor|
|---------------|---------------------------------------------------------------------------------------|
|Nombre	|PlantStatusUpdatedEventHandler|
|Categoría	|Event Handler|
|Propósito	|Gestionar acciones tras actualización de estado (ej. registrar historial, disparar alertas)|
|Evento	|PlantStatusUpdatedEvent|

**PlantConditionsConfiguredEventHandler**

|Propiedad	|Valor|
|---------------|---------------------------------------------------------------------------------------|
|Nombre	|PlantConditionsConfiguredEventHandler|
|Categoría|	Event Handler|
|Propósito	|Gestionar acciones tras la configuración de condiciones ideales (ej. vincular con sensores IoT)|
|Evento	|PlantConditionsConfiguredEvent|

**PlantProfileArchivedEventHandler**

|Propiedad	|Valor|
|---------------|---------------------------------------------------------------------------------------|
|Nombre|	PlantProfileArchivedEventHandler|
|Categoría	|Event Handler|
|Propósito	|Ejecutar acciones tras archivar un perfil (ej. programar eliminación en 30 días)|
|Evento	|PlantProfileArchivedEvent|

**PlantProfileDeletedEventHandler**

|Propiedad	|Valor|
|---------------|---------------------------------------------------------------------------------------|
|Nombre	|PlantProfileDeletedEventHandler|
|Categoría	|Event Handler|
|Propósito	|Gestionar acciones tras la eliminación de un perfil (ej. limpiar registros relacionados)|
|Evento	|PlantProfileDeletedEvent|

### 4.2.2.4. Infrastructure Layer. 
### 4.2.2.5. Bounded Context Software Architecture Component Level Diagrams. 
### 4.2.2.6. Bounded Context Software Architecture Code Level Diagrams. 
#### 4.2.2.6.1. Bounded Context Domain Layer Class Diagrams. 
#### 4.2.2.6.2. Bounded Context Database Design Diagram.

## 4.2.3. Bounded Context: Device Management IoT
### 4.2.3.1. Domain Layer. 
### 4.2.3.2. Interface Layer. 
### 4.2.3.3. Application Layer. 
### 4.2.3.4. Infrastructure Layer. 
### 4.2.3.5. Bounded Context Software Architecture Component Level Diagrams. 
### 4.2.3.6. Bounded Context Software Architecture Code Level Diagrams. 
#### 4.2.3.6.1. Bounded Context Domain Layer Class Diagrams. 
#### 4.2.3.6.2. Bounded Context Database Design Diagram.

## 4.2.4. Bounded Context: Data Telemetry
### 4.2.4.1. Domain Layer. 
### 4.2.4.2. Interface Layer. 
### 4.2.4.3. Application Layer. 
### 4.2.4.4. Infrastructure Layer. 
### 4.2.4.5. Bounded Context Software Architecture Component Level Diagrams. 
### 4.2.4.6. Bounded Context Software Architecture Code Level Diagrams. 
#### 4.2.4.6.1. Bounded Context Domain Layer Class Diagrams. 
#### 4.2.4.6.2. Bounded Context Database Design Diagram.

## 4.2.5. Bounded Context: Notification & Rules Engine
### 4.2.5.1. Domain Layer. 
### 4.2.5.2. Interface Layer. 
### 4.2.5.3. Application Layer. 
### 4.2.5.4. Infrastructure Layer. 
### 4.2.5.5. Bounded Context Software Architecture Component Level Diagrams. 
### 4.2.5.6. Bounded Context Software Architecture Code Level Diagrams. 
#### 4.2.5.6.1. Bounded Context Domain Layer Class Diagrams. 
#### 4.2.5.6.2. Bounded Context Database Design Diagram.

## 4.2.6. Bounded Context: Analysis&Report
### 4.2.6.1. Domain Layer. 
### 4.2.6.2. Interface Layer. 
### 4.2.6.3. Application Layer. 
### 4.2.6.4. Infrastructure Layer. 
### 4.2.6.5. Bounded Context Software Architecture Component Level Diagrams. 
### 4.2.6.6. Bounded Context Software Architecture Code Level Diagrams. 
#### 4.2.6.6.1. Bounded Context Domain Layer Class Diagrams. 
#### 4.2.6.6.2. Bounded Context Database Design Diagram.

## 4.2.7. Bounded Context: Community/Social
### 4.2.7.1. Domain Layer. 

#### Communities
_Tabla de communities_

| Propiedad     | Valor                                                                                                            |
|---------------|------------------------------------------------------------------------------------------------------------------|
| **Nombre**    | communities                                                                                                             |
| **Categoría** | Aggregate Root                                                                                                   |
| **Propósito** | Almacenar la configuración y metadatos de cada comunidad (nombre, descripción, visibilidad). |


_Tabla de atributos de communities_

| Nombre       | Tipo de dato | Visibilidad | Descripción                                          |
| ------------ | -----------: | ----------- | ---------------------------------------------------- |
| id           |         UUID | Private    | Identificador único de la comunidad.                 |
| name         | VARCHAR(150) | Public      | Nombre visible de la comunidad.                      |
| description  |         TEXT | Public      | Descripción corta de la comunidad.                   |
| is_public   |      BOOLEAN | Public      | Indica si la comunidad es pública o privada.         |                           |
| created_at  |    TIMESTAMP | Private    | Fecha de creación.                                   |
| updated_at  |    TIMESTAMP | Private    | Fecha de última actualización.                       |


_Tabla de métodos de communities_

| Nombre                                               | Tipo de retorno | Visibilidad | Descripción                                                  |
| ---------------------------------------------------- | --------------: | ----------- | ------------------------------------------------------------ |
| createCommunity(name, slug, description, is\_public) |       Community | Public      | Crea una nueva comunidad y asigna configuración por defecto. |
| archiveCommunity()                                   |         boolean | Private    | Marca la comunidad como inactiva/archivada.                  |


#### Community_posts

_Tabla de community_posts_

| Propiedad     | Valor                                                                                                             |
| ------------- | ----------------------------------------------------------------------------------------------------------------- |
| **Nombre**    | community_posts                                                                                                 |
| **Categoría** | Aggregate                                                                                 |
| **Propósito** | Representar las publicaciones del feed con contenido, media, estado. |

_Tabla de atributos de community_posts_

| Nombre        |       Tipo de dato | Visibilidad | Descripción                                        |
| ------------- | -----------------: | ----------- | -------------------------------------------------- |
| id            |               UUID | Private    | ID único del post.                                 |
| community_id |               UUID | Private    | FK a `communities`.                                |
| author_id    |               UUID | Public      | FK a `community_members` (autor).                  |
| title         |       VARCHAR(250) | Public      | Título de la publicación.                          |
| body          |               TEXT | Public      | Contenido principal (texto).                       |
| status        |        `Status` (enum) | Public      | Estado: `draft`, `published`, `hidden`, `deleted`. |
| visibility    |        VARCHAR(20) | Public      | Público, privado, solo miembros.                   |
| created\_at   |          TIMESTAMP | Private    | Fecha de creación.                                 |
| updated\_at   |          TIMESTAMP | Private    | Fecha de actualización.                            |
| deleted\_at   | TIMESTAMP NULLABLE | Private    | Fecha de eliminación.                |


_Tabla de métodos de community_posts_

| Nombre                                               | Tipo de retorno | Visibilidad | Descripción                                          |
| ---------------------------------------------------- | --------------: | ----------- | ---------------------------------------------------- |
| createPost(authorId, title, body, visibility) |            Post | Public      | Valida y crea el post; emite `PostCreated`.          |
| editPost(postId, changes)                            |            Post | Public      | Aplica cambios y actualiza `updated_at`.             |
| publish()                                            |         boolean | Public      | Cambia estado a `published` y emite evento.          |
| hide()                                         |         boolean | Private    | Oculta el post.                         |
| delete()                                    |         boolean | Public      | Elimina definitivamente. |     


#### Community_members

_Tabla de community_members_

|     Propiedad | Valor                                                                                                                                |
| ------------: | ------------------------------------------------------------------------------------------------------------------------------------ |
|    **Nombre** | **CommunityMember**                                                                                  |
| **Categoría** | Entity     |
| **Propósito** | Perfil público en la comunidad. Relaciona usuarios con posts y acciones. |


_Tabla de atributos de community_members_

| Nombre            | Tipo de dato | Visibilidad | Descripción                                |
| ----------------- | -----------: | ----------- | ------------------------------------------ |
| id                |         UUID | Private    | ID del miembro (user profile).             |
| user_id          |         UUID | Private    | FK al sistema de usuarios.     |
| role              |  VARCHAR(50) | Private    | Rol: `member`, `admin`.       |
| joined_at        |    TIMESTAMP | Private    | Fecha de ingreso.                          |
| bio               |         TEXT | Public      | Biografía pública.                         |


_Tabla de métodos de community_members_

| Nombre                          | Tipo de retorno | Visibilidad | Descripción                          |
| ------------------------------- | --------------: | ----------- | ------------------------------------ |
| getProfile(memberId)            | CommunityMember | Public      | Recupera perfil público.             |
| updateProfile(changes)          | CommunityMember | Public      | Actualiza campos permitidos.         |




#### Comment

_Tabla de comment_

|     Propiedad | Valor                                                                                                          |
| ------------: | -------------------------------------------------------------------------------------------------------------- |
|    **Nombre** | **Comment**                                                                                                    |
| **Categoría** | Entity                                                                                                         |
| **Propósito** | Comentarios asociados a un post; edición y eliminación; registra autor y timestamps. |


_Tabla de atributos de comment_

| Nombre              |  Tipo de dato | Visibilidad | Descripción                     |
| ------------------- | ------------: | ----------- | ------------------------------- |
| id                  |          UUID | Private    | ID del comentario.              |
| post_id            |          UUID | Private    | FK a `community_posts`.         |
| author_id          |          UUID | Public      | FK a `community_members`.       |
| body                |          TEXT | Public      | Texto del comentario.           |
| status              |   VARCHAR(20) | Public      | `visible`, `hidden`, `deleted`. |
| created_at         |     TIMESTAMP | Private    | Fecha de creación.              |
| updated_at         |     TIMESTAMP | Private    | Fecha de edición.               |


_Tabla de métodos de comment_

| Nombre                                            | Tipo de retorno | Visibilidad     | Descripción                                      |
| ------------------------------------------------- | --------------: | --------------- | ------------------------------------------------ |
| addComment(postId, authorId, body) |         Comment | Public          | Crea un comentario. |
| editComment(commentId, newBody)                   |         Comment | Public          | Edita el comentario (control de autor).          |
| deleteComment(commentId)                          |         boolean | Public | Elimina o marca como eliminado.                  |


### 4.2.7.2. Interface Layer.

#### Communities
_Tabla de communities_
| Propiedad     | Valor                                                                             |
| ------------- | --------------------------------------------------------------------------------- |
| **Nombre**    | `communities`                                                                     |
| **Categoría** | API / Resource                                                                    |
| **Propósito** | Exponer endpoints para crear, obtener, listar, actualizar y archivar comunidades. |
| **Ruta**      | `/api/communities`                                                                |

_Tabla de métodos de communities_

| Nombre           | Ruta                                          |                                   Acción | Handle                                                               |
| ---------------- | --------------------------------------------- | ---------------------------------------: | -------------------------------------------------------------------- |
| listCommunities  | `GET /api/communities`                        |    Obtener lista paginada de comunidades | `CommunitiesController.list()` → `ListCommunitiesQueryHandler`       |
| getCommunity     | `GET /api/communities/{communityId}`          | Obtener detalle público de una comunidad | `CommunitiesController.get()` → `GetCommunityQueryHandler`           |
| createCommunity  | `POST /api/communities`                       |                          Crear comunidad | `CommunitiesController.create()` → `CreateCommunityCommandHandler`   |
| updateCommunity  | `PUT /api/communities/{communityId}`          |           Actualizar datos/configuración | `CommunitiesController.update()` → `UpdateCommunityCommandHandler`   |
| archiveCommunity | `POST /api/communities/{communityId}/archive` |          Archivar / desactivar comunidad | `CommunitiesController.archive()` → `ArchiveCommunityCommandHandler` |


#### Community_posts

_Tabla de community_posts_
| Propiedad     | Valor                                                                    |
| ------------- | ------------------------------------------------------------------------ |
| **Nombre**    | `community_posts`                                                        |
| **Categoría** | API / Resource (Posts)                                                   |
| **Propósito** | Endpoints para CRUD de posts.            |
| **Ruta**      | `/api/communities/{communityId}/posts` |

_Tabla de métodos de community_posts_
| Nombre           | Ruta                                        |                                  Acción | Handle                                                       |
| ---------------- | ------------------------------------------- | --------------------------------------: | ------------------------------------------------------------ |
| listPosts (feed) | `GET /api/communities/{communityId}/posts`  |   Listar posts (paginado, filter, sort) | `PostsController.list()` → `ListFeedQueryHandler`            |
| getPost          | `GET /api/posts/{postId}`                   |                     Obtener post por id | `PostsController.get()` → `GetPostQueryHandler`              |
| createPost       | `POST /api/communities/{communityId}/posts` |            Crear post | `PostsController.create()` → `CreatePostCommandHandler`      |
| editPost         | `PUT /api/posts/{postId}`                   |                             Editar post | `PostsController.edit()` → `EditPostCommandHandler`          |
| publishPost      | `POST /api/posts/{postId}/publish`          |           Publicar post (cambia status) | `PostsController.publish()` → `PublishPostCommandHandler`    |
| hidePost         | `POST /api/posts/{postId}/hide`             |               Ocultar post (moderación) | `ModerationController.hidePost()` → `HidePostCommandHandler` |
| deletePost       | `DELETE /api/posts/{postId}`                |     Borrar post | `PostsController.delete()` → `DeletePostCommandHandler`      |

#### Community_members

_Tabla de community_members_

| Propiedad     | Valor                                                                          |
| ------------- | ------------------------------------------------------------------------------ |
| **Nombre**    | `community_members`                                                            |
| **Categoría** | API / Resource (Members)                                                       |
| **Propósito** | Endpoints para consultar y actualizar perfiles públicos, roles y preferencias. |
| **Ruta**      | `/api/communities/{communityId}/members`  y `/api/members`                     |


_Tabla de métodos de community_members_

| Nombre         | Ruta                                                             |                                 Acción | Handle                                                       |
| -------------- | ---------------------------------------------------------------- | -------------------------------------: | ------------------------------------------------------------ |
| listMembers    | `GET /api/communities/{communityId}/members`                     |       Listar miembros de una comunidad | `MembersController.list()` → `ListMembersQueryHandler`       |
| getProfile     | `GET /api/members/{memberId}`                                    |                 Obtener perfil público | `MembersController.get()` → `GetMemberProfileQueryHandler`   |
| updateProfile  | `PUT /api/members/{memberId}`                                    | Actualizar perfil | `MembersController.update()` → `UpdateProfileCommandHandler` |
| promoteMember  | `POST /api/communities/{communityId}/members/{memberId}/promote` |          Cambiar rol (admin/member) | `AdminController.promote()` → `ChangeRoleCommandHandler`     |
| leaveCommunity | `POST /api/communities/{communityId}/members/{memberId}/leave`   |                    Abandonar comunidad | `MembersController.leave()` → `LeaveCommunityCommandHandler` |


#### Comment

_Tabla de comment_

| Propiedad     | Valor                                                         |
| ------------- | ------------------------------------------------------------- |
| **Nombre**    | `comments`                                                    |
| **Categoría** | API / Resource (Comments)                                     |
| **Propósito** | Crear, editar, eliminar y listar comentarios de posts.        |
| **Ruta**      | `/api/posts/{postId}/comments`  y `/api/comments/{commentId}` |


_Tabla de métodos de comment_

| Nombre        | Ruta                                    |                               Acción | Handle                                                                 |
| ------------- | --------------------------------------- | -----------------------------------: | ---------------------------------------------------------------------- |
| listComments  | `GET /api/posts/{postId}/comments`      |        Listar comentarios de un post | `CommentsController.list()` → `ListCommentsQueryHandler`               |
| addComment    | `POST /api/posts/{postId}/comments`     |                    Añadir comentario | `CommentsController.add()` → `AddCommentCommandHandler`                |
| editComment   | `PUT /api/comments/{commentId}`         | Editar comentario | `CommentsController.edit()` → `EditCommentCommandHandler`              |
| deleteComment | `DELETE /api/comments/{commentId}`      |    Eliminar comentario | `CommentsController.delete()` → `DeleteCommentCommandHandler`          |


### 4.2.7.3. Application Layer. 

#### Communities

| Propiedad     | Valor                                                                                                                                                                                                                                                                                                          |
| ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Nombre**    | `communities`                                                                                                                                                                                                                                                                                                  |
| **Categoría** | Application / Command & Query Handlers                                                          |
| **Propósito** | Orquestar creación, actualización, listado y archivado de comunidades                                                                                                           |
| **Comando**   | `CreateCommunityCommand` → `CreateCommunityCommandHandler`  <br>`UpdateCommunityCommand` → `UpdateCommunityCommandHandler`  <br>`ArchiveCommunityCommand` → `ArchiveCommunityCommandHandler`  <br>`ListCommunitiesQuery` → `ListCommunitiesQueryHandler`  <br>`GetCommunityQuery` → `GetCommunityQueryHandler` |

#### Community_posts

| Propiedad     | Valor                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Nombre**    | `community_posts`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| **Categoría** | Application / Command, Query, Event Handlers                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| **Propósito** | Coordinar creación/edición/publicación/ocultamiento/eliminación de posts(`PostCreated`).                                                                                                                                                                                                                                                                                                                                                                                                      |
| **Comando**   | `CreatePostCommand` → `CreatePostCommandHandler`  <br>`EditPostCommand` → `EditPostCommandHandler`  <br>`PublishPostCommand` → `PublishPostCommandHandler`  <br>`DeletePostCommand` → `DeletePostCommandHandler`  <br>`HidePostCommand` → `HidePostCommandHandler`  <br>`ListFeedQuery` → `ListFeedQueryHandler`  <br>`GetPostQuery` → `GetPostQueryHandler`  <br>**Eventos**: `PostCreatedEvent` → `PostCreatedEventHandler` |

#### Community_members
| Propiedad     | Valor                                                                                                                                                                                                                          |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Nombre**    | `community_members`                                                                                                                                                                                                            |
| **Categoría** | Application / Command & Query Handlers                                                                                                                                                                                         |
| **Propósito** | Orquestar lectura y actualización de perfiles, cambios de rol   |
| **Comando**   | `GetMemberProfileQuery` → `GetMemberProfileQueryHandler`  <br>`UpdateProfileCommand` → `UpdateProfileCommandHandler`  <br>`ChangeRoleCommand` → `ChangeRoleCommandHandler`  <br>`ListMembersQuery` → `ListMembersQueryHandler` |

#### Comment
| Propiedad     | Valor                                                                                                                                                                                                                                                                                                                                                                                              |
| ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Nombre**    | `comment`                                                                                                                                                                                                                                                                                                                                                                                          |
| **Categoría** | Application / Command & Query Handlers                        |
| **Propósito** | Coordinar creación, edición, eliminación.                                |
| **Comando**   | `AddCommentCommand` → `AddCommentCommandHandler`  <br>`EditCommentCommand` → `EditCommentCommandHandler`  <br>`DeleteCommentCommand` → `DeleteCommentCommandHandler`  <br>`ReportCommentCommand` → `ReportCommentCommandHandler`  <br>`ListCommentsQuery` → `ListCommentsQueryHandler` |


### 4.2.7.4. Infrastructure Layer. 

#### CommunitiesRepository

| Propiedad     | Valor                                                                                                                                                                                                                                  |
| ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Nombre**    | `CommunitiesRepository` / Implementaciones                                                                                                                                                                                             |
| **Categoría** | Repository Interface + Implementations                                                                                                                                                                                                 |
| **Propósito** | Persistencia y consultas optimizadas para `communities` (CRUD, búsquedas)                                                                                                                          |
| **Interfaz**  | `ICommunityRepository` (métodos: `save(Community)`, `findById(id)`, `list(filter`, `archive(id)`) |


#### PostsRepository

| Propiedad     | Valor                                                                                                                                                                                                                                                                                                                                                                                                             |
| ------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Nombre**    | `PostsRepository` / Media & Event Adapters                                                                                                                                                                                                                                                                                                                                                                        |
| **Categoría** | Repository + Storage + Message Bus                                                                                                                                                                                                                                                                                                                                                                                |
| **Propósito** | Guardar posts, actualizar estados.                                                                  |
| **Interfaz**  | `IPostRepository` (`save(Post)`, `findById(id)`, `listByCommunity(communityId, filters)`, `updateStatus(postId, status)`, `delete(postId)`) |


#### MembersRepository

| Propiedad     | Valor                                                                                                                                                                                                                                                                         |
| ------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Nombre**    | `MembersRepository` |
| **Categoría** | Repository                                          |
| **Propósito** | Persistir perfiles públicos, roles y preferencias; integrar con sistema de usuarios central (auth).  |
| **Interfaz**  | `IMemberRepository` (`findByUserId(userId)`, `findById(id)`, `save(member)`, `listByCommunity(communityId)`)|


#### CommentsRepository

| Propiedad     | Valor                                                                                                                                                                                                               |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Nombre**    | `CommentsRepository`             |
| **Categoría** | Repository                           |
| **Propósito** | Guardar y consultar comentarios.   |
| **Interfaz**  | `ICommentRepository` (`save(Comment)`, `findById(id)`, `listByPost(postId)`, `delete(commentId)`) |


### 4.2.7.5. Bounded Context Software Architecture Component Level Diagrams. 
### 4.2.7.6. Bounded Context Software Architecture Code Level Diagrams. 
#### 4.2.7.6.1. Bounded Context Domain Layer Class Diagrams. 
#### 4.2.7.6.2. Bounded Context Database Design Diagram.
 
## 4.2.8. Bounded Context: Billing and Subscription
### 4.2.8.1. Domain Layer. 

#### Subscription

_Tabla de Subscription_

| Propiedad     | Valor                                                                                                                                                                               |
| ------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Nombre**    | Subscription      |
| **Categoría** | Aggregate Root       |
| **Propósito** | Representar la suscripción del cliente. |


_Tabla de atributos de Subscription_

| Nombre          | Tipo de dato              | Visibilidad | Descripción                                             |
| --------------- | ------------------------- | ----------- | ------------------------------------------------------- |
| id              | UUID                      | public      | Identificador único del agregado Subscription.          |
| customerId      | UUID                      | public      | Referencia al cliente/owner de la suscripción.          |
| planId          | UUID                      | public      | Identificador del plan suscrito.                        |
| status          | SubscriptionStatus (enum) | public      | Estado: PENDING, ACTIVE, SUSPENDED, CANCELLED, EXPIRED. |
| startDate       | DateTime                  | public      | Fecha de inicio de la suscripción.                      |
| endDate         | DateTime \| null          | public      | Fecha de fin (si aplica, p.ej. cancelación con fin).    |
| nextBillingDate | DateTime                  | public      | Próxima fecha prevista de facturación.                  |
| trialEndDate    | DateTime \| null          | public      | Fin del periodo de prueba si aplica.                    |


_Tabla de métodos de Subscription_

| Nombre                                                                                  | Tipo de retorno | Visibilidad | Descripción                                                                   |
| --------------------------------------------------------------------------------------- | --------------- | ----------- | ----------------------------------------------------------------------------- |
| activate()                                                                              | void            | public      | Activa la suscripción (aplica validaciones).                                  |
| cancel(effectiveDate: DateTime)                                                 | void            | public      | Cancela la suscripción; puede ser inmediata o al final del periodo.           |
| changePlan(newPlanId: UUID, changeDate: DateTime)                                       | void   | public      | Cambia de plan.   |
| isActive()                                                                              | boolean         | public      | Indica si el estado es ACTIVE.                                                |
| suspend(reason: string)                                                                 | void            | public      | Suspende temporalmente la suscripción.                                        |


#### CustomerBillingAccount

| Propiedad     | Valor                                                                                                                 |
| ------------- | --------------------------------------------------------------------------------------------------------------------- |
| **Nombre**    | CustomerBillingAccount                                                                                                |
| **Categoría** | Entity                                                                |
| **Propósito** | Mantener la información de facturación del cliente |

_Tabla de atributos de CustomerBillingAccount_

| Nombre                 | Tipo de dato           | Visibilidad | Descripción                               |
| ---------------------- | ---------------------- | ----------- | ----------------------------------------- |
| id                     | UUID                   | public      | Identificador del account de facturación. |
| customerId             | UUID                   | public      | Referencia al cliente en el sistema.      |
| balance                | float                  | public      | Saldo actual.             |
| createdAt              | DateTime               | public      | Fecha de creación.                        |
| updatedAt              | DateTime               | public      | Fecha de actualización.                   |


_Tabla de métodos de CustomerBillingAccount_

| Nombre                                              | Tipo de retorno | Visibilidad | Descripción                                                   |
| --------------------------------------------------- | --------------- | ----------- | ------------------------------------------------------------- |
| getBalance()                                        | Money           | public      | Retorna el balance actual.                                    |



#### BillingPeriod

_Tabla de BillingPeriod_

| Propiedad     | Valor                                                                                                 |
| ------------- | ----------------------------------------------------------------------------------------------------- |
| **Nombre**    | BillingPeriod                                                                                         |
| **Categoría** | Value Object                                                                                          |
| **Propósito** | Definir intervalos de facturación (desde-hasta), vencimientos. |


_Tabla de atributos de BillingPeriod_

| Nombre    | Tipo de dato        | Visibilidad | Descripción               |
| --------- | ------------------- | ----------- | ------------------------- |
| start     | DateTime            | public      | Fecha inicio del periodo. |
| end       | DateTime            | public      | Fecha fin del periodo.    |
| frequency | BillingCycle (enum) | public      | Frecuencia asociada.      |


_Tabla de métodos de BillingPeriod_

| Nombre                                                     | Tipo de retorno | Visibilidad | Descripción                                  |
| ---------------------------------------------------------- | --------------- | ----------- | -------------------------------------------- |
| contains(date: DateTime)                                   | boolean         | public      | Indica si la fecha está dentro del periodo.  |
| overlapsWith(other: BillingPeriod)                         | boolean         | public      | Indica si hay solapamiento con otro periodo. |
| days()                                                     | int             | public      | Número de días en el periodo.      |


#### Plan

_Tabla de plan_

| Propiedad     | Valor                                                                                                                                 |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| **Nombre**    | Plan                                                                                                                                  |
| **Categoría** | Entity / Value Object ligero                                                                                                          |
| **Propósito** | Definir características del producto suscribible. |


_Tabla de atributos de plan_

| Nombre          | Tipo de dato        | Visibilidad | Descripción                            |
| --------------- | ------------------- | ----------- | -------------------------------------- |
| id              | UUID                | public      | Identificador del plan.                |
| name            | string              | public      | Nombre comercial del plan.             |
| description     | string              | public      | Descripción corta.                     |
| price           | float               | public      | Precio base por periodo.               |
| features        | List<string>        | public      | Beneficios o límites incluidos.        |
| isActive        | boolean             | public      | Indica si el plan está disponible.     |


_Tabla de métodos de plan_

| Nombre                                          | Tipo de retorno | Visibilidad | Descripción                       |
| ----------------------------------------------- | --------------- | ----------- | --------------------------------- |
| activate()                                      | void            | public      | Activa el plan para contratación. |
| deactivate()                                    | void            | public      | Desactiva el plan.                |


### 4.2.8.2. Interface Layer.

#### Subscriptions

_Tabla de Subscriptions_

| Propiedad     | Valor                                                                                                                                       |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| **Nombre**    | Subscriptions                                                 |
| **Categoría** | Interface / Controller                                    |
| **Propósito** | Exponer endpoints para gestionar ciclo de vida de suscripciones del usuario (crear, cambiar plan, cancelar, activar, suspender, consultar). |
| **Ruta**      | `/api/v1/subscriptions`               |


_Tabla de métodos de Subscriptions_

| Nombre                           | Ruta                                                     | Acción                                                           | Handle                               |
| -------------------------------- | -------------------------------------------------------- | ---------------------------------------------------------------- | ------------------------------------ |
| Crear suscripción                | `POST /api/v1/subscriptions`                             | Registrar nueva suscripción para un cliente y plan seleccionado  | `CreateSubscriptionCommandHandler`   |
| Obtener suscripción              | `GET /api/v1/subscriptions/{subscriptionId}`             | Obtener detalle de una suscripción                               | `GetSubscriptionQueryHandler`        |
| Listar suscripciones por cliente | `GET /api/v1/customers/{customerId}/subscriptions`       | Listar todas las suscripciones de un cliente                     | `ListSubscriptionsQueryHandler`      |
| Cambiar plan                     | `PUT /api/v1/subscriptions/{subscriptionId}/change-plan` | Cambiar de plan                    | `ChangePlanCommandHandler`           |
| Cancelar suscripción             | `PUT /api/v1/subscriptions/{subscriptionId}/cancel`      | Solicitar cancelación | `CancelSubscriptionCommandHandler`   |
| Activar suscripción              | `POST /api/v1/subscriptions/{subscriptionId}/activate`   | Activación                                | `ActivateSubscriptionCommandHandler` |
| Suspender suscripción            | `POST /api/v1/subscriptions/{subscriptionId}/suspend`    | Suspender temporalmente la suscripción                           | `SuspendSubscriptionCommandHandler`  |
| Consultar estado (simple)        | `GET /api/v1/subscriptions/{subscriptionId}/status`      | Obtener booleano isActive / status                               | `GetSubscriptionStatusQueryHandler`  |

#### CustomerBillingAccount

_Tabla de CustomerBillingAccount_

| Propiedad     | Valor                                                                                                                               |
| ------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| **Nombre**    | CustomerBillingAccount               |
| **Categoría** | Interface / Controller                         |
| **Propósito** | Exponer operaciones para consultar y mantener la cuenta de facturación del cliente |
| **Ruta**      | `/api/v1/customers/{customerId}/billing-account`                             |


_Tabla de métodos de CustomerBillingAccount_

| Nombre                          | Ruta                                                                                            | Acción                                                                          | Handle                                       |
| ------------------------------- | ----------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- | -------------------------------------------- |
| Obtener account                 | `GET /api/v1/customers/{customerId}/billing-account`                                            | Recuperar datos de facturación del cliente | `GetCustomerBillingAccountQueryHandler`      |
| Obtener balance                 | `GET /api/v1/customers/{customerId}/billing-account/balance`                                    | Retornar balance actual                                            | `GetCustomerBalanceQueryHandler`             |

#### Plans

_Tabla de Plans_

| Propiedad     | Valor                                                                                                 |
| ------------- | ----------------------------------------------------------------------------------------------------- |
| **Nombre**    | Plans                                                                                    |
| **Categoría** | Interface / Controller                                                                    |
| **Propósito** | Exponer endpoints para consultar y administrar planes disponibles (CRUD básico + activar/desactivar). |
| **Ruta**      | `/api/v1/plans`                                                                                       |


_Tabla de métodos de Plans_
| Nombre          | Ruta                                     | Acción                                        | Handle                         |
| --------------- | ---------------------------------------- | --------------------------------------------- | ------------------------------ |
| Listar planes   | `GET /api/v1/plans`                      | Retornar lista de planes activos y filtrables | `ListPlansQueryHandler`        |
| Obtener plan    | `GET /api/v1/plans/{planId}`             | Retornar detalle del plan por id              | `GetPlanQueryHandler`          |
| Crear plan      | `POST /api/v1/plans`                     | Crear nuevo plan (admin)                      | `CreatePlanCommandHandler`     |
| Actualizar plan | `PUT /api/v1/plans/{planId}`             | Modificar atributos del plan (admin)          | `UpdatePlanCommandHandler`     |
| Activar plan    | `POST /api/v1/plans/{planId}/activate`   | Marcar plan como disponible                   | `ActivatePlanCommandHandler`   |
| Desactivar plan | `POST /api/v1/plans/{planId}/deactivate` | Quitar plan de contratación                   | `DeactivatePlanCommandHandler` |


### 4.2.8.3. Application Layer. 

#### PlanApplicationService
| Propiedad     | Valor                                                                                                                      |
| ------------- | -------------------------------------------------------------------------------------------------------------------------- |
| **Nombre**    | PlanApplicationService                 |
| **Categoría** | Application Service / Query & Command Handlers                     |
| **Propósito** | Coordinar casos de uso relacionados con planes: creación, actualización, activación/desactivación y consultas.             |
| **Comando**   | `CreatePlanCommand`, `UpdatePlanCommand`, `ActivatePlanCommand`, `DeactivatePlanCommand`, `ListPlansQuery`, `GetPlanQuery` |

#### CustomerBillingAccountApplicationService
| Propiedad     | Valor                                                                                                                                                                                         |
| ------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Nombre**    | CustomerBillingAccountApplicationService      |
| **Categoría** | Application Service  |
| **Propósito** | Orquestar casos de uso: consulta de cuenta, consulta de balance.                                                                           |
| **Comando**   | `GetCustomerBillingAccountQuery`, `GetCustomerBalanceQuery` |


#### SubscriptionApplicationService
| Propiedad     | Valor                                                                                                                                                                                        |
| ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Nombre**    | SubscriptionApplicationService                     |
| **Categoría** | Application Service / Command & Query Handlers              |
| **Propósito** | Coordinar flujo de operaciones sobre suscripciones: creación, cambio de plan (prorrateo), cancelación, activación, suspensión y consultas.                                                   |
| **Comando**   | `CreateSubscriptionCommand`, `ChangePlanCommand`, `CancelSubscriptionCommand`, `ActivateSubscriptionCommand`, `SuspendSubscriptionCommand`, `GetSubscriptionQuery`, `ListSubscriptionsQuery` |


#### SubscriptionEventHandlers
| Propiedad     | Valor                                                                                                                                                                           |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Nombre**    | SubscriptionEventHandlers        |
| **Categoría** | Event Handlers  |
| **Propósito** | Ejecutar acciones reactivas tras eventos de dominio relevantes (ej.: `SubscriptionCancelled` -> notificar al usuario, `SubscriptionActivated` -> iniciar ciclo de facturación). |
| **Comando**   | `HandleSubscriptionCancelledEvent`, `HandleSubscriptionActivatedEvent`                                                                                                          |


### 4.2.8.4. Infrastructure Layer. 

#### SubscriptionRepositoryImpl
| Propiedad     | Valor                                                                                                                                                                |
| ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Nombre**    | SubscriptionRepositoryImpl    |
| **Categoría** | Repository Implementation                |
| **Propósito** | Implementar `SubscriptionRepository` persistiendo agregados Subscription; operaciones: save, findById, findByCustomer |
| **Interfaz**  | `SubscriptionRepository` (Domain interface: save, findById, findActiveByCustomer)                                                                 |


#### CustomerBillingAccountRepositoryImpl

| Propiedad     | Valor                                                                                                                                                          |
| ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Nombre**    | CustomerBillingAccountRepositoryImpl   |
| **Categoría** | Repository Implementation          |
| **Propósito** | Implementación concreta para persistir/consultar CustomerBillingAccount.|
| **Interfaz**  | `CustomerBillingAccountRepository` (findByCustomerId, updateBalance)           |


#### PlanRepositoryImpl
| Propiedad     | Valor                                                                                                                                        |
| ------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| **Nombre**    | PlanRepositoryImpl                 |
| **Categoría** | Repository Implementation                                    |
| **Propósito** | Implementar `PlanRepository` persistiendo Plan en la BD  y exponiendo búsquedas por id, activo, filtros y páginas. |
| **Interfaz**  | `PlanRepository` (Domain interface: save, findById, findActive, list)       |


### 4.2.8.5. Bounded Context Software Architecture Component Level Diagrams. 
### 4.2.8.6. Bounded Context Software Architecture Code Level Diagrams. 
#### 4.2.8.6.1. Bounded Context Domain Layer Class Diagrams. 
#### 4.2.8.6.2. Bounded Context Database Design Diagram.
 
## 4.2.9. Bounded Context: Platform
### 4.2.9.1. Domain Layer. 
#### Subscription

_Tabla de Subscription_

_Tabla de atributos de Subscription_

_Tabla de métodos de Subscription_
### 4.2.9.2. Interface Layer. 

#### 

_Tabla de _



_Tabla de métodos de _

### 4.2.9.3. Application Layer. 

#### 

### 4.2.9.4. Infrastructure Layer. 
### 4.2.9.5. Bounded Context Software Architecture Component Level Diagrams. 
### 4.2.9.6. Bounded Context Software Architecture Code Level Diagrams. 
#### 4.2.9.6.1. Bounded Context Domain Layer Class Diagrams. 
#### 4.2.9.6.2. Bounded Context Database Design Diagram.

