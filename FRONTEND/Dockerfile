FROM nginx
# WORKDIR /opt/server
RUN rm -rf /usr/share/nginx/html/index.html 
RUN rm -rf /etc/nginx/nginx.conf
RUN rm -rf /etc/nginx/conf.d/default.conf
COPY nginx.conf /etc/nginx/nginx.conf
COPY static /usr/share/nginx/html
# CMD [ "nginx" ] no need , nginx will run automatically 
