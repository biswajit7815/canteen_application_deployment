# stage-1-----------------
# create a base image
FROM node:20 AS deps


WORKDIR /app

COPY package*.json ./

RUN npm ci --only=production

COPY . ./

# stage-2-------------------------------
# create a small base image
FROM node:20-alpine AS runner

# create non-root user for security reason
RUN addgroup --system --gid 1001 nodejs && \
    adduser  --system --uid 1001 nodeuser


WORKDIR /app

COPY --from=deps /app/node_modules ./node_modules



COPY  --chown=nodeuser:nodejs . .


USER nodeuser


EXPOSE 5000


HEALTHCHECK --interval=30s --timeout=10s --start-period=30s --retries=3 \
 CMD wget -qO- http://localhost:5000/ || exit 1


CMD ["node","server.js"]
