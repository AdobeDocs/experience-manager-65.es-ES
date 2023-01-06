---
title: Crear y administrar pruebas A/B para formularios adaptables
seo-title: Create and manage A/B test for adaptive forms
description: AEM Forms se integra con Adobe Target, que permite ejecutar pruebas A/B en formularios adaptables para mejorar la experiencia del cliente y las tasas de conversión.
seo-description: AEM Forms integrates with Adobe Target that allows running A/B tests for adaptive forms to enhance customer experience and improve conversion rates.
uuid: e258805c-4da8-4c5d-ae91-7bea78a6a71b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 8f776f30-ff93-4d19-94c6-c4bfe6f1fae2
docset: aem65
source-git-commit: 9ee8e79777b89fbf4d6e5b5fd1dbb1ef3bc9ad5d
workflow-type: ht
source-wordcount: '1544'
ht-degree: 100%

---

# Crear y administrar pruebas A/B para formularios adaptables{#create-and-manage-a-b-test-for-adaptive-forms}

## Información general {#overview-br}

Es probable que los clientes abandonen un formulario si la experiencia que ofrece no es atractiva. A pesar de que para ellos resulta frustrante, también puede aumentar el volumen y el coste de la asistencia en su organización. Identificar y ofrecer una experiencia del cliente correcta que aumente la tasa de conversión es fundamental, además de un desafío. Adobe Experience Manager Forms es la clave para solucionar este problema.

AEM Forms se integra con Adobe Target, una solución de Adobe Marketing Cloud, para ofrecer experiencias personalizadas y atractivas a través de varios canales digitales. Una de las capacidades clave de Target es la prueba A/B que le permite configurar rápidamente pruebas A/B simultáneas, presentar contenido relevante para los usuarios objetivo e identificar la experiencia que aporta una tasa de conversión mejor.

Con AEM Forms, puede configurar y ejecutar pruebas A/B en formularios adaptables en tiempo real. Además, ofrece capacidades para generar informes listas para usar y personalizables para visualizar el rendimiento en tiempo real de las experiencias de los formularios e identificar la que maximiza el compromiso y la conversión de los usuarios.

## Configurar e integrar Target en AEM Forms {#set-up-and-integrate-target-in-aem-forms}

Antes de empezar a crear y a analizar pruebas A/B para formularios adaptables, debe configurar el servidor de Target e integrarlo en AEM Forms.

### Configurar Target {#set-up-target}

Para integrar AEM con Target, asegúrese de que tiene una cuenta de Adobe Target. Al registrarse en Adobe Target, recibirá un código de cliente. Necesita el código de cliente, el correo electrónico asociado a la cuenta de Target y la contraseña para conectarse AEM Target.

