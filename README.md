# Burier

[![forthebadge](https://forthebadge.com/images/badges/pretty-risque.svg)](https://forthebadge.com)
[![forthebadge](https://forthebadge.com/images/badges/oooo-kill-em.svg)](https://forthebadge.com)
[![forthebadge](https://forthebadge.com/images/badges/60-percent-of-the-time-works-every-time.svg)](https://forthebadge.com)

## Information

Burier is a simple hidden web service container that runs over tor network.

During the building of the burier,
1. Downloads tor source code version *0.4.1.6* from its git repository. Then, compiles it.
2. Uses *alexhaydock/mkp224o* docker image in order to generate vanity v3 tor address. **Prints the tor address during the docker-compose building stage.**
3. Starts tor service in a different docker container.
4. Starts *php:7.2-apache* web server image in a different docker container.

Please checkout [docker-compose.yml](docker-compose.yml), [Dockerfile](tor/Dockerfile) and [torrc](tor/storage/torrc) files before you start the burier.

## Dependencies

- docker: 19.03.4-ce
- docker-compose: 1.24.1

## Instructions

1. Clone this repository to your computer
   - `git clone https://github.com/nsa/burier.git` 
2. Change directory into the repository
   - `cd burier`
3. Copy your PHP and/or HTML web site into `web` directory.
4. Initiate docker composer
   - `sudo docker-compose up --build`

It will give you a **v3 tor address** with the prefix `bur`, you can change this prefix from `docker-compose.yml` file.

5. Check your hidden service by using Tor Browser

## TODO:
- Improve this README


## License

```
               GLWT(Good Luck With That) Public License
                 Copyright (c) Everyone, except Mustafa Çalap

Everyone is permitted to copy, distribute, modify, merge, sell, publish,
sublicense or whatever they want with this software but at their OWN RISK.

                            Preamble

The author has absolutely no clue what the code in this project does.
It might just work or not, there is no third option.


                GOOD LUCK WITH THAT PUBLIC LICENSE
   TERMS AND CONDITIONS FOR COPYING, DISTRIBUTION, AND MODIFICATION

  0. You just DO WHATEVER YOU WANT TO as long as you NEVER LEAVE A
TRACE TO TRACK THE AUTHOR of the original product to blame for or hold
responsible.

IN NO EVENT SHALL THE AUTHORS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING
FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER
DEALINGS IN THE SOFTWARE.

Good luck and Godspeed.
```