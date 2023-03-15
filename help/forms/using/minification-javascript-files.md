---
title: Minificación de los archivos JavaScript
seo-title: Minification of the JavaScript files
description: Instrucciones para generar código minificado después de las personalizaciones de AEM Forms Workspace para optimizar los archivos JS para la web.
seo-description: Instructions to generate minified code after AEM Forms workspace customizations to optimize the JS files for the web.
uuid: ad91e380-a988-4740-9534-e09657e0322a
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: c88a3013-5da2-4b09-9f29-ac1fb00822ec
exl-id: d88c6831-8ae9-426d-acb5-2a7e066ad158
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 100%

---

# Minificación de los archivos JavaScript {#minification-of-the-javascript-files}

La minificación elimina del código fuente los caracteres redundantes, como los espacio en blanco, las líneas nuevas y los comentarios. Esto mejora el rendimiento al reducir el tamaño del código. Aunque la minificación no afecta a la funcionalidad, reduce la legibilidad del código.

Para generar código minificado para cambios semánticos, siga los siguientes pasos.

1. Copie `client-html/src/main/webapp/js` desde src-package en el sistema de archivos.

   >[!NOTE]
   >
   >Consulte [Introducción a la personalización de AEM Forms Workspace](/help/forms/using/introduction-customizing-html-workspace.md) para obtener más información sobre los paquetes.

1. Actualice las rutas de `main.js`, ubicado en client-html/src/main/webapp/js, para obtener modelos o vistas agregados o actualizados.

   Por ejemplo, si se agrega un nuevo modelo de Sharequeue, por ejemplo, mySharequeue, cambie lo siguiente:

   ```javascript
   sharequeuemodel : pathprefix + 'runtime/models/sharequeue',
   ```

   A

   ```javascript
   sharequeuemodel : pathprefix + 'runtime/myModels/mySharequeue',
   ```

1. Actualice `registry-config.xml, located at client-html/src/main/webapp/js/resource_generator,` en el caso de que haya algún cambio o adición de alias en `main.js`.

   Por ejemplo, si se agrega un nuevo modelo de Sharequeue, por ejemplo, mySharequeue, cambie lo siguiente:

   ```xml
   <sharequeue
               name="sharequeue"
               path="runtime/models/sharequeue.js"
               service="service"/>
   ```

   A

   ```xml
   <sharequeue
               name="sharequeue"
               path="runtime/myModels/mySharequeue.js"
               service="service"/>
   ```

1. Ejecute el siguiente comando en client-html/src/main/webapp/js/minifier:

   ```shell
   mvn clean install
   ```

   Este comando genera una carpeta de archivos minificados en client-html/src/main/webapp/js en la que main.js y register.js están minificados.

>[!NOTE]
>
>La minificación solo es compatible con JVM de 64 bits.

>[!NOTE]
>
>Si utiliza la minificación, la actualización se verá afectada.
