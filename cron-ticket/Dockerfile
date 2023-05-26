FROM node:19.2-alpine3.17
# /app /usr /lib

# cd /app
WORKDIR /app

# destino /app
COPY package.json ./

# instalar dependencias
RUN npm i

# destino /app
COPY app.js ./

# Comando run de la imagen
CMD ["node", "app.js"]