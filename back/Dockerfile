# syntax=docker/dockerfile:1.7
FROM node:20-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build


FROM node:20-alpine AS runtime
WORKDIR /app
COPY --from=builder /app/dist ./dist
COPY --from=builder /app/package*.json ./
RUN npm ci --omit-dev

ENV NODE_ENV=production
ENV PORT=3000
EXPOSE $PORT
CMD ["node", "dist/main.js"]
