---
title: Archivos de registro
description: Los eventos como los errores de tiempo de ejecución o de inicio se registran en los archivos de registro del servidor de aplicaciones, que se pueden abrir con cualquier editor de texto.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 23a65be4-3277-4c73-9189-a9b4d7be73cd
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 3%

---

# Archivos de registro {#log-files}

Los eventos, como los errores en tiempo de ejecución o de inicio, se registran en los archivos de registro del servidor de aplicaciones. Si tiene algún problema al implementar en el servidor de aplicaciones, puede utilizar los archivos de registro para ayudarle a encontrar el problema. Puede abrir los archivos de registro con cualquier editor de texto.

Los siguientes archivos de registro se encuentran en la variable `[appserver root]/server/'server'/log` directorio:

* boot.log
* server.log.*[aaaa-mm-dd]*
* server.log

(WebLogic) Los archivos de registro de dominio se encuentran en la `[appserverdomain]` y los archivos de registro del servidor se encuentran en la `[appserverdomain]/servers/[appserver name]/logs` directorio:

* `access.log`
* `[appserver name].log`
* `[appserver name].out.[incremental number]`

(WebSphere) Los siguientes archivos de registro se encuentran en la `[appserver root]/profiles/default/logs/[appserver name]` directorio:

* SystemErr.log
* SystemOut.log
* StartServer.log
