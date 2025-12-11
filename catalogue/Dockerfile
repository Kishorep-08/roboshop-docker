
FROM node:20 AS build
WORKDIR /opt/server
COPY package.json .
COPY server.js .
RUN npm install

FROM gcr.io/distroless/nodejs20-debian12
WORKDIR /opt/server
ENV MONGO="true" \
    MONGO_URL="mongodb://mongodb:27017/catalogue"    
LABEL created_by="Kishore" \
      component="catalogue" \
      project="roboshop"
EXPOSE 8080
# Copying build artifacts from build stage and also changing ownership to roboshop user. This is more efficient way than using separate RUN command for ownership change
COPY --from=build --chown=roboshop:roboshop /opt/server .
# CMD providing default arguments to ENTRYPOINT - so the CMD that keeps the container running will be CMD ["node", "server.js"]
ENTRYPOINT ["node"]
CMD ["server.js"]