---
title: Configuración de fuentes de reserva
seo-title: Configuración de fuentes de reserva
description: Obtenga información sobre cómo configurar las fuentes de reserva.
seo-description: Obtenga información sobre cómo configurar las fuentes de reserva.
uuid: 2745541c-8c6d-4bb4-aa14-ec19afd6bc35
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d997a268-a40a-462d-badd-94f0731f7ba4
translation-type: tm+mt
source-git-commit: d3719a9ce2fbb066f99445475af8e1f1e7476f4e
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---


# Configuración de fuentes de reserva {#configuring-fallback-fonts}

Puede configurar manualmente el archivo FontManagerResources.properties para asignar las fuentes de formularios AEM predeterminadas a las fuentes de reserva (o sustituirlas) si las fuentes predeterminadas no están disponibles en el servidor. Este archivo de propiedad se encuentra en el archivo adobe-fontmanager.jar.

>[!NOTE]
>
>La configuración de fuentes de reserva también se aplica al servicio de ensamblador.

1. Vaya al archivo adobe-livecycle-*`[appserver]`*.ear en el directorio *`[aem-forms root]`*/configurationManager/export, haga una copia de seguridad y desempaquete el original.
1. Busque el archivo adobe-fontmanager.jar y desempaquéelo.
1. Busque el archivo FontManagerResources.properties y ábralo en un editor de texto.
1. Modifique los nombres y las ubicaciones de fuentes genéricas y de reserva según sea necesario y guarde el archivo.

   Las entradas de fuente del archivo FontManagerResources.properties son relativas al directorio *`[aem-forms root]`*/fonts. Si especifica fuentes que no son predeterminadas AEM las fuentes de formularios, debe instalar dichas fuentes dentro de esta estructura de directorio (ya sea dentro de un directorio existente o en uno recién creado).

   >[!NOTE]
   >
   >Si la fuente especificada o la fuente predeterminada no contiene un carácter Unicode específico o si no está disponible, el carácter se toma de una fuente alternativa según la siguiente prioridad:

   * Fuente específica de configuración regional
   * Fuente ROOT si no se ha establecido la configuración regional
   * Fuente genérica, buscada por orden establecido en la tabla de reserva

1. Vuelva a empaquetar el archivo adobe-fontmanager.jar.
1. Vuelva a empaquetar el archivo adobe-livecycle-*`[appserver]`*.ear y, a continuación, vuelva a implementarlo manualmente o ejecutando Configuration Manager.

>[!NOTE]
>
>No utilice Configuration Manager para volver a empaquetar el archivo adobe-livecycle-`[appserver]`.ear porque sobrescribirá las modificaciones con los valores predeterminados de los formularios AEM.

