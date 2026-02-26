---
title: Revisiones de AEM Forms
description: Proporciona información sobre cómo descargar e instalar una revisión para AEM Forms.
exl-id: 37287332-3c8d-4ddc-a77e-3c5ee332898b
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
source-git-commit: 1b8290b3e1b7e5f62cda1dd45561bc4e3c09703f
workflow-type: tm+mt
source-wordcount: '2259'
ht-degree: 81%

---

# Revisiones de Adobe Experience Manager Forms{#aem-form-hotfix}

Este artículo enumera las correcciones esenciales implementadas para abordar los problemas conocidos, mejorar la estabilidad del sistema y mejorar el rendimiento general de AEM Forms.

>[!NOTE]
>
> Las revisiones están diseñadas para ser acumulativas e incluyen todas las correcciones anteriores. Al aplicar la revisión más reciente a una versión, no solo se aborda el problema más reciente, sino que también incorpora todas las correcciones de errores y mejoras anteriores.

## Revisiones de AEM Forms {#hotfix-for-aem-forms}

<table>
  <tbody>
  <tr>
    <td><strong>Fecha</strong></td>
    <td><strong>Vínculo de descarga de revisión (vínculo de distribución de software de AEM)</strong></td>
    <td><strong>Problemas solucionados</strong></td>
  </tr>
  <tr>
    <td>
      <strong>18 de febrero de 2026</strong><br>
      <em>Se aplica a:</em> AEM Forms en el paquete de servicio JEE 6.5.24.0<br>
    </td>
    <td>
    <ul>
    <strong>Jboss:</strong>
    <li>Windows: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-patch/jboss/adobe-aem-forms-jee-hotfix-6.5.24.0-win-jboss.zip">revisión para el paquete de servicio 6.5.24.0 de AEM en el servidor JEE de Windows para JBoss</a></li>
    <li>Linux: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-patch/jboss/adobe-aem-forms-jee-hotfix-6.5.24.0-linux-jboss.zip">revisión para AEM Service Pack 6.5.24.0 en Linux para el servidor JEE de JBoss</a></li>
    <strong>Lógica Web:</strong>
    <li>Windows: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-patch/weblogic/adobe-aem-forms-jee-hotfix-6.5.24.0-win-weblogic.zip">revisión para el Service Pack 6.5.24.0 de AEM en el servidor JEE de Windows para Weblogic</a></li>
    <li>Linux: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-patch/weblogic/adobe-aem-forms-jee-hotfix-6.5.24.0-linux-weblogic.tar.gz">revisión para AEM Service Pack 6.5.24.0 en Linux para el servidor JEE de Weblogic</a></li>
    <strong>Esfera web:</strong>
    <li>Windows: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-patch/websphere/adobe-aem-forms-jee-hotfix-6.5.24.0-win-websphere.zip">revisión para AEM Service Pack 6.5.24.0 en Windows para el servidor Websphere JEE</a></li>
    <li>Linux: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-patch/websphere/adobe-aem-forms-jee-hotfix-6.5.24.0-linux-websphere.zip">revisión para AEM Service Pack 6.5.24.0 en Linux para el servidor Websphere JEE</a></li>
    </ul>
    </td>
    <td>
    <ul>
    <li><b>FORMS-23789</b> soluciona problemas relacionados con Log4j en AEM Forms en JEE SP24 que causaban interrupciones en el registro y la monitorización para clientes empresariales.
    </ul>
    </td>
  </tr>
    <tr>
    <td>
      <strong>17 de febrero de 2026</strong><br>
      <em>Se aplica a:</em> AEM Forms SP24<br>
    </td>
    <td>
    <ul> <a href = "https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/cq-6.5.0-hotfix-GRANITE-64751-SP24-1.0.zip"> revisión de AEM 6.5 Forms</a>
    </ul>
    </td>
    <td>
    <ul>
    <li>Los conectores del modelo de datos de formulario <b>GRANITE-63681</b> pueden no autenticarse debido a que las palabras clave y el patrón regex requeridos no están permitidos de manera predeterminada.</li>
    </ul>
    </td>
  </tr>
    <tr>
    <td>
      <strong>17 de febrero de 2026</strong><br>
      <em>Se aplica a:</em> AEM Forms SP24<br>
    </td>
    <td>
    <ul>
    <li>Windows: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-on-add-on/adobe-aemfd-win-pkg-6.0.1454.zip">revisión para AEM Forms AddOn 6.0.1454 en Windows</a></li>
    <li>Linux: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-on-add-on/adobe-aemfd-linux-pkg-6.0.1454.zip">Revisión para AEM Forms AddOn 6.0.1454 en Linux</a></li>
    <li>OSX: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-on-add-on/adobe-aemfd-osx-pkg-6.0.1454.zip">revisión para el complemento AEM Forms 6.0.1454 en macOS</a></li>
    </ul>
    </td>
    <td>
    <ul>
    <li><b>FORMS-23802</b> Las funciones personalizadas no funcionan en la vista previa ni en la publicación cuando el formulario adaptable está incrustado en una página de Sites y la versión del componente principal de aem-forms es anterior a 1.1.76. Esta revisión restaura la compatibilidad con versiones anteriores de aem-forms-core-component.
    </ul>
    </td>
  </tr>
  <tr>
    <td>
      <strong>10 de febrero de 2026</strong><br>
      <em>Se aplica a:</em> AEM Forms SP24<br>
    </td>
    <td>
    <ul> <a href = "https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/bb-expressionmanager-pkg-10.0.48.zip"> revisión del complemento de AEM 6.5 Forms</a>
    </ul>
    </td>
    <td>
    <ul>
    <li><b>FORMS-23875</b> En la búsqueda del modelo de datos de formulario, se muestra una etiqueta de HTML en la interfaz de usuario aunque no haya una entidad relevante.
      <ul></tr>
  <tr>
    <td>
      <strong>14 de octubre de 2025</strong><br>
      <em>Se aplica a:</em> ImgToPdf está fallando con AEM Forms SP23 Jboss<br>
    </td>
    <td>
    <ul> Para obtener una solución, comuníquese con <a href="https://business.adobe.com/in/support/main.html">Soporte técnico de Adobe Experience Manager Forms</a>
    </ul>
    </td>
    <td>
    <ul>
    <li> <b>(FORMS-22029):</b> Mejora la confiabilidad de la conversión de PDF al solucionar un problema en el que PDF Generator (PDFG) no puede convertir archivos de imagen a PDF después de actualizar a SP23, lo que provoca errores inesperados posteriores al procesamiento.
      <ul></tr>
  <tr>
    <td>
      <strong>23 de septiembre de 2025</strong><br>
    </td>
    <td>
    <ul>
    <strong>Jboss:</strong>
    <li>Windows: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-23-0-hotfix-3/jboss/adobe-aem-forms-jee-hotfix3-6.5.23.0-win-jboss.zip">revisión para AEM Service Pack 6.5.23.0 en Windows para el servidor JBoss JEE</a></li>
    <li>Linux: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-23-0-hotfix-3/jboss/adobe-aem-forms-jee-hotfix3-6.5.23.0-linux-jboss.tar.gz">revisión para AEM Service Pack 6.5.23.0 en Linux para el servidor JBoss JEE</a></li>
    <strong>Lógica Web:</strong>
    <li>Windows: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-23-0-hotfix-3/weblogic/adobe-aem-forms-jee-hotfix3-6.5.23.0-win-weblogic.zip">revisión para AEM Service Pack 6.5.23.0 en Windows para el servidor Weblogic JEE</a></li>
    <li>Linux: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-23-0-hotfix-3/weblogic/adobe-aem-forms-jee-hotfix3-6.5.23.0-linux-weblogic.tar.gz">revisión para AEM Service Pack 6.5.23.0 en Linux para el servidor Weblogic JEE</a></li>
    <strong>Esfera web:</strong>
    <li>Windows: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-23-0-hotfix-3/websphere/adobe-aem-forms-jee-hotfix3-6.5.23.0-win-websphere.zip">revisión para el paquete de servicio 6.5.23.0 de AEM en el servidor JEE de Windows para Websphere</a></li>
    <li>Linux: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-23-0-hotfix-3/websphere/adobe-aem-forms-jee-hotfix3-6.5.23.0-linux-websphere.tar.gz">revisión para AEM Service Pack 6.5.23.0 en Linux para el servidor JEE de Websphere</a></li>
    </ul>
    </td>
    <td>
    <ul>
    <strong>Esta revisión corrige lo siguiente:</strong> 
    <li> <b>(FORMS-21378):</b> Se mejoró la confiabilidad del envío de formularios al solucionar un problema en el que los envíos fallan cuando la validación del lado del servidor (SSV) está habilitada y la información calculada de Meta está vacía.

