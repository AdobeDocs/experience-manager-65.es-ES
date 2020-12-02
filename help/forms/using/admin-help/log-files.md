---
title: Archivos de registro
seo-title: Archivos de registro
description: Eventos como errores de inicio o durante la ejecución se registran en los archivos de registro del servidor de aplicaciones, que se pueden abrir con cualquier editor de texto.
seo-description: Eventos como errores de inicio o durante la ejecución se registran en los archivos de registro del servidor de aplicaciones, que se pueden abrir con cualquier editor de texto.
uuid: 6ed9fdcd-ff02-4b35-893f-09261a6a557a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: cf140483-470f-4bff-8870-304207508aab
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---


# Archivos de registro {#log-files}

Eventos como errores de inicio o durante la ejecución se registran en los archivos de registro del servidor de aplicaciones. Si tiene problemas al implementar en el servidor de aplicaciones, puede utilizar los archivos de registro para ayudarle a encontrar el problema. Puede abrir los archivos de registro con cualquier editor de texto.

(JBoss) Los siguientes archivos de registro se encuentran en el directorio `[appserver root]/server/'server'/log`:

* boot.log
* server.log.*[aaaa-mm-dd]*
* server.log

(WebLogic) Los archivos de registro de dominio se encuentran en el directorio `[appserverdomain]` y los archivos de registro del servidor se encuentran en el directorio `[appserverdomain]/servers/[appserver name]/logs`:

* `access.log`
* `[appserver name].log`
* `[appserver name].out.[incremental number]`

(WebSphere) Los siguientes archivos de registro se encuentran en el directorio `[appserver root]/profiles/default/logs/[appserver name]`:

* SystemErr.log
* SystemOut.log
* StartServer.log

