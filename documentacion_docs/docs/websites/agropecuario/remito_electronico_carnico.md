# Remito Electrónico Cárnico - RG4256/18 RG4303

Interfaz para Servicio Web de AFIP para la emisión de Remito de carnes y subproductos derivados de la faena de bovinos y porcinos, Resolución General 4256/18 y Resolución General 4303/18.


## Descripción General

WSRemCarne (Web Service Remito Electrónico Cárnico) es un nuevo Servicio Web de la AFIP para la emisión de Remito de carnes y subproductos derivados de la faena de bovinos y porcinos. El REC se emitirá para amparar el traslado desde su origen hasta el lugar de destino, siendo un ejemplar para entregar al destinatario / receptor y uno suscripto por el destinatario/receptor como constancia documental de la entrega.

Se encuentran obligados a emitir el REC las personas humanas, sucesiones indivisas, empresas o explotaciones unipersonales, sociedades, asociaciones y demás personas jurídicas que desarrollen cualquiera de las actividades que se detallan a continuación:
Frigorífico / Establecimiento faenador, Usuarios de Faena, Abastecedor, Despostadero, Consignatario de Carnes, Consignatario Directo.

Próxima a entrar en vigencia (Noviembre de 2018):
Las disposiciones establecidas en la presente tendrán vigencia desde el primer día del segundo mes inmediato posterior al 31 de agosto de 2018. Además, se prorroga al 01 de noviembre de 2018 la obligación de emitir el Remito Electrónico Cárnico como único documento válido para el traslado automotor dentro del país de carnes y subproductos de faena de las especies bovina/bubalina y porcina.



## Descargas

