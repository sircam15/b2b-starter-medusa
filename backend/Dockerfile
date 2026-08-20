# Development Dockerfile for Medusa
FROM node:18-alpine

# Install build tools needed for native modules
RUN apk add --no-cache python3 make g++ libc6-compat

# Enable Corepack so Yarn 4 (defined in packageManager field) is used
RUN corepack enable && corepack prepare yarn@4.4.0 --activate

WORKDIR /app

COPY package.json yarn.lock .yarnrc.yml ./

RUN yarn install --immutable

COPY . .

RUN yarn build

EXPOSE 9000

CMD ["sh", "-c", "yarn medusa db:migrate && yarn start"]
