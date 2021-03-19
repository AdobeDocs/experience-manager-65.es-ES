---
title: Habilitar el registro para formularios HTML5
seo-title: Habilitar el registro para formularios HTML5
description: La utilidad logger habilita el registro de un formulario y le ayuda a depurar problemas relacionados con el formulario.
seo-description: La utilidad logger habilita el registro de un formulario y le ayuda a depurar problemas relacionados con el formulario.
uuid: 322306ba-8ad7-463d-8a9d-4cea5a0c4b55
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 973806f8-fb44-4d52-ad3f-bfbf335f60a1
docset: aem65
feature: Mobile Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 6%

---


# Habilitar el registro para formularios HTML5{#enable-logging-for-html-forms}

Puede configurar la utilidad del registrador para empezar a crear registros para formularios HTML5. La utilidad del registrador tiene varios niveles, puede establecer un nivel según sus necesidades. Los formularios HTML5 tienen componentes de servidor y cliente. Puede configurar los registros de ambos componentes.

## Configuración del registro del lado del servidor {#configuring-server-side-logging}

Siga estos pasos para configurar los registros del lado del servidor:

1. Ir a `https://'[server]:[port]'/system/console/configMgr`. Busque y abra la opción *Apace Sling logging logger configuration*. Aparecerá un cuadro de diálogo:

   ![ Cuadro de diálogo de la opción de configuración del registrador de registros de Sling](assets/logconfig.png)

   Opción de configuración del registrador de registros de Sling

1. Cambie **Nivel de registro** a **Depurar**.

1. Especifique el nombre y la ruta del **Archivo de registro**.

   >[!NOTE]
   >
   >Para generar registros en el directorio de registro de formularios HTML5, agregue ../logs/ antes del nombre de archivo.

1. Cambie **Logger** por **HTMLFormsPerfLogger**. Haga clic en **Guardar**.

## Configuración del registro de cliente {#configuring-client-logging}

Puede utilizar los siguientes métodos para habilitar el registro en el lado del cliente en formularios HTML5:

* Uso del parámetro de solicitud denominado `log`
* Uso de CQ Configuration Manager

### Habilitación del registro mediante el parámetro de solicitud {#enabling-logging-using-request-parameter}

Con este método, puede generar registros para una solicitud en particular. El nombre del parámetro de solicitud es `log. La URL de registro es la siguiente:

`https://<server>:<port>/content/xfaforms/profiles/test.html?contentRoot=<path of the folder containing form xdp>&template=<name of the xdp>&log=<log configuration>.`

La configuración de registro está formada por el nivel de registro y la categoría del registrador.

#### Destino de registro {#log-destination}

<table>
 <tbody>
  <tr>
   <th><strong>Destino del registro</strong></th>
   <th><strong>Descripción</strong></th>
  </tr>
  <tr>
   <td>1</td>
   <td>Los registros se dirigen al explorador <strong>Console</strong></td>
  </tr>
  <tr>
   <td>2</td>
   <td>Los registros se recopilan en un objeto JavaScript del lado del cliente y se pueden publicar en <strong>Server</strong> </td>
  </tr>
  <tr>
   <td>3</td>
   <td>Ambas opciones anteriores<br /> </td>
  </tr>
 </tbody>
</table>

#### Niveles de registro {#log-levels}

<table>
 <tbody>
  <tr>
   <th>Nivel de registro</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td>0</td>
   <td>DESACTIVADO<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>3</td>
   <td>FATAL<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>2</td>
   <td>ERROR<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>1</td>
   <td>AVISAR<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>4</td>
   <td>INFORMACIÓN<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>5</td>
   <td>DEPURACIONES<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>6</td>
   <td>TRACE<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>7</td>
   <td>TODO<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

#### Categorías de registrador {#logger-categories}

<table>
 <tbody>
  <tr>
   <th>Categoría de registro</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td>una</td>
   <td>xfa (registros relacionados con el motor de secuencias de comandos)</td>
  </tr>
  <tr>
   <td>b</td>
   <td>xfaView (registros relacionados con el motor de diseño)<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>c</td>
   <td>xfaPerf (registros relacionados con el rendimiento)<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

#### Configuración de registro {#log-configuration}

En la URL del registro, el parámetro de cadena de consulta de configuración del registro se define de la siguiente manera:

`{destination}-{a level}-{b level}-{c level}`

Por ejemplo:

<table>
 <tbody>
  <tr>
   <th>Configuración de registro</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td>2-a4-b5-c6<br type="_moz" /> </td>
   <td>Destino: Nivel xfa del servidor<br />: INFO<br /> xfaView level: Nivel DEBUG<br /> xfaPerf: TRACE</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>El nivel de registro predeterminado para cada categoría de registro a (xfa), b (xfaView) y c (xfaPerf) es 2 (ERROR). Por lo tanto, para la configuración de registros: 2-b6, los niveles de registro para diferentes categorías son:
>a xfa): 2 (nivel predeterminado ERROR)
>b (xfaView): 6 (TRACE especificado por el usuario)
>a (xfaPerf): 2 (nivel predeterminado ERROR)

### Habilitación del registro mediante Configuration Manager {#enabling-logging-using-configuration-manager}

Si utiliza Configuration Manager para habilitar el registro, se generan registros para cada solicitud de procesamiento hasta que se desactive de nuevo el registro.

1. Inicie sesión en CQ Configuration Manager en `https://'[server]:[port]'/system/console/configMgr` e inicie sesión con credenciales de administrador.
1. Busque y haga clic en **Configuraciones móviles de Forms**.
1. En el cuadro de texto Opciones de depuración , introduzca las configuraciones de registro como se describe en la sección anterior, por ejemplo, **2-a4-b5-c6**

   ![Configuración de formularios](assets/forms_configuration.png)

   Configuración de formularios

## Carga de registros {#uploading-logs}

Si el destino se establece como 1, todos los mensajes de registro de scripts de cliente se dirigen a la consola. Si un administrador requiere estos registros junto con los registros del servidor, establezca el nivel de destino en 2. En este nivel, todos los registros se recopilan en un objeto JS del lado del cliente y si el formulario se procesa con el perfil predeterminado, aparece un botón **Send Logs** a la izquierda del botón **Highlight Existing Fields** en la barra de herramientas. Cuando el usuario hace clic en el vínculo, todos los registros recopilados se publican en el servidor y se registran en el archivo de registro de errores configurado en el servidor.

De forma predeterminada, toda la información se agrega al archivo error.log en el directorio /crx-repository/logs/ .

Para cambiar la ubicación y el nombre del archivo de registro:

1. Inicie sesión en Configuration Manager como administrador. La dirección URL predeterminada de Configuration Manager es `https://'[server]:[port]'/system/console/configMgr`.
1. Haga clic en **Configuración del registrador de Apache Sling**. Aparecerá un cuadro de diálogo.

   ![logconfig-1](assets/logconfig-1.png)

1. Cambie **Log Level** a Debug.

1. Especifique la ruta y el nombre del **Archivo de registro**.

   >[!NOTE]
   >
   >Para crear registros en el mismo directorio donde se guardan otros archivos de registro, especifique ../logs/&lt;filename> en la propiedad Archivos de registro.

1. Cambie **Logger** a **HTMLFormsPerfLogger** y haga clic en **Guardar**.
