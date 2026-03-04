# Remito Electrónico Harinero - RG 4519/19


Interfaz para Servicio Web de AFIP para la emisión de Remito de harinas de trigo y los subproductos derivados de la molienda de trigo , Resolución General Conjunta 4514/2019


## Descripción General

La Resolución General N° 4519/2019 establece para el Sector Harinero el uso obligatorio de los Remitos Electrónicos como únicos documentos válidos para las remisiones de los productos obtenidos de la industrialización respecto del traslado de productos y/o derivados de la molienda de trigo.

Sujetos obligados:

- Establecimientos de molienda de trigo.
- Usuarios de molienda de trigo.

El Código de Remito Electrónico (CRE) será por cada comprobante solicitado y autorizado y deberá figurar impreso en el documento para que sea válido.

Fecha de publicación: 04/07/2019

### Operatoria

Según [Noticias AFIP - Remito Electrónico Harinero REH ](http://www.afip.gob.ar/noticias/20190704-Remito-Electronico-Harinero-REH.asp):

> *Es un documento obligatorio para el traslado de harinas de trigo y subproductos derivados de la molienda de trigo.*

> *El REH será solicitado con carácter previo al inicio del traslado. Los sujetos alcanzados deberán ingresar con clave fiscal al servicio REMITOS ELECTRÓNICOS opción REMITO ELECTRÓNICO HARINERO para solicitar el Código de Remito Electrónico. El REH se emitirá por duplicado, un ejemplar se entregará al destinatario/receptor y otro deberá ser suscripto por el destinatario/receptor y servirá como constancia documental de la entrega.*

> *El remitente de la mercadería generará el remito completando los datos solicitados del remitente, del titular de la mercadería -de corresponder-, del depositario -de corresponder-, del destinatario y del transportista, así como el detalle y la cantidad de la mercadería remitida según la tabla consignada en el Anexo I. Y el titular o el depositario de la mercadería, cuando no sea el emisor del remito, deberá ingresar al servicio REMITOS ELECTRÓNICOS opción REMITO ELECTRÓNICO HARINERO para prestar conformidad, validando la remisión de la mercadería.*

> *Luego el destinatario de la mercadería, al recibir la misma, deberá ingresar al servicio REMITOS ELECTRONICOS opción REMITO ELECTRÓNICO HARINERO, para la aceptación de la mercadería recibida o su rechazo parcial o total. Cuando el REH sea rechazado parcialmente o en su totalidad, el sistema habilitará el redestino de la mercadería rechazada.*

> *El emisor, por cuestiones comerciales, estará habilitado a realizar un redestino de la mercadería de un remito ya emitido y aún no recibido, para ello deberá registrar previamente una contingencia de “Evento que ocasiona anulación del Remito sin pérdida de mercadería” y generar un nuevo remito, según el Anexo I.*





### Novedades

Al 29/04/2022, AFIP publica una nueva versión del servicio (v2.6)

- Se incorpora método para la consulta de receptores válidos.

Al 15/05/2020, AFIP publica una nueva versión del servicio (v2.4)

- Se agrega el campo descripción, tanto en el alta, como en la consulta

de remito.

Al 12/12/2019, AFIP publica una nueva versión del servicio (v2.3)

- Presenta arreglos en método de recepción de mercadería
- Arreglo en descripción de recepción de mercadería

Al 01/10/2019, AFIP publica una nueva versión del servicio (v2.1)

- Modifican los circuitos por adecuaciones solicitadas por el sector,
- Se agregan los anexos con información para enviar en los métodos,
- Se agrega Importe COT




## Descargas

- Instalador: [PyAfipWs-2.7.2189-32bit+wsaa_2.11c+wsremharina_1.05b-homo.exe](https://www.sistemasagiles.com.ar/soft/pyafipws/PyAfipWs-2.7.2189-32bit+wsaa_2.11c+wsremharina_1.05b-homo.exe)
- Documentación:[Documento Oficial WSRemHarina v2.1](http://www.afip.gob.ar/ws/remitoHTSDMT/Manual-Desarrollador-WSREMHARINA-v-2-1.pdf) (AFIP) [Manual de Uso General](../documentacion_herramientas/manualpyafipws.md) ([PDF](http://www.sistemasagiles.com.ar/trac/wiki/ManualPyAfipWs?format=pdf))
- Ejemplos:
    - VB: [remito_electronico_harina.bas](https://drive.google.com/file/d/14IbphOpsCXZVlDxoPJUmgyzL8Uip5C_V/view?usp=sharing)
- Archivos de intercambio (muestras): 
- Generación (texto plano JSON): [attachment:wsremharina.json]
- Código Fuente (Python): [wsremharina.py](https://github.com/reingart/pyafipws/blob/develop/wsremharina.py)

## Métodos


- **`Conectar(cache=None, url="", proxy="")`**: en homologación no hace falta pasarle ningún parámetro. En producción, el segundo parámetro es la WSDL.
- **`Dummy()`**: devuelve estado de servidores

Métodos para generar un Remito Electrónico Harinero (REH):

Nuevo Metodos y modificaciones:

- **`CrearRemito(tipo_comprobante, punto_emision, tipo_movimiento, cuit_titular, es_entrega_mostrador, es_mercaderia_consignacion, importe_cot, tipo_emisor, ruca_est_emisor, cod_rem_redestinar, cod_remito, estado, observaciones)`**:
- **`AgregarReceptor(cuit_pais_receptor, cuit_receptor, tipo_dom_receptor, cod_dom_receptor, cuit_despachante, codigo_aduana, denominacion_receptor, domicilio_receptor)`**:
- **`AgregarDepositario(tipo_depositario, cuit_depositario, ruca_est_depositario, tipo_dom_origen, cod_dom_origen)`**:
- **`AgregarViaje(fecha_inicio_viaje, distancia_km)`**:
- **`AgregarVehiculo(dominio_vehiculo, dominio_acoplado)`**:
- **`AgregarTransportista(cod_pais_transportista, cuit_transportista, cuit_conductor, apellido_conductor, cedula_conductor, denom_transportista, id_impositivo, nombre_conductor)`**:

Métodos principales específicos para Remito Electrónico Harina (REH):

- **`GenerarRemito(id_req, archivo="qr.png")`**: Informar los datos necesarios para la generación de un remito nuevo

Métodos principales de consulta:

- **`ConsultarRemito(cod_remito, id_req, archivo="qr.jpg", tipo_comprobante, punto_emision, nro_comprobante, cuit_emisor)`**: si no se especifica cod_remito y/o id_req, pasar nulos y completar el resto de los parámetros
- **`ConsultarReceptoresValidos(cuit_receptor)`**: permite consultar receptores que están impedidos de recibir nuevos remitos (v3.5) **NUEVO!**

## Tablas de Parámetros

### Tipos de Comprobante

| **Código** | **Descripción** |
|---|---|
| 993 | Remito Electrónico Harinero Automotor |
| 994 | Remito Electrónico Harinero Ferroviario |

### Tipos de Paises

| **Código** | **CUIT pais receptor/destino** | **Nombre** | **Tipo Sujeto** |
|---|---|---|---|
| 200 | 50000002000 | ARGENTINA | Físico |
| 200 | 55000002002 | ARGENTINA | Jurídico |
| 200 | 51600002000 | ARGENTINA | Otro tipo de entidad |
| 202 | 50000000040 | BOLIVIA | Físico |
| 202 | 55000000042 | BOLIVIA | Jurídico |
| 202 | 51600000040 | BOLIVIA | Otro tipo de entidad |
| 203 | 50000000059 | BRASIL | Físico |
| 203 | 55000000050 | BRASIL | Jurídico |
| 203 | 51600000059 | BRASIL | Otro tipo de entidad |
| 208 | 50000000032 | CHILE | Físico |
| 208 | 55000000034 | CHILE | Jurídico |
| 208 | 51600000032 | CHILE | Otro tipo de entidad |
| 221 | 50000000024 | PARAGUAY | Físico |
| 221 | 55000000026 | PARAGUAY | Jurídico |
| 221 | 51600000024 | PARAGUAY | Otro tipo de entidad |
| 225 | 50000000016 | URUGUAY | Físico |
| 225 | 55000000018 | URUGUAY | Jurídico |
| 225 | 51600000016 | URUGUAY | Otro tipo de entidad |


### Tipos de Mercaderías

| **Código** | **Descripción** |
|---|---|
| 1 | Harina 0 |
| 2 | Harina 00 |
| 3 | Harinas 000 |
| 4 | Harinas 0000 |
| 5 | Otras Harinas (½ 0, Harinilla de 1ª, Harinilla de 2ª, Harina para Pastelería, Harina para Fideería) |
| 6 | Harinas Acondicionadas (Leudantes) |
| 7 | Premezclas (a base de Harina de Trigo) |
| 8 | Sémolas y Semolines (todas las granulometrías) |
| 9 | Harinas Integrales o de Graham. (gruesas, medianas o finas) |
| 10 | Afrechillo, Pellets de Afrechillo, Salvado, Gérmen, Semitón, Rebacillo y otros subproductos |



### Tipos de Embalaje

| **Código** | **Descripción** |
|---|---|
| 1 | A granel |
| 6 | Bidón |
| 4 | Big Bag |
| 3 | Bolsa <= 1kg |
| 2 | Bolsa > 1kg |
| 8 | Botella |
| 18 | Bultos |
| 11 | Caja |
| 10 | Cajón |
| 12 | Contenedor |
| 14 | Fardo |
| 5 | Frasco |
| 7 | Lata Cuñete |
| 15 | Pallets |
| 13 | Paquete |
| 17 | Pieza |
| 16 | Rollo |
| 9 | Tambor |



### Tipos Unidades de Venta

| **Código** | **Descripción** |
|---|---|
| 1 | Kilogramo |
| 1 | Kilogramo |
| 4 | Litro |
| 5 | Metro cúbico |
| 2 | Tonelada |
| 2 | Unidad |
| 3 | Unidad |



### Tipos Estado

| **Código** | **Descripción** |
|---|---|
| DEN | Denegado |
| ACP | Aceptado Parcialmente |
| EMI | Emitido |
| ACE | Aceptado |
| ANS | Anulado sin emisión |
| NFI | No finalizado |
| NAC | No Aceptado |
| BOR | Borrador |
| PEM | Pendiente de Emitir |
| PAD | Pendiente de Autorizar por Depositario |
| PAT | Pendiente de Autorizar por Titular |
| ANUR | Anulado por Redestino |
| VEN | Vencido |
| ANU | Anulado |

### Tipos Contingencia

| **Código** | **Descripción** |
|---|---|
| 9 | Evento que ocasiona anulación del Remito SIN Pérdida de Mercadería |
| 10 | Evento que produjo pérdida parcial de mercadería y que NO ocasiona anulación del Remito |
| 11 | Evento que produjo pérdida parcial de mercadería y que ocasiona anulación del Remito |
| 12 | Evento que produjo pérdida Total de mercadería y que ocasiona anulación del Remito |
| 13 | Demoras en traslado |
| 14 | Corrección de pérdida informada, mercadería recuperada |

## Novedades

Se recuerda que esta disponible el 
[grupo de noticias](http://groups.google.com.ar/group/pyafipws) donde
se publicarán futuras novedades sobre PyAfipWS: servicios web de
factura electrónica y sus interfases (se recomienda suscribirse)

## Costos y Condiciones

Ver [Condiciones del Soporte Comercial](../documentacion_herramientas/pyafipws.md#costos-y-condiciones).

A su vez, se libera el código fuente bajo licencia GPL (software libre), al igual que se hizo con el restos de los servicios web. Para más detalles ver página FacturaElectronica.