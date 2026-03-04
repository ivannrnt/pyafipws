= FE.py: herramienta ad-hoc para Factura Electrónica =
[[TracNav(noreorder|FacturaElectronica)]]


Herramienta para la solicitud de CAE, generación y envío de Factura Electrónica (AFIP -Argentina), configurable y parametrizable, utilizando la interfaz PyAfipWs (software libre, código abierto - open source):

- Universal: multiplataforma y compatible con bases de datos ODBC, sqlite, PostgreSQL o archivos de texto (independiente del lenguaje de programación y plataforma del sistema operativo)
- Unificada: contempla los servicios web de factura electrónica nacional (WSFE RG2177/06 y RG2485/08), mercado interno versión 1 (WSFEv1 RG2485/08 y RG2904/10), bienes de capital (WSBFE RG2557/2009) y exportación (WSFEX RG2758/2010)
- Integrada: incluye funcionalidad de autenticación, autorización (CAE), generación de PDF, envío de email/FTP y almacenamiento según RG1361

2010 - 2015 © Mariano Reingart – Versión 1.48b
[[Image(htdocs:logo-pyafipws.png, align=right)]]

## Índice
[[TOC(noheading,inline,depth=4)]]

## Características principales:

- Autenticación por certificados, firma digital y soporte para servicios web totalmente transparente (no requiere conocimientos de encriptación ni protocolos web)
- Lectura de una base de datos y/o archivo de texto de los campos necesarios para autorizar y emitir las facturas, según formato utilizado, con los datos correctos y completos de acuerdo a las especificaciones de los servicios web de AFIP (ver formato adjunto para más información)
- Solicitud de Autenticación (Servicio Web WSAA de la AFIP) para utilizar los servicios web de la AFIP con los distintos webservices
- Solicitud de Autorización (obtención de CAE), consulta de último número de comprobante emitido, último id, reproceso, recuperación de datos de facturas emitidas, actualización de tablas de parámetros:
    - Servicio Web WSFE de AFIP por factura individual A/B (factura electrónica "nacional" original) - RG2177/06 y RG2485/08
    - Servicio Web WSFEv1 de AFIP por factura individual A/B (factura electrónica mercado interno versión 1 sin detalle) - RG2485/08 y RG2904/10 art. 4 opción B -
    - Servicio Web WSBFE de AFIP (bono fiscal electrónico - bienes de capital) - RG2557/09
    - Servicio Web WSFEX de AFIP (factura electrónica de exportación) - RG2758/10
- Escritura de los resultado del proceso (Campos: CAE, Resultado, Motivo, Reproceso devueltos por el WSFE) en la base de datos y/o archivo de texto

### Opcionales:

- Generación de un Archivo PDF con la imagen de cada factura, según muestra adjunta.
- Envió por correo electrónico del Archivo PDF según muestra adjunta (pudiendo seleccionar las facturas a enviar y llevando registro de los envíos)
- Envío por FTP a servidores remotos
- Generación de los archivos de almacenamiento de duplicados electrónicos según RG1361

### Características generales:

- Sin intervención de un operador para realizar el proceso
- No requiere servidores intermedios ni abonos o costos por servicios mensuales o por solicitud
- Obtención de CAE practicamente de manera inmediata (dependiente de la congestión de Internet y disponibilidad de los servidores de AFIP)
- Adaptable a las aplicaciones ERP de la empresa contratante mediante base de datos Compatibles con ODBC (pyODBC)
- Archivo de configuración (.ini) con datos de servidores de AFIP, certificados y CUIT a utilizar.

## Modelo de Datos

A continuación se detallan los campos mínimos actualmente necesarios para la generación de factura electrónica y confección de PDF genérico.

Las longitudes son aproximadas según el tipo de datos. Minimamente se utilizará una tabla por cada sección de la factura, interrelacionadas entre sí.

Para mayor información ver la documentación de AFIP.

**Importante:** Los campos numéricos, se leerán por la base de datos siempre con el formato que maneje la misma (por ej., con punto decimal: '123.45'). Al recibirse por archivo de texto tendrán la longitud máxima especificada, y podrán indicarse siempre con punto (ej. '123.45' o '123.00' -completar con 0 a la derecha-) o sin el (ej. '12345' o '12300', similar al formato del aplicativo RECE, RG1361 de AFIP, con la cantidad de posiciones decimales especificadas -completar con 0-).

### Encabezado del comprobante:

- id (Tipo: Numerico, Longitud: 15): identificador secuencial de la factura (*clave primaria*)
- webservice (Tipo: Alfanumerico, Longitud: 5): "wsfe", "wsbfe", "wsfex"
- fecha_cbte (Tipo: Alfanumerico, Longitud: 8): ej. "20100308"
- tipo_cbte (Tipo: Numerico, Longitud: 2): ej. 1 para Facturas A (según tabla de parámetros de AFIP)
- punto_vta (Tipo: Numerico, Longitud: 4): ej. 0001
- cbte_nro (Tipo: Numerico, Longitud: 8): ej. 00000001
- tipo_expo (Tipo: Numerico, Longitud: 1): tipo de exportación (1: bienes, 2: servicios, 3: otros)
- permiso_existente (Tipo: Alfanumerico, Longitud: 1): permiso de exportaión: 'S' o 'N' o nulo
- dst_cmp (Tipo: Numerico, Longitud: 3): código de pais de destino de exportación según tabla de parámetros de AFIP (200: 'ARGENTINA', 203: 'BRASIL', 212: 'ESTADOS UNIDOS', etc.)
- nombre_cliente (Tipo: Alfanumerico, Longitud: 200)
- tipo_doc (Tipo: Numerico, Longitud: 2): código de tipo de documento según tabla AFIP (80: CUIT)
- nro_doc (Tipo: Numerico, Longitud: 11): número de documento (DNI, CUIT, etc.) -corresponde a cuit_pais_cliente en exportación-
- domicilio_cliente (Tipo: Alfanumerico, Longitud: 300)
- id_impositivo (Tipo: Alfanumerico, Longitud: 50): identificación impositiva en país destino (por ej. CNJP, RUC, VAT ID, etc.)
- imp_total (Tipo: Importe, Longitud: 15,3): importe total (con hasta 3 decimales)
- imp_tot_conc (Tipo: Importe, Longitud: 15,3): importe conceptos adicionales (con hasta 3 decimales)
- imp_neto (Tipo: Importe, Longitud: 15,3): importe neto sujeto a cálculo de IVA (con hasta 3 decimales)
- impto_liq (Tipo: Importe, Longitud: 15,3): importe de IVA liquidado (con hasta 3 decimales)
- impto_liq_rni (Tipo: Importe, Longitud: 15,3): importe de IVA liquidado a RNI (con hasta 3 decimales) -obsoleto-
- imp_op_ex (Tipo: Importe, Longitud: 15,3): importe de operaciones exentas de IVA (con hasta 3 decimales)
- impto_perc (Tipo: Importe, Longitud: 15,3): importe de percepciones (con hasta 3 decimales)
- imp_iibb (Tipo: Importe, Longitud: 15,3): importe de ingresos brutos (con hasta 3 decimales)
- impto_perc_mun (Tipo: Importe, Longitud: 15,3): importe de percepciones municipales (con hasta 3 decimales)
- imp_internos (Tipo: Importe, Longitud: 15,3): importe de impuestos internos (con hasta 3 decimales)
- imp_trib (Tipo: Importe, Logintud: 15,3): importe total de impuestos y tributos (no incluye IVA)
- moneda_id (Tipo: Alfanumerico, Longitud: 3): código de moneda según tabla de parámetros de AFIP ('PES': peso, 'DOL': dólares, etc.)
- moneda_ctz (Tipo: Importe, Longitud: 10,6): cotización de la moneda (con hasta 6 decimales)
- obs_comerciales (Tipo: Alfanumerico, Longitud: 1000): observaciones comerciales
- obs (Tipo: Alfanumerico, Longitud: 1000): observaciones generales
- forma_pago (Tipo: Alfanumerico, Longitud: 50): descripción de la forma de pago (ej. 'Efectivo')
- incoterms (Tipo: Alfanumerico, Longitud: 3): término de comercio exterior (ej. 'FOB')
- incoterms_ds (Tipo: Alfanumerico, Longitud: 20): descripción de termino de comercio exterior
- idioma_cbte (Tipo: Alfanumerico, Longitud: 1): idioma del comprobante según tabla de parámetros de AFIP (1: español, etc.)
- zona (Tipo: Alfanumerico, Longitud: 5): -no utilizado-
- fecha_venc_pago (Tipo: Alfanumerico, Longitud: 8): fecha de vencimiento del pago
- presta_serv (Tipo: Numerico, Longitud: 1): prestación de servicio ('S' o 'N')
- fecha_serv_desde (Tipo: Alfanumerico, Longitud: 8): fecha de inicio del servicio
- fecha_serv_hasta (Tipo: Alfanumerico, Longitud: 8): fecha de finalización del servicio
- cae (Tipo: Numerico, Longitud: 14): Código de Autorización Electrónico otorgado
- fecha_vto (Tipo: Alfanumerico, Longitud: 8): fecha de vencimiento del CAE
- resultado (Tipo: Alfanumerico, Longitud: 1): resultado 'A': aceptado, 'R': rechasado
- reproceso (Tipo: Alfanumerico, Longitud: 1): 'S' si hubo reprocesamiento, 'N' si es procesamiento original
- motivo (Tipo: Alfanumerico, Longitud: 40): código o descripción del motivo de rechazo u observación del comprobante, ej: 11 - numeración, 02: cuit no autorizada
- telefono_cliente (Tipo: Alfanumerico, Longitud: 50)
- localidad_cliente (Tipo: Alfanumerico, Longitud: 50)
- provincia_cliente (Tipo: Alfanumerico, Longitud: 50)
- email (Tipo: Alfanumerico, Longitud: 100): destinatario del PDF
- pdf (Tipo: Alfanumerico, Longitud: 100): ruta y nombre de archivo PDF a generar
- err_code (Tipo: Alfanumerico, Longitud: 6): código de error informado por AFIP (Ej. fexerror.!ErrCode='505')
- err_msg (Tipo: Alfanumerico, Longitud: 1000): mensaje de error informado por AFIP (Ej. fexerror.!ErrMsg='Error de Lockeo')
- formato_id (Tipo: Numérico): identificador de formato (para generación del PDF, solo en el esquema)
- Dato_adicional1 (Tipo: Alfanumerico, Comienzo: 4325 Longitud: 30)
- Dato_adicional2 (Tipo: Alfanumerico, Comienzo: 4355 Longitud: 30)
- Dato_adicional3 (Tipo: Alfanumerico, Comienzo: 4385 Longitud: 30)
- Dato_adicional4 (Tipo: Alfanumerico, Comienzo: 4415 Longitud: 100)
- Dato_adicional5 (Tipo: Alfanumerico, Comienzo: 4515 Longitud: 100)
- Dato_adicional6 (Tipo: Alfanumerico, Comienzo: 4615 Longitud: 100)
- Dato_adicional7 (Tipo: Alfanumerico, Comienzo: 4715 Longitud: 1000)

