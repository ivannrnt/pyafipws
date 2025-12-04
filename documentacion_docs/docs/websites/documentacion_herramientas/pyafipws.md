# [PyAfipWs](http://www.pyafipws.com.ar/): Interface de Servicios Web de la AFIP para Windows
[[TracNav(FacturaElectronica|noreorder|nocollapse)]]

Interfaz libre multiplataforma para Emisión y almacenamiento electrónico de comprobantes originales AFIP - Argentina. 
Por Automatización COM (EXE/DLL) simil OCX / ActiveX (Windows) y por línea de comando - archivos de texto (DOS) y tablas DBF.
AFIP RG 1956/05, 1361/02, 1345/02, 2265/07, 2289/07, 2485/08, 2557/09, 2668/09, 2758/10, 2853/10, 2904/10, 2959/10, 2974/10, 3066/11, 3067/11, 3210/11, 3419/12, 3536/13, 3571/13, 3593/14, 3668/14, 3749/15, 3779/15 (servicios web de Factura Electrónica, Trazabilidad y Liquidación de Granos, Consultas de Operaciones cambiarías y otros)

Código de Operaciones de Translado (Remito Electrónico). Ley Provincial 13.405. Normativas 34/2011 y 45/2011 ARBA.

Programa Nacional de Trazabilidad de Medicamentos, Precursores Químicos y Productos Agroquímicos (Fitosanitarios/Veterinarios). Resolución 435/2011 del Ministerio de Salud y Disposición 3683/2011 de ANMAT.  Resolución 900/12 RENPRE. Resolución 369/2013 SENASA.


Para otros productos (herramientas, aplicativos, generación de PDF, etc.) ver el menú lateral.

- PyRece: **Aplicativo independiente -visual-** (simil SIAP/RECE) para gestión de CAE, generación y envío de facturas electrónicas (en formato PDF) por **planilla de calculo**, **archivos de texto**, tablas **DBF** o **XML**
- PyFactura: **Aplicativo independiente -visual-** para facturación electrónica simple (ingreso de datos, obtención de CAE, generación en formato PDF, consultas)
- HerramientaFacturaElectronica (FE.py): **Herramienta integrada** para la solicitud de CAE, generación y envío de Factura Electrónica por **bases de datos**


[[Image(htdocs:logo-pyafipws.png,align=right)]]

