# Práctica 2

## 1. ¿Cuál es la función de la capa de aplicación?
- __Proveer servicios de comunicación__: Ofrece estos servicios tanto a los usuarios (interfaz de usuario o UI) como a las aplicaciones, incluyendo las aplicaciones mismas que utilizan la red
- __Implementar protocolos__: Los protocolos que permiten el funcionamiento de las aplicaciones de red pertenecen a esta capa.
- __Definir la estructura de la comunicación__: Se encarga de definir el formato de los mensajes, su semántica (el significado de cada mensaje) y el diálogo o intercambio de mensajes entre las partes
- __Integrar funciones de otros modelos__: En el enfoque orientado a Internet, la capa de aplicación integra funciones que en el modelo OSI corresponden a las capas de Sesión y Presentación, como la conversión, codificación, compresión y cifrado de datos.

## 2. Si dos procesos deben comunicarse:
- ### a. ¿Cómo podrían hacerlo si están en diferentes máquinas?
    -  Requiere un identificador único compuesto por la dirección del host y el número de puerto (ID del proceso), accedido habitualmente mediante la API de Sockets.
- ### b. Y si están en la misma máquina, ¿qué alternativas existen?
    - Se utilizan mecanismos de IPC (Comunicación Entre Procesos) o las propias interfaces de red locales para el diálogo interno.

## 3. Explique brevemente cómo es el modelo Cliente/Servidor. Dé un ejemplo de un sistema Cliente/Servidor en la “vida cotidiana” y un ejemplo de un sistema informático que siga el modelo Cliente/Servidor. ¿Conoce algún otro modelo de comunicación?
- __Funcionamiento__: Es un esquema de Request/Response y sin estado (stateless)
. El servidor es pasivo (espera la conexión) y el cliente es activo (inicia el diálogo)
- __Transporte y Puertos__: Corre sobre TCP (transporte confiable) utilizando el puerto 80 por defecto en el servidor
. El cliente utiliza cualquier puerto no privilegiado (mayor a 1023)
- __Formato de datos__: Estructura basada en texto (ASCII), aunque permite enviar datos binarios mediante encabezados MIME

## 4. Funcionalidad del "User-Agent"
- __Definición__: Es una cabecera (header) incluida en los requerimientos HTTP que identifica a la entidad que realiza la petición.
- __Propósito__: Permite al servidor conocer qué software, versión y sistema operativo utiliza el cliente.
- __ejemplos__: Identifica si la cosulta proviene de herramientas de línea de comandos como curl o de navegadores específicos como Firefox, Chrome o Safari.
- __Utilidad__: Esta información permite al servidor adaptar el contenido o los mecanismos ofrecidos según las capacidades del cliente (como el manejo de caché o redirecciones)

## 5. Diferencias entre HTML y HTTP
- __HTTP__ (Hypertext Transfer Protocol): Es un protocolo de transferencia de objetos o archivos. Define el esquema de comunicación cliente-servidor, estableciendo la estructura de los mensajes de requerimiento y respuesta(Request/Response)
- __HTML__ (Hypertext Markup Language): Es el lenguaje o formato en el que se escriben los documentos (páginas web). Es un tipo específico de objeto que puede ser transportado por HTTP, junto con otros elementos como imágenes o scripts

## 6. Formato de mensajes HTTP
- __Identificación del mensaje (a)__: La primera línea del mensaje indica si es un requerimiento o una respuesta.
    - Línea de requerimiento: Compuesta por el Método (verbo como GET o POST), el Recurso (nombre del archivo solicitado) y la Versión de HTTP.
    - Línea de respuesta: Compuesta por la Versión de HTTP, el Código de respuesta (ej. 200, 404) y una Frase explicativa para humanos.
- __Cabeceras (a y b)__: Son parámetros adicionales que viajan en una estructura de texto (ASCII). Sirven para brindar información extra, como el software del cliente (User-Agent) o el nombre del servidor (Host)

##  7. Parámetros del comando curl
Aunque la práctica pide investigarlos en la terminal de la VM, basándonos en su uso dentro de los documentos y el funcionamiento estándar de la herramienta, estos sirven para:
- I (o --head): Envía un requerimiento utilizando el método HEAD. Sirve para obtener únicamente las cabeceras de la respuesta del servidor sin descargar el cuerpo del mensaje (el contenido del archivo).
- H (o --header): Permite agregar o modificar cabeceras (headers) personalizadas en el requerimiento enviado al servidor (por ejemplo, para cambiar el User-Agent o el Host).
- X (o --request): Se utiliza para especificar el método HTTP que se desea usar (como GET, POST, HEAD, PUT o DELETE) en lugar del método por defecto.
- s (o --silent): Activa el modo silencioso. Se usa para ocultar la barra de progreso y los mensajes de error en la terminal, lo que resulta útil cuando se redirige la salida a un archivo o a /dev/null.

## 8. Pruebas con curl y navegación
- a. Resultados de curl: Al ejecutar curl sin parámetros, se realiza un único requerimiento y se recibe el código fuente HTML del recurso solicitado. Si se redirige a un archivo .html, se puede abrir con un navegador para ver el contenido estático.
- b. Atributos href/src: En HTML, los atributos href (en etiquetas link) y src (en img) contienen las referencias o rutas a archivos externos necesarios para la página.
- c. Visualización completa: Realizar un único requerimiento no alcanza para ver la página con imágenes; curl solo descarga el archivo solicitado inicialmente y no sus dependencias.
- d. Comparación de requerimientos: Para una página con 2 CSS, 2 JS y 3 imágenes, un navegador realizaría 8 requerimientos (1 HTML + 7 recursos), mientras que curl solo realizaría 1 (solo el HTML)
