## Axios

Axios is a **promise-based** HTTP client for JavaScript which can be used in the frontend application (in browsers) and the Node backend. There are no limitations where and how to use Axios - from plain JavaScript applications to complex frontend frameworks (as you will see soon, we will be using Axios heavily when working with React). Using Axios in Node backend is possible, as you will learn how to do it now.

### Features

As stated in the official [axios](https://github.com/axios/axios) GitHub page, here is the full list of main features:

-   Make [XMLHttpRequests](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest) from the browser,
-   make `HTTP` requests from [Node.js](https://nodejs.org/api/http.html),
-   supports the [Promise API](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise),
-   intercept requests and responses,
-   transform requests and responses data,
-   cancel requests,
-   automatically transforms JSON into JS objects,
-   client-side support for protecting against [XSRF](https://en.wikipedia.org/wiki/Cross-site_request_forgery).

## Installation

Axios can be installed with **NPM** or added through a **CDN**.

Since we are creating a simple page with just **HTML**, **JS** & **CSS** (no **node**) it will be easier and faster for us to use the **CDN** . If we were building a more complex app we would choose the **NPM** version.

**Using CDN**

```jsx
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
```

**Using NPM**

```
$ npm install axios         
```

## Axios calls

### Axios GET call

A standard Axios call for any HTTP request is a method `axios()` that receives a JavaScript object that specifies different options of the request.

Since **Axios** are Promise based, we need to add the `.then()` to process the response, and the `.catch()` method in case there is an error in the response.

These are the most common options:

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

There are many other options we can configure in the **Axios** requests. You can check all of them in the [official Axios documentation](https://github.com/axios/axios#request-config). Check the official documentation to see the full list of available options.

Mostly, we will be using a bit shorter and cleaner syntax:

```jsx
axios.get(url)
.then(responseFromApi => /* do something with response */)
.catch(error => /* do something with the error */)
```
## API testing

The Internet is filled with free APIs available for developers. Google, YouTube, Yahoo, Instagram, Twitter, Flickr, LinkedIn, and many more huge and famous applications provide an open API to integrate into our platform.

To demonstrate how Axios actually works, we will use the **[restcountries](https://restcountries.com/) API**.

### The REST COUNTRIES API

The [restcountries](https://restcountries.com/) is a REST API created by Faydel Florez and acquired by [apilayer](https://apilayer.com/).

REST COUNTRIES provides a simple API for getting information about the world’s nations via REST calls. These calls allow users to retrieve data about all available countries or a single country, based on the user’s search query. The API gives information about the country’s currency, its capital, calling code, region, sub-region, ISO 639-1 language, name, or country code.

If we visit [restcountries end points](https://restcountries.com/#api-endpoints-v2-all) we can see which REST endpoints are available for us to use to search for countries.

Some examples are:

-   search by country name: `https://restcountries.com/v2/name/{name}`
-   search by capital city: `https://restcountries.com/v2/capital/{capital}`
-   search by currency: `https://restcountries.com/v2/currency/{currency}`

Let’s test this in practice.

### API testing through the browser’s navigation bar

If you copy any of the links into the browser’s navigation bar and replace the part within `{}` with real value, you can test any endpoint.

After inputting this URL: [https://restcountries.com/v2/name/spain](https://restcountries.com/v2/name/spain), you should see something like this:![](https://s3-eu-west-1.amazonaws.com/ih-materials/uploads/upload_a8a2c6c5c85922e8b6fce8760da57514.png)

It might be possible that your browser shows a different and unformatted object. If that happens, try installing the **[JSON Viewer](https://chrome.google.com/webstore/detail/jsonview/chklaanhfefbnpoihckbnefhakgolnmc?hl=en)** extension.

### Postman

[Postman](https://www.getpostman.com/docs) is a platform that allows us to test Web API requests. We could use it similarly to the browser, which we just demoed with the GET request. However, not just that, we can use any HTTP verb for the request, and we can handle any amount of parameters.

#### Installing Postman

Go to [the official website](https://www.getpostman.com/) and download Postman. Make sure you select the right operating system for your computer.

We can use Postman as a Google Chrome extension too, but we will use the [GUI](https://en.wikipedia.org/wiki/Graphical_user_interface) version since it is more intuitive.

Alternatively, you can use [Insomnia](https://insomnia.rest/) which is a platform very similar to Postman.

#### API testing with Postman - the GET request

Open Postman. You should see an interface similar to this:

![](https://s3-eu-west-1.amazonaws.com/ih-materials/uploads/upload_af6eb57129e0e23b8d1f19d31e869e38.png)

For now, we will focus on the navigation bar.

The _navigation bar_ simulates the browser’s navigation bar:

-   **_select_** input on the left indicates the HTTP verb you want to use in the request,
-   **_params_ button** on the right is for specifying parameters in the request. If we use GET HTTP verb, it will add the parameters in the URL’s _query string_,
-   **_save_** button allows you to save the request, in case you want to repeat the same request. This is useful when you are introducing the same data repeatedly,
-   **_send_** button will create the request and send it.

Let’s input the request to search by a country name. We will use _spain_ as an example.

When the _send_ button is clicked, Postman will display the information related to the response in the panel below.

![](https://s3-eu-west-1.amazonaws.com/ih-materials/uploads/upload_51323792b25e8a6a053836c3c77b45fc.png)

In the same way, as with REST Countries API, you can try to get the data from any other API and its available endpoints. Super easy, right? 

### Making a GET request to a REST API

Let’s demo how to make an Axios GET request. We won’t be using the Node environment to demo, but a simplified approach with pure JavaScript. Go ahead and create a folder named `rest-countries` and inside create two files: `index.html` and `index.js`.

```
$ mkdir rest-countries
$ cd rest-countries
$ touch index.html index.js

# the structure should look like this:
rest-countries
   ├── index.html
   └── index.js
```

Now add this code to `index.html`.

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

Notice that we did not put the input with the _id_ _country-name-input_ inside a `form` element. The reason why is because the default behavior of the form element is to reload the page on submit. We will address later how to avoid this while keeping with the _W3C_ standard.

And now add some code to the `index.js`:

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
If you input **Spain** and click the button, you will see this array of object(s) in the browser’s console:

![](https://s3-eu-west-1.amazonaws.com/ih-materials/uploads/upload_4920fa417b7723669dedb2757e7a088e.png)

The cool thing about Axios is that **there is no page reload!** If you keep changing the countries. You will get the data without refreshing the page. As a reminder, after every HTTP request, the page is refreshed with a full new page to render. If you wish to test it, know that is it would be refreshed, the console would be empty.

Let’s do an extra step and display the data in the browser, not just in the console. Update the code in `index.js` with the following:

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

With just a dash of DOM manipulation knowledge, we were able to display in the browser the received data from the API. Isn’t this amazing! Opens up so many opportunities for reusing cool APIs.