### Detalle de ítems (artículos)

- id (Tipo: Numerico, Longitud: 15): identificador secuencial de la factura (*clave foránea*)
- codigo (Tipo: Alfanumerico, Longitud: 30): código del artículo
- qty (Tipo: Importe, Longitud: 12,2): cantidad (con 2 decimales)
- umed (Tipo: Numerico, Longitud: 2): código de unidad de medida según tabla de parámetros AFIP (ej. 1 - kg)
- precio (Tipo: Importe, Longitud: 12,3): importe unitario (con hasta 3 decimales)
- imp_total (Tipo: Importe, Longitud: 14,3): importe subtotal (con hasta 3 decimales)
- iva_id (Tipo: Numerico, Longitud: 5): código de alícuota de IVA según tabla de parámetros AFIP (ej. 5 - IVA RI Tasa General 21 %)
- ds (Tipo: Alfanumerico, Longitud: 4000): descripción del artículo
- ncm (Tipo: Alfanumerico, Longitud: 15): código habilitado del Nomenclador Común de Mercosur
- sec (Tipo: Alfanumerico, Longitud: 15): código habilitado de la Secretaría de Comercio -reservado-
- bonif (Tipo: Importe, Longitud: 15,2): importe de descuento (con 2 decimales)
- imp_iva (Tipo: Importe, Comienzo: 4122 Longitud: 15): importe liquidado de IVA para este articulo
- dato_a (Tipo: Alfanumerico, Comienzo: 4137 Longitud: 15): primer dato adicional
- dato_b (Tipo: Alfanumerico, Comienzo: 4152 Longitud: 15): segundo dato adicional
- dato_c (Tipo: Alfanumerico, Comienzo: 4167 Longitud: 50): tercer dato adicional
- dato_d (Tipo: Alfanumerico, Comienzo: 4217 Longitud: 50): cuarto dato adicional
- dato_e (Tipo: Alfanumerico, Comienzo: 4267 Longitud: 100): quinto dato adicional

### Permiso de exportación

- id (Tipo: Numerico, Longitud: 15): identificador secuencial de la factura (*clave foránea*)
- id_permiso (Tipo: Alfanumerico, Longitud: 16): identificador del permiso de exportación, ej: '99999AAXX999999A'
- dst_merc (Tipo: Numerico, Longitud: 3): código de país de destino según tabla de AFIP

### Comprobante Asociado de exportación

- id (Tipo: Numerico, Longitud: 15): identificador secuencial de la factura (*clave foránea*)
- cbte_tipo (Tipo: Numerico, Longitud: 3): tipo de comprobante asociado
- cbte_punto_vta (Tipo: Numerico, Longitud: 4): punto de venta
- cbte_nro (Tipo: Numerico, Longitud: 8): número de comprobante

### Subtotales por Alícuotas de IVA

