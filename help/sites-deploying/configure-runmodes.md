---
title: Ejecutar modos
seo-title: Ejecutar modos
description: Aprenda a ajustar la instancia de AEM para fines específicos mediante los modos de ejecución.
seo-description: Aprenda a ajustar la instancia de AEM para fines específicos mediante los modos de ejecución.
uuid: 8a0c6e5c-4fae-43e2-b745-eee58f346ceb
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 12329e26-40bc-4c94-bc60-6d9cbd01345f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 1%

---


# Ejecutar modos{#run-modes}

Los modos de ejecución le permiten ajustar la instancia de AEM para un fin específico; por ejemplo, crear o publicar, probar, desarrollar, intranet u otros.

Puede hacer lo siguiente:

* [Defina colecciones de parámetros de configuración para cada modo](#defining-configuration-properties-for-a-run-mode) de ejecución.

   Se aplica un conjunto básico de parámetros de configuración para todos los modos de ejecución, puede ajustar conjuntos adicionales según el propósito del entorno específico. Se aplican según sea necesario.

* [Defina paquetes adicionales para instalar en un modo](#defining-additional-bundles-to-be-installed-for-a-run-mode) particular.

Todas las configuraciones y definiciones se almacenan en el único repositorio y se activan configurando el **Modo de ejecución**.

## Modos de ejecución de instalación {#installation-run-modes}

Los modos de ejecución de instalación (o fijos) se utilizan en el momento de la instalación y, a continuación, se corrigen durante toda la duración de la instancia, no se pueden cambiar.

Los modos de ejecución de la instalación se proporcionan de forma predeterminada:

* `author`
* `publish`
* `samplecontent`
* `nosamplecontent`

Son dos pares de modos de ejecución mutuamente excluyentes; por ejemplo, puede:

* define `author` o `publish`, no ambos al mismo tiempo

* combinar `author` con `samplecontent` o `nosamplecontent` (pero no ambos)

>[!CAUTION]
>
>Al utilizar uno de los modos de ejecución anteriores (autor, publicación, muestra de contenido, nosamplecontent), el valor utilizado en el momento de la instalación define el modo de ejecución para la *duración completa* de esa instalación.
>
>Para estos modos de ejecución, *no puede* cambiarlos después de la instalación.

## Modos de ejecución personalizados {#customized-run-modes}

También puede crear sus propios modos de ejecución personalizados. Se pueden combinar para cubrir escenarios como:

* `author` + `development`

* `publish` +  `test`

* `publish` + `test` + `golive`

* `publish` +  `intranet`

* según sea necesario. . .

También se pueden seleccionar modos de ejecución personalizados en cada inicio.

## Uso de contenido de muestra y de nosamplcontent {#using-samplecontent-and-nosamplecontent}

Estos modos le permiten controlar el uso del contenido de muestra. El contenido de muestra se define antes de que se cree el inicio rápido y puede incluir paquetes, configuraciones, etc.:

* El modo de ejecución `samplecontent` instalará este contenido (el modo predeterminado).

* El modo `nosamplecontent` no instalará el contenido de muestra.

El modo de ejecución nosamplecontent está diseñado para instalaciones de producción.

## Definición de propiedades de configuración para un modo de ejecución {#defining-configuration-properties-for-a-run-mode}

Se puede guardar en el repositorio una colección de valores para las propiedades de configuración, que se utilizan para un modo de ejecución concreto.

El modo de ejecución se indica con un sufijo en el nombre de la carpeta. Esto le permite almacenar todas las configuraciones en un repositorio como. Por ejemplo:

* `config`

   Aplicable a todos los modos de ejecución

* `config.author`

   Se utiliza para el modo de ejecución del autor

* `config.publish`

   Se utiliza para el modo de ejecución de publicación

* `config.<run-mode>`

   Se utiliza para el modo de ejecución aplicable; por ejemplo, config

Consulte [Configuración de OSGi en el Repositorio](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) para obtener más detalles sobre la definición de los nodos de configuración individuales dentro de estas carpetas y para crear configuraciones para combinaciones de múltiples modos de ejecución.

>[!NOTE]
>
>Para [Modos de ejecución de instalación](#installation-run-modes) (p. ej., autor), el modo de ejecución no se puede cambiar después de la instalación. Sin embargo, los cambios en las propiedades de configuración individuales surtirán efecto al reiniciar.

## Definición de paquetes adicionales para instalar en modo de ejecución {#defining-additional-bundles-to-be-installed-for-a-run-mode}

También se pueden especificar paquetes adicionales que deben instalarse para un modo de ejecución determinado. Para estas definiciones, las carpetas de instalación se utilizan para guardar los paquetes. Nuevamente, el modo de ejecución se indica con un prefijo:

* `install.author`
* `install.publish`

Estas carpetas son del tipo `nt:folder` y deben contener el paquete apropiado.

## Inicio de CQ con un modo de ejecución específico {#starting-cq-with-a-specific-run-mode}

Si ha definido configuraciones para varios modos de ejecución, debe definir cuál se utilizará al iniciar. Existen varios métodos para especificar qué modo de ejecución se debe utilizar; el orden de resolución es:

1. [ `sling.properties` file](#using-the-sling-properties-file)
1. [ `-r` opción](#using-the-r-option)
1. [propiedades del sistema (`-D`)](#using-a-system-property-in-the-start-script)

1. [Detección de nombre de archivo](#filename-detection-renaming-the-jar-file)

Cuando utiliza un servidor de aplicaciones, también puede [definir el modo de ejecución en web.xml](#defining-the-run-mode-in-web-xml-with-application-server).

### Uso del archivo sling.properties {#using-the-sling-properties-file}

El archivo `sling.properties` puede utilizarse para definir el modo de ejecución requerido:

1. Edite el archivo de configuración:

   `<cq-installation-dir>/crx-quickstart/conf/sling.properties`

1. Añadir las siguientes propiedades; el siguiente ejemplo es para autor:

   `sling.run.modes=author`

### Uso de la opción -r {#using-the-r-option}

Se puede activar un modo de ejecución personalizado mediante la opción `-r` al iniciar el inicio rápido. Por ejemplo, utilice el siguiente comando para iniciar una instancia de AEM con el modo de ejecución establecido en dev. &quot;

```shell
java -jar cq-56-p4545.jar -r dev
```

### Uso de una propiedad del sistema en la secuencia de comandos de inicio {#using-a-system-property-in-the-start-script}

Se puede utilizar una propiedad del sistema en la secuencia de comandos de inicio para especificar el modo de ejecución.

* Por ejemplo, utilice lo siguiente para iniciar una instancia como una instancia de publicación de producción ubicada en EE. UU.:

   `-Dsling.run.modes=publish,prod,us`

### Detección de nombres de archivo: cambio del nombre del archivo jar {#filename-detection-renaming-the-jar-file}

Los dos modos de ejecución de instalación siguientes se pueden activar cambiando el nombre del archivo jar de instalación antes de la instalación:

* instancias de publicación
* author

El archivo jar debe utilizar la convención de nombres:

`cq5-<run-mode>-p<port-number>`

Por ejemplo, para establecer el modo de ejecución `publish`, asigne un nombre al archivo jar:

`cq5-publish-p4503`

### Definición del modo de ejecución en web.xml (con Application Server) {#defining-the-run-mode-in-web-xml-with-application-server}

Cuando utiliza un servidor de aplicaciones, también puede configurar la propiedad:

`sling.run.modes`

en el archivo:

`WEB-INF/web.xml`

Esto se encuentra en el archivo AEM `war` y debe actualizarse antes de la implementación.

Consulte [Instalación de AEM con un servidor de aplicaciones](/help/sites-deploying/application-server-install.md) para obtener más detalles.
