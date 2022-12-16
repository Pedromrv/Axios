## Axios

Axios es un cliente HTTP **basado en promesas** para JavaScript que puede usarse en la aplicación frontend (en navegadores) y en el backend Node. No hay limitaciones sobre dónde y cómo usar Axios - desde aplicaciones JavaScript simples hasta frameworks frontend complejos (como verás pronto, usaremos Axios en gran medida cuando trabajemos con React). Usar Axios en el backend de Node es posible, como aprenderás a hacer ahora.

### Características

Como se indica en la página oficial [axios](https://github.com/axios/axios) GitHub, aquí está la lista completa de las principales características:

- Hacer [XMLHttpRequests](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest) desde el navegador,
- hacer peticiones `HTTP` desde [Node.js](https://nodejs.org/api/http.html),
- soporta la [Promise API](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise),
- interceptar peticiones y respuestas,
- transformar datos de peticiones y respuestas,
- cancelar peticiones,
- transforma automáticamente JSON en objetos JS,
- soporte del lado del cliente para protección contra [XSRF](https://en.wikipedia.org/wiki/Cross-site_request_forgery).

## Instalación

Axios puede ser instalado con **NPM** o añadido a través de una **CDN**.

Como estamos creando una página simple con sólo **HTML**, **JS** & **CSS** (sin **nodo**) nos será más fácil y rápido usar el **CDN** . Si estuviéramos creando una aplicación más compleja elegiríamos la versión **NPM**.

**Con CDN**

```jsx
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
```

**CON NPM**

```
$ npm install axios         
```

## Llamadas Axios 

### Axios llamada GET 

Una llamada Axios estándar para cualquier petición HTTP es un método `axios()` que recibe un objeto JavaScript que especifica diferentes opciones de la petición.

Dado que **Axios** está basado en Promise, necesitamos añadir el método `.then()` para procesar la respuesta, y el método `.catch()` en caso de que haya un error en la respuesta.

Estas son las opciones más comunes:

```jsx
axios({
  method: 'The HTTP method (verb) we are going to use, e.g. GET, POST, PUT, etc.',
  url: 'The url the server is going to receive.',
  params: 'URL parameters to be sent with the request'
})
  .then(response => {
    // Here we can do something with the response object
  })
  .catch(err => {
    // Here we catch the error
  });
```

Hay muchas otras opciones que podemos configurar en las peticiones de **Axios**. Puedes consultarlas todas en la [documentación oficial de Axios](https://github.com/axios/axios#request-config). Consulta la documentación oficial para ver la lista completa de opciones disponibles.

En general, usaremos una sintaxis un poco más corta y limpia:

```jsx
axios.get(url)
.then(responseFromApi => /* do something with response */)
.catch(error => /* do something with the error */)
```
## API testing

Internet está repleto de API gratuitas a disposición de los desarrolladores. Google, YouTube, Yahoo, Instagram, Twitter, Flickr, LinkedIn y muchas más aplicaciones enormes y famosas ofrecen una API abierta para integrar en nuestra plataforma.

Para demostrar cómo funciona Axios, utilizaremos la API **[restcountries](https://restcountries.com/)**.

### La API REST COUNTRIES

Restcountries](https://restcountries.com/) es una API REST creada por Faydel Florez y adquirida por [apilayer](https://apilayer.com/).

REST COUNTRIES proporciona una API sencilla para obtener información sobre las naciones del mundo a través de llamadas REST. Estas llamadas permiten a los usuarios recuperar datos sobre todos los países disponibles o sobre un único país, basándose en la consulta de búsqueda del usuario. La API ofrece información sobre la moneda del país, su capital, código de llamada, región, subregión, idioma ISO 639-1, nombre o código de país.

Si visitamos [restcountries end points](https://restcountries.com/#api-endpoints-v2-all) podemos ver qué puntos finales REST están disponibles para que los utilicemos en la búsqueda de países.

Algunos ejemplos son:

-   buscar por nombre de país: `https://restcountries.com/v2/name/{name}`
-   buscar por capital: `https://restcountries.com/v2/capital/{capital}`
-   buscar por moneda: `https://restcountries.com/v2/currency/{currency}`

Probémoslo en la práctica.

### Pruebas de API a través de la barra de navegación del navegador

Si copia cualquiera de los enlaces en la barra de navegación del navegador y sustituye la parte dentro de `{}` por un valor real, podrá probar cualquier endpoint.

Después de introducir esta URL [https://restcountries.com/v2/name/spain](https://restcountries.com/v2/name/spain), debería ver algo como esto:![](https://s3-eu-west-1.amazonaws.com/ih-materials/uploads/upload_a8a2c6c5c85922e8b6fce8760da57514.png)

Es posible que tu navegador muestre un objeto diferente y sin formato. Si eso ocurre, prueba a instalar la extensión **[JSON Viewer](https://chrome.google.com/webstore/detail/jsonview/chklaanhfefbnpoihckbnefhakgolnmc?hl=en)**.

### Postman

[Postman](https://www.getpostman.com/docs) es una plataforma que nos permite probar peticiones Web API. Podemos usarlo de forma similar al navegador, del que acabamos de hacer una demostración con la petición GET. Pero no sólo eso, podemos utilizar cualquier verbo HTTP para la petición, y podemos manejar cualquier cantidad de parámetros.

#### Instalando Postman

Ve a [la web oficial](https://www.getpostman.com/) y descarga Postman. Asegúrate de seleccionar el sistema operativo adecuado para tu ordenador.

También podemos usar Postman como una extensión de Google Chrome, pero usaremos la versión [GUI](https://en.wikipedia.org/wiki/Graphical_user_interface) ya que es más intuitiva.

Alternativamente, puedes usar [Insomnia](https://insomnia.rest/) que es una plataforma muy similar a Postman.

#### API testing con Postman - la petición GET 

Abra Postman. Debería ver una interfaz similar a ésta:

![](https://s3-eu-west-1.amazonaws.com/ih-materials/uploads/upload_af6eb57129e0e23b8d1f19d31e869e38.png)

Por ahora, nos centraremos en la barra de navegación.

La _barra de navegación_ simula la barra de navegación del navegador:

- **_select_** a la izquierda indica el verbo HTTP que desea utilizar en la petición,
- el botón **_params_** de la derecha sirve para especificar los parámetros de la petición. Si utilizamos el verbo HTTP GET, añadirá los parámetros en la _query string_ de la URL,
- El botón __save_** permite guardar la petición, por si se quiere repetir la misma petición. Esto es útil cuando se introducen los mismos datos repetidamente,
- el botón **_send_** creará la petición y la enviará.

Introduzcamos la solicitud de búsqueda por el nombre de un país. Utilizaremos _spain_ como ejemplo.

Cuando se pulse el botón _enviar_, Postman mostrará la información relacionada con la respuesta en el panel inferior.

![](https://s3-eu-west-1.amazonaws.com/ih-materials/uploads/upload_51323792b25e8a6a053836c3c77b45fc.png)

Del mismo modo que con la API REST Countries, puede intentar obtener los datos de cualquier otra API y sus puntos finales disponibles. Súper fácil, ¿verdad? 

### Haciendo una petición GET a una REST API

Hagamos una demostración de cómo hacer una petición GET a Axios. No usaremos el entorno Node para la demostración, sino un enfoque simplificado con JavaScript puro. Crea una carpeta llamada `rest-countries` y dentro crea dos archivos: `index.html` y `index.js`.

```
$ mkdir rest-countries
$ cd rest-countries
$ touch index.html index.js

# the structure should look like this:
rest-countries
   ├── index.html
   └── index.js
```

Ahora añade este código a `index.html`.

```html
<!-- index.html -->

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Axios GET demo with Countries Rest API</title>
  </head>

  <body>
    <h1>Countries Info</h1>

    <div>
      <input id="country-name-input" type="text" />
      <button id="get-country-btn">Get the country</button>
    </div>

    <h2 id="country-name"></h2>
    <p id="country-capital"></p>
    <div>
      <img id="country-flag" src="" height="200px" />
    </div>

    <script src="https://unpkg.com/axios/dist/axios.min.js"></script>
    <script src="index.js"></script>
  </body>
</html>
```

Observe que no hemos puesto la entrada con el _id_ _country-name-input_ dentro de un elemento `form`. La razón es que el comportamiento por defecto del elemento formulario es recargar la página al enviar. Más adelante veremos cómo evitarlo respetando el estándar _W3C_.

Y ahora añade algo de código al `index.js`:

```jsx
// index.js

const getCountryInfo = countryName => {
  axios
    .get(`https://restcountries.com/v2/name/${countryName}`)
    .then(response => {
      console.log('Response from API is: ', response);
      const countryDetail = response.data[0];
      console.log('a single country details: ', countryDetail);
    })
    .catch(err => console.log(err));
};

document.getElementById('get-country-btn').addEventListener('click', () => {
  const userInput = document.getElementById('country-name-input').value;
  getCountryInfo(userInput);
});

```
Si introduce **España** y pulsa el botón, verá esta matriz de objeto(s) en la consola del navegador:

![](https://s3-eu-west-1.amazonaws.com/ih-materials/uploads/upload_4920fa417b7723669dedb2757e7a088e.png)

Lo bueno de Axios es que **no hay recarga de página!** Si sigues cambiando los países. Obtendrás los datos sin refrescar la página. Como recordatorio, después de cada petición HTTP, la página se actualiza con una nueva página completa. Si deseas probarlo, debes saber que cuando se actualice, la consola estará vacía.

Hagamos un paso extra y mostremos los datos en el navegador, no sólo en la consola. Actualiza el código en `index.js` con lo siguiente:

```jsx
// index.js

const getCountryInfo = countryName => {
  axios
    .get(`https://restcountries.com/v2/name/${countryName}`)
    .then(response => {
      const countryDetail = response.data[0];
      document.getElementById('country-name').innerText = countryDetail.name;
      document.getElementById('country-capital').innerText = countryDetail.capital;
      document.getElementById('country-flag').setAttribute('src', countryDetail.flag);
    })
    .catch(err => {
      console.log(err);
      err.response.status === 404 ? alert(`The country ${countryName} doesn't exist.`) : alert('Server error! Sorry.');
    });
};

document.getElementById('get-country-btn').addEventListener('click', () => {
  const userInput = document.getElementById('country-name-input').value;
  getCountryInfo(userInput);
});
```

Con sólo una pizca de conocimientos de manipulación del DOM, fuimos capaces de mostrar en el navegador los datos recibidos de la API. ¿No es increíble? Abre tantas oportunidades para reutilizar APIs geniales.
