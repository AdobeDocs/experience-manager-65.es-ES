---
title: Crear y administrar una prueba A/B para formularios adaptables
seo-title: Crear y administrar una prueba A/B para formularios adaptables
description: AEM Forms se integra con Adobe Target, que permite ejecutar pruebas A/B para formularios adaptables para mejorar la experiencia del cliente y las tasas de conversión.
seo-description: AEM Forms se integra con Adobe Target, que permite ejecutar pruebas A/B para formularios adaptables para mejorar la experiencia del cliente y las tasas de conversión.
uuid: e258805c-4da8-4c5d-ae91-7bea78a6a71b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 8f776f30-ff93-4d19-94c6-c4bfe6f1fae2
docset: aem65
translation-type: tm+mt
source-git-commit: 3eaace94bc0499aaebfcd389d4dc97b97c7d9160

---


# Crear y administrar una prueba A/B para formularios adaptables{#create-and-manage-a-b-test-for-adaptive-forms}

## Información general {#overview-br}

Es probable que sus clientes abandonen un formulario si la experiencia que ofrece no es atractiva. Aunque resulta frustrante para los clientes, también puede aumentar el volumen de asistencia y el costo de su organización. Es fundamental, al mismo tiempo que resulta difícil identificar y proporcionar la experiencia adecuada del cliente que aumenta la tasa de conversión. Adobe Experience Manager Forms es la clave para este problema.

AEM Forms se integra con Adobe Target, una solución de Adobe Marketing Cloud, para ofrecer experiencias de cliente personalizadas y atractivas en varios canales digitales. Una de las funciones clave de Target es la prueba A/B, que le permite configurar rápidamente pruebas A/B simultáneas, presentar contenido relevante a los usuarios objetivo e identificar la experiencia que impulsa una mejor tasa de conversión.

Con AEM Forms, puede configurar y ejecutar pruebas A/B en formularios adaptables en tiempo real. También proporciona funciones de informes integradas y personalizables para visualizar el rendimiento en tiempo real de las experiencias de formulario e identificar la que maximiza la participación y conversión del usuario.

## Configuración e integración de Target en AEM Forms {#set-up-and-integrate-target-in-aem-forms}

Antes de empezar a crear y analizar pruebas A/B para formularios adaptables, debe configurar el servidor de Target e integrarlo en AEM Forms.

### Configurar Target {#set-up-target}

Para integrar AEM con Target, asegúrese de que tiene una cuenta válida de Adobe Target. Al registrarse en Adobe Target, recibe un código de cliente. Necesita el código de cliente, el correo electrónico asociado a la cuenta de Target y la contraseña para conectar AEM con Target.

