---
title: 'Línea de comandos: start y stop'
seo-title: 'Línea de comandos: start y stop'
description: Obtenga información sobre cómo iniciar y detener AEM desde la línea de comandos.
seo-description: Obtenga información sobre cómo iniciar y detener AEM desde la línea de comandos.
uuid: 585f071c-2286-4a2c-af07-404bf298cba8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 9333ff84-f624-4cfa-a9e4-c5e3882171ff
translation-type: tm+mt
source-git-commit: 3f53945579eaf5de1ed0b071aa9cce30dded89f1

---


# Línea de comandos: start y stop{#command-line-start-and-stop}

## Inicio de Adobe Experience Manager desde la línea de comandos {#starting-adobe-experience-manager-from-the-command-line}

La `start` secuencia de comandos está disponible en *el directorio &lt;cq-installation>/bin* . Se proporcionan las versiones Unix y Windows. La secuencia de comandos inicia la instancia instalada en el directorio *&lt;cq-installation>* .

Estas dos versiones admiten una lista de variables de entorno que podrían utilizarse para iniciar y ajustar la instancia de AEM.

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
   <td>Nombre del host<br /> </td>
  </tr>
  <tr>
   <td>CQ_INTERFACE</td>
   <td>Interfaz que este servidor debe escuchar<br /> </td>
  </tr>
  <tr>
   <td>CQ_RMONUDE</td>
   <td>Modo(s) de ejecución separado por coma<br /> </td>
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
>Tenga en cuenta que algunos modos de ejecución, entre ellos la creación y publicación, deben establecerse antes de iniciar AEM por primera vez y no pueden cambiarse posteriormente. Antes de configurar una instancia de AEM que se supone se va a utilizar en producción, consulte la documentación [de modos de](/help/sites-deploying/configure-runmodes.md) ejecución para obtener más información.

### Ejemplo de secuencia de comandos start.bat de la plataforma Windows {#windows-platform-start-bat-script-example}

```shell
SET CQ_PORT=1234 & ./start.bat
```

### Ejemplo de secuencia de comandos de inicio de plataforma Unix {#unix-platform-start-script-example}

```shell
CQ_PORT=1234 ./start
```

>[!NOTE]
>
>La secuencia de comandos de inicio inicia AEM Quickstart instalado en *la carpeta &lt;cq-installation>/app* .

## Stopping Adobe Experience Manager {#stopping-adobe-experience-manager}

Para detener AEM, realice una de las siguientes acciones:

* Según la plataforma que utilice:

   * Si ha iniciado AEM desde un script o desde la línea de comandos, pulse **Ctrl+C** para cerrar el servidor.
   * Si ha utilizado la secuencia de comandos start en UNIX, debe utilizar la secuencia de comandos stop para detener AEM.

* Si ha iniciado AEM haciendo doble clic en el archivo jar, haga clic en el botón **Activado** de la ventana de inicio (el botón cambia a **Desactivado**) para apagar el servidor.

   ![chlimage_1-63](assets/chlimage_1-63.png)

## Parada de Adobe Experience Manager desde la línea de comandos {#stopping-adobe-experience-manager-from-the-command-line}

La `stop` secuencia de comandos está disponible en *el directorio &lt;cq-installation>/bin* . Se proporcionan las versiones Unix y Windows. La secuencia de comandos detiene la instancia en ejecución instalada en el directorio *&lt;cq-installation>* .

### Ejemplo de secuencia de comandos de parada de plataforma Unix {#unix-platform-stop-script-example}

```shell
./stop
```

### Ejemplo de secuencia de comandos de la plataforma Windows stop.bat {#windows-platform-stop-bat-script-example}

```shell
./stop.bat
```

Si solo desea preconfigurar el repositorio (sin reubicarlo), sólo tiene que:

* extract `repository.xml` to the required location

* actualizar `repository.xml` según sea necesario

* crear `bootstrap.properties` y definir `repository.config`

De nuevo, antes de iniciar la instalación real.