- Instalador: [PyAfipWs-2.7.2140-32bit+wsaa_2.11c+wsremcarne_1.01b-homo.exe](https://www.sistemasagiles.com.ar/soft/pyafipws/PyAfipWs-2.7.2140-32bit+wsaa_2.11c+wsremcarne_1.01b-homo.exe) V 2.0
- Documentación AFIP: [Documento Oficial WSRemCarne v3.5](https://www.afip.gob.ar/ws/remitoElecCarnico/Manual_Desarrollador_WSREMCARNE_v3_5.pdf)
- Ejemplo en Visual Basic / Visual Fox Pro: 
- [remito_electronico_carnico.vbs](https://raw.githubusercontent.com/reingart/pyafipws/master/ejemplos/remito_electronico_carnico.vbs) (VB script)
- [remito_electronico_carnico.prg](https://raw.githubusercontent.com/reingart/pyafipws/master/ejemplos/remito_electronico_carnico.prg)  (VFP)
- Archivos de intercambio (muestras): 
- Generación (texto plano JSON): [attachment:wsremcarne.json]
- Código Fuente (Python): [wsremcarne.py](https://github.com/reingart/pyafipws/blob/master/wsremcarne.py)






## Metodos

- **`Conectar(cache=None, url="", proxy="")`**: en homologación no hace falta pasarle ningún parámetro. En producción, el segudo parametro es la WSDL.
- **`Dummy()`**: devuelve estado de servidores

Métodos para generar un Remito Electrónico Cárnico (REC):

- **`CrearRemito(tipo_comprobante, punto_emision, tipo_movimiento, categoria_emisor, cuit_titular_mercaderia, cod_dom_origen, tipo_receptor, categoria_receptor, cuit_receptor, cuit_depositario, cod_dom_destino, cod_rem_redestinar, cod_remito, estado)`**: crea un remito interno a autorizar, inicializando los datos de cabecera (fecha_recepcion a categoria_receptor son opcionales.
- **`AgregarViaje(cuit_transportista, cuit_conductor, fecha_inicio_viaje, distancia_km)`**: agrega los datos del viaje
- **`AgregarVehiculo(dominio_vehiculo, dominio_acoplado)`**: agrega los datos del vehiculo al viaje
- **`AgregarMercaderia(orden, cod_tipo_prod, cantidad, unidades, tropa)`**: agrega el detalle de cada item de la mercadería (pueden ser varios items)
- **`AgregarDatosAutorizacion(nro_remito, cod_autorizacion, fecha_emision, fecha_vencimiento):`**: agrega los datos de autorización (opcional)
- **`AgregarContingencias(tipo, observacion)`**: agrega  contingencias al remito 

Métodos principales específicos para Remito Electrónico Cárnico (REC):

- **`GenerarRemito(id_req, archivo="qr.png")`**: Informar los datos necesarios para la generación de un remito nuevo
- **`EmitirRemito(archivo="qr.png")`**: Emitir Remitos que se encuentren en estado Pendiente de Emitir. Llamar previamente a `CrearRemito(..., cod_remito)` y permite cambiar datos vía `AgregarViaje` / `AgregarVehiculo`.
- **`AutorizarRemito(archivo="qr.png")`**: Autorizar o denegar un remito (cuando corresponde autorizacion) por parte del titular/depositario. Llamar previamente a `CrearRemito(..., cod_remito, estado)`.
- **`AnularRemito()`**: Anular un remito generado que aún no haya sido emitido. Llamar previamente a `CrearRemito(..., cod_remito)`.

Métodos adicionales de consulta:

- **`ConsultarUltimoRemitoEmitido(tipo_comprobante=995, punto_emision)`**: devuelve el último No de comprobante registrado por AFIP (atributos `CodRemito`, `NroRemito`, etc.). 
- **`ConsultarRemito(cod_remito, id_req, tipo_comprobante, punto_emision, nro_comprobante)`**: obtiene los datos de un remito generado en AFIP (atributos `CodRemito`, `NroRemito`, etc.). Usar null o similar en los parámetros opcionales.
- **`ConsultarCodigosDomicilio(cuit_titular)`**: depósitos que tiene habilitados para operar el cuit informado
- **`ConsultarReceptoresValidos(cuit_receptor)`**: permite consultar receptores que están impedidos de recibir nuevos remitos (v3.5) **NUEVO!!**


 (Aún no implementados por AFIP)

- **`Cantidad_recibida en mercaderias`**: posiblemente se utilice en consultas (devuelto por AFIP) (v2.0)
- **`ConsultarRemito(cuit_emisor)`**: consultar remito ahora recibe un cuit_emisor como criterio de búsqueda (opcional) (v2.0)


Métodos para obtención de tablas de parámetros:

- **`ConsultarTiposComprobante`**:
- **`ConsultarTiposContingencia`**:
- **`ConsultarTiposCategoriaEmisor`**:
- **`ConsultarTiposCategoriaReceptor`**:
- **`ConsultarTiposEstados`**:
- **`ConsultarGruposCarne`**:
- **`ConsultarTiposCarne`**:


Métodos Nuevos v 2.0 (a revisar):

- **`RegistrarRecepcion: permite registrar la recepción de la mercaderia (total o parcial); similar a AutorizarRemito pero habría que llamar a AgregarMercadería con cantidad y orden (si es parcial). Requeriría llamar previamente a CrearRemito interno con cod_remito, categoria_receptor, estado.`**
- **`ConsultarRemitosAutorizador(cuit_emisor, estado_autorizacion, nro_pagina, rango_fechas, rol_autorizador): devuelve listado de remitos (encabezado: cod_remito, cuit_emisor, estado_actual, fecha_oper, id_req, nro_remito, punto_emision, tipo_comprobante). Posiblemente requiera métodos auxiliares ya que devuelve resultados paginados (múltiples llamadas).`**
- **`ConsultarRemitosEmisor: idem`**
- **`ConsultarRemitosReceptor: idem`**
- **`ConsultarEstadosRemito(cod_remito, cuit_emisor, id_req, nro_comprobante, punto_emision, tipo_comprobante): devuelve cuit_usuario, desc_usuario, estado, fecha`**


## Atributos

Propiedaedes:

- **`CodRemito`** devuelto por AFIP
- **`NroRemito`**
- **`CodAutorizacion`**, **`FechaEmision`**, **`FechaVencimiento`**
- **`Estado`**: PAT (pendiente autorizar), EMI (emitido)
- **`Resultado`**: aprobado / rechazado
- **`ErrCode`**, **`ErrMsg`**: errores de AFIP
- **`Excepcion`**, **`Traceback`**: errores internos
- **`Obs`**, **`Evento`**: observaciones y eventos informativos

Listas:

- **`Errores`**, **`ErroresFormato`**
- **`Observaciones`**, **`Eventos`**

## Herramienta por consola

La interfaz presenta una herramienta universal (multiplataforma -Linux / Windows / Mac- compatible con cualquier lenguaje de programación), que puede ser operado de manera automática en segundo plano (no requiere intervención del usuario).

El modo de uso es ejecutando el programa **`WSREMCARNE_CLI.EXE`** con las siguientes opciones y archivos de intercambio.
La herramienta puede ser ejecutada interactivamente en una consola (Inicio, Ejecutar, CMD.EXE) o puede ser llamada desde otro programa o script .BAT

### Parámetros por línea de comando

La herramienta soporta las siguientes opciones principales:

- `--dummy`: consulta estado de servidores
- `--generar``: genera un remito electrónico cárnico
- `--emitir`: emite un remito
- `--anular`: anula un remito
- `--autorizar`: autoriza un remito

Recuperación de datos:

- `--consultar`: recupera un remito electrónico cárnico
- `--ult`: obtiene el último número de comprobante registrado en AFIP

Tablas de referencias:

- `--tipos_comprobante`: tabla de parametros para tipo de comprobante
- `--tipos_contingencia`: tipo de contingencia que puede reportar
- `--tipos_categoria_emisor`: tipos de categorías de emisor
- `--tipos_categoria_receptor`: tipos de categorías de receptor
- `--tipos_estados`: estados posibles en los que puede estar un remito cárnico
- `--grupos_carne`: grupos de los distintos tipos de cortes de carne
- `--tipos_carne`: tipos de corte de carne

Archivo de Intercambio JSON:

- `--cargar`: toma los datos del REC del archivo de entrada
- `--grabar`: guarda el resultado del REC en archivo de salida
- `--prueba`: genera y guarda un REC de prueba (no usar en producción!)

Parámetros auxiliares:

- `--ayuda`: este mensaje
- `--debug`: modo depuración (detalla y confirma las operaciones)
- `--xml`: almacena los requerimientos y respuestas XML (depuración)

### Ejemplo

Generar un REC (Remito Electrónico Cárnico) de prueba (no usar en producción):

```
C:\PYAFIPWS\> WSREMCARNE_CLI.EXE --generar --cargar --guardar --prueba 

Resultado:  A
Cod Remito:  35
Observaciones:  []
Errores: []
Errores Formato: []
Evento: 1111: version beta
hecho.
```

### Archivo de Configuración

Para utilizar este webservice, debe tramitarse un certificado. Ver [Instructivo](../documentacion_herramientas/manualpyafipws.md#certificados)

Luego, se debe configurar el Certificado, clave privada y URL en el archivo de configuración WSREMCARNE.INI:

```
[WSAA]
CERT=reingart.crt
PRIVATEKEY=reingart.key
##URL=https://wsaa.afip.gov.ar/ws/services/LoginCms

[WSRemCarne]
CUIT=20267565393
ENTRADA=entrada.json
SALIDA=salida.json
##URL=https://serviciosjava.afip.gob.ar/wsremcarne/RemCarneService?wsdl
```

Para producción, se debe usar un instalador para tal fin y descomentar la URL (eliminando el numeral). 

El tipo de archivo de intercambio depende de la extensión configurada en WSRemCarne (usar .json para JavaScript)

## Archivo de Intercambio

La herramienta por consola podría soportar tanto:

- archivo JSON de texto (notación de objetos !JavaScript): : ver [attachment:wsremcarne.json] (muestras ejemplo)


## Ejemplo Pseudocodigo

### Visual Basic (ActiveX simil OCX)

Ejemplo compatible para Visual Fox Pro y otros lenguajes que soporten Componentes (COM) ActiveX, similares a un OCX/DLL.

- Consultar último Remito emitido
- Generar un Remito Electrónico Cárnico:

```
' Conectar al Web Service Remito Carne
wsdl = "https://wswhomo.afip.gov.ar/wsfev1/service.asmx?WSDL"
WSRemCarne.Conectar "", wsdl

' Consultar último comprobante autorizado en AFIP
tipo_comprobante = 995
punto_emision = 1
ok = WSRemCarne.ConsultarUltimoRemitoEmitido(tipo_comprobante, punto_emision)

If ok Then
    ult = WSRemCarne.NroRemito
Else
    ult = 0
End If
Debug.Print "Ultimo comprobante: ", ult
Debug.Print "ErrMsg:", WSRemCarne.ErrMsg
if WSRemCarne.Excepcion <> "" Then Debug.Print WSRemCarne.Excepcion, "Excepcion:"

' Establezco los valores del remito a autorizar:
categoria_emisor = 1
cuit_titular_mercaderia = "20222222223"
cod_dom_origen = 1
tipo_movimiento = "ENV" ' "ENV": Envio Normal, "PLA": Retiro en planta, "REP": Reparto, RED: Redestino
tipo_receptor = "EM"  ' "EM": DEPOSITO EMISOR, "MI": MERCADO INTERNO, "RP": REPARTO
categoria_receptor = 1
cuit_receptor = "20111111112"
cuit_depositario = Null
cod_dom_destino = 1
cod_rem_redestinar = Null
cod_remito = Null
estado = Null

ok = WSRemCarne.CrearRemito(tipo_comprobante, punto_emision, tipo_movimiento, categoria_emisor, _
                            cuit_titular_mercaderia, cod_dom_origen, tipo_receptor, _
                            categoria_receptor, cuit_receptor, cuit_depositario, _
                            cod_dom_destino, cod_rem_redestinar, cod_remito, estado)

' Agrego el viaje:
cuit_transportista = "20333333334"
cuit_conductor = "20333333334"
fecha_inicio_viaje = "2018-10-01"
distancia_km = 999
ok = WSRemCarne.AgregarViaje(cuit_transportista, cuit_conductor, fecha_inicio_viaje, distancia_km)

' Agregar vehiculo al viaje
dominio_vehiculo = "AAA000"
dominio_acoplado = "ZZZ000"
ok = WSRemCarne.AgregarVehiculo(dominio_vehiculo, dominio_acoplado)

' Agregar Mercadería (repetir para varios items)
orden = 1
tropa = 1
cod_tipo_prod = "2.13"
cantidad = 10
unidades=1
ok = WSRemCarne.AgregarMercaderia(orden, cod_tipo_prod, cantidad, unidades, tropa)

' Solicito CodRemito:
id_req = Int(DateDiff("s","20-Oct-18 00:00:00", Now))     ' usar un numero interno único / clave primaria (id_remito)
archivo = "qr.png"
ok = WSRemCarne.GenerarRemito(id_req, archivo)

Debug.Print "Resultado: ", WSRemCarne.Resultado
Debug.Print "Cod Remito: ", WSRemCarne.CodRemito
If WSRemCarne.CodAutorizacion Then
    Debug.Print "Numero Remito: ", WSRemCarne.NumeroRemito
    Debug.Print "Cod Autorizacion: ", WSRemCarne.CodAutorizacion
    Debug.Print "Fecha Emision", WSRemCarne.FechaEmision
    Debug.Print "Fecha Vencimiento", WSRemCarne.FechaVencimiento
End If
Debug.Print "Observaciones: ", WSRemCarne.Obs
Debug.Print "Errores:", WSRemCarne.ErrMsg
Debug.Print "Evento:", WSRemCarne.Evento

If not ok Then 
    ' Imprimo pedido y respuesta XML para depuración (errores de formato)
    Debug.Print "Traceback", WSRemCarne.Traceback
    Debug.Print "XmlResponse", WSRemCarne.Traceback
    Debug.Print "XmlRequest", WSRemCarne.Traceback
End If
```

### Python

Generar un Remito Electrónico Cárnico:

```
#!python

# crear y completar internamente la estructura del remito a enviar a AFIP

wsremcarne.CrearRemito(tipo_comprobante=995, punto_emision=1, categoria_emisor=1,
                       cuit_titular_mercaderia='20222222223', cod_dom_origen=1,
                       tipo_receptor='EM',  # 'EM': DEPOSITO EMISOR, 'MI': MERCADO INTERNO, 'RP': REPARTO
                       categoria_receptor=1,
                       cuit_receptor='20111111112', cuit_depositario=None,
                       cod_dom_destino=1, cod_rem_redestinar=None, cod_remito=None, estado=None)
wsremcarne.AgregarViaje(cuit_transportista='20333333334', cuit_conductor='20333333334',
                        fecha_inicio_viaje='2018-10-01', distancia_km=999)
wsremcarne.AgregarVehiculo(dominio_vehiculo='AAA000', dominio_acoplado='ZZZ000')
wsremcarne.AgregarMercaderia(orden=1, tropa=1, cod_tipo_prod='2.13', cantidad=10, unidades=1)
wsremcarne.AgregarContingencias(tipo=1, observacion="anulacion")

ok = wsremcarne.GenerarRemito(id_req=id_req=int(time.time()))
print "Resultado: ", wsremcarne.Resultado
print "Cod Remito: ", wsremcarne.CodRemito
if wsremcarne.CodAutorizacion:
    print "Numero Remito: ", wsremcarne.NumeroRemito
    print "Cod Autorizacion: ", wsremcarne.CodAutorizacion
    print "Fecha Emision", wsremcarne.FechaEmision
    print "Fecha Vencimiento", wsremcarne.FechaVencimiento
print "Observaciones: ", wsremcarne.Observaciones
print "Errores:", wsremcarne.Errores
print "Errores Formato:", wsremcarne.ErroresFormato
print "Evento:", wsremcarne.Evento

```

## Tablas de Parámetros

### Tipos de Comprobante

| 995 | Remito Electrónico Cárnico |
|---|---|

### Tipos de Contingencia

| 1 | Evento que ocasiona anulación del Remito |
|---|---|
| 2 | Evento que produjo pérdida de mercadería y que ocasiona anulación del Remito |
| 3 | Demoras en traslado |
| 4 | Accidente vial |
| 5 | Robo de mercadería |
| 6 | Destrucción de mercadería |
| 7 | Otros siniestros |
| 8 | Anulación total y regreso a planta |


### Tipos Categoría Emisor

| 1 | Frigorífico / Establecimiento Faenador |
|---|---|
| 2 | Usuario Faena |
| 3 | Abastecedor |
| 4 | Despostador |
| 5 | Consignatario Cárnico |
| 6 | Consignatario Directo |


### Tipos Categoría Receptor

| 1 | Frigorífico / Establecimiento Faenador |
|---|---|
| 2 | Usuario Faena |
| 3 | Abastecedor |
| 4 | Despostador |
| 5 | Consignatario Cárnico |
| 6 | Consignatario Directo |
| 7 | Cámara de frío/Depósito/etc. |
| 8 | Carnicero |


### Tipos Receptor

| EM | DEPOSITO EMISOR |
|---|---|
| MI | MERCADO INTERNO |
| RP | REPARTO |


### Tipos de Movimiento

| ENV | Envio Normal |
|---|---|
| PLA | Retiro en planta |
| REP | Reparto |
| RED | Redestino |

### Tipos Estado

| PAT | Pendiente de Autorizar por Titular |
|---|---|
| PAD | Pendiente de Autorizar por Depositario |
| PEM | Pendiente de Emitir |
| EMI | Emitido |
| ACE | Aceptado |
| ACP | Aceptado Parcialmente |
| NAC | No Aceptado |
| DEN | Denegado |
| ANU | Anulado |
| ANU | Anulado |
| ANU | Anulado |
| BOR | Borrador |

### Grupos de Carne

| 1 | Bovina - media res c/hueso |
|---|---|
| 2 | Bovina - cuarto delantero c/hueso |
| 3 | Bovina - cuarto trasero c/hueso |
| 4 | Bovina - media res s/hueso |
| 5 | Bovina - cuarto delantero s/hueso |
| 6 | Bovina - cuarto trasero s/hueso |
| 7 | Bovina - menudencias |
| 8 | Bovina - vísceras |
| 9 | Bovina - grasas |
| 10 | Bovina - huesos |
| 11 | Bovina - opoterápicos |
| 12 | Bovina - otros |
| 13 | Porcina |


### Tipos de carne

| 1.1 | Media res con hueso |
|---|---|
| 2.1 | Asado a 10 costillas "plancha" (con hueso) |
| 2.2 | Asado a 10 costillas con vacío y matambre (con hueso) |
| 2.3 | Asado a 13 costillas "plancha" (con hueso) |
| 2.4 | Asado con vacío (con hueso) |
| 2.5 | Asado exportación (con hueso) |
| 2.6 | Bife 10 costillas (con hueso) |
| 2.7 | Bife 10 costillas con lomo (con hueso) |
| 2.8 | Bife 4 costillas con lomo (con hueso) |
| 2.9 | Bife ancho 4 costillas (con hueso) |
| 2.10 | Corte "chuck and blade": cogote, aguja, carnaza, paleta y asado 5 ó 6 costillas (con hueso) |
| 2.11 | Corte "crops": cogote, aguja, bife ancho, carnaza de paleta y parte del asado (con hueso) |
| 2.12 | Corte "pony": aguja, carnaza, de paleta y parte del asado (con hueso) |
| 2.13 | Corte "ribs and ponies": bife ancho, aguja, carnaza de paleta y parte del asado (con hueso) |
| 2.14 | Cuarto delantero (con hueso) |
| 2.15 | Cuarto delantero 10 costillas (con hueso) |
| 2.16 | Cuarto delantero 3 costillas (con hueso) |
| 2.17 | Cuarto delantero 3 costillas con falda (con hueso) |
| 2.18 | Cuarto delantero 4 costillas (con hueso) |
| 2.19 | Cuarto delantero 5 costillas (con hueso) |
| 2.20 | Cuarto delantero 8 costillas (con hueso) |
| 2.21 | Cuarto delantero 9 costillas (con hueso) |
| 2.22 | Cuarto delantero con vacío (con hueso) |
| 2.23 | Cuarto delantero sin asado (con hueso) |
| 2.24 | Garrón / brazuelo (osobuco) |
| 2.25 | Pecho 3 costillas (con hueso) |
| 2.26 | Pecho de exportación  (con hueso) |
| 3.1 | Asado con vacío (con hueso) |
| 3.2 | Bife ancho 4 costillas (con hueso) |
| 3.3 | Bife angosto con lomo a 4 costillas (con hueso) |
| 3.4 | Bife angosto y ancho a 8 costillas con lomo (con hueso) |
| 3.5 | Bifes angostos con lomo (con hueso) |
| 3.6 | Bifes angostos con lomo y cuadril (con hueso) |
| 3.7 | Bifes angostos y anchos (con hueso) |
| 3.8 | Cuarto trasero 3 costillas (con hueso) |
| 3.9 | Nalga de afuera, nalga de adentro y tortuguita (con hueso) |
| 3.10 | Pierna (con hueso) |
| 3.11 | Pierna mocha (con hueso) |
| 3.12 | Pierna mocha / mocho (con hueso) |
| 3.13 | Pistola 3 costillas (con hueso) |
| 3.14 | Pistola 3 costillas sin garrón (con hueso) |
| 3.15 | Pistola 4 costillas (con hueso) |
| 3.16 | Pistola 5 costillas (con hueso) |
| 3.17 | Pistola 5 costillas sin garrón (con hueso) |
| 3.18 | Pistola 7 costillas (con hueso) |
| 3.19 | Pistola 7 costillas sin garrón (con hueso) |
| 3.20 | Pistola 8 costillas (con hueso) |
| 3.21 | Pistola 10 costillas (con hueso) |
| 3.22 | Rueda (con hueso) |
| 3.23 | Rueda con cuadril / pierna mocha (con hueso) |
| 3.24 | Rueda con cuadril sin garrón / pierna mocha sin garrón (con hueso) |
| 3.25 | Rueda sin garrón (con hueso) |
| 4.1 | Media res sin hueso (manta) |
| 5.1 | Aguja |
| 5.2 | Aguja con cogote |
| 5.3 | Aguja con paleta |
| 5.4 | Asado con vacío (sin hueso) |
| 5.5 | Bife ancho con tapa 7 costillas (sin hueso) |
| 5.6 | Bife ancho sin tapa 4 costillas (sin hueso) |
| 5.7 | Bife ancho sin tapa 5 costillas (sin hueso) |
| 5.8 | Bife ancho sin tapa 6 costillas (sin hueso) |
| 5.9 | Bife ancho sin tapa 7 costillas (sin hueso) |
| 5.10 | Brazuelo |
| 5.11 | Brazuelo al rojo |
| 5.12 | Carnaza de paleta |
| 5.13 | Carnaza de paleta con marucha |
| 5.14 | Centro de asado |
| 5.15 | Centro de carnaza de paleta |
| 5.16 | Chingolo |
| 5.17 | Chingolo al rojo |
| 5.18 | Cogote |
| 5.19 | Cogote, aguja y paleta |
| 5.20 | Corte pony: aguja, carnaza, de paleta y parte asado (sin hueso) |
| 5.21 | Cuarto delantero a 3 costillas (sin hueso) |
| 5.22 | Cuarto delantero en manta |
| 5.23 | Cuarto delantero sin asado (sin hueso) |
| 5.24 | Falda |
| 5.25 | Falda de exportación |
| 5.26 | Falda sin tapa |
| 5.27 | Marucha |
| 5.28 | Marucha al rojo |
| 5.29 | Matambre |
| 5.30 | Pecho a 10 costillas (sin hueso) |
| 5.31 | Pecho a 10 costillas sin tapa (sin hueso) |
| 5.32 | Pecho a 10 costillas sin tapa al rojo (sin hueso) |
| 5.33 | Pecho a 3 costillas sin hueso o en manta (sin hueso) |
| 5.34 | Pecho a 6 costillas (sin hueso) |
| 5.35 | Pecho a 6 costillas sin tapa (sin hueso) |
| 5.36 | Pecho de exportación (sin hueso) |
| 5.37 | Pecho sin tapa (sin hueso) |
| 5.38 | Tapa de aguja - asado de carnicero |
| 5.39 | Tapa de asado |
| 5.40 | Tapa de bife ancho |
| 5.41 | Tapa de falda |
| 5.42 | Tapa de paleta |
| 5.43 | Tapa de pecho |
| 6.1 | Asado con vacío (sin hueso) |
| 6.2 | Bananita |
| 6.3 | Bife angosto 1 costilla con cordón (sin hueso) |
| 6.4 | Bife angosto 1 costilla sin cordón (sin hueso) |
| 6.5 | Bife angosto 3-4 costillas al rojo (sin hueso) |
| 6.6 | Bife angosto 3-4 costillas con cordón (sin hueso) |
| 6.7 | Bife angosto 3-4 costillas sin cordón (sin hueso) |
| 6.8 | Bife de bola de lomo |
| 6.9 | Bife de vacío |
| 6.10 | Bifes angostos y anchos (sin hueso) |
| 6.11 | Bola de lomo |
| 6.12 | Bola de lomo sin tapa |
| 6.13 | Carnaza de cola o cuadrada |
| 6.14 | Carnaza de cola o cuadrada al rojo |
| 6.15 | Centro de corazón de cuadril |
| 6.16 | Centro de entraña |
| 6.17 | Centro de nalga de adentro |
| 6.18 | Colita de cuadril |
| 6.19 | Corazón de cuadril |
| 6.20 | Corcho de cuadril (picaña) |
| 6.21 | Cuadril |
| 6.22 | Cuadril con colita de cuadril |
| 6.23 | Cuadril con tapa y con colita |
| 6.24 | Cuadril sin tapa |
| 6.25 | Cuarto trasero en manta |
| 6.26 | Entraña fina |
| 6.27 | Entraña fina sin membrana |
| 6.28 | Garrón |
| 6.29 | Garrón al rojo |
| 6.30 | Lomo |
| 6.31 | Lomo de cuadril |
| 6.32 | Lomo sin cordón |
| 6.33 | Lomo sin membrana |
| 6.34 | Medallón de bola de lomo |
| 6.35 | Media luna de vacío al rojo |
| 6.36 | Medialuna de vacío (falda) |
| 6.37 | Nalga de adentro (sin hueso) |
| 6.38 | Nalga de adentro sin tapa (sin hueso) |
| 6.39 | Nalga de afuera (sin hueso) |
| 6.40 | Nalga de afuera, nalga de adentro y tortuguita (sin hueso) |
| 6.41 | Peceto |
| 6.42 | Peceto al rojo |
| 6.43 | Pierna (sin hueso) |
| 6.44 | Pierna mocha (sin hueso) |
| 6.45 | Rueda (sin hueso) |
| 6.46 | Rueda sin garrón (sin hueso) |
| 6.47 | Tapa de bola de lomo |
| 6.48 | Tapa de cuadril (picaña) |
| 6.49 | Tapa de nalga |
| 6.50 | Tortuguita |
| 6.51 | Tortuguita sin bananita |
| 6.52 | Vacío |
| 6.53 | Vacío sin bife |
| 7.1 | Aorta |
| 7.2 | Carnes chicas |
| 7.3 | Carnes chicas-carne de cabeza-labio |
| 7.4 | Carnes chicas-carne de tragapasto |
| 7.5 | Carnes chicas-carne de traquea |
| 7.6 | Carnes chicas-nuez de quijada |
| 7.7 | Corazón |
| 7.8 | Entraña gruesa |
| 7.9 | Hígado |
| 7.10 | Lengua c/s epitelio |
| 7.11 | Membrana del diafragama |
| 7.12 | Molleja de cogote |
| 7.13 | Molleja de corazón |
| 7.14 | Nuez de quijada |
| 7.15 | Pulmones |
| 7.16 | Rabo |
| 7.17 | Riñón |
| 7.18 | Sesos |
| 7.19 | Tendones |
| 8.1 | Bazo |
| 8.2 | Bonete / redecilla |
| 8.3 | Chinchulines |
| 8.4 | Cuajo |
| 8.5 | Librillo |
| 8.6 | Mondongo |
| 8.7 | Tripa gorda |
| 8.8 | Tripa orilla primera |
| 8.9 | Tripa orilla segunda |
| 8.10 | Tripa salame |
| 8.11 | Tripón |
| 8.12 | Vejiga |
| 9.1 | Bolsa de hiel (grasa) |
| 9.2 | Canal pelviano (grasa) |
| 9.3 | Capadura (grasa) |
| 9.4 | Cola sin pelo (grasa) |
| 9.5 | Descarne de cueros (grasa) |
| 9.6 | Desperdicios de cabezas (grasa) |
| 9.7 | Desperdicios de pulmón (grasa) |
| 9.8 | Desperdicios de suprarrenales (grasa) |
| 9.9 | Desperdicios de tripa (grasa) |
| 9.10 | Gañote, pulmón, tráquea (grasa) |
| 9.11 | Grasa de cabeza |
| 9.12 | Grasa de centro de entraña |
| 9.13 | Grasa de tapa |
| 9.14 | Grasa de hígado |
| 9.15 | Grasa de molleja cogote |
| 9.16 | Grasa de molleja corazón |
| 9.17 | Grasa de páncreas |
| 9.18 | Grasa de pulmón |
| 9.19 | Grasa de roseta |
| 9.20 | Grasa de suprarrenales |
| 9.21 | Grasa de tripa salame |
| 9.22 | Grasa de corazón |
| 9.23 | Grasa riñonada |
| 9.24 | Grasa de cogote |
| 9.25 | Oreja sin pelo (grasa) |
| 9.26 | Pellejo de medula (grasa) |
| 9.27 | Pellejo de tragapasto (grasa) |
| 9.28 | Pichico (grasa) |
| 9.29 | Recortes de cuero (grasa) |
| 9.30 | Recortes de librillo (grasa) |
| 9.31 | Recortes de mondongo (grasa) |
| 9.32 | Tela vacuna (grasa) |
| 9.33 | Tripa ciega (grasa) |
| 9.34 | Trompa (grasa) |
| 10.1 | Astas |
| 10.2 | Huesos de cabeza |
| 10.3 | Huesos de manos |
| 10.4 | Huesos de maxilar |
| 10.5 | Huesos de patas |
| 10.6 | Machos de astas |
| 10.7 | Pezuñas |
| 11.1 | Epitelio |
| 11.2 | Hiel |
| 11.3 | Hipófisis |
| 11.4 | Hipotálamo |
| 11.5 | Páncreas |
| 11.6 | Paratiroides |
| 11.7 | Pineal |
| 11.8 | Próstata |
| 11.9 | Sangre nonato |
| 11.10 | Sarro |
| 11.11 | Suprarrenales |
| 11.12 | Tiroides |
| 12.1 | Caldo de carne |
| 12.2 | Caldo de hueso y/o concentrados |
| 12.3 | Caldo de pata |
| 12.4 | Carne cocida y congelada en tubos |
| 12.5 | Chorizos - embutidos cocidos (salchichón) |
| 12.6 | Chorizos - embutidos frescos (chorizo) |
| 12.7 | Chorizos - embutidos secos (salame) |
| 12.8 | Cueros |
| 12.9 | Enlatado - pate de foie y de hígado |
| 12.10 | Enlatados - picadillo cárnico |
| 12.11 | Enlatados (corned beef) |
| 12.12 | Estiércol |
| 12.13 | Extracto |
| 12.14 | Gelatina |
| 12.15 | Hamburguesas |
| 12.16 | Mondongo semicocido y congelado |
| 12.17 | Sangre |
| 13.1 | Angueta |
| 13.2 | Bondiola sin hueso |
| 13.3 | Carne Chica Porcina |
| 13.4 | Corazón |
| 13.5 | Corteza |
| 13.6 | Costillar con hueso y lomo |
| 13.7 | Costillar con hueso, lomo y bondiola |
| 13.8 | Costillar sin hueso |
| 13.9 | Cuadril |
| 13.10 | Estómago |
| 13.11 | Hígado |
| 13.12 | Jamón con hueso, corte corto |
| 13.13 | Jamón con hueso, corte largo |
| 13.14 | Jamón con hueso, corte parma |
| 13.15 | Jamón sin hueso desgrasado |
| 13.16 | Lengua |
| 13.17 | Lomo |
| 13.18 | Media Res Porcina |
| 13.19 | Nalga |
| 13.20 | Otros Cortes frescos |
| 13.21 | Paleta con hueso con cuero |
| 13.22 | Paleta sin hueso, sin cuero |
| 13.23 | Panceta con hueso, con cuero |
| 13.24 | Panceta sin hueso con y sin cuero |
| 13.25 | Pata |
| 13.26 | Peceto |
| 13.27 | Pechito con hueso |
| 13.28 | Productos preparados |
| 13.29 | Rabo |
| 13.30 | Res Porcina |
| 13.31 | Riñón |
| 13.32 | Tocino con y sin hueso |
| 13.33 | Tortuga |


## Novedades

Se recuerda que esta disponible el 
[grupo de noticias](http://groups.google.com.ar/group/pyafipws) donde
se publicarán futuras novedades sobre PyAfipWS: servicios web de
factura electrónica y sus interfases (se recomienda suscribirse)

## Historial de cambios

### Diciembre 2018 v 2.0

- nuevo campo tipo_movimiento (prod) en !CrearRemito, "ENV": Envio Normal "PLA": Retiro en planta "REP": Reparto "RED": Redestino
- caracter_receptor -> categoria_receptor (beta/prod) en !CrearRemito
- datosAutorizacion -> datosEmision (beta/prod) en !AgregarDatosAutorizacion
- codRemRedestinar -> codRemRedestinado (beta/prod)
- ajustes mercaderias (beta/prod), cambiando kilos -> cantidad (beta/prod)
- id_cliente -> id_req (beta/prod) en !GenerarRemito y !ConsultarRemito


Algunos son cambios internos, para evitar modificaciones (datosAutorizacion,codRemRedestinado)

#### Cambios externos

Impacto la interfaz con otros sistemas (en negrita):

- **`CrearRemito`**: (tipo_comprobante, punto_emision, **tipo_movimiento**, categoria_emisor, cuit_titular_mercaderia, cod_dom_origen, tipo_receptor, categoria_receptor, cuit_receptor, cuit_depositario, cod_dom_destino, cod_rem_redestinar, cod_remito, estado)
- **`AgregarMercaderia`**: (orden, cod_tipo_prod, cantidad, **unidades**, tropa)
- **`GenerarRemito`**: (**id_req**, archivo="qr.png")
- **`ConsultarRemito`**: (cod_remito, **id_req**, tipo_comprobante, punto_emision, nro_comprobante)

### Abril 2022 v3.5

- Se agrega método para consulta de Receptores Válidos (ConsultarReceptoresValidos)




## Costos y Condiciones

Ver [Condiciones del Soporte Comercial](../documentacion_herramientas/pyafipws.md#costos-y-condiciones).

A su vez, se libera el código fuente bajo licencia GPL (software libre), al igual que se hizo con el restos de los servicios web. Para más detalles ver página FacturaElectronica.