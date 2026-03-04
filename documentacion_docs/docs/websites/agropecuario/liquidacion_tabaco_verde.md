# Liquidación Electrónica de Tabaco Verde


Web Services – (Servicios Web) Liquidación de Tabaco Verde. Generación de una liquidación de tabaco comprado a productores y obtención del CAE (Código de Autorización Electrónico).


## Descripción General

EL WSLTV (Web Service de Liquidación de Tabaco Verde) es un nuevo Servicio Web de la AFIP según [Especificación Técnica 1.1](http://www.afip.gob.ar/ws/tabaco/manual_wsltv_1.1.pdf)
El webservice permite:

- Generación de una liquidación de tabaco comprado a productores y obtención del CAE (Código de Autorización Electrónico).
- Ajustar una o varias liquidaciones hechas con anterioridad.
- Consultas:
- Liquidaciones por CAE y número de comprobante.
- Último número de comprobante por punto de venta.
- Listado de provincias.
- Listado de variedades y clases de tabaco.
- Listado de condiciones de venta.
- Listado de puntos de venta y depósitos de acopio 
- Listado de retenciones tabacaleras y tributos.
- Consulta de totales liquidados para un conjunto de CAEs.

Para mayor información, se puede consultar la documentación orignal en [Micrositio Webservices - AFIP](http://www.afip.gov.ar/ws/paso4.asp) o el [manual](../documentacion_herramientas/manualpyafipws.md) de la presente interfaz. 

URL:

- https://fwshomo.afip.gov.ar/wsltv/LtvService?wsdl (homologación: testing/pruebas)
- https://serviciosjava.afip.gob.ar/wsltv/LtvService?wsdl (producción)

## Descargas

- Instalador: [PyAfipWs-2.7.1945-32bit+wsaa_2.11c+wsltv_1.06b-homo.exe](https://www.sistemasagiles.com.ar/soft/pyafipws/PyAfipWs-2.7.1945-32bit+wsaa_2.11c+wsltv_1.06b-homo.exe) (versión preliminar WSLTVv1.3)
- Documentación: [Documento Oficial WSLTVv1.0 http://www.afip.gob.ar/ws/tabaco/manual_wsltv_1.0.pdf] (AFIP), [Manual de Uso General](../documentacion_herramientas/manualpyafipws.md) ([PDF](http://www.sistemasagiles.com.ar/trac/wiki/ManualPyAfipWs?format=pdf))
- Ejemplo en VB: [wsltv.bas](https://github.com/reingart/pyafipws/blob/master/ejemplos/wsltv/wsltv.bas) *(actualizado)*
- Archivos de intercambio (muestras): *proximamente*
- Código Fuente (Python): [wsltv.py](hhttps://github.com/reingart/pyafipws/blob/master/wsltv.py)
- Ejemplo PDF: [wsltv_liq.pdf](attachment:wsltv_liquidacion_tabaco_verde.pdf) (homologación)

## Metodos

- **`Conectar(cache=None, url="", proxy="")`**: en homologación no hace falta pasarle ningún parámetro. En producción, el segudo parametro es la WSDL.
- **`Dummy()`**: devuelve estado de servidores

Métodos para generar una liquidación de tabaco verde (LTV):

- **`CrearLiquidacion(self, tipo_cbte, pto_vta, nro_cbte, fecha, cod_deposito_acopio, tipo_compra, variedad_tabaco, cod_provincia_origen_tabaco, puerta, nro_tarjeta, horas, control, nro_interno, iibb_emisor, fecha_inicio_actividad)`**: crea una liquidación  a autorizar, inicializando los datos de cabecera. Los siguientes campos son opcionales: `puerta`, `nro_tarjeta`, `horas`, `control`, `nro_interno`, `iibb_emisor`
- **`AgregarCondicionVenta(codigo, descripcion)`**: agrega una condición de venta
- **`AgregarReceptor(cuit, iibb, nro_socio, nro_fet)`**: agrega los datos del receptor
- **`AgregarRomaneo(nro_romaneo, fecha_romaneo)`**: agrega una condición de romaneo (uno o más elementos)
- **`AgregarFardo(cod_trazabilidad, clase_tabaco, peso)`**: agrega los datos del fardo al último romaneo agregado (uno o más elementos)
- **`AgregarPrecioClase(clase_tabaco, precio)`**: agrega la estructura precio clase (uno o más elementos)
- **`AgregarRetencion(cod_retencion, descripcion, importe)`**: agrega una retención de tabaco (Cámara Tabacalera,  Seguro Granizo, Asociación Mutual de Prod. Tabacaleros,  Adelantos de insumos, etc.).
- **`AgregarTributo(codigo_tributo, descripcion, base_imponible, alicuota, importe)`**: agrega un tributo (impuestos nacionales, provinciales, municipales, etc.)
- **`AutorizarLiquidacion()`**: arma la liquidación, envía los datos a AFIP y devuelve `COE`, estableciendo los atributos con los campos de la respuesta.

Métodos adicionales de consulta:

- **`ConsultarLiquidacion(pto_vta, nro_cbte, cae, pdf):`**: Consulta una liquidación por No de comprobante o CAE (establece el resto de los atributos, similar a `AutorizarLiquidacion`). En `pdf` (indicar nombre de archivo para descargarlo de AFIP)
- **`ConsultarUltimoComprobante(tipo_cbte, pto_vta)`**: devuelve el último No de comprobante registrado por AFIP (atributo `NroComprobante`). 

## Atributos

- **`CAE`**
- **`NroComprobante`**
- **`FechaLiquidacion`**
- **`ImporteNeto`**, **`TotalRetenciones`**, **`TotalTributos`**, **`AlicuotaIVA`**, **`ImporteIVA`**, **`Subtotal`**, **`Total`**

## Herramienta por consola

La interfaz presenta una herramienta universal (multiplataforma -linux / windows / mac- compatible con cualquier lenguaje de programación), que puede ser operado de manera automática en segundo plano (no requiere intervención del usuario).

El modo de uso es ejecutando el programa **`WSLTV_CLI.EXE`** con las siguientes opciones y archivos de intercambio.
La herramienta puede ser ejecutada interactivamente en una consola (Inicio, Ejecutar, CMD.EXE) o puede ser llamada desde otro programa o script .BAT

### Parámetros por línea de comando

La herramienta soporta las siguientes opciones principales:

- `--dummy`: consulta estado de servidores
- `--autorizar`: autoriza una liquidación

Recuperación de datos:

- `--consultar`: recupera una liquidacíon
- `--ult`: obtiene el último número de comprobante registrado en AFIP

Tablas de referencias:

- `--provincias`: obtiene el listado de provincias
- `--condicionesventa`: obtiene el listado de condiciones de venta 
- `--tributos`: obtiene el listado de tributos
- `--retenciones`: obtiene el listado de las retenciones de tabaco
- `--variedades`: obtiene el listado de las variedades y especies de tabaco
- `--depositos`: obtiene el listado de los depositos de acopio (para el contrib.)
- `--puntosventa`: obtiene el listado de puntos de venta habilitados


Parámetros auxiliares:

- `--ayuda`: este mensaje
- `--debug`: modo depuración (detalla y confirma las operaciones)
- `--formato`: muestra el formato de los archivos de entrada/salida
- `--prueba`: genera y autoriza una LTV de prueba (no usar en producción!)
- `--xml`: almacena los requerimientos y respuestas XML (depuración)

### Ejemplo

Generar un LTV de prueba (no usar en producción):

```
C:\PYAFIPWS\> WSLTV_CLI.EXE --autorizar --prueba  --testing
Liquidacion: pto_vta=2002 nro_cbte=1 tipo_cbte=150
Autorizando...
Errores: []
CAE 85523002502850
FechaLiquidacion 2016-01-01
NroComprobante 31
ImporteNeto 171000.0
AlicuotaIVA 21.0
ImporteIVA 35910.0
Subtotal 206910.0
TotalRetenciones 24.0
TotalTributos 1200.54
Total 205685.46
hecho.
```

### Archivo de Configuración

Para utilizar este webservice, debe tramitarse un certificado. Ver [Instructivo](../documentacion_herramientas/manualpyafipws.md#certificados)

Luego, se debe configurar el Certificado, clave privada y URL en el archivo de configuración WSLTV.INI:

```
[WSAA]
CERT=reingart.crt
PRIVATEKEY=reingart.key
##URL=https://wsaa.afip.gov.ar/ws/services/LoginCms

[WSLTV]
CUIT=20267565393
ENTRADA=facturas.csv
SALIDA=salida.txt
##URL=https://serviciosjava.afip.gob.ar/wsltv/LtvService?wsdl
```

Para producción, se debe usar un instalador para tal fin y descomentar la URL (eliminando el numeral). 

El tipo de archivo de intercambio depende de la extensión configurada en WSLTV (usar .txt para texto, .csv para planillas CSV, .dbf para tablas DBF y .json para JavaScript)

## Archivo de Intercambio

La herramienta por consola puede soportar tanto:

- archivos de texto de ancho fijo (similares al usado por SIAP -COBOL-): ver [y [attachment:salida_wsltv.txt](attachment:entrada_wsltv.txt]) (muestras ejemplo)
- planillas CSV (archivo de texto valores separados por coma): ver [y [attachment:salida_wsltv.csv](attachment:entrada_wsltv.csv]) (muestras ejemplo WSLTVv1.1)
- tablas DBF (dBase, !FoxPro, Clipper, etc.): ver [wsltv_dbf.zip](attachment:wsltv_dbf.zip) (tablas de muestra WSLTVv1.1)
- archivo JSON (notación de objetos !JavaScript): : ver [attachment:salida_wsltv.json] (muestras ejemplo WSLTVv1.1)


## Ejemplo Pseudocodigo

Ver ejemplo completo para Visual Basic o similar en: [wsltv.bas](https://github.com/reingart/pyafipws/blob/master/ejemplos/wsltv/wsltv.bas) (adaptable a otros lenguajes como Visual Fox Pro, Delphi, etc. -ver otros webservices o consultar-)

```
#!python

# genero una liquidación de ejemplo:
tipo_cbte = 150
pto_vta = 2002
ok = wsltv.ConsultarUltimoComprobante(tipo_cbte, pto_vta)
nro_cbte = wsltv.NroComprobante + 1

# datos de la cabecera:
fecha = '2016-01-01'
cod_deposito_acopio = 207
tipo_compra = 'CPS'
variedad_tabaco = 'BR'
cod_provincia_origen_tabaco = 1
puerta = 22
nro_tarjeta = 6569866
horas = 12
control = "FFAA"
nro_interno = "77888"
iibb_emisor = None
fecha_inicio_actividad = "2016-04-01"

# cargo la liquidación:
wsltv.CrearLiquidacion(
    tipo_cbte, pto_vta, nro_cbte, fecha, 
    cod_deposito_acopio, tipo_compra,
    variedad_tabaco, cod_provincia_origen_tabaco,
    puerta, nro_tarjeta, horas, control,
    nro_interno, iibb_emisor,
    fecha_inicio_actividad)

wsltv.AgregarCondicionVenta(codigo=99, descripcion="otra")

# datos del receptor:
cuit = 20111111112
iibb = 123456
nro_socio = 11223   
nro_fet = 22
wsltv.AgregarReceptor(cuit, iibb, nro_socio, nro_fet)


# datos romaneo:
nro_romaneo = 321
fecha_romaneo = "2015-12-10"
wsltv.AgregarRomaneo(nro_romaneo, fecha_romaneo)
# fardo:
cod_trazabilidad = 355
clase_tabaco = 4
peso= 900
wsltv.AgregarFardo(cod_trazabilidad, clase_tabaco, peso)

# precio clase:
precio = 190
wsltv.AgregarPrecioClase(clase_tabaco, precio)

# retencion:
descripcion = "otra retencion"
cod_retencion = 99
importe = 12
wsltv.AgregarRetencion(cod_retencion, descripcion, importe)

# tributo:
codigo_tributo = 99
descripcion = "Ganancias"
base_imponible = 15000
alicuota = 8
importe = 1200
wsltv.AgregarTributo(codigo_tributo, descripcion, base_imponible, alicuota, importe)

print "Autorizando..." 
ret = wsltv.AutorizarLiquidacion()
    
print "EXCEPCION:", wsltv.Excepcion
print "Errores:", wsltv.Errores

print "CAE", wsltv.CAE
print "FechaLiquidacion", wsltv.FechaLiquidacion
print "NroComprobante", wsltv.NroComprobante
print "ImporteNeto", wsltv.ImporteNeto
print "AlicuotaIVA", wsltv.AlicuotaIVA
print "ImporteIVA", wsltv.ImporteIVA
print "Subtotal", wsltv.Subtotal
print "TotalRetenciones", wsltv.TotalRetenciones
print "TotalTributos", wsltv.TotalTributos
print "Total", wsltv.Total

# ejemplo para obtener parámetros de salida:
print wsltv.GetParametro("fecha")    
print wsltv.GetParametro("peso_total_fardos_kg")  
print wsltv.GetParametro("cantidad_total_fardos")
print wsltv.GetParametro("emisor", "domicilio")
print wsltv.GetParametro("emisor", "razon_social")
print wsltv.GetParametro("receptor", "domicilio")
print wsltv.GetParametro("receptor", "razon_social")

print wsltv.GetParametro("romaneos", 0, "detalle_clase", 0, "cantidad_fardos")
print wsltv.GetParametro("romaneos", 0, "detalle_clase", 0, "cod_clase")
print wsltv.GetParametro("romaneos", 0, "detalle_clase", 0, "importe")
print wsltv.GetParametro("romaneos", 0, "detalle_clase", 0, "peso_fardos_kg")
print wsltv.GetParametro("romaneos", 0, "detalle_clase", 0, "precio_x_kg_fardo")
print wsltv.GetParametro("romaneos", 0, "nro_romaneo")
print wsltv.GetParametro("romaneos", 0, "fecha_romaneo")

```

## Liquidación PDF

La interfaz permite obtener los archivos que devuelve AFIP mediante este webservice:
 
- [attachment:wsltv.pdf]: Liquidación Tabaco Verde en documento PDF

En ambos casos, AFIP devuelve el archivo binario ya generado, por lo que se debe especificar una ruta completa para almacenarlo.
Necesita Acrobat Reader, Microsoft Office / Libre Office o similares para poder abrir los documentos.

## Tablas de Parámetros

En este nuevo servicio web WSLTV utiliza tablas dinámicas para los siguientes datos:

- Provincias
- Variedades y clases de tabaco
- Puntos de venta
- Condiciones de venta
- Depósitos de acopio
- Retenciones tabacaleras 
- Tributos

La interfaz permite obtener los diversos códigos de parámetros a utilizar. A continuación se detallan a modo de ejemplo:

### Provincias

| Código | Descripción |
|---|---|
| 1 | BUENOS AIRES |
| 0 | CAP.FEDERAL |
| 2 | CATAMARCA |
| 16 | CHACO |
| 17 | CHUBUT |
| 3 | CORDOBA |
| 4 | CORRIENTES |
| 5 | ENTRE RIOS |
| 18 | FORMOSA |
| 6 | JUJUY |
| 21 | LA PAMPA |
| 8 | LA RIOJA |
| 7 | MENDOZA |
| 19 | MISIONES |
| 20 | NEUQUEN |
| 22 | RIO NEGRO |
| 9 | SALTA |
| 10 | SAN JUAN |
| 11 | SAN LUIS |
| 23 | SANTA CRUZ |
| 12 | SANTA FE |
| 13 | SGO.DEL ESTERO |
| 24 | TIER.DEL FUEGO |
| 14 | TUCUMAN |

### Condiciones Venta

| Código | Descripción |
|---|---|
| 1 | Contado |
| 96 | Cuenta Corriente |
| 97 | Cheque |
| 99 | Otra |


### Tributos

| Código | Descripción |
|---|---|
| 1 | Impuestos nacionales |
| 2 | Impuestos provinciales |
| 3 | Impuestos municipales |
| 4 | Impuestos internos |
| 5 | IIBB |
| 6 | Percepción de IVA |
| 7 | Percepción de IIBB |
| 8 | Percepciones por Impuestos Municipales |
| 9 | Otras Percepciones |
| 99 | Otros |

### Retenciones Tabacaleras

| Código | Descripción |
|---|---|
| 11 | Cámara Tabacalera |
| 12 | Seguro Granizo |
| 13 | Asociación Mutual de Prod. Tabacaleros |
| 14 | Adelantos de insumos |
| 15 | Otra |

### Variedades / Clases de Tabaco

|  | Variedad |  | Clase |
|---|---|---|---|
| Código | Descripción | Descripción | Código |
| BR | Burley | B1F | 3 |
| BR | Burley | B1FR | 4 |
| BR | Burley | B2F | 11 |
| BR | Burley | B2FR | 12 |
| BR | Burley | B3F | 22 |
| BR | Burley | B3FR | 23 |
| BR | Burley | B3K | 24 |
| BR | Burley | C1F | 6 |
| BR | Burley | C1L | 5 |
| BR | Burley | C2F | 14 |
| BR | Burley | C2L | 13 |
| BR | Burley | C3F | 19 |
| BR | Burley | C3K | 20 |
| BR | Burley | C3L | 18 |
| BR | Burley | NB | 27 |
| BR | Burley | NG | 25 |
| BR | Burley | NX | 26 |
| BR | Burley | T1F | 1 |
| BR | Burley | T1FR | 2 |
| BR | Burley | T2F | 9 |
| BR | Burley | T2FR | 10 |
| BR | Burley | T3K | 17 |
| BR | Burley | X1F | 8 |
| BR | Burley | X1L | 7 |
| BR | Burley | X2F | 16 |
| BR | Burley | X2L | 15 |
| BR | Burley | X3K | 21 |
| CA | Criollo Argentino | B1 | 111 |
| CA | Criollo Argentino | B2 | 112 |
| CA | Criollo Argentino | B3 | 113 |
| CA | Criollo Argentino | C1 | 109 |
| CA | Criollo Argentino | C2 | 110 |
| CA | Criollo Argentino | N | 116 |
| CA | Criollo Argentino | T2 | 114 |
| CA | Criollo Argentino | T4 | 115 |
| CA | Criollo Argentino | X2 | 107 |
| CA | Criollo Argentino | X4 | 108 |
| CH | Criollo Chaqueño | CH1 | 35 |
| CH | Criollo Chaqueño | CH2 | 36 |
| CH | Criollo Chaqueño | CH3 | 37 |
| CH | Criollo Chaqueño | ND | 38 |
| CC | Criollo Correntino | C1 | 28 |
| CC | Criollo Correntino | C2 | 29 |
| CC | Criollo Correntino | C3 | 30 |
| CC | Criollo Correntino | N | 34 |
| CC | Criollo Correntino | T | 33 |
| CC | Criollo Correntino | X1 | 31 |
| CC | Criollo Correntino | X2 | 32 |
| CM | Criollo Misionero | B1 | 41 |
| CM | Criollo Misionero | B2 | 42 |
| CM | Criollo Misionero | C1 | 39 |
| CM | Criollo Misionero | C2 | 40 |
| CM | Criollo Misionero | N4 | 45 |
| CM | Criollo Misionero | N5 | 46 |
| CM | Criollo Misionero | T1 | 43 |
| CM | Criollo Misionero | X1 | 44 |
| CS | Criollo Salteño | B1F | 50 |
| CS | Criollo Salteño | B1L | 49 |
| CS | Criollo Salteño | B3 | 53 |
| CS | Criollo Salteño | C1F | 48 |
| CS | Criollo Salteño | C1L | 47 |
| CS | Criollo Salteño | C3 | 52 |
| CS | Criollo Salteño | N4B | 56 |
| CS | Criollo Salteño | N4X | 55 |
| CS | Criollo Salteño | T2 | 54 |
| CS | Criollo Salteño | X2 | 51 |
| KA | Kentucky Ahumado | B1 | 117 |
| KA | Kentucky Ahumado | B2 | 118 |
| KA | Kentucky Ahumado | B3 | 119 |
| KA | Kentucky Ahumado | N2 | 123 |
| KA | Kentucky Ahumado | X1 | 120 |
| KA | Kentucky Ahumado | X2 | 121 |
| KA | Kentucky Ahumado | X3 | 122 |
| ME | Mezcla | ME | 105 |
| TI | Tabaco Importado | TI | 106 |
| VR | Virginia | B1F | 59 |
| VR | Virginia | B1L | 60 |
| VR | Virginia | B2F | 69 |
| VR | Virginia | B2KF | 72 |
| VR | Virginia | B2KL | 71 |
| VR | Virginia | B2L | 70 |
| VR | Virginia | B3F | 79 |
| VR | Virginia | B3KF | 82 |
| VR | Virginia | B3KL | 81 |
| VR | Virginia | B3L | 80 |
| VR | Virginia | B4F | 89 |
| VR | Virginia | B4L | 90 |
| VR | Virginia | C1F | 61 |
| VR | Virginia | C1L | 62 |
| VR | Virginia | C2F | 73 |
| VR | Virginia | C2K | 75 |
| VR | Virginia | C2L | 74 |
| VR | Virginia | C3F | 83 |
| VR | Virginia | C3K | 85 |
| VR | Virginia | C3L | 84 |
| VR | Virginia | C4F | 91 |
| VR | Virginia | C4L | 92 |
| VR | Virginia | H1F | 102 |
| VR | Virginia | H2F | 103 |
| VR | Virginia | H3F | 104 |
| VR | Virginia | N5B | 101 |
| VR | Virginia | N5C | 100 |
| VR | Virginia | N5K | 98 |
| VR | Virginia | N5X | 99 |
| VR | Virginia | NVB | 97 |
| VR | Virginia | NVC | 96 |
| VR | Virginia | NVX | 95 |
| VR | Virginia | T1F | 57 |
| VR | Virginia | T1L | 58 |
| VR | Virginia | T2F | 65 |
| VR | Virginia | T2KF | 68 |
| VR | Virginia | T2KL | 67 |
| VR | Virginia | T2L | 66 |
| VR | Virginia | X1F | 63 |
| VR | Virginia | X1L | 64 |
| VR | Virginia | X2F | 76 |
| VR | Virginia | X2K | 78 |
| VR | Virginia | X2L | 77 |
| VR | Virginia | X3F | 86 |
| VR | Virginia | X3K | 88 |
| VR | Virginia | X3L | 87 |
| VR | Virginia | X4F | 93 |
| VR | Virginia | X4L | 94 |

## Novedades

Historial de Cambios:

- Febrero 2016 (actualización 01): versión inicial
- Febrero 2017 (actualización 18): revisiones varias, ajusto link instalador actualizado

Se recuerda que esta disponible el 
[grupo de noticias](http://groups.google.com.ar/group/pyafipws) donde
se publicarán futuras novedades sobre PyAfipWS: servicios web de
factura electrónica y sus interfases (se recomienda suscribirse)

## Costos y Condiciones

Debido a la complejidad de este servicio, su fecha de aplicación y las modificaciones que pudieran surgir, los clientes que asi lo requieran pueden adquirir horas de soporte técnico comercial (ver [Condiciones del Soporte Comercial](../documentacion_herramientas/pyafipws.md#costos-y-condiciones)).

A su vez, se libera el código fuente bajo licencia GPL (software libre), al igual que se hizo con el restos de los servicios web. Para más detalles ver página FacturaElectronica.