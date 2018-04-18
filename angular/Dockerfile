FROM node:8-alpine as node

WORKDIR /opt/app

# set our node environment, either development or production
# defaults to production, compose overrides this to development on build and run
ARG NODE_ENV=prod
ENV NODE_ENV $NODE_ENV

# default to port 4200 for angular cli
ARG PORT=4200
ENV PORT $PORT
EXPOSE $PORT

# install dependencies first, before copying the source code so they are in a separate layer
COPY package.json package-lock.json* ./
RUN npm install && npm cache clean --force

# copy in our source code last, as it changes the most
COPY . .

# Define the command to start the server (the first "--" is needed so the parameters are not consu med by npm itself)
CMD npm start -- --environment=$NODE_ENV

# *********************************************************
# To serve the app in production we can use an nginx server instead of the angular-cli live server.
# In order to do that we would comment out the previous CMD command and comment in the following lines
#RUN npm run build -- --environment=$NODE_ENV
#FROM nginx:1.13
#COPY --from=node /opt/app/dist/ /usr/share/nginx/html
#COPY ./nginx-standalone.conf /etc/nginx/conf.d/default.conf
# In addition to this, some other rules must apply:
#   - the docker-compose file should map port 80 (the default port exposed by nginx), for instance: "80:80"
#   - a file named "nginx-standalone.conf" should exist in the host local folder.
#   - the app compiled will be available on the url localhost:80
# *********************************************************
