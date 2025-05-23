---
title: Mitigación de vulnerabilidades de Struts 2 para Experience Manager Forms en JEE
description: Mitigación de vulnerabilidades de Struts 2 para Experience Manager Forms en JEE
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
geptopics: SG_AEMFORMS/categories/jee
role: Admin
exl-id: 73b5aff2-1320-4d9a-8972-54c4fdd3a2c2
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: 9f59606bb58b9e90f07bd22e89f3213afb54a697
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 1%

---

# Mitigación de vulnerabilidades de Struts 2 para Experience Manager Forms {#mitigatin-struts2-rce-vulnerabilities-for-aem-forms}

## Problema

Se han notificado vulnerabilidades de seguridad críticas para Struts 2, un marco de aplicación web popular y de código abierto para el desarrollo de aplicaciones web Java EE. Se han analizado las siguientes vulnerabilidades:

| Vulnerabilidad | ¿Qué se ve afectado? | ¿Qué no se ve afectado? |
|---|---|---|
| [CVE-2023-50164](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2023-50164) | Experience Manager 6.5 Forms en JEE (todas las versiones desde 6.5 GA a 6.5.19.0) | <ul><li> Experience Manager Forms Workbench (todas las versiones)</li> <li> Experience Manager Forms en OSGi (todas las versiones) </li> <li> Experience Manager Forms as a Cloud Service </li> <ul> |

## Resolución

La siguiente tabla muestra la resolución de todas las versiones afectadas:

| Versión | Versión actual | Acción del usuario |
|---|---|---|
| Experience Manager 6.5 Forms en JEE | 6.5.19.0 | [Instalar el Service Pack más reciente](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html?lang=es) |
| Experience Manager 6.5 Forms en JEE | 6.5.13.0: 6.5.18.0 | Utilice uno de los siguientes métodos: <ul><li>  <a href="https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html?lang=es"> Instalar el Service Pack más reciente </a> </li> <li> <a href ="#use-manual-mitigation-steps"> Usar pasos de mitigación manuales </a> |
| Experience Manager 6.5 Forms en JEE | 6.5 - 6.5.12.0 | [Instalar el Service Pack más reciente](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html?lang=es) </br> </br> **NOTA:** AEM Forms admite actualmente las versiones 6.5.13.0 a 6.5.19.0. Si utiliza una versión anterior, le recomendamos que la actualice a la versión 6.5.13.0 o una posterior. AEM Para obtener instrucciones para instalar la versión 6.5.13.0 de o posterior, consulte las notas de la versión. |

### Uso de pasos de mitigación manuales {#use-manual-mitigation-steps}

AEM AEM Puede utilizar los pasos de mitigación manuales para resolver el problema en el servidor de formularios 6.5 que ejecuta el paquete de servicio 13 a servidor de formularios 6.5 que ejecuta el paquete de servicio 18 (6.5.13.0 - 6.5.18.0):

