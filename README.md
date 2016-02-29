# Introduction to docker
The slide deck contains a basic introduction for Docker. The labs are designed for a default Docker and Docker Compose installation using a standard linux shell. The concepts will works for the Docker Toolbox on Windows and Mac as weel but keep in mind you need to replace ip adresses.

- You can see the slides via GitHub static pages [here](http://npalm.github.io/docker-introduction-lb).
- Or just run them in a conainter `docker run -p 80:80 npalm/docker-introduction`

## slides
For the slides we use the [RevealJS](https://github.com/hakimel/reveal.js/) framework.
- See index.html for the slide show composition
- See markdown/* for the slide sources.

### Run the slides from sources
- You can also run the slides locally in a container from sources.
```
docker run -d -p 80:80 --name slides \
  -v ${PWD}:/usr/share/nginx/html nginx
```
- Or use docker-compose to avoid some issues with nginx when running docker in a VM using boot2docker
```
docker compuse up -d
```
- Open a browser [slides](http://localhost/)
