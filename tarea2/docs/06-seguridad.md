# 6. Seguridad en MCP

Conectar un modelo de inteligencia artificial con herramientas que permiten acceder al sistema de archivos introduce riesgos que deben identificarse y mitigarse. La seguridad no depende únicamente del modelo o del protocolo MCP, sino también de la configuración del cliente, las validaciones del servidor y los permisos concedidos al proceso.

## Riesgos principales

1. **Inyección de instrucciones (*prompt injection*):** un archivo puede contener texto malicioso, por ejemplo, instrucciones para ignorar las indicaciones anteriores y eliminar información. Si el modelo interpreta ese contenido como una instrucción que debe seguir, podría intentar utilizar las herramientas disponibles para realizar acciones perjudiciales.
2. **Acceso fuera del directorio autorizado:** una solicitud podría intentar consultar archivos del sistema operativo, documentos personales u otra información que no corresponda a la tarea. Esto puede ocurrir si el servidor no valida correctamente las rutas o tiene permisos demasiado amplios.
3. **Escritura o eliminación no deseadas:** una interpretación incorrecta de la solicitud del usuario o una instrucción maliciosa podría provocar la modificación, sobrescritura o eliminación de archivos importantes.
4. **Exposición de información confidencial:** si el servidor puede acceder a archivos con contraseñas, tokens, claves privadas u otros datos sensibles, estos podrían quedar expuestos al modelo o incluirse accidentalmente en una respuesta.
5. **Permisos excesivos:** ejecutar un servidor con más privilegios de los necesarios aumenta las consecuencias de un error o de una operación maliciosa.

## Medidas de mitigación

- **Confirmación humana (*human-in-the-loop*):** cuando el cliente lo permita, configurar la revisión y confirmación de operaciones sensibles antes de ejecutarlas. No debe suponerse que todos los clientes solicitan autorización para cada herramienta o que una confirmación elimina todos los riesgos. El usuario debe revisar qué operación se realizará y sobre qué archivo.
- **Alcance limitado (*sandboxing*):** configurar el servidor para trabajar únicamente en la carpeta necesaria para la tarea, como `C:\Users\Sanch\mcp-test`. El servidor debe validar las rutas y rechazar los accesos fuera del alcance permitido. Esta restricción debe comprobarse mediante pruebas; no basta con confiar en que la carpeta se indicó en la configuración.
- **Separación entre lectura y escritura:** habilitar únicamente las operaciones necesarias. Si la tarea solo requiere consultar información, conviene utilizar un servidor de solo lectura o deshabilitar las herramientas que modifican archivos.
- **Principio de mínimo privilegio:** ejecutar el servidor con una cuenta y permisos limitados. Así, incluso si se produce un error, se reduce la cantidad de recursos que podrían verse afectados.
- **Protección de información confidencial:** evitar incluir contraseñas, tokens, claves privadas y otros secretos en las carpetas accesibles para el servidor. Las credenciales necesarias para conectarse a servicios deben gestionarse de forma segura.
- **Revisión de las herramientas disponibles:** consultar el catálogo del servidor y comprobar qué operaciones expone. No se debe asumir que todos los servidores utilizan los mismos nombres o que ofrecen las mismas restricciones.
- **Pruebas de seguridad:** comprobar que el servidor puede leer y escribir dentro de la carpeta autorizada cuando corresponda, y que rechaza las operaciones fuera de ella. También conviene probar rutas relativas y otros intentos de evadir las restricciones.

## Conclusión

MCP estandariza la comunicación entre aplicaciones de IA y servidores que ofrecen herramientas, pero no garantiza por sí mismo que todas las operaciones sean seguras. La protección requiere controles en varias capas: permisos del sistema operativo, validación de rutas en el servidor, configuración del cliente, limitación de herramientas y supervisión de operaciones sensibles.

En nuestra práctica, el objetivo será demostrar que el servidor de archivos funciona dentro de la carpeta autorizada y que rechaza los accesos externos. Esta comprobación permitirá verificar una medida concreta de seguridad en lugar de asumir que la configuración es correcta.
