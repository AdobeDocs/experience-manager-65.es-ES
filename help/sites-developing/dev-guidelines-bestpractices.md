---
title: 'AEM Desarrollo: directrices y prácticas recomendadas'
seo-title: AEM Development - Guidelines and Best Practices
description: AEM Directrices y prácticas recomendadas para el desarrollo de soluciones en el área de la
seo-description: Guidelines and best practices for developing on AEM
uuid: a67de085-4441-4a1d-bec3-2f27892a67ff
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: b4cf0ffc-973a-473b-80c8-7f530d111435
exl-id: 8eef7e4d-a6f2-4b87-a995-0761447283c6
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '1093'
ht-degree: 0%

---

# AEM Desarrollo: directrices y prácticas recomendadas{#aem-development-guidelines-and-best-practices}

## Directrices para el uso de plantillas y componentes {#guidelines-for-using-templates-and-components}

AEM Los componentes y las plantillas de forman un conjunto de herramientas muy potente. Los desarrolladores pueden utilizarlas para proporcionar a los usuarios, editores y administradores de sitios web la funcionalidad de adaptar sus sitios web a las cambiantes necesidades comerciales (agilidad de los contenidos), manteniendo al mismo tiempo el diseño uniforme de los sitios (protección de la marca).

Un desafío típico para una persona responsable de un sitio web o un conjunto de sitios web (por ejemplo, en una sucursal de una empresa global) es introducir un nuevo tipo de presentación de contenido en sus sitios web.

Supongamos que es necesario agregar una página de lista de noticias a los sitios web, que enumera extractos de otros artículos ya publicados. La página debe tener el mismo diseño y estructura que el resto del sitio web.

La manera recomendada de abordar ese problema sería la siguiente:

* Reutilice una plantilla existente para crear un nuevo tipo de página. La plantilla define aproximadamente la estructura de la página (elementos de navegación, paneles, etc.), que se ajusta aún más por su diseño (CSS, gráficos).
* Utilice el sistema de párrafos (parsys/iparsys) en las páginas nuevas.
* Defina el derecho de acceso al modo Diseño de los sistemas de párrafos, de modo que solo las personas autorizadas (normalmente el administrador) puedan cambiarlas.
* Defina los componentes permitidos en el sistema de párrafos determinado para que los editores puedan colocar los componentes necesarios en la página. En nuestro caso, podría ser un componente de lista, que puede atravesar un subárbol de páginas y extraer la información según reglas predefinidas.
* Los editores agregan y configuran los componentes permitidos, en las páginas de las que son responsables, para entregar la funcionalidad solicitada (información) a la empresa.

Esto ilustra cómo este enfoque permite a los usuarios y administradores colaboradores del sitio web responder a las necesidades comerciales rápidamente, sin requerir la participación de equipos de desarrollo. Los métodos alternativos, como la creación de una nueva plantilla, suelen ser un ejercicio costoso, que requiere un proceso de gestión del cambio y la participación del equipo de desarrollo. Esto hace que todo el proceso sea mucho más largo y costoso.

AEM Por lo tanto, los desarrolladores de sistemas basados en el uso de deben utilizar:

* plantillas y control de acceso al diseño del sistema de párrafos para la uniformidad y la protección de la marca
* sistema de párrafos, incluidas sus opciones de configuración para una mayor flexibilidad.

Las siguientes reglas generales para desarrolladores tienen sentido en la mayoría de los proyectos habituales:

* Mantenga el número de plantillas bajo, tan bajo como el número de estructuras de página fundamentalmente diferentes en los sitios web.
* Proporcione la flexibilidad y las capacidades de configuración necesarias a los componentes personalizados.
* AEM Maximice el uso de la potencia y la flexibilidad del sistema de párrafos: los componentes parsys e iparsys.

### Personalizar componentes y otros elementos {#customizing-components-and-other-elements}

Al crear sus propios componentes o personalizar un componente existente, a menudo es más fácil (y seguro) reutilizar las definiciones existentes. AEM Los mismos principios también se aplican a otros elementos dentro de la, por ejemplo, el controlador de errores.

Esto se puede hacer copiando y superponiendo la definición existente. Es decir, copiar la definición de `/libs` hasta `/apps/<your-project>`. Esta nueva definición, en `/apps`, se puede actualizar según sus necesidades.

>[!NOTE]
>
>Consulte [Uso de superposiciones](/help/sites-developing/overlays.md) para obtener más información.

Por ejemplo:

* [Personalizar un componente](/help/sites-developing/components.md)

  Esto implicaba superponer una definición de componente:

   * Cree una nueva carpeta de componentes en `/apps/<website-name>/components/<MyComponent>` copiando un componente existente:

      * Por ejemplo, para personalizar la copia del componente Texto:

         * de `/libs/foundation/components/text`
         * hasta `/apps/myProject/components/text`

