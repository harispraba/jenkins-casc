FROM jenkins/jenkins:lts

ENV JAVA_OPTS -Djenkins.install.runSetupWizard=false
ENV CASC_JENKINS_CONFIG /var/jenkins_home/casc.yaml

USER root
RUN apt-get update && apt-get install -y apt-transport-https \
    ca-certificates curl gnupg2 wget \
    software-properties-common
RUN curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -
RUN apt-key fingerprint 0EBFCD88
RUN add-apt-repository \
    "deb [arch=amd64] https://download.docker.com/linux/debian \
    $(lsb_release -cs) stable"
RUN apt-get update && apt-get install -y docker-ce-cli

# Install Sonar Scanner
RUN wget https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-6.0.0.4432-linux.zip &&\
    unzip sonar-scanner-cli-6.0.0.4432-linux.zip &&\
    mv sonar-scanner-6.0.0.4432-linux /opt/sonar-scanner &&\
    rm sonar-scanner-cli-6.0.0.4432-linux.zip

RUN apt-get update && apt-get install -y curl &&\
    curl -sL https://deb.nodesource.com/setup_22.x | bash - &&\
    apt-get install -y nodejs

RUN wget https://github.com/mikefarah/yq/releases/latest/download/yq_linux_amd64 -O /usr/bin/yq &&\
    chmod +x /usr/bin/yq

RUN curl -sfL https://raw.githubusercontent.com/aquasecurity/trivy/main/contrib/install.sh | sh -s -- -b /usr/local/bin v0.52.1

COPY casc.yaml /var/jenkins_home/casc.yaml
RUN jenkins-plugin-cli --plugins \
    "ssh-agent:367.vf9076cd4ee21 sonar:2.17.2 docker-workflow:latest workflow-aggregator:latest github:latest workflow-multibranch:latest git:latest saferestart:latest kubernetes:latest configuration-as-code:latest matrix-auth:latest authorize-project:latest logstash:latest blueocean:latest"
