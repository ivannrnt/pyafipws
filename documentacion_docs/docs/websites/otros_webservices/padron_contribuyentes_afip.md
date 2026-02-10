= Padron Contribuyentes AFIP =
[[TracNav(noreorder|FacturaElectronica)]]

Herramienta para consultar el archivo completo de la condición tributaria de los contribuyentes y responsables de la [Resolución General N° 1817](http://infoleg.mecon.gov.ar/infolegInternet/anexos/100000-104999/103117/texact.htm) (Constancia de Inscripción / Opción - Monotributo)

**[Constancia de Inscripción](wiki:PadronContribuyentesAFIP#ConstanciadeInscripci%C3%B3nWebserviceRG416217)** ([WebService SOAP](wiki:PadronContribuyentesAFIP#ServicioWeb)) para acceder al los datos públicos en el registro único contribuyente (`ws_sr_constancia_inscripcion` ex `ws_sr_padron_a5`)

| La administración Federal de Ingresos Públicos informa que, en el corto plazo las solicitudes de emisión de comprobantes electrónicos de Clase "A" emitidas para CUITs que resultan inválidos, inexistentes o no corresponden a responsables inscriptos en el Impuesto al Valor Agregado, serán rechazadas. En caso que la solicitud se esté efectuando por lote, se deberán reprocesar los registros de los comprobantes siguientes al rechazado en virtud de que se verá alterada la correlatividad y consecutividad de la numeración de los mismos. |
|---|

## Índice
[[Image(htdocs:logo-pyafipws.png, align=right)]]
[[TOC(noheading,inline,depth=3)]]

## Descripción General

Esta herramienta permite buscar en el padrón de contributentes de AFIP, obteniendo los datos de manera similar a la Constancia de inscripción o consulta de la condición tributaria vía "Internet".

Sujetos obligados a consultar la situación fiscal (a efectuarse la primera transacción u operación, con validez de 180 días):

 1. Los responsables inscritos en el impuesto al valor agregado,
 1. los designados como agentes de retención,
 1. los escribanos públicos,
 1. los organismos incluidos en la planilla anexa del artículo 1° del Decreto N° 1108 de fecha 21 de setiembre de 1998 (1.1.), y
 1. los organismos que deban cumplir con la obligación de registrar la Clave Unica de Identificación Tributaria (C.U.I.T.), el Código Unico de Identificación Laboral (C.U.I.L.) o la Clave de Identificación (C.D.I.), conforme a las normas emitidas por los Estados Provinciales y el Gobierno de la Ciudad Autónoma de Buenos Aires.


== Consulta a Padron via Servicios Web == **(SERVICIO DESCONTINUADO POR AFIP)**

**Importante**: a partir Oct-2017, la API rest (JSON) funciona intermitentemente (al ser experimental, podría ser discontinuado); es recomendable pasar a utilizar Web Service SOAP **WS-SR-PADRON**

- `ws_sr_padron_a4`: Servicio de Consulta de Padrón Alcance 4. El servicio de Consulta de Padrón Alcance 4 permite acceder a los datos de un contribuyente registrado en el Padrón de AFIP. Este WS se puede utilizar para acceder a datos de un contribuyente relacionados con su situación tributaria. Ejemplo: impuestos y regimenes en los que esta inscripto.
- `ws_sr_padron_a5`: Servicio de Consulta de Padrón Alcance 5. El servicio de Consulta de Padrón Alcance 5 permite acceder a los datos de la constancia de un contribuyente registrado en el Padrón de AFIP
- `ws_sr_padron_a10` Servicio de Consulta de Padrón Alcance 10. El servicio de Consulta de Padrón Alcance 10 permite acceder a los datos de un contribuyente registrado en el Padrón de AFIP, en su versión mínima. Este WS se puede utilizar para acceder a datos resumidos de un contribuyente.
- `ws_sr_padron_a100`: Servicio de Consulta de Padrón Alcance 100. El servicio de Consulta de parámetros del Sistema Registral o Padrón, Alcance 100, permite obtener todos los registros de una tabla específica de parámetros de la AFIP.

Nuestro componente ya soporta este nuevo webservice, y para compatibilidad hacia atrás se utilizan el nuevo objeto `WSSrPadronA4` / `WSSrPadronA5` (en reemplazo de `PadronAFIP`).
Como se utiliza un webservice, se debe crear un Ticket de Acesso `WSAA` y llamar al método `Conectar` con la URL correcta. Para más info ver [Consultar CUIT online via Web Service (componente)](wiki:PadronContribuyentesAFIP#ConsultarCUITonlineviawebservice)

Por linea de comandos, simplemente invocar al ejecutable `ws_sr_padron.exe` en vez de `padron.exe`. Para más información ver [Consultar CUIT online via Web Service (ejecutable)](wiki:PadronContribuyentesAFIP#ConsultarCUITonlineviawebservice1)

Para formato interno de datos y errores frecuentes, ver sección [Servicio Web](wiki:PadronContribuyentesAFIP#ServicioWeb)

Lista de CUITs publicados por AFIP para pruebas: [http://www.afip.gob.ar/ws/ws_sr_padron_a4/datos-prueba-padron-a4.txt]

### Constancia de Inscripción Webservice RG 4162/17

Según [Resolución General 4162/17](http://biblioteca.afip.gob.ar/dcp/REAG01004162_2017_11_23#articulo_0001) se habilitó la opción 

>  c) Intercambio de información mediante “Web Services”, denominado “CONSULTA CONSTANCIAS DE INSCRIPCIÓN”

Actualmente el nuevo servicio web se ha denominado `ws_sr_constancia_inscripcion` (también conocido como `WSSrPadronA5`).

Nuestro componente contempla la lógica interna para analizar los campos similares al archivo "Condición Tributaria" RG 1817/05 (ver compatibilidad hacia atrás).

Para simplificar el desarrollo, todos nuestros componentes se pueden utilizar con las propiedades y métodos similares (ver `WSSrPadronA4`)

Para más información y ejemplos de uso ver:

- [Componente Consulta Inscripción](wiki:PadronContribuyentesAFIP#ConsultarConstanciaInscripci%C3%B3nonlineviawebservice) (pseudo-código)
- [Herramienta consulta de Inscripción](wiki:PadronContribuyentesAFIP#ConstanciadeInscripci%C3%B3nviawebservice) (línea de comandos)

Ver [Errores Frecuentes](wiki:PadronContribuyentesAFIP#ErroresFrecuentes) para estos nuevos webservices.
### API REST JSON

De manera experimental, ofrecemos un servicio intermedio para facilitar la operatoria con el nuevo webservice, pudiendo ser consumida directamente desde JavaScript u otros lenguajes (sin necesidad de XML / SOAP)

Ejemplo Homologación:

https://www.sistemasagiles.com.ar/padron/consulta/persona/20000000516

Resultado (compatible con el formato de la API pública discontinuada de AFIP):
```
{"success": true, "data": {"fechaInscripcion": "", "tipoClave": "CUIT", "numeroDocumento": "51", "estadoClave": "ACTIVO", "impuestos": [366], "idDependencia": 0, "tipoPersona": "FISICA", "tipoDocumento": "LE", "actividades": [410011], "domicilioFiscal": {"localidad": "", "codPostal": "1425", "idProvincia": 0, "direccion": "ARAOZ 1901"}, "idPersona": "20000000516", "mesCierre": 0, "nombre": "ERNESTO DANIEL, MARCELO NICOLAS"}}
```

Consultar con [mailto:padron@sistemasagiles.com.ar] para mayor información.
## Descargas e Instalación

- Instaladores:
- [PyAfipWs-2.7.3290-32bit+wsaa_2.13a+ws_sr_padron_1.06a-homo.exe](https://www.sistemasagiles.com.ar/soft/pyafipws/PyAfipWs-2.7.3290-32bit+wsaa_2.13a+ws_sr_padron_1.06a-homo.exe) (via webservice)  incluyendo Constancia_Inscripción (Ex Padron_A5)
- [PyAfipWs-2.7.1791-32bit+padron_1.05b-homo.exe](http://www.sistemasagiles.com.ar/soft/pyafipws/PyAfipWs-2.7.1791-32bit+padron_1.05b-homo.exe) (histórico)
- Ejemplos de código (última versión de desarrollo):
- Visual Basic (VB 5/6): [ws_sr_padron.bas](https://github.com/reingart/pyafipws/blob/master/ejemplos/padron/ws_sr_padron.bas) (via webservice) 
- Visual Fox Pro (VFP): [https://github.com/reingart/pyafipws/commit/594355a21c7debde0b0992e24f25e75e791047dc] (via webservice) 
- Visual Basic 5/6: [padron.bas](https://github.com/reingart/pyafipws/blob/master/ejemplos/padron/padron.bas) (histórico, discontinuado por AFIP)
- [Manual de Uso](wiki:ManualPyAfipWs): Documentación General ([PDF](http://www.sistemasagiles.com.ar/trac/wiki/ManualPyAfipWs?format=pdf)) y [Sitio AFIP](http://www.afip.gob.ar/genericos/cInscripcion/archivoCompleto.asp)
- Manual de desarrollo AFIP: [V 3.4](https://www.afip.gob.ar/ws/WSCI/manual-ws-sr-ws-constancia-inscripcion-v3.4.pdf) 08/05/2023
- Código Fuente (Python): ver
- [padron.py](https://github.com/reingart/pyafipws/blob/master/padron.py) (histórico, discontinuado por AFIP)
- [ws_sr_padron.py](https://github.com/reingart/pyafipws/blob/master/ws_sr_padron.py) (via webservice) 

## Métodos

Métodos principales:

- **`Buscar(cuit)`**: Realiza la búsqueda en la base de datos local de contribuyentes. Devuelve verdadero en caso de ejecución satisfactoria, falso en caso de error. Establece los atributos correspondientes. Ver [Ejemplos](http://www.sistemasagiles.com.ar/trac/wiki/PadronContribuyentesAFIP#Ejemplos).
- **`Consultar(cuit)`**: realiza la consulta **online** con AFIP y devulve los campos: cuit, dni, tipo_persona ("FISICA" o "JURIDICA"), tipo_doc (80: "CUIT", 96: "DNI", etc), estado ("ACTIVO"), denominacion, direccion, localidad, provincia, cod_postal, imp_iva, empleador, integrante_soc, cat_iva, monotributo, actividad_monotributo; domicilios, impuestos, actividades (listas) *agregado a partir de la actualización 1.04a*
- **`DescargarConstancia(self, nro_doc, filename)`**: realiza la consulta **online** con AFIP y descarga la constancia de inscripción en formato PDF (filename es el nombre de archivo a guardar, "constancia.pdf" predeterminado). Devuelve verdadero si no hubo inconveinentes, y establece el mensaje de error devuelto por AFIP en el campo Excepcion (si no sep udo descargar la constancia). *agregado a partir de la actualización 1.05a*

Métodos secundarios:

- **`Descargar(url, filename="padron.txt", proxy=None)`**: descarga y descomprime el archivo original de AFIP (solo en caso de que sea más reciente que al último descargado). Los parámetros filename y proxy son opcionales. Devuelve el código 200 si se ha descargado satisfactoriamente, o 304 si el archivo no ha sido modificado por AFIP.
- **`Procesar(filename="padron.txt")`**: recorre el archivo original de AFIP y genera la base de datos interna para consultas (realizar luego de una descarga exitosa).
- **`Conectar(url, proxy, wrapper, cacert, trace))`**: inicializa la conexión hacia los servicios online de AFIP (todos los parámetros son opcionales) *agregado a partir de la actualización 1.04b*
- **`MostrarPDF(archivo, imprimir)`**: abre el visor predeterminado para PDF con el nombre de archivo (por ej. "constancia.pdf"). Si imprimir es verdadero, se utiliza la opción para enviarlo directamente a la impresora. *agregado a partir de la actualización 1.05a*
- **`ObtenerTablaParametros(ObtenerTablaParametros(self, tipo_recurso, sep="||"):`**: devuelve una lista de strings (con el separador indicado) o diccionario (separador nulo) con el id y descripción de los parámetros usados por AFIP en `Consultar`. `tipo_recurso` puede ser `"impuestos"`, `"conceptos"`, `"actividades"`, `"caracterizaciones"`, `"categoriasMonotributo"`, `"categoriasAutonomo"`.

Métodos Auxiliares:

- **`ObtenerTagXml(nombre atributo)`**: permite la consulta de atributos particulares (ver [campos adicionales](https://www.sistemasagiles.com.ar/trac/wiki/PadronContribuyentesAFIP#Obtenci%C3%B3ndeCamposadicionales))

## Atributos

Propiedades principales establecidas por la búsqueda de padrón:

- **`cuit`**: código único de identificación tributaria (completado si existe en el padrón, en blanco en caso contrario)
- **`denominacion`**: nombre y apellido o razón social del contribuyente (30 caracteres)
- **`imp_ganancias`**: 'NI' , 'AC','EX', 'NC' (2 caracteres)
- **`imp_iva`**: 'NI' , 'AC','EX','NA','XN','AN' (2 caracteres)
- **`monotributo`**: 'NI' , "Codigo categoria tributaria" (2 caracteres)
- **`integrante_soc`**: 'N' , 'S' (2 caracteres)
- **`empleador`**: 'N' , 'S' (1 caracteres)
- **`actividad_monotributo`**: (2 caracteres)

Nuevos campos devueltos por la consulta online:

- **`tipo_persona`**: FISICA o JURIDICA
- **`tipo_doc`**, **`nro_doc`**: tipo y número de documento
- **`estado`**: por ej. ACTIVO
- **`direccion`**, **`localidad`**, **`provincia`**, **`cod_postal`**: domicilio fiscal del contribuyente
- **`impuestos`**: lista de los impuestos asociados al contribuyente (array numérico)
- **`actividades`**: lista de las actividades del contribuyente (array numérico)


Referencias:

| 'NI', 'N' | No Inscripto |
|---|---|
| 'AC', 'S' | Activo |
|| 'EX' || Exento
|| 'NA' || No alcanzado 
|| 'XN' || Exento no alcanzado
|| 'AN' || Activo no alcanzado
| 'NC' | No corresponde |
|---|---|

== Obtención de Campos adicionales == (consulta con método ObtenerTagXml)

**primera actividad**:

- 'actividad', 0, 'descripcionActividad'

- 'actividad', 0, 'idActividad'

- 'actividad', 0, 'nomenclador'

- 'actividad', 0, 'orden'

- 'actividad', 0, 'periodo'

**segunda actividad**:

- 'actividad', 1, 'descripcionActividad'

...

**domicilio**:

- 'domicilio', 0, 'codPostal'

- 'domicilio', 0, 'descripcionProvincia'

- 'domicilio', 0, 'direccion'

- 'domicilio', 0, 'idProvincia'

- 'domicilio', 0, 'localidad'

- 'domicilio', 0, 'tipoDomicilio'

**email**:

- 'email', 0, 'direccion'

- 'email', 0, 'estado'

- 'email', 0, 'tipoEmail'


- 'estadoClave'

- 'fechaContratoSocial'

- 'fechaInscripcion'

- 'formaJuridica'

- 'idPersona'

**impuesto**:

- 'impuesto', 0, 'descripcionImpuesto'

- 'impuesto', 0, 'diaPeriodo'

- 'impuesto', 0, 'estado'

- 'impuesto', 0, 'ffInscripcion'

- 'impuesto', 0, 'idImpuesto'

- 'impuesto', 0, 'periodo'


- 'localidadInscripcion'

- 'mesCierre'

- 'numeroInscripcion'

- 'organismoInscripcion'

- 'porcentajeCapitalNacional'

- 'provinciaInscripcion'

- 'razonSocial'

**relacion**:

- 'relacion', 0, 'ffRelacion'

- 'relacion', 0, 'idPersona'

- 'relacion', 0, 'idPersonaAsociada'    

- 'relacion', 0, 'subtipoRelacion'  

- 'relacion', 0, 'tipoRelacion'

**telefono**:

- 'telefono', 0, 'numero'

- 'telefono', 0, 'tipoLinea'

- 'telefono', 0, 'tipoTelefono'

- 'tipoClave'

- 'tipoPersona'


## Ejemplos

Ver fragmentos de código para Visual Basic, Visual Fox Pro y VB.Net en [Descargas e Instalacion](wiki:PadronContribuyentesAFIP#DescargaseInstalación)

### Consultar CUIT localmente

Pseudocódigo en Python para Consulta de Padrón AFIP por CUIT (búsqueda en la base de datos local):

```
#!python
 
padron = PadronAFIP()
cuit = "20267565393"
# consultar un cuit:
ok = padron.Buscar(cuit)
if ok:
    print "Denominacion:", padron.denominacion
    print "Impuesto IVA:", padron.imp_iva
    print "Impuesto a las Ganancias:", padron.imp_ganancias
    print "Monotributo (categoría):", padron.monotributo
    print "Actividad Monotributo:", padron.actividad_monotributo
    print "Empleador:", padron.empleador
    print "Integrante sociedades:", padron.integrante_soc

```

### Consultar CUIT online via webservice

Pseudocódigo en Python para Consulta de Padrón AFIP por CUIT (búsqueda online en el servidor de AFIP):

```
#!python

# obtener ticket de acceso:
wsaa = WSAA()
ta = wsaa.Autenticar("ws_sr_constancia_inscripcion", "reingart.crt", "reingart.key")

# conectar al webservice de padrón:
padron = WSSrPadronA5()
padron.SetTicketAcceso(ta)
padron.Cuit = "20267565393"
padron.Conectar()

# consultar un cuit:
print "Consultando AFIP online...",
id_persona = "20000000516"
ok = padron.Consultar(id_persona)
print "Denominacion:", padron.denominacion
print "CUIT:", padron.cuit 
print "Tipo:", padron.tipo_persona, padron.tipo_doc, padron.dni
print "Estado:", padron.estado
print "Direccion:", padron.direccion
print "Localidad:", padron.localidad
print "Provincia:", padron.provincia
print "Codigo Postal:", padron.cod_postal
print "Impuestos:", padron.impuestos
print "Actividades:", padron.actividades
print "IVA", padron.imp_iva
print "MT", padron.monotributo, padron.actividad_monotributo
print "Empleador", padron.empleador
```

### Consultar Constancia Inscripción online via webservice

Pseudocódigo en Python para Consulta Constancia Inscripción [RG4162/17](wiki:PadronContribuyentesAFIP#ConstanciadeInscripci%C3%B3nWebserviceRG416217) por CUIT (búsqueda online en el servidor de AFIP):

```
#!python

# obtener ticket de acceso:
wsaa = WSAA()
ta = wsaa.Autenticar("ws_sr_constancia_inscripcion", "reingart.crt", "reingart.key")

# conectar al webservice de padrón:
padron = WSSrPadronA5()
padron.SetTicketAcceso(ta)
padron.Cuit = "20267565393"
padron.Conectar()

# consultar un cuit:
print "Consultando AFIP online...",
id_persona = "20000000516"
ok = padron.Consultar(id_persona)
print "Denominacion:", padron.denominacion
print "CUIT:", padron.cuit 
print "Tipo:", padron.tipo_persona, padron.tipo_doc, padron.dni
print "Estado:", padron.estado
print "Direccion:", padron.direccion
print "Localidad:", padron.localidad
print "Provincia:", padron.provincia
print "Codigo Postal:", padron.cod_postal
print "Impuestos:", padron.impuestos
print "Actividades:", padron.actividades
print "IVA", padron.imp_iva
print "MT", padron.monotributo, padron.actividad_monotributo
print "Empleador", padron.empleador

print "Errores", padron.errores
```
=== Consultar CUIT online === **(En desuso por baja de AFIP)**

**Importante**: servicio experimental, discontinuado por AFIP (Oct'2017) Solo sigue vigente la descarga de Constancia.

Pseudocódigo en Python para Consulta de Padrón AFIP por CUIT (búsqueda online en el servidor de AFIP):

```
#!python
 
padron = PadronAFIP()
cuit = "20267565393"
padron.Conectar()
# consultar un cuit:
print "Consultando AFIP online...",
ok = padron.Consultar(cuit)
print "Denominacion:", padron.denominacion
print "Tipo:", padron.tipo_persona, padron.tipo_doc, padron.dni
print "Estado:", padron.estado
print "Direccion:", padron.direccion
print "Localidad:", padron.localidad
print "Provincia:", padron.provincia
print "Codigo Postal:", padron.cod_postal
# ...
```


### Descargar Constancia de Inscripción online

Pseudocódigo en Python para descargar la Constancia de Inscripción de un contribuyente AFIP por CUIT (búsqueda online en el servidor de AFIP):

```
#!python

# instanciar el objeto e iniciar conexión al servidor
padron = PadronAFIP()
cuit = "20267565393"
filename = "constancia.pdf"
padron.Conectar()

# descargar la constancia:
print "Consultando AFIP online...",
ok = padron.DescargarConstancia(cuit, filename)

# mostrar el PDF:
imprimir = False
padron.MostrarPDF(filename, imprimir)
```

Es recomendable indicar una ruta absoluta para evitar cuestiones de permisos de acceso (por ejemplo filename="C:\Windows\TEMP").


## Linea de comandos

PADRON puede también utilizarse por línea de comando (tanto para Windows como para GNU/Linux) y recibe los siguientes argumentos:

- cuit: número sin guiones a consultar
- `--descargar`: realiza la descarga del archivo completo de AFIP
- `--procesar`: procesa el archivo descargado y crea la base de datos interna
- `--online`: realiza la consulta directamente vía los servidores de AFIP   *agregado en actualización 1.04b*
- `--constancia`: descarga la constancia PDF directamente vía los servidores de AFIP   *agregado en actualización 1.05a*

También se puede utilizar `--trace` para ver los mensajes de depuración.
### Consultar CUIT localmente

Ejemplo para consultar por CUIT (sintaxis para windows, busqueda en la base de datos local):
```
C:\PYAFIPWS> PADRON_CLI.EXE 20267565393
Denominacion: REINGART MARIANO ALEJANDRO
IVA: AC
```

### Consultar CUIT online via webservice

Ejemplo para consultar por CUIT (sintaxis para windows, consulta online al servidor de AFIP):
```
C:\PYAFIPWS> WS_SR_PADRON_cli.EXE 20267565393 --constancia
Consultando AFIP online via webservice...
Denominacion: REINGART MARIANO ALEJANDRO
CUIT: 20267565393
Tipo: FISICA 80 26756539
Estado: ACTIVO
Direccion: PROF D CASTAGNA 4942
Localidad: VILLA TESSEI
Provincia: BUENOS AIRES
Codigo Postal: 1688
Impuestos: [30, 308, 11]
Actividades: [620100]
IVA S
MT N 
Empleador N
```

**Nota:** el ejecutable difiere, en este caso usar `WS_SR_PADRON_cli.exe`
### Consultar CUIT online

**Importante**: servicio experimental, discontinuado por AFIP (Oct'2017) Solo sigue vigente la descarga de Constancia.

Ejemplo para consultar por CUIT (sintaxis para windows, consulta online al servidor de AFIP):
```
C:\PYAFIPWS> PADRON_CLI.EXE 20267565393 --online
Consultando AFIP online... ok 
Denominacion: REINGART MARIANO ALEJANDRO
CUIT: 20267565393
Tipo: FISICA 80 26756539
Estado: ACTIVO
Direccion: PROF D CASTAGNA 4942
Localidad: VILLA TESSEI
Provincia: BUENOS AIRES
Codigo Postal: 1688
Impuestos: [30, 308, 11]
Actividades: [620100]
IVA S
MT N 
Empleador N
```

### Constancia de Inscripción online

Ejemplo para descargar y mostrar la constancia de inscripción en formato PDF por CUIT (opción `--constancia`, sintaxis para windows, consulta online al servidor de AFIP):
```
C:\PYAFIPWS> PADRON_CLI.EXE  20267565393 constancia.pdf --constancia --mostrar
Descargando constancia AFIP online... 20267565393 constancia.pdf
ok
```

Luego se debería abrir de manera automática el PDF (opción `--mostrar`)

### Constancia de Inscripción via webservice

Ejemplo para obtener los datos de la constancia de inscripción vía el nuevo Servicio Web según [RG4162/17](wiki:PadronContribuyentesAFIP#ConstanciadeInscripci%C3%B3nWebserviceRG416217) (sintaxis para windows, consulta online al servidor de AFIP):
```
C:\PYAFIPWS> WS_SR_PADRON_cli.EXE 27255820422 --constancia
Consultando AFIP online via webservice... ok 
Denominacion: ALEXA, HILARY
Tipo: FISICA 80 27255820422
Estado: ACTIVO
Direccion: SAN MARTIN 256
Localidad: VILLA CARLOS PAZ
Provincia: CORDOBA
Codigo Postal: 5152
Impuestos: [20]
Actividades: [10L]
IVA N
MT S C VENTAS DE COSAS MUEBLES
Empleador N
```

**Nota:** el ejecutable difiere, en este caso usar `WS_SR_PADRON_cli.exe`
## Servicio Web

Para información general ver [Consultas Padron via Servicios Web](wiki:PadronContribuyentesAFIP#ConsultaaPadronviaServiciosWeb)

URL WSDL WS-SR-Padron-A4:

- Homologación: https://awshomo.afip.gov.ar/sr-padron/webservices/personaServiceA4?wsdl (testing)
- Producción: https://aws.afip.gov.ar/sr-padron/webservices/personaServiceA4?wsdl

Descargar [Instalador](wiki:PadronContribuyentesAFIP#DescargaseInstalación)

Para crear el componente, hacer `CreateObject("WSSrPadronA4")`, ver:

- [Métodos](wiki:PadronContribuyentesAFIP#Métodos): sólo `Consultar` para `WSSrPadronA4`.
- [Propiedades](wiki:PadronContribuyentesAFIP#Atributos): `cuit`, `dni`, `denominacion`, `imp_ganancias`, `imp_iva`, `monotributo`, `integrante_soc`, `empleador`, `actividad_monotributo`, `cat_iva`, `domicilios`, `tipo_doc`, `nro_doc`, `LanzarExcepciones`, `tipo_persona`, `estado`, `impuestos`, `actividades`, `direccion`, `localidad`, `provincia`, `cod_postal`

### Respuesta Alcance 4 (Padrón)

El método `Consultar` (`GetPersona`) del nuevo webservice `WSSrPadronA4` devuelve la siguiente estructura XML (convertida a JSON para simplificar el análisis; como muestra ver [pseudo-código ejemplo](wiki:PadronContribuyentesAFIP#ConsultarCUITonlineviawebservice) concreto):

```
#!python

{'idPersona': 20000000516,
 'apellido': 'ERNESTO DANIEL',
 'nombre': 'MARCELO NICOLAS',
 'estadoClave': 'ACTIVO',
 'fechaInscripcion': '2010-10-30',
 'fechaNacimiento': '1891-1-1',
 'mesCierre': 12,
 'tipoDocumento': 'LE',
 'numeroDocumento': '51',
 'sexo': 'MASCULINO',
 'tipoClave': 'CUIT',
 'tipoPersona': 'FISICA',
 'dependencia': {'descripcionDependencia': 'DISTRITO ZAPALA          ',
                 'idDependencia': 702},
 'domicilio': [{'codPostal': '8371',
                'datoAdicional': 'N/A PATRICIA ANDREA',
                'descripcionProvincia': 'NEUQUEN',
                'direccion': 'LAGUNA LOS SAUCES 2',
                'idProvincia': 20,
                'localidad': 'JUNIN DE LOS ANDES',
                'tipoDatoAdicional': 'NO DETERMINADO',
                'tipoDomicilio': 'FISCAL'},
               {'codPostal': '1425',
                'descripcionProvincia': 'CIUDAD AUTONOMA BUENOS AIRES',
                'direccion': 'ARAOZ 1901',
                'idProvincia': 0,
                'tipoDomicilio': 'LEGAL/REAL'}],
 'actividad': [{'descripcionActividad': 'CONSTRUCCI\xd3N, REFORMA Y REPARACI\xd3N DE EDIFICIOS RESIDENCIALES',
                'idActividad': 410011,
                'nomenclador': 883,
                'orden': 1,
                'periodo': 201311}],
 'impuesto': [{'descripcionImpuesto': 'GANANCIAS PERSONAS FISICAS',
               'diaPeriodo': 30,
               'estado': 'BAJA DEFINITIVA',
               'ffInscripcion': datetime.datetime(2002, 4, 5, 12, 0),
               'idImpuesto': 11,
               'periodo': 200611},
              {'descripcionImpuesto': 'MONOTRIBUTO',
               'diaPeriodo': 30,
               'estado': 'BAJA DEFINITIVA',
               'ffInscripcion': datetime.datetime(2000, 3, 11, 12, 0),
               'idImpuesto': 20,
               'periodo': 200406},
              {'descripcionImpuesto': 'MONOTRIBUTO AUTONOMO',
               'diaPeriodo': 30,
               'estado': 'BAJA DEFINITIVA',
               'ffInscripcion': datetime.datetime(2000, 3, 11, 12, 0),
               'idImpuesto': 21,
               'periodo': 200406},
              {'descripcionImpuesto': 'GANANCIA MINIMA PRESUNTA',
               'diaPeriodo': 30,
               'estado': 'BAJA DEFINITIVA',
               'ffInscripcion': datetime.datetime(2005, 3, 15, 12, 0),
               'idImpuesto': 25,
               'periodo': 200611},
              {'descripcionImpuesto': 'SICORE-IMPTO.EMERG.AUTOMOTORES',
               'diaPeriodo': 31,
               'estado': 'BAJA DEFINITIVA',
               'ffInscripcion': datetime.datetime(2008, 1, 29, 12, 0),
               'idImpuesto': 64,
               'periodo': 200708},
              {'descripcionImpuesto': 'EMPLEADOR-APORTES SEG. SOCIAL',
               'diaPeriodo': 15,
               'estado': 'ACTIVO',
               'ffInscripcion': datetime.datetime(2005, 3, 15, 12, 0),
               'idImpuesto': 301,
               'periodo': 200503},
              {'descripcionImpuesto': 'APORTES SEG.SOCIAL AUTONOMOS',
               'diaPeriodo': 10,
               'estado': 'BAJA DEFINITIVA',
               'ffInscripcion': datetime.datetime(2008, 1, 25, 12, 0),
               'idImpuesto': 308,
               'periodo': 200804},
              {'descripcionImpuesto': 'INTERNOS-SEGUROS ',
               'diaPeriodo': 30,
               'estado': 'BAJA DEFINITIVA',
               'ffInscripcion': datetime.datetime(2005, 9, 12, 12, 0),
               'idImpuesto': 365,
               'periodo': 200611},
              {'descripcionImpuesto': 'ADICIONAL EMERG.CIGARRILLOS',
               'diaPeriodo': 1,
               'estado': 'ACTIVO',
               'ffInscripcion': datetime.datetime(2008, 1, 28, 12, 0),
               'idImpuesto': 366,
               'periodo': 200708}],
  'regimen': [{'descripcionRegimen': 'REG.PER. IMPUESTO DE EMERGENCIA A LOS AUTOMOTORES Y OTROS - FONDO NACIONAL DE INCENTIVO DOCENTE.',
              'estado': 'BAJA DEFINITIVA',
              'idImpuesto': 64,
              'idRegimen': 715,
              'periodo': 200708,
              'tipoRegimen': 'PERCEPCION'}],
}

```

Para compatibilidad hacia atrás, nuestro componente los procesa de forma similar al objeto `Padron` original.


### Respuesta Constancia Inscripcion (Ex Alcance 5)

El método `Consultar` (`GetPersona`) del nuevo webservice `ws_sr_constancia_inscripcion` (Constancia) devuelve la siguiente estructura XML (convertida a JSON para simplificar el análisis; como muestra ver [pseudo-código ejemplo](wiki:PadronContribuyentesAFIP#ConsultarCUITonlineviawebservice) concreto):

```
#!python

{'personaReturn': {
    'datosGenerales': {
        'apellido': str,
        'dependencia': {
            'codPostal': str,
            'descripcionDependencia': str, 
            'descripcionProvincia': str, 
            'direccion': str, 
            'idDependencia': int, 
            'idProvincia': int, 
            'localidad': str
            },
        'domicilioFiscal': {
            'codPostal': str,
            'datoAdicional': str,
            'descripcionProvincia': str, 
            'direccion': str, 
            'idProvincia': int, 
            'localidad': str, 
            'tipoDatoAdicional': str, 
            'tipoDomicilio': str
            },
        'esSucesion': str,
        'estadoClave': str,
        'fechaContratoSocial': datetime,
        'idPersona': long,
        'mesCierre': int, 
        'nombre': str, 
        'razonSocial': str, 
        'tipoClave': str, 
        'tipoPersona': str
        },
    'datosMonotributo': {
        'actividadMonotributista': [{
            'descripcionActividad': str,
            'idActividad': long, 
            'nomenclador': int,
            'orden': int,
            'periodo': int
            }],
        'categoriaMonotributo': {
            'descripcionCategoria': str, 
            'idCategoria': int, 
            'idImpuesto': int, 
            'periodo': int
            },
        'componenteDeSociedad': [{
            'apellidoPersonaAsociada': str, 
            'ffRelacion': 'datetime.datetime', 
            'ffVencimiento': 'datetime.datetime', 
            'idPersonaAsociada': long, 
            'nombrePersonaAsociada': str, 
            'razonSocialPersonaAsociada': str, 
            'tipoComponente': str
            }], 
        'impuesto': [{
            'descripcionImpuesto': str, 
            'idImpuesto': int, 
            'periodo': int
            }]},
    'datosRegimenGeneral': {
            'actividad': [{
                'descripcionActividad': str, 
                'idActividad': long, 
                'nomenclador': int, 
                'orden': int, 
                'periodo': int
                }], 
      'categoriaAutonomo': {
            'descripcionCategoria': str, 
            'idCategoria': int, 
            'idImpuesto': int, 
            'periodo': int
            },
      'impuesto': [{
            'descripcionImpuesto': str, 
            'idImpuesto': int, 
            'periodo': int
            }],
      'regimen': [{
            'descripcionRegimen': str, 
            'idImpuesto': int, 
            'idRegimen': int, 
            'periodo': int, 
            'tipoRegimen': str
            }],
    },
    'errorConstancia': [{'apellido': str, 'error': str, 'idPersona': long, 'nombre': str}], 
    'errorMonotributo': [{'error': str, 'mensaje': str}], 
    'errorRegimenGeneral': [{'error': str, 'mensaje': str}], 
    'metadata': {'fechaHora': 'datetime.datetime', 'servidor': str}
    }
}
```
### Errores Frecuentes

Tanto el webservice de Alcance 4 (padrón) y constancia_inscripcion (constancia) lanzan la siguiente excepción si el CUIT no está registrado: 

- `SoapFault: soap:Server: No existe persona con ese Id` revisar el CUIT enviado (en homologación solo se puede probar con el CUIT de ejemplo)

Nuevos tipos de errores para el webservice constancia_inscripcionde (Ex Alcance 5):

- Error Constancia:
    - `La CUIT del contribuyente fue limitada en los terminos de la RG AFIP 3832/16. Motivo: CUIT LIMITADA - POR INCLUSIÓN EN BASE CONTRIBUYENTES NO CONF`
    - `La clave ingresada no es una CUIT` (seguramente es una CUIL)
    - `La cuit ingresada se encuentra inactiva. Acceda con su clave activa`
    - `Estado erroneo del domicilio`
    - `Sr. Contribuyente de acuerdo a lo establecido en el Art. Nro. 7 de la R.G. AFIP Nro. 3537/13 para obtener la constancia de inscripcion/opcion, debera realizar previamente la actualizacion de todas sus actividades economicas. A tales efectos ingrese al servicio Sistema Registral, opcion Registro Tributario/ F. 420/D Declaracion de actividades, y declare las actividades del nomenclador f. 883 que correspondan.`   
- Error Monotributo: Mensaje: `No cumple con las condiciones para enviar datos monotributo`
- `No consta en nuestros registros que Ud. ha cumplido con la Recategorización o confirmación de datos, según lo normado por la R.G. 4104-E, hasta tanto no normalice su situación no podrá visualizar su constancia.`
- Error Régimen General:

## Tablas de Parámetros

### Impuestos
| **id** | **desc** |
|---|---|
| 3 | INFORMACION NO TRIBUTARIA |
| 4 | INSCRIPCIÓN DE SOCIEDADES RNS |
| 5 | DDJJ  INEXISTENCIA DEUDA RNSS |
| 6 | F.8102 - APLIC. PERCEP CPRAS E |
| 7 | PENALIDADES RENDITA Y ACRETA |
| 8 | DADOR DE TRABAJO SERV. DOM. |
| 10 | GANANCIAS SOCIEDADES |
| 11 | GANANCIAS PERSONAS FISICAS |
| 12 | EXENTO EN GANANCIAS |
| 14 | PRECIOS DE TRANSFERENCIA |
| 15 | EMERGENCIA SOBRE ALTAS RENTAS |
| 20 | MONOTRIBUTO |
| 21 | MONOTRIBUTO AUTONOMO |
| 22 | MONOTRIBUTO SEG.SOCIAL |
| 23 | MONOTRIBUTO-INTEG.DE SOCIEDAD |
| 24 | MONOTRIBUTO OBRA SOCIAL |
| 25 | GANANCIA MINIMA PRESUNTA |
| 26 | INT.PAG.Y COSTO FINAN.ENDEUDAM |
| 27 | PATRIMONIO NETO |
| 28 | SEGURO DE VIDA COLECTIVO |
| 30 | IVA |
| 31 | RENTAS DIVERSAS |
| 32 | IVA EXENTO |
| 33 | IVA RESPONSABLE NO INSCRIPTO |
| 34 | IVA NO ALCANZADO |
| 35 | PRESENT.ESPONTANEA DTO.935/97 |
| 36 | REG.INF.INGRESOS-EGRESOSRG1242 |
| 37 | GARANTIAS |
| 38 | FACILIDADES DE PAGO DTO.938/97 |
| 39 | MULTAS INFRACCIONES FORMALES |
| 40 | REG.ESP.FAC.PAGO |
| 41 | P.FAC PAGO-RG896 RESTO REG GRA |
| 42 | P.FAC PAGO-RG896 RESTO REG EXC |
| 43 | MULTAS L. 11683 |
| 48 | HONORARIOS AGENTES FISCALES |
| 49 | HONORARIOS DE REPRES.DEL FISCO |
| 50 | REG.FACILIDADES PAGO RG.50 |
| 51 | REG DE FAC DE PAGO OBRAS SOCIA |
| 52 | TASA S/ACTUACIONES ANTE TFN |
| 53 | TASA REGISTRO PROPIED.INMUEBLE |
| 55 | SELLOS LEY 18524 |
| 57 | FAC.PAGO-REG.EXCEPIRREG CONCUR |
| 58 | FAC.PAGO-REG.EXCEPIRREG FALLID |
| 59 | FAC.PAG.REG.EXCEP.DEUD.QUIROG. |
| 60 | FAC  PAGO DTO 93/2000 |
| 61 | DECRETO 93/00 DEUDA CONCURSADA |
| 62 | FAC DE PAGO LEY 25190 |
| 64 | SICORE-IMPTO.EMERG.AUTOMOTORES |
| 65 | EMERG.AUTOMOTORES |
| 66 | EXTERIORIZACIÓN - LEY 26.476 |
| 70 | INTERNOS- NACIONALES LEY 21425 |
| 71 | CONTROL REND.BANCARIAS S.2000 |
| 72 | RESP DEUDA AJENA BS.PERS. |
| 73 | RESP DEUDA AJENA GAN MIN PRES |
| 74 | F.PAG.RG.896-REG.GRAL. |
| 75 | F.PAG RG.896-REG.EXC.PL.REG. |
| 76 | F.PAG RG.896-REG.EXC.IRREG. |
| 77 | F PAGO-REG EXC REG-CONCURSADOS |
| 78 | FAC PAGO-REG EXC REG-FALLIDOS |
| 79 | REG.FAC.PAGO-MIS FACILIDADES |
| 83 | CERTIFICADO DE CREDITO FISCAL |
| 85 | CANON MENSUAL TURIVA |
| 90 | REPOSICIÓN DE TOKEN |
| 91 | COMISIONES POR SERV. DE RECA. |
| 100 | SOLIC.COMPENSACIÓN-IMP.DE CRED |
| 101 | SOLICITUD DE DEVOLUCIÓN |
| 102 | GRAVAMEN A SERV.AUX.NAVEGACION |
| 103 | REGIMENES DE INFORMACIÓN |
| 104 | RÉG.ESP.FAC.PAGO-RG,574-RG 904 |
| 105 | PFP-DTO.1384/01-IMPOSITIVAS |
| 106 | PFP-DTO.1384/01-SEG. SOCIAL |
| 107 | PFP-DTO.1384/01-IMPOSIT-CONCUR |
| 108 | PFP-DTO.1384/01-SEG.SOC.CONCUR |
| 109 | PFP-IMPOSIT DTO.338/2002 |
| 110 | PFP-SEG.SOC.DTO.338/2002 |
| 111 | TRANSF.VALORES MOBILIARIOS |
| 112 | DTO905-REFOR.PLAN.ANTER.93/00 |
| 113 | ADIC.EMERG.TIT.PUBLIC.RG.3320 |
| 114 | PFP-DTO.338/02-IMPOSIT-CONCURS |
| 115 | PFP-DTO.338/02-SEG.SOC-CONCURS |
| 116 | PFP-AUTON MONOTRIB D 27/07/04 |
| 117 | PFP-IMPOSITIVO DECRETO 1541/04 |
| 118 | PFP-DTO2724 IMPOSIT.DEUDA 2002 |
| 119 | PFP-DTO2724 IMPOSIT.DEUDA 2003 |
| 120 | SOBRE LOS CAPITALES |
| 121 | PLAN FACILIDADES PAGO RG.184 |
| 122 | FAC.PAGO DEUDA S/GTIA.RG.184 |
| 123 | PRESENTACION ESPONTANEA RG.184 |
| 124 | PRES.ESPONTANEA DEUDA S/GTIA. |
| 125 | PFP-IMPOSITIVO |
| 126 | PFP-IMPOSITIVO |
| 127 | REGIMEN REGULARIZ VOLUNT 24476 |
| 128 | PFP- SEGURIDAD SOCIAL |
| 129 | PFP- SEGURIDAD SOCIAL |
| 130 | IVA RG.3298 |
| 132 | BENEF.PROV.INVERS.CAP.EXTRANJ. |
| 133 | REG.FACILIDADES PAGO D.1164/93 |
| 134 | F.PAGO CONCURSOS PREV. RG.3762 |
| 135 | IMPUESTO |
| 136 | IMPUESTO |
| 137 | TASAS JUDICIALES L.23898 |
| 139 | IMP S/DEB Y CRED OP.EXENTAS |
| 140 | HONORARIO ART 64, LEY 24.946 |
| 141 | HONORARIOS ABOGADOS Y PERITOS |
| 142 | P ESP FAC PAGO L 22681 |
| 143 | PAGO A CTA. FUTUR OBLIGACIONES |
| 144 | IVA-USUARIOS SERVICIO MOLIENDA |
| 145 | RAFA-RET BENEF EXTERIOR |
| 146 | ZONAS AFECTADAS POR INUNDACION |
| 147 | SICORE-S/DEB.CTA.CTE.Y O.OPER. |
| 148 | REG.ESPEC.FACILIDADES DE PAGO |
| 149 | IMP S/DEB Y CRED EN CTA CTE |
| 150 | REVALUACION HACIENDA L.23079 |
| 151 | AHORRO OBLIGATORIO L.23256 |
| 152 | INTERESES AHORRO OBLIGATORIO |
| 153 | REGIMEN CONDONACION SANCIONES |
| 154 | FONDO P/EDUC.Y PROM.COOPTIVA. |
| 155 | REG.FACILIDADES PAGO RG.2757 |
| 156 | REG.FAC.CONCURSOS Y QUIEBRAS |
| 157 | AHORRO OBLIGATORIO L.23549 |
| 158 | INTERES AHORRO OBLIGATORIO |
| 159 | FONDO TRANSIT.P/FINANC.DESEQ. |
| 160 | TARJETAS ADIC ACRED INSCRIPCIO |
| 161 | ADICIONAL EMERG.TIT.PUBLICOS |
| 162 | REG.FACILIDADES PAGO RG.3011 |
| 163 | EMERGENC.AGROPECUARIA RG.3018 |
| 164 | FONDO EMERG.LOCATIVA RG.3033 |
| 165 | S/ACTIVOS FINANCIEROS D.560/89 |
| 166 | SUSPENSION REG.PROM.(GAN.) |
| 167 | SUSPENSION REG.PROM.(IVA) |
| 168 | SUSPENSION REG.PROM.(CAP.) |
| 169 | SUSPENSION REG.PROM.(PN) |
| 170 | CONTRIBUCION SOLIDARIA L.23740 |
| 171 | REG.FAC.PAGO DTO.1299/89 |
| 172 | IMPUESTO TRANSF DE INMUEBLES |
| 173 | EMERG.S/UTILIDADES ENT.FINANC. |
| 174 | CONTRIB.ESPEC.EMERG.L.23764 |
| 175 | SERVICIOS FINANCIEROS L.23760 |
| 176 | APORTE ESPEC.DTOS.435 Y 612/90 |
| 177 | SOBRE LOS ACTIVOS L.23760 |
| 178 | REG.PRES.ESPONT.DTO.1646/90 |
| 179 | PLAN FAC.PAGO DTO.1809/90 |
| 180 | IMPTO.S/BIENES PERSONALES |
| 181 | COMB LIQ L 23966 NAFTAS |
| 182 | GAS NATURAL L.23966 |
| 183 | EMERG.AUTOMOV.RURALES RG.3092 |
| 184 | COMBUST.LIQUIDOS DTO.2733/90 |
| 185 | GRAV.S/ENERGIA ELECT.DTO.2733 |
| 186 | ACTIVOS SOCIEDADES L.23905 |
| 187 | REG.RET.TRANSF.INM.P.F.23905 |
| 188 | REG.PRES.ESPONTAN.DTO.292/91 |
| 189 | REG.FAC.PAGO D.292/91 RG.3318 |
| 190 | SUSPENSION REG.PROM. L.23697 |
| 191 | ALICUOTA ADIC.DIVISAS Y B.EXT. |
| 192 | DIVISAS Y BS.EXTERIOR L.24073 |
| 193 | MONEDAS Y DIVISAS EN EXTERIOR |
| 194 | ACTIVOS UNIPERSONALES |
| 195 | PRES.ESPONTANEA DTO.631/92 |
| 196 | FACILIDADES PAGO D.631/92 |
| 197 | REINTEGRO IVA TURISTAS RG.3495 |
| 198 | F.PAGO PROM.IND.RG.3662 GAN |
| 199 | F.PAGO PROM.IND.RG.3662 IVA |
| 200 | F.PAGO PROM.IND.RG.3662 CAP |
| 201 | F.PAGO PROM.IND.RG.3662 P.NETO |
| 202 | F.PAGO PROM.IND.RG.3662 ACTIV |
| 203 | PRES.ESPONTANEA DTO.932/93 |
| 204 | FACILIDADES DE PAGO D.932/93 |
| 205 | REINTEGRO IVA DTO.937/93 |
| 206 | GANANCIAS RG.2793 |
| 207 | REG.RET.A LAS GANANCIAS |
| 208 | RET.GAN.RG2651-PRE-SICORE |
| 209 | REG.RET.A LAS GANANCIAS |
| 210 | GANANCIAS REG ESP INGR RG 830 |
| 211 | BP-ACCIONES O PARTICIPACIONES |
| 212 | RESP DEUDA AJENA BP - ACC O PA |
| 213 | REG.RET.A LAS GANANCIAS |
| 214 | FONDO SOLIDARIO REDISTRIBUCION |
| 215 | RET. SERV. COM. AUDIOVISUAL |
| 217 | SICORE-IMPTO.A LAS GANANCIAS |
| 218 | IMP.A LAS GAN.- BENEF.DEL EXT. |
| 219 | SICORE-IMPTO.S/ BS PERSONALES |
| 220 | PRESENTAC. DJ RET. Y/O PERCEP |
| 221 | PRESENT DJ COMBUSTIBLES LIQ |
| 224 | REG.RET.A LAS GANANCIAS |
| 226 | DEPOSITOS JUDICIALES |
| 228 | FONDO HIDRIC DE INFRAESTRUCTUR |
| 229 | RECARGO SOBRE EL GAS NATURAL |
| 230 | IVA RG.3298-JTA NAC DE GRANOS |
| 231 | PFP-D.1384/01 Z.DESASTRE-IMPOS |
| 232 | PFP-D.338/02 Z.DESASTRE-IMPOS |
| 235 | REG.FAC.PAGO GANANCIAS RG.4047 |
| 236 | REG.FACILIDADES PAGO RG.4047 |
| 237 | REG.FAC.PAGO BS.PERS.RG.4051 |
| 239 | INTERNOS- AUTOM Y MOTOR GASOIL |
| 240 | NAFTA FONDO HIDRICO DE INFR. |
| 241 | GAS,FONDO HIDRICO DE INFR. |
| 242 | TRANSFERENCIA DE INFORMACIÓN |
| 246 | INT.Y AJUSTES DEP.PLAZO FIJO |
| 248 | PRESENTAC.ESPONTANEA D.493/95 |
| 250 | MORATORIA DTO.963/95 |
| 251 | FACILIDADES PAGO DTO.1053/96 |
| 254 | IVA PRODUCTORES GANADO |
| 255 | IVA GANADO BOVINO RG 3125 |
| 256 | IVA COMPRAVTA GANADO RG3298 |
| 257 | IVA OPER.COMPRA-VENTA FAEN GAN |
| 258 | IVA OPER.COMP-VENTA PROD.YSUBP |
| 259 | IVA OPER.COMPRA-VENTA REDEST. |
| 260 | IVA C. VTA MAT FAENA GANADO |
| 261 | IVA USUARIOS FAENA BOVINO |
| 262 | IVA ESTABLECIMIENTO FAENADOR |
| 263 | IVA CONSIGNATARIOS DE HACIENDA |
| 264 | IVA SUPERMERCADOS |
| 265 | IVA CONSIGNATARIOS DE CARNE |
| 267 | IVA ESTAB FAENADOR PORCINO |
| 268 | IVA CONSIG HACIENDA PORCINO |
| 269 | IVA USUARIO FAENA PORCINO |
| 270 | CONTRIB.VALES ALIMENT.L.24700 |
| 293 | REGULARIZ DTO 793/94 |
| 300 | FAC.PAGO IVA IMP.DEF.BS.USO |
| 301 | EMPLEADOR-APORTES SEG. SOCIAL |
| 302 | APORTES OBRAS SOCIALES |
| 304 | ENTRADAS ESPEC.CINEMATOGRAFICO |
| 305 | IMPTO. S/VIDEOGRAMA GRABADOS |
| 306 | IMPTO.S/SERV.RADIODIFUSION TV. |
| 307 | IMPTO.S/RADIODIFUSION AM/FM |
| 308 | APORTES SEG.SOCIAL AUTONOMOS |
| 309 | PRESENTAC.ESPONTANEA RG.4043 |
| 310 | NORMALIZAC.TRIBUTARIA L 23495 |
| 311 | TRANSF.DE VALORES MOBILIARIOS |
| 312 | ASEG.RIESGO DE TRABAJO L 24557 |
| 313 | SERV. COMUNICACIÓN AUDIOVISUAL |
| 314 | SCA ART 96 INC A, D Y/O E. |
| 315 | SCA ART 96 INC B,C,F Y/O G |
| 318 | BENEF.EVENTUALES RET.INDIVID. |
| 319 | BENEF.EVENTUALES RET.GOBALES |
| 321 | APORTE MAGISTRADOS |
| 330 | IVA MERCADOS MAYORISTAS |
| 331 | REGIMEN DE FACTURACION RG 3419 |
| 340 | PFP.ESTAB.FAENADORES-IMPOSITIV |
| 341 | PFP-ESTAB.FAENADOR-SEG.SOCIAL |
| 348 | AFA-CLUBES DE FÚTBOL-DTO.1212 |
| 349 | PRES.ESPONTANEA DTO.271/95 |
| 350 | REVALUACION HACIENDA L.23079 |
| 351 | CONTRIBUCIONES SEG. SOCIAL |
| 352 | CONTRIBUCIONES OBRA SOCIAL |
| 353 | RETENCIONES CONTRIB.SEG.SOCIAL |
| 354 | APORTES Y CONTR.O.S. PRE-SIJP |
| 355 | REGIMEN FACILIDADES DE PAGO |
| 356 | PAMI AP/CONT ASIG NO REM D1273 |
| 357 | RNOS AP/CONT ASIG NO REM D1273 |
| 358 | CONTRIB.SEG.SOCIAL AUTONOMOS |
| 359 | FONDO TRANSIT.P/FINANC.L.23562 |
| 360 | CONTRIBUCION RENATEA |
| 361 | INTERNOS- TABACOS |
| 362 | INTERNOS-ALCOHOLES |
| 363 | INTERNOS-BEBIDAS ALCOHOL |
| 364 | INTERNOS-VINO CHAMPAGNE |
| 365 | INTERNOS-SEGUROS |
| 366 | ADICIONAL EMERG.CIGARRILLOS |
| 367 | INTERNOS-SERV TEL CEL Y SATEL |
| 368 | INTERNOS-CHAMPAÑAS |
| 369 | INTERNOS-VEHIC AUTOM EMBARC |
| 370 | F.1245 DDJJ PATRIMONIAL INT. |
| 371 | F.1246 DDJJ PATR.COMP.FLIAR |
| 374 | PLAN F. PAGO AUTONOM Y MONOTR |
| 375 | PFP AUTON Y MONOTR CONCURSADOS |
| 376 | MONOTRIB AUTONOMOS DEUDA SICAM |
| 377 | COM LIQ L.23966/24699 ART 2DOA |
| 380 | DTO.271/95 FORM.627 R.III |
| 381 | DTO.271/95 FORM.627 R.IV |
| 382 | DTO.271/95 FORM.627 R.V |
| 383 | REG.FACIL.PAGO DTO.493/95 F624 |
| 384 | PFP-D.1384/01-Z.DESAST-SEG.SOC |
| 385 | PFP-D.338/01-Z.DESASTRE-SEG.SO |
| 386 | SEGURIDAD SOCIAL |
| 387 | FAC.PAGO CONTRIBUC. L.24753 |
| 388 | FAC.PAGO APORTES L.24753 |
| 389 | FAC.PAGO AUTONOMOS L.24753 |
| 390 | SEGURIDAD SOCIAL |
| 391 | PFP-DTO2724 SEG.SOC.DEUDA 2002 |
| 392 | PFP-DTO2724 SEG.SOC.DEUDA 2003 |
| 394 | RAFA-IMPOSITIVO/CONTRIBUCIONES |
| 395 | COMB LIQ L 23966/24699 ART 2 B |
| 396 | COMBUSTIBLES LIQUIDOS IMPORTAD |
| 397 | COMB LIQ L 23966 GAS LICUADO |
| 398 | IMPUESTO S/GAS OIL |
| 399 | G.N.C. L.23966 |
| 400 | RAFA-SEG SOCIAL/APORTES |
| 401 | MANUF.CIGARRILLOS L.23562 |
| 402 | INTERNOS-MANUF TABACALES AFIN |
| 403 | INTERNOS-MANUF.TABACALES HOJAS |
| 405 | INTERNOS-IMPORT.TABACOS ELABOR |
| 408 | TABACOS/COMERCIALIZAC.TABACOS |
| 410 | ACOPIADORES DE TABACO |
| 413 | TABACOS/DESNAT. DE TABACOS |
| 414 | INTERNOS-DESEQ PROV S/CIGARR. |
| 415 | TABACOS/DEPOSITOS GRALES |
| 416 | MANUFACTURA DE CIGARRILLO |
| 417 | INTERNOS-DESTIL ALCOHOL INDUST |
| 418 | INTERNOS-DESTILADOR TANQUES |
| 419 | INTERNOS-DEST.SUBPR.ALCOH ETIL |
| 420 | INTERNOS-FRACCION.ALCOHOL ETIL |
| 421 | FRACCIONAM.PRODUCCION ALCOHOL |
| 426 | INTERNOS-FAB BEBIDAS DESTILADA |
| 427 | INTERNOS-ZONA LIBRE ALCOHOLERA |
| 428 | IMPORTADOR DE PERF A BASE DE A |
| 429 | IMPORTADOR ALCOHOL ETILICO |
| 430 | IVA DETERMIN.OFICIO RG. 3274 |
| 431 | INTERNOS-DESTILERIA SIST MIXTO |
| 432 | ALCOHOLES-COM.ALCOHOL ETILICO |
| 433 | ALCOHOLES-MANIP.ALCOHOL ETILIC |
| 434 | USUARIO ALCOHOL ETILICO |
| 435 | MANIPUL ALCOHOL ETILICO |
| 436 | ALCHOLES COMERCIALIZACION MAYO |
| 437 | USUARIO PRODUCTOS ALCOHOLICOS |
| 438 | CINTA TESTIGO DIGITAL |
| 439 | INFORME DELINSPECTOR-INF.TOTAL |
| 442 | USUARIO ALCOHOL EXENTO |
| 443 | I ALCOHOL FAB DESTIL |
| 444 | FABRICAC PERFUME A BASE DE ALC |
| 445 | ALCOHOLES-FRAC.ALCOHOL DESNAT. |
| 446 | ALCOHOLES FRAC ALC DESNAT |
| 447 | MANIPULADOR ALCOHOL DESNAT |
| 449 | INTERNOS-VEHIC. AUTOMOV MOTOR |
| 450 | INTERNOS-FAB.BEBIDAS ALCOHOLIC |
| 451 | INTERNOS-CERVEZAS |
| 452 | INTERNOS-FAB.BEB.ALCOHOL FERME |
| 453 | INTERNOS-IMPORT BEBIDA ALCOHOL |
| 454 | INTERNOS-IMPORT BEB.ALCOH FERM |
| 457 | INTERNOS-FRACC.BEBIDAS ALCOHOL |
| 458 | GRAV.S/ENERGIA ELECT.LEY 17574 |
| 459 | INTERNOS-CIAS.SEGUROS NACIONAL |
| 460 | INTERNOS-SEGUR CONTRATADOS EXT |
| 461 | INTERNOS-OTROS BIENES Y SERVIC |
| 462 | INTERNOS-ACEITES LUBRICANTES |
| 463 | ADICION.ACEITES LUBRICANTES |
| 464 | GRAV PETROLEO CRUDO PROCESADO |
| 465 | COMBUSTIBLES AERONAVES |
| 466 | SICORE-PREMIOS JUEGOS Y C.DEP |
| 467 | INTERNOS-VINOS/BODEGUEROS |
| 468 | PAGO CONTRIBUCIONES AGP |
| 469 | INTERNOS-FABRIC VINOS POSTRE |
| 470 | INTERNOS-FABR VINOS COMPUESTOS |
| 471 | INTERNOS-FABR VINOS ESPUMOSOS |
| 473 | INTERNOS-FABRICANTES CHAMPAGNE |
| 474 | INTERNOS-VINOS INTERMEDIARIOS |
| 475 | INTERNOS-VINOS IMPORTADORES |
| 476 | INTERNOS-VINOS CORTADORES |
| 477 | INTERNOS-VINOS FRACCIONADORES |
| 478 | GRAVAMEN SERV.AUXIL.NAVEGACION |
| 479 | INTERNOS-SOBRETASA VINO |
| 480 | INTERNOS-ARTICULOS DE TOCADOR |
| 481 | INTERNOS-OBJETOS SUNTUARIOS |
| 482 | INTERNOS-CUBIERTAS |
| 483 | FONDO NAC.VIALIDAD-CUBIERTAS |
| 484 | FON.NAC.COMPLEMENT.VIALIDAD |
| 485 | INTERNOS-BEB.ANALCOHOL JARAB |
| 486 | GRAV ENERGIA ELECTRICA |
| 487 | GRAV PETROLEO CRUDO PROCESADO |
| 488 | CPRA/VTA. DE DIVISAS L.18526 |
| 489 | FONDO DE ASIST. A LOS MEDICAM. |
| 490 | GRAV ENERGIA ELECTRICA L 15336 |
| 491 | TRANSF.COMBUSTIBLES LIQUIDOS |
| 492 | INTERNOS MOTONAFTA, ALCONAFTA |
| 493 | INTERNOS GAS L.23549 |
| 494 | INTERNOS -SERVICIO TELEFONICO |
| 495 | APUESTAS DE CARRERAS L.11242 |
| 496 | FONDO.NAC.AUTOPISTAS L.18408 |
| 497 | GRAV GAS NATURAL L 16656 |
| 498 | SELLOS LEY 11290 |
| 499 | DEPOSITO ACTA FISC. LEY 18820 |
| 582 | TRANSFERENCIA DE DIVISAS |
| 724 | REGIMEN REGULARIZ VOLUNT 26970 |
| 727 | GANANCIAS ADUANA |
| 728 | IVA RETENCIONES GLOB.ADUANA |
| 729 | IVA ADUANA |
| 730 | OPERADORES RG 3569 |
| 731 | IVA GANADO PORCINO |
| 732 | REG.PAGO A CUENTA IVA SALONES |
| 733 | IVA RESTAURANTES |
| 734 | REG PAGO A CUENTA-IVA GARAGES, |
| 735 | IVA RETENCIONES |
| 736 | RETENCION RESTAURANTES HOTELES |
| 737 | PAGO A CUENTA-IVA |
| 738 | IVA POLLOS PARRILLEROS |
| 739 | IVA CAL Y CEMENTO |
| 740 | EXT.TENENCIA M.E.LEY N° 26.860 |
| 741 | INGRESO A CTA RET Y PERCEP IVA |
| 760 | IVA HARINAS Y DERIV DE TRIGO |
| 761 | PRESENTAC.ESPONTANEA RG.3962 |
| 767 | SICORE-IMPTO.AL VALOR AGREGADO |
| 770 | DERECHOS DE EXPORTACION |
| 771 | DERECHOS DE IMPORTACION |
| 772 | TASA ESTADISTICA- ADUANA |
| 773 | TASA  EQUIP.PRECIOS-ADUANA |
| 774 | DERECHOS ANTIDUMPING-ADUANA |
| 775 | TASA SERV EXTRAORD.-ADUANA |
| 776 | TASA COMPROBACION-ADUANA |
| 777 | OTRAS TASAS-ADUANA |
| 778 | FONDO NAC MARINA MERCAN-ADUANA |
| 779 | INTA-ADUANA |
| 780 | INTI-ADUANA |
| 781 | INFRACCIONES LEY 22415 |
| 782 | DOCUMENTO ELECTRONICO ADUANERO |
| 783 | RÉG.APLICACIÓN FONDOS EXT. |
| 785 | PRESENT. DJ SIRE IMPOSITIVO |
| 786 | ART TRAB. CASAS. PARTI. |
| 787 | RET ART 79 LEY GCIAS INC A,BYC |
| 830 | IVA ADUANA |
| 831 | IVA PERCEPCIONES ADUANA |
| 832 | INTERNOS NACIONALES-ADUANA |
| 833 | TABACOS/ADUANA |
| 834 | A LOS COMBUSTIBLES ADUANA |
| 835 | GANANCIAS RETENCIONES EXCEPTO |
| 871 | PRESENT.DJ REASIG. DE SALDOS |
| 935 | RENATEA |
| 936 | DACIÓN EN PAGO DE ESP.PUBLICI. |
| 945 | APORTES TRAB. CASAS PARTI. |
| 946 | CONTRIB. TRAB. CASAS PARTI. |
| 947 | OBRA SOCIAL TRAB. CASAS PARTI. |
| 951 | APORTES EX-CAJAS PROV./MUNICIP |
| 966 | REG.SEG.SOCIAL-AUTONOMOS |
| 967 | CONV.GREMIAL-AFA |
| 968 | ACTAS DE FISCALIZACION-ANSES |
| 969 | ANSES PAGO MORATORIA Y EMPLEAD |
| 970 | CONV.GREMIAL-ALGODONERA |
| 971 | CAJA SUBS.FAM.PERS.INDUSTRIA |
| 972 | SUBSIDIO FLIARES.PERS.COMERCIO |
| 973 | CAFPE ACT.MARIT.FLUV.Y DE INDU |
| 974 | ANSES FAC.PAGO OBRAS SOCIALES |
| 976 | DEUDAS PREV.FAC.PAGO D.933/93 |
| 977 | CONV.GREMIAL-AZUCARERA |
| 978 | CONV.GREMIAL-CEREALERO |
| 979 | CONV.DE C.GREMIAL-LANERO |
| 980 | CONV.DE C.GREMIAL-TABACALERO |
| 981 | CONV.DE C.GREMIAL-GANADERO |
| 982 | CONV.DE C.GREMIAL-VIÑATERO |
| 983 | CONV.GREMIAL-CEREALERO(GRUESA) |
| 984 | CONV.C.GREMIAL-FORESTAL CHACO |
| 985 | FAC.PAGO PREVISIONALES RG.3762 |
| 986 | FAC.PAGO OBRA SOCIALES |
| 987 | FAC.PAGO ASOC.SINDICALES O.S. |
| 988 | PLAN FAC.DE PAGO AUTONOMOS |
| 989 | F.PAGO PREVISIONAL DTO.1164/93 |
| 990 | MORATORIA AUTONOMOS RES.421/85 |
| 991 | APORTES PREVIS.TESORO GRAL. |
| 992 | MORAT.EMPLEADORES RES.420/85 |
| 993 | MORATORIA RES.86/90 INPS |
| 994 | MORATORIA RES.174-158/91 |
| 995 | MORATORIA RES.271/89 |
| 996 | ANSES DISTRIBUCION SECUNDARIA |
| 997 | SUSS DTO.2284/91 EMPLEADORES |
| 998 | REG.NACIONAL OBRAS SOCIALES |
| 1012 | ARANCELES DE OFICIO |
| 1013 | ARANCELES E INGRESOS VARIOS |
| 2010 | DERECHOS DE IMPORTACION |
| 2011 | TASA DE ESTADISTICA |
| 2012 | DERECHOS ANTIDUMPING 1 |
| 2013 | DERECHO COMPENSATORIO |
| 2014 | IMPUESTO EQUIP. DE PREC. |
| 2015 | DERECHO ESPECIFICO |
| 2016 | SUMA AD.TEM. D1330-04 |
| 2017 | DERECHO ANTIDUMPING 2 |
| 2018 | DER.IMP.AJ.EQ.PRE.1 |
| 2019 | DERECHO COMPENSATORIO (2) |
| 2020 | DERECHOS DE EXPORTACION |
| 2021 | DERECHOS EXPO.INT.RESARCITORIO |
| 2022 | DERECHOS EXPO.INT.PUNITORIO |
| 2023 | DERECHOS EXPO. OTROS INTERESES |
| 2024 | DERECHOS DE EXPORTACION CUEROS |
| 2025 | DER.IMP.COMPRAS PROV.EXTERIOR |
| 2026 | DERECHOS EXPORTACION ADICIONAL |
| 2027 | DER. ADIC. EXPO RES 61/07 MEP |
| 2028 | CTA.RECEXC.DTO904/08 |
| 2029 | PAGO 90% EN DJVE |
| 2030 | SUMA AD. NAC. DE. 1330-04 |
| 2031 | TASA DE COMPROBACION |
| 2032 | TASA LEY 24196 |
| 2033 | MULTA ARR. FUERA TER. |
| 2034 | DIEM-SALVAG. |
| 2035 | INT. RESARC. IMPORTACION |
| 2036 | INT. PUNITOR.IMPORTACION |
| 2037 | OTROS INT. IMPORT. |
| 2040 | FDO.GRAT.LEY 23993 |
| 2041 | MULTA DEST. FUERA TER. |
| 2042 | MULTA GRAL. F. DOC. COMP. |
| 2043 | VARIOS |
| 2044 | FDO. JER. LEY 23993 |
| 2046 | MULTA NO TOMAR CONT. |
| 2047 | MULTA FALTA DOC. COMP. |
| 2048 | MULTA TRANS. ART. 320 |
| 2049 | DTO. 258 PROD. EF. Y FISC. |
| 2050 | D.A-DUMP 1/MERCOSUR |
| 2051 | D.A-DUMP 2/MERCOSUR |
| 2052 | I. EQUIP. PRECIOS MERC |
| 2053 | D.I. AJ. EQ. PR. MERC. 1 |
| 2054 | DER. IMP. AJ. EQ. PRE. 2 |
| 2055 | DER. IMP. AJ. EQ. PRE. 2 MERC |
| 2056 | DER. IMP. USADOS R.909/94 |
| 2057 | DER. IMP. USADOS R.12/98 |
| 2058 | DER. ANTIDUMP. AD. VALOR |
| 2059 | DER. ESPECIF. OMC |
| 2060 | DER. ESPECIF. CALZADO |
| 2061 | TASA ESTAD. MONTO MAX. |
| 2062 | TASA ESTAD. MONTO MAX.2 |
| 2063 | MULTA FALTA DOC. COMP. |
| 2064 | MULTA DES. FUERA TER. |
| 2065 | DIEM - CHINA |
| 2066 | TASA REDUCIDA |
| 2101 | GARANTIAS BUENOS AIRES |
| 2103 | GARANTIAS BAHIA BLANCA |
| 2104 | GARANTIAS BARILOCHE |
| 2108 | GARANTIAS CAMPANA |
| 2110 | GARANTIAS BARRANQUERAS |
| 2111 | BONOS ADUANEROS |
| 2112 | GARANTIAS CLORINDA |
| 2113 | GARANTIAS COLON |
| 2114 | GARANTIAS COMODORO RIVADAVIA |
| 2115 | GARANTIAS CONC.DEL URUGUAY |
| 2116 | GARANTIAS CONCORDIA |
| 2117 | GARANTIAS CORDOBA |
| 2118 | GARANTIAS CORRIENTES |
| 2119 | GARANTIAS PUERTO DESEADO |
| 2120 | GARANTIAS DIAMANTE |
| 2123 | GARANTIAS ESQUEL |
| 2126 | GARANTIAS GUALEGUAYCHU |
| 2129 | GARANTIAS IGUAZU |
| 2131 | GARANTIAS JUJUY |
| 2133 | GARANTIAS LA PLATA |
| 2134 | GARANTIAS LA QUIACA |
| 2137 | GARANTIAS MAR DEL PLATA |
| 2138 | GARANTIAS MENDOZA |
| 2140 | GARANTIAS NECOCHEA |
| 2141 | GARANTIAS PARANA |
| 2142 | GARANTIAS PASO DE LOS LIBRES |
| 2145 | GARANTIAS POCITOS |
| 2146 | GARANTIAS POSADAS |
| 2147 | GARANTIAS PUERTO MADRYN |
| 2148 | GARANTIAS RIO GALLEGOS |
| 2149 | GARANTIAS RIO GRANDE |
| 2152 | GARANTIAS ROSARIO |
| 2153 | GARANTIAS SALTA |
| 2154 | GARANTIAS SAN JAVIER |
| 2155 | GARANTIAS SAN JUAN |
| 2157 | GARANTIAS SAN LORENZO |
| 2158 | GAR.S.MARTIN DE LOS ANDES |
| 2159 | GARANTIAS SAN NICOLAS |
| 2160 | GARANTIAS SAN PEDRO |
| 2161 | GARANTIAS SANTA CRUZ |
| 2162 | GARANTIAS SANTA FE |
| 2166 | GARANTIAS TINOGASTA |
| 2167 | GARANTIAS USHUAIA |
| 2169 | GARANTIAS VILLA CONSTITUCION |
| 2173 | GARANTIAS EZEIZA |
| 2174 | GARANTIAS TUCUMAN |
| 2175 | GARANTIAS NEUQUEN |
| 2176 | GARANTIAS ORAN |
| 2178 | GARANTIAS SAN RAFAEL |
| 2179 | GARANTIAS LA RIOJA |
| 2180 | GARANTIAS SAN ANTONIO OESTE |
| 2182 | GARANTIAS BERNARDO DE IRIGOYEN |
| 2183 | GARANTIAS SAN LUIS |
| 2184 | GARANTIAS SANT0 TOME |
| 2186 | GARANTIAS OBERA |
| 2187 | GARANTIAS CALETA OLIVIA |
| 2188 | GARANTIAS GENERAL DEHEZA |
| 2189 | GARANTIAS SANTIAGO DEL ESTERO |
| 2210 | DER. IMPOR. AAE |
| 2217 | IMP. INTERNOS AAE |
| 2285 | VALOR EN AD. AAE |
| 2286 | VALOR EN AD. A PAG. |
| 2300 | CUENTA UNICA MNA |
| 2301 | MNA BUENOS AIRES |
| 2303 | MNA BAHIA BLANCA |
| 2304 | MNA BARILOCHE |
| 2308 | MNA CAMPANA |
| 2310 | MNA BARRANQUERAS |
| 2312 | MNA CLORINDA |
| 2313 | MNA COLON |
| 2314 | MNA COMODORO RIVADAVIA |
| 2315 | MNA CONCEPCION DEL URUGUAY |
| 2316 | MNA CONCORDIA |
| 2317 | MNA CORDOBA |
| 2318 | MNA CORRIENTES |
| 2319 | MNA PTO DESEADO |
| 2320 | MNA DIAMANTE |
| 2323 | MNA ESQUEL |
| 2324 | MNA FORMOSA |
| 2325 | MNA GOYA |
| 2326 | MNA GUALEGUAYCHU |
| 2329 | MNA IGUAZU |
| 2331 | MNA JUJUY |
| 2333 | MNA LA PLATA |
| 2334 | MNA LA QUIACA |
| 2337 | MNA MAR DEL PLATA |
| 2338 | MNA MENDOZA |
| 2340 | MNA NECOCHEA |
| 2341 | MNA PARANA |
| 2342 | MNA PASO DE LOS LIBRES |
| 2345 | MNA POCITOS |
| 2346 | MNA POSADAS |
| 2347 | MNA PTO MADRYN |
| 2348 | MNA RIO GALLEGOS |
| 2349 | MNA RIO GRANDE |
| 2352 | MNA ROSARIO |
| 2353 | MNA SALTA |
| 2354 | MNA SAN JAVIER |
| 2355 | MNA SAN JUAN |
| 2357 | MNA SAN LORENZO |
| 2358 | MNA SAN MARTIN DE LOS ANDES |
| 2359 | MNA SAN NICOLAS |
| 2360 | MNA SAN PEDRO |
| 2361 | MNA SANTA CRUZ |
| 2362 | MNA SANTA FE |
| 2366 | MNA TINOGASTA |
| 2367 | MNA USHUAIA |
| 2369 | MNA VILLA CONSTITUCION |
| 2373 | MNA EZEIZA |
| 2374 | MNA TUCUMAN |
| 2375 | MNA NEUQUEN |
| 2376 | MNA ORAN |
| 2378 | MNA SAN RAFAEL |
| 2379 | MNA LA RIOJA |
| 2380 | MNA SAN ANTONIO OESTE |
| 2382 | MNA BERNARDO DE IRIGOYEN |
| 2383 | MNA SAN LUIS |
| 2384 | MNA SANTO TOME |
| 2385 | MNA VA REGINA |
| 2386 | MNA OBERA |
| 2387 | MNA CALETA OLIVIA |
| 2388 | MNA GENERAL DEHEZA |
| 2389 | MNA SANTIAGO DEL ESTERO |
| 2414 | IVA INTERESES RESARCITORIOS |
| 2415 | IVA |
| 2416 | IVA INTERESES FINANCIEROS |
| 2417 | IMPUESTOS INTERNOS |
| 2418 | IMP. TRANSF. GASOIL |
| 2419 | IMP. INT. CIGARRILLOS |
| 2420 | IVA DEV. REINT.REE |
| 2421 | IMP.COMBUST.LIQUIDOS |
| 2422 | IVA ADICIONAL INSCR. |
| 2423 | IVA ADICIONAL NO INSCR. |
| 2424 | IMP. A LAS GANANCIAS |
| 2425 | IVA DEV. REINT. REEM |
| 2426 | INFRAESTRUC.HIDRICA |
| 2427 | IMP.INT. L24699 ART.3 |
| 2428 | I.COMB.LIQ. L24699 2 |
| 2429 | IIBB BUENOS AIRES |
| 2430 | ANT.IMP.GANANCIAS EXPORTACION |
| 2433 | IVA AD NOINS NOCVDI |
| 2434 | IMP. INT. DEC.290/00 |
| 2435 | I.COMB.LIQ.ADVALOREM |
| 2436 | I.COMB.LIQ.L24699 ADVA |
| 2437 | IMP.INT.CIGARR.MAX. |
| 2438 | IMP.INT.CIGARR.MIN. |
| 2439 | INFRAEST.HID.ADVALOR |
| 2440 | AFIP L 23993 ART. 2C |
| 2441 | GENDARMERIA NACIONAL 2 C |
| 2442 | PREFECTURA N ARG. 2C |
| 2443 | POLICIA FEDERAL ARGENTINA 2 C |
| 2444 | POL. AERONAUTICA NAC. |
| 2445 | GEO FSEG.DTO.258/99 |
| 2449 | INGRESOS BRUTOS - CTA.PTE. |
| 2450 | IIBB CIUDAD BUENOS AIRES |
| 2452 | IIBB CORDOBA |
| 2453 | IIBB CORRIENTES |
| 2455 | IIBB PROVINCIA CHUBUT |
| 2464 | IIBB RIO NEGRO |
| 2467 | IIBB SAN LUIS |
| 2468 | IIBB SANTA CRUZ |
| 2471 | IIBB TIERRA DEL FUEGO |
| 2472 | IIBB TUCUMAN |
| 2473 | IM.TRA.GASOIL L26325 |
| 2474 | IM.INT.AUTOM.L24674 |
| 2499 | AD. FONDOS POR DISTRIBUIR |
| 2500 | ARANCEL SIM IMPO |
| 2501 | ARANCEL SIM EXPO |
| 2502 | FACT-CONVERGENCIA(I) |
| 2505 | DEVOLUCION FC (E) |
| 2506 | DEVOLUCION FC (I) |
| 2509 | ARANCEL UNICO SERVICIOS ADUA. |
| 2510 | INTERESES ARANC.UNI.SERV.ADUA. |
| 2511 | TASA AEROP. SERV. ADUAN. |
| 2512 | MULTA AUSA |
| 2513 | TASA AEROP.SERV.ADUAN.INTERES |
| 2515 | ARANCEL DECLARACIONES SUMARIAS |
| 2516 | INT. ARANCEL DECL. SUMARIAS |
| 2517 | ARANC.UNI.SUSE |
| 2518 | SUSE INTERESES |
| 2519 | MULTA SUSE |
| 2521 | SERV. DE GUARDA Y DIG.(LAKAUT) |
| 2522 | REINT.GASTOS ADM. INF. |
| 2523 | INT.RES.DEST.FUE.TER. |
| 2524 | INT.PUN.DEST.FUE.TER. |
| 2525 | O.INT.M.DEST.FUE.TER. |
| 2530 | INT. PUNITORIO IVA |
| 2531 | INT. RESARCITORIO ESTADISTICA |
| 2532 | INT. PUNITORIO ESTADISTICA |
| 2533 | INT. RESARCITORIOS GANANCIAS |
| 2534 | INT. PUNITORIOS GANANCIAS |
| 2535 | INT. RES. MULTA FALTA DOC.COMP |
| 2536 | INT. PUN. MULTA FALTA DOC.COMP |
| 2537 | INT. RES. IMPUESTOS INTERNOS |
| 2538 | INT. PUN. IMPUESTOS INTERNOS |
| 2539 | INT. RES. LEY 24196 |
| 2540 | INT. PUN. LEY 24196 |
| 2541 | INT. RES. TASA COMP.DESTINO |
| 2542 | INT. PUN. TASA COMP.DESTINO |
| 2551 | SERV.DE GUARDA Y DIG. (DASA) |
| 2555 | ANTIC. PAGO TRIBUTOS ADUANEROS |
| 2556 | PAGO DE GARANTES |
| 2700 | HONO. ABOG. Y PERITOS - ADUANA |
| 2710 | D.I. CERT.DES. |
| 2802 | FACT-CONVER.IMPO (G) |
| 2803 | FACT-CONVER.AAE (G) |
| 2819 | IMP.INT.CIGARR (G) |
| 2820 | DER.SALV.INTR. (G) |
| 2821 | IVA.SALV.INTR. (G) |
| 2822 | IVA AD.SALV.INTR. (G) |
| 2823 | GCIAS.SALV.INTR (G) |
| 2824 | I.INT.SALV.INTR (G) |
| 2849 | DEVOL.BENEFICIOS (G) |
| 2850 | FALTA TIT.TRANSPORTE (G) |
| 2851 | ESTADISTICA (G) |
| 2852 | IVA (G) |
| 2853 | IMP.INTERNOS (G) |
| 2854 | IVA ADIC.INSCR (G) |
| 2855 | IVA ADIC.NO INSC (G) |
| 2856 | IMP.GANANCIAS(G) |
| 2857 | DER.ANTI-DUMP 1 (G) |
| 2858 | DER.ANTI-DUMP 2 (G) |
| 2859 | IMP.INT.A-DUMP 1 (G) |
| 2860 | IVA ANTIDUMPING (G) |
| 2861 | IVA ADI.R.I DUMP. (G) |
| 2862 | IVA ADI.R.N.I DUM. (G) |
| 2863 | IMP.GCIAS.DUMP. (G) |
| 2864 | D.A-DUMP1 MERCO. (G) |
| 2865 | D.A-DUMP2 MERCO. (G) |
| 2866 | DER.IMPORTACION (G) |
| 2867 | DER.COMPENSATOR (G) |
| 2868 | I.EQ.DE PRECIOS (G) |
| 2869 | DER.ESPECIFICO (G) |
| 2870 | DER.IMP.ADICIONAL(G) |
| 2871 | DER.EXPORTACION (G) |
| 2872 | TASA COM.DESTINO (G) |
| 2873 | I.V.A. INTERESES (G) |
| 2874 | IMP.COMB.LIQUID (G) |
| 2882 | MULTA RES 763/305 |
| 2883 | MULTA F. CERT. INSP. |
| 2884 | D.I. USAD.R.12/98 (G) |
| 2885 | VALOR EN ADUANA |
| 2886 | D.I. USAD.G.R.909/94 |
| 2887 | I.INT.L 24699 A.3 (G) |
| 2889 | I.C.LIQ.L24699 2 (G) |
| 2891 | DIEM-CHINA (G) |
| 2892 | DIEM IVA (G) |
| 2893 | DIEM IVAAD (G) |
| 2894 | DIEM IMP GCIAS (G) |
| 2895 | DIF DIEM OMC (G) |
| 2896 | DIF DIEM CHINA (G) |
| 2897 | DIF DIEM DI (G) |
| 2898 | IMP.INT.AUTL24674 (G) |
| 2899 | D.ANTIDUM.AD-VALOR (G) |
| 2900 | CUENTA UNICA |
### Conceptos
| **id** | **desc** |
|---|---|
| 3 | INFORMACION NO TRIBUTARIA |
| 4 | DNPYA  PERMISOS Y PARTES DE PESCA. |
| 7 | INTERESES ACREDITACIONES TARDÍAS |
| 8 | MULTA RENDICIONES TARDÍAS |
| 9 | INFORME ESPECIAL DE CONTADOR PÚBLICO |
| 10 | OP.SUJETOS NO RESID. A TRAVÉS DE ENT. FINANCIERAS LOCALES |
| 12 | EXENCION EN EL  IMPUESTO A LAS GANANCIAS |
| 19 | DECLARACIÓN JURADA |
| 26 | PAGO A CUENTA EMPRESAS TELEFÓNICAS |
| 27 | PAGO A CUENTA |
| 28 | PAGO A CUENTA JUGADORES DE FÚTBOL TÍTULO III CAPÍTULO A |
| 29 | PAGO A CUENTA JUGADORES DE FÚTBOL TÍTULO III CAPÍTULO B |
| 30 | RETENCION S/OP CON ACC QUE NO COTIZAN EN BOLSA |
| 31 | PAGO A CUENTA JUGADORES DE FÚTBOL TÍTULO III CAPÍTULO C |
| 33 | REGIMEN INFORMATIVO DE COMPRAS DE MATERIALES A RECICLAR |
| 35 | CUOTA PLAN |
| 36 | AJUSTE PRESUNTO POR FISCALIZACION LEY 26.476 |
| 40 | PAGO ANTICIPADO CON REINTEGRO |
| 41 | MENSUALIDAD |
| 42 | CÓD INTERNO SDO A FAVOR PLANES JERÓNIMOS REFORMULADOS DTO 93 |
| 43 | PAGO A CUENTA AUTORRETENCIÓN/AUTOPERCEPCIÓN |
| 44 | IVA POR PRESTACIONES DEL EXTERIOR |
| 47 | REGIMEN DE ADUANA EN FACTORIA DECRETO 688/02 |
| 48 | REGIMEN EXCEPCIONAL DE INGRESO - ARTICULO 4 RG N°3818 |
| 49 | COOPERATIVAS Y MUTUALES DEPÓSITOS AHORRO A TÉRMINO Y SALDOS |
| 50 | REG. INF. DE REORG. DE SOC. Y EMPRESAS-AUTORIZACION PREVIA |
| 51 | INTERESES RESARCITORIOS |
| 53 | CADUCIDADES |
| 54 | ARTICULO 27° INCISO C) - ADICIONAL 5% - LEY 26.476 |
| 55 | LEY 26.476 - ARTICULO 3 - RG 2609 - 2% |
| 74 | AJUSTES ADMINISTRATIVOS PAGOS BANCARIOS - REMOTOS |
| 75 | ACUERDO PAGO A CUENTA |
| 76 | REGIMEN INFORMATIVO DE COMBUSTIBLES DESTINO INDUSTRIAL |
| 77 | ARTICULO 27° INCISO A) LEY 26.476 |
| 78 | AJUSTES |
| 79 | ARTICULO 27° INCISO B) LEY 26.476 |
| 80 | DEVOLUCIÓN POR NACIONALIZACIÓN DE VEHICULOS - LEY N° 19.486 |
| 81 | ARTICULO 27° INCISO C) LEY 26.476 |
| 82 | ARTICULO 27° INCISO D) LEY 26.476 |
| 83 | ARTICULO 27° INCISO E) LEY 26.476 |
| 86 | BOLETA DE DEUDA |
| 90 | REPOSICIÓN DE TOKEN |
| 91 | COMISIONES POR SERVICIOS DE RECAUDACIÓN |
| 94 | INTERESES PUNITORIOS |
| 96 | AFIP-DGI TARJETAS DE CRÉDITO OPERACIONES CON EL EXTERIOR |
| 97 | TARJETAS DE DÉBITO OPERACIONES EN EL EXTERIOR |
| 98 | INFORMACION DE CUENTAS FINANCIERAS DE NO RESIDENTES |
| 102 | EMERGENCIA AGROPECUARIA DECRETO 33/09 |
| 103 | ONCCA CONSULTA SOBRE ESTADO DE DEUDA |
| 104 | RÉGIMEN INFORMATIVO MODELOS |
| 108 | MULTA |
| 109 | HONORARIOS DEFENSOR PÚBLICO OFICIAL |
| 110 | DTO.N° 1214/05 - INSCRIPCION DE IMPORTADORES Y EXPORTADORES |
| 111 | R.G. 1469 - SUSTITUCION MEDIDAS CAUTELARES IMP./EXPORT. |
| 113 | DECR.1001/82,ART 4° PUNTO 1, INC.B) GAR. ACT DESP ADUANA |
| 114 | DECR 1001/82 ART. 6° INC A)GARANT ACT. AG. TRANSP. ADUANERO |
| 115 | DECR 1001/82 ART. 57 GARANTÍA ACTUAC OPERADOR CONTENEDORES |
| 116 | DD.JJ DETERM. DE SALDO SIN INTERVENCIÓN AG. BOLSA |
| 117 | RG 7/97(AFIP) GARANTÍA DE ACTUAC TRANSPORT  TRANSP INTERIOR |
| 118 | ART 208 INC.D) CÓD ADUAN. AG POSEEN DEPÓSITOS FISC HABILITAD |
| 119 | EMPR AUTORIZ OPERAR BAJO REGÍM PREVISTOS RG 596 Y 1673(AFIP) |
| 120 | R.G. 2665 ATA OPERADOR LOGISTICO SEGURO |
| 121 | R.G. 2665 TRANSPORTISTA OPERADOR LOGISTICO SEGURO |
| 122 | R.G 2721 PRESTADOR DE SERVICIOS DE ARCHIVOS Y DIGITALIZACION |
| 123 | LEY 26457 INCENTIVO FABRIC. MOTOS DESGRAVACION ARANCELARIA |
| 124 | NOTA INFORMATIVA RG 2784 |
| 125 | LEY 26457 INCENTIVO FABRICACION MOTOS BONO FISCAL |
| 127 | LEY 26457 RES 11/2010 SICPYME ART 17 2° PARR - DESG. ARANC |
| 128 | LEY 26457 RES 11/2010 SICPYME ART 17 2° PARR - BONO FISCAL |
| 129 | PRESTADOR DE SERVICIOS POSTALES COURIER SEGURO |
| 130 | PRESTADOR DE SERVICIOS ISTA RG N° 3206 |
| 131 | PRESTADOR DE SERVICIOS DE ESCANEO RG N° 3249 |
| 132 | DD.JJ DETERMINATIVA DE SALDO C/ INTERV. AG. BOLSA |
| 133 | CONTRIBUCIÓN DIFERENCIAL DE SEGUROS Y BANCOS |
| 134 | CONTRIBUCIÓN DIFERENCIAL COMPANÍAS DE SEGURO |
| 135 | CONTRIBUCIÓN DIFERENCIAL DGI ADUANA |
| 137 | RÉGIMEN INFORMATIVO DE INSTRUMENTOS FINANCIEROS DERIVADOS |
| 138 | FACTURA ELECTRÓNICA-REGIMEN DE INFORMACIÓN DE OPERACIONES |
| 139 | SIST.DE REGISTROS Y ACT. DEDUC. DEL IMP. A LAS GANANCIAS |
| 140 | MULTA AUTOMATICA |
| 141 | ACTA DE INSPECCIÓN 1 |
| 142 | ACTA DE INSPECCIÓN 2 |
| 143 | ACTA DE INSPECCIÓN 3 |
| 144 | ACTA DE INSPECCIÓN 4 |
| 145 | ACTA DE INSPECCIÓN 5 |
| 146 | ACTA DE INSPECCIÓN 6 |
| 147 | ACTA DE INSPECCIÓN 7 |
| 148 | ACTA DE INSPECCIÓN 8 |
| 149 | ACTA DE INSPECCIÓN 9 |
| 150 | ACTA DE INSPECCIÓN 10 |
| 151 | REINTEGRO MALLA ANTIGRANIZO |
| 152 | REGIMEN ESPECIAL MINERIA |
| 159 | REINTEGRO POR CANCELACIÓN DE INSCRIPCIÓN |
| 167 | SEG SOC RG 1566 MULTAS POR MORA |
| 168 | SEG SOC RG 1566 MULTA P/INCUMPL OMISIONES ETC EXCEPTO MORA |
| 173 | SALIDA Y ADMISIÓN TEMPORAL DE VEHÍCULOS EN ALQUILER (ENYSA) |
| 178 | CUOTA PRESENTACIÓN ESPONTÁNEA DTO. 1646/90 |
| 179 | CUOTA RÉGIMEN PLAN DE FAC. DE PAGO DTO. 1809/90 |
| 183 | CUOTA ANTICIPO |
| 191 | ANTICIPOS |
| 192 | ANTICIPOS PERSONAS FISICAS |
| 193 | OPCIÓN RESOLUCIÓN GENERAL 3646 |
| 194 | OPCIÓN RESOLUCIÓN GENERAL 3683 |
| 195 | PAGO A CUENTA FERIA FISCAL |
| 197 | EMISIÓN DE OBLIGACIONES NEGOCIABLES |
| 198 | SALIDAS NO DOCUMENTADAS |
| 199 | DJ INFORMATIVA DE MONOTRIBUTO |
| 209 | INFORME INSPECTOR |
| 211 | REGIMEN DE INFORMACIÓN DE OPERACIONES DE COMPRAS Y VENTAS |
| 213 | CUOTA DECRETO  271/89 |
| 214 | LEY 25988-INVERSIONES BIENES DE CAPITAL-NUEVAS INVERSIONES |
| 222 | 1ER.PAGO PARCIAL DE CUOTA |
| 223 | 2DO.PAGO PARCIAL DE CUOTA |
| 224 | 3ER.PAGO PARCIAL DE CUOTA |
| 225 | 4TO.PAGO PARCIAL DE CUOTA |
| 226 | 5TO.PAGO PARCIAL DE CUOTA |
| 227 | 6TO.PAGO PARCIAL DE CUOTA |
| 228 | 7MO.PAGO PARCIAL DE CUOTA |
| 229 | 8VO.PAGO PARCIAL DE CUOTA |
| 230 | 9NO.PAGO PARCIAL DE CUOTA |
| 231 | 10MO.PAGO PARCIAL DE CUOTA |
| 232 | 11MO.PAGO PARCIAL DE CUOTA |
| 233 | 12MO.PAGO PARCIAL DE CUOTA |
| 234 | 13MO.PAGO PARCIAL DE CUOTA |
| 235 | 14TO.PAGO PARCIAL DE CUOTA |
| 236 | 15TO.PAGO PARCIAL DE CUOTA |
| 237 | 16TO.PAGO PARCIAL DE CUOTA |
| 238 | 17MO.PAGO PARCIAL DE CUOTA |
| 239 | 18VO.PAGO PARCIAL DE CUOTA |
| 240 | DEVOLUCIÓN DE BONOS |
| 248 | DETERMINACIÓN DE INFRACCIÓN |
| 249 | DECLARACION HISTORICA PSP/COURIER |
| 251 | DECLARACION PARA CANCELAR TEMPORALES DE IMPORTACION |
| 252 | SOLICITUD PARA TRAMITES Y/OCONCSULTAS DE INDOLE ADUANERA |
| 253 | SOLICITUD DE DESTINACIÓN SIMPLIFICADA PSP/COURIER |
| 260 | LIQUIDACION ORIGINARIA-ADUANA |
| 261 | LIQUIDACION SUPLEMENTARIA-ADUANA |
| 264 | CUOTA DTO. 2413 - PRESENTACIÓN ESPONTÁNEA |
| 265 | CUOTA DTO. 631/92 - PRESENTACIÓN ESPONTÁNEA |
| 266 | CUOTA DTO. 932/93 - PRESENTACIÓN ESPONTÁNEA |
| 271 | CUOTA PLAN CON GARANTIA |
| 272 | PAGO A CUENTA CUOTA O TOTAL DE PLAN |
| 273 | RG 4002 RUBRO I (GANANCIAS-BS.PERS.) |
| 274 | FACILIDADES DE PAGO (GANANCIAS-BS.PERS.) |
| 279 | DDJJ RETRIBUCION A CONSUMIDORES FINALALES TARJETA DEBITO |
| 280 | CUOTA DTO. 2413 - FACILIDADES DE PAGO |
| 281 | CUOTA DTO. 631/92 - FACILIDADES DE PAGO |
| 282 | CUOTA DTO. 932/93 - FACILIDADES DE PAGO |
| 283 | CUOTA CONSOLIDADA ART.11 |
| 284 | CUOTA DECRETO 1164/93 |
| 285 | PLAN DE FACILIDADES |
| 294 | INF. COMP. IMP. GCIAS. TENEN. ACT. Y PASIVOS EN MON. EXTRAN. |
| 295 | INFORMACIÓN COMPLEMENTARIA AJUSTES GANANCIAS PERSONAS JURÍDI |
| 298 | NOTA DECLARATIVA |
| 299 | DDJJ.RESPONSABLES SUSTITUTOS RG 3348 |
| 302 | CUOTA PRESENTACIÓN ESPONTÁNEA DTOS.271,272, 316/95 |
| 310 | IVA REINTEGRO TURISTAS - IVATUR |
| 311 | CONFORMIDAD ACTA 1 |
| 312 | CONFORMIDAD ACTA 2 |
| 313 | CONFORMIDAD ACTA 3 |
| 314 | CONFORMIDAD ACTA 4 |
| 315 | CONFORMIDAD ACTA 5 |
| 316 | CONFORMIDAD ACTA 6 |
| 317 | CONFORMIDAD ACTA 7 |
| 318 | CONFORMIDAD ACTA 8 |
| 319 | CONFORMIDAD ACTA 9 |
| 320 | CONFORMIDAD ACTA 10 |
| 321 | IMPUESTO DE IGUALACIÓN NO RETENIDO. |
| 323 | AJUSTE PRESUNTO POR FISCALIZACIÓN LEY N° 26.860 |
| 329 | APORTE DIFERENCIAL DEL 10% - LEY 24.018 |
| 335 | RG 3381 ACTUACIÓN RÉGIMEN EXPORTADORES CARBÓN VEGETAL |
| 337 | PERCEPCIÓN DE EMERGENCIA S/ PROD. AGROPECUARIOS |
| 345 | DETERMINACIÓN DE OFICIO |
| 353 | FACILIDADES DE PAGO DTOS. 271, 272 Y 316/95 |
| 354 | DDJJ RETRIBUCION A CONSUMIDORES FINALALES TARJETA CREDITO |
| 355 | IVA TRANSF.DE CRÉDITOS DE EXPORTACIONES U OTRAS OPERACIONES |
| 356 | TRANSFERENCIA DE SALDOS A FAVOR IVA |
| 357 | TRANSFERENCIA SALDO A FAVOR IVA- REINTEGRO BIENES DE CAPITAL |
| 361 | ACTUALIZACIÓN |
| 363 | RÉGIMEN INFORMATIVO DE TRANSPORTADORAS DE CAUDALES |
| 364 | BENEFICIARIO DEL EXTERIOR |
| 371 | MONEDA EXT. - MONOTRIBUTO |
| 372 | MONEDA EXTRANJERA - DEMAS SUJETOS |
| 373 | PAGO ART DECRETO 1771/2015 |
| 413 | RESPONSABLE SOLIDARIO |
| 414 | SOLICITUD DE REINTEGRO POR VENTAS DE BIENES DE CAPITAL |
| 443 | REINTEGRO EXPORTACION |
| 445 | PAGO PUNTUAL ADMINISTRACIÓN GENERAL DE PUERTOS |
| 449 | REGIMEN DE ASISTENCIA FINANCIERA |
| 450 | DDJJ - ACTIVIDAD AGROPECUARIA |
| 451 | RÉGIMEN INFORMATIVO REGISTRO DE OPERACIONES INMOBILIARIAS |
| 469 | CUOTA RG. 3317 |
| 470 | REG.INFORMATIVO DE IDENTIF.FISCAL DE SOPORTES PUBLICITARIOS |
| 471 | REGIMEN INFORMATIVO DE CONTRATOS DE PUBLICIDAD |
| 472 | REGIMEN INFORMATIVO DEL ANUNCIANTE |
| 477 | CUOTA RG 3318 |
| 485 | CUOTA FACILIDADES DE PAGO RG. 3757 |
| 493 | FACILIDADES DE PAGO DTOS. 271, 272 Y 316/95 |
| 494 | RÉGIMEN INFORMATIVO DE COMISIONES SOBRE JUEGOS DE AZAR |
| 495 | REGIMEN INFORMATIVO - OPERACIONES MERC. INTERNO-SUJ. VINC. |
| 507 | FAENA ANIMALES DE TERCEROS PERCEPCION |
| 515 | PRESENTACIÓN ESPONTÁNEA DTOS.272, 316/95 PLANES VIGENTES |
| 523 | PERCEPCIÓN |
| 531 | PERCEPCIÓN |
| 541 | DESISTIMIENTO - ACTA 1 |
| 542 | DESISTIMIENTO - ACTA 2 |
| 543 | DESISTIMIENTO - ACTA 3 |
| 544 | DESISTIMIENTO - ACTA 4 |
| 545 | DESISTIMIENTO - ACTA 5 |
| 546 | DESISTIMIENTO - ACTA 6 |
| 547 | DESISTIMIENTO - ACTA 7 |
| 548 | DESISTIMIENTO - ACTA 8 |
| 549 | DESISTIMIENTO - ACTA 9 |
| 550 | DESISTIMIENTO - ACTA 10 |
| 553 | AFIP DGI LEY 24467 RÉG.INF. SOCIEDADES DE GARANTÍA RECÍPROCA |
| 566 | PERCEPCIÓN |
| 567 | PERCEPCIÓN |
| 574 | RETENCIONES GLOBALES CONSORCIOS |
| 582 | RETENCIONES GLOBALES COMPAÑIAS ASEGURADORAS |
| 590 | FACILIDADES PAGO - PLANES VIGENTES DTOS. 272, 316/95 |
| 591 | DDJJ INFORMATIVA PADRON SENASA |
| 604 | NOTA INFORMATIVA |
| 609 | INVERSORES VINCULADOS CON FUTBOLISTAS PROF.- RÉG.DE INF. |
| 610 | REPRESENTANTES DE FUTBOLISTAS PROFESIONALES - REG. DE INF. |
| 612 | AMORTIZACIÓN DIFERIMIENTO |
| 613 | DIFERIMIENTOS - REG DE CANCELACIÓN ANTICIPADA |
| 620 | NOTA INFORMATIVA RG 3273 |
| 621 | PAGO DE ARANCELES E INGRESOS VARIOS |
| 639 | NOTA INFORMATIVA RG 3274 |
| 647 | NOTA INFORMATIVA RG 3316 |
| 655 | NOTA INFORMATIVA RG.3311 |
| 656 | PLAN DE FACILIDADES DE PAGO - CONVENIO DGI-AFA |
| 663 | NOTA INFORMATIVA RG.2784 |
| 671 | PLANES CADUCOS - CUOTAS VENCIDAS E IMPAGAS DTOS.272, 316/95 |
| 672 | REGIMEN INFORMATIVO - TITULARES PERMISO DE CATEO RG.3692 |
| 698 | PLANES CADUCOS - CUOTAS AL DÍA DTOS. 272, 316/95 |
| 701 | RETENCION TARJETAS DE CREDITO IMPUESTO A LAS GANANCIAS |
| 706 | SOLICITUD ACRED SALDOS A FAVOR IVA POR ADQUISICIÓN BS CAP |
| 728 | RETENCIONES SOBRE DIVIDENDOS Y ACCIONES |
| 729 | RETENCIÓN RG 3629 |
| 735 | RETENCIONES |
| 736 | RETENCIONES |
| 740 | CONTRATO DE COMPRAVENTA DE GRANOS |
| 741 | CONTRATO OFERTA DE ENTREGA DE GRANOS |
| 744 | RETENCION SOBRE CONVENIOS DE RECAUDACION RG. 3130 |
| 752 | RETENCION SOBRE CONVENIOS DE RECAUDACION RG. 3130 |
| 760 | RETENCIONES S/GRANOS Y OLEAGINOSAS RG. 3274 |
| 779 | RETENCIÓN SOBRE HONORARIOS PROFESIONALES |
| 787 | RETENCION SOBRE TARJETAS DE CREDITO |
| 795 | DETERMINACIÓN DE DEUDA CONSOLIDADA DTOS.1829/94 Y 314/95 |
| 796 | RÉGIMEN INFORMATIVO- CUOTAS DE MEDICINA PREPAGA |
| 797 | RENDICIÓN FACTURA ELECTRÓNICA SERVICIOS PÚBLICOS |
| 798 | RÉGIMEN INFORMATIVO DE LOCACIONES TEMPORARIAS |
| 800 | PAGO ADUANERO |
| 809 | DECLARACION JURADA |
| 810 | REGISTRACIÓN DE OPERACIONES DE GRANOS |
| 811 | FIRMA DIGITAL CONTRATOS |
| 817 | RETENCIONES INDIVIDUALES |
| 818 | FACILIDADES DE PAGO EMPLEADORES DTOS. 270, 314/95 |
| 819 | FAC. DE PAGO-SERV. MÉDICO ASISTENCIALES DTOS. 270, 314/95 |
| 820 | FACILIDADES DE PAGO - AUTÓNOMOS DTOS. 270, 314/95 |
| 821 | FAC.DE PAGO-ASOC. SIND. DE TRAB. Y O.S. DTO. 270, 314/95 |
| 823 | DETERMINACIÓN DE DEUDA CONSOLIDADA DTO.1829/94 Y 314/95 |
| 824 | FAC. DE PAGO- OBRAS SOCIALES Y 1ER SEG.SOCIAL DTO. 270/95 |
| 825 | FAC. DE PAGO- SEG. SOCIAL-CUOTAS RESTANTES DTO.270/95 |
| 826 | FACILIDADES DE PAGO DTO. 493/95 |
| 828 | FACILIDADES DE PAGO OBRAS SOCIALES DTO.963/95 |
| 833 | RETENCIONES S/OLEAGINOSAS RG.3274 |
| 834 | REGIMEN DE INFORMACION DE OPERACIONES COMERCIALES MINORISTAS |
| 841 | RESOLUCIÓN DE APELACIÓN - ACTA 1 |
| 842 | RESOLUCIÓN DE APELACIÓN - ACTA 2 |
| 843 | RESOLUCIÓN DE APELACIÓN - ACTA 3 |
| 844 | RESOLUCIÓN DE APELACIÓN - ACTA 4 |
| 845 | RESOLUCIÓN DE APELACIÓN - ACTA 5 |
| 846 | RESOLUCIÓN DE APELACIÓN - ACTA 6 |
| 847 | RESOLUCIÓN DE APELACIÓN - ACTA 7 |
| 848 | RESOLUCIÓN DE APELACIÓN - ACTA 8 |
| 849 | RESOLUCIÓN DE APELACIÓN - ACTA 9 |
| 850 | RESOLUCIÓN DE APELACIÓN - ACTA 10 |
| 851 | BAJA CONTROLADORES FISCALES Y/O RECAMBIO MEMORIA FISCAL |
| 852 | SOLICITUD DE RECUPERO DE SALDO A FAVOR POR LEY 25924 |
| 853 | ADMINISTRADORES COUNTRIES Y CONSORCIOS:PAGO DE EXPENSAS |
| 854 | RÉGIMEN DE OP. DE COMERCIALIZACIÓN PRIMARIA DE LECHE CRUDA |
| 855 | MEMORIA, EST. CONTABLES E INF. DE AUDIT. |
| 856 | REGINEN INFROMARTIVO DE COMBPROBANTES CLASE A RG 3668 |
| 861 | RETEN CONTROLADORES FISC - RECOLECCIÓN ELECTRÓNICA DE DATOS |
| 862 | ITC-COMPROB.RESPALDATORIOS ADQUISICIONES GAS OIL |
| 863 | EXPORTACIONES POR CUENTA DE TERCEROS |
| 864 | REGIMEN INFORMACION UTE-F.2665 |
| 865 | REGIMEN INFORMACION UTE-F.2666 |
| 868 | RG. 3125 |
| 869 | AJUSTES POR DIF DE INVENTARIO/TENENCIA S/RESPALDO DOCUMENTAL |
| 870 | PÓLIZAS SEGUROS DE CAUCIÓN GARANTÍA - OPERACIONES ADUANERAS |
| 871 | PÓLIZAS SEGUROS DE CAUCIÓN GTIA-ACTUACIÓN AGENTES ADUANEROS |
| 872 | PÓLIZA ELECTRÓNICA: INSCRIPCIÓN DE IMPORTADORES/EXPORTADORES |
| 873 | REGIMEN DE INF. DE OPERAC DE VENTA DE VALORES NEGOCIABLES |
| 874 | REGIMEN INFORMACION UTE-F.2663 |
| 875 | PÓLIZAS SEGUROS DE CAUCIÓN GARANTÍA-OPERACIONES IMPOSITIVAS |
| 876 | RETENCIÓN INDIVIDUAL |
| 877 | REGIMEN INFORMACION UTE-F.2664 |
| 878 | RÉGIMEN DE INFORMACIÓN FIDEICOMISOS FINANC. Y NO FINANC. |
| 879 | PÓLIZAS DE SEGURO DE CAUCIÓN RES 11/2010 SICPYME 2° PERIODO |
| 884 | VALES ALIMENTARIOS |
| 885 | FIDEICOMISOS DEL PAIS Y DEL EXTERIOR |
| 886 | DEUDA APORTES MAGISTRADOS |
| 887 | RÉGIMEN DE REMATES Y SUBASTAS |
| 888 | COMERCIALIZACIÓN DE OBRAS DE ARTE |
| 889 | EXISTENCIA ANUAL DE OBRAS DE ARTE |
| 891 | LEY 26190-IVA- APROB. DE COMPROBANTES VINCULADOS AL PROYECTO |
| 892 | APORTE VOLUNTARIO |
| 893 | COBERTURA GRUPO FAMILIAR PRIMARIO |
| 894 | APORTE POR ADHERENTES |
| 895 | DIFERENCIA PROGRAMA MEDICO OBLIGATORIO |
| 896 | DIFERENCIA DE CONTRIBUCIONES |
| 898 | IVA COMPRAS - CRÉD. FISCAL TEÓRICO DEMERITADO |
| 899 | IVA SALDOS - CRÉDITO FISCAL TEÓRICO DEMERITADO |
| 901 | CONSULTA DE DATOS DE COMPROBANTES POR LOTE |
| 902 | CONSULTA DE MONTOS POR LOTE |
| 903 | CONSULTA GLOBAL DE DATOS DE COMPROBANTES POR LOTE |
| 904 | PADRÓN DE PRODUCTORES DE GRANOS MONOTRIBUTISTAS |
| 906 | CAJAS DE ALIMENTOS |
| 907 | REPORTE RESUMEN DE TOTALES |
| 908 | REP.DUP.ELEC.CPTES CLASE A,A C/LEYENDA Y M |
| 909 | REPORTE INFORME DE OPERACIONES ORDENADO POR PRODUCTOS |
| 910 | RÉG.INF.TRANSACCIONES ECONÓMICAS RELEVANTES-DOMICILIOS |
| 911 | RÉG.INF.TRANSAC.ECONÓMICAS RELEVANTES-CUENTAS Y OPERACIONES |
| 912 | IMAGENES SATELITALES |
| 913 | SITER-CAPITULO B-TITULOS VALORES PUBLICOS Y PRIVADOS |
| 914 | DDJJ INFORMATIVA - RG 3130 |
| 915 | SOLICITUD EXENCION DE RETENCION S/IMP TRANSF DE INMUEBLES |
| 916 | LEY 26360-APROBACIÓN DE COMPROBANTES VINCULADOS AL PROYECTO |
| 917 | LEY 26360-SOLICITUD DE RECUPERO DE SALDOS A FAVOR |
| 918 | AFIP DGI - REGIMEN INFORMATIVO DE CUOTAS ESCUELAS PRIVADAS. |
| 919 | LEY 26093 -APROBACIÓN DE COMPROBANTES VINCULADOS AL PROYECTO |
| 920 | LEY 26093 - SOLICITUD DE RECUPERO DE SALDOS A FAVOR |
| 921 | RÉGIMEN INFORMATIVO DE COMBUSTIBLES EXENTOS-COMBEX |
| 922 | DEVOLUCION EN EXCESO |
| 924 | AFIP DGI-RÉGIMEN INFORMATIVO DE FERIAS |
| 925 | LEY 26566-RÉGIMEN ACREDIT.Y/O DEVOL. ANTICIPADA IVA |
| 926 | RÉGIMEN INFORMATIVO - CITI - EMPRESAS PROMOVIDAS |
| 927 | ESTUDIO DE PRECIOS DE TRANSFERENCIA- ANUAL |
| 928 | DDJJ INFORMATIVA ANUAL -PRECIOS DE TRANSFERENCIA-F 969 |
| 929 | REG.INF. SECTOR PESQUERO MARÍTIMO |
| 930 | REGIMEN DE INFORMACION DE VENTAS ANUALES EN MERCADO INTERNO |
| 931 | REGIMEN DE INFORMACION DE ACTIVO NO CORRIENTE |
| 932 | DIFERENCIA ASEGURADORA RIESGOS DE TRABAJO |
| 934 | COOPERATIVAS Y MUTUALES OPERACIONES FINANCIERAS |
| 935 | NÓMINA SALARIAL EMPLEADOS PÚBLICOS NO ADHERIDOS AL SIPA |
| 936 | LEY 26190-IVA-SOLICITUD DE RECUPERO DE SALDOS A FAVOR |
| 937 | LEY26093-APROBACIÓN BENEFICIO AMORTIZACIÓN ACELERADA |
| 938 | LEY 26360-APROBACIÓN DEL BENEFICIO DE AMORTIZACION ACELERADA |
| 939 | AFIP DGI LEY 26190 - APROB. DEL BENEF. DE AMORTIZ. ACELERADA |
| 940 | SOLICITUD CONSTANCIAS DE EXCLUSION DE RETENCIONES  GANANCIAS |
| 941 | RÉGIMEN INFORMATIVO DE TABACO |
| 942 | RÉG. INF. DE REORG. DE SOCIEDADES Y EMPRESAS - FUSIÓN |
| 943 | RÉG. INF. DE REORG. DE SOCIEDADES Y EMPRESAS - ESCISIÓN |
| 944 | RÉG. INF. DE REORG. DE SOCIEDADES Y EMPRESAS - VENTA Y TRANS |
| 945 | CONTROLADORES FISCALES- LECTURA DE DATOS DE MEMORIAS |
| 946 | RG 1277-FLOTA FLUVIAL REINT. IMPOSIT. TASA SOBRE EL GASOIL |
| 947 | LEY 25360 SALDOS A FAVOR |
| 948 | AFIP DGI-PADRON OPERADORES RUCA |
| 949 | DDJJ INFORMATIVA - RG 3202 |
| 950 | AFIP DGI - CITI DERECHOS ECONOMIC Y OPERACIONES RELACIONADAS |
| 951 | REGISTRO FISCAL DE OPERADORES DE GRANOS |
| 952 | SOLICITUD DE EXCLUSION RETENCIONES/PERCEPCIONES IVA |
| 953 | MOVIMIENTO DE GRANOS |
| 954 | COMBUSTIBLES LIQUIDOS DECRETO 1016 |
| 955 | REINTEGRO CONSUMO TARJETAS SOCIALES |
| 956 | TIT. PROY. PROM. NO INDUSTRIALES-INVERSIONES Y COSTO FISCAL |
| 957 | DEC.JURADA DETERMINATIVA DE IMPUESTO |
| 958 | DECLARACIÓN ADUANA |
| 959 | L. 25924 APROBACIÓN DE COMPROBANTES VINCULADOS AL PROYECTO |
| 960 | SICPYME-INFORMATIVO ART.28 LEY DE IVA |
| 961 | MERCADO CAMBIARIO |
| 962 | LEY 25.988- INVERSIONES EN BIENES DE CAPITAL |
| 963 | ONCCA - INFORMACION CARTAS DE PORTE RECIBIDAS |
| 964 | DDJJ INFORMATIVA ANUAL-ENTES INDEPENDIENTES F.741/A |
| 965 | DDJJ.INFORMATIVA RG.2793 |
| 966 | CITI VENTAS |
| 967 | PERSONAL RELACION DEPENDENCIA INF BS PERSONALES RG 1465 |
| 968 | RÉGIMEN INFORMATIVO DE RANCHO PRODUCTORES |
| 969 | RÉGIMEN INFORMATIVO DE RANCHO DISTRIBUIDORES |
| 970 | RÉGIMEN INFORMATIVO DE RANCHO ADQUIRENTES |
| 971 | DONACIONES EN DINERO O ESPECIE EMPLEADORES |
| 972 | RECE- SOLICITUD DE AUTORIZACIÓN DE EMISION DE COMPROBANTES |
| 973 | DONACIONES EN DINERO O ESPECIE - DONANTE |
| 974 | REAR-GENERACION DE INFO REQUERIDA SEGUN PTO 7)ANEXO3.RG1361 |
| 975 | DDJJ INFORMATIVA ANUAL P.JURIDICA Y P.FISICA-F. 743 |
| 976 | DDJJ INFORMATIVA SEMESTRAL - ENTES INDEPENDIENTES F. 741 |
| 977 | DDJJ INFORMATIVA SEMESTRAL-PER.JURIDICA Y PER.FISICA-F.742 |
| 978 | DDJJ INFORMATIVA ANUAL PERSONA JURIDICA-F.743 |
| 979 | DDJJ ANUAL INFORMATIVA - PERSONAS FÍSICAS |
| 980 | DDJJ INFORMATIVA CINES |
| 981 | DDJJ INFORMATIVA |
| 982 | DDJJ.INFORMATIVA ACTIV.AGROPECUARIA |
| 983 | BOLSA DE CEREALES |
| 984 | PARTICIPACIONES SOCIETARIAS |
| 985 | CONSUMOS RELEVANTES |
| 986 | PRODUCTORES DE SEGUROS |
| 987 | REPRESENTANTES DE SUJETOS RESIDENTES EN EL EXTERIOR |
| 988 | REP. DEL EXT. - TERCEROS INTERVINIENTES |
| 989 | TARJETAS DE CRÉDITO |
| 990 | CITI-COMPRAS |
| 991 | OPER DE COMPRA Y DESCUENTO C/ENDOSOS O CESION DE DOC |
| 992 | CITI ESCRIBANOS |
| 993 | GUIA FISCAL HARINERA - ESTABLECIMIENTO MOLINERO |
| 994 | GUIA FISCAL HARINERA - USUARIO DEL SERVICIO DE MOLIENDA |
| 995 | COMBUSTIBLES EXENTOS - COMBEX |
| 996 | COMBUSTIBLES ZONA SUR - COMBSUR |
| 997 | SITER ENTIDADES FINANCIERAS |
| 998 | SITER COMISIONISTAS |
| 999 | DONACIONES EN DINERO O EN ESPECIE - DONATARIOS |
### Actividades
| **id** | **desc** |
|---|---|
| 0 | ACTIVIDADES NO CLASIFICADAS EN OTRA PARTE |
| 7 | JUBILADO |
| 8 | ESTUDIANTE |
| 9 | AMA DE CASA |
| 10 | EX - AGENTE DE LA ADM. PUBLILCA |
| 11 | TRABAJADOR RELAC. DEPENDENCIA |
| 12 | SIN ACTIVIDAD ECONOMICA |
| 13 | AGRICULTURA FAMILIAR |
| 11111 | CULTIVO DE ARROZ |
| 11112 | CULTIVO DE TRIGO |
| 11119 | CULTIVO DE CEREALES N.C.P., EXCEPTO LOS DE USO FORRAJERO |
| 11121 | CULTIVO DE MAÍZ |
| 11122 | CULTIVO DE SORGO GRANIFERO |
| 11129 | CULTIVO DE CEREALES DE USO FORRAJERO N.C.P. |
| 11130 | CULTIVO DE PASTOS DE USO FORRAJERO |
| 11131 | CULTIVO DE SOJA |
| 11132 | CULTIVO DE GIRASOL |
| 11139 | CULTIVO DE OLEAGINOSAS N.C.P. |
| 11140 | CULTIVO DE PASTOS FORRAJEROS |
| 11210 | CULTIVO DE PAPA,BATATA Y MANDIOCA |
| 11211 | CULTIVO DE SOJA |
| 11221 | CULTIVO DE TOMATE |
| 11229 | CULTIVO DE BULBOS,BROTES,RAICES Y HORTALIZAS DE FRUTOS N.C.P. |
| 11230 | CULTIVO DE HORTALIZAS DE HOJA Y DE OTRAS HORTALIZAS FRESCAS |
| 11241 | CULTIVO DE LEGUMBRES FRESCAS |
| 11242 | CULTIVO DE LEGUMBRES SECAS |
| 11251 | CULTIVO DE FLORES |
| 11252 | CULTIVO DE PLANTAS ORNAMENTALES |
| 11291 | CULTIVO DE GIRASOL |
| 11299 | CULTIVO DE OLEAGINOSAS N.C.P. EXCEPTO SOJA Y GIRASOL |
| 11310 | CULTIVO DE PAPA, BATATA Y MANDIOCA |
| 11311 | CULTIVO DE MANZANA Y PERA |
| 11319 | CULTIVO DE FRUTAS DE PEPITA N.C.P. |
| 11320 | CULTIVO DE FRUTAS DE CAROZO |
| 11321 | CULTIVO DE TOMATE |
| 11329 | CULTIVO DE BULBOS, BROTES, RAÍCES Y HORTALIZAS DE FRUTO N.C.P. |
| 11330 | CULTIVO DE FRUTAS CITRICAS |
| 11331 | CULTIVO DE HORTALIZAS DE HOJA Y DE OTRAS HORTALIZAS FRESCAS |
| 11340 | CULTIVO DE NUECES Y FRUTAS SECAS |
| 11341 | CULTIVO DE LEGUMBRES FRESCAS |
| 11342 | CULTIVO DE LEGUMBRES SECAS |
| 11390 | CULTIVO DE FRUTAS N.C.P. |
| 11400 | CULTIVO DE TABACO |
| 11411 | CULTIVO DE ALGODON |
| 11419 | CULTIVO DE PLANTAS PARA LA OBTENCION DE FIBRAS N.C.P. |
| 11421 | CULTIVO DE CAÑA DE AZUCAR |
| 11429 | CULTIVO DE PLANTAS SACARIFERAS N.C.P. |
| 11430 | CULTIVO DE VID PARA VINIFICAR |
| 11440 | CULTIVO DE TE,YERBA MATE Y OTRAS PLANTAS CUYAS HOJAS SE UTILIZAN PARA PREPARAR BEBIDAS |
| 11450 | CULTIVO DE TABACO |
| 11460 | CULTIVO DE ESPECIAS |
| 11490 | CULTIVOS INDUSTRIALES N.C.P. |
| 11501 | CULTIVO DE ALGODÓN |
| 11509 | CULTIVO DE PLANTAS PARA LA OBTENCIÓN DE FIBRAS N.C.P. |
| 11511 | PRODUCCION DE SEMILLAS HIBRIDAS DE CEREALES Y OLEAGINOSAS |
| 11512 | PRODUCCION DE SEMILLAS VARIETALES O AUTOFECUNDADAS DE CEREALES,OLEAGINOSAS,Y FORRAJERAS |
| 11513 | PRODUCCION DE SEMILLAS DE HORTALIZAS Y LEGUMBRES,FLORES Y PLANTAS ORNAMENTALES Y ARBOLES FRUTALES |
| 11519 | PRODUCCION DE SEMILLAS DE CULTIVOS AGRICOLAS N.C.P. |
| 11520 | PRODUCCION DE OTRAS FORMAS DE PROPAGACION DE CULTIVOS AGRICOLAS |
| 11911 | CULTIVO DE FLORES |
| 11912 | CULTIVO DE PLANTAS ORNAMENTALES |
| 11990 | CULTIVOS TEMPORALES N.C.P. |
| 12110 | CULTIVO DE VID PARA VINIFICAR |
| 12111 | CRIA DE GANADO BOVINO -EXCEPTO EN CABAÑAS Y PARA LA PRODUCCION DE LECHE- |
| 12112 | INVERNADA DE GANADO BOVINO EXCEPTO EL ENGORDE EN CORRALES |
| 12113 | ENGORDE EN CORRALES |
| 12120 | CRIA DE GANADO OVINO,EXCEPTO EN CABAÑAS Y PARA LA PRODUCCION DE LANA |
| 12121 | CULTIVO DE UVA DE MESA |
| 12130 | CRIA DE GANADO PORCINO,EXCEPTO EN CABAÑAS |
| 12140 | CRIA DE GANADO EQUINO,EXCEPTO EN HARAS |
| 12150 | CRIA DE GANADO CAPRINO,EXCEPTO EN CABAÑAS Y PARA PRODUCCION DE LECHE |
| 12161 | CRIA DE GANADO BOVINO EN CABAÑAS |
| 12162 | CRIA DE GANADO OVINO,PORCINO Y CAPRINO EN CABAÑAS |
| 12163 | CRIA DE GANADO EQUINO EN HARAS |
| 12169 | CRIA EN CABAÑAS DE GANADO N.C.P. |
| 12171 | PRODUCCION DE LECHE DE GANADO BOVINO |
| 12179 | PRODUCCION DE LECHE DE GANADO N.C.P. |
| 12181 | PRODUCCION DE LANA |
| 12182 | PRODUCCION DE PELOS |
| 12190 | CRIA DE GANADO N.C.P. |
| 12200 | CULTIVO DE FRUTAS CÍTRICAS |
| 12211 | CRIA DE AVES PARA PRODUCCION DE CARNE |
| 12212 | CRIA DE AVES PARA PRODUCCION DE HUEVOS |
| 12220 | PRODUCCION DE HUEVOS |
| 12230 | APICULTURA |
| 12241 | CRIA DE ANIMALES PARA LA OBTENCION DE PIELES Y CUEROS |
| 12242 | CRIA DE ANIMALES PARA LA OBTENCION DE PELOS |
| 12243 | CRIA DE ANIMALES PARA LA OBTENCION DE PLUMAS |
| 12290 | CRIA DE ANIMALES Y OBTENCION DE PRODUCTOS DE ORIGEN ANIMAL,N.C.P. |
| 12311 | CULTIVO DE MANZANA Y PERA |
| 12319 | CULTIVO DE FRUTAS DE PEPITA N.C.P. |
| 12320 | CULTIVO DE FRUTAS DE CAROZO |
| 12410 | CULTIVO DE FRUTAS TROPICALES Y SUBTROPICALES |
| 12420 | CULTIVO DE FRUTAS SECAS |
| 12490 | CULTIVO DE FRUTAS N.C.P. |
| 12510 | CULTIVO DE CAÑA DE AZÚCAR |
| 12590 | CULTIVO DE PLANTAS SACARÍFERAS N.C.P. |
| 12600 | CULTIVO DE FRUTOS OLEAGINOSOS |
| 12701 | CULTIVO DE YERBA MATE |
| 12709 | CULTIVO DE TÉ Y OTRAS PLANTAS CUYAS HOJAS SE UTILIZAN PARA PREPARAR INFUSIONES |
| 12800 | CULTIVO DE ESPECIAS Y DE PLANTAS AROMÁTICAS Y MEDICINALES |
| 12900 | CULTIVOS PERENNES N.C.P. |
| 13011 | PRODUCCIÓN DE SEMILLAS HÍBRIDAS DE CEREALES Y OLEAGINOSAS |
| 13012 | PRODUCCIÓN DE SEMILLAS VARIETALES O AUTOFECUNDADAS DE CEREALES, OLEAGINOSAS, Y FORRAJERAS |
| 13013 | PRODUCCIÓN DE SEMILLAS DE HORTALIZAS Y LEGUMBRES, FLORES Y PLANTAS ORNAMENTALES Y ÁRBOLES FRUTALES |
| 13019 | PRODUCCIÓN DE SEMILLAS DE CULTIVOS AGRÍCOLAS N.C.P. |
| 13020 | PRODUCCIÓN DE OTRAS FORMAS DE PROPAGACIÓN DE CULTIVOS AGRÍCOLAS |
| 14111 | SERVICIOS DE LABRANZA,SIEMBRA,TRANSPLANTE Y CUIDADOS CULTURALES |
| 14112 | SERVICIOS DE PULVERIZACION,DESINFECCION Y FUMIGACION AEREA Y TERRESTRE,EXCEPTO LA MANUAL |
| 14113 | CRÍA DE GANADO BOVINO, EXCEPTO LA REALIZADA EN CABAÑAS Y PARA LA PRODUCCIÓN DE LECHE |
| 14114 | INVERNADA  DE GANADO BOVINO EXCEPTO EL ENGORDE EN CORRALES (FEED-LOT) |
| 14115 | ENGORDE EN CORRALES (FEED-LOT) |
| 14119 | SERVICIOS DE MAQUINARIA AGRICOLA N.C.P.,EXCEPTO LOS DE COSECHA MECANICA |
| 14120 | SERVICIOS DE COSECHA MECANICA |
| 14121 | CRÍA DE GANADO BOVINO REALIZADA EN CABAÑAS |
| 14130 | SERVICIOS DE CONTRATISTAS DE MANO DE OBRA AGRICOLA |
| 14190 | SERVICIOS AGRICOLAS N.C.P |
| 14210 | INSEMINACION ARTIFICIAL Y SERVICIOS N.C.P.PARA MEJORAR LA REPRODUCCION DE LOS ANIMALES Y EL RENDIMIENTO DE SUS PRODUCTOS |
| 14211 | CRÍA DE GANADO EQUINO, EXCEPTO LA REALIZADA EN HARAS |
| 14220 | SERVICIOS DE CONTRATISTAS DE MANO DE OBRA PECUARIA |
| 14221 | CRÍA DE GANADO EQUINO REALIZADA EN HARAS |
| 14291 | SERVICIOS PARA EL CONTROL DE PLAGAS,BAÑOS PARASITICIDAS,ETC. |
| 14292 | ALBERGUE Y CUIDADO DE ANIMALES DE TERCEROS |
| 14299 | SERVICIOS PECUARIOS N.C.P.,EXCEPTO LOS VETERINARIOS |
| 14300 | CRÍA DE CAMÉLIDOS |
| 14410 | CRÍA DE GANADO OVINO -EXCEPTO EN CABAÑAS Y PARA LA  PRODUCCIÓN DE LANA Y LECHE- |
| 14420 | CRÍA DE GANADO OVINO REALIZADA EN CABAÑAS |
| 14430 | CRÍA DE GANADO CAPRINO -EXCEPTO LA REALIZADA EN CABAÑAS Y PARA PRODUCCIÓN DE PELOS Y DE LECHE- |
| 14440 | CRÍA DE GANADO CAPRINO REALIZADA EN CABAÑAS |
| 14510 | CRÍA DE GANADO PORCINO, EXCEPTO LA REALIZADA EN CABAÑAS |
| 14520 | CRÍA DE GANADO PORCINO REALIZADO EN CABAÑAS |
| 14610 | PRODUCCIÓN DE LECHE BOVINA |
| 14620 | PRODUCCIÓN DE LECHE DE OVEJA Y DE CABRA |
| 14710 | PRODUCCIÓN DE LANA Y PELO DE OVEJA Y CABRA (CRUDA) |
| 14720 | PRODUCCIÓN DE PELOS DE GANADO N.C.P. |
| 14810 | CRÍA DE AVES DE CORRAL, EXCEPTO PARA LA PRODUCCIÓN DE HUEVOS |
| 14820 | PRODUCCIÓN DE HUEVOS |
| 14910 | APICULTURA |
| 14920 | CUNICULTURA |
| 14930 | CRÍA DE ANIMALES PELÍFEROS, PILÍFEROS Y PLUMÍFEROS, EXCEPTO DE LAS ESPECIES GANADERAS |
| 14990 | CRÍA DE ANIMALES Y OBTENCIÓN DE PRODUCTOS DE ORIGEN ANIMAL, N.C.P. |
| 15010 | CAZA Y CAPTURA DE ANIMALES VIVOS Y REPOBLACION DE ANIMALES DE CAZA |
| 15020 | SERVICIOS PARA LA CAZA |
| 16111 | SERVICIOS DE LABRANZA, SIEMBRA, TRANSPLANTE  Y  CUIDADOS CULTURALES |
| 16112 | SERVICIOS DE PULVERIZACIÓN, DESINFECCIÓN Y FUMIGACIÓN TERRESTRE |
| 16113 | SERVICIOS DE PULVERIZACIÓN, DESINFECCIÓN Y FUMIGACIÓN AÉREA |
| 16119 | SERVICIOS DE MAQUINARIA AGRÍCOLA N.C.P., EXCEPTO LOS DE COSECHA MECÁNICA |
| 16120 | SERVICIOS DE COSECHA MECÁNICA |
| 16130 | SERVICIOS DE CONTRATISTAS DE MANO DE OBRA AGRÍCOLA |
| 16140 | SERVICIOS DE POST COSECHA |
| 16150 | SERVICIOS DE PROCESAMIENTO DE SEMILLAS PARA SU SIEMBRA |
| 16190 | SERVICIOS DE APOYO AGRÍCOLAS N.C.P |
| 16210 | INSEMINACIÓN ARTIFICIAL Y SERVICIOS N.C.P. PARA MEJORAR LA REPRODUCCIÓN DE LOS ANIMALES Y EL RENDIMIENTO DE SUS PRODUCTOS |
| 16220 | SERVICIOS DE CONTRATISTAS DE MANO DE OBRA PECUARIA |
| 16230 | SERVICIOS DE ESQUILA DE ANIMALES |
| 16291 | SERVICIOS PARA EL CONTROL DE PLAGAS, BAÑOS PARASITICIDAS, ETC. |
| 16292 | ALBERGUE Y CUIDADO DE  ANIMALES DE TERCEROS |
| 16299 | SERVICIOS DE APOYO PECUARIOS N.C.P. |
| 17010 | CAZA Y REPOBLACIÓN  DE ANIMALES DE CAZA |
| 17020 | SERVICIOS DE APOYO PARA LA CAZA |
| 20110 | PLANTACION DE BOSQUES |
| 20120 | REPOBLACION Y CONSERVACION DE BOSQUES NATIVOS Y ZONAS FORESTADAS |
| 20130 | EXPLOTACION DE VIVEROS FORESTALES |
| 20210 | EXTRACCION DE PRODUCTOS FORESTALES DE BOSQUES CULTIVADOS |
| 20220 | EXTRACCION DE PRODUCTOS FORESTALES DE BOSQUES NATIVOS |
| 20310 | SERVICIOS FORESTALES DE EXTRACCION DE MADERA |
| 20390 | SERVICIOS FORESTALES EXCEPTO LOS RELACIONADOS CON LA EXTRACCION DE MADERA |
| 21010 | PLANTACIÓN DE BOSQUES |
| 21020 | REPOBLACIÓN Y CONSERVACIÓN DE BOSQUES NATIVOS Y ZONAS FORESTADAS |
| 21030 | EXPLOTACIÓN DE VIVEROS FORESTALES |
| 22010 | EXTRACCIÓN DE PRODUCTOS FORESTALES DE BOSQUES CULTIVADOS |
| 22020 | EXTRACCIÓN DE PRODUCTOS FORESTALES DE BOSQUES NATIVOS |
| 24010 | SERVICIOS FORESTALES PARA LA EXTRACCIÓN DE MADERA |
| 24020 | SERVICIOS FORESTALES EXCEPTO LOS SERVICIOS PARA LA EXTRACCIÓN DE MADERA |
| 31110 | PESCA DE ORGANISMOS MARINOS, EXCEPTO CUANDO ES REALIZADA EN BUQUES PROCESADORES |
| 31120 | PESCA Y ELABORACIÓN DE PRODUCTOS MARINOS REALIZADA A BORDO DE BUQUES PROCESADORES |
| 31130 | RECOLECCIÓN DE ORGANISMOS MARINOS EXCEPTO PECES, CRUSTÁCEOS Y MOLUSCOS |
| 31200 | PESCA CONTINENTAL: FLUVIAL Y LACUSTRE |
| 31300 | SERVICIOS DE APOYO PARA LA PESCA |
| 32000 | EXPLOTACIÓN DE CRIADEROS DE PECES, GRANJAS PISCÍCOLAS Y OTROS FRUTOS ACUÁTICOS  (ACUICULTURA) |
| 50110 | PESCA MARITIMA,COSTERA Y DE ALTURA |
| 50120 | PESCA CONTINENTAL,FLUVIAL Y LACUSTRE |
| 50130 | RECOLECCION DE PRODUCTOS MARINOS |
| 50200 | EXPLOTACION DE CRIADEROS DE PECES,GRANJAS PISCICOLAS Y OTROS FRUTOS ACUATICOS |
| 50300 | SERVICIOS PARA LA PESCA |
| 51000 | EXTRACCIÓN Y AGLOMERACIÓN DE CARBÓN |
| 52000 | EXTRACCIÓN Y AGLOMERACIÓN DE LIGNITO |
| 61000 | EXTRACCIÓN DE PETRÓLEO CRUDO |
| 62000 | EXTRACCIÓN DE GAS NATURAL |
| 71000 | EXTRACCIÓN DE MINERALES DE HIERRO |
| 72100 | EXTRACCIÓN DE MINERALES Y CONCENTRADOS DE URANIO Y TORIO |
| 72910 | EXTRACCIÓN DE METALES PRECIOSOS |
| 72990 | EXTRACCIÓN DE MINERALES METALÍFEROS NO FERROSOS N.C.P., EXCEPTO MINERALES DE URANIO Y TORIO |
| 81100 | EXTRACCIÓN DE ROCAS ORNAMENTALES |
| 81200 | EXTRACCIÓN DE PIEDRA CALIZA Y YESO |
| 81300 | EXTRACCIÓN DE ARENAS, CANTO RODADO Y TRITURADOS PÉTREOS |
| 81400 | EXTRACCIÓN DE ARCILLA Y CAOLÍN |
| 89110 | EXTRACCIÓN DE MINERALES PARA LA FABRICACIÓN DE ABONOS EXCEPTO TURBA |
| 89120 | EXTRACCIÓN DE MINERALES PARA LA FABRICACIÓN DE PRODUCTOS QUÍMICOS |
| 89200 | EXTRACCIÓN Y AGLOMERACIÓN DE TURBA |
| 89300 | EXTRACCIÓN DE SAL |
| 89900 | EXPLOTACIÓN DE MINAS Y CANTERAS N.C.P. |
| 91000 | SERVICIOS DE APOYO PARA LA EXTRACCIÓN DE PETRÓLEO Y GAS NATURAL |
| 99000 | SERVICIOS DE APOYO PARA LA MINERÍA, EXCEPTO PARA LA EXTRACCIÓN DE PETRÓLEO Y GAS NATUAL |
| 101000 | EXTRACCION Y AGLOMERACION DE CARBON |
| 101011 | MATANZA DE GANADO BOVINO |
| 101012 | PROCESAMIENTO DE CARNE DE GANADO BOVINO |
| 101013 | SALADERO Y PELADERO DE CUEROS DE GANADO BOVINO |
| 101020 | PRODUCCIÓN Y PROCESAMIENTO DE CARNE DE AVES |
| 101030 | ELABORACIÓN DE FIAMBRES Y EMBUTIDOS |
| 101040 | MATANZA DE GANADO EXCEPTO EL BOVINO Y PROCESAMIENTO DE SU CARNE |
| 101091 | FABRICACIÓN DE ACEITES Y GRASAS DE ORIGEN ANIMAL |
| 101099 | MATANZA DE ANIMALES N.C.P. Y PROCESAMIENTO DE SU CARNE, ELABORACIÓN DE SUBPRODUCTOS CÁRNICOS N.C.P. |
| 102000 | EXTRACCION Y AGLOMERACION DE LIGNITO |
| 102001 | ELABORACIÓN DE PESCADOS DE MAR, CRUSTÁCEOS Y  PRODUCTOS MARINOS |
| 102002 | ELABORACIÓN DE PESCADOS DE RÍOS Y LAGUNAS Y OTROS PRODUCTOS FLUVIALES Y LACUSTRES |
| 102003 | FABRICACIÓN DE ACEITES, GRASAS, HARINAS Y PRODUCTOS A BASE DE PESCADOS |
| 103000 | EXTRACCION Y AGLOMERACION DE TURBA |
| 103011 | PREPARACIÓN DE CONSERVAS DE FRUTAS, HORTALIZAS Y LEGUMBRES |
| 103012 | ELABORACIÓN Y ENVASADO DE DULCES, MERMELADAS Y JALEAS |
| 103020 | ELABORACIÓN DE JUGOS NATURALES Y SUS CONCENTRADOS, DE FRUTAS, HORTALIZAS Y LEGUMBRES |
| 103030 | ELABORACIÓN DE FRUTAS, HORTALIZAS Y LEGUMBRES CONGELADAS |
| 103091 | ELABORACIÓN DE HORTALIZAS Y LEGUMBRES DESHIDRATADAS O DESECADAS, PREPARACIÓN N.C.P. DE HORTALIZAS Y LEGUMBRES |
| 103099 | ELABORACIÓN DE FRUTAS DESHIDRATADAS O DESECADAS, PREPARACIÓN N.C.P. DE FRUTAS |
| 104011 | ELABORACIÓN DE ACEITES Y GRASAS VEGETALES  SIN REFINAR |
| 104012 | ELABORACIÓN DE ACEITE DE OLIVA |
| 104013 | ELABORACIÓN DE ACEITES Y GRASAS VEGETALES REFINADOS |
| 104020 | ELABORACIÓN DE MARGARINAS Y GRASAS VEGETALES COMESTIBLES SIMILARES |
| 105010 | ELABORACIÓN DE LECHES Y PRODUCTOS LÁCTEOS DESHIDRATADOS |
| 105020 | ELABORACIÓN DE QUESOS |
| 105030 | ELABORACIÓN INDUSTRIAL DE HELADOS |
| 105090 | ELABORACIÓN DE PRODUCTOS LÁCTEOS N.C.P. |
| 106110 | MOLIENDA DE TRIGO |
| 106120 | PREPARACIÓN DE ARROZ |
| 106131 | ELABORACIÓN DE ALIMENTOS A BASE DE CEREALES |
| 106139 | PREPARACIÓN Y MOLIENDA DE LEGUMBRES Y CEREALES N.C.P., EXCEPTO TRIGO Y ARROZ Y MOLIENDA HÚMEDA DE MAÍZ |
| 106200 | ELABORACIÓN DE ALMIDONES Y PRODUCTOS DERIVADOS DEL ALMIDÓN, MOLIENDA HÚMEDA DE MAÍZ |
| 107110 | ELABORACIÓN DE GALLETITAS Y BIZCOCHOS |
| 107121 | ELABORACIÓN INDUSTRIAL DE PRODUCTOS DE PANADERÍA, EXCEPTO GALLETITAS Y BIZCOCHOS |
| 107129 | ELABORACIÓN DE PRODUCTOS DE PANADERÍA N.C.P. |
| 107200 | ELABORACIÓN DE AZÚCAR |
| 107301 | ELABORACIÓN DE CACAO Y CHOCOLATE |
| 107309 | ELABORACIÓN DE PRODUCTOS DE CONFITERÍA N.C.P. |
| 107410 | ELABORACIÓN DE PASTAS ALIMENTARIAS FRESCAS |
| 107420 | ELABORACIÓN DE PASTAS ALIMENTARIAS SECAS |
| 107500 | ELABORACIÓN DE COMIDAS PREPARADAS PARA REVENTA |
| 107911 | TOSTADO, TORRADO Y MOLIENDA DE CAFÉ |
| 107912 | ELABORACIÓN Y MOLIENDA DE HIERBAS AROMÁTICAS Y  ESPECIAS |
| 107920 | PREPARACIÓN DE HOJAS DE TÉ |
| 107930 | ELABORACIÓN DE YERBA MATE |
| 107991 | ELABORACIÓN DE EXTRACTOS, JARABES Y CONCENTRADOS |
| 107992 | ELABORACIÓN DE VINAGRES |
| 107999 | ELABORACIÓN DE PRODUCTOS ALIMENTICIOS N.C.P. |
| 108000 | ELABORACIÓN DE ALIMENTOS PREPARADOS PARA ANIMALES |
| 109000 | SERVICIOS INDUSTRIALES PARA LA ELABORACIÓN DE ALIMENTOS Y BEBIDAS |
| 110100 | DESTILACIÓN, RECTIFICACIÓN Y MEZCLA DE BEBIDAS ESPIRITOSAS |
| 110211 | ELABORACIÓN DE MOSTO |
| 110212 | ELABORACIÓN DE VINOS |
| 110290 | ELABORACIÓN DE SIDRA Y OTRAS BEBIDAS ALCOHÓLICAS FERMENTADAS |
| 110300 | ELABORACIÓN DE CERVEZA, BEBIDAS MALTEADAS Y MALTA |
| 110411 | EMBOTELLADO DE AGUAS NATURALES Y MINERALES |
| 110412 | FABRICACIÓN DE SODAS |
| 110420 | ELABORACIÓN DE BEBIDAS GASEOSAS, EXCEPTO SODA |
| 110491 | ELABORACIÓN DE HIELO |
| 110492 | ELABORACIÓN DE BEBIDAS NO ALCOHÓLICAS N.C.P. |
| 111000 | EXTRACCION DE PETROLEO CRUDO Y GAS NATURAL |
| 111112 | CRIA GANADO BOVINO |
| 111120 | INVERNADA GANADO BOVINO |
| 111139 | CRIA ANIMALES DE PEDIGRI |
| 111147 | CRIA GANADO EQUINO HARAS |
| 111155 | PRODUCCION LECHE TAMBOS |
| 111163 | CRIA GANADO OVINO Y EXP LANERA |
| 111171 | CRIA GANADO PORCINO |
| 111198 | CRIA ANIMALES P/ PROD PIELES |
| 111201 | CRIA AVES P/ PRODUCCION CARNES |
| 111228 | CRIA AVES P/ PRODUCCION HUEVOS |
| 111236 | APICULTURA |
| 111244 | CRIA Y EXP ANIMALES NO CLASIF |
| 111252 | CULTIVO VID |
| 111260 | CULTIVO CITRICOS |
| 111279 | CULTIVO MANZANAS Y PERAS |
| 111287 | CULTIVO FRUTALES NO CLASIF |
| 111295 | CULTIVO OLIVOS NOGALES ETC |
| 111309 | CULTIVO ARROZ |
| 111317 | CULTIVO SOJA |
| 111325 | CULTIVO CEREALES NO CLASIF |
| 111333 | CULTIVO ALGODON |
| 111341 | CULTIVO CAÑA AZUCAR |
| 111368 | CULTIVO TE YERBA Y TUNG |
| 111376 | CULTIVO TABACO |
| 111384 | CULTIVO PAPAS Y BATATAS |
| 111392 | CULTIVO TOMATES |
| 111406 | CULTIVO HORTALIZAS Y LEGUMBR |
| 111414 | CULTIVO FLOR Y PLANT.VIVEROS |
| 111481 | CULTIVOS NO CLASIFICADOS |
| 112000 | ACTIVIDADES DE SERVICIOS RELACIONADAS CON LA EXTRACCION DE PETROLEO Y GAS,EXCEPTO LAS ACTIVIDADES DE PROSPECCION |
| 112011 | FUMIGACION DE CULTIVOS |
| 112038 | ROTURACION Y SIEMBRA |
| 112046 | COSECHA Y RECOL. DE CULTIVOS |
| 112054 | SERVICIOS AGROPEC. NO CLASIF |
| 113018 | CAZA ORDINARIA |
| 120000 | EXTRACCION DE MINERALES Y CONCENTRADOS DE URANIO Y TORIO |
| 120010 | PREPARACIÓN DE HOJAS DE TABACO |
| 120091 | ELABORACIÓN DE CIGARRILLOS |
| 120099 | ELABORACIÓN DE PRODUCTOS DE TABACO N.C.P. |
| 121010 | EXPLOTACION Y CONSERV BOSQUES |
| 121029 | FORESTACION |
| 121037 | SERVICIOS FORESTALES |
| 122017 | CORTE DESBASTE TRONCOS MADERA |
| 130109 | PESCA ALTURA Y COSTERA |
| 130206 | PESCA FLUVIAL Y LACUST VIVEROS |
| 131000 | EXTRACCION DE MINERALES DE HIERRO |
| 131110 | PREPARACIÓN DE FIBRAS TEXTILES VEGETALES, DESMOTADO DE ALGODÓN |
| 131120 | PREPARACIÓN DE FIBRAS ANIMALES DE USO TEXTIL |
| 131131 | FABRICACIÓN DE HILADOS TEXTILES DE LANA, PELOS Y SUS MEZCLAS |
| 131132 | FABRICACIÓN DE HILADOS TEXTILES DE ALGODÓN Y SUS MEZCLAS |
| 131139 | FABRICACIÓN DE HILADOS TEXTILES N.C.P., EXCEPTO DE LANA  Y DE ALGODÓN |
| 131201 | FABRICACIÓN DE TEJIDOS (TELAS) PLANOS DE LANA Y SUS MEZCLAS, INCLUYE HILANDERÍAS Y TEJEDURÍAS INTEGRADAS |
| 131202 | FABRICACIÓN DE TEJIDOS (TELAS) PLANOS DE ALGODÓN Y SUS MEZCLAS, INCLUYE HILANDERÍAS Y TEJEDURÍAS INTEGRADAS |
| 131209 | FABRICACIÓN DE TEJIDOS (TELAS) PLANOS DE FIBRAS TEXTILES N.C.P., INCLUYE HILANDERÍAS Y TEJEDURÍAS INTEGRADAS |
| 131300 | ACABADO DE PRODUCTOS TEXTILES |
| 132000 | EXTRACCION DE MINERALES METALIFEROS NO FERROSOS,EXCEPTO MINERALES DE URANIO Y TORIO |
| 139100 | FABRICACIÓN DE TEJIDOS DE PUNTO |
| 139201 | FABRICACIÓN DE FRAZADAS, MANTAS, PONCHOS, COLCHAS, COBERTORES, ETC. |
| 139202 | FABRICACIÓN DE ROPA DE CAMA Y MANTELERÍA |
| 139203 | FABRICACIÓN DE ARTÍCULOS DE LONA Y SUCEDÁNEOS DE LONA |
| 139204 | FABRICACIÓN DE BOLSAS DE MATERIALES TEXTILES PARA PRODUCTOS A GRANEL |
| 139209 | FABRICACIÓN DE ARTÍCULOS CONFECCIONADOS DE MATERIALES TEXTILES N.C.P., EXCEPTO PRENDAS DE VESTIR |
| 139300 | FABRICACIÓN DE TAPICES Y ALFOMBRAS |
| 139400 | FABRICACIÓN DE CUERDAS, CORDELES, BRAMANTES Y REDES |
| 139900 | FABRICACIÓN DE PRODUCTOS TEXTILES N.C.P. |
| 141100 | EXTRACCION DE ROCAS ORNAMENTALES |
| 141110 | CONFECCIÓN DE ROPA INTERIOR, PRENDAS PARA DORMIR Y PARA LA PLAYA |
| 141120 | CONFECCIÓN DE ROPA DE TRABAJO, UNIFORMES Y GUARDAPOLVOS |
| 141130 | CONFECCIÓN DE PRENDAS DE VESTIR PARA BEBÉS Y NIÑOS |
| 141140 | CONFECCIÓN DE PRENDAS DEPORTIVAS |
| 141191 | FABRICACIÓN DE ACCESORIOS DE VESTIR EXCEPTO DE CUERO |
| 141199 | CONFECCIÓN DE PRENDAS DE VESTIR N.C.P., EXCEPTO PRENDAS DE PIEL, CUERO Y DE PUNTO |
| 141200 | EXTRACCION DE PIEDRA CALIZA Y YESO |
| 141201 | FABRICACIÓN DE ACCESORIOS DE VESTIR DE CUERO |
| 141202 | CONFECCIÓN DE PRENDAS DE VESTIR DE CUERO |
| 141300 | EXTRACCION DE ARENAS,CANTO RODADO Y TRITURADOS PETREOS |
| 141400 | EXTRACCION DE ARCILLA Y CAOLIN |
| 142000 | TERMINACIÓN Y TEÑIDO DE PIELES, FABRICACIÓN DE ARTÍCULOS DE PIEL |
| 142110 | EXTRACCION DE MINERALES PARA LA FABRIC.DE ABONOS EXCEPTO TURBA. |
| 142120 | EXTRACCION DE MINERALES PARA LA FABRIC.DE PRODUCTOS QUIMICOS |
| 142200 | EXTRACCION DE SAL EN SALINAS Y DE ROCA |
| 142900 | EXPLOTACION DE MINAS Y CANTERAS N.C.P. |
| 143010 | FABRICACIÓN DE MEDIAS |
| 143020 | FABRICACIÓN DE PRENDAS DE VESTIR Y ARTÍCULOS SIMILARES DE PUNTO |
| 149000 | SERVICIOS INDUSTRIALES PARA LA INDUSTRIA CONFECCIONISTA |
| 151100 | CURTIDO Y TERMINACIÓN DE CUEROS |
| 151111 | MATANZA DE GANADO BOVINO |
| 151112 | PROCESAMIENTO DE CARNE DE GANADO BOVINO |
| 151113 | SALADERO Y PELADERO DE CUEROS DE GANADO BOVINO |
| 151120 | MATANZA Y PROCESAMIENTO DE CARNE DE AVES |
| 151130 | ELABORACION DE FIAMBRES Y EMBUTIDOS |
| 151140 | MATANZA DE GANADO EXCEPTO EL BOVINO Y PROCESAMIENTO DE SU CARNE |
| 151191 | FABRICACION DE ACEITES Y GRASAS DE ORIGEN ANIMAL |
| 151199 | MATANZA DE ANIMALES N.C.P.Y PROCESAMIENTO DE SU CARNE,ELABORACION DE SUBPRODUCTOS CARNICOS N.C.P. |
| 151200 | FABRICACIÓN DE MALETAS, BOLSOS DE MANO Y SIMILARES, ARTÍCULOS DE TALABARTERÍA Y ARTÍCULOS DE CUERO N.C.P. |
| 151201 | ELABORACION DE PESCADOS DE MAR,CRUSTACEOS Y PRODUCTOS MARINOS N.C.P. |
| 151202 | ELABORACION DE PESCADOS DE RIOS Y LAGUNAS Y OTROS PRODUCTOS FLUVIALES Y LACUSTRES |
| 151203 | FABRICACION DE ACEITES,GRASAS,HARINAS Y PRODUCTOS A BASE DE PESCADOS N.C.P. |
| 151310 | PREPARACION DE CONSERVAS DE FRUTAS,HORTALIZAS Y LEGUMBRES |
| 151320 | ELABORACION DE JUGOS NATURALES Y SUS CONCENTRADOS,DE FRUTAS,HORTALIZAS Y LEGUMBRES |
| 151330 | ELABORACION Y ENVASADO DE DULCES,MERMELADAS Y JALEAS |
| 151340 | ELABORACION DE FRUTAS,HORTALIZAS Y LEGUMBRES CONGELADAS |
| 151390 | ELABORACION DE FRUTAS,HORTALIZAS Y LEGUMBRES DESHIDRATADAS O DESECADAS,PREPARACION N.C.P.DE FRUTAS,HORTALIZAS Y LEGUMBRES |
| 151410 | ELABORACION DE ACEITES Y GRASAS VEGETALES SIN REFINAR Y SUS SUBPRODUCTOS,ELABORACION DE ACEITE VIRGEN |
| 151420 | ELABORACION DE ACEITES Y GRASAS VEGETALES REFINADAS |
| 151430 | ELABORACION DE MARGARINAS Y GRASAS VEGETALES COMESTIBLES SIMILARES |
| 152010 | ELABORACION DE LECHES Y PRODUCTOS LACTEOS DESHIDRATADOS |
| 152011 | FABRICACIÓN DE CALZADO DE CUERO, EXCEPTO CALZADO DEPORTIVO Y ORTOPÉDICO |
| 152020 | ELABORACION DE QUESOS |
| 152021 | FABRICACIÓN DE CALZADO DE MATERIALES N.C.P., EXCEPTO CALZADO DEPORTIVO Y ORTOPÉDICO |
| 152030 | ELABORACION INDUSTRIAL DE HELADOS |
| 152031 | FABRICACIÓN DE CALZADO DEPORTIVO |
| 152040 | FABRICACIÓN DE PARTES DE CALZADO |
| 152090 | ELABORACION DE PRODUCTOS LACTEOS N.C.P. |
| 153110 | MOLIENDA DE TRIGO |
| 153120 | PREPARACION DE ARROZ |
| 153131 | ELABORACION DE ALIMENTOS A BASE DE CEREALES |
| 153139 | PREPARACION Y MOLIENDA DE LEGUMBRES Y CEREALES N.C.P. |
| 153200 | ELABORACION DE ALMIDONES Y PRODUCTOS DERIVADOS DEL ALMIDON |
| 153300 | ELABORACION DE ALIMENTOS PREPARADOS PARA ANIMALES |
| 154110 | ELABORACION DE GALLETITAS Y BIZCOCHOS |
| 154120 | ELABORACION INDUSTRIAL DE PRODUCTOS DE PANADERIA,EXCLUIDO GALLETITAS Y BIZCOCHOS |
| 154191 | ELABORACION DE MASAS Y PRODUCTOS DE PASTELERIA |
| 154199 | ELABORACION DE PRODUCTOS DE PANADERIA N.C.P. |
| 154200 | ELABORACION DE AZUCAR |
| 154301 | ELABORACION DE CACAO,CHOCOLATE Y PRODUCTOS A BASE DE CACAO |
| 154309 | ELABORACION DE PRODUCTOS DE CONFITERIA N.C.P. |
| 154410 | ELABORACION DE PASTAS ALIMENTARIAS FRESCAS |
| 154420 | ELABORACION DE PASTAS ALIMENTARIAS SECAS |
| 154911 | TOSTADO,TORRADO Y MOLIENDA DE CAFE |
| 154912 | ELABORACION Y MOLIENDA DE HIERBAS AROMATICAS Y ESPECIAS |
| 154920 | PREPARACION DE HOJAS DE TE |
| 154930 | ELABORACION DE YERBA MATE |
| 154991 | ELABORACION DE EXTRACTOS,JARABES Y CONCENTRADOS |
| 154992 | ELABORACION DE VINAGRES |
| 154999 | ELABORACION DE PRODUCTOS ALIMENTICIOS N.C.P. |
| 155110 | DESTILACION DE ALCOHOL ETILICO |
| 155120 | DESTILACION,RECTIFICACION Y MEZCLA DE BEBIDAS ESPIRITOSAS |
| 155210 | ELABORACION DE VINOS |
| 155290 | ELABORACION DE SIDRA Y OTRAS BEBIDAS ALCOHOLICAS FERMENTADAS A PARTIR DE FRUTAS |
| 155300 | ELABORACION DE CERVEZA,BEBIDAS MALTEADAS Y DE MALTA |
| 155411 | EMBOTELLADO DE AGUAS NATURALES Y MINERALES |
| 155412 | FABRICACION DE SODAS |
| 155420 | ELABORACION DE BEBIDAS GASEOSAS,EXCEPTO SODA |
| 155490 | ELABORACION DE HIELO,JUGOS ENVASADOS PARA DILUIR Y OTRAS BEBIDAS NO ALCOHOLICAS |
| 160010 | PREPARACION DE HOJAS DE TABACO |
| 160091 | ELABORACION DE CIGARRILLOS |
| 160099 | ELABORACION DE PRODUCTOS DE TABACO N.C.P. |
| 161001 | ASERRADO Y CEPILLADO DE MADERA  NATIVA |
| 161002 | ASERRADO Y CEPILLADO DE MADERA IMPLANTADA |
| 162100 | FABRICACIÓN DE HOJAS DE MADERA PARA ENCHAPADO, FABRICACIÓN DE TABLEROS CONTRACHAPADOS, TABLEROS LAMINADOS, TABLEROS DE PARTÍCULAS Y TABLEROS Y PANELES N.C.P. |
| 162201 | FABRICACIÓN DE ABERTURAS Y ESTRUCTURAS DE MADERA PARA LA CONSTRUCCIÓN |
| 162202 | FABRICACIÓN DE VIVIENDAS PREFABRICADAS DE MADERA |
| 162300 | FABRICACIÓN DE RECIPIENTES DE MADERA |
| 162901 | FABRICACIÓN DE ATAÚDES |
| 162902 | FABRICACIÓN DE ARTÍCULOS DE MADERA EN TORNERÍAS |
| 162903 | FABRICACIÓN DE PRODUCTOS DE CORCHO |
| 162909 | FABRICACIÓN DE PRODUCTOS DE MADERA N.C.P, FABRICACIÓN DE ARTÍCULOS DE PAJA Y MATERIALES TRENZABLES |
| 170101 | FABRICACIÓN DE PASTA DE MADERA |
| 170102 | FABRICACIÓN DE PAPEL Y CARTÓN EXCEPTO ENVASES |
| 170201 | FABRICACIÓN DE PAPEL ONDULADO Y ENVASES DE PAPEL |
| 170202 | FABRICACIÓN DE CARTÓN ONDULADO Y ENVASES DE CARTÓN |
| 170910 | FABRICACIÓN DE ARTÍCULOS DE PAPEL Y CARTÓN DE USO DOMÉSTICO E HIGIÉNICO SANITARIO |
| 170990 | FABRICACIÓN DE ARTÍCULOS DE PAPEL Y CARTÓN N.C.P. |
| 171111 | DESMOTADO DE ALGODON,PREPARACION DE FIBRAS DE ALGODON |
| 171112 | PREPARACION DE FIBRAS TEXTILES VEGETALES EXCEPTO DE ALGODON |
| 171120 | PREPARACION DE FIBRAS ANIMALES DE USO TEXTIL,INCLUSO LAVADO DE LANA |
| 171131 | FABRICACION DE HILADOS DE LANA Y SUS MEZCLAS |
| 171132 | FABRICACION DE HILADOS DE ALGODON Y SUS MEZCLAS |
| 171139 | FABRICACION DE HILADOS TEXTILES EXCEPTO DE LANA Y DE ALGODON |
| 171141 | FABRICACION DE TEJIDOS (TELAS) PLANOS DE LANA Y SUS MEZCLAS |
| 171142 | FABRICACION DE TEJIDOS (TELAS) PLANOS DE ALGODON Y SUS MEZCLAS |
| 171143 | FABRICACION DE TEJIDOS (TELAS) PLANOS DE FIBRAS MANUFACTURADAS Y SEDA |
| 171148 | FABRICACION DE TEJIDOS (TELAS) PLANOS DE FIBRAS TEXTILES N.C.P. |
| 171149 | FABRICACION DE PRODUCTOS DE TEJEDURIA N.C.P. |
| 171200 | ACABADO DE PRODUCTOS TEXTILES |
| 172101 | FABRICACION DE FRAZADAS,MANTAS,PONCHOS,COLCHAS,COBERTORES,ETC. |
| 172102 | FABRICACION DE ROPA DE CAMA Y MANTELERIA |
| 172103 | FABRICACION DE ART. DE LONA Y SUCEDANEOS DE LONA |
| 172104 | FABRICACION DE BOLSAS DE MATERIALES TEXTILES PARA PRODUCTOS A GRANEL |
| 172109 | FABRICACION DE ART. CONFECCIONADOS DE MATERIALES TEXTILES EXCEPTO PRENDAS DE VESTIR N.C.P. |
| 172200 | FABRICACION DE TAPICES Y ALFOMBRAS |
| 172300 | FABRICACION DE CUERDAS,CORDELES,BRAMANTES Y REDES |
| 172900 | FABRICACION DE PRODUCTOS TEXTILES N.C.P. |
| 173010 | FABRICACION DE MEDIAS |
| 173020 | FABRICACION DE SUETERES Y ART. SIMILARES DE PUNTO |
| 173090 | FABRICACION DE TEJIDOS Y ART. DE PUNTO N.C.P. |
| 181101 | IMPRESIÓN DE DIARIOS Y REVISTAS |
| 181109 | IMPRESIÓN N.C.P., EXCEPTO DE DIARIOS Y REVISTAS |
| 181110 | CONFECCION DE ROPA INTERIOR,PRENDAS PARA DORMIR Y PARA LA PLAYA |
| 181120 | CONFECCION DE INDUMENTARIA DE TRABAJO,UNIFORMES,GUARDAPOLVOS Y SUS ACCESORIOS |
| 181130 | CONFECCION DE INDUMENTARIA PARA BEBES Y NIÑOS |
| 181191 | CONFECCION DE PILOTOS E IMPERMEABLES |
| 181192 | FABRICACION DE ACCESORIOS DE VESTIR EXCEPTO DE CUERO |
| 181199 | CONFECCION DE PRENDAS DE VESTIR N.C.P.,EXCEPTO LAS DE PIEL,CUERO Y SUCEDANEOS,PILOTOS E IMPERMEABLES |
| 181200 | SERVICIOS RELACIONADOS CON LA IMPRESIÓN |
| 181201 | FABRICACION DE ACCESORIOS DE VESTIR DE CUERO |
| 181202 | CONFECCION DE PRENDAS DE VESTIR DE CUERO |
| 182000 | REPRODUCCIÓN DE GRABACIONES |
| 182001 | CONFECCION DE PRENDAS DE VESTIR DE PIEL Y SUCEDANEOS |
| 182009 | TERMINACION Y TEÑIDO DE PIELES,FABRIC.DE ART. DE PIEL N.C.P. |
| 191000 | FABRICACIÓN DE PRODUCTOS DE HORNOS DE COQUE |
| 191100 | CURTIDO Y TERMINACION DE CUEROS |
| 191200 | FABRICACION DE MALETAS,BOLSOS DE MANO Y SIMILARES,ART. DE TALABARTERIA Y ART. DE CUERO N.C.P. |
| 192000 | FABRICACIÓN DE PRODUCTOS DE LA REFINACIÓN DEL PETRÓLEO |
| 192010 | FABRICACION DE CALZADO DE CUERO,EXCEPTO EL ORTOPEDICO |
| 192020 | FABRICACION DE CALZADO DE TELA,PLASTICO,GOMA,CAUCHO Y OTROS MATERIALES,EXCEPTO CALZADO ORTOPEDICO Y DE ASBESTO |
| 192030 | FABRICACION DE PARTES DE CALZADO |
| 201000 | ASERRADO Y CEPILLADO DE MADERA |
| 201110 | FABRICACIÓN DE GASES INDUSTRIALES Y MEDICINALES COMPRIMIDOS O LICUADOS |
| 201120 | FABRICACIÓN DE CURTIENTES NATURALES Y SINTÉTICOS |
| 201130 | FABRICACIÓN DE MATERIAS COLORANTES BÁSICAS, EXCEPTO PIGMENTOS PREPARADOS |
| 201140 | FABRICACIÓN DE COMBUSTIBLE NUCLEAR, SUSTANCIAS Y MATERIALES RADIACTIVOS |
| 201180 | FABRICACIÓN DE MATERIAS QUÍMICAS INORGÁNICAS BÁSICAS N.C.P. |
| 201190 | FABRICACIÓN DE MATERIAS QUÍMICAS ORGÁNICAS BÁSICAS N.C.P. |
| 201210 | FABRICACIÓN DE ALCOHOL |
| 201220 | FABRICACIÓN DE BIOCOMBUSTIBLES EXCEPTO ALCOHOL |
| 201300 | FABRICACIÓN DE ABONOS Y COMPUESTOS DE NITRÓGENO |
| 201401 | FABRICACIÓN DE RESINAS Y CAUCHOS SINTÉTICOS |
| 201409 | FABRICACIÓN DE MATERIAS PLÁSTICAS EN FORMAS PRIMARIAS N.C.P. |
| 202100 | FABRICACION DE HOJAS DE MADERA PARA ENCHAPADO,FABRIC.DE TABLEROS CONTRACHAPADOS,TABLEROS LAMINADOS,TABLEROS DE PARTICULAS Y TABLEROS Y PANELES N.C.P. |
| 202101 | FABRICACIÓN DE INSECTICIDAS, PLAGUICIDAS Y  PRODUCTOS QUÍMICOS DE USO AGROPECUARIO |
| 202200 | FABRICACIÓN DE PINTURAS, BARNICES Y PRODUCTOS DE REVESTIMIENTO SIMILARES, TINTAS DE IMPRENTA Y MASILLAS |
| 202201 | FABRICACION DE ABERTURAS Y ESTRUCTURAS DE MADERA PARA LA CONSTRUCCION |
| 202202 | FABRICACION DE VIVIENDAS PREFABRICADAS DE MADERA |
| 202300 | FABRICACION DE RECIPIENTES DE MADERA |
| 202311 | FABRICACIÓN DE PREPARADOS PARA LIMPIEZA, PULIDO Y SANEAMIENTO |
| 202312 | FABRICACIÓN DE JABONES Y DETERGENTES |
| 202320 | FABRICACIÓN DE COSMÉTICOS, PERFUMES Y  PRODUCTOS DE HIGIENE Y TOCADOR |
| 202901 | FABRICACION DE ART. DE CESTERIA,CAÑA Y MIMBRE |
| 202902 | FABRICACION DE ATAUDES |
| 202903 | FABRICACION DE ART. DE MADERA EN TORNERIAS |
| 202904 | FABRICACION DE PRODUCTOS DE CORCHO |
| 202906 | FABRICACIÓN DE EXPLOSIVOS Y PRODUCTOS DE PIROTECNIA |
| 202907 | FABRICACIÓN DE COLAS, ADHESIVOS, APRESTOS Y CEMENTOS EXCEPTO LOS ODONTOLÓGICOS OBTENIDOS DE SUSTANCIAS MINERALES Y VEGETALES |
| 202908 | FABRICACIÓN DE PRODUCTOS QUÍMICOS N.C.P. |
| 202909 | FABRICACION DE PRODUCTOS DE MADERA N.C.P |
| 203000 | FABRICACIÓN DE FIBRAS MANUFACTURADAS |
| 204000 | SERVICIOS INDUSTRIALES PARA LA FABRICACIÓN DE SUSTANCIAS Y PRODUCTOS QUÍMICOS |
| 210010 | FABRICACIÓN DE MEDICAMENTOS DE USO HUMANO Y PRODUCTOS FARMACÉUTICOS |
| 210013 | EXPLOTACION MINAS DE CARBON |
| 210020 | FABRICACIÓN DE MEDICAMENTOS DE USO VETERINARIO |
| 210030 | FABRICACIÓN DE SUSTANCIAS QUÍMICAS PARA LA ELABORACIÓN DE MEDICAMENTOS |
| 210090 | FABRICACIÓN DE PRODUCTOS DE LABORATORIO Y PRODUCTOS BOTÁNICOS DE USO FARMACEÚTICO N.C.P. |
| 210101 | FABRICACION DE PULPA DE MADERA |
| 210102 | FABRICACION DE PAPEL Y CARTON EXCEPTO ENVASES |
| 210201 | FABRICACION DE ENVASES DE PAPEL |
| 210202 | FABRICACION DE ENVASES DE CARTON |
| 210910 | FABRICACION DE ART. DE PAPEL Y CARTON DE USO DOMESTICO E HIGIENICO SANITARIO |
| 210990 | FABRICACION DE ART. DE PAPEL Y CARTON N.C.P. |
| 220019 | PRODUC PETROLEO Y GAS NATURAL |
| 221100 | EDICION DE LIBROS,FOLLETOS,PARTITURAS Y OTRAS PUBLICACIONES |
| 221110 | FABRICACIÓN DE CUBIERTAS Y CÁMARAS |
| 221120 | RECAUCHUTADO Y RENOVACIÓN DE CUBIERTAS |
| 221200 | EDICION DE PERIODICOS,REVISTAS Y PUBLICACIONES PERIODICAS |
| 221300 | EDICION DE GRABACIONES |
| 221900 | EDICION N.C.P. |
| 221901 | FABRICACIÓN DE  AUTOPARTES DE CAUCHO EXCEPTO CÁMARAS Y CUBIERTAS |
| 221909 | FABRICACIÓN  DE PRODUCTOS DE CAUCHO N.C.P. |
| 222010 | FABRICACIÓN DE ENVASES PLÁSTICOS |
| 222090 | FABRICACIÓN DE PRODUCTOS PLÁSTICOS EN FORMAS BÁSICAS Y ARTÍCULOS DE PLÁSTICO N.C.P., EXCEPTO MUEBLES |
| 222101 | IMPRESION DE DIARIOS Y REVISTAS |
| 222109 | IMPRESION EXCEPTO DE DIARIOS Y REVISTAS |
| 222200 | SERVICIOS RELACIONADOS CON LA IMPRESION |
| 223000 | REPRODUCCION DE GRABACIONES |
| 230103 | EXTRAC MINERAL DE HIERRO |
| 230200 | EXTRAC MINER METAL NO FERROSOS |
| 231000 | FABRICACION DE PRODUCTOS DE HORNOS DE COQUE |
| 231010 | FABRICACIÓN DE ENVASES DE VIDRIO |
| 231020 | FABRICACIÓN Y ELABORACIÓN DE VIDRIO PLANO |
| 231090 | FABRICACIÓN DE PRODUCTOS DE VIDRIO N.C.P. |
| 232000 | FABRICACION DE PRODUCTOS DE LA REFINACION DEL PETROLEO |
| 233000 | FABRICACION DE COMBUSTIBLE NUCLEAR |
| 239100 | FABRICACIÓN DE PRODUCTOS DE CERÁMICA REFRACTARIA |
| 239201 | FABRICACIÓN DE LADRILLOS |
| 239202 | FABRICACIÓN DE REVESTIMIENTOS CERÁMICOS |
| 239209 | FABRICACIÓN DE PRODUCTOS DE ARCILLA Y CERÁMICA NO REFRACTARIA PARA USO ESTRUCTURAL N.C.P. |
| 239310 | FABRICACIÓN DE ARTÍCULOS SANITARIOS DE CERÁMICA |
| 239391 | FABRICACIÓN DE OBJETOS CERÁMICOS PARA USO DOMÉSTICO EXCEPTO ARTEFACTOS SANITARIOS |
| 239399 | FABRICACIÓN DE ARTÍCULOS DE CERÁMICA NO REFRACTARIA PARA USO NO ESTRUCTURAL N.C.P. |
| 239410 | ELABORACIÓN DE CEMENTO |
| 239421 | ELABORACIÓN DE  YESO |
| 239422 | ELABORACIÓN DE CAL |
| 239510 | FABRICACIÓN DE MOSAICOS |
| 239591 | ELABORACIÓN DE HORMIGÓN |
| 239592 | FABRICACIÓN DE PREMOLDEADAS PARA LA CONSTRUCCIÓN |
| 239593 | FABRICACIÓN DE ARTÍCULOS DE CEMENTO, FIBROCEMENTO Y YESO EXCEPTO HORMIGÓN Y MOSAICOS |
| 239600 | CORTE, TALLADO Y ACABADO DE LA PIEDRA |
| 239900 | FABRICACIÓN DE PRODUCTOS MINERALES NO METÁLICOS N.C.P. |
| 241001 | LAMINACIÓN Y ESTIRADO. PRODUCCIÓN DE LINGOTES, PLANCHAS O BARRAS FABRICADAS POR OPERADORES INDEPENDIENTES |
| 241009 | FABRICACIÓN EN INDUSTRIAS BÁSICAS DE PRODUCTOS DE HIERRO Y ACERO N.C.P. |
| 241110 | FABRICACION DE GASES COMPRIMIDOS Y LICUADOS. |
| 241120 | FABRICACION DE CURTIENTES NATURALES Y SINTETICOS. |
| 241130 | FABRICACION DE MATERIAS COLORANTES BASICAS,EXCEPTO PIGMENTOS PREPARADOS. |
| 241180 | FABRICACION DE MATERIAS QUIMICAS INORGANICAS BASICAS N.C.P. |
| 241190 | FABRICACION DE MATERIAS QUIMICAS ORGANICAS BASICAS N.C.P. |
| 241200 | FABRICACION DE ABONOS Y COMPUESTOS DE NITROGENO |
| 241301 | FABRICACION DE RESINAS Y CAUCHOS SINTETICOS |
| 241309 | FABRICACION DE MATERIAS PLASTICAS EN FORMAS PRIMARIAS N.C.P. |
| 242010 | ELABORACIÓN DE ALUMINIO PRIMARIO Y SEMIELABORADOS DE ALUMINIO |
| 242090 | FABRICACIÓN DE PRODUCTOS PRIMARIOS DE METALES PRECIOSOS Y METALES NO FERROSOS N.C.P. Y SUS SEMIELABORADOS |
| 242100 | FABRICACION DE PLAGUICIDAS Y PRODUCTOS QUIMICOS DE USO AGROPECUARIO |
| 242200 | FABRICACION DE PINTURAS,BARNICES Y PRODUCTOS DE REVESTIMIENTO SIMILARES,TINTAS DE IMPRENTA Y MASILLAS |
| 242310 | FABRICACION DE MEDICAMENTOS DE USO HUMANO Y PRODUCTOS FARMACEUTICOS |
| 242320 | FABRICACION DE MEDICAMENTOS DE USO VETERINARIO |
| 242390 | FABRICACION DE PRODUCTOS DE LABORATORIO, SUSTANCIAS QUIMICAS MEDICINALES Y PRODUCTOS BOTANICOS N.C.P. |
| 242411 | FABRICACION DE PREPARADOS PARA LIMPIEZA,PULIDO Y SANEAMIENTO |
| 242412 | FABRICACION DE JABONES Y DETERGENTES |
| 242490 | FABRICACION DE COSMETICOS,PERFUMES Y PRODUCTOS DE HIGIENE Y TOCADOR |
| 242901 | FABRICACION DE TINTAS |
| 242902 | FABRICACION DE EXPLOSIVOS,MUNICIONES Y PRODUCTOS DE PIROTECNIA |
| 242903 | FABRICACION DE COLAS,ADHESIVOS,APRESTOS Y CEMENTOS EXCEPTO LOS ODONTOLOGICOS OBTENIDOS DE SUSTANCIAS MINERALES Y VEGETALES |
| 242909 | FABRICACION DE PRODUCTOS QUIMICOS N.C.P. |
| 243000 | FABRICACION DE FIBRAS MANUFACTURADAS |
| 243100 | FUNDICIÓN DE HIERRO Y ACERO |
| 243200 | FUNDICIÓN DE METALES NO FERROSOS |
| 251101 | FABRICACIÓN DE CARPINTERÍA METÁLICA |
| 251102 | FABRICACIÓN DE PRODUCTOS METÁLICOS PARA USO ESTRUCTURAL |
| 251110 | FABRICACION DE CUBIERTAS Y CAMARAS |
| 251120 | RECAUCHUTADO Y RENOVACION DE CUBIERTAS |
| 251200 | FABRICACIÓN DE TANQUES, DEPÓSITOS Y RECIPIENTES DE METAL |
| 251300 | FABRICACIÓN DE GENERADORES DE VAPOR |
| 251901 | FABRICACION DE AUTOPARTES DE CAUCHO EXCEPTO CAMARAS Y CUBIERTAS |
| 251909 | FABRICACION DE PRODUCTOS DE CAUCHO N.C.P. |
| 252000 | FABRICACIÓN DE ARMAS Y MUNICIONES |
| 252010 | FABRICACION DE ENVASES PLASTICOS |
| 252090 | FABRICACION DE PRODUCTOS PLASTICOS EN FORMAS BASICAS Y ART. DE PLASTICO N.C.P.,EXCEPTO MUEBLES |
| 259100 | FORJADO, PRENSADO, ESTAMPADO Y LAMINADO DE METALES, PULVIMETALURGIA |
| 259200 | TRATAMIENTO Y REVESTIMIENTO DE METALES Y TRABAJOS DE METALES EN GENERAL |
| 259301 | FABRICACIÓN DE HERRAMIENTAS MANUALES Y SUS ACCESORIOS |
| 259302 | FABRICACIÓN DE ARTÍCULOS DE CUCHILLERÍA Y UTENSILLOS DE MESA Y DE COCINA |
| 259309 | FABRICACIÓN DE CERRADURAS, HERRAJES Y ARTÍCULOS DE FERRETERÍA N.C.P. |
| 259910 | FABRICACIÓN DE ENVASES METÁLICOS |
| 259991 | FABRICACIÓN DE TEJIDOS DE ALAMBRE |
| 259992 | FABRICACIÓN DE CAJAS DE SEGURIDAD |
| 259993 | FABRICACIÓN DE PRODUCTOS METÁLICOS DE TORNERÍA Y/O MATRICERÍA |
| 259999 | FABRICACIÓN DE PRODUCTOS ELABORADOS DE METAL N.C.P. |
| 261000 | FABRICACIÓN DE COMPONENTES ELECTRÓNICOS |
| 261010 | FABRICACION DE ENVASES DE VIDRIO |
| 261020 | FABRICACION Y ELABORACION DE VIDRIO PLANO |
| 261091 | FABRICACION DE ESPEJOS Y VITRALES |
| 261099 | FABRICACION DE PRODUCTOS DE VIDRIO N.C.P. |
| 262000 | FABRICACIÓN DE EQUIPOS Y PRODUCTOS INFORMÁTICOS |
| 263000 | FABRICACIÓN  DE EQUIPOS DE COMUNICACIONES Y TRANSMISORES DE RADIO Y TELEVISIÓN |
| 264000 | FABRICACIÓN DE RECEPTORES DE RADIO Y TELEVISIÓN, APARATOS DE GRABACIÓN Y REPRODUCCIÓN DE SONIDO Y VIDEO, Y PRODUCTOS CONEXOS |
| 265101 | FABRICACIÓN DE INSTRUMENTOS Y APARATOS PARA MEDIR, VERIFICAR, ENSAYAR, NAVEGAR Y OTROS FINES, EXCEPTO EL EQUIPO DE CONTROL DE PROCESOS INDUSTRIALES |
| 265102 | FABRICACIÓN DE EQUIPO DE CONTROL DE PROCESOS INDUSTRIALES |
| 265200 | FABRICACIÓN DE RELOJES |
| 266010 | FABRICACIÓN DE EQUIPO MÉDICO Y QUIRÚRGICO Y DE APARATOS ORTOPÉDICOS PRINCIPALMENTE ELECTRÓNICOS Y/O ELÉCTRICOS |
| 266090 | FABRICACIÓN DE EQUIPO MÉDICO Y QUIRÚRGICO Y DE APARATOS ORTOPÉDICOS N.C.P. |
| 267001 | FABRICACIÓN DE EQUIPAMIENTO E INSTRUMENTOS ÓPTICOS Y SUS ACCESORIOS |
| 267002 | FABRICACIÓN DE APARATOS Y ACCESORIOS PARA FOTOGRAFÍA EXCEPTO PELÍCULAS, PLACAS Y PAPELES SENSIBLES |
| 268000 | FABRICACIÓN DE SOPORTES ÓPTICOS Y MAGNÉTICOS |
| 269110 | FABRICACION DE ART. SANITARIOS DE CERAMICA |
| 269191 | FABRICACION DE OBJETOS CERAMICOS PARA USO INDUSTRIAL Y DE LABORATORIO |
| 269192 | FABRICACION DE OBJETOS CERAMICOS PARA USO DOMESTICO EXCEPTO ARTEFACTOS SANITARIOS |
| 269193 | FABRICACION DE OBJETOS CERAMICOS EXCEPTO REVESTIMIENTOS DE PISOS Y PAREDES N.C.P. |
| 269200 | FABRICACION DE PRODUCTOS DE CERAMICA REFRACTARIA |
| 269301 | FABRICACION DE LADRILLOS |
| 269302 | FABRICACION DE REVESTIMIENTOS CERAMICOS |
| 269309 | FABRICACION DE PRODUCTOS DE ARCILLA Y CERAMICA NO REFRACTARIA PARA USO ESTRUCTURAL N.C.P. |
| 269410 | ELABORACION DE CEMENTO |
| 269421 | ELABORACION DE YESO |
| 269422 | ELABORACION DE CAL |
| 269510 | FABRICACION DE MOSAICOS |
| 269591 | FABRICACION DE ART. DE CEMENTO Y FIBROCEMENTO |
| 269592 | FABRICACION DE PREMOLDEADAS PARA LA CONSTRUCCION |
| 269600 | CORTE,TALLADO Y ACABADO DE LA PIEDRA |
| 269910 | ELABORACION PRIMARIA N.C.P.DE MINERALES NO METALICOS |
| 269990 | FABRICACION DE PRODUCTOS MINERALES NO METALICOS N.C.P. |
| 271001 | FUNDICION EN ALTOS HORNOS Y ACERIAS.PRODUCCION DE LINGOTES,PLANCHAS O BARRAS |
| 271002 | LAMINACION Y ESTIRADO |
| 271009 | FABRICACION EN INDUSTRIAS BASICAS DE PRODUCTOS DE HIERRO Y ACERO N.C.P. |
| 271010 | FABRICACIÓN DE MOTORES, GENERADORES Y TRANSFORMADORES ELÉCTRICOS |
| 271020 | FABRICACIÓN DE APARATOS DE DISTRIBUCIÓN Y CONTROL DE LA ENERGÍA ELÉCTRICA |
| 272000 | FABRICACIÓN DE ACUMULADORES, PILAS Y BATERÍAS PRIMARIAS |
| 272010 | ELABORACION DE ALUMINIO PRIMARIO Y SEMIELABORADOS DE ALUMINIO |
| 272090 | PRODUCCION DE METALES NO FERROSOS N.C.P.Y SUS SEMIELABORADOS |
| 273100 | FUNDICION DE HIERRO Y ACERO |
| 273110 | FABRICACIÓN DE CABLES DE FIBRA ÓPTICA |
| 273190 | FABRICACIÓN DE HILOS Y CABLES AISLADOS N.C.P. |
| 273200 | FUNDICION DE METALES NO FERROSOS |
| 274000 | FABRICACIÓN DE LÁMPARAS ELÉCTRICAS Y EQUIPO DE ILUMINACIÓN |
| 275010 | FABRICACIÓN DE COCINAS, CALEFONES, ESTUFAS Y CALEFACTORES NO ELÉCTRICOS |
| 275020 | FABRICACIÓN DE HELADERAS, FREEZERS, LAVARROPAS Y SECARROPAS |
| 275091 | FABRICACIÓN DE VENTILADORES, EXTRACTORES DE AIRE, ASPIRADORAS Y SIMILARES |
| 275092 | FABRICACIÓN DE PLANCHAS, CALEFACTORES, HORNOS ELÉCTRICOS, TOSTADORAS Y OTROS APARATOS GENERADORES DE CALOR |
| 275099 | FABRICACIÓN DE APARATOS DE USO DOMÉSTICO N.C.P. |
| 279000 | FABRICACIÓN  DE EQUIPO ELÉCTRICO N.C.P. |
| 281100 | FABRICACIÓN  DE  MOTORES  Y  TURBINAS,  EXCEPTO  MOTORES  PARA AERONAVES, VEHÍCULOS AUTOMOTORES   Y MOTOCICLETAS |
| 281101 | FABRICACION DE CARPINTERIA METALICA |
| 281102 | FABRICACION DE ESTRUCTURAS METALICAS PARA LA CONSTRUCCION |
| 281200 | FABRICACION DE TANQUES,DEPOSITOS Y RECIPIENTES DE METAL |
| 281201 | FABRICACIÓN DE BOMBAS |
| 281300 | FABRICACION DE GENERADORES DE VAPOR |
| 281301 | FABRICACIÓN DE COMPRESORES, GRIFOS Y VÁLVULAS |
| 281400 | FABRICACIÓN DE COJINETES, ENGRANAJES, TRENES DE ENGRANAJE Y PIEZAS DE TRANSMISIÓN |
| 281500 | FABRICACIÓN DE HORNOS, HOGARES Y QUEMADORES |
| 281600 | FABRICACIÓN DE MAQUINARIA Y EQUIPO DE ELEVACIÓN Y MANIPULACIÓN |
| 281700 | FABRICACIÓN DE MAQUINARIA Y EQUIPO DE OFICINA, EXCEPTO EQUIPO INFORMÁTICO |
| 281900 | FABRICACIÓN DE  MAQUINARIA Y EQUIPO DE USO GENERAL N.C.P. |
| 282110 | FABRICACIÓN DE TRACTORES |
| 282120 | FABRICACIÓN DE MAQUINARIA Y EQUIPO DE USO AGROPECUARIO Y FORESTAL |
| 282130 | FABRICACIÓN DE IMPLEMENTOS DE USO AGROPECUARIO |
| 282200 | FABRICACIÓN DE MÁQUINAS HERRAMIENTA |
| 282300 | FABRICACIÓN DE MAQUINARIA METALÚRGICA |
| 282400 | FABRICACIÓN DE MAQUINARIA PARA LA EXPLOTACIÓN DE MINAS Y CANTERAS Y PARA OBRAS DE CONSTRUCCIÓN |
| 282500 | FABRICACIÓN DE MAQUINARIA PARA LA ELABORACIÓN DE ALIMENTOS, BEBIDAS Y TABACO |
| 282600 | FABRICACIÓN DE MAQUINARIA PARA LA ELABORACIÓN DE PRODUCTOS TEXTILES, PRENDAS DE VESTIR Y CUEROS |
| 282901 | FABRICACIÓN DE MAQUINARIA PARA LA INDUSTRIA DEL PAPEL Y LAS ARTES GRÁFICAS |
| 282909 | FABRICACIÓN DE MAQUINARIA Y EQUIPO DE USO ESPECIAL N.C.P. |
| 289100 | FORJADO,PRENSADO,ESTAMPADO Y LAMINADO DE METALES,PULVIMETALURGIA |
| 289200 | TRATAMIENTO Y REVESTIMIENTO DE METALES,OBRAS DE INGENIERIA MECANICA EN GENERAL REALIZADAS A CAMBIO DE UNA RETRIBUCION O POR CONTRATA |
| 289301 | FABRICACION DE HERRAMIENTAS MANUALES Y SUS ACCESORIOS |
| 289302 | FABRICACION DE ART. DE CUCHILLERIA Y UTENSILLOS DE MESA Y DE COCINA |
| 289309 | FABRICACION DE CERRADURAS,HERRAJES Y ART. DE FERRETERIA N.C.P. |
| 289910 | FABRICACION DE ENVASES METALICOS |
| 289991 | FABRICACION DE TEJIDOS DE ALAMBRE |
| 289992 | FABRICACION DE CAJAS DE SEGURIDAD |
| 289993 | FABRICACION DE PRODUCTOS METALICOS DE TORNERIA Y/O MATRICERIA |
| 289999 | FABRICACION DE PRODUCTOS METALICOS N.C.P. |
| 290114 | EXTRAC PIEDRA P/ CONSTRUCCION |
| 290122 | EXTRAC ARENA |
| 290130 | EXTRAC ARCILLA |
| 290149 | EXTRAC PIEDRA CALIZA (CAL/CEM) |
| 290203 | EXTRAC MINERAL P/PROD QUIMICOS |
| 290300 | EXPLOT MINAS DE SAL (SALINAS) |
| 290904 | EXTRAC MINERALES NO CLASIF |
| 291000 | FABRICACIÓN DE VEHÍCULOS AUTOMOTORES |
| 291100 | FABRICACION DE MOTORES Y TURBINAS, EXCEPTO MOTORES PARA AERONAVES,VEHICULOS AUTOMOTORES Y MOTOCICLETAS |
| 291200 | FABRICACION DE BOMBAS,COMPRESORES,GRIFOS Y VALVULAS |
| 291300 | FABRICACION DE COJINETES,ENGRANAJES,TRENES DE ENGRANAJE Y PIEZAS DE TRANSMISION |
| 291400 | FABRICACION DE HORNOS,HOGARES Y QUEMADORES |
| 291500 | FABRICACION DE EQUIPO DE ELEVACION Y MANIPULACION |
| 291900 | FABRICACION DE MAQUINARIA DE USO GENERAL N.C.P. |
| 292000 | FABRICACIÓN DE CARROCERÍAS PARA VEHÍCULOS AUTOMOTORES, FABRICACIÓN DE REMOLQUES Y SEMIRREMOLQUES |
| 292110 | FABRICACION DE TRACTORES |
| 292190 | FABRICACION DE MAQUINARIA AGROPECUARIA Y FORESTAL,EXCEPTO TRACTORES |
| 292200 | FABRICACION DE MAQUINAS HERRAMIENTA |
| 292300 | FABRICACION DE MAQUINARIA METALURGICA |
| 292400 | FABRICACION DE MAQUINARIA PARA LA EXPLOTACION DE MINAS Y CANTERAS Y PARA OBRAS DE CONSTRUCCION |
| 292500 | FABRICACION DE MAQUINARIA PARA LA ELABORACION DE ALIMENTOS,BEBIDAS Y TABACO |
| 292600 | FABRICACION DE MAQUINARIA PARA LA ELABORACION DE PRODUCTOS TEXTILES,PRENDAS DE VESTIR Y CUEROS |
| 292700 | FABRICACION DE ARMAS Y MUNICIONES |
| 292901 | FABRICACION DE MAQUINARIA PARA LA INDUSTRIA DEL PAPEL Y LAS ARTES GRAFICAS |
| 292909 | FABRICACION DE MAQUINARIA DE USO ESPECIAL N.C.P. |
| 293010 | FABRICACION DE COCINAS,CALEFONES,ESTUFAS Y CALEFACTORES DE USO DOMESTICO NO ELECTRICOS |
| 293011 | RECTIFICACIÓN DE MOTORES |
| 293020 | FABRICACION DE HELADERAS,FREEZERS,LAVARROPAS Y SECARROPAS |
| 293090 | FABRICACIÓN DE PARTES, PIEZAS Y ACCESORIOS PARA VEHÍCULOS AUTOMOTORES Y SUS MOTORES N.C.P. |
| 293091 | FABRICACION DE MAQUINAS DE COSER Y TEJER |
| 293092 | FABRICACION DE VENTILADORES,EXTRACTORES Y ACONDICIONADORES DE AIRE,ASPIRADORAS Y SIMILARES |
| 293093 | FABRICACION DE ENCERADORAS,PULIDORAS,BATIDORAS,LICUADORAS Y SIMILARES |
| 293094 | FABRICACION DE PLANCHAS,CALEFACTORES,HORNOS ELECTRICOS,TOSTADORAS Y OTROS APARATOS GENERADORES DE CALOR |
| 293095 | FABRICACION DE ARTEFACTOS PARA ILUMINACION EXCEPTO LOS ELECTRICOS |
| 293099 | FABRICACION DE APARATOS Y ACCESORIOS ELECTRICOS N.C.P. |
| 300000 | FABRICACION DE MAQUINARIA DE OFICINA,CONTABILIDAD E INFORMATICA |
| 301100 | CONSTRUCCIÓN Y REPARACIÓN DE BUQUES |
| 301200 | CONSTRUCCIÓN Y REPARACIÓN DE EMBARCACIONES DE RECREO Y DEPORTE |
| 302000 | FABRICACIÓN Y REPARACIÓN DE LOCOMOTORAS Y DE MATERIAL RODANTE PARA TRANSPORTE FERROVIARIO |
| 303000 | FABRICACIÓN Y REPARACIÓN DE AERONAVES |
| 309100 | FABRICACIÓN DE MOTOCICLETAS |
| 309200 | FABRICACIÓN DE BICICLETAS Y DE SILLONES DE RUEDAS ORTOPÉDICOS |
| 309900 | FABRICACIÓN DE EQUIPO DE TRANSPORTE N.C.P. |
| 310010 | FABRICACIÓN DE MUEBLES Y PARTES DE MUEBLES, PRINCIPALMENTE DE MADERA |
| 310020 | FABRICACIÓN DE MUEBLES Y PARTES DE MUEBLES, EXCEPTO LOS QUE SON PRINCIPALMENTE DE MADERA (METAL, PLÁSTICO, ETC.) |
| 310030 | FABRICACIÓN DE SOMIERES Y COLCHONES |
| 311000 | FABRICACION DE MOTORES,GENERADORES Y TRANSFORMADORES ELECTRICOS |
| 311111 | MATANZA GANADOS MATADEROS |
| 311138 | FRIGORIFICOS |
| 311146 | MATANZA PREPAR Y CONSERV AVES |
| 311154 | MATANZA ANIMALES NO CLASIF |
| 311162 | ELAB FIAMBRES EMBUT CHACINADO |
| 311219 | FABRIC QUESOS Y MANTECAS |
| 311227 | ELAB Y PASTEURIZACION DE LECHE |
| 311235 | FABRIC PRODUC LACTEOS N/CLASIF |
| 311316 | ELAB ENVAS FRUTAS LEGUM Y JUGO |
| 311324 | ELABOR FRUTAS Y LEGUMB SECAS |
| 311332 | ELABOR ENVAS CALDOS Y SOPAS |
| 311340 | ELABOR ENVAS DULCES JALEAS |
| 311413 | ELABOR ENVAS PESCADOS DE MAR |
| 311421 | ELABOR ENVAS PESCADOS DE RIO |
| 311510 | FABR ACEITE GRASA VEGET COMEST |
| 311529 | FABR ACEITE GRASA ANIM NO COM |
| 311537 | FABRIC ACEITE HARINA PESCADO |
| 311618 | MOLIEN TRIGO |
| 311626 | MOLIEN PULIDO Y LIMPIE ARROZ |
| 311634 | MOLIEN LEGUMB Y CEREAL NO CLAS |
| 311642 | MOLIEN YERBA MATE |
| 311650 | ELABOR ALIMENTO A BASE CEREAL |
| 311669 | ELABOR SEMILLAS SECAS |
| 311715 | FABR PAN Y PRODUCTOS NO SECOS |
| 311723 | FABR GALLETITAS PRODUCT SECOS |
| 311731 | FABRIC MASAS PASTELERIA |
| 311758 | FABRIC PASTAS FRESCAS |
| 311766 | FABRIC PASTAS SECAS |
| 311812 | FABR Y REFIN AZUCAR INGENIOS |
| 311820 | FABR Y REFIN AZUCAR NO CLASIF |
| 311928 | FABRIC CACAO CHOCOLATE BOMBON |
| 311936 | FABR PRODUC CONFITER NO CLASIF |
| 312000 | FABRICACION DE APARATOS DE DISTRIBUCION Y CONTROL DE LA ENERGIA ELECTRICA |
| 312118 | ELABOR TE |
| 312126 | TOSTADO TORRADO MOLIENDA CAFE |
| 312134 | ELAB CONCENTRADO CAFE TE YERBA |
| 312142 | FABRIC HIELO EXCEPTO SECO |
| 312150 | ELABOR MOLIENDA ESPECIAS |
| 312169 | ELABOR VINAGRES |
| 312177 | REFINACION Y MOLIENDA DE SAL |
| 312185 | ELABOR EXTRACT JARABES CONCENT |
| 312193 | FABR PRODUC ALIMENTAR N/CLASIF |
| 312215 | FABRIC ALIMENTOS P/ ANIMALES |
| 313000 | FABRICACION DE HILOS Y CABLES AISLADOS |
| 313114 | DESTILACION BEBID ALCOHOLICAS |
| 313122 | DESTILACION ALCOHOL ETILICO |
| 313211 | FABRIC VINOS |
| 313238 | FABRIC SIDRAS BEBI FERMENTADAS |
| 313246 | FABR SUBPROD DE UVA NO CLASIF |
| 313319 | FABRIC MALTA CERVEZA |
| 313416 | EMBOTELL AGUA NATUR Y MINERAL |
| 313424 | FABRIC SODA |
| 313432 | ELABOR BEBIDAS NO ALCOHOLICAS |
| 314000 | FABRICACION DE ACUMULADORES Y DE PILAS Y BATERIAS PRIMARIAS |
| 314013 | FABRIC CIGARRILLOS |
| 314021 | FABRIC PRODUC TABACO NO CLASIF |
| 315000 | FABRICACION DE LAMPARAS ELECTRICAS Y EQUIPO DE ILUMINACION |
| 319000 | FABRICACION DE EQUIPO ELECTRICO N.C.P. |
| 321000 | FABRICACION DE TUBOS,VALVULAS Y OTROS COMPONENTES ELECTRONICOS |
| 321011 | FABRICACIÓN DE JOYAS FINAS Y ARTÍCULOS CONEXOS |
| 321012 | FABRICACIÓN DE OBJETOS DE PLATERÍA |
| 321020 | FABRICACIÓN DE BIJOUTERIE |
| 321028 | PREPARAC FIBRAS ALGODON |
| 321036 | PREPARAC FIBRAS TEXTIL VEGETAL |
| 321044 | LAVADO LIMPIEZA LANA LAVADERO |
| 321052 | HILADO LANA HILANDERIAS |
| 321060 | HILADO ALGODON HILANDERIAS |
| 321079 | HILADO FIBRA N/LANA NI ALGODON |
| 321087 | ACABADO TEXTIL TINTORERIAS |
| 321117 | TEJIDO LANA TEJEDURIAS |
| 321125 | TEJIDO ALGODON TEJEDURIAS |
| 321133 | TEJIDO FIBRAS SINTETIC Y SEDA |
| 321141 | TEJIDO FIBRAS TEXTIL NO CLASIF |
| 321168 | FABRIC PRODUC TEJEDU NO CLASIF |
| 321214 | FABRIC FRAZADAS MANTAS |
| 321222 | FABRIC ROPA CAMA MANTELERIA |
| 321230 | FABRIC ARTICULOS DE LONA |
| 321249 | FABRIC BOLSAS TEXTILES |
| 321281 | FAB ART MATER TEXTIL NO CLASIF |
| 321311 | FABRIC MEDIAS |
| 321338 | FABRIC TEJIDOS ARTIC DE PUNTO |
| 321346 | ACABADO TEJIDOS DE PUNTO |
| 321419 | FABRIC TAPICES Y ALFOMBRAS |
| 321516 | FABR SOGAS CORDELES Y CONEXOS |
| 321915 | FABR CONF ART TEXTIL NO CLASIF |
| 322000 | FABRICACION DE TRANSMISORES DE RADIO Y TELEVISION Y DE APARATOS PARA TELEFONIA Y TELEGRAFIA CON HILOS |
| 322001 | FABRICACIÓN DE INSTRUMENTOS DE MÚSICA |
| 322016 | CONFEC PRENDAS VESTIR N/PIELES |
| 322024 | CONF PRENDAS VESTIR DE PIELES |
| 322032 | CONFEC PRENDAS VESTIR DE CUERO |
| 322040 | CONFEC PILOTOS E IMPERMEABLES |
| 322059 | FABRIC ACCESORIOS P/ VESTIR |
| 322067 | FABRIC UNIFORMES Y SUS ACCESOR |
| 323000 | FABRICACION DE RECEPTORES DE RADIO Y TELEVISION,APARATOS DE GRABACION Y REPRODUCCION DE SONIDO Y VIDEO,Y PRODUCTOS CONEXOS |
| 323001 | FABRICACIÓN DE ARTÍCULOS DE DEPORTE |
| 323128 | SALADO PELADO DE CUEROS |
| 323136 | CURTIDO CUERO CURTIEMBRES |
| 323217 | PREP DECOLOR TEÑIDO DE PIELES |
| 323225 | CONFEC ART PIEL N/PREND VESTIR |
| 323314 | FABRIC PRODUCT CUERO N/CALZADO |
| 324000 | FABRICACIÓN DE JUEGOS Y JUGUETES |
| 324019 | FABRIC CALZADO DE CUERO |
| 324027 | FAB CALZADO TELA Y OTROS MATER |
| 329010 | FABRICACIÓN DE LÁPICES, LAPICERAS,  BOLÍGRAFOS, SELLOS Y ARTÍCULOS SIMILARES PARA OFICINAS Y ARTISTAS |
| 329020 | FABRICACIÓN DE ESCOBAS, CEPILLOS Y PINCELES |
| 329030 | FABRICACIÓN DE CARTELES, SEÑALES E INDICADORES  -ELÉCTRICOS O NO- |
| 329040 | FABRICACIÓN DE EQUIPO DE PROTECCIÓN Y SEGURIDAD, EXCEPTO CALZADO |
| 329090 | INDUSTRIAS MANUFACTURERAS N.C.P. |
| 331100 | FABRICACION DE EQUIPO MEDICO Y QUIRURGICO Y DE APARATOS ORTOPEDICOS |
| 331101 | REPARACIÓN Y MANTENIMIENTO DE PRODUCTOS DE METAL, EXCEPTO MAQUINARIA Y EQUIPO |
| 331112 | PREPAR Y CONS MADERA ASERRADER |
| 331120 | PREPAR MADERAS TERCIADAS |
| 331139 | FABRIC PUERTAS VENTANAS |
| 331147 | FABRIC VIVIENDA PREFABRICADA |
| 331200 | FABRICACION DE INSTRUMENTOS Y APARATOS PARA MEDIR,VERIFICAR,ENSAYAR,NAVEGAR Y OTROS FINES,EXCEPTO EL EQUIPO DE CONTROL DE PROCESOS INDUSTRIALES |
| 331210 | REPARACIÓN Y MANTENIMIENTO DE MAQUINARIA DE USO GENERAL |
| 331220 | REPARACIÓN Y MANTENIMIENTO DE MAQUINARIA Y EQUIPO DE USO AGROPECUARIO Y FORESTAL |
| 331228 | FABR ENVASES Y EMBALAJE MADERA |
| 331236 | FABRIC ARTIC DE CAÑA Y MIMBRE |
| 331290 | REPARACIÓN Y MANTENIMIENTO DE MAQUINARIA DE USO ESPECIAL N.C.P. |
| 331300 | FABRICACION DE EQUIPO DE CONTROL DE PROCESOS INDUSTRIALES |
| 331301 | REPARACIÓN Y MANTENIMIENTO DE INSTRUMENTOS MÉDICOS, ÓPTICOS Y DE PRECISIÓN, EQUIPO FOTOGRÁFICO, APARATOS PARA MEDIR, ENSAYAR O NAVEGAR, RELOJES, EXCEPTO PARA USO PERSONAL O DOMÉSTI |
| 331400 | REPARACIÓN Y MANTENIMIENTO DE MAQUINARIA Y APARATOS ELÉCTRICOS |
| 331900 | REPARACIÓN Y MANTENIMIENTO DE MÁQUINAS Y EQUIPO N.C.P. |
| 331910 | FABRIC ATAUDES |
| 331929 | FABRIC ARTIC MADERA TORNEADA |
| 331937 | FABRIC PRODUCTOS DE CORCHO |
| 331945 | FABRIC PRODUCT MADERA N/CLASIF |
| 332000 | INSTALACIÓN DE MAQUINARIA Y EQUIPOS INDUSTRIALES |
| 332001 | FABRICACION DE APARATOS Y ACCESORIOS PARA FOTOGRAFIA EXCEPTO PELICULAS,PLACAS Y PAPELES SENSIBLES |
| 332002 | FABRICACION DE LENTES Y OTROS ART. OFTALMICOS |
| 332003 | FABRICACION DE INSTRUMENTOS DE OPTICA |
| 332011 | FABRIC MUEBLES Y ACCESORIOS |
| 332038 | FABRIC COLCHONES |
| 333000 | FABRICACION DE RELOJES |
| 341000 | FABRICACION DE VEHICULOS AUTOMOTORES |
| 341118 | FABRIC PULPA DE MADERA |
| 341126 | FABRIC PAPEL Y CARTON |
| 341215 | FABRIC ENVASES DE PAPEL |
| 341223 | FABRIC ENVASES DE CARTON |
| 341916 | FABRIC ARTIC PAPEL NO CLASIF |
| 342000 | FABRICACION DE CARROCERIAS PARA VEHICULOS AUTOMOTORES,FABRIC.DE REMOLQUES Y SEMIRREMOLQUES |
| 342017 | IMPRESION Y ENCUADERNACION |
| 342025 | SERVIC RELACIONADOS C/IMPRENTA |
| 342033 | IMPRESION DIARIOS Y REVISTAS |
| 342041 | EDITORIA EDICION LIBROS PUBLIC |
| 343000 | FABRICACION DE PARTES,PIEZAS Y ACCESORIOS PARA VEHICULOS AUTOMOTORES Y SUS MOTORES |
| 351100 | CONSTRUCCION Y REPARACION DE BUQUES |
| 351110 | GENERACIÓN DE ENERGÍA TÉRMICA CONVENCIONAL |
| 351113 | DESTIL DE ALCOHOLES NO ETILICO |
| 351120 | GENERACIÓN DE ENERGÍA TÉRMICA NUCLEAR |
| 351121 | FABRIC GASES COMPR Y LICUADOS |
| 351130 | GENERACIÓN DE ENERGÍA HIDRÁULICA |
| 351148 | FABRIC GASES COMPR LICUA U DOM |
| 351156 | FABRIC TANINO |
| 351164 | FABR SUSTANC QUIMICAS N/CLASIF |
| 351190 | GENERACIÓN DE ENERGÍA N.C.P. |
| 351200 | CONSTRUCCION Y REPARACION DE EMBARCACIONES DE RECREO Y DEPORTE |
| 351201 | TRANSPORTE DE ENERGÍA ELÉCTRICA |
| 351210 | FABRIC ABONOS Y FERTILIZANTES |
| 351229 | FABRIC PLAGUICIDAS |
| 351310 | COMERCIO MAYORISTA DE ENERGÍA ELÉCTRICA |
| 351318 | FABRIC RESIN CAUCHOS SINTETICO |
| 351320 | DISTRIBUCIÓN DE ENERGÍA ELÉCTRICA |
| 351326 | FABRIC MATERIAS PLASTICAS |
| 351334 | FABRIC FIBRA ARTIFIC NO CLASIF |
| 352000 | FABRICACION DE LOCOMOTORAS Y DE MATERIAL RODANTE PARA FERROCARRILES Y TRANVIAS |
| 352010 | FABRICACIÓN DE GAS Y PROCESAMIENTO DE GAS NATURAL |
| 352020 | DISTRIBUCIÓN DE COMBUSTIBLES GASEOSOS POR TUBERÍAS |
| 352128 | FABR PINTURAS BARNICES Y LACAS |
| 352217 | FABRIC PRODUCTOS FARMACEUTICOS |
| 352225 | FABRIC VACUNAS SUEROS |
| 352314 | FABRIC JABONES Y DETERGENTES |
| 352322 | FABRIC PREPARADOS P/ LIMPIEZA |
| 352330 | FABRIC PERFUMES PRODUC TOCADOR |
| 352918 | FABRIC TINTAS NEGRO HUMO |
| 352926 | FABRIC FOSFOROS |
| 352934 | FABRIC EXPLOSIVOS PIROTECNIA |
| 352942 | FABRI COLAS ADHESIVOS APRESTOS |
| 352950 | FABR PRODUC QUIMICOS NO CLASIF |
| 353000 | FABRICACION Y REPARACION DE AERONAVES |
| 353001 | SUMINISTRO DE VAPOR Y AIRE ACONDICIONADO |
| 353019 | REFINACION PETROLEO |
| 354015 | FABR PRODUC DERIV DEL PETROLEO |
| 355119 | FABRIC CAMARAS CUBIERTAS |
| 355127 | RECAUCHUTADO CUBIERTAS |
| 355135 | FABRIC PROD CAUCHO P/INDUS AUT |
| 355917 | FABRIC CALZADO DE CAUCHO |
| 355925 | FABR PRODUCTO CAUCHO NO CLASIF |
| 356018 | FABRIC ENVASES PLASTICOS |
| 356026 | FABR PRODUC PLASTICOS N/CLASIF |
| 359100 | FABRICACION DE MOTOCICLETAS |
| 359200 | FABRICACION DE BICICLETAS Y DE SILLONES DE RUEDAS PARA INVALIDOS |
| 359900 | FABRICACION DE EQUIPO DE TRANSPORTE N.C.P. |
| 360010 | CAPTACIÓN, DEPURACIÓN Y DISTRIBUCIÓN DE AGUA DE FUENTES SUBTERRÁNEAS |
| 360020 | CAPTACIÓN, DEPURACIÓN Y DISTRIBUCIÓN DE AGUA DE FUENTES SUPERFICIALES |
| 361010 | FABRICACION DE MUEBLES Y PARTES DE MUEBLES,PRINCIPALMENTE DE MADERA |
| 361011 | FABR OBJET CERAMIC USO DOMEST |
| 361020 | FABRICACION DE MUEBLES Y PARTES DE MUEBLES,PRINCIPALMENTE DE OTROS MATERIALES |
| 361030 | FABRICACION DE SOMIERES Y COLCHONES |
| 361038 | FABRIC OBJ CERAMIC P/USO INDUS |
| 361046 | FABRIC ARTEFACTOS SANITARIOS |
| 361054 | FABRIC OBJETO CERAMIC N/CLASIF |
| 362018 | FABR VIDRIO PLANOS Y TEMPLADOS |
| 362026 | FABRIC ARTIC VIDRIO NO ESPEJOS |
| 362034 | FABRIC ESPEJOS Y VITRALES |
| 369101 | FABRICACION DE JOYAS Y ART. CONEXOS |
| 369102 | FABRICACION DE OBJETOS DE PLATERIA Y ART. ENCHAPADOS |
| 369128 | FABRIC LADRILLOS COMUNES |
| 369136 | FABRIC LADRILLOS DE MAQUINA |
| 369144 | FABRIC CERAMIC P/PISOS Y PARED |
| 369152 | FABRIC MATERIAL REFRACTARIO |
| 369200 | FABRICACION DE INSTRUMENTOS DE MUSICA |
| 369217 | FABRIC CAL |
| 369225 | FABRIC CEMENTO |
| 369233 | FABRIC YESO |
| 369300 | FABRICACION DE ART. DE DEPORTE |
| 369400 | FABRICACION DE JUEGOS Y JUGUETES |
| 369910 | FABRICACION DE LAPICES,LAPICERAS, BOLIGRAFOS,SELLOS Y ART. SIMILARES PARA OFICINAS Y ARTISTAS |
| 369918 | FABRIC ARTIC CEMEN Y FIBROCEME |
| 369920 | FABRICACION DE CEPILLOS Y PINCELES |
| 369926 | FABRIC PREMOLDEADOS P/CONSTRUC |
| 369934 | FABRIC MOSAICOS NO CERAMICOS |
| 369942 | FABRIC PRODUC MARMOL Y GRANITO |
| 369950 | FABR PROD MINE NO MET N/CLASIF |
| 369991 | FABRICACION DE FOSFOROS |
| 369992 | FABRICACION DE PARAGUAS |
| 369999 | INDUSTRIAS MANUFACTURERAS N.C.P. |
| 370000 | SERVICIOS DE DEPURACIÓN DE AGUAS RESIDUALES, ALCANTARILLADO Y CLOACAS |
| 371000 | RECICLAMIENTO DE DESPERDICIOS Y DESECHOS METALICOS |
| 371017 | FUNDIC EN ALTOS HORNOS ACERIA |
| 371025 | LAMINAC Y ESTIRADO LAMINADORA |
| 371033 | FABR IND BASIC HIERRO Y ACERO |
| 372000 | RECICLAMIENTO DE DESPERDICIOS Y DESECHOS NO METALICOS |
| 372013 | FABR PROD PRIMAR MET N/FERROS |
| 381100 | RECOLECCIÓN, TRANSPORTE, TRATAMIENTO Y DISPOSICIÓN FINAL DE RESIDUOS NO PELIGROSOS |
| 381128 | FABRIC HERRAMIENTAS MANUALES |
| 381136 | FABB CUCHIL VAJILLA ACERO INOX |
| 381144 | FAB CUCHIL VAJILLA N/ACER INOX |
| 381152 | FABRIC CERRADURAS Y HERRAJES |
| 381200 | RECOLECCIÓN, TRANSPORTE, TRATAMIENTO Y DISPOSICIÓN FINAL DE RESIDUOS PELIGROSOS |
| 381217 | FABR MUEBLES ACCESOR METALICOS |
| 381314 | FABR PROD CARPINTERIA METALICA |
| 381322 | FABR ESTRUC METALICAS P/CONSTR |
| 381330 | FABR TANQUES DEPOSIT METALICOS |
| 381918 | FABRIC ENVASES DE HOJALATA |
| 381926 | FABR HORNOS ESTUF IND NO ELECT |
| 381934 | FABRIC TEJIDOS DE ALAMBRE |
| 381942 | FABRIC CAJAS DE SEGURIDAD |
| 381950 | FAB PROD METAL TORNER Y MATRIC |
| 381969 | GALVANOPLASTIA PROD METALICOS |
| 381977 | ESTAMPADO METALES |
| 381985 | FABR ARTEF P/ILUMINAC NO ELECT |
| 381993 | FABR PROD METALICOS NO CLASIF |
| 382010 | RECUPERACIÓN DE MATERIALES Y DESECHOS METÁLICOS |
| 382020 | RECUPERACIÓN DE MATERIALES Y DESECHOS NO METÁLICOS |
| 382116 | FABR REPAR MOTORES NO ELECTRIC |
| 382213 | FAB REPAR MAQU P/AGRIC Y GANAD |
| 382310 | FAB MAQU P/TRAB METAL Y MADERA |
| 382418 | FAB REPAR MAQU Y EQUIP P/CONST |
| 382426 | FAB MAQ EQU P/MINERIA Y PETROL |
| 382434 | FAB MAQ EQU P/ELAB Y ENV ALIME |
| 382442 | FABRIC MAQ EQU P/INDUST TEXTIL |
| 382450 | FAB REPA MAQ Y EQU P/IND PAPEL |
| 382493 | FABR REPAR MAQ EQUIPO N/CLASIF |
| 382515 | FABR REPAR MAQU OFICINA COMPUT |
| 382523 | FABRIC REPAR BASCULAS BALANZAS |
| 382914 | FABR REPAR MAQU COSER Y TEJER |
| 382922 | FABR COCINAS CALEFONES ESTUFAS |
| 382930 | FABRIC REPAR ASCENSORES |
| 382949 | FABR GRUAS EQU TRANSP MECANICO |
| 382957 | FABRIC ARMAS |
| 382965 | FABR REPAR MAQ EQUIPO N/CLASIF |
| 383112 | FABR REPAR MOTORES ELECTRICOS |
| 383120 | FAB REPAR EQUIPO DISTRIB ELECT |
| 383139 | FAB REPAR MAQ ELEC IN N/CLASIF |
| 383228 | FABRIC RECEPTORES RADIO TV |
| 383236 | FABR GRABACION DISCOS Y CINTAS |
| 383244 | FABRIC EQUIPOS COMUNICACION |
| 383252 | FAB PIEZAS P/APARATOS RADIO TV |
| 383317 | FABR HELAD FREEZERS LAVARROPAS |
| 383325 | FAB VENTILAD EXTRACT AIRE ACON |
| 383333 | FABR ENCERAD PULIDOR BATIDORAS |
| 383341 | FABR PLANCHA CALEF HORNO ELECT |
| 383368 | FABR APAR ELECT U DOM N/CLASIF |
| 383910 | FABRIC LAMPARAS Y TUBOS ELECTR |
| 383929 | FABR ARTEFACT ELECT P/ILUMINAC |
| 383937 | FABR BATERIAS PILAS ELECTRICAS |
| 383945 | FABRIC CONDUCTORES ELECTRICOS |
| 383953 | FABR BOBINAS ARRANQUES BUJIAS |
| 383961 | FABR APAR Y SUMIN ELEC N/CLASI |
| 384119 | CONSTR MOTORES Y PIEZ P/NAVIOS |
| 384127 | CONSTR REP EMBARC NO DE CAUCHO |
| 384216 | CONSTR MAQU Y EQUIP FERROVIARI |
| 384313 | CONSTR MOTORES P/AUTO CAMIONES |
| 384321 | FABR ARMAD CARROCERIAS P/AUTOM |
| 384348 | FABRIC ARMADO AUTOMOTORES |
| 384356 | FABRIC REMOLQUES SEMIREMOLQUES |
| 384364 | FABR PIEZAS REP P/AUTOMOTORES |
| 384372 | RECTIFICACION DE MOTORES |
| 384410 | FABR MOTO BICICLETAS REPUESTOS |
| 384518 | FABR AERONAVES REPUESTO Y ACC |
| 384917 | FABR MATERIAL TRANSP N/ CLASIF |
| 385115 | FABR REPAR INSTRUMENT CIRUGIA |
| 385123 | FABR REPA EQU CIENTIF N/CLASIF |
| 385212 | FABR APARAT ACCES P/FOTOGRAFIA |
| 385220 | FABRIC INSTRUMENTOS DE OPTICA |
| 385239 | FABR LENTES ARTICUL OFTALMICOS |
| 385328 | FABRIC ARMADO RELOJES Y PIEZAS |
| 390000 | DESCONTAMINACIÓN Y OTROS SERVICIOS DE GESTIÓN DE RESIDUOS |
| 390119 | FABRIC JOYAS |
| 390127 | FABR OBJ PLATER ART ENCHAPADOS |
| 390216 | FABRIC INSTRUMENTOS DE MUSICA |
| 390313 | FABRIC ARTIC DEPOR Y ATLETISMO |
| 390917 | FABR JUEGOS JUGUETES N/PLASTIC |
| 390925 | FABR LAPIZ LAPIC BOLIG Y SIMIL |
| 390933 | FABR CEPILLOS PINCELES ESCOBAS |
| 390941 | FABRIC PARAGUAS |
| 390968 | FABR ARMADO LETREROS ANUNCIOS |
| 390976 | FABRIC ARTICULOS NO CLASIF |
| 401110 | GENERACION DE ENERGIA TERMICA CONVENCIONAL |
| 401120 | GENERACION DE ENERGIA TERMICA NUCLEAR |
| 401130 | GENERACION DE ENERGIA HIDRAULICA |
| 401190 | GENERACION DE ENERGIA N.C.P. |
| 401200 | TRANSPORTE DE ENERGIA ELECTRICA |
| 401300 | DISTRIBUCION DE ENERGIA ELECTRICA |
| 402001 | FABRICACION Y DISTRIBUCION DE GAS |
| 402009 | FABRICACION Y DISTRIBUCION DE COMBUSTIBLES GASEOSOS N.C.P. |
| 403000 | SUMINISTRO DE VAPOR Y AGUA CALIENTE |
| 410010 | CAPTACION,DEPURACION Y DISTRIBUCION DE AGUA DE FUENTES SUBTERRANEAS |
| 410011 | CONSTRUCCIÓN, REFORMA Y REPARACIÓN DE EDIFICIOS RESIDENCIALES |
| 410020 | CAPTACION,DEPURACION Y DISTRIBUCION DE AGUA DE FUENTES SUPERFICIALES |
| 410021 | CONSTRUCCIÓN, REFORMA Y REPARACIÓN DE EDIFICIOS NO RESIDENCIALES |
| 410128 | GENERACION ELECTRICIDAD |
| 410136 | TRANSMISION ELECTRICIDAD |
| 410144 | DISTRIBUCION ELECTRICIDAD |
| 410217 | PRODUCCION GAS NATURAL |
| 410225 | DISTRIBUCION GAS NATURAL |
| 410233 | PRODUCCION GASES NO CLASIF |
| 410241 | DISTRIBUCION GASES NO CLASIF |
| 410314 | PRODUCCION VAPOR AGUA CALIENTE |
| 410322 | DISTRIBUC VAPOR AGUA CALIENTE |
| 420018 | CAPTACION PURIF DISTR DE AGUA |
| 421000 | CONSTRUCCIÓN, REFORMA Y REPARACIÓN DE OBRAS DE INFRAESTRUCTURA PARA EL TRANSPORTE |
| 422100 | PERFORACIÓN DE POZOS DE AGUA |
| 422200 | CONSTRUCCIÓN, REFORMA Y REPARACIÓN DE REDES DISTRIBUCIÓN DE ELECTRICIDAD, GAS, AGUA, TELECOMUNICACIONES Y DE OTROS SERVICIOS PÚBLICOS |
| 429010 | CONSTRUCCIÓN, REFORMA Y REPARACIÓN DE OBRAS HIDRÁULICAS |
| 429090 | CONSTRUCCIÓN DE OBRAS DE INGENIERÍA CIVIL N.C.P. |
| 431100 | DEMOLICIÓN Y VOLADURA DE EDIFICIOS Y DE SUS PARTES |
| 431210 | MOVIMIENTO DE SUELOS Y PREPARACIÓN DE TERRENOS PARA OBRAS |
| 431220 | PERFORACIÓN Y SONDEO, EXCEPTO PERFORACIÓN DE POZOS DE PETRÓLEO, DE GAS, DE MINAS E HIDRÁULICOS  Y PROSPECCIÓN DE YACIMIENTOS DE PETRÓLEO |
| 432110 | INSTALACIÓN DE SISTEMAS DE ILUMINACIÓN, CONTROL Y SEÑALIZACIÓN ELÉCTRICA PARA EL TRANSPORTE |
| 432190 | INSTALACIÓN, EJECUCIÓN Y MANTENIMIENTO DE INSTALACIONES ELÉCTRICAS, ELECTROMECÁNICAS Y ELECTRÓNICAS N.C.P. |
| 432200 | INSTALACIONES DE GAS, AGUA, SANITARIOS Y DE CLIMATIZACIÓN, CON SUS ARTEFACTOS CONEXOS |
| 432910 | INSTALACIONES DE ASCENSORES, MONTACARGAS Y  ESCALERAS MECÁNICAS |
| 432920 | AISLAMIENTO TÉRMICO, ACÚSTICO, HÍDRICO Y ANTIVIBRATORIO |
| 432990 | INSTALACIONES PARA EDIFICIOS Y OBRAS DE INGENIERÍA CIVIL N.C.P. |
| 433010 | INSTALACIONES DE CARPINTERÍA, HERRERÍA DE OBRA Y ARTÍSTICA |
| 433020 | TERMINACIÓN Y REVESTIMIENTO DE PAREDES Y PISOS |
| 433030 | COLOCACIÓN DE CRISTALES EN OBRA |
| 433040 | PINTURA Y TRABAJOS DE DECORACIÓN |
| 433090 | TERMINACIÓN DE EDIFICIOS N.C.P. |
| 439100 | ALQUILER DE EQUIPO DE CONSTRUCCIÓN O DEMOLICIÓN DOTADO DE OPERARIOS |
| 439910 | HINCADO DE PILOTES, CIMENTACIÓN Y OTROS TRABAJOS DE HORMIGÓN ARMADO |
| 439990 | ACTIVIDADES ESPECIALIZADAS DE CONSTRUCCIÓN N.C.P. |
| 451100 | DEMOLICION Y VOLADURA DE EDIFICIOS Y DE SUS PARTES |
| 451110 | VENTA DE AUTOS, CAMIONETAS Y UTILITARIOS NUEVOS |
| 451190 | VENTA DE VEHÍCULOS AUTOMOTORES NUEVOS N.C.P. |
| 451200 | PERFORACION Y SONDEO EXCEPTO: PERFORACION DE POZOS DE PETROLEO,DE GAS,DE MINAS E HIDRAULICOS Y PROSPECCION DE YACIMIENTOS DE PETROLEO |
| 451210 | VENTA DE AUTOS, CAMIONETAS Y UTILITARIOS, USADOS |
| 451290 | VENTA DE VEHÍCULOS AUTOMOTORES USADOS N.C.P. |
| 451900 | MOVIMIENTO DE SUELOS Y PREPARACION DE TERRENOS PARA OBRAS N.C.P. |
| 452100 | CONSTRUCCION,REFORMA Y REPARACION DE EDIFICIOS RESIDENCIALES |
| 452101 | LAVADO AUTOMÁTICO Y MANUAL DE VEHÍCULOS AUTOMOTORES |
| 452200 | CONSTRUCCION,REFORMA Y REPARACION DE EDIFICIOS NO RESIDENCIALES |
| 452210 | REPARACIÓN DE CÁMARAS Y CUBIERTAS |
| 452220 | REPARACIÓN DE AMORTIGUADORES,  ALINEACIÓN DE DIRECCIÓN Y BALANCEO DE RUEDAS |
| 452300 | INSTALACIÓN Y REPARACIÓN DE PARABRISAS, LUNETAS Y VENTANILLAS, CERRADURAS NO ELÉCTRICAS Y GRABADO DE CRISTALES |
| 452310 | CONSTRUCCION,REFORMA Y REPARACION DE OBRAS HIDRAULICAS |
| 452390 | CONSTRUCCION,REFORMA Y REPARACION DE OBRAS DE INFRAESTRUCTURA DEL TRANSPORTE N.C.P |
| 452400 | CONSTRUCCION,REFORMA Y REPARACION DE REDES |
| 452401 | REPARACIONES ELÉCTRICAS DEL TABLERO E INSTRUMENTAL, REPARACIÓN Y RECARGA DE BATERÍAS, INSTALACIÓN DE ALARMAS, RADIOS, SISTEMAS DE CLIMATIZACIÓN |
| 452500 | TAPIZADO Y RETAPIZADO DE AUTOMOTORES |
| 452510 | PERFORACION DE POZOS DE AGUA |
| 452520 | ACTIVIDADES DE HINCADO DE PILOTES,CIMENTACION Y OTROS TRABAJOS DE HORMIGON ARMADO |
| 452590 | ACTIVIDADES ESPECIALIZADAS DE CONSTRUCCION N.C.P. |
| 452600 | REPARACIÓN Y PINTURA DE CARROCERÍAS, COLOCACIÓN Y REPARACIÓN DE GUARDABARROS Y PROTECCIONES EXTERIORES |
| 452700 | INSTALACIÓN Y REPARACIÓN DE CAÑOS DE ESCAPE Y RADIADORES |
| 452800 | MANTENIMIENTO Y REPARACIÓN DE FRENOS Y EMBRAGUES |
| 452900 | OBRAS DE INGENIERIA CIVIL N.C.P. |
| 452910 | INSTALACIÓN Y REPARACIÓN DE EQUIPOS DE GNC |
| 452990 | MANTENIMIENTO Y REPARACIÓN DEL MOTOR N.C.P., MECÁNICA INTEGRAL |
| 453100 | VENTA AL POR MAYOR DE PARTES, PIEZAS Y ACCESORIOS DE VEHÍCULOS AUTOMOTORES |
| 453110 | INSTALACIONES DE ASCENSORES,MONTACARGAS Y ESCALERAS MECANICAS |
| 453120 | INSTALACION DE SISTEMAS DE ILUMINACION,CONTROL Y SEÑALIZACION ELECTRICA PARA EL TRANSPORTE |
| 453190 | EJECUCION Y MANTENIMIENTO DE INSTALACIONES ELECTRICAS Y ELECTRONICAS N.C.P. |
| 453200 | AISLAMIENTO TERMICO,ACUSTICO,HIDRICO Y ANTIVIBRATORIO |
| 453210 | VENTA AL POR MENOR DE CÁMARAS Y CUBIERTAS |
| 453220 | VENTA AL POR MENOR DE BATERÍAS |
| 453291 | VENTA AL POR MENOR DE PARTES, PIEZAS Y ACCESORIOS NUEVOS N.C.P. |
| 453292 | VENTA AL POR MENOR DE PARTES, PIEZAS Y ACCESORIOS USADOS N.C.P. |
| 453300 | INSTALACIONES DE GAS,AGUA,SANITARIOS Y DE CLIMATIZACION,CON SUS ARTEFACTOS CONEXOS |
| 453900 | INSTALACIONES PARA EDIFICIOS Y OBRAS DE INGENIERIA CIVIL N.C.P. |
| 454010 | VENTA DE MOTOCICLETAS Y DE SUS PARTES, PIEZAS Y ACCESORIOS |
| 454020 | MANTENIMIENTO Y REPARACIÓN DE MOTOCICLETAS |
| 454100 | INSTALACIONES DE CARPINTERIA,HERRERIA DE OBRA Y ARTISTICA |
| 454200 | TERMINACION Y REVESTIMIENTO DE PAREDES Y PISOS |
| 454300 | COLOCACION DE CRISTALES EN OBRA |
| 454400 | PINTURA Y TRABAJOS DE DECORACION |
| 454900 | TERMINACION DE EDIFICIOS Y OBRAS DE INGENIERIA CIVIL N.C.P. |
| 455000 | ALQUILER DE EQUIPO DE CONSTRUCCION O DEMOLICION DOTADO DE OPERARIOS |
| 461011 | VENTA AL POR MAYOR EN COMISIÓN O CONSIGNACIÓN DE CEREALES (INCLUYE ARROZ), OLEAGINOSAS Y FORRAJERAS EXCEPTO SEMILLAS |
| 461012 | VENTA AL POR MAYOR EN COMISIÓN O CONSIGNACIÓN DE SEMILLAS |
| 461013 | VENTA AL POR MAYOR EN COMISIÓN O CONSIGNACIÓN DE FRUTAS |
| 461014 | ACOPIO Y ACONDICIONAMIENTO EN COMISIÓN O CONSIGNACIÓN DE CEREALES (INCLUYE ARROZ), OLEAGINOSAS Y FORRAJERAS EXCEPTO SEMILLAS |
| 461019 | VENTA AL POR MAYOR EN COMISIÓN O CONSIGNACIÓN DE PRODUCTOS AGRÍCOLAS N.C.P. |
| 461021 | VENTA AL POR MAYOR EN COMISIÓN O CONSIGNACIÓN DE GANADO BOVINO EN PIE |
| 461022 | VENTA AL POR MAYOR EN COMISIÓN O CONSIGNACIÓN DE GANADO EN PIE EXCEPTO BOVINO |
| 461029 | VENTA AL POR MAYOR EN COMISIÓN O CONSIGNACIÓN DE PRODUCTOS PECUARIOS N.C.P. |
| 461031 | OPERACIONES DE INTERMEDIACIÓN DE CARNE - CONSIGNATARIO DIRECTO - |
| 461032 | OPERACIONES DE INTERMEDIACIÓN DE CARNE EXCEPTO CONSIGNATARIO DIRECTO |
| 461039 | VENTA AL POR MAYOR EN COMISIÓN O CONSIGNACIÓN DE ALIMENTOS, BEBIDAS Y TABACO N.C.P. |
| 461040 | VENTA AL POR MAYOR EN COMISIÓN O CONSIGNACIÓN DE COMBUSTIBLES |
| 461091 | VENTA AL POR MAYOR EN COMISIÓN O CONSIGNACIÓN DE PRODUCTOS TEXTILES, PRENDAS DE VESTIR, CALZADO EXCEPTO EL ORTOPÉDICO,  ARTÍCULOS DE MARROQUINERÍA, PARAGUAS Y SIMILARES Y PRODUCTOS |
| 461092 | VENTA AL POR MAYOR EN COMISIÓN O CONSIGNACIÓN DE  MADERA Y MATERIALES PARA LA CONSTRUCCIÓN |
| 461093 | VENTA AL POR MAYOR EN COMISIÓN O CONSIGNACIÓN DE MINERALES, METALES Y PRODUCTOS QUÍMICOS INDUSTRIALES |
| 461094 | VENTA AL POR MAYOR EN COMISIÓN O CONSIGNACIÓN DE  MAQUINARIA, EQUIPO PROFESIONAL INDUSTRIAL Y COMERCIAL, EMBARCACIONES Y AERONAVES |
| 461095 | VENTA AL POR MAYOR EN COMISIÓN O CONSIGNACIÓN DE PAPEL, CARTÓN, LIBROS, REVISTAS, DIARIOS, MATERIALES DE EMBALAJE Y ARTÍCULOS DE LIBRERÍA |
| 461099 | VENTA AL POR MAYOR EN COMISIÓN O CONSIGNACIÓN DE  MERCADERÍAS N.C.P. |
| 462110 | ACOPIO DE ALGODÓN |
| 462120 | VENTA AL POR MAYOR DE SEMILLAS Y GRANOS PARA FORRAJES |
| 462131 | VENTA AL POR MAYOR DE CEREALES (INCLUYE ARROZ), OLEAGINOSAS Y FORRAJERAS EXCEPTO SEMILLAS |
| 462132 | ACOPIO Y ACONDICIONAMIENTO DE CEREALES Y SEMILLAS, EXCEPTO DE ALGODÓN Y SEMILLAS Y GRANOS PARA FORRAJES |
| 462190 | VENTA AL POR MAYOR DE MATERIAS PRIMAS AGRÍCOLAS Y DE LA SILVICULTURA N.C.P. |
| 462201 | VENTA AL POR MAYOR DE LANAS, CUEROS EN BRUTO Y PRODUCTOS AFINES |
| 462209 | VENTA AL POR MAYOR DE MATERIAS PRIMAS PECUARIAS N.C.P. INCLUSO ANIMALES VIVOS |
| 463111 | VENTA AL POR MAYOR DE PRODUCTOS LÁCTEOS |
| 463112 | VENTA AL POR MAYOR DE FIAMBRES Y QUESOS |
| 463121 | VENTA AL POR MAYOR DE CARNES ROJAS Y DERIVADOS |
| 463129 | VENTA AL POR MAYOR DE AVES, HUEVOS Y PRODUCTOS DE GRANJA Y DE LA CAZA N.C.P. |
| 463130 | VENTA AL POR MAYOR DE PESCADO |
| 463140 | VENTA AL POR MAYOR Y EMPAQUE DE FRUTAS, DE LEGUMBRES Y HORTALIZAS FRESCAS |
| 463151 | VENTA AL POR MAYOR DE PAN, PRODUCTOS DE CONFITERÍA Y PASTAS FRESCAS |
| 463152 | VENTA AL POR MAYOR DE AZÚCAR |
| 463153 | VENTA AL POR MAYOR DE ACEITES Y GRASAS |
| 463154 | VENTA AL POR MAYOR DE CAFÉ, TÉ, YERBA MATE Y OTRAS INFUSIONES Y ESPECIAS Y CONDIMENTOS |
| 463159 | VENTA AL POR MAYOR DE PRODUCTOS Y SUBPRODUCTOS DE MOLINERÍA N.C.P. |
| 463160 | VENTA AL POR MAYOR DE CHOCOLATES, GOLOSINAS Y PRODUCTOS PARA KIOSCOS Y POLIRRUBROS N.C.P., EXCEPTO CIGARRILLOS |
| 463170 | VENTA AL POR MAYOR DE ALIMENTOS BALANCEADOS PARA ANIMALES |
| 463180 | VENTA AL POR MAYOR EN SUPERMERCADOS MAYORISTAS DE ALIMENTOS |
| 463191 | VENTA AL POR MAYOR DE FRUTAS, LEGUMBRES Y CEREALES SECOS Y EN CONSERVA |
| 463199 | VENTA AL POR MAYOR DE PRODUCTOS ALIMENTICIOS N.C.P. |
| 463211 | VENTA AL POR MAYOR DE VINO |
| 463212 | VENTA AL POR MAYOR DE BEBIDAS ESPIRITOSAS |
| 463219 | VENTA AL POR MAYOR DE BEBIDAS ALCOHÓLICAS N.C.P. |
| 463220 | VENTA AL POR MAYOR DE BEBIDAS NO ALCOHÓLICAS |
| 463300 | VENTA AL POR MAYOR DE CIGARRILLOS Y PRODUCTOS DE TABACO |
| 464111 | VENTA AL POR MAYOR DE TEJIDOS (TELAS) |
| 464112 | VENTA AL POR MAYOR DE ARTÍCULOS DE MERCERÍA |
| 464113 | VENTA AL POR MAYOR DE MANTELERÍA, ROPA DE CAMA Y ARTÍCULOS TEXTILES PARA EL HOGAR |
| 464114 | VENTA AL POR MAYOR DE TAPICES Y ALFOMBRAS DE MATERIALES TEXTILES |
| 464119 | VENTA AL POR MAYOR DE PRODUCTOS TEXTILES N.C.P. |
| 464121 | VENTA AL POR MAYOR DE PRENDAS DE VESTIR DE CUERO |
| 464122 | VENTA AL POR MAYOR DE MEDIAS Y PRENDAS DE PUNTO |
| 464129 | VENTA AL POR MAYOR DE PRENDAS Y ACCESORIOS DE VESTIR N.C.P., EXCEPTO UNIFORMES Y ROPA DE TRABAJO |
| 464130 | VENTA AL POR MAYOR DE CALZADO EXCEPTO EL ORTOPÉDICO |
| 464141 | VENTA AL POR MAYOR DE PIELES Y CUEROS CURTIDOS Y SALADOS |
| 464142 | VENTA AL POR MAYOR DE SUELAS Y AFINES |
| 464149 | VENTA AL POR MAYOR DE ARTÍCULOS DE MARROQUINERÍA,  PARAGUAS Y PRODUCTOS SIMILARES N.C.P. |
| 464150 | VENTA AL POR MAYOR DE UNIFORMES Y ROPA DE TRABAJO |
| 464211 | VENTA AL POR MAYOR DE LIBROS Y PUBLICACIONES |
| 464212 | VENTA AL POR MAYOR DE DIARIOS Y REVISTAS |
| 464221 | VENTA AL POR MAYOR DE PAPEL Y PRODUCTOS DE PAPEL Y CARTÓN EXCEPTO ENVASES |
| 464222 | VENTA AL POR MAYOR DE ENVASES DE PAPEL Y CARTÓN |
| 464223 | VENTA AL POR MAYOR DE ARTÍCULOS DE LIBRERÍA Y PAPELERÍA |
| 464310 | VENTA AL POR MAYOR DE PRODUCTOS FARMACÉUTICOS |
| 464320 | VENTA AL POR MAYOR DE PRODUCTOS COSMÉTICOS, DE TOCADOR Y DE PERFUMERÍA |
| 464330 | VENTA AL POR MAYOR DE INSTRUMENTAL MÉDICO Y ODONTOLÓGICO Y ARTÍCULOS ORTOPÉDICOS |
| 464340 | VENTA AL POR MAYOR DE PRODUCTOS VETERINARIOS |
| 464410 | VENTA AL POR MAYOR DE ARTÍCULOS DE ÓPTICA Y DE FOTOGRAFÍA |
| 464420 | VENTA AL POR MAYOR DE ARTÍCULOS DE RELOJERÍA, JOYERÍA Y FANTASÍAS |
| 464501 | VENTA AL POR MAYOR DE ELECTRODOMÉSTICOS Y ARTEFACTOS PARA EL HOGAR EXCEPTO EQUIPOS DE AUDIO Y VIDEO |
| 464502 | VENTA AL POR MAYOR DE EQUIPOS DE AUDIO, VIDEO Y TELEVISIÓN |
| 464610 | VENTA AL POR MAYOR DE MUEBLES EXCEPTO DE OFICINA, ARTÍCULOS DE MIMBRE Y CORCHO, COLCHONES Y SOMIERES |
| 464620 | VENTA AL POR MAYOR DE ARTÍCULOS DE ILUMINACIÓN |
| 464631 | VENTA AL POR MAYOR DE ARTÍCULOS DE VIDRIO |
| 464632 | VENTA AL POR MAYOR DE ARTÍCULOS DE BAZAR Y MENAJE EXCEPTO DE VIDRIO |
| 464910 | VENTA AL POR MAYOR DE CD'S Y DVD'S DE AUDIO Y VIDEO GRABADOS. |
| 464920 | VENTA AL POR MAYOR DE MATERIALES Y PRODUCTOS DE LIMPIEZA |
| 464930 | VENTA AL POR MAYOR DE JUGUETES |
| 464940 | VENTA AL POR MAYOR DE BICICLETAS Y RODADOS SIMILARES |
| 464950 | VENTA AL POR MAYOR DE ARTÍCULOS DE ESPARCIMIENTO Y DEPORTES |
| 464991 | VENTA AL POR MAYOR DE FLORES Y PLANTAS NATURALES Y ARTIFICIALES |
| 464999 | VENTA AL POR MAYOR DE ARTÍCULOS DE USO DOMÉSTICO O PERSONAL N.C.P |
| 465100 | VENTA AL POR MAYOR DE EQUIPOS, PERIFÉRICOS, ACCESORIOS Y PROGRAMAS INFORMÁTICOS |
| 465210 | VENTA AL POR MAYOR DE EQUIPOS DE TELEFONÍA Y COMUNICACIONES |
| 465220 | VENTA AL POR MAYOR DE COMPONENTES ELECTRÓNICOS |
| 465310 | VENTA AL POR MAYOR DE MÁQUINAS, EQUIPOS E IMPLEMENTOS DE USO EN LOS SECTORES AGROPECUARIO, JARDINERÍA, SILVICULTURA, PESCA Y CAZA |
| 465320 | VENTA AL POR MAYOR DE MÁQUINAS, EQUIPOS E IMPLEMENTOS DE USO EN LA ELABORACIÓN DE ALIMENTOS, BEBIDAS Y TABACO |
| 465330 | VENTA AL POR MAYOR DE MÁQUINAS, EQUIPOS E IMPLEMENTOS DE USO EN LA FABRICACIÓN DE TEXTILES, PRENDAS Y ACCESORIOS DE VESTIR, CALZADO, ARTÍCULOS DE CUERO Y MARROQUINERÍA |
| 465340 | VENTA AL POR MAYOR DE MÁQUINAS, EQUIPOS E IMPLEMENTOS DE USO EN IMPRENTAS, ARTES GRÁFICAS Y ACTIVIDADES CONEXAS |
| 465350 | VENTA AL POR MAYOR DE MÁQUINAS, EQUIPOS E IMPLEMENTOS DE USO MÉDICO Y PARAMÉDICO |
| 465360 | VENTA AL POR MAYOR DE MÁQUINAS, EQUIPOS E IMPLEMENTOS DE USO EN LA INDUSTRIA DEL PLÁSTICO Y DEL CAUCHO |
| 465390 | VENTA AL POR MAYOR DE MÁQUINAS, EQUIPOS E IMPLEMENTOS DE USO ESPECIAL N.C.P. |
| 465400 | VENTA AL POR MAYOR DE MÁQUINAS - HERRAMIENTA DE USO GENERAL |
| 465500 | VENTA  AL  POR  MAYOR  DE  VEHÍCULOS,  EQUIPOS  Y  MÁQUINAS  PARA  EL TRANSPORTE FERROVIARIO, AÉREO Y DE NAVEGACIÓN |
| 465610 | VENTA AL POR MAYOR DE MUEBLES E INSTALACIONES PARA OFICINAS |
| 465690 | VENTA AL POR MAYOR DE MUEBLES E INSTALACIONES PARA LA INDUSTRIA, EL COMERCIO Y LOS SERVICIOS N.C.P. |
| 465910 | VENTA AL POR MAYOR DE MÁQUINAS Y EQUIPO DE CONTROL Y SEGURIDAD |
| 465920 | VENTA AL POR MAYOR DE MAQUINARIA Y EQUIPO DE OFICINA, EXCEPTO EQUIPO INFORMÁTICO |
| 465930 | VENTA AL POR MAYOR DE EQUIPO PROFESIONAL Y CIENTÍFICO E INSTRUMENTOS DE MEDIDA Y DE CONTROL N.C.P. |
| 465990 | VENTA AL POR MAYOR DE MÁQUINAS, EQUIPO Y MATERIALES CONEXOS N.C.P. |
| 466110 | VENTA AL POR MAYOR DE COMBUSTIBLES Y LUBRICANTES PARA AUTOMOTORES |
| 466121 | FRACCIONAMIENTO Y DISTRIBUCIÓN DE GAS LICUADO |
| 466129 | VENTA AL POR MAYOR DE COMBUSTIBLES, LUBRICANTES, LEÑA Y CARBÓN, EXCEPTO GAS LICUADO Y COMBUSTIBLES Y LUBRICANTES PARA AUTOMOTORES |
| 466200 | VENTA AL POR MAYOR DE METALES Y MINERALES METALÍFEROS |
| 466310 | VENTA AL POR MAYOR DE ABERTURAS |
| 466320 | VENTA AL POR MAYOR DE PRODUCTOS DE MADERA EXCEPTO MUEBLES |
| 466330 | VENTA AL POR MAYOR DE ARTÍCULOS DE FERRETERÍA Y MATERIALES ELÉCTRICOS |
| 466340 | VENTA AL POR MAYOR DE PINTURAS Y PRODUCTOS CONEXOS |
| 466350 | VENTA AL POR MAYOR DE CRISTALES Y ESPEJOS |
| 466360 | VENTA AL POR MAYOR DE ARTÍCULOS PARA PLOMERÍA, INSTALACIÓN DE GAS Y CALEFACCIÓN |
| 466370 | VENTA AL POR MAYOR DE PAPELES PARA PARED, REVESTIMIENTO PARA PISOS DE GOMA, PLÁSTICO Y TEXTILES,  Y ARTÍCULOS SIMILARES PARA LA DECORACIÓN |
| 466391 | VENTA AL POR MAYOR DE ARTÍCULOS DE LOZA, CERÁMICA Y PORCELANA DE USO EN CONSTRUCCIÓN |
| 466399 | VENTA AL POR MAYOR DE ARTÍCULOS PARA LA CONSTRUCCIÓN N.C.P. |
| 466910 | VENTA AL POR MAYOR DE PRODUCTOS INTERMEDIOS N.C.P., DESPERDICIOS Y DESECHOS TEXTILES |
| 466920 | VENTA AL POR MAYOR DE PRODUCTOS INTERMEDIOS N.C.P., DESPERDICIOS Y DESECHOS DE PAPEL Y CARTÓN |
| 466931 | VENTA AL POR MAYOR DE ARTÍCULOS DE PLÁSTICO |
| 466932 | VENTA AL POR MAYOR DE ABONOS, FERTILIZANTES Y PLAGUICIDAS |
| 466939 | VENTA AL POR MAYOR DE PRODUCTOS INTERMEDIOS, DESPERDICIOS Y DESECHOS DE VIDRIO, CAUCHO, GOMA Y QUÍMICOS N.C.P. |
| 466940 | VENTA AL POR MAYOR DE PRODUCTOS INTERMEDIOS N.C.P., DESPERDICIOS Y DESECHOS METÁLICOS |
| 466990 | VENTA AL POR MAYOR DE PRODUCTOS INTERMEDIOS, DESPERDICIOS Y DESECHOS N.C.P. |
| 469010 | VENTA AL POR MAYOR DE INSUMOS AGROPECUARIOS DIVERSOS |
| 469090 | VENTA AL POR MAYOR DE MERCANCÍAS N.C.P. |
| 471110 | VENTA AL POR MENOR EN HIPERMERCADOS |
| 471120 | VENTA AL POR MENOR EN SUPERMERCADOS |
| 471130 | VENTA AL POR MENOR EN MINIMERCADOS |
| 471190 | VENTA AL POR MENOR EN KIOSCOS, POLIRRUBROS Y COMERCIOS NO ESPECIALIZADOS N.C.P. |
| 471900 | VENTA AL POR MENOR EN COMERCIOS NO ESPECIALIZADOS, SIN PREDOMINIO DE PRODUCTOS ALIMENTICIOS Y BEBIDAS |
| 472111 | VENTA AL POR MENOR DE PRODUCTOS LÁCTEOS |
| 472112 | VENTA AL POR MENOR DE FIAMBRES Y EMBUTIDOS |
| 472120 | VENTA AL POR MENOR DE PRODUCTOS DE ALMACÉN Y DIETÉTICA |
| 472130 | VENTA AL POR MENOR DE CARNES ROJAS, MENUDENCIAS Y CHACINADOS FRESCOS |
| 472140 | VENTA AL POR MENOR DE HUEVOS, CARNE DE AVES Y  PRODUCTOS DE GRANJA Y DE LA CAZA |
| 472150 | VENTA AL POR MENOR DE PESCADOS Y  PRODUCTOS DE LA PESCA |
| 472160 | VENTA AL POR MENOR DE FRUTAS, LEGUMBRES Y HORTALIZAS FRESCAS |
| 472171 | VENTA AL POR MENOR DE PAN Y PRODUCTOS DE PANADERÍA |
| 472172 | VENTA AL POR MENOR DE BOMBONES, GOLOSINAS Y DEMÁS PRODUCTOS DE CONFITERÍA |
| 472190 | VENTA AL POR MENOR DE PRODUCTOS ALIMENTICIOS N.C.P., EN COMERCIOS ESPECIALIZADOS |
| 472200 | VENTA AL POR MENOR DE BEBIDAS EN COMERCIOS ESPECIALIZADOS |
| 472300 | VENTA AL POR MENOR DE TABACO EN COMERCIOS ESPECIALIZADOS |
| 473000 | VENTA AL POR MENOR DE COMBUSTIBLE PARA VEHÍCULOS AUTOMOTORES Y MOTOCICLETAS |
| 474010 | VENTA AL POR MENOR DE EQUIPOS, PERIFÉRICOS,  ACCESORIOS Y PROGRAMAS INFORMÁTICOS |
| 474020 | VENTA AL POR MENOR DE APARATOS DE TELEFONÍA Y COMUNICACIÓN |
| 475110 | VENTA AL POR MENOR DE HILADOS, TEJIDOS Y ARTÍCULOS DE MERCERÍA |
| 475120 | VENTA AL POR MENOR DE CONFECCIONES PARA EL HOGAR |
| 475190 | VENTA AL POR MENOR DE ARTÍCULOS TEXTILES N.C.P. EXCEPTO PRENDAS DE VESTIR |
| 475210 | VENTA AL POR MENOR DE ABERTURAS |
| 475220 | VENTA AL POR MENOR DE MADERAS Y ARTÍCULOS DE MADERA  Y CORCHO, EXCEPTO MUEBLES |
| 475230 | VENTA AL POR MENOR DE ARTÍCULOS DE FERRETERÍA Y MATERIALES ELÉCTRICOS |
| 475240 | VENTA AL POR MENOR DE PINTURAS Y PRODUCTOS CONEXOS |
| 475250 | VENTA AL POR MENOR DE ARTÍCULOS PARA PLOMERÍA E INSTALACIÓN DE GAS |
| 475260 | VENTA AL POR MENOR DE CRISTALES, ESPEJOS, MAMPARAS Y CERRAMIENTOS |
| 475270 | VENTA AL POR MENOR DE PAPELES PARA PARED, REVESTIMIENTOS PARA PISOS Y ARTÍCULOS SIMILARES PARA LA DECORACIÓN |
| 475290 | VENTA AL POR MENOR DE MATERIALES DE CONSTRUCCIÓN N.C.P. |
| 475300 | VENTA AL POR MENOR  DE ELECTRODOMÉSTICOS, ARTEFACTOS PARA EL HOGAR Y EQUIPOS DE AUDIO Y VIDEO |
| 475410 | VENTA AL POR MENOR DE MUEBLES PARA EL HOGAR, ARTÍCULOS DE MIMBRE Y CORCHO |
| 475420 | VENTA AL POR MENOR DE COLCHONES Y SOMIERES |
| 475430 | VENTA AL POR MENOR DE ARTÍCULOS DE ILUMINACIÓN |
| 475440 | VENTA AL POR MENOR DE ARTÍCULOS DE BAZAR Y MENAJE |
| 475490 | VENTA AL POR MENOR DE ARTÍCULOS PARA EL HOGAR N.C.P. |
| 476110 | VENTA AL POR MENOR DE LIBROS |
| 476120 | VENTA AL POR MENOR DE DIARIOS Y REVISTAS |
| 476130 | VENTA AL POR MENOR DE PAPEL, CARTÓN, MATERIALES DE EMBALAJE Y ARTÍCULOS DE LIBRERÍA |
| 476200 | VENTA AL POR MENOR DE CD´S Y DVD´S DE AUDIO Y VIDEO GRABADOS |
| 476310 | VENTA AL POR MENOR DE EQUIPOS  Y ARTÍCULOS DEPORTIVOS |
| 476320 | VENTA AL POR MENOR DE ARMAS, ARTÍCULOS PARA LA CAZA Y PESCA |
| 476400 | VENTA AL POR MENOR DE JUGUETES, ARTÍCULOS DE COTILLÓN Y JUEGOS DE MESA |
| 477110 | VENTA AL POR MENOR DE ROPA INTERIOR, MEDIAS, PRENDAS PARA DORMIR Y PARA LA PLAYA |
| 477120 | VENTA AL POR MENOR DE UNIFORMES ESCOLARES Y GUARDAPOLVOS |
| 477130 | VENTA AL POR MENOR DE INDUMENTARIA PARA BEBÉS Y NIÑOS |
| 477140 | VENTA AL POR MENOR DE INDUMENTARIA DEPORTIVA |
| 477150 | VENTA AL POR MENOR DE PRENDAS DE CUERO |
| 477190 | VENTA AL POR MENOR DE PRENDAS Y ACCESORIOS DE VESTIR N.C.P. |
| 477210 | VENTA AL POR MENOR DE ARTÍCULOS DE TALABARTERÍA Y ARTÍCULOS REGIONALES |
| 477220 | VENTA AL POR MENOR DE CALZADO, EXCEPTO EL ORTOPÉDICO Y EL DEPORTIVO |
| 477230 | VENTA AL POR MENOR DE CALZADO DEPORTIVO |
| 477290 | VENTA AL POR MENOR DE ARTÍCULOS DE MARROQUINERÍA, PARAGUAS Y SIMILARES N.C.P. |
| 477310 | VENTA AL POR MENOR DE PRODUCTOS FARMACÉUTICOS Y DE HERBORISTERÍA |
| 477320 | VENTA AL POR MENOR DE PRODUCTOS COSMÉTICOS, DE TOCADOR Y DE PERFUMERÍA |
| 477330 | VENTA AL POR MENOR DE INSTRUMENTAL MÉDICO Y ODONTOLÓGICO Y ARTÍCULOS ORTOPÉDICOS |
| 477410 | VENTA AL POR MENOR DE ARTÍCULOS DE ÓPTICA Y FOTOGRAFÍA |
| 477420 | VENTA AL POR MENOR DE ARTÍCULOS DE RELOJERÍA Y JOYERÍA |
| 477430 | VENTA AL POR MENOR DE BIJOUTERIE Y FANTASÍA |
| 477440 | VENTA AL POR MENOR DE FLORES, PLANTAS, SEMILLAS, ABONOS, FERTILIZANTES Y OTROS PRODUCTOS DE VIVERO |
| 477450 | VENTA AL POR MENOR DE MATERIALES Y PRODUCTOS DE LIMPIEZA |
| 477460 | VENTA AL POR MENOR DE FUEL OIL, GAS EN GARRAFAS, CARBÓN Y LEÑA |
| 477470 | VENTA AL POR MENOR DE PRODUCTOS VETERINARIOS, ANIMALES DOMÉSTICOS Y ALIMENTO BALANCEADO PARA MASCOTAS |
| 477480 | VENTA AL POR MENOR DE OBRAS DE ARTE |
| 477490 | VENTA AL POR MENOR DE ARTÍCULOS NUEVOS N.C.P. |
| 477810 | VENTA AL POR MENOR DE MUEBLES USADOS |
| 477820 | VENTA AL POR MENOR DE LIBROS, REVISTAS Y SIMILARES USADOS |
| 477830 | VENTA AL POR MENOR DE ANTIGÜEDADES |
| 477840 | VENTA AL POR MENOR DE ORO, MONEDAS, SELLOS Y SIMILARES |
| 477890 | VENTA AL POR MENOR DE ARTÍCULOS USADOS N.C.P. EXCEPTO+E1155 AUTOMOTORES Y MOTOCICLETAS |
| 478010 | VENTA AL POR MENOR DE ALIMENTOS, BEBIDAS Y TABACO EN PUESTOS MÓVILES Y MERCADOS |
| 478090 | VENTA AL POR MENOR DE PRODUCTOS N.C.P. EN PUESTOS MÓVILES Y MERCADOS |
| 479101 | VENTA AL POR MENOR POR INTERNET |
| 479109 | VENTA AL POR MENOR POR CORREO, TELEVISIÓN Y OTROS MEDIOS DE COMUNICACIÓN N.C.P. |
| 479900 | VENTA AL POR MENOR NO REALIZADA EN ESTABLECIMIENTOS  N.C.P. |
| 491110 | SERVICIO DE TRANSPORTE FERROVIARIO URBANO Y SUBURBANO DE PASAJEROS |
| 491120 | SERVICIO DE TRANSPORTE FERROVIARIO INTERURBANO DE PASAJEROS |
| 491200 | SERVICIO DE TRANSPORTE FERROVIARIO DE CARGAS |
| 492110 | SERVICIO DE TRANSPORTE AUTOMOTOR URBANO Y SUBURBANO REGULAR DE PASAJEROS |
| 492120 | SERVICIOS DE TRANSPORTE AUTOMOTOR DE PASAJEROS MEDIANTE TAXIS Y REMISES, ALQUILER DE AUTOS CON CHOFER |
| 492130 | SERVICIO DE TRANSPORTE ESCOLAR |
| 492140 | SERVICIO DE TRANSPORTE AUTOMOTOR URBANO Y SUBURBANO NO REGULAR DE PASAJEROS DE OFERTA LIBRE,  EXCEPTO MEDIANTE TAXIS Y REMISES, ALQUILER DE AUTOS CON CHOFER Y TRANSPORTE ESCOLAR |
| 492150 | SERVICIO DE TRANSPORTE AUTOMOTOR INTERURBANO REGULAR DE PASAJEROS, E1203EXCEPTO TRANSPORTE INTERNACIONAL |
| 492160 | SERVICIO DE TRANSPORTE AUTOMOTOR INTERURBANO NO REGULAR DE PASAJEROS |
| 492170 | SERVICIO DE TRANSPORTE AUTOMOTOR INTERNACIONAL DE PASAJEROS |
| 492180 | SERVICIO DE TRANSPORTE AUTOMOTOR TURÍSTICO DE PASAJEROS |
| 492190 | SERVICIO DE TRANSPORTE AUTOMOTOR DE PASAJEROS N.C.P. |
| 492210 | SERVICIOS DE MUDANZA |
| 492221 | SERVICIO DE TRANSPORTE AUTOMOTOR DE CEREALES |
| 492229 | SERVICIO DE TRANSPORTE AUTOMOTOR DE MERCADERÍAS A GRANEL N.C.P. |
| 492230 | SERVICIO DE TRANSPORTE AUTOMOTOR DE ANIMALES |
| 492240 | SERVICIO DE TRANSPORTE POR CAMIÓN CISTERNA |
| 492250 | SERVICIO DE TRANSPORTE AUTOMOTOR DE MERCADERÍAS Y SUSTANCIAS PELIGROSAS |
| 492280 | SERVICIO DE TRANSPORTE AUTOMOTOR URBANO DE CARGA N.C.P. |
| 492290 | SERVICIO DE TRANSPORTE AUTOMOTOR DE CARGAS N.C.P. |
| 493110 | SERVICIO DE TRANSPORTE POR OLEODUCTOS |
| 493120 | SERVICIO DE TRANSPORTE POR POLIDUCTOS Y FUELODUCTOS |
| 493200 | SERVICIO DE TRANSPORTE POR GASODUCTOS |
| 500011 | CONSTR CALLES CARRETERAS |
| 500038 | CONSTR REFORMA DE EDIFICIOS |
| 500046 | CONSTR NO CLASIF |
| 500054 | DEMOLICION Y EXCAVACION |
| 500062 | PERFORACION POZOS DE AGUA |
| 500070 | HORMIGONADO |
| 500089 | INSTALAC PLOMERIA GAS CLOACAS |
| 500097 | INSTALAC ELECTRICAS |
| 500100 | INSTALAC NO CLASIF |
| 500119 | COLOC CUBIERT ASFALT Y TECHOS |
| 500127 | COLOC CARPINT HERRERIA DE OBRA |
| 500135 | REVOQUE ENYESADO DE PAREDES |
| 500143 | COLOC PULIDO DE PISOS |
| 500151 | COLOC PISOS Y REVEST NO CLASIF |
| 500178 | PINTURA EMPAPELADO |
| 500194 | PRESTACIONES CONSTR NO CLASIF |
| 501100 | SERVICIO DE TRANSPORTE MARÍTIMO DE PASAJEROS |
| 501110 | VENTA DE AUTOS,CAMIONETAS Y UTILITARIOS,NUEVOS |
| 501190 | VENTA DE VEHICULOS AUTOMOTORES,NUEVOS N.C.P. |
| 501200 | SERVICIO DE TRANSPORTE MARÍTIMO DE CARGA |
| 501210 | VENTA DE AUTOS,CAMIONETAS Y UTILITARIOS,USADOS |
| 501290 | VENTA DE VEHICULOS AUTOMOTORES,USADOS N.C.P. |
| 502100 | LAVADO AUTOMATICO Y MANUAL |
| 502101 | SERVICIO DE TRANSPORTE FLUVIAL Y LACUSTRE DE PASAJEROS |
| 502200 | SERVICIO DE TRANSPORTE FLUVIAL Y LACUSTRE DE CARGA |
| 502210 | REPARACION DE CAMARAS Y CUBIERTAS |
| 502220 | REPARACION DE AMORTIGUADORES, ALINEACION DE DIRECCION Y BALANCEO DE RUEDAS |
| 502300 | INSTALACION Y REPARACION DE LUNETAS Y VENTANILLAS, ALARMAS,CERRADURAS,RADIOS,SISTEMAS DE CLIMATIZACION AUTOMOTOR Y GRABADO DE CRISTALES |
| 502400 | TAPIZADO Y RETAPIZADO |
| 502500 | REPARACIONES ELECTRICAS,DEL TABLERO E INSTRUMENTAL,REPARACION Y RECARGA DE BATERIAS |
| 502600 | REPARACION Y PINTURA DE CARROCERIAS,COLOCACION DE GUARDABARROS Y PROTECCIONES EXTERIORES |
| 502910 | INSTALACION Y REPARACION DE CAÑOS DE ESCAPE |
| 502920 | MANTENIMIENTO Y REPARACION DE FRENOS |
| 502990 | MANTENIMIENTO Y REPARACION DEL MOTOR N.C.P.,MECANICA INTEGRAL |
| 503100 | VENTA AL POR MAYOR DE PARTES,PIEZAS Y ACCESORIOS DE VEHICULOS AUTOMOTORES |
| 503210 | VENTA AL POR MENOR DE CAMARAS Y CUBIERTAS |
| 503220 | VENTA AL POR MENOR DE BATERIAS |
| 503290 | VENTA AL POR MENOR DE PARTES,PIEZAS Y ACCESORIOS EXCEPTO CAMARAS,CUBIERTAS Y BATERIAS |
| 504010 | VENTA DE MOTOCICLETAS Y DE SUS PARTES,PIEZAS Y ACCESORIOS |
| 504020 | MANTENIMIENTO Y REPARACION DE MOTOCICLETAS |
| 505000 | VENTA AL POR MENOR DE COMBUSTIBLE PARA VEHICULOS AUTOMOTORES Y MOTOCICLETAS |
| 511000 | SERVICIO DE TRANSPORTE AÉREO DE PASAJEROS |
| 511111 | VENTA AL POR MAYOR EN COMISION O CONSIGNACION DE CEREALES |
| 511112 | VENTA AL POR MAYOR EN COMISION O CONSIGNACION DE SEMILLAS |
| 511119 | VENTA AL POR MAYOR EN COMISION O CONSIGNACION DE PRODUCTOS AGRICOLAS N.C.P. |
| 511121 | OPERACIONES DE INTERMEDIACION DE GANADO EN PIE. |
| 511122 | OPERACIONES DE INTERMEDIACION DE LANAS,CUEROS Y PRODUCTOS AFINES DE TERCEROS. |
| 511911 | OPERACIONES DE INTERMEDIACION DE CARNE - CONSIGNATARIO DIRECTO - |
| 511912 | OPERACIONES DE INTERMEDIACION DE CARNE EXCEPTO CONSIGNATARIO DIRECTO |
| 511919 | VENTA AL POR MAYOR EN COMISION O CONSIGNACION DE ALIMENTOS,BEBIDAS Y TABACO N.C.P. |
| 511920 | VENTA AL POR MAYOR EN COMISION O CONSIGNACION DE PROD.TEXTILES,PRENDAS DE VESTIR,CALZADO EXCEPTO EL ORTOPEDICO, ART.DE MARROQUINERIA,PARAGUAS,SIMILARES Y PRODUCTOS DE CUERO N.C.P. |
| 511930 | VENTA AL POR MAYOR EN COMISION O CONSIGNACION DE MADERA Y MATERIALES PARA LA CONSTRUCCION |
| 511940 | VENTA AL POR MAYOR EN COMISION O CONSIGNACION DE ENERGIA ELECTRICA,GAS Y COMBUSTIBLES |
| 511950 | VENTA AL POR MAYOR EN COMISION O CONSIGNACION DE MINERALES,METALES Y PRODUCTOS QUIMICOS INDUSTRIALES |
| 511960 | VENTA AL POR MAYOR EN COMISION O CONSIGNACION DE MAQUINARIA,EQUIPO PROFESIONAL INDUSTRIAL Y COMERCIAL,EMBARCACIONES Y AERONAVES |
| 511970 | VENTA AL POR MAYOR EN COMISION O CONSIGNACION DE PAPEL,CARTON,LIBROS,REVISTAS,DIARIOS,MATERIALES DE EMBALAJE Y ART. DE LIBRERIA |
| 511990 | VENTA AL POR MAYOR EN COMISION O CONSIGNACION DE MERCADERIAS N.C.P. |
| 512000 | SERVICIO DE TRANSPORTE AÉREO DE CARGAS |
| 512111 | VENTA AL POR MAYOR DE CEREALES |
| 512112 | VENTA AL POR MAYOR DE SEMILLAS |
| 512119 | VENTA AL POR MAYOR DE MATERIAS PRIMAS AGRICOLAS Y DE LA SILVICULTURA N.C.P. |
| 512121 | VENTA AL POR MAYOR DE LANAS,CUEROS EN BRUTO Y PRODUCTOS AFINES |
| 512129 | VENTA AL POR MAYOR DE MATERIAS PRIMAS PECUARIAS INCLUSO ANIMALES VIVOS N.C.P. |
| 512211 | VENTA AL POR MAYOR DE PRODUCTOS LACTEOS |
| 512212 | VENTA AL POR MAYOR DE FIAMBRES Y QUESOS |
| 512221 | VENTA AL POR MAYOR DE CARNES Y DERIVADOS EXCEPTO LAS DE AVES. |
| 512229 | VENTA AL POR MAYOR DE AVES,HUEVOS Y PRODUCTOS DE GRANJA Y DE LA CAZA N.C.P. |
| 512230 | VENTA AL POR MAYOR DE PESCADO |
| 512240 | VENTA AL POR MAYOR Y EMPAQUE DE FRUTAS,DE LEGUMBRES Y HORTALIZAS FRESCAS |
| 512250 | VENTA AL POR MAYOR DE PAN,PRODUCTOS DE CONFITERIA Y PASTAS FRESCAS |
| 512260 | VENTA AL POR MAYOR DE CHOCOLATES,GOLOSINAS Y PRODUCTOS PARA KIOSCOS Y POLIRRUBROS N.C.P.,EXCEPTO CIGARRILLOS |
| 512271 | VENTA AL POR MAYOR DE AZUCAR |
| 512272 | VENTA AL POR MAYOR DE ACEITES Y GRASAS |
| 512273 | VENTA AL POR MAYOR DE CAFE,TE,YERBA MATE Y OTRAS INFUSIONES Y ESPECIAS Y CONDIMENTOS |
| 512279 | VENTA AL POR MAYOR DE PRODUCTOS Y SUBPRODUCTOS DE MOLINERIA N.C.P. |
| 512291 | VENTA AL POR MAYOR DE FRUTAS,LEGUMBRES Y CEREALES SECOS Y EN CONSERVA |
| 512292 | VENTA AL POR MAYOR DE ALIMENTOS PARA ANIMALES |
| 512299 | VENTA AL POR MAYOR DE PRODUCTOS ALIMENTICIOS N.C.P. |
| 512311 | VENTA AL POR MAYOR DE VINO |
| 512312 | VENTA AL POR MAYOR DE BEBIDAS ESPIRITOSAS |
| 512319 | VENTA AL POR MAYOR DE BEBIDAS ALCOHOLICAS N.C.P. |
| 512320 | VENTA AL POR MAYOR DE BEBIDAS NO ALCOHOLICAS |
| 512400 | VENTA AL POR MAYOR DE CIGARRILLOS Y PRODUCTOS DE TABACO |
| 513111 | VENTA AL POR MAYOR DE PRODUCTOS TEXTILES EXCEPTO TELAS,TEJIDOS,PRENDAS Y ACCESORIOS DE VESTIR |
| 513112 | VENTA AL POR MAYOR DE TEJIDOS (TELAS) |
| 513113 | VENTA AL POR MAYOR DE ART. DE MERCERIA |
| 513114 | VENTA AL POR MAYOR DE MANTELERIA,ROPA DE CAMA Y ART. TEXTILES PARA EL HOGAR |
| 513115 | VENTA AL POR MAYOR DE TAPICES Y ALFOMBRAS DE MATERIALES TEXTILES |
| 513121 | VENTA AL POR MAYOR DE PRENDAS DE VESTIR DE CUERO |
| 513122 | VENTA AL POR MAYOR DE MEDIAS Y PRENDAS DE PUNTO |
| 513129 | VENTA AL POR MAYOR DE PRENDAS DE VESTIR N.C.P. |
| 513130 | VENTA AL POR MAYOR DE CALZADO EXCEPTO EL ORTOPEDICO |
| 513141 | VENTA AL POR MAYOR DE PIELES Y CUEROS CURTIDOS Y SALADOS |
| 513142 | VENTA AL POR MAYOR DE SUELAS Y AFINES |
| 513149 | VENTA AL POR MAYOR DE ART. DE MARROQUINERIA, PARAGUAS Y PRODUCTOS SIMILARES N.C.P. |
| 513211 | VENTA AL POR MAYOR DE LIBROS Y PUBLICACIONES |
| 513212 | VENTA AL POR MAYOR DE DIARIOS Y REVISTAS |
| 513221 | VENTA AL POR MAYOR DE PAPEL Y PRODUCTOS DE PAPEL Y CARTON EXCEPTO ENVASES |
| 513222 | VENTA AL POR MAYOR DE ENVASES DE PAPEL Y CARTON |
| 513223 | VENTA AL POR MAYOR DE ART. DE LIBRERIA Y PAPELERIA |
| 513310 | VENTA AL POR MAYOR DE PRODUCTOS FARMACEUTICOS Y VETERINARIOS |
| 513320 | VENTA AL POR MAYOR DE PRODUCTOS COSMETICOS,DE TOCADOR Y DE PERFUMERIA |
| 513330 | VENTA AL POR MAYOR DE INSTRUMENTAL MEDICO Y ODONTOLOGICO Y ART. ORTOPEDICOS |
| 513410 | VENTA AL POR MAYOR DE ART. DE OPTICA Y DE FOTOGRAFIA |
| 513420 | VENTA AL POR MAYOR DE ART. DE RELOJERIA,JOYERIA Y FANTASIAS |
| 513511 | VENTA AL POR MAYOR DE MUEBLES METALICOS EXCEPTO DE OFICINA |
| 513519 | VENTA AL POR MAYOR DE MUEBLES N.C.P.EXCEPTO DE OFICINA,ART. DE MIMBRE Y CORCHO,COLCHONES Y SOMIERES |
| 513520 | VENTA AL POR MAYOR DE ART. DE ILUMINACION |
| 513531 | VENTA AL POR MAYOR DE ART. DE VIDRIO |
| 513532 | VENTA AL POR MAYOR DE ART. DE BAZAR Y MENAJE EXCEPTO DE VIDRIO |
| 513540 | VENTA AL POR MAYOR DE ARTEFACTOS PARA EL HOGAR ELECTRICOS,A GAS,KEROSENE U OTROS COMBUSTIBLES |
| 513551 | VENTA AL POR MAYOR DE INSTRUMENTOS MUSICALES,DISCOS Y CASETES DE AUDIO Y VIDEO,ETC. |
| 513552 | VENTA AL POR MAYOR DE EQUIPOS DE SONIDO,RADIO Y TELEVISION,COMUNICACIONES Y SUS COMPONENTES,REPUESTOS Y ACCESORIOS |
| 513910 | VENTA AL POR MAYOR DE MATERIALES Y PRODUCTOS DE LIMPIEZA |
| 513920 | VENTA AL POR MAYOR DE JUGUETES |
| 513930 | VENTA AL POR MAYOR DE BICICLETAS Y RODADOS SIMILARES |
| 513940 | VENTA AL POR MAYOR DE ART. DE ESPARCIMIENTO Y DEPORTES |
| 513950 | VENTA AL POR MAYOR DE PAPELES PARA PARED,REVESTIMIENTO PARA PISOS DE GOMA,PLASTICO Y TEXTILES, Y ART. SIMILARES PARA LA DECORACION |
| 513991 | VENTA AL POR MAYOR DE FLORES Y PLANTAS NATURALES Y ARTIFICIALES |
| 513992 | VENTA AL POR MAYOR DE PRODUCTOS EN GENERAL EN ALMACENES Y SUPERMERCADOS MAYORISTAS,CON PREDOMINIO DE ALIMENTOS Y BEBIDAS |
| 513999 | VENTA AL POR MAYOR DE ART. DE USO DOMESTICO Y/O PERSONAL N.C.P |
| 514110 | VENTA AL POR MAYOR DE COMBUSTIBLES Y LUBRICANTES PARA AUTOMOTORES |
| 514191 | FRACCIONAMIENTO Y DISTRIBUCION DE GAS LICUADO |
| 514199 | VENTA AL POR MAYOR DE COMBUSTIBLES Y LUBRICANTES,EXCEPTO PARA AUTOMOTORES, LEÑA Y CARBON |
| 514200 | VENTA AL POR MAYOR DE METALES Y MINERALES METALIFEROS |
| 514310 | VENTA AL POR MAYOR DE ABERTURAS |
| 514320 | VENTA AL POR MAYOR DE PRODUCTOS DE MADERA EXCEPTO MUEBLES |
| 514330 | VENTA AL POR MAYOR DE ART. DE FERRETERIA |
| 514340 | VENTA AL POR MAYOR DE PINTURAS Y PRODUCTOS CONEXOS |
| 514350 | VENTA AL POR MAYOR DE VIDRIOS PLANOS Y TEMPLADOS |
| 514391 | VENTA AL POR MAYOR DE ART. DE PLOMERIA,ELECTRICIDAD,CALEFACCION,OBRAS SANITARIAS,ETC. |
| 514392 | VENTA AL POR MAYOR DE ART. DE LOZA,CERAMICA Y PORCELANA DE USO EN CONSTRUCCION |
| 514399 | VENTA AL POR MAYOR DE LADRILLOS,CEMENTO,CAL,ARENA,PIEDRA,MARMOL Y MATERIALES PARA LA CONSTRUCCION N.C.P. |
| 514910 | VENTA AL POR MAYOR DE PRODUCTOS INTERMEDIOS N.C.P.,DESPERDICIOS Y DESECHOS TEXTILES |
| 514920 | VENTA AL POR MAYOR DE PRODUCTOS INTERMEDIOS N.C.P.,DESPERDICIOS Y DESECHOS DE PAPEL Y CARTON |
| 514931 | VENTA AL POR MAYOR DE ABONOS,FERTILIZANTES Y PLAGUICIDAS |
| 514932 | VENTA AL POR MAYOR DE CAUCHO Y PRODUCTOS DE CAUCHO EXCEPTO CALZADO Y AUTOPARTES |
| 514933 | VENTA AL POR MAYOR DE ART. DE PLASTICO |
| 514940 | VENTA AL POR MAYOR DE PRODUCTOS INTERMEDIOS N.C.P.,DESPERDICIOS Y DESECHOS METALICOS |
| 514990 | VENTA AL POR MAYOR DE PRODUCTOS INTERMEDIOS,DESPERDICIOS Y DESECHOS N.C.P. |
| 515110 | VENTA AL POR MAYOR DE MAQUINAS,EQUIPOS E IMPLEMENTOS DE USO EN LOS SECTORES AGROPECUARIO,JARDINERIA,SILVICULTURA,PESCA Y CAZA |
| 515120 | VENTA AL POR MAYOR DE MAQUINAS,EQUIPOS E IMPLEMENTOS DE USO EN LA ELABORACION DE ALIMENTOS,BEBIDAS Y TABACOS |
| 515130 | VENTA AL POR MAYOR DE MAQUINAS,EQUIPOS E IMPLEMENTOS DE USO EN LA FABRIC.DE TEXTILES,PRENDAS Y ACCESORIOS DE VESTIR,CALZADO,ART. DE CUERO Y MARROQUINERIA |
| 515140 | VENTA AL POR MAYOR DE MAQUINAS,EQUIPOS E IMPLEMENTOS DE USO EN IMPRENTAS,ARTES GRAFICAS Y ACTIVIDADES CONEXAS |
| 515150 | VENTA AL POR MAYOR DE MAQUINAS,EQUIPOS E IMPLEMENTOS DE USO MEDICO Y PARAMEDICO |
| 515160 | VENTA AL POR MAYOR DE MAQUINAS,EQUIPOS E IMPLEMENTOS DE USO EN LA INDUSTRIA DEL PLASTICO Y DEL CAUCHO |
| 515190 | VENTA AL POR MAYOR DE MAQUINAS,EQUIPOS E IMPLEMENTOS DE USO ESPECIAL N.C.P. |
| 515200 | VENTA AL POR MAYOR DE MAQUINAS - HERRAMIENTA DE USO GENERAL |
| 515300 | VENTA AL POR MAYOR DE VEHICULOS, EQUIPOS Y MAQUINAS PARA EL TRANSPORTE FERROVIARIO,AEREO Y DE NAVEGACION |
| 515410 | VENTA AL POR MAYOR DE MUEBLES E INSTALACIONES PARA OFICINAS |
| 515420 | VENTA AL POR MAYOR DE MUEBLES E INSTALACIONES PARA LA INDUSTRIA,EL COMERCIO Y LOS SERVICIOS N.C.P. |
| 515910 | VENTA AL POR MAYOR DE EQUIPO PROFESIONAL Y CIENTIFICO E INSTRUMENTOS DE MEDIDA Y DE CONTROL |
| 515921 | VENTA AL POR MAYOR DE EQUIPOS INFORMATICOS Y MAQUINAS ELECTRONICAS DE ESCRIBIR Y CALCULAR |
| 515922 | VENTA AL POR MAYOR DE MAQUINAS Y EQUIPOS DE COMUNICACIONES,CONTROL Y SEGURIDAD |
| 515990 | VENTA AL POR MAYOR DE MAQUINAS,EQUIPO Y MATERIALES CONEXOS N.C.P. |
| 519000 | VENTA AL POR MAYOR DE MERCANCIAS N.C.P. |
| 521010 | SERVICIOS DE MANIPULACIÓN DE CARGA EN EL ÁMBITO TERRESTRE |
| 521020 | SERVICIOS DE MANIPULACIÓN DE CARGA EN EL ÁMBITO PORTUARIO |
| 521030 | SERVICIOS DE MANIPULACIÓN DE CARGA EN EL ÁMBITO AÉREO |
| 521110 | VENTA AL POR MENOR EN HIPERMERCADOS CON PREDOMINIO DE PRODUCTOS ALIMENTARIOS Y BEBIDAS |
| 521120 | VENTA AL POR MENOR EN SUPERMERCADOS CON PREDOMINIO DE PRODUCTOS ALIMENTARIOS Y BEBIDAS |
| 521130 | VENTA AL POR MENOR EN MINIMERCADOS CON PREDOMINIO DE PRODUCTOS ALIMENTARIOS Y BEBIDAS |
| 521190 | VENTA AL POR MENOR EN KIOSCOS,POLIRRUBROS Y COMERCIOS NO ESPECIALIZADOS N.C.P. |
| 521200 | VENTA AL POR MENOR EXCEPTO LA ESPECIALIZADA,SIN PREDOMINIO DE PRODUCTOS ALIMENTARIOS Y BEBIDAS |
| 522010 | SERVICIOS DE ALMACENAMIENTO Y DEPÓSITO EN SILOS |
| 522020 | SERVICIOS DE ALMACENAMIENTO Y DEPÓSITO EN CÁMARAS FRIGORÍFICAS |
| 522091 | SERVICIOS DE USUARIOS DIRECTOS DE ZONA FRANCA |
| 522092 | SERVICIOS DE GESTIÓN DE DEPÓSITOS FISCALES |
| 522099 | SERVICIOS DE ALMACENAMIENTO Y DEPÓSITO N.C.P. |
| 522111 | VENTA AL POR MENOR DE PRODUCTOS LACTEOS |
| 522112 | VENTA AL POR MENOR DE FIAMBRES Y EMBUTIDOS |
| 522120 | VENTA AL POR MENOR DE PRODUCTOS DE ALMACEN Y DIETETICA |
| 522210 | VENTA AL POR MENOR DE CARNES ROJAS,MENUDENCIAS Y CHACINADOS FRESCOS |
| 522220 | VENTA AL POR MENOR DE HUEVOS,CARNE DE AVES Y PRODUCTOS DE GRANJA Y DE LA CAZA N.C.P. |
| 522300 | VENTA AL POR MENOR DE FRUTAS,LEGUMBRES Y HORTALIZAS FRESCAS |
| 522410 | VENTA AL POR MENOR DE PAN Y PRODUCTOS DE PANADERIA |
| 522420 | VENTA AL POR MENOR DE BOMBONES,GOLOSINAS Y DEMAS PRODUCTOS DE CONFITERIA |
| 522500 | VENTA AL POR MENOR DE BEBIDAS |
| 522910 | VENTA AL POR MENOR DE PESCADOS Y PRODUCTOS DE LA PESCA |
| 522991 | VENTA AL POR MENOR DE TABACO Y SUS PRODUCTOS |
| 522999 | VENTA AL POR MENOR DE PRODUCTOS ALIMENTARIOS N.C.P.,EN COMERCIOS ESPECIALIZADOS |
| 523011 | SERVICIOS DE GESTIÓN ADUANERA REALIZADOS POR DESPACHANTES DE ADUANA |
| 523019 | SERVICIOS DE GESTIÓN ADUANERA PARA EL TRANSPORTE DE MERCADERÍAS N.C.P. |
| 523020 | SERVICIOS DE AGENCIAS MARÍTIMAS PARA EL TRANSPORTE DE MERCADERÍAS |
| 523031 | SERVICIOS DE GESTIÓN DE AGENTES DE TRANSPORTE ADUANERO EXCEPTO AGENCIAS MARÍTIMAS |
| 523032 | SERVICIOS DE OPERADORES LOGÍSTICOS SEGUROS (OLS) EN EL ÁMBITO ADUANERO |
| 523039 | SERVICIOS DE OPERADORES LOGÍSTICOS N.C.P. |
| 523090 | SERVICIOS DE GESTIÓN Y LOGÍSTICA PARA EL TRANSPORTE DE MERCADERÍAS N.C.P. |
| 523110 | VENTA AL POR MENOR DE PRODUCTOS FARMACEUTICOS Y DE HERBORISTERIA |
| 523120 | VENTA AL POR MENOR DE PRODUCTOS COSMETICOS,DE TOCADOR Y DE PERFUMERIA |
| 523130 | VENTA AL POR MENOR DE INSTRUMENTAL MEDICO Y ODONTOLOGICO Y ART. ORTOPEDICOS |
| 523210 | VENTA AL POR MENOR DE HILADOS,TEJIDOS Y ART. DE MERCERIA |
| 523220 | VENTA AL POR MENOR DE CONFECCIONES PARA EL HOGAR |
| 523290 | VENTA AL POR MENOR DE ART. TEXTILES N.C.P.EXCEPTO PRENDAS DE VESTIR |
| 523310 | VENTA AL POR MENOR DE ROPA INTERIOR,MEDIAS,PRENDAS PARA DORMIR Y PARA LA PLAYA |
| 523320 | VENTA AL POR MENOR DE INDUMENTARIA DE TRABAJO,UNIFORMES Y GUARDAPOLVOS |
| 523330 | VENTA AL POR MENOR DE INDUMENTARIA PARA BEBES Y NIÑOS |
| 523391 | VENTA AL POR MENOR DE PRENDAS DE VESTIR DE CUERO Y SUCEDANEOS EXCEPTO CALZADO |
| 523399 | VENTA AL POR MENOR DE PRENDAS Y ACCESORIOS DE VESTIR N.C.P.EXCEPTO CALZADO,ART. DE MARROQUINERIA,PARAGUAS Y SIMILARES |
| 523410 | VENTA AL POR MENOR DE ART. REGIONALES Y DE TALABARTERIA |
| 523420 | VENTA AL POR MENOR DE CALZADO EXCEPTO EL ORTOPEDICO |
| 523490 | VENTA AL POR MENOR DE ART. DE MARROQUINERIA,PARAGUAS Y SIMILARES N.C.P. |
| 523510 | VENTA AL POR MENOR DE MUEBLES EXCEPTO DE OFICINA,LA INDUSTRIA,EL COMERCIO Y LOS SERVICIOS,ART. DE MIMBRE Y CORCHO |
| 523520 | VENTA AL POR MENOR DE COLCHONES Y SOMIERES |
| 523530 | VENTA AL POR MENOR DE ART. DE ILUMINACION |
| 523540 | VENTA AL POR MENOR DE ART. DE BAZAR Y MENAJE |
| 523550 | VENTA AL POR MENOR DE ARTEFACTOS PARA EL HOGAR ELECTRICOS,A GAS,A KEROSENE U OTROS COMBUSTIBLES |
| 523560 | VENTA AL POR MENOR DE INSTRUMENTOS MUSICALES,EQUIPOS DE SONIDO,CASETES DE AUDIO Y VIDEO,DISCOS DE AUDIO Y VIDEO |
| 523590 | VENTA AL POR MENOR DE ART. PARA EL HOGAR N.C.P. |
| 523610 | VENTA AL POR MENOR DE ABERTURAS |
| 523620 | VENTA AL POR MENOR DE MADERAS Y ART. DE MADERA Y CORCHO EXCEPTO MUEBLES |
| 523630 | VENTA AL POR MENOR DE ART. DE FERRETERIA |
| 523640 | VENTA AL POR MENOR DE PINTURAS Y PRODUCTOS CONEXOS |
| 523650 | VENTA AL POR MENOR DE ART. PARA PLOMERIA E INSTALACION DE GAS |
| 523660 | VENTA AL POR MENOR DE CRISTALES,ESPEJOS,MAMPARAS Y CERRAMIENTOS |
| 523670 | VENTA AL POR MENOR DE PAPELES PARA PARED,REVESTIMIENTOS PARA PISOS Y ART. SIMILARES PARA LA DECORACION |
| 523690 | VENTA AL POR MENOR DE MATERIALES DE CONSTRUCCION N.C.P. |
| 523710 | VENTA AL POR MENOR DE ART. DE OPTICA Y FOTOGRAFIA |
| 523720 | VENTA AL POR MENOR DE ART. DE RELOJERIA,JOYERIA Y FANTASIA |
| 523810 | VENTA AL POR MENOR DE LIBROS Y PUBLICACIONES |
| 523820 | VENTA AL POR MENOR DE DIARIOS Y REVISTAS |
| 523830 | VENTA AL POR MENOR DE PAPEL,CARTON,MATERIALES DE EMBALAJE Y ART. DE LIBRERIA |
| 523911 | VENTA AL POR MENOR DE FLORES Y PLANTAS NATURALES Y ARTIFICIALES |
| 523912 | VENTA AL POR MENOR DE SEMILLAS,ABONOS,FERTILIZANTES Y OTROS PRODUCTOS DE VIVERO |
| 523920 | VENTA AL POR MENOR DE MATERIALES Y PRODUCTOS DE LIMPIEZA |
| 523930 | VENTA AL POR MENOR DE JUGUETES Y ART. DE COTILLON |
| 523941 | VENTA AL POR MENOR DE ART. DE DEPORTE,EQUIPOS E INDUMENTARIA DEPORTIVA |
| 523942 | VENTA AL POR MENOR DE ARMAS Y ART. DE CUCHILLERIA,ART. PARA LA CAZA Y PESCA |
| 523950 | VENTA AL POR MENOR DE MAQUINAS Y EQUIPOS PARA OFICINA Y SUS COMPONENTES Y REPUESTOS |
| 523960 | VENTA AL POR MENOR DE FUEL OIL,GAS EN GARRAFAS,CARBON Y LEÑA |
| 523970 | VENTA AL POR MENOR DE PRODUCTOS VETERINARIOS Y ANIMALES DOMESTICOS |
| 523991 | VENTA AL POR MENOR DE ART. DE CAUCHO EXCEPTO CAMARAS Y CUBIERTAS |
| 523992 | VENTA AL POR MENOR DE MAQUINAS Y MOTORES Y SUS REPUESTOS |
| 523993 | VENTA AL POR MENOR DE EQUIPO PROFESIONAL Y CIENTIFICO E INSTRUMENTOS DE MEDIDA Y DE CONTROL |
| 523994 | VENTA AL POR MENOR DE ART. DE COLECCION Y OBJETOS DE ARTE |
| 523999 | VENTA AL POR MENOR DE ART. NUEVOS N.C.P. |
| 524100 | VENTA AL POR MENOR DE MUEBLES USADOS |
| 524110 | SERVICIOS DE EXPLOTACIÓN DE INFRAESTRUCTURA PARA EL TRANSPORTE TERRESTRE, PEAJES Y OTROS DERECHOS |
| 524120 | SERVICIOS  DE PLAYAS DE ESTACIONAMIENTO Y GARAJES |
| 524130 | SERVICIOS DE ESTACIONES TERMINALES DE ÓMNIBUS Y FERROVIÁRIAS |
| 524190 | SERVICIOS COMPLEMENTARIOS PARA EL TRANSPORTE TERRESTRE N.C.P. |
| 524200 | VENTA AL POR MENOR DE LIBROS,REVISTAS Y SIMILARES USADOS |
| 524210 | SERVICIOS DE EXPLOTACIÓN DE INFRAESTRUCTURA PARA EL TRANSPORTE MARÍTIMO, DERECHOS DE PUERTO |
| 524220 | SERVICIOS DE GUARDERÍAS NÁUTICAS |
| 524230 | SERVICIOS PARA LA NAVEGACIÓN |
| 524290 | SERVICIOS COMPLEMENTARIOS PARA EL TRANSPORTE MARÍTIMO N.C.P. |
| 524310 | SERVICIOS DE EXPLOTACIÓN DE INFRAESTRUCTURA PARA EL TRANSPORTE AÉREO, DERECHOS DE AEROPUERTO |
| 524320 | SERVICIOS DE HANGARES Y ESTACIONAMIENTO DE AERONAVES |
| 524330 | SERVICIOS PARA LA AERONAVEGACIÓN |
| 524390 | SERVICIOS COMPLEMENTARIOS PARA EL TRANSPORTE AÉREO N.C.P. |
| 524910 | VENTA AL POR MENOR DE ANTIGÜEDADES |
| 524990 | VENTA AL POR MENOR DE ART. USADOS N.C.P.EXCLUIDOS AUTOMOTORES Y MOTOCICLETAS |
| 525100 | VENTA AL POR MENOR POR CORREO,TELEVISION,INTERNET Y OTROS MEDIOS DE COMUNICACION |
| 525200 | VENTA AL POR MENOR EN PUESTOS MOVILES |
| 525900 | VENTA AL POR MENOR NO REALIZADA EN ESTABLECIMIENTOS N.C.P. |
| 526100 | REPARACION DE CALZADO Y ART. DE MARROQUINERIA |
| 526200 | REPARACION DE ART. ELECTRICOS DE USO DOMESTICO |
| 526901 | REPARACION DE RELOJES Y JOYAS |
| 526909 | REPARACION DE ART. N.C.P. |
| 530010 | SERVICIO DE CORREO POSTAL |
| 530090 | SERVICIOS DE MENSAJERÍAS. |
| 551010 | SERVICIOS DE ALOJAMIENTO POR HORA |
| 551021 | SERVICIOS DE ALOJAMIENTO EN PENSIONES |
| 551022 | SERVICIOS DE ALOJAMIENTO EN HOTELES, HOSTERÍAS Y RESIDENCIALES SIMILARES, EXCEPTO POR HORA, QUE INCLUYEN SERVICIO DE RESTAURANTE AL PÚBLICO |
| 551023 | SERVICIOS DE ALOJAMIENTO EN HOTELES, HOSTERÍAS Y RESIDENCIALES SIMILARES, EXCEPTO POR HORA, QUE NO INCLUYEN SERVICIO DE RESTAURANTE AL PÚBLICO |
| 551090 | SERVICIOS DE HOSPEDAJE TEMPORAL N.C.P. |
| 551100 | SERVICIOS DE ALOJAMIENTO EN CAMPING |
| 551210 | SERVICIOS DE ALOJAMIENTO POR HORA |
| 551221 | SERVICIOS DE ALOJAMIENTO EN PENSIONES |
| 551222 | SERVICIOS DE ALOJAMIENTO EN HOTELES,HOSTERIAS Y RESIDENCIALES SIMILARES,EXCEPTO POR HORA,QUE INCLUYEN SERVICIO DE RESTAURANTE AL PUBLICO |
| 551223 | SERVICIOS DE ALOJAMIENTO EN HOTELES,HOSTERIAS Y RESIDENCIALES SIMILARES,EXCEPTO POR HORA,QUE NO INCLUYEN SERVICIO DE RESTAURANTE AL PUBLICO |
| 551229 | SERVICIOS DE HOSPEDAJE TEMPORAL N.C.P. |
| 552000 | SERVICIOS DE ALOJAMIENTO EN CAMPINGS |
| 552111 | SERVICIOS DE RESTAURANTES Y CANTINAS SIN ESPECTACULO |
| 552112 | SERVICIOS DE RESTAURANTES Y CANTINAS CON ESPECTACULO |
| 552113 | SERVICIOS DE PIZZERIAS,FAST FOOD Y LOCALES DE VENTA DE COMIDAS Y BEBIDAS AL PASO |
| 552114 | SERVICIOS DE BARES Y CONFITERIAS |
| 552119 | SERVICIOS DE EXPENDIO DE COMIDAS Y BEBIDAS EN ESTABLECIMIENTOS CON SERVICIO DE MESA Y/O EN MOSTRADOR - EXCEPTO EN HELADERIAS - N.C.P. |
| 552120 | EXPENDIO DE HELADOS |
| 552210 | PROVISION DE COMIDAS PREPARADAS PARA EMPRESAS |
| 552290 | PREPARACION Y VENTA DE COMIDAS PARA LLEVAR N.C.P. |
| 561011 | SERVICIOS DE RESTAURANTES Y CANTINAS SIN ESPECTÁCULO |
| 561012 | SERVICIOS DE RESTAURANTES Y CANTINAS CON ESPECTÁCULO |
| 561013 | SERVICIOS DE FAST FOOD Y LOCALES DE VENTA DE COMIDAS Y BEBIDAS AL PASO |
| 561014 | SERVICIOS DE EXPENDIO DE BEBIDAS EN BARES |
| 561019 | SERVICIOS DE EXPENDIO DE COMIDAS Y BEBIDAS EN ESTABLECIMIENTOS CON SERVICIO DE MESA Y/O EN MOSTRADOR N.C.P. |
| 561020 | SERVICIOS DE PREPARACIÓN DE COMIDAS PARA LLEVAR |
| 561030 | SERVICIO DE EXPENDIO DE HELADOS |
| 561040 | SERVICIOS DE PREPARACIÓN DE COMIDAS REALIZADAS POR/PARA VENDEDORES AMBULANTES. |
| 562010 | SERVICIOS DE PREPARACIÓN DE COMIDAS PARA EMPRESAS Y EVENTOS |
| 562091 | SERVICIOS DE CANTINAS CON ATENCIÓN EXCLUSIVA  A LOS EMPLEADOS O ESTUDIANTES DENTRO DE EMPRESAS O ESTABLECIMIENTOS EDUCATIVOS. |
| 562099 | SERVICIOS DE COMIDAS N.C.P. |
| 581100 | EDICIÓN DE LIBROS, FOLLETOS, Y OTRAS PUBLICACIONES |
| 581200 | EDICIÓN DE DIRECTORIOS Y LISTAS DE CORREOS |
| 581300 | EDICIÓN DE PERIÓDICOS, REVISTAS Y PUBLICACIONES PERIÓDICAS |
| 581900 | EDICIÓN N.C.P. |
| 591110 | PRODUCCIÓN DE FILMES Y VIDEOCINTAS |
| 591120 | POSTPRODUCCIÓN DE FILMES Y VIDEOCINTAS |
| 591200 | DISTRIBUCIÓN DE FILMES Y VIDEOCINTAS |
| 591300 | EXHIBICIÓN DE FILMES Y VIDEOCINTAS |
| 592000 | SERVICIOS DE GRABACIÓN DE SONIDO Y EDICIÓN DE MÚSICA |
| 601000 | EMISIÓN Y RETRANSMISIÓN DE RADIO |
| 601100 | SERVICIO DE TRANSPORTE FERROVIARIO DE CARGAS |
| 601210 | SERVICIO DE TRANSPORTE FERROVIARIO URBANO Y SUBURBANO DE PASAJEROS |
| 601220 | SERVICIO DE TRANSPORTE FERROVIARIO INTERURBANO DE PASAJEROS |
| 602100 | EMISIÓN Y RETRANSMISIÓN  DE TELEVISIÓN ABIERTA |
| 602110 | SERVICIOS DE MUDANZA |
| 602120 | SERVICIOS DE TRANSPORTE DE MERCADERIAS A GRANEL,INCLUIDO EL TRANSPORTE POR CAMION CISTERNA |
| 602130 | SERVICIOS DE TRANSPORTE DE ANIMALES |
| 602180 | SERVICIO DE TRANSPORTE URBANO DE CARGA N.C.P. |
| 602190 | TRANSPORTE AUTOMOTOR DE CARGAS N.C.P. |
| 602200 | OPERADORES DE TELEVISIÓN POR SUSCRIPCIÓN. |
| 602210 | SERVICIO DE TRANSPORTE AUTOMOTOR URBANO REGULAR DE PASAJEROS |
| 602220 | SERVICIOS DE TRANSPORTE AUTOMOTOR DE PASAJEROS MEDIANTE TAXIS Y REMISES,ALQUILER DE AUTOS CON CHOFER |
| 602230 | SERVICIO DE TRANSPORTE ESCOLAR |
| 602240 | SERVICIO DE TRANSPORTE AUTOMOTOR URBANO DE OFERTA LIBRE DE PASAJEROS EXCEPTO MEDIANTE TAXIS Y REMISES,ALQUILER DE AUTOS CON CHOFER Y TRANSPORTE ESCOLAR |
| 602250 | SERVICIO DE TRANSPORTE AUTOMOTOR INTERURBANO DE PASAJEROS |
| 602260 | SERVICIO DE TRANSPORTE AUTOMOTOR DE PASAJEROS PARA EL TURISMO |
| 602290 | SERVICIO DE TRANSPORTE AUTOMOTOR DE PASAJEROS N.C.P. |
| 602310 | EMISIÓN DE SEÑALES DE TELEVISIÓN POR SUSCRIPCIÓN |
| 602320 | PRODUCCIÓN DE PROGRAMAS DE TELEVISIÓN |
| 602900 | SERVICIOS DE TELEVISIÓN N.C.P |
| 603100 | SERVICIO DE TRANSPORTE POR OLEODUCTOS Y POLIDUCTOS |
| 603200 | SERVICIO DE TRANSPORTE POR GASODUCTOS |
| 611010 | SERVICIOS DE LOCUTORIOS |
| 611018 | CONSIGNATARIOS DE HACIENDA |
| 611026 | PLACEROS INTERM GANADO EN PIE |
| 611034 | REMATES EN FERIA INTERM GANADO |
| 611042 | OPER INTERM DE RESES MATARIFES |
| 611050 | ABASTEC CARNES Y DERIV NO AVES |
| 611069 | ACOP Y VTA CEREALES |
| 611077 | ACOP Y VTA SEMILLAS |
| 611085 | OPER INTERMED LANAS Y CUEROS |
| 611090 | SERVICIOS DE TELEFONÍA FIJA, EXCEPTO LOCUTORIOS |
| 611093 | ACOP Y VTA LANAS CUER Y AFINES |
| 611100 | SERVICIO DE TRANSPORTE MARITIMO DE CARGA |
| 611115 | VTA FIAMBRES EMBUTI Y CHACINAD |
| 611123 | VTA AVES HUEVOS |
| 611131 | VTA PRODUCTOS LACTEOS |
| 611158 | ACOP Y VTA FRUTAS HORTA FRESCA |
| 611166 | ACOP Y VTA FRUTAS LEGUMB SECOS |
| 611174 | ACOP Y VTA PESCAD Y PROD MARIN |
| 611182 | VTA ACEITES Y GRASAS |
| 611190 | ACOP Y VTA PRODUCTOS MOLINERIA |
| 611200 | SERVICIO DE TRANSPORTE MARITIMO DE PASAJEROS |
| 611204 | ACOP Y VTA AZUCAR |
| 611212 | ACOP Y VTA CAFE TE YERBA |
| 611220 | DISTR Y VTA CHOCOLAT CARAM ETC |
| 611239 | DISTR Y VTA ALIMENT P/ANIMALES |
| 611298 | ACOP Y VTA PROD GANAD N/CLASIF |
| 611301 | ALMAC Y SUPERM MAYORIS ALIMENT |
| 612000 | SERVICIOS DE TELEFONÍA MÓVIL |
| 612014 | FRACCIONAMIENTO ALCOHOLES |
| 612022 | FRACCIONAMIENTO VINO |
| 612030 | DISTR VENTA VINO |
| 612049 | FRAC DIST VTA BEBI ESPIRITOSAS |
| 612057 | DISTR VTA BEBID NO ALCOHOLICAS |
| 612065 | DISTR VTA TABACOS CIGARRILLOS |
| 612100 | SERVICIO DE TRANSPORTE FLUVIAL DE CARGAS |
| 612200 | SERVICIO DE TRANSPORTE FLUVIAL DE PASAJEROS |
| 613000 | SERVICIOS DE TELECOMUNICACIONES VÍA SATÉLITE, EXCEPTO SERVICIOS DE TRANSMISIÓN DE TELEVISIÓN |
| 613010 | DISTR VTA FIBRAS HILADOS HILOS |
| 613029 | DISTR Y VTA TEJIDOS |
| 613037 | DISTR VTA ARTIC MERCER MEDIAS |
| 613045 | DISTR Y VTA MANTELER ROPA CAMA |
| 613053 | DISTR Y VTA TAPICES ALFOMBRAS |
| 613061 | DISTR VTA PREND VESTIR N/CUERO |
| 613088 | DISTR Y VTA PIELES Y CUEROS |
| 613096 | DISTR VTA ARTIC CUERO N/VESTIR |
| 613118 | DISTR VTA PRENDAS VESTIR CUERO |
| 613126 | DISTR Y VTA CALZADO |
| 613134 | DISTR Y VTA SUELAS Y AFINES |
| 614010 | SERVICIOS DE PROVEEDORES DE ACCESO A INTERNET |
| 614017 | VTA MADERA Y PRODUC NO MUEBLES |
| 614025 | VTA MUEBLES Y ACCESORIOS |
| 614033 | DISTR Y VTA PAPEL CARTON |
| 614041 | DISTR Y VTA ENVASES PAPEL |
| 614068 | DISTR Y VTA ART PAPEL LIBRERIA |
| 614076 | EDICION DISTRIB Y VTA LIBROS |
| 614084 | DISTR Y VTA DIARIOS Y REVISTAS |
| 614090 | SERVICIOS DE TELECOMUNICACIÓN VÍA INTERNET N.C.P. |
| 615013 | DISTR Y VTA SUST QUIMICAS IND |
| 615021 | DISTR Y VTA ABONOS PLAGUICIDAS |
| 615048 | DISTR Y VTA PINTURAS BARNICES |
| 615056 | DISTR/VTA PROD FARMA Y MEDICIN |
| 615064 | DISTR Y VTA ART DE TOCADOR |
| 615072 | DISTR/VTA ART LIMPI PULIDO ETC |
| 615080 | DISTR Y VTA ARTIC DE PLASTICO |
| 615099 | FRACC Y DISTR GAS LICUADO |
| 615102 | DISTR/VTA PETR CARBON Y DERIVA |
| 615110 | DISTR/VTA CAUCHO Y PROD CAUCHO |
| 616028 | DISTR/VTA OBJETOS BARRO PORCEL |
| 616036 | DISTR Y VTA ART BAZAR Y MENAJE |
| 616044 | DISTR/VTA VIDRIO PLANOS Y TEMP |
| 616052 | DISTR/VTA ART VIDRIO Y CRISTAL |
| 616060 | DISTR/VTA ART PLOMERIA ELECTR |
| 616079 | DISTR Y VTA MAT P/CONSTRUCCION |
| 616087 | DISTR Y VTA PUERTAS Y VENTANAS |
| 617016 | DISTR Y VTA HIERRO ACEROS ETC |
| 617024 | DISTR Y VTA MUEBLES METALICOS |
| 617032 | DISTR/VTA ARTICULOS METALICOS |
| 617040 | DISTR Y VTA ARMAS CUCHILLERIA |
| 617091 | DISTR/VTA ART METALIC N/CLASIF |
| 618012 | DISTR/VTA MOTORES EQUIP INDUST |
| 618020 | DISTR/VTA MAQUINAR USO DOMESTI |
| 618039 | DISTR Y VTA REPUES P/VEHICULOS |
| 618047 | DISTR Y VTA COMPUTADORAS ETC |
| 618055 | DISTR Y VTA EQUIP D/RADIO Y TV |
| 618063 | DISTR/VTA INSTR MUSICAL DISCOS |
| 618071 | DISTR/VTA EQU PROFES Y CIENTIF |
| 618098 | DISTR/VTA APARATOS FOTOGRAFIA |
| 619000 | SERVICIOS DE TELECOMUNICACIONES N.C.P. |
| 619019 | DISTR Y VTA JOYAS RELOJES |
| 619027 | DISTR/VTA JUGUETERIA COTILLON |
| 619035 | DISTR Y VTA FLORES PLANTAS |
| 619094 | DISTR/VTA ARTICULOS NO CLASIF |
| 619108 | ALMACENES Y SUPERMER MAYORISTA |
| 620100 | SERVICIOS DE CONSULTORES EN INFORMÁTICA Y SUMINISTROS DE PROGRAMAS DE INFORMÁTICA |
| 620200 | SERVICIOS DE CONSULTORES EN EQUIPO DE INFORMÁTICA |
| 620300 | SERVICIOS DE CONSULTORES EN TECNOLOGÍA DE LA INFORMACIÓN |
| 620900 | SERVICIOS DE INFORMÁTICA N.C.P. |
| 621000 | SERVICIO DE TRANSPORTE AEREO DE CARGAS |
| 621013 | VTA CARNES CARNICERIAS |
| 621021 | VTA PRODUCTOS DE GRANJA |
| 621048 | VTA PESCADO PRODUCTOS MARINOS |
| 621056 | VTA FIAMBRES Y COMIDAS PREPAR |
| 621064 | VTA PRODUCT LACTEOS LECHERIAS |
| 621072 | VTA FRUTAS Y HORTALIZAS |
| 621080 | VTA PAN PANADERIAS |
| 621099 | VTA BOMBONES GOLOSINAS |
| 621102 | VTA PROD ALIMENTARIOS ALMACEN |
| 622000 | SERVICIO DE TRANSPORTE AEREO DE PASAJEROS |
| 622028 | VTA TABACOS Y CIGARRILLOS |
| 622036 | VTA BILLETES LOTERIA QUINIELA |
| 623016 | VTA PRENDAS VESTIR TIENDA |
| 623024 | VTA TAPICES Y ALFOMBRAS |
| 623032 | VTA PRODUCTOS TEXTILES |
| 623040 | VTA ARTIC CUERO MARROQUINERIA |
| 623059 | VTA PRENDAS VESTIR DE CUERO |
| 623067 | VTA CALZADOS ZAPATERIAS |
| 623075 | ALQUILER ROPA EN GENERAL |
| 624012 | VTA ARTIC MADERA NO MUEBLES |
| 624020 | VTA MUEBLES MUEBLERIAS |
| 624039 | VTA INSTRUMEN MUSICALES DISCOS |
| 624047 | VTA ARTIC JUGUETERIA/COTILLON |
| 624055 | VTA ARTIC LIBRERIA Y PAPELERIA |
| 624063 | VTA MAQUI OFICINA COMPUTADORAS |
| 624071 | VTA PINTURAS Y ART FERRETERIA |
| 624098 | VTA ARMAS ARTICUL CAZA Y PESCA |
| 624101 | VTA PROD FARMACEUTIC FARMACIAS |
| 624128 | VTA ARTICULOS TOCADOR PERFUMES |
| 624136 | VTA PROD MEDICINALES P/ANIMALE |
| 624144 | VTA SEMILLAS ABONOS |
| 624152 | VTA FLORES PLANTAS NATUR/ARTIF |
| 624160 | VTA GARRAFAS COMB SOLIDOS/LIQ |
| 624179 | VTA CAMARAS CUBIERTAS GOMERIAS |
| 624187 | VTA ARTICUL CAUCHO N/CUBIERTAS |
| 624195 | VTA ARTICULOS BAZAR MENAJE |
| 624209 | VTA MATERIALES P/ CONSTRUCCION |
| 624217 | VTA SANITARIOS |
| 624225 | VTA ARTEFA ELECT P/ILUMINACION |
| 624233 | VTA ARTICULOS PARA EL HOGAR |
| 624241 | VTA MAQUINAR MOTORES/REPUESTOS |
| 624268 | VTA VEHICUL AUTOMOTORES NUEVOS |
| 624276 | VTA VEHICUL AUTOMOTORES USADOS |
| 624284 | VTA REPUEST ACCES P/VEHICULOS |
| 624292 | VTA EQUIPO PROFES CIENTIFICO |
| 624306 | VTA ARTIC FOTOGRAFIA Y OPTICA |
| 624314 | VTA JOYAS Y RELOJES |
| 624322 | VTA ANTIGUEDADES OBJETOS ARTE |
| 624330 | VTA ANTIG/ART USADOS EN REMATE |
| 624349 | VTA Y ALQUIL ARTIC DE DEPORTE |
| 624381 | VTA DE ARTICULOS NO CLASIF |
| 624403 | VTA PROD EN GRAL SUPERMERCADOS |
| 624500 | ALQUIL COSAS MUEBLES NO CLASIF |
| 631000 | SERVICIOS DE MANIPULACION DE CARGA |
| 631019 | EXPEN COMIDAS BEBID RESTAURANT |
| 631027 | EXPEND PIZZA Y BEBID PARRILLAS |
| 631035 | EXPEND BEBID BARES/CERVECERIAS |
| 631043 | EXPEND PRODUCT LACTEOS HELADOS |
| 631051 | EXPEND CONFITUR Y ALIM LIGEROS |
| 631078 | EXPEND COMIDAS BEBID C/ESPECT |
| 631110 | PROCESAMIENTO DE DATOS |
| 631120 | HOSPEDAJE DE DATOS |
| 631190 | ACTIVIDADES CONEXAS AL PROCESAMIENTO Y HOSPEDAJE DE DATOS N.C.P. |
| 631200 | PORTALES WEB |
| 632000 | SERVICIOS DE ALMACENAMIENTO Y DEPOSITO |
| 632015 | SERV ALOJ Y COMIDA EN HOTELES |
| 632023 | SERV ALOJ Y COMIDA E/PENSIONES |
| 632031 | SERVIC ALOJ POR HORA |
| 632090 | SERV ALOJ EN LUGARES NO CLASIF |
| 633110 | SERVICIOS DE EXPLOTACION DE INFRAESTRUCTURA PARA EL TRANSPORTE TERRESTRE,PEAJES Y OTROS DERECHOS |
| 633120 | SERVICIOS PRESTADOS POR PLAYAS DE ESTACIONAMIENTO Y GARAJES |
| 633190 | SERVICIOS COMPLEMENTARIOS PARA EL TRANSPORTE TERRESTRE N.C.P. |
| 633210 | SERVICIOS DE EXPLOTACION DE INFRAESTRUCTURA PARA EL TRANSPORTE POR AGUA, DERECHOS DE PUERTO |
| 633220 | SERVICIOS DE GUARDERIAS NAUTICAS |
| 633230 | SERVICIOS PARA LA NAVEGACION |
| 633290 | SERVICIOS COMPLEMENTARIOS PARA EL TRANSPORTE POR AGUA N.C.P. |
| 633310 | SERVICIOS DE HANGARES,ESTACIONAMIENTO Y REMOLQUE DE AERONAVES |
| 633320 | SERVICIOS PARA LA AERONAVEGACION |
| 633390 | SERVICIOS COMPLEMENTARIOS PARA EL TRANSPORTE AEREO N.C.P. |
| 634100 | SERVICIOS MAYORISTAS DE AGENCIAS DE VIAJES |
| 634200 | SERVICIOS MINORISTAS DE AGENCIAS DE VIAJES |
| 634300 | SERVICIOS COMPLEMENTARIOS DE APOYO TURISTICO |
| 635000 | SERVICIOS DE GESTION Y LOGISTICA PARA EL TRANSPORTE DE MERCADERIAS |
| 639100 | AGENCIAS DE NOTICIAS |
| 639900 | SERVICIOS DE INFORMACIÓN N.C.P. |
| 641000 | SERVICIOS DE CORREOS |
| 641100 | SERVICIOS DE LA BANCA CENTRAL |
| 641910 | SERVICIOS DE LA BANCA MAYORISTA |
| 641920 | SERVICIOS DE LA BANCA DE INVERSIÓN |
| 641930 | SERVICIOS DE LA BANCA MINORISTA |
| 641941 | SERVICIOS DE INTERMEDIACIÓN FINANCIERA REALIZADA POR LAS COMPAÑÍAS FINANCIERAS |
| 641942 | SERVICIOS DE INTERMEDIACIÓN FINANCIERA REALIZADA POR SOCIEDADES DE AHORRO Y PRÉSTAMO PARA LA VIVIENDA Y OTROS INMUEBLES |
| 641943 | SERVICIOS DE INTERMEDIACIÓN FINANCIERA REALIZADA POR CAJAS DE CRÉDITO |
| 642000 | SERVICIOS DE SOCIEDADES DE CARTERA |
| 642010 | SERVICIOS DE TRANSMISION DE RADIO Y TELEVISION |
| 642020 | SERVICIOS DE COMUNICACION POR MEDIO DE TELEFONO,TELEGRAFO Y TELEX |
| 642091 | EMISION DE PROGRAMAS DE TELEVISION |
| 642099 | SERVICIOS DE TRANSMISION N.C.P.DE SONIDO,IMAGENES,DATOS U OTRA INFORMACION |
| 643001 | SERVICIOS DE FIDEICOMISOS |
| 643009 | FONDOS Y SOCIEDADES DE INVERSIÓN Y ENTIDADES FINANCIERAS SIMILARES N.C.P. |
| 649100 | ARRENDAMIENTO FINANCIERO, LEASING |
| 649210 | ACTIVIDADES DE CRÉDITO PARA FINANCIAR OTRAS ACTIVIDADES ECONÓMICAS |
| 649220 | SERVICIOS DE ENTIDADES DE TARJETA DE COMPRA Y/O CRÉDITO |
| 649290 | SERVICIOS DE CRÉDITO N.C.P. |
| 649910 | SERVICIOS DE AGENTES DE MERCADO ABIERTO PUROS |
| 649991 | SERVICIOS DE SOCIOS INVERSORES EN SOCIEDADES REGULARES SEGÚN LEY 19.550 - S.R.L., S.C.A, ETC, EXCEPTO SOCIOS INVERSORES EN SOCIEDADES ANÓNIMAS INCLUIDOS EN 649999 - |
| 649999 | SERVICIOS DE FINANCIACIÓN Y ACTIVIDADES FINANCIERAS N.C.P. |
| 651100 | SERVICIOS DE LA BANCA CENTRAL |
| 651110 | SERVICIOS DE SEGUROS DE SALUD |
| 651120 | SERVICIOS DE SEGUROS DE VIDA |
| 651130 | SERVICIOS DE SEGUROS PERSONALES EXCEPTO  LOS DE SALUD Y DE VIDA |
| 651210 | SERVICIOS DE ASEGURADORAS DE RIESGO DE TRABAJO (ART) |
| 651220 | SERVICIOS DE SEGUROS PATRIMONIALES EXCEPTO LOS DE LAS ASEGURADORAS DE RIESGO DE TRABAJO (ART) |
| 651310 | OBRAS SOCIALES |
| 651320 | SERVICIOS DE CAJAS DE PREVISIÓN SOCIAL PERTENECIENTES A ASOCIACIONES PROFESIONALES |
| 652000 | REASEGUROS |
| 652110 | SERVICIOS DE LA BANCA MAYORISTA |
| 652120 | SERVICIOS DE LA BANCA DE INVERSION |
| 652130 | SERVICIOS DE LA BANCA MINORISTA |
| 652201 | SERVICIOS DE INTERMEDIACION FINANCIERA REALIZADA POR LAS COMPAÑIAS FINANCIERAS |
| 652202 | SERVICIOS DE INTERMEDIACION FINANCIERA REALIZADA POR SOC.DE AHORRO Y PRESTAMO PARA LA VIVIENDA Y OTROS INMUEBLES |
| 652203 | SERVICIOS DE INTERMEDIACION FINANCIERA REALIZADA POR CAJAS DE CREDITO |
| 653000 | ADMINISTRACIÓN DE FONDOS DE PENSIONES, EXCEPTO LA SEGURIDAD SOCIAL OBLIGATORIA |
| 659810 | ACTIVIDADES DE CREDITO PARA FINANCIAR OTRAS ACTIVIDADES ECONOMICAS |
| 659890 | SERVICIOS DE CREDITO N.C.P. |
| 659910 | SERVICIOS DE AGENTES DE MERCADO ABIERTO PUROS |
| 659920 | SERVICIOS DE ENTIDADES DE TARJETA DE COMPRA Y/O CREDITO |
| 659990 | SERVICIOS DE FINANCIACION Y ACTIVIDADES FINANCIERAS N.C.P. |
| 661110 | SERVICIOS DE SEGUROS DE SALUD |
| 661111 | SERVICIOS DE MERCADOS Y CAJAS DE VALORES |
| 661120 | SERVICIOS DE SEGUROS DE VIDA |
| 661121 | SERVICIOS DE MERCADOS A TÉRMINO |
| 661130 | SERVICIOS DE SEGUROS A LAS PERSONAS EXCEPTO LOS DE SALUD Y DE VIDA |
| 661131 | SERVICIOS DE BOLSAS DE COMERCIO |
| 661210 | SERVICIOS DE ASEGURADORAS DE RIESGO DE TRABAJO |
| 661220 | SERVICIOS DE SEGUROS PATRIMONIALES EXCEPTO LOS DE LAS ASEGURADORAS DE RIESGO DE TRABAJO |
| 661300 | REASEGUROS |
| 661910 | SERVICIOS BURSÁTILES DE MEDIACIÓN O POR CUENTA DE TERCEROS |
| 661920 | SERVICIOS DE CASAS Y AGENCIAS DE CAMBIO |
| 661930 | SERVICIOS DE SOCIEDADES CALIFICADORAS DE RIESGOS FINANCIEROS |
| 661991 | SERVICIOS DE ENVIO Y RECEPCIÓN DE FONDOS DESDE Y HACIA EL EXTERIOR |
| 661992 | SERVICIOS DE ADMINISTRADORAS DE VALES Y TICKETS |
| 661999 | SERVICIOS AUXILIARES A LA INTERMEDIACIÓN FINANCIERA N.C.P. |
| 662000 | ADMINISTRACION DE FONDOS DE JUBILACIONES Y PENSIONES |
| 662010 | SERVICIOS DE EVALUACIÓN DE RIESGOS Y DAÑOS |
| 662020 | SERVICIOS DE PRODUCTORES  Y ASESORES DE SEGUROS |
| 662090 | SERVICIOS AUXILIARES A LOS SERVICIOS DE SEGUROS N.C.P. |
| 663000 | SERVICIOS DE GESTIÓN DE FONDOS A CAMBIO DE UNA RETRIBUCIÓN O POR CONTRATA |
| 671110 | SERVICIOS DE MERCADOS Y CAJAS DE VALORES |
| 671120 | SERVICIOS DE MERCADOS A TERMINO |
| 671130 | SERVICIOS DE BOLSAS DE COMERCIO |
| 671200 | SERVICIOS BURSATILES DE MEDIACION O POR CUENTA DE TERCEROS |
| 671910 | SERVICIOS DE CASAS Y AGENCIAS DE CAMBIO |
| 671920 | SERVICIOS DE SOC.CALIFICADORAS DE RIESGOS |
| 671990 | SERVICIOS AUXILIARES A LA INTERMEDIACION FINANCIERA N.C.P.,EXCEPTO A LOS SERVICIOS DE SEGUROS Y DE ADMINISTRACION DE FONDOS DE JUBILACIONES Y PENSIONES |
| 672110 | SERVICIOS DE PRODUCTORES Y ASESORES DE SEGUROS |
| 672190 | SERVICIOS AUXILIARES A LOS SERVICIOS DE SEGUROS N.C.P. |
| 672200 | SERVICIOS AUXILIARES A LA ADMINISTRACION DE FONDOS DE JUBILACIONES Y PENSIONES |
| 681010 | SERVICIOS DE ALQUILER Y EXPLOTACIÓN DE INMUEBLES PARA FIESTAS, CONVENCIONES Y OTROS EVENTOS SIMILARES |
| 681020 | SERVICIOS DE ALQUILER  DE CONSULTORIOS MÉDICOS |
| 681098 | SERVICIOS INMOBILIARIOS REALIZADOS POR CUENTA PROPIA, CON BIENES URBANOS PROPIOS O ARRENDADOS N.C.P. |
| 681099 | SERVICIOS INMOBILIARIOS REALIZADOS POR CUENTA PROPIA, CON BIENES RURALES PROPIOS O ARRENDADOS N.C.P. |
| 682010 | SERVICIOS DE ADMINISTRACIÓN DE CONSORCIOS DE EDIFICIOS |
| 682091 | SERVICIOS PRESTADOS POR INMOBILIARIAS |
| 682099 | SERVICIOS INMOBILIARIOS REALIZADOS A CAMBIO DE UNA RETRIBUCIÓN O POR CONTRATA N.C.P. |
| 691001 | SERVICIOS JURÍDICOS |
| 691002 | SERVICIOS  NOTARIALES |
| 692000 | SERVICIOS DE CONTABILIDAD, AUDITORÍA Y ASESORÍA FISCAL |
| 701010 | SERVICIOS DE ALQUILER Y EXPLOTACION DE INMUEBLES PARA FIESTAS,CONVENCIONES Y OTROS EVENTOS SIMILARES |
| 701090 | SERVICIOS INMOBILIARIOS REALIZADOS POR CUENTA PROPIA,CON BIENES PROPIOS O ARRENDADOS N.C.P. |
| 702000 | SERVICIOS INMOBILIARIOS REALIZADOS A CAMBIO DE UNA RETRIBUCION O POR CONTRATA |
| 702010 | SERVICIOS DE GERENCIAMIENTO DE EMPRESAS E INSTITUCIONES DE SALUD, SERVICIOS DE AUDITORIA Y MEDICINA LEGAL, SERVICIO DE ASESORAMIENTO FARMACÉUTICO |
| 702091 | SERVICIOS DE ASESORAMIENTO, DIRECCIÓN Y GESTIÓN EMPRESARIAL REALIZADOS POR INTEGRANTES DE LOS ÓRGANOS DE ADMINISTRACIÓN Y/O FISCALIZACIÓN EN SOCIEDADES ANÓNIMAS |
| 702092 | SERVICIOS DE ASESORAMIENTO, DIRECCIÓN Y GESTIÓN EMPRESARIAL REALIZADOS POR INTEGRANTES DE CUERPOS DE DIRECCIÓN EN SOCIEDADES EXCEPTO LAS ANÓNIMAS |
| 702099 | SERVICIOS DE ASESORAMIENTO, DIRECCIÓN Y GESTIÓN EMPRESARIAL N.C.P. |
| 711001 | SERVICIOS RELACIONADOS CON LA CONSTRUCCIÓN. |
| 711002 | SERVICIOS GEOLÓGICOS Y DE PROSPECCIÓN |
| 711003 | SERVICIOS RELACIONADOS CON LA ELECTRÓNICA Y LAS COMUNICACIONES |
| 711009 | SERVICIOS DE ARQUITECTURA E INGENIERÍA Y SERVICIOS CONEXOS DE ASESORAMIENTO TÉCNICO N.C.P. |
| 711100 | ALQUILER DE EQUIPO DE TRANSPORTE PARA VIA TERRESTRE,SIN OPERARIOS NI TRIPULACION |
| 711128 | TRANSP FERROVIARIO |
| 711200 | ALQUILER DE EQUIPO DE TRANSPORTE PARA VIA ACUATICA,SIN OPERARIOS NI TRIPULACION |
| 711217 | TRANSP URBANO Y SUBURBANO |
| 711225 | TRANSP PASAJER A LARGA DISTANC |
| 711300 | ALQUILER DE EQUIPO DE TRANSPORTE PARA VIA AEREA,SIN OPERARIOS NI TRIPULACION |
| 711314 | TRANSP EN TAXIS Y REMISES |
| 711322 | TRANSP DE PASAJEROS NO CLASIF |
| 711411 | TRANS CARG COR MED Y LARG DIST |
| 711438 | SERVICIOS DE MUDANZA |
| 711446 | TRANSP VALORES ENCOMIENDAS |
| 711519 | TRANSP POR OLEOD Y GASODUCTOS |
| 711616 | SERVICIO PLAYA ESTACIONAMIENTO |
| 711624 | SERVICIO GARAGES |
| 711632 | SERVICIO LAVADO DE AUTOMOTORES |
| 711640 | SERVICIO ESTACIONES D/SERVICIO |
| 711691 | SERVIC RELAC C/TRANSP N/CLASIF |
| 712000 | ENSAYOS Y ANÁLISIS TÉCNICOS |
| 712100 | ALQUILER DE MAQUINARIA Y EQUIPO AGROPECUARIO,SIN OPERARIOS |
| 712116 | TRANS OCEANIC D/CARGA Y PASAJE |
| 712200 | ALQUILER DE MAQUINARIA Y EQUIPO DE CONSTRUCCION E INGENIERIA CIVIL,SIN OPERARIOS |
| 712213 | TRANSP P/VIAS D/NAVEG INTERIOR |
| 712300 | ALQUILER DE MAQUINARIA Y EQUIPO DE OFICINA,INCLUSO COMPUTADORAS |
| 712310 | SERVICIO RELAC C/TRANSP P/AGUA |
| 712329 | SERVICIO GUARDERIAS DE LANCHAS |
| 712901 | ALQUILER DE MAQUINARIA Y EQUIPO PARA LA INDUSTRIA MANUFACTURERA,SIN PERSONAL |
| 712902 | ALQUILER DE MAQUINARIA Y EQUIPO MINERO Y PETROLERO,SIN PERSONAL |
| 712909 | ALQUILER DE MAQUINARIA Y EQUIPO N.C.P.,SIN PERSONAL |
| 713001 | ALQUILER DE ROPA |
| 713009 | ALQUILER DE EFECTOS PERSONALES Y ENSERES DOMESTICOS N.C.P. |
| 713112 | TRANSP AEREO D/PASAJE Y CARGAS |
| 713228 | SERVIC RELAC C/EL TRANSP AEREO |
| 719110 | SERVICIO CONEX C/EL TRANSPORTE |
| 719218 | DEPOSITOS INCL CAMARA REFRIGER |
| 720011 | COMUNIC CORREO TELEGRA Y TELEX |
| 720038 | COMUN P/RADIO NO RADIODIFUSION |
| 720046 | COMUNIC TELEFONICAS |
| 720097 | COMUNIC NO CLASIF |
| 721000 | SERVICIOS DE CONSULTORES EN EQUIPO DE INFORMATICA |
| 721010 | INVESTIGACIÓN  Y DESARROLLO EXPERIMENTAL EN EL CAMPO DE LA INGENIERÍA Y LA TECNOLOGÍA |
| 721020 | INVESTIGACIÓN  Y DESARROLLO EXPERIMENTAL EN EL CAMPO DE LAS CIENCIAS MÉDICAS |
| 721030 | INVESTIGACIÓN  Y DESARROLLO EXPERIMENTAL EN EL CAMPO DE LAS CIENCIAS AGROPECUARIAS |
| 721090 | INVESTIGACIÓN Y DESARROLLO EXPERIMENTAL EN EL CAMPO DE LAS CIENCIAS EXACTAS Y NATURALES N.C.P. |
| 722000 | SERVICIOS DE CONSULTORES EN INFORMATICA Y SUMINISTROS DE PROGRAMAS DE INFORMATICA |
| 722010 | INVESTIGACIÓN  Y DESARROLLO EXPERIMENTAL EN EL CAMPO DE LAS CIENCIAS SOCIALES |
| 722020 | INVESTIGACIÓN  Y DESARROLLO EXPERIMENTAL EN EL CAMPO DE LAS CIENCIAS HUMANAS |
| 723000 | PROCESAMIENTO DE DATOS |
| 724000 | SERVICIOS RELACIONADOS CON BASES DE DATOS |
| 725000 | MANTENIMIENTO Y REPARACION DE MAQUINARIA DE OFICINA,CONTABILIDAD E INFORMATICA |
| 729000 | ACTIVIDADES DE INFORMATICA N.C.P. |
| 731001 | SERVICIOS DE COMERCIALIZACIÓN DE TIEMPO Y ESPACIO PUBLICITARIO |
| 731009 | SERVICIOS DE PUBLICIDAD N.C.P. |
| 731100 | INVESTIGACION Y DESARROLLO EXPERIMENTAL EN EL CAMPO DE LA INGENIERIA Y LA TECNOLOGIA |
| 731200 | INVESTIGACION Y DESARROLLO EXPERIMENTAL EN EL CAMPO DE LAS CIENCIAS MEDICAS |
| 731300 | INVESTIGACION Y DESARROLLO EXPERIMENTAL EN EL CAMPO DE LAS CIENCIAS AGROPECUARIAS |
| 731900 | INVESTIGACION Y DESARROLLO EXPERIMENTAL EN EL CAMPO DE LAS CIENCIAS EXACTAS Y NATURALES N.C.P. |
| 732000 | ESTUDIO DE MERCADO, REALIZACIÓN DE ENCUESTAS DE OPINIÓN PÚBLICA |
| 732100 | INVESTIGACION Y DESARROLLO EXPERIMENTAL EN EL CAMPO DE LAS CIENCIAS SOCIALES |
| 732200 | INVESTIGACION Y DESARROLLO EXPERIMENTAL EN EL CAMPO DE LAS CIENCIAS HUMANAS |
| 741000 | SERVICIOS DE DISEÑO ESPECIALIZADO |
| 741101 | SERVICIOS JURIDICOS |
| 741102 | SERVICIOS NOTARIALES |
| 741200 | SERVICIOS DE CONTABILIDAD Y TENEDURIA DE LIBROS,AUDITORIA Y ASESORIA FISCAL |
| 741300 | ESTUDIO DE MERCADO,REALIZACION DE ENCUESTAS DE OPINION PUBLICA |
| 741401 | SERVICIOS DE ASESORAMIENTO,DIRECCION Y GESTION EMPRESARIAL REALIZADOS POR INTEGRANTES DE LOS ORGANOS DE ADMINISTRACION Y/O FISCALIZACION EN SOC.ANONIMAS |
| 741402 | SERVICIOS DE ASESORAMIENTO,DIRECCION Y GESTION EMPRESARIAL REALIZADOS POR INTEGRANTES DE CUERPOS DE DIRECCION EN SOC.EXCEPTO LAS ANONIMAS |
| 741409 | SERVICIOS DE ASESORAMIENTO,DIRECCION Y GESTION EMPRESARIAL N.C.P. |
| 742000 | SERVICIOS DE FOTOGRAFÍA |
| 742101 | SERVICIOS RELACIONADOS CON LA CONSTRUCCION. |
| 742102 | SERVICIOS GEOLOGICOS Y DE PROSPECCION |
| 742103 | SERVICIOS RELACIONADOS CON LA ELECTRONICA Y LAS COMUNICACIONES |
| 742109 | SERVICIOS DE ARQUITECTURA E INGENIERIA Y SERVICIOS CONEXOS DE ASESORAMIENTO TECNICO N.C.P. |
| 742200 | ENSAYOS Y ANALISIS TECNICOS |
| 743000 | SERVICIOS DE PUBLICIDAD |
| 749001 | SERVICIOS DE TRADUCCIÓN E INTERPRETACIÓN |
| 749002 | SERVICIOS DE REPRESENTACIÓN E INTERMEDIACIÓN DE ARTISTAS Y MODELOS |
| 749003 | SERVICIOS DE REPRESENTACIÓN E INTERMEDIACIÓN DE DEPORTISTAS PROFESIONALES |
| 749009 | ACTIVIDADES PROFESIONALES, CIENTÍFICAS Y TÉCNICAS N.C.P. |
| 749100 | OBTENCION Y DOTACION DE PERSONAL |
| 749210 | SERVICIOS DE TRANSPORTE DE CAUDALES Y OBJETOS DE VALOR |
| 749290 | SERVICIOS DE INVESTIGACION Y SEGURIDAD N.C.P. |
| 749300 | SERVICIOS DE LIMPIEZA DE EDIFICIOS |
| 749400 | SERVICIOS DE FOTOGRAFIA |
| 749500 | SERVICIOS DE ENVASE Y EMPAQUE |
| 749600 | SERVICIOS DE IMPRESION HELIOGRAFICA,FOTOCOPIA Y OTRAS FORMAS DE REPRODUCCIONES |
| 749900 | SERVICIOS EMPRESARIALES N.C.P. |
| 750000 | SERVICIOS VETERINARIOS |
| 751100 | SERVICIOS GENERALES DE LA ADMINISTRACION PUBLICA |
| 751200 | SERVICIOS PARA LA REGULACION DE LAS ACTIVIDADES SANITARIAS,EDUCATIVAS,CULTURALES,Y RESTANTES SERVICIOS SOCIALES,EXCEPTO SEGURIDAD SOCIAL OBLIGATORIA |
| 751300 | SERVICIOS PARA LA REGULACION DE LA ACTIVIDAD ECONOMICA |
| 751900 | SERVICIOS AUXILIARES PARA LOS SERVICIOS GENERALES DE LA ADMINISTRACION PUBLICA N.C.P. |
| 752100 | SERVICIOS DE ASUNTOS EXTERIORES |
| 752200 | SERVICIOS DE DEFENSA |
| 752300 | SERVICIOS DE JUSTICIA |
| 752400 | SERVICIOS PARA EL ORDEN PUBLICO Y LA SEGURIDAD |
| 752500 | SERVICIOS DE PROTECCION CIVIL |
| 753000 | SERVICIOS DE LA SEGURIDAD SOCIAL OBLIGATORIA |
| 771110 | ALQUILER DE AUTOMÓVILES SIN CONDUCTOR |
| 771190 | ALQUILER DE VEHÍCULOS AUTOMOTORES N.C.P., SIN CONDUCTOR NI OPERARIOS |
| 771210 | ALQUILER DE EQUIPO DE TRANSPORTE PARA VÍA ACUÁTICA, SIN OPERARIOS NI TRIPULACIÓN |
| 771220 | ALQUILER DE EQUIPO DE TRANSPORTE PARA VÍA AÉREA, SIN OPERARIOS NI TRIPULACIÓN |
| 771290 | ALQUILER DE EQUIPO DE TRANSPORTE N.C.P. SIN CONDUCTOR NI OPERARIOS |
| 772010 | ALQUILER DE VIDEOS Y VIDEO JUEGOS |
| 772091 | ALQUILER DE PRENDAS DE VESTIR |
| 772099 | ALQUILER DE EFECTOS PERSONALES Y ENSERES DOMÉSTICOS N.C.P. |
| 773010 | ALQUILER DE MAQUINARIA Y EQUIPO AGROPECUARIO Y FORESTAL, SIN OPERARIOS |
| 773020 | ALQUILER DE MAQUINARIA Y EQUIPO PARA LA MINERÍA, SIN OPERARIOS |
| 773030 | ALQUILER DE MAQUINARIA Y EQUIPO DE CONSTRUCCIÓN E INGENIERÍA CIVIL, SIN OPERARIOS |
| 773040 | ALQUILER DE MAQUINARIA Y EQUIPO DE OFICINA, INCLUSO COMPUTADORAS |
| 773090 | ALQUILER DE MAQUINARIA Y EQUIPO N.C.P., SIN PERSONAL |
| 774000 | ARRENDAMIENTO Y GESTIÓN DE BIENES INTANGIBLES NO FINANCIEROS |
| 780000 | OBTENCIÓN Y DOTACIÓN DE PERSONAL |
| 791100 | SERVICIOS MINORISTAS DE AGENCIAS DE VIAJES |
| 791200 | SERVICIOS MAYORISTAS DE AGENCIAS DE VIAJES |
| 791901 | SERVICIOS DE TURISMO AVENTURA |
| 791909 | SERVICIOS COMPLEMENTARIOS DE APOYO TURÍSTICO N.C.P. |
| 801000 | ENSEÑANZA INICIAL Y PRIMARIA |
| 801010 | SERVICIOS DE TRANSPORTE DE CAUDALES Y OBJETOS DE VALOR |
| 801020 | SERVICIOS DE SISTEMAS DE SEGURIDAD |
| 801090 | SERVICIOS DE SEGURIDAD E INVESTIGACIÓN N.C.P. |
| 802100 | ENSEÑANZA SECUNDARIA DE FORMACION GENERAL |
| 802200 | ENSEÑANZA SECUNDARIA DE FORMACION TECNICA Y PROFESIONAL |
| 803100 | ENSEÑANZA TERCIARIA |
| 803200 | ENSEÑANZA UNIVERSITARIA EXCEPTO FORMACION DE POSGRADO |
| 803300 | FORMACION DE POSGRADO |
| 809000 | ENSEÑANZA PARA ADULTOS Y SERVICIOS DE ENSEÑANZA N.C.P. |
| 810118 | OPERAC INTERM BANCOS |
| 810215 | OPERAC INTERM COMPAÑIAS FINANC |
| 810223 | OPERAC INTERM FINAN SOC AHORRO |
| 810231 | OPERAC INTERM FINAN CAJA CREDI |
| 810290 | OPERAC INTERM FINANC NO CLASIF |
| 810312 | SERVICIO INTERMED C/MONEDA EXT |
| 810320 | SERVI BURSATILES EXTRABURSATIL |
| 810339 | SERVICIO FINANCI TARJETAS CRED |
| 810428 | OPERAC FINANC REC MONET PROPIO |
| 810436 | OPER C/DIVISAS ACCION RENTISTA |
| 811000 | SERVICIO COMBINADO DE APOYO A EDIFICIOS |
| 812010 | SERVICIOS DE LIMPIEZA GENERAL DE EDIFICIOS |
| 812020 | SERVICIOS DE DESINFECCIÓN Y EXTERMINIO DE PLAGAS EN EL ÁMBITO URBANO |
| 812090 | SERVICIOS DE LIMPIEZA N.C.P. |
| 813000 | SERVICIOS DE JARDINERÍA Y MANTENIMIENTO DE ESPACIOS VERDES |
| 820016 | SERVIC PREST P/CIAS DE SEGUROS |
| 820024 | SERVIC PREST P/CIAS ADMIN JUBI |
| 820091 | SERVIC RELAC C/SEGUR NO CLASIF |
| 821100 | SERVICIOS COMBINADOS DE GESTIÓN ADMINISTRATIVA DE OFICINAS |
| 821900 | SERVICIOS DE FOTOCOPIADO, PREPARACIÓN DE DOCUMENTOS Y OTROS SERVICIOS DE APOYO DE OFICINA |
| 822000 | SERVICIOS DE CALL CENTER |
| 823000 | SERVICIOS DE ORGANIZACIÓN DE CONVENCIONES Y EXPOSICIONES COMERCIALES, EXCEPTO CULTURALES Y DEPORTIVOS |
| 829100 | SERVICIOS DE AGENCIAS DE COBRO Y CALIFICACIÓN CREDITICIA |
| 829200 | SERVICIOS DE ENVASE Y EMPAQUE |
| 829900 | SERVICIOS EMPRESARIALES N.C.P. |
| 831018 | OPERAC CON INMUEBLES |
| 831026 | ALQUILER INMUEBLES PROPIOS |
| 832111 | SERVICIO JURIDICOS ABOGADOS |
| 832138 | SERVICIO NOTARIALES ESCRIBANOS |
| 832219 | SERVICIO CONTABILIDA AUDITORIA |
| 832316 | SERVICIO ELABORA DATO COMPUTAC |
| 832413 | SERVICIO RELAC C/ CONSTRUCCION |
| 832421 | SERVIC GEOLOGIOC Y PROSPECCION |
| 832448 | SERVIC ESTUD TECN ARQ N/CLASIF |
| 832456 | SERVIC ELECTRONICA Y COMUNICAC |
| 832464 | SERVICIO INGENIERIA NO CLASIF |
| 832510 | SERVICIO PUBLICIDAD |
| 832529 | SERVICIO INVESTIGACION MERCADO |
| 832928 | SERVIC CONSULT ECONOM Y FINANC |
| 832936 | SERVICIO DESPACHANTES D/ADUANA |
| 832944 | SERVI GESTOR E INFORM S/CREDIT |
| 832952 | SERVICIO INVESTIG Y VIGILANCIA |
| 832960 | SERVI INFORM AGENCIAS NOTICIAS |
| 832979 | SERVI TECNIC Y PROFES N/CLASIF |
| 833010 | ALQUILER MAQU P/MANUF CONSTRUC |
| 833029 | ALQUILER MAQ Y EQUIPO AGRICOLA |
| 833037 | ALQUILER MAQ/EQUI MINER PETROL |
| 833045 | ALQUILER EQUIP COMPU Y OFICINA |
| 833053 | ALQUILER DE MAQUINAR NO CLASIF |
| 841100 | SERVICIOS GENERALES DE LA ADMINISTRACIÓN PÚBLICA |
| 841200 | SERVICIOS PARA LA REGULACIÓN DE LAS ACTIVIDADES SANITARIAS, EDUCATIVAS, CULTURALES, Y RESTANTES SERVICIOS SOCIALES, EXCEPTO SEGURIDAD SOCIAL OBLIGATORIA |
| 841300 | SERVICIOS PARA LA REGULACIÓN DE LA ACTIVIDAD ECONÓMICA |
| 841900 | SERVICIOS AUXILIARES PARA LOS SERVICIOS GENERALES DE LA ADMINISTRACIÓN PÚBLICA |
| 842100 | SERVICIOS DE ASUNTOS EXTERIORES |
| 842200 | SERVICIOS DE DEFENSA |
| 842300 | SERVICIOS PARA EL ORDEN PÚBLICO Y LA SEGURIDAD |
| 842400 | SERVICIOS DE JUSTICIA |
| 842500 | SERVICIOS DE PROTECCIÓN CIVIL |
| 843000 | SERVICIOS DE LA SEGURIDAD SOCIAL OBLIGATORIA, EXCEPTO OBRAS SOCIALES |
| 851010 | GUARDERÍAS Y JARDINES MATERNALES |
| 851020 | ENSEÑANZA INICIAL, JARDÍN DE INFANTES Y PRIMARIA |
| 851110 | SERVICIOS DE INTERNACION |
| 851120 | SERVICIOS DE HOSPITAL DE DIA |
| 851190 | SERVICIOS HOSPITALARIOS N.C.P. |
| 851210 | SERVICIOS DE ATENCION AMBULATORIA |
| 851220 | SERVICIOS DE ATENCION DOMICILIARIA PROGRAMADA |
| 851300 | SERVICIOS ODONTOLOGICOS |
| 851400 | SERVICIOS DE DIAGNOSTICO |
| 851500 | SERVICIOS DE TRATAMIENTO |
| 851600 | SERVICIOS DE EMERGENCIAS Y TRASLADOS |
| 851900 | SERVICIOS RELACIONADOS CON LA SALUD HUMANA N.C.P. |
| 852000 | SERVICIOS VETERINARIOS |
| 852100 | ENSEÑANZA SECUNDARIA DE FORMACIÓN GENERAL |
| 852200 | ENSEÑANZA SECUNDARIA DE FORMACIÓN TÉCNICA Y PROFESIONAL |
| 853100 | ENSEÑANZA  TERCIARIA |
| 853110 | SERVICIOS DE ATENCION A ANCIANOS CON ALOJAMIENTO |
| 853120 | SERVICIOS DE ATENCION A PERSONAS MINUSVALIDAS CON ALOJAMIENTO |
| 853130 | SERVICIOS DE ATENCION A MENORES CON ALOJAMIENTO |
| 853140 | SERVICIOS DE ATENCION A MUJERES CON ALOJAMIENTO |
| 853190 | SERVICIOS SOCIALES CON ALOJAMIENTO N.C.P. |
| 853200 | SERVICIOS SOCIALES SIN ALOJAMIENTO |
| 853201 | ENSEÑANZA UNIVERSITARIA EXCEPTO FORMACIÓN DE POSGRADO |
| 853300 | FORMACIÓN DE POSGRADO |
| 854910 | ENSEÑANZA DE IDIOMAS |
| 854920 | ENSEÑANZA DE CURSOS RELACIONADOS CON INFORMÁTICA |
| 854930 | ENSEÑANZA PARA ADULTOS, EXCEPTO DISCAPACITADOS |
| 854940 | ENSEÑANZA ESPECIAL Y PARA DISCAPACITADOS |
| 854950 | ENSEÑANZA DE GIMNASIA, DEPORTES Y ACTIVIDADES FÍSICAS |
| 854960 | ENSEÑANZA ARTÍSTICA |
| 854990 | SERVICIOS DE ENSEÑANZA N.C.P. |
| 855000 | SERVICIOS DE APOYO A LA EDUCACIÓN |
| 861010 | SERVICIOS DE INTERNACIÓN EXCEPTO INSTITUCIONES RELACIONADAS CON LA SALUD MENTAL |
| 861020 | SERVICIOS DE INTERNACIÓN EN INSTITUCIONES RELACIONADAS CON LA SALUD MENTAL |
| 862110 | SERVICIOS DE  CONSULTA MÉDICA |
| 862120 | SERVICIOS DE PROVEEDORES DE ATENCIÓN MÉDICA DOMICILIARIA |
| 862130 | SERVICIOS DE ATENCIÓN MÉDICA EN DISPENSARIOS, SALITAS, VACUNATORIOS Y OTROS LOCALES DE ATENCIÓN PRIMARIA DE LA SALUD |
| 862200 | SERVICIOS ODONTOLÓGICOS |
| 863110 | SERVICIOS DE PRÁCTICAS DE DIAGNÓSTICO EN LABORATORIOS |
| 863120 | SERVICIOS DE PRÁCTICAS DE DIAGNÓSTICO POR IMÁGENES |
| 863190 | SERVICIOS DE PRÁCTICAS DE DIAGNÓSTICO N.C.P. |
| 863200 | SERVICIOS DE TRATAMIENTO |
| 863300 | SERVICIO MÉDICO INTEGRADO DE CONSULTA, DIAGNÓSTICO Y TRATAMIENTO |
| 864000 | SERVICIOS DE EMERGENCIAS Y TRASLADOS |
| 869010 | SERVICIOS DE REHABILITACIÓN FÍSICA |
| 869090 | SERVICIOS RELACIONADOS CON LA SALUD HUMANA N.C.P. |
| 870100 | SERVICIOS DE ATENCIÓN A PERSONAS CON PROBLEMAS DE SALUD MENTAL O DE ADICCIONES, CON ALOJAMIENTO |
| 870210 | SERVICIOS DE ATENCIÓN A ANCIANOS CON ALOJAMIENTO |
| 870220 | SERVICIOS DE ATENCIÓN A PERSONAS MINUSVÁLIDAS CON ALOJAMIENTO |
| 870910 | SERVICIOS DE ATENCIÓN A NIÑOS Y ADOLESCENTES CARENCIADOS CON ALOJAMIENTO |
| 870920 | SERVICIOS DE ATENCIÓN A MUJERES CON ALOJAMIENTO |
| 870990 | SERVICIOS SOCIALES CON ALOJAMIENTO N.C.P. |
| 880000 | SERVICIOS SOCIALES SIN ALOJAMIENTO |
| 900010 | RECOLECCION,REDUCCION Y ELIMINACION DE DESPERDICIOS |
| 900011 | PRODUCCIÓN DE ESPECTÁCULOS TEATRALES Y MUSICALES |
| 900020 | SERVICIOS DE DEPURACION DE AGUAS RESIDUALES,ALCANTARILLADO Y CLOACAS |
| 900021 | COMPOSICIÓN Y REPRESENTACIÓN DE OBRAS TEATRALES, MUSICALES Y ARTÍSTICAS |
| 900030 | SERVICIOS CONEXOS A LA PRODUCCIÓN DE ESPECTÁCULOS TEATRALES Y MUSICALES |
| 900040 | SERVICIOS DE AGENCIAS DE VENTAS DE ENTRADAS |
| 900090 | SERVICIOS DE SANEAMIENTO PUBLICO N.C.P. |
| 900091 | SERVICIOS DE ESPECTÁCULOS ARTÍSTICOS N.C.P. |
| 910015 | ADMINISTRACION PUBLI Y DEFENSA |
| 910100 | SERVICIOS DE BIBLIOTECAS Y ARCHIVOS |
| 910200 | SERVICIOS DE MUSEOS Y PRESERVACIÓN DE LUGARES Y EDIFICIOS HISTÓRICOS |
| 910300 | SERVICIOS DE JARDINES BOTÁNICOS, ZOOLÓGICOS Y DE PARQUES NACIONALES |
| 910900 | SERVICIOS CULTURALES N.C.P. |
| 911100 | SERVICIOS DE FEDERACIONES,ASOCIACIONES,CAMARAS,GREMIOS Y ORGANIZACIONES SIMILARES |
| 911200 | SERVICIOS DE ASOCIACIONES DE ESPECIALISTAS EN DISCIPLINAS CIENTIFICAS,PRACTICAS PROFESIONALES Y ESFERAS TECNICAS |
| 912000 | SERVICIOS DE SINDICATOS |
| 919100 | SERVICIOS DE ORGANIZACIONES RELIGIOSAS |
| 919200 | SERVICIOS DE ORGANIZACIONES POLITICAS |
| 919900 | SERVICIOS DE ASOCIACIONES N.C.P. |
| 920001 | SERVICIOS DE RECEPCIÓN DE APUESTAS DE QUINIELA, LOTERÍA Y SIMILARES |
| 920009 | SERVICIOS RELACIONADOS CON JUEGOS DE AZAR Y APUESTAS N.C.P. |
| 920010 | SERVICIO SANEAM RECOL RESIDUOS |
| 921110 | PRODUCCION DE FILMES Y VIDEOCINTAS |
| 921120 | DISTRIBUCION DE FILMES Y VIDEOCINTAS |
| 921200 | EXHIBICION DE FILMES Y VIDEOCINTAS |
| 921301 | SERVICIOS DE RADIO |
| 921302 | PRODUCCION Y DISTRIBUCION POR TELEVISION |
| 921410 | PRODUCCION DE ESPECTACULOS TEATRALES Y MUSICALES |
| 921420 | COMPOSICION Y REPRESENTACION DE OBRAS TEATRALES,MUSICALES Y ARTISTICAS |
| 921430 | SERVICIOS CONEXOS A LA PRODUCCION DE ESPECTACULOS TEATRALES Y MUSICALES |
| 921910 | SERVICIOS DE SALONES DE BAILE,DISCOTECAS Y SIMILARES |
| 921990 | SERVICIOS DE ESPECTACULOS ARTISTICOS Y DE DIVERSION N.C.P. |
| 922000 | SERVICIOS DE AGENCIAS DE NOTICIAS Y SERVICIOS DE INFORMACION |
| 923100 | SERVICIOS DE BIBLIOTECAS Y ARCHIVOS |
| 923200 | SERVICIOS DE MUSEOS Y PRESERVACION DE LUGARES Y EDIFICIOS HISTORICOS |
| 923300 | SERVICIOS DE JARDINES BOTANICOS,ZOOLOGICOS Y DE PARQUES NACIONALES |
| 924110 | SERVICIOS DE ORGANIZACION,DIRECCION Y GESTION DE PRACTICAS DEPORTIVAS Y EXPLOTACION DE LAS INSTALACIONES |
| 924120 | PROMOCION Y PRODUCCION DE ESPECTACULOS DEPORTIVOS |
| 924130 | SERVICIOS PRESTADOS POR PROFESIONALES Y TECNICOS,PARA LA REALIZACION DE PRACTICAS DEPORTIVAS |
| 924910 | SERVICIOS DE ESPARCIMIENTO RELACIONADOS CON JUEGOS DE AZAR Y APUESTAS |
| 924920 | SERVICIOS DE SALONES DE JUEGOS |
| 924990 | SERVICIOS DE ENTRETENIMIENTO N.C.P. |
| 930100 | LAVADO Y LIMPIEZA DE ART. DE TELA,CUERO Y/O DE PIEL,INCLUSO LA LIMPIEZA EN SECO |
| 930201 | SERVICIOS DE PELUQUERIA |
| 930202 | SERVICIOS DE TRATAMIENTO DE BELLEZA,EXCEPTO LOS DE PELUQUERIA |
| 930300 | POMPAS FUNEBRES Y SERVICIOS CONEXOS |
| 930910 | SERVICIOS PARA EL MANTENIMIENTO FISICO-CORPORAL |
| 930990 | SERVICIOS N.C.P. |
| 931010 | SERVICIOS DE ORGANIZACIÓN, DIRECCIÓN Y GESTIÓN DE PRÁCTICAS DEPORTIVAS EN CLUBES |
| 931012 | ENSEÑANZA PREPR PRIM SECUN SUP |
| 931020 | EXPLOTACIÓN DE INSTALACIONES DEPORTIVAS, EXCEPTO CLUBES |
| 931030 | PROMOCIÓN Y PRODUCCIÓN DE ESPECTÁCULOS DEPORTIVOS |
| 931041 | SERVICIOS PRESTADOS POR DEPORTISTAS Y ATLETAS PARA LA REALIZACIÓN DE PRÁCTICAS DEPORTIVAS |
| 931042 | SERVICIOS PRESTADOS POR PROFESIONALES Y TÉCNICOS PARA LA REALIZACIÓN DE PRÁCTICAS DEPORTIVAS |
| 931050 | SERVICIOS DE ACONDICIONAMIENTO FÍSICO |
| 931090 | SERVICIOS PARA LA PRÁCTICA DEPORTIVA N.C.P. |
| 932019 | INSTIT CENTRO INVESTIG/CIENTIF |
| 933112 | SERVICIO ASIST MEDIC/ODONTOLOG |
| 933120 | SERVI ASIST PRES P/MEDIC ODONT |
| 933139 | SERVI ANALISIS CLINI LABORATOR |
| 933147 | SERVICIO DE AMBULANCIAS |
| 933198 | SERVIC ASISTEN MEDICA N/CLASIF |
| 933228 | SERVICIO VETERINAR Y AGRONOMIA |
| 934011 | SERVI ASISTEN ASILO GUARDERIAS |
| 935018 | SERVIC PREST P/ASOC PROFESION |
| 939010 | SERVICIOS DE PARQUES DE DIVERSIONES Y PARQUES TEMÁTICOS |
| 939020 | SERVICIOS DE SALONES DE JUEGOS |
| 939030 | SERVICIOS DE SALONES DE BAILE, DISCOTECAS Y SIMILARES |
| 939090 | SERVICIOS DE ENTRETENIMIENTO N.C.P. |
| 939110 | SERVIC PREST P/ASOC RELIGIOSAS |
| 939919 | SERVI SOCIAL Y COMUN NO CLASIF |
| 941100 | SERVICIOS DE ORGANIZACIONES EMPRESARIALES Y DE EMPLEADORES |
| 941115 | PRODUC PELICULAS CINEMATO Y TV |
| 941123 | SERVI REVELADO COPIA PELICULAS |
| 941200 | SERVICIOS DE ORGANIZACIONES PROFESIONALES |
| 941212 | DISTR/ALQUIL PELICULAS CINEMAT |
| 941220 | DISTR Y ALQUIL PELICULAS VIDEO |
| 941239 | EXHIBICION DE PELICU CINEMATOG |
| 941328 | EMISION/PRODUCCION RADIO Y TV |
| 941417 | PRODUC/ESPECTAC TEAT Y MUSICAL |
| 941425 | PROD Y SERV D/GRABAC MUSICALES |
| 941433 | SERVICIO RELAC C/ ESPECTACULOS |
| 941514 | AUTORES COMPOSITORE Y ARTISTAS |
| 942000 | SERVICIOS DE SINDICATOS |
| 942014 | SERVICIO CULT BIBLIOTEC MUSEOS |
| 949019 | SERVICIO DIVERSION SALON BAILE |
| 949027 | SERVICIO PRACTICAS DEPORTIVAS |
| 949035 | SERVICIO JUEGOS DE SALON |
| 949043 | PRODUC ESPECTACULOS DEPORTIVOS |
| 949051 | DEPORTISTAS PROFESIONALES |
| 949094 | SERVI DIVERS Y ESPARC N/CLASIF |
| 949100 | SERVICIOS DE ORGANIZACIONES RELIGIOSAS |
| 949200 | SERVICIOS DE ORGANIZACIONES POLÍTICAS |
| 949910 | SERVICIOS DE MUTUALES, EXCEPTO MUTUALES DE SALUD Y FINANCIERAS |
| 949920 | SERVICIOS DE CONSORCIOS DE EDIFICIOS |
| 949930 | SERVICIOS DE COOPERATIVAS CUANDO REALIZAN VARIAS ACTIVIDADES |
| 949990 | SERVICIOS DE ASOCIACIONES N.C.P. |
| 950000 | SERVICIOS DE HOGARES PRIVADOS QUE CONTRATAN SERVICIO DOMESTICO |
| 951100 | REPARACIÓN Y MANTENIMIENTO DE EQUIPOS INFORMÁTICOS |
| 951110 | REPAR CALZADO DE CUERO |
| 951200 | REPARACIÓN Y MANTENIMIENTO DE EQUIPOS DE TELEFONÍA Y DE COMUNICACIÓN |
| 951218 | REPAR ARTIC ELECTR DE U/DOMEST |
| 951315 | REPAR AUTOMOTORES MOTOCICLETAS |
| 951412 | REPAR RELOJES Y JOYAS |
| 951919 | SERVICIO TAPICERIA |
| 951927 | SERVICIO REPARACION NO CLASIF |
| 952028 | SERVIC LAVANDERIA Y TINTORERIA |
| 952100 | REPARACIÓN DE ARTÍCULOS ELÉCTRICOS Y ELECTRÓNICOS DE USO DOMÉSTICO |
| 952200 | REPARACIÓN DE CALZADO Y ARTÍCULOS DE MARROQUINERÍA |
| 952300 | REPARACIÓN DE TAPIZADOS Y MUEBLES |
| 952910 | REFORMA Y REPARACIÓN DE CERRADURAS, DUPLICACIÓN DE LLAVES. CERRAJERÍAS |
| 952920 | REPARACIÓN DE RELOJES Y JOYAS. RELOJERÍAS |
| 952990 | REPARACIÓN DE EFECTOS PERSONALES Y ENSERES DOMÉSTICOS N.C.P. |
| 953016 | SERVICIO DOMESTICO AGENCIAS |
| 959111 | SERVICIO PELUQUERIA |
| 959138 | SERVICIO SALONES DE BELLEZA |
| 959219 | SERVIC FOTOGR LABOR FOTOGRAFIC |
| 959928 | SERVICIO POMPAS FUNEBRES |
| 959936 | SERVIC HIGIENE ESTET CORPORAL |
| 959944 | SERVICIOS PERSONALES NO CLASIF |
| 960101 | SERVICIOS DE LIMPIEZA DE PRENDAS PRESTADO POR TINTORERÍAS RÁPIDAS |
| 960102 | LAVADO Y LIMPIEZA DE ARTÍCULOS DE TELA, CUERO Y/O DE PIEL, INCLUSO LA LIMPIEZA EN SECO |
| 960201 | SERVICIOS DE PELUQUERÍA |
| 960202 | SERVICIOS DE TRATAMIENTO DE BELLEZA, EXCEPTO LOS DE PELUQUERÍA |
| 960300 | POMPAS FÚNEBRES Y SERVICIOS CONEXOS |
| 960910 | SERVICIOS DE CENTROS DE ESTÉTICA, SPA Y SIMILARES |
| 960990 | SERVICIOS PERSONALES N.C.P. |
| 970000 | SERVICIOS DE HOGARES PRIVADOS QUE CONTRATAN SERVICIO DOMÉSTICO |
| 990000 | SERVICIOS DE ORGANIZACIONES Y ORGANOS EXTRATERRITORIALES |
### Caracterizaciones
| **id** | **desc** |
|---|---|
| 1 | GRAN CONTRIBUYENTE |
| 5 | PAGO A CUENTA |
| 6 | IMPORTADOR ACEPTADO |
| 7 | IMPORTADOR DADO DE BAJA |
| 8 | IMPORTADOR RECHAZADO |
| 15 | IVA ANUAL AGROP. RG 3743-NO VIGENT- PRIMER EMPADRONAM. |
| 16 | IVA ANUAL AGROP. INACTIVO |
| 17 | IVA ANUAL AGROPECUARIO |
| 22 | PASIVO |
| 24 | ENTIDADES FINANCIERAS - INC A) |
| 37 | REGIONAL |
| 38 | QUIEBRA |
| 39 | CONCURSO PREVENTIVO |
| 40 | EMISORES DE OBLIGACIONES - INC B) |
| 41 | TOMADORES DE PRESTAMOS OTORGADOS - INC C) |
| 42 | APODERADO LEGAL DECRETO 1255/98 |
| 43 | DECRETO 1255/98 |
| 47 | HABILITADO COMPROBANTE A |
| 48 | HABILITADO COMPROBANTE M |
| 49 | ASOCIADO A COOPERATIVA DE TRABAJO |
| 50 | COOPERATIVA EFECTORA |
| 51 | POTENCIAL EFECTOR AGROPECUARIO |
| 52 | POTENCIAL MONOTRIBUTISTA SOCIAL EVENTUAL |
| 54 | POTENCIAL MONOTRIBUTISTA SOCIAL SERVICIOS |
| 55 | POTENCIAL MONOTRIBUTISTA SOCIAL VENTAS |
| 57 | POTENCIAL EFECTOR B CON 2 SOCIOS |
| 58 | POTENCIAL EFECTOR C CON 2 SOCIOS |
| 59 | POTENCIAL EFECTOR C CON 3 SOCIOS |
| 60 | POTENCIAL EFECTOR H CON 3 SOCIOS |
| 61 | NO RESPONDIO AL REQUERIMIENTO |
| 62 | PRODUCTORES DE SEGURO |
| 63 | REPRESENTANTE DE EXTERIOR |
| 64 | TERCEROS INTERVINIENTES |
| 65 | BOLSA DE CEREAL |
| 66 | DONATARIOS |
| 67 | CONSUMOS RELEVANTES |
| 68 | PARTICIPACIONES SOCIETARIAS |
| 69 | LEY 25994 |
| 70 | GANANCIAS EXENTO. ART 20 INC A) |
| 71 | CITI - VENTAS |
| 72 | CITI - COMPRAS |
| 73 | RANCHO - DISTRIBUIDORES |
| 74 | RANCHO - PRODUCTORES |
| 75 | RANCHO - ADQUIRENTES |
| 76 | LEY 24476 |
| 77 | QUIEBRA CON CONTINUIDAD |
| 78 | GMP-EXIMICION PAGO-PRIVAT.TOTAL |
| 79 | GMP-EXIMICION PAGO-PRIVAT.PARCIAL |
| 80 | GMP-REC.EXENCION Y REM.DEUDA-PRIVAT.TOTAL |
| 81 | GMP-REC.EXENCION Y REM.DEUDA-PRIVAT.PARCIAL |
| 82 | CUENTA CORRIENTE |
| 83 | EMERGENCIA AGROPECUARIA LEY 26.509 |
| 84 | EMERGENCIA AGROPECUARIA |
| 85 | CONCURSO HOMOLOGADO |
| 86 | ORDEN JUDICIAL DE INSCRIPCION EN EL REGISTRO |
| 87 | DECLARACTORIA DE HEREDEROS/TESTAMENTO VALIDO |
| 88 | INICIO JUDICIAL DE SUCESION |
| 89 | CUENTA PARTICIONARIA |
| 90 | TRANSFERENCIA DE APORTES. DECRETO 1866/2006 |
| 91 | BENEFICIARIOS DECRETO N° 1.439/01 |
| 92 | AGENTES DEL SISTEMA NACIONAL DEL SEGURO DE SALUD |
| 93 | CONTROL FISCAL DE DIVISAS |
| 94 | REGISTRO DE PROVEEDORES DE PUBLICIDAD DE AFIP |
| 95 | ZONA DE DESASTRE LEY 26.509 |
| 96 | COMPENSACION DE TRIGO-MAIZ |
| 97 | EMPLEADOR MICRO, PEQUEÑA Y MEDIANA EMPRESA |
| 98 | RE. 50/13 SPMSDR SUP. MONT.MIC.PEQ. Y MED.EMP. ART. 1 A 7 |
| 99 | RESOLUCION 50/2013 SPMEDR - ACTIVIDAD EXCLUIDA SECCION J |
| 100 | DDJJ INFORMATIVA-MONOTRIBUTO |
| 101 | LOCADOR DE EMBARCACIONES PESQUERAS |
| 102 | ARMADOR CON EMBARCACION PROPIA |
| 103 | COOPERATIVA DE TRABAJO ROM |
| 104 | PROCESADOR Y/O ALMACENADOR DE RECURSOS MARITIMOS |
| 105 | CONSIG/INTERM. COMER. DE REC. MARITIMOS SUS PROD.Y/O SUBPROD |
| 106 | PLANTA PROCESADORA DE HARINA Y/O ACEITE DE PESCADO |
| 107 | SERVICIOS CONEXOS |
| 108 | CUIT INACTIVA |
| 109 | ARMADOR CON EMBARCACION LOCADA |
| 110 | PRODUCTOR DE SOLVENTES Y AGUARRAS |
| 111 | PRODUCTOR DE NAFTA VIRGEN |
| 112 | PRODUCTOR DE GASOLINA NATURAL |
| 113 | PRODUCTOR DE GASOLINA PIROLISIS |
| 114 | ELABORADOR DE PRODUCTO GRAVADO POR RECUPERACION |
| 115 | ELABORADOR DE THINNERS |
| 116 | ELABORADOR DE DILUYENTES |
| 117 | PRODUCTOR DE PINTURAS |
| 118 | PRODUCCIÓN DE AGROQUÍMICOS |
| 119 | PRODUCCIÓN DE RESINAS |
| 120 | PRODUCCIÓN DE INSECTICIDAS |
| 121 | PRODUCCIÓN DE LUBRICANTES Y ADITIVOS |
| 122 | EXTRACCIÓN DE ACEITES VEGETALES |
| 123 | ELABORACIÓN DE ADHESIVOS |
| 124 | ELABORACIÓN DE TINTAS GRÁFICAS |
| 125 | MANUFACTURAS DE CAUCHO |
| 126 | ELABORACIÓN DE CERAS Y PARAFINAS |
| 127 | PROCESOS DE SEPARACIÓN |
| 128 | ELABORACIÓN DE PRODUCTOS QUÍMICOS |
| 129 | ALQUILACIÓN (CATALÍTICA O ÁCIDA) |
| 130 | HIDROGENACIÓN (CATALÍTICA) |
| 131 | DESHIDROGENACIÓN (CATALÍTIA) |
| 132 | HIDRODESALQUILACIÓN (TÉRMICA O CATALÍTICA) |
| 133 | OXIDACIÓN (CATALÍTICA) |
| 134 | NITRACIÓN |
| 135 | SULFONACIÓN |
| 136 | HALOGENACIÓN |
| 137 | CRAQUEO (TÉRMICO CON VAPOR) |
| 138 | POLIMERIZACIÓN |
| 139 | SÍNTESIS QUÍMICA |
| 140 | EMPRESA USUARIA DE THINNERS |
| 141 | EMPRESA USUARIA DE DILUYENTES |
| 142 | EMPRESA IMPORTADORA DE THINNERS Y/O DILUYENTES |
| 143 | EMPRESA IMPORTADORA DE LOS PRODUCTOS SECCIÓN 1 |
| 144 | EMPRESA EXPORTADORA |
| 145 | EMPRESA DISTRIBUIDORA |
| 146 | EMPRESA DE TRANSPORTE MARÍTIMO Y FLUVIAL |
| 147 | EMPRESA DE TRANSPORTE TERRESTRE |
| 148 | EMPRESA DE ALMACENAJE |
| 149 | EMPRESA QUE PRESTA SERVICIOS DE RECUPERO |
| 150 | SITER CAPÍTULO B |
| 151 | REG DE INFORMACIÓN FIDEICOMISOS FINANCIEROS Y NO FINANCIEROS |
| 152 | ZONA AFECTADA POR VOLCÁN PUYEHUE |
| 153 | SITER CAPITULO A - ENTIDADES FINANCIERAS |
| 154 | SITER CAPITULO A - DOMICILIOS |
| 155 | OBSERVADO SUSS - SUJETO A VERIFICACION |
| 156 | ZONA AFECTADA POR ERUPCIÓN DEL VOLCÁN PUYEHUE. LEY N° 26.697 |
| 157 | CITI ESCRIBANOS |
| 158 | ORGANISMO REPRESENTANTE DE LA PROVINCIA |
| 159 | CITI PROMOVIDAS |
| 160 | CANCELACIÓN DE CUIT RG 3358 |
| 161 | TIPO DE EMPRESA HOLDING |
| 162 | INICIO SUCESIÓN |
| 163 | DISCAPACIDAD PERMANENTE/INCAPACIDAD FÍSICA TEMPORAL |
| 164 | INCAP. LEGAL O INHAB. JUD. INCLUYE INSANÍA, PRIV. DE LA LIB. |
| 165 | REGISTRARSE AMBIENTAL- INICIO |
| 166 | REGISTRARSE DESARROLLO SOCIAL-INICIO |
| 167 | REGISTRARSE TURISMO-INICIO |
| 168 | REGISTRARSE OTROS-INICIO |
| 169 | REGISTRARSE AMBIENTAL |
| 170 | REGISTRARSE DESARROLLO SOCIAL |
| 171 | REGISTRARSE TURISMO |
| 172 | REGISTRARSE OTROS |
| 173 | MENOR DE EDAD CON TÍTULO HABILITANTE EJERC. PROFESIÓN |
| 174 | R.G. Nº 3358 CONTRATO DE COL. EMP. EXENTA EN IVA  - ACE/UTE |
| 175 | R.G. Nº 3358 P. JUR. C/ BIENES REGISTRAB Y SIN ACT. COMERCIA |
| 176 | R.G. Nº 3358 P. JUR. EN ETAPA DE INVERSIÓN INICIAL PROLONGAD |
| 177 | R.G. Nº 3358 P. JUR. CON INICIO/REINICIO DE ACTIVIDADES |
| 178 | R.G. Nº 3358 P.JUR. CON INCUMPLIMIENTOS FORMALES Y/O MATER. |
| 179 | R.G. Nº 3358 REACTIVACIÓN POR DISOLUCIÓN DE LA SOCIEDAD |
| 180 | MEDICINA PREPAGA |
| 181 | COMER.DE B.USADOS NO REG.- DESARMADEROS DE AUTOMOTORES |
| 182 | COMER.DE B.USADOS NO REG.- DESARMADEROS DE OTRO TIPO, ETC |
| 183 | COMER.DE B.USADOS NO REG.- AUTOPARTES Y REPUESTOS PARA AUT. |
| 184 | COMER.DE B.USADOS NO REG.- REPUESTOS PARA MOTOVEHÍCULOS |
| 185 | COMER.DE B.USADOS NO REG.- REPUESTOS P/ OTRO TIPO DE VEHÍC. |
| 186 | COMER.DE B.USADOS NO REG. - EQUIPOS DE TELEFONÍA MÓVIL |
| 187 | COMER.DE B.USADOS NO REG. - PRODUCTOS DE COMPUTACIÓN |
| 188 | COMER.DE B.USADOS NO REG. - PRODUCTOS DE ELECTRÓNICA |
| 189 | COMER.DE B.USADOS NO REG.- JOYAS, PIEDRAS PRECIOSAS, ETC. |
| 190 | COMER.DE B.USADOS NO REG. - INTERMEDIARIOS |
| 191 | COMER.DE B.USADOS NO REG. - OTROS SUJETOS |
| 192 | REGISTRO DE INVERSORES VINCULADOS CON FUTBOLISTAS PROFESIONA |
| 193 | REGISTRO DE REPRESENTANTES DE FUTBOLISTAS PROFESIONALES |
| 194 | PYME FISCAL |
| 195 | CANCELACIÓN DE CUIT POR BASE APOC |
| 196 | BAJA PROYECTO PRODUCTIVO SOLICITADA POR MIN. DESARROLLO SOC. |
| 197 | DJ INFORMATIVA DE MERCADO CAMBIARIO F.337 |
| 198 | RG 3450 ART 9 - ORGANISMOS PÚBLICOS Y SIMILARES |
| 199 | RG 3475 - ZONAS AFECTADAS POR TEMPORAL |
| 200 | ZONA AFECTADA POR VOLCÁN COPAHUE R.G. 3508 |
| 201 | SIST. CTAS. TRIB. - OBLIGATORIEDAD DE USO - R.G. 3486/2013 |
| 202 | TIT.CONC/AUT.DE CASINO/SALA DE JUEGO QUE EXP.DIR.LA ACT |
| 203 | TIT.CONC/AUT.DE CASINO/SALA DE JUEGO QUE NO EXP.DIR.LA ACT |
| 204 | SUJETOS QUE EXP.JUEGOS DE AZAR/APUESTAS, NO TIT.CASINOS/AP. |
| 205 | OTROS SUJETOS QUE DESARROLLEN LA EXPL.DE JUEGOS DE AZAR/AP. |
| 206 | NUEVO PLAN DE FACILIDADES DE PAGO |
| 207 | ÁREAS AFECTADAS ROSARIO 05/08/2013 RG. 3520 |
| 208 | REGISTRO FISCAL DE EMPRESAS MINERAS |
| 209 | REGISTRO FISCAL DE PROVEEDORES DE EMPRESAS MINERAS |
| 210 | REGISTRO FISCAL DE TIT. DE DERECHOS DE EXPLORACION O CATEO |
| 211 | ZONAS AFECTADAS POR INCENDIOS RG.3530 |
| 212 | SOLICITUD ADHESIÓN A MONOTRIBUTO SUJETO A VERIFICACIÓN AFIP |
| 213 | SOLICITUD DE ADHESIÓN A MONOTRIBUTO APROBADA |
| 214 | SOLICITUD DE ADHESIÓN A MONOTRIBUTO RECHAZADA |
| 215 | REG.FEDERAL DE EMPLEO PROTEGIDO P/ PERSONAS CON DISCAPACIDAD |
| 216 | TARJETAS DE CREDITO |
| 217 | REGIMEN DE INFORMACION TRANSPORTADORAS DE CAUDALES |
| 218 | AFIP DGI-REGIMEN DE INFORMACION DE FERIAS |
| 219 | CCG - ADMINISTRADORA DEL FONDO ESPECIAL DEL TABACO |
| 220 | CCG - TABACO VIRGINIA DEL CHACO |
| 221 | CCG - VITIVINICOLA DE RIO NEGRO |
| 222 | CCG - DIRECCION DE BOSQUES |
| 223 | CCG MULTIPRODUCTO DEL CHACO |
| 224 | OBLIGADO A INFORMAR DDJJ PATRIMONIAL INTEGRAL |
| 225 | IMPUESTOS DE COMBUSTIBLES LIQUIDOS DECRETO 1016/97 |
| 226 | GUIA FISCAL HARINERA - ESTABLECIMIENTOS MOLINEROS |
| 227 | GUIA FISCAL HARINERA - USUARIOS DE MOLIENDA |
| 228 | CCG VITIVINICOLA DE SAN JUAN |
| 229 | CCG VITIVINICOLA DE MENDOZA |
| 230 | REGISTRO ESPECIAL DE EXPORTADORES DE SERVICIOS DE SOFTWARE |
| 231 | COMPRA DE MATERIALES RECICLABLES (FISC) |
| 232 | REG.INF. DE OPERACIONES DE COMERCIALIZACION DE LECHE CRUDA |
| 233 | GMP LEY 25063 ART. 3 |
| 234 | ZONAS AFECTADAS POR TEMPORAL EN CHIVILCOY |
| 235 | ACTIVIDAD COMERCIAL EN ZONA TURÍSTICA |
| 236 | PEQUEÑOS PRODUCTORES AGRICOLAS |
| 237 | PEQUEÑOS PRODUCTORES LECHEROS |
| 238 | CCG TABACO JUJUY |
| 239 | CCG VITIVINICOLA DE NUEQUEN |
| 240 | CUIT ESPECIAL CON CORRECCION PAMI |
| 241 | UNIVERSIDADES NACIONALES |
| 242 | CUIT ESPECIAL PAMI - NO PAMI |
| 243 | LEY 22016 SIN ASIGNACIONES FAMILIARES |
| 244 | REGISTRO UTES F. 2664 |
| 245 | REGISTRO UTES F. 2665 |
| 246 | REGIMEN DE INFORMACION DE OPERACIONES COMERCIALES MINORISTAS |
| 247 | EMPRESAS PROV. DE SOFTWARE QUE INTERACTUAN CON WEB SERVICES |
| 248 | PAGO DE EXPENSAS |
| 249 | AFIP DGI-CUOTAS ESCUELAS CUOTAS DE COLEGIOS (FISC) |
| 250 | ZONAS AFECTADAS POR EL TEMPORAL EN SAN JUAN Y MENDOZA.RG3592 |
| 255 | PRESENTACION DE ESTADOS CONTABLES EN FORMATO PDF |
| 256 | PRESTADORES DE SERV. DE MANO DE OBRA PARA EL PROC. DE PESC. |
| 257 | SECRETARÍA DE TRANSPORTE |
| 258 | AREAS AFEC.POR EL TEMP. ACAECIDO EN LAS PROV. NEUQ. Y RIO NE |
| 259 | ADQUISICION DE RESIDENCIA EN MATERIA MIGRAT EN OTRA JURISDIC |
| 260 | PÉRDIDA DE RESID. P/ PERMAN. EN EL EXTERIOR P/ PER. 12 MESES |
| 261 | INICIO SOLIC. CERT.FISCAL PARA CONTRATAR - SIN CRÉD. C/ ESTA |
| 262 | INICIO SOLIC. CERTIF. FISCAL P/CONTRATAR - CON CRÉD.C/ ESTAD |
| 263 | CANCELACIÓN CUIT P/EXCL. PLENO DER.R.G. AFIP Nº 3640 - ART.9 |
| 264 | INSCRIPTO EN FERIA URKUPIÑA |
| 265 | ZONAS AFECT.POR INUND.EN MISIONES/CORRIENTES/FORMOSA RG3641 |
| 266 | ORGANISMO PUBLICO NACIONAL |
| 267 | CONFEDERACION DE PARTIDOS POLITICOS |
| 268 | ALIANZA DE PARTIDOS POLITICOS |
| 269 | FUSION DE PARTIDOS POLITICOS |
| 270 | PARTIDO POLITICO EN FORMACION |
| 271 | PARTIDO POLITICO CADUCO |
| 272 | RES.50 SPMEDR SUJ. NO CAT./F.JUR.EXCL./EXCEP. PRES DJ/ N.INS |
| 273 | REGISTRA CAUSAS PENALES - CERTIFICADO FISCAL PARA CONTRATAR |
| 274 | MICRO, PEQUEÑA Y MEDIAANA EMPRESA ART 1 Y 7° RES. 50/2013 |
| 275 | DACION EN PAGO DE ESPACIOS PUBLICITARIOS |
| 276 | AREAS EFECTADAS POR TEMPORAL R.G. AFIP Nº 3695 |
| 277 | GALERIA DE ARTE |
| 278 | COMERCIALIZADORES E INTERMEDIARIOS DE OBRAS DE ARTE |
| 279 | REGISTRARSE LABORAL - INICIO |
| 280 | REGISTRARSE LABORAL |
| 281 | CERTIFICADO FISCAL PARA CONTRATAR -SIN CRÉDITO CON EL ESTADO |
| 282 | CERT. FISCAL PARA CONTRATAR - CON CRÉDITOS CON EL ESTADO |
| 283 | CADUCIDAD CERT. FISCAL PARA CONTRATAR - REG. CAUSAS PENALES |
| 284 | REGISTRA CAUSAS PENALES - RSE |
| 285 | REG. TRAZABILIDAD ANIMAL -CONSIGNATARIO / COMIS. DE HACIENDA |
| 286 | REG. TRAZABILIDAD ANIMAL -PROVEEDOR DE DISPOSITIVOS - INICIO |
| 287 | REG. TRAZABILIDAD ANIMAL -PROVEEDOR DE LECTORAS - INICIO |
| 288 | REG. TRAZABILIDAD ANIMAL -INTERMEDIARIO |
| 289 | REG. TRAZABILIDAD ANIMAL -PROD. DE HACIENDA BOVINA/BUBALINA |
| 290 | REG. TRAZABILIDAD ANIMAL - FEED LOTS ESTABLEB. DE ENGORDE |
| 291 | REG. TRAZABILIDAD ANIMAL -ESTABLECIMIENTO FAENADOR |
| 292 | REG. TRAZABILIDAD ANIMAL - MERCADO CONCENTRADOR / FERIA |
| 293 | REG. TRAZABILIDAD ANIMAL -USUARIO DE FAENA |
| 294 | REG. TRAZABILIDAD ANIMAL -PROVEEDOR DE DISPOSITIVOS |
| 295 | REG. TRAZABILIDAD ANIMAL -PROVEEDOR DE LECTORAS |
| 296 | NO PASO LOS CONTROLES - SIFTA |
| 297 | REGISTRA CAUSAS PENALES - SIFTA |
| 298 | INTEGRANTE DE PJ CON QUIEBRA /CESACION DE PAGOS |
| 299 | FALLIDO REHABILITADO ART. 236 LEY 24.522 |
| 300 | SITER A - TARJETAS DE DÉBITO OPERACIONES EN EL EXTERIOR |
| 301 | FALLECIDO - BENEFICIARIO ANSES RG 3713 |
| 302 | PERSONA FÍSICA INACTIVA CON USUARIO ESPECIAL RESTRINGIDO |
| 303 | ZONAS AFECTADAS POR INUNDACIONES PCIA. DE CORDOBA, RG 3747 |
| 304 | ZONAS AFECTADAS POR INCENDIOS EN LA PCIA.DEL CHUBUT, RG 3746 |
| 305 | REG. SECTOR AZUCARERO -PRODUCTOR CAÑERO - INICIO |
| 306 | REG. SECTOR AZUCARERO -PRODUCTOR CAÑERO |
| 308 | CCG VITIVINICOLA DE LA RIOJA |
| 309 | CCG YERBA MATE DE MISIONES Y CORRIENTES |
| 310 | MONOTRIBUTO SOCIAL PAGO A CARGO MINISTERIO DESARROLLO SOCIAL |
| 311 | ZONAS AFECTADAS EN LAS PROV. DE RIO NEGRO Y NEUQUEN |
| 312 | OBLIGADO A LIBRO DE SUELDOS DIGITAL |
| 313 | PRODUCTOR APICOLA - INICIO |
| 314 | ACOPIADOR DE MIEL - INICIO |
| 315 | INTERMEDIARIO - INICIO |
| 316 | PRODUCTOR APICOLA |
| 317 | ACOPIADOR DE MIEL |
| 318 | INTERMEDIARIO |
| 319 | SOL. CERT FISCAL P. CONTRA. RECHAZADO - NO ACREDITA CRÉDITOS |
| 320 | REGISTRA CAUSAS PENALES - REG. SECTOR APICOLA |
| 321 | RELEVAMIENTO DE TRABAJADORES CON IRREGULARIDADES DETECTADAS |
| 322 | AREAS AFECTADAS INUNDACIÓN BS. AS Y SANTA FE RG 3794/15 |
| 323 | AERAS AFECTADAS FEN. METEOROLÓG. SALTA RG 3795/15 |
| 324 | TALLER PROTEGIDO ESPECIAL PARA EL EMPLEO (TPEE) |
| 325 | TALLER PROTEGIDO DE PRODUCCION (TPP) |
| 326 | GRUPOS LABORALES PROTEGIDOS (GLP) |
| 327 | PADRON AFA - DECRETO 1212 |
| 328 | UNIVERSO 1 |
| 329 | UNIVERSO 2 |
| 330 | UNIVERSO 3 |
| 331 | UNIVERSO 4 |
| 332 | UNIVERSO 5 |
| 333 | SOLICITUD |
| 334 | CCG FORESTO INDUSTRIAL DE CHACO |
| 335 | CCG VITIVINICOLA DE SALTA |
| 336 | CCG VITIVINICOLA DE CATAMARCA |
| 337 | REGIMEN INFORMATIVO DE COMPRAS Y VENTAS |
| 338 | DISOLUCIÓN |
| 339 | PARTIDO POLÍTICO - REG. CADUCIDAD S/INFO MIN. DEL INTERIOR |
| 340 | CUIT/CUIL/CDI INACTIVADA A PARTIR DE INFORMACIÓN DE RENAPER |
| 341 | SOLICITUD CASOS ESPECIALES |
| 342 | COOP.EFECTORAS INACTIVADAS POR REQ.DEL MIN.DESARROLLO SOCIAL |
| 343 | SOCIEDAD EN FORMACION - INACTIVADA POR INCUMPLIMIENTO |
### Categorias Monotributo
| **id** | **desc** |
|---|---|
| 36 | B LOCACIONES DE SERVICIO |
| 37 | C LOCACIONES DE SERVICIO |
| 38 | D LOCACIONES DE SERVICIO |
| 39 | E LOCACIONES DE SERVICIO |
| 40 | F LOCACIONES DE SERVICIO |
| 41 | G LOCACIONES DE SERVICIO |
| 42 | H LOCACIONES DE SERVICIO |
| 43 | I LOCACIONES DE SERVICIO |
| 44 | B VENTAS DE COSAS MUEBLES |
| 45 | C VENTAS DE COSAS MUEBLES |
| 46 | D VENTAS DE COSAS MUEBLES |
| 47 | E VENTAS DE COSAS MUEBLES |
| 48 | F VENTAS DE COSAS MUEBLES |
| 49 | G VENTAS DE COSAS MUEBLES |
| 50 | H VENTAS DE COSAS MUEBLES |
| 56 | INTEGRANTE DE SOCIEDAD |
| 61 | B MONOTRIBUTO SOCIAL AGROP. |
| 62 | I VENTAS DE COSAS MUEBLES |
| 63 | J VENTAS DE COSAS MUEBLES |
| 64 | K VENTAS DE COSAS MUEBLES |
| 65 | L VENTAS DE COSAS MUEBLES |
| 66 | D 2 SOCIOS LOCACIONES |
| 67 | D 3 SOCIOS LOCACIONES |
| 68 | E 2 SOCIOS LOCACIONES |
| 69 | E 3 SOCIOS LOCACIONES |
| 70 | F 2 SOCIOS LOCACIONES |
| 71 | F 3 SOCIOS LOCACIONES |
| 72 | G 2 SOCIOS LOCACIONES |
| 73 | G 3 SOCIOS LOCACIONES |
| 74 | H 2 SOCIOS LOCACIONES |
| 75 | H 3 SOCIOS LOCACIONES |
| 76 | I 2 SOCIOS LOCACIONES |
| 77 | I 3 SOCIOS LOCACIONES |
| 78 | D 2 SOCIOS VENTAS |
| 79 | D 3 SOCIOS VENTAS |
| 80 | E 2 SOCIOS VENTAS |
| 81 | E 3 SOCIOS VENTAS |
| 82 | F 2 SOCIOS VENTAS |
| 83 | F 3 SOCIOS VENTAS |
| 84 | G 2 SOCIOS VENTAS |
| 85 | G 3 SOCIOS VENTAS |
| 86 | H 2 SOCIOS VENTAS |
| 87 | H 3 SOCIOS VENTAS |
| 88 | I 2 SOCIOS VENTAS |
| 89 | I 3 SOCIOS VENTAS |
| 90 | J 2 SOCIOS VENTAS |
| 91 | J 3 SOCIOS VENTAS |
| 92 | K 2 SOCIOS VENTAS |
| 93 | K 3 SOCIOS VENTAS |
| 94 | L 2 SOCIOS VENTAS |
| 95 | L 3 SOCIOS VENTAS |
| 96 | B TRABAJADOR PROMOVIDO |
| 97 | B ACTIVIDAD PRIMARIA |
| 98 | B ASOCIADO COOPERATIVA |
| 99 | B MONOTRIBUTO SOCIAL LOCACION |
| 100 | B MONOTRIBUTO SOCIAL VENTAS |
| 101 | D 2 SOCIOS PROY. SERVICIOS |
| 102 | D 2 SOCIOS PROY. PRODUCTIVO |
| 103 | E 3 SOCIOS PROY. SERVICIOS |
| 104 | E 3 SOCIOS PROY. PRODUCTIVO |
### Categorias Autonomos
| **id** | **desc** |
|---|---|
| 103 | T1 CAT III INGRESOS HASTA $15.000 |
| 104 | T1 CAT IV INGRES DESDE $15.001 A $30.000 |
| 105 | T1 CAT V INGRESOS DESDE $30.001 |
| 113 | T1 CAT III (PRIMA) ING. HASTA $15.000 |
| 114 | T1 CAT IV (PRIMA) INGR $15.001 A $30.000 |
| 115 | T1 CAT V (PRIMA) INGRESOS DESDE $ 30.001 |
| 123 | T1 CAT III (OPTATIVA) |
| 124 | T1 CAT IV (OPTATIVA) |
| 125 | T1 CAT V (OPTATIVA) |
| 133 | T1 CAT III (PRIMA OPTATIVA) |
| 134 | T1 CAT IV (PRIMA OPTATIVA) |
| 135 | T1 CAT V (PRIMA OPTATIVA) |
| 201 | T2 CAT I INGRESOS HASTA $20.000 |
| 202 | T2 CAT II INGRESOS DESDE $20.001 |
| 210 | CATEGORIA A2 (AMAS DE CASA) |
| 211 | T2 CAT I (PRIMA) INGRESOS HASTA $20.000 |
| 212 | T2 CAT II (PRIMA) INGRESOS DESDE $20.001 |
| 221 | T2 CAT I (OPTATIVA) |
| 222 | T2 CAT II (OPTATIVA) |
| 223 | T2 CAT III (OPTATIVA) |
| 224 | T2 CAT IV (OPTATIVA) |
| 225 | T2 CAT V (OPTATIVA) |
| 231 | T2 CAT I (PRIMA OPTATIVA) |
| 232 | T2 CAT II (PRIMA OPTATIVA) |
| 233 | T2 CAT III (PRIMA OPTATIVA) |
| 234 | T2 CAT IV (PRIMA OPTATIVA) |
| 235 | T2 CAT V (PRIMA OPTATIVA) |
| 301 | T3 CAT I INGRESOS HASTA $25.000 |
| 302 | T3 CAT II INGRESOS DESDE $25.001 |
| 311 | T3 CAT I (PRIMA) INGRESOS HASTA $25.000 |
| 312 | T3 CAT II (PRIMA)INGRESOS DESDE $25.001 |
| 321 | T3 CAT I (OPTATIVA) |
| 322 | T3 CAT II (OPTATIVA) |
| 323 | T3 CAT III ((OPTATIVA) |
| 324 | T3 CAT IV (OPTATIVA) |
| 325 | T3 CAT V (OPTATIVA) |
| 331 | T3 CAT I (PRIMA OPTATIVA) |
| 332 | T3 CAT II (PRIMA OPTATIVA) |
| 333 | T3 CAT III (PRIMA OPTATIVA) |
| 334 | T3 CAT IV (PRIMA OPTATIVA) |
| 335 | T3 CAT V (PRIMA OPTATIVA) |
| 401 | T4 CAT I VOLUNTARIA |
| 422 | T4 CAT II VOLUNTARIA (OPTATIVA) |
| 423 | T4 CAT III VOLUNTARIA (OPTATIVA) |
| 424 | T4 CAT IV VOLUNTARIA (OPTATIVA) |
| 425 | T4 CAT V VOLUNTARIA (OPTATIVA) |
| 501 | CAT I JUBILADO |
| 511 | CAT I MENOR |



## Novedades

Se recuerda que esta disponible el 
[grupo de usuarios y desarrolladores] (http://groups.google.com.ar/group/pyafipws) donde
se publicarán futuras novedades sobre PyAfipWS: servicios web de
factura electrónica y sus interfases (se recomienda suscribirse)

También esta disponible el sitio http://www.pyafipws.com.ar con noticias, anuncios e información técnica general

## Costos y Condiciones


Los clientes que asi lo requieran pueden adquirir horas de soporte técnico adicional (ver [Condiciones del Soporte Comercial](wiki:PyAfipWs#CostosyCondiciones)), se estima conveniente los siguientes planes:

- Soporte Mínimo: por 1 semana de cobertura hasta 1 hs en total (solo instalador para clientes actuales -por tiempo limitado- consulta local)

Ofrecemos soporte técnico comercial avanzado (pago), independiente a la AFIP, desarrollos especiales, interfaces web, etc. 
Obtenga mas información enviando un mail a info@pyafipws.com.ar o (011) 15-3048-9211 (asesoramiento sin cargo)

A su vez, se liberará el código fuente bajo licencia GPLv3 (software libre), al igual que se hizo con el restos de los servicios web. Para más detalles ver página FacturaElectronica.

La información de esta página es proporcionada a titulo informativo.

2014 - 2024 © MarianoReingart

**[Colaboraciones](https://link.mercadopago.com.ar/colaboracionespyafip)**

2014 © MarianoReingart