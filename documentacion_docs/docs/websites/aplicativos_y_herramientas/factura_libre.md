= Factura Libre: aplicación web para Factura Electrónica =
[[TracNav(noreorder|FacturaElectronica)]]


Aplicación web para la solicitud de CAE, generación y envío de Factura Electrónica (AFIP -Argentina), configurable y parametrizable, utilizando la interfaz PyAfipWs (software libre, código abierto - open source).

2010 © Mariano Reingart – Versión 1.25 – Julio 2010
[[Image(htdocs:logo-pyafipws.png, align=right)]]

## Índice
[[TOC(noheading,inline,depth=4)]]

## DEMO Online

"FacturaLibre" es una aplicación web (en web2py) para factura electrónica, utilizando la interfaz PyAfipWs y PyRECE (simil aplicativo SIAP), para brindar una alternativa libre a los servicios por clave fiscal de AFIP ("Comprobantes en Linea"), agregando nuevas funcionalidades, personalizaciones y mejoras requeridas por muchos clientes, que no están contempladas en la aplicación oficial (sobre todo para los nuevos webservices WSFE versión 1, RG2904 con y sin detalle). 

[[Image(PyFactura:aplicativo_factura_electronica_06a_w8.png,align=right,width=223,height=218,link=PyFactura)]]

Está disponible un sitio experimental de desarrollo para demostraciones preliminares:

http://www.sistemasagiles.com.ar/fe

**Importante**: ver PyFactura para aplicativo visual de facturación electrónica (ad-hoc: independiente y de fácil instalación)
## Características principales:

- Agilidad en la carga de datos por formularios web simples, editables y persistentes (sin pérdidas por expiración de sesión), sin limitaciones de cantidad de datos y textos
- Emisión de facturas electrónicas en PDF con formatos totalmente personalizables, incluyendo logos, múltiples líneas, páginación automática, código de barras, etc.
- Envío de notificaciones por correo electrónico y posibilidad de publicación de las facturas para consultas posteriores de los clientes
- Importación y exportación a múltiples formatos (texto simil RECE, planilla CSV, XML simil FacturadorPlus)
- Reportes avanzados: Libro IVA Ventas, detalles de artículos facturados, resúmenes varios, almacenamiento de duplicados electrónicos (RG1361)

## Webservices de AFIP contemplados

- Factura Electrónica Nacional (versión 0 y versión 1, con y sin detalle) (RG2485 y RG2904)
- Factura Electrónica Exportación (RG2758)
- Factura Electrónica Bono Fiscal (RG2557)

## Comprobantes Alcanzados

- Facturas, Notas de Crédito y Notas de Débito A, B y C (con y sin detalle)
- Facturas, Notas de Crédito y Notas de Débito E Comercio Exterior (con detalle)
- Facturas, Notas de Crédito y Notas de Débito A y B para Bono Fiscal (con detalle)

Todos los comprobantes pueden especificarse en moneda nacional (Peso) o moneda extranjera (Dólar, Euro, etc.).

## Sujetos Alcanzados

- Régimen Obligatorio (RECE)
- Régimen Optativo (RECE)
- Contributentes Notificados

## Soporte Comercial

Si necesita asesoramiento, demostración, capacitación, consultoría técnica, ofrecemos Soporte Comercial Pago y abonos de mantenimiento mensuales (opcional).
Comunicarse a [mailto:facturalibre@sistemasagiles.com.ar] o telefónicamente al 15-3048-9211

MarianoReingart
MarianoReingart