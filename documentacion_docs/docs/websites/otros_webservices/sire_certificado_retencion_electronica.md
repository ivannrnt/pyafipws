# WSSIRE - SISTEMA INTEGRAL DE RETENCIONES ELECTRONICAS, Certificado de retención electrónica


Interfaz para Servicio Web correspondiente a la emisión de un certificado C2005 en AFIP por parte de los sistemas del agente de retención. [RG4523/2019](http://servicios.infoleg.gob.ar/infolegInternet/anexos/325000-329999/325072/texact.htm) [RG3726/2015](http://biblioteca.afip.gob.ar/dcp/REAG01003726_2015_01_23)

## Descripción General

Este servicio permite únicamente la emisión de un certificado C2005 en AFIP por parte de los sistemas del agente de retención.

Publicación: Noviembre de 2019 [Documentación Oficial](https://www.afip.gob.ar/sire/documentos/SOAP-SIRE-IVA-Manualparaeldesarrollador_V1_0_0.pdf)

Esta aplicación deberá ser utilizada por los agentes de retención y/o percepción, a efectos de emitir los certificados de retención y/o percepción que los responsables deberán entregar a los sujetos pasibles de las mismas. 

La función principal del sistema es la carga de datos y la emisión de los certificados C2005 (Certificado de Retención/Percepción del Impuesto al Valor Agregado). (según [RG4523/19](http://biblioteca.afip.gob.ar/dcp/REAG01004523_2019_07_10))



## Estado

### Aplicación

Opcional, a partir del día 1 de Diciembre de 2019

Obligatorio,  desde el día 1 de Septiembre de 2020

Prorrogado por [TG 4798/2020](https://www.boletinoficial.gob.ar/detalleAviso/primera/234176/20200827), Obligatorio a partir del 1 de Diciembre de 2020

### URL

- https://ws-aplicativos-reca.homo.afip.gob.ar/sire/ws/v1/c2005/2005?wsdl (homologación)
- https://ws-aplicativos-reca.afip.gob.ar/sire/ws/v1/c2005/2005?wsdl (producción)

 
## Descargas e Instalación

Ver archivos y últimas actualizaciones para descargas en [GitHub](https://github.com/reingart/pyafipws/releases) (actualizado)

- Instalador: [https://www.sistemasagiles.com.ar/soft/pyafipws/PyAfipWs-2.7.2317-32bit+wsaa_2.12c+sire_1.01b-homo.exe]

- Ejemplos de código (última versión de desarrollo):
- Visual Basic 5/6: [https://github.com/reingart/pyafipws/blob/develop/ejemplos/ws_sire/sirews.bas]
 
 
- Código Fuente (Python): ver [https://github.com/reingart/pyafipws/blob/develop/ws_sire.py] 


## Instalación

Está disponible el instalador, simplemente seguir los pasos:

- Aceptar la licencia
- Seleccionar carpeta, por ej `C:\WSSIRE`
- Instalación y registración automática

Para más información ver el [Manual de Uso](../documentacion_herramientas/manualpyafipws.md#instalacion)


## Costos y Condiciones


(ver [Condiciones del Soporte Comercial](../documentacion_herramientas/pyafipws.md#costos-y-condiciones)).

Ofrecemos soporte técnico comercial (pago), independiente a la AFIP, desarrollos especiales, interfaces web, etc. 
Obtenga mas información enviando un mail a info@pyafipws.com.ar (011) 15-3048-9211 (asesoramiento sin cargo)

A su vez, se liberará el código fuente bajo licencia GPLv3 (software libre), al igual que se hizo con el restos de los servicios web. Para más detalles ver página FacturaElectronica.

La información de esta página es proporcionada a titulo informativo.
