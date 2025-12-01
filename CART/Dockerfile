FROM node:20.19.6-alpine AS build  
WORKDIR /opt/server
COPY package.json .
COPY *.js .
RUN npm install

FROM node:20.19.6-alpine
WORKDIR /opt/server
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop && \
    chown -R roboshop:roboshop /opt/server
EXPOSE "80:80"
LABEL com.project="roboshop" \
      component="cart" \
      created_by="Mahaboob"
COPY --from=build --chown=roboshop:roboshop /opt/server /opt/server
USER roboshop
ENV REDIS_HOST="redis" \
    CATALOGUE_HOST="catalogue" \
    CATALOGUE_PORT="8080"
CMD ["node", "server.js"]