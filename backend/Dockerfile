FROM node:latest

### Set the working directory
WORKDIR /app/whatever-backend/

### Update nodejs
RUN npm install npm@latest -g

### Installation for oracle client
RUN apt-get update && apt-get install yum alien libaio1 libaio-dev -y
COPY install/oracle-instantclient19.6-basic-19.6.0.0.0-1.x86_64.rpm ./install/
RUN alien -i install/oracle-instantclient19.6-basic-19.6.0.0.0-1.x86_64.rpm
ENV LD_LIBRARY_PATH=/usr/lib/oracle/19.6/client64/lib:$LD_LIBRARY_PATH

### Configuration of npm proxy and registry
### Comment it if no need
#RUN npm config list
#RUN npm config set proxy http://proxyip:proxyport/
#RUN npm config set registry "http://r.cnpmjs.org/"
#RUN npm config list

### Copy and install nodejs dependency
COPY package*.json ./
RUN npm install
RUN npm update

### Config to auto-reload changes
RUN npm install -g nodemon

EXPOSE 4200

### Copy whole code to container
COPY . .

CMD ["npm", "run", "livereload"]