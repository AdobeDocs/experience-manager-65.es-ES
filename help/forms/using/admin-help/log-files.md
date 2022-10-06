---
title: Archivos de registro
seo-title: Log files
description: Eventos como errores de inicio o en tiempo de ejecución se registran en los archivos de registro del servidor de aplicaciones, que se pueden abrir con cualquier editor de texto.
seo-description: Events such as run-time or startup errors are recorded to the application server log files, which can be  opened using any text editor.
uuid: 6ed9fdcd-ff02-4b35-893f-09261a6a557a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: cf140483-470f-4bff-8870-304207508aab
exl-id: 23a65be4-3277-4c73-9189-a9b4d7be73cd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---

# Archivos de registro {#log-files}

Eventos como errores de inicio o en tiempo de ejecución se registran en los archivos de registro del servidor de aplicaciones. Si tiene problemas de implementación en el servidor de aplicaciones, puede utilizar los archivos de registro para ayudarle a encontrar el problema. Puede abrir los archivos de registro con cualquier editor de texto.

(JBoss) Los siguientes archivos de registro se encuentran en la `[appserver root]/server/'server'/log` directorio:

* boot.log
* server.log.*[aaaa-mm-dd]*
* server.log

(WebLogic) Los archivos de registro de dominio se encuentran en el `[appserverdomain]` y los archivos de registro del servidor se encuentran en la variable `[appserverdomain]/servers/[appserver name]/logs` directorio:

* `access.log`
* `[appserver name].log`
* `[appserver name].out.[incremental number]`

(WebSphere) Los siguientes archivos de registro se encuentran en la `[appserver root]/profiles/default/logs/[appserver name]` directorio:

* SystemErr.log
* SystemOut.log
* StartServer.log
