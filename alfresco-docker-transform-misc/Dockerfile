# Image provides a container in which to run miscellaneous transformations for Alfresco Content Services.

FROM alfresco/alfresco-base-java:11.0.1-openjdk-centos-7-6784d76a7b81

ENV APACHE_LICENSE_FILE=https://github.com/Alfresco/acs-community-packaging/blob/master/distribution/src/main/resources/licenses/3rd-party/Apache%202.0.txt
ENV JAVA_OPTS=""

# Set default user information
ARG GROUPNAME=Alfresco
ARG GROUPID=1000
ARG USERNAME=transform-misc
ARG USERID=33004

COPY target/alfresco-docker-transform-misc-${env.project_version}.jar /usr/bin

RUN ln /usr/bin/alfresco-docker-transform-misc-${env.project_version}.jar /usr/bin/alfresco-docker-transform-misc.jar && \
    curl -s -S $APACHE_LICENSE_FILE -o Apache\ 2.0.txt && \
    yum clean all

ADD target/generated-resources/licenses              /licenses
ADD target/generated-resources/licenses.xml          /licenses/
ADD target/generated-sources/license/THIRD-PARTY.txt /licenses/

RUN groupadd -g ${GROUPID} ${GROUPNAME} && \
    useradd -u ${USERID} -G ${GROUPNAME} ${USERNAME} && \
    chgrp -R ${GROUPNAME} /usr/bin/alfresco-docker-transform-misc.jar

EXPOSE 8090

USER ${USERNAME}

ENTRYPOINT java $JAVA_OPTS -jar /usr/bin/alfresco-docker-transform-misc.jar
