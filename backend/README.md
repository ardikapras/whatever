# Backend service for Whatever

The purpose of this backend is to serve Whatever request (Angular + Bootstrap, not yet finish).

## Tech/framework used

Build with:
* NodeJS
* [OracleDB](https://oracle.github.io/node-oracledb/): Lib to connect to Oracle Database
* [Oracle Client](https://www.oracle.com/database/technologies/instant-client/linux-x86-64-downloads.html): To connect to Oracle Database on other machine
* [Express](https://expressjs.com/): Web application framework
* Morgan: Logger

## Installation

I assume you already install Docker and familiar with it.

### Requirement:
1. Download Oracle Client for Linux 64bit, [oracle-instantclient19.6-basic-19.6.0.0.0-1.x86_64.rpm](https://www.oracle.com/database/technologies/instant-client/linux-x86-64-downloads.html).
2. Put the RPM file into install folder.
3. Let Dockerfile do the job :)

### How to Run

#### Build the image
Open CMD / Terminal in this folder. Run below script to build the images,
```bash
docker build . -t whatever-backend
```
Explanation:
* **docker build .**: To build docker image based on Dockerfile.
* **-t whatever-backend**: To add tag name for this image.

#### Build container
```bash
docker run --name whatever-backend^
 -p 4201:4200 ^
 -v /app/whatever-backend/node_modules ^
 -v %cd%:/app/whatever-backend/ ^
 -d whatever-backend
```
Explanation:
* **docker run --name whatever-backend**: To run docker with name 'whatever-backend'
* **-p 4201:4200**: Port mapping, inside container is using 4200, then in our computer is mapped to 4201
* **-v /app/whatever-backend/node_modules**: To reserve node_modules folder inside container
* **-v %cd%:/app/whatever-backend/**: To allow us to update code from our machine
* **-d whatever-backend**: -d detached mode, and using image 'whatever-backend'

Run below command, to check if node server is up successfully or not
```bash
docker logs whatever-backend

> backend@1.0.0 livereload /app/whatever-backend
> nodemon index.js

[nodemon] 2.0.2
[nodemon] to restart at any time, enter `rs`
[nodemon] watching dir(s): *.*
[nodemon] watching extensions: js,mjs,json
[nodemon] starting `node index.js`
Starting application
Initializing database module
```

#### Go inside the container (optional)
Run below command,
```bash
docker exec -it whatever-backend /bin/sh
```

## Next thing to-do
- [x] Create backend service using nodejs and oracledb
- [x] Dockerize the backend, to minimize the effort of installing dependency of oracledb
- [ ] Test the oracledb and how db connection pool works
- [ ] Create simple API CRUD
- [ ] Create docker compose

## Credits
Inspired by [this awesome web](https://jsao.io/2018/03/creating-a-rest-api-with-node-js-and-oracle-database/)!