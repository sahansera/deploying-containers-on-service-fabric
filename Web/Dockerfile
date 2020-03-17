# Stage 1 - the build process
FROM node as build-deps
WORKDIR /usr/src/app
COPY web-client/package.json web-client/yarn.lock ./
RUN yarn --no-bin-links
COPY ./web-client/. ./
RUN yarn build

# Stage 2 - the deploy process
FROM nginx
COPY --from=build-deps /usr/src/app/build /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]