# builder is the first step of multi step build process
FROM node:alpine as builder
WORKDIR '/app'
COPY ./package.json ./
RUN npm install
COPY ./ ./
run npm run build

# set up nginx production server for react app
FROM nginx
# listens on port 3000
EXPOSE 3000
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
# copy built files from builder step into the production server
COPY --from=builder /app/build /usr/share/nginx/html
