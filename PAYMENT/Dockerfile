# FROM python:3.9
# WORKDIR /opt/server
# COPY payment.ini .
# COPY *.py .
# COPY requirements.txt .
# RUN pip3 install -r requirements.txt
# ENV CART_HOST="cart" \
#     CART_PORT="8080" \
#     USER_HOST="user" \
#     USER_PORT="8080" \
#     AMQP_HOST="rabbitmq"  \
#     AMQP_USER="roboshop" \
#     AMQP_PASS="roboshop123"
# CMD [ "uwsgi","--ini","payment.ini" ]    

FROM python:3.11-slim AS build
WORKDIR /opt/server

# COPY payment.ini *.py requirements.txt . /
COPY payment.ini .
COPY *.py .
COPY requirements.txt . 
# RUN pip3 install --prefix=/install -r requirements.txt
RUN pip3 install --prefix=/install -r requirements.txt


FROM python:3.11-slim
WORKDIR /opt/server
EXPOSE 8080
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop 
LABEL com.project="roboshop" \
      component="payment" \
      creater="Mahaboob"
ENV CART_HOST="cart" \
    CART_PORT="8080" \
    USER_HOST="user" \
    USER_PORT="8080" \
    AMQP_HOST="rabbitmq"  \
    AMQP_USER="roboshop" \
    AMQP_PASS="roboshop123"

COPY --from=build chown=roboshop /install /usr/local/bin/
COPY --chown=roboshop:roboshop payment.ini .
COPY *.py .
COPY requirements.txt .

CMD [ "uwsgi","--ini","payment.ini" ]