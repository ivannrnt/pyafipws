= Carta de Porte Electrónica Derivados Granarios - RG 5235/2022 =

Interfaz para Servicio Web de AFIP para la emisión de Carta de Porte Electrónica Derivados Granarios para transporte automotor.



## Descripción General

 La Resolución General N° 5235/2022 establece el uso obligatorio de los comprobantes electrónicos denominados Carta de Porte - Derivados Granarios como único documento válido para respaldar el traslado y/o entrega -desde o hasta un operador incluido en el Registro Único de Operadores de la Cadena Agroindustrial “RUCA”, de cualquier tipo de productos y/o subproductos obtenidos del procesamiento y/o manipulación y/o acondicionamiento de granos -cereales y oleaginosas- y legumbres secas (“Derivados Granarios”), a cualquier destino dentro de la REPÚBLICA ARGENTINA mediante el transporte automotor, ferroviario o cualquier otro medio de transporte terrestre (ductos, cintas transportadoras, etc.).

 La “CPEDG” sustituye, a los efectos del traslado de los “Derivados Granarios”, al remito establecido por la Resolución General Nº 1.415 (AFIP), sus modificatorias y complementarias.


**Sujetos Obligados**

Podrán solicitar la Carta de Porte - Derivados Granarios “CPEDG” los siguientes sujetos:

- Operadores incluidos en el Sistema de Información Simplificado (“SISA”) conforme a lo dispuesto en la Resolución General N° 4.310 (AFIP) y sus modificatorias, que asimismo estén registrados en el “RUCA” con estado de matrícula habilitado y que dispongan de una o más plantas declaradas y habilitadas en dicho registro, en las cuales ingresen y/o egresen los “Derivados Granarios”.

- Autorizados mediante resolución fundada de la AFIP




Fecha entrada en vigencia: 01/03/2023




**Micrositio:** https://www.afip.gob.ar/actividadesAgropecuarias/sector-agro/carta-porte-electronica/carta-porte-derivados-granarios/que-es.asp


## Descargas

