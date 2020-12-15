---
title: Personalización
seo-title: Personalización
description: Obtenga información sobre la personalización en AEM.
seo-description: Obtenga información sobre la personalización en AEM.
uuid: 5790a3e0-f0ec-4785-b915-330a10dea30c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 03ebc494-8baa-4741-b8de-dac5ace743c8
translation-type: tm+mt
source-git-commit: ffded9c4c08c68db59d05b341166bed92e741e1e
workflow-type: tm+mt
source-wordcount: '1693'
ht-degree: 16%

---


# Personalización {#personalization}

## ¿Qué es Personalización? {#what-is-personalization}

Existe un volumen cada vez mayor de contenido disponible en la actualidad, ya sea en sitios web de Internet, extranet o intranet.

La personalización se centra en proporcionar al usuario un entorno personalizado que muestre contenido dinámico seleccionado según sus necesidades específicas; se basa en perfiles predefinidos, en la selección de usuarios o en el comportamiento interactivo del usuario.

Hay tres elementos principales involucrados en la personalización:

### Usuarios {#users}

* Tener perfiles, tanto individuales como de grupo. Estos perfiles contienen características (como la descripción del trabajo, la ubicación o los intereses) que pueden utilizarse para personalizar el contenido que pueden ver.
* Tome medidas. A continuación, se pueden analizar y comparar con reglas de comportamiento para adaptar el contenido que ven.

### Contenido {#content}

* Es lo que el usuario quiere ver. Preferiblemente contenido de interés y uso para ellos para cumplir sus tareas.
* Se puede categorizar y, por lo tanto, ponerlo a disposición de los usuarios según reglas predefinidas. debe ser dinámico; en otras palabras, el contenido
* De alguna manera, debe depender del usuario; si cada usuario viera el mismo contenido, la personalización sería redundante.

### Reglas {#rules}

* Defina cómo sucede realmente la personalización: qué contenido puede ver el usuario y cuándo.

La personalización puede ser:

#### Explícita {#explicit}

* Personalización: mediante la cual el usuario realiza selecciones de una selección de fuentes de contenido.

#### Implícito {#implicit}

* Basado en reglas: los administradores de negocios definen reglas específicas para acciones basadas en perfiles y/o comportamientos específicos.
* Filtro simple: las selecciones se realizan en base a perfiles predefinidos a nivel de usuario y/o grupo.
* Filtrado colaborativo/de recomendaciones: el comportamiento del usuario se registra según las reglas predefinidas. Estas reglas se basan en el comportamiento observado con personas con ideas afines. La información recopilada se utiliza para adaptar la información que se muestra al usuario, en particular en forma de recomendaciones.

## ¿Cómo y cuándo se puede utilizar la personalización? {#how-and-when-can-personalization-be-used}

La personalización se puede utilizar en muchos casos, por ejemplo:

### Páginas de intranet {#intranet-pages}

* El contenido se puede ofrecer en función de la ubicación, el departamento o la función de un usuario, ya definida en una red interna.
* Según la opción disponible, el usuario puede realizar más selecciones.

### Grupos de usuarios específicos, limitados y de Destinatario - Extranets {#extranets}

* Los usuarios requieren un inicio de sesión para la autorización; se vinculará a un perfil que proporcione la información necesaria para la personalización; posiblemente detalles como su ubicación, relación con el producto, historial de uso, responsabilidades presupuestarias, etc.
* Estas instancias pueden abarcar sitios como:
* Compañías que proporcionan sitios web a una sección altamente especializada de su mercado, por ejemplo, una compañía farmacéutica que proporciona un sitio web especializado para médicos.
* Compañías que proporcionan sitios web que permiten a sus clientes realizar vistas de la cuenta corriente y de la información de facturación; por ejemplo, proveedores de telefonía.

### Sitio Web de ventas y distribución {#sales-site}

* Los sitios web de ventas y distribución, como Amazon, pueden combinar un perfil de usuario, el historial de ventas del usuario y su historial de exploración para hacer sugerencias sobre lo que podría interesar al usuario a continuación.

### Buscar sitios Web {#search-site}

* Muchos de los principales sitios Web de motores de búsqueda tienen herramientas analíticas muy poderosas que registran el comportamiento del usuario, los términos de búsqueda que utilizan y los sitios Web que visitan. A continuación, se utiliza para personalizar el contenido proporcionado, especialmente en lo que respecta a la visualización de anuncios.

