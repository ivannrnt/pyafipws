= Liquidación Electrónica Única Mensual de Lechería  =

[[TracNav(noreorder|FacturaElectronica)]]


Web Services – (Servicios Web)  Liquidación Mensual Única de Lechería. Generación de una liquidación mensual única y obtención del CAE (Código de Autorización Electrónico). 

## Índice
[[Image(htdocs:logo-pyafipws.png, align=right)]]
[[TOC(noheading,inline,depth=2)]]
## Descripción General

EL WSLUM (Web Service de Liquidación única mensual de Lecheria) es un nuevo Servicio Web de la AFIP según [Especificación Técnica 1.2](https://www.afip.gob.ar/ws/wslum/manual_wslum1.2.pdf)
El webservice permite:

- Generación de una liquidación mensual única y obtención del CAE (Código de Autorización Electrónico).
- Ajustar una liquidación.
- Consultas:
- Liquidaciones por CAE y número de comprobante.
- Último número de comprobante por punto de venta.
- Tablas de parámetros:
- Listado de provincias.
- Bonificaciones, penalizaciones y débitos comerciales.
- Otros impuestos.

Para mayor información, se puede consultar la documentación orignal en [Micrositio Webservices - AFIP](http://www.afip.gov.ar/ws) o el [manual](wiki:ManualPyAfipWs) de la presente interfaz. 

URL:

- https://fwshomo.afip.gov.ar/wslum/LumService?wsdl (homologación: testing/pruebas)
- https://serviciosjava.afip.gob.ar/wslum/LumService?wsdl (producción)

## Descargas

- Instalador: [PyAfipWs-2.7.1911-32bit+wsaa_2.11b+wslum_1.02a-homo.exe](https://www.sistemasagiles.com.ar/soft/pyafipws/PyAfipWs-2.7.1911-32bit+wsaa_2.11b+wslum_1.02a-homo.exe) (versión preliminar WSLUMv1.3)
- Documentación: [Documento Oficial WSLUMv1.3](https://www.afip.gob.ar/ws/wslum/manual_wslum1.3.pdf) (AFIP), [Manual de Uso General](wiki:ManualPyAfipWs) ([PDF](http://www.sistemasagiles.com.ar/trac/wiki/ManualPyAfipWs?format=pdf))
- Ejemplo en VB: [wslum.bas](https://github.com/reingart/pyafipws/blob/master/ejemplos/wslum/wslum.bas) *(actualizado)*
- Archivos de intercambio (muestras): [[attachment:wslum_salida.json](attachment:wslum_entrada.json])
- Código Fuente (Python): [wslum.py](https://github.com/reingart/pyafipws/blob/master/wslum.py)

## Metodos

- **`Conectar(cache=None, url="", proxy="")`**: en homologación no hace falta pasarle ningún parámetro. En producción, el segudo parametro es la WSDL.
- **`Dummy()`**: devuelve estado de servidores

Métodos para generar una liquidación única de lechería (LUM):

- **`CrearLiquidacion(tipo_cbte, pto_vta, nro_cbte, fecha, periodo, iibb_adquirente, domicilio_sede, inscripcion_registro_publicone, datos_adicionales, alicuota_iva)`**: crea una liquidación  a autorizar, inicializando los datos de cabecera (los 5 primeros parametros son obligatorios, el resto opcional).
- **`AgregarCondicionVenta(codigo, descripcion)`**: agrega una o más condiciones de venta (detalle opcional)
- **`AgregarTambero(cuit, iibb)`**: agrega los datos del productor (iibb es opcional)
- **`AgregarTambo(nro_tambo_interno, nro_renspa, fecha_venc_cert_tuberculosis, fecha_venc_cert_brucelosis, nro_tambo_provincial)`**: agrega los datos del tambo (nro_tambo_provincial es opcional)
- **`AgregarUbicacionTambo(latitud, longitud, domicilio, cod_localidad, cod_provincia, codigo_postal, nombre_partido_depto)`**: agrega los datos del tambo (nombre_partido_depto es opcional)
- **`AgregarBalanceLitrosPorcentajesSolidos(litros_remitidos, litros_decomisados, kg_grasa, kg_proteina)`**: agrega los litros remitidos, decomisados, kg. grasa / proteína
- **`AgregarConceptosBasicosMercadoInterno(kg_produccion_gb, precio_por_kg_produccion_gb, kg_produccion_pr, precio_por_kg_produccion_pr, kg_crecimiento_gb, precio_por_kg_crecimiento_gb, kg_crecimiento_pr, precio_por_kg_crecimiento_pr)`**: agrega los kg y precio de producción (GB/PR)
- **`AgregarConceptosBasicosMercadoExterno(kg_produccion_gb, precio_por_kg_produccion_gb, kg_produccion_pr, precio_por_kg_produccion_pr, kg_crecimiento_gb, precio_por_kg_crecimiento_gb, kg_crecimiento_pr, precio_por_kg_crecimiento_pr)`**: agrega los kg y precio de producción (GB/PR)
- **`AgregarBonificacionPenalizacion(codigo, detalle, resultado, porcentaje, importe)`**: agrega bonificaciones o recargos por calidad/comerciales (ver tabla de parámetros) -uno o más elementos, codigo/detalle obligatorio-
- **`AgregarOtroImpuesto(tipo, base_imponible, alicuota, detalle)`**: agrega un tributo (impuestos nacionales, provinciales, municipales, etc.) -uno o más elementos, detalle opcional-
- **`AgregarRemito(nro_remito)`**: agrega un tributo (impuestos nacionales, provinciales, municipales, etc.) -uno o más elementos-
- **`AutorizarLiquidacion()`**: arma la liquidación, envía los datos a AFIP y devuelve `COE`, estableciendo los atributos con los campos de la respuesta.

Métodos adicionales de consulta:

- **`ConsultarLiquidacion(pto_vta, nro_cbte, cae, pdf):`**: Consulta una liquidación por No de comprobante o CAE (establece el resto de los atributos, similar a `AutorizarLiquidacion`). En `pdf` (indicar nombre de archivo para descargarlo de AFIP)
- **`ConsultarUltimoComprobante(tipo_cbte, pto_vta)`**: devuelve el último No de comprobante registrado por AFIP (atributo `NroComprobante`). 

## Atributos

- **`CAE`**
- **`NroComprobante`**
- **`FechaLiquidacion`**
- **`AlicuotaIVA`**, **`TotalNeto`**, **`ImporteIVA`**
- **`TotalBonificacionesCalidad`**, **`TotalPenalizacionesCalidad`**
- **`TotalBonificacionesComerciales`**, **`TotalDebitosComerciales`**
- **`TotalOtrosImpuestos`**, **`Total`**

## Herramienta por consola

La interfaz presenta una herramienta universal (multiplataforma -Linux / Windows / Mac- compatible con cualquier lenguaje de programación), que puede ser operado de manera automática en segundo plano (no requiere intervención del usuario).

El modo de uso es ejecutando el programa **`WSLUM_CLI.EXE`** con las siguientes opciones y archivos de intercambio.
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
- `--localidades`: obtiene el listado de localidades para una provincia 
- `--bonificaciones_penalidades`: obtiene el listado de tributos
- `--otros_impuestos`: obtiene el listado de los tributos
- `--puntosventa`: obtiene el listado de puntos de venta habilitados


Parámetros auxiliares:

- `--ayuda`: este mensaje
- `--debug`: modo depuración (detalla y confirma las operaciones)
- `--prueba`: genera y autoriza una LUM de prueba (no usar en producción!)
- `--xml`: almacena los requerimientos y respuestas XML (depuración)

### Ejemplo

Generar un LUM de prueba (no usar en producción):

```
C:\PYAFIPWS\> WSLUM_CLI.EXE --autorizar --prueba  --testing --guardar
Liquidacion: pto_vta=1 nro_cbte=1 tipo_cbte=27
Autorizando...
Errores: [u'2034: La cuit ingresada, no corresponde a un Operador Comercial.']
CAE 75521002437246
FechaComprobante 2015-12-31
NroComprobante 25
TotalNeto 1405.04
AlicuotaIVA 21.0
ImporteIVA 252.53
TotalBonificacionesCalidad 300.0
TotalPenalizacionesCalidad 200.0
TotalBonificacionesComerciales 302.5
TotalDebitosComerciales 200.0
TotalOtrosImpuestos 49.99
Total 1202.5
hecho.
```

### Archivo de Configuración

Para utilizar este webservice, debe tramitarse un certificado. Ver [Instructivo](wiki:ManualPyAfipWs#Certificados)

Luego, se debe configurar el Certificado, clave privada y URL en el archivo de configuración WSLUM.INI:

```
[WSAA]
CERT=reingart.crt
PRIVATEKEY=reingart.key
##URL=https://wsaa.afip.gov.ar/ws/services/LoginCms

[WSLUM]
CUIT=20267565393
ENTRADA=facturas.csv
SALIDA=salida.txt
##URL=https://serviciosjava.afip.gob.ar/wslum/LumService?wsdl
```

Para producción, se debe usar un instalador para tal fin y descomentar la URL (eliminando el numeral). 

El tipo de archivo de intercambio depende de la extensión configurada en WSLUM (usar .txt para texto, .csv para planillas CSV, .dbf para tablas DBF y .json para JavaScript)

## Archivo de Intercambio

La herramienta por consola podría soportar tanto:

- archivos de texto de ancho fijo (similares al usado por SIAP -COBOL-): ver [y [attachment:salida_wslum.txt](attachment:entrada_wslum.txt]) (muestras ejemplo)
- planillas CSV (archivo de texto valores separados por coma): ver [y [attachment:salida_wslum.csv](attachment:entrada_wslum.csv]) (muestras ejemplo WSLUMv1.2)
- tablas DBF (dBase, !FoxPro, Clipper, etc.): ver [wslum_dbf.zip](attachment:wslum_dbf.zip) (tablas de muestra WSLUMv1.2)
- archivo JSON (notación de objetos !JavaScript): : ver [attachment:salida_wslum.json] (muestras ejemplo WSLUMv1.2)


## Ejemplo Pseudocodigo

### Autorizar liquidación

Ejemplo de alta para generar y obtener CAE de una Liquidación única mensual de lechería:

```
#!python

# crear y completar internamente la estructura de la liq. a enviar a AFIP

wslum.CrearLiquidacion(tipo_cbte=27, pto_vta=8, nro_cbte=25, 
        fecha="2015-12-31", periodo="2015/12",
        iibb_adquirente="123456789012345", 
        domicilio_sede="Domicilio Administrativo",
        inscripcion_registro_publico="Nro IGJ", 
        datos_adicionales="Datos Adicionales Varios", 
        alicuota_iva=21.00)
wslum.AgregarCondicionVenta(codigo=1, descripcion=None)
if False:
    wslum.AgregarAjuste(cai="10000000000000", 
            tipo_cbte=0, pto_vta=0, nro_cbte=0, cae_a_ajustar=0)

wslum.AgregarTambero(cuit=11111111111, iibb="123456789012345")

wslum.AgregarTambo(nro_tambo_interno=123456789, 
        nro_renspa="12.345.6.78901/12",
        fecha_venc_cert_tuberculosis="2015-01-01", 
        fecha_venc_cert_brucelosis="2015-01-01",
        nro_tambo_provincial=100000000)
wslum.AgregarUbicacionTambo(
        latitud=-34.62987, longitud=-58.65155, 
        domicilio="Domicilio Tambo",
        cod_localidad=10109, cod_provincia=1, 
        codigo_postal=1234, 
        nombre_partido_depto='Partido Tambo')

wslum.AgregarBalanceLitrosPorcentajesSolidos(
        litros_remitidos=11000, litros_decomisados=1000, 
        kg_grasa=100.00, kg_proteina=100.00)

wslum.AgregarConceptosBasicosMercadoInterno(
        kg_produccion_gb=100, precio_por_kg_produccion_gb=5.00, 
        kg_produccion_pr=100, precio_por_kg_produccion_pr=5.00,
        kg_crecimiento_gb=0, precio_por_kg_crecimiento_gb=0.00,
        kg_crecimiento_pr=0, precio_por_kg_crecimiento_pr=0.00)

wslum.AgregarConceptosBasicosMercadoExterno(
        kg_produccion_gb=0, precio_por_kg_produccion_gb=0.00, 
        kg_produccion_pr=0, precio_por_kg_produccion_pr=0.00,
        kg_crecimiento_gb=0, precio_por_kg_crecimiento_gb=0.00,
        kg_crecimiento_pr=0, precio_por_kg_crecimiento_pr=0.00)

wslum.AgregarBonificacionPenalizacion(codigo=1,
        detalle="opcional", resultado="400", porcentaje=10.00)
wslum.AgregarBonificacionPenalizacion(codigo=10,
        detalle="opcional", resultado="2.5", porcentaje=10.00)
wslum.AgregarBonificacionPenalizacion(codigo=4,
        detalle="opcional", resultado="400", porcentaje=10.00)
wslum.AgregarBonificacionPenalizacion(codigo=1,
        detalle="opcional", resultado="En Saneamiento", 
        porcentaje=10.00)

wslum.AgregarOtroImpuesto(tipo=1, base_imponible=100.00, 
                          alicuota=10.00, detalle="")
wslum.AgregarOtroImpuesto(tipo=9, base_imponible=100.00, 
                          alicuota=10.00, 
                          detalle="Detalle Otras Percepciones")
wslum.AgregarOtroImpuesto(tipo=1, base_imponible=100.00, 
                          alicuota=10.00, detalle="")

wslum.AgregarRemito(nro_remito="123456789012")
wslum.AgregarRemito(nro_remito="123456789")

# llamar al webservice de AFIP para generar la liquidación:

ret = wslum.AutorizarLiquidacion()

if wslum.Excepcion:
    print "EXCEPCION:", wslum.Excepcion
    print  wslum.Traceback

# analizar los valores devueltos por AFIP:

print "Errores:", wslum.Errores
print "CAE", wslum.CAE
print "FechaComprobante", wslum.FechaComprobante
print "NroComprobante", wslum.NroComprobante
print "TotalNeto", wslum.TotalNeto
print "AlicuotaIVA", wslum.AlicuotaIVA
print "ImporteIVA", wslum.ImporteIVA
print "TotalBonificacionesCalidad", wslum.TotalBonificacionesCalidad
print "TotalPenalizacionesCalidad", wslum.TotalPenalizacionesCalidad
print "TotalBonificacionesComerciales", wslum.TotalBonificacionesComerciales
print "TotalDebitosComerciales", wslum.TotalDebitosComerciales
print "TotalOtrosImpuestos", wslum.TotalOtrosImpuestos
print "Total", wslum.Total

# 
pdf = wslum.GetParametro("pdf")

```

Ver ejemplo completo para Visual Basic o similar en: [wslum.bas](https://github.com/reingart/pyafipws/blob/master/ejemplos/wslum/wslum.bas) (adaptable a otros lenguajes como Visual Fox Pro, Delphi, etc. -ver otros webservices o consultar-)

## Liquidación PDF

La interfaz permite obtener los archivos que devuelve AFIP mediante este webservice:
 
- [attachment:wslum.pdf]: Liquidación Unica de Lecheria en documento PDF

En ambos casos, AFIP devuelve el archivo binario ya generado, por lo que se debe especificar una ruta completa para almacenarlo.
Necesita Acrobat Reader, Microsoft Office / Libre Office o similares para poder abrir los documentos.

## Tablas de Parámetros

En este nuevo servicio web WSLUM utiliza tablas dinámicas para los siguientes datos:

- Provincias y Localidades
- Tipos de Comprobante
- Puntos de venta
- Condiciones de venta
- Bonificaciones y Penalizaciones
- Otros Impuestos


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

### Tipos de Comprobante

|| 7 || Liquidación Única – Comercial Impositiva Clase A 
|| 28 || Liquidación Única – Comercial Impositiva Clase B
|| 29 || Liquidación Única – Comercial Impositiva Clase C
|| 43 || Nota de Crédito – Liquidación Única – Comercial Impositiva Clase B 
|| 44 || Nota de Crédito – Liquidación Única – Comercial Impositiva Clase C 
|| 45 || Nota de Débito – Liquidación Única – Comercial Imposiva Clase A
|| 46 || Nota de Débito – Liquidación Única – Comercial Imposiva Clase B 
|| 47 || Nota de Débito – Liquidación Única – Comercial Imposiva Clase C
|| 48 || Nota de Crédito – Liquidación Única – Comercial Impositiva Clase A

### Condiciones Venta

| Código | Descripción |
|---|---|
| 0 |  |
| 1 |  |
| 2 |  |
| 3 |  |

### Otros Impuestos

| Código | Descripción |
|---|---|
| 1 | Impuestos Nacionales |
| 2 | Impuestos Provinciales |
| 3 | Impuestos Municipales |
| 4 | Impuestos Internos |
| 5 | IIBB |
| 6 | Percepción de IVA |
| 7 | Percepción de IIBB |
| 8 | Percepción Impuestos Municipales |
| 9 | Otras Percepciones |
| 10 | Otros |


### Bonificaciones Penalizaciones

| Código | Tipo | Subtipo | Código | Valor | Signo |
|---|---|---|---|---|---|
| BC | Bonificación Calidad | Resultado Recuento Células Somáticas (RCS/ml/miles) | 1 | N3 | + |
| BC | Bonificación Calidad | Resultado Recuento Unidades Formadoras de Colonias (UFC/ml/miles) | 2 | N3 | + |
| BC | Bonificación Calidad | Resultado BRUCELOSIS | 3 | LIBRE | + |
| BC | Bonificación Calidad | Resultado TUBERCULOSIS | 4 | LIBRE | + |
| BC | Bonificación Calidad | Resultado TEMPERATURA (ºC) | 5 | TEMP | + |
| BC | Bonificación Calidad | Resultado Crioscopía (°C) | 6 | CRIO | - |
| BM | Bonificación Comercial | Buenas prácticas de manejo de tambos | 21 | NC | + |
| BM | Bonificación Comercial | Certificado UE (Unión Europea) | 22 | NC | + |
| BM | Bonificación Comercial | Confección de silaje y siembra de pasturas | 23 | NC | + |
| BM | Bonificación Comercial | Ayuda Forraje | 24 | NC | + |
| BM | Bonificación Comercial | Tambo en saneamiento | 25 | NC | + |
| BM | Bonificación Comercial | Libre Otras enfermedades | 26 | NC | + |
| BM | Bonificación Comercial | Volumen | 20 | NC | + |
| BM | Bonificación Comercial | Crecimiento | 27 | NC | + |
| BM | Bonificación Comercial | Crecimiento Interanual | 28 | NC | + |
| BM | Bonificación Comercial | Crecimiento con mes anterior | 29 | NC | + |
| BM | Bonificación Comercial | Adicional leche plus | 30 | NC | + |
| BM | Bonificación Comercial | Volumen unificado | 31 | NC | + |
| BM | Bonificación Comercial | Bonificación especial | 32 | NC | + |
| BM | Bonificación Comercial | Bonificación compensatoria | 33 | NC | + |
| BM | Bonificación Comercial | Permanencia | 34 | NC | + |
| BM | Bonificación Comercial | Antigüedad (tiempo de relación comercial) | 35 | NC | + |
| BM | Bonificación Comercial | Región | 36 | NC | + |
| BM | Bonificación Comercial | Cercanía (distancia a planta) | 37 | NC | + |
| BM | Bonificación Comercial | Sistema de Aseguramiento de la Calidad | 38 | NC | + |
| BM | Bonificación Comercial | Premio por tecnología aplicada a la calidad | 39 | NC | + |
| BM | Bonificación Comercial | Certificación de Buenas Prácticas de Manejo agrícola (Aseguramiento de Calidad) | 40 | NC | + |
| BM | Bonificación Comercial | Otros | 41 | TXT | + |
| DC | Débito Comercial | Débito Comercial | 50 | TXT | - |
| DC | Débito Comercial | Otros | 51 | TXT | - |
| PC | Penalización Calidad | Resultado Recuento Células Somáticas (RCS/ml/miles) | 10 | N3 | - |
| PC | Penalización Calidad | Resultado Recuento Unidades Formadoras de Colonias (UFC/ml/miles) | 11 | N3 | - |
| PC | Penalización Calidad | Resultado Crioscopía (°C) | 12 | CRIO | - |
| PC | Penalización Calidad | Resultado BRUCELOSIS | 13 | NOLIB | - |
| PC | Penalización Calidad | Resultado TUBERCULOSIS | 14 | NOLIB | - |
| PC | Penalización Calidad | Resultado TEMPERATURA (ºC) | 15 | TEMP | - |
| PC | Penalización Calidad | Inhibidores | 52 | TXT | - |


## Novedades

Historial de Cambios:

- Noviembre 2016 (actualización 01): versión inicial

Se recuerda que esta disponible el 
[grupo de noticias](http://www.pyafipws.com.ar) (http://groups.google.com.ar/group/pyafipws) donde
se publicarán futuras novedades sobre PyAfipWS: servicios web de
factura electrónica y sus interfases (se recomienda suscribirse)

## Costos y Condiciones

Debido a la complejidad de este servicio, su fecha de aplicación y las modificaciones que pudieran surgir, los clientes que asi lo requieran pueden adquirir horas de soporte técnico comercial (ver [Condiciones del Soporte Comercial](wiki:PyAfipWs#CostosyCondiciones)).

A su vez, se libera el código fuente bajo licencia GPL (software libre), al igual que se hizo con el restos de los servicios web. Para más detalles ver página FacturaElectronica.

MarianoReingart
