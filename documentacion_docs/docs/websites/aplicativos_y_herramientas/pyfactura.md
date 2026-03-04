= PyFactura: Aplicativo para Facturación Electrónica =

PyFactura es una aplicación libre y gratuita para generar Facturas Electrónicas de manera simple y ágil totalmente ad-hoc (independiente) sin necesidad de poseer o tener que modificar un programa de facturación, base de datos o servidor intermedio. AFIP Resolución General RG2485/08, RG2904/10, RG2757/10, RG3067/11, RG3571/13 (factura electrónica mercado interno y nuevos sujetos obligados al régimen)

Utiliza la interfase PyAfipWs para conectarse a los servicios web de manera online. Esta interfase ha sido basada en los ejemplos de la AFIP y ha sido probada con éxito por varias empresas. También puede ser usada para adaptar programas ya existentes.


## Descripción General


### Interfase de Usuario

La interfase de usuario es gráfica de escritorio (GUI), funciona en Windows o Linux:

[[Image(aplicativo_factura_electronica_06a_w8.png)]]

- Cargar: lee los datos de la factura a procesar
- Guardar: almacena los datos de la factura a procesar
- Limpiar: vuelve los campos a su modo inicial
- Obtener CAE: autoriza la factura, completando el CAE y demás datos
- Imprimir: muestra por pantalla o envía a la impresora la factura generada
- Enviar: envia por correo electrónico las facturas generadas

### Funcionalidades

Es similar al aplicativo *Régimen de Emisión de Comprobantes Electrónicos* (R.E.C.E.) del SIAp  AFIP y Servicio Interactivo de *Comprobantes en Línea* (clave fiscal), con las siguientes ventajas:

