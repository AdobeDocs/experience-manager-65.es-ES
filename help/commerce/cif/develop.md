---
title: AEM Desarrollo de comercio de
description: AEM AEM Obtenga información sobre cómo generar un proyecto de habilitado para el comercio mediante el arquetipo de proyecto de. Aprenda a crear e implementar el proyecto en un entorno de desarrollo local.
topics: Commerce, Development
feature: Commerce Integration Framework
doc-type: tutorial
kt: 5826
thumbnail: 39476.jpg
exl-id: 48479725-8b52-4ff2-a599-d20958b26ee6
source-git-commit: 9d497413d0ca72f22712581cf7eda1413eb8d643
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 24%

---

# AEM Desarrollo de comercio de {#develop}

AEM El desarrollo de proyectos de comercio de basados en Commerce integration framework CIF AEM AEM () para la sigue las mismas reglas y prácticas recomendadas que otros proyectos de. Primero revise estos:

- [Guía del usuario sobre desarrollo en AEM 6.5](/help/sites-developing/getting-started.md)
- [AEM Conceptos principales de](/help/sites-developing/the-basics.md)
- [AEM Desarrollo: directrices y prácticas recomendadas](/help/sites-developing/dev-guidelines-bestpractices.md)
- [AEM Cómo crear proyectos de con Apache Maven](/help/sites-developing/ht-projects-maven.md)

## AEM Desarrollo local para comercio de {#local}

CIF Se recomienda contar con un entorno de desarrollo local para trabajar con proyectos de la.

>[!NOTE]
>
>AEM AEM CIF AEM Las siguientes instrucciones le ayudan a configurar un entorno de desarrollo de local para el comercio de utilizando el enfoque para la versión 6.5). AEM Si está utilizando el as a Cloud Service de la, consulte la [AEM Commerce as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content-and-commerce/home.html?lang=es) documentación.

AEM AEM El complemento de comercio de la de 6,5, también conocido como. CIF AEM El complemento también está disponible para el desarrollo local y se proporciona como paquete de. Se puede descargar desde el [Portal de distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html) como paquete de funciones.

### Software requerido

Lo siguiente debe instalarse de manera local:

- AEM Local 6 5
- [AEM Paquete de servicio de.5](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html) 7 o posterior
- [Java 11](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
- [Apache Maven](https://maven.apache.org/) (3.3.9 o posterior)
- [Nodo LTS](https://nodejs.org/en/)
- [npm 6+](https://www.npmjs.com/)
- [Git](https://git-scm.com/)

### CIF Acceso al complemento de la

CIF El complemento se puede descargar desde el [Portal de distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html)AEM , busque &quot;Complemento de comercio de&quot;.

>[!TIP]
>
>Asegúrese de utilizar siempre la última versión del complemento CIF.

### Configuración local

CIF AEM CIF Para el desarrollo local de proyectos en la comunidad, utilice los pasos siguientes del complemento de la y el:

1. AEM AEM Obtenga la versión de 6.5 e instale el paquete de servicio de 6.5. AEM Se requiere el paquete de servicio 7 de.5, pero el Adobe recomienda instalar el último paquete de servicio disponible.

1. Desempaquete el archivo .jar de AEM para crear la carpeta `crx-quickstart` , ejecute:

   ```bash
   java -jar <jar name> -unpack
   ```

1. Cree una carpeta `crx-quickstart/install` .

1. CIF Copie el paquete completo del complemento de la aplicación de la distribución de software descargado del Portal de distribución de software en el `crx-quickstart/install` carpeta.

>[!TIP]
>
>CIF Como alternativa, el paquete de complementos de la también se puede instalar mediante el Administrador de paquetes.

1. AEM Iniciar el inicio rápido de la

Verifique la configuración mediante la consola OSGI: `http://localhost:4502/system/console/osgi-installer`. CIF La lista debe incluir los paquetes relacionados con el complemento de, el paquete de contenido y las configuraciones de OSGI. Asegúrese de que todos los paquetes estén iniciados.

## Configuración del proyecto {#project}

AEM CIF Existen dos formas de iniciar el proyecto de comercio de la mediante el uso de la.

### Uso del tipo de archivo del proyecto AEM

El [tipo de archivo del proyecto AEM](https://github.com/adobe/aem-project-archetype) es la principal herramienta para arrancar un proyecto preconfigurado para comenzar con CIF. CIF Los componentes principales y todas las configuraciones requeridas se pueden incluir en un proyecto generado con una opción adicional.

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

CIF Los componentes principales se pueden utilizar en cualquier proyecto mediante, o bien la variable proporcionada `all` CIF para usuarios individuales que utilizan el paquete de contenido de y los paquetes OSGI relacionados. Para añadir los componentes principales de CIF manualmente a un proyecto, utilice las siguientes dependencias:

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

Una segunda opción para el inicio de un proyecto CIF es clonar y utilizar la [Tienda de referencia de Venia de AEM](https://github.com/adobe/aem-cif-guides-venia). La Tienda de referencia de Venia de AEM es una aplicación de tienda de referencia que muestra el uso de los componentes principales del CIF de AEM. Está diseñada como un conjunto de ejemplos de prácticas recomendadas y un punto de partida potencial para desarrollar su propia funcionalidad.

Para comenzar con la Tienda de referencia de Venia, simplemente clone el [Repositorio de Git](https://github.com/adobe/aem-cif-guides-venia) y empiece a personalizar el proyecto según sus necesidades.

>[!NOTE]
>
>AEM El proyecto de Tienda de referencia de Venia contiene dos perfiles de compilación para as a Cloud Service AEM y la versión 6.5 de. Compruebe la [archivo readme.md del proyecto](https://github.com/adobe/aem-cif-guides-venia/blob/main/README.md) para ver cómo se utilizan. AEM Para la versión 6.5, utilice la variable `classic` perfil.

### AEM Conectar con el sistema de comercio de

AEM Para conectar el proyecto al sistema de comercio, debe configurarse con el punto final GraphQL del sistema de comercio.

Ambos, un proyecto generado por el [AEM Tipo de archivo del proyecto](https://github.com/adobe/aem-project-archetype) o el [AEM Tienda de referencia de Venia en](https://github.com/adobe/aem-cif-guides-venia), ya incluya un [configuración predeterminada](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json) que deben ajustarse.

Reemplace el valor del `url` in `com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json` con el punto final de GraphQL de su sistema comercial utilizado por el proyecto.

AEM CIF El complemento de comercio de y los componentes principales se conectan al punto de conexión de GraphQL AEM de comercio a través del servidor de y directamente a través del explorador. CIF CIF Las herramientas de creación de complementos de componentes principales y de componentes de cliente de forma predeterminada se conectan a. `/api/graphql`. CIF Si es necesario, esto se puede ajustar mediante la configuración del Cloud Service de la (consulte a continuación).

CIF El complemento proporciona un servlet proxy de GraphQL en `/api/graphql`. AEM Si no planea utilizar un Dispatcher de local, se recomienda configurar también el servlet proxy de GraphQL.

Vaya a http://localhost:4502/system/console/configMgr y cree una configuración OSGI para `Adobe CIF GraphQL Proxy Configuration` servicio. Utilice el mismo punto final de GraphQL de su sistema comercial que se utilizó para el cliente de GraphQL anterior.

## Recursos adicionales

- [Tipo de archivo del proyecto AEM](https://github.com/adobe/aem-project-archetype)
- [Tienda de referencia de Venia de AEM](https://github.com/adobe/aem-cif-guides-venia)