* [Personalizar páginas mostradas por el Controlador de errores](/help/sites-developing/customizing-errorhandler-pages.md#how-to-customize-pages-shown-by-the-error-handler)

  Este caso implica la superposición de un servlet:

   * En el repositorio, copie los scripts predeterminados:

      * de `/libs/sling/servlet/errorhandler/`
      * hasta `/apps/sling/servlet/errorhandler/`

>[!CAUTION]
>
>Usted **no debe** cambiar cualquier cosa en `/libs` ruta.
>
>Esto se debe al contenido de `/libs` se sobrescribe la próxima vez que actualice la instancia (y es posible que se sobrescriba al aplicar una revisión o un paquete de funciones).
>
>Para cambios de configuración y de otro tipo:
>
>1. copie el elemento en `/libs` hasta `/apps`
>1. realice cambios en `/apps`

## Cuándo utilizar Consultas JCR y cuándo no utilizarlas {#when-to-use-jcr-queries-and-when-not-to-use-them}

Las consultas JCR son una herramienta potente cuando se utilizan correctamente. Son adecuados para:

* consultas reales del usuario final, como búsquedas de texto completo en el contenido.
* ocasiones en las que es necesario encontrar contenido estructurado en todo el repositorio.

  En estos casos, asegúrese de que las consultas solo se ejecutan cuando son absolutamente necesarias, por ejemplo, al activar un componente o al invalidar la caché (en oposición a, por ejemplo, Pasos de flujos de trabajo, Controladores de eventos que almacenan en déclencheur las modificaciones del contenido, Filtros, etc.).

Las consultas JCR nunca deben utilizarse para solicitudes de procesamiento puras. Por ejemplo, las consultas JCR no son apropiadas para

* navegación de procesamiento
* información general sobre la creación de las 10 noticias más recientes
* mostrar recuentos de elementos de contenido

Para procesar contenido, utilice el acceso de navegación al árbol de contenido en lugar de realizar una consulta JCR.

>[!NOTE]
>
>Si usa el [Generador de consultas](/help/sites-developing/querybuilder-api.md), utilice Consultas JCR, ya que el Generador de consultas genera Consultas JCR bajo el capó.
>

## Consideraciones de seguridad {#security-considerations}

>[!NOTE]
>
>También merece la pena hacer referencia a la [lista de comprobación de seguridad](/help/sites-administering/security-checklist.md).

### Sesiones JCR (repositorio) {#jcr-repository-sessions}

Debe utilizar la sesión del usuario, no la sesión administrativa. Esto significa que debe utilizar:

```java
slingRequest.getResourceResolver().adaptTo(Session.class);
```

### Protect con scripts en sitios múltiples (XSS) {#protect-against-cross-site-scripting-xss}

El proceso de ejecución de scripts en sitios múltiples (XSS) permite a los atacantes insertar código en páginas web que han visto otros usuarios. Los usuarios web malintencionados pueden aprovechar esta vulnerabilidad de seguridad para evitar los controles de acceso.

AEM Se aplica el principio de filtrado de todo el contenido proporcionado por el usuario en la salida. La prevención de XSS tiene la máxima prioridad tanto durante el desarrollo como durante las pruebas.

Además, un cortafuegos de aplicaciones web, como [mod_security para Apache](https://modsecurity.org), puede proporcionar un control central y fiable sobre la seguridad del entorno de implementación y proteger contra ataques de scripts entre sitios que no se habían detectado anteriormente.

>[!CAUTION]
>
>AEM El código de ejemplo proporcionado con puede no protegerse contra estos ataques y, por lo general, se basa en el filtrado de solicitudes por un cortafuegos de aplicaciones web.

AEM La hoja de trucos de la API XSS contiene información que necesita saber para utilizar la API XSS y hacer que una aplicación de la aplicación sea más segura. Puede descargarlo aquí:

La hoja de trucos de XSSAPI.

[Obtener archivo](assets/xss_cheat_sheet_2016.pdf)

### Proteger la comunicación de información confidencial {#securing-communication-for-confidential-information}

Como para cualquier aplicación de Internet, asegúrese de que al transportar información confidencial

* el tráfico está protegido mediante SSL
* Se utiliza el POST HTTP si corresponde

Esto se aplica a la información que es confidencial para el sistema (como la configuración o el acceso administrativo), así como a la información confidencial para sus usuarios (como sus datos personales)

## Tareas de desarrollo distintas {#distinct-development-tasks}

### Personalización de páginas de error {#customizing-error-pages}

AEM Las páginas de error se pueden personalizar para la creación de informes de. Esto es aconsejable para que la instancia no muestre los seguimientos de sling en los errores internos del servidor.

Consulte [Personalizar páginas de error mostradas por el controlador de error](/help/sites-developing/customizing-errorhandler-pages.md) para obtener información detallada.

### Abrir archivos en el proceso de Java {#open-files-in-the-java-process}

AEM Debido a que puede acceder a un gran número de archivos, se recomienda que el número de [abrir archivos para un proceso de Java](/help/sites-deploying/configuring.md#open-files-in-the-java-process) AEM se configurarán explícitamente para la configuración de la.

Para minimizar este problema, el desarrollo debe garantizar que cualquier archivo abierto se cierre correctamente lo antes posible (de forma significativa).
