# 5. El servidor de sistema de archivos

El servidor de sistema de archivos (*Filesystem MCP Server*) no forma parte del protocolo MCP en sí, sino que es una implementación que permite demostrar cómo utilizar MCP para acceder a archivos y directorios. El protocolo define cómo se comunican el cliente y el servidor, mientras que la implementación determina qué operaciones están disponibles y cómo se ejecutan.

Existen implementaciones de referencia del servidor de archivos, y también es posible desarrollar servidores MCP propios para trabajar con otros sistemas o adaptar las herramientas a necesidades específicas.

## ¿Qué herramientas expone?

El servidor de archivos puede proporcionar herramientas para realizar operaciones sobre el sistema de archivos local. Entre las operaciones habituales se encuentran:

- **Leer archivos:** consultar el contenido de un archivo de texto.
- **Escribir archivos:** crear archivos o modificar su contenido.
- **Listar directorios:** obtener la lista de archivos y carpetas de una ubicación.
- **Crear directorios:** generar nuevas carpetas.
- **Mover o renombrar archivos:** cambiar la ubicación o el nombre de un archivo.
- **Buscar archivos:** localizar archivos que coincidan con determinados criterios, como un patrón de nombre o contenido.

Los nombres exactos de las herramientas dependen de la implementación y de su versión. Por ello, antes de utilizar nombres como `read_file`, `write_file` o `list_directory`, es necesario consultar el catálogo de herramientas que publica el servidor MCP instalado.

## ¿Cómo se limita el acceso mediante directorios?

Al configurar un servidor de archivos, se pueden especificar los directorios en los que está permitido trabajar. En nuestra práctica, utilizaremos la ruta:

`C:\Users\Sanch\mcp-test`

El objetivo es que el servidor permita operar dentro de esa carpeta, en lugar de conceder acceso indiscriminado al sistema de archivos.

Cuando recibe una solicitud para acceder a un archivo, el servidor debe comprobar que la ruta solicitada se encuentre dentro de los directorios permitidos. Si la operación intenta acceder a una ubicación no autorizada, debe rechazarla.

Por ejemplo, si el servidor está limitado a `C:\Users\Sanch\mcp-test`, una solicitud para leer un archivo de `C:\Windows\System32` debería rechazarse.

Esta protección depende de la implementación del servidor y de la forma en que valide las rutas. También es importante considerar los enlaces simbólicos, las rutas relativas y los permisos del sistema operativo. Por tanto, especificar una carpeta permitida no garantiza por sí solo que cualquier implementación sea completamente segura.

## ¿Qué riesgos existirían sin límites de acceso?

Si un servidor de archivos tuviera permisos amplios y no aplicara controles adecuados, las herramientas expuestas podrían permitir operaciones sobre archivos ajenos a la tarea prevista. Entre los riesgos se encuentran:

- **Modificación o eliminación accidental:** una solicitud incorrecta podría alterar o borrar archivos importantes.
- **Exposición de información confidencial:** archivos de configuración, documentos personales o credenciales almacenadas podrían quedar accesibles.
- **Modificación de código fuente:** una operación de escritura podría cambiar archivos de un proyecto fuera del alcance deseado.
- **Abuso mediante inyección de instrucciones (*prompt injection*):** contenido malicioso presente en un archivo podría intentar inducir al modelo a solicitar operaciones perjudiciales mediante las herramientas disponibles.

Estos riesgos no significan que el modelo tenga acceso automático a todo el disco. Las operaciones posibles dependen de las herramientas que exponga el servidor, de sus validaciones y de los permisos con los que se ejecute.

En conclusión, el servidor de archivos muestra cómo MCP permite que una aplicación de IA solicite operaciones sobre archivos mediante herramientas estandarizadas. Para utilizarlo de forma segura, es necesario limitar los directorios permitidos, aplicar validaciones de rutas, conceder únicamente los permisos necesarios y comprobar las operaciones que pueden modificar o eliminar información.
