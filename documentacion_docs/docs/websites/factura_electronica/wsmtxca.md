# Factura Electrónica MTXCAService (RG2904, RG3536)
[[TracNav(noreorder|FacturaElectronica)]]

Interfaz para Servicio Web correspondiente a Factura Electrónica de Mercado Interno con detalle -Régimen CAE codificación de productos- ([Matrix](http://www.afip.gob.ar/matrix/): Codificación de las operaciones efectuadas [WSMTXCA Service](http://www.afip.gov.ar/fe/documentos/manualdesarrolladormtx_v0_1.pdf)) para el régimen especial *los Sujetos notificados de su incorporación al Régimen de emisión y almacenamiento electrónico de comprobantes originales* previstos originalmente en la RG 2757/2010, modificada por [RG 2904/2010](http://www.infoleg.gov.ar/infolegInternet/anexos/170000-174999/171723/norma.htm) -(Artículo 4 opción *"a) Factura con el detalle previsto en el Artículo 5º, inciso c)"*) y [RG 3536/2013](http://www.infojus.gov.ar/legislacion/resolucion-nacional-afip-3536-2013.htm): [RG4540/2019](https://www.boletinoficial.gob.ar/detalleAviso/primera/212546/20190801) Condiciones de Emisión de notas de crédito y/o débito.


## Índice
[[Image(htdocs:logo-pyafipws.png, align=right)]]
[[TOC(noheading,inline,depth=3)]]
## Descripción General

EL WSMTXCA es un nuevo Servicio Web de la AFIP para el 
*Régimen especial para la emisión y almacenamiento electrónico de comprobantes originales que respalden las operaciones de compraventa de cosas muebles, locaciones y prestaciones de servicios, locaciones de cosas y de obras y de las señas o anticipos que congelen precios, efectuadas en el mercado interno.*, correspondiente a la 
Resolución [Resolución General 2904/2010](http://www.afip.gov.ar/fe/#rg) Art.4 Opción A- 

**NOTA**: Ver [WSFEv1](wiki:ProyectoWSFEv1) (Proyecto Factura Electrónica v1, Opción B)


Este nuevo webservice contempla las operaciones de mercado interno (Facturas A y B) y CAE Anticipado.

### Importante: RG3536/2013 AFIP

Esta interfaz ya contempla la [Resolución General 3536/2013](http://biblioteca.afip.gob.ar/gateway.dll/Normas/ResolucionesGenerales/reag01003536_2013_10_30.xml) que dió de baja el aplicativo del SIAP para informar el detalle de la factura, denominado  "AFIP DGI - FACTURA ELECTRONICA - REGIMEN DE INFORMACION DE OPERACIONES - Versión 2.0".

Dicho aplicativo, junto con el webservice anterior (WSFEv1), podrá ser usado solo hasta el 31 de Diciembre de 2013 (usuarios preexistentes notificados por juez administrativo, que en su momento optaron por la opción B de la RG2904), debiendo usar este webservice a partir del 1° de Enero de 2014. Asimismo, el período comprendido entre los días 16 y 31 de diciembre de 2013, ambas fechas inclusive, deberá informarse hasta última hora del día 3 de enero de 2014, inclusive.

Los nuevos sujetos obligados solo pueden usar el webservice WSMTXCA e informar el detalle de la factura (incluyendo códigos de barra, descripción de productos, precio unitario e impuestos) de manera online.

### Importante: Release v0.5

AFIP publicó una nueva [Especificación Técnica "Release v0.5"](http://www.afip.gov.ar/fe/documentos/Web_Service_MTXCAv05.pdf) (manual para desarrolladores) con fecha 15 de Marzo de 2017 AFIP, con las siguientes novedades:

- Nuevo campo Cuit en Comprobantes Asociados
- 88 – Remito de Tabaco Acondicionado 
- 991 – Remito de Tabaco en Hebras

Los ajustes ya han sido realizados al componente, disponibles por actualización a partir de `WSMTX.Version >= 1.13a` (revisión 1941 o superior del instalador), igualmente recomendamos probarlo y evaluarlo en homologación (Ver [Descargas](wiki:FacturaElectronicaMTXCAService#Descargas)), para ver como evoluciona desde AFIP.

Lamentablemente al 16 de Marzo de 2017 todavía no estaría disponible el WSDL de AFIP para homologación.

Recordamos que si no son necesarias las nuevas características, no es obligatorio actualizar y re-instalar el componente. 
Provisoriamente puede limpiarse la carpeta cache de archivos temporales, para que se regeneren y pueda continuar operando.

Para más información ver [Service Pack 2](wiki:ActualizacionesFacturaElectronica#ServicePack2) y documentación [método WSMTX AgregarCmpAsoc](wiki:ManualPyAfipWs#Métodos5) en el manual


### Importante: Release v0.10 Factura de Crédito Electrónica

La [RG4367/ 2018](http://www.afip.gov.ar/noticias/20181220-regimenFacturaCreditoElectronica.asp) incorpora comprobantes Factura de Crédito Electrónica.

AFIP publicó una nueva  Especificación Técnica "Emisión FCE WSMTXCA v0.10" (manual para desarrolladores) con fecha 1 de Julio de 2019 AFIP, con las siguientes novedades:

- Nuevos comprobantes:

   - 201: Factura de Crédito Electrónica MiPyMEs (FCE) A
   - 202: Nota de Débito Electrónica MiPyMEs (FCE) A
   - 203: Nota de Crédito Electrónica MiPyMEs (FCE) A
   - 206: Factura de Crédito Electrónica MiPyMEs (FCE) B
   - 207: Nota de Débito Electrónica MiPyMEs (FCE) B
   - 208: Nota de Crédito Electrónica MiPyMEs (FCE) B
   
- En comprobanteAsociado se agrega campo <fecha emisión>

- Nuevos datos a informar: CBU, alias o código de anulación. Ver [Datos Adicionales AFIP WSMTXCA](wiki:FacturaElectronicaMTXCAService#DatosAdicionales) 
 
  Para esto se agrega método !AgregarOpcional

```
#!vb
WSMTXCA.AgregarOpcional(21, "2850590940090418135201", "alias")  ' CBU (alias opcional) Solo Factura
WSMTXCA.AgregarOpcional(22, "S")        ' Anulación para N/C o N/D

```

Nuevas validaciones de AFIP:

- En las validaciones de los métodos para autorizar un comprobante CAE se agregaron las siguientes validaciones excluyentes:

  - 147: Si codigoTipoComprobante es igual a 201, 202, 203, 206, 207 ó 208. Por las condiciones de la CUIT Emisora, no corresponde realizar FCE (para capo CUIT representada)
  - 148: Si codigoTipoComprobante es igual a 201 ó 206. La Fecha de Vencimiento de Pago es obligatorio para Facturas de Crédito MiPyME  (campo fecha vencimiento de pago)
  - 149: Si codigoTipoComprobante es igual a 202, 203, 207 ó 208. La Fecha de Vencimiento de Pago no debe informarse para Notas de Crédito o Débito de las Facturas de Crédito MiPYME (campo fecha vencimiento de pago)
  - 150: Si codigoTipoComprobante es igual a 201, 202, 203, 206, 207 ó 208. La CUIT Receptora no está incluida en el listado de empresas grandes según cronograma vigente ni optó por ser receptora de Factura de Crédito MiPyme (campos código Tipo Documento / número de documento) 
  - 151: 
        - Si codigoTipoComprobante es igual a 1 ó 6, **y**
        - La CUIT Receptora está incluida en el listado de empresas grandes según cronograma vigente u optó por ser receptora de Factura de Crédito MiPyme, **y**
        - Por las condiciones de la CUIT Emisora, **y**
        - El monto facturado es mayor o igual al Reglamentado

    Corresponde realizar Factura Electrónica de Crédito MiPyME, realice un comprobante con codigoTipoComprobante 201 o 206.  (campos cuit Representada /código tipo de documento / número de documento /importe Total)
  - 152:
        - Si codigoTipoComprobante es igual a 201 ó 206, **y**
        - La CUIT Receptora está incluida en el listado de empresas grandes según cronograma vigente u optó por ser receptora de Factura de Crédito MiPyme, **y**
        - Por las condiciones de la CUIT Emisora, **y**
        - El monto facturado es menor al Reglamentado

    NO Corresponde realizar Factura Electrónica de Crédito MiPyME, realice un comprobante con <codigoTipoComprobante> 1 o 6. (campos cuit Representada / código tipo de documento / número de documento /importe Total)
  - 153: Si <codigoTipoComprobante> es igual a 203 ó 208. El importe total del comprobante a autorizar no puede ser mayor o igual al saldo de la operación actual de la cuenta corriente. ( campo importe total)
  - 154: Si <codigoTipoComprobante> es igual a 202, 203, 207 ó 208, la moneda debe:
         - coincidir con la Factura vinculada, ó
         - ser Pesos Argentinos si la Factura vinculada ya fue aceptada, cancelada o rechazada y se desea realizar un ajuste por diferencia de cambio (campo código moneda)      
  - 155: Si <codigoTipoComprobante> es igual a 201, 202, ó 203 la CUIT del receptor debe encontrarse activa en IVA. (número de documento)
  - 156: Si <codigoTipoComprobante> es igual a 206, 207, ó 208 la CUIT del receptor debe encontrarse activa como Responsable Inscripto, IVA Exento o Monotributista. (campo número de documento)
  - 208: Deberá ser igual a 88, 91, 991 o 995 si el tipo de comprobante cuya autorización se solicita es igual a 201 o 206. (código Tipo de Comprobante)
  - 209: Al autorizar una nota de débito o crédito de Factura Electrónica de Crédito MiPyME (202, 203, 207, 208), debe enviar el campo cuit para el tipo de comprobante asociado indicado. (cuit)
  - 210: Al autorizar una nota de débito o crédito de Factura Electrónica de Crédito MiPyME (202, 203, 207, 208), el campo cuit para el tipo de comprobante asociado indicado debe coincidir con la cuit emisora del comprobante a autorizar. (cuit)
  - 211: Al autorizar una nota de débito o crédito de Factura Electrónica de Crédito MiPyME (202, 203, 207, 208), el comprobante asociado codigoTipoComprobante, PtoVenta, numeroComprobante, deberá obrar en las bases del organismo.
  - 223: 
  - 302:
  - 326 a 332:
  - 433:


### Importante: RG4540/2019 FEv0.13

Se incorpora método AgregarPeriodoComprobantesAsociados como opcional al método Comprobante Asociado, para cumplimentar con lo establecido por la [RG4540/19 Procedimiento, Facturación. Emisión de notas de crédito y/o débito](https://www.boletinoficial.gob.ar/detalleAviso/primera/212546/20190801)

ver: [Métodos WSMTXCA](wiki:ManualPyAfipWs#Métodos5)


### Importante: RG5259/2022 y RG5264/2022

AFIP publicó una nueva [Especificación Técnica "v 0.18"](https://www.afip.gob.ar/ws/manuales-provisorios/documentos/Web-Service-MTXCA-v18.pdf) (manual para desarrolladores)

Se incorpora método para la consulta de Actividades vigentes (ConsultarActividadesVigentes) y una estructura de actividades vinculadas al comprobante tanto en la
emisión de CAE, en el régimen de información de CAEA.
Se modifica el método de ConsultaComprobante para que en caso de tener actividades asociadas al comprobante las retorne.

ver: [Métodos WSMTXCA](wiki:/ManualPyAfipWs#M%C3%A9todos5) 


Aplicación: Resultará de aplicación **optativa** a partir del 15 de noviembre de 2022 y **obligatoria** desde el 15 de diciembre de 2022, posterior a esta fecha, los comprobantes serán rechazados si la actividad es Cárnico.
A partir del 01 de Febrero del 2023 será **optativa** hasta el 28/2 y desde el 01 de Marzo del 2023 será **obligatoria**, siendo rechazados los comprobantes, siendo la actividad Harina.

*Nota:* Al momento de confeccionar el correspondiente comprobante electrónico, que se emita para respaldar las operaciones de venta de carne y subproductos derivados de la faena de hacienda de las especies bovina/bubalina y porcina y las operaciones de venta de harinas y/o subproductos derivados de la molienda de trigo se deberá seleccionar la actividad por la cual se está realizando el mismo, con el objeto de identificar el o los “REC” emitidos.

### RG5616/2024 FEv4

ARCA estableció nuevos criterios de Facturación para las operaciones realizadas en moneda extranjera.

Ver["Resolución 5616/24"](https://www.boletinoficial.gob.ar/detalleAviso/primera/318374/20241218)

- Se afregan nuevos campos al método `CrearFactura(...)`:

                            - `cancela_misma_moneda_ext`
                            - `condicion_iva_receptor_id`

- Nuevos Metodos auxiliares:

                            - `ParamGetCotizacion(moneda_id, fecha)`: se agrega fecha de cotizacion
                            - `ParamGetCondicionIvaReceptor(clase_cmp)`: consultar condiciones de iva por clase de comprobante

Se agregan nuevas validaciones.


Aplicación:  Obligatorio para webservice a partir del 15 de Abril de 2025. (Prorrogado 1 de Agosto 2025)

**Importante**: en `condicion_iva_receptor_id` es obligatorio a partir de la Versión 4, pero no debe ser enviado hasta que este en producción. En homologación ya se encuentra habilitado.

#### Mensaje de Evento 39

El servidor de ARCA devuelve el siguiente mensaje de evento, XmlResponse, independientemente de si en envian los campos nuevos o no.

```
#!xml
<Events>
  <Evt>
    <Code>39</Code>
    <Msg>IMPORTANTE: El dia 6 de abril de 2025, se actualizo la version del Web Service (WS) que permite enviar, de forma opcional, el campo Condicion Frente al IVA del receptor. Cabe destacar que la Resolucion General Nro 5616 indica que ese dato de  enviarse de manera obligatoria a partir del 15/04/2025. No obstante, se mantendra como un dato no excluyente hasta el 30/06/2025, inclusive. A partir del 1/07/2025 se rechazaran las solicitudes de emision de comprobantes sin este dato. Para mas
informacion, consultar el manual en: https://www.arca.gob.ar/fe/ayuda/webservice.asp, https://www.arca.gob.ar/ws/documentacion/ws-factura-electronica.asp</Msg>
  </Evt>
</Events>
```

#### Mensaje de Observacion 10245

El siguiente mensaje de observacion es enviado por el webservice si no se envían los campos nuevos es el siguiente (caso condicion_iva_receptor_id),

```
#!xml
<Observaciones>
  <Obs>
    <Code>10245</Code>
    <Msg>El campo Condicion Frente al IVA del receptor resultara obligatorio conforme lo reglamentado por la Resolucion General Nro 5616. Para mas informacion consular metodo FEParamGetCondicionIvaReceptor</Msg>
  </Obs>
</Observaciones>
```


En este caso revisar que se estan enviando los campos, por ej. con el siguiente codigo:

```
#!vb
ok = WSFEv1.EstablecerCampoFactura("cancela_misma_moneda_ext", "N")
ok = WSFEv1.EstablecerCampoFactura("condicion_iva_receptor_id", "5")
```

Adicionalmente, borrar la carpeta cache donde se encuentran descargada la descripción del servicio web (WSDL), por si esta desactualizada.

Eventualmente utilizar el siguiente instalador para actualizar la carpeta cache:

https://www.sistemasagiles.com.ar/soft/pyafipws/final/PyAfipWS-Cache-UPDATE-2025.4.6.exe

















## Estado

La AFIP publicó la [información técnica](http://www.afip.gov.ar/fe/documentos/manualdesarrolladormtxv0.pdf), y el servicio WSMTXCA ya está disponible en homologación para realizar pruebas.

Por dicho motivo, dado la inminente fecha de aplicación, desarrollaremos para nuestros clientes, un **SIMULADOR** que emula los métodos del servicio web, para poder comenzar los desarrollos:

- https://www.sistemasagiles.com.ar/simulador/

Para esta interfaz, hemos desarrollado nuevas bibliotecas de [Cliente/Servidor SOAP](http://code.google.com/p/pysimplesoap/) y manejo de XML mejorado, mejorando la versión anterior, lo que permitirá mayor flexibilidad, depuración y control de errores.
Por este motivo, la interfaz se instalará de forma separada, para evitar inconvenientes, manteniendo la simplicidad y modo de uso actual.

## Descargas
Ver archivos y últimas actualizaciones para descargas en [GitHub](https://github.com/reingart/pyafipws/releases) (actualizado) y [GoogleCode](http://code.google.com/p/pyafipws/downloads/list) (histórico):

- Instalador: 
- [PyAfipWs-2.7.3284-32bit+wsaa_2.13a+wsmtx_1.17a-homo.exe](https://www.sistemasagiles.com.ar/soft/pyafipws/PyAfipWs-2.7.3284-32bit+wsaa_2.13a+wsmtx_1.17a-homo.exe) para evaluación (WSMTXCA v0.25  2025, RG 5616)
- [instalador-WSMTXCA-1.04b-homo.exe](https://pyafipws.googlecode.com/files/instalador-WSMTXCA-1.04b-homo.exe)
- Ejemplo en VB: [wsmtx.bas](https://github.com/reingart/pyafipws/blob/master/ejemplos/wsmtxca/wsmtx.bas)
- Ejemplo en VFP: [wsmtxca.prg](https://github.com/reingart/pyafipws/blob/master/ejemplos/wsmtxca/wsmtxca.prg)
- Tablas DBF ejemplo: [RECEM_dbf.zip](attachment:recem_dbf.zip) (para dBase, Clipper, !FoxPro, Harbour, etc.) Ver [ManualPyAfipWs#InterfaseporarchivosdetextosímilSIAP-RECE RECEM]
- [Manual de Uso](wiki:ManualPyAfipWs): Documentación ([PDF](http://www.sistemasagiles.com.ar/trac/wiki/ManualPyAfipWs?format=pdf)) [Documentación Oficial PDF AFIP](http://www.afip.gov.ar/fe/documentos/manualdesarrolladormtx_v0_1.pdf)
- Código Fuente (Python): ver archivos publicados en [Google Code](http://code.google.com/p/pyafipws/source/checkout) 

## Instalación

Está disponible el instalador (ver [Descargas](wiki:FacturaElectronicaMTXCAService#Descargas)), simplemente descargar, ejecutar seguir los pasos:

- Aceptar la licencia
- Seleccionar carpeta, por ej `C:\WSMTXCA`
- Instalación y registración automática

Adicionalmente, si no se utilizó el instalador unificado con todos los webservices, es necesario instalar el instalador [instalador-WSAA-2.02c-homo.exe](http://pyafipws.googlecode.com/files/instalador-WSAA-2.02c-homo.exe) para WSAA (autenticación).
Para más información ver el [Manual de Uso](wiki:ManualPyAfipWs#Instalación)

## Cambios respecto a WSFE, WSFEX, WSBFE

En este nuevo servicio web WSMTXCA, además de los campos requeridos por el WSFE para autorizar una factura (obtener el CAE), se debe informar:

- Concepto: similar al tipo de exportación (WSFEX) / presta_serv (WSFE)
- Moneda (según tabla de parámetros) y cotización de la factura
- Comprobantes Asociados: tipo de comprobante, punto de venta y número, similar a WSFEX
- Tributos: id, descripción, base imponible, alícuota (porcentaje), importe
- Subtotales de IVAs: id (según tabla de parámetros), base imponible, importe, similar a WSBFE
- Detallar cada artículo vendido (ítems)
- Código MTX: Codificación del producto (Códigos GTIN 13, GTIN 12 y GTIN 8), correspondientes a la unidad de consumo minorista o presentación al consumidor final
- Unidades MTX: Unidad de referencia (cantidades de unidades de consumo minoristas contenidas en la presentación que se comercializa)
- Código interno del producto
- Descripción completa
- Precio Neto Unitario
- Cantidad 
- Unidad de medida (según tabla de parámetros)
- Bonificaciones
- Categoría de IVA (según tabla de parámetros)
- Importe de IVA
- Importe subtotal

La operatoria es bastante similar al método de autorización del WSFE, teniendo en cuenta esta mayor complejidad por tener que informar el detalle de cada item y las condiciones de exportación.

**NOTA**: Este webservice no tiene ID secuencial ni reproceso, por lo que el programa debe implementar la consulta de CAE en caso de errores de comunicación.

A su vez, el WSMTXCA devuelve mensajes de eventos (mantenimiento programado, advertencias, etc.), los que deben ser capturados e informados al usuario.

Para mayor información, se puede consultar la documentación orignal en [Manual del WSMTXv0 - AFIP](http://www.afip.gov.ar/fe/documentos/manualdesarrolladormtxv0.pdf) o el [manual](wiki:ManualPyAfipWs) manual de la presente interfaz. 

## Ejemplo Intefase COM en VB (5/6)

```
#!vb
' Establezco los valores de la factura a autorizar:
tipo_cbte = 1
punto_vta = 4000
cbte_nro = WSMTXCA.ConsultarUltimoComprobanteAutorizado(tipo_cbte, punto_vta)
fecha = Format(Date, "yyyy-mm-dd")
concepto = 1
tipo_doc = 80: nro_doc = "30000000007"
cbt_desde = cbte_nro + 1: cbt_hasta = cbte_nro + 1
imp_total = "122.00": imp_tot_conc = "0.00": imp_neto = "100.00"
imp_trib = "1.00": imp_op_ex = "0.00": imp_subtotal = "100.00"
fecha_cbte = fecha: fecha_venc_pago = fecha
' Fechas del período del servicio facturado (solo si concepto = 1?)
fecha_serv_desde = fecha: fecha_serv_hasta = fecha
moneda_id = "PES": moneda_ctz = "1.000"
obs = "Observaciones Comerciales, libre"

' Creo la factura (internamente, sin llamar al WS)
ok = WSMTXCA.CrearFactura(concepto, tipo_doc, nro_doc, tipo_cbte, punto_vta, _
    cbt_desde, cbt_hasta, imp_total, imp_tot_conc, imp_neto, _
    imp_subtotal, imp_trib, imp_op_ex, fecha_cbte, fecha_venc_pago, _
    fecha_serv_desde, fecha_serv_hasta, _
    moneda_id, moneda_ctz, obs, cancela_misma_moneda_ext, condicion_iva_receptor_id
)

' Agrego los comprobantes asociados:
If False Then ' solo si es nc o nd
    tipo = 19
    pto_vta = 2
    nro = 1234
    ok = WSMTXCA.AgregarCmpAsoc(tipo, pto_vta, nro)
End If

' Agrego impuestos varios
id = 99
Desc = "Impuesto Municipal Matanza'"
base_imp = "100.00"
alic = "1.00"
importe = "1.00"
ok = WSMTXCA.AgregarTributo(id, Desc, base_imp, alic, importe)

' Agrego subtotales de IVA
id = 5 ' 21%
base_imp = "100.00"
importe = "21.00"
ok = WSMTXCA.AgregarIva(id, base_imp, importe)

' Agrego un Artículo (repetir para todos los artículos y descuentos)
u_mtx = 123456
cod_mtx = "12345678901234"
codigo = "P0001"
ds = "Descripcion del producto P0001"
qty = "1.0000"
umed = 7
precio = "100.00"
bonif = "0.00"
cod_iva = 5
imp_iva = "21.00"
imp_subtotal = "121.00"
ok = WSMTXCA.AgregarItem(u_mtx, cod_mtx, codigo, ds, qty, _
            umed, precio, bonif, cod_iva, imp_iva, imp_subtotal)

' Solicito CAE:
cae = WSMTXCA.AutorizarComprobante()

' verifico que no haya errores
For Each er In WSMTXCA.Errores
    MsgBox er, vbInformation, "Error:"
Next

Debug.Print "Resultado", WSMTXCA.Resultado
Debug.Print "CAE", WSMTXCA.cae
Debug.Print "Vencimiento CAE", WSMTXCA.Vencimiento
Debug.Print "Observaciones", WSMTXCA.Obs
Debug.Print "Observaciones", WSMTXCA.Obs

```

**Nota:** La metodología es similar al resto de los webservices, y se trato de mantener similitud con el código existente:

- Método WSMTXCA.!CrearFactura es similar a WSFE.Authorize (parámetros similares)
- Método WSMTXCA.!AgregarCmpAsoc es similar a WSFEX.!AgregarCmpAsoc
- Método WSMTXCA.!AgregarItem es similar a WSBFE.!AgregarItem
- Propiedades similares: WSMTXCA.CAE, WSMTXCA.Resultado, etc.

## Tablas de Parámetros

Wste nuevo servicio funciona con tablas dinámicas de parámetros para los códigos de comprobante, moneda, IVA, tribuots, unidades de medida. Estas tablas pueden sufrir modificaciones realizadas por la AFIP, con altas y bajas lógicas, por lo que tienen una fecha de vigencia (desde, hasta) y se proveen métodos para consultarlas por el mismo servicio web (a diferencia del WSFE, que las tablas eran documentadas estaticamentes en el sitio web).

Ver Planilla [Anexo Tablas del Sistema](http://www.afip.gov.ar/fe/documentos/TABLAS%20GENERALES%20V.0%20%2025082010.xls) (puede estar desactualizado respecto los últimos cambios)

Como ejemplo, a continuación se copian los resultados de invocar a los webservices para consultar las tablas de parámetros al 20/10/2010 (homologación):

### Tipos de Comprobante
| 1 | Factura A |
|---|---|
| 2 | Nota de Débito A |
| 3 | Nota de Crédito A |
| 6 | Factura B |
| 7 | Nota de Débito B |
| 8 | Nota de Crédito B |
| 201 | Factura de Crédito electrónica MiPyMEs (FCE) A |
| 202 | Nota de Débito electrónica MiPyMEs (FCE) A |
| 203 | Nota de Crédito electrónica MiPyMEs (FCE) A |
| 206 | Factura de Crédito electrónica MiPyMEs (FCE) B |
| 207 | Nota de Débito electrónica MiPyMEs (FCE) B |
| 208 | Nota de Crédito electrónica MiPyMEs (FCE) B |
### Tipos de Documento
| 80 | CUIT |
|---|---|
| 86 | CUIL |
| 87 | CDI |
| 89 | LE |
| 90 | LC |
| 91 | CI Extranjera |
| 92 | en trámite |
| 93 | Acta Nacimiento |
| 95 | CI Bs. As. RNP |
| 96 | DNI |
| 94 | Pasaporte |
| 0 | CI Policía Federal |
| 1 | CI Buenos Aires |
| 2 | CI Catamarca |
| 3 | CI Córdoba |
| 4 | CI Corrientes |
| 5 | CI Entre Ríos |
| 6 | CI Jujuy |
| 7 | CI Mendoza |
| 8 | CI La Rioja |
| 10 | CI San Juan |
| 11 | CI San Luis |
| 9 | CI Salta |
| 12 | CI Santa Fe |
| 13 | CI Santiago del Estero |
| 14 | CI Tucumán |
| 16 | CI Chaco |
| 17 | CI Chubut |
| 18 | CI Formosa |
| 19 | CI Misiones |
| 20 | CI Neuquén |
| 21 | CI La Pampa |
| 22 | CI Río Negro |
| 23 | CI Santa Cruz |
| 24 | CI Tierra del Fuego |
| 99 | Doc. (Otro) |
### Alicuotas de IVA
| 3 | 0% |
|---|---|
| 4 | 10.5% |
| 5 | 21% |
| 6 | 27% |
### Condiciones de IVA
| 1 | No gravado |
|---|---|
| 2 | Exento |
| 3 | 0% |
| 4 | 10.5% |
| 5 | 21% |
| 6 | 27% |
### Concepto

| 1 | Productos |
|---|---|
| 2 | Servicios |
| 3 | Productos y Servicios |

### Monedas
| PES | Pesos Argentinos |
|---|---|
| DOL | Dólar Estadounidense |
| 007 | Florines Holandeses |
| 010 | Pesos Mejicanos |
| 011 | Pesos Uruguayos |
| 014 | Coronas Danesas |
| 015 | Coronas Noruegas |
| 016 | Coronas Suecas |
| 018 | Dólar Canadiense |
| 019 | Yens |
| 021 | Libra Esterlina |
| 023 | Bolívar Venezolano |
| 024 | Corona Checa |
| 025 | Dinar Yugoslavo |
| 026 | Dólar Australiano |
| 027 | Dracma Griego |
| 028 | Florín (Antillas Holandesas) |
| 029 | Güaraní |
| 031 | Peso Boliviano |
| 032 | Peso Colombiano |
| 033 | Peso Chileno |
| 034 | Rand Sudafricano |
| 036 | Sucre Ecuatoriano |
| 051 | Dólar de Hong Kong |
| 052 | Dólar de Singapur |
| 053 | Dólar de Jamaica |
| 054 | Dólar de Taiwan |
| 055 | Quetzal Guatemalteco |
| 056 | Forint (Hungría) |
| 057 | Baht (Tailandia) |
| 059 | Dinar Kuwaiti |
| 012 | Real |
| 030 | Shekel (Israel) |
| 035 | Nuevo Sol Peruano |
| 060 | Euro |
| 040 | Lei Rumano |
| 042 | Peso Dominicano |
| 043 | Balboas Panameñas |
| 044 | Córdoba Nicaragüense |
| 045 | Dirham Marroquí |
| 063 | Lempira Hondureña |
| 046 | Libra Egipcia |
| 047 | Riyal Saudita |
| 062 | Rupia Hindú |
| 061 | Zloty Polaco |
| 064 | Yuan (Rep. Pop. China) |
| 002 | Dólar Libre EEUU |
| 009 | Franco Suizo |
| 041 | Derechos Especiales de Giro |
| 049 | Gramos de Oro Fino |
### Unidades de Medida
| 0 |  |
|---|---|
| 1 | kilogramos |
| 2 | metros |
| 3 | metros cuadrados |
| 4 | metros cúbicos |
| 5 | litros |
| 6 | 1000 kWh |
| 7 | unidades |
| 8 | pares |
| 9 | docenas |
| 10 | quilates |
| 11 | millares |
| 14 | gramos |
| 15 | milimetros |
| 16 | mm cúbicos |
| 17 | kilómetros |
| 18 | hectolitros |
| 20 | centímetros |
| 25 | jgo. pqt. mazo naipes |
| 27 | cm cúbicos |
| 29 | toneladas |
| 30 | dam cúbicos |
| 31 | hm cúbicos |
| 32 | km cúbicos |
| 33 | microgramos |
| 34 | nanogramos |
| 35 | picogramos |
| 41 | miligramos |
| 47 | mililitros |
| 48 | curie |
| 49 | milicurie |
| 50 | microcurie |
| 51 | uiacthor |
| 52 | muiacthor |
| 53 | kg base |
| 54 | gruesa |
| 61 | kg bruto |
| 62 | uiactant |
| 63 | muiactant |
| 64 | uiactig |
| 65 | muiactig |
| 66 | kg activo |
| 67 | gramo activo |
| 68 | gramo base |
| 96 | packs |
| 97 | seña/anticipo |
| 98 | otras unidades |
| 99 | bonificación |
### Tipos de Tributo
| 1 | Impuestos Nacionales |
|---|---|
| 2 | Impuestos Provinciales |
| 3 | Impuestos Municipales |
| 4 | Impuestos Internos |
| 99 | Otros |

### Datos Adicionales
| 1 | Datos adicionales para Entes Reguladores. [NO HABILITADO - RESERVADO PARA USO FUTURO] |
|---|---|
| 2 | Datos adicionales para Empresas Promovidas. Deberá indicarse el identificador de proyecto en el campo 1 (c1). RG 3056/2011 |
| 3 | Datos adicionales para Proveedores de Internet. [NO HABILITADO - RESERVADO PARA USO FUTURO] |
| 10 | Datos adicionales para Educación pública de gestión privada. Deberá indicarse si está (1) o no (0) alcanzado por la norma en el campo 1 (c1). RG 3749/2015 |
| 11 | Datos adicionales para Bienes Inmuebles. Deberá indicarse si está (1) o no (0) alcanzado por la norma en el campo 1 (c1). RG 3749/2015 |
| 12 | Datos adicionales para Loc. Temp. Inmuebles Turísticos. Deberá indicarse si está (1) o no (0) alcanzado por la norma en el campo 1 (c1). RG 3749/2015 |
| 13 | Datos adicionales para Representantes de Modelos. Deberá indicarse si está (1) o no (0) alcanzado por la norma en el campo 1 (c1). RG 3779/2015 |
| 14 | Datos adicionales para Agencias de Publicidad. Deberá indicarse si está (1) o no (0) alcanzado por la norma en el campo 1 (c1). RG 3779/2015 |
| 15 | Datos adicionales para P.F. que Desarrollan Actividades de Modelaje. Deberá indicarse si está (1) o no (0) alcanzado por la norma en el campo 1 (c1). RG 3779/2015 |
| 21 | Datos adicionales para Factura Electrónica de Crédito MiPyME. CBU y Alias del Emisor. Obligatorio para Factura. Deberá indicarse el CBU en el campo 1 (c1). Puede indicarse el Alias en el campo 2 (c2) |
| 22 | Datos adicionales para Factura Electrónica de Crédito MiPyME. Anulación. Obligatorio para Nota de Débito o Nota de Crédito. Indica si el comprobante que se está solicitando la autorización es para anular un comprobante de Factura Electrónica de Crédito Rechazada. Deberá indicarse "S" o "N" en el campo 1 (c1) |
| 23 | Datos adicionales para Factura Electrónica de Crédito MiPyME. Referencia Comercial. Podrá ser utilizado para informar una referencia al receptor del comprobante en el campo 1 (c1) |


## Detalle de Artículos

Ver [RG3188/11](http://biblioteca.afip.gob.ar/afipres/RG_3188_AFIP_A1_V000.pdf)

Los importes correspondientes a descuentos, bonificaciones, contenidos en los documentos emitidos, sólo deberán ser informados como "Total de Descuento Global Diario".

Las notas de crédito que correspondan exclusivamente a descuentos y/o bonificaciones, así como las notas de débito que reviertan tales conceptos, deberán ser informadas incluyendo el respectivo código genérico y sin información del importe documentado".


Datos a suministrar en la solicitud de autorización de emisión de comprobantes electrónicos originales:

 1. Codificación del producto (cod_mtx): los códigos a consignar corresponderán a la estructura provista por la Asociación Argentina de Codificación de Productos Comerciales -código-, denominados códigos GTIN 8, GTIN 12 y GTIN 13, así como los que los modifiquen y/o complementen en el futuro, correspondientes a la unidad de consumo minorista o presentación al consumidor final. El precio unitario asociado a los códigos precitados siempre deberá ser mayor a cero.
 2. Unidad de referencia (u_mtx): cuando la comercialización de los productos se realice en presentaciones distintas a la unidad de consumo minorista o presentación al consumidor final, a la que hace referencia la codificación del producto mencionado en el punto anterior (vg. caja, bulto, "pack", etc.), en el campo "unidad de referencia" se deberá indicar la cantidad de unidades de consumo minorista contenidas en la presentación que se comercializa. En caso de que el producto ya se encuentre individualizado en su unidad de consumo minorista, tanto en el código como en el precio y unidad de medida, la unidad de referencia deberá ser igual a uno.
 3. Códigos genéricos (cod_mtx): cuando corresponda emitir comprobantes incluyendo conceptos distintos a los productos que conforman la operatoria comercial principal del contribuyente, deberán utilizarse los códigos de operación consignados en el apartado B del presente anexo. En el caso de entrega de material promocional y/o muestras se deberá informar el código genérico correspondiente a “ventas varias” previsto en el citado apartado.
 4. Códigos específicos (cod_mtx): cuando esta Administración Federal incorpore a contribuyentes -conforme el procedimiento previsto en el Artículo 2 de la presente– cuya actividad amerite la asignación de códigos específicos para reflejar la comercialización y/o prestación de servicios, deberán utilizarse los códigos que se indican en el apartado C.

### Códigos Genéricos

| Código | Descripción |
|---|---|
| 7790001001030 | Descuentos y bonificaciones comerciales |
| 7790001001047 | Conceptos financieros |
| 7790001001054 | Ventas varias |
| 7790001001061 | Bienes de uso |
| 7790001001078 | Servicios prestados |
| 7790001001085 | Fletes |
| 7790001001092 | Alquileres |
| 7790001001115 | Depósito y servicios de logística |
| 7790001001122 | Repuestos y accesorios |
| 7790001001139 | Ajustes impositivos |
| 7790001001146 | Actividades comerciales no codificadas |
| 7790001001153 | Venta de material de rezago |

### Aclaraciones

Cálculo de importes (detalle de artículos) y validaciones:

- imp_iva: Para tipo_cbte igual a 1, 2 ó 3 (A) y umed distinto a 97 o 99, deberá ser igual a (precio * qty - bonif) * alícuota de IVA (según iva_id correspondiente).
- imp_subtotal: Si tipo_cbte es igual a 1, 2 ó 3 (A) y umed es distinto a 99 ó 97; deberá ser igual a ((precio sin IVA * qty)- bonif)*(1+alícuota). Si tipo_cbte es igual a 6, 7 u 8 (B) y umed es distinto a 99 ó 97; deberá ser igual a (precio con IVA * qty - bonif).

Para los productos sin cargo estableciendo imp_subtotal, precio e imp_iva en 0.

Cálculo de importes generales:

- imp_neto: si tipo_cbte es igual a 1, 2 ó 3 (A): deberá ser igual a la sumatoria de imp_subtotal menos imp_iva para la totalidad de los ítems con iva_id igual a 3, 4, 5 ó 6. Si tipo_cbte es igual a 6, 7 u 8 (B): deberá ser igual a la sumatoria de imp_subtotal menos el IVA correspondiente (calculado en base al importe y la alícuota de cada ítem), para la totalidad de los ítems con iva_id igual a 3, 4, 5 ó 6.
- imp_tot_conc: deberá coincidir con la sumatoria de imp_subtotal para los ítems con iva_id = 1.
- imp_op_ex: deberá coincidir con la sumatoria de imp_subtotal para los ítems con iva_id = 2.
- imp_subtotal: deberá coincidir con la sumatoria de los campos imp_tot_conc + imp_neto + imp_op_ex.
- imp_trib: debe ser igual a la sumatoria de la totalidad de los campos importe de tributos (método !AgregarTributo)
- imp_total: debe ser igual a imp_subtotal + imp_trib + sumatoria de importe liquidado para los subtotales por alícuotas de IVA (método AgregarIVA)

Margen de error: 
  Error relativo porcentual deberá ser <= 0.01% o el error absoluto <=0.01

Mapeo de Campos (con documentación AFIP):

- Generales: imp_subtotal: importeSubtotal, imp_tot_conc: importeNoGravado, imp_neto: importeGravado, imp_op_ex: importeExento, imp_trib: importeOtrosTributos, imp_total: importeTotal
- Detalle: imp_subtotal: importeItem, imp_iva: importeIVA, iva_id: codigoCondicionIVA

## Novedades

Se recuerda que esta disponible el 
[grupo de noticias](http://www.pyafipws.com.ar) (http://groups.google.com.ar/group/pyafipws) donde
se publicarán futuras novedades sobre PyAfipWS: servicios web de
factura electrónica y sus interfases (se recomienda suscribirse)

## Costos y Condiciones

Como este servicio web tiene varias modalidades (CAE normal y CAE anticipado), entre otros cambios, se recomienda consultar previamente.

(ver [Condiciones del Soporte Comercial](wiki:PyAfipWs#CostosyCondiciones)).

Ofrecemos soporte técnico comercial (pago), independiente a la AFIP, desarrollos especiales, interfaces web, etc. 
Obtenga mas información enviando un mail a info@pyafipws.com.ar o (011) 4450-0716 / (011) 15-3048-9211 (asesoramiento sin cargo)

A su vez, se liberará el código fuente bajo licencia GPLv3 (software libre), al igual que se hizo con el restos de los servicios web. Para más detalles ver página FacturaElectronica.

La información de esta página es proporcionada a titulo informativo.

2008-2010 © MarianoReingart
MarianoReingart
MarianoReingart
MarianoReingart
MarianoReingart
MarianoReingart