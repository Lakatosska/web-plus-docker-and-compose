# multi-stage

FROM node:16-alpine as build
WORKDIR /app
COPY ./package*.json ./
RUN npm i
COPY . .
RUN npm run build

FROM node:16-alpine as production
WORKDIR /app
COPY ./package*.json ./
RUN npm i --omit=dev && npm i pm2 -g
COPY --from=build /app/dist ./dist
COPY ./ecosystem.config.js .
EXPOSE 4000
CMD [ "pm2-runtime", "start", "ecosystem.config.js"]