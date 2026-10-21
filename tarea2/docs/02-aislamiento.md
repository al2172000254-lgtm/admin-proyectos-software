# 2. El problema del aislamiento

Un modelo de lenguaje grande (*Large Language Model*, LLM), por sí solo, procesa información en forma de texto y genera respuestas. No tiene acceso automático al sistema de archivos, a los programas ni a los recursos de la computadora del usuario. Por ejemplo, si se le pide que lea el archivo `config.json`, no podrá hacerlo a menos que el contenido se le proporcione o disponga de una herramienta autorizada que le permita acceder al archivo.

El aislamiento de un LLM respecto al entorno del usuario puede explicarse desde dos perspectivas: la arquitectura del sistema y la seguridad.

## Razones de arquitectura

Estas razones se relacionan con la forma en que se construyen y conectan los componentes del sistema:

- **Ejecución remota:** muchos LLM se ejecutan en servidores remotos, como los de servicios en la nube. En esos casos, el servidor que ejecuta el modelo no tiene acceso directo al disco duro de la computadora del usuario. Para acceder a archivos locales, la aplicación necesita un mecanismo adicional de comunicación y una herramienta con los permisos correspondientes.
- **Separación entre el modelo y el entorno:** el modelo procesa la información que recibe en su contexto. No puede consultar por sí mismo variables de entorno, directorios, redes locales ni otros recursos del sistema. Una aplicación puede proporcionarle esa información mediante herramientas o servicios externos.
- **Estado y contexto:** el modelo utiliza el contexto disponible en cada solicitud. La conservación del historial y la recuperación de información entre solicitudes dependen de la aplicación y de los mecanismos que esta implemente; no deben confundirse con un acceso directo del modelo al sistema de archivos.

## Razones de seguridad

Estas razones se relacionan con la protección de los datos, los recursos del sistema y las acciones que puede ejecutar la IA:

- **Aislamiento (*sandboxing*):** conceder a una aplicación de IA permisos de lectura y escritura sin restricciones sobre todo el disco puede provocar daños accidentales o facilitar acciones maliciosas. Limitar el acceso a carpetas y operaciones específicas reduce ese riesgo.
- **Permisos y consentimiento del usuario:** el acceso a los archivos debe controlarse mediante permisos explícitos y mecanismos de autorización adecuados. Por ejemplo, un servidor puede configurarse para trabajar únicamente dentro de una carpeta determinada, en lugar de permitir el acceso a todo el equipo.
- **Inyección de instrucciones (*prompt injection*):** un archivo, una página web u otra fuente externa puede contener instrucciones maliciosas dirigidas al modelo, como pedirle que ignore las indicaciones anteriores o que realice acciones no autorizadas. Si el sistema dispone de herramientas, esas instrucciones podrían intentar inducirlo a utilizarlas de forma perjudicial. Por ello, es importante validar las operaciones, limitar los permisos y solicitar confirmación humana para las acciones sensibles cuando corresponda.

En conclusión, un LLM no obtiene acceso a los archivos del usuario simplemente por ser capaz de comprender texto. Ese acceso depende de la aplicación que lo integra, de las herramientas disponibles y de los permisos que se les concedan. Protocolos como el *Model Context Protocol* (MCP) permiten conectar modelos con herramientas y fuentes de información, pero no eliminan la necesidad de establecer controles de seguridad.
