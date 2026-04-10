# --- Stage 1: builder ---
FROM node:18-alpine AS builder

WORKDIR /app

# Copy dependencies
COPY package*.json ./
RUN npm ci

# Copy source code
COPY . .


# --- Stage 2: production ---
FROM node:18-alpine

WORKDIR /app

# Install only production dependencies
COPY package*.json ./
RUN npm ci --only=production

# Copy full app from builder
COPY --from=builder /app ./

# Expose backend port
EXPOSE 8080

# Run server
CMD ["npm", "start"]