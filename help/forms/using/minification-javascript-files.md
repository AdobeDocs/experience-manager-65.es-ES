---
title: Minificación de los archivos JavaScript
seo-title: Minificación de los archivos JavaScript
description: Instrucciones para generar código reducido después de las personalizaciones del espacio de trabajo de AEM Forms para optimizar los archivos JS para la web.
seo-description: Instrucciones para generar código reducido después de las personalizaciones del espacio de trabajo de AEM Forms para optimizar los archivos JS para la web.
uuid: ad91e380-a988-4740-9534-e09657e0322a
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: c88a3013-5da2-4b09-9f29-ac1fb00822ec
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Minificación de los archivos JavaScript {#minification-of-the-javascript-files}

La minimización elimina del código fuente los caracteres redundantes, como espacio en blanco, nueva línea y comentarios. Esto mejora el rendimiento al reducir el tamaño del código. Aunque la minimización no afecta a la funcionalidad, reduce la legibilidad del código.

Para generar código reducido para cambios semánticos, siga estos pasos.

1. Copie `client-html/src/main/webapp/js` desde src-package en el sistema de archivos.

   >[!NOTE]
   >
   >Consulte [Introducción a la personalización del espacio de trabajo](/help/forms/using/introduction-customizing-html-workspace.md) de AEM Forms para obtener más información sobre los paquetes.

1. Actualice las rutas en `main.js` las que se encuentran en client-html/src/main/webapp/js, para ver las vistas/modelos agregados/actualizados.

   Por ejemplo, la adición de un nuevo modelo Sharequeue, por ejemplo, mySharequeue, cambia:

   ```
   sharequeuemodel : pathprefix + 'runtime/models/sharequeue',
   
   To
   
   sharequeuemodel : pathprefix + 'runtime/myModels/mySharequeue',
   ```

1. Actualice `registry-config.xml, located at client-html/src/main/webapp/js/resource_generator,` en caso de que se produzca un cambio o adición de alias en `main.js`.

   Por ejemplo, la adición de un nuevo modelo Sharequeue, por ejemplo, mySharequeue, cambia:

   ```xml
   <sharequeue
               name="sharequeue"
               path="runtime/models/sharequeue.js"
               service="service"/>
   
   To
   
   <sharequeue
               name="sharequeue"
               path="runtime/myModels/mySharequeue.js"
               service="service"/>
   ```

1. En client-html/src/main/webapp/js/minifier, ejecute el comando:

   ```shell
   mvn clean install
   ```

   Genera una carpeta de archivos minificados, en client-html/src/main/webapp/js con main.js y registration.js minimizados.

>[!NOTE]
>
>La minimización solo funcionará en JVM de 64 bits.

>[!NOTE]
>
>Si minimiza, la actualización se verá afectada.

**[Comuníquese con la asistencia técnica](https://www.adobe.com/account/sign-in.supportportal.html)**
