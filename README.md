# Jenkins Configuration as Code
Ready to deploy Jenkins Configuration as a Code

## Steps to deploy Jenkins Configuration as Code
1. Clone the repository
2. Run the following command to deploy Jenkins Configuration as Code
```bash
docker-compose up -d
```
3. Access Jenkins at http://localhost:8080

## How to add Jenkins plugins?
You can add Jenkins plugins by adding the plugin name in the Dockerfile. For example, to add the Blue Ocean plugin, add the following line in the Dockerfile
```Dockerfile
RUN jenkins-plugin-cli --plugins \
    "workflow-aggregator:latest workflow-multibranch:latest git:latest saferestart:latest kubernetes:latest configuration-as-code:latest matrix-auth:latest authorize-project:latest logstash:latest blueocean:latest"
```

## How to configure Jenkins?
You can configure Jenkins by modifying the `casc.yaml` file. For example, to configure the number of executors, add the following lines in the `casc.yaml` file
```yaml
jenkins:
  securityRealm:
    local:
      allowsSignup: false
      users:
       - id: ${ADMIN_USER}
         password: ${ADMIN_PASSWORD}
  authorizationStrategy:
    globalMatrix:
      permissions:
        - "Overall/Administer:admin"
        - "Overall/Read:authenticated"
  remotingSecurity:
    enabled: true
security:
  queueItemAuthenticator:
    authenticators:
    - global:
        strategy: triggeringUsersAuthorizationStrategy
unclassified:
  location:
    url: http://localhost:8080/
```
