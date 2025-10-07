# Capítulo V: Solution UI/UX Design

## 5.1. Style Guidelines.

Esta sección presenta los estilos establecidos, con el fin de garantizar consistencia, claridad y una experiencia de usuario coherente en todas las plataformas y componentes desarrollados.

### 5.1.1. General Style Guidelines.

**Branding**
El branding de PlantCare está diseñado para transmitir bienestar, conexión con la naturaleza y compromiso con el cuidado responsable de las plantas. La identidad visual busca reflejar un enfoque accesible, amigable y moderno, orientado a personas que desean mejorar el mantenimiento de sus plantas. Se utilizan elementos gráficos que evocan crecimiento, frescura y equilibrio, creando una imagen visual clara, cercana y fácil de reconocer para usuarios interesados en el autocuidado verde y la sostenibilidad.

**Typography**
La tipografía seleccionada es Raleway, una fuente moderna, estilizada y de alta legibilidad, que aporta un aspecto limpio y profesional a la interfaz. Se utilizará Raleway tanto para encabezados como para el cuerpo de texto, aprovechando su versatilidad en diferentes pesos tipográficos para marcar jerarquías visuales claras. Esta elección equilibra seriedad y cercanía, manteniendo una apariencia accesible y coherente con el enfoque natural y amigable de la aplicación PlantCare.

