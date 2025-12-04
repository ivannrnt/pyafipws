# Código de Autorización Electrónica Anticipado (RG2926/RG2904)
[[TracNav(noreorder|FacturaElectronica)]]

Interfaz para los Servicios Web correspondientes a Factura Electrónica de Mercado Interno para el *Régimen especial de emisión y almacenamiento electrónico de comprobantes originales. Factura electrónica. Res. Gral. A.F.I.P. 2.485/08. Código de Autorización Electrónico Anticipado CAEA.* previstos en RG 2926/2010 y en la RG 2904/2010.

## Índice
[[Image(htdocs:logo-pyafipws.png, align=right)]]
[[TOC(noheading,inline,depth=3)]]

## Descripción General

El régimen de CAE Anticipado consiste en consignar en los comprobantes respaldatorios de las operaciones, el Código de Autorización Electrónico Anticipado "CAEA", en reemplazo del "CAE" 

Los sujetos comprendidos deben reunir las siguientes condiciones:
 a. "Autoimpresores" comprendidos en el Registro Fiscal de Imprentas, dispuesto por la RG 100
 b. Incluidos en el régimen de factura electrónica (RG 2485), o nominados (RG 2904)
 c. Dada la magnitud de sus sistemas tengan dificultades con la modalidad de CAE * 
 d. Emitir un mínimo de 1800 comprobantes por mes *

La modalidad CAEA es soportada por dos webservices:

