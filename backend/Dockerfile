# -------- STAGE 1 : Build --------
FROM node:18-alpine AS builder

WORKDIR /app

COPY package*.json ./
RUN npm ci --only=production

# -------- STAGE 2 : Runtime --------
FROM node:18-alpine

# Sécurité : utilisateur non-root
RUN addgroup -S nodejs && adduser -S nodejs -G nodejs

WORKDIR /app

COPY --from=builder /app/node_modules ./node_modules
COPY . .

RUN chown -R nodejs:nodejs /app
USER nodejs

EXPOSE 4000

HEALTHCHECK --interval=30s --timeout=3s \
  CMD wget -q --spider http://localhost:4000/health || exit 1

CMD ["node", "server.js"]
