---
title: Active Directory, Donde Los Hackers Se Divierten - Parte 1
description: Introduccion a Active Directory
excerpt:
  ¿Alguna vez te has preguntado qué pasaría si tu red corporativa fuera una fiesta y el Active Directory el portero?
  Prepárate para descubrirlo
datetime: 2024-05-06T05:35:07.000+00:00
featured: true
category: What is ?
author: Nicolas Gula
type: article
coverImage:  https://jumpcloud.com/wp-content/uploads/2016/07/AD1.png
coverImageAlt: Microsoft AD
coverImageWidth: "2725"
coverImageHeight: "1400"
ogImage: "/assets/blog/hello-world/cover.jpg"
ogImageAlt: something
language: "Spanish"
---


## Por que hablar de Active Directory? 🧐

Active Directory (AD) es como el director de una empresa: organiza y gestiona todos los recursos importantes, como usuarios, computadoras y archivos compartidos, en una estructura jerárquica. Sin embargo, tiene algunas debilidades que los hackers aprovechan para obtener acceso no autorizado. Incluso una cuenta básica de usuario puede acceder a mucha información, lo que hace que proteger adecuadamente Active Directory sea crucial.

![AD Estructura](https://i0.wp.com/dbaontap.com/wp-content/uploads/2016/08/Active-Directory.gif?ssl=1)

Muchas empresas grandes, incluidas casi todas las de Fortune 500, lo utilizan, lo que lo convierte en un objetivo atractivo para los atacantes. Un ataque exitoso podría darles acceso a toda la red, lo que es bastante aterrador. Estos ataques explotan fallas en Active Directory para escalar privilegios y moverse por la red. Por lo tanto, es crucial entender cómo funciona Active Directory para protegerlo mejor.

En resumen, Active Directory es como el núcleo de una empresa, y comprenderlo es esencial para protegerse contra ataques cibernéticos. Por eso, el motivo de este post.

## Contexto 🎬

La historia del AD se remonta a hace décadas, cuando se introdujo por primera vez como parte de los sistemas operativos de Windows. Desde entonces, ha evolucionado enormemente para convertirse en una herramienta fundamental para la gestión de recursos en redes empresariales.

Active Directory comenzó como un proyecto de Microsoft para proporcionar servicios de directorio en los sistemas operativos Windows. A lo largo de los años, ha experimentado varias mejoras y adiciones de características para mejorar su funcionalidad y seguridad.

Uno de los hitos importantes fue su inclusión en Windows Server 2000, lo que lo convirtió en una parte integral del ecosistema de Windows. Desde entonces, ha continuado creciendo y adaptándose a medida que cambian las necesidades de las organizaciones y las tecnologías emergentes.

Con características como la Forest, que permite una administración más flexible de los recursos, y los Servicios de Federación de Active Directory (ADFS), que facilitan el inicio de sesión único para los usuarios, Active Directory ha demostrado ser una herramienta versátil y poderosa para las empresas.

Sin embargo, no está exento de problemas. Desde su introducción, Active Directory ha sido objeto de ataques y vulnerabilidades, lo que ha llevado a la necesidad constante de parches y actualizaciones de seguridad.

Para los profesionales de la seguridad informática, comprender en profundidad Active Directory es esencial. No solo es una herramienta fundamental en muchas empresas, sino que también es un objetivo común para los atacantes. Por lo tanto, entender su estructura, funcionamiento y posibles vulnerabilidades es crucial para proteger eficazmente las redes empresariales.

## Estructura 🧠

Active Directory es como el cerebro detrás de una red de Windows, que organiza y controla todos los recursos importantes, como usuarios, computadoras y archivos compartidos, en una estructura jerárquica. Esencialmente, es como el sistema de archivos de una empresa, pero en lugar de guardar archivos, guarda información sobre usuarios, contraseñas y configuraciones de red.

Lo más importante a tener en cuenta sobre Active Directory es que proporciona funciones de autenticación y autorización dentro de una red de Windows. Esto significa que gestiona quién tiene acceso a qué recursos en la red. Sin embargo, tiene sus debilidades: muchas de sus funciones no son seguras por defecto y pueden ser configuradas incorrectamente, lo que hace que sea más fácil para los hackers infiltrarse en la red.

Los problemas y configuraciones incorrectas de Active Directory pueden ser explotados por los hackers para obtener acceso no autorizado a recursos protegidos en la red, como bases de datos y archivos compartidos. Incluso una cuenta de usuario básica puede ser utilizada para ver información dentro de Active Directory, lo que resalta la importancia de proteger adecuadamente esta herramienta.

Para entender cómo proteger Active Directory, primero necesitas comprender cómo está organizado. Está estructurado como un árbol jerárquico, con un "bosque"(FOREST) en la parte superior que contiene uno o más "dominios". Cada dominio puede tener subdominios, y dentro de estos dominios y subdominios, hay unidades organizativas (OU) que permiten una administración más específica de los recursos.

![Forest and Domains](https://servergeeks.wordpress.com/wp-content/uploads/2012/10/ad-1.jpg)

Aqui podriamos decir que sheik.com es el dominio raiz y contiene los subdominios us.sheik.com y uk.sheikh.com asi como demas objetos que conforman un dominio, como usuarios, grupos, computadoras, OU (Organizational Units).

En organizaciones con múltiples dominios o bosques, es común establecer relaciones de confianza entre ellos para facilitar el acceso a los recursos. Sin embargo, estas relaciones pueden introducir problemas de seguridad si no se administran correctamente. Por ejemplo, en el gráfico se muestra una relación de confianza bidireccional entre los bosques __sheikh.com__ y __habib.com__. Esto permite que los usuarios en un bosque accedan a recursos en el otro bosque.

Aunque los dominios raíz confían en los dominios secundarios en sus respectivos bosques, los dominios secundarios no necesariamente confían en los dominios secundarios en el otro bosque. Por lo tanto, para permitir la comunicación directa entre ciertos dominios secundarios, puede ser necesario crear relaciones de confianza adicionales.

![Active Dorectory Forests & Domains](https://s38063.pcdn.co/wp-content/uploads/2022/06/Active-Directory-forest-.jpg)

## Glosario...in inglsih 😉

### Attributes
En Active Directory, cada objeto tiene características específicas definidas por atributos. Por ejemplo, un objeto de computadora tiene atributos como el nombre de host y el nombre DNS. Estos atributos se utilizan para identificar y organizar los objetos dentro de AD. Cada atributo tiene un nombre único, conocido como nombre LDAP, que se utiliza para consultas y acceso a la información. Por ejemplo, el atributo __"displayName"__ se usa para el nombre completo de un usuario y __"givenName"__ para el nombre de pila.

![Attributes](https://www.windows-active-directory.com/wp-content/uploads/2021/07/attribute-editor-2.png)

### Access Control Entries (ACE)
Cada Entrada de Control de Acceso (ACE) en una Lista de Control de Acceso (ACL) identifica a un administrador, ya sea una cuenta de usuario, una cuenta de grupo o una sesión de inicio de sesión. Esta entrada enumera los derechos de acceso que se permiten, se deniegan o se auditan para ese administrador en relación con el objeto al que se aplica la ACL. En pocas palabras, un ACE especifica quién puede hacer qué con un objeto en Active Directory.

![ACE](https://techcommunity.microsoft.com/t5/image/serverpage/image-id/49175i9B083F7E84DF9978)

### Access Control List (ACL)
Una Lista de Control de Acceso (ACL) en AD es básicamente una lista ordenada de Entradas de Control de Acceso(ACE). Estas entradas determinan quién puede acceder o realizar acciones específicas en un objeto dentro de AD. Por ejemplo, una ACL puede especificar quién puede leer, modificar o eliminar un usuario en el directorio. Cada ACE en la lista describe los permisos concedidos o denegados a un usuario o grupo específico en relación con ese objeto.

### Active Directory Users and Computers (ADUC)
Consola GUI(Graphical User Interface) que se usa comúnmente para administrar usuarios, grupos, computadoras y contactos en AD.

![ADUC](https://cdn-blog.netwrix.com/wp-content/uploads/2023/07/01-1024x434.webp)

### adminCount
El atributo "adminCount" en Active Directory indica si un usuario está protegido por el proceso SDProp. Un valor de 0 o no especificado significa que el usuario no está protegido, mientras que otro valor indica que lo está. Los atacantes suelen buscar cuentas con "adminCount" establecido en 1, ya que suelen ser cuentas privilegiadas que podrían comprometer todo el dominio.

![Admin Count](https://specopssoft.com/wp-content/uploads/2018/09/Check-the-adminCount-attribute.png)

### AdminSDHolder
El objeto AdminSDHolder en Active Directory administra las Listas de Control de Acceso (ACL) para los miembros de ciertos grupos privilegiados. Este objeto actúa como un contenedor para los permisos aplicados a estos grupos. Un proceso llamado SDProp se encarga de aplicar las ACL correctas a los miembros de estos grupos protegidos. Por defecto, este proceso se ejecuta cada hora.

![AdminSDHolder](https://adsecurity.org/wp-content/uploads/2015/09/SneakyADPersistence-AdminSDProp-AdminSDHolder-ADObject.jpg)

### AD Recycle Bin
La Papelera de Reciclaje de AD simplifica la recuperación de objetos eliminados. Con ella, los administradores pueden restaurar objetos sin necesidad de recurrir a copias de seguridad. Los objetos eliminados se conservan durante un período configurable (predeterminado: 60 días), y la mayoría de sus atributos se mantienen, facilitando su restauración completa.

### ADSI Edit
ADSI Edit es una herramienta gráfica para administrar objetos en Active Directory. Es más poderosa que otras herramientas y permite ajustes detallados en los atributos de los objetos, así como agregar, eliminar y mover objetos. Sin embargo, su uso requiere precaución, ya que los cambios incorrectos pueden causar problemas graves en Active Directory.

![ADSI Edit](https://redmondmag.com/articles/2017/08/22/~/media/ECG/redmondmag/Images/2017/08/ADSIEdit_Fig4.ashx)

### Container
Los objetos contenedores contienen otros objetos y tienen un lugar definido en la jerarquía del subárbol de directorios. 

### Domain
Un dominio es un conjunto de objetos, como computadoras y usuarios, organizados de forma lógica. Puedes imaginarlos como ciudades dentro de un país, operando de forma independiente o conectadas mediante relaciones de confianza.

![Domain](https://media.licdn.com/dms/image/D5612AQHvwZvZdNGR8w/article-cover_image-shrink_600_2000/0/1690909350900?e=2147483647&v=beta&t=tlqLSiPKJQkfQ4QlEEANB5A3VluZEM-ZeP99PyEtNpw)

### Distinguished Name (DN)
Un Nombre Distinguido (DN) es la dirección completa de un objeto en Active Directory, como una dirección postal. 
![DN](https://jumpcloud.com//wp-content/uploads/2022/11/1.gif)

### Discretionary Access Control List (DACL)
Las DACL son como la seguridad de una puerta con una lista de personas permitidas o denegadas. Si un objeto tiene una lista, el sistema verifica si un usuario está en ella para decidir si le da acceso. Si no hay lista, el acceso es abierto para todos; si la lista está vacía, se niega el acceso a todos. El sistema revisa la lista de arriba a abajo hasta encontrar una coincidencia o negación.

### dsHeuristics
El atributo "dsHeuristics" es como una caja de herramientas para ajustar la configuración en un bosque de Active Directory. Una de sus funciones es excluir grupos de una lista especial llamada "Grupos protegidos". Si un grupo está excluido, los cambios en él no se desharán automáticamente cuando se ejecute un proceso de seguridad.
![DSHEURISTICS](https://dirteam.com/legacy/sander/DSHeuristics_6B9A22CC.png)

### Forest
Un Forest en AD es como un país que contiene ciudades (Domains). Tiene todos los objetos AD, como usuarios y computadoras. Cada bosque funciona independientemente, pero puede conectarse con otros bosques a través de relaciones de confianza, al igual que países vecinos pueden tener relaciones.

### FSMO Roles
En los primeros días de Active Directory (AD), surgieron problemas con múltiples controladores de dominio (DC) compitiendo por realizar cambios, lo que causaba inconsistencias. Microsoft introdujo los roles de Operación Maestra Única Flexible (FSMO) para resolver este problema. Estos roles asignan responsabilidades específicas a los DC, como administrar el esquema, el nombre del dominio y la asignación de identificadores únicos. Hay cinco roles FSMO: Schema Mastery Domain Naming Master(uno de cada por bosque), Relative ID (RID) Master(uno por dominio), Primary Domain Controller (PDC) Emulator(uno por dominio), y Infrastructure Master(uno por dominio), y se asignan al primer DC en el dominio raíz del bosque. Esto ayuda a garantizar una replicación fluida en AD y el funcionamiento adecuado de los servicios críticos.

### Global Catalog
Un catálogo global (GC) almacena copias de todos los objetos en un bosque de Active Directory, permitiendo a los usuarios y aplicaciones buscar información sobre cualquier objeto en cualquier dominio del bosque. Además de almacenar una copia completa de los objetos del dominio actual, también contiene copias parciales de objetos de otros dominios del bosque. Las funciones principales del GC incluyen la autenticación de usuarios y la búsqueda de objetos en todo el bosque.
![GC](https://networkencyclopedia.com/wp-content/uploads/2019/08/global-catalog-active-directory-infrastructure.jpg)

### Global Unique Identifier (GUID)
Un GUID es un identificador único de 128 bits asignado a cada objeto creado en Active Directory. Este valor único se almacena en el atributo ObjectGUID. Buscar objetos en Active Directory por su GUID es la forma más precisa de encontrarlos, ya que no cambia y es único en toda la empresa. Utilizar el ObjectGUID asegura resultados precisos al buscar información sobre un objeto específico en AD.

![GUID](https://files.readme.io/cbc0567-dfdf8c9-2019-09-17_22_17_08-Amazon_WorkSpaces.png)

### Group Policy Object (GPO)
Los GPO son conjuntos de configuraciones de políticas en Active Directory con un GUID único. Pueden incluir ajustes del sistema de archivos local o de AD y se aplican a usuarios o computadoras. Pueden aplicarse a todo el dominio o a unidades organizativas específicas para controlar la configuración de seguridad y otros aspectos del entorno.

### Leaf
Los objetos hoja no contienen otros objetos y se encuentran al final de la jerarquía del subárbol. 

### NTDS.DIT
El archivo NTDS.DIT es esencial en Active Directory, almacenando datos cruciales como información de usuario, membresía de grupos y, lo más importante, los hashes de contraseñas. Esto lo convierte en un objetivo valioso para los atacantes, ya que pueden extraer los hashes y usarlos para ataques de paso de hash. Si la configuración adecuada está habilitada, también puede contener contraseñas de texto sin cifrar.

### Object
Un objeto se puede definir como CUALQUIER recurso presente dentro de un entorno de Active Directory, como unidades organizativas, impresoras, usuarios, controladores de dominio, etc. 

### Relative Distinguished Name (RDN)
Un nombre distinguido relativo (RDN) es una parte única del nombre de un objeto en Active Directory que lo distingue de otros objetos en el mismo nivel de la jerarquía. 
![RDN](https://i0.wp.com/wentzwu.com/wp-content/uploads/2021/11/DistinguishedNamesandRelativeDistinguishedNames.jpg?ssl=1)

### Read-Only Domain Controller (RODC)
Un controlador de dominio de solo lectura (RODC) tiene una base de datos de Active Directory que solo se puede leer. No almacena contraseñas de usuarios y no permite cambios en la base de datos AD, SYSVOL o DNS. Los RODC ayudan a reducir el tráfico de replicación, separar roles de administrador y proteger el entorno al evitar la replicación de modificaciones no autorizadas.

### Replication
La replicación ocurre en AD cuando los objetos AD se actualizan y transfieren de un controlador de dominio a otro. Cada vez que se agrega un controlador de dominio, se crean objetos de conexión para administrar la replicación entre ellos. Estas conexiones las realiza el servicio Knowledge Consistency Checker (KCC), que está presente en todos los DC. La replicación garantiza que los cambios se sincronicen con todos los demás controladores de dominio en un bosque, lo que ayuda a crear una copia de seguridad en caso de que falle un controlador de dominio. 

### Schema
El Schema de Active Directory define qué tipos de objetos pueden existir en la base de datos de AD y qué información pueden contener. Por ejemplo, define que un usuario puede tener un nombre, una dirección de correo electrónico, etc. Cada objeto en AD se crea a partir de una clase en el esquema, como "usuario" o "computadora", y tiene atributos asociados que definen su información específica. Esto ayuda a organizar y estructurar la información en AD de manera coherente.

### Tree
Un Tree(Arbol) en Active Directory comienza con un Source Domain y puede incluir varios dominios secundarios. Un Forest(Bosque) es una colección de Trees AD. Cada Doamin en un Tree comparte límites con otros Domains y forma relaciones de confianza. Dos Trees en el mismo Forest no pueden tener el mismo nombre. Los Doamins en un Tree comparten un catálogo global que contiene información sobre los objetos del Tree.


## Objetos del AD 🧿

![Objects](https://www.edrawsoft.com/solutions/shapes/active-directory.png)

### **Users**
Son entidades de seguridad en Active Directory con atributos como nombre, dirección de correo electrónico, etc. Son objetivos importantes para los atacantes debido a sus privilegios.

### **Groups** 
Contenedores que pueden incluir usuarios, computadoras u otros grupos. Se utilizan para administrar permisos y accesos de manera eficiente.

### **Organizational Units (OU)**
Contenedores para organizar objetos similares y facilitar la administración. Se usan para delegar tareas administrativas sin otorgar permisos completos.

### **Domains**
Estructura de una red AD que contiene objetos como usuarios y computadoras. Cada dominio tiene su propia base de datos y políticas.

### **Domain Controllers**
Manejan la autenticación, verificación de usuarios y aplican políticas de seguridad en una red AD.

### **Sites**
Conjunto de computadoras en una o más subredes conectadas para una replicación eficiente.

### **Foreign Security Principles (FSP)**
Representan entidades de seguridad de bosques externos en AD, creados cuando se agrega un objeto externo a un grupo en un dominio actual. Se utilizan para resolver nombres a través de relaciones de confianza.


## Relaciones de confianza 🤔

Una relación de confianza (Trusts) permite la autenticación entre dominios, facilitando el acceso a recursos en diferentes partes de una red. Hay varios tipos:

1. Parent-child: Para dominios dentro del mismo bosque. La confianza es bidireccional y transitiva entre el dominio principal y los secundarios.
2. Cross-link: Entre dominios secundarios para agilizar la autenticación.
3. External: No transitiva, conecta dominios en bosques separados. Utiliza filtrado SID.
4. Tree-root: Transitiva y bidireccional, entre un dominio raíz de bosque y un nuevo dominio raíz de árbol.
5. Forest: Transitiva entre dos dominios raíz de bosque.

![Trusts](https://academy.hackthebox.com/storage/modules/74/trusts-diagram.png)

Ufff.... tuvo larga esta introduccion😮‍💨. Aun falta mas, asi que de momento lo dejo por aca y armo una segunda parte.

### Fuentes:

- [https://jumpcloud.com/](https://jumpcloud.com/)  

- [https://dbaontap.com/](https://dbaontap.com/)  

- [https://servergeeks.wordpress.com/](https://servergeeks.wordpress.com/)  

- [https://s38063.pcdn.co/](https://s38063.pcdn.co/)  

- [https://www.windows-active-directory.com/](https://www.windows-active-directory.com/)  

- [https://techcommunity.microsoft.com/](https://techcommunity.microsoft.com/)  

- [https://cdn-blog.netwrix.com/](https://cdn-blog.netwrix.com/)  

- [https://specopssoft.com/](https://specopssoft.com/)  

- [https://adsecurity.org/](https://adsecurity.org/) 

- [https://redmondmag.com/Home.aspx](https://redmondmag.com/Home.aspx)  

- [https://dirteam.com/](https://dirteam.com/)  

- [https://networkencyclopedia.com/](https://networkencyclopedia.com/)  

- [https://www.edrawsoft.com/](https://www.edrawsoft.com/)  

- [https://academy.hackthebox.com/](https://academy.hackthebox.com/)

