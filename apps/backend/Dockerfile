# Stage 1: Build
FROM node:20-alpine AS builder

WORKDIR /app

# Copy package.json & lockfile
COPY package.json package-lock.json ./
# Install dependencies
RUN npm install --legacy-peer-deps

# Copy source code
COPY . .

# Build TypeScript
RUN npm run build

# Stage 2: Production
FROM node:20-alpine

WORKDIR /app

# Copy built files and node_modules
COPY --from=builder /app/dist ./dist
COPY --from=builder /app/node_modules ./node_modules
COPY package.json ./

# Expose port
EXPOSE 5000

# Run the backend
CMD ["node", "dist/index.js"]
