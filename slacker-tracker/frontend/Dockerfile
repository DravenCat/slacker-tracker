# Dockerfile adapted from
# https://mherman.org/blog/dockerizing-a-react-app/

# Build the React app
# basically, this compiles the React jsx to static HTML and js files.
FROM node:14-alpine3.14 as build
WORKDIR /app
ENV PATH /app/node_modules/.bin:$PATH
COPY package.json ./
COPY package-lock.json ./
RUN npm ci --silen --force
RUN npm install react-scripts@3.4.1 -g --silent --force
COPY . ./
RUN npm run build

# Serve these static files with NGINX.
FROM nginx:1.21.6-alpine
COPY --from=build /app/build /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]