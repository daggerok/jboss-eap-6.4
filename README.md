# jboss-eap-6.4 [![CI](https://github.com/daggerok/jboss-eap-6.4/actions/workflows/ci.yaml/badge.svg)](https://github.com/daggerok/jboss-eap-6.4/actions/workflows/ci.yaml)
Patched JBoss EAP 6.4 (including __6.4.22 patch__) Docker automation build based on centos8 / alpine3.9 images

This image is located on [docker hun](https://hub.docker.com/r/daggerok/jboss-eap-6.4/) as `daggerok/jboss-eap-6.4`

## tags

- [latest](https://github.com/daggerok/jboss-eap-6.4/blob/master/Dockerfile)

- [6.4.22-alpine](https://github.com/daggerok/jboss-eap-6.4/blob/6.4.22-alpine/Dockerfile)
- [6.4.22-centos](https://github.com/daggerok/jboss-eap-6.4/blob/6.4.22-centos/Dockerfile)

- [6.4.21-alpine](https://github.com/daggerok/jboss-eap-6.4/blob/6.4.21-alpine/Dockerfile)
- [6.4.21-centos](https://github.com/daggerok/jboss-eap-6.4/blob/6.4.21-centos/Dockerfile)

- [6.4.20-alpine](https://github.com/daggerok/jboss-eap-6.4/blob/6.4.20-alpine/Dockerfile)
- [6.4.20-centos](https://github.com/daggerok/jboss-eap-6.4/blob/6.4.20-centos/Dockerfile)

- [6.4.19-alpine](https://github.com/daggerok/jboss-eap-6.4/blob/6.4.19-alpine/Dockerfile)
- [6.4.19-centos](https://github.com/daggerok/jboss-eap-6.4/blob/6.4.19-centos/Dockerfile)

- [6.4.9-alpine](https://github.com/daggerok/jboss-eap-6.4/blob/6.4.9-alpine/Dockerfile)
- [6.4.9-centos](https://github.com/daggerok/jboss-eap-6.4/blob/6.4.9-centos/Dockerfile)

- [6.4.5-alpine](https://github.com/daggerok/jboss-eap-6.4/blob/6.4.5-alpine/Dockerfile)
- [6.4.5-centos](https://github.com/daggerok/jboss-eap-6.4/blob/6.4.5-centos/Dockerfile)

- [6.4.4-alpine](https://github.com/daggerok/jboss-eap-6.4/blob/6.4.4-alpine/Dockerfile)
- [6.4.4-centos](https://github.com/daggerok/jboss-eap-6.4/blob/6.4.4-centos/Dockerfile)

- [6.4.3-alpine](https://github.com/daggerok/jboss-eap-6.4/blob/6.4.3-alpine/Dockerfile)
- [6.4.3-centos](https://github.com/daggerok/jboss-eap-6.4/blob/6.4.3-centos/Dockerfile)

- [6.4.2-alpine](https://github.com/daggerok/jboss-eap-6.4/blob/6.4.2-alpine/Dockerfile)
- [6.4.2-centos](https://github.com/daggerok/jboss-eap-6.4/blob/6.4.2-centos/Dockerfile)

- [6.4.1-alpine](https://github.com/daggerok/jboss-eap-6.4/blob/6.4.1-alpine/Dockerfile)
- [6.4.1-centos](https://github.com/daggerok/jboss-eap-6.4/blob/6.4.1-centos/Dockerfile)

- [6.4.0-alpine](https://github.com/daggerok/jboss-eap-6.4/blob/6.4.0-alpine/Dockerfile)
- [6.4.0-centos](https://github.com/daggerok/jboss-eap-6.4/blob/6.4.0-centos/Dockerfile)

## usage

### health check

```Dockerfile

FROM daggerok/jboss-eap-6.4:6.4.22-alpine
HEALTHCHECK --retries=33 \
            --timeout=1s \
            --interval=1s \
            --start-period=3s \
            CMD wget -q --spider http://127.0.0.1:8080/my-service/health || exit 1
COPY --chown=jboss ./target/*.war ${JBOSS_HOME}/standalone/deployments/my-service.war

```

### multi deployment

```Dockerfile

FROM daggerok/jboss-eap-6.4:6.4.22-centos
COPY --chown=jboss ./build/libs/*.war ./target/*.war ${JBOSS_HOME}/standalone/deployments/

```

### remote debug

```Dockerfile

FROM daggerok/jboss-eap-6.4:latest
ENV JAVA_OPTS="$JAVA_OPTS -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=5005"
EXPOSE 5005
# ...

```

_ports_

- management: 9990, 9999
- web http: 8080
- https: 8443

<!--

git reset --hard origin/master
git fetch -p -a --prune-tags --force --tags 

git tag -d $tagName
git push --delete origin $tagName

git tag 6.4.22-centos
git push origin --tags --force

git tag 6.4.22-alpine
git push origin --tags --force

-->
