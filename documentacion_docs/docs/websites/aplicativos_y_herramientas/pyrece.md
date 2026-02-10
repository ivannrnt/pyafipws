= PyRece: Aplicativo Autorizador y Generador de Facturas Electrónicas =
[[TracNav(FacturaElectronica|noreorder|nocollapse)]]

## Índice
[[TOC(noheading,inline,depth=2)]]

## Descripción General

PyRece es una aplicación libre y gratuita para generar Facturas Electrónicas (similar al SIAP/RECE) totalmente ad-hoc (independiente) sin necesidad de poseer o tener que modificar un programa de facturación, base de datos o servidor intermedio.

Utiliza la interfase PyAfipWs para conectarse a los servicios web de manera online. Esta interfase ha sido basada en los ejemplos de la AFIP y ha sido probada con éxito por varias empresas. También puede ser usada para adaptar programas ya existentes.

Es similar al aplicativo *Régimen de Emisión de Comprobantes Electrónicos* (R.E.C.E.) del SIAp AFIP, con las siguientes ventajas:

- Permite leer y grabar las facturas desde [Múltiples Formatos de Archivos de Intercambio](wiki:PyRece#Caracterísiticas) (planillas CSV o XLSX -editables por planilla de cálculo / MS Excel-, archivos de texto de longitud fija TXT similar a RECE, archivos XML similares al Facturador Plus, tablas DBF y archivos JSON)
- Autoriza las facturas en linea (usando webservice), simplificando el proceso (no requiere ventanilla electrónica ni ningún otro servicio de clave fiscal o página web)
- Genera las facturas en un formato PDF gráfico adaptable mediante un [Diseñador Visual](wiki:ManualPyAfipWs#DiseñadorVisualPyFEPDF), pudiendo incluir imágenes (logos) e información adicional, incluyendo el código de barras para ser impreso (opcional).
- Permite múltiples hojas de orientación apaisada (landscape) o retrato (portrait), descripciones de múltiples líneas (con corte y transporte automático)  y control arbitrario de la impresión de decimales.
- Envía mensajes de correo electrónico conteniendo la factura en PDF y un mensaje configurable (tanto en texto plano como en texto estilizado con HTML)

[[Image(PyFactura:aplicativo_factura_electronica_06a_w8.png,align=right,width=223,height=218,link=PyFactura)]]

Actualmente implementa Factura Electrónica según RG 1956/05, RG 1956/05, 1345/02, 2265/07, 2289/07, y 2485/08 ([Factura Electrónica Mercado Interno - WSFEv1](wiki:ProyectoWSFEv1)) pudiendose adaptar a la resolución general 2557/09 ([BonosFiscales - Bienes de Capital - WSBFE](wiki:BonosFiscales)) o 2758/10 ([Factura de Exportación - WSFEX](wiki:FacturaElectronicaExportacion)) y 2904/10 ([Factura electrónica con detalle - WSMTXCA](wiki:FacturaElectronicaMTXCAService))

Se distribuye sin cargo (gratis, es software libre bajo licencia GPLv3), y se ofrece [Soporte Técnico](wiki:PyRece#SoporteTécnico) comunitario gratuito o comercial pago opcional (ver [Costos y Condiciones](wiki:PyRece#CostosyCondiciones)). 

Consultar por desarrollos especiales, interfaces web, etc.

**Próximamente**: integración con PyFactura, aplicativo visual de factura electrónica:



### Caracterísiticas

- Autorizar un conjunto de Facturas, ya sea por lote de facturas B o facturas A/B individuales, obteniendo CAE y demas valores
- Confeccionar el PDF con los datos facturados, cliente, detalle, CAE, vencimiento, logo y datos de la empresa emisora, etc.
- Enviar por email el PDF, con un motivo y cuerpo (texto) configurable.

Los datos se ingresan por archivos de varios formatos:

- XLSX compatible con MS Excel / !LibreOffice Calc. Ver [Planilla de Ejemplo (XLSX)](https://github.com/reingart/pyafipws/blob/master/datos/facturas.xlsx)
- CSV compatible con Planilla de Calculo. Ver [Planilla de Ejemplo (CSV)](attachment:facturas.csv)
- XML similar al [Facturador Plus](wiki:PyRece#FormatoXMLsimilFacturador-Plus) [Archivo de Ejemplo (XML)](attachment:facturas.xml)
- TXT similar al [SIAP RECE](wiki:ManualPyAfipWs#Archivodetextodeinterfambio) [Archivo de Ejemplo (TXT)](attachment:facturas.txt)
- DBF compatible con tablas [Tablas dBase/FoxPro](wiki:ManualPyAfipWs#TablasenDBFparaPyFEPDF) [Carpeta Comprimida (DBF)](attachment:tablas-dbf.zip)
- JSON (javascript object notation) para lenguajes modernos e hiperactividad con páginas web.

Consultar por adaptación lectura de facturas a autorizar desde bases de datos u otro método (no incluido en el programa básico)

### Interfase de Usuario

La interfase de usuario es gráfica de escritorio (GUI), funciona en Windows o Linux:

[[Image(pantalla.png)]]

- Examinar: permite buscar el archivo a procesar
- Cargar: carga los datos del archivo a procesar
- Autenticar: inicia la sesión en los servidores de AFIP
- Autorizar: autoriza las facturas, completando el CAE y demás datos
- Previsualizar: muestra por pantalla la factura generada
- Enviar: envia por correo electrónico las facturas generadas

### Planilla de Entrada

El aplicativo necesita los campos obligatorios con el formato y códigos que requiere cada webservice.
Los campos opcionales o adicionales son tendidos en cuenta para la generación del PDF, pero no son informados a AFIP.

La cabecera de cada factura debe contener los siguientes datos:

- tipo_cbte: código de comprobante según tablas de AFIP (1 FCA, 6 FCB, 11 FCC, 19 FCE)
- punto_vta: número del punto de venta (prefijo 4 dígitos)
- cbt_numero: número de comprobante (8 dígitos)
- fecha_cbte: fecha del comprobante en formato AAAAMMDD
- tipo_doc: código de tipo de documento (80: CUIT, 96: DNI, 99: C.F.)
- nro_doc: número de documento, CUIT, etc.
- moneda_id: código de moneda según tabla (PES: pesos, DOL: dólares, 012: Real, etc.)
- moneda_ctz: cotízación de la moneda (ej. 3.987)
- imp_neto: importe neto (gravado por IVA)
- imp_iva / impto_liq: importe total liquidado de IVA
- imp_trib: importe total de los otros tributos
- imp_op_ex: importe de operaciones exentas de IVA
- imp_tot_conc: importe de los conceptos no gravados por IVA
- imp_total: importe total del comprobante (sumatoria de todos los importes parciales)
- fecha_venc_pago: fecha de vencimiento para el pago (solo servicios)
- concepto / presta_serv: tipo facturación (1: productos, 2: servicios, 3: productos y servicios)
- fecha_serv_desde: fecha de inicio del período facturado (solo servicios)
- fecha_serv_hasta: fecha de finalización del período facturado (solo servicios)

Datos del Cliente (solo se informan para WSFEX, pero se usan para generar el PDF):

- nombre
- domicilio
- localidad
- telefono
- categoria: condición de IVA (R.I., Exento, Monotributo, etc.)
- email: dirección de correo electrónico (obligatorio para enviar notificaciones)

Detalles (obligatorio para WSFEX/WSBFE/WSMTXCA):

- cantidad1: (qty)
- descripcion1: nombre o detalle del artículo
- precio1: precio unitario del artículo
- importe1: importe subtotal (precio*cantidad) del artículo
- umed: unidad de medida (7: unidades, kg, metros, etc., solo WSFEX/WSMTXCA/WSBFE)
- iva_id1: alícuota de IVA del artículo (solo WSMTXCA/WSBFE)
- imp_iva1: importe liquidado de IVA del artículo (solo WSMTXCA)
- bonif1: importe bonificado del artículo (solo WSBFE)
- ncm / sec: código del nomenclador común del mercosur, secretaría de comercio (solo WSBFE)

IVAs (solo WSFEv1/WSMTXCA):

- iva_id_1: código de alícuota de IVA (por ej. 5: 21%)
- iva_base_imp_1: base imponible gravada por esta alícuota
- iva_importe_1: importe liquidado de IVA para esta alícuota

Tributos (solo WSFEv1/WSMTXCA):

- tributo_id_1: codigo del tipo de impuesto (1: nacional, 2: provincial, 3: municipal, 99: otro)
- tributo_desc_1: descripción del impuesto (ej. "Perc.IIBB")
- tributo_base_imp_1: base imponible gravada por el impuesto
- tributo_alic_1: alicuota del impuesto
- tributo_importe_1: importe liquidado del impuesto (base_imp * alic / 100)

Respuesta:

- cae: código de autorización electrónica obtenido
- fecha_vto: fecha del vencimiento del CAE
- resultado: estado del proceso (A: aprobado, O: observado, R: rechazado)
- motivo: códigos o detalle de observación
- reproceso: S o N (solo WSFE/WSFEX/WSBFE)
- id; identificador general de la factura (requeido WSFE, WSFEX, WSBFE)
 
**Nota**: los campos repetitivos (por ej. detalle de cada item), se pueden repetir cambiando el número, ej: Cantidad1 para el primer artículo, Cantidad2 para el segundo artículo, etc.

### Formato XML simil Facturador-Plus

Las versiones recientes de PyRece soportan un formato similar al Facturador Plus para simplificar el manejo de facturas mediante archivos XML:

```
#!xml
<?xml version="1.0" encoding="UTF-8"?>
<comprobantes>
    <comprobante>
        <concepto>3</concepto>
        <condicion_frente_iva/>
        <domicilioreceptor>Rua 76 km 34.5 Alagoas</domicilioreceptor>
        <importetotal>122.0</importetotal>
        <idimpositivoreceptor>PJ54482221-l</idimpositivoreceptor>
        <localidadreceptor/>
        <fechaservdesde>20110608</fechaservdesde>
        <receptor>Joao Da Silva</receptor>
        <reproceso/>
        <nrodocreceptor>30000000007</nrodocreceptor>
        <motivo/>
        <id>0</id>
        <tributos>
            <tributo>
                <desc>Impuesto Municipal Matanza</desc>
                <alic>1.0</alic>
                <baseimp>100.0</baseimp>
                <id>99</id>
                <importe>1.0</importe>
            </tributo>
        </tributos>
        <otrosdatoscomerciales>Observaciones Comerciales, texto libre</otrosdatoscomerciales>
        <tipocambio>0.5</tipocambio>
        <tipo>1</tipo>
        <numero_cotizacion/>
        <detalles>
            <detalle>
                <importe>121.0</importe>
                <unimed>7</unimed>
                <numero_despacho/>
                <cant>1.0</cant>
                <preciounit>100.0</preciounit>
                <tasaiva>5</tasaiva>
                <importeiva>21.0</importeiva>
                <ncm/>
                <sec/>
                <bonificacion/>
                <desc>Descripcion del producto P0001</desc>
                <cod>P0001</cod>
            </detalle>
        </detalles>
        <numero_cliente/>
        <ptovta>4000</ptovta>
        <fechaemision>20110608</fechaemision>
        <numero_remito/>
        <tipodocreceptor>80</tipodocreceptor>
        <importeopex>0.0</importeopex>
        <numero>1</numero>
        <telefonoreceptor/>
        <importeiva>21.0</importeiva>
        <fechaservhasta>20110608</fechaservhasta>
        <otrosdatosgenerales>Observaciones Generales, texto libre</otrosdatosgenerales>
        <cuitemisor/>
        <importetotalconcepto>0.0</importetotalconcepto>
        <emailgeneral/>
        <importetributos>1.0</importetributos>
        <resultado/>
        <provinciareceptor/>
        <ivas>
            <iva>
                <baseimp>100.0</baseimp>
                <id>5</id>
                <importe>21.0</importe>
            </iva>
        </ivas>
        <fechavencpago>20110608</fechavencpago>
        <formaspago>
            <formapago>
                <descripcion>30 dias</descripcion>
                <codigo/>
            </formapago>
        </formaspago>
        <importeneto>100.0</importeneto>
        <moneda>012</moneda>
        <fecha_vto>20110320</fecha_vto>
        <idioma/>
        <cae>61123022925855</cae>
        <numero_orden_compra/>
    </comprobante>
</comprobantes>
```

### Formato JSON

Internamente el aplicativo utiliza un formato simple, compatible con los lenguajes modernos mediante archivos .json (Java Script Object Notation):
```
#!js
[
    {
        "tipo_cbte": "6", 
        "punto_vta": "5", 
        "cbt_numero": "7", 
        "tipo_doc": "80", 
        "nro_doc": "30500010912", 
        "fecha_cbte": "20110609", 
        "nombre_cliente": "Cliente XXX", 
        "numero_cliente": "21601192", 
        "domicilio_cliente": "Patricia 1 - Cdad de Buenos Aires - 1405 - Capital Federal - Argentina", 
        "cae": "61233038185853", 
        "fecha_vto": "20110619", 
        "resultado": "A", 
        "cbte_nro": "7", 
        "concepto": "1", 
        "condicion_frente_iva": "Exento", 
        "cuit": "20205766", 
        "datos": [
            {
                "campo": "telefono", 
                "pagina": "", 
                "valor": ""
            }, 
            {
                "campo": "categoria", 
                "pagina": "", 
                "valor": "IVA RESPONSABLE INSCRIPTO"
            }
        ], 
        "detalles": [
            {
                "codigo": "P1675G", 
                "ds": "PRUEBA ART", 
                "imp_iva": "0.00", 
                "importe": "1076.68", 
                "iva_id": "0", 
                "numero_despacho": "110170P", 
                "precio": "1076.68", 
                "qty": "1.0", 
                "umed": "07"
            } 
        ], 
        "email": "mariano@sistemasagiles.com.ar", 
        "fecha_serv_desde": "", 
        "fecha_serv_hasta": "", 
        "fecha_venc_pago": "", 
        "fecha_vto": "", 
        "forma_pago": "30 Dias", 
        "id": "1", 
        "idioma": "1", 
        "imp_iva": "186.86", 
        "imp_neto": "889.82", 
        "imp_op_ex": "0.00", 
        "imp_tot_conc": "0.00", 
        "imp_total": "1085.57", 
        "imp_trib": "8.89", 
        "ivas": [
            {
                "base_imp": "889.82", 
                "importe": "186.86", 
                "iva_id": "5"
            }
        ], 
        "moneda_ctz": "1.000000", 
        "moneda_id": "PES", 
        "motivo": "", 
        "numero_cotizacion": "82016336", 
        "numero_orden_compra": "6443", 
        "numero_remito": "00008001", 
        "reproceso": "", 
        "tributos": [
            {
                "tributo_id": "99",
                "desc": "Impuesto municipal matanza",
                "alic": "1.00",
                "base_imp": "889.82", 
                "importe": "8.89"
            }
        ] 
    }
]
```

### Configuración

Para utilizar este programa, debe habilitar por clave fiscal el Régimen RECE y [generar los certificados](wiki:ManualPyAfipWs#Certificados).

El archivo de configuración permite establecer los parámetros para conectarse al Web Service, generar PDF y envio de email:
```
[WSAA]
CERT=homo.crt
PRIVATEKEY=homo.key
#URL=https://wsaa.afip.gov.ar/ws/services/LoginCms

[WSFE]
CUIT=30000000007
#URL=https://servicios1.afip.gov.ar/wsfe/service.asmx

[WSFEv1]
CUIT=30000000007
#URL=https://servicios1.afip.gov.ar/wsfev1/service.asmx?WSDL

[FACTURA]
ARCHIVO=tipo,letra,numero
FORMATO=factura.csv
DIRECTORIO=.
PAPEL=letter
ORIENTACION=portrait
DIRECTORIO=.
SUBDIRECTORIO=
LOCALE=Spanish_Argentina.1252
FMT_CANTIDAD=0.6
FMT_PRECIO=0.3
CANT_POS=izq
#SALIDA=factura.pdf
COPIAS=3

[PDF]
LOGO=logo.png
EMPRESA=Mariano Reingart
MEMBRETE1=Profesor Castagna 4942
MEMBRETE2=Capital Federal
CUIT=CUIT 20-26756539-3
IIBB=IIBB 20-26756539-3
IVA=IVA Responsable Inscripto
INICIO=Inicio de Actividad: 01/04/2006
Item.Descripcion01=PRUEBA - FACTURA NO VALIDA

[MAIL]
SERVIDOR=smtp.nsis.com.ar
USUARIO=xxxx@nsis.com.ar
CLAVE=xxxxx
MOTIVO=Factura Electronica Nro. NUMERO
CUERPO=Se adjunta Factura en formato PDF
HTML=<b>Se adjunta <i>factura electronica</i> en formato PDF</b>
REMITENTE=Facturador PyRece <pyafipws@sistemasagiles.com.ar>
```

### Diseño de la Factura

El diseño gráfico de la factura en PDF es totalmente parametrizable mediante un archivo CSV, donde se indican los campos y su posición dentro de la hoja, pudidendo establecer los siguientes tipos de campo:

- Texto, con tipo de letra (fuente), tamaño, formato (italico, negrita, subrayado), tamaño y alineación
- Líneas y Cuadros
- Imágenes en formato PNG
- Código de Barras en formato Entrelazado 2 de 5 (requerido por la AFIP)

Ver [Muestra (PDF)](attachment:factura-0004-00000001.pdf) y [Formato de ejemplo (CSV)](attachment:factura.csv).

La herramienta incluye el progama `designer.exe` para modificar visualmente los diseños de factura.

A modo de ejemplo se muestra un pantallazo del [Diseñador Visual](wiki:ManualPyAfipWs#DiseñadorVisualPyFEPDF), con el elemento logo seleccionado, editando sus propiedades:
[[Image(ManualPyAfipWs:designer.png)]]
### Mensaje de Correo Electrónico

El mensaje de correo es configurable su motivo, cuerpo y remitente. El destinatario es tomado del la planilla de datos.
También se debe configurar el servidor de correo saliente, y los datos de autorización de ser necesario.

Ver [Email de Muestra](attachment:email.eml) 

Las versiones recientes permiten incluir un texto con formato HTML para mejorar la presentación del mensaje.
### Transferencia de Archivos (FTP)

Puede configurarse la transferencia de archivos por FTP a un servidor remoto para la posterior descarga de la factura (no incluido en el programa básico).

### Régimen de Almacenamiento de Duplicados Digitales (RG1361)

El programa puede adaptarse para generar los archivos requeridos por el aplicativo SIRED (SIAP) de la Resolución General 1361/02 (no incluido en el programa básico), referente al almacenamiento digital de los comprobantes emitidos (Libro Ventas, Detalle y Cabeceras de Factura)

## Licencia

El código fuente puede ser descargado y utilizado sin cargo respentando la licencia [GPLv3](http://www.spanish-translator-services.com/espanol/t/gnu/gpl-ar.html) de software libre: sin garantias, sin soporte tecnico dedicado y/o obligatorio, informar copyright, no incorporarlo ni distribuirlo junto con software propietario, mantener derivados como software libre y contribuir modificaciones, etc. 


## Soporte Técnico

Ofrecemos Soporte Comercial Opcional Pago (ver [abajo](wiki:PyRece#CostosyCondiciones)), incluyendo garantía limitada (corrección de eventuales errores o ajustes) y respuestas rápidas prioritarias.

Por consultas gratuitas sobre el lenguaje python y demás, dirigirse a [PyAr](http://www.python.org.ar/). 

Para soporte de la comunidad, revisar la [lista de temas](http://code.google.com/p/pyafipws/issues/list?can=1&q=) y/o [crear uno nuevo](http://code.google.com/p/pyafipws/issues/entry) 

## Costos y Condiciones

- Al ser software libre ([GPLv3](wiki:PyRece#Licencia)), puede usar este programa sin costo de licencias.
- "Garantía Limitada" y Soporte Técnico: opcional soporte técnico via email a partir de fecha de factura; el costo varía según el webservice a utilizar:
- Consultar planes vigentes según webservice y tipo de archivo a implementar.
   
- Consultar por soporte avanzado, combinación de varios webservices, base de datos o archivos de intercambio TXT, XML o DBF, almacenamiento por RG1361 o ajustes/mejoras, diseño gráfico del formatos alternativos de factura en PDF (no incluido en el soporte básico).
- Forma de pago: transferencia o depósito bancario 
- Se envía Factura Electrónica C
- Consultar por desarrollos a medida o ajustes menores. 

**Importante**: esta es un aplicativo interactivo que requiere diseñado específicamente para la intervención con un usuario. Para soluciones automatizadas o embebidas, ver:

- PyAfipWs: interfaz COM o por archivo de texto embebible para otros lenguajes 
- HerramientaFacturaElectronica: solución automatizada por base de datos

## Descargas
Archivos disponibles en [GitHub](http://www.sistemasagiles.com.ar/trac/wiki/PyRece):

- Instalador para windows: [PyAfipWs-2.7.2189-32bit+pyrece_1.32b-homo.exe](https://www.sistemasagiles.com.ar/soft/pyafipws/PyAfipWs-2.7.2189-32bit+pyrece_1.32b-homo.exe) (versión 1.32b admite FCE Agosto 2019)
- Instalador para windows: [PyAfipWs-2.7.1701-32bit.pyrece_1.27d-full.exe](https://github.com/reingart/pyafipws/releases/download/2.7/PyAfipWs-2.7.1701-32bit.pyrece_1.27d-full.exe) (Version 1.27c Julio 2015)
- Instalador para windows: [instalador-PyRece-1.23e-full.exe](http://pyafipws.googlecode.com/files/instalador-PyRece-1.23e-full.exe) (Version 1.23e 2011)
- Instalador para windows: [instalador-pyrece-v17.exe](http://pyafipws.googlecode.com/files/instalador-pyrece-v17.exe) (version original)
- Paquete para linux: [pyrece-v18.tgz](http://pyafipws.googlecode.com/files/pyrece-v18.tgz)
- Código fuente: [pyrece-v17.zip](http://pyafipws.googlecode.com/files/pyrece-v17.zip) 

## Notas de Instalación

El instalador para Windows es un archivo ejecutable autoextraible generado con 7zip, que instalará el programa y bibliotecas necesarias en el directorio `C:\PYRECE`

Para ejecutarlo desde el código fuente (en Linux y Windows), ver dependencias en FacturaElectronicaPython, [PythonCard](http://python.org.ar/pyar/PythonCard) y PyFpdf, y ejecutar `pyrece.py`:

Ejemplo para GNU/Linux Debian o derivados (Ubuntu): abrir una consola y ejecutar las siguientes órdenes (actualizar paquetes, bajar archivo, descomprimir, iniciar aplicativo):
```
#!sh
sudo apt-get install python-httplib2 python-m2crypto pythoncard 
wget http://pyafipws.googlecode.com/files/pyrece-v18.tgz
tar xvzf pyrece-v18.tgz
cd pyrece
python pyrece.py
```

Deberá revisar la configuración del archivo `rece.ini` (ver arriba) y generar los certificados que correspondan.

El programa es software libre y se entrega como está, sin garantías explícitas ni implicitas de ningún tipo.
Uselo bajo su propia responsabilidad, conociendo la normativa y reglamentaciones existentes.
Si necesita capacitación, consultoría o soporte técnico no dude en consultarnos a [mailto:pyrece@sistemasagiles.com.ar] o telefónicamente al 15-3048-9211

## Enlaces
Más información en:

- FacturaElectronica: Normativa (RG 1956, 2177, 2485, 2557, 2758)
- PyAfipWs: Interfase para programas de terceros 
- SiaPy: Proyecto SIAP Libre

MarianoReingart

**[Colaboraciones](https://link.mercadopago.com.ar/colaboracionespyafip)**
MarianoReingart