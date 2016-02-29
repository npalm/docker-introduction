# Introduction to docker
The slide deck contains a basic introduction for Docker. The labs are designed for a default Docker and Docker Compose installation using a standard linux shell. The concepts will works for the Docker Toolbox on Windows and Mac as weel but keep in mind you need to replace ip adresses.

## Start the slides
- You can see the slides via GitHub static pages [here](http://npalm.github.io/docker-introduction-lb).
- You can also run the slides locally in a container.
```
docker run -d -p 80:80 --name slides \
  -v ${PWD}:/usr/share/nginx/html nginx
```
  - Open a browser [slides](http://localhost/)


## slides
For the slides we use the [RealJS](https://github.com/hakimel/reveal.js/) framework.
- See index.html for the slide show composition
- See markdown/* for the slide sources.