<li> <b>(FORMS-21721):</b> Se ha mejorado un problema por el que las conversiones de PS a PDF y de HTML a PDF (WebKit) fallan tras implementar la revisión (publicada el <b>5 de agosto de 2025</b>) para 6.5.23.0. 
    </li>
    </ul>
    </td>    
  </tr>
    </ul>
    </td>
  <tr>
    <td>
      <strong>5 de agosto de 2025</strong><br>
      <em>Se aplica a:</em> AEM 6.5 Forms Service Pack 23<br>
      <em>Instrucciones de instalación:</em>
      <a href="/help/forms/using/mitigating-xxe-and-configuration-vulnerabilities-for-experience-manager-forms-jee.md#option-1-for-users-on-version-65230-install-latest-hotfix">
        Mitigación de vulnerabilidades de XXE, configuración y ejecución remota de código (CVE-2025-49533) para AEM Forms en JEE
      </a>
    </td>
    <td>
    <ul>
    <li><strong>Jboss:</strong></li>
    <li>Windows: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-02/jboss/adobe-aem-forms-jee-hotfix2-6.5.23.0-win-jboss.zip">revisión para AEM Service Pack 6.5.23.0 en Windows para el servidor JBoss JEE</a></li>
    <li>Linux: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-02/jboss/adobe-aem-forms-jee-hotfix2-6.5.23.0-linux-jboss.tar.gz">revisión para AEM Service Pack 6.5.23.0 en Linux para el servidor JBoss JEE</a></li>
    <li><strong>Weblogic:</strong></li>
    <li>Windows: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-02/weblogic/adobe-aem-forms-jee-hotfix2-6.5.23.0-win-weblogic.zip">revisión para AEM Service Pack 6.5.23.0 en Windows para el servidor Weblogic JEE</a></li>
    <li>Linux: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-02/weblogic/adobe-aem-forms-jee-hotfix2-6.5.23.0-linux-weblogic.tar.gz">revisión para AEM Service Pack 6.5.23.0 en Linux para el servidor Weblogic JEE</a></li>
    <li><strong>Websphere:</strong></li>
    <li>Windows: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-02/websphere/adobe-aem-forms-jee-hotfix2-6.5.23.0-win-websphere.zip">revisión para el paquete de servicio 6.5.23.0 de AEM en el servidor JEE de Windows para Websphere</a></li>
    <li>Linux: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-02/websphere/adobe-aem-forms-jee-hotfix2-6.5.23.0-linux-websphere.zip">revisión para AEM Service Pack 6.5.23.0 en Linux para el servidor JEE de Websphere</a></li>
    </ul>
    </td>
    <td>
    <ul>
    <li>Seguridad mejorada al abordar una vulnerabilidad de ejecución remota de código (RCE) en Adobe Experience Manager (AEM) Forms. El problema estaba relacionado con el modo de desarrollo Struts en la interfaz de usuario (IU) de administración, que permitía la evaluación arbitraria del lenguaje de navegación objeto-gráfico (OGNL) a través de la funcionalidad de depuración. Esta corrección garantiza que el modo de desarrollo de Struts esté deshabilitado y que se apliquen los filtros de seguridad adecuados para evitar el acceso no autorizado.</li>
    <li>Se ha mejorado la protección contra las vulnerabilidades de entidad externa (XXE) de lenguaje de marcado extensible (XML) en el módulo de componente de documento electrónico (EDC) de Adobe Experience Manager (AEM) Forms. Las vulnerabilidades se debían a la administración incorrecta de documentos XML sin protecciones XXE, lo que podría provocar lecturas de archivos locales. La corrección incluye lo siguiente:
      <ul>
        <li>Asegurarse de que DocumentBuilderFactory utilizado en la clase SecurityCheckHandler está configurado para evitar ataques XXE.</li>
        <li>Actualizar el servicio web de EDC para gestionar documentos XML de forma segura, lo que evita el acceso no autorizado a archivos locales.</li>
      </ul>
    </li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>
      <strong>5 de agosto de 2025</strong><br>
      <em>Se aplica a:</em> AEM 6.5 Forms Service Pack 18 - 22<br>
      <em>Instrucciones de instalación:</em>
      <a href="/help/forms/using/mitigating-xxe-and-configuration-vulnerabilities-for-experience-manager-forms-jee.md#option-2-for-users-on-65180---65220-manual-hotfix-installation">
        Instalación manual de revisión para Service Packs 18-22
      </a>
    </td>
    <td>
    <ul>
    <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/adobe-xxe-configuration-hotfix.zip">Parche para AEM 6.5 Forms Service Pack 18 - AEM 6.5 Forms Service Pack 22 </a></li>
    </ul>
    </td>
    <td>
    <ul>
    <li>Seguridad mejorada al abordar una vulnerabilidad de ejecución remota de código (RCE) en Adobe Experience Manager (AEM) Forms. El problema estaba relacionado con el modo de desarrollo Struts en la interfaz de usuario (IU) de administración, que permitía la evaluación arbitraria del lenguaje de navegación objeto-gráfico (OGNL) a través de la funcionalidad de depuración. Esta corrección garantiza que el modo de desarrollo de Struts esté deshabilitado y que se apliquen los filtros de seguridad adecuados para evitar el acceso no autorizado.</li>
    <li>Se ha mejorado la protección contra las vulnerabilidades de entidad externa (XXE) del lenguaje de marcado extensible (XML) en el módulo de seguridad de documentos de Adobe Experience Manager (AEM) Forms. Las vulnerabilidades se debían a la administración incorrecta de documentos XML sin protecciones XXE, lo que podría provocar lecturas de archivos locales. La corrección incluye lo siguiente:
      <ul>
        <li>Asegurarse de que DocumentBuilderFactory utilizado en la clase SecurityCheckHandler está configurado para evitar ataques XXE.</li>
        <li>Actualizar el servicio web de seguridad de documentos para gestionar documentos XML de forma segura, lo que evita el acceso no autorizado a archivos locales.</li>
      </ul>
    </li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>10 de julio de 2025</td>
    <td>
    <ul>
    <li><strong>Jboss:</strong></li>
    <li>Windows: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-2/jboss/adobe-aem-forms-jee-hotfix-6.5.23.0-win-jboss.zip">revisión para AEM Service Pack 6.5.23.0 en Windows para el servidor JBoss JEE</a></li>
    <li>Linux: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-2/jboss/adobe-aem-forms-jee-hotfix-6.5.23.0-linux-jboss.tar.gz">revisión para AEM Service Pack 6.5.23.0 en Linux para el servidor JBoss JEE</a></li>
    <li><strong>Weblogic:</strong></li>
    <li>Windows: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-2/weblogic/adobe-aem-forms-jee-hotfix-6.5.23.0-win-weblogic.zip">revisión para AEM Service Pack 6.5.23.0 en Windows para el servidor Weblogic JEE</a></li>
    <li>Linux: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-2/weblogic/adobe-aem-forms-jee-hotfix-6.5.23.0-linux-weblogic.tar.gz">revisión para AEM Service Pack 6.5.23.0 en Linux para el servidor Weblogic JEE</a></li>
    <li><strong>Websphere:</strong></li>
    <li>Windows: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-2/websphere/adobe-aem-forms-jee-hotfix-6.5.23.0-win-websphere.zip">revisión para AEM Service Pack 6.5.23.0 en Windows para el servidor Websphere JEE</a></li>
    <li>Linux: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-2/websphere/adobe-aem-forms-jee-hotfix-6.5.23.0-linux-websphere.tar.gz">revisión para AEM Service Pack 6.5.23.0 en Linux para el servidor Websphere JEE</a></li>
    </ul>
    </td>
    <td>
    <ul>
    <li><strong>Esta revisión corrige lo siguiente:</strong>
      <ul>
        <li><strong>FORMS-20533:</strong> AEM Forms ahora incluye una actualización de la versión de Struts de la versión 2.5.33 a la 6.x para el componente de formularios. Esto proporciona cambios, anteriormente omitidos, de Struts que no se han incluido en el SP23. La compatibilidad se añadió mediante una revisión que puede descargar e instalar para que sea compatible con la última versión de Struts.</li>
        <li><strong>FORMS-20532:</strong> AEM Forms ahora incluye una actualización desde la versión Struts 2.5.33 a la 6.x para el componente de salida. Esto proporciona cambios, anteriormente omitidos, de Struts que no se han incluido en el SP23. La compatibilidad se añadió mediante una revisión que puede descargar e instalar para que sea compatible con la última versión de Struts.</li>
        <li><strong>FORMS-20203:</strong> Cuando un usuario actualiza Struts desde AEM Service Pack 2.5.x a AEM Forms Service Pack 6.x, la IU de directivas no muestra todas las configuraciones, como la opción de añadir una marca de agua. Puede descargar e instalar la revisión para resolver este problema.</li>
        <li><strong>FORMS-20360:</strong> Después de actualizar a AEM Forms Service Pack 6.5.23.0, el servicio de conversión ImageToPDF genera el siguiente error:<br>
        <code>17:15:44,468 ERROR [com.adobe.pdfg.GeneratePDFImpl] (default task-49) ALC-PDG-001-000-ALC-PDG-011-028-Error occurred while converting the input image file to PDF. com/adobe/internal/pdftoolkit/core/encryption/EncryptionImp</code><br>
        Puede descargar e instalar la revisión para resolver este problema.</li>
      </ul>
    </li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>26 de marzo de 2025 </br> </br> Para instalar esta corrección, siga las instrucciones <a href="/help/forms/using/mitigating-spring-framework-vulnerabilities-for-aem-forms-on-jee.md"> Mitigación de vulnerabilidades de Spring Framework para AEM Forms en JEE</a>.</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/jboss/adobe-aem-forms-jee-hotfix-6.5.22.0-win-jboss.tar.gz">Revisión para AEM Service Pack 6.5.22.0 en Windows para el servidor JBoss JEE </a> </li>
      <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/jboss/adobe-aem-forms-jee-hotfix-6.5.22.0-linux-jboss.tar.gz">Revisión para AEM Service Pack 6.5.22.0 en Linux para el servidor JBoss JEE </a> </li>
       <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/weblogic/adobe-aem-forms-jee-hotfix-6.5.22.0-win-weblogic.tar.gz">Revisión para AEM Service Pack 6.5.22.0 en Windows para el servidor Weblogic JEE </a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/weblogic/adobe-aem-forms-jee-hotfix-6.5.22.0-linux-weblogic.tar.gz">Revisión para AEM Service Pack 6.5.22.0 en Linux para el servidor Weblogic JEE</a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/websphere/adobe-aem-forms-jee-hotfix-6.5.22.0-win-websphere.tar.gz">Revisión para AEM Service Pack 6.5.22.0 en Windows para el servidor Websphere JEE </a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/websphere/adobe-aem-forms-jee-hotfix-6.5.22.0-linux-websphere.tar.gz">Revisión para AEM Service Pack 6.5.22.0 en Linux para el servidor Websphere JEE</a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li>Mitigación de vulnerabilidades de Spring Framework para AEM Forms en JEE</li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>10 de julio de 2024</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/jboss/win/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-windows-jboss.zip.zip">Revisión AEM Service Pack 6.5.21.0 en Windows para el servidor JBoss JEE </a> </li>
      <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/jboss/linux/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-linux-jboss.tar.gz">Revisión para AEM Service Pack 6.5.21.0 en Linux para el servidor JBoss JEE </a> </li>
       <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/websphere/win/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-windows-websphere.zip.zip">Revisión para AEM Service Pack 6.5.21.0 en Windows para el servidor Websphere JEE </a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/websphere/linux/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-linux-websphere.tar.gz">Revisión para AEM Service Pack 6.5.21.0 en Linux para el servidor Websphere JEE</a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/weblogic/win/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-windows-weblogic.zip.zip">Revisión para AEM Service Pack 6.5.21.0 en Windows para el servidor Weblogic JEE </a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/weblogic/linux/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-linux-weblogic.tar.gz">Revisión para AEM Service Pack 6.5.21.0 en Linux para el servidor Weblogic JEE</a> </li>
     </ul>
     </td>
    <td>
    <ul><li>Cuando un usuario actualiza a AEM Forms Service Pack 20 (6.5.20.0) en el servidor JEE y genera archivos PDF mediante los servicios de salida, los archivos PDF se procesan con problemas de accesibilidad. (LC-3922112)</li><li>Los PDF etiquetados generados mediante el servicio de salida en AEM Forms JEE muestran “Advertencia de estructura inadecuada”. (LC-3922038)</li><li>Cuando se envía un formulario en AEM Forms JEE, las instancias de un elemento XML repetitivo se eliminan de los datos. (LC-3922017)</li><li>Cuando un usuario en un entorno Linux procesa un formulario adaptable (en JEE) en HTML, no se procesa correctamente. (LC-3921957)</li><li>Cuando un usuario convierte un archivo XTG al formato PostScript mediante el servicio de salida en AEM Forms JEE, se produce el siguiente error: AEM_OUT_001_003: Unexpected Exception: PAExecute Failure: XFA_RENDER_FAILURE.  (LC-3921720)</li><li>Después de actualizar a AEM Forms Service Pack 18 (6.5.18.0) en el servidor JEE, cuando un usuario envía un formulario, no pueden procesar formularios HTML5 o PDF y se bloquea XMLFM. (LC-3921718)
    </ul>
    </td>    
  </tr>
  <tr>
    <td>21 de junio de 2024</td>
     <td>
     <ul>
     <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&amp;reserved=0">Revisión para AEM Service Pack 6.5.21.0 o AEM Forms Service Pack 6.5.22.0 en el servidor JBoss JEE </a> </li>
      <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&amp;reserved=0">Revisión para AEM Service Pack 6.5.21.0 o AEM Forms Service Pack 6.5.22.0 en el servidor Weblogic JEE </a> </li>
       <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&amp;reserved=0">Revisión para AEM Service Pack 6.5.21.0 o AEM Forms Service Pack 6.5.22.0 en el servidor Webshop JEE </a> </li>
        <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&amp;reserved=0">Revisión para AEM Service Pack 6.5.21.0 o AEM Forms Service Pack 6.5.22.0 en el servidor OSGi </a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li> Después de actualizar a AEM Forms Service Pack 6.5.21.0 o AEM Forms Service Pack 6.5.22.0, el servicio PaperCapture da error al realizar operaciones de OCR (Reconocimiento óptico de caracteres) en archivos PDF. Para obtener instrucciones de instalación, consulte el artículo <a href="/help/forms/using/papercapture-service-resolution.md"> solución de problemas</a>.(CQDOC-21680) </li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>21 de junio de 2024</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2Fccm-ccr-content-10.0.206.zip">Revisión para AEM Service Pack 6.5.21.0 </a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li>Los borradores de cartas con datos XML se quedan atascados en el estado de carga durante la vista previa. Para obtener instrucciones de descarga e instalación de la revisión, consulte la sección<a href="#install-hotfix"> Descargar e instalar la revisión para el problema con el borrador de la carta</a>.(FORMS-14521)</li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>16 de mayo de 2024</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-win-pkg-6.0.1192-010.zip">Revisión para AEM Service Pack 6.5.20.0 para Microsoft Windows</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-linux-pkg-6.0.1192-010.zip">Revisión para AEM Service Pack 6.5.20.0 para Linux </a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-osx-pkg-6.0.1192-010.zip">Revisión para AEM Service Pack 6.5.20.0 para Apple macOS</a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li>En un formulario adaptable basado en un XDP con scripts incrustados en las casillas de verificación, los scripts no se ejecutan para los elementos después de dichas casillas de verificación. Hay una revisión disponible para este problema. (FORMS-14244) </li>
     <li> Las filas del widget selector de fechas se truncan al recorrer los meses en el widget emergente de los campos con el patrón Editar/Mostrar. Hay una revisión disponible para este problema. (FORMS-13620) </li>
     <li>Los envíos de formularios fallan al intentar utilizar el servicio DOR (documento de registro) en el backend. Aparece este mensaje de error: “No se pudo completar la acción de envío porque el recurso de formulario no se ha asignado correctamente”. (FORMS-13798) </li>
     <li>Cuando se envía un formulario adaptable desde una instancia de publicación de Adobe Experience Manager a un flujo de trabajo de Adobe Experience Manager, el flujo de trabajo no guarda los archivos adjuntos. (FORMS-14209) </li>
     <li> Al instalar AEM 6.5 Forms Service Pack 20 (el paquete de complemento de AEM Forms para SP20), la IU de AEM Sites muestra una degradación significativa del rendimiento.  (FORMS-13791) </li>
     <li>El servicio de rellenado previo falla con una excepción de puntero nulo en las comunicaciones interactivas. (CQDOC-21355)</li>
     <li>Las configuraciones que utilizan el servicio en la nube heredado para Adobe Analytics con autenticación basada en credenciales de usuario no funcionan correctamente, lo que provoca que no se ejecuten las reglas de análisis. (FORMS-15428)
    </ul>
    </td>    
  </tr>
  <tr>
    <td>29 de enero de 2024</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fforms-foundation-qs-content-4.0.170-FORMS-12692-B0001.zip">Revisión para AEM Service Pack 6.5.19.0 para Windows en el servidor JEE</a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li>En AEM Forms en el servidor JEE, no se pueden procesar formularios HTML5 que utilizan la ruta de contexto. (FORMS-12485, FORMS-12691).</li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>29 de enero de 2024</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fadobe-aemfd-win-pkg-6.0.1016-004.zip">Revisión para AEM Service Pack 6.5.18.0 para Microsoft Windows</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fadobe-aemfd-linux-pkg-6.0.1016-004.zip">Revisión para AEM Service Pack 6.5.18.0 para Linux</a></li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fadobe-aemfd-osx-pkg-6.0.1016-004.zip">Revisión para AEM Service Pack 6.5.18.0 para Apple macOS</a></li>
     </ul>
     </td>
    <td>
    <ul>
    <li> El componente de firma manuscrita listo para usar no se puede procesar para una vista previa en un formulario adaptable. (FORMS-12073).</li>
    </ul>
    </td>    
   </tr>
   <tr>
    <td>20 de noviembre de 2023</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-linux-pkg-6.0.1016-002.zip">Revisión para AEM Service Pack 6.5.18.0 para Linux</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-win-pkg-6.0.1016-002.zip">Revisión para AEM Service Pack 6.5.18.0 para Microsoft Windows</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-osx-pkg-6.0.1016-002.zip">Revisión para AEM Service Pack 6.5.18.0 para Apple macOS</a></li>
     </ul>
     </td>
    <td>
    <ul>
    <li>La firma en línea deja de funcionar cuando se establece una URL de redireccionamiento en el contenedor de guía de un formulario adaptable. (FORMS-10493)</li>
    <li>Las plantillas de documento de registro (DoR) no se pueden publicar para formularios adaptables localizados. (FORMS-10535)</li>
    <li>La comunicación interactiva con imágenes en línea grandes no se puede abrir en modo de edición. (FORMS-10578)</li>
    </ul>
    </td>    
  </tr>
  <tbody>