### Puntos fuertes de la Personalización y Puntos a considerar {#strengths-of-personalization-and-points-to-consider}

A continuación se indican los motivos por los que se debe utilizar la personalización:

* Un usuario puede experimentar un sitio web cómodo y centrado.
* La personalización se puede utilizar para propagar automáticamente el acceso a la última versión del contenido.
* Los usuarios tienen a su disposición funciones de colaboración social para comunicarse entre sí, ya que pueden identificarse por sus perfiles.
* Se puede proporcionar al usuario el contenido que necesita para cumplir una tarea determinada. Dentro de la intranet de una compañía, esto puede proporcionar una herramienta inestimable para difundir información.
* Se puede proporcionar al usuario el contenido que necesita o desea, reduciendo así el tiempo necesario para realizar operaciones de búsqueda.
* El proveedor de contenido puede dirigir el contenido para que lo vean categorías específicas de usuarios.
* Las reglas se pueden definir para ofrecer contenido basado en combinaciones de características y comportamiento del usuario. Esto proporciona un mecanismo sofisticado para personalizar su experiencia web.

Al utilizar la personalización, tenga en cuenta lo siguiente:

#### Actuación {#performance}

* Naturalmente, la análisis y la evaluación adicionales repercuten en el rendimiento. Sin embargo, los métodos utilizados son muy sofisticados y se pueden optimizar para minimizar el impacto.

#### Autorización {#authorization}

* La personalización requiere un mecanismo de inicio de sesión, ya que el sitio web debe poder identificar al usuario.

#### Almacenamiento en caché {#caching}

* El almacenamiento en caché es un aspecto que el usuario verá en cuanto al rendimiento y la precisión: la rapidez con la que el sitio web ofrece contenido personalizado y siempre está actualizado.
* El almacenamiento en caché es una consideración clave a la hora de configurar la personalización y debe tomarse tiempo para garantizar que se utilice la implementación correcta.

>[!TIP]
>
>El efecto de la personalización en el rendimiento y los temas relacionados con el almacenamiento en caché se analizan más a fondo en el documento [Optimización del rendimiento.](/help/sites-deploying/configuring-performance.md)

#### Precisión de las reglas {#accuracy}

* La personalización realizada mediante el seguimiento del comportamiento del usuario o la configuración de reglas basadas en el perfil del usuario debe ser precisa y lógica.
* No hay nada más frustrante para el usuario que tener contenido forzado o negado a hacerlo debido a la lógica inexacta de una regla.
* Por lo tanto, las reglas deben estar bien pensadas, con los requisitos del usuario en primer plano. Esto puede requerir mucho esfuerzo y no debe subestimarse; la definición de las reglas comerciales suele superar el esfuerzo técnico al implementar la personalización.

#### Cuándo usar {#when-to-use}

* Al igual que muchas funciones de la web, la personalización debe usarse con cuidado. ¿Su uso beneficiará realmente al usuario? siempre debe ser la primera consideración -o si el objetivo deseado se puede lograr con menos esfuerzo por otro método. La personalización puede correr el riesgo de ser una función que los usuarios configuren una vez (para ver cómo funciona) y sólo una vez, ya que no les ofrece ninguna ventaja real.
* La personalización solo es significativa cuando el contenido es dinámico, ya que depende del usuario de alguna manera. Si todos los usuarios ven el mismo contenido, la personalización es redundante.

#### Confidencialidad {#confidentiality}

* Muchos usuarios están preocupados por la seguridad y protección de datos. En particular, los datos recuperados al rastrear su comportamiento al navegar por la web.

## Personalización y acceso {#personalization-and-access}

La personalización debe considerarse por separado del control de acceso, pero se interrelacionan.

La propia personalización no crea ninguna forma de control de acceso. Se trata simplemente de un método de dirección de lo que ve el usuario; no restringe el acceso del usuario a otro contenido y, como sucede con cualquier contenido, ya debe tener asignados los controles de acceso correctos.

Sin embargo, control de acceso puede utilizarse para crear una forma de personalización. Si permite o deniega a un usuario el acceso al contenido, esto afecta inevitablemente a la elección del contenido que tiene disponible, por lo que personaliza su experiencia web.

## Componentes disponibles para Personalización {#components-available-for-personalization}

Se proporcionan varios componentes con AEM para la personalización. Algunos permiten a los usuarios iniciar sesión y editar sus perfiles, otros (como Mis gadgets) permiten a los usuarios configurar una página específica:

