= Codigo de Operacion de Translado - COT ARBA - Remito Electrónico =

[[TracNav(noreorder|FacturaElectronica)]]

Interfaz para Servicio Web Código de Operaciones de Traslado (COT) "Remito Electronico" correspondiente al  articulo 41 del Código Fiscal que establece la obligación de amparar el traslado o transporte de bienes en el territorio de la provincia de Bs. As (T.O. 2011) incorporado por la Ley 13.405, prorrogada al 19/9/2011 según normativas 34/2011 y 45/2011 [ARBA (Rentas Proincia de Buenos Aires")](http://www.arba.gov.ar/Apartados/Agentes/AgenteCot.asp).  [Resolución General 0038/2014 API (Provincia de Santa Fe)](http://www.santafe.gov.ar/index.php/content/view/full/191149/). [Resolución N° 176 / 2017 AGIP (Ciudad Autónoma de Buenos Aires)](http://www.agip.gob.ar/normativa/resoluciones/2017/agip/resolucion-n-176--agip--2017). 

Sujetos obligados a emitir los comprobantes que respaldan el traslado y entrega de bienes según inciso f) artículo 1 e inciso b del artículo 8 de la Resolución General 1415/03 AFIP

Especificaciones y formato actualizado a Agosto 2011 (última actualización de ARBA)


**NOVEDADES ARBA: Nuevo diseño del Remito electrónico ARBA**

```
    A partir del 3 de junio de 2019 entrará en vigencia el nuevo diseño del Remito electrónico ARBA, el mismo implica los siguientes cambios (prorrogado al 05/08/2019):

- Nueva tabla de comprobantes (código de 3 dígitos; ver nueva Tabla)
- Incremento a 5 posiciones del PREFIJO del punto de venta
- Ampliación de Importe a 12 enteros y 2 decimales
- Información de Importe Neto de componente tributario
- Destinatario Consumidor Final e Importe >= $5.000, debés proporcionar los datos de documento / CUIT y Nombre / Razón Social

 A partir de esta versión ARBA incorpora el campo COT por cada Remito validado. 

 Actualización disponible. 
 
  [(Diseño de archivo)](http://www.arba.gov.ar/archivos/Publicaciones/nuevodiseniodearchivotxt.pdf)
```
**IMPORTANTE: ARBA ANUNCIÓ UNA PRORROGA HASTA EL 5 de AGOSTO de 2019**


## Índice
[[Image(htdocs:logo-pyafipws.png, align=right)]]
[[TOC(noheading,inline,depth=2)]]

## Descargas

- Instalador: [Instalador 1.03a](https://www.sistemasagiles.com.ar/soft/pyafipws/PyAfipWs-2.7.2433-32bit+cot_1.03a-homo.exe) para evaluación
- Ejemplo: [cot.bas](https://github.com/reingart/pyafipws/blob/master/ejemplos/cot/cot.bas) (Visual Basic), [cot.prg](https://github.com/reingart/pyafipws/blob/master/ejemplos/cot/cot.prg) (Visual Fox Pro) 
- Código Fuente (Python): [cot.py](https://github.com/reingart/pyafipws/blob/master/cot.py)
- Documentación oficial: [ARBA](https://www.arba.gov.ar/archivos/Publicaciones/remitoelectronicoautomaticoinstructivo.pdf) (***Importante:** requiere clave ARBA*)

Se debe tramitar la clave ARBA (CIT) en el sitio de pruebas [http://www1.test.arba.gov.ar](http://www1.test.arba.gov.ar/Registracion/transporteBienes.do) (
[Documentación](http://www.test.arba.gov.ar/Apartados/Agentes/AgenteCot.asp?apartado=IIBB&Lugar=E))
                                                            [http://cot.test.arba.gov.ar/TransporteBienes]
 
Para clave CIT producción: [https://www.arba.gov.ar/GuiaTramites/TramiteSeleccionado.asp?tramite=631&categ=33]


Servicio ARBA para efectuar pruebas: [http://www.arba.gov.ar/Informacion/OtrosContri/TransporteBienesServiciosPruebas.asp]


## URL

- Testing: http://cot.test.arba.gov.ar/TransporteBienes/SeguridadCliente/presentarRemitos.do
- Producción: https://cot.arba.gov.ar/TransporteBienes/SeguridadCliente/presentarRemitos.do (***Importante:** modificado por ARBA*)

## Métodos

- **`Conectar(url=None, proxy="", wrapper="", cacert="", trace=False)`**: los parametros son similares a WSFEv1.Conectar (por el momento solo se usa url y trace para depuración)
- **`PresentarRemito(filename, testing="")`**: envia un remito a ARBA. `filename` es el nombre de archivo, `testing` es el nombre de archivo de una respuesta XML de prueba para simulaciones (opcional). Establece los atributos `CuitEmpresa`, `NumeroComprobante`, `NombreArchivo`, `CodigoIntegridad`, `NumeroUnico`, `Procesado` y `COT` de corresponder según respuesta de ARBA, y `TipoError`, `CodigoError`, `MensajeError`: si hay error general.
- **`LeerValidacionRemito()`**: lee el próximo remito validado, `NumeroUnico` y `Procesado` y los errores de validación  (llamar luego a `LeerErrorValidacion` para recorrerlos). Devuelve verdadero (`True`) si hay remito a analizar o  falso (`False`) si ya se analizaron todos los remitos enviados. No es obligatorio llamar a este método si se envia de a un solo remito por archivo.
- **`LeerErrorValidacion()`**: en el caso de ARBA devolver error de validación, completando `CodigoError` y `MensajeError` por cada uno. Devuelve falso (`False`) en caso de no haber más errores para este remito)
- **`ObtenerTagXml(tag1, tag2, ...)`**: busca en el mensaje xml analizado la etiqueta tag1, luego tag2 y así sucesivamente, devolviendo el contenido (texto) del dato si fue encontrada, o nulo en caso contrario. Ver ejemplo.

**IMPORTANTE**: `PresentarRemito` devuelve verdadero (`True`) si ha podido realizar la operación o falso (`False`) en caso contrario. Se capturan los errores, por lo que se deben revisar los atributos luego de llamar al método.

`LeerValidacionRemito` y `ObtenerTagXml` estan disponibles a partir de la versión 2.0a
## Atributos

- `Usuario` y `Password` son los atributos para autenticación (tramitar en ARBA)
- `Version` e `InstallDir` sirven para depuración de la interfaz.
- `XmlResponse`: respuesta xml enviada por ARBA 
- `Excepcion`, `Traceback`: se completan en caso de error interno no esperado (por ej. falla de comunicación).
- `TipoError`, `CodigoError`, `MensajeError`: si hay error general de ARBA se completan según la documentación
- `CuitEmpresa`, `NumeroComprobante`, `NombreArchivo`, `CodigoIntegridad`: campos completados según la respuesta descripta en la documentación de ARBA
- `COT`, `NumeroUnico` y `Procesado`: completados si hay validacionesRemitos.

**IMPORTANTE**: para el manejo de errores, siemper se debe revisar el atributo `Excepcion`, si este no está en blanco, ha ocurrido un error no esperado y debe analizar el `Traceback` (traza) y volver a intentar. Siempre es útil almacenar los valores de `XmlResponse` como respaldo de la operación y para futura referencia o análisis.
## Línea de Comando

Para sistemas operativos legados (DOS bajo windows) y UNIX/Linux, es posible operar la herramienta de remito electrónico por consola.
Recibe como parámetros el nombre de archivo, usuario y clave. Opcionalmente se puede especificar `--testing` para pruebas (usar xml de muestra como respuesta si no se tiene acceso a homologación) y `--trace` para imprimir por pantalla los datos enviados y recibidos.

Ejemplo de uso:
```
C:\PYAFIPWS>COT.EXE TB_20111111112_000000_20080124_000001.txt usuario clave --testing
Error General:  |  |
Error Validacion:  | 85 | El campo ORIGEN_CUIT es inv??lido o inexistente.
Error Validacion:  | 22 | El campo FECHA_SALIDA_TRANSPORTE es inv??lido o inexistente.
CUIT Empresa: 20111111112
Numero Comprobante: 91248293
Nombre Archivo: TB_20111111112_000000_20080124_000001.txt
Codigo Integridad: 15cdd26deef17cb36465252fb5165087
Numero Unico: 091 R999900068148
Procesado: SI
COT: 54556552356565
```


**Importante**: Dependiendo como este generado el instalador, puede ser necesario usar ```COT_CLI.EXE```. 

Para producción, anteponer `--prod` en la linea de comando (primer parámetro)

Para guardar  el resultado, se puede redirigir la salida a un archivo, por ej. agregando `> resultado.txt`

En linux o desde el código fuente invocar con el interprete `python`.
## Ejemplo Intefase COM en VB (5/6)

```
#!vb

Dim COT As Object, ok As Variant

' Crear la interfaz COM
Set COT = CreateObject("COT")

Debug.Print COT.Version
Debug.Print COT.InstallDir

' Establecer Datos de acceso (ARBA)
COT.Usuario = "20267565393"
COT.Password = "23456"

' Archivo a enviar (ruta absoluta):
filename = "C:\TB_20111111112_000000_20080124_000001.txt"
' Respuesta de prueba (dejar en blanco si se tiene acceso para respuesta real):
testing = "" ' "C:\cot_response_2_errores.xml"

' Conectar al servidor (pruebas)
URL = "https://cot.test.arba.gov.ar/TransporteBienes/SeguridadCliente/presentarRemitos.do"
ok = COT.Conectar(URL)

' Enviar el archivo y procesar la respuesta:
ok = COT.PresentarRemito(filename, testing)

' Hubo error interno?
If COT.Excepcion <> "" Then
    Debug.Print COT.Excepcion, COT.Traceback
    MsgBox COT.Traceback, vbCritical, "Excepcion:" & COT.Excepcion
Else
    Debug.Print COT.XmlResponse
    Debug.Print "Error General:", COT.TipoError, "|", COT.CodigoError, "|", COT.MensajeError
    
    ' Hubo error general de ARBA?
    If COT.CodigoError <> "" Then
        MsgBox COT.MensajeError, vbExclamation, "Error " & COT.TipoError & ":" & COT.CodigoError
    End If
    
    ' Datos de la respuesta:
    Debug.Print "CUIT Empresa:", COT.CuitEmpresa
    Debug.Print "Numero Comprobante:", COT.NumeroComprobante
    Debug.Print "Nombre Archivo:", COT.NombreArchivo
    Debug.Print "Codigo Integridad:", COT.CodigoIntegridad
    Debug.Print "Numero Unico:", COT.NumeroUnico
    Debug.Print "Procesado:", COT.Procesado
    Debug.Print "COT:", COT.COT                           ' Version 1.3a+ (2019)
    
    MsgBox "CUIT Empresa: " & COT.CuitEmpresa & vbCrLf & _
            "Numero Comprobante: " & COT.NumeroComprobante & vbCrLf & _
            "Nombre Archivo: " & COT.NombreArchivo & vbCrLf & _
            "Codigo Integridad: " & COT.CodigoIntegridad & vbCrLf & _
            "Numero Unico: " & COT.NumeroUnico & vbCrLf & _
            "Procesado: " & COT.Procesado, _
            vbInformation, "Resultado"
    
    While COT.LeerErrorValidacion():
        Debug.Print "Error Validacion:", COT.TipoError, "|", COT.CodigoError, "|", COT.MensajeError
        MsgBox COT.MensajeError, vbExclamation, "Error Validacion:" & COT.CodigoError
    Wend
End If

```

Ejemplo para analizar varios remitos simultaneamente (enviados en el mismo archivo):
```
#!vb
' Lee el próximo remito, luego del último finaliza
While COT.LeerValidacionRemito()
    ' Imprime los datos de cada remito validado:
    Debug.Print "Numero Unico:", Cot.NumeroUnico
    Debug.Print "Procesado:", COT.Procesado
    Debug.Print "COT:", COT.COT                           ' Version 1.3a+ (2019)
    ' Lee los errores de validación de este remito
    While COT.LeerErrorValidacion()
        print "Error Validacion:", "|", cot.CodigoError, "|", cot.MensajeError
    Wend
Wend
```

Ejemplos de uso !ObtenerTagXml:
```
#!vb
' Obtengo el cuit de la empresa (dato general)
Debug.Print "cuit", COT.ObtenerTagXml('cuitEmpresa')
' Obtengo el campo procesado del primer remito validado:
Debug.Print "p0", COT.ObtenerTagXml('validacionesRemitos', 'remito', 0, 'procesado')
' Obtengo el campo cot del primer y segundo remito validado (2019):
Debug.Print "cot0", COT.ObtenerTagXml('validacionesRemitos', 'remito', 0, 'cot')
Debug.Print "cot1", COT.ObtenerTagXml('validacionesRemitos', 'remito', 1, 'cot')
```
## Archivo de Intercambio

El nombre de archivo debe ser: `TB_ + CUIT Empresa + _ + planta + puerta + _ + aaaammdd +  _ + secuencia + .txt`, por ej: "TB_30111111118_003002_20060716_000183.txt":

- CUIT empresa: 30-11111111-8
- Nro. Planta: 000
- Nro. Puerta: 002
- Fecha: 16-07-2006
- Nro. Secuencial: 000183

El diseño del archivo de texto de intercambio es el definido por ARBA en las especificaciones técnicas:
 [Diseño de Archivo de Texto (en desuso)](http://www.arba.gov.ar/Transporte_Bienes/VerPDF.asp?param=DA)
                                                                                                       
 [NUEVO Diseño de Archivo a partir del 3 de Junio de 2019 (prorrogado al 05/08/2019)](http://www.arba.gov.ar/archivos/Publicaciones/nuevodiseniodearchivotxt.pdf)

### Estructura del Archivo de Texto

Utiliza un formato delimitado por pipas ("|"), donde el primer campo es el tipo de registro:

- HEADER (Encabezado)
- TIPO_REGISTRO: 01
- CUIT_EMPRESA: (sin guiones) ej. 20111111112
- REMITO (al menos 1 registro)
- TIPO_REGISTRO: 02
- FECHA_EMISION: formato AAAAMMDD, ej. |20080124|
- CODIGO_UNICO: formato (CODIGO_AFIP, PREFIJO, NUMERO) ej. 091 |9999900068148|
- FECHA_SALIDA_TRANSPORTE: formato AAAAMMDD
- HORA_SALIDA_TRANSPORTE: formato HHMM
- SUJETO_GENERADOR: 'E' emisor, 'D' destinatario
- DESTINATARIO_CONSUMIDOR_FINAL: 0 no, 1 sí
- DESTINATARIO_TIPO_DOCUMENTO: 'DNI', 'LE', 'PAS', 'CI'
- DESTINATARIO_DOCUMENTO
- DESTIANTARIO_CUIT
- DESTINATARIO_RAZON_SOCIAL
- DESTINATARIO_TENEDOR: 0=no, 1=si. 
- DESTINO_DOMICILIO_CALLE
- DESTINO_DOMICILIO_NUMERO
- DESTINO_DOMICILIO_COMPLE
- DESTINO_DOMICILIO_PISO
- DESTINO_DOMICILIO_DTO
- DESTINO_DOMICILIO_BARRIO
- DESTINO_DOMICILIO_CODIGOP
- DESTINO_DOMICILIO_LOCALIDAD
- DESTINO_DOMICILIO_PROVINCIA: ver tabla de provincias
- PROPIO_DESTINO_DOMICILIO_CODIGO
- ENTREGA_DOMICILIO_ORIGEN: 'SI' o 'NO'
- ORIGEN_CUIT
- ORIGEN_RAZON_SOCIAL
- EMISOR_TENEDOR: 0=no, 1=si
- ORIGEN_DOMICILIO_CALLE
- ORIGEN DOMICILIO_NUMBERO
- ORIGEN_DOMICILIO_COMPLE
- ORIGEN_DOMICILIO_PISO
- ORIGEN_DOMICILIO_DTO
- ORIGEN_DOMICILIO_BARRIO
- ORIGEN_DOMICILIO_CODIGOP
- ORIGEN_DOMICILIO_LOCALIDAD
- ORIGEN_DOMICILIO_PROVINCIA: ver tabla de provincias
- TRANSPORTISTA_CUIT
- TIPO_RECORRIDO: 'U' urbano, 'R' rural, 'M' mixto
- RECORRIDO_LOCALIDAD: máx. 50 caracteres
- RECORRIDO_CALLE: máx. 40 caracteres
- RECORRIDO_RUTA: máx. 40 caracteres
- PATENTE_VEHICULO: 3 letras y 3 números
- PATENTE_ACOPLADO: 3 letras y 3 números
- PRODUCTO_NO_TERM_DEV: 0=No, 1=Si (devoluciones)
- IMPORTE: formato 12 enteros 2 decimales
- PRODUCTOS (al menos 1 registro):
- TIPO_REGISTRO: 03
- CODIGO_UNICO_PRODUCTO: ver [nomenclador COT (Transporte de Bienes)](http://www.arba.gov.ar/Aplicaciones/NomencladorTB/NomencladorTB.asp) 
- ARBA_CODIGO_UNIDAD_MEDIDA: ver tabla unidades de medida
- CANTIDAD: 13 enteros y 2 decimales (no incluir coma ni punto), ej 200 un -> 20000
- PROPIO_CODIGO_PRODUCTO: máx. 25 caracteres
- PROPIO_DESCRIPCION_PRODUCTO: máx. 40 caracteres
- PROPIO_DESCRIPCION_UNIDAD_MEDIDA: máx. 20 caracteres
- CANTIDAD_AJUSTADA: 13 enteros y 2 decimales (no incluir coma ni punto), ej 200 un -> 20000
- 04: FOOTER (Pie)
- TIPO_REGISTRO: 04
- CANTIDAD_TOTAL_REMITOS

### Contenido del Archivo de Texto

El archivo se compone de:

- un único registro 01 (header)
- al menos un remito (registros 02 y 03)
- un único registro 04 (footer)

Un remito se compone de:

- un registro 02 (remito)
- al menos un registro 03 (productos)

Se deberá respetar el órden en que se envían los registros 01, 02, 03, 04.

Los campos de los registros deben estar separados por "|" (pipe), y las longitudes especificadas en el diseño son el tamaño máximo, no debe completarse con 0 o espacios. 
Todos los registros deben terminar con un salto de linea (\n)

### Ejemplo Archivo de Texto

Ejemplo [attachment:TB_20111111112_000000_20080124_000001.txt]:

```
01|20111111112
02|20080124|0919999900068148|20080124| |E|0| | |30682115722|COMPUMUNDO S.A.| 0|Ruta Prov | |S/N|  | | |1200|PUERTO DE ESCOBAR|B| |NO| 23246414254|COMPUMUNDO S.A. | 0|San Martin 5797| |S/N| | | |1766|TABLADA| B| 20045162673|  | | | | | | |0
03|847150|3|100|23891|COMP. SP-3960 VP|UNI DAD| 100
03|852110|3|100|23763|VIDEO CAMARA GR-D750|UNI DAD|100
03|852520|3|500|23666|PERS MOTO K1 SILVER + MEM|UNI DAD| 500
03|852520|3|700|24159|PERSONAL NOKIA 5200 BLUE|UNI DAD| 700
03|852520|3|200|24182|PERS S.ERI C W200 BLAC+MEM|UNI DAD|200
03|852390|3|500|23348|DVD+R X10 4.7GB 10DPR120|UNI DAD|500
03|847170|3|100|23842|HDD 250GB 7200RPM|UNI DAD| 100
03|847160|3|500|23896|GAME PAD EUGA 10 BLUE B/W| UNI DAD| 500
03|847330|3|400|22891|CART TWI NPACK 21 NEGRO|UNI DAD| 400
03|850650|3|500|22693|PI LAS ALCALI NA AA X 4|UNI DAD| 500
03|852431|3|200|23846|NORTON ANTIVIRUS 2007|UNI DAD| 200
03|847170|3|400|23122|DVDRW 16X/18X DRU830A NEG|UNI DAD| 400
03|847170|3|1000|23914|DVDRW AOPEN 20X BOX|UNI DAD| 1000
03|852190|3|100|24248|REPROD DVD DVD-AVD800|UNI DAD| 100
03|851822|3|100|23621|J.PARL HT- 685|UNI DAD| 100
04| 1
```

Utilizar el programa `FORMATO_COT.EXE` (`formato_cot.py`) para analizar un archivo de remito electrónico.

Para más información, ver documentación oficial: [Ejemplos de remitos correctos e incorrectos](http://www.arba.gov.ar/Transporte_Bienes/VerPDF.asp?param=RCI) (***Importante:** requiere clave ARBA*)

### Errores Frecuentes

- !TipoError: DATO
- !CodigoError: 14
- !MensajeError: Número único : 91 R000100000001 No se puede procesar el registro 02-REMITO. Faltan datos.

Este problema puede ser causado por incorrecto uso de separadores de lineas (ARBA requiere CR LF).

__Ejemplo incorrecto enviado:__

```
00000000  30 31 7c 32 30 31 31 31  31 31 31 31 31 32 0d 30  |01|20111111112.0|
00000010  32 7c 32 30 31 37 30 31  31 39 7c 39 31 20 52 30  |2|20170119|91 R0|
```

__Ejemplo correcto en datos:__ ([datos/TB_20111111112_000000_20080124_000001.txt](https://github.com/reingart/pyafipws/blob/master/datos/TB_20111111112_000000_20080124_000001.txt))

```
00000000  30 31 7c 32 30 31 31 31  31 31 31 31 31 32 0d 0a  |01|20111111112..|
00000010  30 32 7c 32 30 30 38 30  31 32 34 7c 39 31 20 52  |02|20080124|91 R|
```

Revisar el CR (caracter 0d en hexadecimal, 13 en decimal) y LF (caracter 0a en hexadecimal, 10 en decimal).
ARBA requiere ambos.
## Tablas de validación

Para más información ver [Tablas de Validación](http://www.arba.gov.ar/Transporte_Bienes/VerPDF.asp?param=TV) (***Importante:** requiere clave ARBA*)
### Tabla de Unidades de medida para Organismo ARBA

| **Código** | **Descripción** |
|---|---|
| 1 | Kilogramos |
| 2 | Litros |
| 3 | Unidades |
| 4 | Metros cuadrados |
| 5 | Metros |
| 6 | Metros Cúbicos |
| 7 | Pares |

### Tabla Unidades de medida para Organismo OPDS

| **Código** | **Descripción** |
|---|---|
| 1 | Kilogramos |
| 2 | Litros |
| 3 | Unidades |

### Table de Provincias

| **Código** | **Descripción** |
|---|---|
| A | Salta |
| B | Buenos Aires |
| C | Capital Federal |
| D | San Luis |
| E | Entre Ríos |
| F | La Rioja |
| G | Santiago del Estero |
| H | Chaco |
| J | San Juan |
| K | Catamarca |
| L | La Pampa |
| M | Mendoza |
| N | Misiones |
| P | Formosa |
| Q | Neuquen |
| R | Río Negro |
| S | Santa Fé |
| T | Tucumán |
| U | Chubut |
| V | Tierra del Fuego |
| W | Corrientes |
| X | Córdoba |
| Y | Jujuy |
| Z | Santa Cruz |

### Table de Comprobantes para Organismo ARBA

| **Código DGI** | **Tipo** | **Descripción** |
|---|---|---|
| 001 | A | FACTURA A |
| 003 | A | NOTA DE CREDITO A |
| 006 | B | FACTURA B |
| 008 | B | NOTA DE CREDITO B |
| 011 | C | FACTURA C |
| 013 | C | NOTA DE CREDITO C |
| 051 | M | FACTURA M |
| 053 | M | NOTA DE CREDITO M |
| 058 | M | CUENTA DE VENTA Y LIQUIDO PRODUCTO M |
| 060 | A | CUENTA DE VENTA Y LIQUIDO PRODUCTO A |
| 061 | B | CUENTA DE VENTA Y LIQUIDO PRODUCTO B |
| 074 | P | CARTA DE PORTE |
| 081 | A | TIQUE FACTURA A |
| 082 | B | TIQUE FACTURA B |
| 083 |  | TIQUE |
| 088 |  | REMITO ELECTRONICO |
| 091 | R | REMITO R |
| 093 | C | CUENTA DE VENTA Y LIQUIDO PRODUCTO C |
| 094 | X | REMITO X |
| 095 | G | GUIA UNICA DE TRASLADO |
| 099 | E | DOCUMENTO EQUIVALENTE |
| 110 |  | TIQUE NOTA DE CREDITO |
| 111 | C | TIQUE FACTURA C |
| 112 | A | TIQUE NOTA DE CREDITO A |
| 113 | B | TIQUE NOTA DE CREDITO B |
| 114 | C | TIQUE NOTA DE CREDITO C |
| 118 | M | TIQUE FACTURA M |
| 119 | M | TIQUE NOTA DE CREDITO M |
| 995 |  | REMITO ELECTRONICO CARNICO |

### Table de Comprobantes para Organismo OPDS

| **Código DGI** | **Tipo** | **Descripción** |
|---|---|---|
| MA | PR | Manifiesto Ley 11720 |


## Novedades

### RG 38/2014 API

Con fecha 12/11/2015 se publicó la Resolución General Resolución General 0038/2014 de la Administración Provincial de Impuestos de la Provincia de Santa Fe establece:

   La obligación de obtener el Código de Operación de Translado (COT) por parte de los sujetos obligados a emitir comprobantes por operaciones referidas en la RG 1415/03 AFIP incisos artículos 1° F. y 8° C., que efectúen el translado de mercaderías en el ámbito de la Provincia de Santa Fe por cualquier medio y/o vía de transporte -terrestre, fluvia, aérea-, siempre que el lugar de origen y/o destino se encuentre ubicado dentro de su territorio.

   [santafe.gov.ar/impuestos](https://www.santafe.gov.ar/index.php/web/content/view/full/121997/(subtema)/118225)


- [Norma completa](https://www.santafe.gov.ar/index.php/web/content/download/211235/1091408/file/Resoluci%C3%B3n%20General%20%200038_2014.pdf)
- Nomenclador de Productos:[Parte 1](https://www.santafe.gov.ar/index.php/web/content/download/211240/1091423/file/Anexo%20II_Parte1.pdf), [Parte 2](https://www.santafe.gov.ar/index.php/web/content/download/211241/1091426/file/Anexo%20II_Parte2.pdf) (Anexo II)
- [Rubros y bienes (Anexo III)](https://www.santafe.gov.ar/index.php/web/content/download/211237/1091414/file/Anexo%20III.pdf)

### Foro anuncios

Se recuerda que esta disponible el 
[grupo de noticias](http://www.pyafipws.com.ar) (http://groups.google.com.ar/group/pyafipws) donde
se publicarán futuras novedades sobre PyAfipWS: servicios web de
factura electrónica y sus interfases (se recomienda suscribirse)
### Leyendas para Remitos - Número de COT

Cuando se utiliza el canal AUTOMÁTICO, no sería necesaria ninguna documentación adicional, sólo bastaría consignar los datos originales (CUIT y N° de remito papel), para que el inspector de ARBA puede realizar la validación. Respuesta de ARBA:

    *Se exhibe el "comprobante papel", sea este remito, factura o equivalente, el cual estará amparado por su transferencia electrónica bajo la modalidad REMITO ELECTRONICO. Resulta recomendable agregar una leyenda en el comprobante haciendo mención a la "Transferencia electrónica en virtud de DN ARBA Nº 32/06 mod. y comp." Eso ayuda a quien visualice en un control que el comprobante exhibido tiene su transferencia electrónica. El nº de remito electrónico se compone de 16 digitos conformados por: 2 primeros en función al tipo de comprobante (91 si es remito) los dos siguientes son un espacio y la letra de ese comprobante ejemplo " R", los restantes 12 son taxativamente los números del comprobante físico Ejemplo 91 R000100004445 correspondiendo a un remito R papel nº 0001-00004445 Así debe ser generado respetando las tablas de validación y diseño especificas de remito electrónico*
## Aplicativo visual para COT

La interfase de usuario es gráfica de escritorio (GUI), funciona en Windows o Linux:

[[Image(aplicativo_remito_electronico.png, align=center)]]

- Lee archivos de remitos desde distintas ubicaciones 
- Procesa los archivos seleccionados (múltiples remitos)
- Muestra los resultados por pantalla (maestro/detalle por cada remito)
- Mueve los archivos procesados a una ubicación definitiva

## Costos y Condiciones

Por soporte comercial consultar al (011) 15-3048-9211 o por mail a info@sistemasagiles.com.ar

Más información en PyAfipWs (ver [Costos y Condiciones del Soporte Comercial](wiki:PyAfipWs#CostosyCondiciones))

MarianoReingart
MarianoReingart