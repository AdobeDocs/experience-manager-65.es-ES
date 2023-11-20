---
title: AEM Revisión para el paquete de servicio del formulario de
description: Proporciona información sobre cómo descargar e instalar la revisión del Service Pack de AEM Forms
source-git-commit: 169d407835098add0312b0d12c2c80035b525762
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 1%

---


# Revisiones de Adobe Experience Manager{#aem-form-hotfix}

La instalación de la última [AEM Paquete de servicio de](/help/release-notes/release-notes.md) se recomienda que incluya correcciones y mejoras clave de seguridad, rendimiento, estabilidad y del cliente realizadas tras la disponibilidad general de Adobe Experience Manager 6.5.

## Revisiones para Forms adaptable {#hotfix-for-adaptive-forms}

<table>
  <tbody>
  <tr>
    <td><strong>Fecha</strong></td>
    <td><strong>Nombres de revisión</strong></td>
    <td><strong>Correcciones</strong></td>
   </tr>
   <tr>
    <td>20 de noviembre de 2023</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-linux-pkg-6.0.1016-002.zip">AEM Revisión para el paquete de servicio 6.5.18.0 de para Linux</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-win-pkg-6.0.1016-002.zip">AEM Revisión para el paquete de servicio 6.5.18.0 de para Windows</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-osx-pkg-6.0.1016-002.zip">AEM Revisión para el paquete de servicio 6.5.18.0 de para el sistema operativo Mac</a></li>
     </ul>
     </td>
    <td>
    <ul>
    <li>La firma en línea deja de funcionar cuando se establece una URL de redireccionamiento en el contenedor de guía de un formulario adaptable. (FORMS-10493)</li>
    <li>Las plantillas de documento de registro (DoR) no se pueden publicar para Forms adaptable localizado. (FORMS-10535)</li>
    <li>La comunicación interactiva con imágenes en línea grandes no se puede abrir en modo de edición. (FORMS-10578)</li>
    </ul>
    </td>    
    </tr>
    <tbody>
     </table>

## Descargar e instalar revisión {#download-install-hotfix}

Siga estos pasos para descargar e instalar la revisión:

1. Descargar [Revisión](#hotfix-for-adaptive-forms) desde el vínculo SD.
1. Extraiga el archivo de revisión para poder obtener un paquete de Experience Manager (.zip) y archivos de paquete (.jar).
1. Cargue e instale el paquete (.zip) mediante el Administrador de paquetes.
1. Abra los paquetes del administrador de configuración `https://server:host/system/console/bundles`, cargue e instale el paquete (.jar).
