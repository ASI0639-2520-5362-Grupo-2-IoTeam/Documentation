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
### 4.2.1.3. Application Layer. 
### 4.2.1.4. Infrastructure Layer. 
### 4.2.1.5. Bounded Context Software Architecture ### Component Level Diagrams. 
### 4.2.1.6. Bounded Context Software Architecture Code Level Diagrams. 
### 4.2.1.6.1. Bounded Context Domain Layer Class ### Diagrams. 
### 4.2.1.6.2. Bounded Context Database Design Diagram.

## 4.2.2. Bounded Context: Plant Management
### 4.2.2.1. Domain Layer. 
### 4.2.2.2. Interface Layer. 
### 4.2.2.3. Application Layer. 
### 4.2.2.4. Infrastructure Layer. 
### 4.2.2.5. Bounded Context Software Architecture Component Level Diagrams. 
### 4.2.2.6. Bounded Context Software Architecture Code Level Diagrams. 
### 4.2.2.6.1. Bounded Context Domain Layer Class Diagrams. 
### 4.2.2.6.2. Bounded Context Database Design Diagram.

## 4.2.3. Bounded Context: Device Management IoT
### 4.2.3.1. Domain Layer. 
### 4.2.3.2. Interface Layer. 
### 4.2.3.3. Application Layer. 
### 4.2.3.4. Infrastructure Layer. 
### 4.2.3.5. Bounded Context Software Architecture Component Level Diagrams. 
### 4.2.3.6. Bounded Context Software Architecture Code Level Diagrams. 
### 4.2.3.6.1. Bounded Context Domain Layer Class Diagrams. 
### 4.2.3.6.2. Bounded Context Database Design Diagram.

## 4.2.4. Bounded Context: Data Telemetry
### 4.2.4.1. Domain Layer. 
### 4.2.4.2. Interface Layer. 
### 4.2.4.3. Application Layer. 
### 4.2.4.4. Infrastructure Layer. 
### 4.2.4.5. Bounded Context Software Architecture Component Level Diagrams. 
### 4.2.4.6. Bounded Context Software Architecture Code Level Diagrams. 
### 4.2.4.6.1. Bounded Context Domain Layer Class Diagrams. 
### 4.2.4.6.2. Bounded Context Database Design Diagram.

## 4.2.5. Bounded Context: Notification & Rules Engine
### 4.2.5.1. Domain Layer. 
### 4.2.5.2. Interface Layer. 
### 4.2.5.3. Application Layer. 
### 4.2.5.4. Infrastructure Layer. 
### 4.2.5.5. Bounded Context Software Architecture Component Level Diagrams. 
### 4.2.5.6. Bounded Context Software Architecture Code Level Diagrams. 
### 4.2.5.6.1. Bounded Context Domain Layer Class Diagrams. 
### 4.2.5.6.2. Bounded Context Database Design Diagram.

## 4.2.6. Bounded Context: Analysis&Report
### 4.2.6.1. Domain Layer. 
### 4.2.6.2. Interface Layer. 
### 4.2.6.3. Application Layer. 
### 4.2.6.4. Infrastructure Layer. 
### 4.2.6.5. Bounded Context Software Architecture Component Level Diagrams. 
### 4.2.6.6. Bounded Context Software Architecture Code Level Diagrams. 
### 4.2.6.6.1. Bounded Context Domain Layer Class Diagrams. 
### 4.2.6.6.2. Bounded Context Database Design Diagram.

## 4.2.7. Bounded Context: Community/Social
### 4.2.7.1. Domain Layer. 
### 4.2.7.2. Interface Layer. 
### 4.2.7.3. Application Layer. 
### 4.2.7.4. Infrastructure Layer. 
### 4.2.7.5. Bounded Context Software Architecture Component Level Diagrams. 
### 4.2.7.6. Bounded Context Software Architecture Code Level Diagrams. 
### 4.2.7.6.1. Bounded Context Domain Layer Class Diagrams. 
### 4.2.7.6.2. Bounded Context Database Design Diagram.
 
## 4.2.8. Bounded Context: Billing and Subscription
### 4.2.8.1. Domain Layer. 
### 4.2.8.2. Interface Layer. 
### 4.2.8.3. Application Layer. 
### 4.2.8.4. Infrastructure Layer. 
### 4.2.8.5. Bounded Context Software Architecture Component Level Diagrams. 
### 4.2.8.6. Bounded Context Software Architecture Code Level Diagrams. 
### 4.2.8.6.1. Bounded Context Domain Layer Class Diagrams. 
### 4.2.8.6.2. Bounded Context Database Design Diagram.
 
## 4.2.9. Bounded Context: Platform
### 4.2.9.1. Domain Layer. 
### 4.2.9.2. Interface Layer. 
### 4.2.9.3. Application Layer. 
### 4.2.9.4. Infrastructure Layer. 
### 4.2.9.5. Bounded Context Software Architecture Component Level Diagrams. 
### 4.2.9.6. Bounded Context Software Architecture Code Level Diagrams. 
### 4.2.9.6.1. Bounded Context Domain Layer Class Diagrams. 
### 4.2.9.6.2. Bounded Context Database Design Diagram.

