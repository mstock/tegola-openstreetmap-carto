# Tegola OpenStreetMap Carto

This repository contains a sample configuration for [Tegola](https://tegola.io/) that was built from the [openstreetmap-carto](https://github.com/gravitystorm/openstreetmap-carto) CartoCSS project using the script in [App-CartoCSS2Tegola](https://github.com/mstock/App-CartoCSS2Tegola/).

## Usage

In order to use this sample, you'll need a render database setup according to the [INSTALL.md](https://github.com/gravitystorm/openstreetmap-carto/blob/master/INSTALL.md) documentation. Please make sure that your database is created using UTF8 encoding (`createdb -E UTF8 -T template0 gis`) and that the database user configured in the `[[providers]]` section of `openstreetmap-carto.toml` can access the render database (or change these settings accordingly). Tegola can then be started as usual and should listen on port 8080:

	tegola serve --config openstreetmap-carto.toml

## Tangram-based rendering

This repository also contains a very basic Tangram style below `tangram` which can be used to render some data in the web browser. This is best done by serving the `tangram` directory with some local web server and then opening the contained `index.html` file in a browser. If your render database contains data from Liechtenstein, you should see some buildings, colorful streets, green trees and some POIs. If you don't have data from Liechtenstein, you can change the parameters to the `map.setView()` call in `index.html`.

## Mapbox-gl-based rendering

This repository also contains a very basic mapbox-gl style below `mapboxgl` which can be used to render some data in the web browser. This is best done by serving the `mapbox` directory with some local web server and then opening the contained `index.html` file in a browser. If your render database contains data from Liechtenstein, you should see some buildings, streets and some water bodies. If you don't have data from Liechtenstein, you can change the `center` parameter to the `mapboxgl.Map()` call in `index.html`.

## `docker-compose`

There is a basic `docker-compose.yml` configuration that is intended to be used in conjunction with the `docker-compose` setup of [openstreetmap-carto](https://github.com/gravitystorm/openstreetmap-carto/blob/master/DOCKER.md). Once this setup is up and running, a command like

    docker-compose -f openstreetmap-carto/docker-compose.yml -f docker-compose.yml up -d webserver tegola

should also start up nginx and Tegola containers. Once they are running, the Tangram-based sample should be available on <http://localhost:3000/tangram/index.html> and the Mapbox-GL one on <http://localhost:3000/mapboxgl/index.html>.
