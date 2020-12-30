# version of node to use
FROM node:12
# define working directory for docker
WORKDIR /app
# copy all our source code into the working directory
COPY ["package.json", "package-lock.json*", "./"]

# install npm dependencies and pm2
RUN npm install 
# expose port 3000 for our server to run on

COPY . .

EXPOSE 3000
# command to start our server
CMD [ "node", "/bin/wwww" ]