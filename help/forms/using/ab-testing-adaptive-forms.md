---
title: Crear y administrar una prueba A/B para formularios adaptables
seo-title: Crear y administrar una prueba A/B para formularios adaptables
description: AEM Forms se integra con Adobe Target, que permite ejecutar pruebas A/B para formularios adaptables para mejorar la experiencia del cliente y mejorar las tasas de conversión.
seo-description: AEM Forms se integra con Adobe Target, que permite ejecutar pruebas A/B para formularios adaptables para mejorar la experiencia del cliente y mejorar las tasas de conversión.
uuid: e258805c-4da8-4c5d-ae91-7bea78a6a71b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 8f776f30-ff93-4d19-94c6-c4bfe6f1fae2
docset: aem65
translation-type: tm+mt
source-git-commit: 3eaace94bc0499aaebfcd389d4dc97b97c7d9160
workflow-type: tm+mt
source-wordcount: '1581'
ht-degree: 0%

---


# Crear y administrar pruebas A/B para formularios adaptables{#create-and-manage-a-b-test-for-adaptive-forms}

## Información general {#overview-br}

Es probable que sus clientes abandonen un formulario si la experiencia que ofrece no es atractiva. Aunque resulta frustrante para los clientes, también puede aumentar el volumen de asistencia y el costo de su organización. Es fundamental, además de todo un desafío, identificar y proporcionar la experiencia adecuada del cliente que aumenta la tasa de conversión. Adobe Experience Manager Forms tiene la clave para este problema.

AEM Forms se integra con Adobe Target, una solución de Adobe Marketing Cloud, para ofrecer experiencias personalizadas y atractivas a los clientes en varios canales digitales. Una de las funciones clave de Destinatario es la prueba A/B que le permite configurar rápidamente pruebas A/B simultáneas, presentar contenido relevante a los usuarios objetivo e identificar la experiencia que conduce a una mejor tasa de conversión.

Con AEM Forms, puede configurar y ejecutar pruebas A/B en formularios adaptables en tiempo real. También ofrece funciones de sistema de informes integradas y personalizables para visualizar el rendimiento en tiempo real de las experiencias de formulario e identificar la que maximiza la participación y conversión del usuario.

## Configurar e integrar Destinatario en AEM Forms {#set-up-and-integrate-target-in-aem-forms}

Antes de empezar a crear y analizar pruebas A/B para formularios adaptables, debe configurar el servidor de Destinatario e integrarlo en AEM Forms.

### Configurar Destinatario {#set-up-target}

Para integrar AEM con Destinatario, asegúrese de tener una cuenta de Adobe Target válida. Cuando se registra en Adobe Target, recibe un código de cliente. Necesita el código de cliente, el correo electrónico asociado con la cuenta de Destinatario y la contraseña para conectarse a AEM con Destinatario.

