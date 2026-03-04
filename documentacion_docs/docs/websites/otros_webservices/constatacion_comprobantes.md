# Constatación de Comprobantes emitidos (CAI, CAE, CAEA) por Web Service AFIP

Interfaz para los Servicios Web para verificar en forma dinámica si los comprobantes recibidos se encuentran autorizados por la AFIP.
[Ley de Procedimiento Tributario N°11683](http://infoleg.mecon.gov.ar/infolegInternet/anexos/15000-19999/18771/texact.htm) (Artículo 33) modificado por [Ley N° 25795](http://infoleg.mecon.gov.ar/scripts1/busquedas/cnsnorma.asp?tipo=Ley&nro=25795) y reglamentado por [Decreto 477/2007](http://biblioteca.afip.gob.ar/dcp/DEC_C_000477_2007_05_02) 


## Descripción General

Este servicio permite verificar la validez en los comprobantes respaldatorios de las operaciones, tanto con Código de Autorización de Impresión (CAI), el Código de Autorización Electrónico, y CAE Anticipado "CAEA". La modalidad CAE y CAEA es soportada por dos webservices:

- [WSFEv1](../factura_electronica/wsfev1.md)(Web Service de Factura Electrónica Versión 1) correspondiente a la  RG 2485 y modificatorias
- [WSMTXCA](../factura_electronica/wsmtxca.md) (Web Service de Factura Electrónica con detalle) correspondiente a la  RG 2904 

Actualmente los comprobantes se pueden validar también por el servicio interactivo de AFIP:

- http://www.afip.gob.ar/genericos/imprentas/facturas.asp Constatación de comprobantes emitidos (C.A.I.) 
- http://www.afip.gob.ar/genericos/consultaCAE/ Constatación de comprobantes electrónicos emitidos (C.A.E.)
- http://www.afip.gob.ar/genericos/consultaCAEA/ Constatación de comprobantes electrónicos emitidos (C.A.E.A.) 

Este webservice permite la automatización de dichas consultas sin la necesidad de intervención del usuario. Publicación: Septiembre de 2013 [Documentación Oficial](http://www.afip.gob.ar/ws/WSCDCV1/ManualDelDesarrolladorWSCDCV1.pdf)

Se encuentran obligados a constatar la debida autorización de las facturas o documentos equivalentes -de conformidad con lo dispuesto por el artículo agregado a continuación del Artículo 33 de la [Ley Nº 11.683](http://infoleg.mecon.gov.ar/infolegInternet/anexos/15000-19999/18771/texact.htm), texto ordenado en 1998 y sus modificaciones- los sujetos que, por poseer montos de compras significativos, montos de ventas relevantes y/o desarrollen actividades de riesgo y/o de relevante interés fiscal (según [Decreto 477/2007](http://biblioteca.afip.gob.ar/dcp/DEC_C_000477_2007_05_02)):

 1. Exportadores y sujetos que realicen actividades asimilables a la exportación, con carácter de habitualistas.
 2. Contribuyentes que actúen como agentes de retención del Impuesto al Valor Agregado.
 3. Contribuyentes que reciban comprobantes electrónicos.
 4. El ESTADO NACIONAL y sus dependencias y/u organismos dependientes, centralizados, descentralizados o autárquicos.
## Descargas e Instalación

Ver archivos y últimas actualizaciones para descargas en [GitHub](https://github.com/reingart/pyafipws/releases) (actualizado) y [GoogleCode](http://code.google.com/p/pyafipws/downloads/list) (histórico):

- Instalador: [https://www.sistemasagiles.com.ar/soft/pyafipws/PyAfipWs-2.7.1994-32bit+wsaa_2.11c+wscdc_1.02e-homo.exe]
- Ejemplos de código (última versión de desarrollo):
- Visual Basic 5/6: [wscdc.bas](https://github.com/reingart/pyafipws/blob/master/ejemplos/wscdc/wscdc.bas)
- Visual Fox Pro 5: [wscdc.prg](https://github.com/reingart/pyafipws/blob/master/ejemplos/wscdc/wscdc.prg)
- Visual Basic .NET: [wscdc.vb](https://github.com/reingart/pyafipws/blob/master/ejemplos/wscdc/wscdc.vb)
- Muestra de archivo de intercambio:
- [salida_wscdc.txt](attachment:salida_wscdc.txt) texto plano, universal (con campos de ancho fijo, simil COBOL)  
- [Manual de Uso](../documentacion_herramientas/manualpyafipws.md): Documentación General ([PDF](http://www.sistemasagiles.com.ar/trac/wiki/ManualPyAfipWs?format=pdf)) y [Manual del Desarrollador WSCDCv1 (AFIP)](http://www.afip.gob.ar/ws/WSCDCV1/ManualDelDesarrolladorWSCDCV1.pdf)
- Código Fuente (Python): ver [wscdc.py](https://code.google.com/p/pyafipws/source/browse/wscdc.py) y [unit test](https://code.google.com/p/pyafipws/source/browse/tests/wscdc.py)

## Métodos

Métodos principales:

- **`ConstatarComprobante(cbte_modo, cuit_emisor, pto_vta, cbte_tipo,cbte_nro, cbte_fch, imp_total, cod_autorizacion, doc_tipo_receptor, doc_nro_receptor)`**: Constatación de Comprobantes. Recibe los datos del comprobante a verificar (todos obligatorios excepto los datos del receptor). Devuelve verdadero en caso de ejecución satisfactoria, falso en caso de error. Establece `Resultado`, `Obs` y demás atributos. Ver [Ejemplos](http://www.sistemasagiles.com.ar/trac/wiki/ConstatacionComprobantes#Ejemplos).

Métodos secundarios:

- **`Conectar(cache=None, url="", proxy="")`**: en homologación no hace falta pasarle ningùn paràmetro. En producciòn, el segudo parametro es la WSDL.
- **`Dummy()`**: devuelve estado de servidores. Devuelve verdadero en caso de ejecución satisfactoria, falso en caso de error. Establece `AppServerStatus`, `DbServerStatus` y `AuthServerStatus` 

Métodos auxiliares:

- **`ConsultarModalidadComprobantes(sep="|")`**: Recuperador de modalidades de autorización de comprobantes (`"CAI"`, `"CAE"`, `"CAEA"`)
- **`ConsultarTipoComprobantes(sep="|")`**: Recuperador de valores referenciales de códigos de Tipos de comprobante
- **`ConsultarTipoDocumentos(sep="|")`**: Recuperador de valores referenciales de códigos de Tipos de Documentos
- **`ConsultarTipoOpcionales(sep="|")`**: Recuperador de valores referenciales de códigos de Tipos de datos Opcionales

## Atributos

Propiedades principales retornadas por el WSCDC:

- **`Resultado`**: `"A"`: Aprobado, `"O"`: Observado, `"R"`: Rechazado
- **`FechaCbte`**: fecha del comprobante
- **`PuntoVenta`**: punto de venta del comprobante
- **`CbteNro`**: fecha del comprobante
- **`DocTipo`**: tipo de documento del receptor
- **`DocNro`**: número de documento del receptor
- **`ImpTotal`**: importe del comprobante
- **`EmisionTipo`**: modo de comprobante (CAE, CAEA, CAI)
- **`CAI`**, **`CAE`**, **`CAEA`**: código de autorización

Propiedades con validaciones devueltas por el WSCDC:

- **`Obs`** (**`Observaciones`**): mensajes advertencia de AFIP
- **`ErrMsg`**, **`ErrCode`** (**`Errores`**): mensajes de error de AFIP

Propiedades secundarias del WSCDC:

- **`Token`**: es el código de autorización generado por la AFIP (WSAA)
- **`Sign`**: es la firma de autorización generado por la AFIP (WSAA)
- **`Cuit`**: es el número de CUIT del emisor de facturas, formato string sin guiones.
- **`AppServerStatus`**, **`DbServerStatus`**, **`AuthServerStatus`**: estados de los servidores de AFIP (string “OK” en caso de estar funcionales)
- **`XmlRequest`**, **`XmlResponse`**: requerimiento y respuesta XML (para depuración)
- **`InstallDir`** *** Nuevo! ***: directorio de instalación (ej. `C:\Archivos de Programa\WSCDC`)
- **`Excepcion`**, **`Traceback`** *** Nuevo! ***: mensaje de error y traza de rastreo (para depuración) 
- **`LanzarExcepciones`** *** Nuevo! *** : establece si se deben emitir errores al lenguaje de programación (habilitado por defecto), o serán controlados por el programa (revisando el atributo Excepcion luego de cada método)

## Ejemplos

Pseudocódigo en Python para Constatación de un comprobante (Factura A con CAEA):

```
#!python
 
cbte_modo = "CAE"                    # modalidad de emision: CAI, CAE, CAEA
cuit_emisor = "20267565393"          # proveedor
pto_vta = 4002                       # punto de venta habilitado en AFIP
cbte_tipo = 1                        # 1: factura A (ver tabla de parametros)
cbte_nro = 109                       # numero de factura
cbte_fch = "20131227"                # fecha en formato aaaammdd
imp_total = "121.0"                  # importe total
cod_autorizacion = "63523178385550"  # numero de CAI, CAE o CAEA
doc_tipo_receptor = 80               # CUIT (obligatorio Facturas A o M)
doc_nro_receptor = "30628789661"     # numero de CUIT del cliente

ok = wscdc.ConstatarComprobante(cbte_modo, cuit_emisor, pto_vta, cbte_tipo, 
                                cbte_nro, cbte_fch, imp_total, cod_autorizacion, 
                                doc_tipo_receptor, doc_nro_receptor)

print "Resultado:", wscdc.Resultado
print "Mensaje de Error:", wscdc.ErrMsg
print "Observaciones:", wscdc.Obs    
```

En caso de que el comprobante esté correctamente autorizado por AFIP, Resultado será "A" (Aprobado), de lo contrario será "R" (Rechazado)

Observaciones más frecuentes:

- 100: El N° de CAI/CAE/CAEA consultado no existe en las bases del organismo.
- 101: Se podran constatar comprobantes con fecha de emision del 01/01/2013 en adelante.
- 113: Para Comprobantes tipo A o tipo M, el documento del receptor debe ser CUIT.
- 114: Para comprobantes tipo A o tipo M el documento del Receptor es obligatorio informarlo..

En caso de que ok no sea verdadero, revisar wscdc.!ErrMsg y wscdc.Excepciones ya que posiblemente hay un problema interno.

Ver fragmentos de código para Visual Basic, Visual Fox Pro y VB.Net en [Descargas e Instalacion](http://www.sistemasagiles.com.ar/trac/wiki/ConstatacionComprobantes#DescargaseInstalación)
## Linea de comandos

WSCDC puede también utilizarse por línea de comando (tanto para Windows como para GNU/Linux) y recibe los siguientes argumentos:

- `--constatar`: realiza la constatación de un comprobante, recibe los mismos argumentos que el método `ConstatarComprobante`
- `--prueba`: utiliza datos de prueba (ver ejemplo)
- `--dummy`: comprueba la infraestructura de AFIP
- `--params`: obtiene y muestra las tablas de parámetro de AFIP
 
Ejemplo para constatar un comprobante (sintaxis para windows):
```
C:\PYAFIPWS> WSCDC_CLI.EXE --constatar CAE 20267565393 5 1 171 20131206 2268.75  63493611413705 80 30606174159
Resultado: R
Mensaje de Error: 
Observaciones: 112: El tipo y número de documento del receptor no se corresponde con los informados para el comprobante consultado o no es válida y no se encontraba activa al momento de emisión de comprobante.
```

Ejemplo para verificar el estado de los servidores (sintaxis para linux):
```
reingart@s5ultra:~/pyafipws$ python wscdc.py --dummy
AppServerStatus OK
DbServerStatus OK
AuthServerStatus OK
```

La configuración se encuentra en el archivo `RECE.INI`:
```
[WSAA]
CERT=reingart.crt
PRIVATEKEY=reingart.key
#URL=https://wsaa.afip.gov.ar/ws/services/LoginCms

[WSCDC]
CUIT=20267565393
#URL=https://servicios1.afip.gov.ar/WSCDC/service.asmx?WSDL
```

### Formato de Intercambio

#### Encabezado

| **Campo** | **Posición** | **Longitud** | **Tipo** | **Descripción** |
| --------- | --------- | --------- | --------- | --------- |
| tipo_reg | 1 | 1 | Alfanumerico | 0: encabezado |
| cbte_modo | 2 | 4 | Alfanumerico | Modalidad de autorización (CAI, CAE, CAEA) |
| cuit_emisor | 6 | 11 | Alfanumerico | CUIT del emisor del comprobante |
| pto_vta | 17 | 4 | Numerico | Punto de Venta del comprobante |
| cbte_tipo | 21 | 3 | Numerico | Tipo de comprobante |
| cbte_nro | 24 | 8 | Numerico | Número de comprobante |
| cbte_fch | 32 | 8 | Alfanumerico | Fecha en formato AAAAMMDD |
| imp_total | 40 | 15 | Importe | Importe total Double (13 + 2) |
| cod_autorizacion | 55 | 14 | Alfanumerico | Número de CAI, CAE, CAEA |
| doc_tipo_receptor | 69 | 2 | Alfanumerico | Tipo de documento del receptor |
| doc_nro_receptor | 71 | 20 | Alfanumerico | N° de documento del receptor |
| resultado | 91 | 1 | Alfanumerico | Resultado (A: Aprobado, O: Observado, R: rechazado) |
| fch_proceso | 92 | 14 | Alfanumerico | Fecha y hora de procesamiento |

#### Observacion

| **Campo** | **Posición** | **Longitud** | **Tipo** | **Descripción** |
| --------- | --------- | --------- | --------- | --------- |
| tipo_reg | 1 | 1 | Alfanumerico | O: observaciones devueltas por AFIP |
| code | 2 | 5 | Numerico | Código de Observación / Error / Evento |
| msg | 7 | 255 | Alfanumerico | Mensaje |

#### Evento

| **Campo** | **Posición** | **Longitud** | **Tipo** | **Descripción** |
| --------- | --------- | --------- | --------- | --------- |
| tipo_reg | 1 | 1 | Alfanumerico | O: observaciones devueltas por AFIP |
| code | 2 | 5 | Numerico | Código de Observación / Error / Evento |
| msg | 7 | 255 | Alfanumerico | Mensaje |

#### Error

| **Campo** | **Posición** | **Longitud** | **Tipo** | **Descripción** |
| --------- | --------- | --------- | --------- | --------- |
| tipo_reg | 1 | 1 | Alfanumerico | O: observaciones devueltas por AFIP |
| code | 2 | 5 | Numerico | Código de Observación / Error / Evento |
| msg | 7 | 255 | Alfanumerico | Mensaje |

## Tablas de Parámetros

### Modalidad Comprobantes

| CAE | Comprobantes - CAE |
|---|---|
| CAEA | Comprobantes - CAEA |
| CAI | Comprobantes - CAI |

### Tipo Comprobantes

| 1 | Facturas A |
|---|---|
| 2 | Notas de Debito A |
| 3 | Notas de Credito A |
| 4 | Recibos A |
| 5 | Notas de Venta al contado A |
| 6 | Facturas B |
| 7 | Notas de Debito B |
| 8 | Notas de Credito B |
| 9 | Recibos B |
| 10 | Notas de Venta al contado B |
| 11 | FACTURAS C |
| 12 | NOTAS DE DEBITO C |
| 13 | NOTAS DE CREDITO C |
| 15 | RECIBOS C |
| 19 | Facturas de Exportacion |
| 20 | N. Deb. p/operac. con el exterior |
| 21 | N. Cre. p/operac. con el exterior |
| 22 | Fac. Perm. Export. Simp. - Dto.855/97 |
| 30 | Cbtes. compra de bienes usados |
| 31 | Mandato/Consignación |
| 32 | COMPROBANTES DE COMPRA DE MATERIALES A RECICLAR PROVENIENTES |
| 34 | Cbtes. A del Anexo I, Apartado A,inc.f),R.G.Nro. 1415 |
| 35 | Cbtes. B del Anexo I,Apartado A,inc. f),R.G. Nro. 1415 |
| 37 | N. Deb/doc. equiv. que cumplan con R.G.Nro. 1415 |
| 38 | N. Cred/doc. equiv. que cumplan con R.G.Nro. 1415 |
| 39 | Otros comprobantes A que cumplan con R.G.Nro. 1415 |
| 40 | Otros comprobantes B que cumplan con R.G.Nro. 1415 |
| 41 | OTROS COMPROBANTES C QUE CUMPLAN CON LA R.G. N° 1415 |
| 51 | Facturas M |
| 52 | Notas de Debito M |
| 53 | Notas de credito M |
| 54 | Recibo M |
| 55 | Notas de Venta al contado M |
| 56 | Comprobantes M del anexo I, Apartado A,inc. f)R.G.Nro.1415 |
| 57 | Otros Comprobantes M que cumplan con la R.G. Nro. 1415 |
| 58 | Cuenta de Venta y Liquido producto M |
| 59 | Liquidacion M |
| 60 | Cta de Vta y Liquido prod. A |
| 61 | Cta de Vta y Liquido prod. B |
| 63 | Liquidacion A |
| 64 | Liquidacion B |
| 70 | Recibo de Factura de Credito R |
| 91 | Remito R |
| 49 | Comprobante de Compra de Bienes Usados |

### Tipo Documentos

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
| 00 | CI Policía Federal |
| 01 | CI Buenos Aires |
| 02 | CI Catamarca |
| 03 | CI Córdoba |
| 04 | CI Corrientes |
| 05 | CI Entre Ríos |
| 06 | CI Jujuy |
| 07 | CI Mendoza |
| 08 | CI La Rioja |
| 09 | CI Salta |
| 10 | CI San Juan |
| 11 | CI San Luis |
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

### Tipo Opcionales

En homologación, actualmente AFIP devuelve: 
```
Mensaje de Error: 503: Sin Resultados: - Metodo OpcionalesTipoConsultar
```
## Novedades

Se recuerda que esta disponible el 
[grupo de usuarios y desarrolladores](http://groups.google.com.ar/group/pyafipws) donde
se publicarán futuras novedades sobre PyAfipWS: servicios web de
factura electrónica y sus interfases (se recomienda suscribirse)

También esta disponible el sitio http://www.pyafipws.com.ar con noticias, anuncios e información técnica general

## Costos y Condiciones

Ofrecemos soporte técnico comercial (pago), independiente a la AFIP, desarrollos especiales, interfaces web, etc. 

Debido a la complejidad de este servicio, su fecha de aplicación y las modificaciones que pudieran surgir, los clientes que así lo requieran pueden adquirir horas de soporte técnico adicional.

Ver [Condiciones del Soporte Comercial](../documentacion_herramientas/pyafipws.md#costos-y-condiciones)

Obtenga mas información enviando un mail a info@pyafipws.com.ar o (011) 15-3048-9211 (asesoramiento sin cargo)

A su vez, se liberará el código fuente bajo licencia GPLv3 (software libre), al igual que se hizo con el restos de los servicios web. Para más detalles ver página FacturaElectronica.

La información de esta página es proporcionada a titulo informativo.
