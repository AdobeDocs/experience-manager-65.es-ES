---
title: Desarrollo AEM comercio
description: Obtenga información sobre cómo generar un proyecto de AEM habilitado para el comercio mediante el tipo de archivo del proyecto de AEM. Aprenda a crear e implementar el proyecto en un entorno de desarrollo local.
topics: Commerce, Development
feature: Marco de integración de Commerce
doc-type: tutorial
kt: 5826
thumbnail: 39476.jpg
translation-type: tm+mt
source-git-commit: 8ead3d1b24177effa4d40141408c5676eaabcc30
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 32%

---


# Desarrollo de AEM Commerce {#develop}

El desarrollo de proyectos AEM Commerce basados en Commerce Integration Framework (CIF) para AEM sigue las mismas reglas y prácticas recomendadas como otros proyectos de AEM. Primero revise estos:

- [Guía del usuario sobre desarrollo en AEM 6.5](/help/sites-developing/home.md)
- [AEM Conceptos principales](/help/sites-developing/the-basics.md)
- [Desarrollo de AEM: directrices y prácticas recomendadas](/help/sites-developing/dev-guidelines-bestpractices.md)
- [Cómo crear AEM proyectos con Apache Maven](/help/sites-developing/ht-projects-maven.md)

## Desarrollo local para comercio AEM {#local}

Se recomienda contar con un entorno de desarrollo local para trabajar con proyectos CIF.

>[!NOTE]
>
>Las siguientes instrucciones le ayudan a configurar un entorno de desarrollo de AEM local para AEM Commerce con CIF enfocado para AEM 6.5). Si utiliza AEM como Cloud Service, consulte la documentación de [AEM Commerce as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/commerce/home.html) .

AEM complemento de comercio para AEM 6.5 también conocido como El complemento CIF también está disponible para el desarrollo local y se proporciona como paquete AEM. Se puede descargar desde el [Portal de distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) como paquete de funciones.

### Software necesario

Lo siguiente debe instalarse de manera local:

