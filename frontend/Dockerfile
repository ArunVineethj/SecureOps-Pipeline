# Stage 1: Build React app
FROM node:20-alpine AS build
WORKDIR /app

COPY package*.json ./
RUN npm ci --legacy-peer-deps

COPY . .

ARG REACT_APP_BASE_URL
ENV REACT_APP_BASE_URL=$REACT_APP_BASE_URL

RUN npm run build

# Stage 2: Serve static files on port 3000
FROM nginx:alpine
RUN sed -i 's/listen       80;/listen       3000;/' /etc/nginx/conf.d/default.conf \
    && sed -i 's|index  index.html index.htm;|index  index.html index.htm;\n        try_files $uri $uri/ /index.html;|' /etc/nginx/conf.d/default.conf

COPY --from=build /app/build /usr/share/nginx/html

EXPOSE 3000
CMD ["nginx", "-g", "daemon off;"]