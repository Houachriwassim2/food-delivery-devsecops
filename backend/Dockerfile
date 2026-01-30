FROM node:18-alpine

WORKDIR /app

# Dépendances nécessaires à bcrypt
RUN apk add --no-cache python3 make g++

# Copier package.json seulement
COPY package*.json ./

# Installer les dépendances EN LINUX
RUN npm ci

# Copier le code source (sans node_modules)
COPY . .

EXPOSE 4000
CMD ["node", "server.js"]
