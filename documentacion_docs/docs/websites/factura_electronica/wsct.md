# Factura Electrónica Comprobantes Turismo (RG3971, 566)
[[TracNav(noreorder|FacturaElectronica)]]

Interfaz para Servicio Web correspondiente a Comprobantes de Turismo (Factura Electrónica T).
Régimen de reintegro del impuesto al valor agregado (TurIVA), facturado por los servicios de alojamiento prestados a turistas del extranjero.
Operaciones "alcanzadas por el beneficio de Reintegro del IVA Decreto 1043/2016"
## Índice
[[Image(htdocs:logo-pyafipws.png, align=right)]]
[[TOC(noheading,inline,depth=3)]]

## Descripción General

EL WSCT es un nuevo Servicio Web de la AFIP para el 
*Régimen especial para el reintegro de IVA a turistas extranjeros por los servicios de alojamiento.*, correspondiente a la 
[Resolución Conjunta General 3971 y Resolución 566/2016](http://servicios.infoleg.gob.ar/infolegInternet/anexos/270000-274999/270043/norma.htm) 

**NOTA**: Ver [WSFEv1](wiki:ProyectoWSFEv1) para el Régimen General de Factura Electrónica

### Sujetos alcanzados

Hoteles, hosterías, pensiones, hospedajes, moteles, campamentos, apart-hoteles y similares, así como las agencias de turismo del país habilitadas por el MINISTERIO DE TURISMO, que revistan el carácter de responsables inscriptos en el impuesto al valor agregado, por las operaciones sujetas a reintegro, y como único documento válido para respaldar las mismas, deberán emitir electrónicamente los comprobantes especificados.

### Comprobantes

Service de Comprobante T destinados a Servicios de Alojamiento a Turistas Extranjeros. V0.1:

- Factura clase “T” (código 195).
- Nota de débito clase “T” (código 196).
- Nota de crédito clase “T” (código 197).

[Modelo de comprobante clase “T”](http://biblioteca.afip.gob.ar/pdfp/RG_3971_AFIP_A2.jpg) (imágen)

[DATOS MÍNIMOS QUE DEBEN CONTENER LOS COMPROBANTES CLASE “T”](http://biblioteca.afip.gob.ar/dcp/REAG01003971_2016_12_28#anexo01__)
 
## Estado

La AFIP publicó la [información técnica](http://www.afip.gov.ar/ws/wsct/Manual_Desarrollador_WSCT_v01.pdf) (v1.0.0 con fecha 10/05/2017).

Al 23 de Junio, el servicio ya está en funcionamiento en homologación, pudiendose autorizar una factura y obtener un CAE.
Al 29 de Junio, el servicio ya está habilitada la URL de producción.


Validaciones Preliminares AFIP:

- 100: La CUIT emisora no se encuentra activa en el Sistema Registral
- 1106: No existen puntos de venta habilitados para utilizar en el presente ws.
- 5000: Error interno [E-20170618-15:41:13.619-20267565393-vii]

Se debe solicitar acceso por mesa de ayuda de AFIP para realizar pruebas para homologación.

En producción, se debe ingresar al "Administrador de Relaciones de Clave Fiscal", sitio web AFIP:

- Adherir nuevo servicio, webservice "Servicio	Web Service Comprobantes T"
- Crear nueva relación, seleccionando el certificado (alias computador fiscal) y el webservice a utilizar.

### WSCTv1.1

El 23/06/2017 AFIP publicó la versión [WSCTv1.1](http://www.afip.gob.ar/fe/documentos/Manual_Desarrollador_WSCT_v11.pdf) que sólo contempla temas menores (cambios en validaciones y agrega estructura general `info` opcional en los
mensajes de respuesta). 

### RG5616/2024 FEv4

ARCA estableció nuevos criterios de Facturación para las operaciones realizadas en moneda extranjera.

Ver["Resolución 5616/24"](https://www.boletinoficial.gob.ar/detalleAviso/primera/318374/20241218)

- Se afregan nuevos campos al método `CrearFactura(...)`:

                            - `cancela_misma_moneda_ext`

- Nuevos Metodos auxiliares:

                            - `ParamGetCotizacion(moneda_id, fecha)`: se agrega fecha de cotizacion

Se agregan nuevas validaciones.

Aplicación:  Obligatorio para webservice a partir del 15 de Abril de 2025. (Prorrogado 1 de Julio 2025)

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

Adicionalmente, borrar la carpeta cache donde se encuentran descargada la descripcion del servicio web (WSDL), por si esta desactuializada.

Eventualmente utilizar el siguiente instalador para actualizar la carpeta cache:

https://www.sistemasagiles.com.ar/soft/pyafipws/final/PyAfipWS-Cache-UPDATE-2025.4.6.exe
### URL

- https://fwshomo.afip.gov.ar/wsct/CTService?wsdl (homologación)
- https://serviciosjava.afip.gob.ar/wsct/CTService?wsdl (producción)

## Descargas

### Instalador

Ver archivos y últimas actualizaciones para descargas en [GitHub](https://github.com/reingart/pyafipws/releases) (actualizado):

- Instalador:  [PyAfipWs-2.7.1976-32bit+wsaa_2.11c+wsct_1.02c-homo.exe](https://www.sistemasagiles.com.ar/soft/pyafipws/PyAfipWs-2.7.1976-32bit+wsaa_2.11c+wsct_1.02c-homo.exe)
- [Manual de Uso](wiki:ManualPyAfipWs): Documentación ([PDF](http://www.sistemasagiles.com.ar/trac/wiki/ManualPyAfipWs?format=pdf)) [Documentación Oficial PDF AFIP](http://www.afip.gov.ar/ws/wsct/Manual_Desarrollador_WSCT_v01.pdf)
- Código Fuente (Python): [wsct.py](https://github.com/reingart/pyafipws/blob/master/wsct.py)
 
### Ejemplos

- Visual Basic: [turismo.bas](https://github.com/reingart/pyafipws/blob/master/ejemplos/wsct/turismo.bas) (vb5, vb6)
- Visual Fox Pro: [turismo.prg](https://github.com/reingart/pyafipws/blob/master/ejemplos/wsct/turismo.prg) (vfp5, vfp9.0)

Para más ejemplos ver [(Delphi, Java, Power Builder, Clarion, Fujitsu Net Cobol, .NET), [repositorio](https://github.com/reingart/pyafipws/tree/master/ejemplos)(wiki:PyAfipWs]), o consultar [Soporte Comercial](wiki:FacturaElectronicaComprobantesTurismo#CostosyCondiciones).
### Archivos de Intercambio

- [attachment:entrada.txt]: archivo de entrada (texto ancho fijo, estilo COBOL y similares)
- [attachment:salida.txt]: archivo de salida (texto ancho fijo, estilo COBOL y similares)
- [attachment:tablas-dbf-recet.zip]: archivos con tablas DBF (compatible con dBase, Fox Pro, Clipper y otros)
- [attachment:factura_t.json]: archivos JSON (compatible con !JavaScript, Java, PHP y otros)

Ver [Formato Archivos de Intercambio](wiki:FacturaElectronicaComprobantesTurismo#FormatoarchivosdeIntercambio) para más información 
## Instalación

Está disponible el instalador (ver [Descargas](wiki:FacturaElectronicaComprobantesTurismo#Descargas)), simplemente descargar, ejecutar seguir los pasos:

- Aceptar la licencia
- Seleccionar carpeta, por ej `C:\WSCT`
- Instalación y registración automática

Para más información ver el [Manual de Uso](wiki:ManualPyAfipWs#Instalación)

## Componente

### Objeto

- El objeto COM se crea invocando a !CreateObject("WSCT")

### Métodos

Métodos principales:

- **`Conectar(cache, wsdl, proxy)`**: realiza la conexión a los servidores de la AFIP (primer paso esencial). Si no se especifica url del wsdl, se utiliza servidores de homologación. El parámetro cache es un directorio donde se almacenan internamente la descripción del servicio (archivo WSDL) para mayor optimización. Proxy es un string con la información del servidor intermedio: "usuario:clave@servidor:puerto"
- **`Dummy()`**: servicio de prueba para obtener el estado de los servidores de la AFIP.

- **`CrearFactura(tipo_doc, nro_doc, tipo_cbte, punto_vta, cbte_nro, imp_total, imp_tot_conc, imp_neto, imp_subtotal, imp_trib, imp_op_ex, imp_reintegro, fecha_cbte, id_impositivo, cod_pais, domicilio, cod_relacion, moneda_id, moneda_ctz, observaciones)`**: crea internamente una factura para luego poder autorizarla, recibe los datos de la factura a emitir. Ver ejemplo para el detalle de los parámetros.
- **`AgregarIva(id, base_imp, importe)`**: agrega internamente un subtotal de IVA a una factura para luego poder autorizarla, recibe los datos del tipo de alícuota, base imponible e importe. Ver ejemplo para el detalle de los parámetros.
- **`AgregarTributo(id, Desc, base_imp, alic, importe)`**: agrega internamente un subtotal de tributo a una factura para luego poder autorizarla, recibe los datos del impuesto nacional, provincial o municipal (descripción), base imponible e importe. Ver ejemplo para el detalle de los parámetros.
- **`AgregarCmpAsoc(tipo, pto_vta, nro, cuit)`**: agrega internamente un comprobante asociado a una factura para luego poder autorizarla, recibe tipo de comprobante, punto de venta y número. Ver ejemplo para el detalle de los parámetros. 
- **`AgregarItem(tipo, codigo_turismo, codigo, ds, iva_id, imp_iva, imp_subtotal,)`**: agrega internamente un item (linea de factura) a una factura para luego poder autorizarla, recibe los datos del item a factura a emitir. Ver ejemplo para el detalle de los parámetros.
- **`AgregarFormaPago(codigo, tipo_tarjeta, numero_tarjeta, swift_code, tipo_cuenta, numero_cuenta)`**: agrega una forma de pago, solo código es obligatorio


- **`AutorizarComprobante()`**: autoriza la emisión de factura electrónica, devuelve el Código de Autorización Electrónico (CAE). Ver [ejemplo](wiki:FacturaElectronicaComprobantesTurismo##EjemploPseudocodigo).


Métodos auxiliares:

- **`EstablecerCampoFactura(campo, valor)`**: establece individualmente el valor de un campo del encabezado de la factura, devuelve True si el campo pertenece al encabezado y se ha actualizado correctamente (ver ejemplo)
- **`EstablecerCampoItem(campo, valor)`**: establece individualmente el valor de un campo del detalle de la factura (último item agregado), devuelve True si el campo pertenece al encabezado y se ha actualizado correctamente (ver ejemplo)


Métodos secundarios:

- **`ConsultarComprobante(tipo_cbte, punto_vta, cbte_nro)`**: recupera los datos de una factura autorizada, recibe tipo de comprobante, punto de venta y número de comprobante original, y devuelve el Código de Autorización Electrónico (CAE) obtenido en su momento. A su vez, establece los datos de la factura (Cae, !FechaCbte, !ImpTotal, !ImpNeto). Ver ejemplo para el detalle de los parámetros y valores devueltos.
- **`CompUltimoAutorizado(tipo_cbte, punto_vta)`**: recupera el último número de factura autorizada, recibe tipo de comprobante y punto de venta. Ver WSFE.RecuperaLastCMP
- **`ConsultarMonedas()`**, **`ConsultarTiposComprobante()`**, **`ConsultarTiposDocumento()`**, **`ConsultarAlicuotasIVA()`**, **`ConsultarCondicionesIVA()`**, **`ConsultarTiposItem()`**, **`ConsultarTiposTributo()`**, **`ConsultarCUITsPaises()`**, **`ConsultarPaises()`**, **`ConsultarTiposDatosAdicionales()`**, **`ConsultarFomasPago()`**, **`ConsultarTiposTarjeta(forma_pagoa)`**, **`ConsultarTiposCuenta()`**, **`ConsultarTiposTributo()`**: recupera valores referenciales de códigos de las tablas de parámetros, devuelve una lista de strings con el id/código, descripción del parámetro y vigencia -si corresponde- (ver ejemplos). Más información en [Tablas de Parámetros](wiki:FacturaElectronicaComprobantesTurismo#TablasdeParámetros)
- **`ConsultarCotizacionMoneda(moneda_id)`**: devuelve cotización y fecha de la moneda indicada como parámetro
- **`ConsultarPuntosVenta()`**: permite consultar los puntos de venta habilitados para CAE en este WS, devuelve una lista (array de strings) con los datos con numero_punto_venta, bloqueado, fecha_baja
  
### Atributos

- **`Token`**: es el código de autorización generado por la AFIP (WSAA)
- **`Sign`**: es la firma de autorización generado por la AFIP (WSAA)
- **`Cuit`**: es el número de CUIT del emisor de facturas, formato string sin guiones.
- **`AppServerStatus`**, **`DbServerStatus`**, **`AuthServerStatus`**: estados de los servidores de AFIP (string “OK” en caso de estar funcionales)
- **`XmlRequest`**, **`XmlResponse`**: requerimiento y respuesta XML (para depuración)
- **`InstallDir`** *** Nuevo! *** : directorio de instalación (ej. `C:\Archivos de Programa\WSAA`)
- **`Excepcion`**, **`Traceback`** *** Nuevo! *** : mensaje de error y traza de rastreo (para depuración) 
- **`Respuesta`**,  **`Obs`**, **`Reproceso`**: valores complementarios que retornan los métodos
- **`CAE`**, Vencimiento: CAE y Fecha de vencimiento autorización
- **`Version`**: versión de la interfase (ej. “1.11”)
- **`FechaCbte`**: fecha del comprobante (del comprobante recuperado devuelto por !GetCmp)
- **`ImpTotal`**: importes del comprobante 
- **`ErrCode`**: código de error (si corresponde)
- **`ErrMsg`**: mensaje de error (si corresponde)
- **`Errores`**: lista de errores (si corresponde)
- **`Eventos`**: lista de eventos (si corresponde)


## Ejemplo Pseudocodigo

Para rutinas completas en VB, VFP, etc. ver [Ejemplos](wiki:FacturaElectronicaComprobantesTurismo#Ejemplos)

Código de ejmplo en Python:

```
#!python

tipo_cbte = 195
punto_vta = 4000
cbte_nro = wsct.ConsultarUltimoComprobanteAutorizado(tipo_cbte, punto_vta)
fecha = datetime.datetime.now().strftime("%Y-%m-%d")
concepto = 3
tipo_doc = 80; nro_doc = "30000000007"
nro_cbte = long(cbte_nro) + 1
cbt_desde = cbte_nro; cbt_hasta = cbt_desde
id_impositivo = "Cliente del Exterior"
cod_relacion = 1      # Alojamiento Directo a Turista No Residente
imp_total = "122.00"; imp_tot_conc = "0.00"; imp_neto = "100.00"
imp_trib = "1.00"; imp_op_ex = "0.00"; imp_subtotal = "100.00"
imp_reintegro = -21   # validación AFIP 346
cod_pais = 203
domicilio = "Rua N.76 km 34.5 Alagoas"
fecha_cbte = fecha
moneda_id = 'PES'; moneda_ctz = '1.000'
obs = "Observaciones Comerciales, libre"

wsct.CrearFactura(tipo_doc, nro_doc, tipo_cbte, punto_vta,
                  nro_cbte, imp_total, imp_tot_conc, imp_neto,
                  imp_subtotal, imp_trib, imp_op_ex, imp_reintegro,
                  fecha_cbte, id_impositivo, cod_pais, domicilio,
                  cod_relacion, moneda_id, moneda_ctz, obs)            

tributo_id = 99
desc = 'Impuesto Municipal Matanza'
base_imp = "100.00"
alic = "1.00"
importe = "1.00"
wsct.AgregarTributo(tributo_id, desc, base_imp, alic, importe)

iva_id = 5 # 21%
base_imp = 100
importe = 21
wsct.AgregarIva(iva_id, base_imp, importe)

tipo = 0    # Item General
cod_tur = 1 # Servicio de hotelería - alojamiento sin desayuno
codigo = "T0001"
ds = "Descripcion del producto P0001"
iva_id = 5
imp_iva = 42.00
imp_subtotal = 242.00
wsct.AgregarItem(tipo, cod_tur, codigo, ds, 
             iva_id, imp_iva, imp_subtotal)

codigo = 68                # tarjeta de credito
tipo_tarjeta = 99          # otra (ver tabla de parametros)
numero_tarjeta = "999999"
swift_code = None
tipo_cuenta = None
numero_cuenta = None
ws.AgregarFormaPago(codigo, tipo_tarjeta, numero_tarjeta, 
                    swift_code, tipo_cuenta, numero_cuenta)

print wsct.factura

wsct.AutorizarComprobante()

print "Resultado", wsct.Resultado
print "CAE", wsct.CAE
print "Vencimiento", wsct.Vencimiento
print "Reproceso", wsct.Reproceso
print "Errores", wsct.ErrMsg

```

**Nota:** La metodología es similar al resto de los webservices, y se trato de mantener similitud con el código existente:

- Método WSCT.!CrearFactura es similar a WSFEXv1.!CrearFactura (parámetros similares)
- Método WSCT.!AgregarCmpAsoc es similar a WSFEXv1.!AgregarCmpAsoc
- Método WSCT.!AgregarItem es similar a WSMTX/WSFEXv1.!AgregarItem
- Propiedades similares: WSFEv1.CAE, WSFEv1.Resultado, etc.

## Herramienta por archivos de intercambio SIAP - RECE

Para lenguajes donde no es posible utilizar objetos COM, como en algunas versiones de COBOL/Clipper/etc., se desarrolló una herramienta por linea de comando (RECET) para poder utilizar los Web Services de la AFIP, que funciona como un programa independiente, manteniendo las ventajas y características presentadas anteriormente.

Esta herramienta funciona :

- Archivos [TXT](attachment:entrada.txt) de texto plano (formato ancho-fijo similar a COBOL)
- Tablas [DBF](attachment:tablas-dbf-recet.zip) (dBase, Clipper, Harbour, etc.)
- Archivos [JSON](attachment:factura_t.json) de texto plano (PHP, JAVA, !JavaScript, etc.)

### Configuración

Editar el archivo RECE.INI en la carpeta de la intefase (C:\PYAFIPWS):

- CERT: ubicación del archivo certificado (ver WSAA)
- PRIVATEKEY: ubicación del archivo de la clave privada (ver WSAA)
- CUIT: CUIT del emisor
- ENTRADA: ubicación del archivo de texto de entrada (para cada webservice)
- SALIDA: ubicación del archivo de texto de salida (para cada webservice)
- URL: dirección de los servicios web de producción (para cada webservice)

Otras Secciones:

- [DBF]: configura los nombres de archivos con las tablas requeridas
- [PROXY]: configura el servidor intermedio de salida a internet (firewall, antivirus, proxy, etc.), ej:

Para Más información ver [Manual Configuración](wiki:ManualPyAfipWs#Configuración)

Ejemplo:
```
[WSAA]
CERT=C:\SISTEMA\empresa.crt
PRIVATEKEY= C:\SISTEMA\empresa.key
URL=https://wsaa.afip.gov.ar/ws/services/LoginCms

[WSCT]
CUIT=20267565393
ENTRADA=entrada.txt
SALIDA=salida.txt
Reprocesar= S
URL=https://serviciosjava.afip.gob.ar/wsmtxca/services/MTXCAService
```

### Forma de uso

Llamar al ejecutable RECET.EXE  en la carpeta de la intefase (C:\PYAFIPWS)

En caso de ejecución correcta, informara por pantalla los ID y CAE obtenidos y el código de retorno es 0:
```
NRO: 3 Resultado: A CAE: 67253025979341 Obs:  Err:  Reproceso: 
```

El CAE obtenido, fecha de vencimiento y demás valores devueltos por WSCT (resultado, reproceso, motivo de rechazo u observación) son escritos en el archivo de salida, con la misma información de la factura que en el archivo de entrada.

En el caso de error, informa por pantalla el motivo y el código de retorno es distinto de 0:

```
NRO: 1 Resultado: R :  Obs:  Err: 5000: Error interno [E-20170621-15:36:54.386-20267565393-vii] Reproceso: 
```

### Parámetros

RECET.EXE recibe los siguientes argumentos por línea de comando:

- /ayuda: lista los parámetros habilitados 
- /prueba: Teniendo los certificados instalados, se puede realizar una prueba donde la interface generará un archivo de entrada para las tres próximas facturas, obteniendo los últimos números de transacción y comprobante.
- /ult: Solicita Tipo de comprobante y Punto de Venta y devuelve el último numero de comprobante registrado
- /dummy: consulta estado de servidores (deberían ser OK los 3 servidores)
- /ptosventa: devuelve los puntos de venta habilitados para emitir facturas electrónicas
- /debug: modo depuración (detalla y confirma las operaciones)
- /formato: muestra el formato de los archivos de entrada/salida
- /get: recupera datos de un comprobante autorizado previamente (verificación)
- /xml: almacena los requerimientos y respuestas XML (útil para depuración y registro)
- /json: utiliza el formato JSON para el archivo de entrada

Se puede especificar como primer parámetro un nombre de archivo RECE.INI alternativo, para cargar distintas configuraciones, por ej:
```
RECET.EXE rece-empresax.ini ....
```

Si no se especifica accion, por defecto se envía la información del archivo de intercambio para autorizar la emisión de factura electrónica, devuelve el Código de Autorización Electrónico (CAE) y demás datos que responde AFIP.

Para más información ver [Manual](wiki:ManualPyAfipWs#Parámetros)
## Formato archivos de Intercambio

Estructura para archivos de texto (ancho fijo simil COBOL) o tablas DBF (dBase, Clipper, Fox Pro, etc.)
Para muestras ver [Descargas](wiki:FacturaElectronicaComprobantesTurismo#Descargas)

### Encabezado
| **Campo** | **Pos.** | **Long.** | **Tipo** | **Decimales** |  |
|---|---|---|---|---|---|
| tipo_reg | 1 | 1 | Numerico |  |  |
| fecha_cbte | 2 | 10 | Alfanumerico |  |  |
| tipo_cbte | 12 | 3 | Numerico |  |  |
| punto_vta | 15 | 4 | Numerico |  |  |
| cbte_nro | 19 | 8 | Numerico |  |  |
| tipo_doc | 27 | 2 | Numerico |  |  |
| nro_doc | 29 | 11 | Numerico |  |  |
| imp_total | 40 | 15 | Importe | 2 |  |
| imp_tot_conc | 55 | 15 | Importe | 2 |  |
| imp_neto | 70 | 15 | Importe | 2 |  |
| imp_subtotal | 85 | 15 | Importe | 2 |  |
| imp_trib | 100 | 15 | Importe | 2 |  |
| imp_op_ex | 115 | 15 | Importe | 2 |  |
| imp_reintegro | 130 | 15 | Importe | 2 |  |
| moneda_id | 145 | 3 | Alfanumerico |  |  |
| moneda_ctz | 148 | 10 | Importe | 6 |  |
| fecha_venc_pago | 158 | 10 | Alfanumerico |  |  |
| id_impositivo | 168 | 2 | Numerico |  |  |
| cod_relacion | 170 | 2 | Numerico |  |  |
| cod_pais | 172 | 3 | Numerico |  |  |
| domicilio | 175 | 300 | Alfanumerico |  |  |
| cae | 475 | 14 | Alfanumerico |  |  |
| fch_venc_cae | 489 | 10 | Alfanumerico |  |  |
| resultado | 499 | 1 | Alfanumerico |  |  |
| motivos_obs | 500 | 1000 | Alfanumerico |  |  |
| err_code | 1500 | 6 | Alfanumerico |  |  |
| err_msg | 1506 | 1000 | Alfanumerico |  |  |
| reproceso | 2506 | 1 | Alfanumerico |  |  |
| emision_tipo | 2507 | 4 | Alfanumerico |  |  |
| observaciones | 2511 | 1000 | Alfanumerico |  |  |
### Tributo
| **Campo** | **Pos.** | **Long.** | **Tipo** | **Decimales** |  |
|---|---|---|---|---|---|
| tipo_reg | 1 | 1 | Numerico |  |  |
| tributo_id | 2 | 3 | Alfanumerico |  |  |
| desc | 5 | 100 | Alfanumerico |  |  |
| base_imp | 105 | 15 | Importe | 2 |  |
| alic | 120 | 15 | Importe | 2 |  |
| importe | 135 | 15 | Importe | 2 |  |
### Iva
| **Campo** | **Pos.** | **Long.** | **Tipo** | **Decimales** |  |
|---|---|---|---|---|---|
| tipo_reg | 1 | 1 | Numerico |  |  |
| iva_id | 2 | 3 | Alfanumerico |  |  |
| base_imp | 5 | 15 | Importe | 2 |  |
| importe | 20 | 15 | Importe | 2 |  |
### Comprobante Asociado
| **Campo** | **Pos.** | **Long.** | **Tipo** | **Decimales** |  |
|---|---|---|---|---|---|
| tipo_reg | 1 | 1 | Numerico |  |  |
| tipo | 2 | 3 | Numerico |  |  |
| pto_vta | 5 | 4 | Numerico |  |  |
| nro | 9 | 8 | Numerico |  |  |
| cuit | 17 | 11 | Numerico |  |  |
| cuit | 28 | 11 | Numerico |  |  |
### Detalle
| **Campo** | **Pos.** | **Long.** | **Tipo** | **Decimales** |  |
|---|---|---|---|---|---|
| tipo_reg | 1 | 1 | Numerico |  |  |
| tipo | 2 | 3 | Numerico |  |  |
| cod_tur | 5 | 30 | Alfanumerico |  |  |
| codigo | 35 | 30 | Alfanumerico |  |  |
| iva_id | 65 | 3 | Numerico |  |  |
| imp_iva | 68 | 15 | Importe | 2 |  |
| imp_subtotal | 83 | 15 | Importe | 2 |  |
| ds | 98 | 4000 | Alfanumerico |  |  |
### Forma Pago
| **Campo** | **Pos.** | **Long.** | **Tipo** | **Decimales** |  |
|---|---|---|---|---|---|
| tipo_reg | 1 | 1 | Numerico |  |  |
| codigo | 2 | 3 | Numerico |  |  |
| tipo_tarjeta | 5 | 2 | Numerico |  |  |
| numero_tarjeta | 7 | 6 | Numerico |  |  |
| swift_code | 13 | 11 | Numerico |  |  |
| tipo_cuenta | 24 | 2 | Numerico |  |  |
| numero_cuenta | 26 | 20 | Numerico |  |  |

## Cambios respecto a WSFEv1 / WSMTXCA / WSFEXv1

En este nuevo servicio web WSCT, además de los campos requeridos por el WSFE para autorizar una factura (obtener el CAE), se debe informar:

- `codigo_tipo_comprobante`: 195 (Factura T), 196 (N/D T) y 197 (N/C T)
- `numero_punto_venta`: ídem otros webservices
- `numero_comprobante`: ídem otros webservices
- `fecha_emision`: ídem otros webservices
- `codigo_tipo_autorizacion`: indica el tipo del código de autorización, "E": CAE (Código de Autorización Electrónico) o "A": CAEA (Código de Autorización Electrónico Anticipado, no autorizado en esta versión)
- `fecha_vencimiento`: (date)
- `codigo_tipo_documento`: código de documento del receptor del comprobante (ver Tablas de Parámetros)
- `numero_documento`: Número de documento del receptor del comprobante.
- `id_impositivo`: "Cliente del Exterior", Consumidor Final", "IVA Responsable Inscripto" (ver Tablas de Parámetros)
- `codigo_pais`: informar un código de país habilitado (ver Tablas de Parámetros) si el tipo de ducumento es del exterior.
- `codigo_relacion_emisor_receptor`: 
- 1: Alojamiento Directo a Turista No Residente
- 2: Alojamiento a Agencia de Viaje Residente
- 3: Alojamiento a Agencia de Viaje No Residente
- 4: Agencia de Viaje Residente a Agencia de Viaje No Residente
- 5: Agencia de Viaje Residente a Turista No Residente
- 6: Agencia de Viaje Residente a Agencia de Viaje Residente
- `importe_gravado`:
- `importe_no_gravado`:
- `importe_exento`:
- `importe_otros_tributos`:
- `importe_reintegro`:
- `importe_total`:
- `codigo_moneda`: "PES", "DOL", etc. (según tabla de parámetros)
- `cotizacion_moneda`:  tipo de cambio para la factura, 1 si es PES; no podrá ser inferior al 50% ni superior en un 100% del que suministra AFIP como orientativo de acuerdo a la cotización oficial
- `observaciones`: Observaciones comerciales (Importante: NO es necesario completar con espacios, max 2000)
- Detallar cada artículo vendido (ítems)
- `tipo`: entero (ver Tabla de Parámetros)
    - 0: Item general
    - 97: Anticipo
    - 99: Descuento General
- `codigo_turismo`: (ver Tabla de Parámetros)
    - 1: Servicio de hotelería - alojamiento sin desayuno
    - 2: Servicio de hotelería - alojamiento con desayuno
    - 5 - Excedente
- `codigo`: texto (max 50)
- `descripcion`: texto (max 200)
- `codigo_condicion_iva`: Categoría de IVA (según tabla de parámetros)
    - 5: 21%
- `importe_iva`: 
- `importe_item`:
- Tributos: 
- `codigo`
- `descripcion`
- `base_imponible`
- `importe`
- Subtotales de IVAs: 
- `codigo`
- `importe`
- Comprobantes Asociados: tipo de comprobante, punto de venta y número, similar a WSFEX
- `cuit_emisor`
- `codigo_tipo_comprobante`
- `numero_punto_venta`
- `numero_comprobante`

La operatoria es bastante similar al método de autorización del WSFEv1/WSMTXCA/WSFEXv1, teniendo en cuenta esta mayor complejidad por tener que informar el detalle de cada item y otros campos asociados a los servicios turísticos.

**NOTA**: Este webservice no tiene ID secuencial ni reproceso, por lo que el programa debe implementar la consulta de CAE en caso de errores de comunicación.

A su vez, devuelve mensajes de eventos (mantenimiento programado, advertencias, etc.), los que deben ser capturados e informados al usuario.


## Tablas de Parámetros

Wste nuevo servicio funciona con tablas dinámicas de parámetros para los códigos de comprobante, moneda, IVA, tribuots, unidades de medida. Estas tablas pueden sufrir modificaciones realizadas por la AFIP, con altas y bajas lógicas, por lo que tienen una fecha de vigencia (desde, hasta) y se proveen métodos para consultarlas por el mismo servicio web.

Por el momento el webservice no está disponible, por lo que se muestran valores tentativos.
### Tipos de Comprobante
| 195 | Factura T |
|---|---|
| 196 | Nota de Débito T |
| 197 | Nota de Crédito T |
### Tipos de Documento
| 80 | CUIT |
|---|---|
| 86 | CUIL |
| 87 | CDI |
| 89 | LE |
| 90 | LC |
| 91 | CI Extranjera |
| 92 | en trámite |
| 93 | Acta Nacimiento |
| 95 | CI Bs. As. RNP |
| 96 | DNI |
| 94 | Pasaporte |
| 0 | CI Policía Federal |
| 1 | CI Buenos Aires |
| 2 | CI Catamarca |
| 3 | CI Córdoba |
| 4 | CI Corrientes |
| 5 | CI Entre Ríos |
| 6 | CI Jujuy |
| 7 | CI Mendoza |
| 8 | CI La Rioja |
| 10 | CI San Juan |
| 11 | CI San Luis |
| 9 | CI Salta |
| 12 | CI Santa Fe |
| 13 | CI Santiago del Estero |
| 14 | CI Tucumán |
| 16 | CI Chaco |
| 17 | CI Chubut |
| 18 | CI Formosa |
| 19 | CI Misiones |
| 20 | CI Neuquén |
| 21 | CI La Pampa |
| 22 | CI Río Negro |
| 23 | CI Santa Cruz |
| 24 | CI Tierra del Fuego |
| 99 | Doc. (Otro) |
### Alicuotas de IVA
| 5 | 21% |
|---|---|
### Condiciones de IVA
| 1 | No gravado |
|---|---|
| 2 | Exento |
| 3 | 0% |
| 4 | 10.5% |
| 5 | 21% |
| 6 | 27% |

### Código Relación Receptor Emisor

| 1 | Alojamiento Directo a Turista No Residente |
|---|---|
| 2 | Alojamiento a Agencia de Viaje Residente |
| 3 | Alojamiento a Agencia de Viaje No Residente |
| 4 | Agencia de Viaje Residente a Agencia de Viaje No Residente |
| 5 | Agencia de Viaje Residente a Turista No Residente |
| 6 | Agencia de Viaje Residente a Agencia de Viaje Residente |

### Tipo de Item

| 0 | Item general |
|---|---|
| 97 | Anticipo |
| 99 | Descuento General |

### Código de Item de Turismo

| 1 | Servicio de hotelerída - alojamiento sin desayuno |
|---|---|
| 2 | Servicio de hotelerída - alojamiento con desayuno |
| 5 | Excedente |

### Formas Pago

| 68 | Tarjeta de Crédito |
|---|---|
| 69 | Tarjeta de Débito |
| 9 | Transferencia Bancaria |

### Tipos de Tarjeta

Tarjeta de Crédito (68):

| 1 | American Express |
|---|---|
| 2 | Visa |
| 3 | Mastercard |
| 4 | Credencial |
| 5 | Carta Franca |
| 6 | Cabal |
| 7 | Diners |
| 8 | Tarjeta Shopping |
| 9 | Tarjeta Naranja |
| 99 | Otra |

Tarjeta de Débito (69):

| 1 | Maestro |
|---|---|
| 2 | Visa Electrón |
| 3 | Cabal 24 hs |
| 99 | Otra |
### Tipos de Cuenta

| 1 | Caja de ahorro |
|---|---|
| 2 | Cuenta corriente |
| 3 | Cuenta única |

### Tipos de Tributo
| 1 | Impuestos Nacionales |
|---|---|
| 2 | Impuestos Provinciales |
| 3 | Impuestos Municipales |
| 4 | Impuestos Internos |
| 99 | Otros |

### Tipos de Datos Adicionales

De corresponder se detallan los datos adicionales no soportados por la estructura original del servicio:

| 0 | NO HABILITADO - RESERVADO PARA USO FUTURO |
|---|---|

### Monedas
| PES | Pesos Argentinos |
|---|---|
| DOL | Dólar Estadounidense |
| 007 | Florines Holandeses |
| 010 | Pesos Mejicanos |
| 011 | Pesos Uruguayos |
| 014 | Coronas Danesas |
| 015 | Coronas Noruegas |
| 016 | Coronas Suecas |
| 018 | Dólar Canadiense |
| 019 | Yens |
| 021 | Libra Esterlina |
| 023 | Bolívar Venezolano |
| 024 | Corona Checa |
| 025 | Dinar Yugoslavo |
| 026 | Dólar Australiano |
| 027 | Dracma Griego |
| 028 | Florín (Antillas Holandesas) |
| 029 | Güaraní |
| 031 | Peso Boliviano |
| 032 | Peso Colombiano |
| 033 | Peso Chileno |
| 034 | Rand Sudafricano |
| 036 | Sucre Ecuatoriano |
| 051 | Dólar de Hong Kong |
| 052 | Dólar de Singapur |
| 053 | Dólar de Jamaica |
| 054 | Dólar de Taiwan |
| 055 | Quetzal Guatemalteco |
| 056 | Forint (Hungría) |
| 057 | Baht (Tailandia) |
| 059 | Dinar Kuwaiti |
| 012 | Real |
| 030 | Shekel (Israel) |
| 035 | Nuevo Sol Peruano |
| 060 | Euro |
| 040 | Lei Rumano |
| 042 | Peso Dominicano |
| 043 | Balboas Panameñas |
| 044 | Córdoba Nicaragüense |
| 045 | Dirham Marroquí |
| 063 | Lempira Hondureña |
| 046 | Libra Egipcia |
| 047 | Riyal Saudita |
| 062 | Rupia Hindú |
| 061 | Zloty Polaco |
| 064 | Yuan (Rep. Pop. China) |
| 002 | Dólar Libre EEUU |
| 009 | Franco Suizo |
| 041 | Derechos Especiales de Giro |
| 049 | Gramos de Oro Fino |

### Código de País

Ver campo `cod_pais`, *Errores 307: El código de pais no fue informado o no corresponde a un país valido. Consultar el método consultarPaises* (Validación AFIP)

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
| 162 | SUDAN |
| 163 | SUDAN DEL SUR |
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
| 357 | ESTADO DE PALESTINA |
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
| 671 | ISLAS CAIMAN (TERRITORIO NO AUTONOMO DEL R UNIDO) |
| 997 | RESTO CONTINENTE |
| 998 | INDET.(CONTINENTE) |

### CUITs Paises

Se debe utilizar en campo `nro_doc` *Si es Cliente del Exterior o Consumidor final e informa tipo de documento CUIT debe corresponder a una CUIT de país habilitada.* (*Errores 314: El CUIT país es invalido.* de AFIP)
Ver metodo ConsultarCUITsPaises

| 50000003015 | AFGANISTAN |
|---|---|
| 50000004380 | ALEMANIA, REP. FED. |
| 50000006529 | ANGUILA (Territorio no autónomo del Reino Unido) |
| 50000002256 | ANTIGUA Y BARBUDA (Estado independiente) |
| 50000006596 | ANTILLAS HOLANDESAS (Territorio de Países Bajos) |
| 50000003023 | ARABIA SAUDITA |
| 50000006960 | ARCHIPIELAGO DE SVBALBARD |
| 50000001020 | ARGELIA |
| 50000006022 | ARMENIA |
| 50000006537 | ARUBA (Territorio de Países Bajos) |
| 50000006626 | ASCENCION |
| 50000004992 | AUSTRALIA |
| 50000004054 | AUSTRIA |
| 50000003902 | AZERBAIDZHAN |
| 50000003457 | BANGLADESH |
| 50000002019 | BARBADOS (Estado independiente) |
| 50000004062 | BELGICA |
| 50000002361 | BELICE (Estado independiente) |
| 50000001624 | BENIN |
| 50000006634 | BERMUDAS (Territorio no autónomo del Reino Unido) |
| 50000004399 | BIELORUSIA |
| 50000000040 | BOLIVIA |
| 50000004461 | BOSNIA HERZEGOVINA |
| 50000001039 | BOTSWANA |
| 50000000059 | BRASIL |
| 50000003910 | BRUNEI DARUSSALAM (Estado independiente) |
| 50000004070 | BULGARIA |
| 50000001012 | BURKINA FASO |
| 50000001047 | BURUNDI |
| 50000002825 | BUTAN |
| 50000003066 | CAMBOYA (EX KAMPUCHEA) |
| 50000001055 | CAMERUN |
| 50000006642 | CAMPIONE D@ITALIA |
| 50000002043 | CANADA |
| 50000001071 | CENTRO AFRICANO, REP. |
| 50000001535 | CHAD |
| 50000006057 | CHECA, REPUBLICA |
| 50000000032 | CHILE |
| 50000003104 | CHINA REP.POPULAR |
| 50000002051 | COLOMBIA |
| 50000006650 | COLONIA DE GIBRALTAR |
| 50000001896 | COMORAS |
| 50000002906 | COMUNIDAD DE LAS BAHAMAS (Estado independiente) |
| 50000001527 | CONGO REP.POPULAR |
| 50000003082 | COREA DEMOCRATICA |
| 50000003090 | COREA REPUBLICANA |
| 50000001101 | COSTA DE MARFIL |
| 50000001586 | COSTA RICA |
| 50000006030 | CROACIA |
| 50000002396 | CUBA |
| 50000004097 | DINAMARCA |
| 50000002094 | DOMINICANA, REPUBLICA |
| 50000002426 | ECUADOR |
| 50000001136 | EGIPTO |
| 50000002337 | EL COMMONWEALTH DE DOMINICA (Estado Asociado) |
| 50000002116 | EL SALVADOR |
| 50000003317 | EMIRATOS ARABES UNIDOS (Estado independiente) |
| 50000001853 | ERITREA |
| 50000006065 | ESLOVACA, REPUBLICA |
| 50000004496 | ESLOVENIA |
| 50000004100 | ESPAÑA |
| 50000002882 | ESTADO ASOCIADO DE GRANADA (Estado independiente) |
| 50000003031 | ESTADO DE BAHREIN (Estado independiente) |
| 50000003236 | ESTADO DE KUWAIT (Estado independiente) |
| 50000002981 | ESTADO DE QATAR (Estado independiente) |
| 50000002213 | ESTADO LIBRE ASOCIADO DE PUERTO RICO (Estado asoc. a EEUU) |
| 50000002124 | ESTADOS UNIDOS |
| 50000004402 | ESTONIA |
| 50000001144 | ETIOPIA |
| 50000002892 | FEDERACION DE SAN CRISTOBAL (Islas Saint Kitts and Nevis) |
| 50000005123 | FIJI, ISLAS |
| 50000003120 | FILIPINAS |
| 50000004119 | FINLANDIA |
| 50000004127 | FRANCIA |
| 50000001152 | GABON |
| 50000001160 | GAMBIA |
| 50000003147 | GAZA |
| 50000003880 | GEORGIA |
| 50000001179 | GHANA |
| 50000004194 | GRAN DUCADO DE LUXEMBURGO |
| 50000004135 | GRECIA |
| 50000006669 | GROENLANDIA |
| 50000006677 | GUAM (Territorio no autónomo de los EEUU) |
| 50000002132 | GUATEMALA |
| 50000001187 | GUINEA |
| 50000001845 | GUINEA BISSAU |
| 50000001195 | GUINEA ECUATORIAL |
| 50000002159 | HAITI |
| 50000002167 | HONDURAS |
| 50000006685 | HONK KONG (Territorio de China) |
| 50000004143 | HUNGRIA |
| 50000001985 | INDETERMINADO (AFRICA) |
| 50000002922 | INDETERMINADO (AMERICA) |
| 50000003961 | INDETERMINADO (ASIA) |
| 50000004984 | INDETERMINADO (EUROPA) |
| 50000005980 | INDETERMINADO (OCEANIA) |
| 50000003155 | INDIA |
| 50000003163 | INDONESIA |
| 50000003171 | IRAK |
| 50000002930 | IRAN |
| 50000004151 | IRLANDA (EIRE) |
| 50000006723 | ISLA CHRISTMAS |
| 50000006731 | ISLA DE COCOS O KEELING |
| 50000006766 | ISLA DE MAN (Territorio del Reino Unido) |
| 50000006774 | ISLA DE NORFOLK |
| 50000006804 | ISLA DE SAN PEDRO Y MIGUELON |
| 50000006812 | ISLA QESHM |
| 50000003813 | ISLANDIA |
| 50000006693 | ISLAS AZORES |
| 50000006715 | ISLAS CAIMAN (Territorio no autónomo del Reino Unido) |
| 50000006545 | ISLAS DE COOK (Territorio autónomo asociado a Nueva Zelanda) |
| 50000006707 | ISLAS DEL CANAL:Guernesey,Jersey,Alderney,G.Stark,L.Sark,etc |
| 50000005212 | ISLAS MARIANAS |
| 50000006790 | ISLAS PACIFICO |
| 50000005182 | ISLAS SALOMON |
| 50000006782 | ISLAS TURKAS Y CAICOS (Territorio no autónomo del R. Unido) |
| 50000006820 | ISLAS VIRGENES BRITANICAS(Territorio no autónomo de R.UNIDO) |
| 50000006839 | ISLAS VIRGENES DE ESTADOS UNIDOS DE AMERICA |
| 50000002876 | ISRAEL |
| 50000003546 | ITALIA |
| 50000002175 | JAMAICA |
| 50000003201 | JAPON |
| 50000003929 | KAZAJSTAN |
| 50000001209 | KENIA |
| 50000003937 | KIRGUISTAN |
| 50000005166 | KIRIBATI |
| 50000006847 | LABUAN |
| 50000003244 | LAOS |
| 50000001217 | LESOTHO |
| 50000004410 | LETONIA |
| 50000003252 | LIBANO |
| 50000001233 | LIBIA |
| 50000004429 | LITUANIA |
| 50000003449 | MACAO |
| 50000004909 | MACEDONIA |
| 50000001241 | MADAGASCAR |
| 50000006855 | MADEIRA (Territorio de Portugal) |
| 50000003260 | MALASIA |
| 50000001543 | MALAWI |
| 50000001632 | MALI |
| 50000001276 | MARRUECOS |
| 50000001292 | MAURITANIA |
| 50000002183 | MEXICO |
| 50000005905 | MICRONESIA ESTADOS FED. |
| 50000004437 | MOLDOVA |
| 50000003295 | MONGOLIA |
| 50000006863 | MONTSERRAT (Territorio no autónomo del Reino Unido) |
| 50000001519 | MOZAMBIQUE |
| 50000002841 | MYANMAR (EX BIRMANIA) |
| 50000001837 | NAMIBIA |
| 50000003309 | NEPAL |
| 50000002191 | NICARAGUA |
| 50000001306 | NIGER |
| 50000001314 | NIGERIA |
| 50000006871 | NIUE |
| 50000004224 | NORUEGA |
| 50000005042 | NUEVA ZELANDA |
| 50000004232 | PAISES BAJOS |
| 50000003325 | PAKISTAN |
| 50000005913 | PALAU |
| 50000005131 | PAPUA, ISLAS |
| 50000009986 | PARA PERSONAS FISICAS DE INDETERMINADO (CONTINENTE) |
| 50000009994 | PARA PERSONAS FISICAS DE OTROS PAISES |
| 50000000024 | PARAGUAY |
| 50000006553 | PATAU |
| 50000002221 | PERU |
| 50000006901 | PITCAIRN |
| 50000006561 | POLINESIA FRANCESA (Territorio de Ultramar de Francia) |
| 50000004240 | POLONIA |
| 50000004259 | PORTUGAL |
| 50000005077 | POS.AUSTRALIANA (OCEANIA) |
| 50000001454 | POS.BRITANICA (AFRICA) |
| 50000002272 | POS.BRITANICA (AMERICA) |
| 50000004917 | POS.BRITANICA (EUROPA) |
| 50000003414 | POS.BRITANICA (HONG KONG) |
| 50000005085 | POS.BRITANICA (OCEANIA) |
| 50000002280 | POS.DANESA (AMERICA) |
| 50000002310 | POS.E.E.U.U. (AMERICA) |
| 50000005115 | POS.E.E.U.U. (OCEANIA) |
| 50000001462 | POS.ESPAÑOLA (AFRICA) |
| 50000001470 | POS.FRANCESA (AFRICA) |
| 50000002299 | POS.FRANCESA (AMERICA) |
| 50000005093 | POS.FRANCESA (OCEANIA) |
| 50000003422 | POS.JAPONESA (ASIA) |
| 50000005107 | POS.NEOCELANDESA (OCEANIA) |
| 50000002302 | POS.PAISES BAJOS (AMERICA) |
| 50000001489 | POS.PORTUGUESA (AFRICA) |
| 50000004186 | PRINCIPADO DE LIECHTENSTEIN (Estado independiente) |
| 50000004216 | PRINCIPADO DE MONACO |
| 50000004046 | PRINCIPADO DEL VALLE DE ANDORRA |
| 50000006936 | REGIMEN APLICABLE A LAS SA FINANCIERAS(ley 11.073 de la ROU) |
| 50000001373 | REINO DE SWAZILANDIA (Estado independiente) |
| 50000005190 | REINO DE TONGA (Estado independiente) |
| 50000003007 | REINO HACHEMITA DE JORDANIA |
| 50000004267 | REINO UNIDO |
| 50000002140 | REPUBLICA COOPERATIVA DE GUYANA (Estado independiente) |
| 50000004011 | REPUBLICA DE ALBANIA |
| 50000001497 | REPUBLICA DE ANGOLA |
| 50000001500 | REPUBLICA DE CABO VERDE (Estado independiente) |
| 50000003112 | REPUBLICA DE CHIPRE (Estado independiente) |
| 50000001861 | REPUBLICA DE DJIBUTI (Estado independiente) |
| 50000005204 | REPUBLICA DE LAS ISLAS MARSHALL (Estado independiente) |
| 50000001225 | REPUBLICA DE LIBERIA (Estado independiente) |
| 50000003279 | REPUBLICA DE MALDIVAS (Estado independiente) |
| 50000004364 | REPUBLICA DE MALTA (Estado independiente) |
| 50000001284 | REPUBLICA DE MAURICIO |
| 50000005034 | REPUBLICA DE NAURU (Estado independiente) |
| 50000002205 | REPUBLICA DE PANAMA (Estado independiente) |
| 50000001810 | REPUBLICA DE SEYCHELLES (Estado independiente) |
| 50000002434 | REPUBLICA DE TRINIDAD Y TOBAGO |
| 50000005050 | REPUBLICA DE VANUATU |
| 50000003392 | REPUBLICA DEL YEMEN |
| 50000003074 | REPUBLICA DEMOCRATICA SOCIALISTA DE SRI LANKA |
| 50000001411 | REPUBLICA TUNECINA |
| 50000001330 | RUANDA |
| 50000004275 | RUMANIA |
| 50000006014 | RUSA, FEDERACION |
| 50000006952 | SAMOA AMERICANA (Territorio no autónomo de los EEUU) |
| 50000005069 | SAMOA OCCIDENTAL |
| 50000002353 | SAN VICENTE Y LAS GRANADINAS (Estado independiente) |
| 50000006944 | SANTA ELENA |
| 50000002345 | SANTA LUCIA |
| 50000004313 | SANTA SEDE (VATICANO) |
| 50000001829 | SANTO TOME Y PRINCIPE |
| 50000001349 | SENEGAL |
| 50000004283 | SERENISIMA REPUBLICA DE SAN MARINO (Estado independiente) |
| 50000001357 | SIERRA LEONA |
| 50000003333 | SINGAPUR |
| 50000003341 | SIRIA |
| 50000001365 | SOMALIA |
| 50000001713 | SUDAFRICA, REP. DE |
| 50000001381 | SUDAN |
| 50000004291 | SUECIA |
| 50000004305 | SUIZA |
| 50000003287 | SULTANATO DE OMAN |
| 50000002329 | SURINAME |
| 50000002914 | TAILANDIA |
| 50000003139 | TAIWAN |
| 50000001551 | TANZANIA |
| 50000003899 | TAYIKISTAN |
| 50000003570 | TERRITORIOS AUTONOMOS PALESTINOS |
| 50000001403 | TOGO |
| 50000006995 | TOKELAU |
| 50000006987 | TRIESTE (Italia) |
| 50000006979 | TRISTAN DA CUNHA |
| 50000003554 | TURKMENISTAN |
| 50000003503 | TURQUIA |
| 50000005174 | TUVALU |
| 50000006049 | UCRANIA |
| 50000001705 | UGANDA |
| 50000000016 | URUGUAY |
| 50000003562 | UZBEKISTAN |
| 50000002264 | VENEZUELA |
| 50000003376 | VIETNAM |
| 50000004321 | YUGOSLAVIA |
| 50000001616 | ZAIRE |
| 50000001446 | ZAMBIA |
| 50000001322 | ZIMBABWE |
| 50000007002 | ZONA LIBRE DE OSTRAVA (ciudad de la antigua Checoeslovaquia) |

## Aclaraciones


Margen de error: 
  Error relativo porcentual deberá ser <= 0.01% o el error absoluto <=0.01
## Novedades

Se recuerda que esta disponible el 
[grupo de noticias](http://www.pyafipws.com.ar) (http://groups.google.com.ar/group/pyafipws) donde
se publicarán futuras novedades sobre PyAfipWS: servicios web de
factura electrónica y sus interfases (se recomienda suscribirse)

## Costos y Condiciones

Ofrecemos soporte técnico comercial (pago), independiente a la AFIP, desarrollos especiales, interfaces web, etc. 
Obtenga mas información enviando un mail a info@pyafipws.com.ar o (011) 4450-0716 / (011) 15-3048-9211 (asesoramiento sin cargo)

A su vez, se liberará el código fuente bajo licencia GPLv3 (software libre), al igual que se hizo con el restos de los servicios web. Para más detalles ver página FacturaElectronica.

La información de esta página es proporcionada a titulo informativo.

2017 © MarianoReingart
