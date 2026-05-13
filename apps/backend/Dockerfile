# docker build -f apps/backend/Dockerfile . -t backend:1.0.2

ARG NODE_VERSION=24.14.1

FROM node:${NODE_VERSION}-alpine AS build

WORKDIR /app

COPY package*.json ./
COPY apps/backend/package.json ./apps/backend/

RUN npm ci --omit=dev

COPY apps/backend ./apps/backend

FROM node:${NODE_VERSION}-alpine AS run

WORKDIR /app

COPY --from=build /app/node_modules ./node_modules
COPY --from=build /app/apps ./apps

EXPOSE 10000

CMD ["node", "apps/backend/server.js"]