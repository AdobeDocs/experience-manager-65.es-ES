---
title: 'Línea de comandos: start y stop'
seo-title: 'Línea de comandos: start y stop'
description: Obtenga información sobre cómo realizar inicios y detener AEM desde la línea de comandos.
seo-description: Obtenga información sobre cómo realizar inicios y detener AEM desde la línea de comandos.
uuid: 585f071c-2286-4a2c-af07-404bf298cba8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 9333ff84-f624-4cfa-a9e4-c5e3882171ff
translation-type: tm+mt
source-git-commit: 3f53945579eaf5de1ed0b071aa9cce30dded89f1
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 4%

---


# Línea de comandos: start y stop{#command-line-start-and-stop}

## Inicio de Adobe Experience Manager desde la línea de comandos {#starting-adobe-experience-manager-from-the-command-line}

La secuencia de comandos `start` está disponible en *el directorio &lt;cq-installation>/bin*. Se proporcionan las versiones Unix y Windows. La secuencia de comandos inicio la instancia instalada en el directorio *&lt;cq-installation>*.

Estas dos versiones admiten una lista de variables de entorno que podrían utilizarse para realizar inicios y ajustar la instancia de AEM.

<table>
 <tbody>
  <tr>
   <td><strong>Variable de entorno </strong></td>
   <td><strong>Descripción </strong></td>
  </tr>
  <tr>
   <td>CQ_PORT</td>
   <td>Puerto TCP utilizado para secuencias de comandos de detención y estado<br /> </td>
  </tr>
  <tr>
   <td>CQ_HOST</td>
   <td>Nombre de host<br /> </td>
  </tr>
  <tr>
   <td>CQ_INTERFACE</td>
   <td>Interfaz que este servidor debe escuchar<br /> </td>
  </tr>
  <tr>
   <td>CQ_RMONUDE</td>
   <td>Los modos de ejecución separados por coma<br /> </td>
  </tr>
  <tr>
   <td>CQ_JARFILE</td>
   <td>Nombre del archivo de jerga<br /> </td>
  </tr>
  <tr>
   <td>CQ_USE_JAAS</td>
   <td>Uso de JAAS (si es true)<br /> </td>
  </tr>
  <tr>
   <td>CQ_JAAS_CONFIG</td>
   <td>Ruta de la configuración de JAAS<br /> </td>
  </tr>
  <tr>
   <td>CQ_JVM_OPTS</td>
   <td>Opciones de JVM predeterminadas<br /> </td>
  </tr>
 </tbody>
</table>

>[!CAUTION]
>
>Tenga en cuenta que algunos modos de ejecución, entre ellos la creación y la publicación, deben establecerse antes de iniciar la primera AEM y no pueden cambiarse posteriormente. Antes de configurar una instancia de AEM que se supone se debe utilizar en producción, consulte la [documentación de modos de ejecución](/help/sites-deploying/configure-runmodes.md) para obtener más detalles.

### Ejemplo de secuencia de comandos inicio.bat de la plataforma Windows {#windows-platform-start-bat-script-example}

```shell
SET CQ_PORT=1234 & ./start.bat
```

### Ejemplo de secuencia de comandos de inicio de la plataforma Unix {#unix-platform-start-script-example}

```shell
CQ_PORT=1234 ./start
```

>[!NOTE]
>
>La secuencia de comandos de inicio inicia el AEM Quickstart instalado en *la carpeta &lt;cq-installation>/app*.

## Deteniendo Adobe Experience Manager {#stopping-adobe-experience-manager}

Para detener AEM, realice una de las siguientes acciones:

* Según la plataforma que utilice:

   * Si ha empezado a AEM desde una secuencia de comandos o la línea de comandos, pulse **Ctrl+C** para apagar el servidor.
   * Si ha utilizado el script inicio en UNIX, debe utilizar el script stop para detener AEM.

* Si ha empezado a AEM haciendo clic con el doble en el archivo jar, haga clic en el botón **Activado** en la ventana de inicio (el botón luego cambia a **Desactivado**) para apagar el servidor.

   ![chlimage_1-63](assets/chlimage_1-63.png)

## Parada de Adobe Experience Manager desde la línea de comandos {#stopping-adobe-experience-manager-from-the-command-line}

La secuencia de comandos `stop` está disponible en *el directorio &lt;cq-installation>/bin*. Se proporcionan las versiones Unix y Windows. La secuencia de comandos detiene la instancia en ejecución instalada en el directorio *&lt;cq-installation>*.

### Ejemplo de secuencia de comandos de parada de plataforma Unix {#unix-platform-stop-script-example}

```shell
./stop
```

### Ejemplo de secuencia de comandos de la plataforma Windows stop.bat {#windows-platform-stop-bat-script-example}

```shell
./stop.bat
```

Si solo desea preconfigurar el repositorio (sin reubicarlo), sólo tiene que:

* extraer `repository.xml` a la ubicación requerida

* actualizar `repository.xml` según sea necesario

* crear `bootstrap.properties` y definir `repository.config`

De nuevo, antes de iniciar la instalación real.

