---
title: Personalización
seo-title: Personalization
description: Obtenga información sobre la personalización en AEM.
seo-description: Learn about personalization in AEM.
uuid: 5790a3e0-f0ec-4785-b915-330a10dea30c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 03ebc494-8baa-4741-b8de-dac5ace743c8
exl-id: 3a550a33-b54b-4217-b9a6-b5a7971276ee
source-git-commit: d6b595b6b5477b5cad662e219f1abd483491897f
workflow-type: tm+mt
source-wordcount: '1686'
ht-degree: 16%

---

# Personalización {#personalization}

## ¿Qué es la personalización? {#what-is-personalization}

Actualmente hay un volumen cada vez mayor de contenido disponible, ya sea en sitios web de Internet, extranet o intranet.

La personalización se centra en proporcionar al usuario un entorno personalizado que muestre el contenido dinámico seleccionado según sus necesidades específicas; esto se debe a perfiles predefinidos, selección de usuarios o comportamiento interactivo del usuario.

Hay tres elementos principales involucrados en la personalización:

### Usuarios {#users}

* Tienen perfiles, individuales y de grupo. Estos perfiles contienen características (como la descripción del trabajo, la ubicación, los intereses) que se pueden utilizar para personalizar el contenido que pueden ver.
* Realice acciones. Después, se pueden analizar y comparar con las reglas de comportamiento para adaptar el contenido que ven.

### Contenido {#content}

* Es lo que el usuario quiere ver. Preferiblemente contenido de interés, y uso, para ellos para el cumplimiento de sus tareas.
* Se puede categorizar y, por lo tanto, ponerlo a disposición de los usuarios según las reglas predefinidas.
* Debe ser dinámico.

En otras palabras, el contenido debe, de alguna manera, depender del usuario. Si todos los usuarios ven el mismo contenido, la personalización es redundante.

### Reglas {#rules}

* Defina cómo se produce realmente la personalización: qué contenido puede ver el usuario y cuándo.

La personalización puede ser:

#### Explícita {#explicit}

* Personalización: mediante el cual el usuario realiza selecciones entre una selección de fuentes de contenido.

#### Implicit {#implicit}

* Reglas basadas en: los administradores de negocio definen reglas específicas para acciones basadas en perfiles o comportamientos específicos.
* Filtro simple: las selecciones se realizan en función de perfiles predefinidos a nivel de usuario o grupo.
* Filtrado colaborativo/de recomendaciones: el comportamiento del usuario se registra según las reglas predefinidas. Estas reglas se basan en el comportamiento observado con personas con ideas afines. La información recopilada se utiliza para adaptar la información mostrada al usuario, especialmente en forma de recomendaciones.

## ¿Cómo y cuándo se puede utilizar la personalización? {#how-and-when-can-personalization-be-used}

La personalización se puede utilizar en muchos casos, por ejemplo:

### Páginas de Intranet {#intranet-pages}

* El contenido se puede ofrecer en función de la ubicación, el departamento o la función de un usuario (ya definido dentro de una red interna).
* Según la opción disponible, el usuario puede realizar más selecciones.

### Grupos de usuarios específicos, limitados y de destino: Extranets {#extranets}

* Los usuarios requieren un inicio de sesión para la autorización; se vinculará a un perfil que proporcione la información necesaria para la personalización; posiblemente detalles como su ubicación, relación con el producto, historial de uso, responsabilidades de presupuesto, etc.
* Estas instancias pueden abarcar sitios como:
* Empresas que proporcionan sitios web a una sección altamente especializada de su mercado, por ejemplo una empresa farmacéutica que proporciona un sitio web especializado para médicos.
* Empresas que proporcionan sitios web que permiten a sus clientes ver la información de cuenta corriente y de facturación; por ejemplo, proveedores de teléfono.

### Sitio Web de ventas y distribución {#sales-site}

* Los sitios web de ventas y distribución, como Amazon, pueden combinar un perfil de usuario, el historial de ventas del usuario y su historial de navegación para realizar sugerencias sobre lo que podría interesar al siguiente usuario.

### Buscar sitios web {#search-site}

* Muchos de los principales sitios web de motores de búsqueda tienen poderosas herramientas analíticas que registran el comportamiento de los usuarios, los términos de búsqueda que utilizan y los sitios web que visitan. A continuación, se utiliza para personalizar el contenido proporcionado, especialmente con respecto a la visualización de anuncios.

