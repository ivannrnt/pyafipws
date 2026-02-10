= Trazabilidad de Precursores Químicos - !TrazaMed SDRN RENPRE SEDRONAR SNT =

[[TracNav(noreorder|FacturaElectronica)]]

Interfaz para Servicio Web Trazabilidad de Precursores Químicos !TrazaMed.SDRN (SOAP) para informar movimientos de [Sustancias Químicas Controladas](http://renpre.servicios.pami.org.ar/portal_traza_renpre/pdfs/precursores_quimicos.pdf) –[Decreto 1095/96](http://www.renpre.gov.ar/pdfs/decretos/decreto_nacional_1168_96_comit_trabajo_conjunto.pdf), modificado por [Decreto 1161/00](http://www.renpre.gov.ar/pdfs/decretos/decreto_nacional_1095_96_actualizado_por_1161_00.pdf): Sistema Nacional de Trazabilidad modulo de Precursores Químicos (RENPRE SEDRONAR PAMI INSSJP) que deberán implementar el operador de precursores químicos obtención de número de CUFE (Código de Ubicación Física de Establecimiento). Entrenamiento y Alineación de Datos. [Resolución 900/12 RENPRE](http://www.renpre.gov.ar/pdfs/reso_y_dispo/2012_resolucion_900_12.pdf)



## Índice
[[TOC(noheading,inline,depth=2)]]

## Introducción

Biblioteca para el web service de RENPRE que permite automatizar la gestión de las trazabilidad de precursores químicos.

Sujetos obligados: ''Las empresas o sociedades comerciales que produzcan, fabriquen, preparen, exporten o importen sustancias o productos químicos
autorizados y que por sus características o componentes puedan ser derivados ilegalmente para servir de base o ser utilizados en la elaboración de estupefacientes''

Se debe informar: *Puesta en stock inicial, Fabricación, Merma, Destrucción, Recepción de eslabón anterior, Envío a eslabón posterior, Importación, Exportación, Recepción por transferencia, Envío por transferencia, Recepción por devolución, Envío por devolución, Uso propio o interno*

Características de esta herramienta:

- Interfaz COM: Simil DLL/OCX, embebible para aplicaciones programadas en lenguajes visuales bajo windows (Visual Basic, Visual Fox Pro, SAP, etc.)
- Interfaz por consola (linea de comandos / archivo de texto): similar a aplicativos SIAP para sistemas legados (ej. RM COBOL) multiplataforma (DOS, Windows, Unix)
- Interfaz por tablas DBF: compatible con dBase, !FoxPro, Clipper *-proximamente-*
- Interfaz por base de datos: compatible con conectores ODBC (MS SQL Server), PostgreSQL y otros (Oracle, DB2) *-proximamente-*

Simplifica y cubre totalmente el proceso, puede ser adaptado a programas existentes y no es requerido intervención del usuario.

Para más información ver PyAfipWs, basado en nuestra interfaz TrazabilidadMedicamentos


**Importante**: El documento ***["SNT Especificación Técnica Servicio Web"](http://renpre.servicios.pami.org.ar/portal_traza_renpre/pdfs/documento_ws_sedronar.pdf)*** estaría entrando en vigencia proximamente (1° de enero de 2014). Ver [[set de datos](http://renpre.servicios.pami.org.ar/portal_traza_renpre/pdfs/set_de_datos_renpre.pdf) para alineación / entrenamiento.

## Descargas

- Instalador: [instalador-TrazaRenpre-1.10a-homo.exe](https://pyafipws.googlecode.com/files/instalador-TrazaRenpre-1.10a-homo.exe) (para desarrollo)
- Documentación Oficial: [Sitio RENPRE](http://renpre.servicios.pami.org.ar/portal_traza_renpre/index.html)
- Ejemplo en VB: [trazarenpre.bas](https://github.com/reingart/pyafipws/blob/master/ejemplos/trazarenpre/trazarenpre.bas)
- Ejemplo en VFP: [trazarenpre.prg](https://github.com/reingart/pyafipws/blob/master/ejemplos/trazarenpre/trazarenpre.prg)
- Código Fuente (Python): [trazarenpre.py](https://github.com/reingart/pyafipws/blob/master/trazarenpre.py)


URL:

- Producción: https://trazabilidad.pami.org.ar:59050/trazamed.WebServiceSDRN ([WSDL](https://trazabilidad.pami.org.ar:59050/trazamed.WebServiceSDRN?wsdl))
- Entrenamiento: https://servicios.pami.org.ar/trazamed.WebServiceSDRN ([WSDL](https://servicios.pami.org.ar/trazamed.WebServiceSDRN?wsdl))

## Métodos

- **`SaveTransacciones(usuario, password, gln_origen, gln_destino, f_operacion,  id_evento, cod_producto, n_cantidad, n_documento_operacion, n_remito, id_tipo_transporte, id_paso_frontera_ingreso, id_paso_frontera_egreso, id_tipo_documento_operacion, d_dominio_tractor, d_dominio_semi, n_serie, n_lote, doc_despacho_plaza, djai, n_cert_rnpq, id_tipo_documento, n_documento, m_calidad_analitica)`**: Esta capacidad de servicio permite el informe por parte de un agente de una o varias transacciones por parte de los agentes involucrados en el Sistema Nacional de Trazabilidad.
- **`SendCancelacTransacc(usuario, password, codigo_transaccion)`**:  Capacidad de servicio que permite la cancelación de una transacción por parte de un agente de una o varias transacciones por parte de los agentes involucrados en el Sistema Nacional de Trazabilidad.

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

## Ejemplos

Ejemplo en pseudocódigo Python para informar transacciones de precursores químicos:
```
#!python
usuario = "pruebasws"
password = "pruebasws"
gln_origen = 9998887770004
gln_destino = 4
f_operacion = "01/01/2012"
id_evento = 40                  # 43: COMERCIALIZACION COMPRA, 44: COMERCIALIZACION VENTA
cod_producto = 88800000000028   # Acido Clorhidrico
n_cantidad = 1
n_documento_operacion = 1
#m_entrega_parcial = ""
n_remito = 123
n_serie = 112

TrazaRenpre.SaveTransacciones(usuario, password, gln_origen, gln_destino, 
                              f_operacion="01/01/2012", id_evento, cod_producto, n_cantidad, 
                              n_documento_operacion, m_entrega_parcial, n_remito, n_serie,
                             )

print "Resultado", TrazaRenpre.Resultado
print "CodigoTransaccion", TrazaRenpre.CodigoTransaccion
print "Excepciones", TrazaRenpre.Excepcion
print "Errores", TrazaRenpre.Errores
```


Ejemplo en pseudocódigo Python para cancelar una transaccion de precursores químicos:
```
#!python
usuario = "pruebasws"
password = "pruebasws"
codigo_transaccion = 123456

TrazaRenpre.SendCancelacTransacc(usuario, password, codigo_transaccion)

print "Resultado", TrazaRenpre.Resultado
print "CodigoTransaccion", TrazaRenpre.CodigoTransaccion
print "Excepciones", TrazaRenpre.Excepcion
print "Errores", TrazaRenpre.Errores
```


**Importante**: si un campo no debe enviarse, completar con None, Null, Empty, ? o el valor equivalente para campos nulos. No usar cadena vacia o 0 ya que son datos válidos y se enviarán al webservice. No saltear u omitir parámetros, salvo que esten al final o sean pasados por nombre (keyword arguments), usar !SetParametro en dicho caso.
## Linea de Comandos

Para sistemas operativos legados (DOS bajo windows) y UNIX/Linux, es posible operar la herramienta de trazabilidad por consola. Recibe como parámetros los datos correspondientes a la llamada remota (ver métodos). Opcionalmente se puede especificar --testing para pruebas (usar xml de muestra como respuesta si no se tiene acceso a homologación) y --trace para imprimir por pantalla los datos enviados y recibidos.

**Nota**: dependiendo de la compilación y el instalador, el ejecutable puede ser **`TRAZARENPRE_CLI.EXE`**

Ejemplo de uso para Informar un Medicamento (por defecto recibe los argumentos según el método !SaveTransacciones):

```
C:\PYAFIPWS>trazarenpre.exe "pruebasws" "pruebasws" ...
|Resultado  True|CodigoTransaccion     279695|Errores||
```


Si no se específican los campos por linea de comando, de manera predeterminada se utilizará el formato de texto
Para usar Tablas DBF agregar a la linea de comandos el parámetro `--dbf`. 
Para soporte de JSON (!JavaScript Object Notation), agregar parametro `--json`.
Se debe anteponer `--cargar` y `--grabar` para leer y escribir los datos en los archivos de intercambio.

Ejemplos para informar medicamentos usando archivos de texto, dbf y json respectivamente  (*consultar disponibilidad*):
```
C:\PYAFIPWS>trazarenpre.exe --cargar --grabar "pruebasws" "pruebasws"
C:\PYAFIPWS>trazarenpre.exe --cargar --grabar --dbf "pruebasws" "pruebasws"
C:\PYAFIPWS>trazarenpre.exe --cargar --grabar --json "pruebasws" "pruebasws"
```


Ejemplo de uso para cancelar una transacción (recibe usuario, password y número de transacción):

```
C:\PYAFIPWS>trazarenpre.exe --cancela "pruebasws" "pruebasws" "5114801" 
|Resultado False|CodigoTransaccion       None|Errores|3: Transaccion NO encontrada, NO se puede anular.|
```

**Importante**: alguna de las características mencionadas pueden no estar completamente habilitadas (*consultar disponibilidad*).

## Entrenamiento

**IMPORTANTE**: Solo usuarios habilitados. Consultar con técnicos de PAMI/SEDRONAR: [contactotrazabilidadsedronar@pami.org.ar](mailto:contactotrazabilidadsedronar@pami.org.ar)

Para poder realizar la trazabilidad de precursores químicos a través del !WebService, deberá antes realizar
el entrenamiento con datos ejemplo que lo ayudarán a comprender y probar el funcionamiento
del servicio.

Deberá utilizar en esta etapa el usuario, contraseña y CUFE asignado en la registración en el
modo de entrenamiento por la web de RENPRE.

Los siguientes son los eventos que deberá realizar a través del webservice. Previamente deberá
cumplimentar los pasos de entrenamiento descriptos en la página de trazabilidad. Tenga en
cuenta que siempre podrá ver el estado actual de su entrenamiento ingresando a la opción
Agentes / Mi puntuación.

## Errores

Fallas SOAP (!SoapFault) en atributo `Excepcion`:

- `soap:Server: La aplicacion usuario:"testwservice" intento ingresar con el password invalido:"testwservicepsw"`: verificar atributos `Username`, `Password` y url en `Conectar` (ambiente testing o producción)
- `soap:Server: La aplicacion usuario:"testwservice" no esta registrado en el sistema`: verificar atributos `Username`, `Password` y url en `Conectar` (ambiente testing o producción)
- `ns1:InvalidSecurity: An error was discovered processing the <wsse:Security> header`: ha proporcionado incorrectamente las credenciales de acceso o la biblioteca no soporta los encabezados de seguridad requeridos.

Errores Internos del webservice en atributo `Errores` (lista):

- `1: Error de autentificacion, verifique el usuario y/o contrase?a.`: verificar usuario y contraseña pasada al método `SendMedicamentos` (para testing es "pruebasws1" "pruebasws")

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


## Novedades

Se recuerda que esta disponible el 
[grupo de noticias](http://www.pyafipws.com.ar) (http://groups.google.com.ar/group/pyafipws) donde
se publicarán futuras novedades sobre PyAfipWS: servicios web de
factura electrónica y sus interfases (se recomienda suscribirse)

Historial de cambios:

- Diciembre de 2013: Versión inicial (ajuste de TrazabilidadMedicamentos)

## Costos y Condiciones

Por soporte comercial consultar al (011) 15-3048-9211 o por mail a info@sistemasagiles.com.ar

Costos de soporte estimativos (puede variar dependiendo de las necesidades de cada implementación puntual):

- Soporte mínimo: $49.680.- (por 1 semana de cobertura), sólo acceso a instalador y soporte por temas de instalación únicamente, no incluye consultas generales o ajustes. (prefentemente para clientes actuales)
- Soporte básico: $131.100.- (hasta 6 hs en total por 1 mes máx.), incluye consultas particulares y ajustes menores, contemplando TLB (TypeLib para lenguajes estáticos -solo TrazaMed, consultar otros WS-)
- Soporte avanzado: $196.650.- (hasta 9hs en total por 3 meses máx.) adicional, incluyendo ajustes y desarrollo de ejemplos, documentación, pruebas, etc., contempla temas urgentes y/o grandes empresas/ciclos de desarrollo
- Soporte por actualización: desde $49.680 (1 semana máx., hasta 1 hs en total, solo instalación y acceso a actualizaciones por correcciones generales), aplica a la versión 2 para clientes previos.

Para soporte sin cargo de la comunidad, revisar la [lista de temas](https://github.com/reingart/pyafipws/issues) y/o [crear uno nuevo](https://github.com/reingart/pyafipws/issues/new). 
Por novedades y consultas genereales, puede usar el  [Google Groups](https://groups.google.com/forum/#!forum/pyafipws) (Foro Público).
Código fuente en [GitHub](https://code.google.com/p/pyafipws/source/browse/).


Más información en PyAfipWs

MarianoReingart
MarianoReingart
MarianoReingart
MarianoReingart
MarianoReingart