El código de cliente identifica la cuenta de cliente de Adobe Target y se utiliza como subdominio en la dirección URL al llamar al servidor de Adobe Target. Antes de continuar, asegúrese de que sus credenciales le permiten iniciar sesión en [https://testandtarget.omniture.com/](https://testandtarget.omniture.com/).

### Integración de Target en AEM Forms {#integrate-target-in-aem-forms}

Siga estos pasos para integrar un servidor de Target en ejecución con AEM Forms:

1. En el servidor AEM, vaya a https://&lt;*hostname*>:&lt;*port*>/libs/cq/core/content/tools/cloudservices.html.

1. En la sección **Adobe Target** , haga clic en **Mostrar configuraciones** y, a continuación, en el icono **+** para agregar una nueva configuración.
Si está configurando target por primera vez, haga clic en **Configurar ahora.**

1. En el cuadro de diálogo Crear configuración, especifique un **Título** y, opcionalmente, un **Nombre** para la configuración.

1. Haga clic en **Crear**. Se abre el cuadro de diálogo Editar componente.
1. Especifique los detalles de la cuenta de Target, como código de cliente, correo electrónico y contraseña.
1. Seleccione **Resto** en la lista desplegable Tipo de API.

1. Haga clic en **Conectar con Adobe Target** para inicializar la conexión con Target. Si la conexión se realiza correctamente, se muestra el mensaje Conexión correcta. Haga clic en **Aceptar** en el mensaje y, a continuación, en **Aceptar** en el cuadro de diálogo. La cuenta de Target está configurada.

1. Cree un marco de Target como se describe en [Agregar un marco](/help/sites-administering/target.md).

1. Vaya a https://&lt;*hostname*>:&lt;*port*>/system/console/configMgr.

1. Haga clic en Configuración **de destino de** AEM Forms.
1. Seleccione un **Target Framework**.
1. En el campo Direcciones URL **de Target** , especifique todas las direcciones URL donde se ejecutarán las pruebas A/B. Por ejemplo, https://&lt;*hostname*>:&lt;*port*>/ para el servidor de AEM Forms en OSGi o https://&lt;*hostname*>:&lt;*port*>/lc/ para el servidor de AEM Forms en JEE.
Considere que desea configurar una URL de Target para una instancia de publicación y que sus clientes pueden acceder a ella mediante el nombre de host o la dirección IP. Deberá configurar ambas como direcciones URL de Target, utilizando el nombre de host y la dirección IP. Si configura solo una de las direcciones URL, la prueba A/B no se ejecutará para los clientes que provengan de la otra dirección URL. Haga clic **+** para especificar varias direcciones URL.

1. Haga clic en **Guardar**.

El servidor de Target está integrado con AEM Forms. Ahora puede activar la prueba A/B si dispone de una licencia completa para utilizar Adobe Target.

Si dispone de una licencia completa para utilizar Adobe Target, inicie el servidor con los siguientes parámetros después de integrar Target con AEM Forms:

`parameter -Dabtesting.enabled=true java -Xmx2048m -XX:MaxPermSize=512M -jar -Dabtesting.enabled=true`

Si la instancia de AEM se está ejecutando en JBoss, iniciada como un servicio de llave en mano, en el `jboss\bin\standalone.conf.bat` archivo, agregue el parámetro -Dabtesting.enabled=true en la siguiente entrada:

`set "JAVA_OPTS=%JAVA_OPTS% -Dadobeidp.serverName=server1 -Dfile.encoding=utf8 -Djava.net.preferIPv4Stack=true -Dabtesting.enabled=true"`

Además del servidor jSC, puede agregar el argumento -Dabtesting.enabled=true jvm en la secuencia de comandos de inicio del servidor para cualquier servidor de aplicaciones. Ahora puede crear y ejecutar pruebas A/B para formularios adaptables.

>[!NOTE]
>
>Si actualiza las direcciones URL de Target configuradas más adelante, asegúrese de actualizar todas las pruebas A/B en ejecución para que apunten a las direcciones URL actuales. Para obtener información sobre la actualización de pruebas A/B, consulte [Actualización de la prueba](/help/forms/using/ab-testing-adaptive-forms.md#p-update-a-b-test-p)A/B.


## Creación de audiencias en AEM {#create-audiences-within-aem}

AEM le permite crear una audiencia y utilizarla para una prueba A/B. La audiencia que crea en AEM está disponible en AEM Forms. Realice los siguientes pasos para crear audiencias en AEM:

1. En la instancia de creación, toque **Adobe Experience Manager** > **Personalización** > **Audiencias**.

1. En la página Audiencias, toque **Crear audiencia > Crear audiencia** de Target.
1. En el cuadro de diálogo Configuración de Adobe Target, seleccione una configuración de Target y haga clic en **Aceptar**.
1. En la página Crear nueva audiencia, cree reglas. Las reglas permiten clasificar la audiencia. Por ejemplo, desea categorizar las audiencias en función del sistema operativo. Su audiencia A viene de Windows y la audiencia B viene de Linux.

   1. Para categorizar una audiencia en función de Windows, en la regla 1, seleccione el tipo de atributo de **SO** . En la lista desplegable Cuándo, seleccione **Windows.**

   1. Para categorizar una audiencia en función de Linux, en la regla 2, seleccione el tipo de atributo de **SO** . En la lista desplegable **Cuándo** , seleccione **Linux** y haga clic en **Siguiente**.

1. Especifique un nombre para la audiencia creada y haga clic en **Guardar**.

Puede seleccionar la audiencia al configurar la prueba A/B para un formulario, como se muestra a continuación.

## Crear prueba A/B {#create-a-b-test}

Realice los pasos siguientes para crear una prueba A/B para un formulario adaptable.

1. Vaya a **Forms &amp; Documents** en https://&lt;*hostname*>:&lt;*port*>/aem/forms.html/content/dam/formsanddocuments.

1. Vaya a la carpeta que contiene el formulario adaptable.
1. Haga clic en la herramienta **Seleccionar** de la barra de herramientas y seleccione el formulario adaptable.
1. Haga clic en **Más** en la barra de herramientas y seleccione **Configurar prueba** A/B. Se abre la página Configurar pruebas A/B.

[ Página de configuración de la prueba ![A/B para formularios adaptables](assets/ab-test-configure.png)](assets/ab-test-configure-1.png)

1. Especifique un nombre **de** actividad para la prueba A/B.

1. En la lista desplegable Audiencia, seleccione una audiencia a la que desee ofrecer distintas experiencias del formulario. Por ejemplo, **Visitantes que utilizan Chrome**. La lista de audiencias se rellena desde el servidor de Target configurado.

1. En los campos **de distribución** de experiencias para las experiencias A y B, especifique la distribución, en porcentaje, para determinar la distribución de experiencias entre la audiencia total. Por ejemplo, si especifica 40, 60 para las experiencias A y B, respectivamente, la experiencia A se ofrecerá al 40 % de la audiencia y el 60 % restante verá la experiencia B.
1. Haga clic en **Configurar**. Aparece un cuadro de diálogo para confirmar la creación de la prueba A/B.
1. Haga clic en **Editar experiencia B** para abrir el formulario adaptable en modo de edición. Modifique el formulario para crear una experiencia distinta a la experiencia A predeterminada. Las posibles variaciones permitidas en la Experiencia B son los cambios en:

   * CSS o estilo
   * Orden de los campos en diferentes paneles o en el mismo panel
   * Diseño de panel
   * Títulos del panel
   * Descripción, etiqueta y texto de ayuda de un campo
   * Secuencias de comandos que no afectan o rompen el flujo de envío
   * Validaciones (tanto del cliente como del servidor)
   * Tema de la experiencia B. (Puede seleccionar un tema alternativo para la experiencia B)

1. Vaya a la interfaz de usuario de Forms y Documents, seleccione el formulario adaptable, haga clic en **Más** y seleccione **Iniciar prueba** A/B.

La prueba A/B se está ejecutando y la audiencia especificada se mostrará aleatoriamente en función de la distribución especificada.

## Update A/B test {#update-a-b-test}

Puede actualizar las distribuciones de audiencia y experiencia de una prueba A/B en ejecución. Para ello:

1. En la interfaz de usuario de Forms &amp; Documents, vaya a la carpeta que contiene el formulario adaptable en el que se está ejecutando la prueba A/B.
1. Seleccione el formulario adaptable.
1. Haga clic en **Más** y, a continuación, seleccione **Editar prueba** A/B. Se abre la página de prueba A/B de actualización.

1. Actualice las distribuciones de audiencia y experiencia según sea necesario.
1. Click **Update**.

## Visualización y análisis del informe de prueba A/B {#view-and-analyze-a-b-test-report}

Una vez que haya permitido que la prueba A/B se ejecute durante el período deseado, puede generar un informe y comprobar qué experiencia ha resultado en una mejor conversión. Puede declarar una experiencia de mejor rendimiento como ganadora o elegir ejecutar otra prueba A/B. Para ello, lleve a cabo los siguientes pasos:

1. Seleccione el formulario adaptable, haga clic en **Más** y, a continuación, en Informe **de prueba** A/B. Se muestra el informe.

[ Informe de prueba ![A/B](assets/ab-test-report-2.png)](assets/ab-test-report-3.png)

1. Analice el informe y compruebe si tiene suficientes puntos de datos para declarar como ganadoras una de las experiencias con mejor rendimiento. Puede elegir continuar con la misma prueba A/B durante más tiempo o declarar un ganador y finalizar la prueba A/B.
1. Para declarar un ganador y finalizar la prueba A/B, haga clic en **Finalizar prueba** A/B en el tablero de informes. Un cuadro de diálogo le solicita que declare una de las dos experiencias como ganadora. Seleccione un ganador y confirme que desea finalizar la prueba A/B.
También puede declarar un ganador primero haciendo clic en el botón **Declarar ganador** para la experiencia correspondiente. Le solicita que confirme el ganador. Haga clic en **Sí** para finalizar la prueba A/B.

Si eligió la experiencia A como ganadora, la prueba A/B finalizará y, a partir de ahora, solo se ofrecerá la experiencia A a todas las audiencias.
