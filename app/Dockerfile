FROM node:lts-alpine

EXPOSE 3000

ENV TZ=Asia/Tokyo
ENV LANG=ja_JP.UTF-8

RUN apk update && apk upgrade

WORKDIR /usr/src/app
RUN yarn create next-app \
  --ts --tailwind --eslint \
  --no-app --no-src-dir \
  --import-alias "@/*" \
  --use-yarn \
  sample

WORKDIR /usr/src/app/sample

RUN yarn build

CMD [ "yarn", "start" ]
