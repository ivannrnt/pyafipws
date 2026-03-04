= Ingresos Brutos - WS ARBA DFE =


Interfaz para Servicio web para obtención de Alícuotas "RÉGIMEN DE RECAUDACIÓN POR SUJETO" correspondiente a la Resolución Normativa N° 64/10, N° 55/12, N° 02/13, N° 13/13, N° 28/14 ARBA (Rentas Provincia de Buenos Aires).

Especificación para la Aplicación Cliente actualizado a 22-12-2009 (última actualización de ARBA)

Permite consultar en forma on-line directamente desde su aplicación cliente, sin intervención de operadores, invocando servicios web (requerimiento https a un servicio remoto) que permite recuperar las alícuotas correspondientes a determinado período para la CUIT de su interés. 

Internamente genera y envía el archivo DFERespuesta_codigohash.xml con el algorítmo MD5 y analizando la respuesta en formato XML.



## Descargas

- Instalador: [Instalador 1.01b para evaluación](http://www.sistemasagiles.com.ar/soft/pyafipws/PyAfipWs-2.7.1556-32bit+iibb_1.01b-homo.exe)
- Ejemplo en VB: [iibb.bas](https://github.com/reingart/pyafipws/blob/master/ejemplos/iibb/iibb.bas)
- Código Fuente (Python): https://github.com/reingart/pyafipws/blob/master/iibb.py
- Documentación oficial: [http://www.arba.gov.ar/Informacion/IBrutos/LinksIIBB/RegimenSujeto.asp] (***Importante:** requiere clave ARBA*)

## URL

- Testing: https://dfe.test.arba.gov.ar/DomicilioElectronico/SeguridadCliente/dfeServicioConsulta.do
- Producción: https://dfe.arba.gov.ar/DomicilioElectronico/SeguridadCliente/dfeServicioConsulta.do

## Métodos

- **`Conectar(url=None, proxy="", wrapper="", cacert="", trace=False, testing="")`**: los parametros son similares a WSFEv1.Conectar (por el momento solo se usa url y trace para depuración), `testing` es el nombre de archivo de una respuesta XML de prueba para simulaciones (opcional)
- **`ConsultarContribuyentes(self, fecha_desde, fecha_hasta, cuit_contribuyente)`**: realiza la consulta remota a ARBA, estableciendo los resultados . Establece los atributos `NumeroComprobante`, `CantidadContribuyentes`,  `CodigoHash` de corresponder según respuesta de ARBA, y `TipoError`, `CodigoError`, `MensajeError`: si hay error general.
- **`LeerContribuyente()`**: lee el próximo contribuyente devuelto por ARBA. Devuelve verdadero (`True`) si hay contribuyente o  falso (`False`) si ya se analizaron todos los datos recibidos. No es obligatorio llamar a este método si se envia de a un solo un CUIT por consulta. Establece los atributos `CuitContribuyente, `AlicuotaPercepcion`, `AlicuotaRetencion`, `GrupoPercepcion`, `GrupoRetencion`
- **`ObtenerTagXml(tag1, tag2, ...)`**: busca en el mensaje xml analizado la etiqueta tag1, luego tag2 y así sucesivamente, devolviendo el contenido (texto) del dato si fue encontrada, o nulo en caso contrario. Ver ejemplo.

**IMPORTANTE**: `ConsultarContribuyentes` devuelve verdadero (`True`) si ha podido realizar la operación o falso (`False`) en caso contrario. Se capturan los errores, por lo que se deben revisar los atributos luego de llamar al método.

## Atributos

- `Usuario` y `Password` son los atributos ara autenticación (tramitar en ARBA)
- `Version` e `InstallDir` sirven para depuración de la interfaz.
- `XmlResponse`: respuesta xml enviada por ARBA 
- `Excepcion`, `Traceback`: se completan en caso de error interno no esperado (por ej. falla de comunicación).
- `TipoError`, `CodigoError`, `MensajeError`: si hay error general de ARBA se completan según la documentación
- `NumeroComprobante`, `CantidadContribuyentes`, `CodigoHash`: campos completados según la respuesta descripta en la documentación de ARBA
- `CuitContribuyente, `AlicuotaPercepcion`, `AlicuotaRetencion`, `GrupoPercepcion`, `GrupoRetencion`: completados si hay datos de contribuyentes devueltos.

**IMPORTANTE**: para el manejo de errores, siempre se debe revisar el atributo `Excepcion`, si este no está en blanco, ha ocurrido un error no esperado y debe analizar el `Traceback` (traza) y volver a intentar. Siempre es útil almacenar los valores de `XmlResponse` como respaldo de la operación y para futura referencia o análisis.

## Línea de Comando

Para sistemas operativos legados (DOS bajo windows) y UNIX/Linux, es posible operar la herramienta de remito electrónico por consola.
Recibe como parámetros el nombre de archivo, usuario y clave. Opcionalmente se puede especificar `--testing` para pruebas (usar xml de muestra como respuesta si no se tiene acceso a homologación) y `--trace` para imprimir por pantalla los datos enviados y recibidos.

Ejemplo de uso (usuario clave fecha_desde fecha_hasta cuit):
```
C:\PYAFIPWS>IIBB.EXE  20267565393 CIT 20150301 20150331 27269434894 --prod --trace
Numero Comprobante: 68800675
Codigo HASH: f1800fba55a255c8a6317b324bf5efc7
Error General:  |  | 
CUIT Contribuytente: 27269434894
AlicuotaPercepcion: 6,00
AlicuotaRetencion: 3,00
GrupoPercepcion: 15
GrupoRetencion: 15
```


**Importante**: Dependiendo como este generado el instalador, puede ser necesario usar ```IIBB_CLI.EXE```

En linux o desde el código fuente invocar con el interprete `python iibb.py`.

## Ejemplo Intefase COM en VB (5/6)

```
#!vb

Dim IIBB As Object, ok As Variant

' Crear la interfaz COM
Set IIBB = CreateObject("IIBB")

Debug.Print IIBB.Version
Debug.Print IIBB.InstallDir

' Establecer Datos de acceso (ARBA)
IIBB.Usuario = "20267565393"
IIBB.Password = "99999"          ' CIT

url = "https://dfe.test.arba.gov.ar/DomicilioElectronico/SeguridadCliente/dfeServicioConsulta.do"

' Conectar al servidor (pruebas)
ok = IIBB.Conectar(url)

' Enviar el archivo y procesar la respuesta:
fecha_desde = "20150301"
fecha_hasta = "20150331"
cuit_contribuyente = "27269434894"
ok = IIBB.ConsultarContribuyentes(fecha_desde, fecha_hasta, cuit_contribuyente)

' Hubo error interno?
If IIBB.Excepcion <> "" Then
    Debug.Print IIBB.Excepcion, IIBB.Traceback
    MsgBox IIBB.Traceback, vbCritical, "Excepcion:" & IIBB.Excepcion
Else
    Debug.Print IIBB.XmlResponse
    Debug.Print "Error General:", IIBB.TipoError, "|", IIBB.CodigoError, "|", IIBB.MensajeError
    
    ' Hubo error general de ARBA?
    If IIBB.CodigoError <> "" Then
        MsgBox IIBB.MensajeError, vbExclamation, "Error " & IIBB.TipoError & ":" & IIBB.CodigoError
    End If
    
    ' Datos generales de la respuesta:
    Debug.Print "Numero Comprobante:", IIBB.NumeroComprobante
    Debug.Print "Codigo Hash:", IIBB.CodigoHash

    ' Datos del contribuyente consultado:
    Debug.Print "CUIT Contribuytente:", IIBB.CuitContribuyente
    Debug.Print "AlicuotaPercepcion:", IIBB.AlicuotaPercepcion
    Debug.Print "AlicuotaRetencion:", IIBB.AlicuotaRetencion
    Debug.Print "GrupoPercepcion:", IIBB.GrupoPercepcion
    Debug.Print "GrupoRetencion:", IIBB.GrupoRetencion
    

    MsgBox "CUIT Contribuytente: " & IIBB.CuitContribuyente & vbCrLf & _
            "Numero Comprobante: " & IIBB.NumeroComprobante & vbCrLf & _
            "Codigo Hash: " & IIBB.CodigoHash & vbCrLf & _
            "AlicuotaPercepcion: " & IIBB.AlicuotaPercepcion & vbCrLf & _
            "AlicuotaRetencion: " & IIBB.AlicuotaRetencion & vbCrLf & _
            "GrupoPercepcion: " & IIBB.GrupoPercepcion & vbCrLf & _
            "GrupoRetencion: " & IIBB.GrupoRetencion, _
            vbInformation, "Resultado"
    
End If

```


Ejemplos de uso !ObtenerTagXml:
```
#!vb
Debug.Print "desde", iibb.ObtenerTagXml('fechaDesde')
Debug.Print "hasta", iibb.ObtenerTagXml('fechaHasta')
Debug.Print "cuit", iibb.ObtenerTagXml('contribuyentes', 'contribuyente', 0, 'cuitContribuyente')
Debug.Print "alicuota", iibb.ObtenerTagXml('contribuyentes', 'contribuyente', 0, 'alicuotapercepcion')
```


## Novedades

Se recuerda que esta disponible el 
[grupo de noticias](http://www.pyafipws.com.ar) (http://groups.google.com.ar/group/pyafipws) donde
se publicarán futuras novedades sobre PyAfipWS: servicios web de
factura electrónica y sus interfases (se recomienda suscribirse)

## Costos y Condiciones

Por soporte comercial consultar al (011) 15-3048-9211 o por mail a info@sistemasagiles.com.ar

Más información en PyAfipWs (ver [Costos y Condiciones del Soporte Comercial](../documentacion_herramientas/pyafipws.md#costos-y-condiciones))

MarianoReingart