- id (Tipo: Numerico, Longitud: 15): identificador secuencial de la factura (*clave foránea*)
- iva_id (Tipo: Numerico, Comienzo: 2 Longitud: 5): tipo de alícuota (ver [tablas de parámetros de WSFEv1](wiki:wiki/ProyectoWSFEv1#AlicuotasdeIVA), por ej. 5 para 21%)
- base_imp (Tipo: Importe, Comienzo: 7 Longitud: (15, 3)): base imponible para esta alícuota
- importe (Tipo: Importe, Comienzo: 22 Longitud: (15, 3)): importe liquidado para esta alícuota

### Otros Tributos

- id (Tipo: Numerico, Longitud: 15): identificador secuencial de la factura (*clave foránea*)
- tributo_id (Tipo: Numerico, Comienzo: 2 Longitud: 5): tipo de tributo (ver [tablas de parámetros de WSFEv1](wiki:wiki/ProyectoWSFEv1#TiposdeTributo), por ej. 2 para impuestos provinciales)
- desc (Tipo: Alfanumerico, Comienzo: 7 Longitud: 100): descripción (por ej. 'IIBB prov. de Bs.As.')
- base_imp (Tipo: Importe, Comienzo: 107 Longitud: (15, 3)): base imponible para este impuesto:
- alic (Tipo: Importe, Comienzo: 122 Longitud: 15): alícuota (porcentaje, por ej. 3%)
- importe (Tipo: Importe, Comienzo: 137 Longitud: (15, 3)): importe liquidado para este impuesto

### Mensajes XML de requerimiento y Respuesta

Tabla opcional con los datos enviados y recibidos para registro y/o posterior depuración:

- id (Tipo: Numerico, Longitud: 15): identificador secuencial de la factura (*clave foránea*)
- xml_request (Tipo: Alfanumerico, Longitud: MEMO): requerimiento enviado a la AFIP
- xml_response (Tipo: Alfanumerico, Longitud: MEMO): respuesta recibida de la AFIP
- ts (Tipo: Fecha/hora): estampa del momento de la operación con AFIP

## Datos requeridos por cada Webservice y PDF

### Campos requeridos para Mercado Interno (WSFEv1)

Como primer paso, se debe crear un registro de encabezado con los siguientes datos obligatorios:

- id: identificador único de factura (numero interno, por ej un autoincremental)
- tipo_doc, nro_doc: Tipo (80 CUIT, 96 DNI, etc.) y número de Documento
- tipo_cbte: Tipo de comprobante (según tabla de parámetros)
- punto_vta: Nº de punto de venta (debe estar autorizado para WSFE)
- cbte_nro: Nº de comprobante
- fecha_cbte: Fecha del comprobante (no puede ser mayor o menor a 10 días)
- concepto: tipo de factura (1: productos, 2: servicios, etc.)
- imp_total: Importe total de la factura
- imp_tot_conc: Importe total de conceptos no gravados por el IVA
- imp_neto: Importe neto (gravado por el IVA) de la factura
- impto_liq(imp_iva): Importe del IVA liquidado
- imp_trib: Importe de otros tributos  (incluyendo percepciones de IVA, retenciones, IVA no inscripto, etc.)
- imp_op_ex: Importe de operaciones exentas
- moneda_id: Moneda de la factura (según tabla de parámetros)
- moneda_ctz: Cotización de la moneda de la factura (1.000 para pesos)
- fecha_vto_pago: Fecha de vencimiento de pago (si es de servicios)
- fecha_serv_desde, fecha_serv_hasta: fecha del servicios (si corresponde)

Luego, por cada alicuota de IVA, se debe crear un registro de iva con los siguientes parámetros:

- id: identificador único de factura (numero interno, clave foránea con encabezado)
- iva_id: código Alícuota de IVA (según tabla de parámetros, por ej 4 para 10.5%, 5 para 21%, 6 para 27%)
- base_imp: base imponible (suma de los precios netos gravados a esta tasa)
- importe: importe liquidado de iva

De existir otros tributos, se debe un registro en tributo con los siguientes parámetros:

- id: identificador único de factura (numero interno, clave foránea con encabezado)
- tributo_id: código tipo de impuesto (según tabla de parámetros, ej 1 para impuestos nacionales, 2 para provinciales, 3 para municipales, 4 para impuestos internos, 99 otros)
- desc (ds): descripción del tributo (por ej. "Impuesto Municipal Matanza", obligatorio para otros)
- base_imp: base imponible (suma de importes gravado por este impuesto)
- alic: alicuota (porcentaje de este impuesto)
- importe: importe liquidado de este impuesto

También se puede agregar registros a cbte_asoc para detallar los comprobantes asociados a una nota de crédito, con los siguientes parámetros:

- id: identificador único de factura (numero interno, clave foránea con encabezado)
- cbte_tipo: Código de tipo de comprobante (1: factura A, 6: factura B, etc.)
- cbte_pto_vta: Punto de venta
- cbte_nro: Numero de comprobante

### Campos requeridos para Exportación (WSFEX)

Como primer paso, se debe crear un registro de encabezado con los siguientes datos obligatorios:

- id: identificador único de factura (numero interno, por ej un autoincremental, cambiar en caso de rechazos)
- tipo_cbte: código de comprobante (19: 'Facturas de Exportación', 20: 'Nota de Débito por Operaciones con el Exterior', 21: 'Nota de Crédito por Operaciones con el Exterior'}
- punto_vta: Nº de punto de venta (debe estar autorizado para WSFEX)
- cbte_nro: Nº de comprobante
- fecha_cbte: Fecha del comprobante (no puede ser mayor o menor a 10 días)
- imp_total: Importe total de la factura
- tipo_expo: Tipo de exportacion (1: 'Exportación definitiva de Bienes', 2: 'Servicios', 4: 'Otros')
- permiso_existente: Indica si se posee documento aduanero de exportación (permiso de embarque). Posibles Valores: 'S', 'N', '' (vacío)
- dst_cmp: País de destino del comprobante (200: 'ARGENTINA', 203: 'BRASIL', 212: 'ESTADOS UNIDOS', etc.)
- nombre_cliente: Apellido y Nombre ó Razón Social del comprador
- nro_doc (cuit_pais_cliente): CUIT del país destino/Contribuyente (Ej: 50000000059: 'BRASIL - Persona Física', 51600000059: 'BRASIL - Otro tipo de Entidad', etc.)
- domicilio_cliente: Domicilio comercial cliente.
- id_impositivo: Clave de identificación tributaria del comprador (RUT, RUC, CNJP). 
- moneda_id: Moneda de la factura ('DOL': 'Dólar Estadounidense', 'PES': 'Pesos Argentinos', '012': 'Real', etc.)
- moneda_ctz: Cotización de la moneda de la factura (1.000 para pesos)
- obs_comerciales: observaciones comerciales (texto arbitrario)
- obs: observaciones (texto arbitrario)
- forma_pago: texto arbitrario (ej '30 días')
- incoterms: clausula de venta, terminos de comercio exterior ('DAF', 'DDP', 'CIF', 'FCA', 'FAS', 'DES', 'CPT', 'EXW', 'CIP', 'DDU', 'FOB', 'DEQ', 'CFR')
- idioma_cbte: idioma del comprobante {1: 'Español', 2: 'Inglés', 3: 'Portugués'}

Luego, por cada artículo vendido (ítem), se debe agregar un registro en detalle con los siguientes parámetros:

- id: identificador único de factura (numero interno, clave foránea con encabezado)
- codigo: código del producto
- ds: Descripción completa
- precio: Precio Unitario
- qty: Cantidad
- umed: Unidad de medida (según tabla de parámetros, ej 7 para unidades)
- imp_total: Importe total del artículo

Adicionalmente se puede agregar registros de permiso de exportación para detallar los permisos de embarque y destinaciones de la mercadería, con los siguientes parámetros:

- id: identificador único de factura (numero interno, clave foránea con encabezado)
- id_permiso: Código de despacho – Permiso de Embarque, formato 99999AAXX999999A (donde XX podrán ser números o letras)
- dst_merc: País de destino de la mercadería

También se puede agregar registros a cbte_asoc para detallar los comprobantes asociados a una nota de crédito, con los siguientes parámetros:

- id: identificador único de factura (numero interno, clave foránea con encabezado)
- cbte_tipo: Código de tipo de comprobante.
- cbte_punto_venta: Punto de venta
- cbte_numero: Numero de comprobante

### Campos requeridos para Generación de Factura (PDF)

Más allá de los datos obligatorios para autorizar facturas con cada webservice, para generar correctamente el PDF se necesita completar la mayor cantidad de campos dependiendo del formato de factura:

- Encabezado: fecha_cbte, tipo_cbte, punto_vta, cbte_nro, dst_cmp (si se usa campo pais), nombre_cliente, tipo_doc, nro_doce, domicilio_cliente, telefono_cliente, localidad_cliente, provincia_cliente, email, id_impositivo (RUC, RUT, CNJP o condición de IVA: Responsable Inscript, Monotributo, etc.),imp_total, imp_tot_conc (opcional), imp_neto, impto_liq (opcional si no se discriminan tasas), impto_liq_rni (opcional, solo si se usa), imp_op_ex (opcional, solo si se usa), moneda_id, moneda_ctz, obs_comerciales, obs, forma_pago, incoterms (solo exportación), incoterms_ds (solo exportación), fecha_venc_pago, fecha_serv_desde, fecha_serv_hasta (si corresponde por servicios), cae, fecha_vto, motivo, 
- Detalle: todos los campos (codigo, ds, precio, umed, precio, qty, imp_total). Para Facturas B, el precio e importe total del artículo debe contener el IVA.
- IVA: todos los campos, de corresponder (salvo exportación)
- Tributos: todos los campos -incluyendo descripción- (salvo exportación)

Igualmente, todos los campos del encabezado estan disponibles para generar el PDF.

## Tablas de parámetros:

Los servicios web de AFIP utilizan tablas relacionadas, las que deben ser consultadas y posiblemente almacenadas en la base de datos.

En general, estas tablas poseen un código y una descripción, y pueden sufrir modificaciones realizadas por la AFIP, con altas y bajas lógicas, por lo que tienen una fecha de vigencia (desde, hasta) y se proveen métodos para consultarlas por el mismo servicio web.

Ver [anexo_tablas_referenciales.sql](attachment:anexo_tablas_referenciales.sql) para el esquema SQL y datos generales (devueltos por el webservice) a modo de ejemplo. 

### Tablas referenciales WSFE

Tablas documentadas estaticamentes en el sitio web de AFIP: http://www.afip.gov.ar/fe/documentos/TABLAS%20GENERALES%20V.0.1%20%2026012011.xls
### Tablas referenciales WSBFE

Tablas dinámicas de parámetros para los códigos de comprobante, moneda, alícuotas de iva, producto según NCM, zonas, unidades de medida.

Ver BonosFiscales para más información.

### Tablas referenciales WSFEX

Tablas dinámicas de parámetros para los códigos de comprobante, moneda, paises, tipos de exportación, idiomas, CUIT referenciales de paises, unidades de medida. 

Ver FacturaElectronicaExportacion para más información

### Tablas referenciales WSFEv1

Tablas dinámicas de parámetros para los códigos de comprobante, tipos de conceptos, moneda, paises, alicuotas de iva, tributos, opcionales. 

Ver [wiki:ProyectoWSFEv1] para más información

### Tablas accesorias:

Será necesario implementar tablas para determinadas llamadas a los webservices: dummy (estado de los servidores de AFIP), último número de comprobante emitido, último ID, validar permiso de exportación, obtener cotización de la moneda.

A su vez, la recuperación de un comprobante se realizará sobre tablas similares a las necesarias para su autorización.

### Esquema SQL mínimo para WSFE/WSBFE/WSFEX

Esquema básico de las tablas necesarias para factura electrónica:
```
#!sql
CREATE TABLE encabezado (
    id INTEGER  PRIMARY KEY,
    tipo_reg INTEGER ,
    webservice VARCHAR (5),
    fecha_cbte VARCHAR (8),
    tipo_cbte INTEGER ,
    punto_vta INTEGER ,
    cbte_nro INTEGER ,
    tipo_expo INTEGER ,
    permiso_existente VARCHAR (1),
    dst_cmp INTEGER ,
    nombre_cliente VARCHAR (200),
    tipo_doc INTEGER ,
    nro_doc INTEGER ,
    domicilio_cliente VARCHAR (300),
    id_impositivo VARCHAR (50),
    imp_total NUMERIC (15, 3),
    imp_tot_conc NUMERIC (15, 3),
    imp_neto NUMERIC (15, 3),
    impto_liq NUMERIC (15, 3),
    impto_liq_rni NUMERIC (15, 3),
    imp_op_ex NUMERIC (15, 3),
    impto_perc NUMERIC (15, 2),
    imp_iibb NUMERIC (15, 3),
    impto_perc_mun NUMERIC (15, 3),
    imp_internos NUMERIC (15, 3),
    imp_trib NUMERIC (15, 3),
    moneda_id VARCHAR (3),
    moneda_ctz NUMERIC (10, 6),
    obs_comerciales VARCHAR (1000),
    obs VARCHAR (1000),
    forma_pago VARCHAR (50),
    incoterms VARCHAR (3),
    incoterms_ds VARCHAR (20),
    idioma_cbte VARCHAR (1),
    zona VARCHAR (5),
    fecha_venc_pago VARCHAR (8),
    presta_serv INTEGER ,
    fecha_serv_desde VARCHAR (8),
    fecha_serv_hasta VARCHAR (8),
    cae INTEGER ,
    fecha_vto VARCHAR (8),
    resultado VARCHAR (1),
    reproceso VARCHAR (1),
    motivo VARCHAR (40),
    telefono_cliente VARCHAR (50),
    localidad_cliente VARCHAR (50),
    provincia_cliente VARCHAR (50),
    formato_id INTEGER ,
    email VARCHAR (100),
    pdf VARCHAR (100),
    err_code VARCHAR (6),
    err_msg VARCHAR (1000)
);
CREATE TABLE detalle (
    id INTEGER  FOREING KEY encabezado,
    tipo_reg INTEGER ,
    codigo VARCHAR (30),
    qty NUMERIC (12, 2),
    umed INTEGER ,
    precio NUMERIC (12, 3),
    imp_total NUMERIC (14, 3),
    iva_id INTEGER ,
    ds VARCHAR (4000),
    ncm VARCHAR (15),
    sec VARCHAR (15),
    bonif NUMERIC (15, 2)
);
CREATE TABLE permiso (
    id INTEGER  FOREING KEY encabezado,
    tipo_reg INTEGER ,
    id_permiso VARCHAR (16),
    dst_merc INTEGER 
);
CREATE TABLE cmp_asoc (
    id INTEGER  FOREING KEY encabezado,
    tipo_reg INTEGER ,
    cbte_tipo INTEGER ,
    cbte_punto_vta INTEGER ,
    cbte_nro INTEGER 
);
CREATE TABLE iva (
    id INTEGER  FOREING KEY encabezado,
    tipo_reg INTEGER ,
    iva_id INTEGER ,
    base_imp NUMERIC (15, 3),
    importe NUMERIC (15, 3)
);
CREATE TABLE tributo (
    id INTEGER  FOREING KEY encabezado,
    tipo_reg INTEGER ,
    tributo_id INTEGER ,
    desc VARCHAR (100),
    base_imp NUMERIC (15, 3),
    alic NUMERIC (15, 2),
    importe NUMERIC (15, 3)
);
CREATE TABLE xmls (
    id INTEGER  FOREING KEY encabezado,
    xml_response TEXT,
    xml_request TEXT,
    ts TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

Adicionalmente, es posible agregar campos a estas tablas que estarán disponibles al general el PDF.

## Formato del archivo de texto de intercambio

La herramienta puede utilizar archivos de texto de campos con longitud fija para importar o exportar datos.
A continuación se detallan los tipos de registros disponibles:

### Encabezado

- tipo_reg (Tipo: Numerico, Comienzo: 1 Longitud: 1): VALOR FIJO 0
- webservice (Tipo: Alfanumerico, Comienzo: 2 Longitud: 6)
- fecha_cbte (Tipo: Alfanumerico, Comienzo: 8 Longitud: 8)
- tipo_cbte (Tipo: Numerico, Comienzo: 16 Longitud: 2)
- punto_vta (Tipo: Numerico, Comienzo: 18 Longitud: 4)
- cbte_nro (Tipo: Numerico, Comienzo: 22 Longitud: 8)
- tipo_expo (Tipo: Numerico, Comienzo: 30 Longitud: 1)
- permiso_existente (Tipo: Alfanumerico, Comienzo: 31 Longitud: 1)
- dst_cmp (Tipo: Numerico, Comienzo: 32 Longitud: 3)
- nombre_cliente (Tipo: Alfanumerico, Comienzo: 35 Longitud: 200)
- tipo_doc (Tipo: Numerico, Comienzo: 235 Longitud: 2)
- nro_doc (Tipo: Numerico, Comienzo: 237 Longitud: 11)
- domicilio_cliente (Tipo: Alfanumerico, Comienzo: 248 Longitud: 300)
- id_impositivo (Tipo: Alfanumerico, Comienzo: 548 Longitud: 50)
- imp_total (Tipo: Importe, Comienzo: 598 Longitud: (15, 3))
- imp_tot_conc (Tipo: Importe, Comienzo: 613 Longitud: (15, 3))
- imp_neto (Tipo: Importe, Comienzo: 628 Longitud: (15, 3))
- impto_liq (Tipo: Importe, Comienzo: 643 Longitud: (15, 3))
- impto_liq_nri (Tipo: Importe, Comienzo: 658 Longitud: (15, 3))
- imp_op_ex (Tipo: Importe, Comienzo: 673 Longitud: (15, 3))
- impto_perc (Tipo: Importe, Comienzo: 688 Longitud: 15)
- imp_iibb (Tipo: Importe, Comienzo: 703 Longitud: (15, 3))
- impto_perc_mun (Tipo: Importe, Comienzo: 718 Longitud: (15, 3))
- imp_internos (Tipo: Importe, Comienzo: 733 Longitud: (15, 3))
- imp_trib (Tipo: Importe, Comienzo: 748 Longitud: (15, 3))
- moneda_id (Tipo: Alfanumerico, Comienzo: 763 Longitud: 3)
- moneda_ctz (Tipo: Importe, Comienzo: 766 Longitud: (10, 6))
- obs_comerciales (Tipo: Alfanumerico, Comienzo: 776 Longitud: 1000)
- obs (Tipo: Alfanumerico, Comienzo: 1776 Longitud: 1000)
- forma_pago (Tipo: Alfanumerico, Comienzo: 2776 Longitud: 50)
- incoterms (Tipo: Alfanumerico, Comienzo: 2826 Longitud: 3)
- incoterms_ds (Tipo: Alfanumerico, Comienzo: 2829 Longitud: 20)
- idioma_cbte (Tipo: Alfanumerico, Comienzo: 2849 Longitud: 1)
- zona (Tipo: Alfanumerico, Comienzo: 2850 Longitud: 5)
- fecha_venc_pago (Tipo: Alfanumerico, Comienzo: 2855 Longitud: 8)
- presta_serv (Tipo: Numerico, Comienzo: 2863 Longitud: 1)
- fecha_serv_desde (Tipo: Alfanumerico, Comienzo: 2864 Longitud: 8)
- fecha_serv_hasta (Tipo: Alfanumerico, Comienzo: 2872 Longitud: 8)
- cae (Tipo: Numerico, Comienzo: 2880 Longitud: 14)
- fecha_vto (Tipo: Alfanumerico, Comienzo: 2894 Longitud: 8)
- resultado (Tipo: Alfanumerico, Comienzo: 2902 Longitud: 1)
- reproceso (Tipo: Alfanumerico, Comienzo: 2903 Longitud: 1)
- motivo (Tipo: Alfanumerico, Comienzo: 2904 Longitud: 40)
- id (Tipo: Numerico, Comienzo: 2944 Longitud: 15)
- telefono_cliente (Tipo: Alfanumerico, Comienzo: 2959 Longitud: 50)
- localidad_cliente (Tipo: Alfanumerico, Comienzo: 3009 Longitud: 50)
- provincia_cliente (Tipo: Alfanumerico, Comienzo: 3059 Longitud: 50)
- formato_id (Tipo: Numerico, Comienzo: 3109 Longitud: 10)
- email (Tipo: Alfanumerico, Comienzo: 3119 Longitud: 100)
- pdf (Tipo: Alfanumerico, Comienzo: 3219 Longitud: 100)
- err_code (Tipo: Alfanumerico, Comienzo: 3319 Longitud: 6)
- err_msg (Tipo: Alfanumerico, Comienzo: 3325 Longitud: 1000)
- Dato_adicional1 (Tipo: Alfanumerico, Comienzo: 4325 Longitud: 30)
- Dato_adicional2 (Tipo: Alfanumerico, Comienzo: 4355 Longitud: 30)
- Dato_adicional3 (Tipo: Alfanumerico, Comienzo: 4385 Longitud: 30)
- Dato_adicional4 (Tipo: Alfanumerico, Comienzo: 4415 Longitud: 30)

### Detalle

- tipo_reg (Tipo: Numerico, Comienzo: 1 Longitud: 1): VALOR FIJO 1
- codigo (Tipo: Alfanumerico, Comienzo: 2 Longitud: 30)
- qty (Tipo: Importe, Comienzo: 32 Longitud: (12, 2))
- umed (Tipo: Numerico, Comienzo: 44 Longitud: 2)
- precio (Tipo: Importe, Comienzo: 46 Longitud: (12, 3))
- imp_total (Tipo: Importe, Comienzo: 58 Longitud: (14, 3))
- iva_id (Tipo: Numerico, Comienzo: 72 Longitud: 5)
- ds (Tipo: Alfanumerico, Comienzo: 77 Longitud: 4000)
- ncm (Tipo: Alfanumerico, Comienzo: 4077 Longitud: 15)
- sec (Tipo: Alfanumerico, Comienzo: 4092 Longitud: 15)
- bonif (Tipo: Importe, Comienzo: 4107 Longitud: 15)

### Permiso

- tipo_reg (Tipo: Numerico, Comienzo: 1 Longitud: 1): VALOR FIJO 2
- id_permiso (Tipo: Alfanumerico, Comienzo: 2 Longitud: 16)
- dst_merc (Tipo: Numerico, Comienzo: 18 Longitud: 3)

### Comprobante Asociado

- tipo_reg (Tipo: Numerico, Comienzo: 1 Longitud: 1): : VALOR FIJO 3
- cbte_tipo (Tipo: Numerico, Comienzo: 2 Longitud: 3)
- cbte_punto_vta (Tipo: Numerico, Comienzo: 5 Longitud: 4)
- cbte_nro (Tipo: Numerico, Comienzo: 9 Longitud: 8)

### Alicuotas de IVA

- tipo_reg (Tipo: Numerico, Comienzo: 1 Longitud: 1): VALOR FIJO 4
- iva_id (Tipo: Numerico, Comienzo: 2 Longitud: 5)
- base_imp (Tipo: Importe, Comienzo: 7 Longitud: (15, 3))
- importe (Tipo: Importe, Comienzo: 22 Longitud: (15, 3))

### Tributos

- tipo_reg (Tipo: Numerico, Comienzo: 1 Longitud: 1): VALOR FIJO 5
- tributo_id (Tipo: Numerico, Comienzo: 2 Longitud: 5)
- desc (Tipo: Alfanumerico, Comienzo: 7 Longitud: 100)
- base_imp (Tipo: Importe, Comienzo: 107 Longitud: (15, 3))
- alic (Tipo: Importe, Comienzo: 122 Longitud: 15)
- importe (Tipo: Importe, Comienzo: 137 Longitud: (15, 3))

## Diseño de la Factura en Formato de PDF

El diseño gráfico de la factura en PDF es totalmente parametrizable mediante un archivo CSV o tablas en la base de datos, donde se indican los campos y su posición dentro de la hoja.

Ver [Formato de ejemplo (CSV)](attachment:factura.csv) y muestras adjuntas en PDF:

- [Muestra Modelo de Factura Electrónica Exportación (ejemplo detallado)](attachment:FacturaE0002-00000098.pdf)
- [Muestra Modelo de Factura Electrónica Nacional (ejemplo simple)](attachment:FacturaA0002-00000136.pdf)

**Propiedades:** para facilitar el seguimiento y control, el programa establece las propiedades del PDF  a los siguientes valores:

- Título: Factura E 0002-00000098 (ejemplo)
- Autor: CUIT 20267565393 (ejemplo)
- Motivo: CAE 60283152133455 (ejemplo)
- Palabras clave: AFIP Factura Electrónica
- Creador: versión de la interfaz

### Tipos de elementos
Para el diseño del PDF es posible establecer los siguientes tipos de campo (elementos gráficos):

- Texto (T), con tipo de letra (fuente), tamaño, formato (italico, negrita, subrayado), tamaño y alineación
- Líneas (L) y Cuadros (B)
- Imágenes (I) en formato PNG o JPG 
- Código de Barras (CB) en formato Entrelazado 2 de 5 (requerido por la AFIP)

### Definición de elementos

Las columnas de la planilla (factura.csv) o estructura de la tabla formato para definir los elementos gráficos es:

- name (alfanumérico): nombre del campo
- type (alfanumérico): tipo del campo: T, L, I, B, CB
- x1 (numérico): coordenada horizontal izquierda (en mm)
- y1 (numérico): coordenada vertical superior (en mm)
- x2 (numérico): coordenada horizontal derecha (en mm)
- y2 (numérico): coordenada vertical inferior (en mm)
- font (alfanumérico): nombre de la tipografía (fuente)
- size (numérico): tamaño en puntos del texto
- bold (verdadero/falso): estilo negrita para el texto (1 o 0)
- italic (verdadero/falso): estilo cursiva (itálica) para el texto (1 o 0)
- underline (verdadero/falso): estilo subrayado para el texto (1 o 0)
- foreground (numérico): color RGB de dibujo
- backgroud (numérico): color RGB de relleno del fondo (si aplica al elemento)
- align (alfanumérico): alineación: I: izquierda, D: derecha, C: centrado
- text (alfanumérico): texto estático o fórmula
- priority (numérico): orden z en el que se dibujan los elementos (a menor prioridad se dibuja primero)
- formato_id (numérico): identificador de formato (para relacionar en la tabla encabezado) -no aplica a planilla csv-
- pk (numérico): clave primaria para identificar los elementos -no aplica a planilla csv-

**Estilos HTML**: Adicionalmente, los estilos negrita, itálica y subrayado pueden establecerse en tiempo de ejecución, encerrando todo el texto con el tag html correspondiente (en el orden indicado). Ej:

- ```<B>texto en negrita</B>```
- ```<I>texto en cursiva</I>```
- ```<U>texto subrayado</U>```
- ```<B><I><U>texto en negrita, cursiva y subrayado</U></I></B>```
 
### Datos predefinidos y personalizados (fórmulas)

**Campos Genéricos**: son completados con los datos del encabezado y de la configuración (rece.ini, sección [PDF]), según su nombre. Ej. el campo 'logo' se completa con el texto especificado en la configuración, el campo 'motivo' con el texto de la tabla encabezado para dicha columna, etc. 

Adicionalmente, ciertos campos especiales son completados con los datos de la factura (también según su nombre), que acontinuación se detallan

**Encabezado y Pie**:  estan disponibles:

- Numero: punto_vta y cbte_nro (en formato 0000-000000000)
- Fecha: fecha_cbte (en formato dd/mm/aaaa)
- Vencimiento: fecha_venc_pago (en formato dd/mm/aaaa)
- LETRA: según tipo_cbte (A, B, C o E) 
- TipoCBTE: tipo_cbte en leyenda  requeida por AFIP (formato "COD.00")
- Comprobante.L: descripción del tipo_cbte ("Factura", "Recibo", "Nota de Crédito", etc.)
- !ComprobanteEx.L: descripción del tipo_cbte "extendida" ("Factura de Exportación", "Nota de Crédito de Exportación", etc.), si el comprobante no es de exportación (tipos 19, 20 o 21), contiene la misma descripción que Comprobante.L
- Pagina: leyenda "Hoja *n* de *x*"
- Hoja: nº de hoja actual
- Hojas: nº de hojas totales
- Continua: leyenda "Continua en hoja *n*" (si corresponde)
- Periodo.Desde: fecha_serv_desde
- Periodo.Hasta: fecha_serv_hasta
- Cliente.Nombre: campo nombre_cliente
- Cliente.Domicilio: domicilio_cliente
- Cliente.Localidad: localidad_cliente
- Cliente.Provincia: provincia_cliente
- Cliente.Telefono: telefono_cliente
- Cliente.IVA: id_impositivo ("Responsable Inscripto", "monotributo" o CNJP, RUC, etc.)
- Cliente.CUIT: nro_doc (con formato CUIT)
- Cliente.!TipoDoc: descricpión según tipo_doc (80: CUIT, 86: CUIL, 96:DNI)
- Cliente.!PaisDestino: nombre del pais según tabla Paises AFIP y campo dst_cmp (código destino del comprobante), considerar caso de AAE (Áreas Aduaneras Especiales) y Zonas Francas.
- Cliente.Observaciones: obs_comerciales
- IMP_NETO: imp_neto (importe neto)
- IMPTO_LIQ: impto_liq (IVA liquidado)
- IMP_TOTAL: imp_total (importe total)
- IMPTO_PERC: impto_perc (percepciones)
- IMP_OP_EX: imp_op_ex (importe operaciones exentas)
- IMP_IIBB: imp_iibb (importe ingresos brutos)
- IMPTO_PERC_MUN: impto_perc_mun (importe percepciones municipales)
- IMP_INTERNOS: imp_internos (importe impuestos internos)
- NETO: imp_neto (importe neto, solo facturas A)
- IVA21: impto_liq (IVA liquidado, solo facturas A)
- IVA10.5: iva liquidado al 10.5%
- TOTAL: imp_total (importe total)
- CAE: cae
- CAE.Vencimiento: fecha_vto (vencimiento de CAE)
- !CodigoBarras: barras
- !CodigoBarrasLegible: barras
- motivos_ds: leyenda "Irregularidades observadas por AFIP (F136): código ..." (campo motivo de encabezado)
- cmps_asoc_ds: lista de comprobantes asociados (ej. "Factura E 0001-000000001, ...") 
- permisos_ds: lista de documentos aduaneros asociados (ej. "Codigo de Despacho 09052EC01006154G - Destino de la mercadería: BRASIL, ...")

**Detalle:** Los items se especifican según su posición (01 para el primero, 02 para el segundo) Por ej. Item.Cantidad01 es la primer cantidad. Los campos disponibles son:

- Item.Cantidad: qty
- Item.Codigo: codigo
- Item.UMed: descripción de la unidad de medida
- Item.Descripcion: ds
- Item.Precio: precio (en formato importe)
- Item.Importe: imp_total (en formato importe)

**Múltiples líneas (renglones)**: El campo *descripción* acepta múltiples líneas, ya sea explícitas indicadas por el caracter salto de línea ```'\n'```, o implícitas (automáticamente se divide abarcando las líneas que hagan falta). Si un artículo (item de detalle) se extiende en varias líneas, el *código* y *cantidad* es completado en la primera, y el *precio* e *importe* en la última línea que le corresponda.

**Observaciones:** en el campo descripción se agregan las *observaciones generales* (campo 'obs') y las *observaciones comerciales* (campo 'obs_comerciales'), divididas en múltiples líneas si fuera necesario, incluyendo el título de cada una y separadas por líneas en blanco.  Si los campos 'cmps_asoc_ds', 'permisos_ds' no están presentes en el formato, se agregan a la descripción (bajo el título "Comprobantes Asociados" y "Permisos de Embarque" respectivamente).

**Visibilidad:** Los campos referentes a la *moneda*, *cotización*, *iva*, *incoterms*, *período facturado (servicios)* se muestran o se ocultan automáticamente dependiendo de si se proporcionan dichos datos o no. El resto de los campos es siempre visible.

**Campos personalizados**: es posible usar el formato formula, ya que todos los campos especificados en la tabla encabezado se encuentran en la variable ```fact``` (diccionario). Ejemplo para el campo permiso_existente:

- Nombre del elemento:  ```=PermisoExistente```    (= para indicar formula)
- Texto del elemento: ```fact['permiso_existente']```

**Paginación**: la cantidad de renglones para la descripción del detalle está limitada por la configuración de LINEAS_MAX (por defecto 24 líneas, se recomienda dejar 2 líneas libres para mensaje de transporte/continuación y demás). Una vez completada la cantidad de líneas definidas en dicho parámetro, se abrirá automáticamente una nueva página, donde se completarán el resto de las descripciones, y así sucesivamente. Los campos 'pagina', 'hoja', 'hojas', 'continua' se establecen con los valores correspondientes a cada página, y el subtotal (transporte) se calcula y se completa en el mismo campo 'Total' (cambiando su leyenda)

### Esquema SQL para generación de PDF

Es posible reemplazar el archivo con el diseño de la factura en PDF (```factura.csv```) con una tabla en la base de datos , donde se especifican los elementos gráficos:
```
#!sql
CREATE TABLE formatos_pdf (
    pk INTEGER IDENTITY PRIMARY KEY, 
    formato_id INTEGER,
    name VARCHAR (50),
    type VARCHAR (2),
    x1 FLOAT,
    y1 FLOAT,
    x2 FLOAT,
    y2 FLOAT,
    font VARCHAR (50),
    size FLOAT,
    bold BIT,
    italic BIT,
    underline BIT,
    foreground INTEGER,
    backgroud INTEGER,
    align VARCHAR(1),
    text VARCHAR(250),
    priority INTEGER
);
```

Para utilizar el formato pdf descripto en esta tabla, especificar el formato_id en la tabla encabezado. 

## Mensaje de Correo Electrónico

La herramienta tiene incorporado la funcionalidad de mandar la factura electrónica por correo (ver parámetro --email)
El mensaje de correo es configurable su motivo, cuerpo y remitente. 
El destinatario es tomado del la base de datos.
Automáticamente se adjunta el archivo PDF (si corresponde)

Se debe configurar el servidor de correo saliente, y los datos de autorización de ser necesario.

Ver [Email de Muestra](attachment:email.eml) 

### Utilitario ad-hoc para envio de emails

Adicionalmente se provee una herramienta separada correo.py (correo.exe) para enviar correos electrónicos arbitrarios sin necesidad de conectarse a la base de datos o procesar una factura. 

Para el envío utiliza la configuración general.

Modo de Uso: indicar datos del correo y archivo a adjuntar (si corresponde). 
```
correo.exe  motivo destinatario mensaje [archivo]
```

Ejemplo:
```
correo.exe  prueba reingart@gmail.com "Su factura electrónica esta disponible"
```

## Transferencia de Archivos (FTP)

Puede configurarse la transferencia de archivos por FTP a un servidor remoto para la posterior descarga de la factura (no incluido en el programa básico por el momento).

## Régimen de Almacenamiento de Duplicados Digitales (RG1361)

El programa puede adaptarse para generar los archivos requeridos por el aplicativo SIRED (SIAP) de la Resolución General 1361/02 (no incluido en el programa básico por el momento), referente al almacenamiento digital de los comprobantes emitidos (Libro Ventas, Detalle y Cabeceras de Factura)

## Invocación del programa

El programa de autorización y/o generación de facturas electrónica se ejecutará a pedido en primer plano (sin entorno gráfico visual), para procesar las facturas pendientes en la base de datos y al finalizar, devolver el control al programa principal, informando como salida el resultado general de las operaciones.

El programa leerá las facturas de la base de datos y llamará a los servicios web de AFIP pidiendo autorización en orden secuencial, almacenando los resultados (de corresponder).

Si no se dispone de base de datos principal (o no es posible acceder vía ODBC), se contempla la posibilidad de utilizar una base de datos secundaria interna temporal (sqlite), y cargar las facturas desde un archivo de texto de entrada, para luego grabar el resultado en otro archivo de texto de salida.

Ante cualquier inconveniente (error de comunicación, datos no válidos, rechazo u error de los servidores de AFIP, etc.),  el programa finalizará notificando a la aplicación principal por los medios estándar. De corresponder, la aplicación deberá corregir los datos de las facturas almacenados en la base de datos (modificando los campos no válidos o renumerando los comprobantes) para que puedan ser procesados correctamente.

En ambos casos (éxito o fracaso de autorización), el programa finalizará y solo comenzará nuevamente al ser invocado con el proceso de autorización.

En caso de error grave (pérdida de conexión, falta de memoria, problema con la base de datos, falla grave del sistema operativo, etc.), el programa se cerrará y deberá ser invocado manualmente para su reinicio luego de la solución del problema que causo el error.

Es responsabilidad de la base de datos velar por la consistencia e integridad de los datos, en ningún caso el programa almacenará internamente de manera permanente ningún valor asociado a la operatoria de facturación electrónica. El programa utilizará transacciones de la base de datos para el procesamiento atómico y persistente de lecturas y escrituras de cada comprobante.

Para un correcto seguimiento y/o eventual depuración de errores, el programa contemplará una bitácora de texto (log) para el registro de sus operaciones y resultados (salida estándar), siendo responsabilidad del sistema operativo su correcto almacenamiento al disco. Adicionalmente se almacenarán en la base de datos el requerimiento y la respuesta XML de acuerdo a la normativa vigente.

## Configuración

Como primer parámetro se informa el archivo de configuración (por defecto ```rece.ini```) contiene los parámetros necesarios para ejecutar la interfaz:

```
[WSAA]
CERT=empresa.crt
PRIVATEKEY=empresa.key
#URL=https://wsaa.afip.gov.ar/ws/services/LoginCms

[WSFE]
CUIT=20267565393
ENTRADA=entrada.txt
SALIDA=salida.txt
#URL=https://servicios1.afip.gov.ar/wsfe/service.asmx

[WSFEv1]
CUIT=20267565393
ENTRADA=entrada.txt
SALIDA=salida.txt
#URL=https://servicios1.afip.gov.ar/wsfev1/service.asmx?WSDL

[WSBFE]
CUIT=20267565393
ENTRADA=entrada.txt
SALIDA=salida.txt
#URL=https://servicios1.afip.gov.ar/wsfe/service.asmx

[WSFEX]
CUIT=20267565393
ENTRADA=entrada.txt
SALIDA=salida.txt
#URL=https://servicios1.afip.gov.ar/wsfex/service.asmx

[FACTURA]
ARCHIVO=tipo,letra,numero
FORMATO=factura.csv
DIRECTORIO=.
LINEAS_MAX=24
COPIAS=1

[PDF]
LOGO=serpiente.png
EMPRESA=Empresa de Prueba
MEMBRETE1=Direccion de Prueba
MEMBRETE2=Capital Federal
CUIT=CUIT 20-26756539-3
IIBB=IIBB 20-26756539-3
IVA=IVA Responsable Inscripto
INICIO=Inicio de Actividad: 01/04/2006

[MAIL]
SERVIDOR=adan.nsis.com.ar
USUARIO=no.responder@nsis.com.ar
CLAVE=noreplyauto123
MOTIVO=Factura Electronica Nro. NUMERO
CUERPO=Se adjunta Factura en formato PDF
REMITENTE=Facturador PyAfipWs <pyafipws@nsis.com.ar>

[BASE_DATOS]
DRIVER=sqlite
DSN=pyafipws
SERVER=localhost
DATABASE=pyafipws.db
UID=pyafipws
PWD=pyafipws
# nombre de tablas:
encabezado=encabezado
detalle=detalle

[PROXY]
HOST=10.0.0.1
PORT=3129
USER=mariano
PASS=reingart
```

Convenciones:

- La secciones se indican entre corchetes. Por ej. ```[WSAA]``` es la configuración referente al web service de autenticación, ```[WSFE]``` para la sección del web service de factura electrónica nacional, etc.
- Las opciones se indican con el nombre del parámetro en mayúsculas, seguido por el signo igual, seguido por el valor elegido. Por ej:  ```CERT=reingart.crt```
- Las lineas comentadas (que comienzan con un caracter # -numeral-) no son tenídas en cuenta, adaptando los valores por defecto para dichas opciones.

### Sección [WSAA]

Configuración referente al web service de autenticación:

- CERT: ubicación del archivo que contiene el certificado
- PRIVATEKEY: ubicación de la clave privada correspondiente al certificado
- URL: dirección del servidor de AFIP. Por ej., para producción: https://wsaa.afip.gov.ar/ws/services/LoginCms

### Sección [WSFE]

Configuración referente al web service de factura nacional:

- CUIT: nº de cuit del emisor (sin guiones). Por ej.: 20267565393
- ENTRADA: nombre de archivo con datos para autorizar/generar (si corresponde). Por ej.: entrada.txt
- SALIDA: nombre de archivo para almacenar el resultado (si corresponde). Por ej: salida.txt
- URL: dirección del servidor de AFIP. Por ej., para producción: URL=https://servicios1.afip.gov.ar/wsfe/service.asmx

### Sección [WSFEX]

Configuración referente al web service de factura exportación:

- CUIT: nº de cuit del emisor (sin guiones). Por ej.: 20267565393
- ENTRADA: nombre de archivo con datos para autorizar/generar (si corresponde). Por ej.: entrada.txt
- SALIDA: nombre de archivo para almacenar el resultado (si corresponde). Por ej: salida.txt
- URL: dirección del servidor de AFIP. Por ej., para producción: URL=https://servicios1.afip.gov.ar/wsfex/service.asmx


### Sección [FACTURA]

Controla la generación del PDF (si no se especifica campo PDF en tabla encabezado):

- ARCHIVO: nombre de archivo PDF a generar, por ej. incluyendo tipo,letra,numero
- FORMATO: formato del PDF a generar, por ej. en planilla factura.csv
- DIRECTORIO: directorio donde almacenar los archivos PDF.
- LINEAS_MAX: cantidad de lineas para el detalle (artículos), por defecto 24
- COPIAS: cantidad de copias en el PDF (Original, Duplicado, Triplicado, etc.)

### Sección [PDF]

Controla campos del PDF a personalizar (si no se especifican los campo texto en tabla formato del PDF): 

- LOGO: archivo con imagen logotipo, por ej. serpiente.png
- EMPRESA: ej. Empresa de Prueba
- MEMBRETE1: ej. Direccion de Prueba
- MEMBRETE2: ej. Capital Federal
- CUIT: CUIT 20-26756539-3
- IIBB: IIBB 20-26756539-3
- IVA: IVA Responsable Inscripto
- INICIO: Inicio de Actividad: 01/04/2006

### Sección [MAIL]

Configura el envío de emails de facturas electrónicas:

- SERVIDOR: nombre del equipo para enviar correos electrónicos, por ej.: adan.nsis.com.ar
- USUARIO: nombre de usuario (si es requerido), por ej.: no.responder@nsis.com.ar
- CLAVE: contraseña del usuario (si es requerido), por ej.: noreplyauto123
- MOTIVO: título (subjet) del correo electrónico, por ej.: Factura Electronica Nro. NUMERO
- CUERPO: mensaje, por ej.: Se adjunta Factura en formato PDF
- REMITENTE: dirección del correo electronico de envío, por ej.: Facturador PyAfipWs <pyafipws@nsis.com.ar>

### Sección [BASE_DATOS]

Establece las opciones para conectarse a la base de datos:

- DRIVER: tipo de motor (con ajustes predeterminados), por ej.: pgsql (PostgreSQL), mssql (MS Sql Server), sqlite u otro (progress)
- DSN: orígen de datos del sistema (con ajustes personalizados), por ej.: pyafipws
- SERVER: nombre del servidor, por ej.: localhost
- DATABASE: nombre dela base de datos, por ej.: pyafipws
- UID: nombre de usuario de conexión, por ej.: pyafipws
- PWD: contraseña del usuario de conexión, por ej.: pyafipws
- encabezado: nombre de tabla de encabezado, por ej.: PUB.encabezado
- detalle: nombre de tabla detalle, , por ej.: PUB.detalle
- permiso: nombre de la tabla permisos de despacho
- cbt_asoc: nombre de la tabla de comprobantes asociados
- xml: nombre de la tabla para registrar los mensajes XML enviados/recibidos

Si no se establece la configuración de una base de datos, se operará sobre una base de datos interna secundaria y temporal (sqlite en memoria) para procesar los comprobantes cargados desde el archivo de entrada y grabados en el archivo de salida.

En este caso, para respaldar los datos, es posible utilizar el motor sqlite y crear una base de datos secundaria que se almacene en disco (configurando ```DRIVER=sqlite``` y en DATABASE el nombre de del archivo donde se almacenarán los datos).

### Sección [PROXY]

Establece las opciones para conectarse a los servicios web a través de un servidor próximo (proxy):

- HOST: ip o nombre del servidor proxy, por ej.: 10.0.0.1
- PORT: puerto del servidor proxy, por ej.: 3129
- USER: nombre de usuario de proxy, por ej.: mariano
- PASS: contraseña del usuario de proxy, por ej.: reingart

Por el momento solo se soportan el esquema de autenticación HTTP básico.

Igualmente, recomendamos no utilizar servidores intermedios, ya que la comunicación es encriptada (igualmente no puede ser analizada por el proxy) y para evitar un nuevo punto de falla, errores de conexión, cache temporales obsoletas, etc.

Si utiliza firewall (cortafuegos de seguridad), para utilizar los webservices debe habilitar el acceso a los servidores de AFIP:

- https://wsaahomo.afip.gov.ar (homologación) y https://wsaa.afip.gov.ar (producción)
- https://wswhomo.afip.gov.ar (homologación) y https://servicios1.afip.gov.ar (producción) 

(todos puerto 443, protocolo HTTP seguro)

## Modo de uso

El programa ```fe_bd.exe``` se utiliza desde línea de comandos (o puede ser ejecutado desde otros programas).

### Argumento --ayuda

Muestra la ayuda interna para descripción de las opciones):

```
C:\PYAFIPWS>fe_bd.exe --ayuda

Opciones:
  --ayuda: este mensaje

  --debug: modo depuración (detalla y confirma las operaciones)
  --esquema: muestra el esquema de la base de datos a utilizar
  --formato: muestra el formato de los archivos de entrada/salida
  --prueba: genera y autoriza una factura de prueba (no usar en producción!)
  --cargar: carga un archivo de entrada (txt) a la base de datos
  --grabar: graba un archivo de salida (txt) con los datos de los comprobantes procesados
  --xml: almacena los requerimientos y respuestas XML (depuración)
  --pdf: genera la imágen de factura en PDF
  --email: envia el pdf generado por correo electronico

  --wsfe o --wsfev1 -wsbfe o --wsfex: selecciona el webservice a utilizar

  --dummy: consulta estado de servidores
  --aut: obtiene el código de autorización electrónico (sino no llama al webservice)
  --get: recupera datos de un comprobante autorizado previamente (verificación)
  --ult: consulta último número de comprobante
  --id: recupera último número de transacción

Ver rece.ini para parámetros de configuración (URL, certificados, etc.)"
```

### Argumentos --formato y --esquema

Muestran el formato de los archivos de texto (entrada y salida) y esquema genérico de la base de datos (respectivamente)

### Argumentos --wsfe, --wsfev1, --wsfex y --wsbfe

Seleccionan el tipo de servicio web a utilizar. 
Si no se especifíca se producirá un error, ya que el resto de los métodos dependen del webservice a utlizar.

### Argumento --dummy (estado)

Consulta el estado de los servidores:
```
C:\PYAFIPWS>fe_bd.exe --wsfe --dummy

{'appserver': 'OK', 'authserver': 'OK', 'dbserver': 'OK'}
```

En este caso, el sevidor de aplicación, autenticación y base de datos de AFIP funcionan correctamente (OK)

### Argumento --aut (autorización)

Solicita autorización de las facturas indicadas (si se ha especificado un ID como argumento en la línea de parámetro) o de todas las facturas no autorizadas hasta el momento.

El programa leerá la base de datos, solicitará autorización (obtención de CAE) por cada factura, actualizara los resultados obtenidos y mostrará en su salida un resumen de la operación:

```
C:\PYAFIPWS>fe_bd.exe --wsfex --aut 44

ID: 44 CAE: 60253670823272 Obs:  Reproceso: N
```

En este caso se está autorizando solo la factura cuyo ID es 44.

### Argumentos --pdf y --email

Estas opciones generan el PDF y lo envían por correo (respectivamente).

Se pueden usar en forma separada, o de manera conjunta con aut para realizar todo el proceso en un único paso.

Recordar informar el número de ID de factura para procesar la factura correspondiente, ej:

```
C:\PYAFIPWS>fe_bd.exe --wsfex --pdf --email 44

Generado C:\factura.pdf
Enviando C:\factura.pdf

```

Los datos para generar la factura y enviarla están especificados en la base de datos o en su defecto en la configuración.

### Argumento --ult (último número de comprobante)

Consulta y muestra el último número de factura electrónica autorizada por AFIP para un determinado tipo de comprobante y punto de venta:

```
C:\PYAFIPWS>fe_bd.exe --wsfex --ult

Consultar ultimo numero:
Tipo de comprobante: 19
Punto de venta: 99

Fecha:  20100616
Ultimo numero:  14
```

Para automatizar la operatoria, es posible pasarle el tipo y numero de comprobante por linea de comandos:

```
C:\PYAFIPWS>fe_bd.exe --wsfex --ult 19 99

Consultar ultimo numero:
Fecha:  20100616
Ultimo numero:  14
```

Importante: como se espera el tipo de comprobante y punto de venta, --ult debe ser el ultimo parametro.

Esta opción es útil para probar el funcionamiento de la interfaz, su configuración (CUIT) y certificados, ya que utiliza todos estos elementos.

### Argumento --get (recuperar datos de comprobante)

Consulta y muestra la factura electrónica autorizada por AFIP para un determinado tipo de comprobante, punto de venta y numero:

```
C:\PYAFIPWS>fe_bd.exe --wsfex --get
Recuperar comprobante:
Tipo de comprobante: 19
Punto de venta: 99
Numero de comprobante: 14
imp_total = 3144
fch_cbte = 20100616
fch_venc_cae = 20100626
cuit = 55000004102
obs = 
cae = 60253429864912
```

### Argumento --id (último id de transacción)

Consulta y muestra el último (mayor) id de transacción:

```
C:\PYAFIPWS>fe_bd.exe --wsfex --id

Ultimo numero (ID) de transacción:  44
```

### Argumento --prueba

Crea una factura ficticia (de ejemplo) para su autorización.
**No utilizar en producción** (ya que no se puede borrar)

### Argumento --cargar

Carga el archivo ENTRADA en las tablas de la base de datos.
Ver formatos y esquema. Ver [archivo txt de muestra](attachment:salida.txt)

Para evita inconvenientes, se recomienda utilizar esta opción cuidadosamente, ya que la aplicación debería insertar los registros que correspondan en la base de datos antes de ejecutar el programa, para que ante cualquier pérdida de energía o error del sistema operativo los datos permanezcan almacenados.

### Argumento --grabar

Graba en el archivo SALIDA los datos procesados (desde la base de datos).
Ver formatos y esquema. Ver [archivo txt de muestra](attachment:salida.txt)

El archivo de salida se crea si no existe, y se van agregando los resultados conforme se autorizan los comprobantes.

### Argumentos --debug y --xml

Estas opciones sirven para depuración del programa.

En especial, --xml guardará los mensajes enviados y recibidos por AFIP (por ejemplo: ```request-20100622001013.xml``` y ```response-20100622001013.xml```), y es fundamental su almacenamiento como bitácora de la comunicación y para posterior análisis en caso de corresponder.

## Ticket de Acceso (WSAA)

De acuerdo a la normativa de AFIP, el programa solicitará un ticket de acceso para poder operar con los servicios web de factura electrónica (```ta-wsfe.xml``` para factura nacional o ```ta-wsfex.xml``` para exportación)

Para ello se utilizan el certificado y clave privada configurada en la sección WSAA, siempre que los archivos temporales del ticket de acceso no existan o cuando estos hayan expirado (por defecto 6 horas).

**Importante**: al cambiar el certificado (o ajustar fecha/hora del equipo), eliminar los archivos temporales ya que de lo contrario se utilizarán con datos incorrectos o expirados.

## Funcionamiento Interno

Ver en el ManualPyAfipWs los respectivos métodos de autenticación y autorización y la descripción detallada de los campos y formatos a utilizar. 

## Comprobaciones en Producción

### WSAA (autenticación)

Para verificar el comportamiento correcto en producción o en homologación (testing), se puede utilizar la herramienta en modo depuración (sin necesidad de autorizar una factura, solo solicitar acceso):

```
C:\PYAFIPWS>fe_bd.exe --wsfex --debug
wsaa_url https://wsaahomo.afip.gov.ar/ws/services/LoginCms
wsfex_url https://wswhomo.afip.gov.ar/wsfex/service.asmx
creando ta-wsfex.xml
------------------------------------------------------------------------------
<?xml version="1.0" encoding="UTF-8"?>
<loginTicketRequest version="1.0">
 <header>
  <uniqueId>1279056027</uniqueId>
  <generationTime>2010-07-13T13:20:27</generationTime>
  <expirationTime>2010-07-13T23:20:27</expirationTime>
 </header>
 <service>wsfex</service>
</loginTicketRequest>
------------------------------------------------------------------------------
POST https://wsaahomo.afip.gov.ar/ws/services/LoginCms
SOAPAction: "http://ar.gov.afip.dif.facturaelectronica/loginCms"
Content-length: 3369
Content-type: text/xml; charset="UTF-8"

<?xml version="1.0" encoding="UTF-8"?><soap:Envelope 
xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" 
...
```

Para descartar cualquier problema técnico se puede utilizar la salida que es la traza de depuración de la comunicación con AFIP a la mesa de ayuda (requerimiento y respuesta xml).

Si se estaría conectando correctamente a producción, el certificado y las URL son correctas, etc., se debería constatar que:

- El ticket de requerimiento de acceso (TRA) correctamente solicita servicio wsfex: ```<service>wsfex</service>```
- Se está solicitando acceso a los servidores de producción (```wsaa_url```): ```POST https://wsaa.afip.gov.ar/ws/services/LoginCms``` y no ```http://wsaahomo.afip.gov.ar/ws/services/LoginCms```
- El equipo que responde sería de producción: ```pereza.afip.gov.ar``` o ```envidia.afip.gov.ar``` (producción) y no ```avaricia.afip.gov.ar``` (homologación). Nota: los nombres de los servidores pueden cambiar.

Si la autenticación es exitosa (```El archivo TA.xml se ha generado correctamente.```, en el mensaje XML contenido en dicho archivo se puede verificar los siguientes datos:

- Fuente: AFIP producción (```<source>CN=wsaa, O=AFIP, C=AR, SERIALNUMBER=CUIT 33693450239</source>```), sinó diría ```CN=wsaahomo```
- Destino: cliente en producción -datos del certificado- (```<destination>C=ar, O=empresa sa, SERIALNUMBER=CUIT 20267565393, CN=pyafipws</destination>```)

Si el ambiente es el correcto (producción/homologación) y sigue devolviendo acceso denegado: ```ns1:coe.notAuthorized: Computador no autorizado a acceder al servicio (gov.afip.desein.dvadac.sua.view.wsaa.LoginFault)```, revisar el certificado, ARFE (asociación de servicio), RECE/REAR/RFI sobre régimen habilitado, puntos de venta, y demás trámites ante AFIP.

### WSFEX

Para comprobar que el programa funcione bien pueden realizar las siguientes pruebas (solicitar último ID, último número de comprobante y recuperar comprobante, preferentemente luego de haber realizado la primer factura):

```
C:\PYAFIPWS>fe_bd.exe --wsfex --id
Ultimo numero (ID) de transacción:  99000000000582

C:\PYAFIPWS>fe_bd.exe  --wsfex --ult
Consultar ultimo numero:
Tipo de comprobante: 19
Punto de venta: 99
Fecha:  20100616
Ultimo numero:  14

C:\PYAFIPWS>fe_bd.exe  --wsfex --get --xml
Recuperar comprobante:
Tipo de comprobante: 19
Punto de venta: 99
Numero de comprobante: 14
imp_total = 3144
fch_cbte = 20100616
fch_venc_cae = 20100626
cuit = 55000004102
obs =
cae = 60253429864912

```

Además, se generan los archivos xml (por ej. ```request-20100713180024.xml``` y ```response-20100713180024.xml```), de los cuales se debería revisar la respuesta (response) donde están todos los campos que registró la AFIP.

## Tratamiento de errores

### Redirección salida y errores

Se recomienda ejecutar el programa desde un archivo BAT o SH, almacenando la salida estándar como bitácora (log) y la salida de error para informar al usuario final:

```
@ECHO OFF
REM Cambio al directorio de la interfaz
CD C:\PYAFIPWS
REM Ejecuto la herramienta, redirigiendo salida y errores
FE_BD.EXE %1 %2 %3 %4 %5 %6 %7 %8 %9 --debug --xml >> bitacora.txt 2> error.txt
REM Informo el error al usuario/aplicación (si hay)
TYPE error.txt
```

En el ejemplo, una aplicación podría fácilmente ejecutar estas órdenes pudiendo mostrar al usuario la información relevante del error, y el registro de la operatoria quedaría almacenado en el archivo de bitácora para futura referencia por parte de los programadores. 

En este caso, el archivo error.txt se sobreescribe en cada uso (contemplar nombres de archivo diferentes si es necesario acceso simultáneo).

### Ejemplos de errores
La salida de error consta de dos líneas: código y descripción.

El WSAA informa el código alfanumérico (por ejemplo, si el reloj esta de-sincronizado):
```
ns1:xml.generationTime.invalid
generationTime en el futuro o m?s de 24 horas de antig?edad
```

El WSFE, WSBFE y WSFEX informa el código numérico:
```
1550
Campo Permiso_existente:''.Obligatorio para Factura E y tipo_expo=1. Debe ser S o N.
```

**Base de datos**: adicionalmente, estos últimos errores (WSFE, WSFEX y WSFEX), de corresponder, se almacenan en la tabla encabezado, campos err_code y err_msg.

Consultar la documentación de los respectivos webservices para el listado completo de los códigos de error y/o mayor información:

- [Especificación Técnica WSAA](http://wswhomo.afip.gov.ar/fiscaldocs/WSAA/Especificacion_Tecnica_WSAA_1.2.0.pdf)
- [Manual para el desarrollador WSFE](http://wswhomo.afip.gov.ar/fiscaldocs/WSFE/WSFE%20-%20Manual%20para%20el%20desarrollador%20-%20090317.pdf)
- [Manual para el desarrollador WSFEX](http://wswhomo.afip.gov.ar/fiscaldocs/WSFEX/WSFEX%20-%20Manual%20para%20el%20desarrollador.pdf)

## Soporte Comercial

Si necesita asesoramiento, demostración, capacitación, consultoría técnica, ofrecemos Soporte Comercial Pago y abonos de mantenimiento mensuales (opcional).
Comunicarse a [mailto:facturaelectronica@sistemasagiles.com.ar] o telefónicamente al 15-3048-9211

MarianoReingart
MarianoReingart