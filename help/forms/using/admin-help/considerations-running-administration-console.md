---
title: Consideraciones al ejecutar la AdministrationConsole
seo-title: Considerations when running AdministrationConsole
description: Este documento enumera algunos puntos a tener en cuenta al ejecutar la consola de administración.
seo-description: This document lists a few points to consider when running Administration Console.
uuid: e260f187-4728-44f3-a5c1-7388ff3965c4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 525c4afc-e109-4546-b78c-1efee63edc43
exl-id: e15dae6f-d30d-4770-a5ca-34f522a01d31
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 3%

---

# Consideraciones al ejecutar la consola de administración {#considerations-when-running-administrationconsole}

Estas son algunas cuestiones que se deben tener en cuenta al ejecutar la consola de administración:

* Si accede a la consola de administración mediante la dirección URL `https://[hostname]:'port'/adminui`Sin embargo, el nombre de host especificado no puede contener guiones bajos. De lo contrario, es posible que los vínculos a algunas áreas de la consola de administración no funcionen correctamente.
* Si ejecuta la consola de administración en el Explorador de Windows en un sistema operativo japonés, puede encontrar estos problemas:

   * Al hacer clic en un vínculo, vuelve a la página de inicio de sesión en lugar de al vínculo esperado.
   * Al hacer clic en un vínculo, se muestra un error de permiso.

   Una práctica recomendada es ejecutar la consola de administración desde otro explorador, como Mozilla Firefox, para garantizar que ningún vínculo falle.

* No utilice caracteres de barra invertida () al realizar búsquedas en la consola de administración.
