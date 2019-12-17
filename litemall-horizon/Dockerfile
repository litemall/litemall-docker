FROM node:12.10-alpine as BUILD-LITEMALL-HORIZON
ARG VERSION=master
ARG VUE_APP_BASE_API=http://127.0.0.1:8081/admin
RUN apk add git \
  && git clone -b $VERSION --dept 1 https://github.com/doopai/litemall-horizon /opt/litemall-horizon \
  && echo "ENV = 'production'" > /opt/litemall-horizon/.env.production \
  && echo "NODE_ENV = production" >> /opt/litemall-horizon/.env.production \
  && echo "NODE_ENV = production" >> /opt/litemall-horizon/.env.production \
  && echo "VUE_APP_BASE_API = '$VUE_APP_BASE_API'" >> /opt/litemall-horizon/.env.production \
  && cd /opt/litemall-horizon \
  && npm install -g cnpm http-server --registry=https://registry.npm.taobao.org \
  && cnpm install \
  && cnpm run build


FROM node:12.10-alpine

COPY --from=BUILD-LITEMALL-HORIZON \
  /opt/litemall-horizon/dist \
  /opt/litemall-horizon

RUN npm install -g http-server

WORKDIR /opt/litemall-horizon

CMD ["http-server", "-a", "0.0.0.0", "-p", "8000"]
