# FROM node:20
# WORKDIR /opt/server
# EXPOSE 8080
# COPY package.json .
# COPY *.js .
# RUN npm install
# ENV MONGO=true \
#     REDIS_URL="redis://redis:6379" \
#     MONGO_URL="mongodb://mongodb:27017/users"
# CMD ["node", "server.js"]


FROM node:20.19.6-alpine AS build
WORKDIR /opt/server
COPY package.json .
COPY *.js .
RUN npm install


FROM node:20.19.6-alpine 
WORKDIR /opt/server
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop && \
    chown -R roboshop:roboshop /opt/server
EXPOSE 8080
LABEL com.project="roboshop" \
      component="user" \
      created_by="Mahaboob"
COPY  --from=build --chown=roboshop:roboshop /opt/server /opt/server
USER roboshop
ENV MONGO=true \
    REDIS_URL="redis://redis:6379" \
    MONGO_URL="mongodb://mongodb:27017/users"
CMD [ "server.js"]
ENTRYPOINT [ "node" ]