- Instalador para Homologación (pruebas):  https://www.sistemasagiles.com.ar/soft/pyafipws/PyAfipWs-beta-2.7.2917-32bit+wsaa_2.13a+wscpev2_2.00a-homo.exe
- Documentación:

                 [Documento Oficial WSCPE v2.0.0](https://www.afip.gob.ar/ws/documentos/manual_wscpe.pdf) (AFIP)

                 [Documento Oficial WSCPE v2.0.6 del 25/07/2025](https://www.afip.gob.ar/ws/documentos/manual-wscpe-version-2-0-6.pdf) (ARCA)
 
                  

- [Manual de Uso General](../documentacion_herramientas/manualpyafipws.md) ([PDF](http://www.sistemasagiles.com.ar/trac/wiki/ManualPyAfipWs?format=pdf))


- Código Fuente (Python): [wscpedg.py](https://github.com/reingart/pyafipws/blob/main/wscpedg.py)


## Instalación

Está disponible el instalador para evaluación (ver [Descargas](wiki:CartadePorteDerivadosGranarios#Descargas)), simplemente descargar, ejecutar siguiendo los pasos:

- Aceptar la licencia
- Seleccionar carpeta, por ej `C:\WSCPEDG`
- Instalación y registración automática

Para más información ver el [Manual de Uso](../documentacion_herramientas/manualpyafipws.md#Instalacion)

## Metodos

- **`Conectar(cache=None, url="", proxy="")`**: en homologación no hace falta pasarle ningún parámetro. En producción, el segundo parámetro es la WSDL.
- **`Dummy()`**: devuelve estado de servidores

Métodos generales:

- **`CrearCPE()`**: Inicializa una estructura de CPE vacía para solicitar autorización.
- **`ActualizarCPE()`**: Inicializa una CPE para poder llamar a los métodos de actualización.
- **`AgregarCabecera(tipo_cpe, sucursal, nro_orden)`**: completa los datos básicos de una CPE
- **`AgregarOrigen(es_usuario_industrial, cuit_titular_planta, domicilio_origen_tipo, domicilio_origen_orden, planta)`**: completa los datos de origen de una CPE; IMPORTANTE: usar operador (con planta) o productor, no ambos
- **`AgregarDestino(cuit_destino, domicilio_destino_tipo, domicilio_destino_orden, planta, cuit_destinatario)`**: completa los datos de destino; IMPORTANTE: cuit_destino y cuit_destinatario son opcionales dependiendo del caso.
- **`AgregarIntervinientes(cuit_reminitente_comercial, cuit_mercado_a_termino, cuit_comisionista, cuit_corredor)`**: completa los datos de intervinientes; IMPORTANTE: todos los campos son opcionales
- **`AgregarDatosCarga(cod_grano, cod_derivado_granario, peso_bruto, peso_tara, tipo_embalaj,otro_embalaje, unidad_media, cantidad_unidades, kg_litro_m3, lote, fecha_lote)`**: completa los datos de carga.
- **`AgregarTransporte(cuit_transportist,dominio, fecha_hora_partida,km_recorrer,codigo_turno, cuit_chofer,tarifa, cuit_pagador_flete, mercaderia_fumigada, cuit_intermediario_flete)`**:  completa los datos de transporte; IMPORTANTE: volver a llamar a este método para más de 1 dominio (ej acoplado), sólo completando ese campo.


Métodos para generar una Carta de Porte:

- **`AutorizarCPEAutomotorDG(archivo)`** Solicita una nueva carta de porte del tipo automotor derivados granarios.


NOTA: indicar el nombre al archivo PDF generado por AFIP en un directorio con permisos de escritura (ej. C:\WINDOWS\TEMP)

Métodos específicos:

- **`AceptarEmisionDG()`**: Método para aceptar una carta de porte en estado pendiente de emisión.
- **`RechazarEmisionDG()`**: Método para rechazar una carta de porte en estado pendiente de emisión.
- **`EditarCPEConfirmadaAutomotorDG(nro_ctg, cuit_corredor, cuit_remitente_comercial, cuit_comisionista, observaciones)`**: Permite modificar datos de una CP Automotor DG en estado Confirmado. Disponible desde v.1.07a de 10/23
- **`ConfirmacionDefinitivaCPEAutomotorDG()`**: Informa la confirmación definitiva de una carta de porte existente. Llamar antes a AgregarCabecera(tipo_cpe, cuit_solicitante, sucursal, nro_orden)
- **`DesvioCPEAutomotorDG()`**: Informar el desvío de una carta de porte existente. Requiere AgregarCabecera(tipo_cpe, cuit_solicitante, sucursal, nro_orden) 
- **`NuevoDestinoDestinatarioCPEAutomotorDG()`**: Informa el nuevo destino / destinatario de una carta de porte existente.
- **`RegresoOrigenCPEAutomotorDG()`**: Informa el regreso a origen de una carta de porte automotor de derivados granarios. Requiere AgregarCabecera(tipo_cpe, cuit_solicitante, sucursal, nro_orden) AgregarTransporte(fecha_hora_partida, km_recorrer, codigo_turno)


Métodos adicionales de consulta:
 
- **`ConsultarCPEAutomotorDG(tipo_cpe, cuit_solicitante, sucursal, nro_orden, nro_ctg, archivo, cuit_titular_planta)`**: Busca una CPE existente según parámetros de búsqueda y retorna información de la misma.

- **`ConsultarCPEDGPendienteActivasion(planta)`**: Retorna las CPEs de derivados granarios (Ferrovaria y Automotor) que estén en estado Pendiente de Emisión.
 
 NOTA: ConsultarCPEAutomotorDG, indicar el nombre al archivo PDF generado por AFIP en un directorio con permisos de escritura (ej. C:\WINDOWS\TEMP)

 

Métodos para obtención de tablas de parámetros:

- **`ConsultarProvincias`**: Devuelve un listado con el código y descripción de todas las provincias.
- **`ConsultarLocalidadesPorProvincia`**: Devuelve un listado con el código y descripción de todas las localidades pertenecientes a la provincia indicada como parámetro.
- **`ConsultarTiposGrano`**: Devuelve un listado con el código y descripción de los tipos de granos permitidos.
- **`ConsultarDerivadosGranarios(cuit)`**: Retorna un listado con el código y descripción de todos los derivados granarios existentes.
- **`ConsultarPlantasDG(cuit)`**:  Retorna un listado con las plantas de derivados granarios existentes para la CUIT indicada.
- **`ConsultarTiposEmbalaje`**: Retorna un listado con el código y descripción de todos los tipos de embalaje.
- **`ConsultarUnidadesMedida`**: Retorna un listado con el código y descripción de todas las unidades de medida.

## Ejemplos

### Pseudocódidgo
```
#!python

wscpe = WSCPE()

ok = wscpe.CrearCPE()

        ok = wscpe.AgregarCabecera(
                  tipo_cpe=284,
                  sucursal=221,
                  nro_orden=nro_orden,

        )
        ok = wscpe.AgregarOrigen(
                  es_usuario_industrial=True,
                  cuit_titular_planta=20200000006,
                  domicilio_origen_tipo=2,
                  domicilio_origen_orden=1,
                  planta=1,
            
        )
        ok = wscpe.AgregarDestino(
                  cuit_destino=CUIT,
                  domicilio_destino_tipo=1,
                  domicilio_destino_orden=2,
                  planta=1938,
                  cuit_destinatario=CUIT,

        )
        ok = wscpe.AgregarRetiroProductor(
                  corresponde_retiro_productor=False,
                  es_solicitante_campo=True,
                  certificado_coe=330100025869,
                  cuit_remitente_comercial_productor=20111111112,

        )
        ok = wscpe.AgregarIntervinientes(
                  cuit_reminitente_comercial=20111111112,
                  cuit_mercado_a_termino=20222222223,
                  cuit_comisionista=20222222223,
                  cuit_corredor=20400000000,

        )
        ok = wscpe.AgregarDatosCarga(
                  cod_grano=23, 
                  cod_derivado_granario=136, 
                  peso_bruto=110, 
                  peso_tara=10, 
                  tipo_embalaje=1,  # a granel 
                  otro_embalaje=None, 
                  unidad_media=1, #kg
                  cantidad_unidades=None,
                  kg_litro_m3=None, 
                  lote=None, 
                  fecha_lote=None,
            
        )
        ok = wscpe.AgregarTransporte(
                  cuit_transportista=20333333334,
                  dominio="ZZZ000",
                  fecha_hora_partida="2016-11-17T12:00:39",
                  km_recorrer=500,
                  codigo_turno="00,
                  cuit_chofer=,
                  tarifa=,
                  cuit_pagador_flete=,
                  mercaderia_fumigada=,
                  cuit_intermediario_flete=,
             
        )
        ok = wscpe.AgregarDominio("AC000TU")

        wscpe.LanzarExcepciones = False

        ok = wscpe.AutorizarCPEAutomotorDG()

        # respuesta:
        print("Numero de ctg:", wscpe.NroCTG)
        print("Fecha de emision:", wscpe.FechaEmision)
        print("Estado:", wscpe.Estado, "-", ESTADO_CPE[wscpe.Estado])
        print("Fecha de inicio de estado:", wscpe.FechaInicioEstado)
        print("Fecha de vencimiento:", wscpe.FechaVencimiento)
```


### Visual Basic

#### Autorizar CPEDG
```
#!vb

    ok = WSCPE.CrearCPE()

    tipo_cpe = 284
    cuit_solicitante = "20111111112"
    sucursal = 1
    nro_orden = 1
    planta = 1
    carta_porte = 1
    nro_ctg = 10100000542#
    observaciones = "Notas del transporte"
    ok = WSCPEDG.AgregarCabecera(tipo_cpe, cuit_solicitante, sucursal, nro_orden, planta, carta_porte, nro_ctg, observaciones)
    
    es_usuario_industrial = True
    cuit_titular_planta = "20200000006"
    domicilio_origen_tipo = 2
    domicilio_origen_orden = 1
    planta = 1
    ok = WSCPE.AgregarOrigen(es_usuario_industrial, cuit_titular_planta, domicilio_origen_tipo, domicilio_origen_orden, planta)
    
    cuit_destino = "20111111112"
    domicilio_destino_tipo = 1
    domicilio_destino_orden = 2
    planta = 1938
    cuit_destinatario = CUIT
    ok = WSCPE.AgregarDestino(cuit_destino, domicilio_destino_tipo, domicilio_destino_orden, planta, cuit_destinatario)
    
    corresponde_retiro_productor = True
    es_solicitante_campo = True
    certificado_coe = "330100025869"
    cuit_remitente_comercial_productor = "20111111112"
    ok = WSCPE.AgregarRetiroProductor(corresponde_retiro_productor, es_solicitante_campo, certificado_coe, cuit_remitente_comercial_productor)
        
    cuit_reminitente_comercial = "20111111112"
    cuit_mercado_a_termino = "20222222223"
    cuit_comisionista = "20222222223"
    cuit_corredor = "20400000000"
    ok = WSCPE.AgregarIntervinientes(cuit_reminitente_comercial, cuit_mercado_a_termino, cuit_comisionista, cuit_corredor)
    
    cod_grano = 23
    cod_derivado_granario = 136
    peso_bruto = 110
    peso_tara = 10
    tipo_embalaje = 1
    otro_embalaje = vbNull
    unidad_media = 1
    cantidad_unidades = vbNull
    kg_litro_m3 = vbNull
    lote = vbNull
    fecha_lote = vbNull
    ok = WSCPE.AgregarDatosCarga(cod_grano, cod_derivado_granario, peso_bruto, peso_tara, tipo_embalaje, otro_embalaje, unidad_media, cantidad_unidades, kg_litro_m3, lote, fecha_lote)
    
    cuit_transportista = "20333333334"
    cuit_transportista_tramo2 = "20222222223"
    nro_vagon = 55555556
    nro_precinto = 1
    nro_operativo = "1111111111"
    dominio = "AB001ST"
    fecha_hora_partida = "2021-08-21T23:29:26.579557"
    km_recorrer = 500
    codigo_turno = "00"
    cuit_chofer = "20333333334"
    tarifa = 100.1
    cuit_pagador_flete = "20333333334"
    mercaderia_fumigada = True
    cuit_intermediario_flete = "20333333334"
    codigo_ramal = False
    descripcion_ramal = "XXXXX"
    tarifa_referencia = vbNull
    ok = WSCPE.AgregarTransporte(cuit_transportista, cuit_transportista_tramo2, nro_vagon, nro_precinto, nro_operativo, dominio, fecha_hora_partida, km_recorrer, codigo_turno, cuit_chofer, tarifa, cuit_pagador_flete, mercaderia_fumigada, cuit_intermediario_flete, codigo_ramal, descripcion_ramal, tarifa_referencia)
    
    ' ok = WSCPE.LoadTestXML(App.Path & "\autorizar.xml")
    
    archivo = App.Path & "\cpe.pdf"
    ok = WSCPE.AutorizarCPEAutomotorDG(archivo)
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

#### Consultar CPEDG Generados
```
#!vb

    
    ok = WSCPE.LoadTestXML(App.Path & "\consultar.xml")
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
        

    

Exit Sub
ManejoError:
    ' Si hubo error:
    Debug.Print Err.Description            ' descripci�n error afip
    Debug.Print Err.Number - vbObjectError ' codigo error afip
    Select Case MsgBox(Err.Description, vbCritical + vbRetryCancel, "Error:" & Err.Number - vbObjectError & " en " & Err.Source)
        Case vbRetry
            Debug.Assert False
            Resume
        Case vbCancel
            Debug.Print Err.Description
    End Select
    Debug.Print WSCPE.XmlRequest
    Debug.Assert False

End Sub


    
## Tablas de Parámetros

### Tipos CPEDG

| 284 | CPE Automotor |
|---|---|
| 285 | CPE Ferroviaria |
| 286 | CPE Emitida en Destino |
| 287 | CPE Ductos |

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

### Derivados Granarios

| Grano Padre | Grano Padre Descripcion | Codigo | Descripcion |
|---|---|---|---|
| 35 | Arroz | 136 | DESECHOS DE ARROZ |
| 16 | Avena | 137 | DESECHOS DE AVENA |
| 50 | Otros Granos | 119 | BALANCEADO y/o SUPLEMENTO GRANARIO PARA AVES |
| 50 | Otros Granos | 120 | BALANCEADO y/o SUPLEMENTO GRANARIO PARA BOVINOS |
| 50 | Otros Granos | 121 | BALANCEADO y/o SUPLEMENTO GRANARIO PARA EQUINOS |
| 50 | Otros Granos | 123 | BALANCEADO y/o SUPLEMENTO GRANARIO PARA OVINOS |
| 50 | Otros Granos | 124 | BALANCEADO y/o SUPLEMENTO GRANARIO PARA PORCINOS |
| 100 | Cebada | 287 | PELLETS DE CEBADA |
| 107 | Colza/Canola | 225 | TORTA DE PRESIÓN DE COLZA |
| 2 | Girasol | 101 | ACEITE CRUDO DE GIRASOL |
| 2 | Girasol | 138 | DESECHOS DE GIRASOL |
| 2 | Girasol | 144 | EXPELLER DE GIRASOL |
| 2 | Girasol | 152 | GIRASOL QUEBRADO ¿ PARTIDO |
| 2 | Girasol | 199 | PELLETS DE GIRASOL |
| 2 | Girasol | 204 | PRENSADO DE GIRASOL |
| 1 | Lino | 222 | TORTA DE PRESION DE LINO |
| 19 | Maíz | 102 | ACEITE CRUDO DE MAÍZ |
| 19 | Maíz | 139 | DESECHOS DE MAÍZ |
| 19 | Maíz | 187 | MAÍZ QUEBRADO - PARTIDO |
| 19 | Maíz | 200 | PELLETS DE MAÍZ |
| 101 | Maní | 223 | TORTA DE PRESIÓN DE MANÍ |
| 23 | Soja | 103 | ACEITE CRUDO DE SOJA |
| 23 | Soja | 140 | DESECHOS DE SOJA |
| 23 | Soja | 145 | EXPELLER DE SOJA |
| 23 | Soja | 146 | EXTRUJADO DE SOJA |
| 23 | Soja | 201 | PELLETS DE SOJA |
| 23 | Soja | 205 | PRENSADO DE SOJA |
| 23 | Soja | 218 | SOJA DESACTIVADA |
| 23 | Soja | 219 | SOJA QUEBRADO ¿ PARTIDO |
| 23 | Soja | 220 | SOJA TOSTADA |
| 23 | Soja | 221 | SOJILLA |
| 104 | Sorgo | 141 | DESECHOS DE SORGO |
| 104 | Sorgo | 202 | PELLETS DE SORGO |
| 103 | Trigo | 142 | DESECHOS DE TRIGO |
| 103 | Trigo | 226 | TRIGO QUEBRADO ¿ PARTIDO |
| 103 | Trigo | 227 | TRIGUILLO |


## Información Adicional

**Validez de los Comprobantes**

La carta de porte electrónica DG automotor tendrá una validez de 10 días, mientras que la carta de porte electrónica DG ferroviaria contará con 30 días hasta su vencimiento. 

Ambos períodos podrán extenderse en caso de declarar “Contingencias”.


