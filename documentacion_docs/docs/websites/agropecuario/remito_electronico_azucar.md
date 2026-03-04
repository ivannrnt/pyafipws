# Remito Electrónico Azúcar y Derivados - RG 4519/19

Interfaz para Servicio Web de AFIP para la emisión de Remito de Azúcar y derivados, Resolución General 4519/19


## Descripción General

La Resolución General N° 4519/2019 establece para el Sector Azucarero el uso obligatorio de los Remitos Electrónicos como únicos documentos válidos para las remisiones de los productos obtenidos de la industrialización de la caña de azúcar (azúcar, alcohol, bagazo y melaza) efectuadas por los ingenios azucareros.

Sujetos obligados:

- Emisor del remito: ingenio azucarero titular o depositario de la mercadería a trasladar.
- Autorizante del remito: titular de la mercadería a trasladar cuando la misma se encuentre en depósito de terceros.
- Destinatario del remito: receptor de la mercadería.

El Código de Remito Electrónico (CRE) será por cada comprobante solicitado y autorizado y deberá figurar impreso en el documento para que sea válido.

Próxima a entrar en vigencia (Septiembre 2019): Las disposiciones establecidas en esta resolución general conjunta tendrán vigencia desde su publicación en el Boletín Oficial y resultarán de aplicación a partir del 1 de septiembre de 2019.


## Descargas

- Instalador: [PyAfipWs-2.7.2433-32bit+wsaa_2.12c+wsremazucar_1.04a-homo.exe](https://www.sistemasagiles.com.ar/soft/pyafipws/PyAfipWs-2.7.2433-32bit+wsaa_2.12c+wsremazucar_1.04a-homo.exe)
- Documentación:[Documento Oficial WSRemAzucar v2.0.3](https://www.afip.gob.ar/ws/remitoElecAzucar/Manual-Desarrollador-WSREMAZUCAR-2.0.3.pdf) (AFIP) [Manual de Uso General](../documentacion_herramientas/manualpyafipws.md) ([PDF](http://www.sistemasagiles.com.ar/trac/wiki/ManualPyAfipWs?format=pdf))
- Archivos de intercambio (muestras): 
- Generación (texto plano JSON): [attachment:wsremazucar.json]
- Código Fuente (Python): [wsremazucar.py](https://github.com/reingart/pyafipws/blob/develop/wsremazucar.py)

## Métodos


- **`Conectar(cache=None, url="", proxy="")`**: en homologación no hace falta pasarle ningún parámetro. En producción, el segundo parámetro es la WSDL.
- **`Dummy()`**: devuelve estado de servidores

Métodos para generar un Remito Electrónico Azúcar (REC):

- **`CrearRemito(tipo_comprobante, punto_emision, tipo_titular_mercaderia, cuit_titular_mercaderia, cuit_autorizado_retirar, cuit_productor_contrato, numero_maquila, cod_remito, estado, es_entrega_mostrador)`**: crea un remito interno a autorizar
- **`AgregarReceptor(cuit_pais_receptor, cuit_receptor, cod_dom_receptor,cuit_despachante, codigo_aduana, denominacion_receptor, domicilio_receptor)`**:
- **`AgregarViaje(fecha_inicio_viaje, distancia_km, cod_pais_transportista)`**: agrega los datos del viaje
- **`AgregarVehiculo(dominio_vehiculo, dominio_acoplado, cuit_transportista, cuit_conductor, apellido_conductor, cedula_conductor, denom_transportista, id_impositivo, nombre_conductor)`**: agrega los datos del vehiculo al viaje
- **`AgregarMercaderia(orden, cod_tipo_prod, cod_tipo_emb, cantidad_emb, cod_tipo_unidad, cant_unidad, anio_safra)`**: agrega el detalle de cada item de la mercadería (pueden ser varios items)

Métodos principales específicos para Remito Electrónico Azúcar (REC):

- **`GenerarRemito(id_req, archivo="qr.png")`**: Informar los datos necesarios para la generación de un remito nuevo
- **`AnularRemito()`**: Llamar previamente a CrearRemito con todos los datos del Remito y luego llamar a AnularRemito.


## Tablas de Parámetros

### Tipos de Comprobante

| **Código** | **Descripción** |
|---|---|
| 998 | Remito Electrónico para Azúcar, Alcohol y Subproductos -Exportación- |
| 997 | Remito Electrónico para Azúcar, Alcohol y Subproductos -Mercado Interno- |

### Tipos de Paises

| **Código** | **CUIT pais receptor/destino** | **Nombre** | **Tipo Sujeto** |

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
| 10 | Alcohol etílico de primera calidad "Buen gusto" |
| 11 | Alcohol etílico de primera calidad "Mal gusto" |
| 12 | Alcohol etílico desnaturalizado |
| 2 | Azúcar Crudo |
| 3 | Azúcar común tipo A |
| 4 | Azúcar común tipo B |
| 8 | Azúcar liquida |
| 6 | Azúcar otras |
| 5 | Azúcar refinada |
| 7 | Bagazo |
| 1 | Caña de Azúcar |
| 9 | Melaza |


### Tipos de Embalaje

| **Código** | **Descripción** |
|---|---|
| 6 | A Granel |
| 1 | Bolsón de 1000 kg |
| 4 | Bolsón de 25 kg |
| 3 | Bolsón de 50 kg |
| 2 | Bolsón de 60 kg |
| 5 | Fardo de 10 kg |
| 7 | Otros |


### Tipos Unidades de Venta

| **Código** | **Descripción** |
|---|---|
| 1 | Kg |
| 2 | Lt |

## Novedades

Se recuerda que esta disponible el 
[grupo de noticias](http://groups.google.com.ar/group/pyafipws) donde
se publicarán futuras novedades sobre PyAfipWS: servicios web de
factura electrónica y sus interfases (se recomienda suscribirse)

## Costos y Condiciones

Ver [Condiciones del Soporte Comercial](../documentacion_herramientas/pyafipws.md#costos-y-condiciones).

A su vez, se libera el código fuente bajo licencia GPL (software libre), al igual que se hizo con el restos de los servicios web. Para más detalles ver página FacturaElectronica.