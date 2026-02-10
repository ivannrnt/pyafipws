= Trazabilidad de Medicamentos - WS !TrazaMed ANMAT/PAMI SNT =

[[TracNav(noreorder|FacturaElectronica)]]

Interfaz para Servicio Web Código de Trazabilidad de Medicamentos (SOAP) correspondiente a la [Resolución 435/2011](http://www.anmat.gov.ar/webanmat/Legislacion/Medicamentos/Resolucion_435-2011.pdf) del Ministerio de Salud y [Disposición 3683/2011](http://www.anmat.gov.ar/webanmat/Legislacion/Medicamentos/Disposicion_3683-2011.pdfp) de A.N.M.A.T.: Sistema Nacional de Trazabilidad de Medicamentos que deberán implementar las personas físicas o jurídicas que intervengan en la cadena de comercialización, distribución y  dispensación de especialidades medicinales incluidas en el Registro de Especialidades Medicinales. SNT Especificación Técnica V2.


## Índice
[[TOC(noheading,inline,depth=2)]]

## Introducción

Biblioteca para el web service de ANMAT/PAMI que permite automatizar la gestión de las trazabilidad de medicamentos: 

- Interfaz COM: Simil DLL/OCX, embebible para aplicaciones programadas en lenguajes visuales bajo windows (Visual Basic, Visual Fox Pro, SAP, etc.)
- Interfaz por consola (linea de comandos / archivo de texto): similar a aplicativos SIAP para sistemas legados (ej. RM COBOL) multiplataforma (DOS, Windows, Unix)
- Interfaz por tablas DBF: compatible con dBase, !FoxPro, Clipper -proximamente-
- Interfaz por base de datos: compatible con conectores ODBC (MS SQL Server), PostgreSQL y otros (Oracle, DB2) -proximamente-

Cubre totalmente el proceso, puede ser adaptado a programas existentes y no es requerido intervención del usuario.

Para más información ver PyAfipWs


**Importante**: El documento ***["ANMAT Especificación Técnica para Pruebas de Servicios v2"](attachment:trazamed_anmat_snt_especificacion_tecnica_v2.pdf)*** estaría entrando en vigencia a partir del 1/3/2013. Ver abajo los cambios ("Versión 2")
## Descargas

- Instalador: [instalador-PyAfipWs-2.33a-32bit+trazamed_1.15b-homo.exe](http://www.sistemasagiles.com.ar/soft/pyafipws/instalador-PyAfipWs-2.33a-32bit+trazamed_1.15b-homo.exe) (homologación v2 actualizado al 17/06/2014) 
- Documentación Oficial: [especificación técnica original](http://186.153.145.7/site/pdfs/documentacion_tecnica_especifica.pdf), [especificación técnica v2](attachment:trazamed_anmat_snt_especificacion_tecnica_v2.pdf), [especificación técnica v2 (actualizada en marzo y abril de 2013)](http://anmat.servicios.pami.org.ar/pdfs/especificacion_tecnica_v2.pdf), [set de datos](http://186.153.145.7/site/pdfs/set_de_datos.pdf), [set de datos v2 (actualizado marzo/2013)](http://anmat.servicios.pami.org.ar/pdfs/set_de_datos.pdf), [Catálogo Electrónico de Datos](http://186.153.145.7/site/pdfs/ced_20111129.pdf)
- Ejemplo en VB: [trazamed.bas](https://github.com/reingart/pyafipws/blob/master/ejemplos/trazamed/trazamed.bas)
- Ejemplo en VFP: [trazamed.prg](https://github.com/reingart/pyafipws/blob/master/ejemplos/trazamed/trazamed.prg)
- Código Fuente (Python): [trazamed.py](https://github.com/reingart/pyafipws/blob/master/trazamed.py)

URL:

- Entrenamiento: https://servicios.pami.org.ar/trazamed.WebService ([WSDL](https://servicios.pami.org.ar/trazamed.WebService?wsdl))
- Producción: https://trazabilidad.pami.org.ar:9050/trazamed.WebService ([WSDL](https://trazabilidad.pami.org.ar:9050/trazamed.WebService?wsdl))

## Métodos

- **`SendMedicamentos(usuario, password, f_evento, h_evento, gln_origen, gln_destino, n_remito, n_factura, vencimiento, gtin, lote, numero_serial, id_obra_social, id_evento, cuit_origen, cuit_destino, apellido, nombres, tipo_docmento, n_documento, sexo, direccion, numero, piso, depto, localidad, provincia, n_postal, fecha_nacimiento, telefono, nro_asociado)`**: Realiza el registro de una transacción de medicamentos
- **`SendCancelacTransacc(usuario, password, codigo_transaccion)`**:  Realiza la cancelación de una transacción
- **`SendMedicamentosDHSerie(usuario, password, f_evento, h_evento, gln_origen, gln_destino, n_remito, n_factura, vencimiento, gtin, lote, desde_numero_serial, hasta_numero_serial, id_obra_social, id_evento, cuit_origen, cuit_destino, apellido, nombres, tipo_docmento, n_documento, sexo, direccion, numero, piso, depto, localidad, provincia, n_postal, fecha_nacimiento, telefono, nro_asociado)`**: Realiza el registro de una transacción de medicamentos. Envía un lote de medicamentos informando el desde-hasta número de serie (`desde_numero_serial`, `hasta_numero_serial`)
- **`SendMedicamentosFraccion(usuario, password, f_evento, h_evento, gln_origen, gln_destino, n_remito, n_factura, vencimiento, gtin, lote, numero_serial, id_obra_social, id_evento, cuit_origen, cuit_destino, apellido, nombres, tipo_docmento, n_documento, sexo, direccion, numero, piso, depto, localidad, provincia, n_postal, fecha_nacimiento, telefono, nro_asociado, cantidad)`**: Nuevo método para Transacción de medicamentos fraccionados (farmacias)

### Nuevos métodos Versión 2

- **`SendConfirmaTransacc(usuario, password, p_ids_transac, f_operacion)`**: Confirma la recepción de un medicamento (recibe nro de transacción individual al medicamento seriado; fecha en que ocurre el evento)
- **`SendAlertaTransacc(usuario, password, codigo_transaccion)`**: Alerta un medicamento, acción contraria a “confirmar la transacción”.
- **`SendCancelacTransaccParcial(usuario, password, codigo_transaccion, gtin_medicamento, numero_serial)`**:  Realiza la cancelación parcial de una transacción, gtin_medicamento y numero serial son parámetros opcionales. *Disponible desde la actualización 1.12a*.
- **`GetTransaccionesNoConfirmadas(usuario, password, p_id_transaccion_global, id_agente_informador, id_agente_origen, id_agente_destino, id_medicamento, id_evento, fecha_desde_op, fecha_hasta_op, fecha_desde_t, fecha_hasta_t, fecha_desde_v, fecha_hasta_v, n_remito, n_factura, estado, lote, numero_serial)`**: Trae un listado de las transacciones donde el agente es el destino y no están confirmadas por el agente receptor (estado = 1: informada, 2: anulada, 3: confirmada, 4:alertada, 5: cargada). Salvo usuario y password, el resto de los parámetros son opcionales. lote y numero_serial agregado en *actualización 1.14a*.
- **`GetEnviosPropiosAlertados(usuario, password, p_id_transaccion_global, id_agente_informador, id_agente_origen, id_agente_destino, id_medicamento, id_evento, fecha_desde_op, fecha_hasta_op, fecha_desde_t, fecha_hasta_t, fecha_desde_v, fecha_hasta_v, n_remito, n_factura)`**: Obtiene las distribuciones y envíos propios hacia otro eslabón que han sido alertados en vez de confirmados. Todos los parámetros son opcionales excepto usuario y password. *Disponible desde la actualización 1.12a*.

Nuevos métodos auxiliares (*Disponible desde la actualización 1.15a*):

- **`GetTransaccionesWS(usuario, password, p_id_transaccion_global, id_agente_origen, id_agente_destino, id_medicamento, id_evento, fecha_desde_op, fecha_hasta_op, fecha_desde_t, fecha_hasta_t, fecha_desde_v, fecha_hasta_v, n_remito, n_factura, id_estado, nro_pag,)`**: Obtiene los movimientos realizados y permite filtros de búsqueda
- **`GetCatalogoElectronicoByGTIN(usuario, password, cuit_fabricante, gtin, descripcion, id_monodroga)`**: Obtiene el Catálogo Electrónico de Medicamentos

### Métodos generales / accesorios

- **`Conectar(cache, url_webservice_wsdl, proxy, wrapper, cacert)`**: Establece la conexión con el servidor remoto, recibe el directorio de archivos temporales, la URL del WSDL (descripción del webservice) y proxy en formato 'usuario:clave@servidor:puerto'. Si no se especifíca url, se utiliza servidores de homologación. Parametros adicionales optativos: wrapper es la librería HTTP a utilizar y cacert la ruta al certificado de la autoridad de certificante del servidor (CA)
- **`LeerError()`**: devuelve el error notificado por el webservice, o vacio si no hay más errores para informar.
- **`LeerTransaccion()`**: obtiene la próxima transacción a devuelta por el webservice al consultar (luego llamar a !GetParametro para obtener los valores de cada campo). Devuelve False si no hay más transacciones
- **`SetParametro(clave, valor)`**: establece el parámetro de entrada de nombre "clave" con el respectivo "valor", que será usado al llamar al webservice (útil para lenguajes de programación que solo soportan 27 parámetros como VFP)
- **`GetParametro(clave)`**: devuelve el parámetro de salida de nombre "clave", que fue establecido al llamar un método del webservice (útil para recorrer las transacciones devueltas de las consultas, previa llamada a `LeerTransaccion`)


Los métodos devuelven `True` (verdadero) en caso de que se ejecuten correctamente, y establecen los atributos `Resultado`, `Errores` y `CodigoTransaccion` según corresponda.

En caso de falla (por ej. error de comunicación), devuelven `False` (falso) y se debe revisar atributos `Excepcion` y `Traceback`
## Atributos

- `Username`, `Password`: credenciales de seguridad para operar el webservice 
- `CodigoTransaccion`: número otorgado por el método remoto (en caso correcto)
- `Errores`: lista de validaciones fallidas devueltas por el método remoto
- `Resultado`: verdadero (`True`) si fue procesado correctamente
- `TransaccionPlainWS`: lista de diccionarios (array clave->valor) de parámetros de salida de `GetTransaccionesNoConfirmadas` (consulta de transacciones)
- `XmlRequest`, `XmlResponse`: mensajes xml crudos sin procesar (para depuración)
- `Version`, `InstallDir`: datos para depuración
- `Traceback`, `Excepcion`: errores no esperados de comunicación o similar (por ej. !SoapFault)

### Campos MedicamentosDTO, MedicamentosDTODHSerie, MedicamentosDTOFraccion

El método !SendMedicamentos recibe los datos correspondientes a una transacción de medicamentos:

| **Nombre** | **Tipo** | **Longitud** | **Obligatorio** | **Descripción** |
|---|---|---|---|---|
| f_evento | alfanumérico | 10 | si | Fecha en que ocurre el evento. Formato DD/MM/YYYY |
| h_evento | alfanumérico | 5 | si | Hora en la que ocurre el evento. Formato HH:MM |
| gln_origen | alfanumérico | 13 | si | Código GLN del agente origen. |
| cuit_origen | alfanumérico | 11 | si | Número de CUIT del agente origen. Numérico sin guiones. |
| gln_destino | alfanumérico | 13 | no | Código GLN del agente destino |
| cuit_destino | alfanumérico | 11 | no | Número de CUIT del agente destino. Numérico sin guiones. |
| n_remito | alfanumérico | 20 | no | Número de Remito |
| n_factura | alfanumérico | 20 | no | Número de Factura |
| vencimiento | alfanumérico | 10 | si | Fecha de Vencimiento del medicamento. Formato DD/MM/YYYY |
| gtin | alfanumérico | 14 | si | GTIN del medicamento |
| lote | alfanumérico | 20 | si | Número de lote |
| numero_serial | alfanumérico | 20 | si | Número de serie |
| id_evento | numerico | 2 | si | Identificador del evento. Ver tabla de Eventos. |
| apellido | alfanumérico | 50 | no | Apellido de la persona a la que se dispensó el medicamento. |
| nombres | alfanumérico | 100 | no | Nombre /s de la persona a la que se dispensó el medicamento |
| n_documento | alfanumérico | 10 | no | Número de Documento de la persona a la que se dispensó el medicamento |
| sexo | alfanumérico | 1 | no | Sexo de la persona de la persona a la que se dispensó el medicamento |
| tipo_documento | numerico |  | no | Tipo de Documento de la persona a la que se dispensó el medicamento |
| direccion | alfanumérico | 100 | no | Domicilio de la persona a la que se dispensó el medicamento |
| localidad | alfanumérico | 50 | no | Localidad de la persona a la que se dispensó el medicamento |
| numero | alfanumérico | 10 | no | Numero de calle de la persona a la que se dispensó el medicamento |
| piso | alfanumérico | 5 | no | Piso del departamento de la persona a la que se dispensó el medicamento |
| dpto | alfanumérico | 5 | no | Departamento de la persona a la que se dispensó el medicamento |
| n_postal | alfanumérico | 8 | no | Código postal de la persona a la que se dispensó el medicamento |
| telefono | alfanumérico | 30 | no | Número de teléfono de la persona a la que se le dispensó el medicamento. |
| id_obra_social | numerico | 9 | no | Numero de obra social que financia el medicamento cuando se dispensa al paciente. Ver tabla de obras sociales en documento set_de_datos.pdf |
| nro_asociado | alfanumérico | 30 | no | Número de afiliado a la obra social que financia el medicamento cuando se dispensa al paciente. |
| id_motivo_devolucion | numérico |  | no | (provisorio, no documentado por ANMAT al 03-02-2014) |
| otro_motivo_devolucion | alfanumérico |  | no | (provisorio, no documentado por ANMAT al 03-02-2014) |

El método SendMedicamentosDHSerie cambia el dato numero_serial por un rango:

| **Nombre** | **Tipo** | **Longitud** | **Obligatorio** | **Descripción** |
|---|---|---|---|---|
| desde_numero_serial | alfanumérico | 20 | si | Número de serie desde. |
| hasta_numero_serial | alfanumérico | 20 | si | Número de serie hasta. |

El método !SendMedicamentosFraccion agrega el siguiente campo luego del numero_serial:

| **Nombre** | **Tipo** | **Longitud** | **Obligatorio** | **Descripción** |
|---|---|---|---|---|
| cantidad | numerico | 3 | no | Indica la cantidad a dispensar del medicamento siempre que el mismo pueda ser fraccionado. La cantidad máxima esta dada por la cantidad de unidades de la presentación. La cantidad mínima es 1. |


**Importante**: si un campo no debe enviarse, completar con None, Null, Empty, ? o el valor equivalente para campos nulos. No usar cadena vacia o 0 ya que son datos válidos y se enviarán al webservice. No saltear u omitir parámetros, salvo que esten al final o sean pasados por nombre (keyword arguments), usar !SetParametro en dicho caso.
### Campos devueltos al consultar - !TransaccionPlainWs - Version 2

El método !GetTransaccionesNoConfirmadas devuelve la lista de transacciones que coincicidan con los criterios de búsqueda especificados.
Se puede acceder al atributo !TransaccionPlainWs para leer estos datos (diccionario clave - valor, dependiendo del lenguaje de programación).
Es posible recorrer dichas transacciones una por una usando el método !LeerTransaccion (devuelve True y establece los parámetros de salida, que pueden ser consultados con GetParametro).



Para el listado de transacciones no confirmadas, los parámetros de salida definidos en la documentación de ANMAT son los siguientes:

- `id_transaccion`: Numero de transaccion individual (a nivel nro de serie)
- `id_transac_global`: Numero Global
- ~~`nro_transaccion`: N/A~~
- `f_evento`: Fecha del evento
- `gln_destino`: GLN Destino
- ~~`cuit_destino`: CUIT Destino~~
- `gln_origen`: GLN Origen
- `n_remito`: Numero de Remito
- ~~`cuit_origen`: CUIT Origen~~
- `n_factura`: Numero de Factura
- `vencimiento`: Fecha de vencimiento de transaccion
- `gtin`: GTIN medicamento
- `lote`: Número de Lote
- `numero_serial`: Numero Serial
- `id_evento`: Numero de Evento (reestablecido pero no documentado por ANMAT al 03-02-2014)
- `d_evento`: Descripción del Evento
- `f_transaccion`: Fecha Transaccion*
- ~~`gln_agente_informador`: GLN Agente Informador~~
- ~~`c_usuario_informador`: Codigo de Usuario Informador~~
- ~~`id_transac_ws_anul`: ID Transaccion de Anulación~~
- ~~`f_anulacion`: Fecha de anulación (si aplica)~~
- `id_estado`: Estado de la transaccion
- ~~`d_provincia`: Provincia~~
- ~~`paciente`: Paciente (si aplica)~~
- ~~`cant_fraccion`: Cantidad Fraccion~~

**Importante**: en la respuesta devuelta por ANMAT, pueden no estar todos los parámetros presentes (depende de la transacción). Si no se encuentra el parámetro, !GetParametro devolverá nulo.

Los campos tachados fueron incluidos en la documentación preliminar pero omitidos por ANMAT en la versión definitiva. 
A partir del 17 de Junio de 2014, los campos no incluyen el guión bajo debido a un cambio en la descripción del servicio de ANMAT.
## Linea de Comandos

Para sistemas operativos legados (DOS bajo windows) y UNIX/Linux, es posible operar la herramienta de trazabilidad por consola. Recibe como parámetros los datos correspondientes a la llamada remota (ver métodos). Opcionalmente se puede especificar --testing para pruebas (usar xml de muestra como respuesta si no se tiene acceso a homologación) y --trace para imprimir por pantalla los datos enviados y recibidos.

**Nota**: dependiendo de la compilación y el instalador, el ejecutable puede ser **`TRAZAMED_CLI.EXE`**

Ejemplo de uso para Informar un Medicamento (por defecto recibe los argumentos según el método !SendMedicamento):

```
C:\PYANMAT>trazamed.exe "pruebasws" "Clave1234" "31/03/2015" "04:24" "9999999999918" "glnws" "R123400001234" "A123400001234" "31/03/2015" "GTIN1" "2015" "12348" "" 134 "20267565393" "20267565393" "Reingart" "Mariano" "96" "26756539" "M" "Saraza" "1234" "1" "A" "Hurlingham" "Buenos Aires" "1688" "01/01/2000" "5555-5555"
|Resultado  True|CodigoTransaccion   31013624|Errores||

```


Si no se específican los campos por linea de comando, de manera predeterminada se utilizará el formato de texto
Para usar Tablas DBF agregar a la linea de comandos el parámetro `--dbf`. 
Para soporte de JSON (JavaScript Object Notation), agregar parametro `--json`.
Se debe anteponer `--cargar` y `--grabar` para leer y escribir los datos en los archivos de intercambio.

Ejemplos para informar medicamentos usando archivos de texto, dbf y json respectivamente  (*disponible desde actualización 1.11a*):
```
C:\PYANMAT>trazamed.exe --cargar --grabar "pruebasws" "Clave1234"
C:\PYANMAT>trazamed.exe --cargar --grabar --dbf "pruebasws" "Clave1234"
C:\PYANMAT>trazamed.exe --cargar --grabar --json "pruebasws" "Clave1234"
```


Ejemplo de uso para cancelar una transacción (recibe usuario, password y número de transacción):

```
C:\PYANMAT>trazamed.exe --cancela "pruebasws" "pruebasws" "5114801" 
|Resultado False|CodigoTransaccion       None|Errores|3: Transaccion NO encontrada, NO se puede anular.|
```

Ejemplo de uso para cancelar una transacción parcialmente (recibe usuario, password, número de transacción, gtin y numero de serie -estos dos últimos opcionales-):

```
C:\PYANMAT>trazamed.exe --cancela_parcial  pruebasws pruebasws 2224635 000000000GTIN2 998
|Resultado False|CodigoTransaccion       None|Errores|3: Transaccion NO encontrada, NO se puede anular.|
```


Ejemplo de uso para Consultar transacciones no confirmadas -v2-:

```
C:\PYANMAT>trazamed.exe --consulta "pruebasws" "pruebasws"
| _gtin | _lote | _numero_serial | _id_transaccion | _estado | _f_transaccion | _d_evento | _gln_origen | _gln_destino |
|---|---|---|---|---|---|---|---|---|
| 07795360005385 | 412568 | 1200 | 5114793 | Informada | 19/02/2013 | ENVIO... | 9992105600005 | glnws |
| 07795347900511 | 412568 | 1200 | 5114796 | Informada | 19/02/2013 | ENVIO... | 9992105600005 | glnws |
| 00121231323232 | 412568 | 1200 | 5114798 | Informada | 19/02/2013 | ENVIO... | 9992105600005 | glnws |
| 55564646464645 | 412568 | 1200 | 5114801 | Informada | 19/02/2013 | ENVIO... | 9992105600005 | glnws |
```

Para generar un archivo de intercambio con los datos de las transacciones, especificar `--grabar` (*disponible desde actualización 1.11a*):

```
C:\PYANMAT>trazamed.exe --grabar --consulta "pruebasws" "pruebasws"
```

Ejemplo de uso para Consultar transacciones alertadas por el eslabón posterior (!GetEnviosPropiosAlertados) -v2-:

```
C:\PYANMAT>trazamed.exe --alertadas --consulta "pruebasws" "pruebasws"
CantPaginas None
HayError None
| _id_transaccion | _id_transaccion_global | _f_evento | _f_transaccion | _gtin | _lote | _numero_serial | _d_evento | _gln_origen | _gln_destino | _n_remito | _n_factura | _vencimiento |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 2224635 | 842235 | 14/06/2012 | 15/06/2012 15:14 | 000000000GTIN2 | 9999 | 998 | RECEPCION DE PRODUCTO DESDE UN ESLABON ANTERIOR | 9999999999918 | glnws | 4433 | A000100000001 | 15/12/2012 |
| 10493358 | 12479556 | 06/03/2013 | 23/04/2013 09:54 | 000000000GTIN4 | 1 | 77777565 | ENVIO DE PRODUCTO EN CARACTER DEVOLUCION | 9991106600007 | glnws | 1 | 1 | 31/12/2015 |
| 10493357 | 12479556 | 06/03/2013 | 23/04/2013 09:54 | 000000000GTIN4 | 1 | 77777564 | ENVIO DE PRODUCTO EN CARACTER DEVOLUCION | 9991106600007 | glnws | 1 | 1 | 31/12/2015 |
```


Ejemplo de uso para confirmar una transacción -v2- (recibe usuario, password, número de transacción y fecha de operación):

```
C:\PYANMAT>trazamed.exe --confirma "pruebasws" "pruebasws" "5114793" "25/02/2013"
|Resultado  True|CodigoTransaccion       None|Errores||
```


Ejemplo de uso para alertar una transacción -v2- (recibe usuario, password, número de transacción):

```
C:\PYANMAT>trazamed.exe --alerta "pruebasws" "pruebasws" "5114798"
|Resultado  True|CodigoTransaccion       None|Errores||
```

## Archivos de Intercambio

Desde la actualización 1.11a, la herramienta soporta archivos de intercambio en DBF, JSON o archivos de texto fijo (COBOL):

- **Medicamentos** (entrada/salida): [[attachment:medicamentos.json](attachment:medicamentos.txt],), [attachment:Medicame.dbf] (usado por `SendMedicamentos`, `SendMedicamentosDHSerie`, `SendMedicamentosFraccion`)
- **Transacciones** (salida): [[attachment:transacciones.json](attachment:transacciones.txt],), [attachment:Transacc.dbf] (usado por `GetTransaccionesNoConfirmadas`, parámetro `--consulta`)
- **Errores** (salida): [[attachment:errores.json](attachment:errores.txt],), [attachment:Errores.dbf]

### Formato para Medicamentos
| Nombre | Tipo | Long. | Pos(txt) | Campo(dbf) |
|---|---|---|---|---|
| f_evento | Alfanumerico | 10 | 1 | fevento |
| h_evento | Alfanumerico | 5 | 11 | hevento |
| gln_origen | Alfanumerico | 13 | 16 | glnorigen |
| gln_destino | Alfanumerico | 13 | 29 | glndestino |
| n_remito | Alfanumerico | 20 | 42 | nremito |
| n_factura | Alfanumerico | 20 | 62 | nfactura |
| vencimiento | Alfanumerico | 10 | 82 | vencimient |
| gtin | Alfanumerico | 14 | 92 | gtin |
| lote | Alfanumerico | 20 | 106 | lote |
| numero_serial | Alfanumerico | 20 | 126 | numeroseri |
| desde_numero_serial | Alfanumerico | 20 | 146 | desdenumer |
| hasta_numero_serial | Alfanumerico | 20 | 166 | hastanumer |
| id_obra_social | Numerico | 9 | 186 | idobrasoci |
| id_evento | Numerico | 3 | 195 | idevento |
| cuit_origen | Alfanumerico | 11 | 198 | cuitorigen |
| cuit_destino | Alfanumerico | 11 | 209 | cuitdestin |
| apellido | Alfanumerico | 50 | 220 | apellido |
| nombres | Alfanumerico | 100 | 270 | nombres |
| tipo_documento | Numerico | 2 | 370 | tipodocume |
| n_documento | Alfanumerico | 10 | 372 | ndocumento |
| sexo | Alfanumerico | 1 | 382 | sexo |
| direccion | Alfanumerico | 100 | 383 | direccion |
| numero | Alfanumerico | 10 | 483 | numero |
| piso | Alfanumerico | 5 | 493 | piso |
| depto | Alfanumerico | 5 | 498 | depto |
| localidad | Alfanumerico | 50 | 503 | localidad |
| provincia | Alfanumerico | 100 | 553 | provincia |
| n_postal | Alfanumerico | 8 | 653 | npostal |
| fecha_nacimiento | Alfanumerico | 100 | 661 | fechanacim |
| telefono | Alfanumerico | 30 | 761 | telefono |
| nro_asociado | Alfanumerico | 30 | 791 | nroasociad |
| cantidad | Numerico | 3 | 821 | cantidad |
| codigo_transaccion | Alfanumerico | 14 | 824 | codigotran |
### Formato para Transacciones
| Nombre | Tipo | Long. | Pos(txt) | Campo(dbf) |
|---|---|---|---|---|
| id_transaccion | Alfanumerico | 14 | 1 | idtransacc |
| id_transaccion_global | Alfanumerico | 14 | 15 | idtransac1 |
| f_evento | Alfanumerico | 10 | 29 | fevento |
| f_transaccion | Alfanumerico | 16 | 39 | ftransacci |
| gtin | Alfanumerico | 14 | 55 | gtin |
| lote | Alfanumerico | 20 | 69 | lote |
| numero_serial | Alfanumerico | 20 | 89 | numeroseri |
| nombre | Alfanumerico | 200 | 109 | nombre |
| d_evento | Alfanumerico | 100 | 309 | devento |
| gln_origen | Alfanumerico | 13 | 409 | glnorigen |
| razon_social_origen | Alfanumerico | 200 | 422 | razonsocia |
| gln_destino | Alfanumerico | 13 | 622 | glndestino |
| razon_social_destino | Alfanumerico | 200 | 635 | razonsoci1 |
| n_remito | Alfanumerico | 20 | 835 | nremito |
| n_factura | Alfanumerico | 20 | 855 | nfactura |
| vencimiento | Alfanumerico | 10 | 875 | vencimient |
### Formato para Errores
| Nombre | Tipo | Long. | Pos(txt) | Campo(dbf) |
|---|---|---|---|---|
| _c_error | Alfanumerico | 4 | 1 | cerror |
| _d_error | Alfanumerico | 250 | 5 | derror |
## Ejemplos

### Intefase COM en VB (5/6)

Envio de Medicamentos (transacción de trazabilidad):
```
#!vb

Dim TrazaMed As Object, ok As Variant

' Crear la interfaz COM
Set TrazaMed = CreateObject("TrazaMed")

' Establecer credenciales de seguridad
TrazaMed.Username = "testwservice"
TrazaMed.Password = "testwservicepsw"

' Conectar al servidor (pruebas)
ok = TrazaMed.Conectar()

' datos de prueba
usuario = "pruebasws": Password = "pruebasws"
f_evento = "25/11/2011": h_evento = "04:24"
gln_origen = "glnws": gln_destino = "glnws"
n_remito = "1234": n_factura = "1234"
vencimiento = "30/11/2011": gtin = "GTIN1": lote = "1111"
numero_serial = "12348": id_obra_social = "": id_evento = 133
cuit_origen = "20267565393": cuit_destino = "20267565393":
apellido = "Reingart": nombres = "Mariano"
tipo_docmento = "96": n_documento = "26756539": sexo = "M"
direccion = "Saraza": numero = "1234": piso = "": depto = ""
localidad = "Hurlingham": provincia = "Buenos Aires"
n_postal = "B1688FDD": fecha_nacimiento = "01/01/2000"
telefono = "5555-5555"

' Enviar datos y procesar la respuesta:
ok = TrazaMed.SendMedicamentos(usuario, Password, _
                     f_evento, h_evento, gln_origen, gln_destino, _
                     n_remito, n_factura, vencimiento, gtin, lote, _
                     numero_serial, id_obra_social, id_evento, _
                     cuit_origen, cuit_destino, apellido, nombres, _
                     tipo_docmento, n_documento, sexo, _
                     direccion, numero, piso, depto, localidad, provincia, _
                     n_postal, fecha_nacimiento, telefono)

Debug.Print "Resultado:", TrazaMed.Resultado
Debug.Print "CodigoTransaccion:", TrazaMed.CodigoTransaccion
    
For Each er In TrazaMed.Errores
     MsgBox er, vbExclamation, "Error!"
Next
    
MsgBox "Resultado: " & TrazaMed.Resultado & vbCrLf & _
        "CodigoTransaccion: " & TrazaMed.CodigoTransaccion, _
        vbInformation, "Resultado"

```

Ejemplo para anular una transacción de trazabilidad de medicamentos:
```
#!vb

' Cancelo la transacción (anulación):
codigo_transaccion = TrazaMed.CodigoTransaccion
ok = TrazaMed.SendCancelacTransacc(usuario, password, codigo_transaccion)
MsgBox "Resultado: " & TrazaMed.Resultado & vbCrLf & _
       "CodigoTransaccion: " & TrazaMed.CodigoTransaccion, _
       vbInformation, "SendCancelacTransacc"
```

Ejemplo de consulta de transacciones de trazabilidad de medicamentos (v2):
```
#!vb

' llamo al webservice para realizar la consulta:
ok = TrazaMed.GetTransaccionesNoConfirmadas(usuario, password, _
        p_id_transaccion_global, id_agente_informador, _
        id_agente_origen, id_agente_destino, id_medicamento, _
        id_evento, fecha_desde_op, fecha_hasta_op, _
        fecha_desde_t, fecha_hasta_t, _
        fecha_desde_v, fecha_hasta_v, _
        n_remito, n_factura, estado)
' recorro las transacciones devueltas (TransaccionPlainWS)
Do While TrazaMed.LeerTransaccion:
    If MsgBox("GTIN:" & TrazaMed.GetParametro("gtin") & vbCrLf & _
              "Estado: " & TrazaMed.GetParametro("estado") & vbCrLf & _
              "CodigoTransaccion: " & TrazaMed.GetParametro("id_transaccion"), _
              vbInformation + vbOKCancel, "GetTransaccionesNoConfirmadas") = vbCancel Then
        Exit Do
    End If
Loop
```


Ejemplo de confirmación de transacciones de trazabilidad de medicamentos (v2):
```
#!vb
' Confirmo la transacción
p_ids_transac = "5142760" ' TrazaMed.CodigoTransaccion
f_operacion = CStr(Date)  ' ej. 25/02/2013
ok = TrazaMed.SendConfirmaTransacc(usuario, password, _
                                   p_ids_transac, f_operacion)
If ok Then
    MsgBox "Resultado: " & TrazaMed.Resultado & vbCrLf & _
           "CodigoTransaccion: " & TrazaMed.CodigoTransaccion, _
           vbInformation, "SendConfirmaTransacc"
    For Each er In TrazaMed.Errores
        MsgBox er, vbExclamation, "Error en SendConfirmaTransacc"
    Next
End If
```
### Intefase COM en VFP 9

```

*-- Crear objeto interface COM
TrazaMed = CREATEOBJECT("TrazaMed") 
    
*-- Establecer credenciales de seguridad
TrazaMed.Username = "testwservice"
TrazaMed.Password = "testwservicepsw"

*-- Conectar al servidor (pruebas)
ok = TrazaMed.Conectar()

*-- datos de prueba
usuario = "pruebasws" 
password = "pruebasws"
f_evento = "25/11/2011"
h_evento = "04;24"
gln_origen = "glnws"
gln_destino = "glnws"
n_remito = "1234"
n_factura = "1234"
vencimiento = "30/11/2011"
gtin = "GTIN1"
lote = "1111"
numero_serial = "12349"
id_obra_social = ""
id_evento = 133

*-- Establezco parámetros adicionales:

ok = TrazaMed.SetParametro("nro_asociado", "9999999999999")

*-- Enviar datos y procesar la respuesta:
ok = ""
ok = TrazaMed.SendMedicamentos(usuario, password, ;
                     f_evento, h_evento, gln_origen, gln_destino, ;
                     n_remito, n_factura, vencimiento, gtin, lote, ;
                     numero_serial, id_obra_social, id_evento ;
				     )
```
## Entrenamiento

**IMPORTANTE**: Solo usuarios habilitados. Consultar con técnicos de PAMI/ANMAT: [contactotrazabilidad@pami.org.ar](mailto:contactotrazabilidad@pami.org.ar) y [trazabilidad@anmat.gov.ar](mailto:trazabilidad@anmat.gov.ar)

Para la Pruebas de Servicios (desarrollo) debe utilizar las siguientes credenciales (ver [Paso 1 ANMAT SNT](http://anmat.servicios.pami.org.ar/paso1.tiz)):

- Usuario: pruebasws
- Contraseña: Clave1234
- GLN de usuario de Prueba: glnw
- URL: https://servicios.pami.org.ar/trazamed.WebService
- Descripción de capacidades: https://servicios.pami.org.ar/trazamed.WebService?wsdl
- [Set de datos](http://anmat.servicios.pami.org.ar/pdfs/set_de_datos.pdf)

Para poder realizar la trazabilidad de medicamentos a través del !WebService, deberá antes realizar
el entrenamiento con datos ejemplo que lo ayudarán a comprender y probar el funcionamiento
del servicio (ver [Paso 2 ANMAT SNT](http://anmat.servicios.pami.org.ar/paso2.tiz)).

Deberá utilizar en esta etapa el usuario, contraseña y GLN asignado en la registración en el
modo de entrenamiento por la web de https://servicios.pami.org.ar/trazamed/registro.tz

Para el entorno de producción (definitivo) registrarse en https://trazabilidad.pami.org.ar/trazamed/registro.tz

Los siguientes son los eventos que deberá realizar a través del webservice. Previamente deberá
cumplimentar los pasos de entrenamiento descriptos en la página de trazabilidad. Tenga en
cuenta que siempre podrá ver el estado actual de su entrenamiento ingresando a la opción
Agentes / Mi puntuación.

 1. Debe informar un lote de 20 productos recibidos desde un eslabón anterior.
 2. Debe informar un lote de 20 productos como entrega de producto en carácter de devolución.
 3. Debe informar un lote de 20 productos como robados / extraviados.
 4. Debe informar un lote de 20 productos como vencidos.
 5. Debe informar un lote de 8 productos como DEVOLUCION POR PROHIBICION.

Ver también [Instructivo Farmacias](http://www.anmat.gov.ar/trazabilidad/docs/Manual_Trazabilidad_VF-Farmacias-130212.pdf)
### Agentes de prueba

| **GLN** | **Tipo de Agente** |
|---|---|
| GLNWS | LABORATORIO |
| 9999999999918 | Laboratorio |
| 9999999999925 | Distribuidora |
| 9999999999932 | Operador Logístico |
| 9999999999949 | Droguería |
| 9999999999956 | Farmacia |
| 9999999999963 | Establecimiento Asistencial |
| 9999999999970 | Laboratorio de Mezcla |

### Transacciones No Confirmadas

Según la documentación de la v2, el método !GetTransaccionesNoConfirmadas:

- *Trae un listado de las transacciones donde el agente es el destino y no están confirmadas por el agente receptor.*
- *El usuario (laboratorio/droguería/operador logístico/farmacia) mediante esta capacidad, puede ver todas las transacciones donde el es el destino, y no están confirmadas. Mediante este listado se obtienen los números de transacción individual (a nivel medicamento seriado) para poder invocar la capacidad de confirmar o alertar transaccion.*

A modo de ejemplo, se copia a continuación la tabla que devuelve la consulta de transacciones no confirmadas al 25 de febrero de 2012 en el ambiente de pruebas (resumida y simplificada por cuestiones de espacio):

| **_gtin** | **_lote** | **_numero_serial** | **_id_transaccion** | **_estado** | **_f_transaccion** | **_d_evento** | **_gln_origen** | **_gln_destino** |
|---|---|---|---|---|---|---|---|---|
| 07795360005385 | 412568 | 1200 | 5114793 | Informada | 19/02/2013 | ENVIO... | 9992105600005 | glnws |
| 07795347900511 | 412568 | 1200 | 5114796 | Informada | 19/02/2013 | ENVIO... | 9992105600005 | glnws |
| 00121231323232 | 412568 | 1200 | 5114798 | Informada | 19/02/2013 | ENVIO... | 9992105600005 | glnws |
| 55564646464645 | 412568 | 1200 | 5114801 | Informada | 19/02/2013 | ENVIO... | 9992105600005 | glnws |
| 55564646464645 | 412568 | 1200 | 5114806 | Informada | 19/02/2013 | ENVIO... | 9992105600005 | glnws |
| 07795349010010 | 412568 | 1200 | 5114808 | Informada | 19/02/2013 | ENVIO... | 9992105600005 | glnws |
| 07798113890290 | 412568 | 1200 | 5114810 | Informada | 19/02/2013 | ENVIO... | 9992105600005 | glnws |
| 07795349169589 | 412568 | 1200 | 5114813 | Informada | 19/02/2013 | ENVIO... | 9992105600005 | glnws |
| 77956464646464 | 412568 | 1200 | 5114815 | Informada | 19/02/2013 | ENVIO... | 9992105600005 | glnws |
| 07795349169190 | 412568 | 1200 | 5114818 | Informada | 19/02/2013 | ENVIO... | 9992105600005 | glnws |
| 07798144340010 | 412568 | 1200 | 5114821 | Informada | 19/02/2013 | ENVIO... | 9992105600005 | glnws |
| 07795384000021 | 412568 | 1200 | 5114824 | Informada | 19/02/2013 | ENVIO... | 9992105600005 | glnws |
| 07795368001228 | 12569 | 1201 | 5114851 | Informada | 19/02/2013 | ENVIO... | 9992105600005 | glnws |
| 07795347901006 | 12569 | 1001 | 5114855 | Informada | 19/02/2013 | ENVIO... | 9992105600005 | glnws |
| 07798112990151 | 12569 | 1200 | 5114858 | Informada | 19/02/2013 | ENVIO... | 9992105600005 | glnws |
| 07798112990304 | 12569 | 1200 | 5114866 | Informada | 19/02/2013 | ENVIO... | 9992105600005 | glnws |
| 07798112990281 | 12569 | 1200 | 5114868 | Informada | 19/02/2013 | ENVIO... | 9992105600005 | glnws |
| 07798112990335 | 12569 | 1200 | 5114873 | Informada | 19/02/2013 | ENVIO... | 9992105600005 | glnws |
| 08470008243426 | 68 | 121 | 5139846 | Informada | 25/02/2013 | ENVIO... | 7795366000001 | glnws |
| 08470008243426 | 68 | 135 | 5139860 | Informada | 25/02/2013 | ENVIO... | 7795366000001 | glnws |
| 08470008243426 | 68 | 134 | 5139859 | Informada | 25/02/2013 | ENVIO... | 7795366000001 | glnws |
| 07790375000295 | 2012 | 7790123456000 | 5140385 | Informada | 25/02/2013 | ENVIO... | 7798142290009 | glnws |
| 07790375000295 | 2012 | 7790123456001 | 5140386 | Informada | 25/02/2013 | ENVIO... | 7798142290009 | glnws |
| 07790375000295 | 2012 | 7790123456002 | 5140387 | Informada | 25/02/2013 | ENVIO... | 7798142290009 | glnws |
| 07795366452732 | 0015 | 1501 | 5141722 | Informada | 25/02/2013 | ENVIO... | 7795366000001 | glnws |
| 07795366452732 | 0015 | 1502 | 5141723 | Informada | 25/02/2013 | ENVIO... | 7795366000001 | glnws |
| 07795366452732 | 0015 | 1503 | 5141724 | Informada | 25/02/2013 | ENVIO... | 7795366000001 | glnws |
| 07795366454545 | 0206 | 5013 | 5142011 | Informada | 25/02/2013 | ENVIO... | 7795366000001 | glnws |
| 07795366454545 | 0206 | 5020 | 5142018 | Informada | 25/02/2013 | ENVIO... | 7795366000001 | glnws |
| 07795366454545 | 0206 | 5011 | 5142009 | Informada | 25/02/2013 | ENVIO... | 7795366000001 | glnws |
| 06554847518371 | 123456 | 1219 | 5142437 | Informada | 25/02/2013 | ENVIO... | 9992105600005 | glnws |
| 06554847518371 | 123456 | 1218 | 5142436 | Informada | 25/02/2013 | ENVIO... | 9992105600005 | glnws |
| 06554847518371 | 123456 | 1217 | 5142435 | Informada | 25/02/2013 | ENVIO... | 9992105600005 | glnws |
| 07795347000037 | 123456 | 1207 | 5142522 | Informada | 25/02/2013 | ENVIO... | 9992105600005 | glnws |
| 07795347000037 | 123456 | 1208 | 5142523 | Informada | 25/02/2013 | ENVIO... | 9992105600005 | glnws |
| 07795347000037 | 123456 | 1209 | 5142524 | Informada | 25/02/2013 | ENVIO... | 9992105600005 | glnws |
| 07749583345148 | 12345 | 1203 | 5142711 | Informada | 25/02/2013 | ENVIO... | 9992105600005 | glnws |
| 07749583345148 | 12345 | 1202 | 5142710 | Informada | 25/02/2013 | ENVIO... | 9992105600005 | glnws |
| 07749583345148 | 12345 | 1201 | 5142709 | Informada | 25/02/2013 | ENVIO... | 9992105600005 | glnws |
| 07795306206722 | 2000 | 7795123456000 | 5142759 | Informada | 25/02/2013 | ENVIO... | 7798142290009 | glnws |
| 07795306206722 | 2000 | 7795123456002 | 5142761 | Informada | 25/02/2013 | ENVIO... | 7798142290009 | glnws |
| 07795306206722 | 2000 | 7795123456003 | 5142762 | Informada | 25/02/2013 | ENVIO... | 7798142290009 | glnws |

Ver tabla completa adjuntada en: [trazamed_ej_pyafipws_transacciones_no_confirmadas.xls](attachment:trazamed_ej_pyafipws_transacciones_no_confirmadas.xls)

**Nota**: al momento de su evaluación, algunas transacciones listadas en esta tabla pueden estar ya confirmadas / alertadas o canceladas. Se recomiendo obtener una tabla actualizada (como se describe en las secciones previas) o consultarnos (ver soporte abajo).
## Errores

Fallas SOAP (!SoapFault) en atributo `Excepcion`:

- `soap:Server: La aplicacion usuario:"testwservice" intento ingresar con el password invalido:"testwservicepsw"`: verificar atributos `Username`, `Password` y url en `Conectar` (ambiente testing o producción)
- `soap:Server: La aplicacion usuario:"testwservice" no esta registrado en el sistema`: verificar atributos `Username`, `Password` y url en `Conectar` (ambiente testing o producción)
- `ns1:InvalidSecurity: An error was discovered processing the <wsse:Security> header`: ha proporcionado incorrectamente las credenciales de acceso o la biblioteca no soporta los encabezados de seguridad requeridos.
- `soap:Server: Error grave: null`: por lo visto, si no se especifica criterio de búsqueda o el criterio es muy amplio el webservice está devolviendo este error. En `GetTransaccionesWS` especificar al menos los parámetros de fechas (`fecha_desde_op` y `fecha_hasta_op`, ver [ejemplo completo en VB](https://code.google.com/p/pyafipws/source/browse/ejemplos/trazamed/trazamed.bas#260))

Errores Internos del webservice en atributo `Errores` (lista):

- `1: Error de autentificacion, verifique el usuario y/o contrase?a.`: verificar usuario y contraseña pasada al método `SendMedicamentos` (para testing es "pruebasws1" "pruebasws")
- `3014: No puede informar mas de una vez el mismo evento para el mismo número de serie.`: verifique los datos enviados (`numero_serial`), solo se puede enviar los requerimientos una vez.
- `No ha informado la recepcion del medicamento que desea enviar`: en ocasiones sucedía por una falla interna de los servidores, si se ha informado la recepción con !SendMedicamentos, consultar con los técnicos de PAMI/ANMAT: [contactotrazabilidad@pami.org.ar](mailto:contactotrazabilidad@pami.org.ar)
- `-20001: ORA-20001: ERROR al intentar guardar informacion de auditoria: ORA-01653: no se ha podido ampliar la tabla TRAZAMED.AU_WS_INFORM_AGENTE con 8192 en el tablespace TS_DATA` `-06512: en "TRAZAMED.TR_AU_WS_INFORME_AGENTE", línea 118` `ORA-04088: error durante la ejecución del disparador 'TRAZAMED.TR_AU_WS_INFORME_AGENTE' TRYVADA 30 CMPR REC serie: 1300178000` son errores internos del servidor de ANMAT, suele solucionarse automáticamente (reportado 9 de mayo de 2013)

El atributo Errores contendrá una lista con el código y mensaje de error devuelto por el webservice, se puede recorrer uno a uno:

```
#!vb

' recorro y muestro los errores
For Each er In TrazaMed.Errores
    MsgBox er, vbExclamation, "Error"
Next
```


Se puede recorrer la lista o llamar a !LeerError() que irá devolviendo cada error uno por uno, retornando cadena vacía al finalizar, ejemplo:

```
#!vb

' obtengo el error (si hay)
er = TrazaMed.LeerError()
Do While er <> ""
    MsgBox er, vbExclamation, "Error"
    er = TrazaMed.LeerError()   ' obtengo el proximo error (si hay)
Next
```

Errores frecuentes para !SendMedicamentos (en general, revisar código de operación, datos del medicamento, etc.):

- 3023: No se puede informar envios o recepciones entre un mismo agente GTIN: 000000000GTIN1 SERIE: ... 
- 2009: El campo GLN_DESTINO no tiene un formato valido. GTIN: 000000000GTIN1 SERIE: ...  
- 3022: El campo numero serial no tiene un valor correcto, verifiquelo. GTIN: 000000000GTIN1 SERIE: ... 
- 2009: El campo GLN_DESTINO no tiene un formato valido. GTIN: 000000000GTIN1 SERIE: ... 
- 3021: El medicamento que desea recibir ya lo informo como recibido. 
- 3010: El gln origen o el gln destino debe corresponderse con el gln del agente asignado a su usuario. verifiquelo. GTIN: 000000000GTIN1 SERIE: ...
- 3019 No ha informado la recepcion del medicamento que desea enviar. 

Errores de formato (ahora usar letra + 4 dígitos punto de venta + 8 digitos numero de comprobante, ejemplo: "A000100000001")

- 2038: El campo N_REMITO no tiene la longitud deseada. [13](Long:)
- 2039: El campo N_FACTURA no tiene la longitud deseada. [13](Long:)
- 2039: El campo nro factura no tiene un valor valido.

Ejemplos para los métodos de confirmación:

- 3: Transaccion NO encontrada, NO se puede anular. (en !SendCancelacTransacc)
- 10001: El ID de Transaccion indicado no existe. No es posible Confirmar la misma. (en !SendConfirmaTransacc)
- 10001: El ID de Transaccion indicado no existe. No es posible Alertar la misma. (en !SendAlertaTransacc)

## Novedades

Se recuerda que esta disponible el 
[grupo de noticias](http://www.pyafipws.com.ar) (http://groups.google.com.ar/group/pyafipws) donde
se publicarán futuras novedades sobre PyAfipWS: servicios web de
factura electrónica y sus interfases (se recomienda suscribirse)

Historial de cambios:

- Mayo de 2014: Se agregan metodos `GetTransaccionesWS` y `GetCatalogoElectronicoByGTIN`.
- Febrero de 2014: Se agregan cambios por actualización de especificación técnica ANMAT al 30/01/2014 (método `GetTransaccionesNoConfirmadas`: nuevos parametros lote, numero_serial, y respuesta con _id_estado en TransaccionPlainWS)
- Septiembre de 2013: Se agregan archivos de intercambio (dbf, txt, json) y métodos v2: `SendCancelacTransaccParcial` y `GetEnviosPropiosAlertados`
- Febrero de 2013: Se agrega v2: `SendConfirmaTransacc`, `SendAlertaTransacc` y `GetTransaccionesNoConfirmadas`
- Agosto de 2012: Se agrega `SendMedicamentosFraccion` para enviar `cantidad`
- Agosto de 2012: Se agrega `nro_asociado` para enviar el numero de afiliado a la obra social
- Junio de 2012: Se agrega soporte para librería de tipos (!TypeLib o TLB)
- Mayo de 2012: Se agrega soporte para Visual Fox Pro
- Enero de 2011: Mejoras en la captura de errores
- Diciembre de 2011: Se agrega `SendCancelacTransacc` y `SendMedicamentosDHSerie`
- Noviembre de 2011: Versión inicial

Implementación del sistema de trazabilidad para productos críticos:

Etapa 1: 

- Desde LABORATORIO hasta DROGUERIA: Hasta SEIS (6) MESES a partir del 15/06/2011 
- Desde DROGUERIA hasta FARMACIA: Hasta SEIS (6) MESES a partir del 15/06/2011 

Etapa 2: VALIDACION DEL SISTEMA desde: 

- LABORATORIO TITULAR  DISTRIBUIDORA  DROGUERIA  FARMACIA/ESTABLECIMIENTO ASISTENCIAL  PACIENTE: Hasta DOCE (12) MESES a partir del 15/06/2011

### IDL y TLB (libreria de tipos) para lenguajes estáticos

Liberamos una  versión del instalador para Trazabilidad de ANMAT con el archivo !TrazaMed.TLB (Type Library)para usar en Clarion y otros lenguajes estáticos:

http://www.sistemasagiles.com.ar/soft/pyafipws/instalador-TrazaMed-1.05a-tlb-homo.exe

Luego de instalar, deben registrar el tlb ejecutando
```
C:\Archivos de Programa\TrazaMed\TrazaMed.EXE --register
```
El IDL fuente está publicado en:

https://github.com/reingart/pyafipws/blob/master/typelib

IMPORTANTE: el TLB no sirve para la versión normal previa, solo se
debe usar con este instalador y viceversa.

Si lo usan con Visual Basic, deben ir a Referencias y agregar el
archivo TLB, y luego cambiar la definición:
```
Dim TrazaMedObj As TrazaMed
```
La única diferencia con la versión estandard sin TLB, es que se activa
el autocompletado y tips de llamadas (información de metodos y
parámetros estáticos), pero no hay parámetros opcionales (deben
completarlos con string vacios "") y se pierde las funcionalidades
dinámicas (deben pasar practicamente todo como string)

## Costos y Condiciones

Por soporte comercial consultar al (011) 15-3048-9211 o por mail a info@sistemasagiles.com.ar

Costos de soporte estimativos (puede variar dependiendo de las necesidades de cada implementación puntual):

- Soporte mínimo: $49.680.- (por 1 semana de cobertura), sólo acceso a instalador y soporte por temas de instalación únicamente, no incluye consultas generales o ajustes. (prefentemente para clientes actuales)
- Soporte básico: $131.100.- (hasta 6 hs en total por 1 mes máx.), incluye consultas particulares y ajustes menores, contemplando TLB (TypeLib para lenguajes estáticos -solo TrazaMed, consultar otros WS-)
- Soporte avanzado: $196.650.- (hasta 9hs en total por 3 meses máx.) adicional, incluyendo ajustes y desarrollo de ejemplos, documentación, pruebas, etc., contempla temas urgentes y/o grandes empresas/ciclos de desarrollo
- Soporte por actualización: desde $49.680 (1 semana máx., hasta 1 hs en total, solo instalación y acceso a actualizaciones por correcciones generales), aplica a la versión 2 para clientes previos.

Para soporte sin cargo de la comunidad, revisar la [lista de temas](https://github.com/reingart/pyafipws/issues) y/o [crear uno nuevo](https://github.com/reingart/pyafipws/issues/new). 
Por novedades y consultas genereales, puede usar el  [Google Groups](https://groups.google.com/forum/#!forum/pyafipws) (Foro Público).
Código fuente en [GitHub](https://github.com/reingart/pyafipws/).


Más información en PyAfipWs

MarianoReingart
MarianoReingart
MarianoReingart
MarianoReingart