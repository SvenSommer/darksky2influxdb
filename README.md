# darksky2influxdb
Stores weather forcecast data from Dark Sky Api into a influxdb database.
<br>[Powered by Dark Sky](https://darksky.net/poweredby/)

This information can by used to display forecast data with [grafana](https://grafana.com/).

## Preview

![](https://github.com/SvenSommer/darksky2influxdb/blob/master/forecast_preview.png?raw=true)


## Getting Started

Clone repository `git clone https://github.com/SvenSommer/darksky2influxdb`

### Prerequisites

#### Node and npm
Node and npm are required. See https://docs.npmjs.com/getting-started/installing-node.
Test your version by
```
node -v
npm -v
```
Get the latest npm version with `npm install npm@latest -g`

#### Dark Sky API Key

Get your https://darksky.net/dev/register here.
<br>Please note that only the first 1000 API requests you make every day are free of charge.

#### Influxdb
Please follow the official installation documentation https://docs.influxdata.com/influxdb/v1.2/introduction/installation/

#### Grafana
If you want to visualise the data in a chart I can hardly reccomend [grafana](https://grafana.com/). <br> You can find my dashboard for import in `grafana\Weather - Forecast-Dashboard.json`.

### Installing

1. Enter cloned directory: `cd darksky2influxdb` and install dependencies `npm install`
2. Configure config/default.yml file

Here is an example of `default.yml`
```
general:
  debug: true
  cron: '*/15 * * * *'
darksky:
  key: abcdefghiklmnopqrstuvwxyz1234567
  units: auto
  longitude: -123.41670367098749
  latitude: 47.20296790272209
influxdb:
  host: 192.168.188.2
  database: weather
  username: darkskyimport_user
  password: supersecretpassword!?
```

|Option|Description|
|---|---|
|`debug`|Enables Debug mode and provides additional informations <br><br>**Type:** `booleon`<br>**Possible values:** `true`,`false`|
|`cron`|Programm is repating itself in a given period<br><br>**Type:** `string`<br>**Possible values:** `'*/15 * * * *'` - every 15 minutes,<br>`''` - running only once|
|darksky - `key`|get your darksky key here https://darksky.net/dev/register<br><br>**Type:** `string`<br>**Possible values:** `abcdefghiklmnopqrstuvwxyz1234567` |
|darksky - `units`|Return weather conditions in the requested units. See https://darksky.net/dev/docs/forecast<br><br>**Type:** `string`<br>**Possible values:** `auto`,`ca`,`uk2`,`us`,`si` |
|darksky - `longitude` and `latitude `|Coordinates of forecast location (in decimal degrees).<br><br>**Type:** `float`<br>**Possible values:** `latitude: 47.20296790272209` and `longitude:-123.41670367098749` |
|influxdb - `host`|Server your influxdb is running <br><br>**Type:** `string`<br>**Possible values:** `localhost` , `192.168.188.2` |
|influxdb - `database`|Name of your Database the forecast data is stored. <br><br>**Type:** `string`<br>**Possible values:** `weather` , `forecast`|
|influxdb - `username`|User with writing privileges on the database|
|influxdb - `password`|Password of user with writing privileges on the database|



## Running the Import

Start the import with `node importForecast.js` If you have given a valid cron interval in the configfile the programm will repeat the import automaticly.

## Tested

This is coded and tested on a RaspberryPi 3

## Authors

* **SvenSommer** - [SvenSommer](https://github.com/SvenSommer/)

See also the list of [contributors](https://github.com/your/project/contributors) who participated in this project.

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments

* This code is originally based on ErwinSteffens project [darksky-influxdb](https://github.com/ErwinSteffens/darksky-influxdb). Many thanks to him!
