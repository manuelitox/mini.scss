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

* **base**: lo principal que necesitamos configurar en nuestra estructura de proyecto. Encontrarás el archivo para generar el grid y un archivo de reseteo o ajuste para los atributos principales (párrafos, títulos, enlaces, imágenes, entre otros), donde deberás configurar el tamaño de letra, márgenes, entre otras cosas básicas.

* **helpers**: uno de los directorios más grandes de mini.scss; encontrarás las funciones, mixins, extends, clases de ayuda y el archivo de configuración del sistema (parámetros guardados en variables: breakpoints, media queries, paths, colores, entre otros).

* **modules**: para que el front end de nuestro proyecto sea lo más modular posible, he dispuesto un directorio para guardar los componentes que vayamos agregando. El proceso de creación de un módulo (componente) es muy sencillo, les he dejado en el directorio un pequeño ejemplo para que puedan ver su funcionamiento.

* **pages**: con la finalidad de imprimir hojas de estilo livianas y que sólo tengan código requerido para la visualización correcta de cada página, he creado un directorio llamado pages. En él vamos a guardar todo lo que sea único para cada página que integre nuestro proyecto. Del mismo modo que en el directorio modules, les he dejado un pequeño ejemplo para que puedan ver su funcionamiento y su fácil ampliación.

Todas los directorios mencionados en la lista anterior a excepción de pages, se encuentran conectados a dos archivos en el directorio principal de mini.scss: **ie.scss** y **main.scss**. Estos archivos son los que utilizará Sass al momento de convertir nuestro trabajo a CSS.

Ningún archivo del directorio **pages**, debe importarse o conectarse a ie.scss y main.scss. Recuerden, la función de este directorio es separar estilos específicos que solo serán utilizados en una página y así no cargar nuestra hoja de estilo principal con código extra, con este modelo de trabajo logramos hacerlas más livianas y leíbles. En cada sub-directorio (por ejemplo: **Home**) Debe existir un archivo maestro (nombre-pagina.scss) para que Sass pueda generar un archivo único y luego, nosotros podamos llamarlo en el HTML en la página requerida.