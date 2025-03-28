---
title: Mitigación de vulnerabilidades de Spring Framework para AEM Forms en JEE
description: Mitigación de vulnerabilidades de Spring Framework para AEM Forms en JEE
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
geptopics: SG_AEMFORMS/categories/jee
role: Admin
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: 61cce7cd8290156bec6dcc351a59093f545a4ec7
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 1%

---


# Mitigación de vulnerabilidades de Spring Framework para AEM Forms en JEE

Este documento proporciona instrucciones para abordar dos vulnerabilidades críticas del marco de trabajo de primavera que afectan a AEM Forms en JEE:

- **[CVE-2024-38819](https://spring.io/security/cve-2024-38819)**: vulnerabilidad de recorrido de ruta en marcos web funcionales
- **[CVE-2024-38820](https://spring.io/security/cve-2024-38820)**: Excepción de coincidencia con distinción de mayúsculas y minúsculas en DataBinder de Spring Framework

## Versiones afectadas

- Adobe Experience Manager 6.5 Forms en JEE
- Versiones de AEM 6.5 Forms GA en 6.5.22.0

## Resolución

### Soluciones específicas de la versión

| Versión de AEM Forms | Acción necesaria |
|-------------------|-----------------|
| 6.5.22.0 | 1. [Descargue la revisión para su entorno](/help/release-notes/aem-forms-hotfix.md). </br> 2. Para instalar esta corrección, siga las instrucciones para [instalar Service Pack en un formulario de AEM en JEE](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). |
| 6.5.17.0 - 6.5.21.0 | [Aplicar pasos de mitigación manuales](#manual-mitigation-steps). |
| 6.5 - 6.5.16.0 | 1. [Instale el Service Pack más reciente](/help/release-notes/release-notes.md)<br>2. [Implemente la solución adecuada](#version-specific-solutions) según su versión actualizada. |

> **Nota**: AEM Forms solo admite oficialmente los seis Service Packs más recientes. Los usuarios con versiones anteriores deben actualizar primero al Service Pack más reciente y, a continuación, instalar la revisión necesaria.

## Consideraciones de implementación

### Para Entornos Agrupados

Al trabajar con una implementación agrupada:

- Aplicar reemplazos de archivos JAR (paso #4) en **todos los nodos** del clúster
- Mantenga la coherencia utilizando versiones JAR idénticas en todos los servidores
- Actualizaciones completas en todos los nodos antes de iniciar cualquier reinicio del servicio
- Implementar una estrategia de reinicio coordinada para minimizar el tiempo de inactividad del sistema

### Para entornos de un solo nodo

Al trabajar con una implementación independiente:

- Siga un proceso simplificado, ya que no hay servidores de localización que administrar
- Omita los pasos relacionados con la configuración o el inicio del servidor del localizador
- Complete todos los demás pasos según las instrucciones, especialmente los reemplazos de JAR y las actualizaciones de manifiestos
- Reinicie el servidor de aplicaciones después de implementar todos los cambios

## Pasos de mitigación manuales

1. Detenga los servidores de aplicaciones.
1. Detenga y localice servidores.
1. Retire los JAR de muelle del EAR principal:
   1. Navegue hasta `[Adobe_Experience_Manager_Forms installation directory]/deploy`.
   1. Abra el archivo `adobe-core-<appserver>.ear` con una herramienta de administración de archivos. Donde `<appserver>` puede ser JBoss, WebLogic o WebSphere, según su entorno:
   - **Para JBoss:** Vaya a la carpeta `ear/lib` y elimine los siguientes archivos JAR:
- `spring-core-<version>.jar`
- `spring-web-<version>.jar`

   - **Para WebLogic o WebSphere:** Elimine los siguientes archivos JAR de la raíz de EAR:
- `spring-core-<version>.jar`
- `spring-web-<version>.jar`

   - **Para todos los servidores de aplicaciones:** En el nivel raíz de `adobe-core-<appserver>.ear`, abra el archivo `adobe-dscf.jar` y edite el archivo `META-INF/MANIFEST.MF` para quitar cualquier referencia a los siguientes archivos JAR:
- `spring-core-<version>.jar`
- `spring-web-<version>.jar`

1. Reemplazar archivos JAR de la distribución Geode:
   1. Navegue hasta `<Adobe_Experience_Manager_Forms>/lib/caching/lib`
   1. Reemplace los archivos JAR existentes con las versiones actualizadas:
   - `spring-context-<version>.jar` → `spring-context-6.1.14.jar`
   - `spring-beans-<version>.jar` → `spring-beans-6.1.14.jar`
   - `spring-core-<version>.jar` → `spring-core-6.1.14.jar`
   - `spring-jcl-<version>.jar` → `spring-jcl-6.1.14.jar`
   - `spring-web-<version>.jar` → `spring-web-6.1.14.jar`

   Para obtener los archivos JAR más recientes, descargue el archivo spring-6.1.14-jars.zip de [Adobe Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/spring-6.1.14-jars.zip) y extraiga el archivo ZIP para acceder a los archivos JAR actualizados del módulo de Spring.

   1. Actualice los archivos MANIFEST.MF en los siguientes archivos JAR:
   - `geode-server-all-<version>.jar`
   - `gfsh-dependencies.jar`

   Para cada JAR:
   - Abra el JAR con una herramienta de administrador de archivos
   - Busque y extraiga el archivo `META-INF/MANIFEST.MF`
   - Edite el archivo MANIFEST.MF en un editor de texto
   - Busque la sección &quot;Ruta de clase&quot; y actualice todas las referencias del marco de trabajo de primavera:
      - `spring-core-<version>.jar` a `spring-core-6.1.14.jar`
      - `spring-web-<version>.jar` a `spring-web-6.1.14.jar`
      - `spring-context-<version>.jar` a `spring-context-6.1.14.jar`
      - `spring-beans-<version>.jar` a `spring-beans-6.1.14.jar`
      - `spring-jcl-<version>.jar` a `spring-jcl-6.1.14.jar`
   - Guarde el archivo MANIFEST.MF modificado
   - Reemplace el MANIFEST.MF original en el JAR por su versión actualizada
   - Guarde el archivo JAR

   1. Problemas comunes a tener en cuenta:
      - Asegúrese de que no haya entradas duplicadas en el manifiesto
      - Mantener los extremos de línea adecuados
      - Comprobar que todos los JAR a los que se hace referencia existen en las ubicaciones especificadas

   1. Pasos de verificación:
      - Compruebe si el manifiesto se ha actualizado correctamente
      - Compruebe que se hace referencia correctamente a todas las dependencias Spring
      - Asegúrese de que no queden referencias de versiones antiguas
      - Pruebe la aplicación para confirmar que no hay problemas de carga de clases

1. Ejecute el Administrador de configuración.

1. Reiniciar servidores:
   - Inicio de los servidores de localización mediante JDK 17
   - Inicie los servidores de aplicaciones utilizando la misma versión de JDK (JDK 8 o JDK 11) utilizada anteriormente.
