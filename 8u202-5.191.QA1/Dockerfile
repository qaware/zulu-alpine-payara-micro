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

ENV PAYARA_PKG https://dl.bintray.com/qaware-oss/generic/payara-micro/$PAYARA_TAG/payara-micro.jar
ENV PAYARA_VERSION $PAYARA_RELEASE
ENV PKG_FILE_NAME payara-micro.jar

USER payara
WORKDIR $PAYARA_PATH

RUN curl --silent --show-error --output $PAYARA_PATH/$PKG_FILE_NAME -L $PAYARA_PKG

ENV DEPLOY_DIR $PAYARA_PATH/deployments
ENV AUTODEPLOY_DIR $PAYARA_PATH/deployments
ENV PAYARA_MICRO_JAR=$PAYARA_PATH/$PKG_FILE_NAME

# Default payara ports to expose
EXPOSE 8080 8443 6900

ENTRYPOINT ["java", "-server", "-Xshare:on", "-XX:+UnlockExperimentalVMOptions", "-XX:+UseCGroupMemoryLimitForHeap", "-XX:MaxRAMFraction=3", "-XX:ThreadStackSize=256", "-XX:MaxMetaspaceSize=128m", "-XX:+UseG1GC", "-XX:ParallelGCThreads=2", "-XX:CICompilerCount=2", "-XX:+UseStringDeduplication", "-jar", "/opt/payara/payara-micro.jar"]
CMD ["--deploymentDir", "/opt/payara/deployments"]
