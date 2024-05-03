---
title: Consideraciones al ejecutar la consola de administración
description: Este documento enumera algunos puntos a tener en cuenta al ejecutar la consola de administración.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e15dae6f-d30d-4770-a5ca-34f522a01d31
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# Consideraciones al ejecutar la consola de administración {#considerations-when-running-administrationconsole}

Estas son algunas cuestiones que se deben tener en cuenta al ejecutar la consola de administración:

* Si accede a la consola de administración mediante la dirección URL `https://[hostname]:'port'/adminui`Sin embargo, el nombre de host especificado no puede contener guiones bajos. De lo contrario, es posible que los vínculos a algunas áreas de la consola de administración no funcionen correctamente.
* Si ejecuta una consola de administración en el Explorador de Windows en un sistema operativo japonés, puede encontrar estos problemas:

   * Al hacer clic en un vínculo, vuelve a la página de inicio de sesión en lugar de al vínculo esperado.
   * Al hacer clic en un vínculo, se muestra un error de permiso.

  Se recomienda ejecutar la consola de administración desde otro explorador, como Mozilla Firefox, para garantizar que no se produzcan errores en los vínculos.

* No utilice caracteres de barra invertida () al realizar búsquedas en la consola de administración.
