# Ejemplo 6

## Plataformas IoT

Hasta el momento hemos visto los siguientes temas:

* Conceptos basicos de programación de las sistemas de desarrollo Arduino UNO y ESP32.
* Algunos conceptos basicos entre sensores y actuadores.
* Comunicación serial.
* Comunicación inalambrica usando Wifi.

De los temas anteriormente vistos, es importante resaltar la importancia que juega la comunicación en una arquitectura IoT; asi mismo, que estas no son las unicas maneras de trabajar con datos, sin embargo, con saber por ahora esto basta.

Tal y como se muestra en la siguiente figura (tomada de IoT Engineering - [link](https://github.com/tamberg/fhnw-iot/tree/master/03))

![Iot-reference-model](Iot-reference-model.png)

En el modelo de referencia IoT, uno de los elementos claves son las plataformas IoT pues permiten almacenar y almacenar (entre otras cosas) datos de sensores. Para conectar las cosas con estas plataformas con las cosas, es importante conocer la forma como se lleva a cabo la comunicación y la interación establecida por estas la cual, generalmente es a traves de peticiones HTTP expuestas a traves de APIs.

Respecto al manejo de APIs, el siguiente documento se muestra un ejemplo tipico de un API ([cheatsheet_api](cheatsheet_api.pdf))

## APIs

Una interfaz de programación de aplicaciones (API) permite una conversación de software con otra.  Utiliza interacciones basadas en la web o protocolos de comunicación comunes y sus propios estándares patentados determinando qué tipo de datos, servicios y funcionalidad expone la aplicación a terceros.

![API](imagenes_teoria/api.png)

Las API están diseñadas para ser consumidas mediante programación por otras aplicaciones y también pueden ser usadas por usuarios que desean interactuar con la aplicación manualmente. 

Los tres tipos más populares de estilos arquitectónicos API son:
* RPC
* SOAP
* ⁪REST

## API REST

Transferencia de Estado Representacional (REST) es un estilo arquitectónico escrito por Roy Thomas Fielding.

Una API de servicio web REST (API REST) es una interfaz de programación que se comunica a través de HTTP, por lo que utiliza los mismos conceptos que el protocolo HTTP:
* Solicitudes/respuestas HTTP
* Verbos HTTP
* Código de estado HTTP
* Encabezados/cuerpo HTTP

![api-rest](imagenes_teoria/api-rest.png)

A continuación vamos a analizar tanto las solicitudes como las respuestas.

### Solicitudes de API REST

Las solicitudes de API REST son solicitudes HTTP en las que una aplicación (cliente) pide al servidor que realice una función.  Las solicitudes de API REST se componen de cuatro componentes principales:
* **Identificador uniforme de recursos (URI)**: También conocido como **localizador uniforme de recursos (URL)**, identifica qué recurso desea manipular el cliente. 
  
  ![componentes-uri](imagenes_teoria/componentes-uri.png)

  Tal y como se resalta en la figura anterior, las URI tienen los siguientes componentes:
  * **Esquema**: especifica qué protocolo HTTP se debe usar, http o https.
  * **Autoridad**: consta de dos partes, a saber, host y puerto
  * **Ruta de acceso**: representa la ubicación del recurso, los datos u objeto, que se va a manipular en el servidor. 
  * **Consulta**: proporciona detalles adicionales sobre el ámbito, el filtrado o para aclarar una solicitud. 
  
* **Método HTTP:**: Empleado para comunicarse con los servicios web para los que se solicita la acción para el recurso dado. La asignación sugerida del método HTTP a la acción es la siguiente:
  
  |Método HTTP:|Acción|Descripción|
  |---|---|---|
  |POST|Crear (Create)|Crear un nuevo objeto o recurso.|
  |GET|lectura (Read)|Recuperar detalles de recursos del sistema.|
  |PUT|Actualizar|Reemplace o actualice un recurso existente.|  
  |PARCHE|Actualización parcial|Actualice algunos detalles de un recurso existente.|
  |DELETE|Eliminar (Delete)|Remover un recurso del sistema.|

* **Encabezado**: tienen el formato de pares **```nombre-valor```** separados por dos puntos (**:**); esto es, ```[nombre]: [valor]```. Podemos distinguir dos tipos de encabezados:
  *  **Encabezados de solicitud**: incluye información adicional que no esté relacionada con el contenido del mensaje.
  

    |Clave | Valor de ejemplo |Descripción |
    |---|---|---|
    |Autorización|DMFNCMFUDDP2YWDYYW básico|Proporciona credenciales para autorizar la solicitud|


  *  **Encabezados de entidad**: información adicional que describe el contenido del cuerpo del mensaje.
    

    |Clave | Valor de ejemplo |Descripción |
    |---|---|---|
    |Tipo de contenido|aplicación/ JSON|PEspecificar el formato de los datos en el cuerpo|
 
* **Cuerpo**: El cuerpo de la solicitud de API REST contiene los datos correspondientes al recurso que el cliente desee manipular. Las solicitudes de API REST que utilizan el método HTTP POST, PUT y PATCH suelen incluir un cuerpo lo que hace que cuerpo sea opcional dependiendo del método HTTP. 

### Respuestas API REST

Las respuestas de la API REST son respuestas HTTP que comunica los resultados de la solicitud HTTP de un cliente. La Respuesta REST API se componen de tres componentes principales:
* **Estado HTTP**: El código de estado HTTP ayuda al cliente a determinar el motivo del error y a veces puede proporcionar sugerencias para solucionar el problema. Los códigos de estado HTTP constan de tres dígitos, donde el primer dígito es la categoría de respuesta y los otros dos dígitos son asignados en orden numérico. Hay cinco categorías diferentes de códigos de estado HTTP:
   * **1xx - Informativo**: con fines informativos, las respuestas no contienen un cuerpo
   * **2xx - Éxito**: el servidor recibió y ha aceptado la solicitud
   * **3xx - Redirección**: el cliente tiene que tomar una acción adicional para completar la solicitud
   * **4xx - Error de cliente**: la solicitud contiene un error como sintáxis incorrecta o entrada no válida
   * **5xx - Error del servidor**: no se pueden cumplir las solicitudes válidas.
 
    Los codigos de estado mas comunes se muestran a continuación:

    |Código de Estado HTTP|Mensaje de estado|Descripción|
    |---|---|---|
    |200|Aceptar|La solicitud se realizó correctamente y normalmente contiene una carga útil (cuerpo)|
    |201|Creada|Se cumplió la solicitud y se creó el recurso que fue solicitado|
    |202|Aceptada|La solicitud ha sido aceptada para su procesamiento y está en proceso|
    |400|Solicitud no valida|La solicitud no se procesará debido a un error con la solicitud|
    |401|No autorizado|La solicitud no tiene credenciales de autenticación válidas para realizar la solicitud|
    |403|Prohibida|La solicitud ha sido entendida pero ha sido rechazada por el servidor|
    |404|No se encontró|No se puede cumplir la solicitud porque la ruta de acceso del recurso de la solicitud no se encontró en el servidor|
    |500|Error del servidor interno|No se puede cumplir la solicitud debido a un error del servidor|
    |503|El servicio no está disponible|No se puede cumplir la solicitud porque actualmente el servidor no puede manejar la solicitud|

* **Encabezado**: El encabezado de la respuesta proporciona información adicional entre el servidor y el cliente en el formato de par **```nombre-valor```** que está separado por dos puntos (**:**), ```[nombre]:[valor]```. Hay dos tipos de encabezados: 
   * **Encabezados de respuesta**: contiene información adicional que no está relacionada con el contenido del mensaje. Los encabezados de respuesta típicos para una solicitud de API REST incluyen:
    
     |Clave|Valor de ejemplo|Descripción|
     |---|---|---|
     |Set-Cookie|JSESSIONID=30A9DN810FQ428P; Ruta=/|Se utiliza para enviar Cookies desde el servidor|
     |Control de caché|Control de caché: max-edad=3600, público|Especificar directivas que DEBEN ser obedecidas por todos los mecanismos de almacenamiento en el caché|

   * **Encabezados de entidad**: son información adicional que describe el contenido del cuerpo del mensaje. Un encabezado de entidad común especifica el tipo de datos que son devueltos:

     |Clave|Valor de ejemplo|Descripción|
     |---|---|---|
     |Tipo de contenido|Aplicación/JSON|SEspecificar el formato de los datos en el cuerpo|
    
* **Cuerpo**: Contiene los datos asociados a la respuesta.

## Algunos APIs de utilidad

* https://learn.adafruit.com/adafruit-io/rest-api
* https://www.sparkfun.com/news/2379
* http://dweet.io/
* http://freeboard.io/


## Enlaces

1. https://wokwi.com/
2. https://markmegarry.github.io/AVR8js-Falstad/
3. https://wokwi.com/
4. https://tawjaw.github.io/Arduino-Robot-Virtual-Lab/
5. https://tawjaw.github.io/Arduino-Robot-Virtual-Lab/index.html
6. https://forum.arduino.cc/t/virtual-online-arduino-and-esp32-simulator-wokwi-arduino-simulator-features/698481/5
7. http://iotfactory.eu/iot-knowledge-center/overview-of-iot-networks/
8. https://www.c-sharpcorner.com/UploadFile/f88748/internet-of-things-iot-an-introduction/
9. https://www.c-sharpcorner.com/UploadFile/f88748/internet-of-things-part-2/
10. https://www.c-sharpcorner.com/UploadFile/f88748/internet-of-things-iot-part-3/
11. https://www.c-sharpcorner.com/UploadFile/f88748/internet-of-thingsiot-part-4-network-protocols-and-arc/
12. https://www.ccontrols.net/cz-sk/applications/internet-of-things-iot/wireless-networks/
13. https://www.sam-solutions.com/blog/internet-of-things-iot-protocols-and-connectivity-options-an-overview/
14. https://www.lanner-america.com/es/iot/
15. https://en.wikipedia.org/wiki/Comparison_of_wireless_data_standards
16. https://www.digikey.com/en/articles/comparing-low-power-wireless-technologies
17. https://www.digikey.com/en/articles/comparing-low-power-wireless-technologies-part-2
18. https://bismark.net.co/como-avanzan-redes-lpwan/
19. http://www.ane.gov.co/Documentos%20compartidos/ArchivosDescargables/consultapublica/contenidos/ComentariosAnexoNormatividadUsoLibre/Respuesta_Comentarios_Anexo_Normatividad_Uso_Libre.pdf
20. https://www.aprendiendoarduino.com/tag/sigfox/
21. https://repositorio.uchile.cl/bitstream/handle/2250/171099/Evaluacion-del-protocolo-HTTP2-para-Internet-de-las-cosas.pdf?sequence=1&isAllowed=y
22. https://editores-srl.com.ar/sites/default/files/aa2_semle_protocolos_ilot.pdf
23. https://forum.huawei.com/enterprise/es/protocolo-http-en-iot-miuconhuawei/thread/624779-100275
24. https://cloud.google.com/blog/products/iot-devices/http-vs-mqtt-a-tale-of-two-iot-protocols
25. https://microsoft.github.io/IoT-For-Beginners/#/2-farm/lessons/2-detect-soil-moisture/README
26. https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-devguide-protocols
27. https://docs.oracle.com/en/cloud/paas/iot-cloud/iotrq/toc.htm
28. https://www.nabto.com/rest-api-iot-guide/
29. https://docs.microsoft.com/en-us/rest/api/iothub/
30. https://github.com/homieiot/homie-esp8266
31. https://openforce.com/de/blog/openhab-mqtt-homie/
32. https://www.instructables.com/Building-Homie-Devices-for-IoT-or-Home-Automation/
33. https://diyprojects.io/getting-start-homie-library-mqtt-connected-objects-esp8266/#.YbDMOL3MLIU
34. http://revistas.unisimon.edu.co/index.php/innovacioning/article/view/3771/4701
35. https://aprendiendoarduino.wordpress.com/2017/10/11/saber-mas-iniciacion-arduino-2017/
36. http://www.microhomie.com/en/master/
37. https://arest.io/
38. http://dweet.io/
39. https://create.arduino.cc/projecthub/frankzhao/iot4car-1b07f1
40. https://bossinsights.com/integrations/iot/adafruit/
41. https://learn.sparkfun.com/tutorials/esp8266-thing-hookup-guide?_ga=2.146596982.374019962.1638969666-812475524.1634861735
42. http://lucstechblog.blogspot.com/2019/07/esp-webserver-tutorial-part-1-textfields.html
43. https://www.esp8266.com/
44. https://learn.sparkfun.com/tutorials/internet-of-things-experiment-guide
45. https://learn.sparkfun.com/tutorials/photon-remote-water-level-sensor#setting-up-text-alerts
46. https://docs.arduino.cc/cloud/iot-cloud/tutorials/esp-32-cloud
47. https://docs.arduino.cc/built-in-examples/control-structures/WhileStatementConditional
48. https://docs.arduino.cc/tutorials/generic/basic-servo-control
49. https://docs.arduino.cc/tutorials/generic/introduction-to-the-serial-peripheral-interface
50. https://programarfacil.com/podcast/proyectos-iot-con-arduino/
51. https://www.instructables.com/Send-SMS-from-Arduino-over-the-Internet-using-ENC2/
52. https://www.networkworld.com/article/3133738/dweetio-a-simple-effective-messaging-service-for-the-internet-of-things.html
53. https://github.com/gamo256/dweet-esp
54. https://www.hackster.io/javier-munoz-saez/esp8266-sending-data-to-an-online-deskboard-3e7e91
55. https://www.fatalerrors.org/a/building-a-simple-internet-of-things-project-with-esp8266.html