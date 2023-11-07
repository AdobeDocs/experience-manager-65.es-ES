---
title: Configurar fuentes de reserva
description: Obtenga información sobre cómo configurar fuentes de reserva para AEM Forms. Puede utilizar el archivo FontManagerResources.properties para asignar manualmente las fuentes predeterminadas a las fuentes de reserva.
uuid: 2745541c-8c6d-4bb4-aa14-ec19afd6bc35
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d997a268-a40a-462d-badd-94f0731f7ba4
feature: PDF Generator
exl-id: 76dd2b0c-9f16-47bf-a565-99277be750fb
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 2%

---

# Configurar fuentes de reserva {#configuring-fallback-fonts}

AEM Puede configurar manualmente el archivo FontManagerResources.properties para asignar las fuentes predeterminadas de los formularios de la fuente predeterminada a la reserva (o sustituto) si las fuentes predeterminadas no están disponibles en el servidor. Este archivo de propiedades se encuentra en el archivo adobe-fontmanager.jar.

>[!NOTE]
>
>La configuración de fuentes de reserva también se aplica al servicio de ensamblador.

1. Vaya a adobe-livecycle-*`[appserver]`*.ear en el archivo *`[aem-forms root]`*/configurationManager/export, realizar una copia de seguridad y desempaquetar el original.
1. Busque el archivo adobe-fontmanager.jar y desempaquételo.
1. Busque el archivo FontManagerResources.properties y ábralo en un editor de texto.
1. Modifique las ubicaciones y los nombres de las fuentes genéricas y de reserva según sea necesario y guarde el archivo.

   Las entradas de fuente del archivo FontManagerResources.properties son relativas a *`[aem-forms root]`* directorio /fonts. AEM Si especifica fuentes que no son fuentes de formularios predeterminadas, debe instalarlas dentro de esta estructura de directorios (ya sea en un directorio existente o en uno recién creado).

   >[!NOTE]
   >
   >Si la fuente especificada o la fuente predeterminada no contiene un carácter Unicode específico o si no está disponible, el carácter se toma de una fuente de reserva según la siguiente prioridad:

   * Fuente específica de la configuración regional
   * Fuente ROOT si no se ha definido la configuración regional
   * Fuente genérica, buscada por orden establecido en la tabla de reserva

1. Vuelva a empaquetar el archivo adobe-fontmanager.jar.
1. Volver a empaquetar adobe-livecycle-*`[appserver]`*.ear y, a continuación, vuelva a implementarlo manualmente o ejecutando el Administrador de configuración.

>[!NOTE]
>
>No utilice el Administrador de configuración para volver a empaquetar adobe-livecycle-`[appserver]`AEM .ear, porque sobrescribirá las modificaciones con los valores predeterminados de los formularios de la aplicación de datos de la aplicación.
