FROM azul/zulu-openjdk-alpine:8u162

LABEL maintainer="qaware-oss@qaware.de"

ENV PAYARA_PATH /opt/payara

RUN apk -q add wget && \
 mkdir -p $PAYARA_PATH/deployments && \
 mkdir -p $PAYARA_PATH/libs && \
 adduser -D -h $PAYARA_PATH payara && echo payara:payara | chpasswd && \
 chown -R payara:payara /opt

ENV PAYARA_PKG https://search.maven.org/remotecontent?filepath=fish/payara/extras/payara-micro/5.181/payara-micro-5.181.jar
ENV PAYARA_VERSION 5.181
ENV PKG_FILE_NAME payara-micro.jar

RUN wget --quiet -O $PAYARA_PATH/$PKG_FILE_NAME $PAYARA_PKG

ENV DEPLOY_DIR $PAYARA_PATH/deployments
ENV AUTODEPLOY_DIR $PAYARA_PATH/deployments
ENV PAYARA_MICRO_JAR=$PAYARA_PATH/$PKG_FILE_NAME

# Default payara ports to expose
EXPOSE 8080 8181 5900 6900

USER payara
WORKDIR $PAYARA_PATH

ENTRYPOINT ["java", "-server", "-XX:+UnlockExperimentalVMOptions", "-XX:+UseCGroupMemoryLimitForHeap", "-XX:MaxRAMFraction=3", "-XX:ThreadStackSize=256", "-XX:MaxMetaspaceSize=128m", "-XX:+UseG1GC", "-XX:ParallelGCThreads=2", "-XX:CICompilerCount=2", "-XX:+UseStringDeduplication", "-jar", "/opt/payara/payara-micro.jar"]
CMD ["--deploymentDir", "/opt/payara/deployments"]
