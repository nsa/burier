# Burier

[![forthebadge](https://forthebadge.com/images/badges/pretty-risque.svg)](https://forthebadge.com)
[![forthebadge](https://forthebadge.com/images/badges/oooo-kill-em.svg)](https://forthebadge.com)
[![forthebadge](https://forthebadge.com/images/badges/60-percent-of-the-time-works-every-time.svg)](https://forthebadge.com)

Burier is a simple hidden web service container that runs over tor network.

During the building of the burier,
1. Downloads tor source code version *0.4.5* from its git repository. Then, compiles it.
2. Uses *alexhaydock/mkp224o* docker image in order to generate vanity v3 tor address. **Prints the tor address during the docker-compose building stage.**
3. Starts tor service in a different docker container.
4. Starts *php:7.2-apache* web server image in a different docker container.

Please checkout [docker-compose.yml](docker-compose.yml), [Dockerfile](tor/Dockerfile) and [torrc](tor/storage/torrc) files before you start the burier.

## Dependencies

- docker: tested on version 19.03.13-ce
- docker-compose: tested on version 1.25.5

## Instructions

1. Clone this repository to your computer
   - `git clone --depth 1 https://github.com/nsa/burier.git`
   - `cd burier`
2. Copy your PHP and/or HTML web site into `web` directory.
3. Initiate docker composer
   - `docker-compose up --build` (**SUDO** power may be needed)

It will give you a **v3 tor address** with the prefix `bur`, you can change this prefix from `docker-compose.yml` file.

4. Check your hidden service by using Tor Browser

## Troubleshooting

- **Problem bootstrapping. Stuck at 10% (conn_done): Connected to a relay.**
  - This could mean that your tor connection is blocked. You may try tor bridges.
  - Open [torrc](tor/storage/torrc) file with an editor and uncomment these lines: 6,7,8.
  - Request a bridge from [here](https://bridges.torproject.org/bridges?transport=obfs4) and change the [line 8](/tor/storage/torrc#L8) of [torrc](tor/storage/torrc) file with your new bridge or insert it as a new line.
  - Run `docker-compose up --build` command again.

## TODO:
- Make an option for importing existing tor address keys.
- Improve this README

