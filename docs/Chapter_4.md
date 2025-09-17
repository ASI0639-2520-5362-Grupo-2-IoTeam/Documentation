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

#### 4.1.2. Context Mapping.

### 4.1.3. Software Architecture.

#### 4.1.3.1. Software Architecture System Landscape Diagram.

#### 4.1.3.2. Software Architecture Context Level Diagrams.

#### 4.1.3.2. Software Architecture Container Level Diagrams.

#### 4.1.3.3. Software Architecture Deployment Diagrams.

## 4.2. Tactical-Level Domain-Driven Design

### 4.2.X. Bounded Context: <Bounded Context Name>

#### 4.2.X.1. Domain Layer.

#### 4.2.X.2. Interface Layer.

#### 4.2.X.3. Application Layer.

#### 4.2.X.4. Infrastructure Layer.

#### 4.2.X.5. Bounded Context Software Architecture Component Level Diagrams.

#### 4.2.X.6. Bounded Context Software Architecture Code Level Diagrams.

##### 4.2.X.6.1. Bounded Context Domain Layer Class Diagrams.

##### 4.2.X.6.2. Bounded Context Database Design Diagram.
