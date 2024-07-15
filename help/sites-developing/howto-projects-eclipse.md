---
title: AEM Cómo desarrollar proyectos de mediante Eclipse
description: AEM En esta guía se describe cómo utilizar Eclipse para desarrollar proyectos basados en el
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
exl-id: 9d421599-0417-4329-a528-9cda4e3716f5
solution: Experience Manager, Experience Manager Sites
feature: Developing,Developer Tools
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---

# AEM Cómo desarrollar proyectos de mediante Eclipse{#how-to-develop-aem-projects-using-eclipse}

AEM En esta guía se describe cómo utilizar Eclipse para desarrollar proyectos basados en el.

>[!NOTE]
>
>El Adobe AEM AEM ahora proporciona las [Herramientas de desarrollo para Eclipse](/help/sites-developing/aem-eclipse.md), que le ayudan a desarrollar soluciones para el desarrollo de Eclipse a través de la herramienta de desarrollo de.

## Información general {#overview}

AEM Para comenzar con el desarrollo de la en Eclipse, se requieren los siguientes pasos.

Cada uno de ellos se explica con más detalle en el resto de este tutorial.

* Instalación de Eclipse 4.3 (Kepler)
* AEM Configurar el proyecto de en función de Maven
* Preparar la compatibilidad con JSP para Eclipse en el POM de Maven
* Importar el proyecto Maven en Eclipse

>[!NOTE]
>
>Esta guía se basa en Eclipse 4.3 (Kepler AEM) y en la versión 5.6.1 de la.

## Instalar Eclipse {#install-eclipse}

Descargue &quot;Eclipse IDE para desarrolladores de Java EE&quot; desde la [página de descargas de Eclipse](https://www.eclipse.org/downloads/).

Instale Eclipse siguiendo las [instrucciones de instalación](https://wiki.eclipse.org/Eclipse/Installation).

## AEM Configurar el proyecto de en función de Maven {#set-up-your-aem-project-based-on-maven}

AEM A continuación, configure su proyecto mediante Maven tal como se describe en [Cómo crear proyectos de mediante Apache Maven](/help/sites-developing/ht-projects-maven.md).

## Preparar compatibilidad con JSP para Eclipse {#prepare-jsp-support-for-eclipse}

Eclipse también puede proporcionar soporte en el trabajo con JSP, por ejemplo,

* finalización automática de bibliotecas de etiquetas
* Reconocimiento de eclipse de los objetos definidos por &lt;cq:defineObjects /> y &lt;sling:defineObjects />

Para que esto funcione:

1. AEM Siga las instrucciones de [Cómo trabajar con JSP](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps) en [Cómo crear proyectos de con Apache Maven](/help/sites-developing/ht-projects-maven.md).
1. Agregue lo siguiente a la sección &lt;build /> del POM de su módulo de contenido.

   El complemento de soporte Maven de Eclipse, m2e, no proporciona soporte para el complemento maven-jspc-plugin, y esta configuración le indica a m2e que ignore el complemento y la tarea relacionada de limpiar los resultados de compilación temporales.

   Esto no es un problema: como se indica en [Cómo trabajar con JSP](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps), el complemento maven-jspc de esta configuración solo se usa para validar que los JSP se compilan como parte del proceso de compilación. Eclipse ya informa de problemas en JSP y no depende de este complemento de Maven para poder hacerlo.

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
1. En el cuadro de diálogo de importación, elija Maven > Proyectos Maven existentes y, a continuación, haga clic en &quot;Siguiente&quot;.

   ![chlimage_1-41](assets/chlimage_1-41a.png)

1. Introduzca la ruta a la carpeta de nivel superior del proyecto y, a continuación, haga clic en &quot;Seleccionar todo&quot; y &quot;Finalizar&quot;.

   ![chlimage_1-42](assets/chlimage_1-42a.png)

1. AEM Ahora ya está todo listo para usar Eclipse para desarrollar su proyecto de, incluido el autocompletado de JSP.

   ![chlimage_1-43](assets/chlimage_1-43a.png)

   >[!NOTE]
   >
   >Si incluye `/libs/foundation/global.jsp` u otros JSP en `/libs`, debe copiarlos al proyecto para que Eclipse pueda resolver la inclusión. Al mismo tiempo, debe asegurarse de que Maven no lo incluya en su paquete de contenido. AEM En [Cómo crear proyectos de con Apache Maven](/help/sites-developing/ht-projects-maven.md) se describe cómo lograr esto.
