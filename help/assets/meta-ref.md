---
title: Referencia de esquemas de metadatos
description: 'Obtenga información sobre las convenciones estándar para describir metadatos de recursos, incluidos Dublin Core, IPTC y otros esquemas de metadatos. '
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Referencia de esquemas de metadatos {#metadata-schemata-reference}

La siguiente referencia incluye información sobre un esquema de metadatos concreto (en orden alfabético), así como una lista de propiedades y sus definiciones.

## Dublin Core {#dublin-core}

Los metadatos de Dublin Core proporcionan un conjunto estandarizado de convenciones para describir los recursos y facilitar su búsqueda. En Recursos AEM, Dublin Core describe recursos digitales, incluidos vídeo, sonido, imágenes y documentos.

El conjunto de elementos de metadatos básico de Dublín (DCMES) simple contiene 15 elementos de metadatos como se muestra en la tabla siguiente. Cada elemento Dublin Core es opcional y se puede repetir. Puede agregar o eliminar información de metadatos de Dublin Core como lo haría con metadatos específicos de tipo de medios.

Además del DCMES, hay otros elementos de metadatos creados por la Iniciativa Dublin Core. Consulte la Iniciativa [](https://dublincore.org/) Dublin Core para obtener más información.

| Propiedad | Descripción |
|---|---|
| colaborador | Persona o empresa responsable de contribuir al contenido. |
| cobertura | Ubicación geográfica o período de tiempo que cubre el activo. |
| creador | Persona o empresa responsable de la creación del contenido. |
| date | Fecha o período de tiempo asociado al activo. |
| Descripción | Más información sobre el recurso. |
| format | Formato de archivo, medio físico o dimensiones del recurso. AEM utiliza dc:format para denotar el tipo MIME del recurso. |
| identifier | Una referencia única al recurso. |
| language | Idioma del recurso (por ejemplo, en inglés). |
| publisher | Persona o empresa responsable de la disponibilidad del activo. |
| relation | Un recurso relacionado. |
| derechos | Información sobre quién tiene los derechos de este recurso. |
| source | Recurso relacionado del que se deriva el activo. |
| subject | Tema del recurso. |
| el título | Un nombre para el recurso. |
| tipo | La naturaleza o el género del recurso. |

## IPTC {#iptc}

El Consejo Internacional de Telecomunicaciones de Prensa (IPTC) es un consorcio de agencias de noticias de todo el mundo - uno de sus objetivos es desarrollar y mantener estándares técnicos. El IPTC definió un conjunto de estándares de metadatos de fotos para imágenes que son casi universalmente aceptados por los fotógrafos. Estas normas de metadatos formaban parte de la norma más amplia conocida como el Modelo de Intercambio de Información IPTC (IIM) creado en los años noventa.

Aunque la información del encabezado IPTC ha sido reemplazada mayormente por XMP, un esquema central IPTC y un esquema de extensión están disponibles para XMP. En los programas de imágenes, las propiedades XMP e IPTC están sincronizadas.
