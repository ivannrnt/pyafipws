# Código Trazabilidad de Granos (RG2806/2010, RG3113/11, RG3593/14)


Interfaz para Servicio Web correspondiente a Boletín Oficial 05/04/2010 - Resolución General 2806/2010 - TRANSPORTE DE GRANOS - Procedimiento. Decreto Nº 34/09. Norma Conjunta RG 2595 (AFIP), Resolución 3253 (ONCCA) y Disposición 6 (SSTA), su modificatoria y complementaria. Sistema de emisión, seguimiento y control de Carta de Porte. Transporte automotor y ferroviario de carga de granos. Resolución General AFIP Nº 3113/2011 V.1. Resolución General AFIP 3593/14: registro sistémico de movimientos y existencias de granos

## Descripción General

EL WSCTG (Web Service de Código de Trazabilidad Electrónica) es un nuevo Servicio Web de la AFIP para 
Transporte de Granos, correspondiente a la [RG 2806/2010 V.0](http://biblioteca.afip.gob.ar/gateway.dll/Normas/ResolucionesGenerales/reag01002806_2010_03_26.xml) y su [RG3113/11 modificatoria V.1](http://biblioteca.afip.gob.ar/gateway.dll/Normas/ResolucionesGenerales/reag01003113_2011_05_17.xml) (marco normativo [RG2300/07](http://biblioteca.afip.gob.ar/gateway.dll/Normas/ResolucionesGenerales/reag01002300_2007_09_03.xml), [Transporte Automotor - RG2595/09](http://biblioteca.afip.gov.ar/gateway.dll/Normas/ResolucionesGenerales/reag01002595_2009_04_14.xml) y [Registro de Operaciones - RG2596/09](http://biblioteca.afip.gob.ar/gateway.dll/Normas/ResolucionesGenerales/reag01002596_2009_04_15.xml))

El servicio WSCTG ya esta en etapa Producción. El webservice permite la Solicitud del CTG (carta de porte) y su Confirmación (obteniendo constancia en PDF)

La nueva versión WSCTGv1.1 incluye soporte para WEB SERVICE DE CODIGO DE TRAZABILIDAD DE GRANOS (wsctg)  **Versión 1.1** (modificada el 29-03-2012)

Para mayor información, se puede consultar la documentación orignal en [Micrositio Granos - AFIP](http://www.afip.gob.ar/granos/) o el [manual](../documentacion_herramientas/manualpyafipws.md) de la presente interfaz. 

Recordar verificar la correcta obtención del CTG para la Carta de Porte y Vehiculo en [Consulta Validez CTG](http://www.afip.gov.ar/genericos/granos/consultaCTG/WebForm1.aspx)

### RG3593/14: Movimientos y existencia de granos

El 20/2/2014 AFIP ha pulbicado la [Resolución General 3593/14](http://www.boletinoficial.gov.ar/DisplayPdf.aspx?f=20140220&s=01&pd=17&ph=19&sup=False) "REGIMEN DE REGISTRACION SISTEMATICA DE MOVIMIENTOS Y EXISTENCIA DE GRANOS", para los sujetos comprendidos en el "Registro Unico de Operadores de la Cadena Agroalimentaria”, de acuerdo con la Resolución N° 302 del 15 de mayo de 2012 del Ministerio de Agricultura". 

- Sujetos obligados: Acopiador-Consignatario, Acopiador de maní, Acopiador de legumbres, Comprador de granos para consumo propio, Desmotadora de algodón, Industrial aceitero, Industrial biocombustibles, Industrial balanceador, Industrial cervecero, Industrial destilería, Industrial molinero, Industrial arrocero, Industrial molinero de harina de trigo, Industrial seleccionador, Acondicionador, Explotador de depósito y/o elevador de granos, Fraccionador de granos, Complejo industrial.
- Comprobantes alcanzados: Carta de Porte vinculada al transporte automotor o ferroviario de granos; Conocimiento de Embarque; Remito "R" o "X"
- Serán considerados como ingreso de granos a la planta de almacenaje a partir de la confirmación definitiva del Código de Trazabilidad de Granos "CTG" o cuando tenga lugar la obtención del "CODIGO DE TRAZABILIDAD DE GRANOS – FLETE CORTO" en el lugar de destino de la mercadería; a partir de su recepción vía utilización del servicio "REGISTRO SISTEMICO DE MOVIMIENTOS Y EXISTENCIAS DE GRANOS"
- El responsable deberá informar la recepción definitiva de los granos arribados al establecimiento en el servicio “CODIGO DE TRAZABILIDAD DE GRANOS - CTG”, opción “Confirmación Definitiva del CTG”, y suministrar la información sobre los kilogramos netos efectivamente ingresados. Asimismo, para suministrar dicha información se podrá utilizar el procedimiento de intercambio de información basado en el servicio "web", establecido por la Resolución General No 2.806 y su modificación. 

#### WSCTGv2

El 20/03/2014 AFIP publico la nueva descripción del servicio web WSCTGv2 (CTG Service v2.0) con los siguientes cambios:

- `SolicitarCTGInicial` tiene un nuevo parámetro `remitente_comercial_como_canjeador` y cambia `km_recorridos` a `km_a_recorrer`
- `ConfirmarArribo` agrega parametro `consumo_propio`
- `ConfirmarDefinitivo` agrega parametros `establecimiento``codigo_cosecha`, `peso_neto`
- `CambiarDestinoDestinatarioCTGRechazado` y `DesviarCTG` cambia `km_recorridos` a `km_a_recorrer`
- `ConsultarDetalleCTGDatos` agrega `detalle` y `remitente_comercial_como_canjeador` a la respuesta
- Nuevos métodos: `CTGsPendientesResolucion` que devuelve `ctg_rechazados`, `ctg_otorgados`, `ctg_confirmados`

~~Lamentablemente por el momento el nuevo webservice WSCTGv2 da error de AFIP: `Falla SOAP: soapenv:Server Error de acceso a la base de datos` y `soapenv:Server java.lang.RuntimeException: common.0015`~~ *al 1-4-2014, el servicio web esta operativo tanto en producción como homologación*

Si bien en principio no hay grandes cambios, pero como AFIP ha modificado la estructura interna, la versión anterior de la interface no funcionaría con la nueva URL devolviendo AFIP el siguiente error: `Falla SOAP: soapenv:Client org.apache.axis2.databinding.ADBException: Unexpected subelement datosSolicitarCTGInicial`

**NOTA:** no se han podido verificar completamente el funcionamiento ya que muchos métodos devolvían ERROR por parte de AFIP en homologación (por lo que se recomienda pruebas extensivas con datos propios). A su vez, se ha realizado una corrección interna ya que el WSDL publicado por AFIP tiene inconsistencias (kmARecorrer -> kmRecorridos en ConsultarDetalleCTG), por lo que posiblemente no es el definitivo y será actualizado por AFIP.

**IMPORTANTE:** el webservice anterior parece que deja de funcionar (WSCTGv1.1, al menos en homologación): devolviendo el siguiente error `Falla SOAP: soapenv:Server A partir del 01/04/2014 utilizar wsctg v2.0`

#### WSCTGv3

El 15/12/2014 AFIP publicó la nueva descripción del servicio web WSCTGv2 (CTG Service v2.3) donde al método Solicitar CTG Inicial 

- a `SolicitarCTGInicial` se le agregó 2 parametros opcionales: `cuit_corredor`y `remitente_comercial_como_productor`: S (SI) / N (NO)
- en `ConfirmarArribo` se hizo obligatorio el campo `cuit_chofer`

Notar que en la documentación técnica la URL de la descripción del servicio (WSDL) publicada es incorrecta, sería:

- Homologación: https://fwshomo.afip.gov.ar/wsctg/services/CTGService_v3.0?wsdl (usada por defecto para el instalador de evaluación)
- Producción: https://serviciosjava.afip.gob.ar/wsctg/services/CTGService_v3.0?wsdl

Estamos trabajando en ello, en cuanto este completamente operativo liberaremos la versión funcional para evaluación, consultar por [email](mailto:pyafipws+wsctg2@sistemasagiles.com.ar) en caso de estar interesado y necesitar [soporte comercial prioritario](http://www.sistemasagiles.com.ar/trac/wiki/PyAfipWs#CostosyCondiciones) (desde $750+IVA en caso de actualizaciones).

Descarga del instalador preliminar para homologación: [instalador-PyAfipWs-2.33a-32bit+wsaa_2.08a+wsctgv2_1.13a-homo.exe](http://www.sistemasagiles.com.ar/soft/pyafipws/instalador-PyAfipWs-2.33a-32bit+wsaa_2.08a+wsctgv2_1.13a-homo.exe) ([código fuente](https://code.google.com/p/pyafipws/source/browse/wsctgv2.py), ver historial de cambios para mayor información)

#### WSCTGv4

El 1/6/2017 AFIP publicó la nueva descripción del servicio web WSCTGv4 (CTG Service v4)  

- se agregó `turno` como parametro opcional a `SolicitarCTGInicial`, `SolicitarCTGDatoPendiente` y `CambiarDestinoDestinatarioCTGRechazado` 
- se agregó `ctc_codigo` y `turno` al `ConsultarCTG` (propiedades `CtcCodigo` y `Turno`)

Notar que en la documentación técnica la URL de la descripción del servicio (WSDL) publicada es incorrecta, sería:

- Homologación: https://fwshomo.afip.gov.ar/wsctg/services/CTGService_v4.0?wsdl (predeterminada en el instalador de evaluación)
- Producción: https://serviciosjava.afip.gob.ar/wsctg/services/CTGService_v4.0?wsdl


Descarga del instalador preliminar para homologación: [PyAfipWs-2.7.1958-32bit+wsaa_2.11c+wsctgv4_1.14a-homo.exe](https://www.sistemasagiles.com.ar/soft/pyafipws/PyAfipWs-2.7.1958-32bit+wsaa_2.11c+wsctgv4_1.14a-homo.exe) (ver historial de cambios para mayor información)

El 12/08/2020 AFIP publica nuevo ajuste:

- se agregó la posibilidad de informar dos dominios adicionales `opcionalPatenteUno` y `opcionalPatenteDos` como parámetros opcionales en `SolicitarCTGInicial`


## Descargas

- Instalador: [instalador-PyAfipWs-2.7.2246-32bit+wsaa_2.12c+wsctgv4_1.15e-homo.exe](https://www.sistemasagiles.com.ar/soft/pyafipws/PyAfipWs-2.7.2246-32bit+wsaa_2.12c+wsctgv4_1.15e-homo.exe) (versión WSCTGv4)
- Documentación: [Documento Oficial WSCTGv1.1](http://www.afip.gov.ar/cartaDePorte/documentos/Web%20Service%20CTGv1.1.pdf) [WSCTGv2.0](http://www.afip.gov.ar/cartaDePorte/documentos/WebServiceCTGv2.0.pdf)  [WSCTGv3.0](http://www.afip.gov.ar/ws/WSCTG/WebServiceCTG_v3.0.pdf)  [WSCTGv4.0](http://www.afip.gov.ar/ws/WSCTG/WebServiceCTG_v4.0.pdf) (AFIP), [Manual de Uso General](../documentacion_herramientas/manualpyafipws.md) ([PDF](http://www.sistemasagiles.com.ar/trac/wiki/ManualPyAfipWs?format=pdf))
- Ejemplo en VB: [wsctg.bas](https://github.com/reingart/pyafipws/blob/master/ejemplos/wsctgv2/wsctg.bas) *(actualizado)* [ejemplo_wstg.zip](http://code.google.com/p/pyafipws/downloads/detail?name=ejemplo_wsctg.zip&can=2&q=)
- Archivos de intercambio (muestras): [wsctg_dbf.zip](attachment:wsctg_dbf.zip), [entrada_wsctg.txt](attachment:entrada_wsctg.txt), [salida_wsctg.txt](attachment:salida_wsctg.txt), [entrada_wsctg.csv](attachment:entrada_wsctg.csv), [salida_wsctg.csv](attachment:salida_wsctg.csv), [wsctg.json](attachment:salida_wsctg.json)
- Código Fuente (Python): [wsctg.py](http://code.google.com/p/pyafipws/source/browse/wsctg.py) y [wsctg11.py](http://code.google.com/p/pyafipws/source/browse/wsctg11.py) *(actualizado)*

## Metodos

**Importante**: actualizado según [WSCTGv4](#wsctgv4):

- **`Conectar(cache=None, url="", proxy="")`**: en homologación no hace falta pasarle ningùn paràmetro. En producciòn, el segudo parametro es la WSDL.
- **`Dummy()`**: devuelve estado de servidores
- **`AnularCTG(carta_porte, ctg)`**: devuelve `CodigoOperacion`
- **`RechazarCTG(carta_porte, ctg, motivo)`**: devuelve `CodigoOperacion`
- **`SolicitarCTGInicial(numero_carta_de_porte, codigo_especie, cuit_canjeador, cuit_destino, cuit_destinatario, codigo_localidad_origen, codigo_localidad_destino, codigo_cosecha, peso_neto_carga, [cant_horas, patente_vehiculo, cuit_transportista, km_a_recorrer, remitente_comercial_como_canjeador,  cuit_corredor, remitente_comercial_como_productor, turno, patente_opcional_uno, patente_opcional_dos])`**: devueve `NumeroCTG`. Parámetro `remitente_comercial_como_canjeador` agregado en WSCTGv2, `cuit_corredor` y `remitente_comercial_como_productor` agregado en WSCTGv3 *(disponible a partir de la actualización 1.14a)*
- **`SolicitarCTGDatoPendiente(numero_carta_de_porte, cant_horas, patente_vehiculo, cuit_transportista, turno)`**: devuelve NumeroCTG (metodo opcional si no se envio vehiculo, cuit_transportisata y cant_horas en SolicitarCTGInicial) Importante: por ahora esta dando error en las pruebas
- **`ConfirmarArribo(numero_carta_de_porte, numero_ctg, cuit_transportista, peso_neto_carga, consumo_propio, establecimiento, cuit_chofer)`**: devuelve `CodigoTransaccion`. Parámetro `consumo_propio` (S/N) agregado en WSCTGv2 *(disponible a partir de la actualización 1.11a)*, `cuit_chofer` obligatorio a partir de WSCTGv3
- **`ConfirmarDefinitivo(numero_carta_de_porte, numero_CTG, [establecimiento, codigo_cosecha, peso_neto_carga])`**: Parámetros `establecimiento`, `codigo_cosecha`, `peso_neto_carga` agregados en WSCTGv2 *(disponible a partir de la actualización 1.11a)*
- **`ConsultarCTG([numero_carta_de_porte, numero_CTG, patente, cuit_solicitante, cuit_destino, fecha_emision_desde, fecha_emision_hasta])`**: fecha_emision_desde es obligatoria (formato dd/mm/yyyy)
- **`ConsultarDetalleCTG(numero_ctg)`**: Operación mostrar este detalle de la  solicitud de CTG seleccionada (incluyendo **`TarifaReferencia`**)
- **`LeerDatosCTG()`**: carga los datos de cada ctg consultado (uno por vez)
- **`ConsultarCTGExcel(numero_carta_de_porte, numero_ctg, patente, cuit_solicitante, cuit_destino, fecha_emision_desde, fecha_emision_hasta, archivo="planilla.xls"):`**: Consulta los CTG y genera una planilla -archivo y fecha_emision_desde son obligatorios- *(disponible a partir de la actualización 1.09a)*
- **`ConsultarConstanciaCTGPDF(numero_ctg, archivo="constancia.pdf")`**: Consulta la constancia para un CTG y genera una documento PDF *(disponible a partir de la actualización 1.09a)*
- **`CTGsPendientesResolucion()`**: Consulta de CTGs Otorgados, CTGs Rechazados y CTGs Confirmados a Resolver. Utilizar `LeerDatosCTG` con parámetros "arrayCTGsRechazadosAResolver", "arrayCTGsOtorgadosAResolver", "arrayCTGsConfirmadosAResolver". Método agregado en WSCTGv2 *(disponible a partir de la actualización 1.11a)*.
- **`ConsultarCTGRechazados()`**: Consulta de CTGs Rechazados (utilizar LeerDatoCTG para recorrer los valores devueltos: ctg, carta porte, fecha rechazo, destino, destinatario, observaciones). Método agregado en WSCTGv2 *(disponible a partir de la actualización 1.12a)*.
- **`ConsultarCTGActivosPorPatente(patente)`**: Consulta de CTGs Rechazados (utilizar LeerDatoCTG para recorrer los valores devueltos: numero CTG, carta porte, patente, peso neto, fecha emision, fecha vencimiento, usuario solicitante, usuario real). Método agregado en WSCTGv2 *(disponible a partir de la actualización 1.12a)*.
- **`RegresarAOrigenCTGRechazado(numero_carta_de_porte, numero_ctg, km_a_recorrer)`**: Al consultar los CTGs rechazados se puede Regresar a Origen. Método agregado en WSCTGv2 *(disponible a partir de la actualización 1.12a)*.
- **`CambiarDestinoDestinatarioCTGRechazado(umero_carta_de_porte, numero_ctg, codigo_localidad_destino, cuit_destino, cuit_destinatario, km_a_recorrer, turno)`**: Consulta de CTGs Rechazados. Método agregado en WSCTGv2 *(disponible a partir de la actualización 1.14a)*.

## Atributos

**Importante**: actualizado según [WSCTGv4](#wsctgv4):

- **`NumeroCTG`**
- **`CartaPorte`**
- **`FechaHora`**: completado por `SolicitarCTGInicial` y `LeerDatosCTG` (`ConsultarCTG`, `ConsultarCTGRechazados`, `ConsultarCTGActivosPorPatente`, etc).
- **`CodigoOperacion`**: completado por anular y rechazar
- **`CodigoTransaccion`**: completado por confirmar arribo / definitivo
- **`Observaciones`**: string, completado por `SolicitarCTGInicial`
- **`Controles`**: lista, completado por `SolicitarCTGInicial`
- **`VigenciaHasta, VigenciaDesde`**: completado por `SolicitarCTGInicial`
- **`Estado e ImprimeConstancia y DatosCTG`**: completado por `ConsultarCTG`/`LeerDatosCTG`
- **`TarifaReferencia`**: devuelto por `ConsultarDetalleCTG`
- **`Destino`**: devuelto por `ConsultarDetalleCTG` y `ConsultarCTGRechazados` agregados en WSCTGv2 *(disponible a partir de la actualización 1.11a)*
- **`Destinatario`**: devuelto por `ConsultarDetalleCTG` y `ConsultarCTGRechazados` agregados en WSCTGv2 *(disponible a partir de la actualización 1.11a)*
- **`Detalle`**: devuelto por `ConsultarDetalleCTG` y y `ConsultarCTGRechazados` agregados en WSCTGv2 *(disponible a partir de la actualización 1.11a)*
- **`Patente`**: devuelto por `ConsultarCTGActivosPorPatente` agregados en WSCTGv2 *(disponible a partir de la actualización 1.12a)*
- **`PesoNeto`**: devuelto por `ConsultarCTGActivosPorPatente` agregados en WSCTGv2 *(disponible a partir de la actualización 1.12a)*
- **`FechaVencimiento`**: devuelto por `ConsultarCTGActivosPorPatente` agregados en WSCTGv2 *(disponible a partir de la actualización 1.12a)*
- **`UsuarioSolicitante`**: devuelto por `ConsultarCTGActivosPorPatente` agregados en WSCTGv2 *(disponible a partir de la actualización 1.12a)*
- **`UsuarioReal`**: devuelto por `ConsultarCTGActivosPorPatente` agregados en WSCTGv2 *(disponible a partir de la actualización 1.12a)*
- **`CtcCodigo`**: devuelto por `ConsultarCTG` agregados en WSCTGv4 *(disponible a partir de la actualización 1.14a)*
- **`Turno`**: devuelto por `ConsultarCTG` agregados en WSCTGv4 *(disponible a partir de la actualización 1.14a)*

## Herramienta por consola

La interfaz presenta una herramienta universal (multiplataforma -linux / windows / mac- compatible con cualquier lenguaje de programación), que puede ser operado de manera automática en segundo plano (no requiere intervención del usuario).

El modo de uso es ejecutando el programa **`WSCTG_CLI.EXE`** con las siguientes opciones y archivos de intercambio.
La herramienta puede ser ejecutada interactivamente en una consola (Inicio, Ejecutar, CMD.EXE) o puede ser llamada desde otro programa o script .BAT

### Parámetros por línea de comando

La herramienta soporta las siguientes opciones principales:

- --dummy: consulta estado de servidores
- --solicitar: obtiene el CTG (según archivo de entrada en TXT o CSV)
- --confirmar: confirma el CTG (según archivo de entrada en TXT o CSV)
- --anular: anula el CTG
- --rechazar: permite al destino rechazar el CTG
- --confirmar_arribo: confirma el arribo de un CTG
- --confirmar_definitivo: confirma el arribo definitivo de un CTG
- --regresar_a_origen_rechazado: tomar la acción de "Regresar a Origen"
- --cambiar_destino_destinatario_rechazado: "Cambio de Destino y Destinatario"

Recuperación de datos:

- --consultar: consulta las CTG generadas
- --consultar_excel: consulta las CTG generadas (genera un excel)
- --consultar_detalle: obtiene el detalle de una CTG
- --consultar_constancia_pdf: descarga el documento PDF de una CTG
- --pendientes: consulta CTGs otorgados, rechazados, confirmados a resolver (WSCTGv2)
- --consultar_rechazados: obtener CTGs rechazados para darles un nuevo curso
- --consultar_activos_por_patente: consulta de CTGs activos por patente 

Tablas de referencias:

- --provincias: obtiene el listado de provincias
- --localidades: obtiene el listado de localidades por provincia
- --especies: obtiene el listado de especies
- --cosechas: obtiene el listado de cosechas

Parámetros auxiliares:

- --ayuda: este mensaje
- --debug: modo depuración (detalla y confirma las operaciones)
- --formato: muestra el formato de los archivos de entrada/salida
- --prueba: genera y autoriza una CTG de prueba (no usar en producción!)
- --xml: almacena los requerimientos y respuestas XML (depuración)

### Ejemplo

Generar un CTG de prueba (no usar en producción):

```
C:\PYAFIPWS\> WSCTG11_CLI.EXE --prueba --solicitar
solicitando... codigo_especie=23 tarifa_referencia=0.0 transaccion=10000001681 codigo_cosecha=910 observaciones= patente_vehiculo=CZO985 codigo_localidad_destino=3059 km_recorridos=1234 numero_carta_de_porte=512345679 estado= imprime_constancia= cuit_transportista=20234455967 establecimiento=1 cuit_destinatario=20267565393 codigo_localidad_origen=3058 tipo_reg=0 controles= fecha_hora= errores= cuit_destino=20061341677 numero_ctg=43816783 vigencia_desde= vigencia_hasta= peso_neto_carga=1000 cuit_canjeador=0 cant_horas=1
numero CTG:  93664014
Observiacion:  CTG otorgado exitosamente
Carta Porte 512345679
Numero CTG 93664014
Fecha y Hora 30/05/2013 16:02:23
Vigencia Desde 30/05/2013
Vigencia Hasta 04/06/2013
Tarifa Referencia:  396.51
Errores: []
Controles: []
hecho.
```

### Archivo de Configuración

Para utilizar este webservice, debe tramitarse un certificado. Ver [Instructivo](../documentacion_herramientas/manualpyafipws.md#certificados)

Luego, se debe configurar el Certificado, clave privada y URL en el archivo de configuración WSCTG.INI:

```
[WSAA]
CERT=reingart.crt
PRIVATEKEY=reingart.key
#URL=https://wsaa.afip.gov.ar/ws/services/LoginCms

[WSCTG]
CUIT=20267565393
ENTRADA=entrada_wsctg.txt
SALIDA=salida_wsctg.txt
#URL=https://cereales.afip.gov.ar/wsctg/services/CTGService_v1.1?wsdl
```

Para producción, se debe usar un instalador para tal fin y descomentar la URL (eliminando el numeral). 

El tipo de archivo de intercambio depende de la extensión configurada en WSCTG (usar .txt para texto, .csv para planillas CSV, .dbf para tablas DBF y .json para JavaScript)
## Archivo de Intercambio

La herramienta por consola soporta tanto:

- archivos de texto de ancho fijo (similares al usado por SIAP -COBOL-): ver [y [attachment:salida_wsctg.txt](attachment:entrada_wsctg.txt]) (muestras ejemplo)
- planillas CSV (archivo de texto valores separados por coma): ver [y [attachment:salida_wsctg.csv](attachment:entrada_wsctg.csv]) (muestras ejemplo WSCTGv1.1)
- tablas DBF (dBase, !FoxPro, Clipper, etc.): ver [wsctg_dbf.zip](attachment:wsctg_dbf.zip) (tablas de muestra WSCTGv1.1)
- archivo JSON (notación de objetos !JavaScript): : ver [attachment:salida_wsctg.json] (muestras ejemplo WSCTGv1.1)

Formato de los campos del archivo de texto es el siguiente (el nombre de los campos es el mismo para todos los formatos, salvo para tablas DBF que están limitadas a 8 caracteres):

### Encabezado

**Importante**: actualizado según [WSCTGv2](#wsctgv2) y [WSCTGv3](#wsctgv3):

- Campo: tipo_reg             Posición:   1 Longitud:    1 Tipo: Alfanumerico 
- Campo: numero_carta_de_porte Posición:   2 Longitud:   13 Tipo: Numerico 
- Campo: codigo_especie       Posición:  15 Longitud:    5 Tipo: Numerico 
- Campo: cuit_canjeador       Posición:  20 Longitud:   11 Tipo: Numerico 
- Campo: cuit_destino         Posición:  31 Longitud:   11 Tipo: Numerico 
- Campo: cuit_destinatario    Posición:  42 Longitud:   11 Tipo: Numerico 
- Campo: codigo_localidad_origen Posición:  53 Longitud:    6 Tipo: Numerico 
- Campo: codigo_localidad_destino Posición:  59 Longitud:    6 Tipo: Numerico 
- Campo: codigo_cosecha       Posición:  65 Longitud:    4 Tipo: Numerico 
- Campo: peso_neto_carga      Posición:  69 Longitud:    5 Tipo: Numerico 
- Campo: cant_horas           Posición:  74 Longitud:    2 Tipo: Numerico 
- Campo: patente_vehiculo     Posición:  76 Longitud:    6 Tipo: Alfanumerico (usar campo al final para más digitos) 
- Campo: cuit_transportista   Posición:  82 Longitud:   11 Tipo: Numerico  
- Campo: km_a_recorrer        Posición:  93 Longitud:    4 Tipo: Numerico  (km_recorridos en consulta WSCTGv2)
- Campo: establecimiento      Posición:  97 Longitud:    6 Tipo: Numerico  
- Campo: remitente_comercial_como_canjeador Posición: 103 Longitud:    1 Tipo: Alfanumerico (S/N solicitar CTG inicial WSCTGv2))
- Campo: consumo_propio       Posición: 104 Longitud:    1 Tipo: Alfanumerico  (S/N confirmar arribo WSCTGv2)
- Campo: numero_ctg           Posición: 105 Longitud:    8 Tipo: Numerico  
- Campo: fecha_hora           Posición: 113 Longitud:   19 Tipo: Alfanumerico  
- Campo: vigencia_desde       Posición: 132 Longitud:   10 Tipo: Alfanumerico  
- Campo: vigencia_hasta       Posición: 142 Longitud:   10 Tipo: Alfanumerico  
- Campo: transaccion          Posición: 152 Longitud:   12 Tipo: Numerico 
- Campo: tarifa_referencia    Posición: 164 Longitud:    6 Tipo: Importe Decimales: 2
- Campo: estado               Posición: 170 Longitud:   20 Tipo: Alfanumerico 
- Campo: imprime_constancia   Posición: 190 Longitud:    5 Tipo: Alfanumerico
- Campo: observaciones        Posición: 195 Longitud:  200 Tipo: Alfanumerico
- Campo: errores              Posición: 395 Longitud: 1000 Tipo: Alfanumerico
- Campo: controles            Posición: 1395 Longitud: 1000 Tipo: Alfanumerico
- Campo: detalle              Posición: 2395 Longitud: 1000 Tipo: Alfanumerico (consultar detalle WSCTGv2)
- Campo: cuit_chofer          Posición: 3395 Longitud:   11 Tipo: Numerico (agregado WSCTGv2)
- Campo: cuit_corredor        Posición: 3406 Longitud:   12 Tipo: Numerico (agregado WSCTGv3)
- Campo: remitente_comercial_como_productor Posición: 3418 Longitud:    1 Tipo: Alfanumerico (agregado WSCTGv3)
- Campo: patente_vehiculo     Posición: 3419 Longitud:   10 Tipo: Alfanumerico 

## Ejemplo Intefase COM en VB (5/6)

Ver ejemplo completo para Visual Basic o similar en: [wsctg.bas](https://github.com/reingart/pyafipws/blob/master/ejemplos/wsctgv2/wsctg.bas) (adaptable a otros lenguajes como Visual Fox Pro, Delphi, etc. -ver otros webservices o consultar-)

```
#!vb

numero_carta_de_porte = "512345678"
codigo_especie = 23
cuit_remitente_comercial = "20267565393"
cuit_destino = "20267565393"
cuit_destinatario = "20267565393"
codigo_localidad_origen = 3058
codigo_localidad_destino = 3059
codigo_cosecha = "0910"
peso_neto_carga = 1000
cant_horas = 1
patente_vehiculo = "AAA000"
cuit_transportista = "2026756539"
   
numero_CTG = WSCTG.SolicitarCTG(numero_carta_de_porte, codigo_especie, _
    cuit_remitente_comercial, cuit_destino, cuit_destinatario, codigo_localidad_origen, _
    codigo_localidad_destino, codigo_cosecha, peso_neto_carga, cant_horas, _
    patente_vehiculo, cuit_transportista)
     
MsgBox numero_CTG, vbInformation, "SolicitarCTG: número CTG:"

numero_CTG = "43816783"
transaccion = WSCTG.ConfirmarCTG(numero_carta_de_porte, numero_CTG, cuit_transportista, peso_neto_carga)
   
MsgBox WSCTG.Observaciones, vbInformation, "ConfirmarCTG: código transaccion:" & WSCTG.CodigoTransaccion

```
## Constancia PDF y Planilla Excel

La interfaz permite obtener los archivos que devuelve AFIP mediante este webservice:
 
- [attachment:constancia_ctg.pdf]: Constancia CTG en documento PDF (ver método `ConsultarConstanciaCTGPDF` u opción `--consultar_constancia_pdf`)
- [attachment:planilla_ctg.xls]: Consulta de CTG en planilla Excel (ver método `ConsultarCTGExcel` u opción `--consular_excel`)

En ambos casos, AFIP devuelve el archivo binario ya generado, por lo que se debe especificar una ruta completa para almacenarlo.
Necesita Acrobat Reader, Microsoft Office / Libre Office o similares para poder abrir los documentos.
## Tablas de Parámetros

En este nuevo servicio web WSCTGv1.1 utiliza tablas dinámicas para los siguientes datos:

- Provincias
- Localidades
- Especies
- Cosechas

La interfaz permite obtener los diversos códigos de parámetros a utilizar. A continuación se detallan a modo de ejemplo:

### Especies

| Código | Descripción |
|---|---|
| 1 | Lino |
| 2 | Girasol |
| 3 | Mani en caja |
| 4 | Girasol Descascarado |
| 5 | Mani para industria de seleccion |
| 6 | Mani para industria aceitera |
| 7 | Mani tipo confiteria |
| 8 | Colza |
| 9 | Colza "00" / Canola |
| 10 | Trigo Forrajero |
| 11 | Cebada Forrajera |
| 12 | Cebada apta para Malteria |
| 14 | Trigo Candeal |
| 15 | Trigo Pan |
| 16 | Avena |
| 17 | Cebada Cervecera |
| 18 | Centeno |
| 19 | Maiz |
| 20 | Mijo |
| 21 | Arroz Cascara |
| 22 | Sorgo Granifero |
| 23 | Soja |
| 24 | Trigo Blando |
| 25 | Trigo Plata |
| 26 | Maiz Flynt o Plata |
| 27 | Maiz Pisingallo |
| 28 | Triticale |
| 30 | Alpiste |
| 31 | Algodon |
| 32 | Cartamo |
| 33 | Poroto Blanco Natural Oval y Alubia |
| 34 | Poroto Distinto del Blanco Oval y Alubia |
| 35 | Arroz |
| 46 | Lenteja |
| 47 | Arveja |
| 48 | Poroto Blanco Seleccionado Oval y Alubia |
| 49 | Otras Legumbres |
| 50 | Otros Granos |
| 59 | Garbanzo |

### Cosechas

| Código | Descripción |
|---|---|
| 0910 | 09-10 |
| 0809 | 08-09 |
| 0708 | 07-08 |

### Provincias

| Código | Descripción |
|---|---|
| 0 | CIUDAD AUTÓNOMA DE BUENOS AIRES |
| 1 | BUENOS AIRES |
| 2 | CATAMARCA |
| 3 | CORDOBA |
| 4 | CORRIENTES |
| 5 | ENTRE RIOS |
| 6 | JUJUY |
| 7 | MENDOZA |
| 8 | LA RIOJA |
| 9 | SALTA |
| 10 | SAN JUAN |
| 11 | SAN LUIS |
| 12 | SANTA FE |
| 13 | SANTIAGO DEL ESTERO |
| 14 | TUCUMAN |
| 16 | CHACO |
| 17 | CHUBUT |
| 18 | FORMOSA |
| 19 | MISIONES |
| 20 | NEUQUEN |
| 21 | LA PAMPA |
| 22 | RIO NEGRO |
| 23 | SANTA CRUZ |
| 24 | TIERRA DEL FUEGO |

### Localidades

Las localidades dependen de la provincia, por ej. algunas localidades para Tierra del Fuego:

| Código | Descripción |
|---|---|
| 899 | ASERRADERO ARROYO |
| 985 | BAHIA LAPATAIA |
| 1345 | BASE AEREA TENIENTE MATIENZO |
| 1350 | BASE EJERCITO ESPERANZA |
| 1638 | CABANA RUBY |
| 1659 | CABO SAN PABLO |
| 1813 | CAMPAMENTO CENTRAL Y P F |
| 3997 | COMISARIA RADMAN |
| 4416 | DESTACAMENTO MELCHIOR |
| 5181 | EL PARAMO |
| 5679 | ESTACION AERONAVAL |
| 5694 | ESTACION CIENTIFICA ALTE BROWN |
| 7026 | ISLA DE LOS ESTADOS |
| 7038 | ISLA GRAN MALVINA |
| 7042 | ISLA JOINVILLE |
| 7058 | ISLA SHETLAND DEL SUR |
| 7060 | ISLA SOLEDAD |
| 7069 | ISLAS GEORGIAS |
| 7070 | ISLAS ORCADAS |
| 13928 | TOLHUIN |
| 14214 | USHUAIA |
| 18510 | RIO GRANDE |
| 18911 | SAN SEBASTIAN |
| 18992 | SANTA INES |

## Novedades

Historial de Cambios:

- Junio 2016 (actualizacion 1.14): ajuste por [WSCTGv4](#wsctgv4)
- Diciembre 2014 (actualización 1.13): ajuste por [WSCTGv3](#wsctgv3)
- Marzo 2014 (actualización 1.11): ajustes por [WSCTGv2](#wsctgv2) RG3593/14
- Mayo 2013 (actualización 1.09): se agrega soporte para constancia en PDF, planilla en Excel y archivos de intercambio (texto, json, dbf)
- Abril 2013  (actualización 1.08): ajustes menores en consultar detalle
- Marzo 2013  (actualización 1.07): ajustes en leer dato ctg
- Febrero 2013  (actualización 1.06):: ajustes cuit_canjeador
- Abril 2012  (actualización 1.04 - 1.06): ajustes iniciales para Version 1.1 (solicitar CTG inicial)

Se recuerda que esta disponible el 
[grupo de noticias](http://groups.google.com.ar/group/pyafipws) donde
se publicarán futuras novedades sobre PyAfipWS: servicios web de
factura electrónica y sus interfases (se recomienda suscribirse)

## Costos y Condiciones

(ver [Condiciones del Soporte Comercial](../documentacion_herramientas/pyafipws.md#costos-y-condiciones)).

Para WSCTGv3, como en otros casos, dado que es un nuevo webservice, ofrecemos soporte comercial por la actualización (desde $5.540 + IVA por hasta 2 hs en un mes de cobertura) para los clientes previos que hayan contratado soporte para WSCTGv2 o WSCTGv1.1.

A su vez, se liberará el código fuente bajo licencia GPL (software libre), al igual que se hizo con el restos de los servicios web. Para más detalles ver página FacturaElectronica.

MarianoReingart