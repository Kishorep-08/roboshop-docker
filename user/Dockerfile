FROM node:20 AS build
WORKDIR /opt/server
COPY package.json .
COPY server.js .
RUN npm install

FROM node:20.19-alpine
WORKDIR /opt/server
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop 
ENV MONGO="true" \
    REDIS_URL='redis://redis:6379' \
    MONGO_URL="mongodb://mongodb:27017/users"    
LABEL created_by="Kishore" \
      component="catalogue" \
      project="roboshop"
EXPOSE 8080
# Copying build artifacts from build stage
COPY --from=build /opt/server .
# Changing ownership to roboshop user
RUN chown -R roboshop:roboshop /opt/server
USER roboshop
# CMD providing default arguments to ENTRYPOINT - so the CMD that keeps the container running will be CMD ["node", "server.js"]
ENTRYPOINT ["node"]
CMD ["server.js"]


# FROM node:20
# WORKDIR /opt/server
# COPY package.json .
# COPY *js .
# RUN npm install
# ENV MONGO="true" \
#     REDIS_URL='redis://redis:6379' \
#     MONGO_URL="mongodb://mongodb:27017/users"
# EXPOSE 8080
# CMD ["node", "server.js"]