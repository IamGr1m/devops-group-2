# --- Stage 1: builder ---
FROM node:18-alpine AS builder

WORKDIR /app

COPY package*.json ./
RUN npm ci

COPY . .

# Build React app
RUN npm run build


# --- Stage 2: production ---
FROM node:18-alpine

WORKDIR /app

# Install serve
RUN npm install -g serve

# Copy build folder
COPY --from=builder /app/build ./build

# Expose frontend port
EXPOSE 80

# Run React app
CMD ["serve", "-s", "build", "-l", "3000"]