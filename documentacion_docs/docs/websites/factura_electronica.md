# Factura Electrónica
[[TracNav(noreorder|FacturaElectronica)]]

Aquí encontrará novedades y actualizaciones sobre los temas de emisión y almacenamiento electrónico de comprobantes originales:
Servicios Web de AFIP (wsaa, wsfe, wsbfe web services);
Factura electrónica en Argentina (segun RG 1956/05, RG 1361/02, RG 1345/02, RG 2265/07, RG 2289/07, RG 2177/06, RG 2485/08, 2557/09, 2758/10, RG2757/10, RG2904/10, RG2975/10, RG2959/10, RG2853/10, RG2926/10, RG3067/11, RG3536/13, RG3571/13, RG3668/14, RG3689/14, etc.);
Interfase con otros lenguajes y miscelaneas (PyAfipWs, PyRece)

[[Image(htdocs:logo-pyafipws.png)]] 
## Menú
- Documentación Componentes y Herramientas Generales: 
- [PyAfipWs](wiki:PyAfipWs): Interfase simil [OCX](wiki:OcxFacturaElectronica) con otros lenguajes (VB, VFP, Cobol ...) [Costos y Condiciones](wiki:PyAfipWs#CostosyCondiciones)
- [Manual](wiki:ManualPyAfipWs): Documentación,  [Información Importante](wiki:ManualPyAfipWs#Importante:leerprimeroantesdecomenzar), [Certificados](wiki:ManualPyAfipWs#Certificados), [Errores Frecuentes](wiki:ManualPyAfipWs#ErroresFrecuentes)
- [Herramienta "universal"](wiki:ManualPyAfipWs#InterfaseporarchivosdetextosímilSIAP-RECE): archivos de intercambio TXT Cobol, DBF dBase/!FoxPro, JSON PHP/Java
- [PyFEPDF](wiki:ManualPyAfipWs#PyFEPDF:generadordePDFdefacturaselectrónicas): Generador de [Factura Electrónica](wiki:FacturaElectronica) en formato PDF
- Factura Electrónica - Servicios Web AFIP:
- [Mercado Interno](wiki:ProyectoWSFEv1): Factura Electrónica A/B/C/M WSFEv1+ (RG2485/2757/3067/3571/3668/3749/4004)
- [Matrix (codificación productos)](wiki:FacturaElectronicaMTXCAService): Factura Electrónica A/B con detalle (RG2904/3536)
- [Bienes de Capital](wiki:BonosFiscales): Bonos Fiscales Electrónicos - Factura Electrónica A (RG2557)
- [Exportación](wiki:FacturaElectronicaExportacion): Factura Electrónica E Exportadores (RG2758 RG3689)
- [Turismo](wiki:FacturaElectronicaComprobantesTurismo): Comprobantes Factura Electrónica T WSCT CAE/CAEA (RG3971) ** Nuevo! **
- Código de Autorización Electrónico Anticipado [CAEA](wiki:FacturaElectronicaCAEAnticipado)
- Agropecuario - Servicios web AFIP:
- [Código Trazabilidad de Granos](wiki:CodigoTrazabilidadGranos): Transporte de granos WSCTGv4 (RG2806 RG3113 RG3493)
- [Liquidación y Certificación de Granos](wiki:LiquidacionPrimariaGranos): WSLPGv1.17 F. C1116 A / B / RT (RG3419 RG3690 RG3691)  
- [Liquidación de Tabaco Verde](wiki:LiquidacionTabacoVerde): WSLTVv1.3 ** ¡Actualizado! **
- [Liquidación Única Mensual Lechería](wiki:LiquidacionUnicaMensualLecheria): WSLUMv1.3 
- [Liquidación Sector Pecuario](wiki:LiquidacionSectorPecuario): Hacienda, Compra directa, Carne WSLSPv1.3
- [Remito Electrónico Cárnico](wiki:RemitoElectronicoCarnico):a WSRemCarne (RG4256/18 y RG4303/18) ** ¡Nuevo! **
- Otros webservices y utilidades AFIP
- [Constatación de Comprobantes](wiki:ConstatacionComprobantes) CAI, CAE, CAEA (WSCDC) 
- [Padron Contribuyentes AFIP](wiki:PadronContribuyentesAFIP): Constancia de Inscripción RG1817/2005 WS-SR-Padron ** Nuevo! **
- [Consulta de Operaciones Cambiarias](wiki:ConsultaOperacionesCambiarias): Compra de Divisas (WSCOC) 
- Webservices provinciales: ARBA (Prov. Bs.As.), AGIP (C.A.B.A), API (Sta.Fe), DGR (Córdoba):
- [Remito Electrónico](wiki:RemitoElectronicoCotArba): COT Código de Operaciones de Translado (ARBA, API, AGIP, DGR) 
- [Ingresos Brutos](wiki:IngresosBrutosArba): Consulta de alícuotas WS DFE IIBB ARBA
- SNT: Sistema Nacional de Trazabilidad ANMAT, SEDRONAR, SENASA
- [Trazabilidad de Medicamentos](wiki:TrazabilidadMedicamentos): ANMAT Disposición 3683/2011  
- [Trazabilidad de Productos Médicos](wiki:TrazabilidadProductosMedicos): ANMAT Disposición 2303/2014 y 2175/14 ** ¡Nuevo! **
- [Trazabilidad de Precursores Químicos](wiki:TrazabilidadPrecursoresQuimicos): RENPRE SEDRONAR Resolución 900/12
- [Trazabilidad de Productos Fitosanitarios](wiki:TrazabilidadProductosFitosanitarios): SENASA Resolución 369/13
- Aplicativos Genéricos y Herramientas Avanzadas:
- [PyRece](wiki:PyRece): Aplicativo visual simil SIAP - RECE (CSV, PDF, Email)
- [FE.py](wiki:HerramientaFacturaElectronica): Herramienta universal, unificada e integrada
- [FacturaLibre](wiki:FacturaLibre): Aplicacion online (web2py)
- [PyFactura](wiki:PyFactura) Aplicativo visual y simple (gui2py) para CAE y PDF factura electrónica
- [LibPyAfipWs](wiki:LibPyAfipWs): [DllFacturaElectronica Biblioteca DLL] para lenguajes C / C++ y similares
- [Factura Electrónica en Python](wiki:FacturaElectronicaPython): Información Técnica (SOAP, XML, PDF, DBF, etc.)


**Importante**: Ver [Preguntas Frecuentes generales](wiki:FacturaElectronica#PreguntasFrecuentes) abajo.

## Interfase con otros Lenguajes
Hemos desarrollado una interface COM autoinstalable para windows compatible con otros lenguajes (Visual Basic, Visual Fox Pro, Delphi, PHP, .Net, Java, etc.) y una interfase por línea de comando ("DOS") - archivo de texto simil SIAP/RECE para lenguajes que no soporten la creación de objetos COM (algunas versiones de COBOL y Fox Pro). DLL/EXE de automatización COM similar a OCX/ActiveX (ver [ventajas](wiki:OcxFacturaElectronica)). Software libre de código abierto, incorporable a sistemas propietarios (ver [PyAfipWs#CostosyCondiciones condiciones]).

Más información en PyAfipWs (ejemplos, documentación, demo e Información sobre soporte comercial)

También disponible para Python (Windows o Linux): ver FacturaElectronicaPython

También puede utilizarse de lenguajes que soporten JSON (por ej. PHP, tanto en Windows como Linux): ver [factura_electronica.php](https://github.com/reingart/pyafipws/blob/master/ejemplos/factura_electronica.php)

Código fuente y ejemplos totalmente publicados y disponibles gratuitamente en el sitio de [GitHub](https://github.com/reingart/pyafipws) (licenciado bajo GPLv3)

## Aplicativo Ad-Hoc
Hemos desarrollado un aplicativo (ejecutable con interfase "visual") para windows/linux (multiplataforma), que autoriza, genera pdf y envía los mais con facturas electrónicas (de manera libre y gratis).

Más información en PyRece

## Factura electrónica por Web, FTP o Email
Paralelamente disponemos de un servicio de facturación por página web, protocolo FTP o correo electrónico, para ambientes o plataformas donde no es viable incorporar bibliotecas o interfaces externas (por ej. mainframes, AS/400, sistemas de facturación legados, etc.).
Consultar [facturaelectronica@sistemasagiles.com.ar]()

----
## Novedades
Inscribirse a [Grupo de Noticias en Google](http://groups.google.com.ar/group/pyafipws) para recibir información sobre actualizaciones y eventos:
### Importadores, Turismo y Proveedores del Estado
La AFIP ha incluido nuevos sujetos obligados a realizar Factura Electrónica, cuya entrada en vigencia es:

 1. Importadores (RG2975): a partir del 1/1/2011
 1. Actividad turística y hotelera (RG2959): a partir del 1/1/2011
 1. Proveedores del Sector Público Nacional (RG2853): a partir del 1/11/2010

Nuestra interfaz PyAfipWs ya soporta los webservices actuales (WSFE, WSFEv1 y WSMTXCA) para autorizar estos tipos de comprobantes.
### Nuevo servicio Web Mercado Interno (WSFEv1 - WSMTXCA)
Nuevo servicio web de factura electrónica en el mercado interior
(WSFEv1, WSMTXCA), que extiende la Resolución General 2485 (RG2757, RG2904)
con las siguientes características:

 1. Detalle de factura: concepto, alícuotas de IVA, tributos, moneda, comprobantes asociados, etc.
 2. CAEA: CAE Anticipado ("simil autoimpresores") RG2926/10

Estamos en proceso de desarrollar una nueva versión de nuestra
interfaz PyAfipWs para poder comunicarse con este nuevo servicio web
(WSFEv1, MTX) utilizando estas nuevas modalidades.

Por favor consultar via email (info@pyafipws.com.ar) para mayor información y
coordinación de pruebas (homologación).

Ver [Proyecto Factura Electrónica Versión 1](wiki:ProyectoWSFEv1) para estado y ejemplos.
### Código de Trazabilidad de Granos
Disponemos de la implementación para el servicio web código de trazabilidad de granos (transporte de granos) para solicitar y confirmar el CTG, según la Resolución General 2806/2010. Ver CodigoTrazabilidadGranos 
### Facturas de Exportación
Tenemos desarrollada la implementación para el servicio web para facturas de exportación (comercio exterior) según la Resolución General 2758/2010. Ver FacturaElectronicaExportacion 
### Seguros de caución (pólizas)
Estamos desarrollando la interfaz para *Operaciones por servicios de otorgamiento de pólizas de seguros de caución (RG 2668)*.
Interesados por favor comunicarse a [mailto:facturaelectronica@sistemasagiles.com.ar]

Para mantenerse informados, recomendamos inscribirse al [Grupo de Noticias](http://groups.google.com.ar/group/pyafipws)
Interesados por favor comunicarse a [mailto:facturaelectronica@sistemasagiles.com.ar]
## Capacitación
Participamos en conferencias y eventos de software libre:

 1. Taller en Conferencia Internacional de Software Libre 2014: [Workshops](http://cislargentina.org/workshops/)
 1. Curso en la ACP: **[2010](http://www.clubdeprogramadores.com/cursos/CursoMuestra.php?Id=600)** [2009](http://www.clubdeprogramadores.com/cursos/CursoMuestra.php?Id=485)  ([Materiales](http://groups.google.com.ar/group/pyafipws/web/curso-en-la-acp))
 2. [Charla en Conferencia Python Argentina 2009](http://ar.pycon.org/2009/conference/schedule/event/37/)
 3. [Charla en Conferencia Conurbania 2009](http://www.conurbania.org/pagina/1248)
Consultar por capacitación y cursos a medida.


----
## Preguntas Frecuentes ¿Qué es la factura electrónica?
Las facturas electrónicas son comprobantes originales respaldatorios de las operaciones comerciales.
Contienen los mismos datos y tienen la misma validez que los comprobantes tradicionales (talonarios "físicos" en papel), pero su confección, autorización, transmisión y almacenamiento es totalmente electrónico (por computadora, internet, etc., aunque también pueden ser impresos).

Esta regulado por la AFIP (Administración Federal de Ingresos Públicos, organismo recaudador a nivel nacional de Argentina), y en principio alcanza obligatoriamente a ciertas actividades: Servicios de planes de salud, transmisión de televisión, acceso a Internet, telefonía móvil, transporte de caudales, seguridad, limpieza, publicidad, Medios de comunicación, Encuestadoras, construcción, informática y desarrolladores de software, profesionales -abogados, contadores, escribanos, licenciados, ingenieros, arquitectos, etc.; Industrias de Bienes de Capital, Informática y Telecomunicaciones; Aseguradoras - pólizas de seguros de Caución; etc. (con determinadas excepciones). Otras actividades pueden utilizar estos servicios de manera optativa.
### ¿Qué regímenes de facturación electrónica estan disponibles?
Por el momento existen dos opciones:
 1. Régimen de Emisión de Comprobantes Electrónicos (R.E.C.E.): Permite autorizar Facturas A,B, M y C para Responsables Inscriptos y Monotributistas mediante Web Services, aplicativo AFIP SIAP RECE o servicio por clave fiscal "Comprobantes en linea" (máximo 100 comprobantes) 
 2. Régimen de Emisión de Comprobantes Electrónicos en Línea (R.C.E.L.): Permite autorizar Facturas A, B, M para Responsables Inscriptos (máximo 100 comprobantes) y Facturas C para monotributitas, solo por el servicio por clave fiscal "Comprobantes en linea"

Esta interfaz PyAfipWs y el aplicativo PyRece (y en general todas las soluciones de factura electrónica de terceros) solo funciona mediante web services (RECE), por disposiciones normativas no es posible adaptarlos al RCEL.

Más información en el sitio de [AFIP - eFactura](http://www.afip.gov.ar/eFactura/)
### ¿Que servicios web están disponibles para factura electrónica?
Por el momento, están habilitados:
 1. WSFE: Web Service Factura Electrónica (original, sin detallar artículos) 
 2. WSBFE: Web Service Bono Fiscal Electrónico (Bienes de Capital, detallando artículos según NCM)
 3. WSSEG: Web Service Seguros de Caución (describiendo pólizas, endosos, etc.)
 4. WSFEX: Web Service Factura Electrónica Exportación
 5. WSFEv1: Web Service Factura Electrónica (versión 1, sin detallar artículos)
 6. WSMTXCA: Web Service Factura Electrónica (con detalle de artículos)
### ¿Que ventajas tiene esta interfaz respecto a otras alternativas disponibles?
A diferencia de otras alternativas cerradas, este proyecto esta sustentado en el modelo de software libre y código abierto, basado en el desarrollo colaborativo para obtener productos de nivel empresarial, apoyado comercialmente brindando los servicios de soporte necesarios para este tipo de soluciones.
Creemos que este modelo y las tecnologías relacionadas permiten flexibilidad, mejorar la calidad y ser sostenibles en el tiempo.
Para información más detallada ver [OcxFacturaElectronica comparativa].
### ¿Como pruebo la generación de facturas electrónicas?
La AFIP dispone de dos ambientes:
 1. Homologación: servidores de prueba
 1. Producción: servidores definitivos

En homologación no es necesario activar el servicio de factura electrónica (régimen RECE), declarar los puntos de venta, etc. 
Las facturas autorizadas en homologación no tienen validez fiscal (los CAE obtenidos no pueden utilizarse).
Para cambiar de un servidor a otro se debe modificar la URL, el resto de la operatoria es idéntico.
### ¿Como genero un certificado electrónico para firma digital?
Ver [Manual PyAfipWs, Certificados](wiki:ManualPyAfipWs#Certificados):
 1. para homologación, enviar el pedido por email a webservices en afip.gov.ar
 1. para producción, subir el pedido por clave fiscal y bajarse el certificado

  **Nota**: Cualquier persona que posea CUIT puede generar un certificado para homologación.
### ¿Que es el CAE?
El C.A.E. (*Código de Autorización Electrónico*) es un número (formato similar al C.A.I.) que otorga la AFIP al autorizar la emisión de un comprobante por web service, aplicativo RECE o por el servicio por clave fiscal "Comprobantes en linea" ("facturas electrónicas").
Sin CAE, la factura no tiene validez fiscal. 

Este código debe informarse en la factura electrónica, consignando también su vencimiento (plazo a ser informado al cliente), código de comprobante, y demás datos de las facturas tradicionales.
Incluir el código de barras que representa estos datos es opcional.

El CAE es único por facturas A, pero puede ser el mismo para un lote de facturas B consecutivas, del el mismo día y cada una menor a $1000.- (en este último caso, se autorizan las facturas B en una sola operación por el monto total).
### ¿Como consulto la validez de un CAE de un comprobante electrónico?
Hay tres opciones:
 1. Consulta interactiva CAE: http://www.afip.gov.ar/genericos/consultacae/
 1. Por Clave Fiscal, servicio *Verificación de validez de comprobantes emitidos*
 1. Por Servicio Web, Para Facturas de Exportación o Bienes de Capital, método `GetCmp` del webservice `WSBFE` y `WSFEX`

Adicionalmente, los servicios web WSBFE y WSSEG poseen métodos para que el emisor pueda recuperar los datos de un comprobante individual ya emitido (ver ManualPyAfipWs), pero no es posible listar todas las facturas electrónicas realizadas.
### ¿Que es el ID?
El ID es el Identificador del requerimiento, un número interno de secuencia controlado por el emisor, que permite identificar de manera única cada operación de autorización (solicitud de CAE). 
Este dato es de vital importancia para poder recuperar un CAE frente a problemas de comunicación o fallas del hardware/software. Sin el, és imposible recuperar un CAE y se puede llegar a bloquear todo el circuito de facturación electrónica en los servidores de AFIP.
Por ello es recomendable que sea un dato propio del sistema de facturación, almacenado en un soporte permanente (base de datos en el disco rígido o similares)

En el caso de fallas, los webservices poseen métodos para recuperar el último ID informado (ver ManualPyAfipWs).
### ¿Las facturas electrónicas se pueden anular o borrar?
No, los comprobantes para los cuales se haya obtenido CAE no pueden ser eliminados o borrados, el proceso de autorización es definitivo y permanente.

A su vez, no puede haber saltos en la numeración (las autorizaciones deben ser correlativas) y las fechas deben ser siempre crecientes.
En el caso de rechazos (si la AFIP no otorga CAE) el comprobante no es válido, por lo que no debe ser anulado pero si debe ser descartado.

Si por algún motivo se pierde la correlatividad con los datos informados a la AFIP, los webservices poseen métodos para recuperar el último número de comprobante emitido (ver ManualPyAfipWs).
### ¿Como se deben almacenar los duplicados electrónicos?
Mas allá del sistema de gestión o base de datos, los emisores de facturas electronicas por web service (RECE) deben cumplir con la normativa """Almacenamiento de duplicados de comprobantes electrónicos""" (RG 1361/02).
Para ello podemos adaptar un conversor de formato ya desarrollado que genera los archivos para el aplicativo SIAP SIRED.
### ¿Donde se encuentra la información técnica oficial sobre servicios web?
La AFIP pone a disposición los siguientes sitios con información para desarrolladores y programadores sobre servicios web de factura electrónica (SOAP, XMP, encriptación, canal de seguridad, certificados, manuales, especificaciones, herramientas, ejemplos, etc.):
 1. https://wswhomo.afip.gov.ar/wsfedocs/
 2. http://wswhomo.afip.gov.ar/fiscaldocs/
### ¿Que soporte técnico ofrece la AFIP para servicios web?
En general, para consultas técnicas están disponibles los siguientes canales oficiales:
 1. Desarrollo: webservices@afip.gov.ar o (011) 4347-1219 / 1213  
 1. Mesa ayuda para producción: sri@afip.gov.ar o 0800-333-6372 opción 1

Recordar que no está orientado a cuestiones de programación, y se recomienda tener los archivos XML como documentación para una más rápida solución.

La información de esta página es proporcionada a titulo informativo.

Ofrecemos soporte té