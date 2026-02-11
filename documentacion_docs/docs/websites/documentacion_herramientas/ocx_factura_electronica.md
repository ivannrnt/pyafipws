# Factura Electrónica: Ventajas Automatización COM PyAfipWs vs OCX y otros 

Nuestra interfaz PyAfipWs es un componente DLL/EXE de automatización COM similar a un OCX/ActiveX para Windows compatible con varios lenguajes (Visual Basic, Visual Fox Pro, Delphi, PHP, .Net, Java, etc.) y además cuenta con una herramienta por linea de comando - archivo de texto similar al formato SIAP/RECE de compatibilidad universal (especialmente lenguajes para "DOS": RM/Cobol, dBase, !FoxPro, QBasic, etc.).

Funcionalmente, un objeto de automatización COM se crea simplemente llamando a la función `CreateObject("objeto")` y luego se accede a sus propiedades y métodos de manera idéntica a un control OCX. Ver ejemplos completos en ManualPyAfipWs

Respecto a un OCX, nuestra interface PyAfipWs tiene las siguientes ventajas:

- Factura Electrónica en 10 líneas, sin necesidad de referencias ni agregar controles ni constantes
- Funciona en aplicaciones Visuales (con formularios) y también en no Visuales (módulos de código). Ver ejemplos completos: [VB](https://github.com/reingart/pyafipws/blob/master/ejemplos/wsfev1/wsfev1.bas), [VFP](https://github.com/reingart/pyafipws/blob/master/ejemplos/wsfev1/wsfev1.prg), [VB.NET](https://github.com/reingart/pyafipws/blob/master/ejemplos/wsfev1/wsfev1.vb), [PHP](https://github.com/reingart/pyafipws/blob/master/ejemplos/wsfe/php/ejemplo.php), [Delphi](https://github.com/reingart/pyafipws/blob/master/ejemplos/wsfe/delphi/Project1.dpr), etc.
- Compatible con herramientas de oficina ([Access 97](https://storage.googleapis.com/google-code-archive-downloads/v2/code.google.com/pyafipws/pyafipws.mdb) / [Access 2000](https://storage.googleapis.com/google-code-archive-downloads/v2/code.google.com/pyafipws/pyafipws2k.mdb), Excel, etc.) y programas de terceros con soporte COM ([SAP ABAP](./pyafipws.md#ejemplo-para-sap-abap), [Fujitsu NetCobol](./pyafipws.md#ejemplo-para-fujitsu-net-cobol), [Clarion](./pyafipws.md#ejemplo-para-clarion), [Power Builder](./pyafipws.md#ejemplo-para-powerbuilder), etc.)
- Herramientas alternativas por linea de comandos para soporte de archivos de intercambio simil [SIAP RECE](./manualpyafipws.md#interfase-por-archivos-de-texto-símil-siap---rece) (TXT ancho fijo COBOL, DBF, JSON, XML, etc.)
- Actualización simple, sin necesidad de modificar el proyecto ni recompilar
- Tipos de datos dinámicos y métodos flexibles para simplicidad y compatibilidad con lenguajes legados

Al ser **Software libre de código abierto totalmente publicado**:

- Protege su inversión al poder acceder al [código fuente](https://github.com/reingart/pyafipws) gratuitamente **sin costo** ni ninguna restricción o limitación técnica
- Programado en Python, un lenguaje moderno, multipropósito, simple y claro usado por Google (entre otras empresas), con una [comunidad local PyAr](http://python.org.ar/pyar/) de miles de personas en Argentina.
- Liberado a la comunidad: probado por múltiples desarrolladores y proyectos, con más de [1000 miembros en el grupo de usuarios](http://groups.google.com/group/pyafipws/about) y [varios desarrolladores](https://github.com/reingart/pyafipws/graphs/contributors) en el proyecto principal
- Multiplataforma: funciona tanto en Windows (XP, 2000, 2003, 7, 8) tanto 32bits como 64 bits, Linux (Debian, Ubuntu, Redhat, Fedora) y posiblemente Mac, Solaris, etc.
- "Licencia comercial" disponible: más de [PyAfipWs#ReferenciasComerciales 200 clientes] han utilizado esta interfaz en diversos entornos y ambientes de programación.

Ventajas adicionales:

- Único archivo autoinstalable de ~2.5MB todo incluido, sin dependencias a .Net ni Java
- Instalación guiada simple en un click, con posibilidad de embeberla en otros instaladores (modo "silencioso" o desatendido)
- Incorporable a sistemas propietarios (ver condiciones) sin restricciones de usuarios ni licencias adicionales
- Reconexión automática y características avanzadas de reprocesamiento, depuración y manejo de excepciones
- Soporte de librerías HTTP avanzadas (Ej. servidor proxy MS ISA Server y verificación de certificados)
- Interfaces adicionales para generación de PDF, códigos de barra y envío de email.
- Implementación concisa y unificada, abstrayendo la complejidad y diferencias de los webservices de AFIP
- Flexibilidad para el uso de certificados (pueden almacenarse de manera segura en base de datos o similar)
- Con implementación de referencia completa y funcional: Aplicativo PyRece (incluyendo gestión de CAE, generación de PDF y envío por email)
- Herramienta opcional por línea de comando ("D.O.S.") (útil para pruebas y consultas !UltNro, !LastId, etc.)
- Interfaz por archivo de texto y/o soporte de tablas DBF (lenguajes legados: Clipper, dBase, !FoxPro, Cobol, XBase, Harbour)

Este proyecto no solo es una interfaz particular, ademas cuenta con herramientas utilitarias y aplicativos para cubrir las distintas soluciones necesarias para factura electrónica:

- `PYAFIPWS.EXE` y `PYAFIPWS.DLL`: Servidor de Automatización COM (expone los servicios de factura electrónica a otros lenguajes)
- `RECE.EXE`: utilitario para facturación electrónica mediante archivo de texto formato simil SIAP/RECE (por consola)
- `RECEB.EXE`: utilitario para facturación electrónica de bienes de capital mediante archivo de texto (por consola)
- `RECEX.EXE`: utilitario para facturación electrónica de exportación mediante archivo de texto (por consola)
- `RECE1.EXE`: utilitario para facturación electrónica de mercado interno mediante archivo de texto o tablas DBF (por consola)
- `RG1361.EXE`: utilitario para almacenamiento de duplicados electrónicos para SIAP SIRED - RG 1361 (por consola)
- `WSAA.EXE`: utilitario para gestionar el ticket de acceso a los servicios web
- `PYRECE.EXE`: aplicativo para facturación electrónica similar a SIAP/RECE (interfaz gráfica - "visual")
- `FE.PY`: herramienta para facturación electrónica desde base de datos (servicio)

Este proyecto es y se sustenta en Software Libre, particularmente:

- [Python](http://www.python.org): Lenguaje de programación moderno, estable y flexible (ver [PyAr](http://www.python.org.ar) - Comunidad Argentina)
- [M2Crypto](http://chandlerproject.org/bin/view/Projects/MeTooCrypto): Vínculos python para la robusta librería [OpenSSL](http://www.openssl.org/) (encriptación y firma digital)
- [httplib2](https://pypi.python.org/pypi/httplib2): Librería avanzada de acceso web

Para más detalles técnicos respecto al Servidor COM de autenticación y su funcionamiento desde Python ver [ejemplo](http://python.org.ar/pyar/Recetario/ServidorCom)

Para más información, ver [FacturaElectronica](../factura_electronica.md) y [PyAfipWs](./pyafipws.md)