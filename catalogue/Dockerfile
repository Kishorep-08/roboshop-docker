FROM node:20 AS build
WORKDIR /opt/server
COPY ../catalogue-v3/package.json .
COPY ../catalogue-v3/server.js .
RUN npm install

FROM node:20.19-alpine
WORKDIR /opt/server
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop && \
    chown -R roboshop:roboshop /opt/server
ENV MONGO="true" \
    MONGO_URL="mongodb://mongodb:27017/catalogue"    
LABEL created_by="Kishore" \
      component="catalogue" \
      project="roboshop"
EXPOSE 8080
COPY --from=build /opt/server .
USER roboshop
RUN chown -R roboshop:roboshop /opt/server
CMD ["node", "server.js"]