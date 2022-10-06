---
title: 'Línea de comandos: start y stop'
seo-title: Command Line Start and Stop
description: Aprenda a iniciar y detener AEM desde la línea de comandos.
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

## Inicio de Adobe Experience Manager desde la línea de comandos {#starting-adobe-experience-manager-from-the-command-line}

La variable `start` la secuencia de comandos está disponible en *el &lt;cq-installation>/bin* directorio. Se proporcionan las versiones Unix y Windows. La secuencia de comandos inicia la instancia instalada en *&lt;cq-installation>* directorio.

Estas dos versiones admiten una lista de variables de entorno que podrían utilizarse para iniciar y ajustar la instancia de AEM.

<table>
 <tbody>
  <tr>
   <td><strong>Variable de entorno </strong></td>
   <td><strong>Descripción </strong></td>
  </tr>
  <tr>
   <td>CQ_PORT</td>
   <td>Puerto TCP usado para scripts de detención y estado<br /> </td>
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
   <td>CQ_RUNMODE</td>
   <td>Modo de ejecución separado por coma<br /> </td>
  </tr>
  <tr>
   <td>CQ_JARFILE</td>
   <td>Nombre del archivo de jerga<br /> </td>
  </tr>
  <tr>
   <td>CQ_USE_JAAS</td>
   <td>Uso de JAAS (si es verdadero)<br /> </td>
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
>Tenga en cuenta que algunos modos de ejecución, entre ellos el de autor y publicación, deben configurarse antes del primer inicio AEM y no se pueden cambiar posteriormente. Antes de configurar una instancia de AEM que se supone que debe utilizarse en la producción, consulte la [documentación de modos de ejecución](/help/sites-deploying/configure-runmodes.md) para obtener más información.

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
>La secuencia de comandos de inicio inicia el AEM Quickstart instalado en *el &lt;cq-installation>/app* carpeta.

## Detención de Adobe Experience Manager {#stopping-adobe-experience-manager}

Para detener AEM, realice una de las siguientes acciones:

* Según la plataforma que utilice:

   * Si ha empezado a AEM desde una secuencia de comandos o la línea de comandos, pulse **Ctrl + C** para apagar el servidor.
   * Si ha utilizado el script de inicio en UNIX, debe utilizar el script de parada para detener AEM.

* Si ha empezado a AEM haciendo doble clic en el archivo jar, haga clic en el botón **Activado** en la ventana de inicio (el botón luego cambia a **Off**) para apagar el servidor.

   ![imagen_1-63](assets/chlimage_1-63.png)

## Detención de Adobe Experience Manager desde la línea de comandos {#stopping-adobe-experience-manager-from-the-command-line}

La variable `stop` la secuencia de comandos está disponible en *el &lt;cq-installation>/bin* directorio. Se proporcionan las versiones Unix y Windows. La secuencia de comandos detiene la instancia en ejecución instalada en *&lt;cq-installation>* directorio.

### Ejemplo de script de parada de plataforma Unix {#unix-platform-stop-script-example}

```shell
./stop
```

### Ejemplo de script de Windows platform stop.bat {#windows-platform-stop-bat-script-example}

```shell
./stop.bat
```

Si solo desea preconfigurar el repositorio (sin reubicarlo), solo tiene que:

* extracción `repository.xml` a la ubicación requerida

* actualizar `repository.xml` según se requiera

* crear `bootstrap.properties` y definir `repository.config`

De nuevo, antes de iniciar la instalación real.
