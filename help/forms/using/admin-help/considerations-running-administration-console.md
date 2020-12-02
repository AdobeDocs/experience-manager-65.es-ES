---
title: Consideraciones al ejecutar AdministrationConsole
seo-title: Consideraciones al ejecutar AdministrationConsole
description: Este documento lista algunos puntos que deben tenerse en cuenta al ejecutar la Consola de administración.
seo-description: Este documento lista algunos puntos que deben tenerse en cuenta al ejecutar la Consola de administración.
uuid: e260f187-4728-44f3-a5c1-7388ff3965c4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 525c4afc-e109-4546-b78c-1efee63edc43
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 0%

---


# Consideraciones al ejecutar la Consola de administración {#considerations-when-running-administrationconsole}

Estos son algunos aspectos a tener en cuenta al ejecutar la Consola de administración:

* Si accede a la consola de administración mediante la dirección URL `https://[hostname]:'port'/adminui`, el nombre de host especificado no puede contener caracteres de subrayado. De lo contrario, es posible que los vínculos a algunas áreas de la consola de administración no funcionen correctamente.
* Si ejecuta la consola de administración en el Explorador de Windows en un SO japonés, puede solucionar estos problemas:

   * Al hacer clic en un vínculo regresa a la página de inicio de sesión en lugar del vínculo esperado.
   * Al hacer clic en un vínculo se muestra un error de permiso.

   Se recomienda ejecutar la consola de administración desde otro navegador, como Mozilla Firefox, para garantizar que no se produzca ningún error en los vínculos.

* No utilice caracteres de barra invertida () al realizar búsquedas en la consola de administración.

