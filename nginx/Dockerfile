FROM nginx

EXPOSE 80

RUN rm -rf /usr/share/nginx/html/index.html
COPY ./html /usr/share/nginx/html

ENTRYPOINT ["nginx", "-g", "daemon off;"]
