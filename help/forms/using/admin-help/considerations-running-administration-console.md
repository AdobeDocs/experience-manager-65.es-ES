---
title: Consideraciones al ejecutar la consola de administración
description: Este documento enumera algunos puntos a tener en cuenta al ejecutar la consola de administración.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e15dae6f-d30d-4770-a5ca-34f522a01d31
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---

# Consideraciones al ejecutar la consola de administración {#considerations-when-running-administrationconsole}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

Estas son algunas cuestiones que se deben tener en cuenta al ejecutar la consola de administración:

* Si accede a la consola de administración mediante la dirección URL `https://[hostname]:'port'/adminui`, el nombre de host especificado no puede contener caracteres de guion bajo. De lo contrario, es posible que los vínculos a algunas áreas de la consola de administración no funcionen correctamente.
* Si ejecuta una consola de administración en el Explorador de Windows en un sistema operativo japonés, puede encontrar estos problemas:

   * Al hacer clic en un vínculo, vuelve a la página de inicio de sesión en lugar de al vínculo esperado.
   * Al hacer clic en un vínculo, se muestra un error de permiso.

  Se recomienda ejecutar la consola de administración desde otro explorador, como Mozilla Firefox, para garantizar que no se produzcan errores en los vínculos.

* No utilice caracteres de barra invertida () al realizar búsquedas en la consola de administración.
