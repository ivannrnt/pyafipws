= Liquidación y Certificación de Granos (RG3419/2012, RG3690/2014, RG3691/2014) =

[[TracNav(noreorder|FacturaElectronica)]]

Interfaz para Servicio Web correspondiente a la Resolución General 3419/2012 AFIP: régimen especial obligatorio para la emisión electrónica de la “Liquidación Primaria de Granos” para respaldar las operaciones de compraventa y de consignación de granos no destinados a la siembra y legumbres secas que realicen, a productores agrícolas, los adquirentes, adquirentes-exportadores, acopiadores, cooperativas, consignatarios, acopiadores-consignatarios, demás intermediarios y los mercados de cereales a término. 

Aplicativo Formularios C 1116 B o C - Registración de las operaciones de compraventa de granos no destinados a la siembra -cereales y oleaginosos-, y legumbres secas -porotos, arvejas y lentejas

RG 3690/2014 AFIP: Operaciones De Compraventa De Granos No Destinados A La Siembra. "Liquidación Secundaria de Granos"

RG 3691/2014 AFIP: "Certificación Primaria de Depósito, Retiro y/o Transferencia de Granos" no destinados a la siembra.
## Índice
[[Image(htdocs:logo-pyafipws.png, align=right)]]
[[TOC(noheading,inline,depth=2)]]
## Descripción General

