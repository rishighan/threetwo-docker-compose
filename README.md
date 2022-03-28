## docker-compose configuration for [ThreeTwo](https://github.com/rishighan/threetwo)

This repo contains the `docker-compose` files necessary to run:

1. ThreeTwo UI
2. `threetwo-core-service` and its dependencies
3. `threetwo-metadata-service` and its dependencies


### Pre-requisites

#### Docker and docker-compose

You need both `docker` and `docker-compose` installed on your OS. Currently, `Docker version 20.10.10, build b485636` and `docker-compose version 1.29.2, build 5becea4c` have tested well on `Debian 4.19.208-1`

#### `comics` and `userdata` folders

You need 2 folders:

1. `comics` will contain your... comics
2. `userdata` will be used by the app to create app-specific files


#### ComicVine

To get ComicVine to work for metadata scraping and other functions, you _must_ have a ComicVine API key.
You can get one [here.](https://comicvine.gamespot.com/api/) Metadata scraping will not work unless you supply an API key.

#### AirDC++

1. To use AirDC++, you need a working install of... [AirDC++](https://www.airdcpp.net/download)
2. Then within the UI, you need to set up the connection at `Settings > Acquisition > AirDC++ > Connection`
3. After successfully connecting, you need to select your default hubs for search under `Settings > Acquisition > AirDC++ > Hubs`

## Building the stack

1. Clone this repo
2. Edit the `docker-compose.env` file
