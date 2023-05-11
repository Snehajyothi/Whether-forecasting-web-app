# Whether-forecasting-web-app
HTML:

<!DOCTYPE html>

<html lang="en">

<head>

    <meta charset="UTF-8">

    <meta http-equiv="X-UA-Compatible" content="IE=edge">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Weather</title>

    <link rel="stylesheet" href="style.css">

</head>

<body>

    <form id="form">

        <input type="text" id="search" placeholder="Search By Loaction" autocomplete="off">

    </form>

    <main id="main">

    </main>

    <script src="app.js"></script>

</body>

</html>

CSS:

@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@200;400;600&display=swap");

* {

    box-sizing: border-box;

}

body {

    margin: 0;

    font-family: "Poppins", sans-serif;

    background-color: linear-gradiet(300deg, #757b87, #909d9d);

    display: flex;

    justify-content: center;

    align-items: center;

    min-height: 100vh;

    flex-direction: column;

}

input {

    padding: 1rem;

    border-radius: 25px;

    border: none;

    background-color: #fff;

    font-family: inherit;

    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);

    min-width: 300px;

    font-size: 1rem;

}

input:focus {

    outline: none;

}

.weather {

    text-align: center;

    font-size: 2rem;

}

.weather h2 {

    margin-bottom: 0;

    display: flex;

    align-items: center;

} /* .weather img{ transform: scale(2); } */

Javascript :

const apiKey = "ENTER YOUR API KEY";

const main = document.getElementById('main');

const form = document.getElementById('form');

const search = document.getElementById('search');

  

const url = (city)=> `https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=${apiKey}`;

async function getWeatherByLocation(city){

     

         const resp = await fetch(url(city), {

             origin: "cros" });

         const respData = await resp.json();

     

           addWeatherToPage(respData);

          

     }

      function addWeatherToPage(data){

          const temp = Ktoc(data.main.temp);

          const weather = document.createElement('div')

          weather.classList.add('weather');

          weather.innerHTML = `

          <h2><img src="https://openweathermap.org/img/wn/${data.weather[0].icon}@2x.png" /> ${temp}°C <img src="https://openweathermap.org/img/wn/${data.weather[0].icon}@2x.png" /></h2>

          <small>${data.weather[0].main}</small>

          

          `;

        //   cleanup 

          main.innerHTML= "";

           main.appendChild(weather);

      };

     function Ktoc(K){

         return Math.floor(K - 273.15);

     }

     form.addEventListener('submit',(e) =>{

        e.preventDefault();

        const city = search.value;

        if(city){

            getWeatherByLocation(city)

        }

     });
