= Consulta de Operaciones Cambiarias - Compra de Divisas (RG3210/2011) =

[[TracNav(noreorder|FacturaElectronica)]]

Interfaz para Servicio Web Código de Operaciones Cambiarias (WSCOC) correspondiente a la [Resolución General N° 3210](http://www.afip.gov.ar/genericos/novedades/rg3210.asp), donde AFIP implementó el Programa de Consulta de Operaciones Cambiarias, a fin de controlar en tiempo real la situación fiscal y económico-financiera de quien realiza compras de moneda extranjera (dólar, euro, real, etc.)

Mediante el webservice se puede consultar cuál es el resultado de la evaluación sistémica que realizó la AFIP, previamente a realizar la compra, similar al servicio con Clave Fiscal, Nivel de Seguridad 2, denominado "Consulta de Operaciones Cambiarias".

El servicio web permite realizar la consulta para personas físicas/jurídicas (buscando los CUIT para determinado tipo y número de documento) y para turistas extranjeros.

Las entidades autorizadas a operar en cambios por el Banco Central de la República Argentina deberán consultar y registrar, el importe en pesos del total de cada una de las operaciones cambiarias, en el momento en que se efectúe la misma

Se encuentran alcanzadas las operaciones de venta de moneda extranjera -divisas o billetes- en todas sus modalidades, cualquiera sea su finalidad o destino.


## Índice
[[Image(htdocs:logo-pyafipws.png, align=right)]]
[[TOC(noheading,inline,depth=2)]]

## Introducción

Biblioteca para el WSCOC permite automatizar la gestión de las solicitudes de compra de divisas (operaciones cambiarias): 

- Interfaz COM: Simil DLL/OCX, embebible para aplicaciones programadas en lenguajes visuales bajo windows (Visual Basic, Visual Fox Pro, SAP, etc.)
- Interfaz por archivo de texto: similar a aplicativos SIAP para sistemas legados (ej. RM COBOL) multiplataforma (DOS, Windows, Unix) -proximamente-
- Interfaz por tablas DBF: compatible con dBase, !FoxPro, Clipper -proximamente-
- Interfaz por base de datos: compatible con conectores ODBC (MS SQL Server), PostgreSQL y otros (Oracle, DB2) -proximamente-

Cubre totalmente el proceso, puede ser adaptado a programas existentes y no es requerido intervención del usuario.

Para más información ver PyAfipWs

**IMPORTANTE**: Este servicio web es *restringido* por AFIP, disponible solo a Casas de Cambio y Entidades Financieras.

**Novedades**: La Actualización 1.05b incluye soporte para **WSCOC v2.1** Consulta de Operaciones Cambiarias - Compra de Divisas (RG3210/2011 modificada 27/03/2012)

## Descargas

- Instalador: [instalador-WSCOC-1.09a-homo.exe](https://www.sistemasagiles.com.ar/soft/pyafipws/PyAfipWs-2.7.2080-32bit+wsaa_2.11c+wscoc_1.09a-homo.exe) (homologación)
- Documentación Oficial: [WSCOCv2.1](http://www.afip.gov.ar/ws/WSCOC/ManualDelDesarrollador_WSCOC_v2_1.pdf)
- Ejemplo en VB: [wscoc.bas](https://github.com/reingart/pyafipws/blob/master/ejemplos/wscoc/wscoc.bas)
- Código Fuente (Python): [wscoc.py](https://github.com/reingart/pyafipws/blob/master/wscoc.py)

## Métodos

- **`GenerarSolicitudCompraDivisa(cuit_comprador, codigo_moneda, cotizacion_moneda, monto_pesos, cuit_representante, codigo_destino, [djai, codigo_excepcion_djai,djas, codigo_excepcion_djas, tipo_referencia, codgio_referencia])`**: Generar una solicitud de Operación Cambiaria
- **`InformarSolicitudCompraDivisa(codigo_solicitud, nuevo_estado)`**: Informar la aceptación o desistir de una solicitud generada con anterioridad.
- **`AnularCOC(coc, cuit_comprador)`**: Anular un COC
- **`ConsultarCOC(coc)`**:Consultar un COC determinado
- **`ConsultarCUIT(numero_doc, tipo_doc)`**: Consultar para un determinado tipo y número de documente, la CUIT/CDI/CUIL asociada
- **`ConsultarSolicitudCompraDivisa(codigo_solicitud)`**: Consultar una solicitud determina.
- **`ConsultarSolicitudesCompraDivisas(cuit_comprador, estado_solicitud, fecha_emision_desde, fecha_emision_hasta,)`**: Consultar Solicitudes generados dentro de un rango de fechas, para un determinado comprador o estado, según el parámetro ingresado
- **`LeerSolicitudConsultada()`**: recorre los datos devueltos por la búsqueda de `ConsultarSolicitudesCompraDivisas`
- **`ConsultarDJAI(djai, cuit)`**: Consultar Declaración Jurada Anticipada de Importación. Establece DJAI, Monto FOB, Codigo Moneda, Estado DJAI
- **`ConsultarDJAS(djas, cuit)`**: Consultar Declaración Jurada Anticipada de Servicios. Establece DJAS, Monto FOB, Codigo Moneda, Estado DJAS
- **`ConsultarDestinosCompra()`**: lista los Tipos de Destinos de compra de divisas.
- **`ConsultarMonedas()`**: lista los Tipos de Monedas
- **`ConsultarTiposDocumento()`**: lista los Tipos de Documentos
- **`ConsultarTiposEstadoSolicitud()`**: lista los Tipos de estados de una solicitud
- **`ConsultarMotivosExcepcionDJAI()`**: lista el universo de motivos de excepciones a la Declaración Jurada Anticipada de Importación
- **`ConsultarDestinosCompraDJAI()`**: lista el subconjunto de los destinos de compra de divisas alcanzados por las normativas de la Declaración Jurada Anticipada de Importación
- **`ConsultarMotivosExcepcionDJAS()`**: lista el universo de motivos de excepciones a la Declaración Jurada Anticipada de Servicios
- **`ConsultarDestinosCompraDJAS()`**: lista el subconjunto de los destinos de compra de divisas alcanzados por las normativas de la Declaración Jurada Anticipada de Servicios
- **`ConsultarTiposReferencia()`**: lista los Tipos de Documentos
- **`ConsultarDestinosCompraTipoReferencia(tipo)`**: lista el subconjunto de los destinos de compra de divisas alcanzados por el tipo de referencia
- **`ConsultarReferencia(tipo, codigo)`**: devuelve los datos de una referencia según su tipo (1: DJAI, 2: DJAS, 3: DJAT)
 
## Atributos

Propiedades principales retornadas por el WSCOC:

- `Resultado`: `"A"`: Aprobado, `"O"`: Observado, `"R"`: Rechazado o `"E"`: Error
- `EstadoSolicitud`: `"OT"`: Otorgado, `"CO"`: Confirmado, `"DC"`: Desistido por el Cliente, `"DB"`: Desistido por el Banco o la Entidad Financiera, `"AN"`: Anulado, `"CA"`: Cancelado o `"RE"`: Rechazado
- `CodigoSolicitud`: código de la solicitud de cambio (entero `long`)
- `FechaSolicitud`: fecha y hora de la solicitud
- `COC`: número de consulta (12 dígitos enteros)
- `FechaEmisionCOC`: fecha y hora de la consulta de operación de cambio
- `CodigoDestino`: ver tabla (abajo)
- `FechaEstado`: fecha y hora del último cambio de estado
- `CUITComprador` y `DenominacionComprador`
- `CodigoMoneda`: según tabla, 1 para Dólar EEUU (ver abajo)
- `CotizacionMoneda`: tipo de cambio usada para la operación (10 dígitos, 4 enteros, 6 decimales)
- `MontoPesos`: importe de la operación (15 dígitos, 13 enteros y 2 decimales)
- `CUITRepresentante` y `DenominacionRepresentante`
- `DJAS`, `DJAI`: códigos de Declaración Jurada Anticipada de Servicios / Importación

Propiedades secundarias del WSCOC:

- `TipoDoc`, `NumeroDoc`: parametros consultados por `ConsultarCUIT`
- `CUITConsultada` y `DenominacionConsultada`: parametros devueltos por `LeerCUITconsultados`
- `CodigoMoneda`, `MontoFOB`, `DJAS`, `DJAI`, `EstadoDJAS`, `EstadoDJAI`: establecidos por `ConsultarDJAI` y `ConsultarDJAS`
- `Tipo`, `Codigo`, `Estado`, `MontoFOB`: datos devueltos de referencias (DJAI, DJAS, DJAT)

Validaciones:

- `Excepcion`: errores excepcionales, por ej., pasar un dato alfanumérico en un campo numérico (!SoapFault)
- `Errores`: lista de validaciones de negocio, por ej: '10500: Número de solicitud inválido, inexistente o no corresponde a la entidad'
- `ErroresFormato`: lista de validaciones según los tipos de datos definidos, por ej: "cvc-enumeration-valid:  El valor 'ER' no está incluído en la lista '[CO, DC, DB]'. Debe tener un valor de la lista.", "cvc-type.3.1.3:  El valor 'ER' del elemento 'nuevoEstado' no es válido."
- `Inconsistencias`: lista de validaciones de negocio que no implican la no generación de la solicitud (a nivel de rechazo), por ej. por problemas en el domicilio fiscal

## Ejemplo Intefase COM en VB (5/6)

Consulta de CUITs para un Tipo y Número de Documento:
```
#!vb
nro_doc = 99999999
tipo_doc = 96
cuits = WSCOC.ConsultarCUIT(nro_doc, tipo_doc)
' recorro el detalle de los cuit devueltos:
While WSCOC.LeerCUITConsultado():
    Debug.Print "CUIT", WSCOC.CUITConsultada
    Debug.Print "Denominación", WSCOC.DenominacionConsultada
Wend
```

Solicitud de Operación de Cambio:
```
#!vb

' Genero una solicitud de operación de cambio
cuit_comprador = "20267565393"
codigo_moneda = "1"
cotizacion_moneda = "4.26"
monto_pesos = "100"
cuit_representante = None
codigo_destino = 625
ok = WSCOC.GenerarSolicitudCompraDivisa(cuit_comprador, codigo_moneda, _
                        cotizacion_moneda, monto_pesos, _
                        cuit_representante, codigo_destino)

If HuboErrores(WSCOC) Then End

Debug.Print 'Resultado', WSCOC.Resultado
Debug.Print 'COC', WSCOC.COC
Debug.Print "FechaEmisionCOC", WSCOC.FechaEmisionCOC
Debug.Print 'CodigoSolicitud', WSCOC.CodigoSolicitud
Debug.Print "EstadoSolicitud", WSCOC.EstadoSolicitud
Debug.Print "FechaEstado", WSCOC.FechaEstado
Debug.Print "DetalleCUITComprador", WSCOC.CUITComprador, WSCOC.DenominacionComprador
Debug.Print "CodigoMoneda", WSCOC.CodigoMoneda
Debug.Print "CotizacionMoneda", WSCOC.CotizacionMoneda
Debug.Print "MontoPesos", WSCOC.MontoPesos
Debug.Print "CodigoDestino", WSCOC.CodigoDestino

      
' Informar la aceptación o desistir una solicitud generada con anterioridad
COC = WSCOC.COC
codigo_solicitud = WSCOC.CodigoSolicitud
' "CO": confirmar, o "DC" (desistio cliente) "DB" (desistio banco)
nuevo_estado = "CO"
ok = WSCOC.InformarSolicitudCompraDivisa(codigo_solicitud, nuevo_estado)

If HuboErrores(WSCOC) Then End

Debug.Print 'Resultado', WSCOC.Resultado
Debug.Print 'COC', WSCOC.COC
Debug.Print "EstadoSolicitud", WSCOC.EstadoSolicitud

' para pruebas, anulo la solicitud de cambio
ok = WSCOC.AnularCOC(COC, cuit_comprador)

If HuboErrores(WSCOC) Then End

Debug.Print 'Resultado', WSCOC.Resultado
Debug.Print 'COC', WSCOC.COC
Debug.Print "EstadoSolicitud", WSCOC.EstadoSolicitud
      
' consulto para verificar el estado
ok = WSCOC.ConsultarSolicitudCompraDivisa(codigo_solicitud)

If HuboErrores(WSCOC) Then End

Debug.Print 'CodigoSolicitud', WSCOC.CodigoSolicitud
Debug.Print "EstadoSolicitud", WSCOC.EstadoSolicitud
                 
```

Consulto todas las operaciones realizadas:
```
#!vb
cuit_comprador = Null
estado_solicitud = Null
fecha_emision_desde = "2011-11-01"
fecha_emision_hasta = "2011-11-30"
sols = WSCOC.ConsultarSolicitudesCompraDivisas(cuit_comprador, _
                                     estado_solicitud, _
                                     fecha_emision_desde, _
                                     fecha_emision_hasta)

If HuboErrores(WSCOC) Then End

' muestro los resultados de la búsqueda
Debug.Print "Solicitudes consultadas:"
For Each sol In sols:
    Debug.Print "Código de Solicitud:", sol
    ' podría llamar a WSCOC.ConsultarSolicitudCompraDivisa
Next
Debug.Print "hecho."

' recorro y leeo el detalle de las solicitudes devueltas
While WSCOC.LeerSolicitudConsultada():
    Debug.Print "----------------------------------------"
    Debug.Print 'COC', WSCOC.COC
    Debug.Print "FechaEmisionCOC", WSCOC.FechaEmisionCOC
    Debug.Print 'CodigoSolicitud', WSCOC.CodigoSolicitud
    Debug.Print "EstadoSolicitud", WSCOC.EstadoSolicitud
    Debug.Print "FechaEstado", WSCOC.FechaEstado
    Debug.Print "DetalleCUITComprador", WSCOC.CUITComprador, WSCOC.DenominacionComprador
    Debug.Print "CodigoMoneda", WSCOC.CodigoMoneda
    Debug.Print "CotizacionMoneda", WSCOC.CotizacionMoneda
    Debug.Print "MontoPesos", WSCOC.MontoPesos
    Debug.Print "CodigoDestino", WSCOC.CodigoDestino
    Debug.Print "========================================"
Wend

```

Verificación de errores:
```
#!vb
Function HuboErrores(WSCOC)
    ' Analizo errores (realizar luego de cada método)
    ' devuelvo False si no hubo error
    HuboErrores = False
    For Each er In WSCOC.Errores:
        Debug.Print "Error:", er
        MsgBox er, vbExclamation, "Error General AFIP"
        HuboErrores = True
    Next
    For Each er In WSCOC.ErroresFormato:
        Debug.Print "Error Formato:", er
        MsgBox er, vbExclamation, "Error Formato AFIP"
        HuboErrores = True
    Next
    For Each er In WSCOC.Inconsistencias:
        Debug.Print "Inconsistencia:", er
        MsgBox er, vbExclamation, "Inconsistencia AFIP"
        HuboErrores = True
    Next
End Function
```

Para más información ver [ejemplo completo en Visual Basic](http://pyafipws.googlecode.com/hg/ejemplos/wscoc/wscoc.bas)

## Tablas de Parámetros

### Tipos de Estado Solicitud
| **Código** | **Descripción** |
|---|---|
| OT | Otorgada - pendiente de ser Consumida o Desistida |
| CO | Consumida |
| DB | Desistida por el Banco |
| DC | Desistida por el Contribuyente |
| AN | Anulada |
| CA | Cancelada |
| RE | Rechazda |
### Monedas
| **Código** | **Descripción** |
|---|---|
| 1 | Dólar ESTADOUNIDENSE |
| 2 | Dólar EEUU LIBRE |
| 3 | FRANCOS FRANCESES |
| 4 | LIRAS ITALIANAS |
| 5 | PESETAS |
| 6 | MARCOS ALEMANES |
| 7 | FLORINES HOLANDESES |
| 8 | FRANCOS BELGAS |
| 9 | FRANCOS SUIZOS |
| 10 | PESOS MEJICANOS |
| 11 | PESOS URUGUAYOS |
| 12 | REAL  (Brasil) |
| 13 | ESCUDOS PORTUGUESES |
| 14 | CORONAS DANESAS |
| 15 | CORONAS NORUEGAS |
| 16 | CORONAS SUECAS |
| 17 | CHELINES AUTRIACOS |
| 18 | Dólar CANADIENSE |
| 19 | YENS |
| 21 | LIBRA ESTERLINA |
| 22 | MARCOS FINLANDESES |
| 23 | BOLIVAR VENEZOLANO |
| 24 | CORONA CHECA |
| 25 | DINAR (YUGOSLAVO) |
| 26 | Dólar AUSTRALIANO |
| 27 | DRACMA (GRIEGO) |
| 28 | FLORIN (ANTILLAS HOLANDESAS) |
| 29 | GUARANI PARAGUAYO |
| 30 | SHEKEL (ISRAEL) |
| 31 | PESO BOLIVIANO |
| 32 | PESO COLOMBIANO |
| 33 | PESO CHILENO |
| 34 | RAND (SUDAFRICANO) |
| 35 | NUEVO SOL PERUANO |
| 36 | SUCRE (ECUATORIANO) |
| 40 | LEI RUMANOS |
| 41 | DERECHOS ESPECIALES DE GIRO |
| 42 | PESOS DOMINICANOS |
| 43 | BALBOAS PANAMEÑAS |
| 44 | CORDOBAS NICARAGÛENSES |
| 45 | DIRHAM MARROQUÍES |
| 46 | LIBRAS EGIPCIAS |
| 47 | RIYALS SAUDITAS |
| 48 | BRANCOS BELGAS FINANCIERAS |
| 49 | GRAMOS DE ORO FINO |
| 50 | LIBRAS IRLANDESAS |
| 51 | Dólar DE HONG KONG |
| 52 | Dólar DE SINGAPUR |
| 53 | Dólar DE JAMAICA |
| 54 | Dólar DE TAIWAN |
| 55 | QUETZAL (GUATEMALTECOS) |
| 56 | FORINT (HUNGRIA) |
| 57 | BAHT (TAILANDIA) |
| 58 | ECU |
| 59 | DINAR KUWAITI |
| 60 | EURO |
| 61 | ZLTYS POLACOS |
| 62 | RUPIAS HINDÚES |
| 63 | LEMPIRAS HONDUREÑAS |
| 64 | YUAN (Rep. Popular de China) |
| 80 | PESOS |
| 100 | OTRAS MONEDAS |
### Tipos de Destinos de Compra

| **Tipo** | **Descripción** |
|---|---|
| ME | Mercancias |
| SE | Servicios |
| RE | Rentas |
| CA | Capital |
| OT | Otros |

### Destinos de Compra
| **Tipo** | **Código** | **Descripción** |
|---|---|---|
| ME | 153 | Pagos de deudas comerciales por importaciones de bienes sin registro de ingreso aduanero. |
| ME | 154 | Pagos a la vista de importaciones de bienes con registro de ingreso aduanero. |
| ME | 155 | Pagos a la vista de importaciones de bienes sin registro de ingreso aduanero. |
| ME | 156 | Pagos anticipados de importaciones de bienes. |
| ME | 157 | Pagos de deudas comerciales por importaciones de bienes con registro de ingreso aduanero. |
| ME | 158 | Compra de libros por particulares |
| ME | 159 | Otras compras de bienes de particulares |
| ME | 160 | Cancelaciones de prefinanciaciones de exportaciones, descuentos y otras financiaciones otorgadas por cobros de exportaciones en divisas de convenio |
| ME | 161 | Pagos al exterior de deudas contraídas por la venta de bienes en tiendas libres de impuestos |
| ME | 163 | Pagos al exterior por compras de mercaderías no ingresadas al país y vendidas a terceros países. |
| ME | 164 | Devoluciones al exterior de cobros de exportaciones de bienes exportados bajo el régimen de precios FOB sujetos a una determinación posterior al momento de registro de dicha operación (precios revisables), por resultar el precio definitivo inferior al cobrado al cliente. |
| ME | 165 | Importaciones temporarias sin giro de divisas que se cancelan con una destinación de exportación a consumo bajo los subregímenes EC03, EG03 o EC04. |
| ME | 166 | Pagos de deudas por importaciones de bienes con anterioridad a la fecha de vencimiento. |
| ME | 167 | Bonificaciones pagadas al exterior por problemas de calidad de la mercadería exportada. |
| ME | 168 | Otras bonificaciones. |
| ME | 169 | Boletos técnicos por faltantes, mermas y deficiencias según la Comunicación "A" 4025 y Complementarias |
| ME | 170 | Cancelación de prefinanciaciones de exportaciones con aplicación de divisas de anticipos de clientes |
| ME | 171 | Cancelación de garantías comerciales de entidades financieras de importaciones de bienes sin registro de ingreso aduanero. |
| ME | 172 | Cancelación de garantías comerciales de entidades financieras de importaciones de bienes con registro de ingreso aduanero. |
| SE | 610 | Fletes de importación ganados por buques |
| SE | 611 | Fletes de importación ganados por aeronaves |
| SE | 612 | Fletes de importación ganados por medios terrestres |
| SE | 613 | Otros fletes |
| SE | 614 | Pasajes Ganados por buques y aeronaves |
| SE | 615 | Pasajes ganados por empresas de transporte terrestre |
| SE | 616 | Gastos en el exterior de buques, aeronaves y medios de transporte terrestre |
| SE | 617 | Arrendamiento de buques, aeronaves y medios terrestres |
| SE | 618 | Arrendamiento de contenedores, espacios o depósitos en puertos |
| SE | 619 | Seguros de importaciones |
| SE | 620 | Pagos de siniestros. |
| SE | 621 | Otras primas de seguros |
| SE | 622 | Primas de redescuentos en el exterior |
| SE | 623 | Servicios de Comunicaciones |
| SE | 624 | Servicios de Construcción |
| SE | 625 | Otros servicios de información e informática. |
| SE | 626 | Gastos médicos |
| SE | 627 | Patentes y marcas |
| SE | 628 | Regalías |
| SE | 629 | Derechos de autor |
| SE | 630 | Primas por préstamos de jugadores |
| SE | 631 | Servicios empresariales profesionales y técnicos |
| SE | 632 | Comisiones bancarias y otros servicios financieros |
| SE | 633 | Gastos por operaciones bancarias |
| SE | 634 | Servicios personales culturales y recreativos |
| SE | 635 | Turismo y viajes |
| SE | 636 | Comisiones Comerciales |
| SE | 637 | Recaudaciones consulares. |
| SE | 638 | Remesas de embajadas, consulados y otras representaciones oficiales. |
| SE | 639 | Gastos de embajadas, consulados y otras representaciones oficiales. |
| SE | 640 | Gastos de inscripción y concurrencia a ferias y exposiciones internacionales |
| SE | 641 | Pago y amortización de contratos globales por obras y servicios |
| SE | 642 | Extracción y legalización de partidas de nacimiento, bautismo, casamiento y defunción. |
| SE | 643 | Compra / Suscripción a diarios y revistas del exterior |
| SE | 644 | Gastos de representaciones bancarias y comerciales |
| SE | 645 | Cuotas de afiliación a asociaciones internacionales |
| SE | 646 | Devolución de impuestos a turistas no residentes |
| SE | 647 | Gastos en el exterior de servicios técnicos y profesionales |
| SE | 648 | Aportes de residentes para la organización de congresos o convenciones internacionales en el exterior. |
| SE | 649 | Primas de reaseguros en el exterior. |
| SE | 650 | Pagos de recuperos a reaseguradores del exterior. |
| SE | 651 | Alquiler de maquinarias, herramientas y otros bienes muebles. |
| SE | 652 | Pagos de garantías comerciales por exportaciones de bienes y servicios. |
| SE | 653 | Gastos por cancelación de orden de compra |
| SE | 655 | Pagos por contratos globales para la modernización de aeronaves y buques |
| SE | 656 | Devoluciones al exterior de fondos ingresados al país para la atención de gastos en el país de buques, aeronaves y medios de transporte terrestre. |
| SE | 657 | Gastos originados por acciones sometidas a consideración de Tribunales de Arbitraje Internacionales. |
| SE | 658 | Servicios de información de agencias de noticias internacionales. |
| SE | 659 | Derechos de explotación de películas, vídeo y audio extranjeros. |
| SE | 660 | Servicios por transferencia de tecnología por Ley 22.426 (excepto patentes y marcas) |
| RE | 744 | Pagos de intereses al exterior por deudas. |
| RE | 745 | Utilidades y dividendos pagados al exterior |
| RE | 747 | Otras rentas pagadas al exterior |
| RE | 748 | Renta pagada a entidades financieras locales por descuento de créditos de exportaciones y otros créditos locales |
| RE | 749 | Remuneraciones y/o sueldos de trabajadores. |
| RE | 750 | Alquiler o arrendamiento de inmuebles ubicados en el país de propiedad de no residentes. |
| CA | 801 | Pagos de deudas financieras con el exterior originadas en importaciones de bienes |
| CA | 802 | Devolución al exterior de anticipos de exportaciones no cumplidas |
| CA | 803 | Devolución de prefinanciaciones de exportaciones no cumplidas al exterior |
| CA | 839 | Repatriación de inversiones en inmuebles en el país de no residentes. |
| CA | 840 | Compras de billetes en moneda extranjera para destino específico. Punto 2.4 de la Com. "A" 5085 |
| CA | 841 | Compras de billetes en moneda extranjera para destino específico. Punto 2.5 de la Com. "A" 5085 |
| CA | 842 | Cancelación de financiaciones externas de empresas controlantes para proyectos de infraestructura fondeados por agencias oficiales de crédito |
| CA | 843 | Compra de billetes en moneda extranjera por transferencias negociadas inciso b) Art. 26 de la Ley 26.476 |
| CA | 844 | Operaciones de Caja de Valores por servicios de títulos valores en custodia R. D. nº 307/05 |
| CA | 847 | Aportes de inversiones directas en el exterior de residentes |
| CA | 848 | Préstamos de organismos internacionales |
| CA | 849 | Préstamos de agencias oficiales de crédito |
| CA | 850 | Préstamos garantizados por agencias oficiales de crédito |
| CA | 851 | Préstamos financieros de hasta 1 año de plazo |
| CA | 852 | Préstamos financieros de más de 1 año de plazo |
| CA | 855 | Préstamos otorgados a no residentes |
| CA | 856 | Compra para tenencia de billetes extranjeros en el país |
| CA | 857 | Repatriación de inversiones de portafolio en el país de no residentes. |
| CA | 858 | Garantías financieras |
| CA | 859 | Inversiones inmobiliarias en el exterior |
| CA | 860 | Inversiones de portafolio en el exterior de personas físicas (2) |
| CA | 861 | Otras inversiones en el exterior de residentes |
| CA | 862 | Inversiones de portafolio en el exterior de personas jurídicas( 2) |
| CA | 863 | Cancelaciones de operaciones de pase con entidades financieras del exterior |
| CA | 864 | Pagos por contratos de cobertura entre monedas extranjeras o de tasa de interés |
| CA | 865 | Pagos por contratos de cobertura de precios de commodities |
| CA | 867 | Cancelación de deudas con el exterior por emisión de cheques de viajero |
| CA | 868 | Compra de cheques de viajero. |
| CA | 869 | Amortizaciones de préstamos financieros punto 2.1. de la Comunicación "A" 3843 y Complementarias. |
| CA | 870 | Constitución de Fondos Fiduciarios para refinanciaciones de deudas con el exterior. |
| CA | 871 | Amortizaciones de capital correspondientes a deudas financieras punto 2.2. de la Comunicación "A" 3880 y Complementarias. |
| CA | 872 | Pagos por cancelación de contratos de futuros de cambio. |
| CA | 873 | Venta por instrucción judicial de fondos para la constitución de depósitos judiciales en moneda extranjera. |
| CA | 874 | Inversiones de portafolio en el exterior para la reestructuración de deudas con acreedores externos |
| CA | 876 | Compra de moneda extranjera para su entrega a la entidad en pago de financiaciones locales |
| CA | 877 | Otras repatriaciones de inversiones directas en el país de no residentes. |
| CA | 878 | Cancelación de líneas de crédito otorgadas a bancos locales por entidades financieras del exterior |
| CA | 879 | Inversiones de portafolio de Fondos Comunes de Inversión |
| CA | 880 | Compra de billetes de Fondos Comunes de Inversión |
| CA | 881 | Inversiones de portafolio en el exterior para la atención de vencimientos de servicios de deudas con acreedores externos. |
| CA | 882 | Extinción de obligaciones contingentes por descuentos de créditos por exportaciones en el exterior |
| CA | 883 | Devolución de financiaciones por descuentos de créditos por exportaciones |
| CA | 884 | Pagos por contratos de cobertura de DIVA |
| CA | 885 | Compra de entidades financieras de títulos valores emitidos por residentes liquidados contra cable. |
| CA | 886 | Compra de entidades financieras de títulos valores emitidos por residentes liquidados contra cuentas bancarias locales en moneda extranjera |
| CA | 887 | Adquisición por parte de entidades financieras locales de créditos otorgados a residentes por entidades financieras del exterior. |
| CA | 888 | Compra de moneda extranjera para la constitución de depósitos Decreto Nº 616/2005 |
| CA | 890 | Inversiones de portafolio en el exterior para la atención de pagos de importaciones |
| CA | 891 | Suscripción primaria de las entidades financieras de títulos en moneda extranjera del BCRA |
| CA | 892 | Compras de moneda extranjera para afectación a proyectos de inversión |
| CA | 893 | Suscripción primaria de entidades financieras de valores del Gobierno Nacional emitidos en moneda extranjera |
| CA | 894 | Suscripción primaria de entidades financieras de bonos del sector privado emitidos en moneda extranjera |
| CA | 895 | Compra de moneda extranjera para la suscripción primaria de títulos públicos emitidos por el Gobierno Nacional |
| CA | 896 | Inversiones de portafolio en el exterior para la atención de pagos de importaciones. |
| CA | 897 | Inversiones de portafolio en el exterior para la atención de pagos de utilidades y dividendos. |
| CA | 898 | Inversiones de portafolio en el exterior para la atención de pagos de inversiones directas en el exterior. |
| CA | 899 | Devolución de aportes irrevocables a inversores del exterior. |
| OT | 900 | Inversiones directas en el exterior de residentes (Comunicación "A" 4669) |
| OT | 962 | Becas y gastos de estudios |
| OT | 963 | Ayuda familiar |
| OT | 964 | Jubilaciones y pensiones |
| OT | 965 | Aportes a cajas de jubilaciones del exterior |
| OT | 966 | Constitución de garantías requeridas por mercados autorregulados sujetos al control de la Comisión Nacional de Valores, destinadas a la operatoria de contratos de futuros y opciones. |
| OT | 967 | Devoluciones al emisor de cupones de bonos públicos nacionales |
| OT | 969 | Compra por canjes con representaciones diplomáticas y consulares, organismos internacionales y otro personal diplomático acreditado en el país. |
| OT | 970 | Pagos de gastos y derechos exigibles a la importación en el país de destino por ventas realizadas bajo condición DDP. |
| OT | 971 | Devolución al exterior de fondos utilizados para depósitos judiciales por no residentes. |
| OT | 972 | Donaciones |
| OT | 973 | Compra de activos no financieros no producidos |
| OT | 974 | Venta de billetes para su entrega a través de entidades financieras a buques y aeronaves para la atención de gastos en el exterior |
| OT | 975 | Utilización de margen por pagos anticipados y a la vista de importaciones de bienes (Comunicación "A" 4605 y complementarias) |
| OT | 976 | Otros gastos consulares por importaciones argentinas |
| OT | 977 | Retenciones impositivas efectuadas en el país de destino sobre cobros de exportaciones de bienes |
| OT | 978 | Fondos transferidos al exterior por residentes para la constitución de depósitos judiciales |
| OT | 981 | Operaciones de organismos internacionales, representaciones diplomáticas y consulares, misiones especiales, etc.(Comunicación "A" 5239 Punto 1a) |
| OT | 982 | Operaciones de gobiernos locales (Comunicación "A" 5239 Punto 1b) |
| OT | 983 | Operaciones de empleados de gobiernos locales no integrados al Sistema Integrado Previsional Argentino - SIPA (Comunicación "A" 5239 Punto 1 segundo párrafo) |
| OT | 984 | Operaciones de personas físicas por préstamos hipotecarios para la compra de vivienda (Comunicación "A" 5239 Punto 1c incorporado por la Comunicación "A" 5240 ) |
| OT | 985 | Operaciones de cambio en concepto de turismo y viajes a no residentes (Comunicación "A" 5241) |
| OT | 986 | Operaciones de personas físicas por fondos resultantes del cobro de jubilaciones y pensiones percibidas del exterior (Comunicación "A" 5239 Punto 1d incorporado por la Comunicación "A" 5242 ) |
### Tipos de Documento
| **Código** | **Descripción** |
|---|---|
| 0 | C.I.CAPITAL FEDERAL |
| 1 | C.I.BUENOS AIRES |
| 2 | C.I.CATAMARCA |
| 3 | C.I.CORDOBA |
| 4 | C.I.CORRIENTES |
| 5 | C.I.ENTRE RIOS |
| 6 | C.I.JUJUY |
| 7 | C.I.MENDOZA |
| 8 | C.I.LA RIOJA |
| 9 | C.I.SALTA |
| 10 | C.I.SAN JUAN |
| 11 | C.I.SAN LUIS |
| 12 | C.I.SANTA FE |
| 13 | C.I.SGO.DEL ESTERO |
| 14 | C.I.TUCUMAN |
| 16 | C.I.CHACO |
| 17 | C.I.CHUBUT |
| 18 | C.I.FORMOSA |
| 19 | C.I.MISIONES |
| 20 | C.I.NEUQUEN |
| 21 | C.I.LA PAMPA |
| 22 | C.I.RIO NEGRO |
| 23 | C.I.SANTA CRUZ |
| 24 | C.I.TIERRA DEL FUEGO |
| 30 | CERTIFICADO DE MIGRACIÓN |
| 40 | C.I.PAIS LIMITROFE |
| 88 | USADO POR ANSES PARA PADRÓN |
| 89 | LIBRETA CIVICA |
| 90 | LIBRETA DE ENROLAMIENTO |
| 91 | C.I.EXTRANJERA |
| 92 | EN TRAMITE |
| 93 | ACTA DE NACIMIENTO |
| 94 | PASAPORTE |
| 95 | C.I.BS.AS.R.N.P. |
| 96 | DOC.NACIONAL DE IDENTIDAD |
| 98 | D.N.I. (N° MÚLTIPLE) |
| 99 | INDETERMINADO |

### Motivos Excepcion DJAI
| 1 | Régimen de Reimportación |
|---|---|
| 2 | Régimen de Importación o Exportación para compensar envíos de mercaderías con  deficiencias |
| 3 | Régimen de Donaciones |
| 4 | Régimen de Muestras |
| 5 | Régimen de Franquicias Diplomáticas |
| 6 | Importación de mercaderías con franquicias de derechos y tributos |
| 7 | Régimen de Courier |
| 8 | Régimen de envíos postales |
| 9 | Envíos escalonados aprobados con anterioridad al 1 de febrero de 2012 |
| 10 | Planta llave en mano aprobadas con anterioridad al 1 de febrero de 2012 |
| 11 | Excepción Artículo 3° R.G. AFIP 3255 |
| 99 | Otros Subregímenes de Importación no Alcanzados por RG 3255 |
### Destinos Compra DJAI
| 153 | Pagos de deudas comerciales por importaciones de bienes sin registro de ingreso aduanero. |
|---|---|
| 154 | Pagos a la vista de importaciones de bienes con registro de ingreso aduanero. |
| 155 | Pagos a la vista de importaciones de bienes sin registro de ingreso aduanero. |
| 156 | Pagos anticipados de importaciones de bienes. |
| 157 | Pagos de deudas comerciales por importaciones de bienes con registro de ingreso aduanero. |
| 166 | Pagos de deudas por importaciones de bienes con anterioridad a la fecha de vencimiento. |
| 171 | Cancelación de garantías comerciales de entidades financieras de importaciones de bienes sin registro de ingreso aduanero. |
| 172 | Cancelación de garantías comerciales de entidades financieras de importaciones de bienes con registro de ingreso aduanero. |
| 801 | Pagos de deudas financieras con el exterior originadas en importaciones de bienes |
### Motivos Excepcion DJAS
| 1 | Operación No Alcanzada RG 3276 - Monto Mínimo |
|---|---|
### Destinos Compra DJAS
| 625 | Otros servicios de información e informática. |
|---|---|
| 627 | Patentes y marcas |
| 628 | Regalías |
| 629 | Derechos de autor |
| 630 | Primas por préstamos de jugadores |
| 631 | Servicios empresariales profesionales y técnicos |
| 634 | Servicios personales culturales y recreativos |
| 652 | Pagos de garantías comerciales por exportaciones de bienes y servicios. |
| 659 | Derechos de explotación de películas, vídeo y audio extranjeros. |
| 660 | Servicios por transferencia de tecnología por Ley 22.426 (excepto patentes y marcas) |
| 747 | Otras rentas pagadas al exterior |
| 973 | Compra de activos no financieros no producidos |
## Novedades

Se recuerda que esta disponible el 
[grupo de noticias](http://www.pyafipws.com.ar) (http://groups.google.com.ar/group/pyafipws) donde
se publicarán futuras novedades sobre PyAfipWS: servicios web de
factura electrónica y sus interfases (se recomienda suscribirse)

## Costos y Condiciones

Por soporte comercial consultar al (011) 15-3048-9211 o por mail a info@sistemasagiles.com.ar

Más información en PyAfipWs

MarianoReingart
MarianoReingart