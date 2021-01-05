# version of node to use
FROM node:12
# define working directory for docker
WORKDIR /app

# install npm dependencies and pm2 && npm install -g pm2
COPY ["package.json", "package-lock.json*", "./"]
RUN npm install 

# copy all our source code into the working directory
COPY . .

# expose port 3000 for our server to run on
EXPOSE 3000

# command to start our server "pm2-runtime"
CMD [ "node", "./bin/www" ]