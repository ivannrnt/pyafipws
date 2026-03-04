= Carta de Porte Electrónica - RG 5017/2021 =

Interfaz para Servicio Web de AFIP para la emisión de Carta de Porte Electrónica para transporte ferroviario y automotor.





## Descripción General

La Resolución General N° 5017/2021 establece el uso obligatorio de los comprobantes electrónicos denominados Carta de Porte para el Transporte Ferroviario de Granos y Carta de Porte para el Transporte Automotor de Granos, como únicos documentos válidos para respaldar el traslado de granos no destinados a la siembra -cereales y oleaginosos- y de legumbres secas -porotos, arvejas y lentejas-, así como de aquellas semillas aún no identificadas como tales por la Autoridad Competente, a cualquier destino dentro de la República Argentina, mediante el transporte automotor o ferroviario.

Exceptuado, el traslado realizado por transporte internacional cuando corresponda a operaciones de importación y/o exportación, y se encuentre respaldado por la documentación aduanera que corresponda de acuerdo con la normativa vigente.

Los referidos comprobantes sustituyen, al remito establecido por la RG 1.415/2003 de la AFIP, sus modificatorias y complementarias.

**Sujetos Obligados**

Podrán solicitar la Carta de Porte los sujetos incluidos en el Sistema de información Simplificado (SISA)

- Productores de granos que, se encuentren registrados en carácter de tales, ante la AFIP, y de corresponder, en la categoría “Planta de Acopio de Productor” del RUCA, que funciona en el ámbito de la Dirección Nacional de Control Comercial Agropecuario de la Secretaría de Agricultura, Ganadería y Pesca del Ministerio de Agricultura, Ganadería y Pesca, de acuerdo con lo previsto por la Resolución Nro RESOL-2017-21-APN-MA, sus modificatorias y complementarias.

- Operadores del comercio de granos que dispongan de una o más plantas habilitadas por la Autoridad Competente para el ingreso y/o egreso de granos, que se encuentren declaradas en el RUCA.

   Los mismos deberán informar un estado de matrícula habilitado en el Registro único de operadores de la cadena Agroindustrial (RUCA), para obtener la Carta de Porte.

- Autorizados mediante resolución fundada de la AFIP





Fecha de publicación: 25/06/2021

Fecha entrada en vigencia: 01/09/2021




**Micrositio:** https://www.afip.gob.ar/actividadesAgropecuarias/sector-agro/carta-porte-electronica/


## Descargas

