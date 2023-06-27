[![Simulation](../../actions/workflows/main.yml/badge.svg)](../../actions/workflows/main.yml)

# Lesson 6 - Managing weather

The goal of this lesson is to introduce that various ways of getting and using weather data in a GridLAB-D simulation.  The specific learning objectives are the following.

1. How to change from using TMY data to CSV data.
2. How to obtain historical data from NSRDB.
3. How to obtain realtime data from METAR.
4. How to obtain a weather forecast from NOAA.

## Reading CSV Data

Normally TMY data is loaded from a TMY3 file using a [climate object](https://docs.gridlabd.us/index.html?owner=arras-energy&project=gridlabd&branch=master&folder=/Module/Climate&doc=/Module/Climate/Climate.md).  This data can be used to provide typical weather data for any year past, present, or future.  If you want to provide alternative TMY data, you can either generate you own TMY3 file (which can be difficult) or you can define a [CSV reader](https://docs.gridlabd.us/index.html?owner=arras-energy&project=gridlabd&branch=master&folder=/Module/Climate&doc=/Module/Climate/Csv_reader.md) to load a more generic data file as TMY.  

## Downloading Historical Data

Historical data can be retrieved from the National Solar Radiation Database (NSRDB) using the Python `nsrdb_weather` module.  The tool only allows access to historical weather records in North America, so you have to specify the year using `-y=YEAR` and geographic location using `-p=LAT,LON`.  You also have to specify the name of the GLM file in which the historical weather object is stored using `-g=FILENAME.glm`.

The NSRDB database requires access credentials. In GitHub, you must use the [Settings/Secrets/Actions](../../settings/secrets/actions) tab to create an actions secret. Click the [New repository secret](../../settings/secrets/actions/new) button and add your NSRDB credentials, giving it a name of your choice. If you have forked this repository, you can use the name `NSRDB_CREDENTIAL`. To get your NSRDB credential, you should visit the [NSRDB website](https://developer.nrel.gov/signup/). You should save the credentials in the format `{"YOUR_EMAIL": "YOUR_API_KEY"}`. Once you have the credentials, you can add them to [the workflow file](.github/workflows/main.yml).

## Download Realtime Data

Realtime weather data can be accessed using the FAA's METAR system.  The Python module `metar2glm` can retrieve the weather at any airport in North America and generates a GLM file that can be saved and loaded.  Since the METAR object's default class name `weather` is the same as a `climate` module's class name, we have to rename the class using the option `-c CLASSNAME`.

## Downloading Forecast Data

Weather forecasts are downloaded from NOAA. Here too, you must specify the location using the `-p=LAT,LON` option. You can also specify the name of the CSV file using the `-c=FILENAME.csv` option, the name of the forecast object using the `-n=OBJECTNAME`, and the name of the GLM file using the `-g=FILENAME.glm` option.

The GLM file contains some helpful global variables you can use to identify what time range is provided by the forecast:

- `NOAA_FORECAST_TIMEZONE`, e.g., `PST+8PDT`
- `NOAA_FORECAST_STARTTIME`, e.g., `2023-06-26T11:00:00-07:00`
- `NOAA_FORECAST_STOPTIME`, e.g., `2023-07-09T09:00:00-07:00`

## Tasks

1. Load [`sample.csv`](sample.csv) file as TMY weather data ([`main.glm@6`](main.glm#L6-L17))
   1. Load the climate module (see [`main.glm@7`](main.glm#L7))
   2. Add a CSV reader to read the file (see [`main.glm@8`](main.glm#L8-L12)).
   3. Add a climate object to use the data from the CSV reader (see [`main.glm@13`](main.glm#L13-L17)).
2. Get and load the historical weather for Redwood City, CA (37.5N,122.4W) for the year 2020.
   1. Get the historical weather object (see [`main.glm@21`](main.glm#L20-L22)). (Hint: the data doesn't change each time you run the command, so you have test for the existence of the file and avoid downloading the data more than once.)
   2. Load the historical data object (see [`main.glm@23`](main.glm#L23))
   3. Add the credentials to your workflow file (see [`.github/workflows/main.yml@17`](.github/workflows/main.yml#L17-L22)).
3. Get and load the realtime weather for San Francisco International Airport (KSFO).
   1. Get the realtime weather (see [`main.glm@26`](main.glm#L26))
   2. Load the realtime weather (see [`main.glm@27`](main.glm#L27))
4. Get and load the weather forecast for Redwood City, CA, and set the simulation time to the forecast time.
   1. Get the forecast (see [`main.glm@30`](main.glm#L30))
   2. Load the forecast (see [`main.glm@31`](main.glm#L31)))
   3. Set the clock (see [`main.glm@32`](main.glm#L32-L37)))

# Exercices

1. Change the weather history, realtime, and forecast to run in Seattle, Washington.

# More Information

* [TMY Weather](https://docs.gridlabd.us/index.html?owner=arras-energy&project=gridlabd&branch=master&folder=/Subcommand&doc=/Subcommand/Weather.md)
* [NSRDB Weather](https://docs.gridlabd.us/index.html?owner=arras-energy&project=gridlabd&branch=master&folder=/Utilities&doc=/Utilities/Nsrdb_weather.md)
* [METAR Weather](https://docs.gridlabd.us/)
* [NOAA Weather](https://docs.gridlabd.us/index.html?owner=arras-energy&project=gridlabd&branch=master&folder=/Utilities&doc=/Utilities/Noaa_forecast.md)
