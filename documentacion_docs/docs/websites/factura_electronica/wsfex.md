# Factura Electrónica de Exportación (RG2758/2010 y RG3689/14 -> RG4401/19)
[[TracNav(noreorder|FacturaElectronica)]]

Interfaz para Servicio Web correspondiente a Factura Electrónica de Exportación para *los exportadores responsables inscriptos en el IVA y en los "Registros Especiales Aduaneros" previstos en el Título II de la RG 2570/09* (Resolución General 2758/2010). Régimen especial de emisión y almacenamiento electrónico de comprobantes originales que respalden operaciones de exportación de servicios (Resolución General 3689/2014 y su sustitución por Resolución General 4401/2019)

## Índice
[[Image(htdocs:logo-pyafipws.png, align=right)]]
[[TOC(noheading,inline,depth=3)]]
## Descripción General

### RG2758/10

EL WSFEX (Web Service de Factura Electrónica de Exportación) es un nuevo Servicio Web de la AFIP para el 
Régimen especial de emisión y almacenamiento electrónico de comprobantes originales (RG2485), correspondiente al Artículo 4 inciso A de la 
[Resolución General 2758/2010](http://biblioteca.afip.gob.ar/gateway.dll/Normas/ResolucionesGenerales/reag01002758_2010_01_20.xml), entrar en vigencia:

- Sujetos incluidos en las disposiciones de la RG 596 y su modificatoria: 1 de marzo de 2010.
- Demás responsables: 1 de mayo de 2010.

### RG3689/14

Desde el día 1 de febrero de 2015 los sujetos que realicen prestaciones de servicios en el país cuya utilización o explotación efectiva se lleve a cabo en el exterior —exportación de servicios—  deberán emitir comprobantes electrónicos originales. Comprobantes alcanzados:

- Facturas de exportación clase “E”.
- Notas de crédito y notas de débito clase “E”.

La parte técnica no cambia, el intercambio de información sigue siendo "RG 2758 Diseño de Registro XML V.1" (o sea, WSFEXv1), pero aparentemente se debe empadronar por el servicio de clave fiscal, llendo a:

- Regimenes de facturación y registración (REAR/RECE/RFI)
- Empadronamiento REAR/RECE
- Regimenes de Facturación
- RUBRO I. C) RECE (FACTURA ELECTRÓNICA Y FACTURA ELECTRÓNICA EN LINEA
- Factura Electronica - Exportacion de Servicios
- Webservice/Facturador Plus

### RG4401/2019

Sustitución RG3689/14 y modificaciones.

- Obligatoriedad de consignar información correspondiente de comprobante asociado cuando se emitan Notas de Crédito y/o Débito.
- El tipo de cambio aplicable a las notas de crédito y/o débito será el correspondiente al comprobante asociado que se está ajustando.

Nuevos métodos y parámetros WSFEX version 1.5.0:

- Se agrega método [WSFEXv1.GetParamMonConCotizacion](wiki:ManualPyAfipWs#M%C3%A9todos3) y ejemplo [RECEX1 /monctz](wiki:ManualPyAfipWs#EjemploRECEX1consultamonedasconcotización) para consultar cotización moneda ADUANA por fecha

Errores frecuentes:

- Err: 2053: Cotizacion informada no valida. (FechaCot utilizada: 30/01/2019 - CotAduana: 37.51 para este caso)

### RG5264/2022

AFIP publicó una nueva [Especificación Técnica "FEXv2.0.0"](https://www.afip.gob.ar/ws/manuales-provisorios/documentos/WSFEX-Manualparaeldesarrollador-V2-0.pdf) (manual para desarrolladores)

Se incorpora método para la consulta de Actividades vigentes (GetParamActividades) y una estructura de actividades vinculadas al comprobante tanto en la
emisión de CAE, como en la consulta de los comprobantes ya autorizados.

ver: [Métodos WSFEXv1](wiki:ManualPyAfipWs#M%C3%A9todos3) 

Aplicación:

Resultará de aplicación **optativa** a partir del 01 de Febrero de 2023 y **obligatoria** desde el 01 de Marzo de 2023, posterior a esta fecha, los comprobantes serán rechazados si la actividad es Harina.

*Nota:* Al momento de confeccionar el correspondiente comprobante electrónico, que se emita para respaldar las operaciones de venta de harinas y/o subproductos derivados de la molienda de trigo se deberá seleccionar la actividad por la cual se está realizando el mismo, con el objeto de identificar el o los “REC” emitidos.

### RG5616/2024 FEv4

ARCA estableció nuevos criterios de Facturación para las operaciones realizadas en moneda extranjera.

Ver["Resolución 5616/24"](https://www.boletinoficial.gob.ar/detalleAviso/primera/318374/20241218)

- Se afregan nuevos campos al método `CrearFactura(...)`:

                            - `cancela_misma_moneda_ext`

- Nuevos Metodos auxiliares:

                            - `ParamGetCotizacion(moneda_id, fecha)`: se agrega fecha de cotizacion

Se agregan nuevas validaciones.


Aplicación:  Obligatorio para webservice a partir del 15 de Abril de 2025. (Prorrogado 1 de Julio 2025)



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

Ejemplo completo para VB: https://www.sistemasagiles.com.ar/trac/attachment/wiki/FacturaElectronicaExportacion/wsfexv1_canmismon.txt

Adicionalmente, borrar la carpeta cache donde se encuentran descargada la descripcion del servicio web (WSDL), por si esta desactuializada.

Eventualmente utilizar el siguiente instalador para actualizar la carpeta cache:

https://www.sistemasagiles.com.ar/soft/pyafipws/final/PyAfipWS-Cache-UPDATE-2025.4.6.exe
## Estado

**Importante**: Según [RG3066/11](http://biblioteca.afip.gob.ar/gateway.dll/Normas/ResolucionesGenerales/reag01003066_2011_03_18.xml) (Anexo II) AFIP publicó una nueva versión del webservice: [WSFEXv1](http://www.afip.gov.ar/fe/documentos/WSFEX-Manualparaeldesarrollador_V1.pdf) (“RG 2758 Diseño de Registro XML V.1” / “RG 2758 Manual para el Desarrollador V.1”), cuya entrada en vigencia es: 

- **1 de abril de 2011**: optativa
- **31 de diciembre de 2011**: obligatoria (reemplazando al webservice WSFEX version 0 anterior)




## Descargas

- Instalador: [instalador-PyAfipWs-2.7.3290-homo.exe](https://www.sistemasagiles.com.ar/soft/pyafipws/PyAfipWs-2.7.3290-32bit+wsaa_2.13a+wsfexv1_1.12a-homo.exe)
- Ejemplo en VB: [https://github.com/reingart/pyafipws/blob/master/ejemplos/wsfexv1/wsfexv1.bas]
- Ejemplo en MS Acess/VBA: [pyafipws.mdb](http://pyafipws.googlecode.com/files/pyafipws.mdb): WSFEv1 y WSFEX (base de datos MS Access 97 o sup.) 
- [Manual de Uso](wiki:ManualPyAfipWs): Documentación ([PDF](http://www.sistemasagiles.com.ar/trac/wiki/ManualPyAfipWs?format=pdf))
- Código Fuente (Python): ver archivos publicados en [GitHub](https://github.com/reingart/pyafipws/blob/master/wsfexv1.py) 

## Cambios respecto a WSFE

En este nuevo servicio web WSFEX, además de los campos requeridos por el WSFE para autorizar una factura (obtener el CAE), se debe informar:

- Tipo de Exportación: Exportación definitiva de Bienes, Servicios, Otros
- Permiso Existente
- País Destino
- Apellido y nombre, identificación tributaria del comprador
- Moneda (según tabla de parámetros) y cotización de la factura
- Observaciones comerciales 
- Forma de Pago
- Incoterms y su descripción
- Permiso de embarque y destinaciones (código de permiso y país de destino)
- Comprobantes Asociados:
- Tipo de comprobante (incluyendo 88: Remito Electrónico y 89: Resumen de Datos *** Nuevo WSFEXv1! ***)
- Punto de venta 
- Número de comprobante
- CUIT que generó el comprobante (*** Nuevo WSFEXv1! ***)
- Detallar cada artículo vendido (ítems):
- Código del producto (
- Descripción completa
- Precio Neto Unitario
- Cantidad 
- Unidad de medida (según tabla de parámetros, incluyendo 97: Anticipos y 99: Descuentos *** Nuevo WSFEXv1! ***)
- Importe total
- Bonificación (*** Nuevo WSFEXv1! ***)

La operatoria es bastante similar al método de autorización del WSFE (con un ID secuencial, observaciones, reproceso, etc.), teniendo en cuenta esta mayor complejidad por tener que informar el detalle de cada item y las condiciones de exportación.

A su vez, el WSFEX devuelve mensajes de eventos (mantenimiento programado, advertencias, etc.), los que deben ser capturados e informados al usuario.

Para mayor información, se puede consultar la documentación orignal en [Manual del WSFEXv1 - AFIP](http://www.afip.gov.ar/fe/documentos/WSFEX-Manualparaeldesarrollador_V1.pdf) o el [manual](wiki:ManualPyAfipWs) manual de la presente interfaz. 

## Cambios WSFEXv1 respecto a WSFEXv0

La nueva versión V.1 principalmente agrega:

- Nuevas unidades de medidas para Facturas en $0.- y/o Señas / Descuentos
- Bonificación por ítem
- Nuevos tipos de comprobantes para remitos electronicos y Resumen de Datos (ej. Tabaco) y CUIT en comprobantes asociados

Recursos para desarrollo:

- Ejemplo Actualizado: [https://raw.githubusercontent.com/reingart/pyafipws/2.7.1843/ejemplos/wsfexv1/wsfexv1.bas]
- Instalador Preliminar: [instalador-WSFEXV1-1.00a-homo.exe](http://pyafipws.googlecode.com/files/instalador-WSFEXV1-1.00a-homo.exe)
- Instalador Unificado Homologacion: [instalador-PyAfipWs-1.27d-homo.exe](http://pyafipws.googlecode.com/files/instalador-PyAfipWs-1.27d-homo.exe)

Ver [y [wiki:FacturaElectronicaExportacion#TablasdeParámetros Tablas de Parámetros](wiki:FacturaElectronicaExportacion#CambiosRespectoaWSFE]) para mayor información

**Nota**: Por el momento solo soporta los metodos principales (con algunos cambios: bonificaciones y remitos de tabaco, entre otros). 

**Importante**: Esta interfaz se mantiene **compatibilidad hacia atrás** (las aplicaciones anteriores que usen WSFEX simplemente deben instanciar el objeto "WSFEXv1" y ajustar la URL en Conectar)

Cambios de WSFEXv1 según la [Documentación Oficial de AFIP](http://www.afip.gov.ar/fe/documentos/WSFEX-Manualparaeldesarrollador_V1.pdf):

- Se levanta validación sobre los permisos de embarque para que acepte más de 5 permisos en un mismo request.
- A nivel de item, se amplia la cantidad de decimales para precio unitario y cantidad a 6.
- Se cambia el formato de algunos campos por el tratamiento de decimales. El formato pasa de Double a Decimal.
- Se agrega bonificación a nivel de ítem. (6 decimales) 
- Concepto de señas y bonificación general, a nivel del  comprobante.
- Los importes totales del ítem y del comprobante se limitan a 2 decimales.
- Se valida el total del ítem y del comprobante con los márgenes  de error absoluto y relativo indicados en Margen de error mediante (Error Absoluto y Error Relativo) (criterio Round Half Even) a 5 decimales.
- Acepta total del ítem igual a cero, también se permite que el  precio unitario sea 0.
- Se amplía la longitud máxima del campo <Obs_comerciales>  a 4000 caracteres.
- Incoterms, solamente es obligatorio si es una factura (Cbte_Tipo=19) y concepto igual a productos (Tipo_expo=1)
- Permite asociar remitos de tabaco. Esto es solamente para las empresas que exportan tabaco. Se modificó la estructura del array de comprobantes asociados para que pueden informar la CUIT en caso de ser un remito tabaco realizado por un tercero.
- Se reemplaza el nombre del campo Tipo_cbte por Cbte_Tipo.

## Ejemplo Intefase COM en VB (5/6)
```
#!vb
' Creo una factura (internamente, no se llama al WebService):
ok = WSFEX.CrearFactura(tipo_cbte, punto_vta, cbte_nro, fecha_cbte, _
            imp_total, tipo_expo, permiso_existente, dst_cmp, _
            cliente, cuit_pais_cliente, domicilio_cliente, _
            id_impositivo, moneda_id, moneda_ctz, _
            obs_comerciales, obs, forma_pago, incoterms, _
            idioma_cbte, incoterms_ds, fecha_pago, cancela_misma_moneda_ext, condicion_iva_receptor_id)
    
' Agrego un item (internamente, no se llama al WebService):
ok = WSFEX.AgregarItem(codigo, ds, qty, umed, precio, imp_total)

' Agrego un permiso de exportación (ver manual para el desarrollador)
ok = WSFEX.AgregarPermiso(id, dst)
        
' Agrego un comprobante asociado (ver manual para el desarrollador)
ok = WSFEX.AgregarCmpAsoc(tipo_cbte_asoc, punto_vta_asoc, cbte_nro_asoc, cbte_cuit)

' Llamo al WebService de Autorización para obtener el CAE
cae = WSFEX.Authorize(id)
```

## Tablas de Parámetros

A diferencia del WSFE, este nuevo servicio funciona con tablas dinámicas de parámetros para los códigos de comprobante, moneda, paises, tipos de exportación, idiomas, CUIT referenciales de paises, unidades de medida.
Estas tablas pueden sufrir modificaciones realizadas por la AFIP, con altas y bajas lógicas, por lo que tienen una fecha de vigencia (desde, hasta) y se proveen métodos para consultarlas por el mismo servicio web (a diferencia del WSFE, que las tablas eran documentadas estaticamentes en el sitio web).

Ver Planilla [Anexo Tablas referenciales.xls](http://www.sistemasagiles.com.ar/soft/pyafipws/anexo_tablas_referenciales.xls) (puede estar desactualizado respecto los últimos cambios)

Como ejemplo, a continuación se copian los resultados de invocar a los webservices para consultar las tablas de parámetros al 15/06/2010 (homologación):

### Monedas
| PES | Pesos Argentinos |
|---|---|
| DOL | Dólar Estadounidense |
| 002 | Dólar Libre EEUU |
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
| 046 | Libra Egipcia |
| 047 | Riyal Saudita |
| 061 | Zloty Polaco |
| 062 | Rupia Hindú |
| 063 | Lempira Hondureña |
| 064 | Yuan (Rep. Pop. China) |
| 009 | Franco Suizo |
### Tipos Comprobante
| 19 | Facturas de Exportación |
|---|---|
| 20 | Nota de Débito por Operaciones con el Exterior |
| 21 | Nota de Crédito por Operaciones con el Exterior |
| 88 | Remito Electrónico (solo para comprobantes asociados, *** Nuevo WSFEXv1! ***) |
| 89 | Resumen de Datos (solo para comprobantes asociados, *** Nuevo WSFEXv1! ***) |
### Tipos Exportación
| 1 | Exportación definitiva de Bienes |
|---|---|
| 2 | Servicios |
| 4 | Otros |
### Idiomas
| 1 | Español |
|---|---|
| 2 | Inglés |
| 3 | Portugués |
### Unidades de medida
| 41 | miligramos |
|---|---|
| 14 | gramos |
| 1 | kilogramos |
| 29 | toneladas |
| 10 | quilates |
| 47 | mililitros |
| 5 | litros |
| 27 | cm cúbicos |
| 15 | milimetros |
| 20 | centímetros |
| 17 | kilómetros |
| 7 | unidades |
| 8 | pares |
| 9 | docenas |
| 11 | millares |
| 96 | packs |
| 97 | hormas |
| 2 | metros |
| 3 | metros cuadrados |
| 4 | metros cúbicos |
| 6 | 1000 kWh |
| 98 | bonificación |
| 99 | otras unidades |
| 16 | mm cúbicos |
| 18 | hectolitros |
| 25 | jgo. pqt. mazo naipes |
| 30 | dam cúbicos |
| 31 | hm cúbicos |
| 32 | km cúbicos |
| 33 | microgramos |
| 34 | nanogramos |
| 35 | picogramos |
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
| 0 | (*** NUEVO WSFEXv1! *** para descripciones) |
| 97 | seña/anticipo (*** NUEVO WSFEXv1! *** para importes negativo) |
| 98 | otras unidades |
| 99 | bonificación (*** NUEVO WSFEXv1! *** para importes negativo) |
### INCOTERMs
| EXW | EXW |
|---|---|
| FCA | FCA |
| FAS | FAS |
| FOB | FOB |
| CFR | CFR |
| CIF | CIF |
| CPT | CPT |
| CIP | CIP |
| DAF | DAF |
| DES | DES |
| DEQ | DEQ |
| DDU | DDU |
| DDP | DDP |
| DAP | DAP |
| DAT | DAT |
### Pais Destino
| 101 | BURKINA FASO |
|---|---|
| 102 | ARGELIA |
| 103 | BOTSWANA |
| 104 | BURUNDI |
| 105 | CAMERUN |
| 107 | REP. CENTROAFRICANA. |
| 108 | CONGO |
| 109 | REP.DEMOCRAT.DEL CONGO EX ZAIRE |
| 110 | COSTA DE MARFIL |
| 111 | CHAD |
| 112 | BENIN |
| 113 | EGIPTO |
| 115 | GABON |
| 116 | GAMBIA |
| 117 | GHANA |
| 118 | GUINEA |
| 119 | GUINEA ECUATORIAL |
| 120 | KENYA |
| 121 | LESOTHO |
| 122 | LIBERIA |
| 123 | LIBIA |
| 124 | MADAGASCAR |
| 125 | MALAWI |
| 126 | MALI |
| 127 | MARRUECOS |
| 128 | MAURICIO,ISLAS |
| 129 | MAURITANIA |
| 130 | NIGER |
| 131 | NIGERIA |
| 132 | ZIMBABWE |
| 133 | RWANDA |
| 134 | SENEGAL |
| 135 | SIERRA LEONA |
| 136 | SOMALIA |
| 137 | SWAZILANDIA |
| 138 | SUDAN |
| 139 | TANZANIA |
| 140 | TOGO |
| 141 | TUNEZ |
| 142 | UGANDA |
| 144 | ZAMBIA |
| 145 | TERRIT.VINCULADOS AL R UNIDO |
| 146 | TERRIT.VINCULADOS A ESPAÑA |
| 147 | TERRIT.VINCULADOS A FRANCIA |
| 149 | ANGOLA |
| 150 | CABO VERDE |
| 151 | MOZAMBIQUE |
| 152 | SEYCHELLES |
| 153 | DJIBOUTI |
| 155 | COMORAS |
| 156 | GUINEA BISSAU |
| 157 | STO.TOME Y PRINCIPE |
| 158 | NAMIBIA |
| 159 | SUDAFRICA |
| 160 | ERITREA |
| 161 | ETIOPIA |
| 197 | RESTO (AFRICA) |
| 198 | INDETERMINADO (AFRICA) |
| 200 | ARGENTINA |
| 201 | BARBADOS |
| 202 | BOLIVIA |
| 203 | BRASIL |
| 204 | CANADA |
| 205 | COLOMBIA |
| 206 | COSTA RICA |
| 207 | CUBA |
| 208 | CHILE |
| 209 | REPÚBLICA DOMINICANA |
| 210 | ECUADOR |
| 211 | EL SALVADOR |
| 212 | ESTADOS UNIDOS |
| 213 | GUATEMALA |
| 214 | GUYANA |
| 215 | HAITI |
| 216 | HONDURAS |
| 217 | JAMAICA |
| 218 | MEXICO |
| 219 | NICARAGUA |
| 220 | PANAMA |
| 221 | PARAGUAY |
| 222 | PERU |
| 223 | PUERTO RICO |
| 224 | TRINIDAD Y TOBAGO |
| 225 | URUGUAY |
| 226 | VENEZUELA |
| 227 | TERRIT.VINCULADO AL R.UNIDO |
| 228 | TER.VINCULADOS A DINAMARCA |
| 229 | TERRIT.VINCULADOS A FRANCIA AMERIC. |
| 230 | TERRIT. HOLANDESES |
| 231 | TER.VINCULADOS A ESTADOS UNIDOS |
| 232 | SURINAME |
| 233 | DOMINICA |
| 234 | SANTA LUCIA |
| 235 | SAN VICENTE Y LAS GRANADINAS |
| 236 | BELICE |
| 237 | ANTIGUA Y BARBUDA |
| 238 | S.CRISTOBAL Y NEVIS |
| 239 | BAHAMAS |
| 240 | GRENADA |
| 241 | ANTILLAS HOLANDESAS |
| 250 | AAE Tierra del Fuego - ARGENTINA |
| 251 | ZF La Plata - ARGENTINA |
| 252 | ZF Justo Daract - ARGENTINA |
| 253 | ZF Río Gallegos - ARGENTINA |
| 254 | Islas Malvinas - ARGENTINA |
| 255 | ZF Tucumán - ARGENTINA |
| 256 | ZF Córdoba - ARGENTINA |
| 257 | ZF Mendoza - ARGENTINA |
| 258 | ZF General Pico - ARGENTINA |
| 259 | ZF Comodoro Rivadavia - ARGENTINA |
| 260 | ZF Iquique |
| 261 | ZF Punta Arenas |
| 262 | ZF Salta - ARGENTINA |
| 263 | ZF Paso de los Libres - ARGENTINA |
| 264 | ZF Puerto Iguazú - ARGENTINA |
| 265 | SECTOR ANTARTICO ARG. |
| 270 | ZF Colón - REPÚBLICA DE PANAMÁ |
| 271 | ZF Winner (Sta. C. de la Sierra) - BOLIVIA |
| 280 | ZF Colonia - URUGUAY |
| 281 | ZF Florida - URUGUAY |
| 282 | ZF Libertad - URUGUAY |
| 283 | ZF Zonamerica - URUGUAY |
| 284 | ZF Nueva Helvecia - URUGUAY |
| 285 | ZF Nueva Palmira - URUGUAY |
| 286 | ZF Río Negro - URUGUAY |
| 287 | ZF Rivera - URUGUAY |
| 288 | ZF San José - URUGUAY |
| 291 | ZF Manaos - BRASIL |
| 295 | MAR ARG ZONA ECO.EX |
| 296 | RIOS ARG NAVEG INTER |
| 297 | RESTO AMERICA |
| 298 | INDETERMINADO (AMERICA) |
| 301 | AFGANISTAN |
| 302 | ARABIA SAUDITA |
| 303 | BAHREIN |
| 304 | MYANMAR (EX-BIRMANIA) |
| 305 | BUTAN |
| 306 | CAMBODYA (EX-KAMPUCHE) |
| 307 | SRI LANKA |
| 308 | COREA DEMOCRATICA |
| 309 | COREA REPUBLICANA |
| 310 | CHINA |
| 312 | FILIPINAS |
| 313 | TAIWAN |
| 315 | INDIA |
| 316 | INDONESIA |
| 317 | IRAK |
| 318 | IRAN |
| 319 | ISRAEL |
| 320 | JAPON |
| 321 | JORDANIA |
| 322 | QATAR |
| 323 | KUWAIT |
| 324 | LAOS |
| 325 | LIBANO |
| 326 | MALASIA |
| 327 | MALDIVAS ISLAS |
| 328 | OMAN |
| 329 | MONGOLIA |
| 330 | NEPAL |
| 331 | EMIRATOS ARABES UNIDOS |
| 332 | PAKISTÁN |
| 333 | SINGAPUR |
| 334 | SIRIA |
| 335 | THAILANDIA |
| 337 | VIETNAM |
| 341 | HONG KONG |
| 344 | MACAO |
| 345 | BANGLADESH |
| 346 | BRUNEI |
| 348 | REPUBLICA DE YEMEN |
| 349 | ARMENIA |
| 350 | AZERBAIJAN |
| 351 | GEORGIA |
| 352 | KAZAJSTAN |
| 353 | KIRGUIZISTAN |
| 354 | TAYIKISTAN |
| 355 | TURKMENISTAN |
| 356 | UZBEKISTAN |
| 357 | TERR. AU. PALESTINOS |
| 397 | RESTO DE ASIA |
| 398 | INDET.(ASIA) |
| 401 | ALBANIA |
| 404 | ANDORRA |
| 405 | AUSTRIA |
| 406 | BELGICA |
| 407 | BULGARIA |
| 409 | DINAMARCA |
| 410 | ESPAÑA |
| 411 | FINLANDIA |
| 412 | FRANCIA |
| 413 | GRECIA |
| 414 | HUNGRIA |
| 415 | IRLANDA |
| 416 | ISLANDIA |
| 417 | ITALIA |
| 418 | LIECHTENSTEIN |
| 419 | LUXEMBURGO |
| 420 | MALTA |
| 421 | MONACO |
| 422 | NORUEGA |
| 423 | PAISES BAJOS |
| 424 | POLONIA |
| 425 | PORTUGAL |
| 426 | REINO UNIDO |
| 427 | RUMANIA |
| 428 | SAN MARINO |
| 429 | SUECIA |
| 430 | SUIZA |
| 431 | VATICANO(SANTA SEDE) |
| 433 | POS.BRIT.(EUROPA) |
| 435 | CHIPRE |
| 436 | TURQUIA |
| 438 | ALEMANIA,REP.FED. |
| 439 | BIELORRUSIA |
| 440 | ESTONIA |
| 441 | LETONIA |
| 442 | LITUANIA |
| 443 | MOLDAVIA |
| 444 | RUSIA |
| 445 | UCRANIA |
| 446 | BOSNIA HERZEGOVINA |
| 447 | CROACIA |
| 448 | ESLOVAQUIA |
| 449 | ESLOVENIA |
| 450 | MACEDONIA |
| 451 | REP. CHECA |
| 453 | MONTENEGRO |
| 454 | SERBIA |
| 497 | RESTO EUROPA |
| 498 | INDET.(EUROPA) |
| 501 | AUSTRALIA |
| 503 | NAURU |
| 504 | NUEVA ZELANDIA |
| 505 | VANATU |
| 506 | SAMOA OCCIDENTAL |
| 507 | TERRITORIO VINCULADOS A AUSTRALIA |
| 508 | TERRITORIOS VINCULADOS AL R. UNIDO |
| 509 | TERRITORIOS VINCULADOS A FRANCIA |
| 510 | TER VINCULADOS A NUEVA. ZELANDA |
| 511 | TER. VINCULADOS A ESTADOS UNIDOS |
| 512 | FIJI, ISLAS |
| 513 | PAPUA NUEVA GUINEA |
| 514 | KIRIBATI, ISLAS |
| 515 | MICRONESIA,EST.FEDER |
| 516 | PALAU |
| 517 | TUVALU |
| 518 | SALOMON,ISLAS |
| 519 | TONGA |
| 520 | MARSHALL,ISLAS |
| 521 | MARIANAS,ISLAS |
| 597 | RESTO OCEANIA |
| 598 | INDET.(OCEANIA) |
| 997 | RESTO CONTINENTE |
| 998 | INDET.(CONTINENTE) |
### CUIT Pais Destino
| 50000000016 | URUGUAY - Persona Física |
|---|---|
| 50000000024 | PARAGUAY - Persona Física |
| 50000000032 | CHILE - Persona Física |
| 50000000040 | BOLIVIA - Persona Física |
| 50000000059 | BRASIL - Persona Física |
| 50000001012 | BURKINA FASO - Persona Física |
| 50000001020 | ARGELIA - Persona Física |
| 50000001039 | BOTSWANA - Persona Física |
| 50000001047 | BURUNDI - Persona Física |
| 50000001055 | CAMERUN - Persona Física |
| 50000001071 | CENTRO AFRICANO, REP. - Persona Física |
| 50000001101 | COSTA DE MARFIL - Persona Física |
| 50000001136 | EGIPTO - Persona Física |
| 50000001144 | ETIOPIA - Persona Física |
| 50000001152 | GABON - Persona Física |
| 50000001160 | GAMBIA - Persona Física |
| 50000001179 | GHANA - Persona Física |
| 50000001187 | GUINEA - Persona Física |
| 50000001195 | GUINEA ECUATORIAL - Persona Física |
| 50000001209 | KENIA - Persona Física |
| 50000001217 | LESOTHO - Persona Física |
| 50000001225 | REPUBLICA DE LIBERIA (Estado independiente) - Persona Física |
| 50000001233 | LIBIA - Persona Física |
| 50000001241 | MADAGASCAR - Persona Física |
| 50000001276 | MARRUECOS - Persona Física |
| 50000001284 | REPUBLICA DE MAURICIO - Persona Física |
| 50000001292 | MAURITANIA - Persona Física |
| 50000001306 | NIGER - Persona Física |
| 50000001314 | NIGERIA - Persona Física |
| 50000001322 | ZIMBABWE - Persona Física |
| 50000001330 | RUANDA - Persona Física |
| 50000001349 | SENEGAL - Persona Física |
| 50000001357 | SIERRA LEONA - Persona Física |
| 50000001365 | SOMALIA - Persona Física |
| 50000001373 | REINO DE SWAZILANDIA (Estado independiente) - Persona Física |
| 50000001381 | SUDAN - Persona Física |
| 50000001403 | TOGO - Persona Física |
| 50000001411 | REPUBLICA TUNECINA - Persona Física |
| 50000001446 | ZAMBIA - Persona Física |
| 50000001454 | POS.BRITANICA (AFRICA) - Persona Física |
| 50000001462 | POS.ESPAÑOLA (AFRICA) - Persona Física |
| 50000001470 | POS.FRANCESA (AFRICA) - Persona Física |
| 50000001489 | POS.PORTUGUESA (AFRICA) - Persona Física |
| 50000001497 | REPUBLICA DE ANGOLA - Persona Física |
| 50000001500 | REPUBLICA DE CABO VERDE (Estado independiente) - Persona Física |
| 50000001519 | MOZAMBIQUE - Persona Física |
| 50000001527 | CONGO REP.POPULAR - Persona Física |
| 50000001535 | CHAD - Persona Física |
| 50000001543 | MALAWI - Persona Física |
| 50000001551 | TANZANIA - Persona Física |
| 50000001586 | COSTA RICA - Persona Física |
| 50000001616 | ZAIRE - Persona Física |
| 50000001624 | BENIN - Persona Física |
| 50000001632 | MALI - Persona Física |
| 50000001705 | UGANDA - Persona Física |
| 50000001713 | SUDAFRICA, REP. DE - Persona Física |
| 50000001810 | REPUBLICA DE SEYCHELLES (Estado independiente) - Persona Física |
| 50000001829 | SANTO TOME Y PRINCIPE - Persona Física |
| 50000001837 | NAMIBIA - Persona Física |
| 50000001845 | GUINEA BISSAU - Persona Física |
| 50000001853 | ERITREA - Persona Física |
| 50000001861 | REPUBLICA DE DJIBUTI (Estado independiente) - Persona Física |
| 50000001896 | COMORAS - Persona Física |
| 50000001985 | INDETERMINADO (AFRICA) - Persona Física |
| 50000002019 | BARBADOS (Estado independiente) - Persona Física |
| 50000002043 | CANADA - Persona Física |
| 50000002051 | COLOMBIA - Persona Física |
| 50000002094 | DOMINICANA, REPUBLICA - Persona Física |
| 50000002116 | EL SALVADOR - Persona Física |
| 50000002124 | ESTADOS UNIDOS - Persona Física |
| 50000002132 | GUATEMALA - Persona Física |
| 50000002140 | REPUBLICA COOPERATIVA DE GUYANA (Estado independiente) - Persona Física |
| 50000002159 | HAITI - Persona Física |
| 50000002167 | HONDURAS - Persona Física |
| 50000002175 | JAMAICA - Persona Física |
| 50000002183 | MEXICO - Persona Física |
| 50000002191 | NICARAGUA - Persona Física |
| 50000002205 | REPUBLICA DE PANAMA (Estado independiente) - Persona Física |
| 50000002213 | ESTADO LIBRE ASOCIADO DE PUERTO RICO (Estado asoc. a EEUU) - Persona Física |
| 50000002221 | PERU - Persona Física |
| 50000002256 | ANTIGUA Y BARBUDA (Estado independiente) - Persona Física |
| 50000002264 | VENEZUELA - Persona Física |
| 50000002272 | POS.BRITANICA (AMERICA) - Persona Física |
| 50000002280 | POS.DANESA (AMERICA) - Persona Física |
| 50000002299 | POS.FRANCESA (AMERICA) - Persona Física |
| 50000002302 | POS.PAISES BAJOS (AMERICA) - Persona Física |
| 50000002310 | POS.E.E.U.U. (AMERICA) - Persona Física |
| 50000002329 | SURINAME - Persona Física |
| 50000002337 | EL COMMONWEALTH DE DOMINICA (Estado Asociado) - Persona Física |
| 50000002345 | SANTA LUCIA - Persona Física |
| 50000002353 | SAN VICENTE Y LAS GRANADINAS (Estado independiente) - Persona Física |
| 50000002361 | BELICE (Estado independiente) - Persona Física |
| 50000002396 | CUBA - Persona Física |
| 50000002426 | ECUADOR - Persona Física |
| 50000002434 | REPUBLICA DE TRINIDAD Y TOBAGO - Persona Física |
| 50000002825 | BUTAN - Persona Física |
| 50000002841 | MYANMAR (EX BIRMANIA) - Persona Física |
| 50000002876 | ISRAEL - Persona Física |
| 50000002882 | ESTADO ASOCIADO DE GRANADA (Estado independiente) - Persona Física |
| 50000002892 | FEDERACION DE SAN CRISTOBAL (Islas Saint Kitts and Nevis) - Persona Física |
| 50000002906 | COMUNIDAD DE LAS BAHAMAS (Estado independiente) - Persona Física |
| 50000002914 | TAILANDIA - Persona Física |
| 50000002922 | INDETERMINADO (AMERICA) - Persona Física |
| 50000002930 | IRAN - Persona Física |
| 50000002981 | ESTADO DE QATAR (Estado independiente) - Persona Física |
| 50000003007 | REINO HACHEMITA DE JORDANIA - Persona Física |
| 50000003015 | AFGANISTAN - Persona Física |
| 50000003023 | ARABIA SAUDITA - Persona Física |
| 50000003031 | ESTADO DE BAHREIN (Estado independiente) - Persona Física |
| 50000003066 | CAMBOYA (EX KAMPUCHEA) - Persona Física |
| 50000003074 | REPUBLICA DEMOCRATICA SOCIALISTA DE SRI LANKA - Persona Física |
| 50000003082 | COREA DEMOCRATICA  - Persona Física |
| 50000003090 | COREA REPUBLICANA - Persona Física |
| 50000003104 | CHINA REP.POPULAR - Persona Física |
| 50000003112 | REPUBLICA DE CHIPRE (Estado independiente) - Persona Física |
| 50000003120 | FILIPINAS - Persona Física |
| 50000003139 | TAIWAN - Persona Física |
| 50000003147 | GAZA - Persona Física |
| 50000003155 | INDIA - Persona Física |
| 50000003163 | INDONESIA - Persona Física |
| 50000003171 | IRAK - Persona Física |
| 50000003201 | JAPON - Persona Física |
| 50000003236 | ESTADO DE KUWAIT (Estado independiente) - Persona Física |
| 50000003244 | LAOS - Persona Física |
| 50000003252 | LIBANO - Persona Física |
| 50000003260 | MALASIA - Persona Física |
| 50000003279 | REPUBLICA DE MALDIVAS (Estado independiente) - Persona Física |
| 50000003287 | SULTANATO DE OMAN - Persona Física |
| 50000003295 | MONGOLIA - Persona Física |
| 50000003309 | NEPAL - Persona Física |
| 50000003317 | EMIRATOS ARABES UNIDOS (Estado independiente) - Persona Física |
| 50000003325 | PAKISTAN - Persona Física |
| 50000003333 | SINGAPUR - Persona Física |
| 50000003341 | SIRIA - Persona Física |
| 50000003376 | VIETNAM - Persona Física |
| 50000003392 | REPUBLICA DEL YEMEN - Persona Física |
| 50000003414 | POS.BRITANICA (HONG KONG) - Persona Física |
| 50000003422 | POS.JAPONESA (ASIA) - Persona Física |
| 50000003449 | MACAO - Persona Física |
| 50000003457 | BANGLADESH - Persona Física |
| 50000003503 | TURQUIA - Persona Física |
| 50000003546 | ITALIA - Persona Física |
| 50000003554 | TURKMENISTAN - Persona Física |
| 50000003562 | UZBEKISTAN - Persona Física |
| 50000003570 | TERRITORIOS AUTONOMOS PALESTINOS - Persona Física |
| 50000003813 | ISLANDIA - Persona Física |
| 50000003880 | GEORGIA - Persona Física |
| 50000003899 | TAYIKISTAN - Persona Física |
| 50000003902 | AZERBAIDZHAN - Persona Física |
| 50000003910 | BRUNEI DARUSSALAM (Estado independiente) - Persona Física |
| 50000003929 | KAZAJSTAN - Persona Física |
| 50000003937 | KIRGUISTAN - Persona Física |
| 50000003961 | INDETERMINADO (ASIA) - Persona Física |
| 50000004011 | REPUBLICA DE ALBANIA - Persona Física |
| 50000004046 | PRINCIPADO DEL VALLE DE ANDORRA - Persona Física |
| 50000004054 | AUSTRIA - Persona Física |
| 50000004062 | BELGICA - Persona Física |
| 50000004070 | BULGARIA - Persona Física |
| 50000004097 | DINAMARCA - Persona Física |
| 50000004100 | ESPAÑA - Persona Física |
| 50000004119 | FINLANDIA - Persona Física |
| 50000004127 | FRANCIA - Persona Física |
| 50000004135 | GRECIA - Persona Física |
| 50000004143 | HUNGRIA - Persona Física |
| 50000004151 | IRLANDA (EIRE) - Persona Física |
| 50000004186 | PRINCIPADO DE LIECHTENSTEIN (Estado independiente) - Persona Física |
| 50000004194 | GRAN DUCADO DE LUXEMBURGO - Persona Física |
| 50000004216 | PRINCIPADO DE MONACO - Persona Física |
| 50000004224 | NORUEGA - Persona Física |
| 50000004232 | PAISES BAJOS - Persona Física |
| 50000004240 | POLONIA - Persona Física |
| 50000004259 | PORTUGAL - Persona Física |
| 50000004267 | REINO UNIDO - Persona Física |
| 50000004275 | RUMANIA - Persona Física |
| 50000004283 | SERENISIMA REPUBLICA DE SAN MARINO (Estado independiente) - Persona Física |
| 50000004291 | SUECIA - Persona Física |
| 50000004305 | SUIZA - Persona Física |
| 50000004313 | SANTA SEDE (VATICANO) - Persona Física |
| 50000004321 | YUGOSLAVIA - Persona Física |
| 50000004364 | REPUBLICA DE MALTA (Estado independiente) - Persona Física |
| 50000004380 | ALEMANIA, REP. FED. - Persona Física |
| 50000004399 | BIELORUSIA - Persona Física |
| 50000004402 | ESTONIA - Persona Física |
| 50000004410 | LETONIA - Persona Física |
| 50000004429 | LITUANIA - Persona Física |
| 50000004437 | MOLDOVA - Persona Física |
| 50000004461 | BOSNIA HERZEGOVINA - Persona Física |
| 50000004496 | ESLOVENIA - Persona Física |
| 50000004909 | MACEDONIA - Persona Física |
| 50000004917 | POS.BRITANICA (EUROPA) - Persona Física |
| 50000004984 | INDETERMINADO (EUROPA) - Persona Física |
| 50000004992 | AUSTRALIA - Persona Física |
| 50000005034 | REPUBLICA DE NAURU (Estado independiente) - Persona Física |
| 50000005042 | NUEVA ZELANDA - Persona Física |
| 50000005050 | REPUBLICA DE VANUATU - Persona Física |
| 50000005069 | SAMOA OCCIDENTAL - Persona Física |
| 50000005077 | POS.AUSTRALIANA (OCEANIA) - Persona Física |
| 50000005085 | POS.BRITANICA (OCEANIA) - Persona Física |
| 50000005093 | POS.FRANCESA (OCEANIA) - Persona Física |
| 50000005107 | POS.NEOCELANDESA (OCEANIA) - Persona Física |
| 50000005115 | POS.E.E.U.U. (OCEANIA) - Persona Física |
| 50000005123 | FIJI, ISLAS - Persona Física |
| 50000005131 | PAPUA, ISLAS - Persona Física |
| 50000005166 | KIRIBATI - Persona Física |
| 50000005174 | TUVALU - Persona Física |
| 50000005182 | ISLAS SALOMON - Persona Física |
| 50000005190 | REINO DE TONGA (Estado independiente) - Persona Física |
| 50000005204 | REPUBLICA DE LAS ISLAS MARSHALL (Estado independiente) - Persona Física |
| 50000005212 | ISLAS MARIANAS - Persona Física |
| 50000005905 | MICRONESIA ESTADOS FED. - Persona Física |
| 50000005913 | PALAU - Persona Física |
| 50000005980 | INDETERMINADO (OCEANIA) - Persona Física |
| 50000006014 | RUSA, FEDERACION - Persona Física |
| 50000006022 | ARMENIA - Persona Física |
| 50000006030 | CROACIA - Persona Física |
| 50000006049 | UCRANIA - Persona Física |
| 50000006057 | CHECA, REPUBLICA - Persona Física |
| 50000006065 | ESLOVACA, REPUBLICA - Persona Física |
| 50000006529 | ANGUILA (Territorio no autónomo del Reino Unido) - Persona Física |
| 50000006537 | ARUBA (Territorio de Países Bajos) - Persona Física |
| 50000006545 | ISLAS DE COOK (Territorio autónomo asociado a Nueva Zelanda) - Persona Física |
| 50000006553 | PATAU - Persona Física |
| 50000006561 | POLINESIA FRANCESA (Territorio de Ultramar de Francia) - Persona Física |
| 50000006596 | ANTILLAS HOLANDESAS (Territorio de Países Bajos) - Persona Física |
| 50000006626 | ASCENCION - Persona Física |
| 50000006634 | BERMUDAS (Territorio no autónomo del Reino Unido) - Persona Física |
| 50000006642 | CAMPIONE D@ITALIA - Persona Física |
| 50000006650 | COLONIA DE GIBRALTAR - Persona Física |
| 50000006669 | GROENLANDIA - Persona Física |
| 50000006677 | GUAM (Territorio no autónomo de los EEUU) - Persona Física |
| 50000006685 | HONK KONG (Territorio de China) - Persona Física |
| 50000006693 | ISLAS AZORES - Persona Física |
| 50000006707 | ISLAS DEL CANAL:Guernesey,Jersey,Alderney,G.Stark,L.Sark,etc - Persona Física |
| 50000006715 | ISLAS CAIMAN (Territorio no autónomo del Reino Unido) - Persona Física |
| 50000006723 | ISLA CHRISTMAS - Persona Física |
| 50000006731 | ISLA DE COCOS O KEELING - Persona Física |
| 50000006766 | ISLA DE MAN (Territorio del Reino Unido) - Persona Física |
| 50000006774 | ISLA DE NORFOLK - Persona Física |
| 50000006782 | ISLAS TURKAS Y CAICOS (Territorio no autónomo del R. Unido) - Persona Física |
| 50000006790 | ISLAS PACIFICO - Persona Física |
| 50000006804 | ISLA DE SAN PEDRO Y MIGUELON - Persona Física |
| 50000006812 | ISLA QESHM - Persona Física |
| 50000006820 | ISLAS VIRGENES BRITANICAS(Territorio no autónomo de R.UNIDO) - Persona Física |
| 50000006839 | ISLAS VIRGENES DE ESTADOS UNIDOS DE AMERICA - Persona Física |
| 50000006847 | LABUAN - Persona Física |
| 50000006855 | MADEIRA (Territorio de Portugal) - Persona Física |
| 50000006863 | MONTSERRAT (Territorio no autónomo del Reino Unido) - Persona Física |
| 50000006871 | NIUE - Persona Física |
| 50000006901 | PITCAIRN - Persona Física |
| 50000006936 | REGIMEN APLICABLE A LAS SA FINANCIERAS(ley 11.073 de la ROU) - Persona Física |
| 50000006944 | SANTA ELENA - Persona Física |
| 50000006952 | SAMOA AMERICANA (Territorio no autónomo de los EEUU) - Persona Física |
| 50000006960 | ARCHIPIELAGO DE SVBALBARD - Persona Física |
| 50000006979 | TRISTAN DA CUNHA - Persona Física |
| 50000006987 | TRIESTE (Italia) - Persona Física |
| 50000006995 | TOKELAU - Persona Física |
| 50000007002 | ZONA LIBRE DE OSTRAVA (ciudad de la antigua Checoeslovaquia) - Persona Física |
| 50000009986 | PARA PERSONAS FISICAS DE INDETERMINADO (CONTINENTE) - Persona Física |
| 50000009994 | PARA PERSONAS FISICAS DE OTROS PAISES - Persona Física |
| 51600000016 | URUGUAY - Otro tipo de Entidad |
| 51600000024 | PARAGUAY - Otro tipo de Entidad |
| 51600000032 | CHILE - Otro tipo de Entidad |
| 51600000040 | BOLIVIA - Otro tipo de Entidad |
| 51600000059 | BRASIL - Otro tipo de Entidad |
| 51600001012 | BURKINA FASO - Otro tipo de Entidad |
| 51600001020 | ARGELIA - Otro tipo de Entidad |
| 51600001039 | BOTSWANA - Otro tipo de Entidad |
| 51600001047 | BURUNDI - Otro tipo de Entidad |
| 51600001055 | CAMERUN - Otro tipo de Entidad |
| 51600001071 | CENTRO AFRICANO, REP. - Otro tipo de Entidad |
| 51600001101 | COSTA DE MARFIL - Otro tipo de Entidad |
| 51600001136 | EGIPTO - Otro tipo de Entidad |
| 51600001144 | ETIOPIA - Otro tipo de Entidad |
| 51600001152 | GABON - Otro tipo de Entidad |
| 51600001160 | GAMBIA - Otro tipo de Entidad |
| 51600001179 | GHANA - Otro tipo de Entidad |
| 51600001187 | GUINEA - Otro tipo de Entidad |
| 51600001195 | GUINEA ECUATORIAL - Otro tipo de Entidad |
| 51600001209 | KENIA - Otro tipo de Entidad |
| 51600001217 | LESOTHO - Otro tipo de Entidad |
| 51600001225 | REPUBLICA DE LIBERIA (Estado independiente) - Otro tipo de Entidad |
| 51600001233 | LIBIA - Otro tipo de Entidad |
| 51600001241 | MADAGASCAR - Otro tipo de Entidad |
| 51600001276 | MARRUECOS - Otro tipo de Entidad |
| 51600001284 | REPUBLICA DE MAURICIO - Otro tipo de Entidad |
| 51600001292 | MAURITANIA - Otro tipo de Entidad |
| 51600001306 | NIGER - Otro tipo de Entidad |
| 51600001314 | NIGERIA - Otro tipo de Entidad |
| 51600001322 | ZIMBABWE - Otro tipo de Entidad |
| 51600001330 | RUANDA - Otro tipo de Entidad |
| 51600001349 | SENEGAL - Otro tipo de Entidad |
| 51600001357 | SIERRA LEONA - Otro tipo de Entidad |
| 51600001365 | SOMALIA - Otro tipo de Entidad |
| 51600001373 | REINO DE SWAZILANDIA (Estado independiente) - Otro tipo de Entidad |
| 51600001381 | SUDAN - Otro tipo de Entidad |
| 51600001403 | TOGO - Otro tipo de Entidad |
| 51600001411 | REPUBLICA TUNECINA - Otro tipo de Entidad |
| 51600001446 | ZAMBIA - Otro tipo de Entidad |
| 51600001454 | POS.BRITANICA (AFRICA) - Otro tipo de Entidad |
| 51600001462 | POS.ESPAÑOLA (AFRICA) - Otro tipo de Entidad |
| 51600001470 | POS.FRANCESA (AFRICA) - Otro tipo de Entidad |
| 51600001489 | POS.PORTUGUESA (AFRICA) - Otro tipo de Entidad |
| 51600001497 | REPUBLICA DE ANGOLA - Otro tipo de Entidad |
| 51600001500 | REPUBLICA DE CABO VERDE (Estado independiente) - Otro tipo de Entidad |
| 51600001519 | MOZAMBIQUE - Otro tipo de Entidad |
| 51600001527 | CONGO REP.POPULAR - Otro tipo de Entidad |
| 51600001535 | CHAD - Otro tipo de Entidad |
| 51600001543 | MALAWI - Otro tipo de Entidad |
| 51600001551 | TANZANIA - Otro tipo de Entidad |
| 51600001586 | COSTA RICA - Otro tipo de Entidad |
| 51600001616 | ZAIRE - Otro tipo de Entidad |
| 51600001624 | BENIN - Otro tipo de Entidad |
| 51600001632 | MALI - Otro tipo de Entidad |
| 51600001705 | UGANDA - Otro tipo de Entidad |
| 51600001713 | SUDAFRICA, REP. DE - Otro tipo de Entidad |
| 51600001810 | REPUBLICA DE SEYCHELLES (Estado independiente) - Otro tipo de Entidad |
| 51600001829 | SANTO TOME Y PRINCIPE - Otro tipo de Entidad |
| 51600001837 | NAMIBIA - Otro tipo de Entidad |
| 51600001845 | GUINEA BISSAU - Otro tipo de Entidad |
| 51600001853 | ERITREA - Otro tipo de Entidad |
| 51600001861 | REPUBLICA DE DJIBUTI (Estado independiente) - Otro tipo de Entidad |
| 51600001896 | COMORAS - Otro tipo de Entidad |
| 51600001985 | INDETERMINADO (AFRICA) - Otro tipo de Entidad |
| 51600002019 | BARBADOS (Estado independiente) - Otro tipo de Entidad |
| 51600002043 | CANADA - Otro tipo de Entidad |
| 51600002051 | COLOMBIA - Otro tipo de Entidad |
| 51600002094 | DOMINICANA, REPUBLICA - Otro tipo de Entidad |
| 51600002116 | EL SALVADOR - Otro tipo de Entidad |
| 51600002124 | ESTADOS UNIDOS - Otro tipo de Entidad |
| 51600002132 | GUATEMALA - Otro tipo de Entidad |
| 51600002140 | REPUBLICA COOPERATIVA DE GUYANA (Estado independiente) - Otro tipo de Entidad |
| 51600002159 | HAITI - Otro tipo de Entidad |
| 51600002167 | HONDURAS - Otro tipo de Entidad |
| 51600002175 | JAMAICA - Otro tipo de Entidad |
| 51600002183 | MEXICO - Otro tipo de Entidad |
| 51600002191 | NICARAGUA - Otro tipo de Entidad |
| 51600002205 | REPUBLICA DE PANAMA (Estado independiente) - Otro tipo de Entidad |
| 51600002213 | ESTADO LIBRE ASOCIADO DE PUERTO RICO (Estado asoc. a EEUU) - Otro tipo de Entidad |
| 51600002221 | PERU - Otro tipo de Entidad |
| 51600002256 | ANTIGUA Y BARBUDA (Estado independiente) - Otro tipo de Entidad |
| 51600002264 | VENEZUELA - Otro tipo de Entidad |
| 51600002272 | POS.BRITANICA (AMERICA) - Otro tipo de Entidad |
| 51600002280 | POS.DANESA (AMERICA) - Otro tipo de Entidad |
| 51600002299 | POS.FRANCESA (AMERICA) - Otro tipo de Entidad |
| 51600002302 | POS.PAISES BAJOS (AMERICA) - Otro tipo de Entidad |
| 51600002310 | POS.E.E.U.U. (AMERICA) - Otro tipo de Entidad |
| 51600002329 | SURINAME - Otro tipo de Entidad |
| 51600002337 | EL COMMONWEALTH DE DOMINICA (Estado Asociado) - Otro tipo de Entidad |
| 51600002345 | SANTA LUCIA - Otro tipo de Entidad |
| 51600002353 | SAN VICENTE Y LAS GRANADINAS (Estado independiente) - Otro tipo de Entidad |
| 51600002361 | BELICE (Estado independiente) - Otro tipo de Entidad |
| 51600002396 | CUBA - Otro tipo de Entidad |
| 51600002426 | ECUADOR - Otro tipo de Entidad |
| 51600002434 | REPUBLICA DE TRINIDAD Y TOBAGO - Otro tipo de Entidad |
| 51600002825 | BUTAN - Otro tipo de Entidad |
| 51600002841 | MYANMAR (EX BIRMANIA) - Otro tipo de Entidad |
| 51600002876 | ISRAEL - Otro tipo de Entidad |
| 51600002884 | ESTADO ASOCIADO DE GRANADA (Estado independiente) - Otro tipo de Entidad |
| 51600002892 | FEDERACION DE SAN CRISTOBAL (Islas Saint Kitts and Nevis) - Otro tipo de Entidad |
| 51600002906 | COMUNIDAD DE LAS BAHAMAS (Estado independiente) - Otro tipo de Entidad |
| 51600002914 | TAILANDIA - Otro tipo de Entidad |
| 51600002922 | INDETERMINADO (AMERICA) - Otro tipo de Entidad |
| 51600002930 | IRAN - Otro tipo de Entidad |
| 51600002981 | ESTADO DE QATAR (Estado independiente) - Otro tipo de Entidad |
| 51600003007 | REINO HACHEMITA DE JORDANIA - Otro tipo de Entidad |
| 51600003015 | AFGANISTAN - Otro tipo de Entidad |
| 51600003023 | ARABIA SAUDITA - Otro tipo de Entidad |
| 51600003031 | ESTADO DE BAHREIN (Estado independiente) - Otro tipo de Entidad |
| 51600003066 | CAMBOYA (EX KAMPUCHEA) - Otro tipo de Entidad |
| 51600003074 | REPUBLICA DEMOCRATICA SOCIALISTA DE SRI LANKA - Otro tipo de Entidad |
| 51600003082 | COREA DEMOCRATICA  - Otro tipo de Entidad |
| 51600003090 | COREA REPUBLICANA - Otro tipo de Entidad |
| 51600003104 | CHINA REP.POPULAR - Otro tipo de Entidad |
| 51600003112 | REPUBLICA DE CHIPRE (Estado independiente) - Otro tipo de Entidad |
| 51600003120 | FILIPINAS - Otro tipo de Entidad |
| 51600003139 | TAIWAN - Otro tipo de Entidad |
| 51600003147 | GAZA - Otro tipo de Entidad |
| 51600003155 | INDIA - Otro tipo de Entidad |
| 51600003163 | INDONESIA - Otro tipo de Entidad |
| 51600003171 | IRAK - Otro tipo de Entidad |
| 51600003201 | JAPON - Otro tipo de Entidad |
| 51600003236 | ESTADO DE KUWAIT (Estado independiente) - Otro tipo de Entidad |
| 51600003244 | LAOS - Otro tipo de Entidad |
| 51600003252 | LIBANO - Otro tipo de Entidad |
| 51600003260 | MALASIA - Otro tipo de Entidad |
| 51600003279 | REPUBLICA DE MALDIVAS (Estado independiente) - Otro tipo de Entidad |
| 51600003287 | SULTANATO DE OMAN - Otro tipo de Entidad |
| 51600003295 | MONGOLIA - Otro tipo de Entidad |
| 51600003309 | NEPAL - Otro tipo de Entidad |
| 51600003317 | EMIRATOS ARABES UNIDOS (Estado independiente) - Otro tipo de Entidad |
| 51600003325 | PAKISTAN - Otro tipo de Entidad |
| 51600003333 | SINGAPUR - Otro tipo de Entidad |
| 51600003341 | SIRIA - Otro tipo de Entidad |
| 51600003376 | VIETNAM - Otro tipo de Entidad |
| 51600003392 | REPUBLICA DEL YEMEN - Otro tipo de Entidad |
| 51600003414 | POS.BRITANICA (HONG KONG) - Otro tipo de Entidad |
| 51600003422 | POS.JAPONESA (ASIA) - Otro tipo de Entidad |
| 51600003449 | MACAO - Otro tipo de Entidad |
| 51600003457 | BANGLADESH - Otro tipo de Entidad |
| 51600003503 | TURQUIA - Otro tipo de Entidad |
| 51600003546 | ITALIA - Otro tipo de Entidad |
| 51600003554 | TURKMENISTAN - Otro tipo de Entidad |
| 51600003562 | UZBEKISTAN - Otro tipo de Entidad |
| 51600003570 | TERRITORIOS AUTONOMOS PALESTINOS - Otro tipo de Entidad |
| 51600003813 | ISLANDIA - Otro tipo de Entidad |
| 51600003880 | GEORGIA - Otro tipo de Entidad |
| 51600003899 | TAYIKISTAN - Otro tipo de Entidad |
| 51600003902 | AZERBAIDZHAN - Otro tipo de Entidad |
| 51600003910 | BRUNEI DARUSSALAM (Estado independiente) - Otro tipo de Entidad |
| 51600003929 | KAZAJSTAN - Otro tipo de Entidad |
| 51600003937 | KIRGUISTAN - Otro tipo de Entidad |
| 51600003961 | INDETERMINADO (ASIA) - Otro tipo de Entidad |
| 51600004011 | REPUBLICA DE ALBANIA - Otro tipo de Entidad |
| 51600004046 | PRINCIPADO DEL VALLE DE ANDORRA - Otro tipo de Entidad |
| 51600004054 | AUSTRIA - Otro tipo de Entidad |
| 51600004062 | BELGICA - Otro tipo de Entidad |
| 51600004070 | BULGARIA - Otro tipo de Entidad |
| 51600004097 | DINAMARCA - Otro tipo de Entidad |
| 51600004100 | ESPAÑA - Otro tipo de Entidad |
| 51600004119 | FINLANDIA - Otro tipo de Entidad |
| 51600004127 | FRANCIA - Otro tipo de Entidad |
| 51600004135 | GRECIA - Otro tipo de Entidad |
| 51600004143 | HUNGRIA - Otro tipo de Entidad |
| 51600004151 | IRLANDA (EIRE) - Otro tipo de Entidad |
| 51600004186 | PRINCIPADO DE LIECHTENSTEIN (Estado independiente) - Otro tipo de Entidad |
| 51600004194 | GRAN DUCADO DE LUXEMBURGO - Otro tipo de Entidad |
| 51600004216 | PRINCIPADO DE MONACO - Otro tipo de Entidad |
| 51600004224 | NORUEGA - Otro tipo de Entidad |
| 51600004232 | PAISES BAJOS - Otro tipo de Entidad |
| 51600004240 | POLONIA - Otro tipo de Entidad |
| 51600004259 | PORTUGAL - Otro tipo de Entidad |
| 51600004267 | REINO UNIDO - Otro tipo de Entidad |
| 51600004275 | RUMANIA - Otro tipo de Entidad |
| 51600004283 | SERENISIMA REPUBLICA DE SAN MARINO (Estado independiente) - Otro tipo de Entidad |
| 51600004291 | SUECIA - Otro tipo de Entidad |
| 51600004305 | SUIZA - Otro tipo de Entidad |
| 51600004313 | SANTA SEDE (VATICANO) - Otro tipo de Entidad |
| 51600004321 | YUGOSLAVIA - Otro tipo de Entidad |
| 51600004364 | REPUBLICA DE MALTA (Estado independiente) - Otro tipo de Entidad |
| 51600004380 | ALEMANIA, REP. FED. - Otro tipo de Entidad |
| 51600004399 | BIELORUSIA - Otro tipo de Entidad |
| 51600004402 | ESTONIA - Otro tipo de Entidad |
| 51600004410 | LETONIA - Otro tipo de Entidad |
| 51600004429 | LITUANIA - Otro tipo de Entidad |
| 51600004437 | MOLDOVA - Otro tipo de Entidad |
| 51600004461 | BOSNIA HERZEGOVINA - Otro tipo de Entidad |
| 51600004496 | ESLOVENIA - Otro tipo de Entidad |
| 51600004909 | MACEDONIA - Otro tipo de Entidad |
| 51600004917 | POS.BRITANICA (EUROPA) - Otro tipo de Entidad |
| 51600004984 | INDETERMINADO (EUROPA) - Otro tipo de Entidad |
| 51600004992 | AUSTRALIA - Otro tipo de Entidad |
| 51600005034 | REPUBLICA DE NAURU (Estado independiente) - Otro tipo de Entidad |
| 51600005042 | NUEVA ZELANDA - Otro tipo de Entidad |
| 51600005050 | REPUBLICA DE VANUATU - Otro tipo de Entidad |
| 51600005069 | SAMOA OCCIDENTAL - Otro tipo de Entidad |
| 51600005077 | POS.AUSTRALIANA (OCEANIA) - Otro tipo de Entidad |
| 51600005085 | POS.BRITANICA (OCEANIA) - Otro tipo de Entidad |
| 51600005093 | POS.FRANCESA (OCEANIA) - Otro tipo de Entidad |
| 51600005107 | POS.NEOCELANDESA (OCEANIA) - Otro tipo de Entidad |
| 51600005115 | POS.E.E.U.U. (OCEANIA) - Otro tipo de Entidad |
| 51600005123 | FIJI, ISLAS - Otro tipo de Entidad |
| 51600005131 | PAPUA, ISLAS - Otro tipo de Entidad |
| 51600005166 | KIRIBATI - Otro tipo de Entidad |
| 51600005174 | TUVALU - Otro tipo de Entidad |
| 51600005182 | ISLAS SALOMON - Otro tipo de Entidad |
| 51600005190 | REINO DE TONGA (Estado independiente) - Otro tipo de Entidad |
| 51600005204 | REPUBLICA DE LAS ISLAS MARSHALL (Estado independiente) - Otro tipo de Entidad |
| 51600005212 | ISLAS MARIANAS - Otro tipo de Entidad |
| 51600005905 | MICRONESIA ESTADOS FEDERADOS - Otro tipo de Entidad |
| 51600005913 | PALAU - Otro tipo de Entidad |
| 51600005980 | INDETERMINADO (OCEANIA) - Otro tipo de Entidad |
| 51600006014 | RUSA, FEDERACION - Otro tipo de Entidad |
| 51600006022 | ARMENIA - Otro tipo de Entidad |
| 51600006030 | CROACIA - Otro tipo de Entidad |
| 51600006049 | UCRANIA - Otro tipo de Entidad |
| 51600006057 | CHECA, REPUBLICA - Otro tipo de Entidad |
| 51600006065 | ESLOVACA, REPUBLICA - Otro tipo de Entidad |
| 51600006529 | ANGUILA (Territorio no autónomo del Reino Unido) - Otro tipo de Entidad |
| 51600006537 | ARUBA (Territorio de Países Bajos) - Otro tipo de Entidad |
| 51600006545 | ISLAS DE COOK (Territorio autónomo asociado a Nueva Zelanda) - Otro tipo de Entidad |
| 51600006553 | PATAU - Otro tipo de Entidad |
| 51600006561 | POLINESIA FRANCESA (Territorio de Ultramar de Francia) - Otro tipo de Entidad |
| 51600006596 | ANTILLAS HOLANDESAS (Territorio de Países Bajos) - Otro tipo de Entidad |
| 51600006626 | ASCENCION - Otro tipo de Entidad |
| 51600006634 | BERMUDAS (Territorio no autónomo del Reino Unido) - Otro tipo de Entidad |
| 51600006642 | CAMPIONE D@ITALIA - Otro tipo de Entidad |
| 51600006650 | COLONIA DE GIBRALTAR - Otro tipo de Entidad |
| 51600006669 | GROENLANDIA - Otro tipo de Entidad |
| 51600006677 | GUAM (Territorio no autónomo de los EEUU) - Otro tipo de Entidad |
| 51600006685 | HONK KONG (Territorio de China) - Otro tipo de Entidad |
| 51600006693 | ISLAS AZORES - Otro tipo de Entidad |
| 51600006707 | ISLAS DEL CANAL:Guernesey,Jersey,Alderney,G.Stark,L.Sark,etc - Otro tipo de Entidad |
| 51600006715 | ISLAS CAIMAN (Territorio no autónomo del Reino Unido) - Otro tipo de Entidad |
| 51600006723 | ISLA CHRISTMAS - Otro tipo de Entidad |
| 51600006731 | ISLA DE COCOS O KEELING - Otro tipo de Entidad |
| 51600006766 | ISLA DE MAN (Territorio del Reino Unido) - Otro tipo de Entidad |
| 51600006774 | ISLA DE NORFOLK - Otro tipo de Entidad |
| 51600006782 | ISLAS TURKAS Y CAICOS (Territorio no autónomo del R. Unido) - Otro tipo de Entidad |
| 51600006790 | ISLAS PACIFICO - Otro tipo de Entidad |
| 51600006804 | ISLA DE SAN PEDRO Y MIGUELON - Otro tipo de Entidad |
| 51600006812 | ISLA QESHM - Otro tipo de Entidad |
| 51600006820 | ISLAS VIRGENES BRITANICAS(Territorio no autónomo de R.UNIDO) - Otro tipo de Entidad |
| 51600006839 | ISLAS VIRGENES DE ESTADOS UNIDOS DE AMERICA - Otro tipo de Entidad |
| 51600006847 | LABUAN - Otro tipo de Entidad |
| 51600006855 | MADEIRA (Territorio de Portugal) - Otro tipo de Entidad |
| 51600006863 | MONTSERRAT (Territorio no autónomo del Reino Unido) - Otro tipo de Entidad |
| 51600006871 | NIUE - Otro tipo de Entidad |
| 51600006901 | PITCAIRN - Otro tipo de Entidad |
| 51600006936 | REGIMEN APLICABLE A LAS SA FINANCIERAS(ley 11.073 de la ROU) - Otro tipo de Entidad |
| 51600006944 | SANTA ELENA - Otro tipo de Entidad |
| 51600006952 | SAMOA AMERICANA (Territorio no autónomo de los EEUU) - Otro tipo de Entidad |
| 51600006960 | ARCHIPIELAGO DE SVBALBARD - Otro tipo de Entidad |
| 51600006979 | TRISTAN DA CUNHA - Otro tipo de Entidad |
| 51600006987 | TRIESTE (Italia) - Otro tipo de Entidad |
| 51600006995 | TOKELAU - Otro tipo de Entidad |
| 51600007002 | ZONA LIBRE DE OSTRAVA (ciudad de la antigua Checoeslovaquia) - Otro tipo de Entidad |
| 51600009986 | PARA PERSONAS FISICAS DE INDETERMINADO (CONTINENTE) - Otro tipo de Entidad |
| 51600009994 | PARA PERSONAS FISICAS DE OTROS PAISES - Otro tipo de Entidad |
| 55000000018 | URUGUAY - Persona Jurídica |
| 55000000026 | PARAGUAY - Persona Jurídica |
| 55000000034 | CHILE - Persona Jurídica |
| 55000000042 | BOLIVIA - Persona Jurídica |
| 55000000050 | BRASIL - Persona Jurídica |
| 55000001014 | BURKINA FASO - Persona Jurídica |
| 55000001022 | ARGELIA - Persona Jurídica |
| 55000001030 | BOTSWANA - Persona Jurídica |
| 55000001049 | BURUNDI - Persona Jurídica |
| 55000001057 | CAMERUN - Persona Jurídica |
| 55000001073 | CENTRO AFRICANO, REP. - Persona Jurídica |
| 55000001103 | COSTA DE MARFIL - Persona Jurídica |
| 55000001138 | EGIPTO - Persona Jurídica |
| 55000001146 | ETIOPIA - Persona Jurídica |
| 55000001154 | GABON - Persona Jurídica |
| 55000001162 | GAMBIA - Persona Jurídica |
| 55000001170 | GHANA - Persona Jurídica |
| 55000001189 | GUINEA - Persona Jurídica |
| 55000001197 | GUINEA ECUATORIAL - Persona Jurídica |
| 55000001200 | KENIA - Persona Jurídica |
| 55000001219 | LESOTHO - Persona Jurídica |
| 55000001227 | REPUBLICA DE LIBERIA (Estado independiente) - Persona Jurídica |
| 55000001235 | LIBIA - Persona Jurídica |
| 55000001243 | MADAGASCAR - Persona Jurídica |
| 55000001278 | MARRUECOS - Persona Jurídica |
| 55000001286 | REPUBLICA DE MAURICIO - Persona Jurídica |
| 55000001294 | MAURITANIA - Persona Jurídica |
| 55000001308 | NIGER - Persona Jurídica |
| 55000001316 | NIGERIA - Persona Jurídica |
| 55000001324 | ZIMBABWE - Persona Jurídica |
| 55000001332 | RUANDA - Persona Jurídica |
| 55000001340 | SENEGAL - Persona Jurídica |
| 55000001359 | SIERRA LEONA - Persona Jurídica |
| 55000001367 | SOMALIA - Persona Jurídica |
| 55000001375 | REINO DE SWAZILANDIA (Estado independiente) - Persona Jurídica |
| 55000001383 | SUDAN - Persona Jurídica |
| 55000001405 | TOGO - Persona Jurídica |
| 55000001413 | REPUBLICA TUNECINA - Persona Jurídica |
| 55000001448 | ZAMBIA - Persona Jurídica |
| 55000001456 | POS.BRITANICA (AFRICA) - Persona Jurídica |
| 55000001464 | POS.ESPAÑOLA (AFRICA) - Persona Jurídica |
| 55000001472 | POS.FRANCESA (AFRICA) - Persona Jurídica |
| 55000001480 | POS.PORTUGUESA (AFRICA) - Persona Jurídica |
| 55000001499 | REPUBLICA DE ANGOLA - Persona Jurídica |
| 55000001502 | REPUBLICA DE CABO VERDE (Estado independiente) - Persona Jurídica |
| 55000001510 | MOZAMBIQUE - Persona Jurídica |
| 55000001529 | CONGO REP.POPULAR - Persona Jurídica |
| 55000001537 | CHAD - Persona Jurídica |
| 55000001545 | MALAWI - Persona Jurídica |
| 55000001553 | TANZANIA - Persona Jurídica |
| 55000001588 | COSTA RICA - Persona Jurídica |
| 55000001618 | ZAIRE - Persona Jurídica |
| 55000001626 | BENIN - Persona Jurídica |
| 55000001634 | MALI - Persona Jurídica |
| 55000001707 | UGANDA - Persona Jurídica |
| 55000001715 | SUDAFRICA, REP. DE - Persona Jurídica |
| 55000001812 | REPUBLICA DE SEYCHELLES (Estado independiente) - Persona Jurídica |
| 55000001820 | SANTO TOME Y PRINCIPE - Persona Jurídica |
| 55000001839 | NAMIBIA - Persona Jurídica |
| 55000001847 | GUINEA BISSAU - Persona Jurídica |
| 55000001855 | ERITREA - Persona Jurídica |
| 55000001863 | REPUBLICA DE DJIBUTI (Estado independiente) - Persona Jurídica |
| 55000001898 | COMORAS - Persona Jurídica |
| 55000001987 | INDETERMINADO (AFRICA) - Persona Jurídica |
| 55000002010 | BARBADOS (Estado independiente) - Persona Jurídica |
| 55000002045 | CANADA - Persona Jurídica |
| 55000002053 | COLOMBIA - Persona Jurídica |
| 55000002096 | DOMINICANA, REPUBLICA - Persona Jurídica |
| 55000002118 | EL SALVADOR - Persona Jurídica |
| 55000002126 | ESTADOS UNIDOS - Persona Jurídica |
| 55000002134 | GUATEMALA - Persona Jurídica |
| 55000002142 | REPUBLICA COOPERATIVA DE GUYANA (Estado independiente) - Persona Jurídica |
| 55000002150 | HAITI - Persona Jurídica |
| 55000002169 | HONDURAS - Persona Jurídica |
| 55000002177 | JAMAICA - Persona Jurídica |
| 55000002185 | MEXICO - Persona Jurídica |
| 55000002193 | NICARAGUA - Persona Jurídica |
| 55000002207 | REPUBLICA DE PANAMA (Estado independiente) - Persona Jurídica |
| 55000002215 | ESTADO LIBRE ASOCIADO DE PUERTO RICO (Estado asoc. a EEUU) - Persona Jurídica |
| 55000002223 | PERU - Persona Jurídica |
| 55000002258 | ANTIGUA Y BARBUDA (Estado independiente) - Persona Jurídica |
| 55000002266 | VENEZUELA - Persona Jurídica |
| 55000002274 | POS.BRITANICA (AMERICA) - Persona Jurídica |
| 55000002282 | POS.DANESA (AMERICA) - Persona Jurídica |
| 55000002290 | POS.FRANCESA (AMERICA) - Persona Jurídica |
| 55000002304 | POS.PAISES BAJOS (AMERICA) - Persona Jurídica |
| 55000002312 | POS.E.E.U.U. (AMERICA) - Persona Jurídica |
| 55000002320 | SURINAME - Persona Jurídica |
| 55000002339 | EL COMMONWEALTH DE DOMINICA (Estado Asociado) - Persona Jurídica |
| 55000002347 | SANTA LUCIA - Persona Jurídica |
| 55000002355 | SAN VICENTE Y LAS GRANADINAS (Estado independiente) - Persona Jurídica |
| 55000002363 | BELICE (Estado independiente) - Persona Jurídica |
| 55000002398 | CUBA - Persona Jurídica |
| 55000002428 | ECUADOR - Persona Jurídica |
| 55000002436 | REPUBLICA DE TRINIDAD Y TOBAGO - Persona Jurídica |
| 55000002827 | BUTAN - Persona Jurídica |
| 55000002843 | MYANMAR (EX BIRMANIA) - Persona Jurídica |
| 55000002878 | ISRAEL - Persona Jurídica |
| 55000002884 | ESTADO ASOCIADO DE GRANADA (Estado independiente) - Persona Jurídica |
| 55000002894 | FEDERACION DE SAN CRISTOBAL (Islas Saint Kitts and Nevis) - Persona Jurídica |
| 55000002908 | COMUNIDAD DE LAS BAHAMAS (Estado independiente) - Persona Jurídica |
| 55000002916 | TAILANDIA - Persona Jurídica |
| 55000002924 | INDETERMINADO (AMERICA) - Persona Jurídica |
| 55000002932 | IRAN - Persona Jurídica |
| 55000002983 | ESTADO DE QATAR (Estado independiente) - Persona Jurídica |
| 55000003009 | REINO HACHEMITA DE JORDANIA - Persona Jurídica |
| 55000003017 | AFGANISTAN - Persona Jurídica |
| 55000003025 | ARABIA SAUDITA - Persona Jurídica |
| 55000003033 | ESTADO DE BAHREIN (Estado independiente) - Persona Jurídica |
| 55000003068 | CAMBOYA (EX KAMPUCHEA) - Persona Jurídica |
| 55000003076 | REPUBLICA DEMOCRATICA SOCIALISTA DE SRI LANKA - Persona Jurídica |
| 55000003084 | COREA DEMOCRATICA  - Persona Jurídica |
| 55000003092 | COREA REPUBLICANA - Persona Jurídica |
| 55000003106 | CHINA REP.POPULAR - Persona Jurídica |
| 55000003114 | REPUBLICA DE CHIPRE (Estado independiente) - Persona Jurídica |
| 55000003122 | FILIPINAS - Persona Jurídica |
| 55000003130 | TAIWAN - Persona Jurídica |
| 55000003149 | GAZA - Persona Jurídica |
| 55000003157 | INDIA - Persona Jurídica |
| 55000003165 | INDONESIA - Persona Jurídica |
| 55000003173 | IRAK - Persona Jurídica |
| 55000003203 | JAPON - Persona Jurídica |
| 55000003238 | ESTADO DE KUWAIT (Estado independiente) - Persona Jurídica |
| 55000003246 | LAOS - Persona Jurídica |
| 55000003254 | LIBANO - Persona Jurídica |
| 55000003262 | MALASIA - Persona Jurídica |
| 55000003270 | REPUBLICA DE MALDIVAS (Estado independiente) - Persona Jurídica |
| 55000003289 | SULTANATO DE OMAN - Persona Jurídica |
| 55000003297 | MONGOLIA - Persona Jurídica |
| 55000003300 | NEPAL - Persona Jurídica |
| 55000003319 | EMIRATOS ARABES UNIDOS (Estado independiente) - Persona Jurídica |
| 55000003327 | PAKISTAN - Persona Jurídica |
| 55000003335 | SINGAPUR - Persona Jurídica |
| 55000003343 | SIRIA - Persona Jurídica |
| 55000003378 | VIETNAM - Persona Jurídica |
| 55000003394 | REPUBLICA DEL YEMEN - Persona Jurídica |
| 55000003416 | POS.BRITANICA (HONG KONG) - Persona Jurídica |
| 55000003424 | POS.JAPONESA (ASIA) - Persona Jurídica |
| 55000003440 | MACAO - Persona Jurídica |
| 55000003459 | BANGLADESH - Persona Jurídica |
| 55000003505 | TURQUIA - Persona Jurídica |
| 55000003548 | ITALIA - Persona Jurídica |
| 55000003556 | TURKMENISTAN - Persona Jurídica |
| 55000003564 | UZBEKISTAN - Persona Jurídica |
| 55000003572 | TERRITORIOS AUTONOMOS PALESTINOS - Persona Jurídica |
| 55000003815 | ISLANDIA - Persona Jurídica |
| 55000003882 | GEORGIA - Persona Jurídica |
| 55000003890 | TAYIKISTAN - Persona Jurídica |
| 55000003904 | AZERBAIDZHAN - Persona Jurídica |
| 55000003912 | BRUNEI DARUSSALAM (Estado independiente) - Persona Jurídica |
| 55000003920 | KAZAJSTAN - Persona Jurídica |
| 55000003939 | KIRGUISTAN - Persona Jurídica |
| 55000003963 | INDETERMINADO (ASIA) - Persona Jurídica |
| 55000004013 | REPUBLICA DE ALBANIA - Persona Jurídica |
| 55000004048 | PRINCIPADO DEL VALLE DE ANDORRA - Persona Jurídica |
| 55000004056 | AUSTRIA - Persona Jurídica |
| 55000004064 | BELGICA - Persona Jurídica |
| 55000004072 | BULGARIA - Persona Jurídica |
| 55000004099 | DINAMARCA - Persona Jurídica |
| 55000004102 | ESPAÑA - Persona Jurídica |
| 55000004110 | FINLANDIA - Persona Jurídica |
| 55000004129 | FRANCIA - Persona Jurídica |
| 55000004137 | GRECIA - Persona Jurídica |
| 55000004145 | HUNGRIA - Persona Jurídica |
| 55000004153 | IRLANDA (EIRE) - Persona Jurídica |
| 55000004188 | PRINCIPADO DE LIECHTENSTEIN (Estado independiente) - Persona Jurídica |
| 55000004196 | GRAN DUCADO DE LUXEMBURGO - Persona Jurídica |
| 55000004218 | PRINCIPADO DE MONACO - Persona Jurídica |
| 55000004226 | NORUEGA - Persona Jurídica |
| 55000004234 | PAISES BAJOS - Persona Jurídica |
| 55000004242 | POLONIA - Persona Jurídica |
| 55000004250 | PORTUGAL - Persona Jurídica |
| 55000004269 | REINO UNIDO - Persona Jurídica |
| 55000004277 | RUMANIA - Persona Jurídica |
| 55000004285 | SERENISIMA REPUBLICA DE SAN MARINO (Estado independiente) - Persona Jurídica |
| 55000004293 | SUECIA - Persona Jurídica |
| 55000004307 | SUIZA - Persona Jurídica |
| 55000004315 | SANTA SEDE (VATICANO) - Persona Jurídica |
| 55000004323 | YUGOSLAVIA - Persona Jurídica |
| 55000004366 | REPUBLICA DE MALTA (Estado independiente) - Persona Jurídica |
| 55000004382 | ALEMANIA, REP. FED. - Persona Jurídica |
| 55000004390 | BIELORUSIA - Persona Jurídica |
| 55000004404 | ESTONIA - Persona Jurídica |
| 55000004412 | LETONIA - Persona Jurídica |
| 55000004420 | LITUANIA - Persona Jurídica |
| 55000004439 | MOLDOVA - Persona Jurídica |
| 55000004463 | BOSNIA HERZEGOVINA - Persona Jurídica |
| 55000004498 | ESLOVENIA - Persona Jurídica |
| 55000004900 | MACEDONIA - Persona Jurídica |
| 55000004919 | POS.BRITANICA (EUROPA) - Persona Jurídica |
| 55000004986 | INDETERMINADO (EUROPA) - Persona Jurídica |
| 55000004994 | AUSTRALIA - Persona Jurídica |
| 55000005036 | REPUBLICA DE NAURU (Estado independiente) - Persona Jurídica |
| 55000005044 | NUEVA ZELANDA - Persona Jurídica |
| 55000005052 | REPUBLICA DE VANUATU - Persona Jurídica |
| 55000005069 | SAMOA OCCIDENTAL - Persona Jurídica |
| 55000005079 | POS.AUSTRALIANA (OCEANIA) - Persona Jurídica |
| 55000005087 | POS.BRITANICA (OCEANIA) - Persona Jurídica |
| 55000005095 | POS.FRANCESA (OCEANIA) - Persona Jurídica |
| 55000005109 | POS.NEOCELANDESA (OCEANIA) - Persona Jurídica |
| 55000005117 | POS.E.E.U.U. (OCEANIA) - Persona Jurídica |
| 55000005125 | FIJI, ISLAS - Persona Jurídica |
| 55000005133 | PAPUA, ISLAS - Persona Jurídica |
| 55000005168 | KIRIBATI - Persona Jurídica |
| 55000005176 | TUVALU - Persona Jurídica |
| 55000005184 | ISLAS SALOMON - Persona Jurídica |
| 55000005192 | REINO DE TONGA (Estado independiente) - Persona Jurídica |
| 55000005206 | REPUBLICA DE LAS ISLAS MARSHALL (Estado independiente) - Persona Jurídica |
| 55000005214 | ISLAS MARIANAS - Persona Jurídica |
| 55000005907 | MICRONESIA ESTADOS FED. - Persona Jurídica |
| 55000005915 | PALAU - Persona Jurídica |
| 55000005982 | INDETERMINADO (OCEANIA) - Persona Jurídica |
| 55000006016 | RUSA, FEDERACION - Persona Jurídica |
| 55000006024 | ARMENIA - Persona Jurídica |
| 55000006032 | CROACIA - Persona Jurídica |
| 55000006040 | UCRANIA - Persona Jurídica |
| 55000006059 | CHECA, REPUBLICA - Persona Jurídica |
| 55000006067 | ESLOVACA, REPUBLICA - Persona Jurídica |
| 55000006520 | ANGUILA (Territorio no autónomo del Reino Unido) - Persona Jurídica |
| 55000006539 | ARUBA (Territorio de Países Bajos) - Persona Jurídica |
| 55000006547 | ISLAS DE COOK (Territorio autónomo asociado a Nueva Zelanda) - Persona Jurídica |
| 55000006555 | PATAU - Persona Jurídica |
| 55000006563 | POLINESIA FRANCESA (Territorio de Ultramar de Francia) - Persona Jurídica |
| 55000006598 | ANTILLAS HOLANDESAS (Territorio de Países Bajos) - Persona Jurídica |
| 55000006628 | ASCENCION - Persona Jurídica |
| 55000006636 | BERMUDAS (Territorio no autónomo del Reino Unido) - Persona Jurídica |
| 55000006644 | CAMPIONE D@ITALIA - Persona Jurídica |
| 55000006652 | COLONIA DE GIBRALTAR - Persona Jurídica |
| 55000006660 | GROENLANDIA - Persona Jurídica |
| 55000006679 | GUAM (Territorio no autónomo de los EEUU) - Persona Jurídica |
| 55000006687 | HONK KONG (Territorio de China) - Persona Jurídica |
| 55000006695 | ISLAS AZORES - Persona Jurídica |
| 55000006709 | ISLAS DEL CANAL:Guernesey,Jersey,Alderney,G.Stark,L.Sark,etc - Persona Jurídica |
| 55000006717 | ISLAS CAIMAN (Territorio no autónomo del Reino Unido) - Persona Jurídica |
| 55000006725 | ISLA CHRISTMAS - Persona Jurídica |
| 55000006733 | ISLA DE COCOS O KEELING - Persona Jurídica |
| 55000006768 | ISLA DE MAN (Territorio del Reino Unido) - Persona Jurídica |
| 55000006776 | ISLA DE NORFOLK - Persona Jurídica |
| 55000006784 | ISLAS TURKAS Y CAICOS (Territorio no autónomo del R. Unido) - Persona Jurídica |
| 55000006792 | ISLAS PACIFICO - Persona Jurídica |
| 55000006806 | ISLA DE SAN PEDRO Y MIGUELON - Persona Jurídica |
| 55000006814 | ISLA QESHM - Persona Jurídica |
| 55000006822 | ISLAS VIRGENES BRITANICAS(Territorio no autónomo de R.UNIDO) - Persona Jurídica |
| 55000006830 | ISLAS VIRGENES DE ESTADOS UNIDOS DE AMERICA - Persona Jurídica |
| 55000006849 | LABUAN - Persona Jurídica |
| 55000006857 | MADEIRA (Territorio de Portugal) - Persona Jurídica |
| 55000006865 | MONTSERRAT (Territorio no autónomo del Reino Unido) - Persona Jurídica |
| 55000006873 | NIUE - Persona Jurídica |
| 55000006903 | PITCAIRN - Persona Jurídica |
| 55000006938 | REGIMEN APLICABLE A LAS SA FINANCIERAS(ley 11.073 de la ROU) - Persona Jurídica |
| 55000006946 | SANTA ELENA - Persona Jurídica |
| 55000006954 | SAMOA AMERICANA (Territorio no autónomo de los EEUU) - Persona Jurídica |
| 55000006962 | ARCHIPIELAGO DE SVBALBARD - Persona Jurídica |
| 55000006970 | TRISTAN DA CUNHA - Persona Jurídica |
| 55000006989 | TRIESTE (Italia) - Persona Jurídica |
| 55000006997 | TOKELAU - Persona Jurídica |
| 55000007004 | ZONA LIBRE DE OSTRAVA (ciudad de la antigua Checoeslovaquia) - Persona Jurídica |
| 55000009988 | PARA PERSONAS FISICAS DE INDETERMINADO (CONTINENTE) - Persona Jurídica |
| 55000009996 | PARA PERSONAS FISICAS DE OTROS PAISES - Persona Jurídica |
## Novedades

Se recuerda que esta disponible el 
[grupo de noticias](http://www.pyafipws.com.ar) (http://groups.google.com.ar/group/pyafipws) donde
se publicarán futuras novedades sobre PyAfipWS: servicios web de
factura electrónica y sus interfases (se recomienda suscribirse)

## Costos y Condiciones

(ver [Condiciones del Soporte Comercial](wiki:PyAfipWs#CostosyCondiciones)).

**Importante**: WSFEXv1 es un **nuevo webservice** y AFIP ha agregado campos (bonificación), ha cambiado varios tipos de datos (en importes, cantidad de decimales), ha agregado códigos de tablas de parámetros (unidades de medida) y comprobantes asociados (remitos de tabaco) y además realiza nuevas validaciones, por lo que recomendamos probar exhaustivamente la interfaz con el desarrollo para exportación.

A su vez, se libera el código fuente bajo licencia GPL (software libre), al igual que se hizo con el restos de los servicios web. Para más detalles ver página FacturaElectronica.

MarianoReingart