# Proyecto Factura Electrónica Versión 1 a 2.6 (RG2485, RG2904, RG2757, RG3067, RG3571, RG3668 RG3749, RG4109-E, RG4367-4291, RG5614-5616)

Interfaz para Servicio Web correspondiente a Factura Electrónica de Mercado Interno para el régimen especial [RG 2485/08](http://www.infoleg.gov.ar/infolegInternet/anexos/140000-144999/144058/norma.htm), previstos originalmente en la RG 2757/2010, modificada por RG 2904/2010, sus modificatorias y complementarias. [RG 3067/2011](http://infoleg.mecon.gov.ar/infolegInternet/anexos/180000-184999/180613/norma.htm):  Régimen Simplificado para Pequeños Contribuyentes (RS - Monotributo). Régimen especial de emisión y almacenamiento electrónico de comprobantes originales. [RG 3571/2013](http://www.infoleg.gob.ar/infolegInternet/anexos/220000-224999/224058/norma.htm): Responsables inscriptos en IVA nuevas actividades y sujetos alcanzados. [RG 3668/2014](http://www.afip.gob.ar/genericos/novedades/RG3668.asp): Factura A IVA F.8001 (restaurant, bares, gastronomía, hotelería, garajes, etc.) [RG 3749/2015](http://www.infoleg.gob.ar/infolegInternet/anexos/240000-244999/244572/norma.htm):  Responsables inscriptos y sujetos exentos en el impuesto al valor agregado. 
RG 4004-E Alquiler de inmuebles con destino casa habitación. [RG 4109-E/2017](http://afip.gov.ar/noticias/20170824mueblesRegistrables.asp): Venta de bienes muebles registrables. [RG4367/ 2018](http://www.afip.gov.ar/noticias/20181220-regimenFacturaCreditoElectronica.asp): [Factura de Crédito Electrónica MiPymes](#importante-rg43672018-fev213). [RG4540/2019](https://www.boletinoficial.gob.ar/detalleAviso/primera/212546/20190801) Condiciones de Emisión de notas de crédito y/o débito.

La administración Federal de Ingresos Públicos informa que, en el corto plazo las solicitudes de emisión de comprobantes electrónicos de Clase "A" emitidas para CUITs que resultan inválidos, inexistentes o no corresponden a responsables inscriptos en el Impuesto al Valor Agregado, serán rechazadas. En caso que la solicitud se esté efectuando por lote, se deberán reprocesar los registros de los comprobantes siguientes al rechazado en virtud de que se verá alterada la correlatividad y consecutividad de la numeración de los mismos.

## Descripción General

EL WSFEv1 (Web Service de Factura Electrónica Versión 1) es un nuevo Servicio Web de la AFIP para el 
*Régimen especial para la emisión y almacenamiento electrónico de comprobantes originales que respalden las operaciones de compraventa de cosas muebles, locaciones y prestaciones de servicios, locaciones de cosas y de obras y de las señas o anticipos que congelen precios, efectuadas en el mercado interno.* (RG2485), correspondiente a la 
Resolución [Resolución General 2904/2010](http://www.afip.gov.ar/fe/#rg) Art.4 Opción B, próxima a entrar en vigencia:

- 27 de Octubre de 2010: Autoimpresores - CAE Anticipado RG2926
- 1 de Noviembre de 2010: Sujetos notificados RG2904
- 1 de Abril de 2011: Importadores RG2975 (opcional a partir de 1 de Enero de 2011)
- 1 de Julio de 2011: Obligatorio para todas las actividades y sujetos comprendidos en la RG2845 (reemplaza WSFE versión 0)

**NOTA:** La notificación es mediante nota cursada por Juez Administrativo (RG2904)

Este nuevo webservice contempla las operaciones de mercado interno (Facturas A y B) y CAE Anticipado.

**NOTA**: Ver [WSMTXCA](wsmtxca.md) (webservice v0, Opción A).

## Estado

La AFIP publicó la [información técnica](http://www.afip.gov.ar/fe/documentos/manual_desarrollador_COMPG_v1.pdf), el servicio WSFEv1 está disponible en homologación para realizar pruebas.

En su momento hemos desarrollado para nuestros clientes, un **SIMULADOR** que emula los métodos del servicio web, para poder comenzar los desarrollos:

- https://www.sistemasagiles.com.ar/simulador/

Para esta interfaz, hemos desarrollado nuevas bibliotecas de [Cliente/Servidor SOAP](http://code.google.com/p/pysimplesoap/) y manejo de XML mejorado, mejorando la versión anterior, lo que permitirá mayor flexibilidad, depuración y control de errores.
Por este motivo, la interfaz se instalará de forma separada, para evitar inconvenientes, manteniendo la simplicidad y modo de uso actual.

### Importante: RG3571/2013 AFIP

Esta interfaz ya contempla la  [Resolución General 3571/2013](http://www.afip.gov.ar/genericos/novedades/rg3571.asp) que suma nuevos sujetos obligados al régimen de factura electrónica.

#### Nuevas actividades alcanzadas

- GRUPO 1 (construcción): 1 de abril de 2014, inclusive
- GRUPO 2 (alquileres y servicios inmoviliarios): 1 de mayo de 2014, inclusive
- GRUPO 3 (alquileres de bienes muebles: automóviles, vehiculos, transportes, maquinarias, etc.): 1 de junio de 2014, inclusive
- GRUPO 4 (investigación y desarrollo experimental): 1 de julio de 2014, inclusive
- GRUPO 5 (reparación y mantenimiento de maquinarias, servicios profesionales, informática y datos, etc.): 1 de agosto de 2014, inclusive
- GRUPO 6 (división grandes contribuyentes): 1 de agosto de 2014, inclusive

#### Prestadores de Servicios Públicos

Los prestadores de gas natural, energía eléctrica, provisión de agua potable y desagües cloacales deberán usar el comprobante "Liquidación de Servicios Públicos" (incluyendo  Número de CESP – Código Electrónico de Servicios Públicos, precedido de la sigla "CESP Nº", informando consumo kW/m3 y categoría tarifaria), para los comprobantes que se emitan a partir del día 1 de abril de 2014, inclusive, pudiendo los sujetos obligados optar por adherir al régimen a partir del día 1 de marzo de 2014
A su vez, deberán utilizar el aplicativo denominado "AFIP – RENDICIÓN COMPROBANTES DE SERVICIOS PÚBLICOS – Versión 1.0", dado que están obligados a informar respecto de cada punto de venta habilitado, las operaciones diarias realizadas con los C.E.S.P. otorgados, así como los tramitados y no utilizados.
### Importante: RG3668/2014 AFIP

La [Resolución General 3668/2014](http://www.afip.gob.ar/genericos/novedades/RG3668.asp) suma nuevos sujetos alcanzados al régimen de factura electrónica: bares, restaurantes, hoteles, estacionamientos, etc. (relacionadas con las modificaciónes a la ley de IVA: "presunción de no vinculación con la actividad gravada" según Ley N° 24.475 y cambios a la RG 1415).

Si bien la interfaz ya contempla la especificación “RG 2485 Diseño de Registro XML V.2“ / “RG 2485 Manual para el Desarrollador V.2“ para emitir facturas electrónicas, se deberá consignar en los campos que se identifican como “Adicionales por R.G.”, la información que se indica en el Artículo 8 de la norma (datos de la declaración jurada [Form. 8001](http://www.afip.gov.ar/genericos/formularios/archivos/pdf/f8001.pdf)):

 a. Código de Identificación “5” - Dato 01 (Locador/Prestador del mismo), Dato 02 (Conferencias/congresos/convenciones/eventos similares), Dato 03 (Operaciones contempladas en la Resolución General Nº 74), Dato 04 (Bienes de cambio), Dato 05 (Ropa de utilización exclusiva en lugares de trabajo), Dato 06 (Intermediario). La codificación de los datos formará parte de las tablas del sistema.
 b. Código de Identificación “6.1” - Dato a ingresar: Tipo de Documento
 c. Código de Identificación “6.2” - Dato a informar: Número de documento.
 d. Código de Identificación “7” - Dato 01 (Titular), Dato 02 (Director/Presidente), Dato 03 (Apoderado), Dato 04 (Empleado). La codificación de los datos formará parte de las tablas del sistema.

*Importante*: La codificación de los datos  habilitada en las [tablas de parametros](#tablas-de-parametros) del webservice de AFIP, debiendo utilizar el nuevo tipo de registro: "Dato Opcional", correspondiente a nuevo método `AgregarDatoOpcional(id, valor)`. Para más información y ejemplos ver [Datos Opcionales AFIP WSFEv1](../documentacion_herramientas/manualpyafipws.md#datos-opcionales-afip-wsfev1).

En caso de optar por emitir comprobantes electrónicos originales, no sería necesario utilizar el nuevo Régimen Informativo de Comprobantes clase "A".

*Vigencia*: a partir del día 09 de septiembre de 2014 y resultarán de aplicación respecto de las operaciones que se efectúen a partir del día 1 de noviembre de 2014. 

AFIP ha publicado el 22 de Octubre [RG 2485 - Manual para el desarrollador V.2.4](http://www.afip.gov.ar/fe/documentos/manual_desarrollador_COMPG_v2_4.pdf)  que contempla las alícuotas de IVA incorporadas por la ley 26982 y contiene todas las funcionalidades de la versión 2 más la posibilidad de autorizar los comprobantes con las disposiciones de la RG 3668.

### Importante: RG3749/2015 AFIP

La [Resolución General 3749/2015](http://www.infoleg.gob.ar/infolegInternet/anexos/240000-244999/244572/norma.htm) suma nuevos sujetos alcanzados al régimen de factura electrónica: Los sujetos que revistan el carácter de responsables inscriptos en el impuesto al valor agregado deberán emitir comprobantes electrónicos originales, en los términos de la Resolución General N° 2.485, sus modificatorias y complementarias, para respaldar todas sus operaciones realizadas en el mercado interno. Comprobantes alcanzados:

- Facturas y recibos clase “A”, “A” con la leyenda “PAGO EN C.B.U. INFORMADA” y/o “M”, de corresponder.
- Notas de crédito y notas de débito clase “A”, “A” con la leyenda “PAGO EN C.B.U. INFORMADA” y/o “M”, de corresponder.
- Facturas y recibos clase “B”.
- Notas de crédito y notas de débito clase “B”.

Los sujetos que revistan la calidad de exentos frente al impuesto al valor agregado podrán ejercer la opción de emitir comprobantes electrónicos originales en los términos de la Resolución General N° 2.485, sus modificatorias y complementarias. De ejercer dicha opción, quedarán obligados a emitir los documentos electrónicos alcanzados por el presente título para respaldar todas las operaciones realizadas en el mercado interno. Comprobantes alcanzados:

- Facturas clase “C”.
- Notas de crédito y notas de débito clase “C”.
- Recibos clase “C”.


Adicionalmente, se establecen nuevos sujetos específicos alcanzados:

- Empresas prestadoras de servicios de medicina prepaga (RG 3270)
- Galerías de arte, comercializadores y/o intermediarios de obras de arte (RG 3730)
- Establecimientos de educación pública de gestión privada incorporados al sistema educativo nacional en los niveles educación inicial, educación primaria y educación secundaria (RG 3368)
- Personas físicas, sucesiones indivisas y demás sujetos que resulten locadores de inmuebles rurales (RG 2820)
- Sujetos que administren, gestionen, intermedien o actúen como oferentes de locación temporaria de inmuebles de terceros con fines turísticos o titulares de inmuebles que efectúen contratos de locación temporaria de dichos inmuebles con fines turísticos (RG 3687)

*Importante*: Los sujetos que se encuentren utilizando una versión anterior (WSFE), deberán adecuar sus sistemas a fin de cumplir con la última actualización prevista (WSFEv1): “RG 2485 Diseño de Registro XML V.2” (soportada por las últimas actualizaciones de nuestra herramienta, ya que se podría requerir datos opcionales). 

Datos Adicionales por RG (Se deberán emitir los comprobantes electrónicos en forma separada por actividad comprendida o no comprendida dentro del Régimen de Información pertinente):

 1. Establecimientos de educación pública de gestión privada

- Actividades no comprendidas: Código de identificación “10” - Dato “0” - cero.
- Actividades comprendidas Código de identificación “10” - Dato “1” - uno.
- Código de Identificación “10.11” - Dato a ingresar: Tipo de Documento (titular del pago)
- Código de Identificación “10.12” - Dato a informar: Número de Documento (titular del pago)

 2. Operaciones económicas vinculadas con bienes inmuebles

- Actividades no comprendidas: Código de identificación “11” - Dato “0” - cero.
- Actividades comprendidas: Código de identificación “11” - Dato “1” - uno.

 3. Locación temporaria de inmuebles con fines turísticos

- Actividades no comprendidas: Código de identificación “12” - Dato “0” - cero.
- Actividades comprendidas: Código de identificación “12” - Dato “1” - uno.

*Vigencia*: 1 de julio de 2015 (responsables inscriptos y actividades especiales), 1 de abril de 2015 (exentos)

### Importante: RG3779/2015 AFIP

La [Resolución General 3779/2015](http://infoleg.mecon.gov.ar/infolegInternet/anexos/245000-249999/247990/norma.htm) suma nuevos sujetos alcanzados al régimen de factura electrónica: 

- Operaciones del Mercado Lácteo, sus productos y subproductos por el Art. 4 de la Res. Conjunta 739/11 y 495/11 de los MAGyP y MEyFP respectivamente, por las que se emita el comprobante "Liquidación Mensual Única - Comercial Impositiva". RG 3187/11.
- Operaciones de Acopiadores, intermediarios o industrias que adquieran y/o reciban tabaco sin acondicionar, tanto productores y/u otros acopios o que adquieran, reciban y/o acopien tabaco acondicionado sin despalilla; o lámina, palo y/o "scrap", por las que se emita el "Comprobante de Compra Primaria del Sector Tabacalero". RG 3382/12.

Adicionalmente, se establecen nuevos sujetos específicos alcanzados:

- Representantes de Modelos (tengan o no contrato de representación)
- Agencias de Publicidad, Modelos, de Promociones, Productoras y similares
- Personas físicas que desarrollen actividad de modelaje (RG 2863 Art 1)

Datos Adicionales por RG (Se deberán emitir los comprobantes electrónicos en forma separada por actividad comprendida o no comprendida dentro del Régimen de Información pertinente):

 1. Representantes de Modelos (Resolución General N° 2.863)

- Actividades no comprendidas: Código de identificación “13” - Dato “0”.
- Actividades comprendidas Código de identificación “13” - Dato “1”.

 2. Agencias de publicidad (Resolución General N° 2.863)

- Actividades no comprendidas: Código de identificación “14” - Dato “0”.
- Actividades comprendidas Código de identificación “14” - Dato “1”.

 3. Personas físicas que desarrollen actividad de modelaje (Artículo 1° Resolución General N° 2.863)

- Actividades no comprendidas: Código de identificación “15” - Dato “0”.

*Vigencia*: 1° de enero de 2016 (según [preguntas frecuentes AFIP](http://www.afip.gob.ar/genericos/guiavirtual/consultas_detalle.aspx?id=19333567))

### Importante: COMPGv2.8

Las últimas semanas de Agosto de 2016 AFIP está informando los siguientes eventos en Homologación:

- 3: Se informa que se encuentra disponible en modo testing la version 2.8 del ws wsfev1 en el ambiente http://wswhomo.afip.gov.ar/wsfev1/service.asmx. El manual del desarrollador se encuentra en http://www.afip.gob.ar/fe/documentos/manualdesarrolladorCOMPGv28.pdf. Los cambios impactaran en produccion a partir del dia 01/09/2016.
- 4: IMPORTANTE: El 01/11/2016 se renovarán los certificados SSL utilizados por los webservices de AFIP. Los nuevos certificados utilizarán el algoritmo de encriptación SHA-256. Para más información http://www.afip.gob.ar/ws/comoAfectaElCambio.asp

Dado que todavía no se puede descargar el PDF que indica el mensaje de "evento" de AFIP, aparentemente no se encuentran hay cambios significativos según el WSDL publicado en homologación por AFIP.

**Solo se agregarían Observaciones a la solicitud de CAEA**.

Si bien estas cuestiones no deberían causar incidencias al utilizar este proyecto (siempre que se utilice versiones actualizadas), se recomienda probar estas cuestiones en homologación antes que sean aplicadas en producción.

Para más información y evaluación de las nuevas características, ver publicación en el repositorio: https://github.com/reingart/pyafipws/releases/tag/2.7.1856

Este release incluye además todas las actualizaciones acumuladas y nuevas funcionalidades/mejoras:[solicitud de múltiples comprobantes CAE](../documentacion_herramientas/manualpyafipws.md#metodos-alternativos-para-solicitud-de-multiples-cae), [obtención de campos](../documentacion_herramientas/manualpyafipws.md#metodos-basicos-de-wsfev1), [Tabla de parámetros de Paises](#tipos-de-paises), etc.

*Vigencia*: 1° de Septiembre de 2016

### Importante: FEv2.9

AFIP publicó una nueva [Especificación Técnica "FEv2.9"](http://www.afip.gov.ar/fe/documentos/manual_desarrollador_COMPG_v2_9.pdf) (manual para desarrolladores) con fecha 13 de Marzo de 2017 AFIP, con las siguientes novedades:

- Nuevo campo Cuit en Comprobantes Asociados (especialmente para tipos de comprobante 88 y 911)
- 88 – Remito de Tabaco Acondicionado 
- 991 – Remito de Tabaco en Hebras
- Nuevos [tipos de datos opcionales](#tipos-de-datos-opcionales) RG 4004-E Alquiler de inmuebles con destino casa habitación (Impuesto a las Ganancias)
- Id: 17, valor 1 (facturación vía intermediario) o 2 (facturación directa)
- Id: 1801 (CUIT) y 1802 (Denominación) en caso de ser necesario informar titular o cotitular

Los ajustes ya han sido realizados al componente, disponibles por actualización a partir de `WSFEv1.Version >= 1.19a` (revisión 1940 o superior del instalador), igualmente recomendamos probarlo y evaluarlo en homologación (Ver [Descargas](#descargas)), para ver como evoluciona desde AFIP.

Recordamos que si no son necesarias las nuevas características, no es obligatorio actualizar y re-instalar el componente. 
Provisoriamente puede limpiarse la carpeta cache de archivos temporales, para que se regeneren y pueda continuar operando.

Para más información ver [Service Pack 2](wiki:ActualizacionesFacturaElectronica#ServicePack2) y documentación [método WSFEv1 AgregarCmpAsoc](../documentacion_herramientas/manualpyafipws.md#metodos-basicos-de-wsfev1) en el manual

### Importante: RG4109-E/2017 AFIP COMPG_v2_10

La [Resolución General RG4109-E/2017](http://afip.gov.ar/noticias/20170824mueblesRegistrables.asp) implementa un nuevo procedimiento para la facturación de bienes muebles registrables. (modificando la RG 1415 y 2485).

- Se agrega esctructura de Compradores para dar soporte a receptores múltiples. Por cada Comprador se debe consignar:
- doc_tipo: int (string 2)
- doc_nro: long (string 80)
- porcentaje: double (float 2+2)
 
- Se agrega en el manual la validación correspondiente al código 10119 (cotización de moneda) y 10070 (si neto > 0, informar IVA).
- Se da de alta el código 11002 (el punto de venta debe ser uno habilitado en AFIP).
- Se agrega la validación 10151 para cuando envia cuit en comprobantes asociados.
- Se agrega la validación 1432 con el fin de limitar el ingreso de compradores múltiples por régimen informativo de CAEA.

AFIP ha publicado con fecha del 9 de Agosto [RG 2485 – Proyecto FE v2.10](http://www.afip.gob.ar/fe/documentos/manual_desarrollador_COMPG_v2_10.pdf)  que contempla la nueva estructura "Compradores" y contiene todas las funcionalidades de la versión 2 más la posibilidad de autorizar los comprobantes con las disposiciones de la RG 4109-E.

Para utilizar esta funcionalidad, la actualización incluye 1.20a (ver [Descargas](#descargas)) un nuevo método `WSFEv1.AgregarComprador(doc_tipo, doc_nro, porcentaje)` (componente) y tipo de registro 7 / tabla compradores.dbf para RECE1 (herramienta por archivo de intercambio). Para más información ver [Historial de Cambios](../documentacion_herramientas/manualpyafipws.md#historial-de-cambios)

Mensaje Evento AFIP: *5: MPORTANTE: El 29/08/2017 se actualizara el wsdl agregando una estructura opcional para compradores multiples segun RG 4109-E. Para mas informacion historial 2.10 del manual http://www.afip.gob.ar/fe/documentos/manual_desarrollador_COMPG_v2_10.pdf*

### Importante: RG4367/2018 FEv2.13

La [RG4367/ 2018](http://www.afip.gov.ar/noticias/20181220-regimenFacturaCreditoElectronica.asp) incorpora comprobantes *Factura de Crédito Electrónica*.

AFIP publicó una nueva [Especificación Técnica "FEv2.13"](http://www.afip.gob.ar/facturadecreditoelectronica/documentos/manual-desarrollador-COMPG-v2-13-Beta2.pdf) (manual para desarrolladores) con fecha 16 de Enero de 2019 AFIP, con las siguientes novedades:

- Nuevos comprobantes:

   - 201: Factura de Crédito Electrónica MiPyMEs (FCE) A
   - 202: Nota de Débito Electrónica MiPyMEs (FCE) A
   - 203: Nota de Crédito Electrónica MiPyMEs (FCE) A
   - 206: Factura de Crédito Electrónica MiPyMEs (FCE) B
   - 207: Nota de Débito Electrónica MiPyMEs (FCE) B
   - 208: Nota de Crédito Electrónica MiPyMEs (FCE) B
   - 211: Factura de Crédito Electrónica MiPyMEs (FCE) C
   - 212: Nota de Débito Electrónica MiPyMEs (FCE) C
   - 213: Nota de Crédito Electrónica MiPyMEs (FCE) C

- Se agregan obligatoriedad campo `fecha_venc_pago` en método `CrearFactura` ver [Descripción Metodos CAE](../documentacion_herramientas/manualpyafipws.md#descripcion-del-metodo-aut-obtencion-de-cae)
- Se agrega campo `fecha` y `CUIT`en `AgregarCbteAsoc` ver [Métodos WSFEv1](../documentacion_herramientas/manualpyafipws.md#metodos-basicos-de-wsfev1)
- Nuevos datos a informar: CBU, alias o código de anulación. Ver [Datos Opcionales AFIP WSFEv1](../documentacion_herramientas/manualpyafipws.md#datos-opcionales-afip-wsfev1)
 
Nuevas validaciones de AFIP:

- Uso de Campo asociado: Si el tipo de comprobante que está autorizando es MiPyMEs (FCE) y corresponde a un comprobante de débito o crédito, es obligatorio informar comprobantes asociados.
- Se modifican los siguientes códigos para modalidad de autorización CAE:

   - 10000: orden 10: “LA CUIT INFORMADA NO SE ENCUENTRA REGISTRADA COMO PYME SEGÚN EL REGIMEN FCE” y orden 11: “LA CUIT INFORMADA NO TIENE ACTIVO EL DOMICILIO FISCAL ELECTRONICO”
   - 10003: Para comprobantes del tipo MiPyMEs (FCE), la cantidad habilitada es 1 comprobante por request.
   - 10007: Campo CbteTipo sea 201, 202, 203, 206, 207, 208, 211, 212, 213 para los clase FCE
   - 10015: Para comprobantes MiPyMEs (FCE) el documento del receptor debe ser 80 CUIT.
   - 10016: Para comprobantes MiPyMEs (FCE) estar comprendido en el rango N-5 y N+1 siendo N la fecha de envío del pedido de autorización. De tratarse de notas de débito o crédito, la fecha del comprobante puede ser hasta N-5.
   - 10040: 
            - Para comprobantes MiPyMEs (FCE) 201, 206 o 211 puede asociarse los comprobantes (91, 990, 991, 993, 994,995). 
            - Para comprobantes MiPyMEs (FCE) A 202 y 203, puede asociar 201,202 o 203.
            - Para comprobantes MiPyMEs (FCE) B 207, 208 puede asociar 206, 207, 208.
            - Para comprobantes MiPyMEs (FCE) C 212, 213 puede asociarse 211, 212, 213.
   - 10042: Para comprobantes MiPyMEs (FCE) siempre es obligatoria la descripción.
   - 10068: El array Opcionales no es obligatorio. Solo puede informarse si CbteTipo es 1, 2, 3, 4, 6, 7, 8, 9, 11,12, 13, 15, 49, 51, 52, 53, 54, 201,206, 211, 203, 208, 213, 202, 207, 212.
   - 10151: Para comprobante del tipo MiPyMEs (FCE) del tipo débito o crédito es obligatorio informar el campo CbteAsoc CUIT
   - 10152: Si informa fecha de comprobante <CbteFch> para comprobantes del tipo MiPyMEs (FCE) con fecha superior a la fecha de envío de autorización, el mes de la fecha del comprobante <CbteFch> debe coincidir con el mes de la fecha de envío de autorización.
 
Errores frecuentes del Servidor de AFIP (homologación):

- 501: Error interno de base de datos - Fecred
- 501: Error interno de base de datos - Comprobante Credito Autorizar

TIP: Revisar concepto (usar 1 para pruebas, sin fecha servicio desde/hasta) y comprobantes asociados

Dato: Para FCE el importe del comprobante a autorizar debe ser superior a $6.000.000.- (hasta el 01/07/2019, luego probablemente este valor se modifique)

### Importante: RG4540/2019 FEv2.18

Se incorpora método AgregarPeriodoComprobantesAsociados como opcional al método Comprobante Asociado , para cumplimentar con lo establecido por la [RG4540/19 Procedimiento, Facturación. Emisión de notas de crédito y/o débito](https://www.boletinoficial.gob.ar/detalleAviso/primera/212546/20190801)

ver: [Métodos WSFEv1](../documentacion_herramientas/manualpyafipws.md#metodos-basicos-de-wsfev1)

*Nota:* Cada vez que se emite una NC/ND se deberá informar el o los comprobantes asociados o el periodo asociado de los comprobantes. Se informa uno u otro, no ambos. 


### Importante: RG5259/2022 y RG5264/2022, FEv3

AFIP publicó una nueva [Especificación Técnica "FEv3"](https://www.afip.gob.ar/fe/ayuda/documentos/wsfev1-COMPG.pdf) (manual para desarrolladores)

Se incorpora método para la consulta de Actividades vigentes (ParamGetActividades) y una estructura de actividades vinculadas al comprobante tanto en la
emisión de CAE, en el régimen de información de CAEA y en las consultas de los comprobantes ya autorizados.

ver: [Métodos WSFEv1](../documentacion_herramientas/manualpyafipws.md#metodos-basicos-de-wsfev1)


Aplicación: Resultará de aplicación **optativa** a partir del 15 de noviembre de 2022 y **obligatoria** desde el 15 de diciembre de 2022, posterior a esta fecha, los comprobantes serán rechazados si la actividad es Cárnico.
A partir del 01 de Febrero del 2023 será **optativa** hasta el 28/2 y desde el 01 de Marzo del 2023 será **obligatoria**, siendo rechazados los comprobantes, siendo la actividad Harina.

*Nota:* Al momento de confeccionar el correspondiente comprobante electrónico, que se emita para respaldar las operaciones de venta de carne y subproductos derivados de la faena de hacienda de las especies bovina/bubalina y porcina y las operaciones de venta de harinas y/o subproductos derivados de la molienda de trigo se deberá seleccionar la actividad por la cual se está realizando el mismo, con el objeto de identificar el o los “REC” emitidos.

### RG5614/2024

ARCA estableció nuevos criterios de Facturación para Facturas emitidas a Consumidores Finales "Régimen de Transparecia Fiscal al Consumidor"
["Resolución 5614/24"](https://www.boletinoficial.gob.ar/detalleAviso/primera/318151/20241213)

Esta nueva normativa no implica cambios en la interfaz PyAFIPWS, no obstante, si será necesaria una actualización para aquellos que se encuentren utilizando las herramientas PyFEPDF, PyRECE y PyFactura.

Aplicación: Será de aplicación obligatoria a partir del 1° de Enero de 2025, para las empresas definidas como “grandes empresas”.
Para el resto de los contribuyentes alcanzados será optativo desde el 1° de Enero de 2025 y obligatorio a partir del 1 de Abril de 2025.

### RG5616/2024 FEv4

ARCA estableció nuevos criterios de Facturación para las operaciones realizadas en moneda extranjera.

Ver["Resolución 5616/24"](https://www.boletinoficial.gob.ar/detalleAviso/primera/318374/20241218)

- Se afregan nuevos campos al método `CrearFactura(...)`:

                            - `cancela_misma_moneda_ext`
                            - `condicion_iva_receptor_id`

- Nuevos Metodos auxiliares:

                            - `ParamGetCotizacion(moneda_id, fecha)`: se agrega fecha de cotizacion
                            - `ParamGetCondicionIvaReceptor(clase_cmp)`: consultar condiciones de iva por clase de comprobante

Se agregan nuevas validaciones.


Aplicación:  Obligatorio para webservice a partir del 15 de Abril de 2025. (Prorrogado 1 de Septiembre 2025)


**Importante**: en `condicion_iva_receptor_id` es obligatorio a partir de la Versión 4, pero no debe ser enviado hasta que este en producción. En homologación ya se encuentra habilitado.


#### Mensaje de Evento 39

El servidor de ARCA devuelve el siguiente mensaje de evento, XmlResponse, independientemente de si en envian los campos nuevos o no.

```
#!xml
<Events>
  <Evt>
    <Code>39</Code>
    <Msg>IMPORTANTE: El dia 6 de abril de 2025, se actualizo la version del Web Service (WS) que permite enviar, de forma opcional, el campo Condicion Frente al IVA del receptor. Cabe destacar que la Resolucion General Nro 5616 indica que ese dato de  enviarse de manera obligatoria a partir del 15/04/2025. No obstante, se mantendra como un dato no excluyente hasta el 30/06/2025, inclusive. A partir del 1/07/2025 se rechazaran las solicitudes de emision de comprobantes sin este dato. Para mas
informacion, consultar el manual en: https://www.arca.gob.ar/fe/ayuda/webservice.asp, https://www.arca.gob.ar/ws/documentacion/ws-factura-electronica.asp</Msg>
  </Evt>
</Events>
```

#### Mensaje de Evento 41

El servidor de ARCA devuelve el siguiente mensaje de evento, XmlResponse, independientemente de si en envian los campos nuevos o no.

```
#!xml
<Events>
  <Evt>
    <Code>41</Code>
    <Msg>IMPORTANTE: El dia 9 de junio de 2025 se actualizo la version del Web Service (WS) en el ambiente de Homologacion Externa en la cual se establece como obligatorio el campo Condicion Frente al IVA del receptor. Cabe destacar que la Resolucion General Nro 5616 indica que ese dato debe enviarse de manera obligatoria. 
Para mas informacion, consultar el manual en: https://www.arca.gob.ar/fe/ayuda/webservice.asp, https://www.arca.gob.ar/ws/documentacion/ws-factura-electronica.asp</Msg>
  </Evt>
</Events>
```





#### Mensaje de Observacion 10245

El siguiente mensaje de observacion es enviado por el webservice si no se envían los campos nuevos es el siguiente (caso condicion_iva_receptor_id),

```
#!xml
<Observaciones>
  <Obs>
    <Code>10245</Code>
    <Msg>El campo Condicion Frente al IVA del receptor resultara obligatorio conforme lo reglamentado por la Resolucion General Nro 5616. Para mas informacion consular metodo FEParamGetCondicionIvaReceptor</Msg>
  </Obs>
</Observaciones>
```


En este caso revisar que se estan enviando los campos, por ej. con el siguiente codigo:

```
#!vb
ok = WSFEv1.EstablecerCampoFactura("cancela_misma_moneda_ext", "N")
ok = WSFEv1.EstablecerCampoFactura("condicion_iva_receptor_id", "5")
```


Ejemplo completo para VB: https://www.sistemasagiles.com.ar/trac/attachment/wiki/ProyectoWSFEv1/wsfev1.txt

Adicionalmente, borrar la carpeta cache donde se encuentran descargada la descripción del servicio web (WSDL), por si esta desactualizada.

Eventualmente utilizar el siguiente instalador para actualizar la carpeta cache:

https://www.sistemasagiles.com.ar/soft/pyafipws/final/PyAfipWS-Cache-UPDATE-2025.4.6.exe















## Descargas
Ver archivos y últimas actualizaciones para descargas en [GitHub](https://github.com/reingart/pyafipws/releases) (actualizado) y [GoogleCode](http://code.google.com/p/pyafipws/downloads/list) (histórico):

- Instalador: 
- [PyAfipWs-2.7.2942-32bit+wsaa_2.13a+wsfev1_1.28b-homo.exe](https://www.sistemasagiles.com.ar/soft/pyafipws/PyAfipWs-2.7.2942-32bit+wsaa_2.13a+wsfev1_1.28b-homo.exe) para evaluación (WSFEv1.28b Febrero 2025, incluyendo RG 5616)
- Ejemplos (última versión de desarrollo desde el repositorio del proyecto):
- VB 5/6: [wsfev1.bas](https://github.com/reingart/pyafipws/blob/master/ejemplos/wsfev1/wsfev1.bas) [FCE](https://drive.google.com/file/d/1woTaOrLIDoNes_x0Mr8I8dGBoxYlcGr9/view?usp=sharing)
- VFP: [wsfev1.prg](https://github.com/reingart/pyafipws/blob/master/ejemplos/wsfev1/wsfev1.prg) (última versión de dearrollo)
- VB .NET: [wsfev1.vb](https://github.com/reingart/pyafipws/blob/master/ejemplos/wsfev1/wsfev1.vb) 
- C# .NET: [wsfev1.cs](https://github.com/reingart/pyafipws/blob/master/ejemplos/wsfev1/wsfev1.cs)
- VBS: [factura_electronica.vbs](https://github.com/reingart/pyafipws/blob/master/ejemplos/factura_electronica.vbs) (no necesita IDE VB / .NET)
- Java: [FacturaElectronica.java](https://github.com/reingart/pyafipws/blob/master/ejemplos/FacturaElectronica.java) (requiere JACOB para Windows)
- PHP:
    - por JSON: [factura_electronica.php](https://github.com/reingart/pyafipws/blob/master/ejemplos/factura_electronica.php) (multiplataforma)
    - por COM: [https://github.com/reingart/pyafipws/blob/master/ejemplos/wsfev1/factura_electronica.php]  (windows)
- Power Builder: [ej_powerbuilder.txt](https://github.com/reingart/pyafipws/blob/master/ejemplos/wsfev1/ej_powerbuilder.txt)
- Python: [factura_electronica.py](https://github.com/reingart/pyafipws/blob/py3k/ejemplos/factura_electronica.py) (multiplataforma)
- Ejemplos MS Access/VBA: 
- [pyafipws.mdb](http://pyafipws.googlecode.com/files/pyafipws.mdb): WSFEv1 y WSFEX (base de datos MS Access 97 o sup.) 
- [pyafipws2k.mdb](http://pyafipws.googlecode.com/files/pyafipws2k.mdb): WSFEv1 y WSFEX (base de datos MS Access 2000 o sup.) 
- Tablas DBF ejemplo: [RECE1_dbf.zip](attachment:rece1_dbf.zip) (para dBase, Clipper, !FoxPro, Harbour, etc.) Ver [ManualPyAfipWs#InterfaseporarchivosdetextosímilSIAP-RECE RECE1]
- [Manual de Uso](../documentacion_herramientas/manualpyafipws.md): Documentación ([PDF](http://www.sistemasagiles.com.ar/trac/wiki/ManualPyAfipWs?format=pdf))
- Código Fuente (Python): ver archivos publicados en [GitHub](https://github.com/reingart/pyafipws/blob/master/wsfev1.py) 
- Listado de empresas para Pruebas Factura de Crédito MiPymes: [http://www.afip.gob.ar/facturadecreditoelectronica/documentos/Pruebas-homologacion-WS-FCE.zip]

## Instalación

Está disponible el instalador, simplemente seguir los pasos:

- Aceptar la licencia
- Seleccionar carpeta, por ej `C:\WSFEv1`
- Instalación y registración automática

Adicionalmente, si no se utilizó el instalador unificado con todos los webservices, es necesario instalar el instalador [instalador-WSAA-2.02c-homo.exe](http://pyafipws.googlecode.com/files/instalador-WSAA-2.02c-homo.exe) para WSAA (autenticación).
Para más información ver el [Manual de Uso](../documentacion_herramientas/manualpyafipws.md#instalacion)

## Cambios respecto a WSFE, WSFEX, WSBFE

En este nuevo servicio web WSFEv1, además de los campos requeridos por el WSFE para autorizar una factura (obtener el CAE), se debe informar:

- Concepto: similar al tipo de exportación (WSFEX) / presta_serv (WSFE)
- Moneda (según tabla de parámetros) y cotización de la factura
- Comprobantes Asociados: tipo de comprobante, punto de venta y número, similar a WSFEX
- Tributos: id, descripción, base imponible, alícuota (porcentaje), importe
- IVAs: id (según tabla de parámetros), base imponible, importe, similar a WSBFE
- ~~Detallar cada artículo vendido (ítems)~~: esto se removió de la versión 1 (si aplica en [Matrix WSMTXCA](wsmtxca.md))
- Código del producto
- Descripción completa
- Precio Neto Unitario
- Cantidad 
- Unidad de medida (según tabla de parámetros)
- Alicuota de Iva
- Importe total

La operatoria es bastante similar al método de autorización del WSFE, teniendo en cuenta esta mayor complejidad por tener que informar el detalle de cada item y las condiciones de exportación.

**NOTA**: Este webservice no tiene ID secuencial ni reproceso, por lo que el programa debe implementar la consulta de CAE en caso de errores de comunicación.

A su vez, el WSFEv1 devuelve mensajes de eventos (mantenimiento programado, advertencias, etc.), los que deben ser capturados e informados al usuario.

Para mayor información, se puede consultar la documentación orignal en [Manual del WSFEv1 - AFIP](http://www.afip.gov.ar/fe/documentos/manual_desarrollador_COMPG_v1.pdf) o el [manual](../documentacion_herramientas/manualpyafipws.md) manual de la presente interfaz. 

### Comprobantes clase C

Ver [ManualPyAfipWs#FacturaCMonotributoExento Manual de Uso: Factura C Monotributo/Exento] con las consideraciones a tener en cuenta en estos casos (valores de campos recomendados y ejemplos).

#### Monotributo RG3067/11

Según [Resolución General 3067/2011 de AFIP](http://www.afip.gov.ar/fe/#monoHIJKL), los monotributistas pueden usar webservices para automatizar la emisión de facturas electrónicas (pudiendo optar por ingresar voluntariamente y siendo obligatorio a partir de las H, I, J, K y L).

De hecho los monotributistas no necesitan reempadronarse al RECE ya que deben habilitar el servicio "Comprobantes en linea" (RCEL) por Clave Fiscal.

Para emitir facturas electrónicas tienen que crear un nuevo punto de ventas del tipo "Factura electronica. Monotributo - Web Services" (servicio online "Régimen de Regimenes de facturación y registración (REAR/RECE/RFI)" por Clave Fiscal) y ya pueden usar este servicio web [WSFEv1](http://www.sistemasagiles.com.ar/trac/wiki/ManualPyAfipWs#ServicioWebdeFacturaElectrónicaMercadoInternoVersión1WSFEv1) con el tipo de comprobante 11 (Factura C)

Errores frecuentes del webservice reportados por AFIP cuando el emisor está adherido al régimen simplificado para pequeños contribuyentes (monotributo):

- 10071: Para comprobantes tipo C el objeto IVA no debe informarse.
- 10000: NO AUTORIZADO A EMITIR COMPROBANTES - LA CUIT INFORMADA NO CORRESPONDE A UN RESPONSABLE INSCRIPTO EN EL IMPUESTO IVA.
- 10000: NO AUTORIZADO A EMITIR COMPROBANTES - LA CUIT INFORMADA NO SE ENCUENTRA AUTORIZADA A EMITIR COMPROBANTES ELECTRONICOS ORIGINALES O EL PERIODO DE INICIO AUTORIZADO ES POSTERIOR AL DE LA GENERACION DE LA SOLICITUD
- 10005: NO AUTORIZADO A EMITIR COMPROBANTES - EL PUNTO DE VENTA INFORMADO DEBE ESTAR DADO DE ALTA Y SER DEL TIPO RECE

Estos errores se solucionan enviando los datos correctos. 

#### Exentos RG3749/15

Según [RG 3749/2015](http://www.infoleg.gob.ar/infolegInternet/anexos/240000-244999/244572/norma.htm), los sujetos exentos en el impuesto al valor agregado pueden optar por el régimen de facturación electrónica. Para poder emitir comprobantes clase C, además de seguir las pautas señaladas en esta sección, el punto de venta debe estar dado de alta como "Factura Electrónica - Exento en IVA - Web Services".
En este caso aplican las mismas consideraciones que a los Monotributistas (explicado anteriormente)
## Ejemplo Intefase COM en VB (5/6)

```
' Crear objeto interface Web Service de Factura Electrónica de Mercado Interno
Set WSFEv1 = CreateObject("WSFEv1")
Debug.Print WSFEv1.version

' Setear tocken y sing de autorización (pasos previos)
WSFEv1.Token = WSAA.Token
WSFEv1.Sign = WSAA.Sign

' CUIT del emisor (debe estar registrado en la AFIP)
WSFEv1.Cuit = "20267565393"

' Conectar al Servicio Web de Facturación
ok = WSFEv1.Conectar() ' homologación

' Llamo a un servicio nulo, para obtener el estado del servidor (opcional)
WSFEv1.Dummy
Debug.Print "appserver status", WSFEv1.AppServerStatus
Debug.Print "dbserver status", WSFEv1.DbServerStatus
Debug.Print "authserver status", WSFEv1.AuthServerStatus
   
' Establezco los valores de la factura a autorizar:
tipo_cbte = 1
punto_vta = 1
cbte_nro = 0
fecha = "20101006"
concepto = 1
tipo_doc = 80: nro_doc = "23111111113"
cbt_desde = cbte_nro + 1: cbt_hasta = cbte_nro + 1
imp_total = "121.00": imp_tot_conc = "0.00": imp_neto = "100.00"
imp_iva = "21.00": imp_trib = "0.00": imp_op_ex = "0.00"
fecha_cbte = fecha: fecha_venc_pago = fecha
' Fechas del período del servicio facturado (solo si concepto = 1?)
fecha_serv_desde = fecha: fecha_serv_hasta = fecha
moneda_id = "DOL": moneda_ctz = "3.856"

ok = WSFEv1.CrearFactura(concepto, tipo_doc, nro_doc, tipo_cbte, punto_vta, _
	cbt_desde, cbt_hasta, imp_total, imp_tot_conc, imp_neto, _
	imp_iva, imp_trib, imp_op_ex, fecha_cbte, fecha_venc_pago, _
	fecha_serv_desde, fecha_serv_hasta, _
	moneda_id, moneda_ctz)

' Agrego los comprobantes asociados:
tipo = 19
pto_vta = 2
nro = 1234
ok = WSFEv1.AgregarCmpAsoc(tipo, pto_vta, nro)

' Agrego impuestos varios
id = 0
Desc = "Impuesto Municipal Matanza'"
base_imp = 150
alic = 5.2
importe = 5.8
ok = WSFEv1.AgregarTributo(id, Desc, base_imp, alic, importe)

' Agrego tasas de IVA
id = 5 ' 21%
base_im = 100
importe = 21
ok = WSFEv1.AgregarIva(id, base_imp, importe)

' Solicito CAE:
cae = WSFEv1.CAESolicitar()

Debug.Print "Resultado", WSFEv1.Resultado
Debug.Print "CAE", WSFEv1.cae
```

**Nota:** La metodología es similar al resto de los webservices, y se trato de mantener similitud con el código existente:

- Método WSFEv1.!CrearFactura es similar a WSFE.Authorize (parámetros similares)
- Método WSFEv1.!AgregarCmpAsoc es similar a WSFEX.!AgregarCmpAsoc
- Propiedades similares: WSFEv1.CAE, WSFEv1.Resultado, etc.

## Tablas de Parámetros

Este nuevo servicio funciona con tablas dinámicas de parámetros para los códigos de comprobante, moneda, IVA, tributos, datos opcionales. Estas tablas pueden sufrir modificaciones realizadas por la AFIP, con altas y bajas lógicas, por lo que tienen una fecha de vigencia (desde, hasta) y se proveen métodos para consultarlas por el mismo servicio web (a diferencia del WSFE, que las tablas eran documentadas estaticamentes en el sitio web).

Ver Planilla [Anexo Tablas del Sistema](http://www.afip.gov.ar/fe/documentos/TABLAS%20GENERALES%20V.0%20%2025082010.xls) (puede estar desactualizado respecto los últimos cambios)

Como ejemplo, a continuación se copian los resultados de invocar a los webservices para consultar las tablas de parámetros al 22/10/2010 (homologación):

### Tipos de Comprobante
| 1 | Factura A | 20100917 | NULL |
|---|---|---|---|
| 2 | Nota de Débito A | 20100917 | NULL |
| 3 | Nota de Crédito A | 20100917 | NULL |
| 6 | Factura B | 20100917 | NULL |
| 7 | Nota de Débito B | 20100917 | NULL |
| 8 | Nota de Crédito B | 20100917 | NULL |
| 4 | Recibos A | 20100917 | NULL |
| 5 | Notas de Venta al contado A | 20100917 | NULL |
| 9 | Recibos B | 20100917 | NULL |
| 10 | Notas de Venta al contado B | 20100917 | NULL |
| 63 | Liquidacion A | 20100917 | NULL |
| 64 | Liquidacion B | 20100917 | NULL |
| 34 | Cbtes. A del Anexo I, Apartado A,inc.f),R.G.Nro. 1415 | 20100917 | NULL |
| 35 | Cbtes. B del Anexo I,Apartado A,inc. f),R.G. Nro. 1415 | 20100917 | NULL |
| 39 | Otros comprobantes A que cumplan con R.G.Nro. 1415 | 20100917 | NULL |
| 40 | Otros comprobantes B que cumplan con R.G.Nro. 1415 | 20100917 | NULL |
| 60 | Cta de Vta y Liquido prod. A | 20100917 | NULL |
| 61 | Cta de Vta y Liquido prod. B | 20100917 | NULL |
| 11 | Factura C | 20110330 | NULL |
| 12 | Nota de Débito C | 20110330 | NULL |
| 13 | Nota de Crédito C | 20110330 | NULL |
| 15 | Recibo C | 20110330 | NULL |
| 49 | Comprobante de Compra de Bienes Usados a Consumidor Final | 20130904 | NULL |
| 51 | Factura M | 20150522 | NULL |
| 52 | Nota de Débito M | 20150522 | NULL |
| 53 | Nota de Crédito M | 20150522 | NULL |
| 54 | Recibo M | 20150522 | NULL |
| 201 | Factura de Crédito electrónica MiPyMEs (FCE) A | 20181226 | NULL |
| 202 | Nota de Débito electrónica MiPyMEs (FCE) A | 20181226 | NULL |
| 203 | Nota de Crédito electrónica MiPyMEs (FCE) A | 20181226 | NULL |
| 206 | Factura de Crédito electrónica MiPyMEs (FCE) B | 20181226 | NULL |
| 207 | Nota de Débito electrónica MiPyMEs (FCE) B | 20181226 | NULL |
| 208 | Nota de Crédito electrónica MiPyMEs (FCE) B | 20181226 | NULL |
| 211 | Factura de Crédito electrónica MiPyMEs (FCE) C | 20181226 | NULL |
| 212 | Nota de Débito electrónica MiPyMEs (FCE) C | 20181226 | NULL |
| 213 | Nota de Crédito electrónica MiPyMEs (FCE) C | 20181226 | NULL |

### Tipos de Concepto
| 1 | Producto | 20100917 | NULL |
|---|---|---|---|
| 2 | Servicios | 20100917 | NULL |
| 3 | Productos y Servicios | 20100917 | NULL |
### Tipos de Documento
| 80 | CUIT | 20080725 | NULL |
|---|---|---|---|
| 86 | CUIL | 20080725 | NULL |
| 87 | CDI | 20080725 | NULL |
| 89 | LE | 20080725 | NULL |
| 90 | LC | 20080725 | NULL |
| 91 | CI Extranjera | 20080725 | NULL |
| 92 | en trámite | 20080725 | NULL |
| 93 | Acta Nacimiento | 20080725 | NULL |
| 95 | CI Bs. As. RNP | 20080725 | NULL |
| 96 | DNI | 20080725 | NULL |
| 94 | Pasaporte | 20080725 | NULL |
| 0 | CI Policía Federal | 20080725 | NULL |
| 1 | CI Buenos Aires | 20080725 | NULL |
| 2 | CI Catamarca | 20080725 | NULL |
| 3 | CI Córdoba | 20080725 | NULL |
| 4 | CI Corrientes | 20080728 | NULL |
| 5 | CI Entre Ríos | 20080728 | NULL |
| 6 | CI Jujuy | 20080728 | NULL |
| 7 | CI Mendoza | 20080728 | NULL |
| 8 | CI La Rioja | 20080728 | NULL |
| 9 | CI Salta | 20080728 | NULL |
| 10 | CI San Juan | 20080728 | NULL |
| 11 | CI San Luis | 20080728 | NULL |
| 12 | CI Santa Fe | 20080728 | NULL |
| 13 | CI Santiago del Estero | 20080728 | NULL |
| 14 | CI Tucumán | 20080728 | NULL |
| 16 | CI Chaco | 20080728 | NULL |
| 17 | CI Chubut | 20080728 | NULL |
| 18 | CI Formosa | 20080728 | NULL |
| 19 | CI Misiones | 20080728 | NULL |
| 20 | CI Neuquén | 20080728 | NULL |
| 21 | CI La Pampa | 20080728 | NULL |
| 22 | CI Río Negro | 20080728 | NULL |
| 23 | CI Santa Cruz | 20080728 | NULL |
| 24 | CI Tierra del Fuego | 20080728 | NULL |
| 99 | Doc. (Otro) | 20080728 | NULL |
### Alicuotas de IVA
| 3 | 0% | 20090220 | NULL |
|---|---|---|---|
| 4 | 10.5% | 20090220 | NULL |
| 5 | 21% | 20090220 | NULL |
| 6 | 27% | 20090220 | NULL |
| 8 | 5% | 20141020 | NULL |
| 9 | 2.5% | 20141020 | NULL |

NOTA: Se incorporararon las alícuotas identificadas en la Ley 26982 (5% y 2.5%). 
### Monedas
| PES | Pesos Argentinos | 20090403 | NULL |
|---|---|---|---|
| DOL | Dólar Estadounidense | 20090403 | NULL |
| 002 | Dólar Libre EEUU | 20090416 | NULL |
| 007 | Florines Holandeses | 20090403 | NULL |
| 010 | Pesos Mejicanos | 20090403 | NULL |
| 011 | Pesos Uruguayos | 20090403 | NULL |
| 014 | Coronas Danesas | 20090403 | NULL |
| 015 | Coronas Noruegas | 20090403 | NULL |
| 016 | Coronas Suecas | 20090403 | NULL |
| 018 | Dólar Canadiense | 20090403 | NULL |
| 019 | Yens | 20090403 | NULL |
| 021 | Libra Esterlina | 20090403 | NULL |
| 023 | Bolívar Venezolano | 20090403 | NULL |
| 024 | Corona Checa | 20090403 | NULL |
| 025 | Dinar Yugoslavo | 20090403 | NULL |
| 026 | Dólar Australiano | 20090403 | NULL |
| 027 | Dracma Griego | 20090403 | NULL |
| 028 | Florín (Antillas Holandesas) | 20090403 | NULL |
| 029 | Güaraní | 20090403 | NULL |
| 031 | Peso Boliviano | 20090403 | NULL |
| 032 | Peso Colombiano | 20090403 | NULL |
| 033 | Peso Chileno | 20090403 | NULL |
| 034 | Rand Sudafricano | 20090403 | NULL |
| 036 | Sucre Ecuatoriano | 20090403 | NULL |
| 051 | Dólar de Hong Kong | 20090403 | NULL |
| 052 | Dólar de Singapur | 20090403 | NULL |
| 053 | Dólar de Jamaica | 20090403 | NULL |
| 054 | Dólar de Taiwan | 20090403 | NULL |
| 055 | Quetzal Guatemalteco | 20090403 | NULL |
| 056 | Forint (Hungría) | 20090403 | NULL |
| 057 | Baht (Tailandia) | 20090403 | NULL |
| 059 | Dinar Kuwaiti | 20090403 | NULL |
| 012 | Real | 20090403 | NULL |
| 030 | Shekel (Israel) | 20090403 | NULL |
| 035 | Nuevo Sol Peruano | 20090403 | NULL |
| 060 | Euro | 20090403 | NULL |
| 040 | Lei Rumano | 20090415 | NULL |
| 042 | Peso Dominicano | 20090415 | NULL |
| 043 | Balboas Panameñas | 20090415 | NULL |
| 044 | Córdoba Nicaragüense | 20090415 | NULL |
| 045 | Dirham Marroquí | 20090415 | NULL |
| 046 | Libra Egipcia | 20090415 | NULL |
| 047 | Riyal Saudita | 20090415 | NULL |
| 061 | Zloty Polaco | 20090415 | NULL |
| 062 | Rupia Hindú | 20090415 | NULL |
| 063 | Lempira Hondureña | 20090415 | NULL |
| 064 | Yuan (Rep. Pop. China) | 20090415 | NULL |
| 009 | Franco Suizo | 20091110 | NULL |
| 041 | Derechos Especiales de Giro | 20100125 | NULL |
| 049 | Gramos de Oro Fino | 20100125 | NULL |
### Tipos de datos opcionales
| 2 | RG Empresas Promovidas - Indentificador de proyecto vinculado a Régimen de Promoción Industrial | 20100917 | NULL |
|---|---|---|---|
| 91 | RG Bienes Usados 3411 - Nombre y Apellido o Denominación del vendedor del bien usado. | 20130401 | NULL |
| 92 | RG Bienes Usados 3411 - Nacionalidad del vendedor del bien usado. | 20130401 | NULL |
| 93 | RG Bienes Usados 3411 - Domicilio del vendedor del bien usado. | 20130401 | NULL |
| 5 | Excepcion computo IVA Credito Fiscal | 20141016 | NULL |
| 61 | RG 3668 Impuesto al Valor Agregado - Art.12 IVA Firmante Doc Tipo | 20141016 | NULL |
| 62 | RG 3668 Impuesto al Valor Agregado - Art.12 IVA Firmante Doc Nro | 20141016 | NULL |
| 7 | |RG 3668 Impuesto al Valor Agregado - Art.12 IVA Carácter del Firmante | 20141016 | NULL |
| 10 | RG 3.368 Establecimientos de educación pública de gestión privada - Actividad Comprendida | 20150605 | NULL |
| 1011 | RG 3.368 Establecimientos de educación pública de gestión privada - Tipo de Documento | 20150605 | NULL |
| 1012 | RG 3.368 Establecimientos de educación pública de gestión privada - Número de Documento | 20150605 | NULL |
| 11 | RG 2.820 Operaciones económicas vinculadas con bienes inmuebles - Actividad Comprendida | 20150605 | NULL |
| 12 | RG 3.687 Locación temporaria de inmuebles con fines turísticos - Actividad Comprendida | 20150605 | NULL |
| 13 | RG 2.863 Representantes de Modelos | 20160101 | NULL |
| 14 | RG 2.863 Agencias de publicidad | 20160101 | NULL |
| 15 | RG 2.863 Personas físicas que desarrollen actividad de modelaje | 20160101 | NULL |
| 17 | RG 4004-E Locación de inmuebles destino 'casa-habitación'. Dato 2 (dos) = facturación directa / Dato 1 (uno) = facturación a través de intermediario | 20170309 | NULL |
| 1801 | RG 4004-E Locación de inmuebles destino 'casa-habitación'. Clave Única de Identificación Tributaria (CUIT). | 20170309 | NULL |
| 1802 | RG 4004-E Locación de inmuebles destino 'casa-habitación'. Apellido y nombres, denominación y/o razón social. | 20170309 | NULL |
| 2101 | RG 4367 Factura de Crédito Electrónica MiPyMEs (FCE) - CBU del Emisor | 20181226 | NULL |
| 2102 | RG 4367 Factura de Crédito Electrónica MiPyMEs (FCE) - Alias del Emisor | 20181226 | NULL |
| 22 | RG 4367 Factura de Crédito Electrónica MiPyMEs (FCE) - Anulación | 20181226 | NULL |
| 23 | RG 4367 Factura de Crédito Electrónica MiPyMEs (FCE) - Referencia Comercial | 20190308 | NULL |
| 27 | RG 4919 Factura de Crédito Electrónica MiPyMEs (FCE) - Sistema de transmisión |


### Tipos de Tributo
| 1 | Impuestos nacionales | 20100917 | NULL |
|---|---|---|---|
| 2 | Impuestos provinciales | 20100917 | NULL |
| 3 | Impuestos municipales | 20100917 | NULL |
| 4 | Impuestos Internos | 20100917 | NULL |
| 99 | Otro | 20100917 | NULL |

### Condicion Iva Receptor A
| 1 | IVA Responsable Inscripto | A |
|---|---|---|
| 6 | Responsable Monotributo | A |
| 13 | Monotributista Social | A |
| 16 | Monotributo Trabajador Independiente Promovido | A |

### Condicion Iva Receptor M
| 1 | IVA Responsable Inscripto | M |
|---|---|---|
| 6 | Responsable Monotributo | M |
| 13 | Monotributista Social|M |
| 16 | Monotributo Trabajador Independiente Promovido | M |

### Condicion Iva Receptor B
| 4 | IVA Sujeto Exento | B |
|---|---|---|
| 5 | Consumidor Final | B |
| 7 | Sujeto No Categorizado | B |
| 8 | Proveedor del Exterior | B |
| 9 | Cliente del Exterior | B |
| 10 | IVA Liberado – Ley N° 19.640 | B |
| 15 | IVA No Alcanzado | B |

### Condicion Iva Receptor C
| 1 | IVA Responsable Inscripto | C |
|---|---|---|
| 6 | Responsable Monotributo | C |
| 13 | Monotributista Social | C |
| 16 | Monotributo Trabajador Independiente Promovido | C |
| 4 | IVA Sujeto Exento | C |
| 5 | Consumidor Final | C |
| 7 | Sujeto No Categorizado | C |
| 8 | Proveedor del Exterior | C |
| 9 | Cliente del Exterior | C |
| 10 | IVA Liberado – Ley N° 19.640 | C |
| 15 | IVA No Alcanzado | C |


### Tipos de Paises
| 101 | BURKINA FASO |
|---|---|
| 102 | ARGELIA |
| 103 | BOTSWANA |
| 104 | BURUNDI |
| 105 | CAMERUN |
| 107 | REP. CENTROAFRICANA. |
| 108 | CONGO |
| 109 | REP.DEMOCRAT.DEL CONGO EX ZAIRE |
| 110 | COSTA DE MARFIL |
| 111 | CHAD |
| 112 | BENIN |
| 113 | EGIPTO |
| 115 | GABON |
| 116 | GAMBIA |
| 117 | GHANA |
| 118 | GUINEA |
| 119 | GUINEA ECUATORIAL |
| 120 | KENYA |
| 121 | LESOTHO |
| 122 | LIBERIA |
| 123 | LIBIA |
| 124 | MADAGASCAR |
| 125 | MALAWI |
| 126 | MALI |
| 127 | MARRUECOS |
| 128 | MAURICIO,ISLAS |
| 129 | MAURITANIA |
| 130 | NIGER |
| 131 | NIGERIA |
| 132 | ZIMBABWE |
| 133 | RWANDA |
| 134 | SENEGAL |
| 135 | SIERRA LEONA |
| 136 | SOMALIA |
| 137 | SWAZILANDIA |
| 138 | SUDAN |
| 139 | TANZANIA |
| 140 | TOGO |
| 141 | TUNEZ |
| 142 | UGANDA |
| 144 | ZAMBIA |
| 145 | TERRIT.VINCULADOS AL R UNIDO |
| 146 | TERRIT.VINCULADOS A ESPAÑA |
| 147 | TERRIT.VINCULADOS A FRANCIA |
| 149 | ANGOLA |
| 150 | CABO VERDE |
| 151 | MOZAMBIQUE |
| 152 | SEYCHELLES |
| 153 | DJIBOUTI |
| 155 | COMORAS |
| 156 | GUINEA BISSAU |
| 157 | STO.TOME Y PRINCIPE |
| 158 | NAMIBIA |
| 159 | SUDAFRICA |
| 160 | ERITREA |
| 161 | ETIOPIA |
| 197 | RESTO (AFRICA) |
| 198 | INDETERMINADO (AFRICA) |
| 200 | ARGENTINA |
| 201 | BARBADOS |
| 202 | BOLIVIA |
| 203 | BRASIL |
| 204 | CANADA |
| 205 | COLOMBIA |
| 206 | COSTA RICA |
| 207 | CUBA |
| 208 | CHILE |
| 209 | REPÚBLICA DOMINICANA |
| 210 | ECUADOR |
| 211 | EL SALVADOR |
| 212 | ESTADOS UNIDOS |
| 213 | GUATEMALA |
| 214 | GUYANA |
| 215 | HAITI |
| 216 | HONDURAS |
| 217 | JAMAICA |
| 218 | MEXICO |
| 219 | NICARAGUA |
| 220 | PANAMA |
| 221 | PARAGUAY |
| 222 | PERU |
| 223 | PUERTO RICO |
| 224 | TRINIDAD Y TOBAGO |
| 225 | URUGUAY |
| 226 | VENEZUELA |
| 227 | TERRIT.VINCULADO AL R.UNIDO |
| 228 | TER.VINCULADOS A DINAMARCA |
| 229 | TERRIT.VINCULADOS A FRANCIA AMERIC. |
| 230 | TERRIT. HOLANDESES |
| 231 | TER.VINCULADOS A ESTADOS UNIDOS |
| 232 | SURINAME |
| 233 | DOMINICA |
| 234 | SANTA LUCIA |
| 235 | SAN VICENTE Y LAS GRANADINAS |
| 236 | BELICE |
| 237 | ANTIGUA Y BARBUDA |
| 238 | S.CRISTOBAL Y NEVIS |
| 239 | BAHAMAS |
| 240 | GRENADA |
| 241 | ANTILLAS HOLANDESAS |
| 242 | ARUBA |
| 250 | AAE Tierra del Fuego - ARGENTINA |
| 251 | ZF La Plata - ARGENTINA |
| 252 | ZF Justo Daract - ARGENTINA |
| 253 | ZF Río Gallegos - ARGENTINA |
| 254 | Islas Malvinas - ARGENTINA |
| 255 | ZF Tucumán - ARGENTINA |
| 256 | ZF Córdoba - ARGENTINA |
| 257 | ZF Mendoza - ARGENTINA |
| 258 | ZF General Pico - ARGENTINA |
| 259 | ZF Comodoro Rivadavia - ARGENTINA |
| 260 | ZF Iquique |
| 261 | ZF Punta Arenas |
| 262 | ZF Salta - ARGENTINA |
| 263 | ZF Paso de los Libres - ARGENTINA |
| 264 | ZF Puerto Iguazú - ARGENTINA |
| 265 | SECTOR ANTARTICO ARG. |
| 270 | ZF Colón - REPÚBLICA DE PANAMÁ |
| 271 | ZF Winner (Sta. C. de la Sierra) - BOLIVIA |
| 280 | ZF Colonia - URUGUAY |
| 281 | ZF Florida - URUGUAY |
| 282 | ZF Libertad - URUGUAY |
| 283 | ZF Zonamerica - URUGUAY |
| 284 | ZF Nueva Helvecia - URUGUAY |
| 285 | ZF Nueva Palmira - URUGUAY |
| 286 | ZF Río Negro - URUGUAY |
| 287 | ZF Rivera - URUGUAY |
| 288 | ZF San José - URUGUAY |
| 291 | ZF Manaos - BRASIL |
| 295 | MAR ARG ZONA ECO.EX |
| 296 | RIOS ARG NAVEG INTER |
| 297 | RESTO AMERICA |
| 298 | INDETERMINADO (AMERICA) |
| 301 | AFGANISTAN |
| 302 | ARABIA SAUDITA |
| 303 | BAHREIN |
| 304 | MYANMAR (EX-BIRMANIA) |
| 305 | BUTAN |
| 306 | CAMBODYA (EX-KAMPUCHE) |
| 307 | SRI LANKA |
| 308 | COREA DEMOCRATICA |
| 309 | COREA REPUBLICANA |
| 310 | CHINA |
| 312 | FILIPINAS |
| 313 | TAIWAN |
| 315 | INDIA |
| 316 | INDONESIA |
| 317 | IRAK |
| 318 | IRAN |
| 319 | ISRAEL |
| 320 | JAPON |
| 321 | JORDANIA |
| 322 | QATAR |
| 323 | KUWAIT |
| 324 | LAOS |
| 325 | LIBANO |
| 326 | MALASIA |
| 327 | MALDIVAS ISLAS |
| 328 | OMAN |
| 329 | MONGOLIA |
| 330 | NEPAL |
| 331 | EMIRATOS ARABES UNIDOS |
| 332 | PAKISTÁN |
| 333 | SINGAPUR |
| 334 | SIRIA |
| 335 | THAILANDIA |
| 337 | VIETNAM |
| 341 | HONG KONG |
| 344 | MACAO |
| 345 | BANGLADESH |
| 346 | BRUNEI |
| 348 | REPUBLICA DE YEMEN |
| 349 | ARMENIA |
| 350 | AZERBAIJAN |
| 351 | GEORGIA |
| 352 | KAZAJSTAN |
| 353 | KIRGUIZISTAN |
| 354 | TAYIKISTAN |
| 355 | TURKMENISTAN |
| 356 | UZBEKISTAN |
| 357 | TERR. AU. PALESTINOS |
| 397 | RESTO DE ASIA |
| 398 | INDET.(ASIA) |
| 401 | ALBANIA |
| 404 | ANDORRA |
| 405 | AUSTRIA |
| 406 | BELGICA |
| 407 | BULGARIA |
| 409 | DINAMARCA |
| 410 | ESPAÑA |
| 411 | FINLANDIA |
| 412 | FRANCIA |
| 413 | GRECIA |
| 414 | HUNGRIA |
| 415 | IRLANDA |
| 416 | ISLANDIA |
| 417 | ITALIA |
| 418 | LIECHTENSTEIN |
| 419 | LUXEMBURGO |
| 420 | MALTA |
| 421 | MONACO |
| 422 | NORUEGA |
| 423 | PAISES BAJOS |
| 424 | POLONIA |
| 425 | PORTUGAL |
| 426 | REINO UNIDO |
| 427 | RUMANIA |
| 428 | SAN MARINO |
| 429 | SUECIA |
| 430 | SUIZA |
| 431 | VATICANO(SANTA SEDE) |
| 433 | POS.BRIT.(EUROPA) |
| 435 | CHIPRE |
| 436 | TURQUIA |
| 438 | ALEMANIA,REP.FED. |
| 439 | BIELORRUSIA |
| 440 | ESTONIA |
| 441 | LETONIA |
| 442 | LITUANIA |
| 443 | MOLDAVIA |
| 444 | RUSIA |
| 445 | UCRANIA |
| 446 | BOSNIA HERZEGOVINA |
| 447 | CROACIA |
| 448 | ESLOVAQUIA |
| 449 | ESLOVENIA |
| 450 | MACEDONIA |
| 451 | REP. CHECA |
| 453 | MONTENEGRO |
| 454 | SERBIA |
| 497 | RESTO EUROPA |
| 498 | INDET.(EUROPA) |
| 501 | AUSTRALIA |
| 503 | NAURU |
| 504 | NUEVA ZELANDIA |
| 505 | VANATU |
| 506 | SAMOA OCCIDENTAL |
| 507 | TERRITORIO VINCULADOS A AUSTRALIA |
| 508 | TERRITORIOS VINCULADOS AL R. UNIDO |
| 509 | TERRITORIOS VINCULADOS A FRANCIA |
| 510 | TER VINCULADOS A NUEVA. ZELANDA |
| 511 | TER. VINCULADOS A ESTADOS UNIDOS |
| 512 | FIJI, ISLAS |
| 513 | PAPUA NUEVA GUINEA |
| 514 | KIRIBATI, ISLAS |
| 515 | MICRONESIA,EST.FEDER |
| 516 | PALAU |
| 517 | TUVALU |
| 518 | SALOMON,ISLAS |
| 519 | TONGA |
| 520 | MARSHALL,ISLAS |
| 521 | MARIANAS,ISLAS |
| 597 | RESTO OCEANIA |
| 598 | INDET.(OCEANIA) |
| 997 | RESTO CONTINENTE |
| 998 | INDET.(CONTINENTE) |

### Actividades

| 11111: 32 CULTIVO DE ARROZ |
|---|
| 11119: 33 CULTIVO DE CEREALES N.C.P., EXCEPTO LOS DE USO FORRAJERO |
| 11130: 34 CULTIVO DE PASTOS DE USO FORRAJERO |
| 11211: 35 CULTIVO DE SOJA |
| 11400: 36 CULTIVO DE TABACO |
| 12320: 37 CULTIVO DE FRUTAS DE CAROZO |
| 12510: 38 CULTIVO DE CAÃ`A DE AZÃ¿CAR |
| 14113: 39 CRÃ¿A DE GANADO BOVINO, EXCEPTO LA REALIZADA EN CABAÃ`AS Y PARA LA PRODUCCIÃ¿N DE LECHE |
| 14440: 40 CRÃ¿A DE GANADO CAPRINO REALIZADA EN CABAÃ`AS |
| 14930: 41 CRÃ¿A DE ANIMALES PELÃ¿FEROS, PILÃ¿FEROS Y PLUMÃ¿FEROS, EXCEPTO DE LAS ESPECIES GANADERAS |
| 16112: 42 SERVICIOS DE PULVERIZACIÃ¿N, DESINFECCIÃ¿N Y FUMIGACIÃ¿N TERRESTRE |
| 16113: 43 SERVICIOS DE PULVERIZACIÃ¿N, DESINFECCIÃ¿N Y FUMIGACIÃ¿N AÃ¿REA |
| 16119: 44 SERVICIOS DE MAQUINARIA AGRÃ¿COLA N.C.P., EXCEPTO LOS DE COSECHA MECÃ¿NICA |
| 16140: 45 SERVICIOS DE POST COSECHA |
| 16299: 46 SERVICIOS DE APOYO PECUARIOS N.C.P. |
| 31120: 47 PESCA Y ELABORACIÃ¿N DE PRODUCTOS MARINOS REALIZADA A BORDO DE BUQUES PROCESADORES |
| 51000: 48 EXTRACCIÃ¿N Y AGLOMERACIÃ¿N DE CARBÃ¿N |
| 61000: 49 EXTRACCIÃ¿N DE PETRÃ¿LEO CRUDO |
| 62000: 50 EXTRACCIÃ¿N DE GAS NATURAL |
| 72910: 51 EXTRACCIÃ¿N DE METALES PRECIOSOS |
| 81300: 52 EXTRACCIÃ¿N DE ARENAS, CANTO RODADO Y TRITURADOS PÃ¿TREOS |
| 89120: 53 EXTRACCIÃ¿N DE MINERALES PARA LA FABRICACIÃ¿N DE PRODUCTOS QUÃ¿MICOS |
| 101011: 17 MATANZA DE GANADO BOVINO |
| 101012: 18 PROCESAMIENTO DE CARNE DE GANADO BOVINO |
| 101040: 15 MATANZA DE GANADO EXCEPTO EL BOVINO Y PROCESAMIENTO DE SU CARNE |
| 101099: 16 MATANZA DE ANIMALES N.C.P. Y PROCESAMIENTO DE SU CARNE, ELABORACIÓN DE SUBPRODUCTOS CÁRNICOS N.C.P. |
| 104011: 54 ELABORACIÃ¿N DE ACEITES Y GRASAS VEGETALES  SIN REFINAR |
| 104012: 55 ELABORACIÃ¿N DE ACEITE DE OLIVA |
| 107500: 56 ELABORACIÃ¿N DE COMIDAS PREPARADAS PARA REVENTA |
| 108000: 57 ELABORACIÃ¿N DE ALIMENTOS PREPARADOS PARA ANIMALES |
| 120010: 19 PREPARACIÓN DE HOJAS DE TABACO |
| 120099: 20 ELABORACIÓN DE PRODUCTOS DE TABACO N.C.P. |
| 131300: 58 ACABADO DE PRODUCTOS TEXTILES |
| 152031: 59 FABRICACIÃ¿N DE CALZADO DEPORTIVO |
| 161001: 60 ASERRADO Y CEPILLADO DE MADERA  NATIVA |
| 192000: 61 FABRICACIÃ¿N DE PRODUCTOS DE LA REFINACIÃ¿N DEL PETRÃ¿LEO |
| 202200: 62 FABRICACIÃ¿N DE PINTURAS, BARNICES Y PRODUCTOS DE REVESTIMIENTO SIMILARES, TINTAS DE IMPRENTA Y MASILLAS |
| 222010: 63 FABRICACIÃ¿N DE ENVASES PLÃ¿STICOS |
| 251101: 64 FABRICACIÃ¿N DE CARPINTERÃ¿A METÃ¿LICA |
| 275091: 65 FABRICACIÃ¿N DE VENTILADORES, EXTRACTORES DE AIRE, ASPIRADORAS Y SIMILARES |
| 275092: 66 FABRICACIÃ¿N DE PLANCHAS, CALEFACTORES, HORNOS ELÃ¿CTRICOS, TOSTADORAS Y OTROS APARATOS GENERADORES DE CALOR |
| 323001: 67 FABRICACIÃ¿N DE ARTÃ¿CULOS DE DEPORTE |
| 324000: 68 FABRICACIÃ¿N DE JUEGOS Y JUGUETES |
| 351110: 69 GENERACIÃ¿N DE ENERGÃ¿A TÃ¿RMICA CONVENCIONAL |
| 351120: 70 GENERACIÃ¿N DE ENERGÃ¿A TÃ¿RMICA NUCLEAR |
| 382010: 71 RECUPERACIÃ¿N DE MATERIALES Y DESECHOS METÃ¿LICOS |
| 410021: 72 CONSTRUCCIÃ¿N, REFORMA Y REPARACIÃ¿N DE EDIFICIOS NO RESIDENCIALES |
| 421000: 73 CONSTRUCCIÃ¿N, REFORMA Y REPARACIÃ¿N DE OBRAS DE INFRAESTRUCTURA PARA EL TRANSPORTE |
| 422200: 74 CONSTRUCCIÃ¿N, REFORMA Y REPARACIÃ¿N DE REDES DISTRIBUCIÃ¿N DE ELECTRICIDAD, GAS, AGUA, TELECOMUNICACIONES Y DE OTROS SERVICIOS PÃ¿BLICOS |
| 431210: 75 MOVIMIENTO DE SUELOS Y PREPARACIÃ¿N DE TERRENOS PARA OBRAS |
| 432110: 76 INSTALACIÃ¿N DE SISTEMAS DE ILUMINACIÃ¿N, CONTROL Y SEÃ`ALIZACIÃ¿N ELÃ¿CTRICA PARA EL TRANSPORTE |
| 433040: 77 PINTURA Y TRABAJOS DE DECORACIÃ¿N |
| 439100: 78 ALQUILER DE EQUIPO DE CONSTRUCCIÃ¿N O DEMOLICIÃ¿N DOTADO DE OPERARIOS |
| 451110: 79 VENTA DE AUTOS, CAMIONETAS Y UTILITARIOS NUEVOS |
| 452220: 80 REPARACIÃ¿N DE AMORTIGUADORES,  ALINEACIÃ¿N DE DIRECCIÃ¿N Y BALANCEO DE RUEDAS |
| 461011: 81 VENTA AL POR MAYOR EN COMISIÃ¿N O CONSIGNACIÃ¿N DE CEREALES (INCLUYE ARROZ), OLEAGINOSAS Y FORRAJERAS EXCEPTO SEMILLAS |
| 461013: 82 VENTA AL POR MAYOR EN COMISIÃ¿N O CONSIGNACIÃ¿N DE FRUTAS |
| 461014: 83 ACOPIO Y ACONDICIONAMIENTO EN COMISIÃ¿N O CONSIGNACIÃ¿N DE CEREALES (INCLUYE ARROZ), OLEAGINOSAS Y FORRAJERAS EXCEPTO SEMILLAS |
| 461019: 84 VENTA AL POR MAYOR EN COMISIÃ¿N O CONSIGNACIÃ¿N DE PRODUCTOS AGRÃ¿COLAS N.C.P. |
| 461021: 85 VENTA AL POR MAYOR EN COMISIÃ¿N O CONSIGNACIÃ¿N DE GANADO BOVINO EN PIE |
| 461022: 86 VENTA AL POR MAYOR EN COMISIÃ¿N O CONSIGNACIÃ¿N DE GANADO EN PIE EXCEPTO BOVINO |
| 461031: 1 OPERACIONES DE INTERMEDIACIÓN DE CARNE - CONSIGNATARIO DIRECTO - |
| 461032: 2 OPERACIONES DE INTERMEDIACIÓN DE CARNE EXCEPTO CONSIGNATARIO DIRECTO |
| 461039: 21 VENTA AL POR MAYOR EN COMISIÓN O CONSIGNACIÓN DE ALIMENTOS, BEBIDAS Y TABACO N.C.P. |
| 461099: 87 VENTA AL POR MAYOR EN COMISIÃ¿N O CONSIGNACIÃ¿N DE  MERCADERÃ¿AS N.C.P. |
| 462110: 88 ACOPIO DE ALGODÃ¿N |
| 462120: 89 VENTA AL POR MAYOR DE SEMILLAS Y GRANOS PARA FORRAJES |
| 462132: 90 ACOPIO Y ACONDICIONAMIENTO DE CEREALES Y SEMILLAS, EXCEPTO DE ALGODÃ¿N Y SEMILLAS Y GRANOS PARA FORRAJES |
| 462190: 91 VENTA AL POR MAYOR DE MATERIAS PRIMAS AGRÃ¿COLAS Y DE LA SILVICULTURA N.C.P. |
| 463121: 4 VENTA AL POR MAYOR DE CARNES ROJAS Y DERIVADOS |
| 463129: 92 VENTA AL POR MAYOR DE AVES, HUEVOS Y PRODUCTOS DE GRANJA Y DE LA CAZA N.C.P. |
| 463191: 93 VENTA AL POR MAYOR DE FRUTAS, LEGUMBRES Y CEREALES SECOS Y EN CONSERVA |
| 463219: 94 VENTA AL POR MAYOR DE BEBIDAS ALCOHÃ¿LICAS N.C.P. |
| 463300: 3 VENTA AL POR MAYOR DE CIGARRILLOS Y PRODUCTOS DE TABACO |
| 464114: 95 VENTA AL POR MAYOR DE TAPICES Y ALFOMBRAS DE MATERIALES TEXTILES |
| 464223: 96 VENTA AL POR MAYOR DE ARTÃ¿CULOS DE LIBRERÃ¿A Y PAPELERÃ¿A |
| 464320: 97 VENTA AL POR MAYOR DE PRODUCTOS COSMÃ¿TICOS, DE TOCADOR Y DE PERFUMERÃ¿A |
| 466110: 98 VENTA AL POR MAYOR DE COMBUSTIBLES Y LUBRICANTES PARA AUTOMOTORES |
| 466330: 99 VENTA AL POR MAYOR DE ARTÃ¿CULOS DE FERRETERÃ¿A Y MATERIALES ELÃ¿CTRICOS |
| 466932: 100 VENTA AL POR MAYOR DE ABONOS, FERTILIZANTES Y PLAGUICIDAS |
| 471190: 101 VENTA AL POR MENOR EN KIOSCOS, POLIRRUBROS Y COMERCIOS NO ESPECIALIZADOS N.C.P. |
| 472130: 5 VENTA AL POR MENOR DE CARNES ROJAS, MENUDENCIAS Y CHACINADOS FRESCOS |
| 473000: 102 VENTA AL POR MENOR DE COMBUSTIBLE PARA VEHÃ¿CULOS AUTOMOTORES Y MOTOCICLETAS |
| 475230: 103 VENTA AL POR MENOR DE ARTÃ¿CULOS DE FERRETERÃ¿A Y MATERIALES ELÃ¿CTRICOS |
| 475250: 104 VENTA AL POR MENOR DE ARTÃ¿CULOS PARA PLOMERÃ¿A E INSTALACIÃ¿N DE GAS |
| 476130: 105 VENTA AL POR MENOR DE PAPEL, CARTÃ¿N, MATERIALES DE EMBALAJE Y ARTÃ¿CULOS DE LIBRERÃ¿A |
| 476400: 106 VENTA AL POR MENOR DE JUGUETES, ARTÃ¿CULOS DE COTILLÃ¿N Y JUEGOS DE MESA |
| 477330: 107 VENTA AL POR MENOR DE INSTRUMENTAL MÃ¿DICO Y ODONTOLÃ¿GICO Y ARTÃ¿CULOS ORTOPÃ¿DICOS |
| 477440: 108 VENTA AL POR MENOR DE FLORES, PLANTAS, SEMILLAS, ABONOS, FERTILIZANTES Y OTROS PRODUCTOS DE VIVERO |
| 477470: 109 VENTA AL POR MENOR DE PRODUCTOS VETERINARIOS, ANIMALES DOMÃ¿STICOS Y ALIMENTO BALANCEADO PARA MASCOTAS |
| 491200: 110 SERVICIO DE TRANSPORTE FERROVIARIO DE CARGAS |
| 492221: 111 SERVICIO DE TRANSPORTE AUTOMOTOR DE CEREALES |
| 492229: 112 SERVICIO DE TRANSPORTE AUTOMOTOR DE MERCADERÃ¿AS A GRANEL N.C.P. |
| 492230: 113 SERVICIO DE TRANSPORTE AUTOMOTOR DE ANIMALES |
| 492240: 114 SERVICIO DE TRANSPORTE POR CAMIÃ¿N CISTERNA |
| 492290: 115 SERVICIO DE TRANSPORTE AUTOMOTOR DE CARGAS N.C.P. |
| 511000: 116 SERVICIO DE TRANSPORTE AÃ¿REO DE PASAJEROS |
| 512000: 117 SERVICIO DE TRANSPORTE AÃ¿REO DE CARGAS |
| 551021: 6 SERVICIOS DE ALOJAMIENTO EN PENSIONES |
| 551022: 7 SERVICIOS DE ALOJAMIENTO EN HOTELES, HOSTERÍAS Y RESIDENCIALES SIMILARES, EXCEPTO POR HORA, QUE INCLUYEN SERVICIO DE RESTAURANTE AL PÚBLICO |
| 551023: 8 SERVICIOS DE ALOJAMIENTO EN HOTELES, HOSTERÍAS Y RESIDENCIALES SIMILARES, EXCEPTO POR HORA, QUE NO INCLUYEN SERVICIO DE RESTAURANTE AL PÚBLICO |
| 551090: 9 SERVICIOS DE HOSPEDAJE TEMPORAL N.C.P. |
| 552000: 10 SERVICIOS DE ALOJAMIENTO EN CAMPINGS |
| 561013: 118 SERVICIOS DE "FAST FOOD" Y LOCALES DE VENTA DE COMIDAS Y BEBIDAS AL PASO |
| 561019: 119 SERVICIOS DE EXPENDIO DE COMIDAS Y BEBIDAS EN ESTABLECIMIENTOS CON SERVICIO DE MESA Y/O EN MOSTRADOR N.C.P. |
| 561030: 120 SERVICIO DE EXPENDIO DE HELADOS |
| 561040: 121 SERVICIOS DE PREPARACIÃ¿N DE COMIDAS REALIZADAS POR/PARA VENDEDORES AMBULANTES. |
| 562010: 122 SERVICIOS DE PREPARACIÃ¿N DE COMIDAS PARA EMPRESAS Y EVENTOS |
| 620100: 123 SERVICIOS DE CONSULTORES EN INFORMÃ¿TICA Y SUMINISTROS DE PROGRAMAS DE INFORMÃ¿TICA |
| 620300: 124 SERVICIOS DE CONSULTORES EN TECNOLOGÃ¿A DE LA INFORMACIÃ¿N |
| 631190: 125 ACTIVIDADES CONEXAS AL PROCESAMIENTO Y HOSPEDAJE DE DATOS N.C.P. |
| 649210: 126 ACTIVIDADES DE CRÃ¿DITO PARA FINANCIAR OTRAS ACTIVIDADES ECONÃ¿MICAS |
| 649220: 127 SERVICIOS DE ENTIDADES DE TARJETA DE COMPRA Y/O CRÃ¿DITO |
| 649999: 128 SERVICIOS DE FINANCIACIÃ¿N Y ACTIVIDADES FINANCIERAS N.C.P. |
| 653000: 129 ADMINISTRACIÃ¿N DE FONDOS DE PENSIONES, EXCEPTO LA SEGURIDAD SOCIAL OBLIGATORIA |
| 661121: 130 SERVICIOS DE MERCADOS A TÃ¿RMINO |
| 681098: 131 SERVICIOS INMOBILIARIOS REALIZADOS POR CUENTA PROPIA, CON BIENES URBANOS PROPIOS O ARRENDADOS N.C.P. |
| 681099: 132 SERVICIOS INMOBILIARIOS REALIZADOS POR CUENTA PROPIA, CON BIENES RURALES PROPIOS O ARRENDADOS N.C.P. |
| 682010: 133 SERVICIOS DE ADMINISTRACIÃ¿N DE CONSORCIOS DE EDIFICIOS |
| 682099: 134 SERVICIOS INMOBILIARIOS REALIZADOS A CAMBIO DE UNA RETRIBUCIÃ¿N O POR CONTRATA N.C.P. |
| 691001: 135 SERVICIOS JURÃ¿DICOS |
| 692000: 136 SERVICIOS DE CONTABILIDAD, AUDITORÃ¿A Y ASESORÃ¿A FISCAL |
| 702091: 137 SERVICIOS DE ASESORAMIENTO, DIRECCIÃ¿N Y GESTIÃ¿N EMPRESARIAL REALIZADOS POR INTEGRANTES DE LOS Ã¿RGANOS DE ADMINISTRACIÃ¿N Y/O FISCALIZACIÃ¿N EN SOCIEDADES ANÃ¿NIMAS |
| 711001: 138 SERVICIOS RELACIONADOS CON LA CONSTRUCCIÃ¿N. |
| 711009: 139 SERVICIOS DE ARQUITECTURA E INGENIERÃ¿A Y SERVICIOS CONEXOS DE ASESORAMIENTO TÃ¿CNICO N.C.P. |
| 712000: 140 ENSAYOS Y ANÃ¿LISIS TÃ¿CNICOS |
| 749009: 141 ACTIVIDADES PROFESIONALES, CIENTÃ¿FICAS Y TÃ¿CNICAS N.C.P. |
| 750000: 142 SERVICIOS VETERINARIOS |
| 771110: 143 ALQUILER DE AUTOMÃ¿VILES SIN CONDUCTOR |
| 772099: 144 ALQUILER DE EFECTOS PERSONALES Y ENSERES DOMÃ¿STICOS N.C.P. |
| 773010: 145 ALQUILER DE MAQUINARIA Y EQUIPO AGROPECUARIO Y FORESTAL, SIN OPERARIOS |
| 791100:  11 SERVICIOS MINORISTAS DE AGENCIAS DE VIAJES |
| 791200:  12 SERVICIOS MAYORISTAS DE AGENCIAS DE VIAJES |
| 791901:  13 SERVICIOS DE TURISMO AVENTURA |
| 791909:  14 SERVICIOS COMPLEMENTARIOS DE APOYO TURÍSTICO N.C.P. |
| 813000:  146 SERVICIOS DE JARDINERÃ¿A Y MANTENIMIENTO DE ESPACIOS VERDES |
| 821100:  147 SERVICIOS COMBINADOS DE GESTIÃ¿N ADMINISTRATIVA DE OFICINAS |
| 841100: | 148 SERVICIOS GENERALES DE LA ADMINISTRACIÃ¿N PÃ¿BLICA |
| 841900: | 149 SERVICIOS AUXILIARES PARA LOS SERVICIOS GENERALES DE LA ADMINISTRACIÃ¿N PÃ¿BLICA |
| 842100: | 150 SERVICIOS DE ASUNTOS EXTERIORES |
| 853100: | 151 ENSEÃ`ANZA  TERCIARIA |
| 854920: | 152 ENSEÃ`ANZA DE CURSOS RELACIONADOS CON INFORMÃ¿TICA |
| 880000: | 153 SERVICIOS SOCIALES SIN ALOJAMIENTO |
| 900011: | 154 PRODUCCIÃ¿N DE ESPECTÃ¿CULOS TEATRALES Y MUSICALES |
| 900040: | 155 SERVICIOS DE AGENCIAS DE VENTAS DE ENTRADAS |
| 949920: | 156 SERVICIOS DE CONSORCIOS DE EDIFICIOS |
| 949990: | 157 SERVICIOS DE ASOCIACIONES N.C.P. |
| 960300: | 158 POMPAS FÃ¿NEBRES Y SERVICIOS CONEXOS |
| 960990: | 159 SERVICIOS PERSONALES N.C.P |
## Novedades

Se recuerda que esta disponible el 
[grupo de noticias](http://www.pyafipws.com.ar) (http://groups.google.com.ar/group/pyafipws) donde
se publicarán futuras novedades sobre PyAfipWS: servicios web de
factura electrónica y sus interfases (se recomienda suscribirse)

## Costos y Condiciones

Como este servicio web tiene varias modalidades (CAE normal y CAE anticipado), entre otros cambios, se recomienda consultar previamente.

(ver [Condiciones del Soporte Comercial](../documentacion_herramientas/pyafipws.md#costos-y-condiciones)).

Ofrecemos soporte técnico comercial (pago), independiente a la AFIP, desarrollos especiales, interfaces web, etc. 
Obtenga mas información enviando un mail a info@pyafipws.com.ar o (011) 4450-0716 / (011) 15-3048-9211 (asesoramiento sin cargo)

A su vez, se liberará el código fuente bajo licencia GPLv3 (software libre), al igual que se hizo con el restos de los servicios web. Para más detalles ver página FacturaElectronica.

La información de esta página es proporcionada a titulo informativo.

2008-2022 © MarianoReingart


**[Colaboraciones](https://link.mercadopago.com.ar/colaboracionespyafip)**