- [WSFEv1](wiki:ProyectoWSFEv1)(Web Service de Factura Electrónica Versión 1) (RG2485), correspondiente a la  Resolución [Resolución General 2904/2010](http://www.afip.gov.ar/fe/#rg) Art.4 Opción B, 
- [WSMTXCA](wiki:FacturaElectronicaMTXCAService) (Web Service de Factura Electrónica con detalle) (RG2904), correspondiente a la  Resolución [Resolución General 2904/2010](http://www.afip.gov.ar/fe/#rg) Art.4 Opción A, 

La operatoria es similar a la modalidad CAE, con la salvedad que se debe solicitar un único código CAEA para todas las facturas de la quincena, informando posteriormente cada factura emitida de manera individual con el CAEA.

Cada quincena se identifica por un período (año mes, ej: '201102') y orden (1: primer quincena, 2: segunda quincena).
El CAEA debe solicitarse antes de que comienze la quincena, y los comprobantes deben informarse dentro de los 30 días corridos.
Si no se han emitido comprobantes con CAEA en dicho período, debe informarse sin movimiento. 

Los CAEA se validan por el servicio interactivo de AFIP:
http://www.afip.gob.ar/genericos/consultaCAEA/

La información de cada factura deberá suministrarse dentro de los TREINTA (30) días corridos contados desde el día inmediato siguiente al de finalización de cada período, pudiendo enviarse a partir del día inmediato siguiente al de comienzo de cada período. 

Entrada en vigencia:

- 27 de Octubre de 2010: Autoimpresores - CAE Anticipado [RG 2926](http://biblioteca.afip.gob.ar/dcp/reag01002926_2010_09_24)

## Descargas e Instalación

Ver la información respectiva a cada webservice:

- [WSFEv1](wiki:ProyectoWSFEv1)
- [WSMTXCA](wiki:FacturaElectronicaMTXCAService)

## Ejemplo Intefase COM en VB (5/6)

### CAEA sin detalle (WSFEv1)

Ver ejemplos completos en [wsfev1_caea.bas](https://github.com/reingart/pyafipws/blob/master/ejemplos/wsfev1/wsfev1_caea.bas)
Para más información ver [Documentación](wiki:ManualPyAfipWs#ServicioWebdeFacturaElectrónicaMercadoInternoVersión1WSFEv1) y [WSFEv1](wiki:ProyectoWSFEv1)

#### Conexión inicial (ver autenticación con WSAA)
```
#!vb

' Crear objeto interface Web Service de Factura Electrónica de Mercado Interno
Set WSFEv1 = CreateObject("WSFEv1")
Debug.Print WSFEv1.version

' Setear tocken y sing de autorización (pasos previos)
WSFEv1.Token = WSAA.Token
WSFEv1.Sign = WSAA.Sign

' CUIT del emisor (debe estar registrado en la AFIP)
WSFEv1.Cuit = "20267565393"

' Conectar al Servicio Web de Facturación
ok = WSFEv1.Conectar() ' homologación
```

#### PASO 1: Solicito CAE Anticipado para el período/orden

```
#!vb

' NOTA: solicitar por única vez para un determinado período
' consultar si se ha solicitado previamente

periodo = "201102"  ' Año y mes
orden = "2"         ' Segunda Quincena

' consulto CAEA ya solicitado
CAEA = WSFEv1.CAEAConsultar(periodo, orden)
If CAEA = "" Then
    ' solicito nuevo CAEA
    CAEA = WSFEv1.CAEASolicitar(periodo, orden)
End If

MsgBox "Periodo: " & periodo & " Orden " & orden & vbCrLf & _
       "CAEA: " & CAEA & vbCrLf & _
       "Obs:" & WSFEv1.Obs & vbCrLf & _
       "Errores:" & WSFEv1.ErrMsg

```

#### PASO 2: Informar una factura emitida con CAEA

```
#!vb

' PASO 2: Establezco los valores de la factura a informar:
tipo_cbte = 6
punto_vta = 4005
cbte_nro = WSFEv1.CompUltimoAutorizado(tipo_cbte, punto_vta)
fecha = Format(Date, "yyyymmdd")
concepto = 1
tipo_doc = 80: nro_doc = "33693450239"
cbte_nro = clng(cbte_nro) + 1
cbt_desde = cbte_nro: cbt_hasta = cbte_nro
imp_total = "122.00": imp_tot_conc = "0.00": imp_neto = "100.00"
imp_iva = "21.00": imp_trib = "1.00": imp_op_ex = "0.00"
fecha_cbte = fecha: fecha_venc_pago = ""
' Fechas del período del servicio facturado (solo si concepto = 1?)
fecha_serv_desde = "": fecha_serv_hasta = ""
moneda_id = "PES": moneda_ctz = "1.000"

' creo una factura (con CAEA)
ok = WSFEv1.CrearFactura(concepto, tipo_doc, nro_doc, tipo_cbte, punto_vta, _
    cbt_desde, cbt_hasta, imp_total, imp_tot_conc, imp_neto, _
    imp_iva, imp_trib, imp_op_ex, fecha_cbte, fecha_venc_pago, _
    fecha_serv_desde, fecha_serv_hasta, _
    moneda_id, moneda_ctz, CAEA)

' Agrego los comprobantes asociados (solo nc/nd)
If tipo_cbte <> 1 And tipo cbte <> 6 Then 
    tipo = 19
    pto_vta = 2
    nro = 1234
    ok = WSFEv1.AgregarCmpAsoc(tipo, pto_vta, nro)
End If
    
' Agrego impuestos varios
id = 99
Desc = "Impuesto Municipal Matanza'"
base_imp = "100.00"
alic = "1.00"
importe = "1.00"
ok = WSFEv1.AgregarTributo(id, Desc, base_imp, alic, importe)

' Agrego tasas de IVA
id = 5 ' 21%
base_im = "100.00"
importe = "21.00"
ok = WSFEv1.AgregarIva(id, base_imp, importe)

' Informo comprobante emitido con CAE anticipado:
cae = WSFEv1.CAEARegInformativo()

MsgBox "Resultado:" & WSFEv1.Resultado & _
       " CAE: " & cae & _
       " Venc: " & WSFEv1.Vencimiento & _
       " Obs: " & WSFEv1.Obs, vbInformation + vbOKOnly
```

**Nota:** La metodología es similar al resto de los webservices, y se trato de mantener similitud con el código existente:

- Método WSFEv1.!CrearFactura es similar a WSFE.Authorize (parámetros similares), con la salvedad que incluye el CAEA
- Método WSFEv1.!AgregarCmpAsoc es similar a WSFEX.!AgregarCmpAsoc
- Propiedades similares: WSFEv1.CAE, WSFEv1.Resultado, etc.


### CAEA con detalle (WSMTXCA)

Ver ejemplos completos en [wsmtx_caea.bas](https://github.com/reingart/pyafipws/blob/master/ejemplos/wsmtxca/wsmtx_caea.bas).
Para más información ver [Documentación](wiki:ManualPyAfipWs#ServicioWebdeFacturaElectrónicaMercadoInternoProgramaMatrixWSMTXCA) y [WSMTXCA](wiki:FacturaElectronicaMTXCAService)
#### Conexión inicial (ver autenticación con WSAA)
```
#!vb

' Crear objeto interface Web Service de Factura Electrónica de Mercado Interno
Set WSMTXCA = CreateObject("WSMTXCA")
Debug.Print WSMTXCA.version

' Setear tocken y sing de autorización (pasos previos)
WSMTXCA.Token = WSAA.Token
WSMTXCA.Sign = WSAA.Sign

' CUIT del emisor (debe estar registrado en la AFIP)
WSMTXCA.Cuit = "20267565393"

' Conectar al Servicio Web de Facturación
ok = WSMTXCA.Conectar() ' homologación
```

#### PASO 1: Solicito CAE Anticipado para el período/orden

```
#!vb

' NOTA: solicitar por única vez para un determinado período
' consultar si se ha solicitado previamente

periodo = "201104"  ' Año y mes
orden = "2"         ' Segunda Quincena

' consulto CAEA ya solicitado
CAEA = WSMTXCA.ConsultarCAEA(periodo, orden)
If CAEA = "" Then
    ' solicito nuevo CAEA
    CAEA = WSMTXCA.SolicitarCAEA(periodo, orden)
End If

MsgBox "Periodo: " & periodo & " orden " & orden & vbCrLf & _
       "CAEA: " & CAEA & vbCrLf & _
       "Obs:" & WSMTXCA.Obs & vbCrLf & _
       "Errores:" & WSMTXCA.ErrMsg

```

#### PASO 2: Informar una factura emitida con CAEA

```
#!vb

' PASO 2: Establezco los valores de la factura a informar:
tipo_cbte = 1
punto_vta = 4000
cbte_nro = WSMTXCA.CompUltimoAutorizado(tipo_cbte, punto_vta)
fecha = Format(Date, "yyyy-mm-dd")
vencimiento = Format(Date + 5, "yyyy-mm-dd")
concepto = 3
tipo_doc = 80: nro_doc = "30000000007"
cbte_nro = CLng(cbte_nro) + 1
cbt_desde = cbte_nro: cbt_hasta = cbte_nro
imp_total = "122.00": imp_tot_conc = "0.00": imp_neto = "100.00"
imp_trib = "1.00": imp_op_ex = "0.00": imp_subtotal = "100.00"
fecha_cbte = fecha: fecha_venc_pago = fecha
' Fechas del período del servicio facturado (solo si concepto = 1?)
fecha_serv_desde = fecha: fecha_serv_hasta = fecha
moneda_id = "PES": moneda_ctz = "1.000"
Obs = "Observaciones Comerciales, libre"

' Creo internamente la estructura de datos para la factura
ok = WSMTXCA.CrearFactura(concepto, tipo_doc, nro_doc, tipo_cbte, punto_vta, _
    cbt_desde, cbt_hasta, imp_total, imp_tot_conc, imp_neto, _
    imp_subtotal, imp_trib, imp_op_ex, fecha_cbte, fecha_venc_pago, _
    fecha_serv_desde, fecha_serv_hasta, _
    moneda_id, moneda_ctz, Obs, CAEA, vencimiento)

' Agrego los comprobantes asociados (opcional):
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
base_im = "100.00"
importe = "21.00"
ok = WSMTXCA.AgregarIva(id, base_imp, importe)

u_mtx = 123456
cod_mtx = "1234567890"
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
ok = WSMTXCA.AgregarItem(u_mtx, cod_mtx, codigo, ds, qty, _
            umed, precio, bonif, cod_iva, imp_iva, imp_subtotal)
ok = WSMTXCA.AgregarItem(u_mtx, cod_mtx, "DESC", "Descuento", 0, _
            "99", 0#, 0, cod_iva, "-21.00", "-121.00")

' Informo comprobante emitido con CAE anticipado:
cae = WSMTXCA.InformarComprobanteCAEA()

MsgBox "Resultado:" & WSMTXCA.Resultado & _
       " CAE: " & cae & _
       " Venc: " & WSMTXCA.Vencimiento & _
       " Obs: " & WSMTXCA.Obs, vbInformation + vbOKOnly
```


## Novedades

Se recuerda que esta disponible el 
[grupo de noticias](http://www.pyafipws.com.ar) (http://groups.google.com.ar/group/pyafipws) donde
se publicarán futuras novedades sobre PyAfipWS: servicios web de
factura electrónica y sus interfases (se recomienda suscribirse)

## Costos y Condiciones


Debido a la complejidad de este servicio, su fecha de aplicación y las modificaciones que pudieran surgir, los clientes que asi lo requieran pueden adquirir horas de soporte técnico adicional, se recomienda consultar previamente (ver [Condiciones del Soporte Comercial](wiki:PyAfipWs#CostosyCondiciones)).

Ofrecemos soporte técnico comercial (pago), independiente a la AFIP, desarrollos especiales, interfaces web, etc. 
Obtenga mas información enviando un mail a info@pyafipws.com.ar o (011) 4450-0716 / (011) 15-3048-9211 (asesoramiento sin cargo)

A su vez, se liberará el código fuente bajo licencia GPLv3 (software libre), al igual que se hizo con el restos de los servicios web. Para más detalles ver página FacturaElectronica.

La información de esta página es proporcionada a titulo informativo.

2008-2010 © MarianoReingart
MarianoReingart
MarianoReingart