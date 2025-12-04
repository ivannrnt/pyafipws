# Factura Crédito Electrónica MiPyMEs (RG4367) 
[[TracNav(noreorder|FacturaElectronica)]]

Interfaz para Servicio Web correspondiente al régimen Factura de Crédito Electrónica [Ley N° 27440](http://biblioteca.afip.gob.ar/dcp/LEY_C_027440_2018_05_09), reglamentado en el [Decreto 471/17](http://biblioteca.afip.gob.ar/dcp/DEC_C_000471_2018_05_17), e instrumentado según [RG 4367/2018](http://biblioteca.afip.gob.ar/dcp/REAG01004367_2018_12_19), sus modificatorias y complementarias. [RG4367/ 2018](http://www.afip.gov.ar/noticias/20181220-regimenFacturaCreditoElectronica.asp): [Factura de Crédito Electrónica](wiki:ProyectoWSFEv1#Importante:RG43672018FEv2.13).

| *En todas las operaciones comerciales en las que una Micro, Pequeña o Mediana Empresa esté obligada a emitir comprobantes electrónicos originales (factura o recibo) a una empresa grande, conforme las reglamentaciones que dicte la Administración Federal de Ingresos Públicos, entidad autárquica en el ámbito del Ministerio de Hacienda, se deberá emitir “Facturas de Crédito Electrónicas MiPyMEs”* |
|---|

## Índice
[[Image(htdocs:logo-pyafipws.png, align=right)]]
[[TOC(noheading,inline,depth=3)]]

## Descripción General

EL WSFECred (Web Service de Factura Electrónica de Crédito) es un nuevo Servicio Web de la AFIP para el 
*REGISTRO DE FACTURAS de CRÉDITO ELECTRÓNICA MiPyMEs.*, correspondiente a la 
Resolución [Resolución General 4367/2018](http://www.afip.gov.ar/fe/#rg)

**NOTA:** Ver grandes empresas [Listado-RFCE-Mi-PyMe.pdf](http://www.afip.gob.ar/facturadecreditoelectronica/documentos/Listado-RFCE-Mi-PyMe.pdf) y [Cronograma](http://www.afip.gob.ar/facturadecreditoelectronica/documentos/CRONOGRAMA-FCE.pdf) de aplicación

La AFIP publicó la [información técnica](http://www.afip.gob.ar/facturadecreditoelectronica/documentos/Manual_Desarrollador_WSFECRED_v1.0.3-rc1.pdf), el servicio WSFECred está disponible en homologación para realizar pruebas.


### Emisión de FCE

La [RG4367/ 2018](http://www.afip.gov.ar/noticias/20181220-regimenFacturaCreditoElectronica.asp) incorpora comprobantes *Factura de Crédito Electrónica*.

Para Emisión de Factura de Crédito Electrónicas ver el webservice tradicional WSFEv1: [RG4367/18 Factura de Crédito Electrónica MiPyMEs FEv2.13 FCE](wiki:ProyectoWSFEv1#Importante:RG43672018FEv2.13), donde se agregan:

- [WSFEv1.AgregarCmpAsoc](wiki:ManualPyAfipWs#M%C3%A9todosb%C3%A1sicosdeWSFEv1)
- [datos opcionales CBU](wiki:ManualPyAfipWs#DatosOpcionalesAFIPWSFEv1) 

AFIP publicó la [Especificación Técnica "FEv2.13"](http://www.afip.gob.ar/facturadecreditoelectronica/documentos/manual-desarrollador-COMPG-v2-13-Beta2.pdf) (manual para desarrolladores) con fecha 16 de Enero de 2019 AFIP, con las siguientes nuevos comprobantes:

- 201: Factura de Crédito Electrónica MiPyMEs (FCE) A
- 202: Nota de Débito Electrónica MiPyMEs (FCE) A
- 203: Nota de Crédito Electrónica MiPyMEs (FCE) A
- 206: Factura de Crédito Electrónica MiPyMEs (FCE) B
- 207: Nota de Débito Electrónica MiPyMEs (FCE) B
- 208: Nota de Crédito Electrónica MiPyMEs (FCE) B
- 211: Factura de Crédito Electrónica MiPyMEs (FCE) C
- 212: Nota de Débito Electrónica MiPyMEs (FCE) C
- 213: Nota de Crédito Electrónica MiPyMEs (FCE) C

Si se trata de emitir un comprobante tradicional pero corresponde FCE, la nueva validación es de AFIP lo impide: **10192: 1 - No es un comprobante valido bajo el Regimen de la Ley n. 27.440**

> *Según la categorización de las CUITs emisora y receptora y el monto facturado debe realizar una factura de crédito electrónica MiPyMEs (FCE). *
> *Ver micrositio http://www.afip.gob.ar/facturadecreditoelectronica/*

## Descargas
Ver archivos y últimas actualizaciones para descargas en [GitHub](https://github.com/reingart/pyafipws/releases) (actualizado):

- Instalador: 
- [PyAfipWs-2.7.2171-32bit+wsaa_2.11c+wsfev1_1.23c+wsfecred_1.05e-homo.exe](https://www.sistemasagiles.com.ar/soft/pyafipws/PyAfipWs-2.7.2171-32bit+wsaa_2.11c+wsfev1_1.23c+wsfecred_1.05e-homo.exe) para evaluación (WSFECred v1.03 Octubre 2019, incluyendo RG 4367 FCE Facturas de Crédito Electrónicas MiPyMEs Ley 27.440)
- [Manual de Uso](wiki:ManualPyAfipWs): Documentación ([PDF](http://www.sistemasagiles.com.ar/trac/wiki/ManualPyAfipWs?format=pdf))
- Código Fuente (Python): ver archivos publicados en [GitHub](https://github.com/reingart/pyafipws/blob/master/wsfecred.py) 

Para más información ver el [Manual de Uso](wiki:ManualPyAfipWs#Instalación)




## Ejemplos

Inicialización para Intefase COM en VB (5/6), VFP y similar:

```
#!vb

' Crear objeto interface Web Service de Factura Electrónica de Mercado Interno
Set WSFECred = CreateObject("WSFECred")
Debug.Print WSFECred.Version

' Setear tocken y sing de autorización (pasos previos)
WSFECred.Token = WSAA.Token
WSFECred.Sign = WSAA.Sign

' CUIT del emisor (debe estar registrado en la AFIP)
WSFECred.Cuit = "20267565393"

' Conectar al Servicio Web de Facturación
ok = WSFECred.Conectar() ' homologación

' Llamo a un servicio nulo, para obtener el estado del servidor (opcional)
WSFECred.Dummy
Debug.Print "appserver status", WSFECred.AppServerStatus
Debug.Print "dbserver status", WSFECred.DbServerStatus
Debug.Print "authserver status", WSFECred.AuthServerStatus
   
```

### Consultar Monto Obligado

Conocer la obligación respecto a la emisión o recepción de Facturas de Créditos:

```
#!vb

cuit_consultar = 30500010912
minimo = wsfecred.ConsultarMontoObligadoRecepcion(cuit_consultar)
print "Obligado:", wsfecred.Resultado
print "Monto Desde:", minimo
```

Salida de muestra:
```
Obligado: S
Monto Desde: 2000000
```

### Consultar Cuentas Corrientes

Obtener las cuentas corrientes que fueron generadas a partir de la facturación:

```
#!python

cuit_contraparte = 30999999999
rol = "Emisor"
ret = wsfecred.ConsultarCtasCtes(cuit_contraparte, rol)
print "Observaciones:", wsfecred.Obs
print "Cantidad de Ctas Ctes", ret

# leer primer cuenta corriente:
pos = 0
cc = wsfecred.LeerCtaCte(pos)

```

Salida de muestra:

```
{
 'cod_cta_cte': 12554,
 'cuit_emisor': 20267565393,
 'estado_cta_cte': 'Modificable',
 'fecha_hora_estado': "2019-06-19 16:17:36",
 'tipo_cbte': 201,
 'nro_cbte': 5,
 'punto_vta': 14,
 'importe_total_fc': 7440000.00,
 'saldo': 7440000.00,
 'saldo_aceptado': 0.00,
 'cod_moneda': 'PES',
}
{
 'cod_cta_cte': 2561,
 'cuit_emisor': 20267565393,
 'estado_cta_cte': 'Modificable',
 'fecha_hora_estado': "2019-05-13 09:25:32",
 'tipo_cbte': 201,
 'nro_cbte': 22,
 'punto_vta': 999,
 'importe_total_fc': 12850000.00,
 'saldo': 12850000.00,
 'saldo_aceptado': 0.00,
 'cod_moneda': 'PES',
}
```


### Aceptar Factura
```
#!python

' Establezco los valores de la factura a autorizar:

cuit_emisor = 30999999999
tipo_cbte = 201
punto_vta = 99
nro_cbte = 22

cod_moneda = "PES"
ctz_moneda_ult = 1
importe_cancelado = 1000.00
importe_embargo_pesos = 0.00
importe_total_ret_pesos = 0.00
saldo_aceptado = 1000.00
tipo_cancelacion = "TOT"

ok = wsfecred.CrearFECred(
        cuit_emisor, tipo_cbte, punto_vta, nro_cbte, cod_moneda, ctz_moneda_ult,
        importe_cancelado, importe_embargo_pesos, importe_total_ret_pesos,
        saldo_aceptado, tipo_cancelacion)

codigo = 2
descripcion = "Transferencia Bancaria"
ok = wsfecred.AgregarFormasCancelacion(codigo, descripcion)

' Aceptar Factura:
cae = WSFECred.AceptarFECred()

print "Resultado", WSFECred.Resultado
print "CodCtaCte", WSFECred.CodCtaCte
```

### Rechazar Factura

```
#!python

# indicar FCE a rechazar:

cuit_emisor = 30999999999
tipo_cbte = 201
punto_vta = 99
nro_cbte = 22

ok = wsfecred.CrearFECred(cuit_emisor, tipo_cbte, punto_vta, nro_cbte)

# indicar motivos:

cod_motivo = "6"
desc = "Falta de entrega"
justificacion = "prueba"

ok = wsfecred.AgregarMotivoRechazo(cod_motivo, desc, justificacion)

# invocar al webservice y obtener el respuesta:

ok = wsfecred.RechazarFECred()

print "Resultado", wsfecred.Resultado
print "CodCtaCte", wsfecred.CodCtaCte
```

### Consultar Comprobantes

```
#!python

# establecer filtros de búsqueda: (usar None/null para traer todos los valores)

cuit_contraparte = 30999999999
rol = "emisor"
fecha_desde = "2019-01-01"
fecha_hasta = "2019-12-31"
fecha_tipo = "Emision"
cod_tipo_cmp = 201
estado_cmp = "Recepcionado"  # "PendienteRecepcion", "Recepcionado", "Aceptado", "Rechazado", "InformadaAgDpto"
cod_cta_cte = None
estado_cta_cte = None        # "Modificable", "Aceptada", "Rechazada", "CanceladaTotal", "InformadaAgDpto"

ret = wsfecred.ConsultarComprobantes(cuit_contraparte, rol, fecha_desde, fecha_hasta, fecha_tipo,
                                     cod_tipo_cmp, estado_cmp, cod_cta_cte, estado_cta_cte)

print "Cantidad de comprobantes:", ret
print "Observaciones:", wsfecred.Obs

# leer resultados, ej para primer comprobante (pos=0):
pos = 0 
print wsfecred.LeerCampoComprobante(pos, 'cod_cta_cte')
print wsfecred.LeerCampoComprobante(pos, 'estado')

# lista de motivos de rechazo:
print wsfecred.LeerCampoComprobante(pos, 'motivos_rechazo', 0, 'cod_motivo')
print wsfecred.LeerCampoComprobante(pos, 'motivos_rechazo', 0, 'justificacion')

# incrementar pos para el siguiente registro
# lista de items, subtotales_iva, tributos y cbtes_asoc funcionan igual que lista de motivos de rechazo
```


Estructura de ejemplo con campos devueltos:
```
{
 'cod_cta_cte': 2392,
 'tipo_cbte': 203,
 'punto_vta': 999,
 'cbte_nro': 3,
 'cuit_emisor': 20267565393
 'cuit_receptor': 30999999999 
 'estado': 'Recepcionado',
 'tipo_cod_auto': 'E',
 'cod_autorizacion': 69203743197889, 
 'cbu_emisor': null,
 'cbu_pago': null,
 'alias_emisor': null,
 'razon_social_emi': 'REINGART MARIANO ALEJANDRO',
 'razon_social_recep': 'RECEPTOR',
 'fecha_emision': '2019-05-15',
 'fecha_hora_acep': null,
 'fecha_hora_estado': '2019-05-15 13:00',
 'fecha_info_ag_dpto_cltv': null,
 'fecha_puesta_dispo': '2019-05-15',
 'fecha_venc_acep': '2019-06-09',
 'fecha_venc_pago': null,
 'id_pago_ag_dpto_cltv': null,
 'imp_total': 1980.00
 'info_ag_dtpo_cltv': null,
 'leyenda_comercial': null,
 'tipo_acep': null,
 'moneda_ctz': 1
 'moneda_id': 'PES',
 'referencias_comerciales': [],
 'datos_comerciales': null
 'datos_generales': null
 'es_anulacion': 'N',
 'es_post_aceptacion': 'N',
 'motivos_rechazo': [{'desc': 'Falta de entrega', 
                      'justificacion': 'prueba',
                      'cod_motivo': 6}],
 'items': [{'orden': 1, 
            'ds': "articulo de prueba", 
            'codigo': "1234", 
            'umed': 7, 
            'cantidad': 1, 
            'precio': 1, 
            'importe': 12.10, 
            'importe_bonif': 0.00, 
            'ncm': null,
            'iva_id': 5, 
            'imp_iva': 2.10, 
            'u_mtx': null, 
            'cod_mtx': null,
            }],
 'subtotales_iva': [{'base_imp': 1500
                     'importe': 315
                     'iva_id': 5}],
 'tributos': [{'base_imp': 1500
               'detalle': 'PERCEPCION INGRESOS BRUTOS BA',
               'importe': 75
               'tributo_id': 2},
              {'base_imp': 1500
               'detalle': 'Percepcion IIBB CAPITAL',
               'importe': 90
               'tributo_id': 2}]}
 'cbtes_asoc': [{'cuit': 20267565393, 
                 'nro': 21, 
                 'pto_vta': 999,
                 'tipo': 201}],
}
```

## Herramienta por linea de comandos

Ejemplo:

```
WSFECRED_cli.exe --cargar --aceptar --trace --grabar
```

Resultado:

```
Resultado R
CodCtaCte None
Errores: [{'descripcion': u'No existe la cuenta corriente indicada', 'codigo': 1102}] []
hecho.
```

Utilizar `--prueba` para generar un archivo de entrada con datos ficticios.

Opciones principales:

- `--aceptar`: Acepta una FCE
- `--rechazar`: Rechaza una FCE
- `--rechazar-ndc`: Rechaza una N/C o N/D
- `--informar-cancelacion-total`: informa la cancelación total de una FEC

Opciones de consulta:

- `--obligado`: consultar monto obligado a recepcion de FEC (según CUIT, indicado como siguiente parámetro)
- `--ctasctes`: consultar cuentas corrientes generadas a partir de facturación (según cuit_contraparte)
- `--comprobantes`: consultar comprobantes (según cuit_contraparte)


## Formato Archivo de Intercambio

Muestras de Ejemplo:

- [attachment:wsfecred.json] para PHP y lenguajes modernos


Para COBOL y similares (archivo de texto de ancho fijo):

- [attachment:entrada_wsfecred.txt]
- [attachment:entrada_wsfecred.txt]

### encabezado

- Campo: tipo_reg             Posición:   1 Longitud:    1 Tipo: Numerico Valor: 0
- Campo: cuit_emisor          Posición:   2 Longitud:   11 Tipo: Numerico
- Campo: tipo_cbte            Posición:  13 Longitud:    3 Tipo: Numerico
- Campo: punto_vta            Posición:  16 Longitud:   11 Tipo: Numerico
- Campo: nro_cbte             Posición:  27 Longitud:    8 Tipo: Numerico
- Campo: cod_moneda           Posición:  35 Longitud:    3 Tipo: Alfanumerico
- Campo: ctz_moneda_ult       Posición:  38 Longitud:   18 Tipo: Importe Decimales: 6
- Campo: importe_cancelado    Posición:  56 Longitud:   17 Tipo: Importe Decimales: 2
- Campo: importe_embargo_pesos Posición:  73 Longitud:   17 Tipo: Importe Decimales: 2
- Campo: importe_total_ret_pesos Posición:  90 Longitud:   17 Tipo: Importe Decimales: 2
- Campo: saldo_aceptado       Posición: 107 Longitud:   17 Tipo: Importe Decimales: 2
- Campo: tipo_cancelacion     Posición: 124 Longitud:    3 Tipo: Alfanumerico
- Campo: resultado            Posición: 127 Longitud:    1 Tipo: Alfanumerico
- Campo: cod_cta_cte          Posición: 128 Longitud:   17 Tipo: Numerico
- Campo: obs                  Posición: 145 Longitud: 1000 Tipo: Alfanumerico
- Campo: err_code             Posición: 1145 Longitud:    6 Tipo: Alfanumerico
- Campo: err_msg              Posición: 1151 Longitud: 1000 Tipo: Alfanumerico

### formas_cancelacion

- Campo: tipo_reg             Posición:   1 Longitud:    1 Tipo: Numerico Valor: 1
- Campo: codigo               Posición:   2 Longitud:    5 Tipo: Numerico
- Campo: descripcion          Posición:   7 Longitud:  100 Tipo: Alfanumerico

### retenciones

- Campo: tipo_reg             Posición:   1 Longitud:    1 Tipo: Numerico Valor: 2
- Campo: cod_tipo             Posición:   2 Longitud:    5 Tipo: Numerico
- Campo: porcentaje           Posición:   7 Longitud:    5 Tipo: Importe
- Campo: importe              Posición:  12 Longitud:   17 Tipo: Importe
- Campo: desc_motivo          Posición:  29 Longitud:  250 Tipo: Alfanumerico

### ajuste_operacion

- Campo: tipo_reg             Posición:   1 Longitud:    1 Tipo: Numerico Valor: 3
- Campo: codigo               Posición:   2 Longitud:    5 Tipo: Numerico
- Campo: importe              Posición:   7 Longitud:   17 Tipo: Importe

### confirmar_nota_dc

- Campo: tipo_reg             Posición:   1 Longitud:    1 Tipo: Numerico Valor: 4
- Campo: cuit_emisor          Posición:   2 Longitud:   11 Tipo: Numerico
- Campo: tipo_cbte            Posición:  13 Longitud:    3 Tipo: Numerico
- Campo: punto_vta            Posición:  16 Longitud:   11 Tipo: Numerico
- Campo: nro_cbte             Posición:  27 Longitud:    8 Tipo: Numerico
- Campo: acepta               Posición:  35 Longitud:    1 Tipo: Alfanumerico

### motivo_rechazo

- Campo: tipo_reg             Posición:   1 Longitud:    1 Tipo: Numerico Valor: 5
- Campo: cod_motivo           Posición:   2 Longitud:    5 Tipo: Numerico
- Campo: desc                 Posición:   7 Longitud:  250 Tipo: Alfanumerico
- Campo: justificacion        Posición: 257 Longitud:  250 Tipo: Alfanumerico

## Tablas de Parámetros

Este nuevo servicio funciona con tablas dinámicas de parámetros para los códigos de tipos de ajuste, formas de cancelación, motivos de rechazo, retenciones. 
Estas tablas pueden sufrir modificaciones realizadas por la AFIP, con altas y bajas lógicas, por lo que tienen una fecha de vigencia (desde, hasta) y se proveen métodos para consultarlas por el mismo servicio web.

Como ejemplo, a continuación se copian los resultados de invocar a los webservices para consultar las tablas de parámetros al 9/7/2019 (homologación):

### Tipos de Comprobante
| 201 | Factura de Crédito electrónica MiPyMEs (FCE) A | 20181226 | NULL |
|---|---|---|---|
| 202 | Nota de Débito electrónica MiPyMEs (FCE) A | 20181226 | NULL |
| 203 | Nota de Crédito electrónica MiPyMEs (FCE) A | 20181226 | NULL |
| 206 | Factura de Crédito electrónica MiPyMEs (FCE) B | 20181226 | NULL |
| 207 | Nota de Débito electrónica MiPyMEs (FCE) B | 20181226 | NULL |
| 208 | Nota de Crédito electrónica MiPyMEs (FCE) B | 20181226 | NULL |
| 211 | Factura de Crédito electrónica MiPyMEs (FCE) C | 20181226 | NULL |
| 212 | Nota de Débito electrónica MiPyMEs (FCE) C | 20181226 | NULL |
| 213 | Nota de Crédito electrónica MiPyMEs (FCE) C | 20181226 | NULL |

### Tipos de Formas de Cancelación
| 1 | Compensación |
|---|---|
| 2 | Transferencia Bancaria |
| 3 | Cheque |
| 4 | Cesión |
| 5 | Otros medios de pago habilitados por el BCRA |

### Tipos de Ajuste
| 1 | Ajuste por diferencia de cambio |
|---|---|

### Tipos de Retenciones
| 1 | Retención por impuestos nacionales | 15 |
|---|---|---|
| 2 | Retención por impuestos provincias y ciudad autónoma de Bs As | 4 |
| 3 | Retención por impuestos de municipios | 1 |

### Tipos de Motivos de Rechazo
| 1 | Daño en las mercaderías, cuando no estuviesen expedidas o entregadas por su cuenta y riesgo. |
|---|---|
| 2 | Vicios, defectos y diferencias en la calidad o en la cantidad debidamente comprobados. |
| 3 | Divergencias en los plazos o en los precios estipulados. |
| 4 | No correspondencia con los servicios o la obra efectivamente contratados. |
| 5 | Existencia de vicios formales que causen su inhabilidad tanto como titulo ejecutivo y valor no cartular, así como documento comercial. |
| 6 | Falta de entrega de la mercadería o prestación del servicio. |

## Novedades

Se recuerda que esta disponible el 
[grupo de noticias](http://www.pyafipws.com.ar) (http://groups.google.com.ar/group/pyafipws) donde
se publicarán futuras novedades sobre PyAfipWS: servicios web de
factura electrónica y sus interfases (se recomienda suscribirse)

## Costos y Condiciones


Debido a la complejidad de este servicio, su fecha de aplicación y las modificaciones que pudieran surgir, ofrecemos horas de soporte técnico adicional (consultar) por 3 meses (ver [Condiciones del Soporte Comercial](wiki:PyAfipWs#CostosyCondiciones)).

Ofrecemos soporte técnico comercial (pago), independiente a la AFIP, desarrollos especiales, interfaces web, etc. 
Obtenga mas información enviando un mail a info@pyafipws.com.ar o (011) 4450-0716 / (011) 15-3048-9211 (asesoramiento sin cargo)

A su vez, se liberará el código fuente bajo licencia GPLv3 (software libre), al igual que se hizo con el restos de los servicios web. Para más detalles ver página FacturaElectronica.

La información de esta página es proporcionada a titulo informativo.

2019 © MarianoReingart
MarianoReingart