## Índice
[[TOC(noheading,inline,depth=2)]]
## Introducción
PyAfipWs es una interface de software libre a los Servicios Web de la AFIP, desarrollado en Python compatible con Visual Basic, ASP, Fox Pro, Cobol, Delphi, Genexus, !PowerBuilder, PHP, .Net, Java, etc. y cualquier lenguaje/aplicación que pueda crear objetos [COM (automatización)](http://es.wikipedia.org/wiki/Component_Object_Model) en Windows o mediante archivos de texto o tablas DBF simil SIAP/RECE. Funciona tanto para web services de autenticación, factura electrónica, [bienes de capital - bono fiscal electrónico](wiki:BonosFiscales) y [facturas de exportación](wiki:FacturaElectronicaExportacion) y otros webservices de AFIP (próximamente remito electrónico, seguros de caución).

La interfase ha sido basada en los ejemplos de la AFIP y ha sido probada con éxito por varias empresas.

Actualmente implementa [Factura Electrónica](wiki:ProyectoWSFEv1) (emisión electrónica de comprobantes originales) según RG 1956/05, 1345/02, 2265/07, 2289/07, 2485, y 2557/09 (BonosFiscales - Bienes de Capital), 3057, 2953. [Facturas Electrónicas de Exportación](wiki:FacturaElectronicaExportacion) (según RG 2758/10) y [Factura Electrónica con detalle](wiki:FacturaElectronicaMTXCAService) (RG 2904/10 y RG 2926), Factura Electrónica Importadores (RG2975/10), Turismo (RG2959/10) y Proveedores del Estado (RG2853/10). Proximamente incluirá para Pólizas de Seguro de Caución (según RG 2668/09).

También se incluye una interfase por archivo de texto (similar al SIAP/RECE pero online y más simplificada), para lenguajes que no soporten Objetos COM, como algunas versiones de Cobol y Fox Pro (ver el [Manual de Uso](wiki:ManualPyAfipWs) para mayor información). Incluyendo soporte para tablas DBF, JSON, XML y  otros formatos.

En paralelo se ha desarrollado PyRece, un aplicativo ad-hoc para autorizar, generar pdf y enviar por correo electrónico facturas electrónicas. [Ver Más](wiki:PyRece); Herramientas PyFEPDF para generar facturas en formato PDF y PyI25 para generar códigos de barra.

Temas relacionados: **COT**, biblioteca para Remito Electrónico. [Ver Más](wiki:RemitoElectronicoCotArba); servicio web **WSCOC**, Consulta de operaciones cambiaras, [PadronContribuyentesAFIP Padrón Contribuyentes],  [Ver Más](wiki:ConsultaOperacionesCambiarias); Servicio web Trazabilidad de [ Medicamentos](wiki:TrazabilidadMedicamentos) (**!TrazaMed** ANMAT), [ Precursores Químicos](wiki:TrazabilidadPrecursoresQuimicos) (**!TrazaRenpre** SEDRONAR), [ Fitosanitarios](wiki:TrazabilidaProductosFitosanitarios) (**!TrazaFito** SENASA).

Consultar por desarrollos especiales, interfaces web, etc.
## Licencia

El código fuente puede ser descargado y utilizado sin cargo (gratis) respentando la licencia [GPLv3](https://www.gnu.org/licenses/gpl-faq.es.html) de software libre (versión actualizada de la licencia del kernel de Linux):  sin garantías, sin soporte técnico dedicado y/o obligatorio, informar copyright, no incorporarlo ni distribuirlo junto con software propietario, mantener derivados como software libre y contribuir modificaciones, etc. 

Se ofrece instalación y soporte técnico comercial pago, incluyendo atención prioritaria y autorización especial para incorporar y distribuir esta interfaz a sistemas de gestión propietarios que no sean software libre. 

A su vez, al ser software libre de código abierto "open source", permite proteger su inversión a futuro, al no depender de un componente cerrado del cual no puede tener acceso al código fuente, revisar su funcionamiento, realizar futuras actualizaciones, etc. 
Cuenta con un [foro](http://groups.google.com/group/pyafipws) (grupo público de usuarios y desarrolladores) de más de 350 miembros de todo el país, donde se brinda soporte comunitario sin costo (gratuito) y sin compromiso.
El repositorio con el código fuente e historial de cambios se encuentra públicado en [GoogleCode](https://code.google.com/p/pyafipws/) (histórico) y [GitHub](https://github.com/reingart/pyafipws) (actualizado).

Por consultas sobre el lenguaje Python y demás, dirigirse a [PyAr](http://www.python.org.ar). Para más información ver FacturaElectronica.



## Características

- Interfaz COM directa (online) de simple uso: autenticación y obtención de CAE en 10 líneas!
- No usa archivos temporales ni formatos especiales
- No usa servidores intermedios (conexión directa con WS de AFIP)
- No requiere programas residentes o batch (por lotes)
- No es necesario tener conocimientos de encriptación ni protocolos web
- Autoinstalable 2.5MB (Todo en uno)
- Sin dependencias ni librerias o runtimes externas (Php, .Net o Java)
- Sin licencia de uso ni límites por cada usuario final
- Código abierto: archivos fuentes publicados, revisados y modificables (Software Libre)
- Sin problemas de instalación de OCX ni ActiveX (ver [comparativa](wiki:OcxFacturaElectronica))
- No requiere formularios visuales ni referencias a DLL

## Funcionamiento
La interface maneja automáticamente la generación de documentos xml, firmas digitales criptográficas y servicios web (SOAP), por lo que no se requiere el manejo de dichos temas por parte de la aplicación.

Ver [Tabla Comparativa](wiki:ManualPyAfipWs#TablacomparativaWebservices) para mayor información.

La interfase del **Web Service de Autenticación y Autorización (WSAA)** permite:

- Creación de Ticket de Requerimiento de Acceso (TRA)
- Firma del ticket y creación del mensaje firmado criptográficamente (CMS)
- Ejecución del método remoto de autenticación y obtención del Ticket de Acceso (TA)

La interfase del **Web Service de Facturación Electrónica (WSFE)** permite:

- Ejecución del método remoto Dummy() para obtención del estado de servidores (uso opcional)
- Ejecución del método remoto !UltNro() para recuperar el último número de transacción (ID)
- Ejecución del método remoto Aut() devuelve el Código de Autorización Electrónico o de Emisión (CAE)
- Ejecución del método remoto RecuperaLastCMP() para obtención del último número de comprobante autorizado (uso opcional)
- Ejecución del método remoto !RecuperaQty() para recuperar la cantidad máxima de registros de detalle (uso opcional)

La interfase del **Web Service de Bono Fiscal Electrónico (WSBFE)** (ver [Bonos Fiscales - Bienes de Capital](wiki:BonosFiscales) RG2557) permite:

- Ejecución del método remoto Dummy() para obtención del estado de servidores (uso opcional)
- Ejecución del método remoto !CrearFactura() para crear una factura de bono fiscal electrónico 
- Ejecución del método remoto !AgregarItem() para agregar un artículo a una factura de bono fiscal electrónico
- Ejecución del método remoto Authorize() devuelve el Código de Autorización Electrónico o de Emisión (CAE)

La interfase del **Web Service de Factura Electrónica de Exportación (WSFEXv1)** (ver [Factura Exportación](wiki:FacturaElectronicaExportacion) RG2758) permite:

- Ejecución del método remoto Dummy() para obtención del estado de servidores (uso opcional)
- Ejecución del método remoto !CrearFactura() para crear una factura electrónica de exportación 
- Ejecución del método remoto !AgregarItem() para agregar un artículo a una factura electrónica de exportación
- Ejecución del método remoto !AgregarPermiso() para agregar un permiso de embarque
- Ejecución del método remoto !AgregarCmpAsoc() para agregar un comprobante asociado
- Ejecución del método remoto Authorize() devuelve el Código de Autorización Electrónico o de Emisión (CAE)
- Ejecición de los métodos remotos !GetParamMon, !GetParamTipoCbte, !GetParamTipoExpo, !GetParamIdiomas, !GetParamUMed, !GetParamIncoterms, !GetParamDstPais, !GetParamDstCUIT, !GetParamCtz para obtención de tablas referenciales y datos auxiliares.

La interfase del **Web Service de Factura Electrónica Mercado Interno Versión 1 (WSFEv1)** (ver [wiki:ProyectoWSFEv1] RG2485, RG2975 Importadores, RG2959 Turismo, RG3057 Monotributistas, RG2953 Proveedores del Estado Nacional, RG2926 CAE Anticipado Autoimpresores, entre otros) permite:

- Ejecución del método remoto Dummy() para obtención del estado de servidores (uso opcional)
- Ejecución del método remoto !CrearFactura() para crear una factura electrónica local A, B, C o M (en moneda nacional o extranjera)
- Ejecución del método remoto !AgregarIVA() para agregar una alícuota de IVA
- Ejecución del método remoto !AgregarTributos() para agregar otros impuestos nacionales, provinciales o municipales
- Ejecución del método remoto !AgregarCmpAsoc() para agregar un comprobante asociado
- Ejecución del método remoto FECAESolicitar() devuelve el Código de Autorización Electrónico o de Emisión (CAE) o 
- Ejecución del método remoto CAEASolicitar, CAEAConsultar y CAEARegInformativo para CAE Anticipado.
- Ejecución del método remoto !CompConsultar para recuperar un comprobante.
- Ejecución de los métodos remotos !ParamGetTiposCbte, !ParamGetTiposConcepto, !ParamGetTiposDoc, !ParamGetTiposIva, !ParamGetTiposMonedas, !ParamGetTiposOpcional, !ParamGetTiposTributos, !ParamGetCotizacion, !ParamGetPtosVenta para obtención de tablas referenciales y datos auxiliares.

La interfase del **Web Service de Factura Electrónica Mercado Interno con Detalle (WSMTXCA)** (ver [wiki:FacturaElectronicaMTXCAService] RG2904 Sujetos Notificados, RG2926 CAE Anticipado Autoimpresores, entre otros) permite:

- Ejecución del método remoto Dummy() para obtención del estado de servidores (uso opcional)
- Ejecución del método remoto !CrearFactura() para crear una factura electrónica A o B 
- Ejecución del método remoto !AgregarItem() para agregar un artículo, incluyendo código de barras MTX
- Ejecución del método remoto !AgregarIVA() para agregar una alícuota de IVA
- Ejecución del método remoto !AgregarTributos() para agregar otros impuestos nacionales, provinciales o municipales
- Ejecución del método remoto !AgregarCmpAsoc() para agregar un comprobante asociado
- Ejecución del método remoto !AutorizarComprobante() devuelve el Código de Autorización Electrónico o de Emisión (CAE)
- Ejecución de los métodos remotos SolicitarCAEA, ConsultarCAEAEntreFechas, ConsultarCAEA (emulado) y InformarComprobanteCAEA para CAE Anticipado
- Ejecución del método remoto !ConsultarComprobante para recuperar un comprobante.
- Ejecución de los métodos remotos !ConsultarComprobante, !ConsultarTiposComprobante, !ConsultarTiposDocumento, !ConsultarAlicuotasIVA, !ConsultarCondicionesIVA, !ConsultarMonedas, !ConsultarUnidadesMedida, !ConsultarTiposTributo, !ConsultarCotizacionMoneda para obtención de tablas referenciales y datos auxiliares.

### Ejemplo en Visual Basic (VB 5/6)
```
#!vb
' Crear objeto interface Web Service Autenticación y Autorización
Set WSAA = CreateObject("WSAA") 

tra = WSAA.CreateTRA() ' Generar un Ticket de Requerimiento de Acceso (TRA)
cms = WSAA.SignTRA(tra, "ghf.crt", "ghf.key") ' Generar el mensaje firmado (CMS) 

' Llamar al web service para autenticar
ta = WSAA.CallWSAA(cms, "https://wsaahomo.afip.gov.ar/ws/services/LoginCms") 
    
' Crear objeto interface Web Service de Factura Electrónica
Set WSFE = CreateObject("WSFE") 
WSFE.Token = WSAA.Token ' Setear tocken y sing de autorización (pasos previos)
WSFE.Sign = WSAA.Sign    
WSFE.Cuit = "3000000000" ' CUIT del emisor

' Conectar al Servicio Web de Facturación
ok = WSFE.Conectar("https://wswhomo.afip.gov.ar/wsfe/service.asmx") 
    
' Llamo al WebService de Autorización para obtener el CAE
cae = WSFE.Aut(id, presta_serv, tipo_doc, nro_doc, tipo_cbte, punto_vta, cbt_desde, cbt_hasta, imp_total, 
        imp_tot_conc, imp_neto, impto_liq, impto_liq_rni, imp_op_ex, fecha_cbte, fecha_venc_pago) 
```

### Ejemplo en Visual Fox Pro 5 (VFP5)
```
#!vb
*-- Crear objeto interface Web Service Autenticación y Autorización
WSAA = CREATEOBJECT("WSAA") 
*-- Generar un Ticket de Requerimiento de Acceso (TRA)
tra = WSAA.CreateTRA() 
*-- Generar el mensaje firmado (CMS) 
cms = WSAA.SignTRA(tra, "ghf.crt", "ghf.key") 
*-- Llamar al web service para autenticar
ta = WSAA.CallWSAA(cms, url_webservice)     

*-- Crear objeto interface Web Service de Factura Electrónica
WSFE = CREATEOBJECT("WSFE") 
*-- Setear tocken y sing de autorización (pasos previos) Y CUIT del emisor
WSFE.Token = WSAA.Token 
WSFE.Sign = WSAA.Sign    
WSFE.Cuit = "3000000000"
*-- Conectar al Servicio Web de Facturación
ok = WSFE.Conectar(url_webservice)     
*-- Llamo al WebService de Autorización para obtener el CAE
cae = WSFE.Aut(id, presta_serv, tipo_doc, nro_doc, tipo_cbte, punto_vta, cbt_desde, cbt_hasta, imp_total, ;
               imp_tot_conc, imp_neto, impto_liq, impto_liq_rni, imp_op_ex, fecha_cbte, fecha_venc_pago) 
```

### Ejemplo para SAP (ABAP)
La interfaz es compatible con practicamente cualquier lenguaje que soporte Automaticación COM/ActiveX, como en el caso de ABAP:

```
CREATE OBJECT WSAA 'WSAA'.

CALL METHOD OF WSAA 'CreateTRA' = TRA
  EXPORTING #1 = SERVICE
  #2 = TTL.

CALL METHOD OF WSAA 'SignTRA' = CMS
  EXPORTING #1 = TRA
  #2 = CERTIFICADO
  #3 = CLAVEPRIVADA.


CALL METHOD OF WSAA 'CallWSAA' = TA
  EXPORTING #1 =ZCMS
  #2 = URL.

GET PROPERTY OF WSAA 'Token' = TOKEN.
GET PROPERTY OF WSAA 'Sign' = SIGN.
```

Para más información ver:
http://wiki.sdn.sap.com/wiki/display/Snippets/ABAP+-+OLE+Automation+using+MS-Word


### Ejemplo para Delphi

En Delphi, se debe definir el objeto como variant:

```
var WSAA: Variant;
```

y luego crearlo con:

```
WSAA := CreateOleObject('WSAA');
```

Ver el ejemplo completo de factura electronica, que se puede adaptar para otros cosos, en [Project1.dpr](https://code.google.com/p/pyafipws/source/browse/ejemplos/wsfe/delphi/Project1.dpr)


### Ejemplo para Java

En Java (bajo Windows), se pude usar vía [Java COM Bridge](http://sourceforge.net/projects/jacob-project/): 

```
#!java

ActiveXComponent wsaa = new ActiveXComponent("WSAA");
            
System.out.println(Dispatch.get(wsaa, "InstallDir").toString() + 
                               Dispatch.get(wsaa, "Version").toString()
                              );
                        
/* Solicitar Ticket de Acceso a AFIP (cambiar URL producción) */
String wsdl = "https://wsaahomo.afip.gov.ar/ws/services/LoginCms";
String userdir = System.getProperty("user.dir");
Dispatch.call(wsaa, "Autenticar", 
              new Variant("wsfe"), 
              new Variant(userdir + "/reingart.crt"), 
              new Variant(userdir + "/reingart.key"), 
              new Variant(wsdl));
String excepcion =  Dispatch.get(wsaa, "Excepcion").toString();
System.out.println("Excepcion: " + excepcion);
String token = Dispatch.get(wsaa, "Token").toString();
String sign = Dispatch.get(wsaa, "Sign").toString();
System.out.println("Token: " + token +  "Sign: " + sign);
```

Ver el ejemplo completo de factura electronica, que se puede adaptar para otros cosos, en [FacturaElectronica.java](https://code.google.com/p/pyafipws/source/browse/ejemplos/FacturaElectronica.java)

Bajo linux se podría usar con archivos de intercambio de texto, JSON, o similar.
### Ejemplo para !PowerBuilder

Ejemplo del código para gestionar un ticket de acceso en !PowerBuilder (extensible a otros webservices):

```
// definir las variables:

OLEObject WSAA
string tra
string cms
string ta

// crear el objeto COM (similar a CreateObject en otros lenguajes):
WSAA = CREATE OLEObject
status = WSAA.ConnectToNewObject("WSAA")

// generar el requerimiento de ticket de acceso:
tra = WSAA.CreateTRA("wsfe", 3600)

// firmar el requerimiento de ticket de acceso:
cms = WSAA.SignTRA(tra, "reingart.crt", "reingart.key") 

// conectarse al webservice
ok = WSAA.Conectar("", "https://wsaa.afip.gov.ar/ws/services/LoginCms", "")

// otener ticket de acceso MARIANO //
ta = WSAA.LoginCMS(cms) 

// mostrar los datos del ticket de acceso:
MessageBox("Ticket", ta, Exclamation!)
MessageBox("Token", string(WSAA.Token), Exclamation!)
MessageBox("Sign", string(WSAA.Sign), Exclamation!)

```

Ver el ejemplo completo de factura electrónica v1, que se puede adaptar para otros cosos, en [ej_powerbuilder.txt](https://code.google.com/p/pyafipws/source/browse/ejemplos/wsfev1/ej_powerbuilder.txt)
### Ejemplo para Clarion

Para Clarion, existirìan varios métodos.
En principio no se registra una OCX, sino que se usa directamente con !CreateObject como en otros lenguajes.

Para comenzar, crear un control OLE llamado OLE1 y luego probar el siguiente código:
```
    Code
        WSAA = ?OLE1{'CreateObject("WSAA")'}
        Stop(?OLE1{WSAA & '.Version'})
    Return
```

Ejemplo alternativo tentativo:

```

?Ole{prop:create}='WSAA'
?Ole{'Conectar("", "https://wsaa.afip.gov.ar/ws/services/LoginCms?wsdl" )'}
TRA = ?Ole{'CreateTRA("wsfe")'}
CMS = ?Ole{'SignTRA("'&CLIP(TRA)&'", "C:\reingart.CRT", "c:\reingart.key")'}
TA = ?Ole{'LoginCMS("'&CLIP(CMS)&'")'}

MESSAGE(TRA,'TRA')
MESSAGE(CMS,'CMS')
MESSAGE(TA,'TA')
MESSAGE(?Ole{'XmlRequest'}, 'XmlRequest')
MESSAGE(?Ole{'XmlResponse'}, 'XmlResponse')
MESSAGE(?Ole{'LoginCMS'}, 'LoginCMS')
MESSAGE(?Ole{'Excepcion'}, 'Excepcion')
MESSAGE(?Ole{'Traceback'}, 'Traceback')
MESSAGE(?Ole{'Token'},'Token')
MESSAGE(?Ole{'Sign'},'Sign')

?Ole:2{'CreateObject("WSFEv1")'} 
?Ole:2{'Conectar("", "https://servicios1.afip.gov.ar/wsfev1/service.asmx?WSDL?wsdl" )'}

! establecer datos generales:

?Ole:2{'SetParametros("cuit", "", "")'}
?Ole:2{'SetTicketAcceso("'&CLIP(TA)&'")'}

! alternativamente usand propiedades (descomentar):

! ?Ole:2{PROP:Cuit} = "30... "
! ?Ole:2{PROP:Token} = Token
! ?Ole:2{PROP:Sign} = Sign

! llamar a los metodos de factura electronica (reemplazar por valores)

OK=?Ole:2{'wsfev1.CrearFactura("concepto", "tipo_doc", "nro_doc", "tipo_cbte", "punto_vta", "cbt_desde", "cbt_hasta", "imp_total", "imp_tot_conc", "imp_neto", "imp_iva", "imp_trib", "imp_op_ex", "fecha_cbte", "fecha_venc_pago", "fecha_serv_desde", "fecha_serv_hasta", "moneda_id", "moneda_ctz")'}

OK=?Ole:2{'AgregarIva("id", "base_imp", "importe")'}

CAE=?Ole:2{'CAESolicitar()'}

MESSAGE(CAE)
```

Si hay algun error se necesitaría el contenido de las propiedades XmlRequest y XmlResponse, Excepcion y Traceback, por ej ?Ole:2:{PROP:XmlRequest}
### Ejemplo para Fujitsu Net Cobol
La interfaz es compatible tambien con varias versiones de Cobol que soporten Automaticación COM/ActiveX, como en el caso de Fujitsu !NetCobol:

```
IDENTIFICATION DIVISION.
 PROGRAM-ID. "PYAFIPWSDEMO".
 ENVIRONMENT DIVISION.
 CONFIGURATION SECTION.
 REPOSITORY.
    CLASS COM-EXCEPTION AS "*COM-EXCEPTION"
    CLASS COM AS "*COM".
 DATA            DIVISION.
 WORKING-STORAGE SECTION.
 01  VARIABLES.
    05  WSAA-CONNECTION-TYPE   PIC X(8192) VALUE "WSAA".
    05  WSFE-CONNECTION-TYPE   PIC X(8192) VALUE "WSFEv1".
    05  WSAA OBJECT REFERENCE COM.
    05  WSFE OBJECT REFERENCE COM.

    05  CERT-STRING PIC X(500)  VALUE "C:\REINGART.CRT".
    05  CLAVE-STRING PIC X(500) VALUE "C:\REINGART.KEY".
    05  WSAA-TRA X(10240).
    05  WSAA-CMS X(10240).
    05  WSAA-TOKEN X(10240).
    05  WSAA-SIGN X(10240).
    05  CUIT-EMISOR PIC X(11) VALUE "20267565393".

    05  PUNTO-VENTA PIC X(4) VALUE "4002".
    05  TIPO-CBTE PIC X(2) VALUE "01".
    05  NRO-CBTE PIC X(8).
    05  IMP-TOTAL PIC 9(17)V9(2).
    05  CAE PIC X(14).
    05  CAE-VENCIMIENTO PIC X(10).

    05  WSFE-EXCEPCION X(10240).
    05  WSFE-TRACEBACK X(10240).
    05  WSFE-ERR X(10240).
    05  WSFE-OBS X(10240).
    05  WSFE-XMLREQUEST X(10240).
    05  WSFE-XMLRESPONSE X(10240).


 PROCEDURE DIVISION.
 MAIN SECTION.
    *> crear objeto COM autenticacion
    INVOKE COM "CREATE-OBJECT"
           USING WSAA-CONNECTION-TYPE
           RETURNING WSAA.

    *> crear requerimiento de acceso
    INVOKE WSAA "CreateTRA"
           RETURNING WSAA-TRA.
    *> firmar requerimiento de acceso
    INVOKE WSAA "SignTRA"
           USING TRA CERT-STRING CLAVE-STRING
           RETURNING WSAA-CMS.

    *> llamar al webservice y obtener ticket de acceso
    INVOKE WSAA "CallWSAA"
           USING CMS
           RETURNING WSAA-TA.

    INVOKE OBJ-FIELDS "GET-Token"
           RETURNING WSAA-TOKEN.

    INVOKE OBJ-FIELDS "GET-Sign"
           RETURNING WSAA-SIGN.

    *> crear objeto COM factura electronica
    INVOKE COM "CREATE-OBJECT"
           USING WSFE-CONNECTION-TYPE
           RETURNING WSFE.

    INVOKE WSFE "SET-Token"
           USING WSAA-TOKEN.

    INVOKE WSFE "SET-Sign"
           USING WSAA-SIGN.

    INVOKE WSFE "SET-Cuit"
           USING CUIT-EMISOR.

    *> conectarse a AFIP (para producción pasar la cache y URL)
    INVOKE WSFE "Conectar".

    *> consultar ultimo numero
    INVOKE WSFE "CompUltimoAutorizado"
           USING TIPO-CBTE PUNTO-VENTA
           RETURNING NRO-CBTE.

    *> obtengo mensajes xml, excepcion/traza, error y observaciones AFIP 
    *> (para depuracion)
    INVOKE OBJ-FIELDS "GET-XmlRequest"
           RETURNING WSFE-XMLREQUEST.
    INVOKE OBJ-FIELDS "GET-XmlResponse"
           RETURNING WSFE-XMLRESPONSE.
    INVOKE OBJ-FIELDS "GET-Excepcion"
           RETURNING WSFE-EXCEPCION.
    INVOKE OBJ-FIELDS "GET-Traceback"
           RETURNING WSFE-TRACEBACK.
    INVOKE OBJ-FIELDS "GET-ErrMsg"
           RETURNING WSFE-ERR.
    INVOKE OBJ-FIELDS "GET-Obs"
           RETURNING WSFE-OBS.

    *> consultar datos del ultimo comprobante
    INVOKE WSFE "CompConsultar"
           USING TIPO-CBTE PUNTO-VENTA NRO-CBTE
           RETURNING CAE.

    *> obtengo datos del comprobante registrado en AFIP
    INVOKE OBJ-FIELDS "GET-FechaCbte"
           RETURNING FECHA-CBTE.
    INVOKE OBJ-FIELDS "GET-Vencimiento"
           RETURNING CAE-VENCIMIENTO.
    INVOKE OBJ-FIELDS "GET-ImpTotal"
           RETURNING IMP-TOTAL.
```

Para otras versiones de Cobol, es posible también utilizar archivos de texto de ancho fijo similar al SIAP/RECE, por ej. para WSFE:
(ignorar campos de relleno FILLERx)
```
       01  HDR-PYAFIPWS.
           02 FE-FILLERA        PIC 9.
           02 FE-FECHACBTE      PIC 9(8).
           02 FE-TIPOCBTE       PIC 99.
           02 FE-FILLERB        PIC X.
           02 FE-PUNTOVTA       PIC 9999.
           02 FE-CBTDESDE       PIC 9(8).
           02 FE-CBTHASTA       PIC 9(8).
           02 FE-FILLERC        PIC 999.
           02 FE-TIPODOC        PIC 99.
           02 FE-NRODOC         PIC 9(11).
           02 FE-FILLERD        PIC X(30).
           02 FE-IMPTOTAL       PIC 9(15).
           02 FE-IMPTOTCONC     PIC 9(15).
           02 FE-IMPNETO        PIC 9(15).
           02 FE-IMPTOLIQ       PIC 9(15).
           02 FE-IMPTOLIQRNI    PIC 9(15).
           02 FE-IMPOPEX        PIC 9(15).
           02 FE-FILLERE        PIC 9(15).
           02 FE-FILLERF        PIC 9(15).
           02 FE-FILLERG        PIC 9(15).
           02 FE-FILLERH        PIC 9(15).
           02 FE-FILLERI        PIC 9(8).
           02 FE-FILLERJ        PIC 9(8).
           02 FE-FILLERK        PIC 9(8).
           02 FE-FILLERL        PIC 9(6).
           02 FE-FILLERM        PIC 9.
           02 FE-FILLERN        PIC X.
           02 FE-CAE            PIC 9(14).
           02 FE-FECHAVTO       PIC 9(8).
           02 FE-FILLERO        PIC 9(8).
           02 FE-RESULTADO      PIC X.
           02 FE-MOTIVO         PIC XX.
           02 FE-REPROCESO      PIC X.
           02 FE-FECHAVENCPAGO  PIC 9(8).
           02 FE-PRESTASERV     PIC 9.
           02 FE-FECHASERVDESDE PIC 9(8).
           02 FE-FECHASERVHASTA PIC 9(8).
           02 FE-ID             PIC 9(15).
```
### Certificados
Para poder utilizar la interfase se deben tramitar y asociar los certificados de homologación/producción en la AFIP. Para mas información ver  [Página principal de Factura Electrónica (AFIP)](http://www.afip.gov.ar/eFactura/)

Pasos para crear el certificado (más información en [Instructivo AFIP](https://wswhomo.afip.gov.ar/wsfedocs/cert-req-howto.txt)):

- Bajar e instalar [OpenSSL para windows](http://www.nsis.com.ar/soft/Win32OpenSSL-0_9_8i.exe) (en caso de inconvenientes, instalar [Redistribuible de Visual C++](http://www.microsoft.com/downloads/details.aspx?familyid=9B2DA534-3E03-4391-8A4D-074B9F2BC1BF))
- Bajar el archivo [afip-openssl.cnf](http://www.sistemasagiles.com.ar/soft/pyafipws/afip-openssl.cnf) y guardarlo en ```C:\OpenSSL\bin\``` (modalidad previa, ver de pasar argumentos por línea de comandos)
- Ingresar por línea de comando al directorio de OpenSSL ```C:\OpenSSL\bin>```
- Generar la clave privada:

```
openssl genrsa -out empresa.key 2048
```

- Generar el pedido (CSR: certificate signing request) por línea de comando:

```
openssl req -new -key empresa.key -out empresa.csr -config afip-openssl.cnf
```

- ```Country Name (2 letter code) [AR]:``` **AR**
- ```Organization Name (por ej., empresa) [EMPRESA SA]:``` *ingresar nombre de la empresa tal cual figura en la consulta de inscripción, ej.:* **Empresa S A **
- ```Common Name (por ej., su nombre) []:``` *ingresar el nombre del servicio, aplicación u unidad operativa, ej:* **Sistema Facturas**
- ```Ingrese: CUIT XXXXXXXXXXX (XXXXXXXXXXX es la CUIT sin guiones)``` *ingresar* **CUIT xxxxxxxxxxx**
- Enviar el ```empresa.csr``` a la AFIP para que lo firmen y devuelvan el certificado ```empresa.crt```. Para asociar el certificado de homologación, enviarlo por email a la AFIP (webservices@afip...). Para producción, enviarlo [por clave fiscal](https://wswhomo.afip.gov.ar/wsfedocs/WSAA%20-%20Procedimiento%20obtencion%20y%20asociacion%20de%20certificados%20-%20090323.pdf), y descargar el certificado CRT.
- Con esta interfase no es necesario convertir el certificado en formato pkcs12 ni importarlo al repositorio de Windows

En caso de inconvenientes, los servidores de la AFIP responderán con un mensaje que identifica el problema:

- ```ns1:coe.notAuthorized Computador no autorizado a acceder los servicios de AFIP```: el certificado no es válido o no está correctamente asociado al ambiente en el cual se intenta usar (ej. certificado de homologación usado en producción). Revisar el proceso de generación y asociación del certificado.
- ```ns1:cms.cert.expired Certificado expirado```: los certificados poseen una fecha de vencimiento que varía según el ambiente para el cual fueron creados y la fecha de emisión. Generar y asociar nuevamente el certificado.

## Descargas

- [Manual de Uso](wiki:ManualPyAfipWs): Documentación ([PDF](http://www.sistemasagiles.com.ar/trac/wiki/ManualPyAfipWs?format=pdf))
- [GitHub](https://github.com/reingart/pyafipws/releases): Instalador para Homologación (Ejecutable Autoinstalable)
- [ej_vb.zip](http://www.sistemasagiles.com.ar/soft/pyafipws/ej_vb.zip): Proyecto de ejemplo en Visual Basic 5/6 (comprimido)
- [ej_vfp.zip](http://www.sistemasagiles.com.ar/soft/pyafipws/ej_vfp.zip): Proyecto de ejemplo en Visual Fox Pro 5 o posterior (comprimido)
- [pyafipws97.mdb](https://storage.googleapis.com/google-code-archive-downloads/v2/code.google.com/pyafipws/pyafipws.mdb) y [pyafipws2k.mdb](https://storage.googleapis.com/google-code-archive-downloads/v2/code.google.com/pyafipws/pyafipws2k.mdb): ejemplo completo de WSFEv1 y WSFEX (base de datos MS Access 97 o sup.) 
- [ej_php.zip](http://www.sistemasagiles.com.ar/soft/pyafipws/ej_php.zip): Proyecto de ejemplo en PHP 5 o posterior (comprimido)
- [ej_delphi.zip](http://www.sistemasagiles.com.ar/soft/pyafipws/ej_delphi.zip): Proyecto de ejemplo en Turbo Delphi 2006 (comprimido)
- [ej_cobol.txt](http://www.sistemasagiles.com.ar/soft/pyafipws/ej_cobol.txt): Ejemplo del formato del registro para COBOL (archivo de texto)
- [ej_powerbuilder.txt](http://www.sistemasagiles.com.ar/soft/pyafipws/ej_powerbuilder.txt): Ejemplo básico para !PowerBuilder (archivo de texto)

## Código Fuente

- Ver FacturaElectronica

## Costos y Condiciones

- Instalador para demostración sin cargo completamente funcional (para homologación)
- Código fuente publicado licenciado bajo GPLv3 (ver [Licencia](wiki:PyAfipWs#Licencia))
- Soporte comunitario: para uso gratuito sin cargo por el [fóro público](http://groups.google.com/group/pyafipws) (Google Group), foro PyAFIPWs (Telegram) ver [Modos Homologación/Producción](wiki:ManualPyAfipWs#ModosHomologaciónyProducción) e [Instalación Codigo Fuente](https://github.com/reingart/pyafipws/wiki/InstalacionCodigoFuente)
- Costo del soporte técnico comercial básico para webservices de AFIP y productos relacionados: (por única vez por empresa desarrolladora de software, sin activación ni limitaciones de CUIT, consultar por presupuestos a medida)
- Para [Colaboraciones $](https://link.mercadopago.com.ar/colaboracionespyafip)

### Paquetes promocionales
**(precios al 01/09/2025, consultar valores actuales por mail a info@sistemasagiles.com.ar)**

Planes con descuento adquiriendo soporte para varios webservices (consultar por presupuestos especiales, ver abajo precios individuales, condiciones y aclaraciones):

| **Paquete Recomendado: Webservice / Herramienta y funcionalidades** | **Período de Cobertura "garantía limitada"** [**](wiki:PyAfipWs#ProductosyServiciosincluidos) | **Hs. de soporte estimadas** | **Costo** |
|---|---|---|---|
| Consultas por temas menores (certificados WSAA, constatación WSCDC, padrón contribuyentes RG1817, almacenamiento RG1361, código barras, envío emails, etc.) *-sin cargo para clientes con soporte vigente, según hs contratadas-* *(asesoramiento gratuito de cortesía en homologación)* | 1 semana | hasta 1hs | **$65.000** |
| **Instaladores / Actualizaciones**: soporte mínimo instalación en producción, solo acceso a instalador para producción (aplicable a todos los componentes y herramientas para AFIP, sin consultas ni ajustes) **No válido para WSLPG, WSRemCarnico, WSRemHarina, WSRemAzucar, WSFECred y WSCPE**. Solo disponible para clientes con versiones recientes (12 meses) | 1 semana |  | **$** |
| Soporte general componentes simil OCX (por webservice): para lenguajes legados VB, VFP, .NET, Java y similares (Windows) por hora | 1 semana | hasta 1hs | **$65.000** |
| Soporte general herramientas por archivo de intercambio (por webservice): para lenguajes legados Cobol, dBase, xBase, PHP, Java, etc. (Windows/Linux) | 1 mes | hasta 3hs | **$** |
| __**Varios**__ |  |  |  |
| **COT / IIBB:** Remito Electrónico / Alicuotas Ingresos Brutos ARBA (soporte mínimo: solo instalador, sin consultas ni ajustes) | 2 semanas | hasta 3hs | **$** |
| **!TrazaMed / !TrazaRenPre / !TrazaFito / !TrazaVet:** Webservices Sistema Nacional de Trazabilidad ANMAT, SEDRONAR, SENASA (soporte mínimo) | 1 mes | hasta 5hs | **$** |
| __**Factura Electrónica**__ |  |  |  |
| **WSAA + WSFEv1:** factura electrónica mercado interno sin detalle CAE / CAEA (RG2485 V.2.5 ) | 1 mes | hasta 3hs | **$** |
| **WSAA + WSFEXv1 o WSBFEv1:** factura electrónica exportación (RG2758) o bono fiscal (RG2557) | 1 mes | hasta 4hs | **$** |
| **WSAA + WSMTXCA:** factura electrónica mercado interno con detalle CAE / CAEA (RG2904) | 2 meses | hasta 5hs | **$** |
| **WSAA + WSFEv1 + PyFEPDF:** factura electrónica mercado interno y generación de PDF (diseño estándar y campos genéricos) | 1 mese | hasta 5hs | **$** |
| **WSAA + WSFEv1 + WSFEXv1:** factura electrónica mercado interno y exportación | 2 meses | hasta 7hs | **$** |
| **WSAA + WSFEv1 + WSFEXv1 + PyFEPDF:** factura electrónica estándar -CAE o CAEA, con generación de PDF- | 2 meses | hasta 8hs | **$** |
| **WSAA + WSFEv1 + WSBFEv1 / WSMTXCA + WSFEXv1:** factura electrónica básico CAE o CAEA | 2 meses | hasta 10hs | **$** |
| **WSAA + WSFEv1 + WSBFEv1 + WSMTXCA + WSFEXv1 + PyFEPDF:** factura electrónica avanzado con generación de PDF, CAE y CAEA | 3 meses | hasta 14hs | **$** |
| __** Granos, Hacienda y otros **__ |  |  |  |
| **WSAA + WSCTGv4 + WSLPGv1.23:** trazabilidad y liquidación primaria electrónica de granos  (LPG, incluye generación PDF Form. C 1116 B/C) | 2 meses | hasta 11hs | **$** |
| **WSAA + WSLPGv1.23:** liquidación primaria y certificación electrónica de granos (LPG y CG) | 3 meses | hasta 9hs | **$** |
| **WSAA + WSLPGv1.23:** liquidación primaria, secundaria y certificación electrónica de granos (LPG, LSG y CG) | 3 meses | hasta 10hs | **$** |
| **WSAA + WSCTGv4 + WSLPGv1.23:** trazabilidad (CTG) , liquidación primaria, secundaria y certificación de granos (LPG, LSG y CG) | 4 meses | hasta 12hs | **$** |
| **WSAA + WSLSPv2.2.2:** liquidación sector pecuario - bobino, porcino (soporte mínimo recomendado, consultar alcance y métodos contemplados*) NUEVO Avícola consultar | 3 meses | hasta 12hs | **$** |
| **WSAA + WSLUMv1.3:** liquidación única mensual lechería - (soporte básico recomendado, consultar alcance y métodos contemplados*) | 3 meses | hasta 14hs | **$** |
| **WSAA + WSLTVv1.1:** liquidación de tabaco verde (soporte general recomendado, consultar alcance y métodos contemplados*) | 4 meses | hasta 20hs | **$** |

**Importante***: Consultar por paquetes a medida (soporte mínimo solo instalador, soporte por actualizaciones y cambios de AFIP, mayor o menor cantidad de horas o meses de cobertura, etc.).
 Ver [Productos y Servicios incluidos](http://www.sistemasagiles.com.ar/trac/wiki/PyAfipWs#ProductosyServiciosincluidos) para más información y períodos aplicables.
                   Para LINUX se adiciona soporte Avanzado, consultar.


 El valor hora publicado es acorde al sugeridos por el CPCIBA (Consejo Profesional de Ciencias Informáticas de la Provincia de Buenos  Aires) a Septiembre 2025.
 Para valores 2025 ver:
 [https://www.cpciba.org.ar]  


 Todo cambio en las especificaciones de AFIP no esta cubierto y se presupuesta por separado.

#### Servicios web AFIP
(precio al 01/11/2024, consultar valores actuales por mail a info@sistemasagiles.com.ar)

Precios recomendados de soporte por servicio web para contratación individual:

- WSAA (autenticación y autorización): $  (hasta 1 hs en total) *requerido para todos los web services*
- WSBFEv1 (factura electrónica bienes de capital): $  (hasta 4 hs en total por 1 mes de cobertura)
- WSSEG (factura electrónica seguros de caución): $ (hasta 4 hs en total por 1 mes de cobertura)
- WSFEv1 (factura electrónica mercado interno -sin detalle- versión 1 CAE o CAEA): soporte básico desde $ (hasta 3 hs en total por 3 semanas cobertura)
- WSMTXCA (factura electrónica mercado interno -con detalle- CAE o CAEA): soporte básico desde $ (hasta 4 hs en total por 1 mes de cobertura)
- WSFEXv1 (factura electrónica exportación -versión 1-): $ (hasta 4 hs en total, 1 mes de cobertura) -incluye soporte WSFEX original-
- WSCOC (código de operaciones cambiarias): -consultar-
- WSCTGv4 (código de trazabilidad de granos): recomendado: $ (hasta 4 hs en total por 1 mes de cobertura)
- WSLPGv1.23 (LPG: liquidación electrónica primaria de granos): recomendado: $ (hasta 6 hs en total por 2 meses de cobertura, con generación de PDF)
- WSLPGv1.23 (LSG: liquidación electrónica secundaria de granos): recomendado: $ (hasta 5 hs en total por 2 meses de cobertura, sin generación de PDF)
- WSLPGv1.23 (CG: certificación electrónica de granos): recomendado: $ (hasta 6 hs en total por 3 meses de cobertura, sin generación de PDF)
- WSCDC (Constatacion de Comprobantes): recomendado: $  (hasta 3 hs en total por 3 semanas de cobertura). 
- WSLUM (Liquidación única mensual "lechería") Consultar costo según métodos a implementar. 
- WSLSP (Liquidación sector pecuario - carne, porcino) recomendado: $ (hasta 11 hs en total, por 2 meses de cobertura) 
- WSCT (Comprobantes Turismo): recomendado: $ (1 mes de cobertura,hasta 5 hs en total).
- WS_SR_Padron_a4 / a5 (Consulta de Padrón Contribuyentes AFIP):$.- (hasta 3 hs en total por 2 semanas de cobertura).
- WS_SIRE (Sistema Integral de Retenciones Electrónicas): $ (por 1 mes de cobertura, hasta 4hs en total)
- WSRemCarne (Remito electrónico cárnico), WSRemAzucar (Remito Azucar y derivados) y WSRemHarina (Remito de harína de trigo y subproductos) : Consultar
- WSFECRED (Registro de Facturas de Crédito electrónica MyPyMes): Consultar costo según métodos a implementar. Paquete especial Emisores por Métodos -Monto Obligado Recepción, Cta. Corriente y Ctas. Corrientes $


#### Herramientas adicionales AFIP
(precio al 01/11/2024, consultar valores actuales por mail a info@sistemasagiles.com.ar)


Precios de soporte por herramientas individuales:

- PyFEPDF: Costo del soporte técnico comercial para la herramienta de generación de facturas en formato PDF:
    - Soporte mínimo (promocional para clientes con soporte vigente): $122.400 (por una semana de cobertura), sólo acceso a instalador y un mínimo de consultas por temas de instalación únicamente, no incluye análisis de errores o ajustes.
    - Soporte básico **Incluye generación de QR y nueva plantilla.**: $183.600.- (hasta 3 hs en total), incluye consultas generales y técnicas, correcciones y ajustes menores (no incluye rediseños del formato de factura, consultar modelos y ejemplos contemplados) 
    - Soporte avanzado: opcional desde $61.200.- (hasta 1 hs) adicional por cada rediseño de formato de factura (estandard)
- Pyi25: Costo del soporte técnico comercial para la herramienta de generación de código de barras:
    - Soporte mínimo: $28.400 (hasta 1 hs en total), sólo acceso a instalador y un mínimo de consultas por temas de instalación únicamente (hasta 1h, no incluye consultas o ajustes).
- Pyimail: Costo del soporte técnico comercial para la herramienta de generación de código de barras:
    - Soporte mínimo: $28.400 (hasta 1 hs en total), sólo acceso a instalador y un mínimo de consultas por temas de instalación únicamente (hasta 1h, no incluye consultas o ajustes).
- PyQR: Costo del soporte técnico comercial para la herramienta de generación de código QR: 
    - Soporte Mínimo: $28.400.-, por 1 semana de cobertura hasta 1hs en total, solo acceso a instalador y consultas generales, no incluye consultas técnicas, análisis de errores u ajustes
    - Soporte básico: $56.800.-, por 2 semanas de cobertura, hasta 2hs en total, incluye acceso instalador, consultas generales y técnicas, análisis y corrección de errores y ajustes menores
- Padrón de Contribuyentes ws_sr_constancia_inscripcion: 
    - Soporte Mínimo: $122.400, por 1 semana de cobertura hasta 1 hs en total, solo acceso a instalador, no incluye consultas u ajustes
    - Soporte básico: $244.800, por 4 semanas de cobertura, hasta 4 hs en total, incluye instalador, consultas, correcciones y ajustes menores
   
#### Servicios web ARBA


- COT: Remito Electrónico - código de operaciones de transporte / Consulta alícuotas IIBB (ARBA):
- Soporte mínimo: $130.000.-  (por 1 semana de cobertura, hasta 1 hs en total), sólo acceso a instalador productivo, no incluye consultas o ajustes, solo temas de instalación.
- Soporte básico: $260.000.-  (por 3 semanas de cobertura, hasta 3hs en total), incluye instalador productivo, consultas particulares, corrección de errores  y ajustes menores
- Soporte avanzado: opcional desde $520.000.-, incluye desarrollo/ajustes de ejemplos estándards, herramientas, contempla temas urgentes y/o grandes empresas/ciclos de desarrollo, LINUX, con 2 meses de cobertura por cambios y correcciones, hasta 8hs en total.


#### Servicios web Sistema Nacional de Trazabilidad SNT

!TrazaMed / !TrazaRenPre / !TrazaFito: Trazabilidad de Medicamentos (ANMAT) / Trazabilidad de Precursores Químicos (!SeDroNar) / Trazabilidad de Productos Agroalimentarios (Fitosanitarios y Veterinarios):

- Soporte mínimo: $85.200.- (por 1 semana de cobertura), sólo acceso a instalador y soporte por temas de instalación únicamente, no incluye consultas generales o ajustes. (prefentemente para clientes actuales)
- Soporte básico: $227.200.- (hasta 8 hs en total por 1 mes máx.), incluye consultas particulares y ajustes menores, contemplando TLB (!TypeLib para lenguajes estáticos -solo !TrazaMed, consultar otros WS-)
- Soporte avanzado: $340.800.- (hasta  12hs en total por 3 meses máx.) adicional, incluyendo ajustes y desarrollo de ejemplos, documentación, pruebas, etc., contempla temas urgentes y/o grandes empresas/ciclos de desarrollo
 
### Precios especiales para clientes
**(precio al 01/12/2023, consultar valores actuales por mail a info@sistemasagiles.com.ar)**

Los clientes que ya hayan adquirido soporte para webservices anteriores (por tiempo limitado) pueden contratar:

- Soporte por Actualización (por ej a WSFEv1 o WSFEXv1): $33.120.- (hasta 1 semana de cobertura, sólo temas de instalación, no incluye consultas ni ajustes). Válido para clientes que hayan adquirido soporte para el webservice anterior, dentro del año contando desde la finalización del soporte contratado (WSFEv1, WSFEXv1, WSBFE).  
- Soporte Avanzado/Extendido Adicional al plan básico(soporte adicional LINUX): $49.680 (hasta 3 hs en total), incluye desarrollo/ajustes de ejemplos estándards, herramientas, CAE y/o CAE Anticipado, contempla temas urgentes y/o grandes empresas/ciclos de desarrollo, instalación en otros sistemas operativos (Linux), con 1 mes adicional de cobertura por cambios y correcciones.

Para consultas puntuales o temas menores ofrecemos un paquete de 1 hora de soporte técnico comercial (válido por una semana): $16560.-

### Forma de Pago

- Forma de pago: transferencia, depósito bancario (CBU)
- Forma de entrega: Se envía el instalador para producción por email y Factura por correo electrónico
- Consultar por facilidades de pago, soporte técnico comercial avanzado, desarrollos a medida o ajustes especiales.
- Los precios no incluyen IVA, adicionar IVA 21% 
- La cantidad de horas es estimativa (promedio estandarizado basado en nuestra experiencia para cada webservice, y no es cronometrada, por lo que no se cobran adicionales no presupuestados ni se bonifica por servicios no utilizados), cubre todos los aspectos del servicio (consultas, ajustes y mantenimiento postventa, ya sean solicitados o no). Ver [Aclaraciones](wiki:PyAfipWs#Aclaraciones)

### Productos y Servicios incluidos

El Soporte Técnico Comercial básico incluye: 

- Atención prioritaria y personalizada (vía email o telefónica a partir de fecha de factura una vez confirmado el pago)
- Acceso a instalador para producción (sin límite de usuarios/emisores ni archivos de licencias o activación) 
- "Garantía (limitada)": 1 mes de consultas sobre instalación, gestiones ante AFIP, Ajustes menores y análisis y corrección de errores (según período facturado)
- Autorización al contratante ("licencia dual") para incorporar ejemplos y distribuir la interfaz con software propietario (sistemas de gestión/facturación) de su propiedad (excepción a la licencia GPLv3)
- Soporte para interfaz COM (aplicaciones Windows) y/o por archivo de textos / DBF (línea de comandos), json o cualquier otro formato de archivo de intercambio soportado. 

**Importante:** El soporte comercial se brinda sólo para los webservices y versiones contratadas, no incluye acceso ni cobertura para futuros webservices o cambios mayores (por ej. nuevas resoluciones o modificaciones de AFIP, actualizaciones técnicas por cuestiones de seguridad, mejoras en el lenguaje de programación, etc.) 

**Aclaraciones:**: El paquete puntual de 1h abarca sólo 1 semana de consultas y no contempla el acceso a actualizaciones ni a instaladores. El soporte mínimo de 2hs no incluye consultas ni ajustes (atención limitada para instalación solo por email). Se encuentra publicada la documentación y ejemplos genéricos, en caso de necesidades particulares o mayor acompañamiento, recomendamos un soporte básico o superior. La cantidad de meses de cobertura varía dependiendo del plan contratado.

### Aclaraciones

Las cantidad de horas mencionada en cada plan de soporte es un estimativo, basado en un calculo de 1 hora por cada consulta / pedido (email, chat, llamado telefónico, etc. tanto pre-venta como pos-venta), aunque algunos temas pueden requerir mayor cantidad (incluye no solo el tiempo de la interacción con el cliente, sino también el mantenimiento, seguimiento, documentación y otras tareas administrativas que realizamos internamente, incluyendo ajustes preventivos y correcciones generales aunque no la haya solicitado directamente el cliente, tendientes a la mejora continua de nuestras soluciones).

En general, estos planes de soporte mencionados debería ser suficiente según nuestra experiencia para los casos generales, igualmente ofrecemos planes especiales a medida y ante cualquier duda estamos disponibles para consultas sobre el alcance del soporte contratado o si es necesario presupuestar adicionales.

Después del período mencionado en cada plan de soporte, el servicio no se renueva automáticamente, pero los clientes pueden solicitar soporte mínimo adicional (hasta 4 hs por 1 mes de cobertura), o contratar paquetes de abonos por mantenimiento y similares (generalmente trimestrales o anuales).

Las horas de soporte no son utilizables ni acumulables fuera del período facturado, y si bien se realizan los esfuerzos razonables para ofrecer asesoramiento y soporte técnico comunitario gratuito (ver [Foro público de noticias y consultas](https://groups.google.com/forum/#!forum/pyafipws)), no existe obligación ni podemos garantizar la atención a aquellos usuarios que no tengan contratado soporte comercial vigente. 


### Consideraciones generales

- Los precios están sujetos a modificaciones y pueden variar sin previo aviso (valor hora de referencia: $28.400/h Nov.2024).
- El tiempo promedio de respuesta es en el día (<24hs), pudiendo variar dependiendo de cada caso puntual.
- Queda a criterio de Sistemas Ágiles elegir los tiempos, prioridad y modalidad de prestación de los servicios.
- Se ofrecen demostraciones sin cargo y el código fuente está publicado, por lo que una vez contratado el servicio, no se aceptarán reclamos ni se efectuarán devoluciones.

El software es un desarrollo propio, previo, no exclusivo ni confidencial, Copyright 2008/2024 por Mariano Alejandro Reingart. 
Se reservan los derechos de autor Ley 11723. Se autoriza el uso, incorporación y distribución de la solución a la empresa contratante de los servicios, junto a su sistema de gestión/facturación. Se prohíbe el relicenciamiento a terceros.

Los servicios detallados en el presente serán prestados sólo al profesional o a empleados de la empresa contratante, no a terceros ni a clientes de la misma. 

### Disclaimer / Aviso Legal

Toda información es proporcionada a Titulo Informativo. El programa es software libre liberado bajo licencia GPLv3 (ver [Licencia](wiki:PyAfipWs#Licencia)) y se entrega como está, sin garantías explícitas ni implícitas de ningún tipo, incluyendo sin limitación, pérdida de ganancias, interrupción de negocios, pérdida de programas u otros datos en sistemas de computación o cualquier otro reclamo. Al usarlo acepta hacerlo bajo su propia responsabilidad, conociendo la normativa y reglamentaciones existentes.

Estos términos y condiciones se rigen y elaboran en base a las leyes de la República Argentina.  
Si el descargo de responsabilidad de garantía y el límite de responsabilidad proporcionado anteriormente no tiene efectos legales de acuerdo a otras leyes aplicables, los juzgados deberán aplicar la ley local que más se asemeje a una renuncia absoluta de la responsabilidad civil concerniente al Programa.

En caso de controversias respecto del presente, las partes pactan la jurisdicción de los Tribunales Ordinarios Civiles y Comerciales de la Ciudad de Morón (Provincia de Buenos Aires), renunciando expresamente a cualquier otro fuero que pudiere corresponder.
## Referencias Comerciales

Con más de 7 años de experiencia en el mercado dedicados a Factura Electrónica, la interfaz ha sido descargada miles de veces desde el [Sitio del Proyecto en GoogleCode](http://code.google.com/p/pyafipws/downloads/list), cuenta con una grupo de usuarios de más de cien miembros (ver [PyAfipWs en GoogleGroups ](http://groups.google.com/group/pyafipws)) y a Abril de 2013 tenemos más de 300 clientes que han contratado nuestros servicios, en los siguientes rubros:

- Empresas y desarrolladores de Sistemas de Gestión y ERP Corporativos
- Distribuidores, Consumo Masivo y Retail
- Productos Farmaceuticos y Hospitalarios
- Importadores y Exportadores
- Empresas de Turismo
- Editoriales, Librerías y Diarios
- Proveedores de Internet y Televisión por Cable
- Profesionales Independientes
- Servicios de facturación e impresión masivos

Clientes Destacados:

- Latin America Group - The Coca-Cola Company
- La Hispano Argentina Curtiembre SA
- Agro Aceitunera SA (Nucete)
- Boehringer Ingelheim S.A.
- Alliance One Tobacco Argentina SA
- TUPPERWARE Brands Argentina
- Alfajores Jorgito SA
- Droguería 20 de Junio SA
- Grupo Solunet S.A. (ISP)
- Diario El Litoral SRL
- Scienza Argentina
- E-Payment SRL (!DineroMail)
- Canal 4 Carlos Pelegrini S.R.L
- FILA Argentina
- Maximo Bauducco S.A.
- Gamisol y Cía S.A.
- Quantum Consulting SRL - Consultora en desarrollo e implementación de software.
- Qplus Consultores
- Natural Software SRL
- Belgrano Software S.A.
- Tierra Byte SA
- Asoc. Arg. Arventista del 7 día (Granix)
- Hreñuc SA (Rosamonte)
- Rafaela Alimentos SA
- CLYFER - Cooperativa de Luz y Fuerza electríca Rojas LTDA 
- Alliance one tabacco Argentina SA
- CTM Cooperativa Agroindustrial de Misiones
- BINOVA Soluciones
- entre otros

Por cuestiones de privacidad, la información de contacto y detalle de las referencias comerciales esta disponible bajo requerimiento por email.

A su vez, hemos presentado la interfaz en conferencias y eventos de software libre:

- [Artículo](http://www.41jaiio.org.ar/sites/default/files/15_JSL_2012.pdf) (ISSN: 1850-2857) y  [Charla](https://sl.linti.unlp.edu.ar/wp-content/uploads/2012/08/PyAfipWs_41JAIIO2.pdf) en las [JAIIO 2012](http://www.41jaiio.org.ar/) (Jornadas Argentinas de Informática Organizadas por SADIO y celebrado en la Universidad de La Plata, [Simposio de Software Libre](http://www.41jaiio.org.ar/sites/default/files/ProgramaJSL.pdf))
- [Charla en la CISL 2011](http://www.cisl.org.ar/). [Presentación](http://t.co/albZqNY) - [Video](http://t.co/tsRTnNg) (Conferencia Internacional de Software Libre, celebrada en la Biblioteca Nacional)
- [Reunión de desarrollo](http://ar.pycon.org/2012/projects/index#29) en la Conferencia Python Argentina 2013 (Buenos Aires)
- [Charla en Conferencia Python Argentina 2010](http://ar.pycon.org/2010/activity/accepted#451) (Córdoba, Universidad Siglo 21)
- [Charla (r) en Conferencia Python Argentina 2009](http://ar.pycon.org/2009/conference/schedule/event/37/)
- Curso en la ACP 2010 y Curso en la ACP 2009 (Materiales)
- Disertación en Conferencia Conurbania 2009
- Disertación (r) en Jornadas Regionales de Software Libre 2010

Esta interfase también se ofrecía por !TrabajoFreelance.com, ver [Comentarios](http://www.trabajofreelance.com.ar/perfil-marianix:reputacion)
## Capacitación

- [Manual de Uso](wiki:ManualPyAfipWs)
- Ver [Curso en la ACP](http://www.clubdeprogramadores.com/cursos/CursoMuestra.php?Id=485)

## Novedades

- Ver [Grupo de Noticias en Google](http://groups.google.com.ar/group/pyafipws)

## Contacto

Para mayor información, consultar por mail a [[reingart@gmail.com](mailto:facturaelectronica@sistemasagiles.com.ar],) (directo), [r.castrogiovani@gmail.com] (directo) o telefónicamente de Lu a Vi de 10 a 17hs al 15-3048-9211

Para soporte de la comunidad gratuito, ver [Foro Público](http://groups.google.com/group/pyafipws) (grupo google), revisar la [lista de temas](http://code.google.com/p/pyafipws/issues/list?can=1&q=) y/o [crear uno nuevo](http://code.google.com/p/pyafipws/issues/entry) 

PyAfipWs Copyright 2008, 2009, 2010, 2011, 2012, 2013, 2014, 2015, 2016, 2017, 2018, 2019, 2020, 2021, 2022, 2023, 2024 por MarianoReingart

**[https://link.mercadopago.com.ar/colaboracionespyafip] Colaboraciones**