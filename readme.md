#Estructura básica Front end creada en Sass. 

Ligera librería que agrupa un conjunto de buenas prácticas que nos permiten comenzar a trabajar de una manera correcta en cualquier Aplicación o Sitio Web.

## Instalación:

* Mediante Github, tienes dos opciones: 

	1. Clonar el repositorio: 
		
		<code>$ git clone https://github.com/manuelitox/mini.scss.git</code>

	2. Descargar el paquete con la [versión 0.6](https://github.com/manuelitox/mini.scss/releases/tag/0.6) 


* Mediante Bower: 

	<code>$ bower install mini.scss</code>
	
## Cómo usarlo: 

En el directorio scss/, encontrarás el núcleo de mini.scss. Dicho directorio se divide en varias secciones:

* **base**: lo principal que necesitamos configurar en nuestra estructura de proyecto. Encontrarás un archivo de reseteo o ajuste para los atributos principales (párrafos, títulos, enlaces, imágenes, entre otros), donde deberás configurar el tamaño de letra, márgenes, entre otras cosas básicas.

* **helpers**: uno de los directorios más grandes de mini.scss; encontrarás las funciones, mixins, extends, clases de ayuda y el archivo de configuración del sistema (parámetros guardados en variables: breakpoints, media queries, paths, colores, entre otros).

* **modules**: para que el front end de nuestro proyecto sea lo más modular posible, he dispuesto un directorio para guardar los componentes que vayamos agregando. El proceso de creación de un módulo (componente) es muy sencillo, les he dejado en el directorio un pequeño ejemplo para que puedan ver su funcionamiento.

* **pages**: con la finalidad de imprimir hojas de estilo livianas y que sólo tengan código requerido para la visualización correcta de cada página, he creado un directorio llamado pages. En él vamos a guardar todo lo que sea único para cada página que integre nuestro proyecto. Del mismo modo que en el directorio modules, les he dejado un pequeño ejemplo para que puedan ver su funcionamiento y su fácil ampliación.

Todas los directorios mencionados en la lista anterior a excepción de pages, se encuentran conectados a dos archivos en el directorio principal de mini.scss: **ie.scss** y **main.scss**. Estos archivos son los que utilizará Sass al momento de convertir nuestro trabajo a CSS.

Ningún archivo del directorio **pages**, debe importarse o conectarse a ie.scss y main.scss. Recuerden, la función de este directorio es separar estilos específicos que solo serán utilizados en una página y así no cargar nuestra hoja de estilo principal con código extra, con este modelo de trabajo logramos hacerlas más livianas y leíbles. En cada sub-directorio (por ejemplo: **Home**) Debe existir un archivo maestro (nombre-pagina.scss) para que Sass pueda generar un archivo único y luego, nosotros podamos llamarlo en el HTML en la página requerida.

## Sistemas de Grid:

¿Te gusta usar clases de ayuda en el HTML para crear tu estructura? o ¿Prefieres hacerlo internamente? Ambas opciones son posibles con mini.scss

Por defecto, viene configurado para trabajar con un grid interno, no declarado en el HTML mediante clases del tipo <code>.container, .col12</code>. 

### Cómo usar el Grid Interno:

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

Usamos dos Mixins: **container** y **col**

* **container()**: Sirve para generar el contenedor de nuestra estructura. El Mixin no necesita ningún parámetro.

* **col(desktop-option, tablet-option, mobile-option)**: Es utilizado para crear cada columna. Recibe tres parámetros:
	
	* **desktop-option**: El número de columnas que necesitamos ocupe en Escritorio.
	
	* **tablet-option** y **mobile-option**: son opcionales. Sirven para especificar el comportamiento que tendrá la estructura en tabletas y dispositivos móviles. Los argumentos que pueden pasarse a estas dos opciones son: full, half, two-thirds y one-third. 
	
Para terminar, el HTML nos quedaría de la siguiente manera:

<pre><code>div.content-wrap
	section.blog-posts
		// lista de artículos
	aside
		// contenido de aside
</code></pre>

## Cómo usar el Grid basado en clases de ayuda:

Primeramente, debemos activarlo. Abrimos el archivo <code>modules/base.scss</code> y descomentamos la línea número 10: <code>@import "grid-helper-classes/base";</code> 

Al descomentar la línea, debemos ejecutar Sass para que mini.scss genere automáticamente toda la estructura necesaria para comenzar a trabajar con él. Vamos a realizar el mismo ejemplo de la estructura básica del Grid: 

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

Los dos sistemas de Grid, pueden estar activos al mismo tiempo, pero no sería una buena practica usar ambos en un mismo proyecto.

**Mini.scss** es compatible con todos los navegadores actuales y con versiones viejas de Internet Explorer (>= 8).

