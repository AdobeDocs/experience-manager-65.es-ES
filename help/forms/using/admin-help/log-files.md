---
title: Archivos de registro
seo-title: Archivos de registro
description: Los eventos como errores de inicio o durante la ejecución se registran en los archivos de registro del servidor de aplicaciones, que se pueden abrir con cualquier editor de texto.
seo-description: Los eventos como errores de inicio o durante la ejecución se registran en los archivos de registro del servidor de aplicaciones, que se pueden abrir con cualquier editor de texto.
uuid: 6ed9fdcd-ff02-4b35-893f-09261a6a557a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: cf140483-470f-4bff-8870-304207508aab
translation-type: tm+mt
source-git-commit: d3719a9ce2fbb066f99445475af8e1f1e7476f4e

---


# Log files {#log-files}

Los eventos como errores de inicio o durante la ejecución se registran en los archivos de registro del servidor de aplicaciones. Si tiene problemas al implementar en el servidor de aplicaciones, puede utilizar los archivos de registro para ayudarle a encontrar el problema. Puede abrir los archivos de registro con cualquier editor de texto.

(JBoss) Los siguientes archivos de registro se encuentran en el `[appserver root]/server/[server]/log` directorio:

* boot.log
* server.log.*[aaaa-mm-dd]*
* server.log

(WebLogic) Los archivos de registro de dominio se encuentran en el `[appserverdomain]` directorio y los archivos de registro del servidor se encuentran en el `[appserverdomain]/servers/[appserver name]/logs` directorio:

* `access.log`
* `[appserver name].log`
* `[appserver name].out.[incremental number]`

(WebSphere) Los siguientes archivos de registro se encuentran en el `[appserver root]/profiles/default/logs/[appserver name]` directorio:

* SystemErr.log
* SystemOut.log
* StartServer.log

