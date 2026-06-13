# Parte 1: Investigación Teórica y Análisis de Casos

## 1. El Límite de las Rotaciones Simples y Desbalanceo en "Zig-Zag"

### El Problema Cruzado

Los árboles AVL pertenecen a la familia de los árboles binarios de búsqueda balanceados y tienen como principal objetivo mantener una altura controlada para garantizar operaciones eficientes de búsqueda, inserción y eliminación. Para lograrlo, cada nodo conserva un equilibrio entre sus subárboles, evitando que uno crezca significativamente más que el otro.

Durante el proceso de inserción pueden aparecer configuraciones de desequilibrio que no pueden corregirse mediante una sola rotación. Una de estas configuraciones es el denominado caso "Zig-Zag", el cual surge cuando el crecimiento del árbol ocurre en direcciones opuestas dentro de la misma rama. En este escenario, el nodo responsable del desequilibrio no se encuentra alineado con la dirección principal del crecimiento, lo que impide que una rotación simple reorganice correctamente la estructura.

Las rotaciones simples fueron diseñadas para resolver casos lineales de crecimiento. Cuando la inserción genera una trayectoria cruzada, la aplicación de una única rotación únicamente desplaza el problema sin restaurar completamente las condiciones de balance exigidas por los árboles AVL.

Por esta razón se recurre a las rotaciones dobles, consideradas operaciones compuestas que permiten corregir simultáneamente la posición de varios nodos involucrados en el desequilibrio. Estas rotaciones reorganizan la estructura interna del árbol para que el nodo ubicado en la posición intermedia pase a desempeñar el papel central dentro del subárbol afectado.

Formalmente, una Rotación Izquierda-Derecha (RID) debe ejecutarse cuando el nodo crítico posee un Factor de Equilibrio de -2 y su hijo izquierdo presenta un Factor de Equilibrio de +1. Esta combinación indica que el exceso de altura se originó en una trayectoria izquierda seguida por una desviación hacia la derecha.

El propósito de esta operación es restaurar la simetría estructural del árbol, minimizar su altura y garantizar que las futuras operaciones continúen ejecutándose con complejidad logarítmica.

### Principio DRY (Don't Repeat Yourself)

El principio DRY es una práctica de diseño cuyo objetivo consiste en eliminar la repetición innecesaria de código dentro de una aplicación. Bajo esta filosofía, cada funcionalidad debe implementarse una sola vez y reutilizarse cuando sea necesario.

En el contexto de los árboles AVL, las rotaciones dobles pueden construirse mediante la combinación de rotaciones simples previamente implementadas. Este enfoque evita desarrollar nuevamente la lógica de manipulación de referencias y relaciones entre nodos.

La reutilización de componentes proporciona ventajas importantes. Una de ellas es la reducción del riesgo de errores, ya que las funciones utilizadas han sido probadas previamente. También simplifica el mantenimiento del software porque cualquier mejora realizada sobre una rotación simple beneficia automáticamente a las operaciones más complejas que dependen de ella.

Otro aspecto relevante es la consistencia. Cuando todas las operaciones de balanceo se construyen sobre una misma base lógica, el comportamiento del sistema resulta más predecible y fácil de validar. Esto contribuye a mejorar la calidad general del código y facilita el trabajo colaborativo entre desarrolladores.

Por consiguiente, aplicar el principio DRY en la implementación de estructuras AVL no solo representa una buena práctica de programación, sino también una estrategia efectiva para construir sistemas más robustos, mantenibles y escalables.

---

## 2. Fundamentos de Arquitectura Web y Protocolo HTTP

### El Modelo Cliente-Servidor

La arquitectura cliente-servidor constituye uno de los modelos más utilizados en el desarrollo de aplicaciones distribuidas. Su funcionamiento se basa en la separación de responsabilidades entre quienes solicitan servicios y quienes los proporcionan.

El cliente actúa como consumidor de recursos y es responsable de iniciar la comunicación. Generalmente se trata de un navegador web, una aplicación móvil o cualquier software capaz de enviar solicitudes a través de una red. El servidor, por su parte, recibe dichas solicitudes, procesa la información requerida y genera una respuesta adecuada.

La interacción entre ambos componentes se realiza mediante protocolos de comunicación estandarizados, siendo HTTP uno de los más importantes dentro del entorno web. Gracias a este protocolo es posible intercambiar información entre dispositivos heterogéneos independientemente de su sistema operativo o lenguaje de programación.

Cada comunicación comienza con una petición enviada por el cliente. Esta petición contiene información relacionada con la operación solicitada, así como los datos necesarios para que el servidor pueda procesarla. Una vez recibida, el servidor ejecuta la lógica correspondiente y construye una respuesta que posteriormente es devuelta al cliente.

La respuesta suele incluir un código de estado que indica el resultado de la operación, junto con datos estructurados en formatos como JSON. Este mecanismo permite establecer una comunicación clara, organizada y fácilmente interpretable por distintos sistemas.

La popularidad de este modelo se debe a su capacidad para distribuir responsabilidades, mejorar el rendimiento de las aplicaciones y facilitar la integración entre múltiples plataformas tecnológicas.

### Semántica de Operaciones

Dentro del protocolo HTTP, cada método representa una intención específica respecto al recurso solicitado. Esta clasificación permite que clientes y servidores interpreten correctamente la naturaleza de cada operación.

El método GET se encuentra orientado a la obtención de información existente. Su propósito principal es consultar recursos sin alterar su contenido ni modificar el estado interno del sistema. Debido a esta característica, se considera una operación segura y apropiada para procesos de lectura.

Por otro lado, el método POST está diseñado para enviar información al servidor con el objetivo de generar cambios dentro de la aplicación. Dichos cambios pueden incluir la creación de nuevos registros, la ejecución de procesos internos o la modificación de estructuras de datos ya existentes.

Desde la perspectiva de una API que expone estructuras de datos, GET es el mecanismo adecuado para visualizar el estado actual de dichas estructuras, mientras que POST resulta apropiado para incorporar nuevos elementos o desencadenar operaciones que alteren su configuración interna.

La correcta selección del método HTTP permite mantener una arquitectura coherente, facilita la comprensión de las interfaces de programación y contribuye al cumplimiento de los estándares utilizados en el desarrollo de servicios web modernos.
