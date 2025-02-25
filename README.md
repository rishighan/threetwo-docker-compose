## docker-compose configuration for [ThreeTwo](https://github.com/rishighan/threetwo)

This repo contains the `docker-compose` files necessary to run:

1. ThreeTwo UI
2. `threetwo-core-service` and its dependencies
3. `threetwo-metadata-service` and its dependencies
4. `threetwo-acquisition-service` and its dependencies
5. `elasticsearch`, `kafka`, `zookeeper`, `mongo` and `redis`


### Pre-requisites

#### Docker and docker-compose

You need both `docker` and `docker-compose` installed on your OS. Currently, `Docker version 20.10.10, build b485636` and `docker-compose version 1.29.2, build 5becea4c` have tested well on `Debian 4.19.208-1`

#### `comics` and `userdata` folders

You need 2 folders:

1. `comics` will contain your... comics
2. `userdata` will be used by the app to create app-specific files
3. The structure should be like so:

   ```
   - comics
   - userdata
   ```

#### ComicVine

To get ComicVine to work for metadata scraping and other functions, you _must_ have a ComicVine API key.
You can get one [here.](https://comicvine.gamespot.com/api/) Metadata scraping will not work unless you supply an API key.

#### AirDC++

1. To use AirDC++, you need a working install of... [AirDC++](https://www.airdcpp.net/download)
2. Then within the UI, you need to set up the connection at `Settings > Acquisition > AirDC++ > Connection`
3. After successfully connecting, you need to select your default hubs for search under `Settings > Acquisition > AirDC++ > Hubs`

## Building the stack

1. Clone this repo
2. Create a network using `docker network create proxy`
3. Edit the `docker-compose.env` file
   1. Find the hostname of your machine and set the `UNDERLYING_HOSTNAME` to that. For e.g. `UNDERLYING_HOSTNAME=foo`
   2. Set the `COMICS_DIRECTORY` and `USERDATA_DIRECTORY` to the correct _absolute_ paths
   3. Set the `COMICVINE_API` to your ComicVine API key
   4. To summarize, these are the only variables you need to configure:
      ```
       UNDERLYING_HOSTNAME=myhost
       
       COMICS_DIRECTORY=/path/to/comics
       USERDATA_DIRECTORY=/path/to/userdata
       
       COMICVINE_API_KEY=onethreetwo
      ```
4. Save the file
5. Run the stack using: `env $(cat docker-compose.env | xargs) docker-compose up`

### Ports

1. `threetwo`, the UI runs on port `5173`
2. `threetwo-core-service` service on `3000`
3. `threetwo-metadata-service` service on `3080`


## Troubleshooting

General

1. Some common problems can be traced to out-of-date images, and as such can be mitigated by simply pruning orphaned images: `docker system prune -a`
2. Always check the logs of the offending service, `docker logs --follow <servicename>`
3. Once the stack is up, assuming everything went well, look for `threetwo-ui` service's logs to see something like:

   ```
   threetwo-ui       |   VITE v5.2.7  ready in 145 ms
   threetwo-ui       |
   threetwo-ui       |   ➜  Local:   http://localhost:5173/
   threetwo-ui       |   ➜  Network: http://172.30.0.9:5173/
```

