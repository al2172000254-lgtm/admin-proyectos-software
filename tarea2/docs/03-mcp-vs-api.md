# 3. MCP frente a una API

Para comprender el propósito del *Model Context Protocol* (MCP), primero es necesario entender qué es una API y cómo se relaciona con este protocolo. Aunque ambos permiten la comunicación entre componentes de software, cumplen funciones diferentes y pueden utilizarse conjuntamente.

## ¿Qué es una API?

Una API (*Application Programming Interface* o interfaz de programación de aplicaciones) es un conjunto de reglas y mecanismos que permite que un programa solicite datos o servicios a otro componente de software.

La API define cómo realizar las solicitudes, qué parámetros se necesitan y qué respuestas pueden recibirse. Por ejemplo, una API meteorológica puede ofrecer una operación para consultar el clima de una ciudad. El programa que la utiliza debe conocer la interfaz correspondiente y cumplir con sus requisitos.

La forma de utilizar una API depende de su diseño. Algunas utilizan HTTP y formatos como JSON; otras emplean tecnologías diferentes. Por tanto, una API no es necesariamente un servicio web ni está limitada a un único formato de comunicación.

## ¿Qué es MCP?

El *Model Context Protocol* (MCP) es un protocolo abierto que estandariza la comunicación entre aplicaciones de inteligencia artificial y servicios que proporcionan herramientas o información. Utiliza mensajes basados en JSON-RPC 2.0 para intercambiar solicitudes, respuestas y notificaciones.

Mediante MCP, un servidor puede declarar las capacidades que ofrece, como herramientas (*tools*), recursos (*resources*) y plantillas de instrucciones (*prompts*). El cliente MCP puede consultar las capacidades disponibles y comunicárselas al modelo de IA para que este determine cuáles son pertinentes para una tarea.

Por ejemplo, un servidor MCP podría publicar una herramienta llamada `consultar_clima`, que recibe el nombre de una ciudad y devuelve información meteorológica. El modelo puede seleccionar esa herramienta cuando resulte útil, mientras que el cliente y el servidor se encargan de la comunicación y de ejecutar la operación correspondiente.

Es importante distinguir las funciones de cada componente: el modelo puede decidir qué herramienta solicitar, pero el cliente MCP transmite la solicitud y el servidor procesa la operación. El acceso efectivo depende de las capacidades implementadas y de los permisos establecidos.

## Aclaración clave: MCP no sustituye a las API

MCP y las API pueden trabajar juntos. MCP proporciona una interfaz estandarizada para que una aplicación de IA descubra y solicite capacidades, mientras que una API puede ser el mecanismo que utiliza el servidor MCP para acceder al servicio subyacente.

Por ejemplo, si existe una API meteorológica, no es necesario reemplazarla. Se puede desarrollar un servidor MCP que se comunique con esa API y exponga una herramienta como `consultar_clima`. El flujo sería el siguiente:

1. El modelo de IA determina que necesita consultar el clima.
2. El cliente MCP envía una solicitud al servidor para ejecutar la herramienta seleccionada.
3. El servidor MCP utiliza la API meteorológica para obtener los datos.
4. El servidor devuelve el resultado mediante MCP.
5. La aplicación proporciona el resultado al modelo, que puede utilizarlo para elaborar su respuesta.

Este diseño permite integrar servicios existentes con aplicaciones de IA sin que cada aplicación tenga que implementar desde cero una integración particular. Sin embargo, el servidor MCP todavía debe implementar correctamente la conexión con la API y gestionar sus errores, credenciales y permisos.

## Tabla comparativa

| Criterio | API convencional | MCP |
| :--- | :--- | :--- |
| **Propósito** | Define una interfaz para utilizar funciones o servicios de software. | Estandariza la comunicación entre aplicaciones de IA y servidores que proporcionan capacidades. |
| **Quién decide qué se invoca** | Depende de la aplicación cliente y de su lógica de programación. | El modelo puede seleccionar una herramienta según la tarea; el cliente y el servidor gestionan la solicitud y su ejecución. |
| **Descubrimiento de capacidades** | Depende del diseño de la API; puede requerir documentación o admitir mecanismos de descubrimiento. | Define mecanismos para consultar las capacidades que publica un servidor MCP. |
| **Acoplamiento** | Depende del diseño de la interfaz y de cómo se implemente el cliente. | Puede reducir la necesidad de integraciones específicas entre cada aplicación de IA y cada servicio, pero no elimina todos los acoplamientos. |
| **Formato de mensajes** | Depende de la tecnología utilizada, como REST sobre HTTP, SOAP o gRPC. | Utiliza mensajes basados en JSON-RPC 2.0, con transportes definidos por la especificación. |
| **Autenticación y permisos** | Dependen del mecanismo de autenticación y autorización de la API y de la aplicación. | Dependen del contexto de conexión, del transporte, de la configuración y de los controles implementados; MCP no garantiza que siempre exista confirmación humana explícita. |
| **Reutilización** | Una API puede utilizarse desde distintas aplicaciones compatibles con su interfaz. | Un servidor MCP puede ser utilizado por distintos clientes compatibles, siempre que admitan las capacidades y los mecanismos de conexión necesarios. |

## Conclusión

Una API define cómo utilizar un servicio o componente de software, mientras que MCP establece una forma común para que las aplicaciones de IA descubran y soliciten herramientas y recursos proporcionados por servidores compatibles.

Por ello, no deben considerarse tecnologías que compiten directamente. Una API puede seguir ofreciendo el servicio original y un servidor MCP puede exponer parte de sus funciones a una aplicación de IA mediante una interfaz estandarizada. La seguridad continúa dependiendo de la autenticación, los permisos y las medidas de protección implementadas.
