# Build Stage
FROM node:18-alpine as build

WORKDIR /app

COPY package*.json ./

# Use legacy peer deps for older Material UI versions
RUN npm install --legacy-peer-deps

COPY . .

# Pass build-time environment variable for the API URL
ARG REACT_APP_API_URL
ENV REACT_APP_API_URL=$REACT_APP_API_URL
ENV NODE_OPTIONS=--openssl-legacy-provider

RUN npm run build

# Production Stage
FROM nginx:stable-alpine

COPY --from=build /app/build /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