</table>

## Descargar e instalar una revisión de OSGi {#download-install-hotfix}

Realice los siguientes pasos para descargar e instalar la revisión:

1. Descargue la [revisión](#hotfix-for-adaptive-forms) mediante el vínculo de distribución de software.
1. Extraiga el archivo de revisión para poder obtener un paquete Experience Manager (.zip) y archivos de paquete (.jar).
1. Cargue e instale el paquete (.zip) mediante el [Administrador de paquetes](https://experienceleague.adobe.com/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager.html?lang=es#accessing).
1. Abra los paquetes del administrador de configuración `https://server:host/system/console/bundles`, cargue e instale el paquete (.jar). La revisión está instalada.

## Instalación de un parche JEE {#download-install-jee-patch}

Para obtener instrucciones para instalar un parche JEE, consulte la [documentación del instalador de revisiones JEE de AEM Forms](/help/release-notes/jee-patch-installer-65.md).


## Descargar e instalar la revisión para un problema de cartas borrador {#install-hotfix}

Para resolver el problema, realice los siguientes pasos:

1. Descargue la [revisión](#hotfix-for-adaptive-forms) desde el portal de distribución de software.
2. Cargue e instale el paquete (.zip) mediante el [Administrador de paquetes de CRX](https://experienceleague.adobe.com/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager.html?lang=es#accessing).
