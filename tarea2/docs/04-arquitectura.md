# 4. Arquitectura de MCP

El *Model Context Protocol* (MCP) utiliza una arquitectura cliente-servidor para conectar aplicaciones de inteligencia artificial con herramientas y fuentes de información externas. El protocolo define cómo se comunican los componentes y cómo se anuncian y utilizan sus capacidades.

## Los tres roles principales

1. **Host (aplicación anfitriona):** Es la aplicación que integra el modelo de IA y administra la interacción con el usuario. Por ejemplo, puede ser un editor de código o una aplicación de escritorio con funciones de IA.
2. **Cliente MCP:** Es el componente que se ejecuta dentro del host y mantiene la conexión con un servidor MCP. Se encarga de intercambiar mensajes conforme al protocolo y de gestionar las capacidades disponibles.
3. **Servidor MCP:** Es un programa local o remoto que expone capacidades, como herramientas y recursos. Puede interactuar con archivos, bases de datos, servicios web u otros sistemas, según su implementación y los permisos disponibles.

El modelo de IA participa en la toma de decisiones de la aplicación, por ejemplo, al determinar qué herramienta puede ser útil para una tarea. Sin embargo, no es uno de los tres roles principales definidos por la arquitectura MCP. El host integra el modelo, el cliente MCP gestiona la comunicación y el servidor proporciona las capacidades solicitadas.

## Primitivas del servidor

Los servidores MCP pueden ofrecer distintas capacidades a los clientes:

- **Tools (herramientas):** Son funciones que el modelo puede solicitar mediante la aplicación. Por ejemplo, `read_file` podría leer un archivo y `write_file` podría guardar contenido. El servidor valida la solicitud y ejecuta la operación según su implementación y sus permisos.
- **Resources (recursos):** Son fuentes de información que el cliente puede consultar, identificadas mediante URI. Pueden representar documentos, archivos de configuración u otros datos disponibles para la aplicación.
- **Prompts (plantillas):** Son plantillas de mensajes o instrucciones reutilizables que el cliente puede presentar al usuario para facilitar tareas específicas.

Estas capacidades tienen propósitos diferentes: las herramientas permiten solicitar operaciones, los recursos proporcionan información y las plantillas ayudan a estructurar interacciones con el modelo.

## Capacidades del cliente

El protocolo también contempla capacidades que el cliente puede ofrecer al servidor. Entre ellas se encuentran:

- **Roots (raíces):** Permiten al cliente comunicar al servidor directorios o ubicaciones URI relevantes para una tarea. Pueden ayudar a delimitar el contexto de trabajo, pero no constituyen por sí solas una barrera de seguridad. El servidor debe aplicar sus propias comprobaciones de rutas y permisos.
- **Elicitation (solicitud de información):** Permite al servidor solicitar información adicional al usuario mediante el cliente. Por ejemplo, puede pedir que se aclare un parámetro necesario para continuar. La posibilidad de solicitar información o confirmación depende de la función utilizada y de las capacidades admitidas por el cliente; no significa que todas las operaciones requieran autorización humana.

## Transportes

MCP define mecanismos de transporte para intercambiar mensajes entre el cliente y el servidor. Dos opciones importantes son:

1. **stdio (*Standard Input/Output*):** Se utiliza habitualmente para servidores locales. El cliente inicia o administra el proceso del servidor y se comunica con él mediante sus flujos estándar de entrada y salida. No es necesario que aparezca una terminal visible para el usuario.
2. **Streamable HTTP:** Permite la comunicación con servidores mediante HTTP. Es apropiado para conexiones en las que el servidor se encuentra separado del cliente, por ejemplo, en otro equipo o en una infraestructura remota. La configuración debe considerar autenticación, autorización y protección de la conexión cuando corresponda.

El transporte determina cómo se intercambian los mensajes, mientras que MCP define la estructura y el significado de esos mensajes. Por tanto, el protocolo no debe confundirse con un único medio de transporte.

## Nota sobre la especificación

La versión de la especificación MCP utilizada como referencia para este documento es **2024-11-05**. La versión debe identificarse explícitamente porque la especificación evoluciona y algunas capacidades, mecanismos de transporte y requisitos pueden variar entre versiones.

Para una entrega técnica reproducible, conviene indicar la fecha de la especificación realmente consultada y utilizar esa misma versión al describir la arquitectura y sus capacidades.
