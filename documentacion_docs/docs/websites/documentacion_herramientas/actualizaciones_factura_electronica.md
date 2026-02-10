= Actualización Factura Electrónica =
[[PageOutline]]

## Service Pack 2

El miercoles 15 de Marzo de 2017 surgió una incidencia puntual dado que AFIP ha publicado una nueva especificación técnica [FEv2.9](wiki:ProyectoWSFEv1#Importante:FEv2.9).

Si no han podido obtener CAE para **Notas de Crédito y Débito**, seguramente estén utilizando una versión desactualizada.

*Motivo*: Desde AFIP agregaron un campo CUIT en Comprobantes Asociados, y lamentablemente desde el webservice están enviando ese nuevo campo vacio (sin datos) en algunos casos (aunque no correspondería ni se haya enviado en la solicitud original de CAE), por lo que no puede ser manejado correctamente por versiones previas.

- El nuevo campo CUIT sólo afectaría a las N/C y N/D que tengan comprobantes asociados, y hay nuevos tipos de comprobante 88 o 991.
- También hay novedades respecto a [tipos de datos Opcionales](wiki:ProyectoWSFEv1#Tiposdedatosopcionales) por **RG 4004-E** Locación de inmuebles destino "casa-habitación", relacionada a alquileres / impuesto a las ganancias.

*Solución Provisoria*: se podría borrar los archivos de la carpeta cache (generalmente subdirectorio de C:\Archivos de Programa\PyAfipWs).
Dichos archivos temporales (WSDL) deberían regenerarse automáticamente con los nuevos campos publicados por AFIP, aunque internamente versiones previas no lo utilicen.
Recordar revisar los permisos (solapa de seguridad de Windows), para que puedan ser creados los nuevos archivos.

Estamos preparando una nueva actualización, ver [Descargas WSFEv1](http://www.sistemasagiles.com.ar/trac/wiki/ProyectoWSFEv1#Descargas) para evaluación, e [Instaladores](wiki:ActualizacionesFacturaElectronica#Instaladores) especiales de cortesía para superar la situación de manera urgente.

Recomendamos contratar un mínimo de horas de [soporte comercial](http://www.sistemasagiles.com.ar/trac/wiki/PyAfipWs#CostosyCondiciones), especialmente si deben usar estas nuevas características y/o no habían actualizado recientemente.

[Mensaje de excepción](http://www.sistemasagiles.com.ar/trac/wiki/ManualPyAfipWs#ManejodeExcepciones) relacionado (al solicitar o consultar CAE para N/C y N/D con Comprobantes Asociados) para versiones afectadas:
```
TypeError: Tag: Cuit invalid (type not found)
```

Fragmento relacionado del [Mensaje XML](wiki:ManualPyAfipWs#MensajesXML) -respuesta devuelta por AFIP- (notar campo **<Cuit />** sin datos):
```
#!xml
<CbteAsoc><Tipo>3</Tipo><PtoVta>2</PtoVta><Nro>1234</Nro><Cuit /></CbteAsoc>
```

NOTA: en caso de que AFIP agregue un campo opcional, pero no se utilice (no lo devuelva en la respuesta), el componente seguirá operando correctamente. 
Esta es la situación general de las Facturas, por lo que no serían afectadas.
En caso de no utilizar Comprobantes Asociados, tampoco estaría afectada la operatoria.
### Instaladores firmados digitalmente

A partir de 2017 los instaladores son firmados digitalmente para garantizar su integridad. 

Al ejecutarlos bajo Windows debería aparecer **"Editor Comprobado: Sistemas Agiles (Mariano Reingart)"**, para validar que es el compilado originalmente y no ha sido alterado.

Para más información ver: [Firma Digital - Editor Comprobado](wiki:ManualPyAfipWs#FirmaDigitalEditorComprobado) (recomendamos descargarlos desde nuestro [Sitio Seguro](https://www.sistemasagiles.com.ar) por HTTPS)
## Service Pack 1

Lamentablemente en 2016 se juntaron varias cuestiones, y hubo un tema en particular con los mensajes de Eventos que AFIP rara vez utilizó (error `'code'`).
El miércoles 14 de Septiembre de 2016 surgió una incidencia puntual, que estaba solucionada en el repositorio y estábamos desplegandolo ordenadamente con tiempo (junto con otras modificaciones y mejoras, viendo con cada cliente en particular)

Si no han podido obtener CAE, seguramente estén utilizando una versión desactualizada. Resumen:

- AFIP empezó a enviar Mensaje de Eventos, primero en Homologación y luego en Producción: 
    - 3: Se informa que se encuentra disponible en modo testing la version 2.8 del ws wsfev1 en el ambiente http://wswhomo.afip.gov.ar/wsfev1/service.asmx. El manual del desarrollador se encuentra en http://www.afip.gob.ar/fe/documentos/manualdesarrolladorCOMPGv28.pdf. Los cambios impactaran en produccion a partir del dia 01/09/2016.
    - 4: IMPORTANTE: El 01/11/2016 se renovarán los certificados SSL utilizados por los webservices de AFIP. Los nuevos certificados utilizarán el algoritmo de encriptacián SHA-2. Para más información http://www.afip.gob.ar/ws/comoAfectaElCambio.asp 
- WSFE (original "versión 0") fue desafectadada definitivamente por AFIP: "1000 Servicio no disponible. Ver documentacion de WSFEV1 http://www.afip.gob.ar/fe/documentos/manualdesarrolladorCOMPGv27.pdf". *Esto solo debería afectar a los usuarios que no hayan actualizado desde 2011.*
- WSASS (certificados de homologación): por cuestiones de seguridad, AFIP solicita generar claves privadas de mayor longitud: "createComputer: Error al dar de alta al computador (CUIT='...', ALIAS='....'). La longitud de clave pública debe ser estar comprendida entre 2048 y 8192 bits"

Sumado a estos temas, a lo largo del año hubo mas de 200 cambios menores en los distintos componentes, con mejoras y ajustes acumulados. Entre ellos:

- [Generación claves 2048+ bits](wiki:ManualPyAfipWs#Erroraldardealtacomputador) (incluyendo firma SHA-256)
- [Análisis de vencimiento de certificados](wiki:ManualPyAfipWs#MétodosparaCertificados)
- [Nueva especificación técnica COMPGv2.8 Sept'16](wiki:ProyectoWSFEv1#Importante:COMPGv2.8)
- [Solicitud de múltiples CAEs por envío](wiki:ManualPyAfipWs#MétodosalternativosparasolicituddemúltiplesCAE)

Para más información ver: [Historial de Cambios](wiki:ManualPyAfipWs#HistorialdeCambios) (manual)

Ver sitio del proyecto para información detallada:

- [Releases](https://github.com/reingart/pyafipws/releases): Liberaciones/Lanzamientos (instaladores de evaluación/ajustes)
- [Commits](https://github.com/reingart/pyafipws/commits/master): Historial del repositorio de código fuente

El proyecto usa el esquema de ***liberación continua*** y en general no se hacen cambios a versiones antiguas, por lo que es recomendable actualizar frecuentemente, ya que todos estos temas ya están resueltos/contemplados en el código actualizado.

Generalmente ofrecemos planes de [soporte comercial](http://www.sistemasagiles.com.ar/trac/wiki/PyAfipWs#CostosyCondiciones) con atención y prioritaria específicos para cada caso, dependiendo de que webservices quisieran actualizar, sistemas operativos donde tienen instalado, lenguaje de programación, características que utilizan, etc. y cualquier otra consulta adicional que podrían tener. 

En caso de optar por el soporte comunitario sin cargo y sin compromiso, dirigirse al [foro público](http://groups.google.com/group/pyafipws), donde también comunicamos las novedades generales del proyecto.

### Instaladores

Por estas cuestiones compilamos la actualización especial parcial "Service Pack" para WSFEv1 en producción (recomendado, especialmente para clientes que hayan actualizado de 2015 en adelante) y una versión de WSAA con los ajustes para nuevos certificados:

- https://www.sistemasagiles.com.ar/soft/pyafipws/PyAfipWsSP2-2.7.1939-32bit+wsfev1_1.18c-update.exe: **Service Pack 2**, actualiza sólo archivos temporales por nueva especificación técnica AFIP [FEv2.9](wiki:ProyectoWSFEv1#Importante:FEv2.9) 13-03-2017, no incluye nuevos campos ni otros ajustes.
- https://github.com/reingart/pyafipws/releases/download/2.7.1872/PyAfipWsSP1-2.7.1874-32bit.wsfev1_1.18a-update.exe o [update4](https://www.sistemasagiles.com.ar/soft/pyafipws/PyAfipWsSP1-2.7.1876-32bit+wsfev1_1.18a-update4.exe) (Service Pack 1, con ajustes menores)
- https://github.com/reingart/pyafipws/releases/download/2.7.1843/PyAfipWs-2.7.1843-32bit.wsaa_2.10g-full.exe (WSAA para claves de 2048 bits + SHA2)

Si se utiliza los aplicativos, descargar los siguientes enlaces: [PyRece](https://github.com/reingart/pyafipws/releases/download/2.7.1872/PyAfipWsSP1-2.7.1874-32bit.pyrece_1.27g-update.exe) y [PyFactura](https://github.com/SistemasAgiles/pyfactura/releases/download/0.9g/PyFactura-0.9g-32bit-update.exe).

Si no han actualizado desde 2014, podrían utilizar una versión especial mas antigua llegado el caso (sólo SP1 de 2016, no aplica a los últimos cambios FEv2.9 de 2017):

- [instalador-PyAfipWsSP1-2.33a-32bit+wsfev1_1.14ce-legacy.exe](https://www.sistemasagiles.com.ar/soft/pyafipws/instalador-PyAfipWsUPDATE-2.33a-32bit+wsfev1_1.14ce-legacy.exe) (2014)
- [instalador-PyAfipWsUPDATE-2.33a-32bit+wsaa_2.08a+wsfev1_1.14ce-full.exe](https://www.sistemasagiles.com.ar/soft/pyafipws/instalador-PyAfipWsUPDATE-2.33a-32bit+wsaa_2.08a+wsfev1_1.14ce-full.exe) (2014, con WSAA)
- [instalador-PyAfipWsUPDATE-2.33a-32bit+wsaa_2.08a+wsfev1_1.14ce+pyfepdf_1.07h+pyemail_1.06a+pyi25_1.02c-full.exe](https://www.sistemasagiles.com.ar/soft/pyafipws/instalador-PyAfipWsUPDATE-2.33a-32bit+wsaa_2.08a+wsfev1_1.14ce+pyfepdf_1.07h+pyemail_1.06a+pyi25_1.02c-full.exe) (2014, con WSAA y PDF)
- [instalador-WSFEV1-1.13ce-legacy.exe](https://www.sistemasagiles.com.ar/soft/pyafipws/instalador-WSFEV1-1.13ce-legacy.exe) (2013)
- [instalador-WSFEV1sp1-1.12j-legacy.exe](https://www.sistemasagiles.com.ar/soft/pyafipws/instalador-WSFEV1sp1-1.12j-legacy.exe) (<2012)

Las versiones "legacy" históricas (previas a 2015) solo las deben usar si venían utilizando una versión anterior y no habían actualizado en los últimos años, especialmente si siguen trabajando en Windows XP o sistemas operativos desactualizados.

Las compilamos especialmente para los clientes que no habían actualizado desde 2015, pero es muy recomendado que actualicen por las últimas novedades de seguridad de AFIP.
 
En general no es necesario modificar nada en la programación de su sistema, salvo que estén utilizando alguna de las últimas características que si se modificaron desde AFIP, o tengan casos puntuales que detallamos a continuación.

Deben revisar bien la [validez de comprobantes emitidos](wiki:ManualPyAfipWs#ValidezdeComprobantesElectronicosemitidos), tanto CAE como datos de las facturas enviadas, ya que pudo haber habido cambios en el formato, cantidad de decimales, validaciones, etc. desde la última vez que actualizaron.

Esto no incluye otros ajustes acumulados a WSAA, PDF y otros componentes (justamente para minimizar el impacto de la actualización), pero debería ser suficiente para las incidencias de estos días.

Adicionalmente, hay otros cambios que dispuso AFIP en estos meses, como las claves de 2048 bits o certificados SHA-2, nueva especificación técnica COMPGv2.8 (aún no documentada), entre otros.


Es recomendable que en cuanto puedan actualicen el resto de los componentes, especialmente si tienen versiones antiguas, para estar preparados ante posibles eventualidades que introducen los cambios de AFIP 
### Recomendaciones

Resumimos las principales observaciones a tener en cuenta debido a las diferentes combinaciones que soporta nuestros componentes: de sistemas operativos (Windows/Linux), bibliotecas DLL, métodos de acceso (COM con o sin `TLB` -librería de tipos-), formatos de archivos de intercambio (TXT/DBF), configuraciones y características utilizadas en cada instalación.

Recomendamos utilizar siempre sistemas operativos originales y actualizados para evitar inconvenientes.
Los últimos instaladores se compilan en Windows 10 con las bibliotecas y herramientas actualizadas (OpenSSL 1.0.2h y Python 2.7.12)

Utilizar las siguiente guía de comprobación (***check-list***) para descartar las incidencias más frecuentes. 

Antes de instalar el ajuste, cerrar todas las aplicaciones para evitar bloqueos de archivos y que no sean actualizados. 

En este caso, WSFEv1 se instalará en una carpeta especial (`PyAfipWsSP1` o `PyAfipWsUPDATE`), para no modificar los otros servicios. 
Se puede indicar una ruta especial, ver [instalación avanzada/desatendida](wiki:ManualPyAfipWs#InstalaciónSilenciosaDesatendida).

Si se utiliza la herramienta `RECE1.exe`, es preferible copiar la configuración anterior (`rece.ini`, clave y certificado) a la nueva carpeta de instalación del ajuste, y ejecutar el programa desde su nueva ubicación.

**IMPORTANTE**: Luego de aplicar el ajuste, es recomendable revisar los CAE obtenidos, constatando los importes y demás datos registrados en AFIP, ver [manual](wiki:ManualPyAfipWs#ValidezdeComprobantesElectronicosemitidos)

Para una lista completa de las incidencias frecuentes, antes de reportarlo revisar [Errores Frecuentes](wiki:ManualPyAfipWs#ErroresFrecuentes), donde podrán encontrar las soluciones a los temas más comunes.
#### Configuración

Una vez instalado el ajuste, recomendamos revisar la configuración de conexión (`rece.ini` o parámetros del método `Conectar`), especialmente:

- `[WSAA]` y `[WSFEv1]`:
- `URL`: utilizar las URL oficiales, sin espacios y respetando mayúsculas y minúsculas, ver [Manual](wiki:ManualPyAfipWs#ConfiguraciónparaProducción)
- `WRAPPER`: ver sección posterior si están utilizando un transporte alternativo, no es necesario configurar esta opción si no han tenido problemas de SSL
- `CACERT`: las versiones más actualizadas refuerzan la [verificacion de canal seguro](wiki:ManualPyAfipWs#VerificacióndelCanaldeComunicaciónSeguro), dejar en blanco o eliminar esta opción para usar la configuración predeterminada, o usar `conf\afip_ca_info.crt` (siempre que dicho archivo esté instalado y actualizado) 
- `[PROXY]`: no utilizar si no es necesario (en lo posible eliminar cualquier sección y/o valor residual que haya podido quedar en la configuración)

#### Permisos

Dependiendo de las políticas de seguridad del equipo, si les surge algún tema de permisos ('permission denied' o similar), es recomendable que ejecuten el instalador como Administrador.
Si el problema persiste, deben ir al subdirectorio cache de esa carpeta, propiedades, solapa seguridad y darle acceso de modificación al usuario que utilice el sistema.

#### Protocolos SSL

En ciertas combinaciones de software, máquinas con sistemas operativos desactualizados (especialmente Windows XP) puede haber un tema de protocolos de seguridad (AFIP esta desafectando los protocolos inseguros/obsoletos y tiene una configuración particular -no estaba soportando la última versión en homologación-).
Por eso pasamos los instaladores de 2013 y 2014 con el ajuste, para minimizar las incidencias.

En ese caso, de que tengan dificultades con el protocolo SSL, pueden usar el cuarto parametro wrapper="pycurl" en el método Conectar, para pasarle otro transporte:

```
wrapper = "pycurl"
ok = WSFEv1.Conectar(cache, wsdl, proxy, wrapper, cacert)
```

Si usan RECE1, pueden configurarlo en el rece.ini

```
[WSFEv1]
...
wrapper = pycurl
...
```

En caso de recibir errores `SSL: CERTIFICATE_VERIFY_FAILED` o similar, no les está validando el canal seguro (certificado del servidor).
Deben revisar el parámetro CACERT en la configuración o en método Conectar (dejar en "" o usar "conf\afip_ca_info.crt" que es el archivo actualizado -si utilizan el ultimo instalador- con los certificados de CA que utiliza AFIP ).
 
Más info: 

- [Errores Protocolo SSL](wiki:ManualPyAfipWs#ErroresdeProtocoloSSL)
- [Verificación de Canal Seguro](wiki:ManualPyAfipWs#VerificacióndelCanaldeComunicaciónSeguro)

##### OpenSSL

Si previamente está instalada una versión antigua de la herramienta de criptografía (recomendada por AFIP), puede ser necesario actualizarla:

- https://slproweb.com/download/Win32OpenSSL-1_0_2k.exe (32 bits)
- https://slproweb.com/download/Win64OpenSSL-1_0_2k.exe (64 bits)

En caso de ser solicitado, se necesitaría instalar también los Redistribuibles de Microsoft Visual C 2013 (Runtime):

- https://www.microsoft.com/es-ar/download/details.aspx?id=40784

Para probar el correcto funcionamiento, ingresar a una terminal / consola (Menú Inicio, Ejecutar, CMD) y escribir:
```
C:\> c:\OpenSSL-Win32\bin\openssl.exe version

OpenSSL 1.0.2h  3 May 2016

```


#### Formatos de Intercambio

Si bien no ha habido cambios mayores en los formatos, los siguientes cambios pueden afectar si la versión anterior utilizada era muy antigua:

- [Formato TXT](wiki:ManualPyAfipWs#FacturaelectrónicaMercadoInternoVersión1WSFEv1): usar 2 decimales para los importes (por validación de AFIP)
- [Formato DBF](wiki:ManualPyAfipWs#FacturaelectrónicamercadointernoWSFEv1): Campo `ID` en tabla `IVA` se renombró a `IVAID`. Campo `CAE` debe ser alfanumérico. Ver muestras en [tablas-dbf.zip](attachment:tablas-dbf.zip)

Siempre es posible revisar el formato actual que utiliza la herramienta ejecutando:
```
RECE1.exe /formato
RECE1.exe /formato /dbf
```

En ambos casos, se agregó la estructura para [Datos Opcionales](wiki:ManualPyAfipWs#DatosOpcionalesAFIPWSFEv1) por resolución de AFIP.
No es necesario incluir estos datos si no se utilizan, pero en el caso de Tablas DBF, la misma debe estar vacía.

```
[DBF]
Encabezado = encabeza.dbf
Tributo = tributo.dbf
Iva = iva.dbf
Comprobante Asociado = cbteasoc.dbf
Detalle = detalles.dbf
Permiso = permiso.dbf
Dato = dato.dbf
Datos Opcionales = opcional.dbf
```

Notar de agregar la última linea de ser necesario.

#### Campos vacios o nulos

Dado que AFIP ha agregado reglas y validaciones sobre que algunos campos no deben enviarse -o deben enviarse vacíos- en algunos casos puntuales, la interfaz no envía más valores predeterminados.

En todos los casos debe indicarse un valor específico, los casos puntuales más importante los siguientes (especialmente si están actualizando de una versión relativamente antigua): 

- `doc_nro` debe indicarse en 0 para consumidor Final
- Si no se utilizan importes, pasar 0 o nulo (por ej. en `imp_op_ex` y imp_trib).
- Si no se utiliza la fecha de servicios / vencimiento de pago, debe enviarse nulo en `fecha_venc_pago` por ej.


Para enviar un valor nulo, y que el campo no se envíe, usar vbNull o el que corresponda al lenguaje de programación. 
Para pasar un campo vació, si debe pasarse `""` (string vació).

En estos casos AFIP puede devolver el error `"Server was unable to read request. ... There is an error in XML document (5, 1234)"`, justamente porque no se están enviando bien los datos.
En este, ejemplo se deberí revisar linea 5 caracter 1234 en el requerimiento XML (!XmlRequest), pudiendo encontrar allí el campo incorrecto.

Para más información sobre como depurar estos casos, ver:

- [Mensajes XML](wiki:ManualPyAfipWs#MensajesXML)
- [Manejo de Excepciones](wiki:ManualPyAfipWs#ManejodeExcepciones)
  
### Linux

En Linux (y/o también si utilizan el código fuente), descargando y reemplazando el archivo [wsfev1.py](https://github.com/reingart/pyafipws/raw/master/wsfev1.py) debería solucionarse si tienen una versión actualizada.

Es recomendable hacer un backup ante cualquier eventualidad.

Como solución provisoria si lo anterior no funciona, pueden volver al archivo wsfev1.py original que tenian y comentar las lineas donde aparece el error.
La linea cuestión que deben ajustar, comentar (agregar un #) o eliminar seria:

```
#!python
self.Eventos = ['%s: %s' % (evt['code'], evt['msg']) for evt in events]
```

Pueden ver el cambio en [GitHub](https://github.com/reingart/pyafipws/commit/c072a0a2d337372ac0d61d5dd2830195ef7bb9f1)

En Linux si tienen una versión muy antigua que no es compatible con los últimos cambios, deberían actualizar todas las librerias y componentes (están en el mismo repositorio).
Siempre pueden descargar todo el código fuente actualizado desde: https://github.com/reingart/pyafipws/archive/master.zip

En la documentación del sitio del proyecto pueden obtener más información: 

- Instructivo [Instalación desde el código fuente](https://github.com/reingart/pyafipws/wiki/InstalacionCodigoFuente)
- La explicación más detallada en el [reporte de incidencias](https://github.com/reingart/pyafipws/issues/29)

También ofrecemos soporte comercial para estos casos.

### Algoritmo SHA-2 y claves 2048 bits

#### Certificados Servidores AFIP

El 1/11/16 AFIP cambiaría los certificados de sus servidores a SHA-2, en principio, esto no debería de traer mayores incidencias y no debería implicar ninguna acción por parte de los contribuyentes en sus certificados.

Sí podría afectar la verificación de canal seguro (según especificación técnica de AFIP), ya que esos certificados se utilizan para validar la conexión a los servidores.
Eventualmente, en el caso de que AFIP cambie las [Autoridades certificantes reconocidas por AFIP](http://www.afip.gov.ar/ws/paso4.asp?noalert=1#tablaautoridades) (empresa emisora del certificado del servidor, actualmente "!AddTrust / Comodo" o "!GeoTrust"), sería necesario realizar cambios en la configuración (ver abajo).

Previendo estas cuestiones, nuestro componente ya incorpora los ajustes necesarios, pero igualmente es recomendable dejar configurable por el usuario/administrador los parámetros de conexión (tanto `url` -wsdl-, `cacert`, `wrapper`, etc.) ya que AFIP ha realizado cambios en estas cuestiones a lo largo de los años.

Resumiendo, en general, si tienen el sistema operativo actualizado y versiones recientes de los componentes, no tendría que haber mayores inconvenientes. 

**De todos modos recomendamos actualizar los componentes, tener en cuenta estas configuraciones parametrizable y hacer las pruebas en ambiente de homologación con anticipación.**

Para mas información y alternativas sobre estos temas ver:

- [Verificación de Canal Seguro](wiki:ManualPyAfipWs#VerificacióndelCanaldeComunicaciónSeguro)
- [Protocolo SSL](wiki:ActualizacionesFacturaElectronica#ProtocolosSSL)

**NOTA:**: en caso de que eventualmente AFIP cambie de entidad certificante, se podrían seguir algunas de las siguientes alternativas de configuración (método `Conectar` o secciones `[WSAA]` / `[WSFEv1]` del `rece.ini`):

- utilizar `wrapper="pycurl"` que utiliza los certificados de  CA de Windows (los certificados que utilice AFIP deberían estar incorporados y ser reconocidos por el sistema operativo)
- utilizar `cacert=WSAA.InstallDir+"\httplib2\cacerts.txt"` que contiene todos los certificados (alternativamente, es posible descargar y usar las versiones actualizadas desde los sitios de los respectivos proyectos: [cacerts.txt](https://github.com/httplib2/httplib2/blob/master/python2/httplib2/cacerts.txt) o [cacert.pem](https://curl.haxx.se/ca/cacert.pem))
- modificar el archivo `conf/afip_ca_info.crt` agregando el nuevo certificado de CA (se puede obtener con cualquier navegador, presionando generalmente sobre el ícono de sitio seguro, ver certificado, exportar)
- deshabilitar provisoriamente la comprobación del certificado del servidor de AFIP, pasando string vacio, ej `cacert=""` (no es recomendado ya que implica riesgos de seguridad)

Dado que aún no hay cambios documentados por AFIP en las especificaciones técnicas al respecto, solo se debería prever tener estas opciones configurables, sin realizar ningún cambio inmediato por el momento.
#### Certificados Contribuyentes

Mas allá del tema mencionado anteriormente, todos los contribuyentes deberían generar/renovar entre el mes de Diciembre y Febrero 2017, los certificados con clave de longitud 2048bit y firmados con el nuevo algoritmo SHA-2.

**IMPORTANTE:** los certificados aún no vencidos pueden ser utilizados hasta su fecha de vencimiento, según el [sitio de AFIP](http://www.afip.gov.ar/ws/):

    *Este cambio NO implica que deba gestionarse nuevamente el certificado de su computador fiscal. El mismo podrá seguir siendo utilizado hasta su fecha de vencimiento. Solo deberá asegurarse de que su sistema pueda dialogar con los servicios web de AFIP mediante SSL validando los nuevos certificados de los sitios de AFIP con tecnología SHA-2. Le recomendamos realizar las pruebas antes del 1/11/2016 en el ambiente de homologación, que ya cuenta con los certificados renovados.*

Es posible revisar la fecha de vencimiento por Clave Fiscal, "Administrador de Certificados Digitales", utilizando nuestra herramienta (ver [Métodos para Certificados WSAA](wiki:ManualPyAfipWs#MétodosparaCertificados)) u OpenSSL directamente.

Con las últimas versiones de la interfaz PyAFIPWs, pueden generarse los archivos con los últimos requerimientos de AFIP: [Generación de Certificados](wiki:ManualPyAfipWs#Generación)

Para evaluar un instalador de nuestra herramienta WSAA con estos ajustes iniciales, ver [release](https://github.com/reingart/pyafipws/releases/tag/2.7.1843):

- https://github.com/reingart/pyafipws/releases/download/2.7.1843/PyAfipWs-2.7.1843-32bit.wsaa_2.10g-full.exe

AFIP aparentemente ya estaría renovando los certificados con vencimiento 2018 y nuevo algoritmo, por lo que ya se podrían ir realizando pruebas.
Nuevamente, los certificados antiguos, en teoría, serían válidos hasta la fecha de su vencimiento. 
De todos modos, en estos aspectos, las respuestas de la mesa de ayuda de AFIP han sido ambiguas o inciertas, por lo que recomendamos ir renovandolos con tiempo (se puede tener el certificado antiguo y el nuevo en funcionamiento simultáneamente).

El evento código 4 mensaje *"IMPORTANTE: El 01/11/2016 se renovarán los certificados SSL utilizados por los webservices de AFIP. Los nuevos certificados utilizarón el algoritmo de encriptación SHA-2. Para más información http://www.afip.gob.ar/ws/comoAfectaElCambio.asp"*, no está relacionado con los certificados de los contribuyentes, por lo que en general seguirá apareciendo hasta la fecha en que AFIP lo deje de enviar.

Dado que AFIP puede utilizar los eventos para difundir cuestiones importantes, se recomienda mostrarlo al usuario, desarrollador o quien corresponda.

En caso de necesitar acompañamiento particular para renovar un certificado (generación, trámites, etc.), consultar (ver [planes de soporte comercial](http://www.sistemasagiles.com.ar/trac/wiki/PyAfipWs#Paquetespromocionales)).