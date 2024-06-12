FROM sonarqube:9.9.5-community

# Install Node.js and npm
RUN apt-get update && apt-get install -y curl &&\
    curl -sL https://deb.nodesource.com/setup_22.x | bash - &&\
    apt-get install -y nodejs npm