### Puntos fuertes de la personalización y puntos a tener en cuenta {#strengths-of-personalization-and-points-to-consider}

A continuación se indican los motivos por los que se debe utilizar la personalización:

* Un usuario puede experimentar un sitio web cómodo y centrado.
* La personalización puede utilizarse para propagar automáticamente el acceso a la última versión del contenido.
* Las funciones de colaboración social están disponibles para que los usuarios se comuniquen entre sí, ya que se pueden identificar mediante sus perfiles.
* Se puede proporcionar al usuario el contenido que necesita para realizar una tarea determinada. Dentro de la intranet de una empresa, esto puede proporcionar una herramienta inestimable para difundir información.
* Se puede proporcionar al usuario el contenido que necesita o desea, lo que reduce el tiempo necesario para realizar operaciones de búsqueda.
* El proveedor de contenido puede dirigir el contenido para que lo vean categorías específicas de usuarios.
* Las reglas se pueden definir para ofrecer contenido en función de combinaciones de características de usuario y comportamiento. Esto proporciona un mecanismo sofisticado para personalizar su experiencia web.

Al utilizar la personalización, tenga en cuenta lo siguiente:

#### Actuación {#performance}

* Naturalmente, el análisis y la evaluación adicionales repercuten en el rendimiento. Sin embargo, los métodos utilizados son muy sofisticados y se pueden optimizar para minimizar el impacto.

#### Autorización {#authorization}

* La personalización requiere un mecanismo de inicio de sesión, ya que el sitio web debe poder identificar al usuario.

#### Almacenamiento en caché {#caching}

* El almacenamiento en caché es un aspecto que el usuario verá en términos de rendimiento y precisión: ¿con qué rapidez ofrece el sitio web contenido personalizado y siempre está actualizado?
* El almacenamiento en caché es una consideración clave al configurar la personalización y se debe tomar un tiempo para garantizar que se utiliza la implementación correcta.

>[!TIP]
>
>El efecto de la personalización en los temas de rendimiento y almacenamiento en caché relacionados se discuten más en el documento [Optimización del rendimiento.](/help/sites-deploying/configuring-performance.md)

#### Precisión de las reglas {#accuracy}

* La personalización realizada mediante el seguimiento del comportamiento del usuario o la configuración de reglas basadas en el perfil del usuario debe ser precisa y lógica.
* No hay nada más frustrante para el usuario que tener contenido forzado o denegado debido a la lógica inexacta de una regla.
* Por lo tanto, las reglas deben estar bien pensadas, con los requisitos del usuario en primer plano. Esto puede requerir mucho esfuerzo y no debe subestimarse; la definición de las reglas comerciales suele superar el esfuerzo técnico al implementar la personalización.

#### Cuándo se utiliza {#when-to-use}

* Al igual que muchas funciones de la web, la personalización debe utilizarse con cuidado. ¿Beneficiará realmente su uso al usuario? siempre debe ser la primera consideración -o si el objetivo deseado se puede lograr con menos esfuerzo por otro método-. La personalización puede correr el riesgo de ser una función que los usuarios configuren una vez (para ver cómo funciona) y solo una vez, ya que no les ofrece ninguna ventaja real.
* La personalización solo es significativa cuando el contenido es dinámico, y depende del usuario de alguna manera. Si todos los usuarios ven el mismo contenido, la personalización es redundante.

#### Confidencialidad {#confidentiality}

* Muchos usuarios están preocupados por la protección y seguridad de los datos. En particular, con respecto a los datos recuperados al rastrear su comportamiento al navegar por la web.

## Personalización y acceso {#personalization-and-access}

La personalización debe considerarse por separado del control de acceso, pero está interrelacionada.

La personalización en sí no crea ninguna forma de control de acceso. Es simplemente un método de dirección de lo que el usuario ve; no restringe el acceso del usuario a otro contenido y, como con cualquier contenido, debe tener ya asignados los controles de acceso correctos.

Sin embargo, el control de acceso se puede utilizar para crear una forma de personalización. Si permite o deniega a un usuario el acceso al contenido, esto inevitablemente afecta a la elección del contenido que tiene disponible, personalizando así su experiencia web.

## Componentes disponibles para personalización {#components-available-for-personalization}

Se proporcionan varios componentes con AEM para la personalización. Algunos permiten a los usuarios iniciar sesión y editar sus perfiles, otros (como My Gadgets) permiten a los usuarios configurar una página específica:

