---
title: Ejecutar modos
description: AEM Aprenda a ajustar la instancia de la para fines específicos mediante los modos de ejecución.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
feature: Administering
exl-id: 6d03cb1d-500e-4a23-80e5-347a43dff30e
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '746'
ht-degree: 1%

---

# Ejecutar modos{#run-modes}

AEM Los modos de ejecución permiten ajustar la instancia de la para un propósito específico; por ejemplo, crear o publicar, probar, desarrollar, intranet u otros.

Puede hacer lo siguiente:

* [Definir colecciones de parámetros de configuración para cada modo de ejecución](#defining-configuration-properties-for-a-run-mode).

  Se aplica un conjunto básico de parámetros de configuración para todos los modos de ejecución y, a continuación, puede ajustar conjuntos adicionales para el propósito de su entorno específico. Se aplican según sea necesario.

* [Defina paquetes adicionales para instalarlos en un modo concreto](#defining-additional-bundles-to-be-installed-for-a-run-mode).

Todos los ajustes y definiciones se almacenan en el único repositorio y se activan configurando el **Modo de ejecución**.

## Modos de ejecución de instalación {#installation-run-modes}

Los modos de ejecución de instalación (o fijos) se utilizan en el momento de la instalación y, a continuación, se corrigen durante toda la duración de la instancia; no se pueden cambiar.

Los modos de ejecución de la instalación están disponibles de forma predeterminada:

* `author`
* `publish`
* `samplecontent`
* `nosamplecontent`

Son dos pares de modos de ejecución mutuamente excluyentes; por ejemplo, puede:

* defina `author` o `publish`, no ambas al mismo tiempo

* combinar `author` con cualquiera `samplecontent` o `nosamplecontent` (pero no ambas)

>[!CAUTION]
>
>Cuando se utiliza uno de los modos de ejecución anteriores (author, publish, samplecontent, nosamplecontent), el valor utilizado en el momento de la instalación define el modo de ejecución para el *toda la vida* de dicha instalación.
>
>Para estos modos de ejecución, debe: *no puede* cámbielos después de la instalación.

## Modos de ejecución personalizados {#customized-run-modes}

También puede crear sus propios modos de ejecución personalizados. Se pueden combinar para cubrir situaciones como las siguientes:

* `author` + `development`

* `publish` + `test`

* `publish` + `test` + `golive`

* `publish` + `intranet`

* según sea necesario . .

También se pueden seleccionar modos de ejecución personalizados en cada inicio.

## Uso de samplecontent y nosamplecontent {#using-samplecontent-and-nosamplecontent}

Estos modos permiten controlar el uso del contenido de muestra. El contenido de muestra se define antes de que se genere el inicio rápido y puede incluir paquetes, configuraciones, etc.:

* El `samplecontent` el modo de ejecución instala este contenido (el modo predeterminado).

* El `nosamplecontent` El modo no instala el contenido de muestra.

El modo de ejecución nosamplecontent está diseñado para instalaciones de producción.

## Definición de propiedades de configuración para un modo de ejecución {#defining-configuration-properties-for-a-run-mode}

Se puede guardar en el repositorio una colección de valores para las propiedades de configuración, utilizados para un modo de ejecución concreto.

El modo de ejecución se indica con un sufijo en el nombre de la carpeta. Esto permite almacenar todas las configuraciones en un repositorio como. Por ejemplo:

* `config`

  Aplicable a todos los modos de ejecución

* `config.author`

  Se utiliza para el modo de ejecución de autor

* `config.publish`

  Se utiliza para el modo de ejecución de publicación

* `config.<run-mode>`

  Se utiliza para el modo de ejecución aplicable; por ejemplo, config

Consulte [Configuración de OSGi en el repositorio](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) para obtener más información sobre la definición de los nodos de configuración individuales dentro de estas carpetas y para crear configuraciones para combinaciones de varios modos de ejecución.

>[!NOTE]
>
>Para [Modos de ejecución de instalación](#installation-run-modes) (por ejemplo, autor) el modo de ejecución no se puede cambiar después de la instalación. Sin embargo, los cambios en las propiedades de configuración individuales surtirán efecto tras el reinicio.

## Definición de paquetes adicionales que se van a instalar para un modo de ejecución {#defining-additional-bundles-to-be-installed-for-a-run-mode}

También se pueden especificar paquetes adicionales que deben instalarse para un modo de ejecución concreto. Para estas definiciones, las carpetas de instalación se utilizan para contener los paquetes. De nuevo, el modo de ejecución se indica con un prefijo:

* `install.author`
* `install.publish`

Estas carpetas son del tipo `nt:folder` y deben contener el paquete adecuado.

## Iniciar CQ con un modo de ejecución específico {#starting-cq-with-a-specific-run-mode}

Si ha definido configuraciones para varios modos de ejecución, debe definir cuál se utilizará al iniciar. Existen varios métodos para especificar qué modo de ejecución utilizar; el orden de resolución es el siguiente:

1. [propiedades del sistema (](#using-a-system-property-in-the-start-script)
1. [](#using-the-sling-properties-file)
1. [](#using-the-r-option)
1. [Detección de nombres de archivo](#filename-detection-renaming-the-jar-file)

Cuando utiliza un servidor de aplicaciones, también puede [defina el modo de ejecución en web.xml](#defining-the-run-mode-in-web-xml-with-application-server).

### Uso del archivo sling.properties {#using-the-sling-properties-file}

El `sling.properties` para definir el modo de ejecución necesario:

1. Edite el archivo de configuración:

   `<cq-installation-dir>/crx-quickstart/conf/sling.properties`

1. Añada las siguientes propiedades; el siguiente ejemplo es para autor:

   `sling.run.modes=author`

### Uso de la opción -r {#using-the-r-option}

Se puede activar un modo de ejecución personalizado utilizando `-r` al iniciar el inicio rápido. AEM Por ejemplo, utilice el siguiente comando para iniciar una instancia de con el modo de ejecución establecido en dev. &quot;

```shell
java -jar cq-56-p4545.jar -r dev
```

### Uso de una propiedad del sistema en el script de inicio {#using-a-system-property-in-the-start-script}

Se puede utilizar una propiedad del sistema en el script de inicio para especificar el modo de ejecución.

* Por ejemplo, utilice lo siguiente para iniciar una instancia como instancia de publicación de producción en Estados Unidos:

  `-Dsling.run.modes=publish,prod,us`

### Detección de nombres de archivo: cambiando el nombre del archivo jar {#filename-detection-renaming-the-jar-file}

Los dos modos de ejecución de instalación siguientes se pueden activar cambiando el nombre del archivo jar de instalación antes de la instalación:

* publicación
* autor

El archivo jar debe utilizar la convención de nombres:

`cq5-<run-mode>-p<port-number>`

Por ejemplo, configure el `publish` modo de ejecución asignando un nombre al archivo jar:

`cq5-publish-p4503`

### Definición del modo de ejecución en web.xml (con Application Server) {#defining-the-run-mode-in-web-xml-with-application-server}

Cuando utilice un servidor de aplicaciones, también puede configurar la propiedad:

`sling.run.modes`

en el archivo:

`WEB-INF/web.xml`

AEM Esto es en el `war` y deben actualizarse antes de la implementación.

Consulte [AEM Instalación con un servidor de aplicaciones de](/help/sites-deploying/application-server-install.md) para obtener más información.
