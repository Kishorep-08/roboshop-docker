FROM node:20
WORKDIR /opt/server
COPY ../catalogue-v3/package.json .
COPY ../catalogue-v3/server.js .
RUN npm install
ENV MONGO="true" \
    MONGO_URL="mongodb://mongodb:27017/catalogue" \
    component="catalogue"
EXPOSE 8080
CMD ["node", "server.js"]