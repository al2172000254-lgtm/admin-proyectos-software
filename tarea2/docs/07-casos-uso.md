# 7. Casos de uso actuales

El *Model Context Protocol* (MCP) se utiliza en distintas aplicaciones de inteligencia artificial para conectar modelos con herramientas externas y fuentes de información. En el desarrollo de software, permite integrar asistentes de programación con archivos, repositorios, bases de datos y otros servicios sin depender exclusivamente de que el usuario copie y pegue la información manualmente.

## Herramientas que utilizan MCP

1. **Claude Desktop (Anthropic):** Es una aplicación de escritorio que permite conectar servidores MCP para acceder a herramientas y fuentes de información. Según los servidores instalados y los permisos configurados, es posible consultar archivos, interactuar con servicios y realizar otras operaciones.

2. **Cursor:** Es un editor de código con funciones de inteligencia artificial que admite servidores MCP. Su asistente puede utilizar las herramientas disponibles para consultar fuentes externas, obtener información de servicios conectados y trabajar con el contexto de un proyecto. La ejecución de operaciones depende de las herramientas instaladas y de la configuración del editor.

3. **Zed:** Es un editor de código que integra MCP para conectar su agente de programación con servidores externos. Esta integración permite utilizar herramientas y plantillas de instrucciones proporcionadas por los servidores compatibles.

4. **Google Antigravity:** Es un entorno de desarrollo impulsado por agentes de inteligencia artificial que admite MCP. Permite conectar servidores para obtener información de bases de datos, consultar documentación y utilizar herramientas externas durante las tareas de desarrollo.

La compatibilidad con MCP no significa que todas estas aplicaciones incluyan las mismas herramientas de forma predeterminada. Sus capacidades dependen de los servidores conectados, de las funciones que admita cada aplicación y de los permisos configurados.

## ¿Cómo pueden trabajar con repositorios completos sin copiar archivos manualmente?

Sin una integración con herramientas externas, el usuario podría tener que copiar fragmentos de código y pegarlos en la conversación para que el modelo los analice. Con MCP, una aplicación puede conectarse a un servidor que proporcione herramientas para buscar, leer o modificar archivos.

Por ejemplo, si el programador necesita localizar la función que calcula los impuestos en un repositorio, el flujo de trabajo podría ser el siguiente:

1. **Solicitud del usuario:** pide localizar y revisar la función que calcula los impuestos.
2. **Selección de herramientas:** el modelo identifica que necesita buscar en los archivos y solicita utilizar las herramientas disponibles.
3. **Ejecución en el servidor:** el servidor busca en los directorios autorizados y devuelve los fragmentos de código relevantes.
4. **Análisis:** el modelo utiliza la información recibida para explicar cómo funciona la función o proponer una modificación.
5. **Aplicación del cambio:** si el usuario solicita modificar el código y la aplicación dispone de una herramienta de escritura autorizada, el modelo puede solicitar esa operación al servidor.
6. **Verificación:** el usuario o el agente puede revisar los cambios y ejecutar pruebas mediante las herramientas disponibles.

De esta manera, MCP permite conectar el modelo con información y operaciones externas. Sin embargo, el protocolo no concede automáticamente acceso a todo el repositorio ni garantiza que los cambios se ejecuten sin intervención humana: esas posibilidades dependen de la configuración, los permisos y las capacidades del cliente y del servidor.

## Aclaraciones sobre las tecnologías mencionadas

- **Qwen:** es una familia de modelos de inteligencia artificial, no una plataforma de desarrollo específica. Un modelo de esta familia puede integrarse en una aplicación compatible con herramientas, según la implementación.
- **Google Antigravity:** es un entorno de desarrollo que admite la conexión con servidores MCP.
- **MCP:** es un protocolo abierto de comunicación; no es un modelo de lenguaje, un editor de código ni un servidor de archivos específico.

## Conclusión

MCP facilita la integración de asistentes de inteligencia artificial con herramientas y fuentes de información externas. En el desarrollo de software, esto puede reducir el trabajo manual de proporcionar contexto y permitir flujos de trabajo que incluyan búsqueda, análisis y modificación de código.

No obstante, las operaciones disponibles y el grado de autonomía del asistente dependen de la aplicación, los servidores conectados, los permisos y los controles de seguridad establecidos.
