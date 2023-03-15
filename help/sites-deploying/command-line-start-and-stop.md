---
title: 'Línea de comandos: start y stop'
seo-title: Command Line Start and Stop
description: AEM Obtenga información sobre cómo iniciar y detener el inicio de la línea de comandos desde la línea de comandos.
seo-description: Learn how to start and stop AEM from the command line.
uuid: 585f071c-2286-4a2c-af07-404bf298cba8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 9333ff84-f624-4cfa-a9e4-c5e3882171ff
exl-id: 21041b55-240c-487d-9d79-c54c877f4e1e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 3%

---

# Línea de comandos: start y stop{#command-line-start-and-stop}

## Iniciar Adobe Experience Manager desde la línea de comandos {#starting-adobe-experience-manager-from-the-command-line}

El `start` El script está disponible en *el &lt;cq-installation>/bin* directorio. Se proporcionan las versiones Unix y Windows. La secuencia de comandos inicia la instancia instalada en *&lt;cq-installation>* directorio.

AEM Estas dos versiones admiten una lista de variables de entorno que se pueden usar para iniciar y ajustar la instancia de.

<table>
 <tbody>
  <tr>
   <td><strong>Variable de entorno </strong></td>
   <td><strong>Descripción </strong></td>
  </tr>
  <tr>
   <td>CQ_PORT</td>
   <td>Puerto TCP utilizado para secuencias de comandos de estado y detención<br /> </td>
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
   <td>CQ_RUNMODE</td>
   <td>Modo(s) de ejecución separado(s) por coma<br /> </td>
  </tr>
  <tr>
   <td>CQ_JARFILE</td>
   <td>Nombre del archivo jar<br /> </td>
  </tr>
  <tr>
   <td>CQ_USE_JAS</td>
   <td>Uso de JAAS (si es verdadero)<br /> </td>
  </tr>
  <tr>
   <td>CQ_JAS_CONFIG</td>
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
>AEM Tenga en cuenta que algunos modos de ejecución, entre los que se incluyen Autor y Publicación, deben configurarse antes de comenzar la primera ejecución y no se pueden cambiar posteriormente. AEM Antes de configurar una instancia de que se supone que debe utilizarse en producción, consulte la [documentación sobre los modos de ejecución](/help/sites-deploying/configure-runmodes.md) para obtener más información.

### Ejemplo de script start.bat de la plataforma Windows {#windows-platform-start-bat-script-example}

```shell
SET CQ_PORT=1234 & ./start.bat
```

### Ejemplo de script de inicio de plataforma Unix {#unix-platform-start-script-example}

```shell
CQ_PORT=1234 ./start
```

>[!NOTE]
>
>AEM La secuencia de comandos de inicio inicia el inicio rápido de la aplicación instalado en *el &lt;cq-installation>/app* carpeta.

## Detención de Adobe Experience Manager {#stopping-adobe-experience-manager}

AEM Para detener la, siga uno de estos procedimientos:

* Según la plataforma que utilice:

   * AEM Si ha empezado a utilizar el comando desde una secuencia de comandos o desde la línea de comandos, pulse **Ctrl + C** para apagar el servidor.
   * AEM Si ha utilizado la secuencia de comandos de inicio en UNIX, debe utilizar la secuencia de comandos de parada para detener la ejecución de la secuencia de comandos de inicio de la secuencia de comandos de.

* AEM Si ha empezado a hacer clic en el archivo jar, haga clic en el botón de la barra de herramientas. **Activado** en la ventana de inicio (el botón cambia a **Desactivado**) para apagar el servidor.

   ![chlimage_1-63](assets/chlimage_1-63.png)

## Detención de Adobe Experience Manager desde la línea de comandos {#stopping-adobe-experience-manager-from-the-command-line}

El `stop` El script está disponible en *el &lt;cq-installation>/bin* directorio. Se proporcionan las versiones Unix y Windows. El script detiene la instancia en ejecución instalada en *&lt;cq-installation>* directorio.

### Ejemplo de script de detención de plataforma Unix {#unix-platform-stop-script-example}

```shell
./stop
```

### Ejemplo de script stop.bat de la plataforma Windows {#windows-platform-stop-bat-script-example}

```shell
./stop.bat
```

Si solo desea preconfigurar el repositorio (sin reubicarlo), solo tiene que:

* extracción `repository.xml` a la ubicación requerida

* actualizar `repository.xml` según sea necesario

* crear `bootstrap.properties` y definir `repository.config`

De nuevo, antes de iniciar la instalación real.