- Pantalla para carga de datos de clientes y artículos a facturar (utilizando PadronContribuyentesAFIP RG1817 y almacenamiento según RG1361), contemplando las normativas de AFIP aplicables para facturación electrónica y permitiendo almacenar datos de clientes y facturación para no tener que escribirlos por cada factura.
- Autoriza las facturas en linea (usando webservice), simplificando el proceso (no requiere ventanilla electrónica ni ningún otro servicio de clave fiscal o página web), sin limite de facturas ni textos a incluir
- Genera las facturas en un formato PDF gráfico adaptable mediante un [Diseñador Visual](../documentacion_herramientas/manualpyafipws.md#DiseñadorVisualPyFEPDF), pudiendo incluir imágenes (logos) e información adicional, incluyendo el código de barras para ser impreso (opcional).
- Permite múltiples hojas de orientación apaisada (landscape) o retrato (portrait), descripciones de múltiples líneas (con corte y transporte automático)  y control arbitrario de la impresión de decimales.
- Envía mensajes de correo electrónico conteniendo la factura en PDF y un mensaje configurable (tanto en texto plano como en texto estilizado con HTML)
- Importación / exportación desde [Múltiples Formatos de Archivos de Intercambio](wiki:PyRece#Caracterísiticas) (planillas CSV -editables por planilla de cálculo-, archivos de texto de longitud fija TXT similar a RECE, archivos XML similares al Facturador Plus, tablas DBF y archivos JSON) *Próximamente*

Actualmente implementa Factura Electrónica según RG 1956/05, RG 1956/05, 1345/02, 2265/07, 2289/07, y 2485/08 ([Factura Electrónica Mercado Interno - WSFEv1](../factura_electronica/wsfev1.md)) pudiendose adaptar a la resolución general 2557/09 ([BonosFiscales - Bienes de Capital - WSBFE](wiki:BonosFiscales)) o 2758/10 ([Factura de Exportación - WSFEX](wiki:FacturaElectronicaExportacion)) y 2904/10 ([Factura electrónica con detalle - WSMTXCA](wiki:FacturaElectronicaMTXCAService))

Se distribuye sin cargo (gratis, es software libre bajo licencia GPLv3), y se ofrece [Soporte Técnico](wiki:PyFactura#SoporteTécnico) comunitario gratuito o comercial pago opcional (ver [Costos y Condiciones](wiki:PyFactura#CostosyCondiciones)). 

Consultar por desarrollos especiales, interfaces web, etc.

#### Consultar y Recuperar Comprobantes

Desde la revisión 0.9g se puede utilizar la pantalla de consultas y recuperación de comprobantes registrados en AFIP (Menú Consulta):

[[Image(pyfactura_recupero.png)]]

Para consultar comprobantes almacenados en la base de datos, se deben completar los campos para establecer el criterio del filtro.

Para recuperar comprobantes registrados en AFIP, se debe seleccionar el tipo de comprobante, punto de venta y nro de comprobante (desde/hasta), como se muestra en la imágen.
Dado que a AFIP no se informa los datos de cliente (nombre, dirección, etc.), se utiliza el padrón online para completar esos valores. 
Adicionalmente, como no se informa el detalle de los artículos, solo se muestran los subtotales por cada alícuota de IVA.
### Caracterísiticas

- Pantalla simple y ágil para carga de datos de la factura (cliente, fechas, artículos, tributos)
- Autorizar una Factura obteniendo CAE y demás valores devueltos por AFIP
- Confeccionar el PDF con los datos facturados, cliente, detalle, CAE, vencimiento, logo y datos de la empresa emisora, etc.
- Enviar por email con el PDF adjuntado, pudiendo agregar un motivo y cuerpo (texto) configurable.
- Base de datos interna de facturación y clientes (sqlite incorporada, conectable a otros motores como PostgreSQL, MySQL u ODBC -MSSQL Server y MS Access-)

Los datos podrían importarse por archivos de varios formatos (Ver [CSV compatible con Planilla de Calculo, XML similar al [wiki:PyRece#FormatoXMLsimilFacturador-Plus Facturador Plus](wiki:PyRece]):), TXT similar al [SIAP RECE](../documentacion_herramientas/manualpyafipws.md#Archivodetextodeinterfambio), DBF compatible con tablas [Tablas dBase/FoxPro](../documentacion_herramientas/manualpyafipws.md#TablasenDBFparaPyFEPDF), JSON (javascript object notation) para lenguajes modernos con páginas web.

Consultar por adaptación lectura de facturas a autorizar desde bases de datos u otro método (no incluido en el programa básico)

## Configuración

**Importante**: Para utilizar este programa, debe habilitar por clave fiscal (AFIP) el Régimen RECE y [generar los certificados](../documentacion_herramientas/manualpyafipws.md#Certificados). 
Para homologación (evaluación), si no dispone de certificados podemos enviarles unos de prueba ya generados (solicitarlo por mail a pyfactura@sistemasagiles.com.ar)

El archivo de configuración `rece.ini` permite establecer los parámetros para conectarse al Web Service, generar PDF y envio de email (ver [Manual de Configuración](../documentacion_herramientas/manualpyafipws.md#Configuración)):
```
[WSAA]
CERT=homo.crt
PRIVATEKEY=homo.key
#URL=https://wsaa.afip.gov.ar/ws/services/LoginCms

[WSFEv1]
# datos del emisor:
CUIT=20267565393
# categoria IVA (1: Resp. Inscripto, 4 Exento, 6: Monotributo)
CAT_IVA=1
# punto de venta habilitado para factura electrónica
PTO_VTA=97
# archivos de intercambio:
ENTRADA=entrada.txt
SALIDA=salida.txt
#URL=https://servicios1.afip.gov.ar/wsfev1/service.asmx?WSDL

[ARTICULOS]
# código y descripción de conceptos y productos iniciales:
1 = Producto uno
2 = Producto dos
3 = Producto tres
4 = Producto cuatro
5 = Producto cinco
6 = Producto seis
7 = Producto siete

[FACTURA]
ARCHIVO=tipo,letra,numero
FORMATO=factura.csv
DIRECTORIO=.
PAPEL=letter
ORIENTACION=portrait
DIRECTORIO=.
SUBDIRECTORIO=
LOCALE=Spanish_Argentina.1252
FMT_CANTIDAD=0.4
FMT_PRECIO=0.3
CANT_POS=izq
#SALIDA=factura.pdf

[PDF]
LOGO=logo.png
EMPRESA=Mariano Reingart
MEMBRETE1=Profesor Castagna 4942
MEMBRETE2=Capital Federal
CUIT=CUIT 20-26756539-3
IIBB=IIBB 20-26756539-3
IVA=IVA Responsable Inscripto
INICIO=Inicio de Actividad: 01/04/2006
BORRADOR=HOMOLOGACION

[MAIL]
SERVIDOR=smtp.nsis.com.ar
USUARIO=xxxx@nsis.com.ar
CLAVE=xxxxx
MOTIVO=Factura Electronica Nro. NUMERO
CUERPO=Se adjunta Factura en formato PDF
HTML=<b>Se adjunta <i>factura electronica</i> en formato PDF</b>
REMITENTE=Facturador PyRece <pyafipws@sistemasagiles.com.ar>
#CC=copiar@ejemplo.com
#BCC=copiaoculta@ejemplo.com

```
### Diseño de la Factura

El diseño gráfico de la factura en PDF es totalmente parametrizable mediante un archivo CSV, donde se indican los campos y su posición dentro de la hoja, pudidendo establecer los siguientes tipos de campo:

- Texto, con tipo de letra (fuente), tamaño, formato (italico, negrita, subrayado), tamaño y alineación
- Líneas y Cuadros
- Imágenes en formato PNG
- Código de Barras en formato Entrelazado 2 de 5 (requerido por la AFIP)

Ver [Muestra Factura (PDF)](attachment:factura.pdf) y [Muestra Recibo (PDF)](attachment:factura.pdf).

La herramienta incluye el progama `designer.exe` para modificar visualmente los diseños de factura.

A modo de ejemplo se muestra un pantallazo del [Diseñador Visual](../documentacion_herramientas/manualpyafipws.md#DiseñadorVisualPyFEPDF), con el elemento logo seleccionado, editando sus propiedades.

### Mensaje de Correo Electrónico

El mensaje de correo es configurable su motivo, cuerpo y remitente. El destinatario es tomado del la planilla de datos.
También se debe configurar el servidor de correo saliente, y los datos de autorización de ser necesario.

Las versiones recientes permiten incluir un texto con formato HTML para mejorar la presentación del mensaje.
### Régimen de Almacenamiento de Duplicados Digitales (RG1361)

El programa puede adaptarse para generar los archivos requeridos por el aplicativo SIRED (SIAP) de la Resolución General 1361/02 (no incluido en el programa básico), referente al almacenamiento digital de los comprobantes emitidos (Libro Ventas, Detalle y Cabeceras de Factura)




## Soporte Técnico

Al ser software libre ([GPLv3](wiki:PyFactura#Licencia)), puede descargar y usar este programa sin costo de licencias (gratis).

Por consultas gratuitas sobre el lenguaje python y demás, dirigirse a [PyAr](http://www.python.org.ar/) (comunidad Python en Argentina). 

Para soporte gratuito de la comunidad inscribirse y consultar en el [foro público](http://groups.google.com/group/pyafipws), revisar la [lista de incidencias](http://code.google.com/p/pyafipws/issues/list?can=1&q=) y/o [crear una nueva](http://code.google.com/p/pyafipws/issues/entry).

El programa es software libre y se entrega como está, sin garantías explícitas ni implicitas de ningún tipo.
Uselo bajo su propia responsabilidad, conociendo la normativa y reglamentaciones existentes.
### Costos y Condiciones

Opcionalmente ofrecemos soporte técnico comercial via email (asesoramiento, ajustes, corrección de eventuales errores y respuestas rápidas prioritarias) para aquellos clientes que requieran:

- "Garantía Limitada" y Consultas Técnicas: El costo del soporte comercial varía según el webservice a utilizar. Planes recomendados: 
- Soporte Mínimo: $65.550 por 2 semanas de cobertura para asistencia en instalación y configuración inicial (hasta 3hs, no incluye consultas generales y análisis de errores). 
- Soporte Básico: $109.250 por 1 mes de cobertura (hasta 4 hs en total) abarca asistencia en instalación y configuración, atención de consultas generales y administrativas por cuestiones ante AFIP, y análisis de errores (Gestión de CAE) para WSFEv1 . Adicionar $21.850 para PDF y configuración Email
- Soporte Avanzado: desde $21.850/h para temas especiales, ajustes/mejoras particulares, implementación de otros webservices, conexión con bases de datos, interfaces por archivos de intercambio TXT, XML o DBF, almacenamiento por RG1361, diseño gráfico del formatos alternativos de factura en PDF, etc.

- Soporte para generación de archivos csr y key + gestión de certificado digital  + asociación a servicio: $21.850

- Forma de pago: transferencia o depósito bancario 
- Se envía Factura Electrónica C (los precios son finales)
- Consultar por desarrollos a medida o ajustes menores. 

Si necesita capacitación, consultoría o soporte técnico no dude en consultarnos a [mailto:pyfactura@sistemasagiles.com.ar] o telefónicamente al 15-3048-9211

Para más información Ver [Costos y Condiciones Generales](../documentacion_herramientas/pyafipws.md#costos-y-condiciones)
### Licencia

El código fuente puede ser descargado y utilizado sin cargo respentando la licencia [GPLv3](http://www.spanish-translator-services.com/espanol/t/gnu/gpl-ar.html) de software libre: sin garantias, sin soporte tecnico dedicado y/o obligatorio, informar copyright, no incorporarlo ni distribuirlo junto con software propietario, mantener derivados como software libre y contribuir modificaciones, etc. 

## Descargas

Sitio del proyecto en [GitHub](https://www.github.com/SistemasAgiles/pyfactura):

- Instalador para windows: (83MB ya que incluye padrón de contribuyentes)
- [PyFactura-0.9g-32bit-full.exe](https://github.com/SistemasAgiles/pyfactura/releases/download/0.9g/PyFactura-0.9g-32bit-full.exe): Version preliminar 0.9g 2016, con "IVA incluido" y consulta/recupero de comprobantes.
- [PyFactura-0.9e-32bit-full.exe](https://github.com/SistemasAgiles/pyfactura/releases/download/0.9e/PyFactura-0.9e-32bit-full.exe): Version preliminar 0.9e 2015
- Paquete código fuente: [pyfactura-master.zip](https://github.com/SistemasAgiles/pyfactura/archive/master.zip)
- Código fuente: [factura.pyw](https://github.com/reingart/pyfactura/blob/master/factura.pyw) 

### Notas de Instalación

El instalador para Windows es un archivo ejecutable autoextraible generado con NSIS, que instalará el programa y bibliotecas necesarias en el directorio predeterminado `C:\Archivos de Programa\PyFactura`

Para ejecutarlo desde el código fuente (en Linux y Windows), ver dependencias en FacturaElectronicaPython, [gui2py](http://gui2py.googlecode.com) y PyFpdf, y ejecutar `pyrece.py` (más info en instructivo [Instalación Código Fuente](https://code.google.com/p/pyafipws/wiki/InstalacionCodigoFuente))

Deberá revisar la configuración del archivo `rece.ini` (ver [arriba](wiki:PyFactura#Configuración)) y generar los certificados que correspondan.


### Enlaces

Más información en:

- [Factura Electronica Libre](http://www.pyafipws.com.ar/) (sitio web del proyecto)
- FacturaElectronica: Normativa (RG 1956, 2177, 2485, 2557, 2758)
- PyAfipWs: Interfase para programas de terceros 
- PyRece: Aplicativo libre simil SIAP RECE
- SiaPy: Proyecto SIAP Libre

**Importante**: esta es un aplicativo interactivo diseñado específicamente para la intervención con un usuario. Para soluciones automatizadas o embebidas, ver:

- PyAfipWs: interfaz COM o por archivo de texto embebible para otros lenguajes 
- HerramientaFacturaElectronica: solución automatizada por base de datos

MarianoReingart

**[Colaboraciones](https://link.mercadopago.com.ar/colaboracionespyafip)**
MarianoReingart