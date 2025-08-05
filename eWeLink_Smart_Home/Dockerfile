# ARG BUILD_FROM
# FROM $BUILD_FROM

FROM node:14-slim
ENV CK_API_ENV=prod
RUN sed -i 's|http://deb.debian.org/debian|http://archive.debian.org/debian|g' /etc/apt/sources.list && \
    sed -i 's|http://security.debian.org|http://archive.debian.org/debian-security|g' /etc/apt/sources.list && \
    echo 'Acquire::Check-Valid-Until "false";' > /etc/apt/apt.conf.d/99no-check-valid-until && \
    apt-get update && apt-get install -y python build-essential
RUN mkdir -p /workspace/node_modules
COPY ["./dist", "./package.json", "/workspace/"]
WORKDIR /workspace
RUN npm install --production --save-exact
COPY ["./node_modules", "/workspace/node_modules/"]
EXPOSE 3000
CMD npm start
