# Development Dockerfile for Medusa
FROM node:20-alpine

# Install build tools needed for native modules
RUN apk add --no-cache python3 make g++ libc6-compat

# Enable Corepack so Yarn 4 (defined in packageManager field) is used
RUN corepack enable && corepack prepare yarn@4.4.0 --activate

WORKDIR /app

COPY package.json yarn.lock .yarnrc.yml turbo.json ./
COPY .yarn/releases .yarn/releases
COPY apps/backend/package.json ./apps/backend/
COPY apps/storefront/package.json ./apps/storefront/

RUN yarn install --no-immutable

COPY . .

RUN yarn build

EXPOSE 9000

CMD ["sh", "-c", "yarn medusa db:migrate && yarn start"]
