---
title: Configuración de fuentes de reserva
seo-title: Configuring fallback fonts
description: Aprenda a configurar fuentes de reserva.
seo-description: Learn how to configure fallback fonts.
uuid: 2745541c-8c6d-4bb4-aa14-ec19afd6bc35
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d997a268-a40a-462d-badd-94f0731f7ba4
feature: PDF Generator
exl-id: 76dd2b0c-9f16-47bf-a565-99277be750fb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---

# Configuración de fuentes de reserva {#configuring-fallback-fonts}

Puede configurar manualmente el archivo FontManagerResources.properties para asignar las fuentes de formularios AEM predeterminadas a las fuentes de reserva (o sustituirlas) si las fuentes predeterminadas no están disponibles en el servidor. Este archivo de propiedad se encuentra en el archivo adobe-fontmanager.jar .

>[!NOTE]
>
>La configuración de fuentes de reserva también se aplica al servicio de ensamblador.

1. Vaya a adobe-livecycle-*`[appserver]`*.ear en la variable *`[aem-forms root]`*/configurationManager/export directorio, haga una copia de seguridad y desempaquete el original.
1. Busque el archivo adobe-fontmanager.jar y desempaquete el archivo.
1. Busque el archivo FontManagerResources.properties y ábralo en un editor de texto.
1. Modifique las ubicaciones y los nombres de fuentes genéricas y de reserva según sea necesario y guarde el archivo.

   Las entradas de fuente del archivo FontManagerResources.properties se refieren a la variable *`[aem-forms root]`* directorio /fonts. Si especifica fuentes que no son predeterminadas AEM fuentes de formularios, debe instalar esas fuentes dentro de esta estructura de directorios (ya sea dentro de un directorio existente o en uno recién creado).

   >[!NOTE]
   >
   >Si la fuente especificada o la fuente predeterminada no contienen un carácter Unicode específico o si no está disponible, el carácter se toma de una fuente de reserva de acuerdo con la siguiente prioridad:

   * Fuente específica de configuración regional
   * Fuente ROOT si no se ha definido la configuración regional
   * Fuente genérica, buscada por orden establecido en la tabla de reserva

1. Vuelva a empaquetar el archivo adobe-fontmanager.jar.
1. Vuelva a empaquetar adobe-livecycle-*`[appserver]`*.ear y luego reimplementarlo manualmente o ejecutando Configuration Manager.

>[!NOTE]
>
>No utilice Configuration Manager para volver a empaquetar adobe-livecycle-`[appserver]`archivo .ear porque sobrescribirá las modificaciones con los valores predeterminados de los formularios AEM.
