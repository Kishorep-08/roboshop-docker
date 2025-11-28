FROM node:20
WORKDIR /opt/server
COPY ../catalogue-v3/package.json .
COPY ../catalogue-v3/*.js .
RUN npm install
ENV MONGO="true" \
    MONGO_URL="mongo"
EXPOSE 8080
CMD ["node", "server.js"]