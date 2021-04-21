# Building stage
FROM registry.access.redhat.com/ubi8/ubi:8.1 AS builder

USER root
RUN  mkdir /code1
WORKDIR /code1
COPY package.json package-lock.json ./
RUN npm install
COPY . .
RUN npm run build 

### Stage 2: delivery ###
FROM registry.access.redhat.com/ubi8/nginx-116
# Remove default nginx website
RUN rm -rf /usr/share/nginx/html/*

# Copy output directory from builder to nginx image.
COPY --from=builder /code1/dist/* /usr/share/nginx/html

# Copy nginx configuration file.
COPY ./nginx/nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 4500
