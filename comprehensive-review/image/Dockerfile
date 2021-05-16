FROM registry.redhat.io/ubi7/ubi:7.7

MAINTAINER Arian Jam

ENV NEXUS_VERSION=2.14.3-02 \
    NEXUS_HOME=/opt/nexus

COPY training.repo /etc/yum.repos.d/

ADD nexus-2.14.3-02-bundle.tar.gz  ${NEXUS_HOME}/
ADD nexus-start.sh ${NEXUS_HOME}/

RUN 	groupadd -r nexus -f -g 1001 &&\
	useradd -u 1001 -r -g nexus -m -d ${NEXUS_HOME} \
        -s /sbin/nologin \
        -c "Nexus User" nexus &&\
	chown -R nexus:nexus ${NEXUS_HOME} &&\
	ln -s ${NEXUS_HOME}/nexus-${NEXUS_VERSION} ${NEXUS_HOME}/nexus2


RUN yum install -y --setopt=tsflags=nodocs java-1.8.0-openjdk-devel &&\
	yum clean all -y
USER nexus

WORKDIR ${NEXUS_HOME}

VOLUME /mnt ${NEXUS_HOME}/sonatype-work

CMD ["sh", "nexus-start.sh"]	
