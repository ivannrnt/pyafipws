= Trazabilidad de Productos Fitosanitarios SENASA - Web Service para Empresas (WS_INFO_EMPRESAS / WS_DATOS_GENERALES) =

Interfaz para Servicio Web de Trazabilidad de Productos Fitosanitarios (API REST) correspondiente a la  [Resolución 369/2021](https://www.boletinoficial.gob.ar/detalleAviso/primera/246753/20210712) del Servicio Nacional de Sanidad y Calidad Agroalimentaria (SENASA) conformado por los servicios Operaciones, referida a los Web Service que tendrá Senasa con las empresas (formuladora, sintetizadora, fraccionadora y distribuidor/comercializador) quienes informaran por servicio sus actividades y/o movimientos.
Y Consultas, para que las empresas/usuarios realicen consultas de códigos generales.


## Índice
[[TOC(noheading,inline,depth=2)]]

## Introducción

Biblioteca para el web service de SENASA/PAMI que permite automatizar la gestión de las trazabilidad de productos fitosanitarios: 

- Interfaz COM: Simil DLL/OCX, embebible para aplicaciones programadas en lenguajes visuales bajo windows (Visual Basic, Visual Fox Pro, SAP, etc.)
- Interfaz por consola (linea de comandos / archivo de texto): similar a aplicativos SIAP para sistemas legados (ej. RM COBOL) multiplataforma (DOS, Windows, Unix)
- Interfaz por tablas DBF: compatible con dBase, !FoxPro, Clipper -proximamente-
- Interfaz por base de datos: compatible con conectores ODBC (MS SQL Server), PostgreSQL y otros (Oracle, DB2) -proximamente-

Cubre totalmente el proceso, puede ser adaptado a programas existentes y no es requerido intervención del usuario.



## Descripción General

Sujetos alcanzados: Es de aplicación obligatoria en todo el territorio de la República Argentina, para todas las personas humanas o jurídicas que importen, exporten, sinteticen, formulen, fraccionen, distribuyan, comercialicen, depositen y/o ejerzan la tenencia, con cualquier fin, de productos fitosanitarios inscriptos en el Registro Nacional de Terapéutica Vegetal del SENASA

Entrada en vigencia: 22/09/2021 Prorrogado al 21/12/2021 por [RG485/21](https://www.boletinoficial.gob.ar/detalleAviso/primera/249901/20210922)


## Descargas

- Instalador: 
- [https://www.sistemasagiles.com.ar/soft/pyafipws/PyAfipWs-SENASA-2.7.2902-32bit+trazaagroops_0.1e-homo.exe] (homologación)
 
- Documentación Oficial:
- [WS_Info_Empresas (Operaciones)](https://www.argentina.gob.ar/sites/default/files/2021/08/ws_senasa-operaciones_v1.5-20.12f.pdf)
- [WS_Datos_Generales (Consultas)](https://www.argentina.gob.ar/sites/default/files/2021/08/ws_senasa_consultas_v1.1-9dic21.pdf)
- Ejemplo en VB: 
- Ejemplo en VFP: 
- Código Fuente (Python): 

URL:

- Entrenamiento: [https://test.senasa.gov.ar/agrotraza/src/api/]
- Producción: [https://aps2.senasa.gov.ar/agrotraza/src/api/]



## Métodos
**WS_Info_Empresas (Operaciones)**

- **`AltaEnvio()`**
- **`AceptarEnvio()`**
- **`CancelarEnvio()`**
- **`RechazoTotalEnvio()`**
- **`AceptaRechazoTotalEnvio()`**
- **`RechazoParcialEnvio()`**
- **`AceptarRechazoParcialEnvio()`**
- **`ContingenciaEnvio()`**
- **`ConsultaEnvio()`**
- **`AltaContingencia()`**
- **`EliminarContingencia()`**
- **`AltaAutoconsumoFP()`**
- **`EliminarAutoconsumoFP()`**

**WS_Datos_Generales (Consultas)**

- **`ConsultaStockIngredienteActivo()`**
- **`ConsultaStockProductoFormulado()`**
- **`ConsultarDeposito()`**
- **`ConsultarEstadosDeposito()`**


## Costos y Condiciones

Por soporte comercial consultar al (011) 15-3048-9211 o por mail a info@sistemasagiles.com.ar

Costos de soporte estimativos (puede variar dependiendo de las necesidades de cada implementación puntual):

 
Para soporte sin cargo de la comunidad, revisar la [lista de temas](https://github.com/reingart/pyafipws/issues) y/o [crear uno nuevo](https://github.com/reingart/pyafipws/issues/new). 
Por novedades y consultas genereales, puede usar el  [Google Groups](https://groups.google.com/forum/#!forum/pyafipws) (Foro Público).
Código fuente en [GitHub](https://github.com/reingart/pyafipws/).


MarianoReingart




