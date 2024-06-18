FROM sonarqube:9.9.5-community

USER root

# Install Node.js and npm
RUN apt-get update && apt-get install -y curl &&\
    curl -sL https://deb.nodesource.com/setup_18.x | bash - &&\
    apt-get install -y nodejs@18

USER sonarqube
