FROM node:22.1 AS build
WORKDIR /usr/src/app
COPY .babelrc ./
COPY package*.json ./
COPY webpack.server.build.config.js ./
COPY webpack.client.build.config.js ./
COPY src src
COPY assets assets
RUN npm install
RUN npm run build
FROM node:22.1
WORKDIR /usr/src/app
COPY --from=build /usr/src/app/package.json package.json
COPY --from=build /usr/src/app/dist dist
RUN npm install --only=production
EXPOSE 8000
CMD [ "npm", "run", "server:production" ]