
FROM debian:buster-slim

ENV DOCKER_VERSION=20.10.8
ENV openjdkversion=jdk-18.0.1.1
ENV openjdkurl=https://download.java.net/java/GA/jdk18.0.1.1/65ae32619e2f40f3a9af3af1851d6e19/2/GPL/openjdk-18.0.1.1_linux-x64_bin.tar.gz
ENV openjdktar=openjdk-18.0.1.1_linux-x64_bin.tar.gz
# culr (optional) for downloading/browsing stuff
# openssh-client (required) for creating ssh tunnel
# psmisc (optional) I needed it to test port binding after ssh tunnel (eg: netstat -ntlp | grep 6443)
# nano (required) buster-slim doesn't even have less. so I needed an editor to view/edit file (eg: /etc/hosts) 

RUN apt-get update && apt-get install -y \
	apt-transport-https \
	ca-certificates \
	curl \
    openssh-client \
	psmisc \
	nano \
	less \
	net-tools \
	libdigest-sha-perl \
	groff \
	unzip \
    bzip2 \
    xz-utils \
    p11-kit \
    wget tar gzip ca-certificates-java && \
    wget -q ${openjdkurl} -P /opt/jdk \
    && tar -xzf /opt/jdk/${openjdktar} -C /opt/jdk \
    && rm /opt/jdk/${openjdktar} \
    && apt-get clean; \
    rm -rf /var/lib/apt/lists/* \
    && curl -L https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl -o /usr/local/bin/kubectl \
	&& chmod +x /usr/local/bin/kubectl
# ENV JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64
# ENV PATH "${JAVA_HOME}/bin:${PATH}"
RUN ls -la /opt/jdk
ENV JAVA_HOME=/opt/jdk/${openjdkversion}
ENV PATH "${JAVA_HOME}/bin:${PATH}"
	

RUN curl -o /usr/local/bin/jq -L https://github.com/stedolan/jq/releases/download/jq-1.6/jq-linux64 && \
  	chmod +x /usr/local/bin/jq
RUN curl -o /usr/local/bin/yq -L https://github.com/mikefarah/yq/releases/download/v4.14.2/yq_linux_386 && \
	chmod +x /usr/local/bin/yq

RUN curl -fsSLO https://download.docker.com/linux/static/stable/x86_64/docker-${DOCKER_VERSION}.tgz \
  && tar xzvf docker-${DOCKER_VERSION}.tgz --strip 1 \
                 -C /usr/local/bin docker/docker \
  && rm docker-${DOCKER_VERSION}.tgz

RUN curl -sL https://aka.ms/InstallAzureCLIDeb | bash

COPY binaries/init.sh /usr/local/init.sh
RUN chmod +x /usr/local/init.sh

# COPY binaries/tmc /usr/local/bin/
# RUN chmod +x /usr/local/bin/tmc



ENTRYPOINT [ "/usr/local/init.sh"]