| Título en la barra de tareas | Función |
|---|---|
| Campo de contraseña activado | Solicita una contraseña y la confirmación de la misma. |
| Inicio de sesión combinado | Permite que el usuario inicie sesión en una cuenta existente o que se registre para una nueva cuenta. |
| Campo de dirección de Forms | Campo complejo que permite la introducción de una dirección internacional. |
| Inicio de Forms | Inicia una definición de formulario |
| Forms Captcha | Campo que consta de una palabra alfanumérica que se actualiza automáticamente. El componente captcha protege a los sitios web de los robots. |
| Grupo de casillas de verificación de Forms | Varios elementos organizados en una lista y precedidos por casillas de verificación. Los usuarios pueden activar varias casillas de verificación. |
| Lista desplegable de Forms | Varios elementos organizados en una lista desplegable. El conmutador Selección múltiple especifica si se pueden seleccionar varios elementos de la lista. |
| Forms End | Finaliza la definición del formulario. |
| Carga de archivos de Forms | Elemento de carga que permite al usuario cargar un archivo en el servidor. |
| Campo oculto de Forms | Este campo no se muestra al usuario. Se puede emplear para transportar un valor al cliente y devolverlo al servidor. Este campo no debe tener restricciones. |
| Botón Imagen de Forms | Botón de envío adicional para el formulario que se procesa como imagen. |
| Campo de contraseña de Forms | Igual que un campo de texto pero solo se permite una sola línea y la introducción de texto por parte del usuario no está visible en el campo. |
| Grupo de radio de Forms | Varios elementos organizados en una lista y precedidos por un botón de opción. Los usuarios deben seleccionar únicamente un botón de opción. |
| Botón de envío de Forms | Botón de envío adicional para el formulario donde el título se muestra como texto en el botón. |
| Campo de texto de Forms | Campo de texto que permite a los usuarios introducir información. |
| My Gadgets | Permite incluir uno de una selección de gadgets disponibles. |
| Fotografía de avatar de perfil | Permite la introducción de una fotografía de avatar. |
| Nombre detallado de perfil | Introducción de la información de nombre, incluyendo elementos como título, segundo nombre y sufijo, si es necesario. |
| Nombre para mostrar en el perfil | Nombre para mostrar. |
| Correo electrónico del perfil | Introducción de una dirección de correo electrónico. |
| Género de perfil | Permite la introducción del género. |
| Número de teléfono principal del perfil | Permite la introducción de un número de teléfono. |
| URL principal del perfil | Permite la introducción de una dirección URL. |
| Propiedad Texto general de perfil | Propiedades del perfil. |
| Inicio de sesión | Permite enviar un nombre de usuario y una contraseña al iniciar sesión. |
| Cerrar sesión | Indica el usuario que ha iniciado sesión y le proporciona un vínculo para cerrar la sesión. |
| Nube de etiquetas | Una nube de etiquetas para mostrar una selección de etiquetas presentada gráficamente dentro del sitio web |
| Teaser | Parte de contenido (normalmente una imagen) que se muestra en una página principal para &quot;provocar&quot; que los usuarios accedan al contenido subyacente. |

## Personalización y contenido de la comunidad {#personalization-and-community-content}

Las funciones de la comunidad como blogs, foros y calendarios dan como resultado la creación de contenido de la comunidad, comúnmente denominado contenido generado por el usuario (UGC). Cuando se introduce UGC en un entorno de publicación que consta de varias instancias de AEM (una [publicar granja](/help/communities/topologies.md)), un problema importante ha sido cómo sincronizar UGC en todas las instancias.

con [AEM Communities 6.1](/help/communities/overview.md) extensión, este problema se resuelve usando una [almacén común para UGC](/help/communities/working-with-srp.md). Por lo que se refiere a la personalización, las Comunidades incluyen [Inicio de sesión en Social](/help/communities/social-login.md) : la capacidad de proporcionar la opción para que los visitantes del sitio inicien sesión con Facebook y Twitter.

Sin la extensión de Communities, varios métodos a explorar para abordar el problema de la coherencia UGC son:

* Sincronice las distintas instancias de publicación cuando sea necesario
* Envíe el UGC desde la instancia de publicación al entorno de creación, desde donde se puede publicar de forma similar a la publicación del contenido de la página

El método utilizado para lograr la coherencia UGC en un entorno de publicación que consta de varias instancias de publicación debe diseñarse y probarse cuidadosamente por su rendimiento y coherencia.
