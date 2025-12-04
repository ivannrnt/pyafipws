# Bonos Fiscales Electrónicos - Bienes de Capital (RG2557)
[[TracNav(noreorder|FacturaElectronica)]]

Interfaz paraServicio Web correspondiente a Factura Electrónica de la actividad: *Fabricación de bienes de capital, informática y telecomunicaciones en un establecimiento industrial radicado en el país por parte de sujetos que utilicen bonos fiscales en el pago de impuestos nacionales* (RG 2557)
[RG4367/ 2018](http://www.afip.gov.ar/noticias/20181220-regimenFacturaCreditoElectronica.asp): [Factura de Crédito Electrónica MiPymes](wiki:BonosFiscales#Estado). [RG4540/2019](https://www.boletinoficial.gob.ar/detalleAviso/primera/212546/20190801) Condiciones de Emisión de notas de crédito y/o débito.

## Índice
[[Image(htdocs:logo-pyafipws.png, align=right)]]
[[TOC(noheading,inline,depth=2)]]
## Descripción General

EL WSBFE (Web Service de Bonos Fiscales Electrónicos) es un nuevo Servicio Web de la AFIP para 
Facturas Electrónicas de Bienes de Capital, correspondiente al Artículo 3 de la 
Resolución General 2557/2009, próxima a entrar en vigencia (Junio de 2009):

> "Transcurridos NOVENTA (90) días corridos contados a partir de la
> fecha de entrada en vigencia de la presente resolución general, el
> mencionado intercambio de información se realizará exclusivamente
> incorporando el detalle de la mercadería comprendida en la operación.
> A tal fin, las especificaciones técnicas respectivas serán publicadas
> en el sitio “web” de este Organismo (http://www.afip.gob.ar)"

## Estado

El servicio WSBFE ya esta en etapa Producción.

Entró en operaciones en Julio de 2009.

Existe una versión actualizada (WSBFEv1), que tiene prácticamente las mismas características, y también es soportada por esta interfaz.


### RG4367/2018 - Ley 27.440

Se incorpora comprobantes *Factura de Crédito Electrónica* en conformidad con la  Ley 27.440 MiPyMEs (RG4367/2018)

AFIP publicó una nueva versión [Especificación Técnica "v2.2 Beta1"](https://www.afip.gob.ar/facturadecreditoelectronica/documentos/WSBFEV1-ManualParaElDesarrollador-V2-3.pdf) (manual para desarrolladores) con fecha 28 de Diciembre de 2018 AFIP, con las siguientes novedades:

- Nuevos comprobantes:

   - 201: Factura de Crédito Electrónica MiPyMEs (FCE) A
   - 202: Nota de Débito Electrónica MiPyMEs (FCE) A
   - 203: Nota de Crédito Electrónica MiPyMEs (FCE) A
   - 206: Factura de Crédito Electrónica MiPyMEs (FCE) B
   - 207: Nota de Débito Electrónica MiPyMEs (FCE) B
   - 208: Nota de Crédito Electrónica MiPyMEs (FCE) B
   - 211: Factura de Crédito Electrónica MiPyMEs (FCE) C
   - 212: Nota de Débito Electrónica MiPyMEs (FCE) C
   - 213: Nota de Crédito Electrónica MiPyMEs (FCE) C

- Se agrega campo `fecha_venc_pago` en método `CrearFactura` 
- Se agrega campo `fecha` y `CUIT` en `AgregarCbteAsoc` 
- Se agregan nuevas validaciones de AFIP

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


Aplicación:  Obligatorio para webservice a partir del 15 de Abril de 2025. (Prorrogado 1 de Julio 2025)

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

Adicionalmente, borrar la carpeta cache donde se encuentran descargada la descripción del servicio web (WSDL), por si esta desactualizada.

Eventualmente utilizar el siguiente instalador para actualizar la carpeta cache:

https://www.sistemasagiles.com.ar/soft/pyafipws/final/PyAfipWS-Cache-UPDATE-2025.4.6.exe


## Descargas

- Instalador: 
- [PyAfipWs-2.7.2171-32bit+wsaa_2.11c+wsbfev1_1.07a-homo.exe](https://www.sistemasagiles.com.ar/soft/pyafipws/PyAfipWs-2.7.2171-32bit+wsaa_2.11c+wsbfev1_1.07a-homo.exe) para evaluación (WSBFEv2.3 Mayo 2019, incluyendo FCE Facturas de Crédito Electrónicas MiPyMEs Ley 27.440))
- [instalador-pyafipws-v17.exe](http://pyafipws.googlecode.com/files/instalador-pyafipws-v17.exe) (versión anterior)
- [Manual de Uso](wiki:ManualPyAfipWs): Documentación ([PDF](http://www.sistemasagiles.com.ar/trac/wiki/ManualPyAfipWs?format=pdf))
- Ejemplo en VB: [https://github.com/SistemasAgiles/pyafipws/blob/master/ejemplos/wsbfe/wsbfe.bas]
- Código Fuente (Python): [Hithub de PyAfipWs](https://github.com/reingart/pyafipws/blob/develop/wsbfev1.py)

## Cambios respecto a WSFE

En este nuevo servicio web WSBFE, además de los campos requeridos por el WSFE para autorizar una factura (obtener el CAE), se debe informar:

- Moneda (según tabla de parámetros) y cotización de la factura
- Impuestos:
- Impuestos internos
- Percepciones 
- II.BB.
- Percepciones municipales
- Zona (según tabla de parámetros) - Por el momento 0 (constante)
- Detallar cada artículo vendido:
- Código según el Nomenclador Común del Mercosur (NCM)
- Descripción completa
- Precio Neto Unitario
- Cantidad 
- Unidad de medida (según tabla de parámetros)
- Bonificación
- Alícuota de IVA (según tabla de parámetros)
- Importe total

La operatoria es bastante similar al método de autorización del WSFE (con un ID secuencial, observaciones, reproceso, etc.), teniendo en cuenta esta mayor complejidad por tener que informar el detalle de cada item.

A su vez, el WSBFE devuelve mensajes de eventos (mantenimiento programado, advertencias, etc.), los que deben ser capturados e informados al usuario.

Para mayor información, se puede consultar la documentación orignal en [Manual del WSBFE - AFIP](http://wswhomo.afip.gov.ar/fiscaldocs/WSBFE/WSBFE-ManualParaElDesarrollador.pdf) o el [manual](http://www.nsis.com.ar/soft/pyafipws/manual-wsbfe-beta.pdf) manual de la presente interfaz. 

## Ejemplo Intefase COM en VB (5/6)
El siguiente es un extracto del ejemplo completo para crear una factura electrónica para bienes de capital.
Ver el detalle de la interfaz en el manual o descargar el ejemplo (Ver [BonosFiscales#Descargas]).
```
#!vb
' Creo una factura (internamente, no se llama al WebService):
ok = WSBFE.CrearFactura(tipo_doc, nro_doc, _
            zona, tipo_cbte, punto_vta, cbte_nro, fecha_cbte, _
            imp_total, imp_neto, impto_liq, _
            imp_tot_conc, impto_liq_rni, imp_op_ex, _
            imp_perc, imp_iibb, imp_perc_mun, imp_internos, _
            imp_moneda_id, Imp_moneda_ctz, fecha_venc_pago, cancela_misma_moneda_ext, condicion_iva_receptor_id)

' Agrego los items:
ok = WSBFE.AgregarItem(ncm, sec, ds, qty, umed, precio, bonif, iva_id, imp_total)

' Llamo al WebService de Autorización para obtener el CAE
cae = WSBFE.Authorize(id)
```

## Tablas de Parámetros

A diferencia del WSFE, este nuevo servicio funciona con tablas dinámicas de parámetros para los códigos de comprobante, moneda, alícuotas de iva, producto según NCM, zonas, unidades de medida.
Estas tablas pueden sufrir modificaciones realizadas por la AFIP, con altas y bajas lógicas, por lo que tienen una fecha de vigencia (desde, hasta) y se proveen métodos para consultarlas por el mismo servicio web (a diferencia del WSFE, que las tablas eran documentadas estaticamentes en el sitio web).

A continuación se detallan:

### Comprobantes
| **Id** | **Descripción** |
|---|---|
| 1 | Factura A |
| 2 | Nota de Débito A |
| 3 | Nota de Crédito A |
| 4 | Recibo A |
| 6 | Factura B |
| 7 | Nota de Débito B |
| 8 | Nota de Crédito B |
| 9 | Recibo B |
| 11 | Factura C |
| 12 | Nota de Débito C |
| 13 | Nota de Crédito C |
| 15 | Recibo C |
| 51 | Factura M |
| 52 | Nota de Débito M |
| 53 | Nota de Crédito M |
| 54 | Recibo M |
| 201 | Factura de Crédito electrónica MiPyMEs (FCE) A |
| 202 | Nota de Débito electrónica MiPyMEs (FCE) A |
||203||Nota de Crédito electrónica MiPyMEs (FCE) A|
| 206 | Factura de Crédito electrónica MiPyMEs (FCE) B |
|---|---|
| 207 | Nota de Débito electrónica MiPyMEs (FCE) B |
| 208 | Nota de Crédito electrónica MiPyMEs (FCE) B |
| 211 | Factura de Crédito electrónica MiPyMEs (FCE) C |
| 212 | Nota de Débito electrónica MiPyMEs (FCE) C |
| 213 | Nota de Crédito electrónica MiPyMEs (FCE) C |

### Monedas
| **Id** | **Descripción** |
|---|---|
| DOL | Dólar Estadounidense |
| PES | Pesos Argentinos |
| 010 | Pesos Mejicanos |
| 011 | Pesos Uruguayos |
| 012 | Real |
| 014 | Coronas Danesas |
| 015 | Coronas Noruegas |
| 016 | Coronas Suecas |
| 019 | Yens |
| 032 | Peso Colombiano |
| 033 | Peso Chileno |
| 056 | Forint (Hungría) |
| 057 | Baht (Tailandia) |
| 036 | Sucre Ecuatoriano |
| 051 | Dólar de Hong Kong |
| 052 | Dólar de Singapur |
| 053 | Dólar de Jamaica |
| 031 | Peso Boliviano |
| 029 | Güaraní |
| 028 | Florín (Antillas Holandesas) |
| 034 | Rand Sudafricano |
| 035 | Nuevo Sol Peruano |
| 061 | Zloty Polaco |
| 060 | Euro |
| 063 | Lempira Hondureña |
| 062 | Rupia Hindú |
| 064 | Yuan (Rep. Pop. China) |
| 018 | Dólar Canadiense |
| 025 | Dinar Yugoslavo |
| 002 | Dólar Libre EEUU |
| 027 | Dracma Griego |
| 026 | Dólar Australiano |
| 007 | Florines Holandeses |
| 023 | Bolívar Venezolano |
| 047 | Riyal Saudita |
| 046 | Libra Egipcia |
| 045 | Dirham Marroquí |
| 044 | Córdoba Nicaragüense |
| 043 | Balboas Panameñas |
| 042 | Peso Dominicano |
| 054 | Dólar de Taiwan |
| 040 | Lei Rumano |
| 024 | Corona Checa |
| 030 | Shekel (Israel) |
| 021 | Libra Esterlina |
| 055 | Quetzal Guatemalteco |
| 059 | Dinar Kuwaiti |

### Alícuotas de IVA
| **Id** | **Descripción** |
|---|---|
| 1 | No gravado |
| 2 | Exento |
| 3 | 0% |
| 4 | 10.5% |
| 5 | 21% |
| 6 | 27% |

### Unidades de Medida
| **Id** | **Descripción** |
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
| 97 | hormas |
| 98 | bonificaciòn |
| 99 | otras unidades |

### NCM: Nomenclador Común del Mercosur (productos)

El NCM debe ser usado para identificar los productos. 
Si el código no se encuentra en esta tabla, no puede emitirse factura electronica para bono fiscal.

Actualmente hay 3125 (no todos los códigos del nomenclador se encuentran habilitados).
Por simplicidad, se listan los primeros 10.

| **Código** | **Descripción** |
|---|---|
| 84.57.10.00 | NULL |
| 0705.11.00 | NULL |
| 8480.60.00 | NULL |
| 2104.10.19 | NULL |
| 8519.31.00 | NULL |
| 2104.10.11 | NULL |
| 84.07.29.90 | NULL |
| 84.76.29.00 | NULL |
| 9302.00.00 | NULL |
| 4202.22.10 | NULL |
| 84.67.29.93 | NULL |


### Zonas
Por el momento no se utiliza. Usar constante 0.

## Novedades

Se recuerda que esta disponible el 
[grupo de noticias](http://www.pyafipws.com.ar) (http://groups.google.com.ar/group/pyafipws) donde
se publicarán futuras novedades sobre PyAfipWS: servicios web de
factura electrónica y sus interfases (se recomienda suscribirse)

## Costos y Condiciones

Ver [Condiciones del Soporte Comercial](wiki:PyAfipWs#CostosyCondiciones).

A su vez, se libera el código fuente bajo licencia GPL (software libre), al igual que se hizo con el restos de los servicios web. Para más detalles ver página FacturaElectronica.

MarianoReingart