El código de cliente identifica la cuenta de cliente de Adobe Target y se utiliza como subdominio en la dirección URL al llamar al servidor de Adobe Target. Antes de continuar, asegúrese de que sus credenciales le permiten iniciar sesión en [https://testandtarget.omniture.com/](https://testandtarget.omniture.com/).

### Integrar Destinatario en AEM Forms {#integrate-target-in-aem-forms}

Realice los siguientes pasos para integrar un servidor Destinatario en ejecución con AEM Forms:

1. En AEM servidor, vaya a https://&lt;*hostname*>:&lt;*port*>/libs/cq/core/content/tools/cloudservices.html.

1. En la sección **Adobe Target**, haga clic en **Mostrar configuraciones** y luego en el icono **+** para agregar una nueva configuración.
Si está configurando destinatario por primera vez, haga clic en **Configurar ahora.**

1. En el cuadro de diálogo Crear configuración, especifique un **Título** y, opcionalmente, un **Nombre** para la configuración.

1. Haga clic en **Crear**. Se abre el cuadro de diálogo Editar componente.
1. Especifique los detalles de la cuenta de Destinatario, como código de cliente, correo electrónico y contraseña.
1. Seleccione **Rest** en la lista desplegable Tipo de API.

1. Haga clic en **Conectar a Adobe Target** para inicializar la conexión con Destinatario. Si la conexión se realiza correctamente, se muestra el mensaje Conexión correcta. Haga clic en **Aceptar** en el mensaje y, a continuación, **Aceptar** en el cuadro de diálogo. La cuenta de Destinatario está configurada.

1. Cree una estructura de Destinatario como se describe en [Añada una estructura](/help/sites-administering/target.md).

1. Vaya a https://&lt;*hostname*:&lt;*port*>/system/console/configMgr.

1. Haga clic en **Configuración de Destinatario de AEM Forms**.
1. Seleccione un **Destinatario Framework**.
1. En el campo **URL de Destinatario**, especifique todas las direcciones URL donde se ejecutarán las pruebas A/B. Por ejemplo, https://&lt;*hostname*>:&lt;*port*>/ para el servidor de AEM Forms en OSGi o https://&lt;*hostname*>:&lt;*port*>/lc/ para el servidor de AEM Forms en JEE.
Tenga en cuenta que desea configurar una URL de Destinatario para una instancia de publicación y que sus clientes pueden acceder a ella mediante el nombre de host o la dirección IP. Deberá configurarla como URL de Destinatario, utilizando el nombre de host y la dirección IP. Si configura solo una de las direcciones URL, la prueba A/B no se ejecutará para los clientes que provengan de la otra dirección URL. Haga clic en **+** para especificar varias direcciones URL.

1. Haga clic en **Guardar**.

El servidor Destinatario está integrado con AEM Forms. Ahora puede activar la prueba A/B si dispone de una licencia completa para utilizar Adobe Target.

Si dispone de una licencia completa para utilizar Adobe Target, inicio el servidor con los siguientes parámetros después de integrar Destinatario con AEM Forms:

`parameter -Dabtesting.enabled=true java -Xmx2048m -XX:MaxPermSize=512M -jar -Dabtesting.enabled=true`

Si la instancia de AEM se está ejecutando en JBoss, iniciada como un servicio de llave en mano, en el archivo `jboss\bin\standalone.conf.bat`, agregue el parámetro -Dabtesting.enabled=true en la siguiente entrada:

`set "JAVA_OPTS=%JAVA_OPTS% -Dadobeidp.serverName=server1 -Dfile.encoding=utf8 -Djava.net.preferIPv4Stack=true -Dabtesting.enabled=true"`

Además del servidor jSC, puede agregar el argumento -Dabtesting.enabled=true jvm en la secuencia de comandos de inicio del servidor para cualquier servidor de aplicaciones. Ahora puede crear y ejecutar pruebas A/B para formularios adaptables.

>[!NOTE]
>
>Si actualiza las direcciones URL de Destinatario configuradas más adelante, asegúrese de actualizar todas las pruebas A/B en ejecución para que apunten a las direcciones URL actuales. Para obtener información sobre la actualización de pruebas A/B, consulte [Actualización de la prueba A/B](/help/forms/using/ab-testing-adaptive-forms.md#p-update-a-b-test-p).


## Crear audiencias dentro de AEM {#create-audiences-within-aem}

AEM le permite crear una audiencia y utilizarla para una prueba A/B. La audiencia que cree dentro de AEM está disponible en AEM Forms. Siga estos pasos para crear audiencias dentro de AEM:

1. En la instancia de creación, toque **Adobe Experience Manager** > **Personalización** > **Audiencias**.

1. En la página Audiencias, toque **Crear Audiencia > Crear Audiencia de Destinatario**.
1. En el cuadro de diálogo Configuración de Adobe Target, seleccione una configuración de Destinatario y haga clic en **Aceptar**.
1. En la página Crear nueva Audiencia, cree reglas. Las reglas permiten categorizar la audiencia. Por ejemplo, desea categorizar las audiencias en función del sistema operativo. Su audiencia A viene de Windows, y la audiencia B viene de Linux.

   1. Para categorizar la audiencia en función de Windows, en la regla 1, seleccione el tipo de atributo **OS**. En la lista desplegable Cuándo, seleccione **Windows.**

   1. Para categorizar la audiencia en función de Linux, en la regla 2, seleccione el tipo de atributo **OS**. En la lista desplegable **Cuándo**, seleccione **Linux** y haga clic en **Siguiente**.

1. Especifique un nombre para la audiencia creada y haga clic en **Guardar**.

Puede seleccionar la audiencia al configurar la prueba A/B para un formulario, como se muestra a continuación.

## Crear prueba A/B {#create-a-b-test}

Realice los pasos siguientes para crear una prueba A/B para un formulario adaptable.

1. Vaya a **Forms &amp; Documentos** en https://&lt;*hostname*>:&lt;*port*>/aem/forms.html/content/dam/formsanddocuments.

1. Vaya a la carpeta que contiene el formulario adaptable.
1. Haga clic en la herramienta **Seleccionar** en la barra de herramientas y seleccione el formulario adaptable.
1. Haga clic en **Más** en la barra de herramientas y seleccione **Configurar la prueba A/B**. Se abre la página Configurar pruebas A/B.

[ ![Página de configuración de la prueba A/B para formularios adaptables](assets/ab-test-configure.png)](assets/ab-test-configure-1.png)

1. Especifique un **nombre de Actividad** para la prueba A/B.

1. En la lista desplegable Audiencia, seleccione una audiencia a la que desee ofrecer distintas experiencias del formulario. Por ejemplo, **Visitantes que utilizan Chrome**. La lista de audiencia se rellena desde el servidor de Destinatario configurado.

1. En los campos **Distribución de experiencias** de las experiencias A y B, especifique la distribución, en términos de porcentaje, para determinar la distribución de experiencias entre la audiencia total. Por ejemplo, si especifica 40, 60 para las experiencias A y B, respectivamente, la experiencia A se ofrecerá al 40 % de la audiencia y el 60 % restante verá la experiencia B.
1. Haga clic en **Configurar**. Aparece un cuadro de diálogo para confirmar la creación de la prueba A/B.
1. Haga clic en **Editar experiencia B** para abrir el formulario adaptable en el modo de edición. Modifique el formulario para crear una experiencia distinta a la experiencia A predeterminada. Las posibles variaciones permitidas en la Experiencia B son los cambios en:

   * CSS o estilo
   * Orden de los campos en diferentes paneles o en el mismo panel
   * Diseño de panel
   * Títulos del panel
   * Descripción, etiqueta y texto de ayuda de un campo
   * Secuencias de comandos que no afectan o rompen el flujo de envío
   * Validaciones (tanto del cliente como del servidor)
   * Tema de la experiencia B. (Puede seleccionar un tema alternativo para la experiencia B)

1. Vaya a la interfaz de usuario de Forms y Documentos, seleccione el formulario adaptable, haga clic en **Más** y seleccione **Prueba A/B de Inicio**.

La prueba A/B se está ejecutando y la audiencia especificada se ofrecerá aleatoriamente a las experiencias en función de la distribución especificada.

## Actualizar la prueba A/B {#update-a-b-test}

Puede actualizar las distribuciones de audiencia y experiencia de una prueba A/B en ejecución. Para ello:

1. En la interfaz de usuario de Forms y Documentos, navegue a la carpeta que contenga el formulario adaptable en el que se está ejecutando la prueba A/B.
1. Seleccione el formulario adaptable.
1. Haga clic en **Más** y, a continuación, seleccione **Editar prueba A/B**. Se abre la página de prueba A/B de actualización.

1. Actualice las distribuciones de audiencia y experiencia según sea necesario.
1. Haga clic en **Actualizar**.

## Vista y análisis del informe de prueba A/B {#view-and-analyze-a-b-test-report}

Una vez que haya permitido que la prueba A/B se ejecute durante el período deseado, puede generar un informe y comprobar qué experiencia ha resultado en una mejor conversión. Puede declarar una experiencia de mejor rendimiento como ganadora o elegir ejecutar otra prueba A/B. Para ello, lleve a cabo los siguientes pasos:

1. Seleccione el formulario adaptable, haga clic en **Más** y, a continuación, haga clic en **Informe de prueba A/B**. Se muestra el informe.

[ ![Informe de prueba A/B](assets/ab-test-report-2.png)](assets/ab-test-report-3.png)

1. Analice el informe y compruebe si tiene suficientes puntos de datos para declarar como ganadoras una de las experiencias con mejor rendimiento. Puede elegir continuar con la misma prueba A/B durante más tiempo o declarar un ganador y finalizar la prueba A/B.
1. Para declarar un ganador y finalizar la prueba A/B, haga clic en el botón **Finalizar prueba A/B** del panel de sistema de informes. Un cuadro de diálogo le solicita que declare una de las dos experiencias como ganadora. Seleccione un ganador y confirme que desea finalizar la prueba A/B.
Como alternativa, puede declarar un ganador primero haciendo clic en el botón **Declarar ganador** para la experiencia correspondiente. Le solicita que confirme el ganador. Haga clic en **Sí** para finalizar la prueba A/B.

Si eligió la experiencia A como ganadora, la prueba A/B finalizará y, a partir de ahora, solo se ofrecerá la experiencia A a todas las audiencias.
