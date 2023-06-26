# Lesson 6 - Managing weather

The goal of this lesson is to introduce that various ways of getting and using weather data in a GridLAB-D simulation.  The specific learning objectives are the following.

1. How to change from using TMY data to CSV data.
2. How to obtain historical data from NSRDB.
3. How to obtain realtime data from METAR.
4. How to obtain a weather forecast from NOAA.

## Reading CSV Data

Normally TMY data is loaded from a TMY3 file using a [climate object](https://docs.gridlabd.us/index.html?owner=arras-energy&project=gridlabd&branch=master&folder=/Module/Climate&doc=/Module/Climate/Climate.md).  This data can be used to provide typical weather data for any year past, present, or future.  If you want to provide alternative TMY data, you can either generate you own TMY3 file (which can be difficult) or you can define a [CSV reader]([http](https://docs.gridlabd.us/index.html?owner=arras-energy&project=gridlabd&branch=master&folder=/Module/Climate&doc=/Module/Climate/Csv_reader.md) to load a more generic data file as TMY.  

## Downloading Historical Data

TODO

## Download Realtime Data

TODO

## Downloading Forecast Data

TODO

## Tasks

1. Load [sample.csv](sample.csv) file as TMY weather data ([`main.glm@6`](main.glm#L6-L23))
   1. Add a CSV reader to read the file (see [`main.glm@7`](main.glm#L7-L12)).
   2. Add a climate object to use the data from the CSV reader (see [`main.glm@13`](main.glm#L13-L17)).
   3. Add a clock to specify the date range for which the TMY weather data is generated (see [`main.glm@18`](main.glm#L18-L23)).

# Exercices

1. TODO

# More Information

* [TMY Weather](https://docs.gridlabd.us/index.html?owner=arras-energy&project=gridlabd&branch=master&folder=/Subcommand&doc=/Subcommand/Weather.md)
* [NSRDB Weather](https://docs.gridlabd.us/index.html?owner=arras-energy&project=gridlabd&branch=master&folder=/Utilities&doc=/Utilities/Nsrdb_weather.md)
* [METAR Weather](https://docs.gridlabd.us/)
* [NOAA Weather](https://docs.gridlabd.us/index.html?owner=arras-energy&project=gridlabd&branch=master&folder=/Utilities&doc=/Utilities/Noaa_forecast.md)
