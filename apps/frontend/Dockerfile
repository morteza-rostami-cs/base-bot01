# Stage 1: Build
FROM node:20-alpine AS builder

WORKDIR /app

# Copy package.json & lockfile
COPY package.json package-lock.json ./
RUN npm install

# Copy source code
COPY . .

# Build the Vue app
RUN npm run build

# Stage 2: Serve with Nginx
FROM nginx:alpine

# Copy built files to Nginx html folder
COPY --from=builder /app/dist /usr/share/nginx/html

# Copy custom nginx config (optional)
# COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
