# Proyecto Curso de Asincronismo con JavaScript 2022

**El desafío es crear una landing page sobre algun creador de contenido en YouTube y compartirlo en la comunidad de Platzi.**

##Crear un repositorio
El paso cero a realizar es crear un repositorio en GitHub, para esto el profesor de Platzi recomienda seguir los siguientes pasos.
* Paso 1.- Crear un nuevo repositorio presionando el botón `New` y luego escribir un nombre que sea representativo.
* Paso 2.- Seleccionar la opción `Public`.
* Paso 3.- Checkear la opción para agregar el archivo README.
* Paso 4.- En la lista desplegable de template, seleccionar `node`.
* Paso 5.- En la lista desplegable de licencias, seleccionar la de `MIT`.
* Paso 6.- Presionar el botón `Create repository`.
* Paso 7.- Una vez que la pagina cambie a la vista del proyecto, para conectarlo con nuestra computadora, presionar el botón `Code` y en la pestaña Local, copiar la url que dice HTTPS.
* Paso 8.- En la consola del computador, utilizar comandos para llegar a la carpeta donde almaceno mis proyectos y escribo el comando:  `git clone https://restodeurlcopiada` . Con esto se descargará una copia desde la nube hasta mi computador.
* Paso 9.- Nuevamente en la consola, entro a la carpeta descargada y a continuación inicializo el proyecto con el comando: `npm init -y` 
* Paso 10.- Con Visual Studio Code, abrir la carpeta del proyecto. Crear un nueva carpeta llamada **src**. y dentro un nuevo archivo llamado index.html. También crear una carpeta assets.

## Preparar el contenido de la página.
La idea del proyecto es crear una landing page sobre algún creador de contenidos de YouTube, ya que mediante el uso de una API, vamos a obtener un listado de los últimos videos que a subido a su canal.
El profesor facilitara una plantilla ya diseñada que además de venir la estructura HTML, cuenta con estilos CSS utilizando las clases de Tailwind CSS.
Copiar el código tal cual en mi archivo index.html.
Luego editar la sección del nombre del creador, su nombre en redes sociales, agregar una descripción, y también una imagen de la persona.

## Crear la conexión a la API de YouTube.
* Paso 1: dentro del navegador ir a la página: [rapidapi.com](https://rapidapi.com/) 
* Paso 2: esta página muestra una serie de colecciones de APIs que están disponibles para proyectos. Para poder utilizar una API, debo crear una cuenta o loguearme con mi cuenta de Gmail.
* Paso 3: una vez que cree mi cuenta, en la página principal, en la parte superior donde está la barra de búsqueda, escribir **youtube**. Aparecerán todas las APIs disponibles (las gratis y las de pago).
* Paso 4: Seleccionar la que se llama **Youtube v3**. Cargara una página, al lado izquierdo están las interacciones GET que se pueden hacer con la API, para este ejercicio se utilizara `Channel videos` .
* Paso 5: varias opciones ya estarán completadas, no hay que cambiar nada por el momento. Bajar hasta la categoría **Required Parameters** y donde dice **channelId** cambiar el id que esta por defecto, por el del creador de contenido que quiero tener en mi pagina. 
* Paso 6: para obtener el **id channel** de un canal de YouTube, se puede solicitar en página: [commentpicker.com](https://commentpicker.com/youtube-channel-id.php/) . Al escribir el nombre del canal según el formato que se muestra en el placeholder, y si es correcto, aparecerá un channel_id como por ejemplo: `UCVTL17ftpqx3lQ_IaGUNgSg`
* Paso 7: dentro de **rapidapi**, pegar el id y bajar un poco hacia la sección **Optional Parameters**, en la opción **maxResults** cambiar el numero a 9 para solo obtener los últimos 9 videos publicados por el creador.
* Paso 8: probar si se logró la conexión presionando el botón `Test Endpoint` . Si la conexión es correcta aparecerá un mensaje como: _**Your App default-application_6808747 is now using version v1**_
* Paso 9: Una de las ventajas de **rapidapi**, es que entrega el código necesario para implementar el uso de la API en mi proyecto. En la sección derecha, ir a `Code Snippets` - En la lista desplegable seleccionar **JavaScript** y después **fetch**.
* paso 10: debería aparecer un código como el siguiente ejemplo, este se debe pegar en el archivo main.js

```javascript
const options = {
	method: 'GET',
	headers: {
		'X-RapidAPI-Key': '334534c5c3mshbc7cc8803cffa01p1d21ecjsn90430c8d0772',
		'X-RapidAPI-Host': 'youtube-v31.p.rapidapi.com'
	}
};

fetch('https://youtube-v31.p.rapidapi.com/search?channelId=UCVTL17ftpqx3lQ_IaGUNgSg&part=snippet%2Cid&order=date&maxResults=9', options)
	.then(response => response.json())
	.then(response => console.log(response))
	.catch(err => console.error(err));
```

## Crear la logica del archivo main JavaScript.
Una vez que ya se obtuvo el código base para conectar la API de YouTube con el creador de contenidos elegido, dentro del archivo main.js se crea la lógica utilizando asincronismo.
Para más detalles, revisar el mencionado archivo junto a la explicación del código.

## Desplegar utilizando GitHub Pages.
Cuando el proyecto esta terminado y estamos seguros que en nuestra maquina local funciona correctamente, podemos subirlo y GitHub y luego compartirlo con la comunidad.
Se podría crear una nueva GitHub Pages directamente desde el menú de la página, pero aprovecharemos esta oportunidad para hacer todo el proceso mediante la consola.
* Paso 1: utilizando la consola desde VSC, posicionarse en la carpeta del proyecto y utilizando npm instalar el siguiente paquete como dependencia de desarrollo: 
`npm i gh-pages -D`
* Paso 2: en el archivo **package.json.** En el apartado **scripts**, se puede cambiar el nombre y valor de _**test**_ por uno creado por mi, para este caso se llamara _**deploy**_ y se le debe agregar la ruta de la carpeta raíz donde esta mi proyecto. Debería quedar algo así: 
`"deploy": "gh-pages -d src"`
* Paso 3: subir todos los cambios al repositorio utilizando el comando
`git push origin main`
* Paso 4: nuevamente en la consola de VSC, ejecutar el comando
`npm run deploy`
para que corra el código y suba a una nueva rama la creación del proyecto utilizando GitHub Pages. En la consola deberá aparecer un mensaje indicando: **Published**.
* Paso 5: finalmente, para comprobar que todo resulto perfectamente, desde el repositorio en la pagina de GitHub, presionar el clic en el menú superior `Settings`. En el menú lateral izquierdo, presionar el clic sobre `Pages`. Deberá aparecer una url con el proyecto ya subido. En **source** deberá aparecer la rama _**gh-pages**_ que pertenece a _**/(root)**_.

