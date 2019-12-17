FROM maven:3.6-jdk-8 as BUILD-LITEMALL
ARG VERSION=master
RUN git clone -b $VERSION --dept 1 https://github.com/doopai/litemall /opt/litemall \
  && cd /opt/litemall \
  && mvn clean package

FROM openjdk:8-jdk

RUN mkdir /opt/litemall
COPY --from=BUILD-LITEMALL \
  /opt/litemall/litemall-admin/target/litemall-admin-*-exec.jar \
  /opt/litemall/admin.jar

COPY --from=BUILD-LITEMALL \
  /opt/litemall/litemall-apollo/target/litemall-apollo-*-exec.jar \
  /opt/litemall/apollo.jar
