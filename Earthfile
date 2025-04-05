VERSION 0.8

# Step 1: Dependencies layer
deps:
    FROM node:18
    WORKDIR /app
    COPY package.json package-lock.json ./
    RUN npm ci

# Step 2: Build layer (no npm build used)
build:
    FROM +deps
    COPY . .
    RUN npm install --omit=dev

# Step 3: Docker image output
docker:
    FROM +build
    ENTRYPOINT ["node", "index.js"]
    SAVE IMAGE node-earthly-app:latest

