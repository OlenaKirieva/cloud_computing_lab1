# Stage 1: Build (Збірка проєкту)
FROM node:18-alpine AS build
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# Stage 2: Production (Роздача статичних файлів через nginx)
FROM nginx:stable-alpine
# Копіюємо зібрані файли з першого етапу в папку nginx
COPY --from=build /app/dist /usr/share/nginx/html
# Копіюємо наш файл конфігурації (ми створимо його наступним кроком)
COPY nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]