- AEM local 6.5
- [AEM 6.5 Service Pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)  7 o posterior
- [Java 11](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
- [Apache Maven](https://maven.apache.org/) (3.3.9 o posterior)
- [LTS de nodos](https://nodejs.org/en/)
- [npm 6+](https://www.npmjs.com/)
- [Git](https://git-scm.com/)

### Acceso al complemento CIF.

El complemento CIF se puede descargar desde el [Portal de distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html), buscar el &quot;complemento AEM comercio&quot;.

>[!TIP]
>
>Asegúrese de utilizar siempre la última versión del complemento CIF.

### Configuración local

Para el desarrollo de proyectos del CIF local mediante el AEM y el complemento del CIF, siga estos pasos:

1. Obtenga la versión AEM 6.5 e instale el Service Pack AEM 6.5. Se requiere AEM 6.5 Service Pack 7, pero recomendamos instalar el último Service Pack disponible.

1. Desempaquete el archivo .jar de AEM para crear la carpeta `crx-quickstart` , ejecute:

   ```bash
   java -jar <jar name> -unpack
   ```

1. Cree una carpeta `crx-quickstart/install` .

1. Copie el paquete completo del complemento CIF, descargado del portal de distribución de software, en la carpeta `crx-quickstart/install` .

>[!TIP]
>
>Alternativamente, el paquete de complementos CIF también se puede instalar mediante el Administrador de paquetes.

1. Inicio rápido AEM

Verifique la configuración mediante la consola OSGI: `http://localhost:4502/system/console/osgi-installer`. La lista debe incluir los paquetes relacionados con el complemento CIF, el paquete de contenido y las configuraciones OSGI. Asegúrese de que todos los paquetes estén iniciados.

## Configuración del proyecto {#project}

Existen dos formas de iniciar el proyecto de comercio AEM con CIF.

### Uso del tipo de archivo del proyecto AEM

El [tipo de archivo del proyecto AEM](https://github.com/adobe/aem-project-archetype) es la principal herramienta para arrancar un proyecto preconfigurado para comenzar con CIF. Los componentes principales de CIF y todas las configuraciones requeridas se pueden incluir en un proyecto generado con una opción adicional.

>[!TIP]
>
>Utilice un [tipo de archivo del proyecto AEM 25 o posterior](https://github.com/adobe/aem-project-archetype/releases) para generar el proyecto.

Consulte las [instrucciones de uso](https://github.com/adobe/aem-project-archetype#usage) del tipo de archivo del proyecto AEM para saber cómo generar un proyecto AEM. Para incluir CIF en el proyecto, utilice la opción `includeCommerce` .

Por ejemplo:

```bash
mvn -B archetype:generate \
 -D archetypeGroupId=com.adobe.granite.archetypes \
 -D archetypeArtifactId=aem-project-archetype \
 -D aemVersion=6.5.5 \
 -D appTitle="My Site" \
 -D appId="mysite" \
 -D groupId="com.mysite" \
 -D frontendModule=general \
 -D includeExamples=n \
 -D includeCommerce=y
```

Los componentes principales de CIF se pueden usar en cualquier proyecto incluyendo el paquete proporcionado `all` o una persona utilizando el paquete de contenido de CIF y los paquetes de OSGI relacionados. Para añadir los componentes principales de CIF manualmente a un proyecto, utilice las siguientes dependencias:

```java
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-apps</artifactId>
    <type>zip</type>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-config</artifactId>
    <type>zip</type>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-core</artifactId>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>graphql-client</artifactId>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>magento-graphql</artifactId>
    <version>x.y.z</version>
</dependency>
```

### Tienda de referencia Venia en AEM

Una segunda opción para el inicio de un proyecto CIF es clonar y utilizar la [Tienda de referencia de Venia de AEM](https://github.com/adobe/aem-cif-guides-venia). La Tienda de referencia de Venia de AEM es una aplicación de tienda de referencia que muestra el uso de los componentes principales del CIF de AEM. Está diseñado como un conjunto de ejemplos de prácticas recomendadas y un punto de partida potencial para desarrollar su propia funcionalidad.

Para comenzar con la Tienda de referencia de Venia, simplemente clone el [repositorio de Git](https://github.com/adobe/aem-cif-guides-venia) y empiece a personalizar el proyecto según sus necesidades.

>[!NOTE]
>
>El proyecto de Tienda de referencia de Venia contiene dos perfiles de compilación para AEM as a Cloud Service y AEM 6.5. Compruebe el archivo [readme.md del proyecto](https://github.com/adobe/aem-cif-guides-venia/blob/main/README.md) para ver cómo se utilizan. Para AEM 6.5, utilice el perfil `classic`.

### Conectar AEM al sistema de comercio

Para conectar el proyecto al sistema de comercio, AEM debe configurarse con el extremo GraphQL del sistema de comercio.

Ambos, un proyecto generado por el [AEM tipo de archivo del proyecto](https://github.com/adobe/aem-project-archetype) o el [AEM Tienda de referencia de Venia](https://github.com/adobe/aem-cif-guides-venia), ya incluyen una [configuración predeterminada](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json) que debe ajustarse.

Reemplace el valor de `url` en `com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json` con el extremo GraphQL del sistema de comercio utilizado por el proyecto.

Los componentes principales AEM Commerce Add-On y CIF se conectan al extremo commerce GraphQL a través del servidor AEM y directamente a través del explorador. Los componentes principales del CIF del lado del cliente y las herramientas de creación del complemento CIF de forma predeterminada se conectan a `/api/graphql`. Si es necesario, esto se puede ajustar a través de la configuración del Cloud Service del CIF (ver abajo).

El complemento CIF proporciona un servlet proxy de GraphQL en `/api/graphql`. Si no planea utilizar un Dispatcher AEM local, también se recomienda configurar el servlet proxy de GraphQL.

Vaya a http://localhost:4502/system/console/configMgr y cree una configuración OSGI para el servicio `Adobe CIF GraphQL Proxy Configuration`. Utilice el mismo extremo de GraphQL del sistema de comercio que se ha utilizado para el cliente de GraphQL anterior.

## Recursos adicionales

- [Tipo de archivo del proyecto AEM](https://github.com/adobe/aem-project-archetype)
- [Tienda de referencia de Venia de AEM](https://github.com/adobe/aem-cif-guides-venia)
