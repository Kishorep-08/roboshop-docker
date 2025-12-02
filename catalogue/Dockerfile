FROM node:20 AS build
WORKDIR /opt/server
COPY ../catalogue-v3/package.json .
COPY ../catalogue-v3/server.js .
RUN npm install

FROM node:20.19-alpine
WORKDIR /opt/server
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
ENV MONGO="true" \
    MONGO_URL="mongodb://mongodb:27017/catalogue" \
    component="catalogue"
EXPOSE 8080
COPY --from=build /opt/server .
USER roboshop
CMD ["node", "server.js"]