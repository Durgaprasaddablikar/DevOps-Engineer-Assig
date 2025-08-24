# Use Node 18 runtime for production
FROM node:18-alpine AS deps
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production


# Copy source (adjust if your backend build step is needed)
FROM node:18-alpine AS runner
WORKDIR /app
ENV NODE_ENV=production
COPY --from=deps /app/node_modules ./node_modules
COPY . .


# set a non-root user for better security
RUN addgroup -S app && adduser -S app -G app && \
chown -R app:app /app
USER app


EXPOSE 3000
CMD ["node", "src/server.js"]
