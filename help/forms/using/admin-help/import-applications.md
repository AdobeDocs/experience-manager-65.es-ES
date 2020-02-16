---
title: Importar y administrar aplicaciones
seo-title: Importar y administrar aplicaciones
description: Obtenga información sobre cómo importar y administrar aplicaciones.
seo-description: Obtenga información sobre cómo importar y administrar aplicaciones.
uuid: 7fba6c4e-1a3e-4a4b-9201-acf2ff66a9df
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/importing_and_managing_applications_and_archives
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: dc53a6d0-317a-4abd-990c-455e13f8b824
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Importar y administrar aplicaciones{#import-and-manage-applications}

En los formularios AEM, una *aplicación* es un contenedor para almacenar recursos necesarios para implementar una solución de formularios AEM. Algunos ejemplos de recursos son diseños de formulario, fragmentos de formulario, imágenes, procesos, archivos DDX, guías de formulario, páginas HTML y archivos SWF. Durante la fase de desarrollo de un proyecto, los usuarios de Workbench pueden implementar aplicaciones directamente desde la vista Aplicaciones de Workbench. Una vez implementadas, estas aplicaciones aparecen en la consola de administración, en la ficha Aplicaciones de la página Administración de aplicaciones.

Cuando se completa una aplicación y está lista para su implementación en un servidor de producción, el usuario de Workbench la empaqueta en un archivo *de aplicación de formularios* AEM (.lca). A continuación, un administrador utiliza la consola de administración para importar e implementar el archivo de la aplicación mediante la ficha Aplicaciones de la página Administración de aplicaciones.

También puede utilizar la ficha Archivos de la página Administración de aplicaciones para importar las LCA que se crearon con Workbench 8.x.

>[!NOTE]
>
>Se sabe que los archivos LCA de una versión futura no son necesariamente compatibles con versiones anteriores. Si bien es posible ver e importar archivos LCA de una versión futura de formularios AEM (por ejemplo, una versión de vista previa), no se admite esta acción y puede provocar un comportamiento aberrante.

Utilice la ficha Aplicaciones para importar y administrar las aplicaciones creadas en Workbench. Los administradores de aplicaciones también pueden exportar la configuración del tiempo de ejecución para una aplicación. Exportar la configuración del tiempo de ejecución elimina la necesidad de reconfigurar manualmente los ajustes en el entorno de producción antes de iniciar las aplicaciones implementadas. El archivo de configuración de tiempo de ejecución contiene:

* configuración del servicio
* configuración del grupo
* configuración de extremo
* perfiles de seguridad

## Importar una aplicación o archivo {#import-an-application-or-archive}

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de aplicaciones.
1. Haga clic en Importar.
1. Haga clic en Examinar y seleccione el archivo .lca que desea importar y haga clic en Vista previa. La página Vista previa de la aplicación muestra información sobre la aplicación.
1. (Opcional) Para ver una lista de los recursos contenidos en la aplicación, haga clic en Ver recursos.
1. (Opcional) Para implementar los recursos en tiempo de ejecución, seleccione Implementar recursos en tiempo de ejecución cuando se complete la importación. Si no selecciona esta opción, puede implementar los recursos más adelante.
1. Haga clic en Importar. La aplicación aparece en la ficha Aplicaciones.
1. Inicie sesión en el repositorio de CRX con credenciales de administrador.
1. Navegar al contenido, a la represa y a las aplicaciones

   >[!NOTE]
   >
   >Las aplicaciones importadas se muestran en el nodo de aplicaciones.

1. Haga clic en una de las aplicaciones importadas.

   La ficha Propiedades de la derecha muestra las propiedades del nodo CRX seleccionado.

   La propiedad **syncState** indica el estado de sincronización de datos entre el servidor de formularios AEM y el repositorio de CRX. Tan pronto como se inicia el proceso de importación, este estado se establece en 0 (cero). Este estado indica que los datos no están sincronizados actualmente. Cuando se sincronizan los datos, el estado se establece en 1.

## Implementación de una aplicación {#deploy-an-application}

Puede implementar las aplicaciones importadas o que los usuarios de Workbench importaron desde Workbench.

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de aplicaciones.
1. Seleccione la casilla de verificación situada junto a la aplicación que desea implementar y haga clic en Implementar.
1. Haga clic en Aceptar en el cuadro de diálogo de confirmación que aparece.

## Despliegue de una aplicación {#undeploy-an-application}

Puede anular la implementación de aplicaciones desde el motor de ejecución.

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de aplicaciones.
1. Seleccione la casilla de verificación situada junto a la aplicación que desea cancelar la implementación y haga clic en Desimplementar.
1. Haga clic en Aceptar en el cuadro de diálogo de confirmación que aparece.

## Quitar una aplicación del servidor {#remove-an-application-from-the-server}

Cancele la implementación de la aplicación antes de quitarla del servidor.

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de aplicaciones.
1. Seleccione la casilla de verificación situada junto a la aplicación que desea eliminar y haga clic en Eliminar.
1. Haga clic en Aceptar en el cuadro de diálogo de confirmación que aparece.

## Importación de la configuración del tiempo de ejecución de una aplicación {#import-an-application-s-runtime-configuration}

Si un administrador de la aplicación exportó la configuración de tiempo de ejecución para una aplicación, puede importarla a la aplicación implementada. Puede importarlo mediante la consola de administración o mediante la implementación de LCA mediante scripts.

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de aplicaciones.
1. Haga clic en el nombre de la aplicación.
1. Haga clic en Importar configuración de tiempo de ejecución.
1. Haga clic en Examinar y seleccione el archivo XML que contiene la configuración de tiempo de ejecución.
1. Haga clic en Importar.

## Exportación de la configuración del tiempo de ejecución de una aplicación {#export-an-application-s-runtime-configuration}

Puede exportar la información de configuración del tiempo de ejecución para las aplicaciones implementadas.

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de aplicaciones.
1. Haga clic en el nombre de la aplicación.
1. Haga clic en Exportar configuración de tiempo de ejecución y guarde el archivo de configuración (XML) generado.

## Implementación con secuencias de comandos de aplicaciones de formularios AEM {#scripted-deployment-of-aem-forms-applications}

También puede utilizar una herramienta de implementación mediante secuencias de comandos para implementar archivos de aplicación, incluido un archivo settings.xml que especifica la siguiente configuración:

* configuración del servicio
* configuración del grupo
* configuración de extremo
* perfiles de seguridad

La implementación con secuencias de comandos elimina la necesidad de reconfigurar manualmente los ajustes en el entorno de producción antes de iniciar las aplicaciones implementadas.

1. Desde un símbolo del sistema, desplácese hasta *[aem-forms root]*/sdk/misc/Foundation/ArchiveManagement.
1. Revise el archivo ReadMe.txt para obtener instrucciones más detalladas.
1. Modifique manualmente los archivos scriptedDeploy.bat y sample-files/sample.xml tal como se describe en el archivo readme.txt.
1. Ejecute el archivo scriptedDeploy.bat. Esta acción implementa el archivo de archivos de formularios AEM con la configuración de anulación.

