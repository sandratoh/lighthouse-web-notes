# ISS Spotter Assignment

### Making API requests to different services to solve the problem

1. Fetch our IP Address
2. Fetch the geo coordinates (latitude & longitude) for our IP
3. Fetch the next ISS flyovers for our geo coordinates

Each later step is dependent on data from the previous one.

## API Call #1: Checking public IP address
Check out: [ipify API](https://www.ipify.org)

IPv4 IP address in JSON format: https://api.ipify.org/?format=json

### `Error(...)`
* creates a new Error object that we can pass around
* passed to our callback in our case to indicate something went wrong

## API Call #2: Fetch Geo Coordinates by IP
Check out: [Free Geo IP](https://freegeoip.app) for latitude and longitutde coordinates

JSON format: https://freegeoip.app/json/

## API Call #3: Fetch Flyover Times for ISS
Check out: [open-notify.org](http://open-notify.org) for NASA data

[Overhead Pass Predictions](http://open-notify.org/Open-Notify-API/ISS-Pass-Times/) endpoint (API has 2 required input values and 2 optional ones).
* Latitude *(required)*: `lat`
* Longitude *(required)*: `lon`
* Altitude: `alt`
* Number: `n` - number of passes to return

JSON format: http://api.open-notify.org/iss-pass.json?lat=`${lat}`&lon=`${lon}`

* (fill in `lat` and `lon` with own coordinates)

By default, API will give us the 5 upcoming times that ISS will fly over the given coordinates and for how long it will remain 'visible' in the sky.

## Date and Time in Javascript

> Unix Timestamp starts at January 1, 1970 00:00:00

#### Converting UTC Date and Time to Local Date and Time
Check out: [`.toLocaleString` Method](https://www.w3schools.com/jsref/jsref_tolocalestring.asp)

ISS Examples

```javascript
let datetime = new Date(0);
    datetime.setUTCSeconds(1613154541);
    
    const dateTimeOptions = {
      weekday: 'long',
      year: 'numeric',
      month: 'short',
      day: 'numeric',
      hour12:false,
      timeZone: 'Canada/Pacific',
      timeZoneName: 'long'
    };
    
    let pstDateTime = datetime.toLocaleString('en-CA', dateTimeOptions);
```