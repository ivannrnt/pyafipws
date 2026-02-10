= Trazabilidad de Productos Agroquímicos Fitosanitarios/Veterinarios - WS !TrazaAgr !TrazaVet SENASA PAMI SNT =

[[TracNav(noreorder|FacturaElectronica)]]

Interfaz para Servicio Web Código de Trazabilidad de Productos Fitosanitarios / Veterinarios (SOAP) correspondiente a la [Resolución 369/2013](http://www.senasa.gov.ar/contenido.php?to=n&in=1592&io=24640) del Servicio Nacional de Sanidad y Calidad Agroalimentaria (SENASA) que contemplan en su composición en principio los Principios Activos incluidos en el Anexo I. Sistema Nacional de Trazabilidad.


## Índice
[[TOC(noheading,inline,depth=2)]]

## Introducción

Biblioteca para el web service de SENASA/PAMI que permite automatizar la gestión de las trazabilidad de productos fitosanitarios: 

- Interfaz COM: Simil DLL/OCX, embebible para aplicaciones programadas en lenguajes visuales bajo windows (Visual Basic, Visual Fox Pro, SAP, etc.)
- Interfaz por consola (linea de comandos / archivo de texto): similar a aplicativos SIAP para sistemas legados (ej. RM COBOL) multiplataforma (DOS, Windows, Unix)
- Interfaz por tablas DBF: compatible con dBase, !FoxPro, Clipper -proximamente-
- Interfaz por base de datos: compatible con conectores ODBC (MS SQL Server), PostgreSQL y otros (Oracle, DB2) -proximamente-

Cubre totalmente el proceso, puede ser adaptado a programas existentes y no es requerido intervención del usuario.

Para más información ver PyAfipWs


## Descargas

- Instalador: 
- [instalador-PyAfipWs-2.33a-32bit+trazafito_1.11a-homo.exe](http://www.sistemasagiles.com.ar/soft/pyafipws/instalador-PyAfipWs-2.33a-32bit+trazafito_1.11a-homo.exe) para productos fitosanitarios
- [instalador-PyAfipWs-2.33a-32bit+trazavet_1.11c-homo.exe](http://www.sistemasagiles.com.ar/soft/pyafipws/instalador-PyAfipWs-2.33a-32bit+trazavet_1.11c-homo.exe) para productos veterinarios 
- Documentación Oficial: (especificación técnica original)
- [fitosanitarios](http://senasa.servicios.pami.org.ar/pdfs/especificacion_tecnica_fito.pdf)
- [veterinarios](http://senasa.servicios.pami.org.ar/pdfs/especificacion_tecnica_vet.pdf)
- Ejemplo en VB: [trazafito.bas](https://github.com/reingart/pyafipws/blob/master/ejemplos/trazafito/trazafito.bas) [(ver)](https://github.com/reingart/pyafipws/blob/master/ejemplos/trazafito/trazafito.prg)
- Ejemplo en VFP: [trazafito.prg](https://github.com/reingart/pyafipws/blob/master/ejemplos/trazafito/trazafito.prg) [(ver)](https://github.com/reingart/pyafipws/blob/master/ejemplos/trazafito/trazafito.prg)
- Código Fuente (Python): [trazafito.py](https://github.com/reingart/pyafipws/blob/master/trazafito.py)

URL:

- Entrenamiento: https://servicios.pami.org.ar/trazaenagr.WebService?wsdl / https://servicios.pami.org.ar/trazaenvet.WebService?wsdl
- Producción: https://servicios.pami.org.ar/trazaagr.WebService?wsdl / https://servicios.pami.org.ar/trazavet.WebService?wsdl

## Métodos

- **`GetTransacciones(usuario, password, id_transaccion, id_evento, gln_origen, fecha_desde_t, fecha_hasta_t, fecha_desde_v, fecha_hasta_v, gln_informador, id_tipo_transaccion, gtin_elemento, n_lote, n_serie, n_remito_factura)`**: Trae un listado de las transacciones donde el agente es el destino, siempre y cuando no las haya confirmado todavía. Ver estructura !Transacciones para los parámetros de salida.
- **`SaveTransaccion(usuario, password, gln_origen, gln_destino, f_operacion, f_elaboracion, f_vto,  id_evento, cod_producto, n_cantidad, n_serie, n_lote, n_cai, n_cae, id_motivo_destruccion, n_manifiesto, en_transporte, n_remito, motivo_devolucion, observaciones, n_vale_compra, apellidoNombres, direccion, numero, localidad, provincia, n_postal, cuit))`**: Realiza el registro de un movimiento o evento (utilizado para todos los movimientos excepto para las recepciones de mercadería). Ver estructura !TransaccionDTO para los parametros de entrada.
- **`SendConfirmaTransacc(usuario, password, p_ids_transac, f_operacion, n_cantidad)`**:  Confirma la recepción de un producto y de esa manera registra una recepción de mercadería desde otra sucursal o empresa.
- **`SendAlertaTransacc(usuario, usuario, password, p_ids_transac_ws)`**:  Alerta un producto, acción contraria a "confirmar la transacción".
- **`SendCancelaTransac(usuario, password, codigo_transaccion)`**:  Realiza la cancelación de una transacción

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
- `XmlRequest`, `XmlResponse`: mensajes xml crudos sin procesar (para depuración)
- `Version`, `InstallDir`: datos para depuración
- `Traceback`, `Excepcion`: errores no esperados de comunicación o similar (por ej. !SoapFault)


## Linea de Comandos

Para sistemas operativos legados (DOS bajo windows) y UNIX/Linux, es posible operar la herramienta de trazabilidad por consola. Recibe como parámetros los datos correspondientes a la llamada remota (ver métodos). Opcionalmente se puede especificar --testing para pruebas (usar xml de muestra como respuesta si no se tiene acceso a homologación) y --trace para imprimir por pantalla los datos enviados y recibidos.

**Nota**: dependiendo de la compilación y el instalador, el ejecutable puede ser **`TRAZAFITO_CLI.EXE`**

Si no se específican los campos por linea de comando, de manera predeterminada se utilizará el formato de texto
Para usar Tablas DBF agregar a la linea de comandos el parámetro `--dbf`. 
Para soporte de JSON (JavaScript Object Notation), agregar parametro `--json`.
Se debe anteponer `--cargar` y `--grabar` para leer y escribir los datos en los archivos de intercambio.


Ejemplo de uso para registrar la transacción de un producto (por defecto recibe los argumentos según el método !SaveTransaccion, si se pasa --test utiliza datos de pruebas).
```
C:\PYSENASA>TRAZAFITO.EXE --test "senasaws" "Clave2013"
Procesando registro 0
|Resultado  True|CodigoTransaccion   14905502|Errores||
```

Ejemplo para obtener las transacciones no confirmadas:

```
C:\PYSENASA>TRAZAFITO.EXE --consulta "senasaws" "Clave2013" | less
CantPaginas 1
HayError None

CantPaginas 1
HayError None
| id_transaccion_global | id_transaccion | f_transaccion | f_operacion | f_vencimiento | f_elaboracion | d_evento | n_cantidad | id_unidad | d_unidad | cod_producto | .... |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 14904794 | 33681508 | 2014-05-16 00:00:00 | 2014-05-10 00:00:00 |  |  | Venta/Envío |  |  |  | 88900000000001 | ... |
| 14904796 | 33681509 | 2014-05-16 00:00:00 | 2014-05-10 00:00:00 |  |  | Venta/Envío |  |  |  | 88900000000001 | ... |
...
```

Ejemplo de uso para confirmar una transacción (recibe usuario, password, número de transacción y fecha de operación):

```
C:\PYSENASA>TRAZAFITO.EXE --confirma "senasaws" "Clave2013" "33681506" "17/05/2014"
|Resultado  True|CodigoTransaccion       None|Errores||
```


Ejemplo de uso para alertar una transacción (recibe usuario, password, número de transacción):

```
C:\PYSENASA>TRAZAFITO.EXE --alerta "senasaws" "Clave2013" 33681507
|Resultado  True|CodigoTransaccion       None|Errores||
```

Ejemplo de uso para cancelar una transacción (recibe usuario, password, número de transacción):

```
C:\PYSENASA>TRAZAFITO.EXE --cancela  "senasaws" "Clave2013" 15273619
|Resultado  True|CodigoTransaccion   15273640|Errores||
```
## Archivos de Intercambio

Formato:

- Transacción DTO: utilizado por !SaveTransaccion (ver ejemplo [transacciondto.txt](attachment:transacciondto.txt))
- Transacciones: devuelto por !GetTransacciones (ver ejemplo [transaciones.txt](attachment:transacciones.txt))

### TransaccionDTO
| **Nombre** | **Tipo** | **Long.** | **Pos(txt)** | **Campo(dbf)** |
|---|---|---|---|---|
| gln_origen | Alfanumerico | 13 | 1 | glnorigen |
| gln_destino | Alfanumerico | 13 | 14 | glndestino |
| f_operacion | Alfanumerico | 10 | 27 | foperacion |
| f_elaboracion | Alfanumerico | 10 | 37 | felaboraci |
| f_vto | Alfanumerico | 10 | 47 | fvto |
| id_evento | Numerico | 15 | 57 | idevento |
| cod_producto | Alfanumerico | 14 | 72 | codproduct |
| n_cantidad | Numerico | 30 | 86 | ncantidad |
| n_serie | Alfanumerico | 20 | 116 | nserie |
| n_lote | Alfanumerico | 50 | 136 | nlote |
| n_cai | Alfanumerico | 15 | 186 | ncai |
| n_cae | Alfanumerico | 15 | 201 | ncae |
| id_motivo_destruccion | Alfanumerico | 5 | 216 | idmotivode |
| n_manifiesto | Numerico | 15 | 221 | nmanifiest |
| en_transporte | Alfanumerico | 1 | 236 | entranspor |
| n_remito | Alfanumerico | 15 | 237 | nremito |
| motivo_devolucion | Alfanumerico | 100 | 252 | motivodevo |
| observaciones | Alfanumerico | 1000 | 352 | observacio |
| n_vale_compra | Alfanumerico | 15 | 1352 | nvalecompr |
| apellidoNombres | Alfanumerico | 255 | 1367 | apellidono |
| direccion | Alfanumerico | 200 | 1622 | direccion |
| numero | Numerico | 6 | 1822 | numero |
| localidad | Alfanumerico | 15 | 1828 | localidad |
| provincia | Alfanumerico | 15 | 1843 | provincia |
| n_postal | Alfanumerico | 8 | 1858 | npostal |
| cuit | Alfanumerico | 11 | 1866 | cuit |
| codigo_transaccion | Alfanumerico | 14 | 1877 | codigotran |
### Transacciones
| **'Nombre** | **Tipo** | **Long.** | **Pos(txt)** | **Campo(dbf)** |
|---|---|---|---|---|
| id_transaccion_global | Numerico | 15 | 1 | idtransacc |
| id_transaccion | Numerico | 15 | 16 | idtransac1 |
| f_transaccion | Alfanumerico | 10 | 31 | ftransacci |
| f_operacion | Alfanumerico | 10 | 41 | foperacion |
| f_vencimiento | Alfanumerico | 10 | 51 | fvencimien |
| f_elaboracion | Alfanumerico | 10 | 61 | felaboraci |
| d_evento | Alfanumerico | 100 | 71 | devento |
| n_cantidad / cantidad | Numerico | 30 | 171 | cantidad |
| id_unidad | Numerico | 15 | 201 | idunidad |
| d_unidad | Alfanumerico | 100 | 216 | dunidad |
| cod_producto | Alfanumerico | 14 | 316 | codproduct |
| id_unidad | Numerico | 15 | 330 | idunidad1 |
| n_serie | Alfanumerico | 20 | 345 | nserie |
| n_lote | Alfanumerico | 50 | 365 | nlote |
| n_cai | Alfanumerico | 15 | 415 | ncai |
| n_cae | Alfanumerico | 15 | 430 | ncae |
| d_motivo_destruccion | Alfanumerico | 50 | 445 | dmotivodes |
| d_manifiesto | Alfanumerico | 15 | 495 | dmanifiest |
| en_transporte | Alfanumerico | 1 | 510 | entranspor |
| n_remito | Alfanumerico | 30 | 511 | nremito |
| motivo_devolucion | Alfanumerico | 200 | 541 | motivodevo |
| observaciones | Alfanumerico | 1000 | 741 | observacio |
| n_vale_compra | Alfanumerico | 15 | 1741 | nvalecompr |
| apellidoNombres | Alfanumerico | 255 | 1756 | apellidono |
| direccion | Alfanumerico | 200 | 2011 | direccion |
| numero | Alfanumerico | 6 | 2211 | numero |
| localidad | Alfanumerico | 250 | 2217 | localidad |
| provincia | Alfanumerico | 250 | 2467 | provincia |
| n_postal | Alfanumerico | 8 | 2717 | npostal |
| cuit | Alfanumerico | 11 | 2725 | cuit |
| d_agente_informador | Alfanumerico | 255 | 2736 | dagenteinf |
| d_agente_origen | Alfanumerico | 255 | 2991 | dagenteori |
| d_agente_destino | Alfanumerico | 255 | 3246 | dagentedes |
| d_producto | Alfanumerico | 250 | 3501 | dproducto |
| d_estado_transaccion | Alfanumerico | 30 | 3751 | destadotra |
| d_tipo_transaccion | Alfanumerico | 30 | 3781 | dtipotrans |
### Errores
| **Nombre** | **Tipo** | **Long.** | **Pos(txt)** | **Campo(dbf)** |
|---|---|---|---|---|
| _c_error | Alfanumerico | 4 | 1 | cerror |
| _d_error | Alfanumerico | 250 | 5 | derror |


## Ejemplos

### Intefase COM en VB (5/6)

Registro de transacción de trazabilidad de productos fitosanitarios:
```
#!vb
' datos de prueba
usuario = "senasaws"
password = "Clave2013"

gln_origen = "9876543210982"
gln_destino = "3692581473693"
f_operacion = CStr(Date) ' DD/MM/AAAA
f_elaboracion = CStr(Date) ' DD/MM/AAAA
f_vto = CStr(Date + 30) ' DD/MM/AAAA
id_evento = 11
cod_producto = "88900000000001" ' ABAMECTINA
n_cantidad = 1
n_lote = "2014"
n_serie = "12345678" ' Ejemplo
n_cai = "123456789012345"
n_cae = ""
id_motivo_destruccion = 0
n_manifiesto = ""
en_transporte = "N"
n_remito = "1234"
motivo_devolucion = ""
observaciones = "prueba"
n_vale_compra = ""
apellidoNombres = "Juan Peres"
direccion = "Saraza"
numero = "1234"
localidad = "Hurlingham"
provincia = "Buenos Aires"
n_postal = "1688"
cuit = "20267565393"

ok = TrazaFito.SaveTransaccion(usuario, password, _
                    gln_origen, gln_destino, _
                    f_operacion, f_elaboracion, f_vto, _
                    id_evento, cod_producto, n_cantidad, _
                    n_serie, n_lote, n_cai, n_cae, _
                    id_motivo_destruccion, n_manifiesto, _
                    en_transporte, n_remito, _
                    motivo_devolucion, observaciones, _
                    n_vale_compra, apellidoNombres, _
                    direccion, numero, localidad, _
                    provincia, n_postal, cuit _
                     )
MsgBox "Resultado: " & TrazaFito.Resultado & vbCrLf & _
        "CodigoTransaccion: " & TrazaFito.CodigoTransaccion, _
        vbInformation, "SaveTransacciones"
```


Ejemplo de consulta de transacciones de trazabilidad de productos fitosanitarios:
```
#!vb
' llamo al webservice para realizar la consulta:
ok = TrazaFito.GetTransacciones(usuario, password)
If ok Then
    ' recorro las transacciones devueltas (TRANSACCIONES)
    Do While TrazaFito.LeerTransaccion:
        If MsgBox("GTIN:" & TrazaFito.GetParametro("cod_producto") & vbCrLf & _
                "Evento: " & TrazaFito.GetParametro("d_evento") & vbCrLf & _
                "CodigoTransaccion: " & TrazaFito.GetParametro("id_transaccion"), _
                vbInformation + vbOKCancel, "GetTransacciones") = vbCancel Then
            Exit Do
        End If
        Debug.Print TrazaFito.GetParametro("cod_producto")
        Debug.Print TrazaFito.GetParametro("f_operacion")
        Debug.Print TrazaFito.GetParametro("f_transaccion")
        Debug.Print TrazaFito.GetParametro("d_estado_transaccion")
        Debug.Print TrazaFito.GetParametro("n_lote")
        Debug.Print TrazaFito.GetParametro("n_serie")
        Debug.Print TrazaFito.GetParametro("n_cantidad")
        Debug.Print TrazaFito.GetParametro("d_evento")
        Debug.Print TrazaFito.GetParametro("gln_destino")
        Debug.Print TrazaFito.GetParametro("gln_origen")
        Debug.Print TrazaFito.GetParametro("apellidoNombre")
        Debug.Print TrazaFito.GetParametro("id_transaccion_global")
        Debug.Print TrazaFito.GetParametro("id_transaccion")
        Debug.Print TrazaFito.GetParametro("n_remito")
    Loop
Else
    MsgBox TrazaFito.Traceback, vbCritical, TrazaFito.Excepcion
End If
```


Ejemplo de confirmación de transacciones de trazabilidad de productos fitosanitarios:
```
#!vb
f_operacion = CStr(Date)  ' ej. 25/02/2013
p_ids_transac = 15203916
ok = TrazaFito.SendConfirmaTransacc(usuario, password,p_ids_transac, f_operacion)
If ok Then
    MsgBox "Resultado: " & TrazaFito.Resultado & vbCrLf & _
            "CodigoTransaccion: " & TrazaFito.CodigoTransaccion, _
            vbInformation, "SendConfirmaTransacc"
    For Each er In TrazaFito.Errores
        Debug.Print er
        MsgBox er, vbExclamation, "Error en SendConfirmaTransacc"
    Next
Else
    Debug.Print TrazaFito.XmlResponse
    MsgBox TrazaFito.Traceback, vbExclamation, "Excepcion en SendConfirmaTransacc: " & TrazaFito.Excepcion
End If
```
### Intefase COM en VFP 9

*Proximamente (consultar)* 

## Entrenamiento

**IMPORTANTE**: Solo usuarios habilitados. Consultar con técnicos de SENASA/SNT

Para poder realizar la trazabilidad de medicamentos a través del !WebService, deberá antes realizar
el entrenamiento con datos ejemplo que lo ayudarán a comprender y probar el funcionamiento
del servicio.

Deberá utilizar en esta etapa el usuario, contraseña y GLN asignado en la registración en el
modo de entrenamiento por la web de [SENASA](http://senasa.servicios.pami.org.ar/)

A continuación se analiza el Set de Datos para Prueba de Servicios Fitosanitarios [set_de_datos_fito.pdf](http://senasa.servicios.pami.org.ar/pdfs/set_de_datos_fito.pdf) / Veterinarios [set_de_datos_vet.pdf](http://senasa.servicios.pami.org.ar/pdfs/set_de_datos_vet.pdf):

### Agentes de prueba

| **GLN** | **Tipo de Agente** |
|---|---|
| 9876543210982 | Importador |
| 3692581473693 | Fracciona. / Sintetizador / Elaborador |

### Eventos

Codificación:
| **Código** | **Descripción** |
|---|---|
| 1 | Importación |
| 2 | Liberación de Zona Franca |
| 3 | Exportación |
| 4 | Síntesis de Principio Activo |
| 5 | Uso para Producción de Productos |
| 6 | Producción de Productos |
| 7 | Uso para Fraccionamiento |
| 8 | Resultado de Fraccionamiento |
| 9 | Destrucción / Merma |
| 10 | Robo / Hurto |
| 11 | Venta / Envío |
| 13 | Venta a usuario (Venta minorista por CUIT) |
| 14 | Devolución |
| 16 | Recepción por Devolución Minorista |
| 17 | Producción con materia prima no trazada |
| 18 | Uso para autoconsumo |
| 19 | Importación a zona franca |
| 20 | Exportación desde zona franca |
| 21 | Envío a Comerciante No Inscripto en el Sistema |

**Importante**: para las pruebas con datos genéricos (importador), solo puede usar los eventos relacionados (11, 13), de lo contrario el webservice devolverá un error de validación `3010: El gln origen o el gln destino debe corresponderse con el gln del agente asignado A su usuario. verifiquelo.`. Para realizar el entrenamiento con datos reales debe tramitar un usuario y contraseña habilitado. 

### Unidades
| **Código** | **Detalle** |
|---|---|
| 1 | Kilogramos |
| 2 | Litros |

### Motivos Destrucción

| **Código** | **Detalle** |
|---|---|
| 1 | Vencimiento |
| 2 | Mal estado |
| 3 | Mala formulación |
| 4 | Siniestro |
| 5 | Muestra SENASA |
| 6 | Merma |

### Transacciones No Confirmadas

A modo de ejemplo, se copia a continuación la tabla que devuelve la consulta de transacciones no confirmadas al 17 de mayo de 2014 en el ambiente de pruebas (resumida y simplificada por cuestiones de espacio):

| **id_transaccion_global** | **id_transaccion** | **f_transaccion** | **f_operacion** | **d_evento** | **cod_producto** | **n_serie** | **n_lote** | **en_transporte** | **n_remito** | **d_agente_informador** | **d_agente_origen** | **d_agente_destino** | **d_producto** | **d_estado_transaccion** | **d_tipo_transaccion** |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 14904791 | 33681506 | 2014-05-16 | 2014-05-10 | Venta/Envío | 88900000000001 |  | 234 | N | 12345 | 9876543210982 - 1234567891019 | 9876543210982 - 1234567891019 | 9876543210982 - 1234567891019 | ABAMECTINA | Informada | Informe |
| 14904792 | 33681507 | 2014-05-16 | 2014-05-10 | Venta/Envío | 88900000000001 |  | 234 | N | 12345 | 9876543210982 - 1234567891019 | 9876543210982 - 1234567891019 | 9876543210982 - 1234567891019 | ABAMECTINA | Informada | Informe |
| 14904794 | 33681508 | 2014-05-16 | 2014-05-10 | Venta/Envío | 88900000000001 |  | 234 | N | 12345 | 9876543210982 - 1234567891019 | 9876543210982 - 1234567891019 | 9876543210982 - 1234567891019 | ABAMECTINA | Informada | Informe |
| 14904796 | 33681509 | 2014-05-16 | 2014-05-10 | Venta/Envío | 88900000000001 |  | 234 | N | 12345 | 9876543210982 - 1234567891019 | 9876543210982 - 1234567891019 | 9876543210982 - 1234567891019 | ABAMECTINA | Informada | Informe |
| 14904798 | 33681510 | 2014-05-16 | 2014-05-10 | Venta/Envío | 88900000000001 |  | 234 | N | 12345 | 9876543210982 - 1234567891019 | 9876543210982 - 1234567891019 | 9876543210982 - 1234567891019 | ABAMECTINA | Informada | Informe |
| 14904800 | 33681511 | 2014-05-16 | 2014-05-10 | Venta/Envío | 88900000000001 |  | 234 | N | 12345 | 9876543210982 - 1234567891019 | 9876543210982 - 1234567891019 | 9876543210982 - 1234567891019 | ABAMECTINA | Informada | Informe |
| 14904802 | 33681512 | 2014-05-16 | 2014-05-10 | Venta/Envío | 88900000000001 |  | 234 | N | 12345 | 9876543210982 - 1234567891019 | 9876543210982 - 1234567891019 | 9876543210982 - 1234567891019 | ABAMECTINA | Informada | Informe |
| 14904804 | 33681513 | 2014-05-16 | 2014-05-10 | Venta/Envío | 88900000000001 |  | 234 | N | 12345 | 9876543210982 - 1234567891019 | 9876543210982 - 1234567891019 | 9876543210982 - 1234567891019 | ABAMECTINA | Informada | Informe |
| 14904806 | 33681514 | 2014-05-16 | 2014-05-10 | Venta/Envío | 88900000000001 |  | 234 | N | 12345 | 9876543210982 - 1234567891019 | 9876543210982 - 1234567891019 | 9876543210982 - 1234567891019 | ABAMECTINA | Informada | Informe |
| 14904808 | 33681515 | 2014-05-16 | 2014-05-10 | Venta/Envío | 88900000000001 |  | 234 | N | 12345 | 9876543210982 - 1234567891019 | 9876543210982 - 1234567891019 | 9876543210982 - 1234567891019 | ABAMECTINA | Informada | Informe |
| 14904810 | 33681516 | 2014-05-16 | 2014-05-10 | Venta/Envío | 88900000000001 |  | 234 | N | 12345 | 9876543210982 - 1234567891019 | 9876543210982 - 1234567891019 | 9876543210982 - 1234567891019 | ABAMECTINA | Informada | Informe |
| 14904812 | 33681517 | 2014-05-16 | 2014-05-10 | Venta/Envío | 88900000000001 |  | 234 | N | 12345 | 9876543210982 - 1234567891019 | 9876543210982 - 1234567891019 | 9876543210982 - 1234567891019 | ABAMECTINA | Informada | Informe |
| 14904814 | 33681518 | 2014-05-16 | 2014-05-10 | Venta/Envío | 88900000000001 |  | 234 | N | 12345 | 9876543210982 - 1234567891019 | 9876543210982 - 1234567891019 | 9876543210982 - 1234567891019 | ABAMECTINA | Informada | Informe |
| 14904816 | 33681519 | 2014-05-16 | 2014-05-10 | Venta/Envío | 88900000000001 |  | 234 | N | 12345 | 9876543210982 - 1234567891019 | 9876543210982 - 1234567891019 | 9876543210982 - 1234567891019 | ABAMECTINA | Informada | Informe |
| 14904818 | 33681520 | 2014-05-16 | 2014-05-10 | Venta/Envío | 88900000000001 |  | 234 | N | 12345 | 9876543210982 - 1234567891019 | 9876543210982 - 1234567891019 | 9876543210982 - 1234567891019 | ABAMECTINA | Informada | Informe |
| 14904820 | 33681521 | 2014-05-16 | 2014-05-10 | Venta/Envío | 88900000000001 |  | 234 | N | 12345 | 9876543210982 - 1234567891019 | 9876543210982 - 1234567891019 | 9876543210982 - 1234567891019 | ABAMECTINA | Informada | Informe |
| 14904822 | 33681522 | 2014-05-16 | 2014-05-10 | Venta/Envío | 88900000000001 |  | 234 | N | 12345 | 9876543210982 - 1234567891019 | 9876543210982 - 1234567891019 | 9876543210982 - 1234567891019 | ABAMECTINA | Informada | Informe |
| 14904824 | 33681523 | 2014-05-16 | 2014-05-10 | Venta/Envío | 88900000000001 |  | 234 | N | 12345 | 9876543210982 - 1234567891019 | 9876543210982 - 1234567891019 | 9876543210982 - 1234567891019 | ABAMECTINA | Informada | Informe |
| 14904826 | 33681524 | 2014-05-16 | 2014-05-10 | Venta/Envío | 88900000000001 |  | 234 | N | 12345 | 9876543210982 - 1234567891019 | 9876543210982 - 1234567891019 | 9876543210982 - 1234567891019 | ABAMECTINA | Informada | Informe |
| 14904828 | 33681525 | 2014-05-16 | 2014-05-10 | Venta/Envío | 88900000000001 |  | 234 | N | 12345 | 9876543210982 - 1234567891019 | 9876543210982 - 1234567891019 | 9876543210982 - 1234567891019 | ABAMECTINA | Informada | Informe |
| 14904830 | 33681526 | 2014-05-16 | 2014-05-10 | Venta/Envío | 88900000000001 |  | 234 | N | 12345 | 9876543210982 - 1234567891019 | 9876543210982 - 1234567891019 | 9876543210982 - 1234567891019 | ABAMECTINA | Informada | Informe |
| 14904831 | 33681527 | 2014-05-16 | 2014-05-10 | Venta/Envío | 88900000000001 |  | 234 | N | 12345 | 9876543210982 - 1234567891019 | 9876543210982 - 1234567891019 | 9876543210982 - 1234567891019 | ABAMECTINA | Informada | Informe |

**Nota**: al momento de su evaluación, algunas transacciones listadas en esta tabla pueden estar ya confirmadas / alertadas o canceladas. Se recomiendo obtener una tabla actualizada (como se describe en las secciones previas) o consultarnos (ver soporte abajo).


## Errores

Fallas SOAP (!SoapFault) en atributo `Excepcion`:

- `soap:Server: La aplicacion usuario:"testwservice" intento ingresar con el password invalido:"testwservicepsw"`: verificar atributos `Username`, `Password` y url en `Conectar` (ambiente testing o producción)
- `soap:Server: La aplicacion usuario:"testwservice" no esta registrado en el sistema`: verificar atributos `Username`, `Password` y url en `Conectar` (ambiente testing o producción)
- `ns1:InvalidSecurity: An error was discovered processing the <wsse:Security> header`: ha proporcionado incorrectamente las credenciales de acceso o la biblioteca no soporta los encabezados de seguridad requeridos.

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

Errores frecuentes para !SendMedicamentos (en general, revisar código de operación, datos del producto, etc.):

Errores de formato (ahora usar letra + 4 dígitos punto de venta + 8 digitos numero de comprobante, ejemplo: "A000100000001")

Ejemplos para los métodos de confirmación:
## Novedades

Se recuerda que esta disponible el 
[grupo de noticias](http://www.pyafipws.com.ar) (http://groups.google.com.ar/group/pyafipws) donde
se publicarán futuras novedades sobre PyAfipWS: servicios web de
factura electrónica y sus interfases (se recomienda suscribirse)

Historial de cambios:

- Mayo de 2014: Versión inicial

## Costos y Condiciones

Por soporte comercial consultar al (011) 15-3048-9211 o por mail a info@sistemasagiles.com.ar

Costos de soporte estimativos (puede variar dependiendo de las necesidades de cada implementación puntual):

 [http://www.sistemasagiles.com.ar/trac/wiki/PyAfipWs#ServicioswebSistemaNacionaldeTrazabilidadSNT]

Para soporte sin cargo de la comunidad, revisar la [lista de temas](https://github.com/reingart/pyafipws/issues) y/o [crear uno nuevo](https://github.com/reingart/pyafipws/issues/new). 
Por novedades y consultas genereales, puede usar el  [Google Groups](https://groups.google.com/forum/#!forum/pyafipws) (Foro Público).
Código fuente en [GitHub](https://github.com/reingart/pyafipws/).


Más información en PyAfipWs

MarianoReingart
MarianoReingart