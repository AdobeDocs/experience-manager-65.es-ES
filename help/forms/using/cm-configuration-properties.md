---
title: Propiedades de configuración de la gestión de correspondencia
seo-title: Correspondence Management Configuration Properties
description: En este tema se explica cómo modificar el Compositor de recursos con configuraciones específicas de la solución. En este tema se detallan las propiedades que puede editar, con su descripción, los valores predeterminados y los valores aceptables.
seo-description: This topic explains how you can modify Asset Composer with solution-specific configurations. This topic details the properties you can edit, with their description, default values, and acceptable values.
uuid: 6b401d51-9332-459b-b751-42a9b5a1462d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: f2955419-c680-44a7-9913-c594b4577551
feature: Correspondence Management
exl-id: c9c007d0-c545-4738-b11b-4c50986342ee
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '845'
ht-degree: 4%

---

# Propiedades de configuración de la gestión de correspondencia {#correspondence-management-configuration-properties}

Para configurar estas propiedades, abra la siguiente URL en un explorador: `https://<server>:<port>/<contextPath>/system/console/configMgr` y seleccione **Configuraciones de administración de correspondencia**.

La gestión de correspondencia tiene las siguientes propiedades de configuración:

<table>
 <tbody>
  <tr>
   <th><p><strong>Propiedad</strong></p> </th>
   <th><p><strong>Descripción</strong></p> </th>
   <th><p><strong>Predeterminado</strong></p> </th>
   <th><p><strong>Valores aceptables</strong></p> </th>
  </tr>
  <tr>
   <td><p>Sangría</p> </td>
   <td>Sangría en módulos<p> </p> </td>
   <td><p>12,7 mm</p> </td>
   <td><p>Cualquier número</p> </td>
  </tr>
  <tr>
   <td>Ancho mínimo de número</td>
   <td>Ancho mínimo que se aplicará en el campo viñeta/número, al utilizar listas numeradas separadas de números romanos</td>
   <td>8,0 mm</td>
   <td>Cualquier número</td>
  </tr>
  <tr>
   <td><p>Anchura mínima de los números romanos</p> </td>
   <td><p>Anchura mínima que se aplicará en el campo viñeta/número, al utilizar números romanos</p> </td>
   <td><p>12,7 mm</p> </td>
   <td><p>Cualquier número</p> </td>
  </tr>
  <tr>
   <td>Tipo de representación</td>
   <td>El tipo de representación que utiliza la aplicación Crear correspondencia para obtener la vista previa de la carta. </td>
   <td>Representación del HTML</td>
   <td>Representación del HTML/Representación del PDF</td>
  </tr>
  <tr>
   <td><p>Habilitar resaltado de PDF CCR</p> </td>
   <td><p>Habilita el resaltado en el PDF en la aplicación Crear correspondencia</p> </td>
   <td><p>true</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Tipo de resaltado de destino</p> </td>
   <td><p>Tipo de resaltado de destino en la aplicación Crear correspondencia</p> </td>
   <td><p>border</p> </td>
   <td><p>borde/relleno/ninguno</p> </td>
  </tr>
  <tr>
   <td><p>Color de resaltado de destino</p> </td>
   <td><p>Color de resaltado de destino en la aplicación Crear correspondencia</p> </td>
   <td><p>90;155;245</p> </td>
   <td><p>Cualquier color del RGB en el formato R;G;B</p> </td>
  </tr>
  <tr>
   <td><p>Tipo de resaltado de contenido</p> </td>
   <td><p>Tipo de resaltado de contenido en la aplicación Crear correspondencia</p> </td>
   <td><p>Relleno</p> </td>
   <td><p>borde/relleno/ninguno</p> </td>
  </tr>
  <tr>
   <td><p>Color de resaltado de contenido</p> </td>
   <td><p>Color de resaltado de contenido en la aplicación Crear correspondencia</p> </td>
   <td><p>210;225;245</p> </td>
   <td><p>Cualquier color del RGB en el formato R;G;B</p> </td>
  </tr>
  <tr>
   <td><p>Tipo de resaltado de campo</p> </td>
   <td><p>Tipo de resaltado de campo en la aplicación Crear correspondencia</p> </td>
   <td><p>fill</p> </td>
   <td><p>borde/relleno/ninguno</p> </td>
  </tr>
  <tr>
   <td><p>Color de resaltado de campo</p> </td>
   <td><p>Color de resaltado de campo en la aplicación Crear correspondencia</p> </td>
   <td><p>210;225;245</p> </td>
   <td><p>Cualquier color del RGB en el formato R;G;B</p> </td>
  </tr>
  <tr>
   <td><p>Tiempo de espera de la aplicación</p> </td>
   <td><p>Tiempo de espera de la aplicación en segundos</p> </td>
   <td><p>1200</p> </td>
   <td><p>Cualquier número</p> </td>
  </tr>
  <tr>
   <td><p>nombre del parámetro del documento del PDF</p> </td>
   <td><p>Nombre del parámetro del documento del PDF en el proceso posterior</p> </td>
   <td><p>inPDFDoc</p> </td>
   <td><p>Cualquier nombre de variable de cadena</p> </td>
  </tr>
  <tr>
   <td><p>Nombre del parámetro de datos XML</p> </td>
   <td><p>Nombre del parámetro para documento XML (datos) en proceso posterior</p> </td>
   <td><p>inXMLDoc</p> </td>
   <td><p>Cualquier nombre de variable de cadena</p> </td>
  </tr>
  <tr>
   <td><p>Nombre del parámetro de documento XDP</p> </td>
   <td><p>Nombre del parámetro para el documento XDP enviado al proceso posterior</p> </td>
   <td><p>inXDPDoc</p> </td>
   <td><p>Cualquier nombre de variable de cadena</p> </td>
  </tr>
  <tr>
   <td><p>Nombre del parámetro de URL de redireccionamiento</p> </td>
   <td><p>Nombre del parámetro para la URL de redireccionamiento enviada desde el proceso de publicación Este valor puede ser cualquier nombre de variable de cadena</p> </td>
   <td><p>redirectURL</p> </td>
   <td><p>Cualquier nombre de variable de cadena</p> </td>
  </tr>
  <tr>
   <td><p>Tipo de envío del PDF</p> </td>
   <td><p>Tipo de envío de PDF (tipo de PDF generado al realizar el envío desde la aplicación Crear correspondencia)</p> </td>
   <td><p>nonInteractive</p> </td>
   <td><p>interactivo/no interactivo</p> </td>
  </tr>
  <tr>
   <td><p>Optimizar instancia del diccionario de datos</p> </td>
   <td><p>Habilita la transferencia optimizada de la instancia del diccionario de datos b/w servidor y cliente</p> </td>
   <td><p>true</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Incoherencias de corrección automática </p> </td>
   <td><p>Cuando está habilitado, gestiona automáticamente las posibles incoherencias en las asignaciones de cartas</p> </td>
   <td><p>true</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Usar formatos de datos configurados</p> </td>
   <td><p>Controla si se deben usar formatos de edición de datos configurados y formato de visualización de datos</p> </td>
   <td><p>true</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Formatos de visualización de datos</p> </td>
   <td><p>Especifica el formato de visualización específico de la configuración regional para los datos</p> </td>
   <td><p>locale=en_US; dateFormat=dd-MM-yyyy; numberDecimalSeparator=.; numberGroupSeparator=,; numberUseGroupSeparator=truelocale=de_DE; dateFormat=dd-MM-yyyy; numberDecimalSeparator=,; numberGroupSeparator=.; numberUseGroupSeparator=truelocale=fr_FR; dateFormat=dd-MM-yyyy; numberDecimalSeparator=,; numberGroupSeparator= ; numberUseGroupSeparator=truelocale=ja_JP; dateFormat=dd-MM-yyyy; numberDecimalSeparator=.; numberGroupSeparator=,; numberUseGroupSeparator=true</p> </td>
   <td><p>—</p> </td>
  </tr>
  <tr>
   <td><p>Formato de edición de datos</p> </td>
   <td><p>Editar formato para los datos. Se utiliza al escribir datos como String o al analizar datos de String</p> </td>
   <td><p>locale=en_US; dateFormat=dd-MM-yyyy; numberDecimalSeparator=.; numberGroupSeparator=,; numberUseGroupSeparator=true</p> </td>
   <td>—<p> </p> </td>
  </tr>
  <tr>
   <td><p>Administrar instancias de carta en publicación</p> </td>
   <td><p>Habilitar/deshabilitar la funcionalidad Administrar carta (aplicable solo para el servidor de publicación)</p> </td>
   <td><p>false</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Habilitar auditoría</p> </td>
   <td><p>Habilitar/deshabilitar la funcionalidad de auditoría. Si es false, los registros de auditoría de todas las acciones se desactivarán</p> </td>
   <td><p>false</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Habilitar Leer auditoría</p> </td>
   <td><p>Habilitar/deshabilitar la funcionalidad de auditoría para lecturas de recursos</p> </td>
   <td><p>false</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Habilitar Crear auditoría</p> </td>
   <td><p>Habilitar/deshabilitar la funcionalidad de auditoría para la creación de recursos</p> </td>
   <td><p>false</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Habilitar auditoría de actualización</p> </td>
   <td><p>Habilitar/deshabilitar la funcionalidad de auditoría para la actualización de recursos</p> </td>
   <td><p>false</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Habilitar la auditoría de reversión</p> </td>
   <td><p>Habilitar/deshabilitar la funcionalidad de auditoría para la reversión de recursos</p> </td>
   <td><p>false</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Habilitar auditoría de publicación</p> </td>
   <td><p>Habilitar/deshabilitar la funcionalidad de auditoría para la publicación de recursos</p> </td>
   <td><p>false</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Habilitar auditoría Guardar como borrador</p> </td>
   <td><p>Habilitar/deshabilitar la funcionalidad de auditoría para guardar borradores de letras</p> </td>
   <td><p>false</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Habilitar auditoría de envío</p> </td>
   <td><p>Habilitar/deshabilitar la funcionalidad de auditoría para el envío de cartas</p> </td>
   <td><p>false</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Habilitar auditoría de correo electrónico</p> </td>
   <td><p>Habilitar/deshabilitar la funcionalidad de auditoría para enviar cartas por correo electrónico</p> </td>
   <td><p>false</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Habilitar auditoría de impresión</p> </td>
   <td><p>Habilitar/deshabilitar la funcionalidad de auditoría para imprimir letras</p> </td>
   <td><p>false</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Habilitar auditoría de entrega personalizada</p> </td>
   <td><p>Habilitar/deshabilitar la funcionalidad de auditoría para el envío personalizado de cartas</p> </td>
   <td><p>false</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Nombre del parámetro de documentos adjuntos</p> </td>
   <td><p>Nombre del parámetro para los documentos adjuntos enviados al proceso posterior</p> </td>
   <td><p>inAttachmentDocs</p> </td>
   <td><p>Cualquier nombre de variable de cadena</p> </td>
  </tr>
  <tr>
   <td><p>Raíz del usuario de CM</p> </td>
   <td><p>URL de la carpeta que contiene todos los recursos de usuario de la Gestión de correspondencia</p> </td>
   <td><p>—</p> </td>
   <td><p>Ubicación de carpeta válida</p> </td>
  </tr>
  <tr>
   <td><p>Tamaño de caché de carta</p> </td>
   <td><p>Especifique el número máximo de letras que se guardarán en la caché.</p> <p>Si se cambia este valor, se limpiará <code>in-memory</code> caché.</p> </td>
   <td><p>100</p> </td>
   <td><p>Cualquier valor numérico</p> </td>
  </tr>
  <tr>
   <td><p>Habilitar caché de letras</p> </td>
   <td><p>Habilitar/Deshabilitar la caché de letras.</p> <p>Si se cambia este valor, se limpiará <code>in-memory </code> caché.</p> </td>
   <td><p>true</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Solicitud de elementos de datos</p> </td>
   <td><p>Mantiene el orden de los elementos de datos en la interfaz de creación de correspondencia según su secuencia en Carta</p> </td>
   <td><p>true</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>Recarga de asistencia</p> </td>
   <td><p>Habilitar/Deshabilitar compatibilidad de recarga en letras representadas en el lado del servidor.</p> <p>Deshabilitar esto mejorará el rendimiento del procesamiento de letras.</p> </td>
   <td><p>false</p> </td>
   <td><p>true/false</p> <p> </p> </td>
  </tr>
  <tr>
   <td>Carpeta Temp</td>
   <td>Ubicación de la carpeta temporal.</td>
   <td>acm.tpmFolder</td>
   <td> </td>
  </tr>
  <tr>
   <td>Guardar remoto</td>
   <td>Guarda las instancias de carta en el autor de procesamiento especificado.</td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Opciones de compatibilidad</td>
   <td>Opciones de compatibilidad del formato configname:configvalue separadas por coma.</td>
   <td>acm.compatibilityOptions</td>
   <td> </td>
  </tr>
  <tr>
   <td><p>Directorio de depuración </p> <p> </p> </td>
   <td>Ubicación de la carpeta del sistema de archivos para la depuración. Si el directorio no <code>exists</code>, no se generarán volcados de depuración.</td>
   <td>acm.debugDirectory</td>
   <td> </td>
  </tr>
 </tbody>
</table>