EL WSLPG (Web Service de Liquidación Primaria de Granos) es un nuevo Servicio Web de la AFIP para operaciones de compra/venta de granos, correspondiente a la [Resolución General 3419/12](http://biblioteca.afip.gob.ar/gateway.dll/Normas/ResolucionesGenerales/reag01003419_2012_12_20.xml): *Operaciones de compraventa de granos no destinados a la siembra. Régimen de emisión de comprobantes. Norma conjunta Resolución General Nº 1.593 (AFIP) y Resolución Nº 456 (ex SAGPyA), Resoluciones Generales Nº 1.415, Nº 2.205 y Nº 2.485, sus respectivas modificatorias y complementarias. Norma complementaria y modificatoria.*

**Nuevo**: Generación electrónica del formulario de liquidación de granos en formato PDF. Ver [Generación F1116B en PDF](wiki:LiquidacionPrimariaGranos#GeneraciónFormC1116BenPDF). Basado en el anexo *RG.3419-12 - MODELO - Liquidación Primaria de Granos* (similar al obtenido del aplicativo SIAP F1116_v2r0).

**Importante**: este webservice utiliza un *número de orden* (similar al número de comprobante en factura electrónica), por lo que la primer liquidación debe comenzar por 1, y debe informarse secuencialmente el próximo número (sin saltear números, incrementando el valor siempre que la liquidación sea autorizada correctamente). Ver *Tratamiento del No de Orden* en la documentación de AFIP, ya que es necesario para recuperar los datos de una liquidación en caso de perdida de conexión (método `ConsultarLiquidacion`). También se puede consultar el último número registrado (método `ConsultarUltNroOrden`, aunque en producción se recomienda almacenar el numero internamente).

Esta interfaz se encarga automáticamente de todos los aspectos de la comunicación con los webservices de AFIP (SOAP, XML, encriptación SSL, autenticación por certificado/clave privada - ticket de acceso WSAA-, etc.).
### Novedades

Al 22-02-2013, el servicio WSLPG estaba en etapa de desarrollo:

- Servidor de homologación: al 9 de Marzo de 2013 entro en operación la versión WSLPGv1.1 en pruebas
- Servidor de producción: al 13 de Marzo de 2013 (fecha de aplicación), el servidor para producción esta habilitado

#### Ajustes WSLPGv1.4

~~Según AFIP, al 31-05-2013 algunos métodos están todavía en estudio (principalmente Ajustar Liquidación)~~

Al 29-07-2013, ya se encuentra disponible los metodos de ajustes tentativos según "WEB SERVICE !LpgService Versión 1.4 Manual para el Desarrollador" (en homologación), para los cuales llegó la siguiente comunicación de AFIP:

   ''Estimados desde el día 12/07/2013 se encuentra a disposición el testing ws, para así poder
   probar en detalle las nuevas funcionalidades de las liquidaciones de ajuste.''

   ''El testing publicado contempla el Ajuste Unificado (Débito/Crédito) por COE, la nueva 
   versión del manual referido al mismo, se encontrará disponible a la brevedad.  
   http://www.afip.gob.ar/ws/#WSLiquiGranos
   Las consultas específicas de Liquidación Primaria de Granos realizadas por sistema webservices 
   podrán canalizarse a través de la cuenta wslpg@afip.gob.ar.''

   ''La unificación de los ajustes por crédito y débito, resulta en esta etapa de aplicación para
   aquellos contratos con  UNA UNICA PARCIAL. ''

   ''Sólo está disponible mediante el uso de WEB SERVICES (no se pueden hacer pruebas 
   por carga manual), por lo que les solicitamos que realicen pruebas a fin de informar las
   inconsistencias.''

   ''En una segunda etapa se habilitará el sistema para cerrar VARIAS PARCIALES  en una
   FINAL por CONTRATO REGISTRADO ANTE AFIP.''

A partir de la actualización 1.12 de la interfaz, se incluyen los métodos necesarios para utilizar esta nueva funcionalidad ver abajo sección [Métodos](wiki:LiquidacionPrimariaGranos#Metodos).

La información también aplica a WSLPG versión 1.5 ya que hubo solo cambios menores.

#### Liquidación Secundaria y Certificación de Granos WSLPGv1.6

El 22/10/2014 AFIP ha publicado las siguientes resoluciones generales:

- [RG 3690/14](http://www.infoleg.gob.ar/infolegInternet/anexos/235000-239999/236819/norma.htm): **"Liquidación Secundaria de Granos"** 
- [RG 3691/14](http://www.infoleg.gob.ar/infolegInternet/anexos/235000-239999/236821/norma.htm): **"Certificación Primaria de Depósito, Retiro y/o Transferencia de Granos"** (ex. formularios C1116A y C11116RT)

Según AFIP, al 14/11/2014 todos los métodos son preliminares , solo se encuentra disponible la documentación técnica tentativa ["WEB SERVICE LpgService Versión 1.6 Manual para el Desarrollador"](http://www.afip.gob.ar/ws/WSLiquiGranos/ManualDelDesarrolladorWSLPGV16.pdf). 
Todavía no estan disponible los cambios en el webservice, ni hay ejemplos como para poder probar el servicio. 

A partir de la actualización 1.17 de la interfaz, se están incorporando los métodos necesarios para utilizar estas nueva funcionalidades ver abajo secciones [Versión 1.6](wiki:LiquidacionPrimariaGranos#Version1.6) con [Métodos](wiki:LiquidacionPrimariaGranos#Metodos), [Formato de Intercambio](wiki:LiquidacionPrimariaGranos##FormatodeIntercambio) y ejemplos ([Autorizar Liquidación Secundaria](wiki:LiquidacionPrimariaGranos#AutorizarLiquidaciónSecundaria), [Autorizar Certificación](wiki:LiquidacionPrimariaGranos#AutorizarCertificación)).


### Versión 1.1

El Viernes 08-03-2013, AFIP publicó una nueva versión del webservices denominanda *"Liquidación Primaria Electrónica de Granos - WEB SERVICE !LpgService - Versión 1.1* contemplando ajustes menores en operatoria (punto de emision) y nuevos casos de uso (liquidaciones por canje total -sin retenciones-  y también sin certificado de depósito).

Campos agregdos a nivel general de la liquidación:

- `pto_emision`: Punto de Emisión asociado a la liquidación, No de orden. Junto con el nro_orden identifica de forma única a una solicitud de COE (permite emitir liquidaciones simultaneamente desde distintos puntos de operación)
- `peso_neto_sin_certificado`: Peso Neto del grano a liquidar. Solamente se deberá informar si no se envía <certificados>
- `cod_prov_procedencia`: Provincia de procedencia 

Debido a estos cambios, se han modificado los métodos !CrearLiquidacion, !ConsultarLiquidacion y !ConsultarUltNroOrden.

Estos ajustes están disponibles a partir de la actualización 1.03a de la interfaz.
Dado que los cambios introducidos por AFIP son incompatibles hacia atrás, con versiones anteriores recibirá los siguientes errores desde el servidor de AFIP:

- `cvc-complex-type.2.4.a:  Se encontró contenido inválido en el elemento 'nroOrden'. Se espera '{ptoEmision}'.`
- `cvc-complex-type.2.4.a:  Se encontró contenido inválido en el elemento 'datosAdicionales'. Se espera '{codProvProcedencia}'.`
- `cvc-complex-type.2.4.b:  El contenido del elemento 'wslpg:liqConsXNroOrdenReq' no es completo. Se espera '{nroOrden}'.`


### Version 1.2

El Viernes 27-03-2013, AFIP publicó una nueva versión del webservices denominanda *"Liquidación Primaria Electrónica de Granos - WEB SERVICE !LpgService - Versión 1.2* contemplando ajustes menores:

- ajustes en los tipos de datos (precio_kg_diario ahora soporta hasta 8 decimales, aunque actualmente el servidor solo acepta 4; datos_adicionales fue limitado a 200 caracteres y detalle_deduccion 50 caracteres)
- se eliminó la validación 1100, se agregaron las validaciones 800, 1502, 1521, 1524, 1526, 1527, 1528, 1645, 1711, 1714, 1819, 1858
- la operatoria de ajustes se encuentra bajo análisis. Se implementará en una versión posterior.

### Version 1.3

El Martes 09-04-2013, AFIP publicó una nueva versión del webservices denominanda *"Liquidación Primaria Electrónica de Granos - WEB SERVICE !LpgService - Versión 1.3* contemplando ajustes menores:

- se agregó campos `cod_prov_procedencia_sin_certificado` y `cod_localidad_procedencia_sin_certificado`
- se eliminó la validación 1703, se agregaron las validaciones 1529, 1646, se modificaron 1858, 1854

### Version 1.4

El Viernes 12-07-2013, AFIP publicó una nueva versión del webservices denominanda *"Liquidación Primaria Electrónica de Granos - WEB SERVICE !LpgService - Versión 1.4*, en testing (todavía no habilitado en producción ni por servicios web interactivos / clave fiscal), contemplando los siguientes cambios:

- se agregó los métodos `AjustarLiquidacionUnificada` (por COE), `AjustarLiquidacionUnificadaPapel` (por N° F1116B/C) y `AjustarLiquidacionContrato` (por n° de contrato)
- se agregaron estructuras de datos `AjusteBase`, `AjusteCredito` y `AjusteDebito`, las cuales varía levemente según el tipo de ajuste (ver métodos auxiliares `CrearAjusteBase`, `CrearAjusteCredito`, y `CrearAjusteDebito`)
- se agregaron atributos Subtotal, !TotalIva105, !TotalIva21, !TotalRetencionesGanancias, !TotalRetencionesIVA: importe totales / generales del ajuste (ver totalesUnificados en la documentación de AFIP)
- se agregó parámetro `nro_contrato` en el método `CrearLiquidacion` (dato ulizado para ajustes)
- se eliminó el método `AjustarLiquidación`
- se agregó métodos: `AsociarLiquidacionAContrato`, `ConsultarLiquidacionesPorContrato`, `ConsultarAjuste` y los respectivos parametros `--asociar`, `--consultar_por_contrato`, `--consultar_ajuste`

~~ Al 2-09-2013, la documentación oficial definitiva no se encuentra publicada. ~~ la documentación oficial para WSLPGv1.4 fué publicada definitivamente el 25/07/2013 

### Version 1.5

El 02/10/2013, AFIP publicó una nueva versión del webservices denominanda *"Liquidación Primaria Electrónica de Granos - WEB SERVICE !LpgService - Versión 1.5*, contemplando los siguientes cambios:

- se agrego campo `nro_contrato` a la respuesta de  `AutorizarLiquidacion`
- se agrego campos `iva_deducciones`, `subtotal_deb_cred`, `total_base_deducciones` en la resupuesta de los Ajustes
- se agrego campo `cod_localidad` y `cod_provincia` en `CrearAjusteBase`
- se agrego los métodos `AsociarLiquidacionAContrato`, `ConsultarAjuste` (por nro_contrato, coe y nro de orden), `ConsultarLiquidacionesPorContrato`
- se eliminó el método `AjustarLiquidacionUnificadoPapel`

La mayoría de los cambios fueron introducidos en la versión 1.4 de manera provisoria y no documentada, por lo que están soportados en la interfaz desde la actualización 1.13 y en general no es necesario actualizar la versión de la interfaz.

Entre las validaciones más importantes que se modificaron en AFIP se encuentra la eliminación del código de error *1645: "Si informa certificados, informar como máximo uno."*, por lo que ahora es posible agregar más de un certificado de depósito por liquidación (soportado por esta interfaz desde el comienzo, por lo que tampoco es necesario actualizar la versión).
### Version 1.6

El 10/11/2014, AFIP publicó una nueva versión del webservices denominanda *"Certificación y Liquidación de Granos  WEB SERVICE LpgService Versión 1.6*, contemplando nuevos métodos

- Para [Liquidación Secundaria de Granos](wiki:LiquidacionPrimariaGranos#LiquidaciónSecundariadeGranos) (RG3690/14) se agregaron los métodos `CrearLiqSecundariaBase` (estructura interna) y `AutorizarLiquidacionSecundaria` (llamada remota). Se utiliza los campos generales del tipo de registro [Encabezado](wiki:LiquidacionPrimariaGranos#Encabezado) (Liquidación), sumados a `cantidad_tn`, `nro_act_vendedor`, `detalle_deducciones`, `importe_deducciones`
- Para [Certificación de Depósitos Retiros y Transferencias de Granos](wiki:LiquidacionPrimariaGranos#CertificacióndeDepósitosRetirosyTransferenciasdeGranos) (RG3691/14): se agregaron métodos: `CrearCertificacion`, `AgregarDetalleMuestraAnalisis`, `AgregarCTG` (estructuras internas);  `AutorizarDeposito`, `AutorizarRetiroTransferencia`, `AutorizarPreexistente` (llamadas remotas). Al archivo de intercambio se agregan los tipos de registro [Certificación](wiki:LiquidacionPrimariaGranos#Certificacion), [CTG](wiki:LiquidacionPrimariaGranos#CTG) y [Detalle Muestra Analisis](wiki:LiquidacionPrimariaGranos#Det.MuestraAnalisis).

### Version 1.7

AFIP publicó una nueva versión del webservices denominanda *"Certificación y Liquidación de Granos  WEB SERVICE LpgService Versión 1.7*, contemplando las modificaciones hechas al WSDL: metodo unificado para autorizar certificaciones y cambios en los campos ("retroactiva" al 26-11-2014): 

**Importante**: Cambios en el WSDL (no documentados en la especificación técnica hasta el 1/12/2014 WSLPGv1.7):

- 25-11-2014: los métodos documentados `cgAutorizarDeposito`, `cgAutorizarRetiroTransferencia`, `cgAutorizarPreexistente` han sido reemplazados por cgAutorizar  en el WSDL (juntando las estructuras de datos)
- 28-11-2014: se eliminó `peso_neto_a_certificar` y se agregó `nro_carta_porte` en la estructura CTG (para autorizar certificaciones de depósito)

Próximamente se agregarán el resto de los métodos, estructuras de datos y ejemplos ([Autorizar Liquidación Secundaria](wiki:LiquidacionPrimariaGranos#AutorizarLiquidaciónSecundaria), [Autorizar Certificación](wiki:LiquidacionPrimariaGranos#AutorizarCertificación)).

### Version 1.8

AFIP publicó una nueva versión del webservices denominanda *"Certificación y Liquidación de Granos  WEB SERVICE LpgService Versión 1.8*, contemplando las modificaciones hechas al WSDL: metodo unificado para autorizar certificaciones y cambios en los campos (con fecha del 18-02-2015): 

**Importante**: Ajustes debido a cambios en el WSDL (no documentados en la especificación técnica hasta el 19/2/2015 WSLPGv1.8):

- Certificacion de Granos (CG):
- método `AgregarCertificacionPlantaDepositoElevador` -> `AgregarCertificacionPrimaria` (p/ cambio estructura)
- campo `nro_act_depositario` agregado en formato CERTIFICACION Primaria y R/T (nuevo parámetro)
- campo `cac_certificado_deposito_preexistente` renombrado en formato CERTIFICACION preexistente
- campo `peso_neto_confirmado_definitivo` agregado en formato CTG (nuevo parámetro)
- solo se permite un certificado en autorizacion de R/T
- cambio parametros `--deposito` -> `--primaria` en pruebas (línea de comandos)
- valor "D:en Deposito y/o Elevador" para campo tipo_certificado eliminado (ahora sólo "P: Primaria")
- Liquidación Secundaria de Granos (LSG):
- método `AgregarDeduccion` ajustados (solo se utilizan campos `detalle_aclaratorio`, `base_calculo` y `alicuota` de IVA)
- métodos `AgregarPercepcion`, `AgregarOpcional` agregados

### Version 1.9

AFIP publicó una nueva versión del webservices denominanda *"Certificación y Liquidación de Granos  WEB SERVICE LpgService Versión 1.9*, contemplando algunas modificaciones menores a la documentación y ejemplos xml (con fecha del 24-02-2015)


### Version 1.10

AFIP publicó una nueva versión del webservices denominanda *"Certificación y Liquidación de Granos  WEB SERVICE LpgService Versión 1.10*, contemplando algunas modificaciones menores (con fecha del 12-03-2015)

Ya esta disponible la nueva actualización 1.23a de nuestra herramienta para WSLPGv1.10 que introduce el nuevo formato de registro para "calidad" (tipo_reg "Q", nuevo parámetro `--informar-calidad`, nuevo método `AgregarCalidad` y se modificó `AgregarCertificacionPrimaria`.

### Version 1.11

AFIP publicó una nueva versión del webservices denominanda *"Certificación y Liquidación de Granos  WEB SERVICE LpgService Versión 1.11*, contemplando algunas modificaciones menores (con fecha del 10-04-2015)

Ya esta disponible la nueva actualización 1.25a de nuestra herramienta para WSLPGv1.11 que agrega el parámetro *PDF* a los métodos de consulta para descargar el documento generado por AFIP, e introduce ajustes menores a la estructura de "calidad":

- `cod_grado` opcional
- `valor_cont_proteico` permite 0
- `valor_factor` opcional

También AFIP ha modificado algunas validaciones de negocio.

Próximamente se agregarán el resto de los métodos, estructuras de datos y ejemplos ([Autorizar Liquidación Secundaria](wiki:LiquidacionPrimariaGranos#AutorizarLiquidaciónSecundaria), [Autorizar Certificación](wiki:LiquidacionPrimariaGranos#AutorizarCertificación)).

### Version 1.15

AFIP publicó una nueva versión del webservices denominanda *"Certificación y Liquidación de Granos  WEB SERVICE LpgService Versión 1.15*, contemplando algunas modificaciones menores (con fecha del 06-07-2015)

A partir de la actualización 1.27a de nuestra herramienta para WSLPGv1.15 que agrega los métodos de ajuste, asociación y consulta por contrato para Liquidaciones Secundarias de Granos.

Se agrega el método `AgregarFacturaPapel` para "migrar" liquidaciones preexistentes en papel (método principal `AutorizarLiquidacionSecundaria`), con la siguiente estructura:

- `nro_cai`
- `nro_factura_papel`
- `fecha_factura`
- `tipo_comprobante`

También AFIP ha modificado algunas validaciones de negocio, ampliación de algunos campos (servicios_otros y servicios_gastos_generales), entre otras cuestiones.

Ya esta disponible la nueva actualización 1.28a de nuestra herramienta para WSLPGv1.15 que agrega los métodos de anticipo (método principal `AutorizarAnticipo`) y campos no documentados aún por AFIP para CG: Certificaciones de Granos (`servicios_conceptos_no_gravados`, `servicios_percepciones_iva`, `servicios_otras_percepciones`).

### Version 1.16

AFIP publicó una nueva versión del webservices denominanda *"Certificación y Liquidación de Granos  WEB SERVICE LpgService Versión 1.16*, contemplando algunas modificaciones menores (con fecha del 02/02/2016) con los siguientes cambios:

- Envío de percepciones en el método liquidacionAutorizar.
- Envío de deducciones en el método lpgAutorizarAnticipo.

En principio se agregaron percepciones en la LPG, pero no son obligatorias, y tampoco hay una nueva validación al respecto.
Si vuelve una estructura de percepciones es para la respuesta (por eso falla si no se regeneran los archivos temporales de la carpeta cache).
Lo mismo pasaría con las nuevas deducciones en los anticipos.

Ya esta disponible la nueva actualización 1.29a de nuestra herramienta que básicamente se habilitan los métodos:

- `AgregarPercepcion(codigo_concepto, detalle_aclaratoria, base_calculo, alicuota, importe_final)`
- `AgregarDeduccion(codigo_concepto, detalle_aclaratorio, dias_almacenaje, precio_pkg_diario, comision_gastos_adm, base_calculo, alicuota)`

De la percepción solo se usa detalle_aclaratoria e importe_final (por ahora según la descripción del servicio web de AFIP)

### Version 1.17

AFIP publicó una nueva versión del webservices denominanda *"Certificación y Liquidación de Granos  WEB SERVICE LpgService Versión 1.17*, contemplando algunas modificaciones menores (con fecha del 16/06/2017) con los siguientes cambios:

Ya esta disponible la nueva [actualización 1.30a](wiki:LiquidacionPrimariaGranos#Descargas) de nuestro componente que básicamente modifica los métodos para soportar peso_ajustado:

- `AgregarCertificado(..., peso_neto, ..., coe_certificado_deposito, ...)` ahora puede ser llamado luego de `CrearAjusteCredito` / `CrearAjusteDebito`
- Idem en archivo de intercambio (lectura/escritura), tipo de registro 1 luego de tipo_reg 4/5
- Datos de prueba básica, validación "1921: El certificado que esta en un ajuste de crédito no puede estar en uno de débito y viceversa"

### versión 1.19

Se agrega Fusion en ajustes (LPG/LSG):

- Nuevo método AgregarFusion (nro_ing_brutos, nro_actividad), llamar luego de CrearAjusteBase (afecta a AjustarLiquidacionUnificado/AjustarLiquidacionSecundaria)
- Nuevo tipo de registro 'f' para FUSION (archivo de intercambio TXT / tablas DBF)
- Datos de pruebas genericos para --ajustar --prueba

### Versión 1.20

AFIP publicó una nueva versión del webservices denominanda *"Certificación y Liquidación de Granos  WEB SERVICE LpgService Versión 1.20* (con fecha del 04/12/2018) con los siguientes cambios:

- Se reemplazan los campos de referencia a la RG 2300/2017 por RG 4310/2018
- Campo totalIVARG2300_07 es reemplazado por totalIvaRg4310_18 en el método Autorizar Liquid


### WSLPGv1.22

El 12/03/2021 AFIP publica el reemplazo del método lsgAnular por lsgAnularContraDocumento.
El nuevo procedimiento anula la liquidación original generando una nueva liquidación como contra documento. 
La anulación se corresponde a un ajuste unificado con la misma información que la liquidación anulada.

### Versión 1.23

Con fecha 30/09/2021 AFIP publica la versión 1.23 del webservice.
Se modifica la longitud de los campos nro_carta_porte y nro_ctg
AFIP incorpora el valor posible “CPE” para tipoCTG


### Datos de Prueba

El juego de datos para homologación, así como la simulación del CUIT para actividades habilitadas, se deben solicitar a wslpg@afip.gov.ar. 
A continuación se copia la nota recibido a modo de ejemplo.

Se pueden utilizar las siguientes CUIT genéricas para los diferentes roles (excepto para el que liquida)
 
#### Vendedor

| CUIT | RFOG | IVA/ Monotributo / Ganancias |
|---|---|---|
| 23000000000 | Activo RFOG | IVA y Gan |
| 23000000019 | No activo RFOG | IVA y Gan |
| 23000000027 | --- | Monotributo |
| 23000000035 | --- | Monotributo |

#### Comprador

| CUIT | IVA/Monotributo | RUOCA |
|---|---|---|
| 27000000014 | IVA | 28 - Acondicionador |
| 20400000000 | IVA | 40 – Exportador |

#### Corredor

| CUIT | IVA/ Monotributo | RUOCA |
|---|---|---|
| 20200000006 | IVA | 36 - Corredor |
#### Certificados de Depósito

| F1116 A | 555501200729 |
|---|---|
| F1116 RT | 111101200729 |

*Nota:* esos numeros de certificado ya estan usados y vinculados a liquidaciones en homologación, recuerde solicitar nuevos números de certificados de depósito a wslpg@afip.gov.ar
 
#### Numero de Contrato

| nro_contrato | Vendedor | Comprador | Corredor | Grano | Peso |
|---|---|---|---|---|---|
| 26 | 23000000019 | 20400000000 | 20267565393 | 31 | 1000000 |
| 27 | 23000000019 | 20400000000 | 20267565393 | 31 | 1000000 |
| 28 | 23000000019 | 20400000000 | 20267565393 | 31 | 1000000 |

*Nota:* esos numeros de contrato ya estan usados y vinculados a liquidaciones en homologación para el CUIT 20267565393, recuerde solicitar nuevos números de contratos a wslpg@afip.gov.ar
## Descargas

- Instalador: *consultar por instalador unificado e integrado para evaluación de todos los webservices*
- [PyAfipWs-2.7.1982-32bit+wsaa_2.11c+wsctgv4_1.14a+wslpg_1.30a-homo.exe](https://www.sistemasagiles.com.ar/soft/pyafipws/PyAfipWs-2.7.1982-32bit+wsaa_2.11c+wsctgv4_1.14a+wslpg_1.30a-homo.exe) LPG, LSG y CG WSLPGv1.17 + CTGv4 (versión experimental para desarrollo en homologación ***recomendado***)
- [PyAfipWs-2.7.1982-32bit+wsaa_2.11c+wslpg_1.30a-homo.exe](https://www.sistemasagiles.com.ar/soft/pyafipws/PyAfipWs-2.7.1982-32bit+wsaa_2.11c+wslpg_1.30a-homo.exe): LPG WSLPGv1.17
- Documentación: 
- Especificación técnica oficial AFIP: [WSLPG original](http://www.afip.gov.ar/ws/WSLiquiGranos/ManualDelDesarrolladorWSLPGV1.pdf), [WSLPGv1.1](http://www.afip.gov.ar/ws/WSLiquiGranos/ManualDelDesarrolladorWSLPGV11.pdf),  [WSLPGv1.2](http://www.afip.gov.ar/ws/WSLiquiGranos/ManualDelDesarrolladoWSLPGV12.pdf), [WSLPGv1.3](http://www.afip.gov.ar/ws/WSLiquiGranos/ManualDelDesarrolladoWSLPGV13.pdf), [WSLPGv1.4](http://www.afip.gov.ar/ws/WSLiquiGranos/ManualDelDesarrolladorWSLPGV14.pdf), [WSLPGv1.5](http://www.afip.gov.ar/ws/WSLiquiGranos/ManualDelDesarrolladorWSLPGV15.pdf), [WSLPGv1.6](http://www.afip.gov.ar/ws/WSLiquiGranos/ManualDelDesarrolladorWSLPGV16.pdf), [WSLPGv1.7](http://www.afip.gov.ar/ws/WSLiquiGranos/ManualDelDesarrolladorWSLPGV17.pdf), [WSLPGv1.8](http://www.afip.gov.ar/ws/WSLiquiGranos/ManualDelDesarrolladorWSLPGV18.pdf), [WSLPGv1.9](http://www.afip.gov.ar/ws/WSLiquiGranos/ManualDelDesarrolladorWSLPGV19.pdf), [WSLPGv1.10](http://www.afip.gov.ar/ws/WSLiquiGranos/ManualDelDesarrolladorWSLPGV110.pdf), [WSLPGv1.11](http://www.afip.gov.ar/ws/WSLiquiGranos/ManualDelDesarrolladorWSLPGV111.pdf), [WSLPGv1.15](http://www.afip.gob.ar/ws/WSLiquiGranos/manual_wslpg_1.15.pdf), [WSLPGv1.16](http://www.afip.gob.ar/ws/WSLiquiGranos/manual_wslpg_1.16.pdf), [WSLPGv1.17](http://www.afip.gob.ar/ws/WSLiquiGranos/manual_wslpg_1.17.pdf), [WSLPGv1.18](http://www.afip.gob.ar/ws/WSLiquiGranos/manual_wslpg_1.18.pdf), [WSLPGv1.19](http://www.afip.gob.ar/ws/WSLiquiGranos/manual_wslpg_1.19.pdf), [WSLPGv1.22](https://www.afip.gob.ar/ws/WSLiquiGranos/manual_wslpg_1.22.pdf), [WSLPGv1.23](https://www.afip.gob.ar/ws/WSLiquiGranos/manual_wslpg_1.23.pdf),

- [Manual de Uso](wiki:ManualPyAfipWs): Documentación genérica de la interfaz ([PDF](http://www.sistemasagiles.com.ar/trac/wiki/ManualPyAfipWs?format=pdf))
- Ejemplos: *consultar por otros lenguajes*
- [wslpg.bas](https://github.com/reingart/pyafipws/blob/master/ejemplos/wslpg/wslpg.bas) Liquidación Primaria de Granos (Visual Basic)
- [wslpg_ajuste_unif.bas](https://github.com/reingart/pyafipws/blob/master/ejemplos/wslpg/wslpg_ajuste_unif.bas) Ajuste Unificado (Visual Basic)
- [wslpg_ajuste_contrato.bas](https://github.com/reingart/pyafipws/blob/master/ejemplos/wslpg/wslpg_ajuste_contrato.bas) Ajuste Contrato (Visual Basic)
- [wslpg_ajuste_pdf.bas](https://github.com/reingart/pyafipws/blob/master/ejemplos/wslpg/wslpg_ajuste_pdf.bas) PDF Ajuste (Visual Basic)
- [lsg.bas](https://github.com/reingart/pyafipws/blob/master/ejemplos/wslpg/lsg.bas) Liquidación Secundaria de Granos (Visual Basic)
- [cg.bas](https://github.com/reingart/pyafipws/blob/master/ejemplos/wslpg/cg.bas) Certificación de Granos: F1116A / F1116RT (Visual Basic)
- [wslpg.prg](https://github.com/reingart/pyafipws/blob/master/ejemplos/wslpg/wslpg.prg) Liquidación Primaria de Granos (Visual Fox Pro) 
- [cg.prg](https://github.com/reingart/pyafipws/blob/master/ejemplos/wslpg/cg.prg) Certificación de Granos: Form.C1116A y Form.C1116RT (Visual Fox Pro)  
- [lsg.prg](https://github.com/reingart/pyafipws/blob/master/ejemplos/wslpg/lsg.prg) Liquidación Secundaria de Granos (Visual Fox Pro) 
- [ajuste_lsg.bas](https://github.com/reingart/pyafipws/blob/master/ejemplos/wslpg/ajuste_lsg.bas) Ajuste de Liquidación Secundaria de Granos (Visual Basic)
- Archivos de intercambio (muestras): 
- [entrada_wslpg.txt](attachment:entrada_wslpg.txt) y [salida_wslpg.txt](attachment:salida_wslpg.txt) -liquidación primaria- (Cobol y otros, simil SIAP)
- [entrada_wslpg_ajuste_unif.txt](attachment:entrada_wslpg_ajuste_unif.txt) y [salida_wslpg_ajuste_unif.txt](attachment:salida_wslpg_ajuste_unif.txt) -ajuste unificado- (Cobol y otros, simil SIAP)
- [entrada_wslpg_ajuste_contrato.txt](attachment:entrada_wslpg_ajuste_contrato.txt) y [salida_wslpg_ajuste_contrato.txt](attachment:salida_wslpg_ajuste_contrato.txt) -ajuste por contrato- (Cobol y otros, simil SIAP)
- [entrada_wslpg_lsg.txt](attachment:entrada_wslpg_lsg.txt) -liquidación secundaria- (Cobol y otros, simil SIAP)
- [entrada_wslpg_cg_f1116a.txt](attachment:entrada_wslpg_cg_f1116a.txt) -certificación de deposito F1116A- (Cobol y otros, simil SIAP)
- [entrada_wslpg_cg_f1116rt.txt](attachment:entrada_wslpg_cg_f1116rt.txt) -certificación de deposito F1116RT- (Cobol y otros, simil SIAP)
- [entrada_wslpg_cg_pre.txt](attachment:entrada_wslpg_cg_preexistente.txt) -certificación de deposito preexistente- (Cobol y otros, simil SIAP)
- [wslpg_dbf.zip](attachment:wslpg_dbf.zip) -liquidación primaria- (dBase, !FoxPro, Clipper, Harbour)
- [wslpg_dbf_lsg.zip](attachment:wslpg_dbf_lsg.zip) -liquidación secundaria- (dBase, !FoxPro, Clipper, Harbour)
- [wslpg_dbf_cg.zip](attachment:wslpg_dbf_cg.zip) -certificación de granos- (dBase, !FoxPro, Clipper, Harbour)
- [wslpg.json](attachment:wslpg.json) (PHP y !JavaScript)
- Código Fuente (Python): [wslpg.py](https://github.com/reingart/pyafipws/blob/master/wslpg.py)

## Metodos

### Generales

Metodos comunes para establecer comunicación con el webservice y realizar pruebas básicas:

- **`Conectar(cache=None, url="", proxy="", wrapper="", cacert="")`**: en homologación no hace falta pasarle ningùn paràmetro. En producciòn, el segudo parametro es la WSDL.
- **`Dummy()`**: devuelve estado de servidores

### Liquidación Primaria de Granos

Métodos para autorizar, consultar y anular LPG según RG3419 (incluyendo anticipos y su cancelación):

- **`CrearLiquidacion(nro_orden, cuit_comprador, nro_act_comprador, nro_ing_bruto_comprador, cod_tipo_operacion, es_liquidacion_propia, es_canje, cod_puerto, des_puerto_localidad, cod_grano, cuit_vendedor, nro_ing_bruto_vendedor, actua_corredor, liquida_corredor, cuit_corredor, comision_corredor, nro_ing_bruto_corredor, fecha_precio_operacion, precio_ref_tn, cod_grado_ref, cod_grado_ent, factor_ent, precio_flete_tn, cont_proteico, alic_iva_operacion, campania_ppal, cod_localidad_procedencia, datos_adicionales, pto_emision, cod_prov_procedencia, peso_neto_sin_certificado, val_grado_ent, cod_localidad_procedencia_sin_certificado, cod_prov_procedencia_sin_certificado, nro_contrato)`**: crea una liquidación  a autorizar. Parámetros `pto_emision` y `cod_prov_procedencia` agregados para WSLPGv1.1; `peso_neto_sin_certificado`, `val_grado_ent`, `cod_localidad_procedencia_sin_certificado`, `cod_prov_procedencia_sin_certificado` agregados para WSLPGv1.2 y WSLPGv1.3; `nro_contrato` agregado en actualización 1.12d (WSLPGv1.4)
- **`AgregarCertificado(tipo_certificado_deposito, nro_certificado_deposito, peso_neto, cod_localidad_procedencia, cod_prov_procedencia, campania, fecha_cierre, peso_neto_total_certificado, coe_certificado_deposito)`**: agerga un certificado de depósito (F1116A o F1116RT). `peso_neto_total_certificado` es obligatorio para ajustes unificado (WSLPGv1.4) ajustado en actualizacion 1.12d; peso_neto y coe_certificado_deposito requeridos para ajustes de crédito / débito agregado en actualización 1.30a ([WSLPGv1.17](wiki:LiquidacionPrimariaGranos#Version1.17))
- **`AgregarRetencion(codigo_concepto, detalle_aclaratorio, base_calculo, alicuota, nro_certificado_retencion, fecha_certificado_retencion, importe_certificado_retencion)`**: agerga una retención (IVA, Ganancias, etc.). Número, fecha e importe de certificado de retención son opcionales. Si se envían, alicuota debe ser 0 (ver validación 1856) *ajustado en actualizacion 1.11a*
- **`AgregarDeduccion(codigo_concepto, detalle_aclaratorio, dias_almacenaje, precio_pkg_diario, comision_gastos_adm, base_calculo, alicuota)`**: agerga una deducción (gastos, fletes, almacenaje, etc.)
- **`AutorizarLiquidacion()`**: arma la liquidación, envía los datos a AFIP y devuelve `COE`, estableciendo los atributos con los campos de la respuesta.
- **`AnularLiquidacion(coe)`**: permite anular una liquidación activa, establece atributo `Resultado` (`A`: Aprobado, `R`: Rechazado) y `COE`
- **`ConsultarLiquidacion(pto_emision, nro_orden, coe, pdf):`**: Consulta una liquidación por No de orden o COE (establece el resto de los atributos, similar a `AutorizarLiquidacion`). *pto_emision agregado en actualizacion 1.03a* *pdf (indicar nombre de archivo para descargarlo de AFIP) agregado en actualizacion 1.25a*
- **`ConsultarUltNroOrden(pto_emision)`**: devuelve el último No de orden registrado por AFIP (atributo `NroOrden`) *pto_emision agregado en actualizacion 1.03a*. 
- **`AutorizarAnticipo()`**: arma el anticipo de la liquidación, envía los datos a AFIP y devuelve `COE`, estableciendo los atributos con los campos de la respuesta (similar a `AutorizarLiquidacion`). *agregado en actualizacion 1.28a*
- **`CancelarAnticipo(pto_emision, nro_orden, coe, pdf):`**: Cancela un anticipo y consulta una liquidación por No de orden o COE (establece el resto de los atributos, similar a `ConsultarLiquidacion`). *agregado en actualizacion 1.28a*
- **`AnularContraDocumento(pto_emision, nro_orden, coe):`**: Anula la liquidación original generando una nueva liquidación como contra documento. La anulación se corresponde a un ajuste unificado con la misma información que la liquidación anulada.*agregado en actualización 1.33a*

### Ajustes

Métodos para Ajuste "Único" / Final WSLPG version 1.4 (*agregado en actualizacion 1.12a*):

- **`CrearAjusteBase(pto_emision, nro_orden, coe_ajustado, nro_contrato, tipo_formulario, nro_formulario, nro_act_comprador, cod_grano, cuit_vendedor, cuit_comprador, cuit_corredor, nro_ing_bruto_vendedor, nro_ing_bruto_comprador, nro_ing_bruto_corredor, cod_tipo_operacion, precio_ref_tn, cod_grado_ent, val_grado_ent, precio_flete_tn, cod_puerto, des_puerto_localidad, cod_provincia, cod_localidad, comision_corredor)`**: Inicializa internamente los datos de una liquidación para ajustar. Luego debe llamar a `AgregarCertificado` para completar el contenido de `AjusteBase`, `AjusteCredito` y `AjusteDebito` (en estos últimos casos, con coe y peso_neto a ajustar, ver [WSLPGv1.17](wiki:LiquidacionPrimariaGranos#Version1.17)).
- **`CrearAjusteCredito(datos_adicionales, concepto_importe_iva_0, importe_ajustar_iva_0, concepto_importe_iva_105, importe_ajustar_iva_105, concepto_importe_iva_21, importe_ajustar_iva_21, diferencia_peso_neto, diferencia_precio_operacion, cod_grado, val_grado, factor diferencia_precio_flete_tn)`**: Inicializa internamente los datos del crédito del ajuste. Luego llamar a **`AgregarDeduccion(...)`** y **`AgregarRetencion(...)`** para completar el contenido de `AjusteCredito`.
- **`CrearAjusteDebito(datos_adicionales, concepto_importe_iva_0, importe_ajustar_iva_0, concepto_importe_iva_105, importe_ajustar_iva_105, concepto_importe_iva_21, importe_ajustar_iva_21, diferencia_peso_neto, diferencia_precio_operacion, cod_grado, val_grado, factor diferencia_precio_flete_tn)`**: Inicializa internamente los datos del crédito del ajuste. Luego llamar a **`AgregarDeduccion(...)`** y **`AgregarRetencion(...)`** para completar el contenido de `AjusteDebito`.
- **`AjustarLiquidacionUnificado()`**: permite ajustar una liquidación por COE (operatoria similar a `AutorizarLiquidacion`). 
- **`AjustarLiquidacionUnificadoPapel()`**: permite ajustar Liquidación realizada en un formulario F1116 B / C (papel).
- **`AjustarLiquidacionContrato()`**: permite ajustar una liquidación activa relacionadas a un contrato.
- **`AnalizarAjusteCredito()`** y **`AnalizarAjusteDebito()`**: método auxiliar para analizar el ajuste de de crédito devuelto por AFIP, establecen los atributos con importes totales y otros parámetros de salida (de manera similar a `AutorizarLiquidacion`)
- **`AsociarLiquidacionAContrato(coe, nro_contrato, cuit_comprador, cuit_vendedor, cuit_corredor, cod_grano)`**: asociar un contrato a una liquidación original emitida con anterioridad. *Agregado en actualizacion 1.13a*
- **`ConsultarLiquidacionesPorContrato(nro_contrato, cuit_comprador, cuit_vendedor, cuit_corredor, cod_grano)`**: Obtener una lista de los COE de liquidaciones relacionadas a un contrato. Usar método auxiliar **`LeerDatosLiquidacion()`** para obtener cada dato en el atributo `COE`. *Agregado en actualizacion 1.13a*
- **`ConsultarAjuste(pto_emision, nro_orden, nro_contrato`)**: obtiene los datos de un ajuste registrados en AFIP (usar `pto_emision`, `nro_orden` o `nro_contrato`). Ver `AnalizarAjusteCredito` y `AnalizarAjusteDebito` para analizar los datos. *Agregado en actualizacion 1.13a*

### Liquidación Secundaria de Granos

Métodos incorporados según RG3690/14 WSLPG version 1.6 (*agregado en actualizacion 1.17a*):

- **`CrearLiqSecundariaBase(pto_emision, nro_orden, nro_contrato,cuit_comprador, nro_ing_bruto_comprador,cod_puerto, des_puerto_localidad, cod_grano, cantidad_tn,cuit_vendedor, nro_act_vendedor, nro_ing_bruto_vendedor,actua_corredor, liquida_corredor, cuit_corredor,nro_ing_bruto_corredor, fecha_precio_operacion, precio_ref_tn,precio_operacion, alic_iva_operacion, campania_ppal,cod_localidad_procedencia, cod_prov_procedencia, datos_adicionales):`**: Inicializa internamente los datos de una liquidación secundaria para luego poder autorizarla.
- **`AgregarDeduccion(codigo_concepto, detalle_aclaratorio, dias_almacenaje, precio_pkg_diario, comision_gastos_adm, base_calculo, alicuota)`**: agerga una deducción (gastos, fletes, almacenaje, etc.). Para LSG sólo se utiliza detalle_aclaratorio, base_calculo y alicuota **ajustado WSLPGv1.8** *actualizacion 1.20a*
- **`AgregarPercepcion(detalle_aclaratoria, base_calculo, alicuota)`**: agerga una percepcion. **agregado WSLPGv1.8** *actualizacion 1.20a*
- **`AgregarOpcional(codigo, descripcion)`**: agerga un valor opcional previsto para info adicional. **agregado WSLPGv1.8** *actualizacion 1.20a*
- **`AutorizarLiquidacionSecundaria()`**: permite autorizar una liquidación secundaria, obteniendo el COE (operatoria similar a `AutorizarLiquidacion`). 
- **`AnularLiquidacionSecundaria(coe)`**: permite anular una liquidación secundaria. activa, establece atributo `Resultado` (`A`: Aprobado, `R`: Rechazado) y `COE`. *actualizacion 1.21a*
- **`ConsultarLiquidacionSecundaria(pto_emision, nro_orden, coe, pdf):`**: Consulta una liquidación secundaria por No de orden o COE (establece el resto de los atributos, similar a `AutorizarLiquidacion`).  *actualizacion 1.21a* *pdf (indicar nombre de archivo para descargarlo de AFIP) agregado en actualizacion 1.25a*
- **`ConsultarLiquidacionSecundariaUltNroOrden(pto_emision)`**: devuelve el último No de orden registrado por AFIP (atributo `NroOrden`) *agregado en actualizacion 1.22a*
- **`AgregarFacturaPapel(nro_cai, nro_factura_papel, fecha_factura, tipo_comprobante):`** permite agregar los datos de una factura en papel a una LSG (WSLPGv1.15) *agregado en actualizacion 1.26a*
- **`AjustarLiquidacionUnificado():`** permite ajustar una liquidación secundaria. El procedimiento es similar que para las primaria (llamar a los métodos `CrearAjusteBase`, `AgregarAjusteCredito`, `AgregarPercepcion`, etc., ver pseudocodigo [ejemplo](wiki:LiquidacionPrimariaGranos)) *agregado en actualización 1.26a*
- **`AsociarLiquidacionSecundariaAContrato(coe, nro_contrato, cuit_comprador, cuit_vendedor, cuit_corredor, cod_grano):`** permite asociar una liquidación secundaria a un contrato. El procedimiento es similar que para las primaria (ver métodos `AsociarLiquidacionAContrato`) *agregado en actualización 1.27a*
- **`ConsultarLiquidacionesSecundariasPorContrato(nro_contrato, cuit_comprador, cuit_vendedor, cuit_corredor, cod_grano):`** permite consultar las liquidaciones secundarias por contrato. El procedimiento es similar que para las primaria (ver método `ConsultarLiquidacionesPorContrato`) *agregado en actualización 1.27a*

Próximamente se incorporarán más métodos para consultar, asociar y anular LSB.
### Certificación de Depósitos, Retiros y Transferencias de Granos

Métodos incorporados según RG3691/14 WSLPG version 1.6 a 1.10 (*agregado en actualizacion 1.17b*, *modificados según WSDL en 1.24b*):

- **`CrearCertificacionCabecera(pto_emision=1, nro_orden, tipo_certificado=None, nro_planta, nro_ing_bruto_depositario, titular_grano, cuit_depositante, nro_ing_bruto_depositante, cuit_corredor, cod_grano, campania, datos_adicionales)`**: Inicializa internamente los datos de una certificación primaria de granos para luego poder autorizarla. No todos los parámetros son obligatorios, y algunos solo se utilizan para determinado tipo de autorización.
- **`AgregarCertificacionPrimaria(nro_act_depositario, descripcion_tipo_grano, monto_almacenaje, monto_acarreo, monto_gastos_generales, monto_zarandeo,porcentaje_secado_de, porcentaje_secado_a,monto_secado, monto_por_cada_punto_exceso,monto_otros, porcentaje_merma_volatil, peso_neto_merma_volatil, porcentaje_merma_secado, peso_neto_merma_secado, porcentaje_merma_zarandeo, peso_neto_merma_zarandeo,peso_neto_certificado, servicios_secado,servicios_zarandeo, servicios_otros, servicios_forma_de_pago,)`** *Modificado WSLPGv1.10 actualización 1.23a* 
- **`AgregarCalidad(analisis_muestra, nro_boletin, cod_grado, valor_grado, valor_contenido_proteico, valor_factor)`**: agrega los datos opcionales de calidad, llamar antes de AgregarDetalleMuestraAnalisis` *Nuevo WSLPGv1.10 actualización 1.23a*
- **`AgregarCertificacionRetiroTransferencia(nro_act_depositario, cuit_receptor, fecha, nro_carta_porte_a_utilizar, cee_carta_porte_a_utilizar)`**: permite definir los campos de una Certificación Primaria de Retiro / Transf. de Granos (ex C1116RT), para luego autorizarla 
- **`AgregarCertificacionPreexistente(tipo_certificado_deposito_preexistente, nro_certificado_deposito_preexistente, cac_certificado_deposito_preexistente, fecha_emision_certificado_deposito_preexistente, nro_planta)`**: permite definir los campos de un certificado de granos preexistente (para luego autorizar y dar de alta)
- **`AgregarDetalleMuestraAnalisis(descripcion_rubro, tipo_rubro, porcentaje, valor)`**: Agrega la información referente al detalle de la certificación para luego poder autorizarla.
- **`AgregarCTG(nro_ctg, nro_carta_porte, porcentaje_secado_humedad, importe_secado, peso_neto_merma_secado, tarifa_secado, importe_zarandeo, peso_neto_merma_zarandeo, tarifa_zarandeo, peso_neto_confirmado_definitivo)`**: Agrega la información referente a una CTG de la certificación para luego poder autorizarla.
- **`AutorizarCertificacion()`**: permite autorizar una Certificación Primaria de Depósito de Granos (C1116A y C1116RT), obteniendo el COE (operatoria similar a `AutorizarCertificacion`). 
- **`AnularCertificacion(coe)`**: permite solicitar la anulación de una certificación activa, establece atributo `Estado`. *actualizacion 1.21a*
- **`ConsultarCertificacion(pto_emision, nro_orden, coe, pdf):`**: Consulta una certificación por No de orden o COE (establece el resto de los atributos, similar a `AutorizarCertificacion`).  *actualizacion 1.21a* *pdf (indicar nombre de archivo para descargarlo de AFIP) agregado en actualizacion 1.25a*
- **`ConsultarCertificacionUltNroOrden(pto_emision)`**: devuelve el último No de orden registrado por AFIP (atributo `NroOrden`) *agregado en actualizacion 1.22a*

Métodos adicionales para consultas, *agregado en actualizacion 1.24b*:

- **`BuscarCTG(tipo_certificado, cuit_depositante, nro_planta, cod_grano, campania)`**: consulta CTG a utilizar en una CG, establece los parámetros de salida con los campos "campania", "nro_planta", "nro_ctg", "tipo_ctg", "nro_carta_porte", "kilos_confirmados", "fecha_confirmacion_ctg", "cod_grano", "cuit_remitente_comercial", "cuit_liquida", "cuit_certifica". Para revisar los datos devueltos se puede utilizar `WSLPG.GetParametro("ctgs", 0, "nro_ctg")` -0 para el primer ctg, 1 para el segundo, etc.
- **`BuscarCertConSaldoDisponible(cuit_depositante, cod_grano, campania, coe fecha_emision_des, fecha_emision_has)`**: consultar certificados con saldo disponible para liquidar/retirar/transferir, establece los parámetros de salida con los campos "coe", "tipo_certificado", "campania", "cuit_depositante", "cuit_depositario", "nro_planta", "kilos_disponibles", "cod_grano". Para revisar los datos devueltos se puede utilizar `WSLPG.GetParametro("certificados", 0, "coe")`

Próximamente se incorporarán más métodos para consultar, asociar y anular CG.
### Consultas de Parámetros

Métodos de consulta de tablas de parámetros (devuelven una lista de valores string, sep es el caracter/es de separación):

- **`ConsultarCampanias(sep="||")`**: devuelve las campañas habilitadas (por ej. 1213 para 2012/2013)
- **`ConsultarTipoGrano(sep="||")`**: devuelve los tipos de granos habilitados (por ej. 1: lino, 2: girasol, etc.)
- **`ConsultarGradoEntregadoXTipoGrano(cod_grano, sep="||")`**: devuelve Grado y Valor según Grano Entregado
- **`ConsultarCodigoGradoReferencia(sep="||")`**: devuelve los posibles grados a utilizar en una liquidación (G1, G2, G3)
- **`ConsultarTipoCertificadoDeposito(sep="||")`**:   retorna los tipos de certificados de depósito habilitados en este servicio (1: F1116/RT, 5: F1116/A)
- **`ConsultarTipoDeduccion(sep="||")`**: devuelve los códigos de deducciones (por ej. CO: comisión, AL: almacenaje, OD: otras)
- **`ConsultarTipoRetencion(sep="||")`**: devuelve los códigos de retenciones (por ej. RI: IVA, RG: Ganancias)
- **`ConsultarPuerto(sep="||")`**: devuelve la lista de los código de puertos habilitados
- **`ConsultarTipoActividad(sep="||")`**: devuelve la lista de los códigos de actividad habilitados
- **`ConsultarProvincias(sep="||")`**: devuelve la lista de los códigos de provincia habilitados
- **`ConsultarLocalidadesPorProvincia(localidad, sep="||")`**: devuelve las localidades para una determinada provincia
- **`ConsultarTiposOperacion(sep="||")`**: devuelve los códigos de tipos de operacion y codigos de las actividades habilitadas
- **`ConsultarTipoActividadRepresentado(sep="||")`**: devuelve las actividades en las que emisor/representado se encuentra inscripto en RUOCA *agregado en actualizacion 1.06a*

### Auxiliares

Métodos para pasaje de parámetros (lenguajes legados) y pruebas (*agregado en actualizacion 1.04a*):

- **`SetParametro(clave, valor)`**: establece un parametro para la próxima llamada (clave es el nombre del campo), útil para superar la limitación de VFP de 27 argumentos
- **`GetParametro(clave, [clave1, [clave2]])`**: devuelve un parametro de la última llamada, útil para obtener campos adicionales. clave1 y clave2 se utilizan para campos anidados, por ej retenciones y deducciones (ver ejemplos).
- **`LoadTestXML(archivo)`**: carga respuesta de prueba según documentación de AFIP (usar para simular una llamada si el ws no esta operativo o no se dispone de datos válidos)

### Generación de PDF

Métodos para elaboración de documentos PDF de Liquidación/Ajustes (*agregado en actualizacion 1.05a*):

- **`CrearPlantillaPDF(papel, orientacion)`**: crea una plantilla con el papel (A4, legal o letter) y orientación (portrait, landscape). IMPORTANTE: a partir de la actualización 1.14a llamar al inicio de la rutina de generación para soportar varias plantillas por documento (ajustes).
- **`CargarFormatoPDF(archivo_csv)`**: crea todos los campos del diseño de la factura (layout) leyendolos desde el archivo especificado.
- **`AgregarCampoPDF(nombre, tipo, x1, y1, x2, y2, font, size, bold, italic, underline, foreground, background, align, text, priority)`**: agrega un campo manualmente al diseño de la factura (layout)
- **`AgregarDatoPDF(campo, valor)`**: agrega un dato a un campo adicional
- **`ProcesarPlantillaPDF(num_copias, lineas_max, qty_pos, clave="")`**: procesa los datos de la factura dentro de la plantilla, indicando la cantidad de copioas (1: original, 2: duplicado, 3:triplicado), la cantidad de líneas máximas por página. IMPORTANTE: a partir de la actualización 1.14a, se agrega el parametro clave para indicar el tipo de plantilla a procesar ("" vacio para liquidaciones / ajustes base, "ajuste_credito" o "ajuste_debito" para los Ajustes Crédito / Débito respectivamente)
- **`GenerarPDF(salida, destino="F")`**: genera el archivo PDF terminado con el nombre dado en salida. IMPORTANTE: a partir de la actualización 1.14a, se agrega el parametro destino para indicar si se debe escribir el documento o se procesarán otras plantillas ("F" predeterminado para generar archivo, "" string vacio para ir procesando multiples plantillas sin grabar)
- **`MostrarPDF(salida, imprimir)`**: muestra el contenido del PDF generado (usando Adobe Acrobat Reader o similar) y opcionalmente lo envía directo a la impresora.

**Importante:** si un campo no debe enviarse, completar con None, Null, Empty, ? o el valor equivalente para campos nulos. No usar cadena vacia o 0 ya que son datos válidos y se enviarán al webservice. No saltear u omitir parámetros, salvo que sean pasados por nombre (*keyword arguments*), usar `SetParametro` en dicho caso.
## Atributos

- **`COE`**: Código de Operación Electrónico, completado por !AutorizarLiquidacion
- **`COEAjustado`** completado por !AutorizarLiquidacion
- **`Estado`**: `AC`activo, `AN` anulado, completado por !AutorizarLiquidacion y !ConsultarLiquidacion
- **`TootalDeduccion`**: completado por !AutorizarLiquidacion
- **`TotalRetencion`**: completado por !AutorizarLiquidacion
- **`TotalRetencionAfip`**: completado por !AutorizarLiquidacion
- **`TotalOtrasRetenciones`**: completado por !AutorizarLiquidacion
- **`Subtotal`**: subtotal general del ajuste (`totalesUnificados`)
- **`TotalIva105`**: importe total de IVA al 10.5% del ajuste (`totalesUnificados`)
- **`TotalIva21`**:importe total de IVA al 21% del ajuste (`totalesUnificados`)
- **`TotalRetencionesGanancias`**: importe total de retenciones de ganancia del ajuste (`totalesUnificados`)
- **`TotalRetencionesIVA`**: importe total de retenciones de ganancia del ajuste (`totalesUnificados`)
- **`TotalNetoAPagar`**: completado por !AutorizarLiquidacion
- **`TotalIvaRg2300_07`**: completado por !AutorizarLiquidacion
- **`TotalPagoSegunCondicion`**: completado por !AutorizarLiquidacion
- **`Resultado`**: `A` aprobado, `R` rechazado , completado por !AnularLiquidacion
- **`NroOrden`**: último número de orden registado en AFIP, completado por !ConsultarUltNroOrden
- **`NroContrato`**: número de contrato ajustado (devuelto por AFIP)
- **`FechaCertificacion`**: fecha de autorización del certificado de depósito, retiro/transferencia o preexistente (WSLPGv1.6)

## Interfaz cliente por Consola (CLI)

El programa puede operar independientemente por linea de comandos "MSDOS", consola de órdenes o terminal, invocando el ejecutable principal (`WSLPG_CLI.EXE` o `WSLPG.EXE` dependiendo del instalador, `wslpg.py` desde el código fuente), como se describe a continuación.

Este modo de operación es multiplataforma (compatible con Windows, GNU/Linux, MacOS X y posiblemente otros entornos). 
También puede ser usado desde lenguajes modernos como VB o VFP, ver [ejemplo](wiki:LiquidacionPrimariaGranos#Ejemplopseudocodigo) y [descargas](wiki:LiquidacionPrimariaGranos#Descargas).

NOTA: Al usar archivos de configuración e intercambio de datos, no requiere interactividad con el usuario, por lo que puede ser ejecutado en segundo plano.
### Parámetros por línea de comando

El programa recibe los siguientes argumentos:

- **`--dummy`**: consulta el estado de los servidores
- **`--autorizar`**: carga una liquidación primaria y la autoriza en AFIP (lee y escribe los archivos de intercambio)
- **`--autorizar-lsg`**: carga una liquidación secundaria y la autoriza en AFIP (lee y escribe los archivos de intercambio)
- **`--autorizar-cg`**: carga una certificación de granos y la autoriza en AFIP (lee y escribe los archivos de intercambio)
- **`--informar-calidad`**: informar calidad de una CG ya presentada (espera `coe` como argumento, lee y escribe los archivos de intercambio)
- **`--anular`**: anula una liquidación  (espera `coe` como argumento), anteponer `--lsg` o `--cg` para liquidaciones secundarias o certificaciones, respectivamente
- **`--ajustar`**: ajusta una liquidación (espera `coe_ajustado` y `cod_tipo_ajuste` como argumentos)
- **`--autorizar-anticipo`**: Autoriza un Anticipo 
- **`--ajustar-lsg`**: ajusta una liquidación (por COE o `--contrato`)
- **`--asociar`**: asociar una liquidación a un contrato (lee los datos desde el archivo de entrada). Anteponer `--lsg` para liq. secundaria.
- **`--prueba`**: genera archivo de intercambio de con datos de prueba (útil para `--autorizar`, `--ajustar`, `--asociar`, `--consultar_por_contrato`)
- **`--consultar`**: busca una liquidación en AFIP (espera `pto_emision`, `nro_orden` y `coe` como argumentos -este último opcional-), anteponer `--cancelar-anticipo`, `--lsg` o `--cg` para anticipos, liquidaciones secundarias o certificaciones, respectivamente. Opcionalmente indicar luego del coe el `pdf` (indicando la ruta completa) para descargar el documento generado por AFIP
- **`--consultar_por_contrato`**: devuelve todos los COE de liquidaciones asociadas a un numero de contrato (lee los datos desde el archivo de entrada)
- **`--consultar_ajuste`**: busca un ajuste de liquidación en AFIP (espera `pto_emision` y `nro_orden` y `nro_contrato` como argumentos -este último opcional-)
- **`--ult`**: devuelve el último nro de orden registrado en AFIP (espera `pto_emision` como argumento), anteponer `--lsg` o `--cg` para liquidaciones secundarias o certificaciones, respectivamente
- **`--pdf`**: genera el form. c 1116 b en un archivo con formato PDF (agregar **`--mostrar`** e **`--imprimir`** si es necesario, y **`--ajuste`** para generar ajustes unificados)
- **`--buscar-ctg`**: consulta CTG a utilizar en una CG, espera tipo_certificado, cuit_depositante, nro_planta, cod_grano, campania, ver método `BuscarCTG`
- **`--buscar-cert-con-saldo-disp`**: onsultar certificados con saldo disponible para liquidar/retirar/transferir, espera cuit_depositante, cod_grano, campania, coe fecha_emision_des, fecha_emision_has. Ver método `BuscarCertConSaldoDisponible`
- **`--provincias --localidades --tipograno --campanias --gradoref --gradoent --certdeposito --deducciones --retenciones --puertos --actividades --actividadesrep --operaciones`**: consulta tablas de parametros y valores de referencia
- **`--formato`**: devuelve el formato del archivo de texto
- **`--dbf`**: utilizar tablas DBF (xBase) para los archivos de intercambio
- **`--json`**: utilizar formato json para el archivo de intercambio
- **`--ayuda`**: muestra las opciones del programa
- **`--testing`**: carga respuesta de prueba para simular llamada
- **`--debug`**: muestra los datos internos
- **`--trace`**: muestra los mensajes xml enviados y recibidos

Para ejecutarlo se debe usar el programa compilado WSLPG_CLI.EXE o el código fuente wslpg.py

Ejemplo para autorizar una liquidación (notar que los datos deben estar en el archivo de intercambio, y no debe pasarse parametros adicionales):

```
C:\PYAFIPWS> WSLPG_CLI.EXE --autorizar
Errores: []
COE 330100000357
COEAjustado None
TootalDeduccion 0
TotalRetencion 159.60
TotalRetencionAfip 159.60
TotalOtrasRetenciones 0
TotalNetoAPagar 2017.25
TotalIvaRg2300_07 49.25
TotalPagoSegunCondicion 1968.00
```

Ejemplo para ajustar una liquidación pasando los datos por el archivo de entrada (a partir de versión 1.12b):
```
C:\PYAFIPWS> WSLPG_CLI.EXE --ajustar
Ajustando...
Errores: []
COE 330100013133
Subtotal -734.10
TotalIva105 0
TotalIva21 0
TotalRetencionesGanancias 0
TotalRetencionesIVA -94.50
TotalNetoAPagar -639.07
TotalIvaRg2300_07 94.50
TotalPagoSegunCondicion -733.57
```

Ejemplo para anular una liquidación pasando el COE (a partir de versión 1.02a):
```
C:\PYAFIPWS> WSLPG_CLI.EXE --anular 330100000357
COE 
Resultado R
Errores: [u'500: Error General de Aplicacion.']
```

Ejemplo para consultar la tabla de campañas:
```
C:\PYAFIPWS> WSLPG_CLI.EXE --campanias
| 1213 | 2012/2013 |
|---|---|
| 1112 | 2011/2012 |
| 1011 | 2010/2011 |
| 910 | 2009/2010 |
| 809 | 2008/2009 |
| 708 | 2007/2008 |
hecho.
```

Ejemplo para consultar la tabla de valores para Grado y Valor según Grano Entregado (ejemplo para cod_grano=19 Maiz):
```
C:\PYAFIPWS> WSLPG_CLI.EXE --gradoentregado
Ingrese el código de grano: 19
| G1 | Grado 1 | 1.01 |
|---|---|---|
| G2 | Grado 2 | 1.00 |
| G3 | Grado 3 | 0.985 |
| FG | Fuera de Grado (FG) | 0 |
| F1 | Grado 1 (FG) | 0 |
| F2 | Grado 2 (FG) | 0 |
| F3 | Grado 3 (FG) | 0 |
hecho.
```


Ejemplo para consultar el último nro de orden (a partir de versión 1.02a, pto_emision` agregado a partir de actualización 1.03a, si no se especifica se utiliza 1):
```
C:\PYAFIPWS> WSLPG_CLI.EXE --ult 2
Consultando ultimo nro_orden para pto_emision=2
Ultimo Nro de Orden 0
Errores: []
```

Ejemplo para consultar una liquidación por punto de emision, número de orden o COE (a partir de actualizacion 1.02a, `pto_emision` agregado a partir de actualización 1.03a):
```
C:\PYAFIPWS> WSLPG_CLI.EXE --consultar 1 1 330100000357
COE 
Estado 
Errores: [u'600: No existen datos en las bases de la Administración según los parámetros de búsqueda informados.']
```

Ejemplo para generar un PDF con el Form. C1116B (a partir de actualizacion 1.05a, cargará los datos del archivo de intercambio):
```
C:\PYAFIPWS> WSLPG_CLI.EXE --pdf --mostrar --imprimir
```

Ejemplo para asociar un número de contrato a una liquidación previamente autorizada -datos de prueba- (*a partir de actualizacion 1.13a*):
```
C:\PYAFIPWS> WSLPG_CLI.EXE --asociar --prueba
Asociando... coe=330100004664, cuit_comprador=20400000000, cuit_corredor=20267565393, cuit_vendedor=23000000019, nro_contrato=26
Errores: [u'2112: La liquidacion ya esta relacionada al contrato.']
COE 
Estado 
hecho.

```

Ejemplo para consultar los COE asociados a un número de contrato -datos de prueba- (*a partir de actualizacion 1.13a*):
```
C:\PYAFIPWS> WSLPG_CLI.EXE --consultar_por_contrato --prueba
Consultando liquidaciones por contrato... cuit_comprador=20400000000, cuit_corredor=20267565393, cuit_vendedor=23000000019, nro_contrato=26
Errores: []
COE 330100004664
COE 330100014020
COE 330100014022
COE 330100014023
COE 330100014025
COE 330100014028
COE 330100014029
COE 330100014040
COE 330100014043
COE 330100014057
COE 330100014061
COE 330100014450
COE 330100014454
COE 330100014455
COE 330100014459
COE 330100014467
COE 330100014472
hecho.
```

Ejemplo para consultar un ajuste de liquidación por punto de emision, número de orden o número de contrato (*a partir de actualizacion 1.13a*):
```
C:\PYAFIPWS> WSLPG_CLI.EXE --consultar_ajuste 55 79
Consultando: pto_emision=55 nro_orden=79 nro_contrato=None
COE 330100014505
Estado AN
Errores: []
hecho.
```

Ejemplo para obtener el PDF que genera AFIP para las nuevas Certificación de Granos (primaria, retiro/transferencia o preexistente) ex-Form.C1116A ex-Form.C116RT según especificación WSLPGv1.11 (*a partir de actualizacion 1.25a*):
```
C:\PYAFIPWS> WSLPG_CLI.EXE --cg --consultar 99 5 332000000466 cg.pdf
Consultando: pto_emision=99 nro_orden=5 coe=332000000466
COE 332000000466
Estado AC
Errores: []
hecho.
```

**Nota**: si devuelve `'500: Error General de Aplicacion.'` es un problema interno de AFIP

Ejemplo para autorizar un Anticipo de Liquidación Primaria según especificación WSLPGv1.15 (*a partir de actualizacion 1.28a*):
```
C:\PYAFIPWS> WSLPG_CLI.EXE --autorizar-anticipo
Liquidacion Primaria (Ant): pto_emision=33 nro_orden=1
Errores: []
COE 330200008457
2
2015-03-31
TootalDeduccion 0
TotalRetencion 12.50
TotalRetencionAfip 12.50
TotalOtrasRetenciones 0.00
TotalNetoAPagar 338.36
TotalIvaRg2300_07 22.84
TotalPagoSegunCondicion 315.52
hecho.
```


Ejemplo para cancelar y consultar un Anticipo según especificación WSLPGv1.15 (*a partir de actualizacion 1.28a*):
```
C:\PYAFIPWS> WSLPG_CLI.EXE --cancelar-anticipo --consultar 1 1 330200008412 ant.pdf --testing 
Consultando: pto_emision=1 nro_orden=1 coe=1
COE 330200008412
Estado AC
Errores: []
hecho.
```
### Archivo de Configuración

Para utilizar este webservice, debe tramitarse un certificado. Ver [Instructivo](wiki:ManualPyAfipWs#Certificados)

Luego, se debe configurar el Certificado, clave privada y URL en el archivo de configuración WSLPG.INI:

```
[WSAA]
CERT=reingart.crt
PRIVATEKEY=reingart.key
#URL=https://wsaa.afip.gov.ar/ws/services/LoginCms

[WSLPG]
CUIT=20267565393
ENTRADA=entrada_wslpg.txt
SALIDA=salida_wslpg.txt
#URL=https://serviciosjava.afip.gob.ar/wslpg/LpgService?wsdl
```

Para producción, se debe usar un instalador para tal fin y descomentar la URL (eliminando el numeral). 

## Formato de Intercambio

Si se utilizan archivos de intercambio (texto de ancho fijo, similar al utilizado por los aplicativos de SIAP y los distintos dialectos de COBOL), se utiliza el siguiente formato de datos para representar una Liquidación a autorizar.

Se adjuntan dos archivos de muestra (completos con todos los registros según el ejemplo 1 de AFIP) para "Liquidación Primaria de Granos":

- [entrada_wslpg.txt](attachment:entrada_wslpg.txt): archivo de entrada (con datos de prueba)
- [salida_wslpg.txt](attachment:salida_wslpg.txt): archivo de salida (con datos de prueba)
- [salida_wslpg_ajuste_unif.txt](attachment:salida_wslpg_ajuste_unif.txt): archivo de salida de ajuste de unificado (con datos de prueba)
- [wslpg.json](attachment:wslpg.json): archivo de intercambio en formato JSON (para lenguajes modernos, por ej. PHP)

También se adjuntan muestras del archivo de entrada (con datos de prueba) para "Liquidación Secundaria de Granos" y "Certificaciones de Granos" (WSLPGv1.6):

- [entrada_wslpg_lsg.txt](attachment:entrada_wslpg_lsg.txt):  Liquidación Secundaria de Granos (LSG)
- [entrada_wslpg_cert_dep.txt](attachment:entrada_wslpg_cg_f1116a.txt): Certificación de depósito F1116A
- [entrada_wslpg_cert_rt.txt](attachment:entrada_wslpg_cg_f1116rt.txt): Certificación de retiro / transferencia F1116RT
- [entrada_wslpg_cert_pre.txt](attachment:entrada_wslpg_cg_preexistente.txt): Certificación preexistente

### Encabezado

- Campo: tipo_reg             Posición:   1 Longitud:    1 Tipo: Alfanumerico Valor: 0
- Campo: nro_orden            Posición:   2 Longitud:   18 Tipo: Numerico
- Campo: cuit_comprador       Posición:  20 Longitud:   11 Tipo: Numerico
- Campo: nro_act_comprador    Posición:  31 Longitud:    5 Tipo: Numerico
- Campo: nro_ing_bruto_comprador Posición:  36 Longitud:   15 Tipo: Numerico
- Campo: cod_tipo_operacion   Posición:  51 Longitud:    2 Tipo: Alfanumerico 
- Campo: es_liquidacion_propia Posición:  53 Longitud:    1 Tipo: Alfanumerico 
- Campo: es_canje             Posición:  54 Longitud:    1 Tipo: Alfanumerico 
- Campo: cod_puerto           Posición:  55 Longitud:    4 Tipo: Numerico
- Campo: des_puerto_localidad Posición:  59 Longitud:  240 Tipo: Alfanumerico 
- Campo: cod_grano            Posición: 299 Longitud:    3 Tipo: Numerico
- Campo: cuit_vendedor        Posición: 302 Longitud:   11 Tipo: Numerico
- Campo: nro_ing_bruto_vendedor Posición: 313 Longitud:   15 Tipo: Numerico
- Campo: actua_corredor       Posición: 328 Longitud:    1 Tipo: Alfanumerico 
- Campo: liquida_corredor     Posición: 329 Longitud:    1 Tipo: Alfanumerico 
- Campo: cuit_corredor        Posición: 330 Longitud:   11 Tipo: Numerico
- Campo: nro_ing_bruto_corredor Posición: 341 Longitud:   15 Tipo: Numerico
- Campo: comision_corredor    Posición: 356 Longitud:    5 Tipo: Importe Decimales: 2
- Campo: fecha_precio_operacion Posición: 361 Longitud:   10 Tipo: Alfanumerico 
- Campo: precio_ref_tn        Posición: 371 Longitud:    8 Tipo: Numerico3
- Campo: cod_grado_ref        Posición: 379 Longitud:    2 Tipo: Alfanumerico 
- Campo: cod_grado_ent        Posición: 381 Longitud:    2 Tipo: Alfanumerico 
- Campo: factor_ent           Posición: 383 Longitud:    6 Tipo: Importe Decimales: 3
- Campo: precio_flete_tn      Posición: 389 Longitud:    7 Tipo: Importe Decimales: 2
- Campo: cont_proteico        Posición: 396 Longitud:    6 Tipo: Importe Decimales: 3
- Campo: alic_iva_operacion   Posición: 402 Longitud:    5 Tipo: Importe Decimales: 2
- Campo: campania_ppal        Posición: 407 Longitud:    4 Tipo: Numerico
- Campo: cod_localidad_procedencia Posición: 411 Longitud:    6 Tipo: Numerico
- Campo: datos_adicionales    Posición: 983 Longitud:  400 Tipo: Alfanumerico (actualizado! nueva posición)
- Campo: coe                  Posición: 617 Longitud:   12 Tipo: Numerico
- Campo: coe_ajustado         Posición: 629 Longitud:   12 Tipo: Numerico
- Campo: estado               Posición: 641 Longitud:    2 Tipo: Alfanumerico 
- Campo: total_deduccion      Posición: 643 Longitud:   17 Tipo: Importe Decimales: 2
- Campo: total_retencion      Posición: 660 Longitud:   17 Tipo: Importe Decimales: 2
- Campo: total_retencion_afip Posición: 677 Longitud:   17 Tipo: Importe Decimales: 2
- Campo: total_otras_retenciones Posición: 694 Longitud:   17 Tipo: Importe Decimales: 2
- Campo: total_neto_a_pagar   Posición: 711 Longitud:   17 Tipo: Importe Decimales: 2
- Campo: total_iva_rg_2300_07 Posición: 728 Longitud:   17 Tipo: Importe Decimales: 2
- Campo: total_pago_segun_condicion Posición: 745 Longitud:   17 Tipo: Importe Decimales: 2
- Campo: fecha_liquidacion    Posición: 762 Longitud:   10 Tipo: Alfanumerico 
- Campo: nro_op_comercial     Posición: 772 Longitud:   10 Tipo: Numerico
- Campo: precio_operacion     Posición: 782 Longitud:   17 Tipo: Importe Decimales: 3
- Campo: subtotal             Posición: 799 Longitud:   17 Tipo: Importe Decimales: 2
- Campo: importe_iva          Posición: 816 Longitud:   17 Tipo: Importe Decimales: 2
- Campo: operacion_con_iva    Posición: 833 Longitud:   17 Tipo: Importe Decimales: 2
- Campo: total_peso_neto      Posición: 850 Longitud:    8 Tipo: Numerico
- Campo: pto_emision          Posición: 858 Longitud:    4 Tipo: Numerico
- Campo: cod_prov_procedencia Posición: 862 Longitud:    2 Tipo: Numerico 
- Campo: peso_neto_sin_certificado Posición: 864 Longitud:    8 Tipo: Numerico
- Campo: val_grado_ent        Posición: 874 Longitud:    4 Tipo: Importe Decimales: 3
- Campo: cod_prov_procedencia_sin_certificado Posición: 878 Longitud:    2 Tipo: Numerico
- Campo: cod_localidad_procedencia_sin_certificado Posición: 880 Longitud:    6 Tipo: Numerico 

Campos de entrada específicos para Ajustes:

- Campo: coe_ajustado         (ver lista anterior, similar a Autorizar Liquidación)
- Campo: nro_contrato         Posición: 886 Longitud:   15 Tipo: Numerico
- Campo: tipo_formulario      Posición: 901 Longitud:    2 Tipo: Numerico
- Campo: nro_formulario       Posición: 903 Longitud:   12 Tipo: Numerico

Campos de salida específicos para Ajustes (devueltos por AFIP):

- Campo: coe                  (ver lista anterior, similar a Autorizar Liquidación)
- Campo: subtotal             (ver lista anterior, similar a Autorizar Liquidación)
- Campo: iva_deducciones      Posición: 1383 Longitud:   17 Tipo: Importe Decimales: 2
- Campo: subtotal_deb_cred    Posición: 1400 Longitud:   17 Tipo: Importe Decimales: 2
- Campo: total_base_deducciones Posición: 1417 Longitud:   17 Tipo: Importe Decimales: 2
- Campo: total_iva_10_5       Posición: 915 Longitud:   17 Tipo: Importe Decimales: 2
- Campo: total_iva_21         Posición: 932 Longitud:   17 Tipo: Importe Decimales: 2
- Campo: total_retenciones_ganancias Posición: 949 Longitud:   17 Tipo: Importe Decimales: 2
- Campo: total_retenciones_iva Posición: 966 Longitud:   17 Tipo: Importe Decimales: 2
- Campo: total_neto_a_pagar   (ver lista anterior, similar a Autorizar Liquidación)
- Campo: total_iva_rg_2300_07 (ver lista anterior, similar a Autorizar Liquidación)
- Campo: total_pago_segun_condicion (ver lista anterior, similar a Autorizar Liquidación)

Campos específicos para Liquidación Secundaria de Granos (RG3690/2014):

- Campo: cantidad_tn          Posición: 1434 Longitud:   11 Tipo: Importe Decimales: 3
- Campo: nro_act_vendedor     Posición: 1445 Longitud:    5 Tipo: Numerico
- Campo: total_deducciones    Posición: 1450 Longitud:   19 Tipo: Importe Decimales: 2
- Campo: total_percepciones   Posición: 1469 Longitud:   19 Tipo: Importe Decimales: 2

### Certificado

- Campo: tipo_reg             Posición:   1 Longitud:    1 Tipo: Alfanumerico Valor: 1
- Campo: reservado1           Posición:   2 Longitud:    2 Tipo: Numerico (no utilizar, ver tipo_certificado_deposito abajo)
- Campo: nro_certificado_deposito Posición:   4 Longitud:   12 Tipo: Numerico 
- Campo: peso_neto            Posición:  16 Longitud:    8 Tipo: Numerico
- Campo: cod_localidad_procedencia Posición:  24 Longitud:    6 Tipo: Numerico
- Campo: cod_prov_procedencia Posición:  30 Longitud:    2 Tipo: Numerico 
- Campo: reservado            Posición:  32 Longitud:    2 Tipo: Numerico
- Campo: campania             Posición:  34 Longitud:    4 Tipo: Numerico 
- Campo: fecha_cierre         Posición:  38 Longitud:   10 Tipo: Alfanumerico 
- Campo: peso_neto_total_certificado Posición:  48 Longitud:    8 Tipo: Numerico 
- Campo: coe_certificado_deposito Posición:  56 Longitud:   12 Tipo: Numerico 
- Campo: tipo_certificado_deposito Posición:  68 Longitud:    3 Tipo: Numerico 

**Nota:** tipo_certificado_deposito fue modificado por WSLPGv1.7 aumentando a 3 posiciones para soportar el valor 332 "Certificado Electrónico de Depósito" (*actualización 1.22b*).
Por retrocompatibilidad, se puede seguir usando el campo anterior en posición 2 longitud 1, pero se recomienda actualizar los programas para soportar los tres dígitos.

Campos específicos para Certificación de Retiro/Transferencias de Granos (RG3691/14):

- Campo: coe_certificado_deposito Posición:  56 Longitud:   12 Tipo: Numerico

### Retencion

- Campo: tipo_reg             Posición:   1 Longitud:    1 Tipo: Alfanumerico Valor: 2
- Campo: codigo_concepto      Posición:   2 Longitud:    2 Tipo: Alfanumerico 
- Campo: detalle_aclaratorio  Posición:   4 Longitud:   30 Tipo: Alfanumerico 
- Campo: base_calculo         Posición:  34 Longitud:   10 Tipo: Importe Decimales: 2
- Campo: alicuota             Posición:  44 Longitud:    6 Tipo: Importe Decimales: 2
- Campo: nro_certificado_retencion Posición:  50 Longitud:   14 Tipo: Numerico
- Campo: fecha_certificado_retencion Posición:  64 Longitud:   10 Tipo: Alfanumerico 
- Campo: importe_certificado_retencion Posición:  74 Longitud:   17 Tipo: Importe Decimales: 2
- Campo: importe_retencion    Posición:  91 Longitud:   17 Tipo: Importe Decimales: 2

### Deduccion

- Campo: tipo_reg             Posición:   1 Longitud:    1 Tipo: Alfanumerico Valor: 3
- Campo: codigo_concepto      Posición:   2 Longitud:    2 Tipo: Alfanumerico
- Campo: detalle_aclaratorio  Posición:   4 Longitud:   30 Tipo: Alfanumerico 
- Campo: dias_almacenaje      Posición:  34 Longitud:    4 Tipo: Numerico
- Campo: reservado1           Posición:  38 Longitud:    6 Tipo: Importe Decimales: 3
- Campo: comision_gastos_adm  Posición:  44 Longitud:    5 Tipo: Importe Decimales: 2
- Campo: base_calculo         Posición:  49 Longitud:   10 Tipo: Importe Decimales: 2
- Campo: alicuota             Posición:  59 Longitud:    6 Tipo: Importe Decimales: 2
- Campo: importe_iva          Posición:  65 Longitud:   17 Tipo: Importe Decimales: 2
- Campo: importe_deduccion    Posición:  82 Longitud:   17 Tipo: Importe Decimales: 2
- Campo: precio_pkg_diario    Posición:  99 Longitud:   11 Tipo: Importe Decimales: 8

Nota: el campo `reservado1` era para informar el `precio_pkg_diario`, pero AFIP agregó más decimales en el WSLPGv1.2, por lo que el campo fue movido (aunque por compatibilidad hacia atrás, puede usarse en la posición anterior con menos decimales, ya que actualmente si bien la especificación dice soportar 8 decimales, acepta solo 4 en nuestras pruebas)

### Percepcion

- Campo: tipo_reg             Posición:   1 Longitud:    1 Tipo: Alfanumerico Valor: "P" ****Reg. Agregado Liq.Sec. WSLPGv1.8**'
- Campo: detalle_aclaratoria  Posición:   2 Longitud:   50 Tipo: Alfanumerico 
- Campo: base_calculo         Posición:  52 Longitud:   10 Tipo: Importe Decimales: 2
- Campo: alicuota             Posición:  62 Longitud:    6 Tipo: Importe Decimales: 2

### Opcional

- Campo: tipo_reg             Posición:   1 Longitud:    1 Tipo: Alfanumerico Valor: "O" ****Reg. Agregado Liq.Sec. WSLPGv1.8**'
- Campo: codigo               Posición:   2 Longitud:   50 Tipo: Alfanumerico
- Campo: descripcion          Posición:  52 Longitud:  250 Tipo: Alfanumerico

### Ajuste Crédito / Débito

Campos de entrada:

- Campo: tipo_reg             Posición:   1 Longitud:    1 Tipo: Alfanumerico Valor: "4" para Ajuste Débito, "5" para Ajuste Crédito
- Campo: concepto_importe_iva_0 Posición:   2 Longitud:   20 Tipo: Alfanumerico
- Campo: importe_ajustar_iva_0 Posición:  22 Longitud:   15 Tipo: Importe Decimales: 2
- Campo: concepto_importe_iva_105 Posición:  37 Longitud:   20 Tipo: Alfanumerico 
- Campo: importe_ajustar_iva_105 Posición:  57 Longitud:   15 Tipo: Importe Decimales: 2
- Campo: concepto_importe_iva_21 Posición:  72 Longitud:   20 Tipo: Alfanumerico
- Campo: importe_ajustar_iva_21 Posición:  92 Longitud:   15 Tipo: Importe Decimales: 2
- Campo: diferencia_peso_neto Posición: 107 Longitud:    8 Tipo: Numerico Decimales: 
- Campo: diferencia_precio_operacion Posición: 115 Longitud:   17 Tipo: Importe Decimales: 3
- Campo: cod_grado            Posición: 132 Longitud:    2 Tipo: Alfanumerico
- Campo: val_grado            Posición: 134 Longitud:    4 Tipo: Importe Decimales: 3
- Campo: factor               Posición: 138 Longitud:    6 Tipo: Importe Decimales: 3
- Campo: diferencia_precio_flete_tn Posición: 144 Longitud:    7 Tipo: Importe Decimales: 2
- Campo: datos_adicionales    Posición: 151 Longitud:  400 Tipo: Alfanumerico

Campos de salida (valores devueltos por AFIP similiar al encabezado de una liquidación):

- Campo: fecha_liquidacion    Posición: 551 Longitud:   10 Tipo: Alfanumerico
- Campo: nro_op_comercial     Posición: 561 Longitud:   10 Tipo: Numerico
- Campo: precio_operacion     Posición: 571 Longitud:   17 Tipo: Importe Decimales: 3
- Campo: subtotal             Posición: 588 Longitud:   17 Tipo: Importe Decimales: 2
- Campo: importe_iva          Posición: 605 Longitud:   17 Tipo: Importe Decimales: 2
- Campo: operacion_con_iva    Posición: 622 Longitud:   17 Tipo: Importe Decimales: 2
- Campo: total_peso_neto      Posición: 639 Longitud:    8 Tipo: Numerico
- Campo: total_deduccion      Posición: 647 Longitud:   17 Tipo: Importe Decimales: 2
- Campo: total_retencion      Posición: 664 Longitud:   17 Tipo: Importe Decimales: 2
- Campo: total_retencion_afip Posición: 681 Longitud:   17 Tipo: Importe Decimales: 2
- Campo: total_otras_retenciones Posición: 698 Longitud:   17 Tipo: Importe Decimales: 2
- Campo: total_neto_a_pagar   Posición: 715 Longitud:   17 Tipo: Importe Decimales: 2
- Campo: total_iva_rg_2300_07 Posición: 732 Longitud:   17 Tipo: Importe Decimales: 2
- Campo: total_pago_segun_condicion Posición: 749 Longitud:   17 Tipo: Importe Decimales: 2
- Campo: iva_calculado_iva_0  Posición: 766 Longitud:   15 Tipo: Importe Decimales: 2 (*disponible actualización 1.16b*)
- Campo: iva_calculado_iva_105 Posición: 781 Longitud:   15 Tipo: Importe Decimales: 2 (*disponible actualización 1.16b*)
- Campo: iva_calculado_iva_21 Posición: 796 Longitud:   15 Tipo: Importe Decimales: 2 (*disponible actualización 1.16b*)

### Certificacion

Campos específicos para autorizar "Certificados Primarios de Deposito, Retiro o Transferencia" (RG 3691/14).
**Ajustado al 17/10/2015 actualización 1.28a**

Campos generales para la Cabecera:

- Campo: tipo_reg             Posición:   1 Longitud:    1 Tipo: Alfanumerico Valor: 7
- Campo: pto_emision          Posición:   2 Longitud:    4 Tipo: Numerico 
- Campo: nro_orden            Posición:   6 Longitud:    8 Tipo: Numerico  
- Campo: tipo_certificado     Posición:  14 Longitud:    1 Tipo: Alfanumerico
- Campo: nro_planta           Posición:  15 Longitud:    6 Tipo: Numerico
- Campo: nro_ing_bruto_depositario Posición:  21 Longitud:   15 Tipo: Numerico
- Campo: titular_grano        Posición:  36 Longitud:    1 Tipo: Alfanumerico
- Campo: cuit_depositante     Posición:  37 Longitud:   11 Tipo: Numerico
- Campo: nro_ing_bruto_depositante Posición:  48 Longitud:   15 Tipo: Numerico
- Campo: cuit_corredor        Posición:  63 Longitud:   11 Tipo: Numerico
- Campo: cod_grano            Posición:  74 Longitud:    3 Tipo: Numerico
- Campo: campania             Posición:  77 Longitud:    4 Tipo: Numerico
- Campo: datos_adicionales    Posición:  81 Longitud:  400 Tipo: Alfanumerico
- Campo: reservado1           Posición: 481 Longitud:   14 Tipo: Alfanumerico no usar

Solo para Primaria (ex Planta Deposito Elevador):

- Campo: nro_act_depositario  Posición: 495 Longitud:    5 Tipo: Numerico
- Campo: descripcion_tipo_grano Posición: 500 Longitud:   20 Tipo: Alfanumerico
- Campo: monto_almacenaje     Posición: 520 Longitud:   10 Tipo: Importe Decimales: 2
- Campo: monto_acarreo        Posición: 530 Longitud:   10 Tipo: Importe Decimales: 2
- Campo: monto_gastos_generales Posición: 540 Longitud:   10 Tipo: Importe Decimales: 2
- Campo: monto_zarandeo       Posición: 550 Longitud:   10 Tipo: Importe Decimales: 2
- Campo: porcentaje_secado_de Posición: 560 Longitud:    5 Tipo: Importe Decimales: 2
- Campo: porcentaje_secado_a  Posición: 565 Longitud:    5 Tipo: Importe Decimales: 2
- Campo: monto_secado         Posición: 570 Longitud:   10 Tipo: Importe Decimales: 2
- Campo: monto_por_cada_punto_exceso Posición: 580 Longitud:   10 Tipo: Importe Decimales: 2
- Campo: monto_otros          Posición: 590 Longitud:   10 Tipo: Importe Decimales: 2
- Campo: reservado_calidad    Posición: 600 Longitud:   35 Tipo: Alfanumerico Decimales: 
- Campo: peso_neto_merma_volatil Posición: 635 Longitud:   10 Tipo: Importe Decimales: 2
- Campo: porcentaje_merma_secado Posición: 645 Longitud:    5 Tipo: Importe Decimales: 2
- Campo: peso_neto_merma_secado Posición: 650 Longitud:   10 Tipo: Importe Decimales: 2
- Campo: porcentaje_merma_zarandeo Posición: 660 Longitud:    5 Tipo: Importe Decimales: 2
- Campo: peso_neto_merma_zarandeo Posición: 665 Longitud:   10 Tipo: Importe Decimales: 2
- Campo: peso_neto_certificado Posición: 675 Longitud:   10 Tipo: Importe Decimales: 2
- Campo: servicios_secado     Posición: 685 Longitud:    8 Tipo: Importe Decimales: 3
- Campo: servicios_zarandeo   Posición: 693 Longitud:    8 Tipo: Importe Decimales: 3
- Campo: servicios_otros      Posición: 701 Longitud:    7 Tipo: Importe Decimales: 3
- Campo: servicios_forma_de_pago Posición: 708 Longitud:   20 Tipo: Alfanumerico

Solo para autorizar Retiro / Transferencia:

- Campo: nro_act_depositario  Posición: 495 Longitud:    5 Tipo: Numerico ***Nuevo WSLPGv1.8*** (ídem primaria)
- Campo: cuit_receptor        Posición: 728 Longitud:   11 Tipo: Numerico
- Campo: fecha                Posición: 739 Longitud:   10 Tipo: Alfanumerico 
- Campo: nro_carta_porte_a_utilizar Posición: 749 Longitud:    9 Tipo: Numerico
- Campo: cee_carta_porte_a_utilizar Posición: 758 Longitud:   14 Tipo: Numerico

Solo para autorizar Preexistentes:

- Campo: tipo_certificado_deposito_preexistente Posición: 772 Longitud:    1 Tipo: Numerico
- Campo: nro_certificado_deposito_preexistente Posición: 773 Longitud:   12 Tipo: Numerico
- Campo: cac_certificado_deposito_preexistente Posición: 785 Longitud:   14 Tipo: Numerico
- Campo: fecha_emision_certificado_deposito_preexistente Posición: 799 Longitud:   10 Tipo: Alfanumerico
- Campo: peso_neto            Posición: 809 Longitud:    8 Tipo: Numerico
- Campo: nro_planta           ver arriba ***Nuevo WSLPGv1.8***

Datos devueltos por el webservice: ***Nuevo WSLPGv1.9***

- Campo: reservado2           Posición: 817 Longitud:  183 Tipo: Numerico
- Campo: coe                  Posición: 1000 Longitud:   12 Tipo: Numerico
- Campo: fecha_certificacion  Posición: 1012 Longitud:   10 Tipo: Alfanumerico
- Campo: estado               Posición: 1022 Longitud:    2 Tipo: Alfanumerico
- Campo: reservado3           Posición: 1024 Longitud:  101 Tipo: Alfanumerico
- Campo: peso_bruto_certificado Posición: 1125 Longitud:   10 Tipo: Importe Decimales: 2
- Campo: peso_merma_secado    Posición: 1135 Longitud:   10 Tipo: Importe Decimales: 2
- Campo: peso_merma_zarandeo  Posición: 1145 Longitud:   10 Tipo: Importe Decimales: 2
- Campo: importe_iva          Posición: 1155 Longitud:   10 Tipo: Importe Decimales: 2
- Campo: servicio_gastos_generales Posición: 1165 Longitud:   10 Tipo: Importe Decimales: 2
- Campo: servicio_otros       Posición: 1175 Longitud:   10 Tipo: Importe Decimales: 2
- Campo: servicio_total       Posición: 1185 Longitud:   10 Tipo: Importe Decimales: 2
- Campo: servicio_zarandeo    Posición: 1195 Longitud:   10 Tipo: Importe Decimales: 2
- Campo: cuit_titular_planta  Posición: 1205 Longitud:   11 Tipo: Numerico
- Campo: razon_social_titular_planta Posición: 1216 Longitud:   11 Tipo: Alfanumerico

Campos no documentados ***Nuevo WSLPGv1.15***

- Campo: servicios_conceptos_no_gravados Posición: 1227 Longitud:   10 Tipo: Importe Decimales: 2
- Campo: servicios_percepciones_iva Posición: 1237 Longitud:   10 Tipo: Importe Decimales: 2
- Campo: servicios_otras_percepciones Posición: 1247 Longitud:   10 Tipo: Importe Decimales: 2

### CTG

Campos específicos para autorizar "Certificados Primarios de Deposito" (RG 3691/14) **Ajustado al 18/02/2015 actualización 1.19a**: 

- Campo: tipo_reg             Posición:   1 Longitud:    1 Tipo: Alfanumerico Valor: "C"
- Campo: nro_ctg              Posición:   2 Longitud:    8 Tipo: Numerico
- Campo: nro_carta_porte      Posición:  10 Longitud:    9 Tipo: Numerico
- Campo: porcentaje_secado_humedad Posición:  19 Longitud:    5 Tipo: Importe Decimales: 2
- Campo: importe_secado       Posición:  24 Longitud:   10 Tipo: Importe Decimales: 2
- Campo: peso_neto_merma_secado Posición:  34 Longitud:   10 Tipo: Numerico Decimales: 2
- Campo: tarifa_secado        Posición:  44 Longitud:   10 Tipo: Importe Decimales: 2
- Campo: importe_zarandeo     Posición:  54 Longitud:   10 Tipo: Importe Decimales: 2
- Campo: peso_neto_merma_zarandeo Posición:  64 Longitud:   10 Tipo: Numerico Decimales: 2
- Campo: tarifa_zarandeo      Posición:  74 Longitud:   10 Tipo: Importe Decimales: 2
- Campo: peso_neto_confirmado_definitivo Posición:  84 Longitud:   10 Tipo: Numercio Decimales: 2 ****Nuevo WSLPGv1.8**'

### Calidad

Campos específicos para calidad de "Certificados Primarios de Deposito" (RG 3691/14) **Agregado el 14/03/2015 actualización 1.23a WSLPGv1.10**: 

- Campo: tipo_reg             Posición:   1 Longitud:    1 Tipo: Alfanumerico Valor: "Q"
- Campo: analisis_muestra     Posición:   2 Longitud:   10 Tipo: Numerico 
- Campo: nro_boletin          Posición:  12 Longitud:   10 Tipo: Numerico 
- Campo: cod_grado            Posición:  22 Longitud:    2 Tipo: Alfanumerico 
- Campo: valor_grado          Posición:  24 Longitud:    4 Tipo: Importe Decimales: 3
- Campo: valor_contenido_proteico Posición:  28 Longitud:    5 Tipo: Importe Decimales: 3
- Campo: valor_factor         Posición:  33 Longitud:    6 Tipo: Importe Decimales: 3


### Det. Muestra Analisis

Campos específicos para autorizar "Certificados Primarios de Deposito" (RG 3691/14) **Ajustado al 11/02/2015 actualización 1.18a**: 

- Campo: tipo_reg             Posición:   1 Longitud:    1 Tipo: Alfanumerico Valor: "D"
- Campo: descripcion_rubro    Posición:   2 Longitud:  400 Tipo: Alfanumerico 
- Campo: tipo_rubro           Posición: 402 Longitud:    1 Tipo: Alfanumerico 
- Campo: porcentaje           Posición: 403 Longitud:    5 Tipo: Importe Decimales: 2
- Campo: valor                Posición: 408 Longitud:    5 Tipo: Importe Decimales: 2


### Factura Papel

Campos específicos para factura papel para autorizar "Liquidación Secundaria de Granos" WSLPGv1.15 **Ajustado al 29/07/2015 actualización 1.27f**:

- Campo: tipo_reg             Posición:   1 Longitud:    1 Tipo: Alfanumerico  Valor: "F" 
- Campo: nro_cai              Posición:   2 Longitud:   14 Tipo: Numerico
- Campo: nro_factura_papel    Posición:  16 Longitud:   12 Tipo: Numerico
- Campo: fecha_factura        Posición:  28 Longitud:   10 Tipo: Alfanumerico
- Campo: tipo_comprobante     Posición:  38 Longitud:    3 Tipo: Numerico

### Evento

- Campo: tipo_reg             Posición:   1 Longitud:    1 Tipo: Alfanumerico 
- Campo: codigo               Posición:   2 Longitud:    4 Tipo: Alfanumerico 
- Campo: descripcion          Posición:   6 Longitud:  250 Tipo: Alfanumerico 

### Error

- Campo: tipo_reg             Posición:   1 Longitud:    1 Tipo: Alfanumerico Valor: "R"
- Campo: codigo               Posición:   2 Longitud:    4 Tipo: Alfanumerico 
- Campo: descripcion          Posición:   6 Longitud:  250 Tipo: Alfanumerico 

### Dato

- Campo: tipo_reg             Posición:   1 Longitud:    1 Tipo: Alfanumerico Valor: 9
- Campo: campo                Posición:   2 Longitud:   25 Tipo: Alfanumerico
- Campo: valor                Posición:  27 Longitud:  250 Tipo: Alfanumerico

## Formato Tablas xBase DBF (dBase III / Fox / Clipper)

Desde la actualización 1.07a de la interfaz, ademas de manejo por archivo de texto, soporta manejo por tablas DBF. Estas tablas pueden ser generadas con cualquier librería o aplicación compatible (incluso pueden ser abiertas con planillas de cálculo).

Soporta los siguientes tipos de archivos: dBase III Plus, dBase III Plus w/memos, dBase IV, dBase IV SQL, dBase IV w/memos, dBase IV w/memos, dBase IV w/SQL table, dBase V, FoxBASE, !FoxPro w/memos, Visual !FoxPro, Visual !FoxPro (auto increment field).
Reconoce archivos con extensión .DBF, .DBT, .FPT, entre otros.

Los tipos de campos son:

- C(l): caracter (longitud)
- N(l.d): numerico (longitud y decimales)
- M: camos memo (usado para errores y mensajes extensos >250 caracteres)
- D: campos fecha

Tablas DBF de ejemplo para descargar: 

- Liquidación Primaria de Granos: [wslpg_dbf.zip](attachment:wslpg_dbf.zip)
- Liquidación Secundaria de Granos: [wslpg_dbf_lsg.zip](attachment:wslpg_dbf_lsg.zip) (LSG según WSLPGv1.6)
- Certificación de Granos: [wslpg_dbf_cg.zip](attachment:wslpg_dbf_cg.zip) (depósito F1116A, retiro/transferencia F1116RT y prexistente según WSLPGv1.6)

### Tabla Encabezado (`Encabeza.dbf`)

- tiporeg C(1) : tipo_reg
- nroorden N(17,0) : nro_orden
- cuitcompra N(11,0) : cuit_comprador
- nroactcomp N(5,0) : nro_act_comprador
- nroingbrut N(15,0) : nro_ing_bruto_comprador
- codtipoope N(2,0) : cod_tipo_operacion
- esliquidac C(1) : es_liquidacion_propia
- escanje C(1) : es_canje
- codpuerto N(4,0) : cod_puerto
- despuertol C(240) : des_puerto_localidad
- codgrano N(3,0) : cod_grano
- cuitvended N(11,0) : cuit_vendedor
- nroingbru1 N(15,0) : nro_ing_bruto_vendedor
- actuacorre C(1) : actua_corredor
- liquidacor C(1) : liquida_corredor
- cuitcorred N(11,0) : cuit_corredor
- nroingbru2 N(15,0) : nro_ing_bruto_corredor
- comisionco N(5,2) : comision_corredor
- fechapreci C(10) : fecha_precio_operacion
- precioreft N(8,3) : precio_ref_tn
- codgradore C(2) : cod_grado_ref
- codgradoen C(2) : cod_grado_ent
- factorent N(6,3) : factor_ent
- precioflet N(7,2) : precio_flete_tn
- contprotei N(6,3) : cont_proteico
- alicivaope N(5,2) : alic_iva_operacion
- campaniapp N(4,0) : campania_ppal
- codlocalid N(6,0) : cod_localidad_procedencia
- datosadici C(200) : datos_adicionales
- coe N(12,0) : coe
- coeajustad N(12,0) : coe_ajustado
- estado C(2) : estado
- totaldeduc N(17,2) : total_deduccion
- totalreten N(17,2) : total_retencion
- totalrete1 N(17,2) : total_retencion_afip
- totalotras N(17,2) : total_otras_retenciones
- totalnetoa N(17,2) : total_neto_a_pagar
- totalivarg N(17,2) : total_iva_rg_2300_07
- totalpagos N(17,2) : total_pago_segun_condicion
- fechaliqui C(10) : fecha_liquidacion
- nroopcomer N(10,0) : nro_op_comercial
- preciooper N(17,3) : precio_operacion
- subtotal N(17,2) : subtotal
- importeiva N(17,2) : importe_iva
- operacionc N(17,2) : operacion_con_iva
- totalpeson N(8,0) : total_peso_neto
- ptoemision N(4,0) : pto_emision
- codprovpro N(2,0) : cod_prov_procedencia
- pesonetosi N(8,0) : peso_neto_sin_certificado

### Tabla Certificado (`Certific.dbf`)

- tiporeg C(1) : tipo_reg
- tipocertif N(2,0) : tipo_certificado_deposito
- nrocertifi N(12,0) : nro_certificado_deposito
- pesoneto N(8,0) : peso_neto
- codlocalid N(6,0) : cod_localidad_procedencia
- codprovpro N(2,0) : cod_prov_procedencia
- reservado N(2,0) : reservado
- campania N(4,0) : campania
- fechacierr C(10) : fecha_cierre

### Tabla Retencion (`Retencio.dbf`)

- tiporeg C(1) : tipo_reg
- codigoconc C(2) : codigo_concepto
- detalleacl C(30) : detalle_aclaratorio
- basecalcul N(10,2) : base_calculo
- alicuota N(6,2) : alicuota
- nrocertifi N(14,0) : nro_certificado_retencion
- fechacerti C(10) : fecha_certificado_retencion
- importecer N(17,2) : importe_certificado_retencion
- importeret N(17,2) : importe_retencion

### Tabla Deduccion (`Deduccio.dbf`)

- tiporeg C(1) : tipo_reg
- codigoconc C(2) : codigo_concepto
- detalleacl C(30) : detalle_aclaratorio
- diasalmace N(4,0) : dias_almacenaje
- preciopkgd N(6,3) : precio_pkg_diario
- comisionga N(5,2) : comision_gastos_adm
- basecalcul N(10,2) : base_calculo
- alicuota N(6,2) : alicuota
- importeiva N(17,2) : importe_iva
- importeded N(17,2) : importe_deduccion

## Ejemplo (pseudocodigo)

El siguiente es un fragmento de código para ejemplificar la autorización de una liquidación.

Ver [Descargas](wiki:LiquidacionPrimariaGranos#Descargas) para obtener ejemplos completos en varios lenguages de programación como VB y VFP (donde debe utilizarse la función !CreateObject para crear el objeto C.O.M. y operar directamente con los métodos y propiedades del objeto, similar a los controles OCX visuales).

### Autorizar Liquidación

```
#!python

# creo el objeto interfaz con el webservice:

wslpg = CreateObject("WSLPG")

# establezco parámetros de entrada adicionales (si corresponde):

wslpg.SetParametro("peso_neto_sin_certificado", None)  # agregado v1.1 

# cargo los datos de la liquidación (internamente):

wslpg.CrearLiquidacion(
    nro_orden=1,
    cuit_comprador=23000000000, 
    nro_act_comprador=99, nro_ing_bruto_comprador=23000000000,
    cod_tipo_operacion=1,
    es_liquidacion_propia='N', es_canje='N',
    cod_puerto=14, des_puerto_localidad="DETALLE PUERTO",
    cod_grano=31, 
    cuit_vendedor=30000000007, nro_ing_bruto_vendedor=30000000007,
    actua_corredor="S", liquida_corredor="S", cuit_corredor=20267565393,
    comision_corredor=1, nro_ing_bruto_corredor=20267565393,
    fecha_precio_operacion="2013-02-07",
    precio_ref_tn=2000,
    cod_grado_ref="G1",
    cod_grado_ent="G1",
    factor_ent=98,
    precio_flete_tn=10,
    cont_proteico=20,
    alic_iva_operacion=10.5,
    campania_ppal=1213,
    cod_localidad_procedencia=3,
    datos_adicionales="DATOS ADICIONALES",
    pto_emision=1,                                  # agregado v1.1
    cod_prov_procedencia=1,                         # agregado v1.1
    peso_neto_sin_certificado=None,                 # agregado v1.1 (opcional)
    val_grado_ent=None,                             # agregado v1.1 (opcional)
    cod_localidad_procedencia_sin_certificado=None, # agregado v1.3 (opcional)
    cod_prov_procedencia_sin_certificado=None,      # agregado v1.3 (opcional)
    nro_contrato=26,                                # agregado v1.4 (opcional)
    )
wslpg.AgregarCertificado(
    tipo_certificado_dposito=5,
    nro_certificado_deposito=555501200623,
    peso_neto=1000,
    cod_localidad_procedencia=3,
    cod_prov_procedencia=1,
    campania=1213,
    fecha_cierre="2013-01-13",
    )
wslpg.AgregarRetencion(
    codigo_concepto="RI",
    detalle_aclaratorio="DETALLE DE IVA",
    base_calculo=1970,
    alicuota=10.5,
    )
wslpg.AgregarRetencion(
    codigo_concepto="RG",
    detalle_aclaratorio="DETALLE DE GANANCIAS",
    base_calculo=100,
    alicuota=15,
    )
wslpg.AgregarDeduccion(
    codigo_concepto="OD",
    detalle_aclaratorio="FLETE",
    dias_almacenaje="0",
    precio_pkg_diario=0.0,
    comision_gastos_adm=0.0,
    base_calculo=100.0,
    alicuota=21.0,
    )

# llamo al webservice con los datos cargados:

wslpg.AutorizarLiquidacion()

print "COE", wslpg.COE
print "COEAjustado", wslpg.COEAjustado
print "TootalDeduccion", wslpg.TotalDeduccion
print "TotalRetencion", wslpg.TotalRetencion
print "TotalRetencionAfip", wslpg.TotalRetencionAfip
print "TotalOtrasRetenciones", wslpg.TotalOtrasRetenciones
print "TotalNetoAPagar", wslpg.TotalNetoAPagar
print "TotalIvaRg2300_07", wslpg.TotalIvaRg2300_07
print "TotalPagoSegunCondicion", wslpg.TotalPagoSegunCondicion

# obtengo los datos adcionales desde los parametros de salida:
print "fecha_liquidacion", wslpg.GetParametro("fecha_liquidacion")
print "subtotal", wslpg.GetParametro("subtotal")
print "primer importe_retencion", wslpg.GetParametro("retenciones", 0, "importe_retencion")
print "segundo importe_retencion", wslpg.GetParametro("retenciones", 1, "importe_retencion")
print "primer importe_deduccion", wslpg.GetParametro("deducciones", 0, "importe_deduccion")

# verificacion datos de prueba:

assert wslpg.COE == 330100000357
assert wslpg.COEAjustado == None
assert wslpg.Estado == "AC"
assert wslpg.TotalPagoSegunCondicion == 1968.00         
```
### Ajuste Unificado

Ejemplo 1: Se envía una solicitud de ajuste a una liquidación que ya fue ajustada,
es decir el COE indicado en coeAjustado ya fue ajustado.

**Nota:** se agregó el campo peso_neto_total_certificado a `AgregarCertificado` por validación de AFIP *1648: Debe informar pesoNetoTotalCertificado por tratarse de un ajuste.*

```
#!python

# creo el ajuste base con los datos generales y el certificado:

wslpg.CrearAjusteBase(pto_emision=55, nro_orden=1, coe_ajustado=330100006706)
wslpg.AgregarCertificado(tipo_certificado_deposito=5,
               nro_certificado_deposito=555501200729,
               peso_neto=10000,
               cod_localidad_procedencia=3,
               cod_prov_procedencia=1,
               campania=1213,
               fecha_cierre='2013-04-15',
               peso_neto_total_certificado=10000)

# creo el ajuste de crédito (ver documentación AFIP)

wslpg.CrearAjusteCredito(
        diferencia_peso_neto=1000, diferencia_precio_operacion=100,
        cod_grado="G2", val_grado=1.0, factor=100,
        diferencia_precio_flete_tn=10,
        datos_adicionales='AJUSTE CRED UNIF',
        concepto_importe_iva_0='Alicuota Cero',
        importe_ajustar_iva_0=900,
        concepto_importe_iva_105='Alicuota Diez',
        importe_ajustar_iva_105=800,
        concepto_importe_iva_21='Alicuota Veintiuno',
        importe_ajustar_iva_21=700,
    )
wslpg.AgregarDeduccion(codigo_concepto="AL",
                       detalle_aclaratorio="Deduc Alm",
                       dias_almacenaje="1",
                       precio_pkg_diario=0.01,
                       comision_gastos_adm=1.0,
                       base_calculo=1000.0,
                       alicuota=10.5, )
wslpg.AgregarRetencion(codigo_concepto="RI",
                       detalle_aclaratorio="Ret IVA",
                       base_calculo=1000,
                       alicuota=10.5, )
# Ajuste Peso Neto WSLPGv1.17:
wslpg.AgregarCertificado(peso_neto=100,
                         coe_certificado_deposito='330100025869')

# creo el ajuste de débito (ver documentación AFIP)

wslpg.CrearAjusteDebito(
        diferencia_peso_neto=500, diferencia_precio_operacion=100,
        cod_grado="G2", val_grado=1.0, factor=100,
        diferencia_precio_flete_tn=0.01,
        datos_adicionales='AJUSTE DEB UNIF',
        concepto_importe_iva_0='Alic 0',
        importe_ajustar_iva_0=250,
        concepto_importe_iva_105='Alic 10.5',
        importe_ajustar_iva_105=200,
        concepto_importe_iva_21='Alicuota 21',
        importe_ajustar_iva_21=50,
    )
wslpg.AgregarDeduccion(codigo_concepto="AL",
                       detalle_aclaratorio="Deduc Alm",
                       dias_almacenaje="1",
                       precio_pkg_diario=0.01,
                       comision_gastos_adm=1.0,
                       base_calculo=500.0,
                       alicuota=10.5, )
wslpg.AgregarRetencion(codigo_concepto="RI",
                       detalle_aclaratorio="Ret IVA",
                       base_calculo=100,
                       alicuota=10.5, )
# Ajuste Peso Neto WSLPGv1.17:
wslpg.AgregarCertificado(peso_neto=200,
                         coe_certificado_deposito='330100025869')

# llamo al webservice para autorizar el ajuste de la liquidacion de granos

ok = wslpg.AjustarLiquidacionUnificado()

# muestro los datos generales devueltos por AFIP:

print "COE", wslpg.COE                                     # "330100013133"
print "Estado:", wslpg.Estado                              # "AC"
print "Subtotal:", wslpg.Subtotal                          # "-734.10"
print "Total IVA 10.5%", wslpg.TotalIva105                 # "0"
print "Total IVA 21%", wslpg.TotalIva21                    # "0"
print "Total Ret.Gcias.", wslpg.TotalRetencionesGanancias  # "0"
print "Total Ret.IVA", wslpg.TotalRetencionesIVA           # "-94.50"
print "Neto a Pagar", wslpg.TotalNetoAPagar                # "-639.07"
print "Total IVA RG 2300/07", wslpg.TotalIvaRg2300_07      # "94.50"
print "Total Pago S/Cond.", wslpg.TotalPagoSegunCondicion  # "-733.57"

# Obtener datos del Ajuste Credito y mostrar campos de salida:

ok = wslpg.AnalizarAjusteCredito()

print "Precio Operacion", wslpg.GetParametro("precio_operacion")  # "1.900"
print "Total Peso Neto", wslpg.GetParametro("total_peso_neto")    # "1000"
print "Total Deduccion", wslpg.TotalDeduccion                     # "11.05"
print "Total Pago S/Cond.", wslpg.TotalPagoSegunCondicion         # "2780.95"
print "Importe IVA", wslpg.GetParametro("importe_iva")            # "293.16"
print "Operacion C/IVA", wslpg.GetParametro("operacion_con_iva")  # "3085.16"
print "Importe IVA 1° Deduccion",  wslpg.GetParametro("deducciones", 0, "importe_iva")  # "1.05"

# Obtener datos del Ajuste debito y mostrar campos de salida:

ok = wslpg.AnalizarAjusteDebito()

print "Precio Operacion", wslpg.GetParametro("precio_operacion")  # "2.090"
print "Total Peso Neto", wslpg.GetParametro("total_peso_neto")    # "500"
print "Total Deduccion", wslpg.TotalDeduccion                     # "11.05"
print "Total Pago S/Cond", wslpg.TotalPagoSegunCondicion          # "2047.38"
print "Importe IVA", wslpg.GetParametro("importe_iva")            # "215.55"
print "Operacion C/IVA", wslpg.GetParametro("operacion_con_iva")  # "2268.45"
print "Importe 1° Ret.", wslpg.GetParametro("retenciones", 0, "importe_retencion") # "10.50"

```

### Ajuste Contrato

Ejemplo 1: Se envía un ajuste por contrato donde el número de contrato
ingresado que se encuentra registrado en el servicio Registración de Contratos

```
#!python

# creo el ajuste base con los datos generales y el certificado:

wslpg.CrearAjusteBase(pto_emision=55, nro_orden=1, 
                      nro_contrato=26,
                      coe_ajustado="330100013183",
                      nro_act_comprador=40, 
                      cod_grano=31,
                      cuit_vendedor=23000000019,
                      cuit_comprador=20400000000,
                      cuit_corredor=20267565393,
                      precio_ref_tn=100,
                      cod_grado_ent="G1",
                      val_grado_ent=1.01,
                      precio_flete_tn=1000,
                      cod_puerto=14,
                      des_puerto_localidad="Desc Puerto",
                      )

# creo el ajuste de crédito (ver documentación AFIP)

wslpg.CrearAjusteCredito(
        concepto_importe_iva_0='Ajuste IVA al 0%',
        importe_ajustar_iva_0=100,
    )

# creo el ajuste de débito (ver documentación AFIP)

wslpg.CrearAjusteDebito(
        concepto_importe_iva_105='Ajuste IVA al 10.5%',
        importe_ajustar_iva_105=100,
    )
wslpg.AgregarDeduccion(codigo_concepto="OD",
                       detalle_aclaratorio="Otras Deduc",
                       dias_almacenaje="1",
                       base_calculo=100.0,
                       alicuota=10.5, )

# llamo al webservice para autorizar el ajuste de la liquidacion de granos

ok = wslpg.AjustarLiquidacionContrato()

# muestro los datos generales devueltos por AFIP:

print "COE", wslpg.COE                                     
print "Estado:", wslpg.Estado                              
print "Subtotal:", wslpg.Subtotal                          
print "Total IVA 10.5%", wslpg.TotalIva105                 
print "Total IVA 21%", wslpg.TotalIva21                   
print "Total Ret.Gcias.", wslpg.TotalRetencionesGanancias 
print "Total Ret.IVA", wslpg.TotalRetencionesIVA         
print "Neto a Pagar", wslpg.TotalNetoAPagar              
print "Total IVA RG 2300/07", wslpg.TotalIvaRg2300_07     
print "Total Pago S/Cond.", wslpg.TotalPagoSegunCondicion 

# Ver ejemplo unificado para más información

# obtener campos globales no documentados (directamente desde el XML):

wslpg.AnalizarXml()
print wslpg.ObtenerTagXml("totalesUnificados", "subTotalDebCred")
print wslpg.ObtenerTagXml("totalesUnificados", "totalBaseDeducciones")
print wslpg.ObtenerTagXml("totalesUnificados", "ivaDeducciones")

```

### Ajuste Unificado Papel

Ejemplo 1: Se envía una solicitud de ajuste donde el número de formulario F1116
B informado no existe en las bases del organismo.

**NOTA**: al 26-08-2013, este método está en estudio por AFIP, por lo que ha sido removido del webservice y no está disponible.

```
#!python
wslpg.CrearAjusteBase(pto_emision=50,
                      nro_orden=1,
                      tipo_formulario=6,
                      nro_formulario="000101800999",
                      actividad=46,
                      cuit_comprador=99999999999,
                      nro_ing_bruto_comprador=99999999999,
                      tipo_operacion=1,
                      cod_grano=31,
                      cuit_vendedor=30000000007,
                      nro_ing_bruto_vendedor=30000000007,
                      cod_provincia=1,
                      cod_localidad=5)
wslpg.AgregarCertificado(tipo_certificado_deposito=5,
               nro_certificado_deposito=555501200802,
               peso_neto=10000,
               cod_localidad_procedencia=5,
               cod_prov_procedencia=1,
               campania=1213,
               fecha_cierre='2013-07-12')
wslpg.CrearAjusteCredito(
        concepto_importe_iva_21='IVA al 21%',
        importe_ajustar_iva_21=1500,
    )
wslpg.AgregarRetencion(codigo_concepto="RI",
                       detalle_aclaratorio="Ret IVA",
                       base_calculo=1500,
                       alicuota=8, )
wslpg.CrearAjusteDebito(
        concepto_importe_iva_105='IVA al 0%',
        importe_ajustar_iva_105=100,
    )

ret = wslpg.AjustarLiquidacionUnificadoPapel()

```

### Consulta Ajustes

Ejemplo para obtener importes de iva liquidado devuelto por AFIP (campos `concepto_importe_iva_105^, `importe_ajustar_iva_105` y `iva_calculado_iva_105` agregados en la actualización 1.16a):

```
#!python

ok = wslpg.ConsultarAjuste(pto_emision=50, nro_orden=1,)

ok = wslpg.AnalizarAjusteCredito()

print wslpg.GetParametro("concepto_importe_iva_105")
print wslpg.GetParametro("importe_ajustar_iva_105")
print wslpg.GetParametro("iva_calculado_iva_105")

print "primer importe_deduccion", wslpg.GetParametro("deducciones", 0, "importe_deduccion")

ok = wslpg.AnalizarAjusteDebito()

print wslpg.GetParametro("concepto_importe_iva_0")
print wslpg.GetParametro("importe_ajustar_iva_0")
print wslpg.GetParametro("iva_calculado_iva_0")

print "primer importe_deduccion", wslpg.GetParametro("deducciones", 0, "importe_deduccion")
```

Ejemplo para la obtención avanzada de campos (directamente desde tags XML, utilizable en todas las actualizaciones de la interfaz):

```
#!python

ok = wslpg.AnalizarXml()
print wslpg.ObtenerTagXml("ajusteCredito", "importes", "importeReturn", 0, "ivaCalculado") 
print wslpg.ObtenerTagXml("ajusteCredito", "importes", "importeReturn", 1, "ivaCalculado") 
print wslpg.ObtenerTagXml("ajusteDebito", "importes", "importeReturn", 0, "ivaCalculado") 
```

### Autorizar y Cancelar Anticipo de Liquidación Primaria

Ejemplo tentativo para autorizar un Anticipo de Liquidación Primaria de Granos, método remoto `lpgAutorizarAnticipo`, (*agregado en la actualización 1.28a*):

```
#!python

# Creo internamente la liquidación secundaria

wslpg.CrearLiquidacion(
pto_emision=33,
    nro_orden=1, 
    cuit_comprador='20400000000',  
    nro_act_comprador='40',
    nro_ing_bruto_comprador='123',
    cod_tipo_operacion=2,
    cod_puerto=14, des_puerto_localidad="DETALLE PUERTO",
    cod_grano=1, 
    peso_neto_sin_certificado=100,
    cuit_vendedor="30000000006",
    nro_ing_bruto_vendedor=123456,
    actua_corredor="S", liquida_corredor="S",
    cuit_corredor=wslpg.Cuit, # uso Cuit representado
    nro_ing_bruto_corredor=wslpg.Cuit,
    comision_corredor="20.6",
    fecha_precio_operacion="2015-10-10",
    precio_ref_tn=567,  ## precio_operacion=150,
    alic_iva_operacion="10.5", campania_ppal=1415,
    cod_localidad_procedencia=197,
    cod_prov_procedencia=10,
    datos_adicionales="Prueba",
    )

# Agrego los valores adicionales/repetitivos WSLPGv1.15

wslpg.AgregarRetencion(
    codigo_concepto="RI",
    detalle_aclaratorio="Retenciones IVA",
    base_calculo=100,
    alicuota=10.5, 
    )

wslpg.AgregarRetencion(
    codigo_concepto="Rg",
    detalle_aclaratorio="Retenciones GAN",
    base_calculo=100,
    alicuota=2, 
    )

wslpg.AutorizarAnticipo()

# Analizo los datos devueltos por AFIP:

print "Errores:", wslpg.Errores
print "COE", wslpg.COE

```


### Autorizar Liquidación Secundaria

Ejemplo tentativo para autorizar una Liquidación Secundaria de Granos, método remoto `lsgAutorizar`, (*agregado en la actualización 1.17a*):

```
#!python

# Creo internamente la liquidación secundaria

wslpg.CrearLiqSecundariaBase(
    pto_emision=99,
    nro_orden=1,  nro_contrato=100001232,
    cuit_comprador='20111111112',  
    nro_ing_bruto_comprador='123',
    cod_puerto=8, des_puerto_localidad="DETALLE PUERTO",
    cod_grano=2, cantidad_tn=100,
    cuit_vendedor='20222222223', nro_act_vendedor=29,
    nro_ing_bruto_vendedor=123456,
    actua_corredor='S', liquida_corredor='S',
    cuit_corredor='20267565393',
    nro_ing_bruto_corredor='20267565393',
    fecha_precio_operacion="2014-10-10",
    precio_ref_tn=100, precio_operacion=150,
    alic_iva_operacion=10.5, campania_ppal=1314,
    cod_localidad_procedencia=197,
    cod_prov_procedencia=10,
    datos_adicionales="Prueba",
    )

# Agrego los valores adicionales/repetitivos WSLPGv1.8

wslpg.AgregarDeduccion(
    codigo_concepto="",
    detalle_aclaratorio="deduccion 1",
    dias_almacenaje="",
    precio_pkg_diario=0.0,
    comision_gastos_adm=0.0,
    base_calculo=1000.0,
    alicuota=21.0,
    )

wslpg.AgregarPercepcion(
    detalle_aclaratoria="percepcion 1",
    base_calculo=1000.0,
    alicuota=21.0,
    )

wslpg.AgregarOpcional(
    codigo="1",
    descripcion="opcional",
    )

wslpg.AutorizarLiquidacionSecundaria()

# Analizo los datos devueltos por AFIP:

print "Errores:", wslpg.Errores
print "COE", wslpg.COE
```


### Ajuste Liquidación Secundaria

Ejemplo tentativo para ajustar una Liquidación Secundaria de Granos, método remoto `lsgAjustarXCoe`, (*agregado en la actualización 1.26a*):

```
#!python

# Creo internamente el ajuste de la liquidación secundaria

wslpg.CrearAjusteBase(
        pto_emision=55, nro_orden=0, coe_ajustado='330100025869',
        cod_localidad_procedencia=5544, cod_prov_procedencia=12,
        cod_puerto=14, des_puerto_localidad="DETALLE PUERTO",
        cod_grano=2,
        )

wslpg.CrearAjusteCredito(
        concepto_importe_iva_0='Alicuota Cero',
        importe_ajustar_Iva_0=900,
        concepto_importe_iva_105='Alicuota Diez',
        importe_ajustar_Iva_105=800,
        concepto_importe_iva_21='Alicuota Veintiuno',
        importe_ajustar_Iva_21=700,
        estado=None,
        coe_ajustado=None,
        datos_adicionales='AJUSTE CRED LSG',
    )

wslpg.AgregarPercepcion(
        detalle_aclaratoria='percepcion 1',
        base_calculo=1000, 
        alicuota_iva=21
        )

wslpg.CrearAjusteDebito(
        concepto_importe_iva_0='Alic 0',
        importe_ajustar_Iva_0=250,
        concepto_importe_iva_105='Alic 10.5',
        importe_ajustar_Iva_105=200,
        concepto_importe_iva_21='Alicuota 21',
        importe_ajustar_Iva_21=50,
        percepciones=[{'detalle_aclaratoria': 'percepcion 1',
                      'base_calculo': 1000, 'alicuota_iva': 21}],
        datos_adicionales='AJUSTE DEB LSG',
        )

wslpg.AgregarPercepcion(
        detalle_aclaratoria='percepcion 1',
        base_calculo=1000, 
        alicuota_iva=21
        )

ret = wslpg.AjustarLiquidacionSecundaria()

# continuar con la rutina de analisis de ajuste (similar a LPG)
```
### Autorizar Certificación

Ejemplo tentativo para autorizar una Certificación de Granos, método remoto `cgAutorizar`, (*agregado en la actualización 1.17c*), tanto para depósito (F1116A), retiro / transferencia (F1116R/T) y preexistentes, según el tipo de certificación:

- F1116A: `"P"`: Primaria
- F1116RT: `"R"`:Retiro, `"T"`: Transferencia
- `"E"`:Preexistente 

A continuación se muestran datos ficticios de prueba. Para homologación / producción debe superar todas las validaciones de AFIP

```
#!python

# Establecer el tipo de certificación:
tipo_certificado = "P"

# genero una certificación de ejemplo a autorizar (datos generales de cabecera):
wslpg.CrearCertificacionCabecera(
        pto_emision=99, nro_orden=1,  
        tipo_certificado="P", nro_planta="1",
        nro_ing_bruto_depositario="20267565393",
        titular_grano="T", 
        cuit_depositante='20111111112',  
        nro_ing_bruto_depositante='123',
        cuit_corredor='20222222223',
        cod_grano=2, campania=1314,
        datos_adicionales="Prueba", )

# establezco datos del certificado depósito F1116A:
if tipo_certificado in ('P', ):
    wslpg.AgregarCertificacionPrimaria(
            nro_act_depositario=29,
            descripcion_tipo_grano="SOJA",
            monto_almacenaje=1, monto_acarreo=2, 
            monto_gastos_generales=3, monto_zarandeo=4,
            porcentaje_secado_de=5, porcentaje_secado_a=6,
            monto_secado=7, monto_por_cada_punto_exceso=8,
            monto_otros=9, analisis_muestra=10, nro_boletin=11,
            valor_grado=1.02, 
            valor_contenido_proteico=1, valor_factor=1, 
            porcentaje_merma_volatil=15, peso_neto_merma_volatil=16, 
            porcentaje_merma_secado=17, peso_neto_merma_secado=18, 
            porcentaje_merma_zarandeo=19, peso_neto_merma_zarandeo=20,
            peso_neto_certificado=21, servicios_secado=22,  
            servicios_zarandeo=23, servicios_otros=24, 
            servicios_forma_de_pago=25,
            )
    
    wslpg.AgregarDetalleMuestraAnalisis(
            descripcion_rubro="bonif", tipo_rubro="B", porcentaje=1, valor=1)

    wslpg.AgregarCTG(
            nro_ctg="123456", nro_carta_porte=12345678,
            porcentaje_secado_humedad=1, importe_secado=2,
            peso_neto_merma_secado=3, tarifa_secado=4,
            importe_zarandeo=5, peso_neto_merma_zarandeo=6,
            tarifa_zarandeo=7, peso_neto_confirmado_definitivo=8)

# establezco datos del certificado retiro/transferencia F1116R/T:    
if tipo_certificado in ('R', 'T'):
    wslpg.AgregarCertificacionRetiroTransferencia(
            nro_act_depositario=40,
            cuit_receptor="20400000000",
            fecha="2014-11-26", 
            nro_carta_porte_a_utilizar="12345",
            cee_carta_porte_a_utilizar="123456789012",
            )

    wslpg.AgregarCertificado(
            peso_neto=10000,
            coe_certificado_deposito="123456789012", 
            )
    
# establezco datos del certificado preexistente:    
if tipo_certificado in ('E', ):
    wslpg.AgregarCertificacionPreexistente(
            tipo_certificado_deposito_preexistente=1, # "R" o "T"
            nro_certificado_deposito_preexistente="12345",
            cac_certificado_deposito_preexistente="123456789012",
            fecha_emision_certificado_deposito_preexistente="2014-11-26",
            peso_neto=1000,
            )


# Analizo los datos devueltos por AFIP:

print "Errores:", wslpg.Errores
print "COE", wslpg.COE
print "Fecha", wslpg.FechaCertificacion
```


### Descarga PDF

Ejemplo tentativo para descargar una Certificación de Granos, (*agregado en la actualización 1.25a*), indicando el nombre de archivo PDF a guardar (como 4 parámetro de los métodos de consulta) tanto para:

- `cgConsultarXCoe` depósito (F1116A), retiro / transferencia (F1116R/T), preexistentes: `WSLPG.ConsultarCertificacion(pto_emision, nro_orden, coe, pdf)`
- `lsgConsultarXCoe` liquidaciones secundarias: `WSLPG.ConsultarLiquidacionSecundaria(pto_emision, nro_orden, coe, pdf)`
- `liquidacionXCoeConsultar` liquidaciones primarias (LPG F1116B): `WSLPG.ConsultarLiquidacion(pto_emision, nro_orden, coe, pdf)`

Ejemplo para CG:
```
#!python

# Establecer los datos de certificación a consultar:
pto_emision = 99
nro_orden = 5
coe = 332000000466
pdf = 'C:\cg.pdf'                 

# consulto la certificación para guardar el PDF:
wslpg.ConsultarCertificacion(pto_emision, nro_orden, coe, pdf)
```
## Generación Form C 1116 B en PDF

La interfaz permite generar el formulario de la Liquidación Electrónica Primaria de Granos en formato PDF ("Formulario C 1116 B"). 
Basado en el anexo *RG.3419-12 - MODELO - Liquidación Primaria de Granos* (similar al del aplicativo SIAP F1116_v2r0).

Ver:

- [Plantilla de muestra](attachment:form_c1116b_plantilla_wslpg.pdf)
- [Ejemplo con datos](attachment:9957.pdf)
- [Ejemplo de Ajuste - Liquidación Primaria de Granos](attachment:ajuste_wslpg.pdf)

En el documento, se utilizan los datos enviados a AFIP y sus tablas de parámetros relacionadas (grano, puerto, localidad, etc.) pero se necesitan algunos campos adicionales (no proporcionados por el webservice):

- `nombre_comprador`: ej. "NOMBRE 1"
- `domicilio1_comprador`: ej. "DOMICILIO 1"
- `domicilio2_comprador`: ej. "DOMICILIO 1"
- `localidad_comprador`: ej. "LOCALIDAD 1"
- `iva_comprador`: ej. "R.I."
- `nombre_vendedor`: ej "NOMBRE 2"
- `domicilio1_vendedor`: ej. "DOMICILIO 2"
- `domicilio2_vendedor`: ej. "DOMICILIO 2"
- `localidad_vendedor`: "LOCALIDAD 2"
- `iva_vendedor`: ej. "R.I."
- `nombre_corredor`:  ej. "NOMBRE 3"
- `domicilio_corredor`: ej. "DOMICILIO 3

También se pueden agregar campos adicionales fijos para leyendas y aclaraciones, como ser:

- `formulario`: título, por ej: "Formulario 1116 B (prueba)"
- `art_27`: ej. "Art. 27 inc. ..."
- `forma_pago`: ej.  "Forma de Pago: 1234 pesos ..."
- `constancia`: ej. "Por la presente dejo constancia..."

Los campos adicionales se especifican por el nuevo tipo de registro 9 [DATO](wiki:LiquidacionPrimariaGranos#Dato) en el archivo de texto de intercambio, en la sección [PDF] de la configuración o llamando al método !AgregarDatoPDF

El diseño esta guardado en una plantilla csv (`liquidacion_form_c1116b_wslpg.csv`), esta se puede editar con un editor de texto, hoja de cálculo o usando nuestro [Diseñador Visual](wiki:ManualPyAfipWs#DiseñadorVisualPyFEPDF)

Ver [ métodos](wiki:LiquidacionPrimariaGranos#Metodos) y [ejemplos](wiki:LiquidacionPrimariaGranos#Descargas) o [opción `--pdf`](wiki:LiquidacionPrimariaGranos#Parámetrosporlíneadecomando) para generar el archivo, mostrarlo e imprimirlo.

**NOTA**: dato que utiliza valores devueltos por AFIP, usar el archivo de SALIDA para generar el PDF, o desde lenguajes modernos, llamar a !AutorizarLiquidacion o !ConsultarLiquidacion antes de generar el PDF

**IMPORTANTE AJUSTES**: Para los ajustes, debe completar datos con !CrearAjusteBase y luego !AjustarLiquidacionUnificado / !AjustarLiquidacionContrato o !ConsultarAjuste y completar campos adicionales no devueltos por AFIP (cod_grano, cod_grado_ent, cod_grado_ref, factor_ent, cod_puerto, cod_localidad_procedencia, cod_prov_procedencia, precio_ref_tn, precio_flete_tn, des_grado_ref, alic_iva_operacion). Ver [Ejemplo VB](https://code.google.com/p/pyafipws/source/browse/ejemplos/wslpg/wslpg_ajuste_pdf.bas) para mayor información.
### Formulario 1116B generado (imágen de ejemplo)

[[Image(99_7.png)]]
## Tablas de Parámetros

La interfaz permite obtener los diversos códigos de parámetros a utilizar. A continuación se detallan a modo de ejemplo:
### Campañas

!ConsultarCampanias() retorna las campañas habilitadas a informar en una liquidación.

| Código | Descripción |
|---|---|
| 1213 | 2012/2013 |
| 1112 | 2011/2012 |
| 1011 | 2010/2011 |
| 910 | 2009/2010 |
| 809 | 2008/2009 |
| 708 | 2007/2008 |


### Tipo Grano

!ConsultarTipoGrano() retorna Retorna los tipos de granos habilitados a informar en una liquidación.

| Código | Descripción |
|---|---|
| 1 | LINO |
| 2 | GIRASOL |
| 3 | MANI EN CAJA |
| 4 | GIRASOL DESCASCARADO |
| 5 | MANI PARA INDUSTRIA DE SELECCION |
| 6 | MANI PARA INDUSTRIA ACEITERA |
| 7 | MANI TIPO CONFITERIA |
| 8 | COLZA |
| 9 | COLZA  00    CANOLA |
| 10 | TRIGO FORRAJERO |
| 11 | CEBADA FORRAJERA |
| 12 | CEBADA APTA PARA MALTERIA |
| 14 | TRIGO CANDEAL |
| 15 | TRIGO PAN |
| 16 | AVENA |
| 17 | CEBADA CERVECERA |
| 18 | CENTENO |
| 19 | MAIZ |
| 20 | MIJO |
| 21 | ARROZ CASCARA |
| 22 | SORGO GRANIFERO |
| 23 | SOJA |
| 25 | TRIGO PLATA |
| 26 | MAIZ FLYNT O PLATA |
| 27 | MAIZ PISINGALLO |
| 28 | TRITICALE |
| 30 | ALPISTE |
| 31 | ALGODON |
| 32 | CARTAMO |
| 33 | POROTO BLANCO NATURAL OVAL Y ALUBIA |
| 34 | POROTO DISTINTO DEL BLANCO OVAL Y ALUBIA |
| 35 | ARROZ |
| 46 | LENTEJA |
| 47 | ARVEJA |
| 48 | POROTO BLANCO SELECCIONADO OVAL Y ALUBIA |
| 49 | OTRAS LEGUMBRES |
| 50 | OTROS GRANOS |
| 59 | GARBANZO |


### Grados según Grano

!ConsultarCodigoGradoReferencia() permite consultar los posibles grados a utilizar en una liquidación.


| Código | Descripción |
|---|---|
| G1 | Grado 1 |
| G2 | Grado 2 |
| G3 | Grado 3 |

### Grado y Valor según Grano Entregado

ConsultarGradoEntregadoXTipoGrano(cod_grano) recibe el código de grano a consultar, permite consultar el valor de cada grado para un determinado grano.

Ejemplo para Soja (cod_grano=23):

| Código | Descripción | Valor |
|---|---|---|
| G1 | Grado 1 | 1.01 |
| G2 | Grado 2 | 1.00 |
| G3 | Grado 3 | 0.985 |
| FG | Fuera de Grado (FG) | 0 |
| F1 | Grado 1 (FG) | 0 |
| F2 | Grado 2 (FG) | 0 |
| F3 | Grado 3 (FG) | 0 |
### Tipo Certificado de Depósito

!ConsultarTipoCertificadoDepositoConsultar() retorna los tipos de certificados de depósito habilitados en este servicio.

| Código | Descripción |
|---|---|
| 1 | F1116/RT |
| 5 | F1116/A |
| 332 | Certificado Electrónico de Depósito |
### Tipo Deducción

!ConsultarTipoDeduccion() permite consultar cuales son los tipos de deducciones posibles de informar en el array de
deducciones de la liquidación.

| Código | Descripción |
|---|---|
| CO | Comision o Gastos Administrativos |
| AL | Almacenaje |
| OD | Otras Deducciones |

### Tipo Retención

!ConsultarTipoRetencion() retorna los tipos de retenciones habilitadas en este servicio.

| Código | Descripción |
|---|---|
| RI | I.V.A. |
| RG | Impuesto a las Ganancias |
| IB | Ingresos Brutos |
| OG | Otros Gravámenes |


### Puerto

!ConsultarPuerto() permite consultar los puertos posibles de informar en una liquidación.

| Código | Descripción |
|---|---|
| 1 | SAN LORENZO/SAN MARTIN |
| 2 | ROSARIO |
| 3 | BAHIA BLANCA |
| 4 | NECOCHEA |
| 5 | RAMALLO |
| 6 | LIMA |
| 7 | DIAMANTE |
| 8 | BUENOS AIRES |
| 9 | SAN PEDRO |
| 10 | SAN NICOLAS |
| 11 | TERMINAL DEL GUAZU |
| 12 | ZARATE |
| 13 | VILLA CONSTITUCION |
| 14 | OTROS |


### Tipo Actividad

!ConsultarTipoActividad() retorna las actividades habilitadas a utilizar en este servicio.

A partir del 13 de Marzo de 2013 las actividades han cambiado, y en homologación devuelve la siguiente tabla:

| Código | Descripción |
|---|---|
| 41 | FRACCIONADOR DE GRANOS |
| 29 | ACOPIADOR - CONSIGNATARIO |
| 33 | CANJEADOR DE BIENES Y/O SERVICIOS POR GRANO |
| 40 | EXPORTADOR |
| 31 | ACOPIADOR DE MANÍ |
| 30 | ACOPIADOR DE LEGUMBRES |
| 35 | COMPRADOR DE GRANO PARA CONSUMO PROPIO |
| 44 | INDUSTRIAL ACEITERO |
| 47 | INDUSTRIAL BIOCOMBUSTIBLE |
| 46 | INDUSTRIAL BALANCEADOR |
| 48 | INDUSTRIAL CERVECERO |
| 49 | INDUSTRIAL DESTILERIA |
| 51 | INDUSTRIAL MOLINO DE HARINA DE TRIGO |
| 50 | INDUSTRIAL MOLINERO |
| 45 | INDUSTRIAL ARROCERO |
| 59 | USUARIO DE MOLIENDA DE TRIGO(incluye MAQUILA) |
| 57 | USUARIO DE INDUSTRIA (Otros granos MENOS trigo) |
| 52 | INDUSTRIAL SELECCIONADOR |
| 34 | COMPLEJO INDUSTRIAL |
| 28 | ACONDICIONADOR |
| 36 | CORREDOR |
| 55 | MERCADO DE FUTUROS Y OPCIONES O MERCADO A TERMINO |
| 39 | EXPLOTADOR DE DEPOSITO Y/O ELEVADOR DE GRANOS |
| 37 | DESMOTADOR DE ALGODON |


Antes del 13 de Marzo de 2013 las actividades listadas por el servicio eran:

| Código | Descripción |
|---|---|
| 107 | FRACCIONADOR |
| 36 | ACOPIADOR - CONSIGNATARIO |
| 92 | CANJEADOR DE BIENES Y/O SERVICIOS POR GRANO |
| 40 | EXPORTADOR |
| 106 | ACOPIADOR DE MANÍ |
| 105 | ACOPIADOR DE LEGUMBRES |
| 95 | COMPRADOR DE GRANO PARA CONSUMO PROPIO |
| 46 | INDUSTRIAL ACEITERO |
| 132 | INDUSTRIAL BIODIESEL |
| 47 | INDUSTRIAL BALANCEADOR |
| 48 | INDUSTRIAL CERVECERO |
| 94 | INDUSTRIAL DESTILERIA |
| 101 | INDUSTRIAL MOLINO DE HARINA DE TRIGO |
| 102 | INDUSTRIAL MOLINO DE HARINA DE TRIGO |
| 103 | INDUSTRIAL MOLINO DE HARINA DE TRIGO |
| 104 | INDUSTRIAL MOLINO DE HARINA DE TRIGO |
| 90 | INDUSTRIAL MOLINERO (Otras harinas MENOS de trigo) |
| 45 | INDUSTRIAL MOLINERO ARROCERO |
| 134 | USUARIO DE MOLIENDA DE TRIGO (incluye MAQUILA) |
| 96 | USUARIO DE INDUSTRIA (Otros granos MENOS trigo) |
| 49 | INDUSTRIAL SELECCIONADOR |
| 130 | COMPLEJO INDUSTRIAL |
| 43 | ACONDICIONADOR |
| 38 | CORREDOR |
| 93 | MERCADO DE FUTUROS Y OPCIONES O MERCADO A TERMINO |
| 41 | EXPLOTADOR DE DEPOSITO Y/O ELEVADOR DE GRANOS |
| 128 | DESMOTADOR DE ALGODON |

### Tipo Operación

!ConsultarTiposOperacion() permite consultar los tipos de operación posibles a realizar, dependiendo de la actividad informada en la liquidación.


| Actividad | Código Operación | Descripción |
|---|---|---|
| 107 | 1 | Compraventa de granos |
| 107 | 2 | Consignación de granos |
| 36 | 1 | Compraventa de granos |
| 36 | 2 | Consignación de granos |
| 92 | 1 | Compraventa de granos |
| 40 | 1 | Compraventa de granos |
| 106 | 1 | Compraventa de granos |
| 106 | 2 | Consignación de granos |
| 105 | 1 | Compraventa de granos |
| 105 | 2 | Consignación de granos |
| 95 | 1 | Compraventa de granos |
| 95 | 2 | Consignación de granos |
| 46 | 1 | Compraventa de granos |
| 46 | 2 | Consignación de granos |
| 132 | 1 | Compraventa de granos |
| 132 | 2 | Consignación de granos |
| 47 | 1 | Compraventa de granos |
| 47 | 2 | Consignación de granos |
| 48 | 1 | Compraventa de granos |
| 48 | 2 | Consignación de granos |
| 94 | 1 | Compraventa de granos |
| 94 | 2 | Consignación de granos |
| 101 | 1 | Compraventa de granos |
| 101 | 2 | Consignación de granos |
| 102 | 1 | Compraventa de granos |
| 102 | 2 | Consignación de granos |
| 103 | 1 | Compraventa de granos |
| 103 | 2 | Consignación de granos |
| 104 | 1 | Compraventa de granos |
| 104 | 2 | Consignación de granos |
| 90 | 1 | Compraventa de granos |
| 90 | 2 | Consignación de granos |
| 45 | 1 | Compraventa de granos |
| 45 | 2 | Consignación de granos |
| 134 | 1 | Compraventa de granos |
| 96 | 1 | Compraventa de granos |
| 49 | 1 | Compraventa de granos |
| 49 | 2 | Consignación de granos |
| 130 | 1 | Compraventa de granos |
| 130 | 2 | Consignación de granos |
| 43 | 1 | Compraventa de granos |
| 38 | 1 | Compraventa de granos |
| 38 | 2 | Consignación de granos |
| 93 | 1 | Compraventa de granos |
| 93 | 2 | Consignación de granos |
| 41 | 1 | Compraventa de granos |
| 41 | 2 | Consignación de granos |
| 128 | 1 | Compraventa de granos |
| 128 | 2 | Consignación de granos |
### Provincias

!ConsultarProvincias() Permite consultar las provincias habilitadas a informar en una liquidación mediante este
servicio.

| Código | Descripción |
|---|---|
| 1 | BUENOS AIRES |
| 0 | CAPITAL FEDERAL |
| 2 | CATAMARCA |
| 16 | CHACO |
| 17 | CHUBUT |
| 4 | CORRIENTES |
| 3 | CÓRDOBA |
| 5 | ENTRE RIOS |
| 18 | FORMOSA |
| 6 | JUJUY |
| 21 | LA PAMPA |
| 8 | LA RIOJA |
| 7 | MENDOZA |
| 19 | MISIONES |
| 20 | NEUQUÉN |
| 22 | RIO NEGRO |
| 9 | SALTA |
| 10 | SAN JUAN |
| 11 | SAN LUIS |
| 23 | SANTA CRUZ |
| 12 | SANTA FE |
| 13 | SANTIAGO DEL ESTERO |
| 24 | TIERRA DEL FUEGO |
| 14 | TUCUMÁN |
### Localidades

!ConsultarLocalidadesPorProvincia(cod_provincia) permite consultar cuales son las localidades habilitadas a informar en una liquidación para
una provincia determinada. Para lo cual deberá enviarse el código de provincia por el cual se está consultando.

Las localidades dependen de la provincia, por ej. algunas localidades al 22 de Febrero de 2013:

| Código | Descripción |
|---|---|
| 15149 | 20 DE FEBRERO |
| 23 | 3 ESQUINAS |
| 26 | 6 DE SEPTIEMBRE |
| 20410 | 9 DE JULIO |
| 15164 | 9 DE JULIO |
| 70 | ACASAPE |
| 102 | ADOLFO RODRIGUEZ SAA |
| 15176 | AGUA AMARGA |
| 147 | AGUA DEL PORTEZUELO |
| 153 | AGUA FRIA |
| 15187 | AGUA HEDIONDA |
| 156 | AGUA LINDA |
| 15190 | AGUA SALADA |
| 166 | AGUA SEBALLE |
| 15197 | AGUADA |
| 15202 | AGUADITA |
| 15205 | AGUADITAS |
| 209 | AGUAS DE PIEDRAS |
| 228 | AHI VEREMOS |
| 239 | ALANICES |
| 243 | ALAZANAS |
| 15219 | ALEGRIA |
| 316 | ALFALAND |
| 15225 | ALGARROBAL |
| 332 | ALGARROBITOS |
| 333 | ALGARROBO |
| 340 | ALGARROBOS GRANDES |
| 15240 | ALTA GRACIA |
| 387 | ALTILLO |
| 389 | ALTO |
| 394 | ALTO BLANCO |
| 408 | ALTO DE LA LENA |
| 429 | ALTO DEL LEON |
| 431 | ALTO DEL MOLLE |
| 439 | ALTO DEL VALLE |
| 20411 | ALTO DEL VALLE |
| 20380 | ALTO GRANDE |
| 15248 | ALTO GRANDE |
| 449 | ALTO LINDO |
| 452 | ALTO NEGRO |
| 454 | ALTO PELADO |
| 455 | ALTO PENCOSO |
| 15253 | ALTO VERDE |
| 533 | ANCAMILLA |
| 541 | ANCHORENA |
| 575 | ANGELITA |
| 603 | ANTIHUASI |
| 15280 | ARBOL SOLO |
| 656 | ARBOL VERDE |
| 15284 | ARBOLEDA |
| 15285 | ARBOLES BLANCOS |
| 673 | ARENILLA |
| 689 | ARIZONA |
| 763 | ARROYO DE VILCHES |
| 788 | ARROYO LA CAL |
| 15310 | AVANZADA |
| 944 | AVIADOR ORIGONE |
| 978 | BAGUAL |
| 15315 | BAJADA |
| 15317 | BAJADA NUEVA |
| 1022 | BAJO DE CONLARA |
| 1026 | BAJO DE LA CRUZ |
| 15322 | BAJO GRANDE |
| 1046 | BAJO LA LAGUNA |
| 1053 | BAJOS HONDOS |
| 15334 | BALCARCE |
| 1059 | BALDA |
| 15335 | BALDE |
| 20381 | BALDE |
| 1061 | BALDE AHUMADA |
| 1062 | BALDE DE AMIRA |
| 1063 | BALDE DE ARRIBA |
| 1064 | BALDE DE AZCURRA |
| 1065 | BALDE DE ESCUDERO |
| 1066 | BALDE DE GARCIA |
| 1067 | BALDE DE GUARDIA |
| 1068 | BALDE DE GUINAZU |
| 1069 | BALDE DE LA ISLA |
| 1071 | BALDE DE LA LINEA |
| 1074 | BALDE DE LEDESMA |
| 1077 | BALDE DE MONTE |
| 1078 | BALDE DE NUEVO |
| 1080 | BALDE DE PUERTAS |
| 1081 | BALDE DE QUINES |
| 1082 | BALDE DE TORRES |
| 1083 | BALDE DEL ESCUDERO |
| 15336 | BALDE DEL ROSARIO |
| 1089 | BALDE EL CARRIL |
| 1091 | BALDE HONDO |
| 1102 | BALDE RETAMO |
| 1107 | BALDE VIEJO |
| 15338 | BALDECITO |
| 1110 | BALDECITO LA PAMPA |
| 1385 | BANADITO |
| 1386 | BANADITO VIEJO |
| 1387 | BANADO |
| 1388 | BANADO DE CAUTANA |
| 1396 | BANADO LINDO |
| 1161 | BANDA SUD |
| 1414 | BANOS ZAPALLAR |
| 15343 | BARRANCA COLORADA |
| 15356 | BARRANQUITAS |
| 15361 | BARRIAL |
| 1210 | BARRIALES |
| 1231 | BARRIO BLANCO |
| 1342 | BARZOLA |
| 1364 | BATAVIA |
| 1416 | BEAZLEY |
| 1417 | BEBEDERO |
| 15372 | BEBIDA |
| 15373 | BECERRA |
| 1432 | BELLA ESTANCIA |
| 20522 | BELLA VISTA |
| 15389 | BELLA VISTA |
| 20382 | BELLA VISTA |
| 1482 | BILLIKEN |
| 15401 | BOCA DE LA QUEBRADA |
| 15403 | BOCA DEL RIO |
| 1554 | BOTIJAS |
| 15416 | BUENA ESPERANZA |
| 15418 | BUENA VENTURA |
| 15426 | BUENA VISTA |
| 1644 | CABEZA DE NOVILLO |
| 1674 | CACHI CORRAL |
| 1707 | CAIN DE LOS TIGRES |
| 1735 | CALDENADAS |
| 1742 | CALERA ARGENTINA |
| 1748 | CALERAS CANADA GRANDE |
| 1825 | CAMPANARIO |
| 1889 | CAMPO DE SAN PEDRO |
| 2359 | CANA LARGA |
| 15523 | CANADA |
| 20412 | CANADA |
| 2365 | CANADA ANGOSTA |
| 2367 | CANADA BLANCA |
| 2373 | CANADA DE ATRAS |
| 2382 | CANADA DE LA NEGRA |
| 2386 | CANADA DE LAS LAGUNAS |
| 2390 | CANADA DE LOS TIGRES |
| 2401 | CANADA DE VILAN |
| 2405 | CANADA DEL PASTO |
| 2408 | CANADA DEL PUESTITO |
| 15530 | CANADA GRANDE |
| 15533 | CANADA HONDA |
| 2418 | CANADA HONDA DE GUZMAN |
| 2419 | CANADA LA NEGRA |
| 2420 | CANADA LA TIENDA |
| 20413 | CANADA QUEMADA |
| 2427 | CANADA QUEMADA |
| 15540 | CANADA SAN ANTONIO |
| 15544 | CANADA VERDE |
| 15545 | CANADITAS |
| 15476 | CANDELARIA |
| 2476 | CANITAS |
| 2070 | CANTANTAL |
| 2091 | CANTERAS SANTA ISABEL |
| 2099 | CAPELEN |
| 2199 | CARMELO |
| 15491 | CAROLINA |
| 15492 | CARPINTERIA |
| 2252 | CASA DE CONDOR |
| 20414 | CASA DE PIEDRA |
| 15503 | CASA DE PIEDRA |
| 15513 | CASAS VIEJAS |
| 2297 | CASIMIRO GOMEZ |
| 15548 | CEBOLLAR |
| 15553 | CENTENARIO |
| 15563 | CERRITO |
| 2523 | CERRITO BLANCO |
| 2525 | CERRITO NEGRO |
| 15572 | CERRO BAYO |
| 15575 | CERRO BLANCO |
| 20473 | CERRO BLANCO |
| 15586 | CERRO COLORADO |
| 2587 | CERRO DE LA PILA |
| 2599 | CERRO DE ORO |
| 2600 | CERRO DE PIEDRA |
| 15598 | CERRO NEGRO |
| 20474 | CERRO NEGRO |
| 2743 | CERRO VARELA |
| 2744 | CERRO VERDE |
| 2745 | CERRO VIEJO |
| 2752 | CERROS LARGOS |
| 2770 | CHACARITAS |
| 2792 | CHACRA LA PRIMAVERA |
| 2802 | CHACRAS DEL CANTARO |
| 15611 | CHACRAS VIEJAS |
| 2821 | CHALANTA |
| 2881 | CHANAR DE LA LEGUA |
| 15629 | CHANARITOS |
| 2831 | CHANCARITA |
| 2858 | CHARLONE |
| 2859 | CHARLONES |
| 15635 | CHILCAS |
| 15639 | CHIMBAS |
| 2959 | CHIMBORAZO |
| 2967 | CHIPICAL |
| 2978 | CHISCHACA |
| 2979 | CHISCHAQUITA |
| 3002 | CHOSMES |
| 3029 | CHUTUSA |
| 3062 | CIUDAD JARDIN DE SAN LUIS |
| 3099 | COCHENELOS |
| 3100 | COCHEQUINGAN |
| 15665 | COLONIA BELLA VISTA |
| 3278 | COLONIA CALZADA |
| 3371 | COLONIA EL CAMPAMENTO |
| 3557 | COLONIA LA FLORIDA |
| 15693 | COLONIA LUNA |
| 3888 | COLONIA SANTA VIRGINIA |
| 15757 | COLONIA URDANIZ |
| 3988 | COMANDANTE GRANVILLE |
| 4005 | CONCARAN |
| 15769 | CONLARA |
| 4031 | CONSUELO |
| 4032 | CONSULTA |
| 4071 | CORONEL ALZOGARAY |
| 4117 | CORONEL SEGOVIA |
| 15781 | CORRAL DE PIEDRA |
| 4139 | CORRAL DE TORRES |
| 4143 | CORRAL DEL TALA |
| 4147 | CORRALES |
| 20415 | CORTADERAS |
| 20383 | CORTADERAS |
| 15801 | CORTADERAS |
| 4233 | CRAMER |
| 15806 | CRUCECITAS |
| 4258 | CRUZ BRILLANTE |
| 15808 | CRUZ DE CANA |
| 15810 | CRUZ DE PIEDRA |
| 15816 | CUATRO ESQUINAS |
| 20523 | CUATRO ESQUINAS |
| 4330 | CUEVA DE TIGRE |
| 4381 | DANIEL DONOVAN |
| 4457 | DIQUE LA FLORIDA |
| 20416 | DIVISADERO |
| 15829 | DIVISADERO |
| 4515 | DOMINGUEZ |
| 4537 | DORMIDA |
| 20417 | DURAZNITO |
| 15841 | DURAZNITO |
| 4606 | EL  VALLE |
| 15852 | EL AGUILA |
| 21678 | EL ALGARROBAL |
| 15874 | EL ALTO |
| 4647 | EL AMPARO |
| 15884 | EL ARENAL |
| 15886 | EL ARROYO |
| 15889 | EL BAGUAL |
| 15893 | EL BAJO |
| 15898 | EL BALDE |
| 15900 | EL BALDECITO |
| 15912 | EL BANADO |
| 20524 | EL BANADO |
| 15906 | EL BARRIAL |
| 4702 | EL BLANCO |
| 4727 | EL BURRITO |
| 4736 | EL CADILLO |
| 20525 | EL CALDEN |
| 15936 | EL CALDEN |
| 20518 | EL CALDEN |
| 20475 | EL CALDEN |
| 15939 | EL CAMPAMENTO |
| 4763 | EL CARDAL |
| 20476 | EL CARMEN |
| 15948 | EL CARMEN |
| 15960 | EL CAVADO |
| 4787 | EL CAZADOR |
| 15977 | EL CERRITO |
| 15981 | EL CERRO |
| 15988 | EL CHANAR |
| 20477 | EL CHANAR |
| 20384 | EL CHANAR |
| 20465 | EL CHANAR |
| 4825 | EL CHARABON |
| 4826 | EL CHARCO |
| 4846 | EL CHORRILLO |
| 15997 | EL CINCO |
| 16007 | EL CONDOR |
| 16009 | EL CORO |
| 4926 | EL DICHOSO |
| 16028 | EL DIQUE |
| 16045 | EL DURAZNO |
| 20478 | EL ESPINILLO |
| 16057 | EL ESPINILLO |
| 20486 | EL ESPINILLO |
| 16060 | EL FORTIN |
| 5007 | EL HORMIGUERO |
| 5008 | EL HORNITO |
| 5020 | EL INJERTO |
| 5028 | EL JARILLAL |
| 16089 | EL LECHUZO |
| 16094 | EL MANANTIAL |
| 5064 | EL MANANTIAL ESCONDIDO |
| 16098 | EL MANGRULLO |
| 16104 | EL MARTILLO |
| 5076 | EL MATACO |
| 16109 | EL MILAGRO |
| 16131 | EL MOLINO |
| 16137 | EL MOLLAR |
| 5100 | EL MOLLARCITO |
| 16142 | EL MOLLE |
| 20385 | EL MOLLE |
| 16146 | EL MORRO |
| 5117 | EL NASAO |
| 5119 | EL NEGRO |
| 16155 | EL OASIS |
| 5145 | EL OLMO |
| 5158 | EL PAJARETE |
| 16172 | EL PANTANILLO |
| 16173 | EL PANTANO |
| 5179 | EL PARAGUAY |
| 20418 | EL PARAISO |
| 16180 | EL PARAISO |
| 5186 | EL PASAJERO |
| 5197 | EL PAYERO |
| 5199 | EL PEDERNAL |
| 5201 | EL PEJE |
| 5221 | EL PICHE |
| 5224 | EL PIGUE |
| 5231 | EL PIMPOLLO |
| 16197 | EL PLATEADO |
| 16199 | EL PLUMERITO |
| 5248 | EL POCITO |
| 20419 | EL POLEO |
| 5251 | EL POLEO |
| 16205 | EL PORTEZUELO |
| 16221 | EL PORVENIR |
| 20420 | EL PORVENIR |
| 16225 | EL POTRERILLO |
| 5272 | EL POTRERO DE LEYES |
| 16234 | EL POZO |
| 16241 | EL PROGRESO |
| 16246 | EL PUEBLITO |
| 16249 | EL PUERTO |
| 16253 | EL PUESTITO |
| 20526 | EL PUESTO |
| 16258 | EL PUESTO |
| 20421 | EL PUESTO |
| 20386 | EL QUEBRACHO |
| 16273 | EL QUEBRACHO |
| 5302 | EL QUINGUAL |
| 16280 | EL RAMBLON |
| 5316 | EL RECUERDO |
| 20487 | EL RECUERDO |
| 16296 | EL RETAMO |
| 5331 | EL RIECITO |
| 20422 | EL RINCON |
| 16308 | EL RINCON |
| 20370 | EL RINCON |
| 16311 | EL RIO |
| 16316 | EL RODEO |
| 20423 | EL RODEO |
| 16325 | EL ROSARIO |
| 20424 | EL SALADO |
| 16335 | EL SALADO |
| 5346 | EL SALADO DE AMAYA |
| 20425 | EL SALTO |
| 16344 | EL SALTO |
| 16345 | EL SALVADOR |
| 5357 | EL SARCO |
| 16356 | EL SAUCE |
| 5365 | EL SEMBRADO |
| 16372 | EL SOCORRO |
| 20387 | EL SOCORRO |
| 16384 | EL TALA |
| 20527 | EL TALA |
| 16390 | EL TALITA |
| 20479 | EL TALITA |
| 20426 | EL TALITA |
| 20388 | EL TALITA |
| 5417 | EL TEMBLEQUE |
| 5430 | EL TORCIDO |
| 5433 | EL TORO MUERTO |
| 16406 | EL TOTORAL |
| 20389 | EL TOTORAL |
| 20427 | EL VALLE |
| 16424 | EL VALLE |
| 20428 | EL VALLECITO |
| 16429 | EL VALLECITO |
| 20488 | EL VERANO |
| 16433 | EL VERANO |
| 16436 | EL VOLCAN |
| 5502 | EL YACATAN |
| 16437 | EL ZAMPAL |
| 16444 | EL ZAPALLAR |
| 5527 | ELEODORO LOBOS |
| 5538 | EMBALSE LA FLORIDA |
| 16454 | ENSENADA |
| 16460 | ENTRE RIOS |
| 16471 | ESPINILLO |
| 5666 | ESTABLECIMIENTO LAS FLORES |
| 5736 | ESTACION ZANJITAS |
| 16479 | ESTANCIA |
| 5741 | ESTANCIA 30 DE OCTUBRE |
| 5782 | ESTANCIA DON ARTURO |
| 5792 | ESTANCIA EL CHAMICO |
| 5797 | ESTANCIA EL DIVISADERO |
| 5800 | ESTANCIA EL MEDANO |
| 5807 | ESTANCIA EL QUEBRACHAL |
| 5811 | ESTANCIA EL SALADO |
| 5813 | ESTANCIA EL SAUCECITO |
| 16484 | ESTANCIA GRANDE |
| 5835 | ESTANCIA LA BLANCA |
| 5851 | ESTANCIA LA GUARDIA |
| 5852 | ESTANCIA LA GUILLERMINA |
| 5861 | ESTANCIA LA MORENA |
| 5872 | ESTANCIA LA RESERVA |
| 5877 | ESTANCIA LA UNION |
| 5881 | ESTANCIA LA ZULEMITA |
| 5883 | ESTANCIA LAS BEBIDAS |
| 5908 | ESTANCIA LOS HERMANOS |
| 5913 | ESTANCIA LOS NOGALES |
| 5942 | ESTANCIA RIVADAVIA |
| 5948 | ESTANCIA SAN ALBERTO |
| 16489 | ESTANCIA SAN ANTONIO |
| 5951 | ESTANCIA SAN FRANCISCO |
| 16496 | ESTANCIA SAN ROQUE |
| 5978 | ESTANCIA TRES ARBOLES |
| 16501 | ESTANZUELA |
| 6080 | FAVELLI |
| 6091 | FENOGLIO |
| 16522 | FLORIDA |
| 6201 | FORTIN EL PATRIA |
| 6221 | FORTIN SALTO |
| 16526 | FORTUNA |
| 6232 | FORTUNA DE SAN JUAN |
| 6236 | FRAGA |
| 6268 | FRISIA |
| 6400 | GENERAL PEDERNERA |
| 6415 | GENERAL URQUIZA |
| 6432 | GIGANTE |
| 6444 | GLORIA A DIOS |
| 6503 | GORGONTA |
| 6547 | GRUTA DE INTIHUASI |
| 6573 | GUALTARAN |
| 16552 | GUANACO |
| 6581 | GUANACO PAMPA |
| 6602 | GUASQUITA |
| 6646 | GUZMAN |
| 6716 | HINOJITO |
| 6718 | HINOJOS |
| 16567 | HIPOLITO YRIGOYEN |
| 6743 | HORNITO |
| 6786 | HUALTARAN |
| 6813 | HUCHISSON |
| 6819 | HUEJEDA |
| 6824 | HUERTAS |
| 6978 | INTIHUASI |
| 16586 | INVERNADA |
| 7010 | ISLA |
| 20371 | ISLA |
| 7073 | ISLITAS |
| 16600 | ISONDU |
| 7130 | JARILLA |
| 7202 | JUAN JORBA |
| 7207 | JUAN LLERENA |
| 7219 | JUAN W GEZ |
| 7222 | JUANA KOSLAY |
| 7225 | JUANTE |
| 7266 | JUSTO DARACT |
| 16622 | LA ADELA |
| 7293 | LA AGUA NUEVA |
| 16627 | LA AGUADA |
| 20519 | LA AGUADA |
| 20466 | LA AGUADA |
| 20480 | LA AGUADA |
| 7295 | LA AGUADA DE LAS ANIMAS |
| 7298 | LA AGUEDA |
| 20467 | LA ALAMEDA |
| 16638 | LA ALAMEDA |
| 7303 | LA ALCORTENA |
| 7304 | LA ALEGRIA |
| 16639 | LA ALIANZA |
| 16640 | LA AMALIA |
| 7312 | LA AMARGA |
| 16643 | LA ANGELINA |
| 16648 | LA ANGOSTURA |
| 16653 | LA ARBOLEDA |
| 16660 | LA ARGENTINA |
| 16668 | LA ARMONIA |
| 7332 | LA AROMA |
| 16673 | LA ATALAYA |
| 20489 | LA AURORA |
| 16676 | LA AURORA |
| 20429 | LA AURORA |
| 20468 | LA BAJADA |
| 16680 | LA BAJADA |
| 7363 | LA BAVA |
| 7364 | LA BAVARIA |
| 7371 | LA BERTITA |
| 7379 | LA BOLIVIA |
| 7383 | LA BONITA |
| 16703 | LA BREA |
| 20390 | LA BREA |
| 7397 | LA CABRA |
| 7400 | LA CALAGUALA |
| 7403 | LA CALDERA |
| 16711 | LA CALERA |
| 20391 | LA CANADA |
| 16743 | LA CANADA |
| 20490 | LA CANADA |
| 20481 | LA CANADA |
| 16726 | LA CARMEN |
| 7425 | LA CARMENCITA |
| 16735 | LA CAUTIVA |
| 16749 | LA CELIA |
| 7468 | LA CHANARIENTA |
| 7470 | LA CHERINDU |
| 16758 | LA CHILCA |
| 20372 | LA CHILCA |
| 7478 | LA CHILLA |
| 16773 | LA CIENAGA |
| 16780 | LA COCHA |
| 16783 | LA COLINA |
| 20491 | LA COLONIA |
| 16791 | LA COLONIA |
| 16805 | LA CORA |
| 16806 | LA CORINA |
| 16809 | LA CORTADERA |
| 16816 | LA COSTA |
| 7538 | LA CRISTINA |
| 7539 | LA CRUCECITA |
| 16834 | LA CUMBRE |
| 16839 | LA DELIA |
| 7565 | LA DONOSTIA |
| 16845 | LA DORA |
| 7571 | LA DUDA |
| 20392 | LA DULCE |
| 16850 | LA DULCE |
| 16851 | LA ELENA |
| 16852 | LA ELENITA |
| 7579 | LA ELIDA |
| 7581 | LA ELISA |
| 20430 | LA ELVIRA |
| 16858 | LA ELVIRA |
| 16861 | LA EMILIA |
| 7588 | LA EMMA |
| 7589 | LA EMPAJADA |
| 7600 | LA ERNESTINA |
| 20528 | LA ESCONDIDA |
| 20492 | LA ESCONDIDA |
| 16866 | LA ESCONDIDA |
| 16869 | LA ESMERALDA |
| 20431 | LA ESPERANZA |
| 16881 | LA ESPERANZA |
| 20493 | LA ESPERANZA |
| 7612 | LA ESPESURA |
| 20432 | LA ESQUINA |
| 16889 | LA ESQUINA |
| 7614 | LA ESQUINA DEL RIO |
| 16896 | LA ESTANCIA |
| 16899 | LA ESTANZUELA |
| 16910 | LA ESTRELLA |
| 20494 | LA ESTRELLA |
| 7628 | LA ETHEL |
| 16912 | LA EULOGIA |
| 7644 | LA FELISA |
| 7646 | LA FINCA |
| 16926 | LA FLECHA |
| 16942 | LA FLORIDA |
| 20433 | LA FLORIDA |
| 20469 | LA FLORIDA |
| 20495 | LA FLORIDA |
| 20520 | LA FLORIDA |
| 7656 | LA FRAGUA |
| 7667 | LA GAMA |
| 7671 | LA GARRAPATA |
| 7672 | LA GARZA |
| 16956 | LA GAVIOTA |
| 16957 | LA GERMANIA |
| 7678 | LA GITANA |
| 16961 | LA GRAMILLA |
| 16969 | LA GUARDIA |
| 7702 | LA HERMOSURA |
| 16981 | LA HIGUERITA |
| 16982 | LA HOLANDA |
| 7711 | LA HORTENSIA |
| 16991 | LA HUERTA |
| 7716 | LA HUERTITA |
| 7719 | LA IBERIA |
| 17000 | LA INVERNADA |
| 7730 | LA IRENE |
| 17006 | LA ISABEL |
| 17013 | LA ISLA |
| 7744 | LA JAVIERA |
| 7745 | LA JERGA |
| 7746 | LA JOSEFA |
| 20496 | LA JOSEFA |
| 17019 | LA JOSEFINA |
| 7749 | LA JUANA |
| 17021 | LA JUANITA |
| 20497 | LA JUANITA |
| 17022 | LA JULIA |
| 7754 | LA JUSTA |
| 7762 | LA LAURA |
| 7765 | LA LECHUGA |
| 17041 | LA LEGUA |
| 7777 | LA LINDA |
| 17048 | LA LINEA |
| 17055 | LA LOMA |
| 17064 | LA LUISA |
| 17069 | LA MAGDALENA |
| 17072 | LA MAJADA |
| 17078 | LA MARAVILLA |
| 17083 | LA MARGARITA |
| 7819 | LA MARGARITA CARLOTA |
| 17086 | LA MARIA |
| 7823 | LA MARIA ESTHER |
| 17088 | LA MARIA LUISA |
| 17089 | LA MAROMA |
| 17092 | LA MASCOTA |
| 20498 | LA MASCOTA |
| 7841 | LA MEDIA LEGUA |
| 7843 | LA MEDULA |
| 7845 | LA MELINA |
| 17099 | LA MERCED |
| 17105 | LA MESILLA |
| 7855 | LA MINA |
| 17106 | LA MODERNA |
| 17113 | LA NEGRA |
| 17114 | LA NEGRITA |
| 17115 | LA NELIDA |
| 17121 | LA NUTRIA |
| 17134 | LA PALMIRA |
| 17142 | LA PAMPA |
| 17149 | LA PATRIA |
| 17157 | LA PEREGRINA |
| 7947 | LA PETRA |
| 17171 | LA PLATA |
| 17179 | LA PORFIA |
| 7983 | LA PORTADA |
| 17203 | LA PRIMAVERA |
| 20482 | LA PRIMAVERA |
| 17209 | LA PROVIDENCIA |
| 17214 | LA PUERTA |
| 17224 | LA QUEBRADA |
| 17235 | LA RAMADA |
| 20373 | LA RAMADA |
| 20434 | LA RAMADA |
| 8032 | LA REALIDAD |
| 17246 | LA REFORMA |
| 17247 | LA REINA |
| 17253 | LA REPRESA |
| 8044 | LA REPRESITA |
| 17255 | LA RESERVA |
| 8049 | LA RESISTENCIA |
| 17262 | LA RINCONADA |
| 8056 | LA RIOJITA |
| 17268 | LA ROSADA |
| 17270 | LA ROSALIA |
| 8066 | LA ROSINA |
| 8074 | LA SALA |
| 8079 | LA SALUD |
| 8080 | LA SALVADORA |
| 8082 | LA SANDIA |
| 17285 | LA SEGUNDA |
| 17287 | LA SELVA |
| 17290 | LA SENA |
| 8093 | LA SERRANA |
| 8100 | LA SILESIA |
| 17293 | LA SIRENA |
| 17304 | LA SUIZA |
| 17313 | LA TIGRA |
| 17319 | LA TOMA |
| 17322 | LA TOSCA |
| 20393 | LA TOTORA |
| 20435 | LA TOTORA |
| 17323 | LA TOTORA |
| 8143 | LA TRANCA |
| 17329 | LA TRAVESIA |
| 8150 | LA TULA |
| 8153 | LA TUSCA |
| 8155 | LA ULBARA |
| 20374 | LA UNION |
| 17339 | LA UNION |
| 20394 | LA UNION |
| 8159 | LA URUGUAYA |
| 8161 | LA VACA |
| 8171 | LA VENECIA |
| 20395 | LA VERDE |
| 17349 | LA VERDE |
| 20436 | LA VERTIENTE |
| 17353 | LA VERTIENTE |
| 8197 | LA YERBA BUENA |
| 17367 | LA YESERA |
| 8219 | LAFINUR |
| 17382 | LAGUNA BRAVA |
| 8256 | LAGUNA CAPELEN |
| 8263 | LAGUNA DE LA CANADA |
| 8267 | LAGUNA DE LOS PATOS |
| 8268 | LAGUNA DE PATOS |
| 17390 | LAGUNA LARGA |
| 8304 | LAGUNA SAYAPE |
| 17396 | LAGUNA SECA |
| 8364 | LAS AGUADAS |
| 17421 | LAS AROMAS |
| 17423 | LAS BAJADAS |
| 17428 | LAS BARRANCAS |
| 20396 | LAS BARRANCAS |
| 8390 | LAS BARRANQUITAS |
| 20437 | LAS BARRANQUITAS |
| 17435 | LAS CABRAS |
| 17448 | LAS CANAS |
| 17454 | LAS CANITAS |
| 17437 | LAS CANTERAS |
| 8413 | LAS CARITAS |
| 8414 | LAS CAROLINAS |
| 8417 | LAS CARRETAS |
| 17463 | LAS CHACRAS |
| 8433 | LAS CHACRAS DE SAN MARTIN |
| 20438 | LAS CHACRAS DE SAN MARTIN |
| 17468 | LAS CHACRITAS |
| 17469 | LAS CHILCAS |
| 17471 | LAS CHIMBAS |
| 8444 | LAS CLARITAS |
| 17475 | LAS COLONIAS |
| 17484 | LAS CORTADERAS |
| 17501 | LAS DELICIAS |
| 17504 | LAS ENCADENADAS |
| 20439 | LAS FLORES |
| 17512 | LAS FLORES |
| 8489 | LAS GALERAS |
| 17514 | LAS GAMAS |
| 8499 | LAS GITANAS |
| 20440 | LAS HIGUERAS |
| 17526 | LAS HIGUERAS |
| 8522 | LAS ISLITAS |
| 20499 | LAS LAGUNAS |
| 20441 | LAS LAGUNAS |
| 17549 | LAS LAGUNAS |
| 20397 | LAS LAGUNITAS |
| 17550 | LAS LAGUNITAS |
| 17553 | LAS LAJAS |
| 17559 | LAS LOMAS |
| 20442 | LAS LOMAS |
| 8547 | LAS MANGAS |
| 17572 | LAS MARTINETAS |
| 8556 | LAS MELADAS |
| 8561 | LAS MESIAS |
| 8563 | LAS MESTIZAS |
| 17596 | LAS NIEVES |
| 17603 | LAS PALMAS |
| 17614 | LAS PALOMAS |
| 17619 | LAS PAMPITAS |
| 17626 | LAS PENAS |
| 17634 | LAS PIEDRITAS |
| 17638 | LAS PLAYAS |
| 8623 | LAS PLAYAS ARGENTINAS |
| 8627 | LAS PRADERAS |
| 17639 | LAS PUERTAS |
| 8635 | LAS RAICES |
| 8641 | LAS ROSADAS |
| 17652 | LAS ROSAS |
| 17661 | LAS SALINAS |
| 8665 | LAS TIGRAS |
| 17678 | LAS TOSCAS |
| 17681 | LAS TOTORITAS |
| 8679 | LAS TRES CANADAS |
| 17698 | LAS VISCACHERAS |
| 8722 | LAURA ELISA |
| 8730 | LAVAISSE |
| 17708 | LEANDRO N ALEM |
| 8783 | LIBORIO LUNA |
| 8801 | LINCE |
| 8806 | LINDO |
| 17726 | LOMA DEL MEDIO |
| 17748 | LOMAS BLANCAS |
| 17750 | LOMITAS |
| 8928 | LONGARI |
| 8943 | LOS AGUADOS |
| 17762 | LOS ALAMOS |
| 20443 | LOS ALAMOS |
| 17764 | LOS ALGARROBITOS |
| 20444 | LOS ALGARROBOS |
| 17770 | LOS ALGARROBOS |
| 8960 | LOS ALMACIGOS |
| 8972 | LOS ARADITOS |
| 8976 | LOS ARCES |
| 8978 | LOS ARGUELLOS |
| 17781 | LOS ARROYOS |
| 17790 | LOS BARRIALES |
| 17799 | LOS CAJONES |
| 9023 | LOS CARRICITOS |
| 17810 | LOS CERRILLOS |
| 20398 | LOS CERRILLOS |
| 17813 | LOS CERRITOS |
| 9040 | LOS CESARES |
| 20375 | LOS CHANARES |
| 17819 | LOS CHANARES |
| 20500 | LOS CHANARES |
| 20529 | LOS CHANARES |
| 17822 | LOS CHANARITOS |
| 9046 | LOS CHANCAROS |
| 9052 | LOS CHENAS |
| 17825 | LOS CISNES |
| 17827 | LOS CLAVELES |
| 9071 | LOS COMEDEROS |
| 9072 | LOS COMEDORES |
| 17834 | LOS CONDORES |
| 9083 | LOS COROS |
| 17838 | LOS CORRALES |
| 17840 | LOS CORRALITOS |
| 9092 | LOS CUADROS |
| 17844 | LOS DOS RIOS |
| 9105 | LOS DUEROS |
| 9106 | LOS DURAZNITOS |
| 17845 | LOS DURAZNOS |
| 9112 | LOS ESPINILLOS |
| 9113 | LOS ESQUINEROS |
| 9153 | LOS HINOJOS |
| 17860 | LOS HUAYCOS |
| 17862 | LOS JAGUELES |
| 9173 | LOS LECHUZONES |
| 9178 | LOS LOBOS |
| 20445 | LOS LOBOS |
| 17873 | LOS MANANTIALES |
| 9188 | LOS MEDANITOS |
| 17876 | LOS MEDANOS |
| 9193 | LOS MENBRILLOS |
| 9194 | LOS MENDOCINOS |
| 9208 | LOS MOLLECITOS |
| 20446 | LOS MOLLES |
| 20376 | LOS MOLLES |
| 17890 | LOS MOLLES |
| 9211 | LOS MONTES |
| 17904 | LOS NOQUES |
| 9236 | LOS OSCUROS |
| 9250 | LOS PASITOS |
| 17919 | LOS PEJES |
| 9262 | LOS PEROS |
| 9274 | LOS POLEOS |
| 17936 | LOS POZOS |
| 17940 | LOS PUESTOS |
| 9287 | LOS PUQUIOS |
| 17945 | LOS QUEBRACHOS |
| 17950 | LOS RAMBLONES |
| 9316 | LOS ROLDANES |
| 20447 | LOS SAUCES |
| 17961 | LOS SAUCES |
| 17966 | LOS TALAS |
| 20448 | LOS TALAS |
| 9349 | LOS TAMARINOS |
| 9351 | LOS TAPIALES |
| 9356 | LOS TELARIOS |
| 17967 | LOS TIGRES |
| 9383 | LOS VALLES |
| 17979 | LUJAN |
| 9470 | MACHAO |
| 9563 | MANANTIAL |
| 20449 | MANANTIAL |
| 9564 | MANANTIAL BLANCO |
| 9565 | MANANTIAL DE FLORES |
| 9567 | MANANTIAL DE RENCA |
| 17994 | MANANTIAL GRANDE |
| 9569 | MANANTIAL LINDO |
| 18002 | MANANTIALES |
| 9594 | MANTILLA |
| 18008 | MARAVILLA |
| 9632 | MARAY |
| 9692 | MARLITO |
| 9693 | MARMOL VERDE |
| 9699 | MARTIN DE LOYOLA |
| 9723 | MATACO |
| 9785 | MEDANO BALLO |
| 9787 | MEDANO CHICO |
| 9790 | MEDANO GRANDE |
| 18029 | MEDANOS |
| 18035 | MEDIA LUNA |
| 18039 | MERCEDES |
| 18042 | MERLO |
| 18045 | MILAGRO |
| 18047 | MINA CAROLINA |
| 9896 | MINA LOS CONDORES |
| 9907 | MINA SANTO DOMINGO |
| 18067 | MOLLECITO |
| 18071 | MONTE CARMELO |
| 10044 | MONTE CHIQUITO |
| 10046 | MONTE COCHEQUINGAN |
| 18089 | MONTE VERDE |
| 18102 | MOSMOTA |
| 10130 | MOYAR |
| 10131 | MOYARCITO |
| 10163 | NAHUEL MAPA |
| 10185 | NARANJO |
| 10191 | NASCHEL |
| 10197 | NAVIA |
| 18113 | NEGRO MUERTO |
| 10231 | NILINAST |
| 10246 | NO ES MIA |
| 10254 | NOGOLI |
| 10263 | NOSSAR |
| 10281 | NUEVA CONSTITUCION |
| 18118 | NUEVA ESCOCIA |
| 18123 | NUEVA ESPERANZA |
| 10287 | NUEVA GALIA |
| 15144 | NURILAY |
| 18138 | OJO DE AGUA |
| 20450 | OJO DE AGUA |
| 10352 | OJO DEL RIO |
| 10384 | ONCE DE MAYO |
| 18149 | OTRA BANDA |
| 10467 | PAINES |
| 10477 | PAJE |
| 10494 | PALIGUANTA |
| 18183 | PALOMAR |
| 18187 | PAMPA |
| 10572 | PAMPA DE LOS GOBERNADORES |
| 10577 | PAMPA DEL BAJO |
| 10587 | PAMPA DEL TAMBORERO |
| 20451 | PAMPA GRANDE |
| 18192 | PAMPA GRANDE |
| 10605 | PAMPA INVERNADA |
| 10648 | PAMPITA |
| 10660 | PANTANILLO |
| 10661 | PANTANILLOS |
| 18202 | PAPAGAYOS |
| 18205 | PARAISO |
| 18210 | PASO ANCHO |
| 10794 | PASO DE CUERO |
| 18211 | PASO DE LA CRUZ |
| 10803 | PASO DE LA TIERRA |
| 18214 | PASO DE LAS CARRETAS |
| 10809 | PASO DE LAS SALINAS |
| 10810 | PASO DE LAS SIERRAS |
| 10811 | PASO DE LAS TOSCAS |
| 10812 | PASO DE LAS VACAS |
| 18216 | PASO DE LOS ALGARROBOS |
| 10815 | PASO DE LOS BAYOS |
| 18217 | PASO DE LOS GAUCHOS |
| 10829 | PASO DE PIEDRA |
| 10844 | PASO DEL MEDIO |
| 18222 | PASO DEL REY |
| 18223 | PASO GRANDE |
| 10865 | PASO JUAN GOMEZ |
| 10873 | PASO LOS ALGARROBOS |
| 10913 | PASTAL |
| 10932 | PATIO LIMPIO |
| 10960 | PEDERNERA |
| 10987 | PENICE |
| 11034 | PENON COLORADO |
| 11017 | PESCADORES |
| 11077 | PICOS YACU |
| 18242 | PIE DE LA CUESTA |
| 18247 | PIEDRA BLANCA |
| 11086 | PIEDRA BOLA |
| 18252 | PIEDRA LARGA |
| 11104 | PIEDRA ROSADA |
| 11106 | PIEDRA SOLA |
| 18257 | PIEDRAS ANCHAS |
| 18262 | PIEDRAS BLANCAS |
| 11112 | PIEDRAS CHATAS |
| 11166 | PIQUILLINES |
| 11184 | PISCOYACO |
| 11191 | PIZARRAS BAJO VELEZ |
| 11199 | PLACILLA |
| 11207 | PLANTA DE SANDIA |
| 11235 | PLUMERITO |
| 18272 | POCITOS |
| 11279 | POLLEDO |
| 11305 | PORTADA DEL SAUCE |
| 18280 | PORTEZUELO |
| 18285 | PORVENIR |
| 11347 | POSTA DE FIERRO |
| 11350 | POSTA DEL PORTEZUELO |
| 18289 | POTRERILLO |
| 11376 | POTRERO DE LOS FUNES |
| 11402 | POZO CAVADO |
| 18304 | POZO CERCADO |
| 11426 | POZO DE LAS RAICES |
| 11432 | POZO DE LOS RAYOS |
| 11445 | POZO DEL CARRIL |
| 11452 | POZO DEL ESPINILLO |
| 18318 | POZO DEL MEDIO |
| 18320 | POZO DEL MOLLE |
| 18322 | POZO DEL TALA |
| 18325 | POZO ESCONDIDO |
| 11482 | POZO FRIO |
| 11507 | POZO SANTIAGO |
| 18337 | POZO SECO |
| 11509 | POZO SIMON |
| 11534 | PRIMER AGUA |
| 11689 | PUENTE HIERRO |
| 11691 | PUENTE LA ORQUETA |
| 18369 | PUERTA COLORADA |
| 18370 | PUERTA DE LA ISLA |
| 11727 | PUERTA DE PALO |
| 18376 | PUERTO ALEGRE |
| 18378 | PUERTO RICO |
| 11897 | PUESTITO |
| 11915 | PUESTO BELLA VISTA |
| 11950 | PUESTO DE LOS JUMES |
| 11963 | PUESTO DE TABARES |
| 11985 | PUESTO EL TALA |
| 12063 | PUESTO PAMPA INVERNADA |
| 12065 | PUESTO QUEBRADA CAL |
| 12074 | PUESTO ROBERTO |
| 12085 | PUESTO TALAR |
| 18403 | PUNILLA |
| 18409 | PUNTA DE AGUA |
| 12126 | PUNTA DE LA LOMA |
| 12127 | PUNTA DE LA SIERRA |
| 12134 | PUNTA DEL ALTO |
| 18417 | PUNTA DEL CERRO |
| 18427 | PUNTOS DE AGUA |
| 12171 | PUNTOS DE LA LINEA |
| 18431 | QUEBRACHITO |
| 12189 | QUEBRADA DE LA BURRA |
| 12190 | QUEBRADA DE LA MORA |
| 12191 | QUEBRADA DE LOS BARROSOS |
| 12196 | QUEBRADA DE SAN VICENTE |
| 12199 | QUEBRADA DEL TIGRE |
| 18440 | QUEBRADA HONDA |
| 12247 | QUINES |
| 12307 | RAMADITA |
| 18456 | RAMBLONES |
| 12346 | RANQUELCO |
| 12364 | REAL |
| 12387 | RECONQUISTA |
| 18464 | RECREO |
| 12399 | REFORMA CHICA |
| 12417 | RENCA |
| 12425 | REPRESA DEL CARMEN |
| 12426 | REPRESA DEL CHANAR |
| 20399 | REPRESA DEL MONTE |
| 18469 | REPRESA DEL MONTE |
| 18471 | RETAMO |
| 12440 | RETAZO DEL MONTE |
| 18473 | RETIRO |
| 12467 | RIECITO |
| 12516 | RINCON DEL CARMEN |
| 12518 | RINCON DEL ESTE |
| 18509 | RIO GRANDE |
| 12597 | RIO JUAN GOMEZ |
| 12616 | RIO QUINTO |
| 12635 | RIOJITA |
| 12654 | RODEO CADENAS |
| 12684 | ROMANCE |
| 18541 | ROSALES |
| 18544 | RUMIGUASI |
| 18548 | SALADILLO |
| 18552 | SALADO |
| 12821 | SALADO DE AMAYA |
| 18555 | SALINAS |
| 12842 | SALINAS DEL BEBEDERO |
| 12850 | SALITRAL |
| 12859 | SALTO CHICO |
| 18565 | SAN AGUSTIN |
| 18572 | SAN ALBERTO |
| 12876 | SAN ALEJANDRO |
| 20400 | SAN ANTONIO |
| 18597 | SAN ANTONIO |
| 20501 | SAN ANTONIO |
| 20470 | SAN ANTONIO |
| 20464 | SAN ANTONIO |
| 18615 | SAN CAMILO |
| 18624 | SAN CARLOS |
| 18631 | SAN CELESTINO |
| 12953 | SAN FCO DEL MONTE DE ORO |
| 18654 | SAN FELIPE |
| 18663 | SAN FERNANDO |
| 18683 | SAN GERONIMO |
| 18687 | SAN GREGORIO |
| 18703 | SAN IGNACIO |
| 20502 | SAN ISIDRO |
| 20452 | SAN ISIDRO |
| 18714 | SAN ISIDRO |
| 20503 | SAN JORGE |
| 18739 | SAN JORGE |
| 20401 | SAN JORGE |
| 18754 | SAN JOSE |
| 20453 | SAN JOSE |
| 20504 | SAN JOSE |
| 13024 | SAN JOSE DE LOS CHANARES |
| 13037 | SAN JOSE DEL DURAZNO |
| 18769 | SAN JUAN |
| 13052 | SAN JUAN DE TASTU |
| 20454 | SAN LORENZO |
| 18793 | SAN LORENZO |
| 18803 | SAN LUIS |
| 20402 | SAN MARTIN |
| 18821 | SAN MARTIN |
| 20455 | SAN MARTIN |
| 20377 | SAN MIGUEL |
| 20471 | SAN MIGUEL |
| 18835 | SAN MIGUEL |
| 20456 | SAN MIGUEL |
| 13106 | SAN NICOLAS PUNILLA |
| 18847 | SAN PABLO |
| 20483 | SAN PEDRO |
| 20521 | SAN PEDRO |
| 18864 | SAN PEDRO |
| 20457 | SAN PEDRO |
| 18877 | SAN RAFAEL |
| 13132 | SAN RAIMUNDO |
| 18885 | SAN RAMON |
| 20458 | SAN RAMON |
| 13139 | SAN RAMON SUD |
| 20403 | SAN ROQUE |
| 18896 | SAN ROQUE |
| 13147 | SAN RUFINO |
| 18903 | SAN SALVADOR |
| 18925 | SAN VICENTE |
| 20404 | SAN VICENTE |
| 13176 | SANT ANA |
| 20378 | SANTA ANA |
| 18938 | SANTA ANA |
| 18954 | SANTA CATALINA |
| 18958 | SANTA CECILIA |
| 18965 | SANTA CLARA |
| 20459 | SANTA CLARA |
| 20472 | SANTA CLARA |
| 20484 | SANTA CLARA |
| 13201 | SANTA DIONISIA |
| 13211 | SANTA FELISA |
| 20405 | SANTA ISABEL |
| 19000 | SANTA ISABEL |
| 20485 | SANTA ISABEL |
| 20379 | SANTA LUCIA |
| 19011 | SANTA LUCIA |
| 13226 | SANTA LUCINDA |
| 20460 | SANTA MARIA |
| 20505 | SANTA MARIA |
| 19028 | SANTA MARIA |
| 13242 | SANTA MARTINA |
| 19042 | SANTA RITA |
| 19056 | SANTA ROSA |
| 20406 | SANTA ROSA |
| 13257 | SANTA ROSA DE CONLARA |
| 13265 | SANTA ROSA DEL GIGANTE |
| 19059 | SANTA RUFINA |
| 13272 | SANTA SIMONA |
| 19066 | SANTA TERESA |
| 20407 | SANTA TERESA |
| 19069 | SANTA TERESITA |
| 19071 | SANTA VICTORIA |
| 20506 | SANTO DOMINGO |
| 19084 | SANTO DOMINGO |
| 20408 | SANTO DOMINGO |
| 19111 | SAUCE |
| 19115 | SAUCESITO |
| 13399 | SELCI |
| 13414 | SERAFINA |
| 13503 | SOCOSCORA |
| 20461 | SOL DE ABRIL |
| 13505 | SOL DE ABRIL |
| 13506 | SOL DE ABRIL  DPTO SAN MARTIN |
| 13533 | SOLOBASTA |
| 13534 | SOLOLOSTA |
| 19174 | TALA VERDE |
| 13714 | TALARCITO |
| 19178 | TALITA |
| 13732 | TAMASCANES |
| 13739 | TAMBOREO |
| 13781 | TASTO |
| 13791 | TAZA BLANCA |
| 13805 | TEMERARIA |
| 13859 | TILISARAO |
| 13885 | TINTITACO |
| 13920 | TOIGUS |
| 13921 | TOINGUA |
| 13956 | TORO BAYO |
| 13964 | TORO NEGRO |
| 13983 | TOSCAL |
| 19205 | TOTORAL |
| 20462 | TOTORAL |
| 19208 | TOTORILLA |
| 14014 | TRANSVAL |
| 14015 | TRAPICHE |
| 19215 | TRAVESIA |
| 14023 | TRECE DE ENERO |
| 14024 | TREINTA DE OCTUBRE |
| 14045 | TRES CANADAS |
| 20409 | TRES CANADAS |
| 19240 | TRES LOMAS |
| 19241 | TRES MARIAS |
| 14082 | TRES PUERTAS |
| 14142 | TUKIROS |
| 14181 | UCHAIMA |
| 14196 | UNION |
| 19265 | UNQUILLO |
| 14217 | USIYAL |
| 14220 | USPARA |
| 14238 | VACAS MUERTAS |
| 14254 | VALLE DE LA PANCANTA |
| 19273 | VALLE HERMOSO |
| 14274 | VALLE SAN AGUSTIN |
| 14275 | VALLE SAN JOSE |
| 19276 | VALLECITO |
| 14285 | VARELA |
| 14317 | VENTA DE LOS RIOS |
| 14358 | VIEJA ESTANCIA |
| 14490 | VILLA DE LA QUEBRADA |
| 14495 | VILLA DE PRAGA |
| 19291 | VILLA DEL CARMEN |
| 19294 | VILLA DOLORES |
| 19297 | VILLA ELENA |
| 14576 | VILLA GENERAL ROCA |
| 14636 | VILLA LARCA |
| 14662 | VILLA LUISA |
| 14763 | VILLA REYNOLDS |
| 14815 | VILLA SANTIAGO |
| 14902 | VIRARCO |
| 14911 | VISCACHERAS |
| 19350 | VISTA ALEGRE |
| 14918 | VISTA HERMOSA |
| 14924 | VIVA LA PATRIA |
| 14931 | VIZCACHERAS |
| 14940 | VOLCAN ESTANZUELA |
| 14989 | YACORO |
| 15079 | ZAMPAL |


### Problemas frecuentes

Los siguientes errores que han surgido desde el servidor de AFIP y en ciertos casos hemos consultado a la Mesa de Ayuda para ver como se pueden solucionar. 
Hasta el momento, ninguno es un problema de la interfaz, la mayoría es causada por validaciones (ver [Datos de Prueba](wiki:LiquidacionPrimariaGranos#DatosdePrueba) abajo) y otros han sido producidos por cuestiones internas de los servicios web de AFIP que en general han sido corregidos por el organismo:

- Error `1646: Informar procedencia (codProvProcedenciaSinCertificado/codLocalidadProcedenciaSinCertificado) o Certificados, no ambos.`: **WSLPGv1.3** aparentemente hay que completar dos nuevos campos `cod_prov_procedencia_sin_certificado / cod_localidad_procedencia_sin_certificado` (soportado a partir de la actualización 1.10a)
- Error `1524: El importe neto a pagar no puede ser negativo`: Aparentemente no estaba validando el importe total, pero el error no figura en la documentación oficial y no es un dato enviado hacia la AFIP del que se tenga control (es una campo de la respuesta aparentemente calculado por AFIP). Sucede tanto cuando se envía certificado de depósito o cuando se utiliza el campo `peso_neto_sin_certificado`. **Solución:** originalmente sucedia con cualquier combinación de datos, pero ahora el cálculo parece estar solucionado en AFIP. Revisar peso neto, precio de referencia, retenciones y deducciones (el importe con deducciones y retenciones debe ser mayor a 0).
- Error `1521: El precio por Kg. de la operacion no puede ser negativo`: aparentemente valida el precio final de la operació (este error tampoco figura en la documentación oficial). Revisar el `precio_ref_tn` y `precio_flete_tn` (este último debería ser significativamente menor que el precio de referencia).
- Error `1712: El usuario esta intentando procesar dos liquidaciones simultaneamente`: El código de error no se corresponde a la documentación (`Se puede ingresar mas de una deducción para el concepto OD - "Otras Deducciones", para el resto de los conceptos se debe ingresar solo una deducción`), y sucede tanto si se envían o no deducciones, certificados, etc. **Solución:** ya ha sido solucionado automáticamente por AFIP, en el futuro devolverá `700: Error de sincronismo`.
- Error `1401: El número ingresado no se corresponde con un Certificado de Depósito Intransferible (F 1116/A) y/o Retiro y Transferencias de Granos Certificados y No comercializados (F 1116 RT) con CAC otorgado` y `1411: El certificado de deposito ya fue liquidado anteriormente por otra CUIT`: **Solución**: en pruebas (homologación), solo se puede usar los números de certificado: 555501200623 para F1116 A y 111101200623 para F1116 RT. Otros numeros que ha pasado AFIP para pruebas son F1116 A 555501200822, F1116 RT 111101200866, F1116 A 555501200827, F1116 RT 111101200871. En caso de no corresponder certificado de depósito, no enviarlos y completar campo `peso_neto_sin_certificado`
- Error `1850: La alícuota ingresada para la retención de I.V.A. no se corresponde con la situacion fiscal del vendedor.` y `1850: La alícuota ingresada para la retención de Impuesto a las Ganancias no se corresponde con la situacion fiscal del vendedor`: **Solución**: revisar `alicuota` en retenciones (por ej. 10.5 % para IVA, 15 % para Ganancias).
- Error `1851: La liquidacion no tiene retenciones de IVA.` y `1807: Retencion (Concepto - IMPUESTO GANANCIAS) sin informar.`: las retenciones son obligatorias si no es canje total (`es_canje='T'`). Si no corresponden, se puede enviar `base_calculo` en 0.
- Error `1106: La actividad seleccionada no corresponde al comprador`: revisar `nro_act_comprador` y `cod_tipo_operacion`, ver `--actividades` (`ConsultarTipoActividad`)  y `--operaciones` (`ConsultarTiposOperacion`) habilitadas para la CUIT indicada. **Tip:** usar un CUIT de un acopiador, consignatario, comprador de granos o similar. **Nuevo:** consultar actividades inscriptas en el RUOCA con `--actividadesrep` (`ConsultarTipoActividadRepresentado`)
- Error `1611: Si liquida comprador el cuit del comprador debe ser igual al cuit representado`: revisar las CUIT indicadas (el cuit representado se indica en el archivo de configuración `WSLPG.INI` o con el atributo `WSLPG.Cuit`). En homologación, usar el mismo CUIT que figura en el certificado.

Inconvenientes con trámites en AFIP:

- Falla SOAP `ns3: Receiver [common_003] La CUIT del usuario representado ... no se encuentra habilitado por el Administrador de Relaciones de la AFIP`: revisar que el CUIT representado se indica en el archivo de configuración `WSLPG.INI` o con el atributo `WSLPG.Cuit` este habilitado en producción (en homologación, usar el mismo CUIT que figura en el certificado).

Errores posibles al Ajustar Liquidación (WSLPGv1.4):

- Falla SOAP `1509: Error al generar el nro de COE. [common_009] No se puede procesar esta operación momentáneamente. Por favor intente más tarde.`
- Error `1909: El coe ya registra un ajuste activo del tipo seleccionado.`
- Error `2100: El contrato ingresado no se encuentra registrado.`
- Error `2001: No existe CAC para el F 1116 ingresado.`
- Error `1207: Incumplimiento RG3342: La CUIT del Vendedor ingresado no cumplió con la RG 3342 con respecto a la Información de Producción de:  Soja Campaña de Presentación 1314`

Validaciones y errores **WSLPGv1.6** / **WSLPGv1.7** (liquidación secundaria y certificación de granos, algunos son nuevos mensajes no documentados en la especificación técnica de AFIP):

- Error `1100: El comprador no esta registrado en el RUOCA.`
- Error `1202: El vendedor presenta inconvenientes en el Domicilio Fiscal`
- Error `1208: Matrícula inactiva, no habilitada o no informada por MINAGRI`
- Error `1001: Faltan parametros obligatorios en metodo : armaCertificadosLiquidacion`
- Error `1509: Error al generar el nro de COE. Error de acceso a la base de datos - ORA-06550: line 1, column 7: PLS-00201: identifier 'LPG_NRO_COMP_LS_AFIP' must be declared ORA-06550: line 1, column 7: PL/SQL: Statement ignored`
- Error `3201: El depositante no tiene asociada la planta indicada`


Validaciones y errores **WSLPGv1.8** (aparentemente errores internos por inconsistencias en los datos de prueba):

- Error `3056: Una de las remesas elegidas por el usuario, no esta dentro de las remesas certificables. Número de CTG: ...`
- Error `3059: No existen CTG asociadas al certificado que se quiere dar de alta.`
- Error `3109: El depositario no puede retirar o transferir ya que no tiene una actividad valida para poder retirar o transferir`
- Error `3201: La planta indicada no existe o no posee una actividad valida para la solicitud del certificado.` (revisar nuevo parámetro `nro_planta` en `AgregarCertificacionPreexistente`
- Error `3105: No se encontro un certificado de deposito con los parametros ingesados o no tiene saldo de kilos a retirar/transferir.` (revisar certificado y kilos agregado a la certificación )

Problemas internos de los servidores de AFIP::

- Error `600: No existen datos en las bases de la Administración según los parámetros de búsqueda informados`: aparentemente los datos enviados no coinciden con ninguna liquidación realizada (métodos !AjustarLiquidacion o !ConsultarLiquidacion)
- Error `500: Error General de Aplicacion` y `800: Servicio no disponible`: es devuelto por el servidor cuando no está operativo, se debe reintentar ya que es un error interno del webservice de AFIP.
- Falla `SOAP: ns2:Server helper.ImpresionHelper.crearPDFTransactionalConexion(Lnet/sf/jasperreports/engine/JasperReport;Ljava/util/Map;Lnet/sf/jasperreports/engine/export/JRPdfExporter;)[B`: aparentemente sería un problema interno de AFIP que no genera los PDF al consultar, reintentar con otro CG/LSG/LPG


Validaciones y errores **WSLPGv1.20** (se incorporan validaciones por SISA)

- Error `1850: La alícuota ingresada para la retención de (IVA/Impuesto a las Ganancias) no se corresponde con la situación fiscal del vendedor.` Revisar Campo: <retencion><alicuota>  
- Error `4000: Error accediendo a SISA`: Es devuelto por el servidor cuando no tiene acceso al servicio SISA, se debe reintentar más tarde ya que es un error interno.
- Error `4001: La CUIT corredor no se encuentra inscripta en SISA.`
- Error `4002: La CUIT comprador no posee una categoría válida o no se encuentra inscripta en SISA.` Revisar Campo: <cuitComprador>
- Error `4003: Falta información de SISA para el vendedor.`
- Errores `4004, 4005 y 4007: Error al determinar retención`
- Error `4006: La CUIT ingresada no posee un estado válido para emitir el comprobante ó no se encuentra inscripta en SISA.`
- Error `4008: La CUIT vendedor no posee una categoría válida en SISA.` Revisar Campo:<cuitVendedor>
- Error `4100: La CUIT emisor no posee una categoría válida o no se encuentra inscripta en SISA.`
- Error `4102: La CUIT depositante no posee una categoría válida o no se encuentra inscripta en SISA.`
- Error `4103: La CUIT receptor no posee una categoría válida o no se encuentra inscripta en SISA.`
- Error `4200: La CUIT vendedor no se encuentra inscripta en SISA.` Revisar Campo: <cuitVendedor>
- Error `4201: La CUIT Comprador no se encuentra inscripta en SISA.` Revisar Campo: <cuitComprador>


### Historial de Cambios

- 29 Mar 2015: ajuste de formato de intercambio (3 posiciones para tipo_certificado_deposito) y nuevos métodos `BuscarCTG` y `BuscarCertConSaldoDisponible` (CG) 
- 7 Mar 2015: ajuste de formato de intercambio (campos devueltos por autorizar según ejemplos WSLPGv1.9), y nuevos métodos anular y consultar (CG y LSG)
- 11 Feb 2015: ajuste de campos en el formato de archivo de intercambio (nuevo instalador - actualización 1.18a)
- 16 Dic 2014: agrego nuevo tipo de certificado electrónico de depósito (332) y ajustes acumulados
- 3 Dic 2014: ajustes acumulados para WSLPGv1.7 (nuevo instalador - actualización 1.17f)
- 26 Nove 2014: ajustes acumulados para WSLPGv1.6 (nuevo instalador - actualización 1.17d)
- Nov 2014: ajustes iniciales para "Liquidación Secundaria" (RG3689) y "Certificación de granos" (RG3690) 
- Mar 2014: ajustes menores (WSLPGv1.5)
- Sep 2: WSLPGv1.4 (Ajustes): Se agregan métodos `AsociarLiquidacionAContrato`, `ConsultarLiquidacionesPorContrato`, `ConsultarAjuste` y los respectivos parametros `--asociar`, `--consultar_por_contrato`, `--consultar_ajuste`
- Ago 26:  WSLPGv1.4 (Ajustes): Se agregan campos peso_neto_total_certificado, se actualizan ejemplos, archivo de intercambio, errores frecuentes
- Ago 8: WSLPGv1.4 (Ajustes): Se actualizan ejemplos, actualización del archivo de intercambio, errores frecuentes
- Jul 29: WSLPGv1.4 (Ajustes): Se agregan métodos y atributos tentativos
- May 31: Ajustes menores (instalador, métodos, etc.)
- Abr 12: WSLPGv1.3: Se agregan atributos y cambios menores 
- Abr 9: WSLPGv1.2 y datos de prueba
- Mar 13: Se agregan métodos para generar PDF, se describen problemas frecuentes de AFIP y ajustes generales
- Mar  9: WSLPGv1.1: Se agregan atributos pto_emision, cod_prov_procedencia y peso_neto_sin_certificado, se ajustan métodos !CrearLiquidacion, !ConsultarLiquidacion, !ConsultarUltNroOrden. Se actualizan formato, documentación y ejemplos.
- Mar  7: Se agrega metodos para establecer/recuperar parámetros
- Mar  6: Ajuste de campos del archivo de intercambio (fecha_liquidacion y datos retenciones/deducciones)
- Mar  5: Plantilla Form 1116B de muestra en PDF
- Mar  4: Documentación de métodos adicionales v1.02a (!AjustarLiquidacion, !AnularLiquidacion, etc.)
- Mar  1: Ajustes menores
- Feb 26: Publicación de la versión inicial para desarrollo (v1.01a)
- Feb 22: Creación de esta página


## Costos y Condiciones

(ver [Condiciones del Soporte Comercial](wiki:PyAfipWs#CostosyCondiciones))



Consultar por presupuestos y soluciones a medida.

**Importante:** dado a que todavía los ajustes para WSLPGv1.6 / WSLPGv1.8 no han sido definidos y confirmados por AFIP, estamos analizando las modificaciones y el costo del soporte comercial para "Liquidación Secundaria de Granos" (RG3689) y "Certificación de Granos" (RG3690) está actualmente en estudio.

Para soporte sin cargo de la comunidad, revisar la [lista de temas](http://code.google.com/p/pyafipws/issues/list?can=1&q=) y/o [crear uno nuevo](http://code.google.com/p/pyafipws/issues/entry). 
Por novedades y consultas genereales, puede usar el  [Google Groups](https://groups.google.com/forum/#!forum/pyafipws) (Foro Público).
Código fuente en [Google Code](https://code.google.com/p/pyafipws/source/browse/).

A su vez, se libera el código fuente bajo licencia GPL (software libre), al igual que se hizo con el restos de los servicios web. Para más detalles ver página FacturaElectronica.

### Contacto

Para mayor información, consultar por mail a  info@sistemasagiles.com.ar o telefónicamente al (011) 15-3048-9211

Se recuerda que esta disponible el 
[grupo de noticias](http://www.pyafipws.com.ar) (http://groups.google.com.ar/group/pyafipws) donde
se publicarán futuras novedades sobre PyAfipWS: servicios web de
factura electrónica y sus interfases (se recomienda suscribirse)


MarianoReingart
MarianoReingart