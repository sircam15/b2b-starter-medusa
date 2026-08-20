FROM node:20-alpine

RUN apk add --no-cache python3 make g++ libc6-compat

RUN corepack enable && corepack prepare yarn@4.4.0 --activate

WORKDIR /medusa

COPY package.json yarn.lock .yarnrc.yml ./

RUN yarn install --no-immutable

COPY . .

RUN NODE_OPTIONS=--max-old-space-size=2048 yarn build

EXPOSE 9000

CMD ["sh", "-c", "yarn medusa db:migrate && yarn start"]