El código de cliente identifica la cuenta de cliente de Adobe Target y se utiliza como subdominio en la dirección URL al llamar al servidor de Adobe Target. Antes de continuar, inicie sesión en [https://experience.adobe.com/](https://experience.adobe.com/) y, si tiene acceso, consulte la opción [!DNL Adobe Target] en la sección [!UICONTROL Acceso rápido].

### Integrar Target en AEM Forms {#integrate-target-in-aem-forms}

Siga estos pasos para integrar un servidor de Target en ejecución con AEM Forms:

1. En el servidor de AEM, vaya a https://&lt;*hostname*>:&lt;*port*>/libs/cq/core/content/tools/cloudservices.html.

1. En la sección **Adobe Target**, haga clic en **Mostrar configuraciones** y luego en el icono **+** para agregar una configuración nueva.
Si está configurando Target por primera vez, haga clic en **Configurar ahora.**

1. En el cuadro de diálogo Crear configuración, especifique un **Título** y opcionalmente un **Nombre** para la configuración.

1. Haga clic en **Crear**. Se abrirá el cuadro de diálogo Editar Componente.
1. Especifique los detalles de la cuenta de Target, como el código de cliente, el correo electrónico y la contraseña.
1. Seleccione **Rest** de la lista desplegable Tipo de API.

1. Haga clic en **Conectarse a Adobe Target** para inicializar la conexión con Target. Si la conexión se realiza correctamente, aparecerá el mensaje Conexión correcta. Haga clic en **Aceptar** en el mensaje y, a continuación, **Aceptar** en el cuadro de diálogo. La cuenta de Target está configurada.

1. Cree una estructura de Target como se describe en [Agregar un marco de trabajo](/help/sites-administering/target.md).

1. Vaya a https://&lt;*hostname*>:&lt;*port*>/system/console/configMgr.

1. Haga clic en **Configuración de AEM Forms Target**.
1. Seleccione un **Marco de trabajo de Target**.
1. En el campo **Direcciones URL de destino**, especifique todas las direcciones URL donde se ejecutarán las pruebas A/B. Por ejemplo, https://&lt;*hostname*>:&lt;*port*>/ para el servidor de AEM Forms en OSGi o https://&lt;*hostname*>:&lt;*port*>/lc/ para el servidor de AEM Forms en JEE.
Tenga en cuenta que debe configurar una URL de destino para una instancia de publicación y que los clientes pueden acceder a ella mediante el nombre del host o la dirección IP, debe configurar como URL de destino mediante el nombre del host y la dirección IP. Si configura solo una de las direcciones URL, la prueba A/B no se ejecutará para los clientes que provengan de la otra dirección URL. Haga clic en **+** para especificar varias direcciones URL.

1. Haga clic en **Guardar**.

El servidor de Target está integrado con AEM Forms. Ahora puede habilitar la prueba A/B si dispone de una licencia completa para utilizar Adobe Target.

Si tiene una licencia completa para utilizar Adobe Target, inicie el servidor con los siguientes parámetros después de integrar Target con AEM Forms:

`parameter -Dabtesting.enabled=true java -Xmx2048m -XX:MaxPermSize=512M -jar -Dabtesting.enabled=true`

Si la instancia de AEM se ejecuta en Jboss como servicio de turnkey, en `jboss\bin\standalone.conf.bat`, agregue el parámetro -Dabtesting.enabled=true en la siguiente entrada:

`set "JAVA_OPTS=%JAVA_OPTS% -Dadobeidp.serverName=server1 -Dfile.encoding=utf8 -Djava.net.preferIPv4Stack=true -Dabtesting.enabled=true"`

Además del servidor jboss, puede agregar el argumento -Dabtesting.enabled=true jvm en el script de inicio del servidor para cualquier servidor de aplicaciones. Ahora puede crear y ejecutar pruebas A/B para formularios adaptables.

>[!NOTE]
>
>Si actualiza las direcciones URL de Target configuradas más adelante, asegúrese de actualizar todas las pruebas A/B que se ejecuten para que apunten a las direcciones URL actuales. Para obtener información sobre la actualización de pruebas A/B, consulte [Actualizar la prueba A/B](/help/forms/using/ab-testing-adaptive-forms.md#p-update-a-b-test-p).

## Crear audiencias dentro de AEM {#create-audiences-within-aem}

AEM permite crear una audiencia y utilizarla para una prueba A/B. La audiencia que cree en AEM estará disponible en AEM Forms. Siga estos pasos para crear audiencias dentro de AEM:

1. En la instancia de autor, pulse **Adobe Experience Manager** > **Personalización** > **Audiencias**.

1. En la página Audiencias, pulse **Crear audiencia > Crear audiencia de Target**.
1. En el cuadro de diálogo Configuración de Adobe Target, seleccione una configuración de Target y haga clic en **Aceptar**.
1. En la página Crear audiencia, cree reglas. Las reglas permiten clasificar la audiencia. Por ejemplo, debe categorizar las audiencias en función del sistema operativo. La audiencia A proviene de Windows y la audiencia B procede de Linux.

   1. Para categorizar la audiencia según Windows, en la Regla #1, seleccione el tipo de atributo **Sistema operativo**. En la lista desplegable Cuándo, seleccione **Windows.**

   1. Para categorizar la audiencia según Linux, en la Regla #2, seleccione el tipo de atributo **Sistema operativo**. En el menú desplegable **Cuándo**, seleccione **Linux** y haga clic en **Siguiente**.

1. Especifique un nombre para la audiencia creada y haga clic en **Guardar**.

Puede seleccionar la audiencia cuando configure las pruebas A/B para un formulario, como se muestra a continuación.

## Crear una prueba A/B {#create-a-b-test}

Realice los siguientes pasos para crear una prueba A/B para un formulario adaptable.

1. Vaya a **Formularios y documentos** en https://&lt;*hostname*>:&lt;*port*>/aem/forms.html/content/dam/formsanddocuments.

1. Vaya a la carpeta que contiene el formulario adaptable.
1. Haga clic en la herramienta **Seleccionar** en la barra de herramientas y seleccione el formulario adaptable.
1. Haga clic en **Más** en la barra de herramientas y seleccione **Configurar pruebas A/B**. Se abrirá la página Configurar prueba A/B.

[ ](assets/ab-test-configure-1.png)

1. Especifique un **Nombre de la actividad** para la prueba A/B.

1. En la lista desplegable Audiencia, seleccione la audiencia a la que desee ofrecer diferentes experiencias del formulario. Por ejemplo, **Visitantes que utilicen Chrome**. La lista de audiencias se rellenará desde el servidor de Target configurado.

1. En el campo **Distribución de experiencias** para las experiencias A y B, especifique la distribución, en términos de porcentaje, para determinar la distribución de experiencias entre la audiencia total. Por ejemplo, si especifica 40 o 60 para las experiencias A y B, respectivamente, la experiencia A se ofrecerá al 40 % de la audiencia y el 60 % restante verá la experiencia B.
1. Haga clic en **Configurar**. Aparecerá un cuadro de diálogo para confirmar la creación de la prueba A/B.
1. Haga clic en **Editar experiencia B** para abrir el formulario adaptable en el modo de edición. Modifique el formulario para crear una experiencia diferente a la predeterminada A. Las posibles variaciones permitidas en la Experiencia B son cambios en lo siguiente:

   * CSS o estilo
   * Orden de los campos en diferentes paneles o en el mismo panel
   * Diseño de panel
   * Títulos del panel
   * Descripción, etiqueta y texto de ayuda de un campo
   * Scripts que no afecten o rompan el flujo de envío
   * Validaciones (lado del cliente y del servidor)
   * Temática para la experiencia B. (Puede seleccionar una temática alternativa para la experiencia B)

1. Vaya a la interfaz de usuario de Formularios y documentos, seleccione el formulario adaptable, haga clic en **Más** y seleccione **Iniciar pruebas A/B**.

La prueba A/B se ejecutará y la audiencia especificada recibirá aleatoriamente las experiencias en función de la distribución especificada.

## Actualizar la prueba A/B {#update-a-b-test}

Puede actualizar las distribuciones de audiencia y experiencia de una prueba A/B en ejecución. Para ello:

1. En la interfaz de usuario de Formularios y documentos, navegue hasta la carpeta que contenga el formulario adaptable en el que se esté ejecutando la prueba A/B.
1. Seleccione el formulario adaptable.
1. Haga clic en **Más** y, a continuación, seleccione **Editar prueba A/B**. Se abrirá la página Actualizar la prueba A/B.

1. Actualice las distribuciones de audiencia y experiencia según sea necesario.
1. Haga clic en **Actualizar**.

## Ver y analizar el informe de prueba A/B {#view-and-analyze-a-b-test-report}

Una vez que haya permitido que la prueba A/B se ejecute durante el período deseado, puede generar un informe y comprobar qué experiencia ha resultado en una mejor conversión. Puede declarar la experiencia con mejor rendimiento como ganadora o elegir ejecutar otra prueba A/B. Para ello, realice los siguientes pasos:

1. Seleccione el formulario adaptable, haga clic en **Más** y, a continuación, haga clic en **Informe de prueba A/B**. Se mostrará el informe.

[ ](assets/ab-test-report-3.png)

1. Analice el informe y compruebe si tiene suficientes datos para declarar como ganadora a la experiencia con mejor rendimiento. Puede optar por continuar con la misma prueba A/B durante más tiempo o declarar un ganador y finalizarla.
1. Para declarar un ganador y finalizar la prueba A/B, haga clic en el botón **Finalizar prueba A/B** en el panel de informes. Un cuadro de diálogo le pedirá que declare una de las dos experiencias como ganadoras. Elija un ganador y confirme que desea finalizar la prueba A/B.
Como alternativa, puede declarar un ganador primero si hace clic en el botón **Declarar ganador** de la experiencia correspondiente. Le solicitará que confirme el ganador. Haga clic en **Sí** para finalizar la prueba A/B.

Si eligió la experiencia A como ganadora, la prueba A/B finalizará y, en adelante, solo se ofrecerá la experiencia A a todas las audiencias.
