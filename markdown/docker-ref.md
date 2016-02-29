!SUB
### Docker terminology
|||
|--|--|
|Host       | the machine that is running the containers|
|Image      | a hierarchy of files, with meta-data for how to run a container|
|Container  | a contained running process, started from an image|
|Registry   | a repository of images|
|Volume     | storage outside the container|
|Dockerfile | a script for creating images|

!SUB
### The Life of an Image

| command      | description           |
| ------------ |---------------|
| images       | shows all images|
| build        | creates image from Dockerfile|
| commit       | creates image from a container|
| pull         | pulls an image from registry to local machine|
| push         | pushes an image to the registry from local machine|
| rmi          | removes an image|
| tag          | tags an image to a name (local or registry)}

!SUB
### The Life of a Container

| command      | description           |
| ------------ |---------------|
| create       | creates a container but does not start it|
| run          | creates and starts a container in one operation|
| stop         | stops it|
| start        | starts it again|
| restart      | restarts a container|
| rm           | deletes a container|
| kill         | sends a SIGKILL to a container|
