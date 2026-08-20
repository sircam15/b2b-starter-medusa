FROM node:18-alpine

RUN apk add --no-cache python3 make g++ libc6-compat

RUN corepack enable && corepack prepare yarn@4.4.0 --activate

WORKDIR /app

COPY package.json yarn.lock .yarnrc.yml ./

RUN yarn install --no-immutable

COPY . .

RUN yarn medusa build

EXPOSE 9000

CMD ["sh", "-c", "yarn medusa db:migrate && yarn start"]
