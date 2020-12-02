---
title: Cómo desarrollar AEM proyectos con Eclipse
seo-title: Cómo desarrollar AEM proyectos con Eclipse
description: Esta guía describe cómo utilizar Eclipse para desarrollar proyectos basados en AEM
seo-description: Esta guía describe cómo utilizar Eclipse para desarrollar proyectos basados en AEM
uuid: 79fee76f-6bcc-498f-af46-530816b41bbe
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: aa58cfb8-ec15-4698-a8f0-97683b0de51c
translation-type: tm+mt
source-git-commit: 06f1f753b9bb7f7336454f166e03f753e3735a16
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---


# Cómo desarrollar AEM proyectos usando Eclipse{#how-to-develop-aem-projects-using-eclipse}

En esta guía se describe cómo utilizar Eclipse para desarrollar proyectos basados en AEM.

>[!NOTE]
>
>Adobe ahora proporciona las [Herramientas de desarrollo AEM para Eclipse](/help/sites-developing/aem-eclipse.md) que le ayudan a desarrollar soluciones AEM con Eclipse.

## Información general {#overview}

Para comenzar con AEM desarrollo de Eclipse, se requieren los siguientes pasos.

Cada uno de ellos se explica con más detalle en el resto de este procedimiento.

* Instalación De Eclipse 4.3 (Kepler)
* Configure el proyecto de AEM en base a Maven
* Preparación de la compatibilidad de JSP con Eclipse en el POM de Maven
* Importación del proyecto Maven en Eclipse

>[!NOTE]
>
>Esta guía se basa en Eclipse 4.3 (Kepler) y AEM 5.6.1.

## Instalar Eclipse {#install-eclipse}

Descargue &quot;Eclipse IDE for Java EE Developers&quot; de la [página de descargas de Eclipse](https://www.eclipse.org/downloads/).

Instale Eclipse siguiendo las [Instrucciones de instalación](https://wiki.eclipse.org/Eclipse/Installation).

## Configure el proyecto de AEM en base a Maven {#set-up-your-aem-project-based-on-maven}

A continuación, configure el proyecto con Maven como se describe en [Cómo crear AEM proyectos con Apache Maven](/help/sites-developing/ht-projects-maven.md).

## Preparar compatibilidad con JSP para Eclipse {#prepare-jsp-support-for-eclipse}

Eclipse también puede proporcionar soporte para trabajar con JSP, por ejemplo

* finalización automática de bibliotecas de etiquetas
* Eclipse-aware de objetos definidos por &lt;cq:defineObjects /> y &lt;sling:defineObjects />

Para que funcione:

1. Siga las instrucciones de [Cómo trabajar con JSP](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps) en [Cómo generar AEM proyectos usando Apache Maven](/help/sites-developing/ht-projects-maven.md).
1. Añada lo siguiente en la sección &lt;build /> del POM del módulo de contenido.

   El complemento de soporte Maven de Eclipse, m2e, no proporciona soporte para maven-jspc-plugin, y esta configuración le dice a m2e que ignore el complemento y la tarea relacionada de limpiar los resultados de compilación temporal.

   Esto no es un problema: como se indica en [Cómo trabajar con JSP](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps), el complemento maven-jspc de esta configuración sólo se utiliza para validar que los JSPs se compilen como parte del proceso de compilación. Eclipse ya informa de cualquier problema en los JSPs y no confía en este complemento Maven para poder hacerlo.

   **myproject/content/pom.xml**

   ```xml
   <build>
     <!-- ... -->
     <pluginManagement>
       <plugins>
         <!--This plugin's configuration is used to store Eclipse m2e settings only. It has no influence on the Maven build itself.-->
         <plugin>
           <groupId>org.eclipse.m2e</groupId>
           <artifactId>lifecycle-mapping</artifactId>
           <version>1.0.0</version>
           <configuration>
             <lifecycleMappingMetadata>
               <pluginExecutions>
                 <pluginExecution>
                   <pluginExecutionFilter>
                     <groupId>org.apache.sling</groupId>
                     <artifactId>maven-jspc-plugin</artifactId>
                     <versionRange>[2.0.6,)</versionRange>
                     <goals>
                       <goal>jspc</goal>
                     </goals>
                   </pluginExecutionFilter>
                   <action>
                     <ignore/>
                   </action>
                 </pluginExecution>
                 <pluginExecution>
                   <pluginExecutionFilter>
                     <groupId>org.apache.maven.plugins</groupId>
                     <artifactId>maven-clean-plugin</artifactId>
                     <versionRange>[2.4.1,)</versionRange>
                     <goals>
                       <goal>clean</goal>
                     </goals>
                   </pluginExecutionFilter>
                   <action>
                     <ignore/>
                   </action>
                 </pluginExecution>
               </pluginExecutions>
             </lifecycleMappingMetadata>
           </configuration>
         </plugin>
       </plugins>
     </pluginManagement>
   </build>
   ```

### Importar el proyecto Maven en Eclipse {#import-the-maven-project-into-eclipse}

1. En Eclipse, seleccione Archivo > Importar...
1. En el cuadro de diálogo Importar, elija Maven > Proyectos existentes de mavizado y, a continuación, haga clic en &quot;Siguiente&quot;.

   ![chlimage_1-41](assets/chlimage_1-41a.png)

1. Introduzca la ruta a la carpeta de nivel superior del proyecto y, a continuación, haga clic en &quot;Seleccionar todo&quot; y &quot;Finalizar&quot;.

   ![chlimage_1-42](assets/chlimage_1-42a.png)

1. Ahora está todo listo para usar Eclipse para desarrollar su proyecto de AEM, incluido el autocompletado de JSP.

   ![chlimage_1-43](assets/chlimage_1-43a.png)

   >[!NOTE]
   >
   >Si incluye `/libs/foundation/global.jsp` u otros JSP en `/libs`, deberá copiarlo en su proyecto para que Eclipse pueda resolver la inclusión. Al mismo tiempo, debe asegurarse de que Maven no lo incluye en el paquete de contenido. Cómo lograr esto se describe en [Cómo construir proyectos AEM usando Apache Maven](/help/sites-developing/ht-projects-maven.md).