[![raleway.png](https://i.postimg.cc/GhX13nJC/raleway.png)](https://postimg.cc/1fVdMTjC)

**Colors**
La paleta de colores de PlantCare está compuesta por tonos verdes y cremas, cuidadosamente seleccionados para reflejar la esencia de la naturaleza y promover una experiencia visual tranquila y confiable. Los tonos verdes comunican frescura, crecimiento y sostenibilidad, valores clave en el cuidado de plantas. Por su parte, los tonos crema aportan calidez y naturalidad, generando una conexión visual con la tierra y el entorno orgánico. Estos colores se aplicarán estratégicamente en la interfaz para garantizar una experiencia armoniosa, accesible y agradable en todo tipo de dispositivos, especialmente móviles.

[![Plant-Care.png](https://i.postimg.cc/2ymfyzKd/Plant-Care.png)](https://postimg.cc/WF9yfPjt)

**Spacing**
Se utilizó un espaciado apropiado en toda la interfaz para evitar la saturación de elementos, facilitando así una navegación clara y confortable. Los márgenes y las separaciones entre los distintos componentes se planificaron con detalle para lograr un diseño armónico y bien estructurado.

**Tono de Comunicación y Lenguaje Aplicado:**
El tono de comunicación de PlantCare será cercano, motivador y accesible, con el objetivo de acompañar al usuario en el cuidado de sus plantas de forma clara y positiva. El lenguaje aplicado se define como divertido, casual, respetuoso y entusiasta.
Este enfoque busca generar una experiencia amigable, que inspire confianza y fomente una conexión genuina con la naturaleza a través del uso cotidiano de la aplicación.

### 5.1.2. Web, Mobile and IoT Style Guidelines.

El diseño web, mobile e IoT de PlantCare seguirá principios de accesibilidad, usabilidad y consistencia visual, asegurando que la experiencia del usuario sea clara y fluida en distintos dispositivos.

**Colores**  
Se utilizará la misma paleta de colores definida para la identidad de PlantCare, garantizando coherencia.

| Nombre       | Código HEX | Muestra                                                                                   |
| ------------ | ---------- | ----------------------------------------------------------------------------------------- |
| Primary     | #8AC73D    | ![#8AC73D](https://img.shields.io/badge/-8AC73D-8AC73D?style=flat-square&logoColor=white) |
| Secondary   | #85B88F    | ![#85B88F](https://img.shields.io/badge/-85B88F-85B88F?style=flat-square&logoColor=white) |
| Accent       | #03383C    | ![#03383C](https://img.shields.io/badge/-03383C-03383C?style=flat-square&logoColor=white) |
| Background  | #F7F7ED    | ![#F7F7ED](https://img.shields.io/badge/-F7F7ED-F7F7ED?style=flat-square&logoColor=black) |
| Text | #002933    | ![#002933](https://img.shields.io/badge/-002933-002933?style=flat-square&logoColor=white) |

#### **Tipografía**

- Encabezados: **Raleway** (Google Fonts).
- Cuerpo de texto: **Raleway** (Google Fonts).
- Jerarquía visual clara mediante tamaños escalonados (H1-H6).

#### **Componentes UI**

- **Sidebar** en la parte izquierda con enlaces principales.
- **Cards** para mostrar información de plantas.
- **Gráficos** para análisis.

#### **Interacciones**

- **Animaciones ligeras** para transiciones de secciones.
- **Diseño responsive** adaptando las vistas a pantallas pequeñas.

## 5.2. Information Architecture.

La arquitectura de la información es un elemento clave en el diseño y la facilidad de uso de un sistema digital. Cuando se implementa adecuadamente, facilita que los usuarios localicen, comprendan y utilicen el contenido de forma clara y eficaz.

### 5.2.1. Organization Systems.

Los sistemas de organización en PlantCare estructuran la información y funcionalidades para que la navegación sea intuitiva, eficiente y centrada en el usuario. Se aplican los siguientes enfoques:

- **Jerárquica (Visual Hierarchy):** Se destacan primero los elementos clave como métricas generales (total de plantas, alertas activas, humedad promedio) y un llamado a la acción claro para la siguiente planta que necesita riego. Este orden visual prioriza las tareas más importantes y urgentes para el usuario.

- **Secuencial (Step-by-step):** Aplicado en flujos como agregar una nueva planta, donde el usuario sigue un proceso guiado para ingresar datos como nombre, tipo, frecuencia de riego y sensor vinculado, de forma progresiva y ordenada.

- **Por Tópicos:** Visible en secciones como Settings, donde las opciones están agrupadas por funciones (perfil, suscripción, dispositivos). Este tipo de organización también se refleja en History, donde las acciones se ordenan cronológicamente.

- **Según Audiencia:** Funciones como la gestión de sensores o los planes de suscripción premium están pensadas para usuarios más avanzados o con múltiples dispositivos, adaptando así la experiencia según el perfil y nivel de compromiso del usuario.

[![image.png](https://i.postimg.cc/wB0jZx9R/image.png)](https://postimg.cc/hJQn7BzK)

### 5.2.2. Labeling System.

Se han implementado etiquetas **claras, concisas y accesibles** para representar funciones específicas. Estas etiquetas permiten a los usuarios identificar rápidamente cada sección o acción, sin necesidad de interpretación adicional ni conocimientos técnicos.

Las principales etiquetas utilizadas son:

- **Dashboard**
- **Plants**
- **Add plant**
- **History**
- **Analytics**
- **Community**
- **Configuration**
- **Edit/Delete plant**

Cada etiqueta está acompañada por íconos representativos que refuerzan visualmente su propósito, facilitando la navegación especialmente en interfaces móviles. El enfoque es directo y amigable, asegurando que tanto usuarios principiantes como avanzados puedan comprender rápidamente las funcionalidades disponibles.

### 5.2.3. SEO Tags and Meta Tags

Para optimizar la visibilidad en motores de búsqueda, se proponen las siguientes etiquetas:

- **Title:** PlantCare – Cuidado inteligente de tus plantas
- **Meta Tags Description:** Plataforma digital para el monitoreo y cuidado automatizado de plantas mediante sensores, alertas y recomendaciones personalizadas.
- **Keywords:** plantas, jardinería, sensores de humedad, riego inteligente, cuidado de plantas, app de plantas, PlantCare
- **Author:** PlantCare

### 5.2.4. Searching Systems.

Los sistemas de búsqueda permiten a los usuarios localizar información específica de manera rápida y eficiente dentro de la aplicación, optimizando el acceso al contenido y mejorando la experiencia de uso.

- **Filtros personalizados** para el historial y planta.
- **Resultados presentados con etiquetas visuales**, íconos e información clave como el nombre de la planta, humedad actual, último riego y estado general.

Estos sistemas hacen que la gestión y monitoreo de las plantas sea más ágil, especialmente útil para usuarios con múltiples registros o sensores activos.

### 5.2.5. Navigation Systems.

## 5.3. Landing Page UI Design.

### 5.3.1. Landing Page Wireframe.

### 5.3.2. Landing Page Mock-up.

## 5.4. Applications UX/UI Design.

### 5.4.1. Applications Wireframes.

### 5.4.2. Applications Wireflow Diagrams.

### 5.4.2. Applications Mock-ups.

### 5.4.3. Applications User Flow Diagrams.

## 5.5. Applications Prototyping.