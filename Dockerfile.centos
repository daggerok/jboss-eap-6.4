FROM daggerok/jboss-eap-6.4:6.4.9-centos
LABEL MAINTAINER='Maksim Kostromin <daggerok@gmail.com>'
ENV PRODUCT='jboss-eap-6.4' \
    JBOSS_USER='jboss'
ENV JBOSS_USER_HOME="/home/${JBOSS_USER}" \
    DOWNLOAD_BASE_URL="https://github.com/daggerok/${PRODUCT}/releases/download" \
    JBOSS_EAP_PATCH='6.4.19'
ENV JBOSS_HOME="${JBOSS_USER_HOME}/${PRODUCT}" \
    PATCHES_BASE_URL="${DOWNLOAD_BASE_URL}/${JBOSS_EAP_PATCH}"
ENV PATH="${JBOSS_HOME}/bin:/tmp:${PATH}"
USER ${JBOSS_USER}
RUN sudo yum update --security -y \
 && sudo yum update -y \
 && sudo yum autoremove -y \
 && sudo yum clean all -y
WORKDIR /tmp
ADD --chown=jboss ./install.sh .
RUN ( standalone.sh --admin-only & ( sudo chmod +x /tmp/install.sh && install.sh && sudo rm -rf /tmp/* ) )
WORKDIR ${JBOSS_USER_HOME}

# ############################################### USAGE ##################################################
# #                                                                                                      #
# # FROM daggerok/jboss-eap-6.4:6.4.19-centos                                                             #
# #                                                                                                      #
# # # debug:                                                                                             #
# # ENV JAVA_OPTS="$JAVA_OPTS -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=5005"        #
# # EXPOSE 5005                                                                                          #
# #                                                                                                      #
# # # health check:                                                                                      #
# # HEALTHCHECK --timeout=1s \                                                                           #
# #             --retries=33 \                                                                           #
# #             CMD test `netstat -ltnp | grep 9990 | wc -l` -ge 1 || exit 1                             #
# # # or:                                                                                                #
# # HEALTHCHECK --timeout=1s \                                                                           #
# #             --retries=33 \                                                                           #
# #             CMD wget -q --spider http://127.0.0.1:8080/my-service/health || exit 1                   #
# #                                                                                                      #
# # # multi deployment:                                                                                  #
# # COPY --chown=jboss ./path/to/apps/*.war ./path/to/libs/*.war ${JBOSS_HOME}/standalone/deployments/   #
# #                                                                                                      #
# ########################################################################################################
#
# # FROM registry.access.redhat.com/rhel7:7.6-119 or rhel7-minimal:7.6-119
# # https://access.redhat.com/containers/?tab=changeSummary
# FROM centos:centos7.5.1804
# LABEL MAINTAINER='Maksim Kostromin <daggerok@gmail.com>'
# ENV PRODUCT='jboss-eap-6.4'                                                                            \
#     JBOSS_USER='jboss'
# ENV ADMIN_USER='admin'                                                                                 \
#     ADMIN_PASSWORD='Admin.123'                                                                         \
#     JDK_VERSION='jdk1.8.0_191'                                                                         \
#     JBOSS_USER_HOME="/home/${JBOSS_USER}"                                                              \
#     DOWNLOAD_BASE_URL="https://github.com/daggerok/${PRODUCT}/releases/download"                       \
#     JBOSS_EAP_PATCH='6.4.5'
# ENV JBOSS_HOME="${JBOSS_USER_HOME}/${PRODUCT}"                                                         \
#     ARCHIVES_BASE_URL="${DOWNLOAD_BASE_URL}/archives"                                                  \
#     PATCHES_BASE_URL="${DOWNLOAD_BASE_URL}/${JBOSS_EAP_PATCH}"
# ENV PATH="${JBOSS_HOME}/bin:/tmp:${PATH}"                                                              \
#     JAVA_HOME="/usr/lib/jvm/${JDK_VERSION}"
# USER root
# RUN yum update -y                                                                                   && \
#     yum update --security -y                                                                        && \
#     yum install -y wget ca-certificates unzip sudo openssh-client unzip zip net-tools               && \
#     echo "${JBOSS_USER} ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers                                    && \
#     adduser -U -m -d /home/jboss -s /bin/bash jboss                                                 && \
#     usermod -a -G ${JBOSS_USER} ${JBOSS_USER}
# USER ${JBOSS_USER}
# CMD /bin/bash
# ENTRYPOINT standalone.sh
# EXPOSE 8080 8443 9990 9999
# WORKDIR /tmp
# ADD --chown=jboss ./install.sh .
# RUN wget ${ARCHIVES_BASE_URL}/${JDK_VERSION}.tar.gz                                                    \
#          -q --no-cookies --no-check-certificate -O /tmp/${JDK_VERSION}.tar.gz                       && \
#     sudo mkdir -p /usr/lib/jvm                                                                      && \
#     sudo tar xzfz /tmp/${JDK_VERSION}.tar.gz -C /usr/lib/jvm/                                       && \
#     wget ${ARCHIVES_BASE_URL}/jce_policy-8.zip                                                         \
#          -q --no-cookies --no-check-certificate -O /tmp/jce_policy-8.zip                            && \
#     unzip -q /tmp/jce_policy-8.zip -d /tmp                                                          && \
#     ( sudo mv -f ${JAVA_HOME}/lib/security ${JAVA_HOME}/lib/backup-security || echo 'no backups.' ) && \
#     sudo mv -f /tmp/UnlimitedJCEPolicyJDK8 ${JAVA_HOME}/lib/security                                && \
#     wget ${ARCHIVES_BASE_URL}/jboss-eap-6.4.0.zip                                                      \
#          -q --no-cookies --no-check-certificate -O /tmp/jboss-eap-6.4.0.zip                         && \
#     unzip -q /tmp/jboss-eap-6.4.0.zip -d ${JBOSS_USER_HOME}                                         && \
#     add-user.sh ${ADMIN_USER} ${ADMIN_PASSWORD} --silent                                            && \
#     echo 'JAVA_OPTS="-Djboss.bind.address=0.0.0.0 -Djboss.bind.address.management=0.0.0.0"'            \
#          >> ${JBOSS_HOME}/bin/standalone.conf                                                       && \
#     sudo yum autoremove -y                                                                          && \
#     sudo yum clean all -y                                                                           && \
#     sudo rm -rf /tmp/*.zip /tmp/*.tar.gz /var/cache/yum                                             && \
#     ( standalone.sh --admin-only                                                                       \
#       & ( sudo chmod +x /tmp/install.sh && install.sh && rm -rf /tmp/install.sh ) )
# WORKDIR ${JBOSS_USER_HOME}