1. Descargue [struts-core 2.5.33 jar](https://repo1.maven.org/maven2/org/apache/struts/struts2-core/2.5.33/struts2-core-2.5.33.jar) a una carpeta local. Por ejemplo, C:\Users\labuser\Desktop\struts2-core-2.5.33.jar.
1. Descargue la herramienta de revisión manual de AEM Forms en JEE desde [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/patch_utility/archive-patcher-1.0.0.zip).
1. Descomprima el archivo de la herramienta de aplicación manual de parches. Por ejemplo, realice la extracción en `/Users/labuser/Desktop/archive-patcher-1.0.0 folder`. Se extraen los siguientes archivos:
   * archive-patcher-1.0.0.jar
   * patch-archive.bat
   * patch-archive.sh

>[!BEGINTABS]

>[!TAB Windows]

1. Cierre todas las instancias y ubicaciones del servidor.

1. Abra la ventana del terminal y vaya a la carpeta que contiene la Herramienta de aplicación manual de parches de AEM Forms en JEE (archivos extraídos).

1. Ejecute el siguiente comando para buscar todos los archivos con bibliotecas struts2 más antiguas. Antes de ejecutar el comando, reemplace la ruta del comando por la ruta del servidor de AEM Forms:


   ```
   patch-archive.bat -root=C:\Adobe\Adobe_Experience_Manager_Forms\configurationManager\export -pattern=.*struts2-core.*jar$
   ```

   >[!NOTE]
   >
   >
   >La herramienta requiere conectividad a Internet, ya que descarga dependencias en tiempo de ejecución. Por lo tanto, antes de ejecutar la herramienta, asegúrese de que está conectado a Internet.

1. Ejecute los siguientes comandos en el orden indicado para el reemplazo recurrente in situ. Antes de ejecutar el comando, reemplace la ruta del comando por la ruta de acceso del servidor de AEM Forms y el archivo `struts2-core-2.5.33.jar`.



   ```
   patch-archive.bat -root=C:\Adobe\Adobe_Experience_Manager_Forms\configurationManager\export -pattern=.*struts2-core.*jar$ -action=replace C:\Users\labuser\Desktop\struts2-core-2.5.33.jar
   ```

   Los pasos anteriores parchean todos los archivos ear con bibliotecas struts2 más antiguas.

1. Anule la implementación del EAR anterior e implemente el archivo EAR parcheado, disponible en la carpeta de exportación, en el servidor de aplicaciones.

1. Inicie el servidor de AEM Forms.

>[!TAB Linux]

1. Cierre todas las instancias y ubicaciones del servidor.

1. Abra la ventana del terminal y vaya a la carpeta que contiene la Herramienta de aplicación manual de parches de AEM Forms en JEE (archivos extraídos).

1. Ejecute el siguiente comando para buscar todos los archivos con bibliotecas struts2 más antiguas. Antes de ejecutar el comando, reemplace la ruta del comando por la ruta del servidor de AEM Forms:


   ```
   ./patch-archive.sh -root=/opt/Adobe/Adobe_Experience_Manager_Forms/configurationManager/export/ -pattern=.*struts2-core.*jar$
   ```

   >[!NOTE]
   >
   >
   >La herramienta requiere conectividad a Internet, ya que descarga dependencias en tiempo de ejecución. Por lo tanto, antes de ejecutar la herramienta, asegúrese de que está conectado a Internet.

1. Ejecute los siguientes comandos en el orden indicado para el reemplazo recurrente in situ. Antes de ejecutar el comando, reemplace la ruta del comando por la ruta de acceso del servidor de AEM Forms y el archivo `struts2-core-2.5.33.jar`.



   ```
   ./patch-archive.sh -root=/opt/Adobe/Adobe_Experience_Manager_Forms/configurationManager/export/ -pattern=.*struts2-core.*jar$ -action=replace /opt/struts2-core-2.5.33.jar
   ```

   Los pasos anteriores parchean todos los archivos ear con bibliotecas struts2 más antiguas.

1. Anule la implementación del EAR anterior e implemente el archivo EAR parcheado, disponible en la carpeta de exportación, en el servidor de aplicaciones.

1. Inicie el servidor de AEM Forms.

>[!ENDTABS]




<!-- 
### Manual patching tool 


>[!BEGINTABS]

>[!TAB Windows]

    ```
    
    patch-archive.bat [-root=dir-or-file] [-pattern=regex] [-action=list(default)|delete|replace <replacement-file>]

    ```

* **dir-or-file**: Specifies path of directory containing multiple archives to patch. The default path for AEM Forms on JEE is <>. 
* **regex**: Specifies regular expression identifying a file or an archive entry to patch. It is tested against each file's or archive entry's absolute path. For example, the pattern `.*struts2-core-2.5.30.jar$` search for all the lines that end with the exact string `struts2-core-2.5.30.jar`.
* **list**: Lists the matched files or archive entries. It recursively searches for and reports all instances of the supplied pattern matched in any entry present in any archive file (zip/jar/war/ear) inside the supplied root directory. No changes are made to any file. It is the default action of the tool, when no action is specified.
* **delete**: Deletes the matched files or archive entries. If the matched entity is an archive, deletion happens before traversing it. This prevents any potentially matching entries inside it from being reported.  
* **replace**: Substitutes the matched files or archive entries with the supplied replacement. If the matched entity is an archive, replacement happens before traversing it. This prevents any potentially matching entries inside it from being reported.

>[!TAB macOS]

    ```
    
    patch-archive.sh [-root=dir-or-file] [-pattern=regex] [-action=list(default)|delete|replace <replacement-file>]

    ```

* **dir-or-file**: Specifies path of directory containing multiple archives to patch. The default path for AEM Forms on JEE is <>. 
* **regex**: Specifies regular expression identifying a file or an archive entry to patch. It is tested against each file's or archive entry's absolute path. For example, the pattern `.*struts2-core-2.5.30.jar$` search for all the lines that end with the exact string `struts2-core-2.5.30.jar`.
* **list**: Lists the matched files or archive entries. It recursively searches for and reports all instances of the supplied pattern matched in any entry present in any archive file (zip/jar/war/ear) inside the supplied root directory. No changes are made to any file. It is the default action of the tool, when no action is specified.
* **delete**: Deletes the matched files or archive entries. If the matched entity is an archive, deletion happens before traversing it. This prevents any potentially matching entries inside it from being reported.  
* **replace**: Substitutes the matched files or archive entries with the supplied replacement. If the matched entity is an archive, replacement happens before traversing it. This prevents any potentially matching entries inside it from being reported.  

>[!TAB Linux]

    ```
    
    patch-archive.sh [-root=dir-or-file] [-pattern=regex] [-action=list(default)|delete|replace <replacement-file>]

    ```

* **dir-or-file**: Specifies path of directory containing multiple archives to patch. The default path for AEM Forms on JEE is <>. 
* **regex**: Specifies regular expression identifying a file or an archive entry to patch. It is tested against each file's or archive entry's absolute path. For example, the pattern `.*struts2-core-2.5.30.jar$` search for all the lines that end with the exact string `struts2-core-2.5.30.jar`.
* **list**: Lists the matched files or archive entries. It recursively searches for and reports all instances of the supplied pattern matched in any entry present in any archive file (zip/jar/war/ear) inside the supplied root directory. No changes are made to any file. It is the default action of the tool, when no action is specified.
* **delete**: Deletes the matched files or archive entries. If the matched entity is an archive, deletion happens before traversing it. This prevents any potentially matching entries inside it from being reported.  
* **replace**: Substitutes the matched files or archive entries with the supplied replacement. If the matched entity is an archive, replacement happens before traversing it. This prevents any potentially matching entries inside it from being reported.  



>[!ENDTABS]









-->
