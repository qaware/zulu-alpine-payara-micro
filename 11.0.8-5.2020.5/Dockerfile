ARG ZULU_VERSION
FROM azul/zulu-openjdk-alpine:$ZULU_VERSION

LABEL maintainer="qaware-oss@qaware.de"

ENV PAYARA_PATH /opt/payara

RUN apk -q add curl && \
  mkdir -p $PAYARA_PATH/deployments && \
  mkdir -p $PAYARA_PATH/libs && \
  adduser -D -h $PAYARA_PATH payara && echo payara:0 | chpasswd && \
  chown -R payara:0 $PAYARA_PATH && \
  echo "export PS1='> '" >> /etc/bash.bashrc && \
  echo "alias ll='ls -al'" >> /etc/bash.bashrc && \
  java -Xshare:dump

ARG PAYARA_TAG
ARG PAYARA_RELEASE

ENV PAYARA_PKG https://search.maven.org/remotecontent?filepath=fish/payara/extras/payara-micro/$PAYARA_TAG/payara-micro-$PAYARA_TAG.jar
ENV PAYARA_VERSION $PAYARA_RELEASE
ENV PKG_FILE_NAME payara-micro.jar

USER payara
WORKDIR $PAYARA_PATH

RUN curl --silent --location --show-error --output $PAYARA_PATH/$PKG_FILE_NAME $PAYARA_PKG

ENV DEPLOY_DIR $PAYARA_PATH/deployments
ENV AUTODEPLOY_DIR $PAYARA_PATH/deployments
ENV PAYARA_MICRO_JAR=$PAYARA_PATH/$PKG_FILE_NAME

# Default payara ports to expose
EXPOSE 8080 8443 6900

ENTRYPOINT ["java", "-server", "-Xshare:auto", "-XX:+UseContainerSupport", "-XX:MaxRAMPercentage=50.0", "-XX:ThreadStackSize=256", "-XX:MaxMetaspaceSize=128m", "-XX:+UseG1GC", "-XX:MaxGCPauseMillis=500", "-XX:+UseStringDeduplication", "-jar", "/opt/payara/payara-micro.jar"]
CMD ["--nocluster", "--disablephonehome", "--deploymentDir", "/opt/payara/deployments"]
