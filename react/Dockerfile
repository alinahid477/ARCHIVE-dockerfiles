FROM node:latest

# RUN npm config get proxy && npm config rm proxy && npm config rm https-proxy && npm install && npm install react-scripts@3.4.1 -g --silent
# RUN which npm
# RUN npm config get registry
# RUN npm config set strict-ssl false
# the set registry to https://registry.npmjs.com/ WAS SUPER CRITICAL
RUN npm config set registry https://registry.npmjs.com/
# RUN npm cache clear --force
# RUN npm config set unsafe-perm true
# RUN npm install
RUN npm install react-scripts@3.4.1 -g