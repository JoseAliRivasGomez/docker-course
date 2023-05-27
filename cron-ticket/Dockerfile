# FROM --platform=linux/amd64 node:19.2-alpine3.17 as deps
# FROM --platform=$BUILDPLATFORM node:19.2-alpine3.17 as deps
FROM node:19.2-alpine3.17 as deps
# FROM node:19.2-alpine3.17
# /app /usr /lib

# cd /app
WORKDIR /app

# destino /app
COPY package.json ./

# instalar dependencias
RUN npm i



FROM node:19.2-alpine3.17 as builder

# cd /app
WORKDIR /app

# Copia los node_modules de la fase deps
COPY --from=deps /app/node_modules ./node_modules

# destino /app, copy all except .dockerignore
COPY . .

# Realizar testing
RUN npm run test



FROM node:19.2-alpine3.17 as prod-deps

# cd /app
WORKDIR /app

# destino /app
COPY package.json ./

# Unicamente instala las dependencias de produccion
RUN npm i --prod



FROM node:19.2-alpine3.17 as runner

# cd /app
WORKDIR /app

# Copia los node_modules de la fase prod-deps
COPY --from=prod-deps /app/node_modules ./node_modules

COPY app.js ./
COPY tasks/ ./tasks
COPY package.json ./

# Comando run de la imagen
CMD ["node", "app.js"]