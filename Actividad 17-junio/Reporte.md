

## Carné

202503403


17 de junio de 2026

---

# Parte 1: Fundamentación Teórica y Análisis Crítico

## 1. El Tránsito hacia los Sistemas Distribuidos y Multi-Capa

### La Limitación del Monolito Local

En una arquitectura monolítica local, la interfaz de usuario, la lógica de negocio y el almacenamiento de datos se ejecutan en una misma máquina física. Este enfoque resulta funcional para aplicaciones pequeñas, pero presenta limitaciones importantes cuando aumenta la cantidad de usuarios o la complejidad del sistema.

La escalabilidad se ve afectada debido a que todos los recursos computacionales son compartidos por los diferentes componentes. Además, la sincronización de datos entre múltiples usuarios puede volverse complicada, ya que toda la información depende de un único punto de ejecución. Si la máquina falla, el sistema completo deja de estar disponible.

### Distinción Crítica (Layers vs. Tiers)

Las capas (Layers) representan una división lógica dentro del software. Cada capa agrupa funcionalidades relacionadas y define responsabilidades específicas dentro del código.

Los niveles (Tiers) representan una separación física de la infraestructura. Cada nivel puede ejecutarse en servidores independientes y comunicarse mediante una red.

En resumen, las capas organizan el software desde el punto de vista lógico, mientras que los niveles organizan el despliegue físico de los componentes.

### Responsabilidades en la Arquitectura de 3 Niveles

#### Nivel 1: Capa de Presentación (Presentation Tier)

Su función principal es interactuar con el usuario. Se encarga de mostrar información, capturar datos y enviar solicitudes al servidor.

Tecnologías comunes:

* HTML
* CSS
* JavaScript
* Razor Views
* Navegadores web

#### Nivel 2: Capa de Aplicación o Negocio (Application Tier)

Contiene las reglas de negocio y coordina el procesamiento de la información. Actúa como intermediario entre la presentación y los datos.

Tecnologías comunes:

* ASP.NET Core
* C#
* APIs REST
* Servicios de negocio

#### Nivel 3: Capa de Datos (Data Tier)

Se encarga del almacenamiento, recuperación y administración de la información persistente.

Tecnologías comunes:

* SQL Server
* MySQL
* PostgreSQL
* Oracle Database

### Seguridad Perimetral

Exponer directamente una base de datos a Internet constituye una práctica insegura debido a que incrementa la superficie de ataque del sistema. Un atacante podría intentar acceder a la información mediante ataques de fuerza bruta, explotación de vulnerabilidades o robo de credenciales.

La práctica recomendada consiste en mantener la base de datos dentro de una red privada y permitir el acceso únicamente a través de la capa de aplicación. De esta forma se implementan mecanismos de autenticación, autorización y filtrado de solicitudes antes de llegar a los datos.

---

## 2. Desacoplamiento Lógico con el Patrón MVC

### La Crisis del Código Espagueti

Cuando la lógica de negocio, las consultas SQL y la presentación visual se encuentran mezcladas en un mismo archivo, el mantenimiento del sistema se vuelve complejo. Los cambios realizados en una sección pueden provocar errores inesperados en otras partes del código.

Esta situación dificulta la realización de pruebas unitarias, aumenta el acoplamiento entre componentes y reduce la capacidad de reutilizar código.

### Separación de Preocupaciones (SoC)

#### Modelo (Model)

El Modelo representa los datos y las reglas de negocio de la aplicación. Su responsabilidad principal es administrar la información y garantizar la consistencia de los datos.

El Modelo no debe conocer la forma en que la información será presentada al usuario, ya que esto rompería el principio de separación de responsabilidades.

#### Vista (View)

La Vista es la encargada de mostrar la información al usuario final. Se considera una entidad pasiva porque recibe los datos ya procesados y únicamente los presenta.

La Vista no debe contener lógica de negocio, consultas SQL ni cálculos complejos.

#### Controlador (Controller)

El Controlador actúa como intermediario entre la Vista y el Modelo. Recibe las solicitudes del usuario, coordina el procesamiento necesario y determina cuál será la respuesta que se enviará al cliente.

Por esta razón suele describirse como el director de orquesta del patrón MVC.

### Métricas de Ingeniería de Software

El patrón MVC promueve una alta cohesión debido a que cada componente posee responsabilidades claramente definidas.

Asimismo, favorece un bajo acoplamiento porque los cambios realizados en un componente afectan mínimamente a los demás.

Estas características mejoran la mantenibilidad, la escalabilidad, la reutilización de código y la facilidad para realizar pruebas unitarias.

---

# Parte 2: Modelado del Ciclo de Vida y Enrutamiento Semántico

## 1. Mapeo Analítico de URLs

Tomando como base la plantilla de enrutamiento:

```text
{controller=Home}/{action=Index}/{id?}
```

| URL Entrante del Cliente                                     | Clase Controladora Buscada por el Framework | Método (Acción) Ejecutado | Parámetro id Inyectado |
| ------------------------------------------------------------ | ------------------------------------------- | ------------------------- | ---------------------- |
| https://ingenieria.usac.edu.gt/ControlAcademico/Login        | ControlAcademicoController                  | Login                     | Ninguno                |
| https://ingenieria.usac.edu.gt/Estudiante/Historial/20260123 | EstudianteController                        | Historial                 | 20260123               |
| https://ingenieria.usac.edu.gt/Asignacion/Detalle/10         | AsignacionController                        | Detalle                   | 10                     |
| https://ingenieria.usac.edu.gt/Home                          | HomeController                              | Index                     | Ninguno / Opcional     |

---

## 2. Diagramación del Flujo Interactivo

### Flujo de una petición HTTP en MVC

1. El usuario realiza una acción en el navegador, como presionar un botón o acceder a una dirección URL.

2. El servidor ASP.NET Core recibe la solicitud HTTP y el sistema de enrutamiento identifica el controlador y la acción correspondientes.

3. El Controlador procesa la solicitud y solicita al Modelo los datos o servicios necesarios.

4. El Modelo ejecuta las reglas de negocio y obtiene la información requerida.

5. El Controlador envía los datos a la Vista, la cual genera dinámicamente el contenido HTML que finalmente es devuelto al navegador para su visualización.

---

# Parte 4: Auditoría y Control de Calidad

## Prueba de Cohesión (GET)

La acción Listar mantiene una alta cohesión porque su única responsabilidad consiste en obtener los datos y enviarlos a la Vista correspondiente. No realiza cálculos complejos ni incorpora sentencias SQL directamente dentro del controlador.

## Evaluación de Antipatrones

El controlador implementado sigue la filosofía de Skinny Controllers, ya que los métodos son cortos, claros y poseen responsabilidades específicas. Ningún método excede significativamente las veinte líneas de código, por lo que no se identifica la presencia del antipatrón conocido como Fat Controller.

---

# Parte 5: Referencias Bibliográficas

Facultad de Ingeniería, USAC. (2026). Sesión 11: Modelado Base y Arquitecturas de Despliegue. Evolución de Sistemas Distribuidos, Fundamentos del Modelo Cliente-Servidor y Diseño Físico Multi-Capas (N-Tier). Laboratorio del curso Introducción a la Programación y Computación 2. Guatemala.

Facultad de Ingeniería, USAC. (2026). Sesión 12: Arquitectura y Componentes del Patrón MVC. Desacoplamiento Lógico de Software, Ciclo de Vida de las Peticiones y Enrutamiento en Aplicaciones Interactivas Modernas. Laboratorio del curso Introducción a la Programación y Computación 2. Guatemala.