- Instalador para Homologación:  https://www.sistemasagiles.com.ar/soft/pyafipws/PyAfipWs-2.7.2467-32bit+wsaa_2.12c+wscpe_1.06a-homo.exe
- Documentación:

                 [Documento Oficial WSCPE v1.0.0](https://www.afip.gob.ar/ws/documentos/manual_wscpe_1.0.0.pdf) (AFIP)
 
                 [Documento Oficial, Actualización WSCPE v1.1](https://www.afip.gob.ar/ws/documentos/manual_wscpe.pdf)

                 [Documento Oficial, Actualización WSCPE v1.3 del 08/09/21](https://www.afip.gob.ar/ws/documentos/manual_wscpe_1.3.pdf)   
           
                 [Documento Oficial, Actualización WSCPE v1.4 del 15/09/21](https://www.afip.gob.ar/ws/documentos/manual_wscpe_1.4.pdf)

                 [Documento Oficial, Actualización WSCPE v1.5 del 28/09/21](https://www.afip.gob.ar/ws/documentos/manual_wscpe_1.5.pdf)

                 [Documento Oficial, Actualización WSCPE v1.6 del 29/10/21](https://www.afip.gob.ar/ws/documentos/manual_wscpe_1.6.pdf) 

- [Manual de Uso General](../documentacion_herramientas/manualpyafipws.md) ([PDF](http://www.sistemasagiles.com.ar/trac/wiki/ManualPyAfipWs?format=pdf))


- Código Fuente (Python): [wscpe.py](https://github.com/reingart/pyafipws/blob/main/wscpe.py)

## Instalación

Está disponible el instalador para evaluación (ver [Descargas](wiki:CartadePorte#Descargas)), simplemente descargar, ejecutar seguir los pasos:

- Aceptar la licencia
- Seleccionar carpeta, por ej `C:\WSCPE`
- Instalación y registración automática

Para más información ver el [Manual de Uso](../documentacion_herramientas/manualpyafipws.md#Instalación)
## Metodos

- **`Conectar(cache=None, url="", proxy="")`**: en homologación no hace falta pasarle ningún parámetro. En producción, el segundo parámetro es la WSDL.
- **`Dummy()`**: devuelve estado de servidores

Métodos generales:

- **`CrearCPE()`**: Inicializa una estructura de CPE vacía para solicitar autorización
- **`AgregarCabecera(tipo_cpe, cuit_solicitante, sucursal, nro_orden, planta, carta_porte, nro_ctg, observaciones)`**: completa los datos básicos de una CPE
- **`AgregarOrigen(cod_provincia_operador, cod_localidad_operador, planta, cod_provincia_productor, cod_localidad_productor)`**: completa los datos de origen de una CPE; IMPORTANTE: usar operador (con planta) o productor, no ambos
- **`AgregarRetiroProductor(corresponde_retiro_productor, es_solicitante_campo, certificado_coe, cuit_remitente_comercial_productor)`**: completa la estructura de retiro productor; IMPORTANTE: usar certificado_coe y remitente comercial simultaneamente (son opcionales)
- **`AgregarIntervinientes(cuit_remitente_comercial_venta_primaria, cuit_remitente_comercial_venta_secundaria, cuit_remitente_comercial_venta_secundaria2, cuit_mercado_a_termino, cuit_corredor_venta_primaria, cuit_corredor_venta_secundaria, cuit_representante_entregador, cuit_representante_recibidor)`**: completa los datos de intervinientes; IMPORTANTE: todos los campos son opcionales
- **`AgregarDatosCarga(cod_grano, cosecha, peso_bruto, peso_tara)`**: completa los datos de carga; IMPORTANTE: no informar cosecha para usar eso_bruto, peso_tara (confirmar arribo)
- **`AgregarDestino(cuit_destino, es_destino_campo, cod_provincia, cod_localidad, planta, cuit_destinatario)`**: completa los datos de destino; IMPORTANTE: cuit_destino y cuit_destinatario son opcionales dependiendo del caso
- **`AgregarTransporte(cuit_transportista, cuit_transportista_tramo2, nro_vagon, nro_precinto, nro_operativo, dominio, fecha_hora_partida, km_recorrer, codigo_turno, cuit_chofer, tarifa, cuit_pagador_flete, mercaderia_fumigada, cuit_intermediario_flete, codigo_ramal, descripcion_ramal)`**: completa los datos de transporte; IMPORTANTE: si se indica codigo_ramal es ferroviario, de lo contrario es automotor. volver a llamar a este método para más de 1 dominio (ej acoplado), sólo completando ese campo.

- **`AgregarContingencia(concepto, descripcion)`**: agrega una contingencia para luego informarla a AFIP
- **`AgregarCerrarContingencia(concepto, cuit_transportista, nro_operativo, concepto_desactivacion, descripcion)`**: idem para cierre de contingencia

NOTA: Algunos parámetros pueden ser opcionales o no corresponder para la operación a realizar, enviar `null` o similar en esos casos (no saltear campos y respetar el órden de parámetros).


Métodos para generar una Carta de Porte:

- **`AutorizarCPEFerroviaria(archivo)`**: Solicita una nueva carta de porte del tipo ferroviaria.
- **`AutorizarCPEAutomotor(archivo)`**: Solicita una nueva carta de porte del tipo automotor.

NOTA: indicar el nombre al archivo PDF generado por AFIP en un directorio con permisos de escritura (ej. C:\WINDOWS\TEMP)

Métodos específicos:

- **`AnularCPE()`**: Anula una CPE existente. Llamar antes a AgregarCabecera(tipo_cpe, cuit_solicitante, sucursal, nro_orden)
- **`RechazoCPE()`**: Informar el rechazo de una carta de porte existente. AgregarCabecera(tipo_cpe, cuit_solicitante, sucursal, nro_orden)
- **`ConfirmacionDefinitivaCPEAutomotor()`**: Informa la confirmación de arribo. Llamar antes a AgregarCabecera(tipo_cpe, cuit_solicitante, sucursal, nro_orden)
- **`ConfirmacionDefinitivaCPEFerroviaria()`**: Informar la confirmación definitiva de una carta de porte ferroviaria existente.
- **`ConfirmarArriboCPE()`**: Informar la confirmación definitiva de una carta de porte automotor existente. Requiere AgregarCabecera(tipo_cpe, cuit_solicitante, sucursal, nro_orden) y AgregarDatosCarga(peso_bruto, peso_tara)
- **`ConfirmacionDefinitivaCPEFerroviaria()`**: Informa la confirmación de arribo. Llamar antes a AgregarCabecera(tipo_cpe, cuit_solicitante, sucursal, nro_orden)
- **`Confirmación definitiva CPE Ferroviaria`**: Informar la confirmación definitiva de una carta de porte existente.
- **`InformarContingencia()`**: Informe de contingencia de una CPE existente. Requiere AgregarCabecera(tipo_cpe, cuit_solicitante, sucursal, nro_orden) y AgregarContingencia(concepto, descripcion)
- **`CerrarContingenciaCPE()`**:  Permite informar el cierre de una contingencia asociado a una carta de porte ferroviaria.
- **`NuevoDestinoDestinatarioCPEFerroviaria()`**: Informa el nuevo destino / destinatario de una carta de porte existente.
- **`RegresoOrigenCPEAutomotor()`**: Informa el regreso a origen de una carta de porte existente. Requiere AgregarCabecera(tipo_cpe, cuit_solicitante, sucursal, nro_orden) AgregarTransporte(codigo_ramal, descripcion_ramal, fecha_hora_partida, km_recorrer)
- **`DesvioCPEFerroviaria()`**: Informa el desvío de una carta de porte ferroviaria existente.
- **`DescargadoDestinoCPE()`**: Indica por el solicitante de la Carta de Porte que la mercadería ha sido enviada. Requiere AgregarCabecera(tipo_cpe, cuit_solicitante, sucursal, nro_orden)
- **`DesvioCPEAutomotor()`**: Informar el nuevo destino / destinatario de una carta de porte existente. Requiere AgregarCabecera(tipo_cpe, cuit_solicitante, sucursal, nro_orden) AgregarDestino(cuit_destino, cod_provincia, cod_localidad, planta) AgregarTransporte(codigo_ramal, descripcion_ramal, fecha_hora_partida, km_recorrer)
- **`RegresoOrigenCPEAutomotor()`**: Informa el regreso a origen de una carta de porte automotor existente. Requiere AgregarCabecera(tipo_cpe, cuit_solicitante, sucursal, nro_orden) AgregarTransporte(fecha_hora_partida, km_recorrer, codigo_turno)
- **`DesvioCPEAutomotor()`**: Informa el desvío de una carta de porte existente. Requiere AgregarCabecera(tipo_cpe, cuit_solicitante, sucursal, nro_orden)  AgregarDestino(cuit_destino, cod_provincia, cod_localidad, planta, es_destino_campo)  AgregarTransporte(fecha_hora_partida, km_recorrer, codigo_turno)

- **`EditarCPEAutomotor(nro_ctg, cuit_corredor_venta_primaria, cuit_corredor_venta_secundaria, cuit_remitente_comercial_venta_primaria, cuit_remitente_comercial_venta_secundaria, cuit_remitente_comercial_productor, tarifa, km_recorrer, observaciones)`**: Permite modificar datos de una CP Automotor. En v.1.07a de 12/23 se incorpora tarifa, km_recorrer, observaciones

Métodos adicionales de consulta:

- **`ConsultarCPEFerroviaria(tipo_cpe, sucursal, nro_orden, cuit_solicitante)`**: Busca una CPE existente según parámetros de búsqueda y retorna información de la misma.
- **`ConsultaCPEFerroviariaPorNroOperativo(nro_operativo)`**: Obtiene información resumida de cartas de porte asociadas a un mismo número de operativo. Esta operación solo es válida para

 transportistas.

- **`ConsultarCPEAutomotor(tipo_cpe, cuit_solicitante, sucursal, nro_orden, nro_ctg, archivo)`**: Busca una CPE existente según parámetros de búsqueda y retorna información de la misma.
- **`ConsultarUltNroOrden(sucursal, tipo_CPE)`**: Retorna el último número de orden de CPE autorizado según número de sucursal.

 NOTA: ConsultarCPEAutomotor, indicar el nombre al archivo PDF generado por AFIP en un directorio con permisos de escritura (ej. C:\WINDOWS\TEMP)


Métodos para obtención de tablas de parámetros:

- **`ConsultarProvincias`**: Devuelve un listado con el código y descripción de todas las provincias.
- **`ConsultarLocalidadesPorProvincia`**: Devuelve un listado con el código y descripción de todas las localidades pertenecientes a la provincia indicada como parámetro.
- **`ConsultarTiposGrano`**: Devuelve un listado con el código y descripción de los tipos de granos permitidos.
- **`ConsultarLocalidadesProductor`**: Devuelve un listado con el código y descripción de todas las localidades según productor.


## Atributos


## Ejemplo

### Pseudocódidgo
```
#!python

wscpe = WSCPE()

ok = wscpe.CrearCPE()

ok = wscpe.AgregarCabecera(
        tipo_cp=74,  # 74: CPE Automotor, 75: CPE Ferroviaria,  274: Flete Corto.
        cuit_solicitante="20267565393",
        sucursal=1,
        nro_orden=1,
        planta=NULL,
        carta_porte=NULL,
        nro_ctg=NULL,
        observaciones="Observación", # Opcional
)
ok = wscpe.AgregarOrigen(
        cod_provincia_operador=12,
        cod_localidad_operador=5544,
        planta=1,
        cod_provincia_productor=12,
        cod_localidad_productor=5544,
)
ok = wscpe.AgregarRetiroProductor(
        corresponde_retiro_productor=True,
        es_solicitante_campo=False,
        certificado_coe=330100025869,
        cuit_remitente_comercial_productor=20111111112,
)
ok = wscpe.AgregarIntervinientes(
        cuit_intermediario=20222222223,
        cuit_remitente_comercial_venta_primaria=20222222223,
        cuit_remitente_comercial_venta_secundaria=20222222223,
        cuit_mercado_a_termino=20222222223,
        cuit_corredor_venta_primaria=20222222223,
        cuit_corredor_venta_secundaria=20222222223,
        cuit_representante_entregador=20222222223,
)
ok = wscpe.AgregarDatosCarga(
        cod_grano=31,
        cosecha=910,
        peso_bruto=1000,
        peso_tara=1000,
)
ok = wscpe.AgregarDestino(
        cuit_destino="20111111112",
        es_destino_campo=True,
        cod_provincia=12,
        cod_localidad=3058,
        planta=1,
        cuit_destinatario="20111111112",
)
ok = wscpe.AgregarTransporte(
        cuit_transportista=20333333334,
        dominio="ZZZ000",
        fecha_hora_partida="2016-11-17T12:00:39",
        km_recorrer=500,
        codigo_turno="00,
     )
ok = wscpe.AutorizarCPE(self, archivo="cpe.pdf"):

# Resultados:

print wscpe.NroCTG
print wscpe.FechaEmision
print wscpe.FechaInicioEstado
print wscpe.Estado
print wscpe.FechaVencimiento
```

### Visual Basic

#### Autorizar CPE
```
#!vb
    ok = WSCPE.CrearCPE()

    tipo_cpe = 74
    cuit_solicitante = 20111111112#
    sucursal = 1
    nro_orden = 1
    ok = WSCPE.AgregarCabecera(tipo_cpe, cuit_solicitante, sucursal, nro_orden)
    
    planta = 1
    cod_provincia_operador = 12
    cod_localidad_operador = 5544
    cod_provincia_productor = 12
    cod_localidad_productor = 5544
    ok = WSCPE.AgregarOrigen(planta, cod_provincia_operador, cod_localidad_operador, cod_provincia_productor, cod_localidad_productor)
    
    planta = 1
    cod_provincia = 12
    es_destino_campo = True
    cod_localidad = 3058
    cuit_destino = 20111111112#
    cuit_destinatario = 30000000006#
    ok = WSCPE.AgregarDestino(planta, cod_provincia, es_destino_campo, cod_localidad, cuit_destino, cuit_destinatario)
    
    certificado_coe = 330100025869#
    cuit_remitente_comercial_productor = 20111111112#
    corresponde_retiro_productor = True
    es_solicitante_campo = True
    ok = WSCPE.AgregarRetiroProductor(certificado_coe, cuit_remitente_comercial_productor, corresponde_retiro_productor, es_solicitante_campo)
        
    cuit_mercado_a_termino = 20222222223#
    cuit_corredor_venta_primaria = 20222222223#
    cuit_corredor_venta_secundaria = vbNull
    cuit_remitente_comercial_venta_secundaria =vbNull
    cuit_intermediario = 20222222223#
    cuit_remitente_comercial_venta_primaria = 20222222223#
    cuit_representante_entregador = 20222222223#
    cuit_representante_recibidor = 20222222223#
    ok = WSCPE.AgregarIntervinientes(cuit_remitente_comercial_venta_primaria, cuit_remitente_comercial_venta_secundaria, cuit_remitente_comercial_venta_secundaria2, cuit_mercado_a_termino, cuit_corredor_venta_primaria, cuit_corredor_venta_secundaria, cuit_representante_entregador, cuit_representante_recibidor)
    
    peso_tara = 1000
    cod_grano = 31
    peso_bruto = 1000
    cosecha = 2021
    ok = WSCPE.AgregarDatosCarga(peso_tara, cod_grano, peso_bruto, cosecha)
    
    cuit_transportista = 20333333334#
    fecha_hora_partida = "2021-08-21T23:29:26.579557"
    codigo_turno = "00"
    dominio = "ZZZ000"
    km_recorrer = 500
    cuit_chofer = 20333333334#
    tarifa = 100.1
    cuit_pagador_flete = 20333333334#
    cuit_intermediario_flete = 20333333334#
    mercaderia_fumigada = True
    ok = WSCPE.AgregarTransporte(cuit_transportista, fecha_hora_partida, codigo_turno, dominio, km_recorrer, cuit_chofer, tarifa, cuit_pagador_flete, cuit_intermediario_flete, mercaderia_fumigada)
    
    archivo = App.Path & "\cpe.pdf"
    ok = WSCPE.AutorizarCPEAutomotor(archivo)
    Debug.Print "Numero de CTG:", WSCPE.NroCTG
    Debug.Print "Fecha de emision:", WSCPE.FechaEmision
    Debug.Print "Estado:", WSCPE.Estado
    Debug.Print "Fecha de inicio de estado:", WSCPE.FechaInicioEstado
    Debug.Print "Fecha de vencimiento:", WSCPE.FechaVencimiento
            
    Debug.Print WSCPE.XmlResponse
    Debug.Print WSCPE.ErrMsg

    If Not ok Then
        ' muestro los errores
        Dim MensajeError As Variant
        For Each MensajeError In WSCPE.Errores
            MsgBox MensajeError, vbCritical, "WSCPE: Errores"
        Next
    End If
       
    MsgBox "CTG: " & WSCPE.NroCTG, vbInformation, "AutorizarCTE:"
```

#### Consultar CPE
```
#!vb
    
    ' Consulto los CTG generados (genera planilla Excel por AFIP)
    
    Dim nro_ctg As Variant
    nro_ctg = 10100000542#
    
    If nro_ctg <> 0 Then
        ok = WSCPE.ConsultarCPEAutomotor(Null, Null, Null, Null, nro_ctg)
    Else
        ok = WSCPE.ConsultarCPEAutomotor(tipo_cpe, sucursal, nro_orden, cuit_solicitante)
    End If
    ' Obtengo la constacia CTG -debe estar confirmada- (documento PDF AFIP)
    
    Debug.Print WSCPE.XmlResponse
    Debug.Print "Numero de CTG:", WSCPE.NroCTG
    Debug.Print "Errores:", WSCPE.ErrMsg
```

## Linea de Comandos

### wscpe.ini

Configurar cuit, certificado y clave privada:
```
# EJEMPLO de archivo de configuración de la interfaz PyAfipWs
# DEBE CAMBIAR Certificado (CERT) y Clave Privada (PRIVATEKEY)
# Para producción debe descomentar las URL (sacar ##)
# Más información:
# http://www.sistemasagiles.com.ar/trac/wiki/ManualPyAfipWs#Configuración
[WSAA]
CERT=reingart.crt
PRIVATEKEY=reingart.key
#PROXY=mariano:clave@localhost:999
#CACERT=afip_ca_info.crt
#WRAPPER=pycurl
#URL=https://wsaa.afip.gov.ar/ws/services/LoginCms
URL=https://wsaahomo.afip.gov.ar/ws/services/LoginCms?wsdl

[WSCPE]
CUIT=20267565393
ENTRADA=wscpe.txt
SALIDA=wscpe_sal.txt
#URL=https://fwshomo.afip.gov.ar/wscpe/services/soap?wsdl
#URL=https://serviciosjava.afip.gob.ar/cpe-ws/services/wscpe?wsdl
#CACERT=afip_ca_info.crt
#WRAPPER=pycurl
```

### Autorizar CPE

`wscpe_cli.exe --cargar --autorizar`

```
Numero CTG:  10100000542
Fecha Emision 2021-08-13 11:15:35
Fecha Vencimiento 2021-08-27 09:06:00
Estado:  CN
Observaciones:  []
Errores: []
Evento:
hecho.
```


### Consultar Ult Nro CPE

`wscpe_cli.py  --ult 74 1` (cambiar tipo de cpe y sucursal)

```
Ultimo Nro de CPE 3
```

### Consultar CPE

Por CTG:
`wscpe_cli.py  --conslutar 1 221 74 10100000542` (cambiar tipo de cpe y sucursal, sin CTG enviar "")

```
Nro de CTG 10100000542
Errores: []
{}
Resultado:  None
Numero CTG:  10100000542
Fecha Emision 2021-08-13 11:15:35
Fecha Vencimiento 2021-08-27 09:06:00
Estado:  CN
Observaciones:  []
Errores: []
Evento:
```


## Constancia PDF

La interfaz permite obtener el archivo que devuelve AFIP mediante este webservice:
 
- [attachment:ej_cpe_automotor.pdf]: Constancia CPE en documento PDF
 
AFIP devuelve el archivo binario ya generado, por lo que se debe especificar una ruta completa para almacenarlo.
Necesita Acrobat Reader, Microsoft Office / Libre Office o similares para poder abrir los documentos.

[[Image(cpe.jpg,25%)]]

## Formato

Archivos de intercambio de texto (TXT de ancho fijo cobol)

### encabezado
| Campo | Posición | Longitud | Tipo | Dec. | Valor |

| tipo_reg | 1 | 1 | Alfanumerico |  | 0 |
| tipo_cpe | 2 | 2 | Numerico |  |  |
| sucursal | 4 | 5 | Numerico |  |  |
| nro_orden | 9 | 18 | Numerico |  |  |
| planta | 27 | 5 | Numerico |  |  |
| cuit_solicitante | 32 | 11 | Numerico |  |  |
| razon_social_titular_planta | 43 | 11 | Alfanumerico |  |  |
| peso_bruto_descarga | 54 | 10 | Numerico |  |  |
| peso_tara_descarga | 64 | 10 | Numerico |  |  |
| nro_ctg | 74 | 12 | Numerico |  |  |
| fecha_emision | 86 | 10 | Alfanumerico |  |  |
| fecha_inicio_estado | 96 | 10 | Numerico |  |  |
| estado | 106 | 15 | Numerico |  |  |
| fecha_vencimiento | 121 | 10 | Alfanumerico |  |  |
### datos_carga
| Campo | Posición | Longitud | Tipo | Dec. | Valor |

| tipo_reg | 1 | 1 | Alfanumerico |  | C |
| cod_grano | 2 | 2 | Numerico |  |  |
| cosecha | 4 | 4 | Numerico |  |  |
| peso_bruto | 8 | 10 | Numerico |  |  |
| peso_tara | 18 | 10 | Numerico |  |  |
### destino
| Campo | Posición | Longitud | Tipo | Dec. | Valor |

| tipo_reg | 1 | 1 | Alfanumerico |  | D |
| cuit_destino | 2 | 11 | Numerico |  |  |
| es_destino_campo | 13 | 5 | Alfanumerico |  |  |
| cod_provincia | 18 | 2 | Numerico |  |  |
| cod_localidad | 20 | 6 | Numerico |  |  |
| planta | 26 | 5 | Numerico |  |  |
| cuit_destinatario | 31 | 11 | Numerico |  |  |
### errores
| Campo | Posición | Longitud | Tipo | Dec. | Valor |

| tipo_reg | 1 | 1 | Alfanumerico |  | E |
| codigo | 2 | 4 | Alfanumerico |  |  |
| descripcion | 6 | 250 | Alfanumerico |  |  |
### intervinientes
| Campo | Posición | Longitud | Tipo | Dec. | Valor |

| tipo_reg | 1 | 1 | Alfanumerico |  | I |
| cuit_intermediario | 2 | 11 | Numerico |  |  |
| cuit_remitente_comercial_venta_primaria | 13 | 11 | Numerico |  |  |
| cuit_remitente_comercial_venta_secundaria | 24 | 11 | Numerico |  |  |
| cuit_mercado_a_termino | 35 | 11 | Numerico |  |  |
| cuit_corredor_venta_primaria | 46 | 11 | Numerico |  |  |
| cuit_corredor_venta_secundaria | 57 | 11 | Numerico |  |  |
| cuit_representante_entregador | 68 | 11 | Numerico |  |  |
| cuit_representante_recibidor | 79 | 11 | Numerico |  |  |
### origen
| Campo | Posición | Longitud | Tipo | Dec. | Valor |

| tipo_reg | 1 | 1 | Alfanumerico |  | O |
| cod_provincia_operador | 2 | 2 | Numerico |  |  |
| cod_localidad_operador | 4 | 6 | Numerico |  |  |
| planta | 10 | 5 | Numerico |  |  |
| cod_provincia_productor | 15 | 2 | Numerico |  |  |
| cod_localidad_productor | 17 | 6 | Numerico |  |  |
### retiro_productor
| Campo | Posición | Longitud | Tipo | Dec. | Valor |

| tipo_reg | 1 | 1 | Alfanumerico |  | R |
| corresponde_retiro_productor | 2 | 5 | Alfanumerico |  |  |
| es_solicitante_campo | 7 | 5 | Alfanumerico |  |  |
| certificado_coe | 12 | 12 | Numerico |  |  |
| cuit_remitente_comercial_productor | 24 | 11 | Numerico |  |  |
### transporte
| Campo | Posición | Longitud | Tipo | Dec. | Valor |

| tipo_reg | 1 | 1 | Alfanumerico |  | T |
| cuit_transportista | 2 | 11 | Numerico |  |  |
| dominio | 13 | 10 | Alfanumerico |  |  |
| fecha_hora_partida | 23 | 20 | Alfanumerico |  |  |
| km_recorrer | 43 | 5 | Numerico |  |  |
| codigo_turno | 48 | 30 | Numerico |  |  |
| cuit_chofer | 78 | 11 | Numerico |  |  |
| tarifa | 89 | 10 | Importe | 2 |  |
| cuit_intermediario_flete | 99 | 11 | Numerico |  |  |
| cuitPagadorFlete | 110 | 11 | Numerico |  |  |
| mercaderia_fumigada | 121 | 5 | Alfanumerico |  |  |

### contingencia
| Campo | Posición | Longitud | Tipo | Dec. | Valor |

| tipo_reg | 1 | 1 | Alfanumerico |  | N |
| concepto | 2 | 2 | Alfanumerico |  |  |
| cuit_transportista | 4 | 11 | Numerico |  |  |
| nro_operativo | 15 | 11 | Numerico |  |  |
| concepto_desactivacion | 26 | 2 | Alfanumerico |  |  |
| descripcion | 28 | 140 | Alfanumerico |  |  |
### eventos
| Campo | Posición | Longitud | Tipo | Dec. | Valor |

| tipo_reg | 1 | 1 | Alfanumerico |  | V |
| codigo | 2 | 4 | Alfanumerico |  |  |
| descripcion | 6 | 250 | Alfanumerico |  |  |

## Tablas de Parámetros

### Provincias

| 0 | CAP.FEDERAL |
|---|---|
| 1 | BUENOS AIRES |
| 2 | CATAMARCA |
| 3 | CORDOBA |
| 4 | CORRIENTES |
| 5 | ENTRE RIOS |
| 6 | JUJUY |
| 7 | MENDOZA |
| 8 | LA RIOJA |
| 9 | SALTA |
| 10 | SAN JUAN |
| 11 | SAN LUIS |
| 12 | SANTA FE |
| 13 | SGO.DEL ESTERO |
| 14 | TUCUMAN |
| 16 | CHACO |
| 17 | CHUBUT |
| 18 | FORMOSA |
| 19 | MISIONES |
| 20 | NEUQUEN |
| 21 | LA PAMPA |
| 22 | RIO NEGRO |
| 23 | SANTA CRUZ |
| 24 | TIER.DEL FUEGO |


### Tipo de Granos

| 59 | Garbanzo |
|---|---|
| 60 | Amaranto (Amaranthus caudatus) |
| 61 | Amapola (Papaver rhoeas) |
| 62 | Chía (Salvia Hispanica) |
| 63 | Coriandro (Coriandrum sativum) |
| 64 | Habas (Vicia faba) |
| 65 | Lupines (Lupinus mutabilis) |
| 66 | Lupino (Lupinus albus) |
| 68 | Mostaza Marrón (Brassica juncea) |
| 69 | Mostaza Negra ( Brassica nigra) |
| 70 | Mostaza Blanca ( Sinapis alba) |
| 73 | Poroto Manteca  (Phaseolus lunatus) |
| 74 | Poroto Mung (Vigna radiata) |
| 76 | Poroto Pallar (Phaseolus coccineus L) |
| 77 | Quinoa (Chenopodium Quinoa Willd) |
| 78 | Sésamo (Sesamum indicum) |
| 80 | Trigo Sarraceno (Fagopyrum Esculentum) |
| 81 | Avena Amarilla (Avena Byzantina) |
| 100 | Cebada |
| 101 | Maní |
| 102 | Poroto |
| 103 | Trigo |
| 104 | Sorgo |
| 105 | Otros granos y legumbres provenientes de Cultivos de Invierno ("COSECHA FINA") |
| 106 | Otros granos y legumbres provenientes de Cultivos de Verano ("COSECHA GRUESA") |
| 107 | Colza/Canola |
| 19 | Maíz |
| 35 | Arroz |
| 1 | Lino |
| 2 | Girasol |
| 3 | Maní en caja |
| 5 | Maní para industria de selección |
| 6 | Maní para industria aceitera |
| 7 | Maní tipo confitería |
| 8 | Colza |
| 9 | Colza "00" / Canola |
| 10 | Trigo Forrajero |
| 11 | Cebada Forrajera |
| 12 | Cebada apta para Maltería |
| 14 | Trigo Candeal |
| 15 | Trigo Pan |
| 16 | Avena |
| 17 | Cebada Cervecera |
| 18 | Centeno |
| 20 | Mijo |
| 21 | Arroz Cáscara |
| 22 | Sorgo Granífero |
| 23 | Soja |
| 24 | Trigo Blando |
| 25 | Trigo Plata |
| 26 | Maíz Flynt o Plata |
| 27 | Maíz Pisingallo |
| 28 | Triticale |
| 30 | Alpiste |
| 31 | Algodón |
| 32 | Cártamo |
| 33 | Poroto Blanco Natural Oval Y Alubia |
| 34 | Poroto Distinto del Blanco Oval Y Alubia |
| 46 | Lenteja |
| 47 | Arveja |
| 48 | Poroto Blanco Seleccionado Oval y Alubia |
| 49 | Otras Legumbres |
| 50 | Otros Granos |
### Localidades por provincia


| 3 | 12 DE AGOSTO |
|---|---|
| 4 | 12 DE OCTUBRE |
| 5 | 16 DE JULIO |
| 6 | 17 DE AGOSTO |
| 11 | 20 DE JUNIO |
| 16 | 25 DE MAYO |
| 24 | 30 DE AGOSTO |
| 29 | 9 DE ABRIL |
| 30 | 9 DE JULIO |
| 32 | ABASTO |
| 33 | ABBOTT |
| 36 | ABEL |
| 68 | ACAMBUCO |
| 71 | ACASSUSO |
| 74 | ACEILAN |
| 77 | ACEVEDO |
| 85 | ACHUPALLAS |
| 95 | ADELA |
| 98 | ADELA SAENZ |
| 99 | ADOLFO ALSINA |
| 101 | ADOLFO GONZALES CHAVES |
| 108 | AEROPUERTO EZEIZA |
| 112 | AGOTE |
| 207 | AGUAS CORRIENTES |
| 214 | AGUAS VERDES |
| 221 | AGUIRREZABALA |
| 223 | AGUSTIN MOSCONI |
| 225 | AGUSTINA |
| 235 | ALAGON |
| 238 | ALAMOS |
| 242 | ALASTUEY |
| 251 | ALBERDI |
| 252 | ALBERTI |
| 279 | ALDEA ROMANA |
| 281 | ALDEA SAN ANDRES |
| 298 | ALDO BONZI |
| 299 | ALEGRE |
| 304 | ALEJANDRO KORN |
| 306 | ALEJANDRO PETION |
| 315 | ALFALAD |
| 321 | ALFREDO DEMARCHI |
| 355 | ALMACEN EL CRUCE |
| 356 | ALMACEN EL DESCANSO |
| 357 | ALMACEN LA COLINA |
| 358 | ALMACEN PIATTI |
| 361 | ALMIRANTE BROWN |
| 363 | ALMIRANTE IRIZAR |
| 380 | ALTA VISTA |
| 381 | ALTAMIRA |
| 382 | ALTAMIRANO |
| 465 | ALTO VERDE |
| 475 | ALVAREZ JONTE |
| 476 | ALVARO BARROS |
| 479 | ALZAGA |
| 484 | AMALIA |
| 502 | AMBROSIO P LEZICA |
| 505 | AMERICA |
| 529 | ANASAGASTI |
| 547 | ANCON |
| 552 | ANDANT |
| 553 | ANDERSON |
| 561 | ANDRES VACCOREZZA |
| 610 | ANTONIO CARBONI |
| 612 | ANTONIO DE LOS HEROS |
| 624 | APARICIO |
| 649 | ARAUJO |
| 657 | ARBOLEDA |
| 663 | ARBUCO |
| 671 | ARENALES |
| 672 | ARENAZA |
| 677 | AREVALO |
| 680 | ARGERICH |
| 699 | ARQUEDAS |
| 706 | ARRIBENOS |
| 711 | ARROYO AGUAS BLANCAS |
| 713 | ARROYO AGUILA NEGRA |
| 714 | ARROYO ALELI |
| 726 | ARROYO BOTIJA FALSA |
| 732 | ARROYO BURGOS |
| 736 | ARROYO CANELON |
| 738 | ARROYO CARABELITAS |
| 750 | ARROYO CHICO |
| 760 | ARROYO DE LA CRUZ |
| 762 | ARROYO DE LUNA |
| 766 | ARROYO DEL PESCADO |
| 771 | ARROYO DULCE |
| 772 | ARROYO EL AHOGADO |
| 790 | ARROYO LA MAZA |
| 797 | ARROYO LAS CRUCES |
| 799 | ARROYO LAS ROSAS |
| 804 | ARROYO LOS HUESOS |
| 808 | ARROYO LOS TIGRES |
| 821 | ARROYO NEGRO |
| 828 | ARROYO PAREJA |
| 838 | ARROYO PESQUERIA |
| 865 | ARROYO TAJIBER |
| 876 | ARROYO VENADO |
| 880 | ARROYO ZANJON |
| 882 | ARROYO NACURUTU |
| 883 | ARROYO NACURUTU CHICO |
| 890 | ARTURO SEGUI |
| 891 | ARTURO VATTEONE |
| 892 | ASAMBLEA |
| 908 | ASTURIAS |
| 912 | ATAHUALPA |
| 913 | ATALAYA |
| 923 | ATUCHA |
| 937 | AVELLANEDA |
| 942 | AVESTRUZ |
| 953 | AZCUENAGA |
| 956 | AZOPARDO |
| 960 | AZUL |
| 969 | B LOS AROMOS SAN PATRICIO |
| 970 | B NUESTRA SENORA DE LA PAZ |
| 971 | B SARMIENTO DON ROLANDO |
| 974 | BACACAY |
| 976 | BADANO |
| 980 | BAGUES |
| 988 | BAHIA SAN BLAS |
| 993 | BAIGORRITA |
| 1043 | BAJO HONDO |
| 1056 | BALCARCE |
| 1125 | BALNEARIO ATLANTIDA |
| 1127 | BALNEARIO CHAPALCO |
| 1128 | BALNEARIO CLAROMECO |
| 1131 | BALNEARIO FRENTE MAR |
| 1133 | BALNEARIO LA BALIZA |
| 1136 | BALNEARIO LOS ANGELES |
| 1137 | BALNEARIO MAR CHIQUITA |
| 1138 | BALNEARIO MAR DE COBO |
| 1139 | BALNEARIO OCEANO |
| 1140 | BALNEARIO ORENSE |
| 1142 | BALNEARIO PARADA |
| 1144 | BALNEARIO PLAYA DORADA |
| 1145 | BALNEARIO RETA |
| 1146 | BALNEARIO SAN ANTONIO |
| 1148 | BALNEARIO SAUCE GRANDE |
| 1150 | BALSA |
| 1165 | BANDERALO |
| 1169 | BANFIELD |
| 1183 | BARKER |
| 1216 | BARRIO 1 DE MAYO |
| 1221 | BARRIO ALMAFUERTE |
| 1226 | BARRIO AVELLANEDA |
| 1228 | BARRIO BATAN |
| 1233 | BARRIO CAISAMAR |
| 1234 | BARRIO CAROSIO |
| 1236 | BARRIO CHAPADMALAL |
| 1245 | BARRIO EL CAZADOR |
| 1246 | BARRIO EL HUECO |
| 1248 | BARRIO EL PORTENO |
| 1252 | BARRIO GARIN NORTE |
| 1253 | BARRIO GASTRONOMICO |
| 1254 | BARRIO GENERAL ROCA |
| 1255 | BARRIO GENERAL SAN MARTIN |
| 1258 | BARRIO INDIO TROMPA |
| 1261 | BARRIO JOSE M ESTRADA |
| 1262 | BARRIO JUAN B JUSTO |
| 1263 | BARRIO JUAREZ |
| 1264 | BARRIO JULIO DE VEDIA |
| 1265 | BARRIO JURAMENTO |
| 1266 | BARRIO LA DOLLY |
| 1272 | BARRIO LA LUISA |
| 1277 | BARRIO LAS MANDARINAS |
| 1279 | BARRIO LOMA PARAGUAYA |
| 1280 | BARRIO LOS ANDES |
| 1284 | BARRIO NOROESTE |
| 1286 | BARRIO OBRERO |
| 1290 | BARRIO PARQUE BRISTOL |
| 1291 | BARRIO PARQUE LAMBARE |
| 1292 | BARRIO PARQUE LELOIR |
| 1294 | BARRIO PEDRO RICO |
| 1295 | BARRIO PEDRO ROCCO |
| 1297 | BARRIO PINARES |
| 1298 | BARRIO PRIMERA JUNTA |
| 1299 | BARRIO PUEBLO NUEVO |
| 1302 | BARRIO ROSARIO SUD |
| 1303 | BARRIO SAN ALEJO |
| 1305 | BARRIO SAN BLAS |
| 1306 | BARRIO SAN CARLOS |
| 1309 | BARRIO SAN JACINTO |
| 1310 | BARRIO SAN JOSE |
| 1313 | BARRIO SAN MARTIN |
| 1315 | BARRIO SAN ROQUE |
| 1317 | BARRIO SANTA MAGDALENA |
| 1322 | BARRIO TIERRA DE ORO |
| 1323 | BARRIO TIRO FEDERAL |
| 1324 | BARRIO TROCHA |
| 1326 | BARRIO U O C R A |
| 1331 | BARRIO VILLA MUNIZ |
| 1332 | BARRIO VILLA ORTEGA |
| 1333 | BARRIO VILLA SALADILLO |
| 1335 | BARRIO VISTA ALEGRE |
| 1348 | BASE AERONAVAL CMTE ESPORA |
| 1349 | BASE AERONAVAL PUNTA INDIO |
| 1357 | BASE NAVAL RIO SANTIAGO |
| 1369 | BATERIAS |
| 1373 | BAUDRIX |
| 1425 | BELEN DE ESCOBAR |
| 1435 | BELLA VISTA |
| 1438 | BELLOCQ |
| 1442 | BENAVIDEZ |
| 1444 | BENITEZ |
| 1445 | BENITO JUAREZ |
| 1453 | BERDIER |
| 1455 | BERISSO |
| 1459 | BERMUDEZ |
| 1462 | BERNAL ESTE |
| 1463 | BERNAL OESTE |
| 1468 | BERNARDO VERA Y PINTADO |
| 1471 | BERRAONDO |
| 1474 | BERUTTI |
| 1487 | BLANCA GRANDE |
| 1492 | BLANDENGUES |
| 1493 | BLAQUIER |
| 1495 | BLAS DURANONA |
| 1497 | BLONDEAU |
| 1498 | BME BAVIO GRAL MANSILLA |
| 1516 | BOCAYUBA |
| 1526 | BOLIVAR |
| 1534 | BONNEMENT |
| 1540 | BORDENAVE |
| 1550 | BOSCH |
| 1552 | BOSQUES |
| 1555 | BOULOGNE |
| 1563 | BRAGADO |
| 1565 | BRAVO DEL DOS |
| 1585 | BUCHANAN |
| 1610 | BURZACO |
| 1642 | CABEZA DE BUEY |
| 1696 | CADRET |
| 1703 | CAILOMUTA |
| 1738 | CALDERON |
| 1776 | CALVO |
| 1778 | CAMAOTI |
| 1780 | CAMARON CHICO |
| 1785 | CAMBACERES |
| 1794 | CAMINERA GENERAL LOPEZ |
| 1795 | CAMINERA JUAREZ |
| 1796 | CAMINERA LUJAN |
| 1797 | CAMINERA NAPALEOFU |
| 1798 | CAMINERA SAMBOROMBON |
| 1804 | CAMINO CENTENARIO KM 11500 |
| 1810 | CAMPAMENTO |
| 1823 | CAMPANA |
| 1841 | CAMPO ARISTIMUNO |
| 1856 | CAMPO BUENA VISTA |
| 1867 | CAMPO COLIQUEO |
| 1873 | CAMPO CRISOL |
| 1887 | CAMPO DE MAYO |
| 1898 | CAMPO DEL NORTE AMERICANO |
| 1946 | CAMPO LA LIMA |
| 1951 | CAMPO LA PLATA |
| 1955 | CAMPO LA ZULEMA |
| 1960 | CAMPO LEITE |
| 1963 | CAMPO LOPE SECO |
| 1983 | CAMPO PENA LOPEZ |
| 2000 | CAMPO ROJAS |
| 2004 | CAMPO SABATE |
| 2009 | CAMPO SAN JUAN |
| 2031 | CAMPODONICO |
| 2036 | CANAL 15 CERRO DE LA GLORIA |
| 2037 | CANAL MARTIN IRIGOYEN |
| 2039 | CANAL N ALEM 2A SEC |
| 2063 | CANGALLO |
| 2067 | CANNING |
| 2068 | CANONIGO GORRITI |
| 2071 | CANTERA AGUIRRE |
| 2072 | CANTERA ALBION |
| 2076 | CANTERA LA FEDERACION |
| 2077 | CANTERA LA MOVEDIZA |
| 2079 | CANTERA MONTE CRISTO |
| 2082 | CANTERA VILLALONGA |
| 2084 | CANTERAS DE GREGORINI |
| 2097 | CAPDEPONT |
| 2117 | CAPILLA DEL SENOR |
| 2134 | CAPITAN CASTRO |
| 2140 | CAPITAN SARMIENTO |
| 2150 | CARABELAS |
| 2163 | CARAPACHAY |
| 2178 | CARHUE |
| 2180 | CARI LARQUEA |
| 2182 | CARILO |
| 2184 | CARLOS BEGUERIE |
| 2186 | CARLOS CASARES |
| 2188 | CARLOS KEEN |
| 2189 | CARLOS LEMEE |
| 2194 | CARLOS SALAS |
| 2195 | CARLOS SPEGAZZINI |
| 2197 | CARLOS TEJEDOR |
| 2201 | CARMEN DE ARECO |
| 2202 | CARMEN DE PATAGONES |
| 2277 | CASALINS |
| 2285 | CASCADA |
| 2289 | CASEROS |
| 2291 | CASEY |
| 2311 | CASTELAR |
| 2313 | CASTELLI |
| 2316 | CASTILLA |
| 2357 | CAZON |
| 2372 | CANADA DE ARIAS |
| 2424 | CANADA MARIANO |
| 2425 | CANADA MARTA |
| 2429 | CANADA RICA |
| 2434 | CANADA SECA |
| 2477 | CANUELAS |
| 2493 | CENTENARIO |
| 2506 | CENTRO GUERRERO |
| 2514 | CERRI |
| 2522 | CERRITO |
| 2534 | CERRO AGUILA |
| 2584 | CERRO DE LA GLORIA CANAL 15 |
| 2595 | CERRO DE LOS LEONES |
| 2736 | CERRO SOTUYO |
| 2767 | CHACABUCO |
| 2789 | CHACRA EXPERIMENTAL INTA |
| 2832 | CHANCAY |
| 2840 | CHAPAR |
| 2863 | CHAS |
| 2864 | CHASCOMUS |
| 2865 | CHASICO |
| 2916 | CHENAUT |
| 2929 | CHICLANA |
| 2949 | CHILLAR |
| 2981 | CHIVILCOY |
| 2988 | CHOIQUE |
| 3027 | CHURRUCA |
| 3056 | CITY BELL |
| 3059 | CIUDAD DE EDUARDO MADERO |
| 3061 | CIUDAD EVITA |
| 3063 | CIUDAD JARDIN DEL PALOMAR |
| 3065 | CIUDADELA |
| 3074 | CLAYPOLE |
| 3083 | CNA NACIONAL DE ALIENADOS |
| 3085 | CNEL RODOLFO BUNGE |
| 3094 | COBO |
| 3103 | COCHRANE |
| 3127 | COLEGIO SAN PABLO |
| 3134 | COLIQUEO |
| 3143 | COLMAN |
| 3151 | COLON |
| 3156 | COLONIA  MIGUEL ESTEVERENA |
| 3182 | COLONIA ALBERDI |
| 3233 | COLONIA BARON HIRSCH |
| 3247 | COLONIA BELLA VISTA |
| 3323 | COLONIA CUARENTA Y TRES |
| 3336 | COLONIA DE VAC CHAPADMALAL |
| 3358 | COLONIA DR GDOR UDAONDO |
| 3370 | COLONIA EL BALDE |
| 3384 | COLONIA EL GUANACO |
| 3436 | COLONIA FERRARI |
| 3489 | COLONIA HINOJO |
| 3491 | COLONIA HIPOLITO YRIGOYEN |
| 3493 | COLONIA HOGAR R GUTIERREZ |
| 3499 | COLONIA INCHAUSTI |
| 3536 | COLONIA LA BEBA |
| 3545 | COLONIA LA CATALINA |
| 3547 | COLONIA LA CELINA |
| 3554 | COLONIA LA ESPERANZA |
| 3555 | COLONIA LA ESTRELLA |
| 3566 | COLONIA LA INVERNADA |
| 3577 | COLONIA LA MERCED |
| 3584 | COLONIA LA NENA |
| 3586 | COLONIA LA NORIA |
| 3601 | COLONIA LA REINA |
| 3611 | COLONIA LA VANGUARDIA |
| 3612 | COLONIA LA VASCONGADA |
| 3615 | COLONIA LABORDEROY |
| 3620 | COLONIA LAPIN |
| 3630 | COLONIA LAS YESCAS |
| 3635 | COLONIA LEVEN |
| 3644 | COLONIA LOS ALAMOS |
| 3646 | COLONIA LOS BOSQUES |
| 3650 | COLONIA LOS HORNOS |
| 3651 | COLONIA LOS HUESOS |
| 3658 | COLONIA LOS TOLDOS |
| 3661 | COLONIA LOS TRES USARIS |
| 3696 | COLONIA MAURICIO |
| 3713 | COLONIA MONTE LA PLATA |
| 3730 | COLONIA NAVIERA |
| 3733 | COLONIA NIEVES |
| 3745 | COLONIA OCAMPO |
| 3764 | COLONIA PALANTELEN |
| 3784 | COLONIA PHILLIPSON N 1 |
| 3799 | COLONIA PUEBLO RUSO |
| 3824 | COLONIA RUSA |
| 3837 | COLONIA SAN EDUARDO |
| 3838 | COLONIA SAN ENRIQUE |
| 3842 | COLONIA SAN FRANCISCO |
| 3854 | COLONIA SAN MARTIN |
| 3858 | COLONIA SAN PEDRO |
| 3860 | COLONIA SAN RAMON |
| 3878 | COLONIA SANTA MARIANA |
| 3883 | COLONIA SANTA ROSA |
| 3895 | COLONIA SERE |
| 3908 | COLONIA STEGMAN |
| 3914 | COLONIA TAPATTA |
| 3967 | COLONIA ZAMBUNGO |
| 3981 | COMAHUE OESTE |
| 3987 | COMANDANTE GIRIBONE |
| 3991 | COMANDANTE NICANOR OTAMENDI |
| 3999 | COMODORO PY |
| 4016 | CONDARCO |
| 4040 | COOPER |
| 4046 | COPETONAS |
| 4053 | CORACEROS |
| 4057 | CORAZZI |
| 4058 | CORBETT |
| 4080 | CORONEL BOERR |
| 4082 | CORONEL BRANDSEN |
| 4083 | CORONEL CHARLONE |
| 4087 | CORONEL DORREGO |
| 4091 | CORONEL FALCON |
| 4096 | CORONEL GRANADA |
| 4099 | CORONEL ISLENOS |
| 4105 | CORONEL MARCELINO FREYRE |
| 4107 | CORONEL MARTINEZ DE HOZ |
| 4113 | CORONEL PRINGLES |
| 4114 | CORONEL RODOLFO BUNGE |
| 4118 | CORONEL SEGUI |
| 4119 | CORONEL SUAREZ |
| 4120 | CORONEL VIDAL |
| 4162 | CORTI |
| 4176 | COSTA BONITA BALNEARIO |
| 4177 | COSTA BRAVA |
| 4225 | COVELLO |
| 4239 | CRISTIANO MUERTO |
| 4245 | CROTTO |
| 4254 | CRUCESITA |
| 4284 | CUARTEL 2 |
| 4286 | CUARTEL 8 |
| 4287 | CUARTEL CUATRO |
| 4288 | CUARTEL V |
| 4297 | CUATRO DE NOVIEMBRE |
| 4316 | CUCULLU |
| 4317 | CUENCA |
| 4347 | CURAMALAN |
| 4350 | CURARU |
| 4375 | D ORBIGNY |
| 4384 | DARREGUEIRA |
| 4386 | DE BARY |
| 4387 | DE BRUYN |
| 4388 | DE FERRARI |
| 4390 | DE LA GARMA |
| 4395 | DEL VALLE |
| 4396 | DEL VISO |
| 4398 | DELFIN HUERGO |
| 4400 | DELGADO |
| 4402 | DENNEHY |
| 4411 | DESPENADEROS |
| 4418 | DESVIO AGUIRRE |
| 4425 | DESVIO GARBARINI |
| 4428 | DESVIO SAN ALEJO |
| 4429 | DESVIO SANDRINI |
| 4439 | DIEGO GAYNOR |
| 4445 | DIONISIA |
| 4464 | DIQUE LUJAN |
| 4484 | DOCK CENTRAL |
| 4485 | DOCK SUD |
| 4488 | DOCTOR DOMINGO CABRED |
| 4497 | DOCTOR RICARDO LEVENE |
| 4501 | DOLORES |
| 4508 | DOMINGO FAUSTINO SARMIENTO |
| 4518 | DON BOSCO |
| 4519 | DON CIPRIANO |
| 4530 | DON TORCUATO |
| 4531 | DON VICENTE |
| 4549 | DOS HERMANOS |
| 4552 | DOS NACIONES |
| 4565 | DOYLE |
| 4571 | DRABBLE |
| 4575 | DUCOS |
| 4576 | DUDIGNAC |
| 4578 | DUGGAN |
| 4579 | DUHAU |
| 4587 | DURANONA |
| 4596 | EDMUNDO PERKINS |
| 4599 | EGANA |
| 4613 | EL 60 |
| 4630 | EL ALBA |
| 4659 | EL ARBOLITO PERGAMINO |
| 4678 | EL BAGUAL |
| 4705 | EL BOMBERO |
| 4708 | EL BOQUERON |
| 4762 | EL CARBON |
| 4768 | EL CARMEN DE LANGUEYU |
| 4772 | EL CARPINCHO |
| 4773 | EL CARRETERO |
| 4799 | EL CENTINELA |
| 4817 | EL CHALAR |
| 4831 | EL CHEIQUE |
| 4849 | EL CHUMBIAO |
| 4887 | EL CORTAPIE |
| 4913 | EL DESCANSO |
| 4923 | EL DIA |
| 4933 | EL DIVISORIO |
| 4950 | EL ESPINILLO |
| 4957 | EL EUCALIPTUS |
| 4959 | EL FENIX |
| 4978 | EL GALLO |
| 4998 | EL GUALICHO |
| 5006 | EL HERVIDERO |
| 5022 | EL JABALI |
| 5024 | EL JAGUEL |
| 5036 | EL JUNCO |
| 5038 | EL JUPITER |
| 5047 | EL LENGUARAZ |
| 5054 | EL LUCERO |
| 5073 | EL MARQUESADO |
| 5086 | EL MIRADOR |
| 5107 | EL MORO |
| 5113 | EL NACIONAL |
| 5124 | EL NILO |
| 5170 | EL PALOMAR |
| 5171 | EL PAMPERO |
| 5183 | EL PARCHE |
| 5202 | EL PELADO |
| 5206 | EL PENSAMIENTO |
| 5211 | EL PEREGRINO |
| 5234 | EL PINO |
| 5263 | EL PORVENIR |
| 5295 | EL QUEMADO |
| 5318 | EL REFUGIO |
| 5327 | EL RETIRO PDO GRAL VIAMONTE |
| 5332 | EL RINCON |
| 5341 | EL ROSARIO |
| 5358 | EL SAUCE |
| 5371 | EL SIASGO |
| 5372 | EL SILENCIO |
| 5378 | EL SOCORRO |
| 5381 | EL SOLDADO |
| 5399 | EL TALAR |
| 5415 | EL TATU |
| 5416 | EL TEJAR |
| 5444 | EL TREBANON |
| 5452 | EL TRIGO |
| 5453 | EL TRIO |
| 5454 | EL TRIUNFO |
| 5488 | EL VERANO |
| 5491 | EL VIGILANTE |
| 5499 | EL VOLANTE |
| 5518 | EL ZORRO |
| 5528 | ELIAS ROMERO |
| 5530 | ELORDI |
| 5534 | ELVIRA |
| 5546 | EMILIANO REYNOSO |
| 5547 | EMILIO AYARZA |
| 5549 | EMILIO LAMARCA |
| 5554 | EMMA |
| 5555 | EMPALME |
| 5562 | EMPALME LOBOS |
| 5563 | EMPALME MAGDALENA |
| 5565 | EMPALME PIEDRA ECHADA |
| 5574 | ENCINA |
| 5578 | ENERGIA |
| 5582 | ENRIQUE FYNN |
| 5584 | ENRIQUE LAVALLE |
| 5588 | ENSENADA |
| 5595 | EPUMER |
| 5597 | EREZCANO |
| 5598 | ERIZE |
| 5599 | ERNESTINA |
| 5602 | ESC NAV MILITAR RIO SANT |
| 5612 | ESCRIBANO P NICOLAS |
| 5619 | ESPARTILLAR |
| 5625 | ESPIGAS |
| 5633 | ESPORA |
| 5636 | ESQUINA DE CROTTO |
| 5655 | EST SAN FRANCISCO BELLOQ |
| 5675 | ESTABLECIMIENTO SAN MIGUEL |
| 5684 | ESTACION ASCENSION |
| 5686 | ESTACION BARADERO |
| 5687 | ESTACION BARROW |
| 5690 | ESTACION CAIOMUTA |
| 5697 | ESTACION CORONEL PRINGLES |
| 5705 | ESTACION GOMEZ |
| 5709 | ESTACION LAGO EPECUEN |
| 5710 | ESTACION LAZZARINO |
| 5712 | ESTACION LINCOLN |
| 5716 | ESTACION MITIKILI |
| 5722 | ESTACION PROVINCIAL |
| 5763 | ESTANCIA CHAPAR |
| 5886 | ESTANCIA LAS GAMAS |
| 5949 | ESTANCIA SAN ANTONIO |
| 5950 | ESTANCIA SAN CLAUDIO |
| 5961 | ESTANCIA SAN RAFAEL |
| 5982 | ESTANCIA VIEJA |
| 5994 | ESTEBAN A GASCON |
| 5995 | ESTEBAN DE LUCA |
| 5997 | ESTEBAN DIAZ |
| 6001 | ESTELA |
| 6010 | ESTHER |
| 6012 | ESTOMBA |
| 6015 | ESTRELLA NACIENTE |
| 6016 | ESTRUGAMOU |
| 6038 | EXALTACION DE LA CRUZ |
| 6040 | EZEIZA |
| 6041 | EZPELETA ESTE |
| 6042 | EZPELETA OESTE |
| 6051 | FAIR |
| 6068 | FARO |
| 6072 | FARO SAN ANTONIO |
| 6073 | FARO SEGUNDA BARRANCOSA |
| 6076 | FATIMA ESTACION EMPALME |
| 6079 | FAUZON |
| 6095 | FERRE |
| 6162 | FLAMENCO |
| 6171 | FLORENCIO VARELA |
| 6172 | FLORENTINO AMEGHINO |
| 6176 | FLORIDA OESTE |
| 6180 | FONTEZUELA |
| 6182 | FORTABAT |
| 6185 | FORTIN ACHA |
| 6197 | FORTIN CHACO |
| 6208 | FORTIN IRENE |
| 6214 | FORTIN MERCEDES |
| 6215 | FORTIN NECOCHEA |
| 6216 | FORTIN OLAVARRIA |
| 6225 | FORTIN TIBURCIO |
| 6229 | FORTIN VIEJO |
| 6230 | FORTIN VIGILANCIA |
| 6240 | FRANCISCO ALVAREZ |
| 6241 | FRANCISCO AYERZA |
| 6242 | FRANCISCO BERRA |
| 6244 | FRANCISCO DE VITORIA |
| 6246 | FRANCISCO J MEEKS |
| 6247 | FRANCISCO MADERO |
| 6248 | FRANCISCO MAGNANO |
| 6250 | FRANCISCO MURATURE |
| 6257 | FRANKLIN |
| 6261 | FRENCH |
| 6264 | FRIGORIFICO ARMOUR |
| 6266 | FRIGORIFICO LAS PALMAS |
| 6280 | FUERTE ARGENTINO |
| 6281 | FUERTE BARRAGAN |
| 6285 | FULTON |
| 6294 | GAHAN |
| 6298 | GALERA DE TORRES |
| 6304 | GALO LLORENTE |
| 6307 | GALVAN |
| 6311 | GANDARA |
| 6321 | GARCIA DEL RIO |
| 6326 | GARIN |
| 6329 | GARRE |
| 6355 | GENERAL ALVARADO |
| 6356 | GENERAL ALVEAR |
| 6357 | GENERAL ARENALES |
| 6364 | GENERAL CONESA |
| 6365 | GENERAL DANIEL CERRI |
| 6374 | GENERAL GELLY |
| 6376 | GENERAL GUIDO |
| 6378 | GENERAL HORNOS |
| 6382 | GENERAL LAMADRID |
| 6383 | GENERAL LAS HERAS |
| 6384 | GENERAL LAVALLE |
| 6387 | GENERAL MADARIAGA |
| 6393 | GENERAL O BRIEN |
| 6398 | GENERAL PACHECO |
| 6403 | GENERAL PINTO |
| 6404 | GENERAL PIRAN |
| 6409 | GENERAL RIVAS |
| 6411 | GENERAL RODRIGUEZ |
| 6412 | GENERAL RONDEAU |
| 6416 | GENERAL VALDEZ |
| 6418 | GENERAL VIAMONTE |
| 6419 | GENERAL VILLEGAS |
| 6423 | GERENTE CILLEY |
| 6425 | GERLI |
| 6427 | GERMANIA |
| 6434 | GIL |
| 6445 | GLORIALDO |
| 6448 | GOBERNADOR ANDONAEGHI |
| 6449 | GOBERNADOR ARIAS |
| 6452 | GOBERNADOR CASTRO |
| 6454 | GOBERNADOR COSTA |
| 6470 | GOBERNADOR OBLIGADO |
| 6479 | GOBERNADOR UDAONDO |
| 6483 | GOBOS |
| 6488 | GOLDNEY |
| 6492 | GOMEZ  DE LA VEGA |
| 6495 | GONDRA |
| 6498 | GONZALEZ CATAN |
| 6500 | GONZALEZ RISOS |
| 6502 | GORCHS |
| 6504 | GORNATTI |
| 6506 | GOROSTIAGA |
| 6508 | GOUIN |
| 6511 | GOYENA |
| 6512 | GOYENECHE |
| 6515 | GRACIARENA |
| 6532 | GRAND BOURG |
| 6533 | GRAND DOCK |
| 6540 | GREGORIO DE LA FERRERE |
| 6541 | GREGORIO VILLAFANE |
| 6543 | GRISOLIA |
| 6544 | GRUNBEIN |
| 6575 | GUAMINI |
| 6578 | GUANACO |
| 6596 | GUARDIA DEL MONTE |
| 6630 | GUERNICA |
| 6634 | GUERRICO |
| 6636 | GUIDO SPANO |
| 6638 | GUILLERMO E HUDSON |
| 6641 | GUIRONDO |
| 6651 | HAEDO |
| 6655 | HALE |
| 6656 | HAM |
| 6659 | HARAS CHACABUCO |
| 6660 | HARAS CHAPADMALAL |
| 6661 | HARAS EL CARMEN |
| 6662 | HARAS EL CATORCE |
| 6663 | HARAS EL CENTINELA |
| 6665 | HARAS EL MORO |
| 6666 | HARAS EL OMBU |
| 6667 | HARAS EL SALASO |
| 6668 | HARAS LA ELVIRA |
| 6669 | HARAS LA LULA |
| 6671 | HARAS NACIONAL |
| 6672 | HARAS OJO DEL AGUA |
| 6674 | HARAS R DE LA PARVA |
| 6676 | HARAS SAN IGNACIO |
| 6679 | HARAS TRUJUI |
| 6684 | HEAVY |
| 6687 | HENDERSON |
| 6689 | HEREFORD |
| 6700 | HERRERA VEGAS |
| 6712 | HILARIO ASCASUBI |
| 6717 | HINOJO |
| 6731 | HOGAR MARIANO ORTIZ BASUALDO |
| 6745 | HORNOS |
| 6748 | HORTENSIA |
| 6750 | HOSPITAL INTERZONAL DR DOMINGO |
| 6751 | HOSPITAL NECOCHEA |
| 6753 | HOSPITAL SAN ANTONIO DE LA LLA |
| 6825 | HUESO CLAVADO |
| 6827 | HUETEL |
| 6851 | HUNTER |
| 6853 | HURLINGHAM |
| 6854 | HUSARES |
| 6865 | IBANEZ |
| 6876 | IGARZABAL |
| 6880 | IGNACIO CORREAS ARANA |
| 6898 | INDACOCHEA |
| 6900 | INDIA MUERTA |
| 6904 | INES INDART |
| 6914 | INGENIERO ADOLFO SOURDEAUX |
| 6920 | INGENIERO BEAUGEY |
| 6925 | INGENIERO DE MADRID |
| 6937 | INGENIERO MASCHWITZ |
| 6940 | INGENIERO MONETA |
| 6943 | INGENIERO SILVEYRA |
| 6944 | INGENIERO THOMPSON |
| 6945 | INGENIERO WHITE |
| 6946 | INGENIERO WILLIAMS |
| 6986 | INVERNADAS |
| 6991 | IRALA |
| 6992 | IRAOLA |
| 6994 | IRENE |
| 6996 | IRIARTE |
| 7009 | ISIDRO CASANOVA |
| 7019 | ISLA CATARELLI |
| 7045 | ISLA LOS LAURELES |
| 7047 | ISLA MARTIN GARCIA |
| 7050 | ISLA PAULINO |
| 7057 | ISLA SANTIAGO |
| 7064 | ISLA VERDE |
| 7066 | ISLAS |
| 7075 | ISONDU |
| 7094 | ITURREGUI |
| 7096 | ITUZAINGO |
| 7100 | J M MICHEO |
| 7137 | JAUREGUI JOSE MARIA |
| 7150 | JOAQUIN GORINA |
| 7157 | JOSE A GUISASOLA |
| 7161 | JOSE CLEMENTE PAZ |
| 7166 | JOSE FERRARI |
| 7168 | JOSE INGENIEROS |
| 7169 | JOSE LEON SUAREZ |
| 7173 | JOSE MARIA BLANCO |
| 7174 | JOSE MARIA GUTIERREZ |
| 7178 | JOSE SOJO |
| 7184 | JUAN A PRADERE |
| 7187 | JUAN B JUSTO ING WHITE |
| 7193 | JUAN COUSTE |
| 7195 | JUAN E BARRA |
| 7196 | JUAN F IBARRA |
| 7198 | JUAN G PUJOL |
| 7204 | JUAN JOSE ALMEYRA |
| 7206 | JUAN JOSE PASO |
| 7210 | JUAN N FERNANDEZ |
| 7215 | JUAN TRONCONI |
| 7216 | JUAN V CILLEY |
| 7218 | JUAN VUCETICH EX DR R LEVENE |
| 7221 | JUANA A DE LA PENA |
| 7223 | JUANCHO |
| 7268 | KENNY |
| 7280 | KRABBE |
| 7285 | LA  AURORA |
| 7289 | LA ADELAIDA |
| 7301 | LA ALAMEDA |
| 7302 | LA ALCIRA |
| 7311 | LA AMALIA |
| 7316 | LA AMISTAD |
| 7320 | LA ANGELITA |
| 7331 | LA ARMONIA |
| 7337 | LA AURORA |
| 7339 | LA AZOTEA |
| 7341 | LA AZUCENA |
| 7343 | LA BALANDRA |
| 7345 | LA BALLENA |
| 7367 | LA BEBA |
| 7375 | LA BLANCA |
| 7376 | LA BLANQUEADA |
| 7380 | LA BOLSA |
| 7388 | LA BRAVA |
| 7391 | LA BUANA MOZA |
| 7404 | LA CALERA |
| 7406 | LA CALETA |
| 7408 | LA CALIFORNIA ARGENTINA |
| 7413 | LA CAMPANA |
| 7423 | LA CARLOTA |
| 7430 | LA CARRETA |
| 7444 | LA CAUTIVA |
| 7453 | LA CELIA |
| 7454 | LA CELINA |
| 7457 | LA CENTRAL |
| 7489 | LA CHOZA |
| 7507 | LA COLINA |
| 7511 | LA COLORADA |
| 7512 | LA COLORADA CHICA |
| 7517 | LA CONSTANCIA |
| 7521 | LA COPETA |
| 7522 | LA CORA |
| 7523 | LA CORINA |
| 7531 | LA COSTA |
| 7535 | LA COTORRA |
| 7554 | LA DELFINA |
| 7555 | LA DELIA |
| 7557 | LA DESPIERTA |
| 7570 | LA DORMILONA |
| 7582 | LA ELMA |
| 7605 | LA ESPERANZA |
| 7609 | LA ESPERANZA GRAL MADARIAGA |
| 7610 | LA ESPERANZA PDO LAS FLORES |
| 7626 | LA ESTRELLA |
| 7631 | LA EVA |
| 7643 | LA FELICIANA |
| 7654 | LA FLORIDA |
| 7659 | LA FRATERNIDAD |
| 7670 | LA GARITA |
| 7674 | LA GAVIOTA |
| 7679 | LA GLEVA |
| 7680 | LA GLORIA |
| 7683 | LA GRACIELITA |
| 7690 | LA GREGORIA |
| 7701 | LA HERMINIA |
| 7706 | LA HIGUERA |
| 7710 | LA HORQUETA |
| 7714 | LA HUAYQUERIA |
| 7728 | LA INVENCIBLE |
| 7759 | LA LARGA |
| 7760 | LA LARGA NUEVA |
| 7761 | LA LATA |
| 7786 | LA LOMA |
| 7793 | LA LUCIA |
| 7794 | LA LUCILA |
| 7798 | LA LUISA |
| 7799 | LA LUNA |
| 7801 | LA LUZ |
| 7812 | LA MANTEQUERIA |
| 7813 | LA MANUELA |
| 7818 | LA MARGARITA |
| 7832 | LA MARTINA |
| 7836 | LA MASCOTA |
| 7838 | LA MATILDE |
| 7867 | LA NACION |
| 7869 | LA NARCISA |
| 7870 | LA NAVARRA |
| 7873 | LA NELIDA |
| 7878 | LA NINA |
| 7880 | LA NORIA |
| 7883 | LA NUMANCIA |
| 7892 | LA ORIENTAL |
| 7904 | LA PALA |
| 7909 | LA PALMA |
| 7923 | LA PARA |
| 7927 | LA PASTORA |
| 7934 | LA PAZ |
| 7943 | LA PEREGRINA |
| 7944 | LA PERLA |
| 7958 | LA PIEDRA |
| 7963 | LA PINTA |
| 7971 | LA PLAYA |
| 7976 | LA POCHOLA |
| 7985 | LA POSADA |
| 7986 | LA POSTA |
| 7990 | LA PRADERA |
| 7991 | LA PRIMAVERA |
| 7996 | LA PRIMITIVA |
| 7998 | LA PROTECCION |
| 7999 | LA PROTEGIDA |
| 8000 | LA PROVIDENCIA |
| 8018 | LA QUERENCIA |
| 8024 | LA RABIA |
| 8038 | LA REFORMA |
| 8041 | LA REJA |
| 8051 | LA RICA |
| 8052 | LA RINCONADA |
| 8062 | LA ROSADA |
| 8063 | LA ROSALIA |
| 8075 | LA SALADA |
| 8085 | LA SARA |
| 8086 | LA SARITA |
| 8105 | LA SIRENA |
| 8106 | LA SOBERANIA |
| 8109 | LA SOMBRA |
| 8112 | LA SORTIJA |
| 8114 | LA SUIZA |
| 8116 | LA TABLADA |
| 8118 | LA TALINA |
| 8127 | LA TIGRA |
| 8133 | LA TOMASA |
| 8138 | LA TORRECITA |
| 8148 | LA TRINIDAD |
| 8157 | LA UNION |
| 8165 | LA VANGUARDIA |
| 8167 | LA VASCONGADA |
| 8181 | LA VICTORIA |
| 8182 | LA VICTORIA DESVIO |
| 8184 | LA VIOLETA |
| 8185 | LA VIRGINIA |
| 8188 | LA VITICOLA |
| 8198 | LA YESCA |
| 8200 | LA ZANJA |
| 8202 | LA ZARATENA |
| 8209 | LABARDEN |
| 8250 | LAGUNA ALSINA |
| 8255 | LAGUNA BRAVA |
| 8261 | LAGUNA DE GOMEZ |
| 8265 | LAGUNA DE LOBOS |
| 8266 | LAGUNA DE LOS PADRES |
| 8272 | LAGUNA DEL CURA |
| 8274 | LAGUNA DEL MONTE |
| 8277 | LAGUNA DEL SOLDADO |
| 8287 | LAGUNA LAS MULITAS |
| 8290 | LAGUNA MEDINA |
| 8331 | LANGUEYU |
| 8335 | LANUS |
| 8343 | LAPLACETTE |
| 8344 | LAPRIDA |
| 8348 | LARRAMENDY |
| 8354 | LARTIGAU |
| 8375 | LAS ARMAS |
| 8385 | LAS BANDURRIAS |
| 8402 | LAS BRUSCAS |
| 8432 | LAS CHACRAS |
| 8437 | LAS CHILCAS |
| 8453 | LAS CORTADERAS |
| 8463 | LAS CUATRO PUERTAS |
| 8488 | LAS FLORES |
| 8504 | LAS GUASQUITAS |
| 8510 | LAS HERMANAS |
| 8520 | LAS ISLETAS |
| 8524 | LAS JUANITAS |
| 8543 | LAS LOMAS |
| 8546 | LAS MALVINAS |
| 8552 | LAS MARIANAS |
| 8553 | LAS MARTINETAS |
| 8558 | LAS MERCEDES |
| 8572 | LAS MOSTAZAS |
| 8573 | LAS MULAS |
| 8576 | LAS NIEVES |
| 8577 | LAS NUTRIAS |
| 8579 | LAS OSCURAS |
| 8585 | LAS PALMAS |
| 8598 | LAS PARVAS |
| 8616 | LAS PIEDRTAS |
| 8642 | LAS ROSAS |
| 8643 | LAS SALADAS |
| 8650 | LAS SUIZAS |
| 8651 | LAS SULTANAS |
| 8673 | LAS TORTUGAS |
| 8674 | LAS TOSCAS |
| 8680 | LAS TRES FLORES |
| 8705 | LAS VIBORAS |
| 8720 | LASTRA |
| 8738 | LAZZARINO |
| 8741 | LEANDRO N ALEM |
| 8748 | LEGARISTI |
| 8765 | LERTORA |
| 8769 | LEUBUCO |
| 8774 | LEZICA Y TORREZURI |
| 8777 | LIBANO |
| 8779 | LIBERTAD |
| 8784 | LIBRES DEL SUD |
| 8785 | LICENCIADO MATIENZO |
| 8793 | LIMA |
| 8803 | LINCOLN |
| 8833 | LLAVALLOL |
| 8840 | LOBERIA |
| 8863 | LOMA DE SALOMON |
| 8867 | LOMA DEL INDIO |
| 8876 | LOMA NEGRA |
| 8878 | LOMA PARTIDA |
| 8902 | LOMAS DE ZAMORA |
| 8904 | LOMAS DEL MIRADOR |
| 8929 | LONGCHAMPS |
| 8934 | LOPEZ LECUBE |
| 8942 | LOS ACANTILADOS |
| 8963 | LOS ALTOS |
| 8969 | LOS ANGELES |
| 8977 | LOS ARCOS |
| 8980 | LOS AROMOS |
| 9005 | LOS BOSQUES |
| 9015 | LOS CALDENES |
| 9016 | LOS CALLEJONES |
| 9020 | LOS CARDALES |
| 9022 | LOS CARDOS |
| 9036 | LOS CERRILLOS |
| 9038 | LOS CERROS |
| 9069 | LOS COLONIALES |
| 9094 | LOS CUATRO CAMINOS |
| 9117 | LOS EUCALIPTOS |
| 9118 | LOS EUCALIPTUS CASCO URBANO |
| 9129 | LOS GAUCHOS |
| 9161 | LOS HUESOS |
| 9174 | LOS LEONES |
| 9198 | LOS MERINOS |
| 9209 | LOS MOLLES |
| 9251 | LOS PATOS |
| 9325 | LOS SANTOS VIEJOS |
| 9346 | LOS TALAS |
| 9429 | LUIS CHICO |
| 9431 | LUIS GUILLON |
| 9442 | LUMB |
| 9451 | LURO |
| 9466 | MACEDO |
| 9494 | MAGDALA |
| 9495 | MAGDALENA |
| 9497 | MAGUIRRE |
| 9505 | MAIPU |
| 9518 | MALABIA |
| 9559 | MAMAGUITA |
| 9570 | MANANTIALES |
| 9571 | MANANTIALES GRANDES |
| 9596 | MANUEL ALBERTI |
| 9597 | MANUEL B GONNET |
| 9602 | MANUEL JOSE GARCIA |
| 9603 | MANUEL OCAMPO |
| 9605 | MANZANARES |
| 9607 | MANZO Y NINO |
| 9608 | MANZONE |
| 9609 | MAORI |
| 9621 | MAR CHIQUITA |
| 9622 | MAR DE AJO |
| 9623 | MAR DE COBO |
| 9625 | MAR DEL PLATA |
| 9626 | MAR DEL SUD |
| 9627 | MAR DEL TUYU |
| 9636 | MARCELINO UGARTE |
| 9638 | MARCOS PAZ |
| 9639 | MARCOS PAZ B BERNASCONI |
| 9640 | MARCOS PAZ B EL MARTILLO |
| 9641 | MARCOS PAZ B EL MORO |
| 9643 | MARCOS PAZ B LA LONJA |
| 9644 | MARCOS PAZ B LA MILAGROSA |
| 9645 | MARCOS PAZ B MARTIN FIERRO |
| 9646 | MARCOS PAZ B URIOSTE |
| 9649 | MARI LAUQUEN |
| 9666 | MARIA IGNACIA |
| 9670 | MARIA LUCILA |
| 9674 | MARIA P MORENO |
| 9679 | MARIANO ACOSTA |
| 9680 | MARIANO BENITEZ PERGAMINO |
| 9682 | MARIANO H ALFONZO |
| 9688 | MARIANO UNZUE |
| 9690 | MARISCAL SUCRE |
| 9697 | MARTIN BERRAONDO |
| 9698 | MARTIN CORONADO |
| 9704 | MARTINEZ |
| 9719 | MASUREL |
| 9732 | MATHEU |
| 9746 | MAURAS |
| 9751 | MAXIMO FERNANDEZ |
| 9752 | MAXIMO PAZ |
| 9762 | MAYOR JOSE ORELLANO |
| 9777 | MECHITA |
| 9781 | MEDALAND |
| 9791 | MEDANOS |
| 9804 | MELCHOR ROMERO |
| 9812 | MEMBRILLAR |
| 9818 | MERCADO CENTRAL |
| 9819 | MERCADO DE VICTORIA |
| 9821 | MERCEDES |
| 9825 | MERIDIANO VO |
| 9847 | MICAELA CASCALLARES |
| 9930 | MINISTRO RIVADAVIA |
| 9935 | MIRA PAMPA |
| 9941 | MIRAMONTE |
| 9942 | MIRANDA |
| 9978 | MOCTEZUMA |
| 10000 | MOLINO GALILEO |
| 10002 | MOLL |
| 10024 | MONES CAZON |
| 10027 | MONROE |
| 10028 | MONSALVO |
| 10043 | MONTE CHINGOLO |
| 10055 | MONTE FIORE |
| 10058 | MONTE GRANDE |
| 10060 | MONTE HERMOSO |
| 10092 | MOORES |
| 10102 | MOREA |
| 10109 | MORON |
| 10117 | MORSE |
| 10125 | MOURAS |
| 10136 | MULCAHY |
| 10141 | MUNRO |
| 10147 | MUTTI |
| 10151 | MUNOZ |
| 10168 | NAHUEL RUCA |
| 10175 | NAPALEOFU |
| 10178 | NAPOSTA |
| 10196 | NAVARRO |
| 10201 | NECOCHEA |
| 10202 | NECOL ESTACION FCGM |
| 10218 | NICANOR OLIVERA |
| 10221 | NICOLAS DESCALZI |
| 10223 | NICOLAS LEVALLE |
| 10228 | NIEVES |
| 10259 | NORBERTO DE LA RIESTRA |
| 10262 | NORUMBEGA |
| 10272 | NUEVA ATLANTIS |
| 10283 | NUEVA ESPANA |
| 10297 | NUEVA ROMA |
| 10319 | O HIGGINS |
| 10337 | OCHANDIO |
| 10344 | ODORQUI |
| 10360 | OLASCOAGA |
| 10361 | OLAVARRIA |
| 10363 | OLIDEN |
| 10366 | OLIVERA |
| 10368 | OLIVIERA CESAR |
| 10374 | OMBU |
| 10379 | OMBUCTA |
| 10385 | ONCE DE SETIEMBRE |
| 10389 | OPEN DOOR |
| 10397 | ORENSE |
| 10399 | ORLANDO |
| 10407 | ORTIZ BASUALDO |
| 10408 | ORTIZ DE ROSAS |
| 10411 | OSTENDE |
| 10437 | PABLO ACOSTA |
| 10438 | PABLO NOGUES |
| 10445 | PACHAN |
| 10517 | PALMITAS |
| 10519 | PALO BLANCO |
| 10655 | PANAME |
| 10657 | PANCHO DIAZ |
| 10667 | PAPIN |
| 10674 | PARADA LOS ROBLES |
| 10676 | PARADA TATAY |
| 10679 | PARAGUIL |
| 10705 | PARAJE LA VASCA |
| 10727 | PARAJE SANTA ROSA |
| 10728 | PARAJE STARACHE |
| 10749 | PARISH |
| 10751 | PARQUE CARILO |
| 10753 | PARQUE MUNOZ |
| 10757 | PARQUE SAN MARTIN |
| 10759 | PARQUE TAILLADE |
| 10760 | PARRAVICHINI |
| 10772 | PASMAN |
| 10776 | PASO ALSINA |
| 10792 | PASO CRAMER |
| 10843 | PASO DEL MEDANO |
| 10847 | PASO DEL REY |
| 10879 | PASO MAYOR |
| 10912 | PASOS |
| 10915 | PASTEUR |
| 10935 | PATRICIOS |
| 10937 | PAULA |
| 10954 | PAZOS KANKI |
| 10959 | PEDERNALES |
| 10967 | PEDRO GAMEN |
| 10969 | PEDRO LASALLE |
| 10971 | PEDRO LURO |
| 10972 | PEDRO NICOLAS ESCRIBANO |
| 10978 | PEHUAJO |
| 10981 | PEHUELCHES |
| 10982 | PEHUEN CO |
| 10983 | PELICURA |
| 10996 | PEREYRA |
| 11003 | PEREZ MILLAN |
| 11019 | PESSAGNO |
| 11027 | PENAFLOR |
| 11071 | PICHINCHA |
| 11084 | PIEDRA ANCHA |
| 11118 | PIEDRITAS |
| 11120 | PIERES |
| 11121 | PIERINI |
| 11124 | PILA |
| 11128 | PILAR |
| 11136 | PILLAHUINCO |
| 11143 | PINAMAR |
| 11160 | PINZON |
| 11161 | PIPINAS |
| 11177 | PIROVANO |
| 11181 | PIRUCO |
| 11195 | PINEIRO |
| 11197 | PLA |
| 11198 | PLA Y RAGNONI |
| 11208 | PLATANOS |
| 11211 | PLAYA CHAPADMALAL |
| 11214 | PLAYA LAS MARGARITAS |
| 11215 | PLAYA SERENA |
| 11224 | PLAZA MONTERO |
| 11229 | PLOMER |
| 11265 | POBLET |
| 11281 | POLVAREDAS |
| 11339 | PORVENIR |
| 11388 | POURTALE |
| 11528 | PRESIDENTE DERQUI |
| 11529 | PRESIDENTE QUINTANA |
| 11539 | PRIMERA JUNTA |
| 11599 | PUAN |
| 11606 | PUEBLITOS |
| 11640 | PUEBLO MARTINEZ DE HOZ |
| 11644 | PUEBLO NUEVO |
| 11645 | PUEBLO NUEVO DTO JUNIN |
| 11647 | PUEBLO OTERO |
| 11657 | PUEBLO SAN ESTEBAN |
| 11658 | PUEBLO SAN JOSE |
| 11659 | PUEBLO SANTA MARIA |
| 11669 | PUENTE BATALLA |
| 11673 | PUENTE CASTEX |
| 11674 | PUENTE CANETE |
| 11687 | PUENTE EL OCHENTA |
| 11756 | PUERTO BAHIA BLANCA |
| 11760 | PUERTO BELGRANO |
| 11774 | PUERTO COLOMA |
| 11780 | PUERTO DE ESCOBAR |
| 11793 | PUERTO GALVAN |
| 11810 | PUERTO LA PLATA |
| 11831 | PUERTO NECOCHEA |
| 11854 | PUERTO ROSALES |
| 11875 | PUERTO TRES BONETES |
| 11889 | PUERTO WASSERMANN |
| 12099 | PUJOL |
| 12125 | PUNTA DE CANAL |
| 12148 | PUNTA INDIO |
| 12149 | PUNTA LARA |
| 12152 | PUNTA MEDANOS |
| 12216 | QUENUMA |
| 12232 | QUILCO |
| 12237 | QUILMES |
| 12238 | QUILMES OESTE |
| 12263 | QUIRNO COSTA |
| 12264 | QUIROGA |
| 12279 | QUINIHUAL ESTACION |
| 12292 | RAFAEL CASTILLO |
| 12294 | RAFAEL OBLIGADO |
| 12309 | RAMALLO |
| 12321 | RAMON BIAUS |
| 12325 | RAMON J NEILD |
| 12327 | RAMON SANTAMARINA |
| 12332 | RAMOS OTERO |
| 12333 | RANCAGUA |
| 12338 | RANCHOS |
| 12343 | RANELAGH |
| 12359 | RAUCH |
| 12360 | RAULET |
| 12361 | RAWSON |
| 12365 | REAL AUDIENCIA |
| 12406 | REGINALDO J NEILD |
| 12415 | REMEDIOS DE ESCALADA |
| 12429 | REQUENA |
| 12435 | RETA |
| 12443 | RETIRO SAN PABLO |
| 12458 | RICARDO CANO |
| 12459 | RICARDO GAVINA |
| 12462 | RICARDO ROJAS |
| 12477 | RINCON DE BAUDRIX |
| 12500 | RINCON DE MILBERG |
| 12502 | RINCON DE NOARIO |
| 12513 | RINCON DE VIVOT |
| 12538 | RINCON NORTE |
| 12601 | RIO LUJAN |
| 12638 | RIVADAVIA |
| 12639 | RIVADEO |
| 12641 | RIVERA |
| 12643 | ROBERTO PAYRO |
| 12644 | ROBERTS |
| 12677 | ROJAS |
| 12683 | ROMAN BAEZ |
| 12693 | ROOSEVELT PARTIDO RIVADAVIA |
| 12694 | ROQUE PEREZ |
| 12709 | ROSAS |
| 12733 | RUIZ SOLIS |
| 12752 | RUTA 26 MAQUINISTA F SAVIO |
| 12796 | SAFORCADA |
| 12806 | SALADA CHICA |
| 12814 | SALADILLO |
| 12818 | SALADILLO NORTE |
| 12829 | SALAZAR |
| 12835 | SALDUNGARAY |
| 12838 | SALINA DE PIEDRA |
| 12840 | SALINAS CHICAS |
| 12853 | SALLIQUELO |
| 12858 | SALTO |
| 12866 | SALVADOR MARIA |
| 12870 | SAMBOROMBON |
| 12873 | SAN ADOLFO |
| 12874 | SAN AGUSTIN |
| 12875 | SAN ALBERTO |
| 12880 | SAN ANDRES |
| 12881 | SAN ANDRES DE GILES |
| 12884 | SAN ANTONIO |
| 12886 | SAN ANTONIO DE ARECO |
| 12898 | SAN ANTONIO DE PADUA |
| 12916 | SAN BERNARDO |
| 12918 | SAN BERNARDO DEL TUYU |
| 12921 | SAN CALA |
| 12924 | SAN CARLOS |
| 12929 | SAN CAYETANO |
| 12934 | SAN CORNELIO |
| 12937 | SAN DANIEL |
| 12943 | SAN EDUARDO DEL MAR |
| 12945 | SAN EMILIO |
| 12946 | SAN ENRIQUE |
| 12947 | SAN ERNESTO |
| 12955 | SAN FEDERICO |
| 12956 | SAN FELIPE |
| 12958 | SAN FERMIN |
| 12959 | SAN FERNANDO |
| 12965 | SAN FRANCISCO DE BELLOCQ |
| 12973 | SAN FRANCISCO SOLANO |
| 12980 | SAN GERVACIO |
| 12988 | SAN IGNACIO |
| 12993 | SAN JACINTO |
| 13004 | SAN JORGE |
| 13015 | SAN JOSE DE GALI |
| 13025 | SAN JOSE DE LOS QUINTEROS |
| 13030 | SAN JOSE DE OTAMENDI |
| 13044 | SAN JUAN |
| 13058 | SAN JULIAN |
| 13061 | SAN LAUREANO |
| 13084 | SAN MARTIN DE TOURS |
| 13089 | SAN MAURICIO |
| 13092 | SAN MIGUEL |
| 13093 | SAN MIGUEL ARCANGEL |
| 13097 | SAN MIGUEL DEL MONTE |
| 13098 | SAN MIGUEL DEL MORO |
| 13105 | SAN NICOLAS DE LOS ARROYOS |
| 13110 | SAN PASCUAL |
| 13112 | SAN PATRICIO |
| 13131 | SAN RAFAEL |
| 13136 | SAN RAMON DE ANCHORENA |
| 13142 | SAN ROMAN |
| 13144 | SAN ROQUE |
| 13150 | SAN SEBASTIAN |
| 13152 | SAN SIMON |
| 13156 | SAN VALENTIN |
| 13157 | SAN VICENTE |
| 13189 | SANTA CECILIA CENTRO |
| 13190 | SANTA CECILIA NORTE |
| 13191 | SANTA CECILIA SUD |
| 13195 | SANTA CLARA DEL MAR |
| 13197 | SANTA CLEMENTINA |
| 13198 | SANTA COLOMA |
| 13203 | SANTA ELEODORA |
| 13209 | SANTA FELICIA |
| 13217 | SANTA INES |
| 13218 | SANTA IRENE |
| 13219 | SANTA ISABEL |
| 13227 | SANTA LUISA |
| 13230 | SANTA MARIA |
| 13231 | SANTA MARIA BELLOQ |
| 13247 | SANTA REGINA |
| 13248 | SANTA RITA |
| 13251 | SANTA ROSA |
| 13261 | SANTA ROSA DE MINELLONO |
| 13277 | SANTA TERESA |
| 13279 | SANTA TERESITA |
| 13280 | SANTA TERESITA PERGAMINO |
| 13281 | SANTA TRINIDAD |
| 13289 | SANTIAGO GARBARINI |
| 13296 | SANTO DOMINGO |
| 13304 | SANTO TOMAS |
| 13307 | SANTOS LUGARES |
| 13308 | SANTOS UNZUE |
| 13316 | SARANDI |
| 13318 | SARASA |
| 13331 | SATURNO |
| 13337 | SAUCE CHICO |
| 13339 | SAUCE CORTO |
| 13345 | SAUCE GRANDE |
| 13371 | SAUZALES |
| 13398 | SEGUROLA |
| 13404 | SEMINARIO PIO XII |
| 13423 | SEVIGNE |
| 13430 | SHAW |
| 13435 | SIEMPRE VERDE |
| 13449 | SIERRA DE LA VENTANA |
| 13466 | SIERRAS BAYAS |
| 13498 | SMITH |
| 13508 | SOL DE MAYO |
| 13510 | SOLALE |
| 13513 | SOLANO |
| 13548 | SOURIGUES |
| 13552 | SPERATTI |
| 13553 | SPERONI |
| 13555 | SPURR |
| 13557 | STEGMANN |
| 13568 | SUCRE |
| 13575 | SUIPACHA |
| 13591 | SUNDBLAD |
| 13618 | TABLADA |
| 13730 | TAMANGUEYU |
| 13737 | TAMBO NUEVO |
| 13749 | TAPALQUE |
| 13757 | TAPIALES |
| 13795 | TEDIN URIBURU |
| 13800 | TEJO GALETA |
| 13812 | TENIENTE ORIGONE |
| 13834 | TERMAS LOS GAUCHOS |
| 13841 | THAMES |
| 13851 | TIGRE |
| 13873 | TIMOTE |
| 13889 | TIO DOMINGO |
| 13926 | TOLDOS VIEJOS |
| 13936 | TOMAS JOFRE |
| 13954 | TORNQUIST |
| 13955 | TORO |
| 14029 | TRENQUE LAUQUEN |
| 14031 | TRES  LAGUNAS |
| 14037 | TRES ARROYOS |
| 14051 | TRES CUERVOS |
| 14067 | TRES LEGUAS |
| 14068 | TRES LOMAS |
| 14076 | TRES PICOS |
| 14086 | TRES SARGENTOS |
| 14104 | TRISTAN SUAREZ |
| 14105 | TRIUNVIRATO |
| 14114 | TRONCOS DEL TALAR |
| 14118 | TROPEZON |
| 14122 | TRUJUI |
| 14161 | TURDERA |
| 14177 | TUYUTI |
| 14179 | UBALLES |
| 14186 | UDAQUIOLA |
| 14194 | UNIDAD TURISTICA CHAPADMALAL |
| 14205 | URIBELARREA |
| 14210 | URQUIZA |
| 14242 | VALDEZ |
| 14248 | VALENZUELA ANTON |
| 14249 | VALERIA DEL MAR |
| 14278 | VALLIMANCA |
| 14287 | VASQUEZ |
| 14288 | VANA |
| 14290 | VECINO |
| 14291 | VEDIA |
| 14304 | VELA |
| 14312 | VENANCIO |
| 14325 | VERGARA |
| 14330 | VERONICA |
| 14339 | VIBORAS |
| 14342 | VICENTE LOPEZ |
| 14352 | VICTORINO DE LA PLAZA |
| 14361 | VIEYTES |
| 14362 | VIGELENCIA |
| 14376 | VILLA ADELINA |
| 14379 | VILLA AGUEDA |
| 14399 | VILLA ANGUS |
| 14404 | VILLA ARCADIA |
| 14408 | VILLA ASTOLFI |
| 14413 | VILLA BALLESTER |
| 14429 | VILLA BOSCH |
| 14431 | VILLA BRANDA |
| 14433 | VILLA BROWN |
| 14434 | VILLA BUENOS AIRES |
| 14435 | VILLA BUIDE |
| 14439 | VILLA CACIQUE |
| 14448 | VILLA CARUCHA |
| 14451 | VILLA CASTELAR EST ERIZE |
| 14456 | VILLA CERRITO |
| 14463 | VILLA CLELIA |
| 14475 | VILLA COPACABANA |
| 14487 | VILLA DA FONTE |
| 14494 | VILLA DE MAYO |
| 14501 | VILLA DEL MAR |
| 14510 | VILLA DEPIETRI |
| 14513 | VILLA DIAMANTINA |
| 14515 | VILLA DIAZ VELEZ |
| 14521 | VILLA DOMINICO |
| 14525 | VILLA DUFAU |
| 14535 | VILLA ELENA |
| 14543 | VILLA ESPANA |
| 14544 | VILLA ESPIL |
| 14553 | VILLA FLANDRIA |
| 14557 | VILLA FLORESTA |
| 14558 | VILLA FLORIDA |
| 14561 | VILLA FORTABAT |
| 14562 | VILLA FOX |
| 14567 | VILLA GALICIA |
| 14571 | VILLA GENERAL ARIAS |
| 14580 | VILLA GESELL |
| 14587 | VILLA GODOY |
| 14591 | VILLA GRAL SAVIO EX SANCHEZ |
| 14599 | VILLA HERMINIA |
| 14606 | VILLA IGOLLO |
| 14610 | VILLA IRIS |
| 14612 | VILLA ITALIA |
| 14622 | VILLA LA CHECHELA |
| 14625 | VILLA LA FLORIDA |
| 14640 | VILLA LAURA |
| 14641 | VILLA LAZA |
| 14643 | VILLA LEANDRA |
| 14646 | VILLA LEZA |
| 14647 | VILLA LIA |
| 14650 | VILLA LIBRE |
| 14654 | VILLA LORETO |
| 14665 | VILLA LUZURIAGA |
| 14667 | VILLA LYNCH |
| 14668 | VILLA LYNCH PUEYRREDON |
| 14676 | VILLA MARGARITA |
| 14677 | VILLA MARIA |
| 14682 | VILLA MASSONI |
| 14686 | VILLA MAYOR |
| 14688 | VILLA MAZA |
| 14696 | VILLA MITRE |
| 14701 | VILLA MOQUEHUA |
| 14711 | VILLA NOCITO |
| 14716 | VILLA NUMANCIA |
| 14721 | VILLA OLGA GRUMBEIN |
| 14723 | VILLA ORTEGA |
| 14724 | VILLA ORTIZ |
| 14735 | VILLA PENOTTI |
| 14741 | VILLA PRECEPTOR M ROBLES |
| 14742 | VILLA PRECEPTOR MANUEL CRUZ |
| 14744 | VILLA PROGRESO |
| 14745 | VILLA PUEBLO NUEVO |
| 14746 | VILLA PUERTO QUEQUEN |
| 14756 | VILLA RAFFO |
| 14757 | VILLA RAMALLO |
| 14758 | VILLA RAMALLO ESTACION FFCC |
| 14765 | VILLA RIO CHICO |
| 14776 | VILLA ROSA |
| 14778 | VILLA ROSAS |
| 14783 | VILLA RUIZ |
| 14786 | VILLA SABOYA |
| 14787 | VILLA SAENZ PENA |
| 14788 | VILLA SAN ALBERTO |
| 14801 | VILLA SAN PEDRO |
| 14806 | VILLA SANGUINETTI |
| 14810 | VILLA SANTA MARIA |
| 14816 | VILLA SANTOS TESEI |
| 14820 | VILLA SARITA |
| 14824 | VILLA SAUCE |
| 14825 | VILLA SAURI |
| 14829 | VILLA SENA |
| 14834 | VILLA SOLDATI |
| 14840 | VILLA TALLERES |
| 14850 | VILLA TRIANGULO |
| 14858 | VILLA VALLIER |
| 14859 | VILLA VATTEONE |
| 14865 | VILLA VIGNOLO |
| 14870 | VILLA YORK |
| 14880 | VILLAIGRILLO |
| 14881 | VILLALONGA |
| 14886 | VILLARS |
| 14907 | VIRREY DEL PINO |
| 14909 | VIRREYES |
| 14921 | VITEL |
| 14927 | VIVORATA |
| 14934 | VINA |
| 14944 | VOLTA |
| 14945 | VOLUNTAD |
| 14949 | VUELTA DE OBLIGADO |
| 14950 | VUELTA DE ZAPATA |
| 14966 | WILDE |
| 15076 | YUTUYACO |
| 15081 | ZAMUDIO |
| 15097 | ZAPIOLA |
| 15100 | ZARATE |
| 15103 | ZAVALIA |
| 15106 | ZELAYA |
| 15110 | ZENTENA |
| 15112 | ZOILO PERALTA |
| 15113 | ZONA DELTA SAN FERNANDO |
| 19372 | ADROGUE |
| 19378 | VILLA MADERO |
| 19380 | ANDERSON |
| 19382 | SAN ENRIQUE |
| 19383 | SAN JOSE |
| 19384 | ALTAMIRA |
| 19385 | LA AURORA |
| 19387 | PALANTELEN |
| 21571 | VILLA ITALIA |
| 21572 | LA PROTEGIDA |
| 21573 | SAN BERNARDO |
| 21574 | SANTA ROSA |
| 21578 | LA PORTENA |
| 21579 | MARTIN FIERRO |
| 21580 | SAN RAMON |
| 21582 | LA HORQUETA |
| 21583 | LA PASTORA |
| 21585 | ALGARROBO |
| 21586 | EL PARAISO |
| 21588 | GRACIARENA |
| 21589 | LA MASCOTA |
| 21608 | SAN JACINTO |
| 21609 | SAN JUAN |
| 21610 | COLONIA SAN FRANCISCO |
| 21611 | LAS CORTADERAS |
| 21612 | SAN JUAN |
| 21613 | SAN RAMON |
| 21614 | LA FLORIDA |
| 21615 | LA MASCOTA |
| 21616 | LA REFORMA |
| 21617 | LA VICTORIA |
| 21618 | LAS CHILCAS |
| 21619 | SAN ANTONIO |
| 21620 | COLONIA SANTA ROSA |
| 21621 | SAN ANDRES |
| 21622 | SAN EMILIO |
| 21623 | SAN JOSE |
| 21624 | LA ESPERANZA |
| 21625 | SANTA TERESA |
| 21626 | LOMA NEGRA |
| 21627 | SAN JOSE |
| 21628 | EL JAGUEL |
| 21629 | LOS INDIOS |
| 21630 | SOL DE MAYO |
| 21631 | VILLA PROGRESO |
| 21632 | LA REFORMA |
| 21633 | ALTA VISTA |
| 21634 | ESPARTILLAR |
| 21635 | LA MARGARITA |
| 21636 | ESPORA |
| 21637 | LA FLORIDA |
| 21638 | BELLA VISTA |
| 21639 | ALGARROBO |
| 21640 | LAS FLORES |
| 21641 | LA SARA |
| 21642 | FRANCISCO CASAL |
| 21643 | SAN JUSTO |
| 21644 | LA PERLA |
| 21645 | GERLI |
| 21646 | LOS PINOS |
| 21647 | LA PORTENA |
| 21648 | SANTA ELENA |
| 21649 | VILLA FRANCIA |
| 21650 | LA PRIMAVERA |
| 21651 | LA COLORADA |
| 21652 | SANTA ELENA |
| 21653 | LA VERDE |
| 21654 | SAUCE GRANDE |
| 21655 | GRISOLIA |
| 21656 | EL PITO |
| 21657 | SAN JOSE |
| 21658 | COLONIA SERE |
| 21659 | LA ESTRELLA |
| 21660 | LA PROTEGIDA |
| 21661 | PUEBLO NUEVO |
| 21662 | LA COSTA |
| 21663 | LA HORQUETA |
| 21664 | LA LIMPIA |
| 21665 | PINEYRO |
| 21666 | ARROYO LAS ROSAS |
| 21667 | CANNING |
| 21668 | SANTA ROSA |
| 21669 | LA REFORMA |
| 21670 | MIRAMAR |
| 21671 | LA CHUMBEADA |
| 21672 | LA ESPERANZA |
| 21673 | ESPARTILLAR |
| 21674 | LOMA VERDE |
| 21675 | BARRIO TIRO FEDERAL |
| 21676 | LA FLORIDA |
| 21685 | YRAIZOS |
| 3073 | CLAVERIE |
| 4652 | EL ARAZA |
| 4939 | EL DURAZNO |
| 5548 | EMILIO BUNGE |
| 5553 | EMITA |
| 6332 | GARRO |
| 6915 | INGENIERO ALLAN |
| 7191 | JUAN BLAQUIER |
| 7490 | LA CHUMBEADA |
| 8107 | LA SOFIA |
| 8694 | LAS VAQUERIAS |
| 9275 | LOS POLVORINES |
| 9281 | LOS POZOS |
| 11288 | PONTAUT |
| 14246 | VALENTIN GOMEZ |
| 21575 | GENERAL CONESA |
| 21581 | SANTA INES |
| 21587 | EL RINCON |
| 21576 | CHOIQUE |
| 21577 | LA MARGARITA |
| 19381 | LA TRIBU |
| 21584 | REMEDIOS DE ESCALADA |
| 19386 | SAN JOSE |
| 43 | ABRA DE HINOJO |
| 57 | ABRA MAYO |
| 96 | ADELA CORTI |
| 199 | AGUARA |
| 224 | AGUSTIN ROCA |
| 249 | ALBARINO |
| 296 | ALDECON |
| 314 | ALFA |
| 318 | ALFEREZ SAN MARTIN |
| 353 | ALMACEN CASTRO |
| 364 | ALMIRANTE SOLIER |
| 374 | ALSINA |
| 466 | ALTONA |
| 474 | ALVAREZ DE TOLEDO |
| 506 | AMERICA UNIDA |
| 565 | ANEQUE GRANDE |
| 640 | ARANA |
| 644 | ARANO |
| 682 | ARIEL |
| 704 | ARRECIFES |
| 756 | ARROYO CORTO |
| 773 | ARROYO EL CHINGOLO |
| 780 | ARROYO GRANDE |
| 894 | ASCENCION |
| 946 | AYACUCHO |
| 981 | BAHIA BLANCA |
| 1126 | BALNEARIO CAMET NORTE |
| 1134 | BALNEARIO LA CALETA |
| 1141 | BALNEARIO ORIENTE |
| 1147 | BALNEARIO SANTA ELENA |
| 1170 | BARADERO |
| 1214 | BARRIENTOS |
| 1249 | BARRIO EMIR RAMON JUAREZ |
| 1267 | BARRIO LA FALDA |
| 1273 | BARRIO LA PERLA CASCO URBANO |
| 1287 | BARRIO OESTE |
| 1293 | BARRIO PARQUE PATAGONIA |
| 1307 | BARRIO SAN CAYETANO |
| 1314 | BARRIO SAN PABLO |
| 1356 | BASE NAVAL AZOPARDO |
| 1370 | BATHURST ESTACION |
| 1377 | BAYAUCA |
| 1420 | BECCAR |
| 1452 | BERAZATEGUI |
| 1501 | BO STA CATALINA HORNERO LA L |
| 1533 | BONIFACIO |
| 1541 | BORDEU |
| 1649 | CABILDO |
| 1658 | CABO SAN FERMIN |
| 1669 | CACHARI |
| 1743 | CALERA AVELLANEDA |
| 1755 | CALFUCURA |
| 1790 | CAMET |
| 1793 | CAMINERA AZUL |
| 1920 | CAMPO FUNKE |
| 1942 | CAMPO LA ELISA |
| 1948 | CAMPO LA NENA |
| 1953 | CAMPO LA TRIBU |
| 1964 | CAMPO LOS AROMOS |
| 1981 | CAMPO PELAEZ |
| 2032 | CAMPOMAR VINEDO |
| 2038 | CANAL N ALEM 1A SEC |
| 2049 | CANCHA DEL POLLO |
| 2074 | CANTERA LA AURORA |
| 2081 | CANTERA SAN LUIS |
| 2174 | CARDENAL CAGLIERO |
| 2190 | CARLOS MARIA NAON |
| 2284 | CASBAS |
| 2501 | CENTRO AGRICOLA EL PATO |
| 2688 | CERRO NEGRO |
| 2819 | CHALA QUILCA |
| 2838 | CHAPALEOUFU |
| 2843 | CHAPI TALO |
| 3067 | CLARAZ |
| 3071 | CLAUDIO C MOLINA |
| 3230 | COLONIA BARGA |
| 3241 | COLONIA BEETHOVEN |
| 3394 | COLONIA EL PINCEN |
| 3563 | COLONIA LA GRACIELA |
| 3645 | COLONIA LOS ALFALFARES |
| 3721 | COLONIA MURATURE |
| 3727 | COLONIA NACIONAL DE MENORES |
| 3856 | COLONIA SAN MIGUEL |
| 3877 | COLONIA SANTA MARIA |
| 3947 | COLONIA VELEZ |
| 4103 | CORONEL MALDONADO |
| 4110 | CORONEL MON |
| 4163 | CORTINES |
| 4174 | COSTA AZUL |
| 4241 | CRISTINO BENAVIDEZ |
| 4285 | CUARTEL 6 |
| 4290 | CUATREROS |
| 4305 | CUCHA CUCHA |
| 4376 | DAIREAUX |
| 4389 | DE LA CANAL |
| 4394 | DEL CARRIL |
| 4417 | DESTILERIA FISCAL |
| 4424 | DESVIO EL CHINGOLO |
| 4483 | DOCE DE AGOSTO |
| 4489 | DOCTOR DOMINGO HAROSTEGUY |
| 4516 | DOMSELAAR |
| 4564 | DOYHENARD |
| 4573 | DRYSDALE |
| 4577 | DUFAUR |
| 4589 | DUSSAUD |
| 4598 | EDUARDO COSTA |
| 4766 | EL CARMEN |
| 4816 | EL CHAJA |
| 4894 | EL CRISTIANO |
| 4920 | EL DESTINO |
| 5050 | EL LIBERTADOR |
| 5055 | EL LUCHADOR |
| 5065 | EL MANGRULLO |
| 5180 | EL PARAISO |
| 5184 | EL PARQUE |
| 5241 | EL PITO |
| 5312 | EL RECADO |
| 5326 | EL RETIRO |
| 5354 | EL SANTIAGO |
| 5450 | EL TRIANGULO |
| 5483 | EL VENCE |
| 5559 | EMPALME CERRO CHATO |
| 5567 | EMPALME QUERANDIES |
| 5606 | ESCALADA |
| 5618 | ESPADANA |
| 5702 | ESTACION GENERAL ARENALES |
| 5717 | ESTACION MORENO |
| 5890 | ESTANCIA LAS ISLETAS |
| 5966 | ESTANCIA SANTA CATALINA |
| 5987 | ESTANCIAS |
| 6017 | ETCHEGOYEN |
| 6071 | FARO QUERANDI |
| 6077 | FATRALO |
| 6089 | FELIPE SOLA |
| 6094 | FERNANDO MARTI |
| 6175 | FLORIDA |
| 6212 | FORTIN LAVALLE |
| 6218 | FORTIN PAUNERO |
| 6243 | FRANCISCO CASAL |
| 6288 | FUNKE |
| 6323 | GARDEY |
| 6360 | GENERAL BELGRANO |
| 6388 | GENERAL MANSILLA |
| 6413 | GENERAL SAN MARTIN |
| 6439 | GIRODIAS |
| 6443 | GLEW |
| 6447 | GNECCO |
| 6471 | GOBERNADOR ORTIZ DE ROSAS |
| 6480 | GOBERNADOR UGARTE |
| 6491 | GOMEZ |
| 6499 | GONZALEZ MORENO |
| 6505 | GOROSO |
| 6509 | GOWLAND |
| 6513 | GONI |
| 6632 | GUERRERO |
| 6643 | GUNTHER |
| 6654 | HALCEY |
| 6658 | HARAS 1 DE MAYO |
| 6664 | HARAS EL CISNE |
| 6670 | HARAS LOS CARDALES |
| 6677 | HARAS SAN JACINTO |
| 6688 | HENRY BELL |
| 6715 | HINOJALES |
| 6791 | HUANGUELEN |
| 6902 | INDIO RICO |
| 6917 | INGENIERO BALBIN |
| 6972 | INOCENCIO SOSA |
| 6995 | IRENEO PORTELA |
| 7135 | JARRILLA |
| 7143 | JEPPENER |
| 7158 | JOSE B CASAS |
| 7175 | JOSE MARMOL |
| 7185 | JUAN ATUCHA |
| 7190 | JUAN BAUTISTA ALBERDI |
| 7217 | JUAN VELA |
| 7233 | JULIO ARDITI |
| 7251 | JUNIN |
| 7288 | LA ADELA |
| 7317 | LA AMORILLA |
| 7330 | LA ARGENTINA |
| 7340 | LA AZOTEA GRANDE |
| 7346 | LA BALLENERA |
| 7356 | LA BARRANCOSA |
| 7508 | LA COLMENA |
| 7524 | LA CORINCO |
| 7568 | LA DORITA |
| 7572 | LA DULCE |
| 7731 | LA ISABEL |
| 7776 | LA LIMPIA |
| 7795 | LA LUCILA DEL MAR |
| 7802 | LA MADRECITA |
| 7820 | LA MARIA |
| 7871 | LA NEGRA |
| 7875 | LA NEVADA |
| 7884 | LA NUTRIA |
| 7913 | LA PALMIRA |
| 7917 | LA PAMPA |
| 7935 | LA PAZ CHICA |
| 7946 | LA PESQUERIA |
| 7970 | LA PLATA |
| 7984 | LA PORTENA |
| 8030 | LA RAZON |
| 8046 | LA RESERVA |
| 8069 | LA RUBIA |
| 8131 | LA TOBIANA |
| 8146 | LA TRIBU |
| 8164 | LA VALEROSA |
| 8175 | LA VERDE |
| 8227 | LAGO EPECUEN |
| 8257 | LAGUNA CHASICO |
| 8300 | LAGUNA REDONDA |
| 8350 | LARREA |
| 8362 | LAS ACHIRAS |
| 8381 | LAS BAHAMAS |
| 8462 | LAS CUATRO HERMANAS |
| 8480 | LAS ESCOBAS |
| 8575 | LAS NEGRAS |
| 8615 | LAS PIEDRITAS |
| 8656 | LAS TAHONAS |
| 8671 | LAS TONINAS |
| 8771 | LEZAMA |
| 8789 | LIERRA ADJEMIRO |
| 8800 | LIN CALEL |
| 8822 | LISANDRO OLMOS ETCHEVERRY |
| 8842 | LOBOS |
| 8872 | LOMA HERMOSA |
| 8884 | LOMA VERDE |
| 8932 | LOPEZ |
| 8935 | LOPEZ MOLINARI |
| 9050 | LOS CHANARES |
| 9162 | LOS INDIOS |
| 9172 | LOS LAURELES |
| 9235 | LOS ORTIZ |
| 9265 | LOS PINOS |
| 9365 | LOS TOLDOS |
| 9401 | LOUGE |
| 9405 | LOZANO |
| 9412 | LUCAS MONTEVERDE |
| 9438 | LUJAN |
| 9493 | MAGALLANES |
| 9529 | MALECON GARDELIA |
| 9555 | MALVINAS ARGENTINAS |
| 9610 | MAPIS |
| 9613 | MAQUINISTA F SAVIO |
| 9620 | MAR AZUL |
| 9624 | MAR DE LAS PAMPAS |
| 9642 | MARCOS PAZ B EL ZORZAL |
| 9686 | MARIANO ROLDAN |
| 9700 | MARTIN FIERRO |
| 9710 | MARUCHA |
| 9748 | MAURICIO HIRSCH |
| 9760 | MAYOR BURATOVICH |
| 9766 | MAZA |
| 9774 | MECHA |
| 9778 | MECHONGUE |
| 9786 | MEDANO BLANCO |
| 9826 | MERLO |
| 9940 | MIRAMAR |
| 10021 | MONASTERIO |
| 10049 | MONTE CRESPO |
| 10075 | MONTE VELOZ |
| 10080 | MONTECARLO |
| 10084 | MONTES DE OCA |
| 10105 | MORENO |
| 10150 | MUNIZ |
| 10216 | NEWTON |
| 10289 | NUEVA HERMOSURA |
| 10294 | NUEVA PLATA |
| 10299 | NUEVA SUIZA |
| 10369 | OLIVOS |
| 10398 | ORIENTE |
| 10413 | OTAMENDI |
| 10416 | OTONO |
| 10439 | PABLO PODESTA |
| 10483 | PALANTELEN |
| 10487 | PALEMON HUERGO |
| 10703 | PARAJE LA AURORA |
| 10744 | PARDO |
| 10945 | PAVON |
| 10952 | PAYRO R |
| 10956 | PEARSON |
| 10984 | PELLEGRINI |
| 10997 | PEREYRA IRAOLA PARQUE |
| 11004 | PERGAMINO |
| 11123 | PIGUE |
| 11196 | PINEYRO |
| 11233 | PLUMACHO |
| 11267 | POCITO |
| 11289 | PONTEVEDRA |
| 11520 | PRADERE JUAN A |
| 11614 | PUEBLO BALNEARIO RETA |
| 11972 | PUESTO DEL MEDIO |
| 12117 | PUNTA ALTA |
| 12217 | QUEQUEN |
| 12291 | RAFAEL CALZADA |
| 12331 | RAMOS MEJIA |
| 12383 | RECALDE |
| 12624 | RIO TALA |
| 12649 | ROCHA |
| 12679 | ROLITO ESTACION FCGB |
| 12715 | ROVIRA |
| 12787 | SAAVEDRA |
| 12807 | SALADA GRANDE |
| 12882 | SAN ANDRES DE TAPALQUE |
| 12915 | SAN BENITO |
| 12933 | SAN CLEMENTE DEL TUYU |
| 12944 | SAN ELADIO |
| 12978 | SAN GERMAN |
| 12991 | SAN ISIDRO |
| 13005 | SAN JOSE |
| 13048 | SAN JUAN DE NELSON |
| 13060 | SAN JUSTO |
| 13073 | SAN MANUEL |
| 13090 | SAN MAYOL |
| 13115 | SAN PEDRO |
| 13130 | SAN QUILCO |
| 13134 | SAN RAMON |
| 13151 | SAN SEVERO |
| 13174 | SANSINENA |
| 13178 | SANTA ALICIA |
| 13187 | SANTA CATALINA |
| 13202 | SANTA ELENA |
| 13224 | SANTA LUCIA |
| 13250 | SANTA RITA PDO GUAMINI |
| 13290 | SANTIAGO LARRE |
| 13305 | SANTO TOMAS CHICO |
| 13442 | SIERRA CHICA |
| 13452 | SIERRA DE LOS PADRES |
| 13512 | SOLANET |
| 13532 | SOLIS |
| 13562 | STROEDER |
| 13668 | TACUARI |
| 13743 | TANDIL |
| 13786 | TATAY |
| 13806 | TEMPERLEY |
| 13810 | TENIENTE CORONEL MINANA |
| 13918 | TODD |
| 13953 | TORDILLO |
| 13978 | TORRES |
| 13981 | TORTUGUITAS |
| 14034 | TRES ALGARROBOS |
| 14095 | TRIGALES |
| 14116 | TRONGE |
| 14203 | URDAMPILLETA |
| 14240 | VAGUES |
| 14245 | VALENTIN ALSINA |
| 14308 | VELLOSO |
| 14340 | VICENTE CASARES |
| 14345 | VICENTE PEREDA |
| 14350 | VICTORIA |
| 14366 | VILELA |
| 14377 | VILLA ADRIANA |
| 14386 | VILLA ALDEANITA |
| 14420 | VILLA BELGRANO DTO JUNIN |
| 14436 | VILLA BURGOS |
| 14441 | VILLA CAPDEPONT |
| 14446 | VILLA CAROLA |
| 14455 | VILLA CENTENARIO |
| 14488 | VILLA DAZA |
| 14509 | VILLA DELFINA |
| 14518 | VILLA DOMINGO PRONSATO |
| 14537 | VILLA ELISA |
| 14564 | VILLA FRANCIA |
| 14586 | VILLA GOBERNADOR UDAONDO |
| 14598 | VILLA HARDING GREEN |
| 14609 | VILLA INSUPERABLE |
| 14653 | VILLA LOMA |
| 14670 | VILLA MAIO |
| 14680 | VILLA MARTELLI |
| 14699 | VILLA MONICA |
| 14703 | VILLA MOSCONI |
| 14717 | VILLA OBRERA |
| 14772 | VILLA ROCH |
| 14794 | VILLA SAN JOSE |
| 14805 | VILLA SANCHEZ ELIA |
| 14817 | VILLA SANZ |
| 14830 | VILLA SERRA |
| 14843 | VILLA TERESA |
| 14862 | VILLA VERDE |
| 14875 | VILLAFANE |
| 14884 | VILLANUEVA |
| 14914 | VISTA ALEGRE |
| 14957 | WARNES |
| 15044 | YERBAS |
| 15057 | YRAZOZ |
| 15105 | ZEBALLOS |
| 15109 | ZENON VIDELA DORNA |
| 15124 | ZUBIAURRE |
| 4934 | EL DORADO |
| 8088 | LA SAUDADE |


## Información Adicional

**Validez de los Comprobantes**

La validez de la Carta de Porte Electrónica se determinará teniendo en cuenta los kilómetros a recorrer
y el tipo de transporte a utilizar.

La Carta de Porte Automotor tendrá una validez máxima de 5 días, mientras que la CPE Ferroviaria
contará con hasta 30 días de vencimiento.

Ambos períodos podrán extenderse en caso de declarar “Contingencias”.


**¿En que momento se emite la Carta de Porte Electrónica Flete Corto?**

La CPE Flete Corto se emite automáticamente con la aceptación del “Productor”.
Para ello deberá ingresar hasta 72 horas antes de comenzar el traslado al sistema “Carta de
Porte Electrónica – Consulta CP Flete Corto” y aceptar las CPE FC que se encuentren
pendientes de aceptación.


**¿Cómo funciona la opción “Contingencias”?**

El sistema de CPE permite informar las contingencias que puedan ocurrir en un traslado de
granos.
Desde el momento en que se informa la contingencia, la CPE queda en estado “Activa con
contingencia declarada” y se encuentra inhabilitada para circular.
Cuando se resuelve la misma, la CPE vuelve a quedar en estado “Activa” y habilitada para
continuar el viaje.
Los datos informados en la CPE, incluido el “Código de Turno”, son válidos para continuar el
traslado.


'''¿ Cómo funciona el proceso de confirmación de una CPE cuando el destino es el
campo de un productor?'''

El proceso de confirmación de una CPE por parte de un productor contiene los mismos pasos
que el actual CTG, se deberá realizar primero la “Confirmación de Arribo” y posteriormente la
“Confirmación Definitiva”.

'''¿ Se pueden realizar traslados de granos desde un campo hacia otro campo del
mismo productor ? Se deberá realizar el circuito completo de confirmación?'''

Si, se pueden realizar traslados entre campos de un mismo productor. En estos casos se
deberá realizar el circuito completo de confirmación para que no afecte la cuenta corriente
granaria.





## Novedades

Se recuerda que esta disponible el 
[grupo de noticias](http://www.pyafipws.com.ar) (http://groups.google.com.ar/group/pyafipws) donde
se publicarán futuras novedades sobre PyAfipWS: servicios web de
factura electrónica y sus interfases (se recomienda suscribirse)






