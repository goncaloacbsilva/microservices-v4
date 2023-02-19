FROM gxspace/svc-base

WORKDIR /app

ENV PORT=3333
EXPOSE ${PORT}

RUN yarn nx run service-2:build:production

CMD ["yarn", "nx", "run", "service-2:serve:production"]
