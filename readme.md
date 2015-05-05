#Estructura básica Front end creada en Sass. 

Estructura base que nos permite comenzar a trabajar el front-end de un proyecto de una manera rápida y agradable. No establece por defecto ningún patrón de diseño para atributos/elementos. Mini.scss, es un facilitador, te brinda una estructura profesional en pocos minutos. 

## Instalación:

* Mediante Github, tienes dos opciones: 

	1. Clonar el repositorio: 
		
		<code>$ git clone https://github.com/manuelitox/mini.scss.git</code>

	2. Descargar el paquete con la [versión 1.0](https://github.com/manuelitox/mini.scss/releases/tag/1.0) 


* Mediante Bower: 

	<code>$ bower install mini.scss</code>
	
## Cómo usarlo: 

En el directorio <code>scss/</code>, encontrarás el núcleo de mini.scss. Dicho directorio se divide en varias secciones:

* **base**: lo principal que necesitamos configurar en nuestro proyecto. Encontrarás un archivo de reseteo o ajuste para los atributos principales (párrafos, títulos, enlaces, imágenes, entre otros), donde deberás configurar el tamaño de letra, márgenes, entre otras características básicas.

* **helpers**: uno de los directorios más grandes de Mini.scss; encontrarás Funciones, Mixins, Extends y el archivo de configuración del sistema (<code>vars.scss</code>: parámetros guardados en variables: paths, colores y valores de grid).

* **modules**: en este directorio deberías agregar todos los componentes de la aplicación. El proceso de creación es muy sencillo, les he dejado en el directorio un pequeño ejemplo para que puedan ver su fácil y útil funcionamiento. Los Componentes pueden ser: formularios de registro, mensajes de alerta/error del sistema. 

* **pages**: con la finalidad de imprimir hojas de estilo livianas y que sólo tengan código requerido para la visualización correcta de cada página, he creado un directorio llamado pages. En él vamos a guardar todo lo que sea único para cada página que integre nuestro proyecto. Del mismo modo que en el directorio modules, les he dejado un pequeño ejemplo para que puedan ver su funcionamiento y su fácil ampliación.

Todas los directorios mencionados en la lista anterior a excepción de pages, se encuentran conectados a dos archivos en el directorio principal de mini.scss: **ie8.scss** y **main.scss**. Estos archivos son los que utilizará Sass al momento de procesar a CSS.

***Importante:***

Ningún archivo del directorio **pages**, debe importarse a ie8.scss o main.scss. Recuerden, la función de este directorio es separar estilos específicos que solo serán utilizados en una página, con esto conseguimos dejar en el archivo principal estilos comunes, logrando hacerlas más livianas.

En cada sub-directorio (por ejemplo: **Home**) Debe existir un archivo maestro (nombre-pagina.scss) para que Sass pueda generar un archivo único y luego, nosotros podamos llamarlo en el HTML en la página requerida.

## Soporte a SassDOC:

La documentación ya pueden encontrarla en <code>sassdoc/index.html</code>

### TODO:

* [ ] Documentación de Sistemas de grid.

## Sistemas de Grid:

¿Te gusta usar clases de ayuda en el HTML para crear tu estructura? o ¿Prefieres hacerlo internamente? Ambas opciones son posibles en Mini.scss

Por defecto, viene configurado para trabajar con un grid interno, no declarado en el HTML, mediante clases del tipo <code>.container, .col12</code>. 

### Cómo usar el Grid Interno (Soporte para Intenet Explorer >= 9):

Muy fácil, supongamos que necesitamos crear la estructura básica de un Blog:

<pre><code>.content-wrap {
	@include container();
}

.blog-posts {
	@include col(8, "two-thirds", "full");
}

aside {
	@include col(4, "one-third", "full");
}</code></pre>

Para terminar, el HTML nos quedaría de la siguiente manera:

<pre><code>div.content-wrap
	section.blog-posts
		// lista de artículos
	aside
		// contenido de aside
</code></pre>

Tenemos a disposición la siguiente serie de Mixins y Funciones que hace posible el funcionamiento del Grid Intenro:

####Mixins:

* **container()**: Sirve para generar el contenedor de nuestra estructura. El Mixin no necesita ningún parámetro.

* **col(desktop-option, tablet-option, mobile-option)**: Es utilizado para crear columnas. Recibe tres parámetros:
	
	* **desktop-option**: El número de columnas que necesitamos ocupe en Escritorio.
	
	* **tablet-option** y **mobile-option**: son opcionales. Sirven para especificar el comportamiento que tendrá la estructura en tabletas y dispositivos móviles. Los argumentos que pueden pasarse a estas dos opciones son: full (100%), half (50%), two-thirds (66.66%) y one-third (33.33%). 

* **gutter(col, type)**: margen extra para columnas. Recibe dos argumentos: col y type.
	
	* **col**: margen extra, representado en las columnas del grid, ejemplo: sí utilizamos col2 en X elemento, se le agregaría un margen lateral de 160px. El valor máximo será el número de columnas configurado en el map <code>$config-grid</code>, se encuentra en <code>scss/helpers/vars.scss</code>, por defecto 12.	 
	
	* **type**: se utiliza para especificar la posición lateral (derecha o izquierda) donde se aplicará el margen extra. Contamos con dos opciones posibles: pre (margen-left) y suf (margin-right).
	
* **inner-col(option-large, option-medium, option-small)**: genera columnas dentro de columnas. Los parámetros que recibe son *option-large*, *option-medium* y *option-small*. Valores aceptados por todas las opciones: full, half, two-thirds, one-third.
	
	*  **option-large**: para pantallas grandes (escritorios, laptops).
	
	* **option-medium**: pantallas de 6 a 10 pulgadas aproximadamente (tabletas).
	
	* **option-small**: dispositivos pequeños, hasta 5 pulgadas (celulares/dispositivos móviles).

* **inner-container()**: la misma definición de **inner-col** pero aplicado en contenedores. No recibe ningún parámetro y su ancho siempre será representado en porcentajes (100%).

* **row(position, amount)**: generar relleno vertical en los contenedores. Recibe dos parámetros: **position** y **amount**. Internamente tiene el valor **base** definido que luego se utiliza para calcular la cantidad (amount) pasada como argumento.
	
	* **position**: donde se quiere agregar el relleno, tres opciones disponibles: bottom (parte inferio), top (parte superior) o full (ambos).
	
	* **amount**: número para calcular el relleno.   
	
	* **base**: el valor base se encuentra definido dentro del Mixin. Se utiliza en conjunto con **amount** para calcular el relleno.
	
####Funciones:

Para el tratamiento de columnas:

* **calc-col-fixed(col-qty, type)**: Calcula el ancho (en pixeles) de columnas, es utilizado para pantallas grandes (Escritorios y Laptops). Recibe dos parámetros: 
	
	* **col-qty**: cantidad de columnas.
	
	* **type**: utilizado para saber cuales datos se utilizaran, normal (normales) o big (grandes). Toda la información sobre los datos de configuración del grid los encuentran en <code>scss/helpers/vars.scss</code>.  

* **calc-col-percentage(type)**: Calcula el ancho (en porcentaje) de columnas, es utilizado para dispositivos móviles (tabletas y teléfonos). Recibe un solo parámetros:
	
	* **type**: Existen cuatro opciones posibles: full (100%), half (50%), two-thirds (66.66%) y one-third (33.33%).

* **calc-gutter-extra(col-qty, col-width, gutter)**: Sirve para calcular el espacio/margen extra que se le puede aplicar a las columnas. Recibe tres parámetros:
	
	* **col-qty**: candidad de columnas.
	
	* **col-width**: ancho de columna.
	
	* **gutter**: cantidad expresada en pixeles utlilizada para agregar espacio/margen extra a las columnas. Tenemos dos valores por defecto 20px (normal) y 30px (big), puedes revisar esto al detalle en <code>scss/helpers/vars.scss</code>.

Para el tratamiento de contenedores:

* **calc-container(col-width, col-qty, gutter)**: calcular el ancho del contenedor. Recibe tres parámetros:

	* **col-width**: ancho de columna.
	
	* **col-qty**: cantidad de columnas.
	
	* **gutter**: cantidad expresada en pixeles utlilizada para agregar espacio/margen extra a las columnas. Tenemos dos valores por defecto 20px (normal) y 30px (big), puedes revisar esto al detalle en <code>scss/helpers/vars.scss</code>.

* **calc-row(base, amount)**: calcular en pixeles el relleno vertical del contenedor. Recibe dos parámetros:

	* **base**: el valor base se encuentra definido dentro del mixin. Se utiliza en conjunto con **amount** para calcular el relleno.
	
	* **amount**: número para calcular el relleno que se utilizará.

### Cómo usar el Grid basado en clases de ayuda (Soporte para Intenet Explorer >= 8):

Primeramente, debemos activarlo (Recordatorio: el Grid Interno es el que viene activo por defecto). Abrimos el archivo <code>modules/base.scss</code> y descomentamos la línea número 10: <code>@import "grid-helper-classes/base";</code> 

Al descomentar la línea, debemos ejecutar Sass para que mini.scss genere automáticamente toda la estructura necesaria para comenzar a trabajar. Vamos a realizar el mismo ejemplo de la estructura básica del Grid: 

Ya tenemos todas nuestras clases de ayuda generadas, solo debemos crear el HTML:

<pre><code>div.container
	div.col8
		section.blog-posts
			// lista de artículos
	div.col4
		aside
			// contenido de aside
</code></pre>

### Notas finales:

Los dos sistemas de Grid, pueden estar activos al mismo tiempo, pero no sería adecuado usar ambos en un mismo proyecto.

**Mini.scss** es compatible con todos los navegadores actuales y con versiones viejas de Internet Explorer (>= 8).

