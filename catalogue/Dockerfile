FROM node:20 AS build
WORKDIR /opt/server
COPY package.json .
COPY server.js .
RUN npm install

FROM node:20.19-alpine
WORKDIR /opt/server
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop 
ENV MONGO="true" \
    MONGO_URL="mongodb://mongodb:27017/catalogue"    
LABEL created_by="Kishore" \
      component="catalogue" \
      project="roboshop"
EXPOSE 8080
COPY --from=build /opt/server .
RUN chown -R roboshop:roboshop /opt/server
USER roboshop
ENTRYPOINT ["node"]
CMD ["server.js"]