| Título en la barra de tareas | Función |
|---|---|
| Campo de contraseña activado | Solicita una contraseña y la confirmación de la misma. |
| Registro combinado de inicio de sesión | Permite que el usuario inicie sesión en una cuenta existente o que se registre en una cuenta nueva. |
| Campo de dirección de Forms | Campo complejo que permite la introducción de una dirección internacional. |
| Forms Begin | Inicio una definición de formulario |
| Forms Captcha | Campo que consta de una palabra alfanumérica que se actualiza automáticamente. El componente captcha protege a los sitios web de los robots. |
| Grupo de casillas de verificación de Forms | Varios elementos organizados en una lista y precedidos por casillas de verificación. Los usuarios pueden activar varias casillas de verificación. |
| Lista desplegable de Forms | Varios elementos organizados en una lista desplegable. El conmutador Selección múltiple especifica si se pueden seleccionar varios elementos de la lista. |
| Forms End | Termina la definición del formulario. |
| Carga de archivos de Forms | Elemento de carga que permite al usuario cargar un archivo en el servidor. |
| Campo oculto de Forms | Este campo no se muestra al usuario. Se puede emplear para transportar un valor al cliente y devolverlo al servidor. Este campo no debe tener restricciones. |
| Botón Imagen de Forms | Botón de envío adicional para el formulario que se procesa como imagen. |
| Campo de contraseña de Forms | Igual que un campo de texto pero solo se permite una sola línea y la introducción de texto por parte del usuario no está visible en el campo. |
| Forms Radio Group | Varios elementos organizados en una lista y precedidos por un botón de opción. Los usuarios deben seleccionar únicamente un botón de opción. |
| Botón de envío de Forms | Botón de envío adicional para el formulario donde el título se muestra como texto en el botón. |
| Campo de texto de Forms | Campo de texto que permite a los usuarios introducir información. |
| My Gadgets | Permite incluir uno de los gadgets disponibles. |
| Fotografía de avatar de perfil | Permite la introducción de una fotografía de avatar. |
| Nombre detallado de perfil | Introducción de la información de nombre, incluyendo elementos como título, segundo nombre y sufijo, si es necesario. |
| Nombre para mostrar en el perfil | Nombre para mostrar. |
| Correo electrónico del perfil | Introducción de una dirección de correo electrónico. |
| Género de perfil | Permite la introducción del género. |
| Número de teléfono principal de perfil | Permite la introducción de un número de teléfono. |
| URL principal del perfil | Permite la introducción de una dirección URL. |
| Perfil General Text, propiedad | Propiedades del perfil. |
| Inicio de sesión | Permite enviar un nombre de usuario y una contraseña al iniciar sesión. |
| Cerrar sesión | Indica el usuario que ha iniciado sesión y le proporciona un vínculo para cerrar la sesión. |
| Nube de etiquetas | Una nube de etiquetas para mostrar una selección de etiquetas presentada gráficamente en el sitio web |
| Teaser | Parte de contenido (generalmente una imagen) que se muestra en una página principal para &quot;animar&quot; a los usuarios a acceder al contenido subyacente. |

## Personalización y contenido de la comunidad {#personalization-and-community-content}

Las funciones de la comunidad como blogs, foros y calendarios resultan en la creación de contenido de la comunidad, comúnmente denominado contenido generado por el usuario (UGC). Cuando se introduce UGC en un entorno de publicación que consta de varias instancias de AEM (un [conjunto de servidores de publicación](/help/communities/topologies.md)), un problema importante ha sido cómo sincronizar UGC en todas las instancias.

Con la extensión [AEM Communities 6.1](/help/communities/overview.md), este problema se resuelve mediante el uso de un [almacén común para UGC](/help/communities/working-with-srp.md). Por lo que respecta a la personalización, Communities incluye [Inicio de sesión en Social](/help/communities/social-login.md): la capacidad de proporcionar la opción para que los visitantes del sitio inicien sesión con Facebook y Twitter.

Sin la extensión de Comunidades, varios métodos para explorar para abordar el problema de la coherencia de los UGC son:

* Sincronice las varias instancias de publicación cuando sea necesario
* Envíe el UGC desde la instancia de publicación al entorno de creación, desde donde se puede publicar de forma similar a como se publica el contenido de la página

El método utilizado para lograr la coherencia UGC en un entorno de publicación que consta de varias instancias de publicación debe diseñarse y probarse cuidadosamente para comprobar el rendimiento y la coherencia.
