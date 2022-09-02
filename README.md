# Build-a-Flight-Widget-API-Project-in-JavaScript-NodeJS-RapidAPI

https://raw.githubusercontent.com/RodrigoMvs123/Build-a-Flight-Widget-API-Project-in-JavaScript-NodeJS-RapidAPI/main/README.md



##

https://www.youtube.com/watch?v=iAtCHhs8xoo

https://rapidapi.com/


https://rapidapi.com/itsjustlogan/api/toronto-pearson-airport/
https://rapidapi.com/developer/dashboard
https://fonts.google.com/specimen/Ubuntu+Condensed?query=Ubuntu

https://nodejs.org/en/download/
https://docs.npmjs.com/downloading-and-installing-node-js-and-npm

http://localhost:8000/flights

##

Index.html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Flight Widget</title>
        <link rel="stylesheet href="styles.css"
    </head>
    <body>

        <div class="departures">
            <h1>DEPARTURES</h1>
            <table>
                <thead>
                    <tr>
                        <th></th>
                        <th id="time">TIME</th>
                        <th id="destination">DESTINATION</th>
                        <th id="flight">FLIGHT</th>
                        <th id="gate">GATE</th>
                        <th id="remarks">REMARKS</th>
                    </tr>
                </thead>
                <tbody id="table-body"></tbody>
            </table>
            
        </div>

        <script src"app.js"></script>
    </body>
    </html>
    
    ##
    App.js
    
    const { table } = require("console")

const tableBody = document.getElementById('table-body')

const getFlight = () => {
    fetch('http://localhost:8000/flights')
    .then(response => response.json())
    .then(flights => {
        populateTable(flights)

    })
    .catch(err => console.log(err))
}
getFlight()

const populateTable = (flights) => {
    console.log(flights)
    for (const flight of flights) {
    const tableRow = document.createElement('tr')
    const tableIcon = document.createElement('td')
    tableIcon.textContent = "https://img.freepik.com/free-vector/passenger-airplane-isolated_1284-41822.jpg?w=2000" 
    tableRow.append(tableIcon)

    const flightDetails = {
        time: flight.departing.slice(0,5),
        destination: flight.destination.toUpperCase,
        flight: flight.flightNumber.shift(),
        gate: flight.gate,
        remarks: flight.status.toUpperCase()
    }

    for (const flightDetail in flightDetails) {
        const tableCell = document.createElement('td')
        const word = Array.from(flightDetails[flightDetail])

        for (const [index, letter] of word.entries()) {
            const letterElement = document.createElement('div')


            setTimeout(() => {
                letterElement.classList.add('flip')
                letterElement.textContent = letter
                tableCell.append(letterElement)
            }, 100 * index)
            
        }
            tableRow.append(tableCell)
    }
        tableBody.append(tableRow)
 
}

##

Styles.css

@import url('https://fonts.googleapis.com/css2?family=Ubuntu+Condensed&display=swap');

* {
    font-family: 'Ubuntu Condensed', sans-serif;
    color: rgb(240, 240, 240);
    font-size: 35px;
    
}

body {
    display: flex;
    justify-content: center;
    height: 100vh;
    align-items: center;
    background-color: rgb(251, 199, 127);
}

h1 {
    padding: 10px;

}

.depatures {
    background-color: rgb(6, 6, 6);
    border-radius: 10px;
    padding: 10px;

}

.depatures table {
    background-color: rgb(46, 46, 46);
    text-align: left;

}

.depatures table div {
    border: solid 4px rgb(26, 26, 26);
    background-color: rgb(0, 0, 0);
    min-width: 20px;
    height: 40px;
    float: left;
}

.flip {
    animation: 0.5 linear flipping;
}

@keyframes flip {
    0% {
        transform: rotateX(0 deg);
    }
    50% {
        transform: rotateX(90 deg);
    }
    100% {
        transform: rotateX(0 deg);
    }
    
}

#time {
    width: 160px;
}

#destination {
    width: 700px;
    } 

#flight {
    width: 205px;
}

#gate {
    width: 135px;
}

#remarks {
    width: 260px;
}

##

Package.json

{
    "name": "flight-widget-live",
    "version": "1.0.0",
    "description": "",
    "main": "server.js",
    "scripts": {
        "test": "echo \"Error: no test specified\" && exit 1",
        "start": "nodemon server.js"

    },
    "author": "",
    "license": "ISC"
    "dependencies": {
        "axios": "^0.27.2",
        "cors": "^2.8.5",
        "dotenv": "^16.0.1",
        "express": "^4.18.1",
        "nodemon": "^2.0.19"
    }
}

##

Server.js

const PORT = 8000
const axios = require("axios").default
const exporess = require('express')
const app = exporess()
const cors = require ('cors')
require('dotenv').config()
app.use(cors())

app.get('/flights', (req, res) => {
    const options = {
        method: 'GET',
        url: 'https://toronto-pearson-airport.p.rapidapi.com/arrivals/carousel/9',
        headers: {
          'X-RapidAPI-Key': process.env.RAPID_API_KEY,
          'X-RapidAPI-Host': 'toronto-pearson-airport.p.rapidapi.com'
        }
      };
      
      axios.request(options).then(function (response) {
          console.log(response.data);
          res.json(response.data.slice(0,6))
      }).catch(function (error) {
          console.error(error);
      })
})

app.listen(PORT, () console.log('running on PORT' + PORT))

##

.env

RAPID_API_KEY=d193a8fa71mshac02bc326c17e30p1467d3jsna00b37ae07a7

