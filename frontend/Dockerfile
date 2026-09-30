# =========================
# Stage 1: Build React app
# =========================
FROM node:20-alpine AS build

WORKDIR /app

# Copy dependency files first for Docker layer caching
COPY package*.json ./

RUN npm ci

# Copy source code
COPY . .

# Build Vite application
RUN npm run build

RUN cp -r /app/dist /app/build-output  
# absolute path

# mounting volume se che noi dung co san trong image
# khi build thi dists da nam ben trong image
# 2 container khong tu dong nhin thay filesystem cua nhau
# vi the nen can mot thu trung gian de share files, its volume
# frontend ---> frontend-dists(Docker Volume) <--- nginx
# chinh vi bi che nen ta can create ra 1 ban copy cua dist, la buil-ouput
# ban copy nay se khong bi mount, dist moi la thang bi mount



## =========================
## Stage 2: Serve with NGINX
## =========================
# FROM nginx:alpine

# Copy built files from Stage 1
# COPY --from=build /app/dist /usr/share/nginx/html

# Copy custom NGINX configuration
# COPY nginx.conf /etc/nginx/conf.d/default.conf

# EXPOSE 80

# Container health check
# HEALTHCHECK --interval=30s --timeout=5s --start-period=10s --retries=3 \
#    CMD wget --no-verbose --tries=1 --spider http://127.0.0.1/ || exit 1

# CMD ["nginx", "-g", "daemon off;"]
