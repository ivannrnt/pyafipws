# Liquidación Electrónica Sector 

Web Services – (Servicios Web)  Liquidación Única Sector Pecuario. Generación de una liquidación mensual única (hacienda/compra directa/carne) y obtención del CAE (Código de Autorización Electrónico). 

Resolución General AFIP N° 3964/2016. Registro Fiscal de Operadores de la Cadena de Producción y Comercialización de Haciendas y Carnes Bovinas y Bubalinas (RFOCB). “Liquidación de Compra - Venta Primaria para el Sector Pecuario” a través de consignatarios. “Liquidación de Compra Directa”. “Liquidación de Venta Directa”. Resolución General N° 3.873, su modificatoria y su complementaria. Norma complementaria. Resolución General N° 1.415, sus modificatorias y complementarias. Norma modificatoria.

Resolución General AFIP N° 3873/2016. Impuesto al Valor Agregado. "Sistema Registral". "Registro Fiscal de Operadores de la Cadena de Producción y Comercialización de Haciendas y Carnes Bovinas y Bubalinas". "RFOCB". Regímenes de percepción, pagos a cuenta y retención. Resolución General Nº 4.059 (DGI), sus modificatorias y complementarias. 


## Descripción General

EL WSLSP (Web Service de Liquidación única Sector Pecuario) es un nuevo Servicio Web de la AFIP según [WSLSPv1.4.1](#wslspv141)
El webservice permite:

- Generación de una liquidación sector pecuario y obtención del CAE (Código de Autorización Electrónico).
- Consultas:
- Liquidaciones por CAE y número de comprobante.
- Último número de comprobante por punto de venta.
- Ajuste de liquidación (físico, monetario y financiero)
- Tablas de parámetros:
- Listado de provincias y localidades
- Tipos de comprobantes y liquidaciones.
- Operaciones permitidas, carácter emisor/receptor, categorías, motivos, razas, cortes, gastos y tributos.
- Gastos y tributos.

Para mayor información, se puede consultar la documentación orignal en [Micrositio Webservices - AFIP](http://www.afip.gov.ar/ws) o el [manual](../documentacion_herramientas/manualpyafipws.md) de la presente interfaz. 

URL:

- https://fwshomo.afip.gov.ar/wslsp/LspService?wsdl (homologación: testing/pruebas)
- https://serviciosjava.afip.gob.ar/wslsp/LspService?wsdl (producción)

### WSLSPv1.2

- Cambios a [Ajustes de Liquidación](#ajuste-liquidacion) (entrada en funcionamiento)
- Se modificó el envío y recepción de la información de la raza.
- Se agregó el importe de precio recupero, numero_item (ver [métodos](#metodos))

Para más información ver [Especificación Técnica AFIP WSLSP Versión 1.2](http://www.afip.gov.ar/ws/WSLSP/manual_wslsp_1.2.pdf) del 22/02/2017

### WSLSPv1.3

- Código de barras: Por cuestiones de compatibilidad AFIP ya no retornará valor en el campo !NroCodigoBarras, se reserva para uso futuro.

Para más información ver [Especificación Técnica AFIP WSLSP Versión 1.3](http://www.afip.gov.ar/ws/WSLSP/manual_wslsp_1.3.pdf) del 10/04/2017

### WSLSPv1.4.1

- Se agrega tipo_iva_nulo a [AgregarGasto](#metodos), valores permitidos (sí alicuota_iva = 0 o nulo) 
- "NG": No Gravado
- "NA": No Alcanzado
- "EX": Exento
- Se actualiza tabla de parámetros de [Categorías](#categorias)

Para más información ver [Especificación Técnica AFIP WSLSP Versión 1.4.1](http://www.afip.gov.ar/ws/WSLSP/manual_wslsp_1.4.1.pdf) del 30/06/2017

### WSLSPv1.7
 
- Se amplían campos, agrega validaciones y modifica los anexos (funcionalidades)
- Modificaciones en las consultas de tablas auxiliares de parámetros
- Se actualiza tabla de parámetros de [Categorías](#categorias), [Operaciones](#operaciones), [Caracteres](#caracteres), [Razas](#razas), [Cortes](#cortes), [Tributos](#tributos)

Para más información ver [Especificación Técnica AFIP WSLSP Versión 1.7](http://www.afip.gob.ar/ws/WSLSP/manual_wslsp_1.7.pdf) del 25/05/2018

### Datos de Prueba

Según documentación de AFIP:

  ''Con el objeto de facilitar las pruebas a realizar por los contribuyentes, se han 
  creado las siguientes CUITs genéricas, a los fines que puedan ser utilizadas
  exclusivamente en el rol de Receptores.
  Asímismo, las validaciones correspondientes a los roles emisores, no serán
  efectuadas en el ambiente de testing/homologación.''

| **CUIT** | **Denominación** | **Carácter** | **Impuesto** | **CUIT Autorizado** |
|---|---|---|---|---|
| 20160000024 | Productor/criador | 1 | IVA |  |
| 20160000032 | Productor/criador | 1 | EXENTO |  |
| 20160000067 | Productor/criador | 1 | MONOTRIBUTO |  |
| 20160000083 | Feed lots | 2 | IVA |  |
| 20160000105 | Feed lots | 2 | EXENTO |  |
| 20160000113 | Feed lots | 2 | MONOTRIBUTO |  |
| 20160000121 | Invernador | 3 | IVA |  |
| 23160000139 | Invernador | 3 | EXENTO |  |
| 20160000148 | Invernador | 3 | MONOTRIBUTO |  |
| 30160000011 | Establecimientos faenadores y/o frigorífico | 4 | IVA | 20160000261 |
| 20160000156 | Establecimientos faenadores y/o frigorífico | 4 | EXENTO | 20160000326 |
| 20160000180 | Establecimientos faenadores y/o frigorífico | 4 | MONOTRIBUTO | 23160000279 |
| 20160000199 | Matarifes abastecedores y carniceros y otros usuarios de faena | 9 | IVA | 20160000261 |
| 20160000210 | Matarifes abastecedores y carniceros y otros usuarios de faena | 9 | EXENTO | 20160000326 |
| 20160000253 | Matarifes abastecedores y carniceros y otros usuarios de faena | 9 | MONOTRIBUTO | 23160000279 |
| 20170000022 | Productor RIVA sin CBU con Registro | 1 | IVA |  |
| 20170000030 | Productor RIVA con CBU con Registro | 1 | IVA |  |
| 20170000065 | Productor RIVA con CBU sin Registro |  |  |  |
| 20170000138 | Matarife RIVA sin CBU con Registro | 4 | IVA |  |
| 20170000189 | Matarife RIVA con CBU con Registro | 4 | IVA |  |
| 20170000197 | Matarife RIVA con CBU sin Registro |  | IVA |  |

Los CUITs autorizados para los caracteres 4 y 9 son:

| **CUIT** | **Denominación** |
|---|---|
| 20160000261 | CUIT PARA AUTORIZADOS |
| 20160000326 | CUIT PARA AUTORIZADOS |
| 23160000279 | CUIT PARA AUTORIZADOS |

Los CUITs – N° RUCA para receptores caracteres 4 y 9 son:

| **CUIT** | **Denominación** | **N° de RUCA** |
|---|---|---|
| 30160000011 | Establecimientos faenadores y/o frigorífico | 1011 |
| 20160000156 | Establecimientos faenadores y/o frigorífico | 1156 |
| 20160000180 | Establecimientos faenadores y/o frigorífico | 1180 |
| 20160000199 | Matarifes abastecedores y carniceros y otros usuarios de faena | 1199 |
| 20160000210 | Matarifes abastecedores y carniceros y otros usuarios de faena | 1210 |
| 20160000253 | Matarifes abastecedores y carniceros y otros usuarios de faena | 1253 |
| 20160000083 | Feed lots | 1083 |
| 20160000105 | Feed lots | 1105 |
| 20160000113 | Feed lots | 1113 |
| 20170000138 | Matarife RIVA sin CBU con Registro | 1138 |
| 20170000189 | Matarife RIVA con CBU con Registro | 1189 |
| 20170000197 | Matarife RIVA con CBU sin Registro | 1197 |

Números de Planta Frigorífico:

| **CUIT** | **Nro Planta** |
|---|---|
| 30160000011 | 1 |
| 20160000156 | 1 |
| 20160000199 | 1 |

## Descargas

- Instalador: [PyAfipWs-2.7.1982-32bit+wsaa_2.11c+wslsp_1.06a-homo.exe](https://www.sistemasagiles.com.ar/soft/pyafipws/PyAfipWs-2.7.1982-32bit+wsaa_2.11c+wslsp_1.06a-homo.exe) (versión actualizada para WSLSPv1.4.1)
- Documentación: [Documento Oficial WSLSPv1.4.1](http://www.afip.gov.ar/ws/WSLSP/manual_wslsp_1.4.1.pdf) (AFIP), [Manual de Uso General](../documentacion_herramientas/manualpyafipws.md) ([PDF](http://www.sistemasagiles.com.ar/trac/wiki/ManualPyAfipWs?format=pdf))
- Ejemplo en VB: [wslsp.bas](https://github.com/reingart/pyafipws/blob/master/ejemplos/wslsp/wslsp.bas) *(actualizado)*
- Archivos de intercambio (muestras): 
- Liquidación (texto plano JSON): [[attachment:wslsp_salida.json](attachment:wslsp_entrada.json])
- Ajuste (texto plano JSON): [[attachment:wslsp_ajuste_salida.json](attachment:wslsp_ajuste_entrada.json])
- Código Fuente (Python): [wslsp.py](https://github.com/reingart/pyafipws/blob/master/wslsp.py)

## Metodos

- **`Conectar(cache=None, url="", proxy="")`**: en homologación no hace falta pasarle ningún parámetro. En producción, el segudo parametro es la WSDL.
- **`Dummy()`**: devuelve estado de servidores

Métodos para generar una liquidación de tabaco verde (LUM):

- **`CrearLiquidacion(cod_operacion, fecha_cbte, fecha_op, cod_motivo, cod_localidad_procedencia, cod_provincia_procedencia, cod_localidad_destino, cod_provincia_destino, lugar_realizacion, fecha_recepcion, fecha_faena, datos_adicionales)`**: crea una liquidación  a autorizar, inicializando los datos de cabecera (fecha_recepcion a datos_adicionales son opcionales.
- **`AgregarFrigorifico(cuit, nro_planta)`**: agrega Agrego el frigorifico a la liquidacíon (opcional).
- **`AgregarEmisor(tipo_cbte, pto_vta, nro_cbte, cod_caracter, fecha_inicio_act, iibb, nro_ruca, nro_renspa, cuit_autorizado)`**: agrega los datos del emisor (cuit_autorizado, iibb, ruca y renspa es opcional)
- **`AgregarReceptor(cod_caracter)`**: agrega los datos del receptor
- **`AgregarOperador(cuit, iibb, nro_ruca, nro_renspa, cuit_autorizado)`**: agrega los datos del operador (iibb, ruca, renspa y cuit autorizado es opcional)
- **`AgregarItemDetalle(cuit_cliente, cod_categoria, tipo_liquidacion, cantidad, precio_unitario, alicuota_iva, cod_raza, cantidad_cabezas, nro_tropa, cod_corte, cantidad_kg_vivo, precio_recupero, detalle_raza,nro_item)`**: agrega el detalle de item de la liquidación (desde cantidad_cabezas son parámetros opcionales, detalle_raza y nro_item agregado en [WSLSPv1.2](#wslspv12))
- **`AgregarCompraAsociada(tipo_cbte, pto_vta, nro_cbte, cant_asoc, nro_item)`**: agrega la información referente a la liquidación compra asociada (para cada item); nro_item agregado en [WSLSPv1.2](#wslspv12)
- **`AgregarGasto(cod_gasto, descripcion, base_imponible, alicuota, importe, alicuota_iva,tipo_iva_nulo)`**: agrega uno o más gastos (sólo cod_gasto es obligatorio, pasar null en los parametros que no correspondan). Si alicuota_iva=0, se debe indicar tipo_iva_nulo ([WSLSPv1.4](#wslspv141))
- **`AgregarTributo(cod_tributo, descripcion, base_imponible, alicuota, importe)`**: agrega a información referente a los tributos de la liquidación (sólo cod_tributo es obligatorio)
- **`AgregarDTE(nro_dte, nro_renspa)`**: agrega un DTE -uno o más elementos, detalle opcional-
- **`AgregarGuia(nro_remito)`**: agrega una guia -uno o más elementos-
- **`AutorizarLiquidacion()`**: arma la liquidación, envía los datos a AFIP y devuelve `COE`, estableciendo los atributos con los campos de la respuesta.

Métodos específicos para Ajustes (agregado en WSLSPv1.2, desde actualización 1.04a):

- **`CrearAjuste(tipo_ajuste,  fecha_cbte)`**: crea un ajuste de liquidación a autorizar, inicializando los datos de cabecera; tipo_ajuste puede ser 'C' para créditos o 'D' para débitos.
- **`AgregarEmisor(tipo_cbte, pto_vta, nro_cbte)`**: agrega los datos del emisor (idem liquidación, cod_caracter y fecha_inicio son opcionales)
- **`AgregarComprobanteAAjustar(tipo_cbte, pto_vta, nro_cbte)`**: agrega los datos del comprobante original a ajustar
- **`AgregarItemDetalleAjuste(nro_item_ajustar)`**: agrega un detalle de item al ajuste de la liquidación
- **`AgregarCompraAsociada(tipo_cbte, pto_vta, nro_cbte, cant_asoc, nro_item)`**: agrega la información referente a la liquidación compra asociada (para cada item); nro_item agregado en WSLSPv1.2
- **`AgregarAjusteFisico(cantidad, cantidad_cabezas, cantidad_kg_vivo)`**: agrega los datos de ajuste que se realizan sobre las cantidades que se identificaron en la unidad de medida en el comprobante a ajustar (solo cantidad es oblogatorio)
- **`AgregarAjusteMonetario(precio_unitario, precio_recupero)`**: agrega los datos que afectan a los valores (precios) según sea el tipo de liquidación indicada en el comprobante a original; precio unitario obligatorio.
- **`AgregarAjusteFinanciero()`**: para ajustar, permite agregar Gastos y/o Tributos sobre el comprobante original a ajustar.
- **`AgregarGastos(cod_gasto, descripcion, base_imponible, alicuota, importe)`**: agrega uno o más gastos (sólo cod_gasto es obligatorio)
- **`AgregarTributo(cod_tributo, descripcion, base_imponible, alicuota, importe)`**: agrega a información referente a los tributos de la liquidación (sólo cod_tributo es obligatorio)
- **`AjustarLiquidacion()`**: arma el ajuste de liquidación, envía los datos a AFIP y devuelve `CAE`, estableciendo los atributos con los campos de la respuesta (similar a `AutorizarLiquidacion`, pero adicionalmente se completan los campos `tipo_ajuste`, `modo_ajuste` y `cbte_ajuste`).

Métodos adicionales de consulta:

- **`ConsultarLiquidacion(tipo_cbte, pto_vta, nro_cbte, cae, cuit_comprador, pdf):`**: Consulta una liquidación por No de comprobante o CAE (establece el resto de los atributos, similar a `AutorizarLiquidacion`). En `pdf` indicar nombre de archivo para descargarlo de AFIP.
- **`ConsultarUltimoComprobante(tipo_cbte, pto_vta)`**: devuelve el último No de comprobante registrado por AFIP (atributo `NroComprobante`). 

Métodos para obtención de tablas de parámetros:

- **`ConsultarOperaciones`**:
- **`ConsultarTiposComprobante`**:
- **`ConsultarTiposLiquidacion`**:
- **`ConsultarCategorias`**:
- **`ConsultarMotivos`**:
- **`ConsultarRazas`**:
- **`ConsultarCortes`**:
- **`ConsultarCaracteresParticipante`**:
- **`ConsultarGastos`**:
- **`ConsultarTributos`**:
- **`ConsultarPuntosVentas`**:
- **`ConsultarProvincias`**:
- **`ConsultarLocalidades`**:

a
## Atributos

- **`CAE`**
- **`NroComprobante`**
- **`FechaLiquidacion`**
- **`NroCodigoBarras`**, **`NroCodigoBarras`**, **`FechaProcesoAFIP`**
- **`ImporteBruto`**, **`ImporteIVASobreBruto`**
- **`ImporteTotalGastos`**, **`ImporteIVASobreGastos`**
- **`ImporteTotalTributos`**, **`ImporteTotalNeto`**
        
## Herramienta por consola

La interfaz presenta una herramienta universal (multiplataforma -Linux / Windows / Mac- compatible con cualquier lenguaje de programación), que puede ser operado de manera automática en segundo plano (no requiere intervención del usuario).

El modo de uso es ejecutando el programa **`WSLSP_CLI.EXE`** con las siguientes opciones y archivos de intercambio.
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
- `--operaciones`: obtiene el listado de operaciones permitidas
- `--tributos`: obtiene el listado de los tributos
- `--puntosventa`: obtiene el listado de puntos de venta habilitados


Parámetros auxiliares:

- `--ayuda`: este mensaje
- `--debug`: modo depuración (detalla y confirma las operaciones)
- `--prueba`: genera y autoriza una LUM de prueba (no usar en producción!)
- `--xml`: almacena los requerimientos y respuestas XML (depuración)

### Ejemplo

Generar una LSP de prueba (no usar en producción):

```
C:\PYAFIPWS\> WSLSP_CLI.EXE --autorizar --prueba  --testing --guardar
Liquidacion: pto_vta=1 nro_cbte=1 tipo_cbte=27
Autorizando...
Errores: [u'2100: Receptor: CUIT invá1lida / inactiva. ']
CAE 96465021584954
NroCodigoBarras 12222222222018000300096465021584954201611229
FechaProcesoAFIP 2016-11-16
FechaComprobante 2016-11-12
NroComprobante 52
ImporteBruto 20.00
ImporteTotalNeto -13779.66
ImporteIVA Sobre Bruto 2.10
ImporteIVA Sobre Gastos 726.14
ImporteTotalNeto -13779.66

hecho.
```

### Archivo de Configuración

Para utilizar este webservice, debe tramitarse un certificado. Ver [Instructivo](../documentacion_herramientas/manualpyafipws.md#Certificados)

Luego, se debe configurar el Certificado, clave privada y URL en el archivo de configuración WSLSP.INI:

```
[WSAA]
CERT=reingart.crt
PRIVATEKEY=reingart.key
##URL=https://wsaa.afip.gov.ar/ws/services/LoginCms

[WSLSP]
CUIT=20267565393
ENTRADA=facturas.csv
SALIDA=salida.txt
##URL=https://serviciosjava.afip.gob.ar/wslsp/LumService?wsdl
```

Para producción, se debe usar un instalador para tal fin y descomentar la URL (eliminando el numeral). 

El tipo de archivo de intercambio depende de la extensión configurada en WSLSP (usar .txt para texto, .csv para planillas CSV, .dbf para tablas DBF y .json para JavaScript)

## Archivo de Intercambio

La herramienta por consola podría soportar tanto:

- archivos de texto de ancho fijo (similares al usado por SIAP -COBOL-): ver [y [attachment:salida_wslsp.txt](attachment:entrada_wslsp.txt]) (muestras ejemplo)
- planillas CSV (archivo de texto valores separados por coma): ver [y [attachment:salida_wslsp.csv](attachment:entrada_wslsp.csv]) (muestras ejemplo WSLSPv1.2)
- tablas DBF (dBase, !FoxPro, Clipper, etc.): ver [wslsp_dbf.zip](attachment:wslsp_dbf.zip) (tablas de muestra WSLSPv1.2)
- archivo JSON (notación de objetos !JavaScript): : ver [attachment:wslsp_entrada.json] (muestras ejemplo WSLSPv1.2)


## Ejemplo Pseudocodigo

Ver ejemplo completo para Visual Basic o similar en: [wslsp.bas](https://github.com/reingart/pyafipws/blob/master/ejemplos/wslsp/wslsp.bas) (adaptable a otros lenguajes como Visual Fox Pro, Delphi, etc. -ver otros webservices o consultar-)

### Cuenta de Venta y Líquido Producto - Hacienda

```
#!python

# crear y completar internamente la estructura de la liq. a enviar a AFIP

wslsp.CrearLiquidacion(
        cod_operacion=1, 
        fecha_cbte='2017-02-23', 
        fecha_op='2017-02-23', 
        cod_motivo=6, 
        cod_localidad_procedencia=8274, 
        cod_provincia_procedencia=1, 
        cod_localidad_destino=8274, 
        cod_provincia_destino=1,
        lugar_realizacion='CORONEL SUAREZ',
        fecha_recepcion=None, fecha_faena=None, 
        datos_adicionales=None)

if False:
    wslsp.AgregarFrigorifico(cuit=20160000156, nro_planta=1)

wslsp.AgregarEmisor(
        tipo_cbte=180, pto_vta=3000, nro_cbte=1, 
        cod_caracter=5, fecha_inicio_act='2016-01-01',
        iibb='123456789', nro_ruca=305, nro_renspa=None)

wslsp.AgregarReceptor(cod_caracter=3)
wslsp.AgregarOperador(cuit=30160000011, iibb=3456, 
                      ## nro_ruca=1011,  # Validacion AFIP 1003
                      ## cuit_autorizado=20160000261,   # 1001 
                      nro_renspa='22.123.1.12345/A4')
wslsp.AgregarItemDetalle(
        cuit_cliente="20160000199",     # 2403
        cod_categoria=51020102,
        tipo_liquidacion=1,
        cantidad=2,
        precio_unitario=10.0,
        alicuota_iva=10.5,
        cod_raza=1,
        #cantidad_cabezas=1,        # Validacion AFIP 2408
        )
wslsp.AgregarCompraAsociada(tipo_cbte=185, pto_vta=3000, nro_cbte=33, cant_asoc=2, nro_item=1)

wslsp.AgregarGuia(nro_guia=1)

wslsp.AgregarDTE(nro_dte="418-1", nro_renspa='22.123.1.12345/A5')
wslsp.AgregarDTE(nro_dte="418-2", nro_renspa='22.123.1.12346/A5')

wslsp.AgregarGasto(cod_gasto=16, base_imponible=230520.60, alicuota=3, alicuota_iva=10.5)

wslsp.AgregarTributo(cod_tributo=5, base_imponible=230520.60, alicuota=2.5)
wslsp.AgregarTributo(cod_tributo=3, importe=397)

# llamar al webservice de AFIP para generar la liquidación:

ret = wslsp.AutorizarLiquidacion()

# analizar los valores devueltos por AFIP:
                    
print "Errores:", wslsp.Errores

print "CAE", wslsp.CAE
print "FechaComprobante", wslsp.FechaComprobante
print "NroComprobante", wslsp.NroComprobante

print "ImporteBruto", wslsp.ImporteBruto
print "ImporteIVASobreBruto", wslsp.ImporteIVASobreBruto
print "ImporteTotalGastos", wslsp.ImporteTotalGastos
print "ImporteIVASobreGastos", wslsp.ImporteIVASobreGastos
print "ImporteTotalTributos", wslsp.ImporteTotalTributos
print "ImporteTotalNeto", wslsp.ImporteTotalNeto

print wslsp.NroCodigoBarras
print wslsp.FechaProcesoAFIP

```

Ver Liquidación Sector Pecuario devuelta por AFIP para este ejemplo: [attachment:wslsp_liq.pdf]
### Ajuste Liquidacion

Ejemplo de alta para generar y obtener CAE de un Ajuste (físico, monetario y financiero, tanto débito como crédito) de una Liquidación de Sector Pecuario:

```
#!python

wslsp.CrearAjuste(tipo_ajuste="C", fecha_cbte="2017-01-06", 
                  datos_adicionales="Ajuste sobre liquidacion de compra directa"'
                 )
wslsp.AgregarEmisor(tipo_cbte=186, pto_vta=3000, nro_cbte=1)
wslsp.AgregarComprobanteAAjustar(tipo_cbte=186, pto_vta=2000, nro_cbte=4)

# Repetir por cada item a ajustar, indicando comprobante original:
wslsp.AgregarItemDetalleAjuste(nro_item_ajustar=1)
wslsp.AgregarCompraAsociada(tipo_cbte=185, pto_vta=3000,
                            nro_cbte=33, cant_asoc=2, 
                            nro_item=1)

# NOTA: según Validación de AFIP 3002 se debe elegir un modo:
# "No se pueden realizar ajustes físicos y monetario en un mismo comprobante."
wslsp.AgregarAjusteFisico(   
        cantidad=1,
        cantidad_cabezas=None,        # opcional
        cantidad_kg_vivo=None,        # opcional
        )
wslsp.AgregarAjusteMonetario(
        precio_unitario=15.995,
        precio_recupero=None,        # opcional
        )

# preparar gastos/tributos (generales del ajuste):
wslsp.AgregarAjusteFinanciero()
wslsp.AgregarGasto(cod_gasto=16, base_imponible=230520.60,
                   alicuota=3, alicuota_iva=10.5)
wslsp.AgregarTributo(cod_tributo=5, base_imponible=230520.60,
                     alicuota=2.5)
wslsp.AgregarTributo(cod_tributo=3, importe=397)

# llamar al webservice para obtener CAE:
wslsp.AjustarLiquidacion()
print "CAE:", wslsp.CAE
print "Tipo Ajuste:", wslsp.GetParametro("tipo_ajuste")
print "Modo Ajuste:", wslsp.GetParametro("modo_ajuste")

# comprobaciones de ejemplo para campos de la respuesta:
assert wslsp.GetParametro("cae") == "97029023118043"
assert wslsp.GetParametro("cbte_ajuste", "tipo_cbte") == '186'
assert wslsp.GetParametro("cbte_ajuste", "pto_vta") == '2000'
assert wslsp.GetParametro("cbte_ajuste", "nro_cbte") == '3'

# guardo el pdf obtenido (abrir el archivo en modo binario)
pdf = wslsp.GetParametro("pdf")
if pdf:
    open("liq.pdf", "wb").write(pdf)

```


## Tablas de Parámetros

En este nuevo servicio web WSLSP utiliza tablas dinámicas para los siguientes datos:

- Provincias y Localidades
- Puntos de venta
- Tipos de comprobantes y liquidaciones.
- Operaciones permitidas, carácter emisor/receptor, categorías, motivos, razas, cortes, gastos y tributos.
- Gastos y tributos.

La interfaz permite obtener los diversos códigos de parámetros a utilizar. A continuación se detallan a modo de ejemplo:

### Provincias

| **Código** | **Descripción** |
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

### Operaciones

| **Código** | **Descripción** |
|---|---|
| 1 | Cuenta de Venta y Líquido Producto - Hacienda |
| 2 | Cuenta de Venta y Líquido Producto - Directo |
| 3 | Cuenta de Venta y Líquido Producto - Carne |
| 4 | Liquidación de compra |
| 5 | Liquidación Compra Directa |
| 6 | Liquidación de venta directa |
| 101 | Cuenta de Venta y Líquido Producto - Hacienda - Porcinos |
| 102 | Cuenta de Venta y Líquido Producto - Directo - Porcinos |
| 103 | Cuenta de Venta y Líquido Producto - Carne - Porcinos |
| 104 | Liquidación de compra - Porcinos |
| 105 | Liquidación Compra Directa - Porcinos |
| 106 | Liquidación de venta directa - Porcinos |

### Tipos de Comprobantes

| **Código** | **Descripción** |
|---|---|
| 180 | Cuenta de Venta y Líquido Producto A - Sector Pecuario |
| 182 | Cuenta de Venta y Líquido Producto B - Sector Pecuario |
| 183 | Liquidación de Compra A - Sector Pecuario |
| 185 | Liquidación de Compra B - Sector Pecuario |
| 186 | Liquidación de Compra Directa A - Sector Pecuario |
| 188 | Liquidación de Compra Directa B - Sector Pecuario |
| 189 | Liquidación de Compra Directa C - Sector Pecuario |
| 191 | Liquidación de Venta  Directa B - Sector Pecuario |

**NOTA:** este valor correspondería al parámetro `tipo_cbte`

### Tipos de Liquidación

| **Código** | **Descripción** |
|---|---|
| 1 | Por Cabeza |
| 2 | Por Kilo vivo |
| 3 | Por Kilo de carne |
| 5 | Por Corte |

### Caracteres Participante Emisor/Receptor

| **Código** | **Descripción** |
|---|---|
| 1 | Productor/criador |
| 2 | Feed lots |
| 3 | Invernador |
| 4 | Establecimiento faenador y/o frigorífico |
| 5 | Consignatario y/o comisionista |
| 6 | Consignatario directo |
| 7 | Consignatario de Carnes |
| 9 | Matarife abastecedor y carnicero y usuario de faena |
| 100 | Productores/Criadores Comerciales - Porcinos |
| 101 | Invernadores - Porcinos |
| 102 | Matadero - Frigorífico - Porcinos |
| 103 | Matarifes abastecedores y carniceros y usuarios de faena porcina - Porcinos |
| 104 | Consignatarios y/o comisionistas de hacienda - Porcinos |
| 105 | Consignatarios directos - Porcinos |
| 106 | Consignatario y/o comisionistas de Carnes - Porcinos |


### Categorías

**IMPORTANTE**: actualizado WSLSPv1.4 (22/06/2017)

| **Código** | **Descripción** |
|---|---|
| 5108 | Bovino Bueyes |
| 510901 | Bovino Machos Enteros Especiales y Buenos |
| 510902 | Bovino Machos Enteros Regulares |
| 51030101 | Bovino Novillitos Especiales y Buenos Medianos 351/390 kilos |
| 51030102 | Bovino Novillitos Especiales y Buenos Pesados 391/430 kilos |
| 510302 | Bovino Novillitos Regulares |
| 51040401 | Bovino Novillos Cruza Cebú hasta 440 kilos |
| 51040402 | Bovino Novillos Cruza Cebú más 440 kilos |
| 51040501 | Bovino Novillos Cruza Europea hasta 470 kilos |
| 51040502 | Bovino Novillos Cruza Europea más 470 kilos |
| 51040101 | Bovino Novillos Especiales y Buenos 431/460 kilos |
| 51040102 | Bovino Novillos Especiales y Buenos 461/490 kilos |
| 51040103 | Bovino Novillos Especiales y Buenos 491/520 kilos |
| 51040104 | Bovino Novillos Especiales y Buenos más 520 kilos |
| 510403 | Bovino Novillos Overos Negros más de 500 kilos |
| 51040201 | Bovino Novillos Regulares livianos |
| 51040202 | Bovino Novillos Regulares pesados |
| 5106 | Bovino Terneras hasta 350 kilos |
| 5105 | Bovino Terneros hasta 350 kilos |
| 510701 | Bovino Toros Buenos |
| 510702 | Bovino Toros Regulares |
| 510101 | Bovino Vaca Buenas |
| 510103 | Bovino Vaca Conserva Buena |
| 510104 | Bovino Vaca Conserva Inferior |
| 510102 | Bovino Vaca Regulares |
| 510106 | Bovino Vaca con ternero al pie |
| 510105 | Bovino Vaca preñada |
| 51020101 | Bovino Vaquillona Especiales y Buenas Medianas 351/390 kilos |
| 51020102 | Bovino Vaquillona Especiales y Buenas Pesadas 391/430 kilos |
| 510202 | Bovino Vaquillona Regulares |
| 510203 | Bovino Vaquillona preñada |
| 1208 | Bubalino Bueyes |
| 1204 | Bubalino Novillito |
| 1203 | Bubalino Novillo |
| 1206 | Bubalino Ternera |
| 1205 | Bubalino Ternero |
| 1209 | Bubalino Torito |
| 1207 | Bubalino Toro |
| 1201 | Bubalino Vaca |
| 1202 | Bubalino Vaquillona |
| 520301 | Porcina Padrillo |
| 520302 | Porcina Cerda / Chancha |
| 52030301 | Porcina Lechones Livianos |
| 52030302 | Porcina Lechones Pesados Y Cachorros Parrilleros |
| 520304 | Porcina Capón |
| 520305 | Porcina Cachorro |
| 520306 | Porcina Machos Enteros Inmunocastrados |
| 520307 | Porcina Cachorra |

### Motivos

| **Código** | **Descripción** |
|---|---|
| 1 | FAENA |
| 2 | INVERNADA |
| 3 | REPRODUCCION |
| 4 | CRIA |
| 5 | REMATE DE CARNE |
| 6 | FAENA Y VENTA DE CARNE POR CUENTA Y ORDEN |

### Razas

| **Código** | **Descripción** |
|---|---|
| 1 | Aberdeen Angus |
| 2 | Belted Galloway |
| 3 | Blonde d'aquitaine |
| 4 | Bobino Criollo |
| 5 | Braford |
| 6 | Brahman |
| 7 | Grangus |
| 8 | Charolais |
| 9 | Hereford |
| 10 | Holando Argentino |
| 11 | Jersey |
| 12 | Limangus |
| 13 | Limuosin |
| 14 | Piemontese |
| 15 | Polled Hereford |
| 16 | Retinta |
| 17 | Santa Gertrudis |
| 18 | Shorthorn |
| 19 | Flieckvieh Simmental |
| 20 | West Highland |
| 5201 | YORKSHIRE / LARGE-WHITE |
| 5202 | LANDRACE (DANÉS) |
| 5203 | LANDRACE (BELGA) |
| 5204 | PIETRAIN |
| 5205 | DUROC HERSEY |
| 5206 | HAMPSHIRE |
| 5207 | LÍNEA HÍBRIDA MATERNA |
| 5208 | LÍNEA HÍBRIDA PATERNA |
| 5299 | OTRAS PURO o CRUZA (Detalle) |
| 5221 | XD - Decomisado |
| 5222 | XZ - Golpeado |
| 5223 | Caídos |

### Cortes

| **Código** | **Descripción** |
|---|---|
| 1 | BIFE ANGOSTO CON/SIN CORDON (SIN HUESO) |
| 2 | CUADRIL C/TAPA (S/HUESO Y S/COLITA) |
| 3 | CORAZON DE CUADRIL |
| 4 | LOMITO DE CORAZON DE CUADRIL |
| 5 | COLITA DE CUADRIL |
| 6 | LOMO CON O SIN CORDON |
| 7 | NALGA DE AFUERA |
| 8 | PECETO |
| 9 | CUADRADA (CARNAZA DE COLA) |
| 10 | NALGA DE ADENTRO-NALGA CON TAPA |
| 11 | NALGA DE ADENTRO SIN TAPA |
| 12 | TAPA DE NALGA DE ADENTRO |
| 13 | BOLA DE LOMO |
| 14 | TORTUGUITA (PALOMITA) |
| 15 | GARRON (SIN HUESO) |
| 16 | BIFE ANCHO CON TAPA (SIN HUESO) |
| 17 | BIFE ANCHO SIN TAPA |
| 18 | OJO DE BIFE ANCHO |
| 19 | TAPA DE BIFE ANCHO |
| 20 | PALETA (CARNAZA DE PALETA) |
| 21 | CENTRO DE CARNAZA DE PALETA |
| 22 | AGUJA SIN HUESO |
| 23 | AGUJA SIN TAPA |
| 24 | TAPA DE AGUJA |
| 25 | COGOTE |
| 26 | MARUCHA |
| 27 | CHINGOLO |
| 28 | BRAZUELO SIN HUESO |
| 29 | PECHO |
| 30 | FALDA SIN HUESO |
| 31 | ASADO SIN HUESO |
| 32 | VACIO |
| 33 | BIFE DE VACIO |
| 34 | ENTRAÑA FINA |
| 35 | MATAMBRE |
| 36 | AZOTILLO |
| 37 | BIFE ANGOSTO CON/SIN CORDON (CON HUESO) |
| 38 | GARRON (CON HUESO) |
| 39 | BIFE ANCHO CON TAPA (CON HUESO) |
| 40 | AGUJA CON HUESO |
| 41 | BRAZUELO (CON HUESO) |
| 42 | FALDA CON HUESO |
| 43 | ASADO CON HUESO |
| 44 | TENDONES O NERVIOS |
| 45 | CUERO |
| 46 | CERDA DE COLA |
| 47 | CERDA DE OREJA |
| 48 | HUESO DE PATAS |
| 49 | HUESO DE MANOS |
| 50 | ASTAS |
| 51 | MACHOS DE ASTAS |
| 52 | PEZUÑAS |
| 53 | SANGRE |
| 54 | HIEL |
| 55 | SARRO |
| 56 | HUESO DE CABEZA |
| 57 | HUESO DE MAXILAR |
| 58 | TAPA DE ASADO |
| 59 | HIPOFISIS |
| 60 | PINEAL |
| 61 | HIPOTALAMO |
| 62 | PARATIROIDES |
| 63 | TIROIDES |
| 64 | SUPRARRENALES |
| 65 | EPITELIO |
| 66 | PANCREAS |
| 67 | PROSTATA |
| 68 | LENGUA CON EPITELIO |
| 69 | SESOS |
| 70 | QUIJADAS |
| 71 | PULMON |
| 72 | CORAZON |
| 73 | MOLLEJA DE CORAZON |
| 74 | MOLLEJA DE COGOTE |
| 75 | HIGADO |
| 76 | RIÑONES |
| 77 | RABO-COLA |
| 78 | MEDULA |
| 79 | CARNE CHICA - NUEZ DE QUIJADA |
| 80 | CARNE CHICA - CARNE DE TRAGAPASTO |
| 81 | CARNE CHICA - CARNE DE CABEZA - LABIO |
| 82 | CARNE CHICA - CARNE DE TRAQUEA |
| 83 | PAJARILLA - BONETE |
| 84 | MONDONGO |
| 85 | LIBRILLO |
| 86 | CUAJO |
| 87 | CHINCHULINES |
| 88 | TRIPA GORDA |
| 89 | TRIPA ORILLA PRIMERA |
| 90 | TRIPA ORILLA SEGUNDA |
| 91 | TRIPON |
| 92 | TRIPA SALAME |
| 93 | VEJIGA |
| 94 | GRASA COMESTIBLE |
| 95 | GRASA INDUSTRIAL |
| 96 | MEDIA RES SIN HUESO |
| 97 | MEDIA RES CON HUESO |
| 98 | CUARTO DELANTERO SIN HUESO |
| 99 | CUARTO DELANTERO CON HUESO |
| 100 | CUARTO TRASERO SIN HUESO |
| 101 | CUARTO TRASERO CON HUESO |
| 102 | CORTE PISTOLA A 3 COSTILLAS SIN HUESO |
| 103 | CORTE PISTOLA A 3 COSTILLAS CON HUESO |
| 104 | CORTE PISTOLA A 7 COSTILLAS SIN HUESO |
| 105 | CORTE PISTOLA A 7 COSTILLAS CON HUESO |
| 106 | CUARTO DELANTERO SIN ASADO SIN HUESO |
| 107 | CUARTO DELANTERO SIN ASADO CON HUESO |
| 108 | PECHO A 3 COSTILLAS (S/HUESO) O EN MANTA |
| 109 | PECHO A 3 COSTILLAS (CON HUESO) |
| 110 | RUEDA (SIN HUESO) |
| 111 | RUEDA (CON HUESO) |
| 112 | RUEDA SIN GARRON (SIN HUESO) |
| 113 | RUEDA SIN GARRON (CON HUESO) |
| 114 | PIERNA SIN HUESO |
| 115 | PIERNA CON HUESO |
| 116 | PIERNA MOCHA SIN HUESO |
| 117 | PIERNA MOCHA CON HUESO |
| 118 | CUARTO DELANTERO EN MANTA |
| 119 | CUARTO TRASERO EN MANTA |
| 120 | ASADO CON VACIO SIN HUESO |
| 121 | ASADO CON VACIO CON HUESO |
| 122 | TAPA DE CUADRIL |
| 123 | CORCHO DE CUADRIL |
| 124 | PECHO CON FALDA SIN HUESO |
| 125 | PECHO CON FALDA CON HUESO |
| 126 | LENGUA SIN EPITELIO |
| 127 | JUEGOS (BIFE ANGOSTO-COR. DE CUADRIL-LOMO) |
| 128 | CENTRO DE NALGA DE ADENTRO |
| 129 | RECORTES (CARNE CHICA) |
| 130 | HUESOS DE LOS CORTES |
| 131 | CUADRIL CON TAPA Y CON COLITA |
| 132 | VACIO SIN BIFE |
| 133 | CUADRIL SIN TAPA, SIN COLITA Y SIN CORCHO |
| 134 | CUADRIL SIN TAPA Y SIN COLITA |
| 135 | CUADRIL SIN TAPA Y CON COLITA |
| 136 | CENTRO DE ENTRAÑA |
| 137 | ASADO A 3 COSTILLAS CON HUESO |
| 138 | ASADO A 10 COSTILLAS CON HUESO |
| 139 | ENTRAÑA 50% |
| 140 | MENUDENCIAS |
| 141 | ASADO A 10 COSTILLAS CON VACIO Y MATAMBRE |
| 142 | CUARTO DELANTERO A 3 COSTILLAS CON FALDA CON HUESO |
| 143 | TAPA DE PECHO |
| 144 | PECHO SIN TAPA |
| 145 | TAPA DE FALDA |
| 146 | FALDA SIN TAPA |
| 147 | RAL A 10 COSTILLAS CON HUESO |
| 148 | RAL A 4 COSTILLAS CON HUESO |
| 149 | CENTRO DE ASADO |
| 150 | TAPA DE ASADO |
| 151 | TAPA DE PALETA |
| 152 | BIFE A 4 COSTILLAS CON LOMO CON HUESO |
| 153 | BIFE A 10 COSTILLAS CON LOMO CON HUESO |
| 154 | BIFE A 10 COSTILLAS CON HUESO |
| 201 | Media res porcina |
| 202 | Corte carré con hueso |
| 203 | Jamón con hueso, corte largo |
| 204 | Jamón con hueso, corte corto |
| 205 | Jamón con hueso, corte parma |
| 206 | Jamón sin hueso, desgrasado |
| 207 | Paleta con hueso, con cuero |
| 208 | Paleta sin hueso, con cuero desgrasado |
| 209 | Costillar con hueso, lomo y bondiola |
| 210 | Costillar con hueso, lomo |
| 211 | Costillar sin hueso |
| 212 | Bondiola sin hueso |
| 213 | Pechito con hueso |
| 214 | Lomo |
| 215 | Tocino con y sin cuero |
| 216 | Panceta con hueso, con cuero |
| 217 | Panceta sin hueso, con y sin cuero |
| 218 | Lengua |
| 219 | Hígado |
| 220 | Pata |
| 221 | Corazón |
| 222 | Estómago |
| 223 | Riñón |
| 224 | Rabo |
| 225 | Corteza |
| 226 | Carne chica porcina |
| 227 | Otro |
| 901 | EXTRACTO |
| 902 | CALDO DE CARNE |
| 903 | JUGOS |
| 904 | GELATINA |
| 905 | CALDO DE HUESO Y/O CONCENTRADOS |
| 906 | ENLATADOS (CORNED BEEF) |
| 907 | CARNE COCIDA Y CONGELADA EN TUBOS |
| 908 | CALDO DE PATA |
| 909 | HAMBURGUESAS |
| 910 | CHORIZOS - EMBUTIDOS FRESCOS (CHORIZO) |
| 911 | CHORIZOS - EMBUTIDOS SECOS (SALAME) |
| 912 | CHORIZOS - EMBUTIDOS COCIDOS (SALCHICHON) |
| 913 | ENLATADO - PATE DE FOIE Y DE HIGADO |
| 914 | ENLATADOS - PICADILLO DE CARNES |
| 915 | MONDONGO SEMICOCIDO Y CONGELADO |


### Tributos

| **Código** | **Descripción** |
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
| 14 | Retencion IIGG - RG 830 |
| 15 | Retencion IVA - RG 3873 |
| 16 | Pago a cuenta IVA - RG 3873 |
| 17 | Percepción IVA . RG 3873 |
| 20 | Percepción RG 2126/06 |
| 23 | Retención IVA - RG 4199 |
| 21 | Pago a cuenta IVA - RG 4199 |
| 22 | Percepción IVA  RG 4199 |
| 99 | Otros |


### Gastos

| **Código** | **Descripción** |
|---|---|
| 1 | Fondo De Garantia |
| 2 | Gastos De Frigorifico |
| 3 | Guia |
| 4 | Flete |
| 5 | Derecho De Registro |
| 6 | Ipcva |
| 7 | Servicio De Faena |
| 8 | Etiquetado |
| 9 | Arancel Feria |
| 10 | Arancel Remate |
| 11 | Sellos |
| 12 | Psta/Dta |
| 13 | Dte |
| 14 | Caravana |
| 15 | Control Y Entrega |
| 99 | Otros |
| 16 | Comision |



## Novedades

Historial de Cambios:
 
- Mayo 2018: Inclusión de liquidaciones para especies porcinas, especificación técnica [WSLSPv1.7](#wslspv17) de AFIP
- Julio 2017: cambios por nueva especificación técnica [WSLSPv1.4.1](#wslspv141) de AFIP
- Marzo 2017: Ajustes Liquidación, especificación técnica [WSLSPv1.3](#wslspv12) de AFIP
- Febrero 2017: cambios por nueva especificación técnica [WSLSPv1.2](#wslspv12) de AFIP
- Diciembre 2016 (actualización 01): versión inicial

Se recuerda que esta disponible el 
[grupo de noticias](http://groups.google.com.ar/group/pyafipws) donde
se publicarán futuras novedades sobre PyAfipWS: servicios web de
factura electrónica y sus interfases (se recomienda suscribirse)

## Costos y Condiciones

Debido a la complejidad de este servicio, su fecha de aplicación y las modificaciones que pudieran surgir, los clientes que asi lo requieran pueden adquirir horas de soporte técnico comercial (ver [Condiciones del Soporte Comercial](../documentacion_herramientas/pyafipws.md#costos-y-condiciones)).

A su vez, se libera el código fuente bajo licencia GPL (software libre), al igual que se hizo con el restos de los servicios web. Para más detalles ver página FacturaElectronica.