# SDH-Machine-Harvesters

Docker deployment of Harvesters.

This repository deploys these containers:
* Redis Database for Gitlab Collector/Enhancer
* Gitlab Collector
* Gitlab Enhancer API
* Organization Harvester
* Continuous Integration Harvester
* Source Code Management Harvester
* Nginx

### Ports (container - host):
* ORG: 80 - 8000
* SCM: 80 - 8001
* CI: 80 - 8002
* Nginx: 80 - 80

### Nginx Access:
|Nginx Path|Container/Path|
|:---------|:----------|
|/orgharvester|orgharvester/harvester/ldp4j/api/service|
|/scmharvester|scmharvester/harvester/ldp4j/api/service|
|/ciharvester|ciharvester/harvester/service|

### Docker - Requirements:

* docker > 1.7.0
* docker-compose > 1.3.1

### Docker - Usage:

|Alias|Command|
|:---------|:----------|
|Start|```docker-compose up -d```|
|Stop|```docker-compose stop```|
|Delete|```docker-compose rm -f```|
|Rebuild|```docker-compose build```|

### Docker - Tips:

If you want to change port redirection or configuration, we suggest you:

1. Stop
2. Delete
3. Build (if you have changed any file or physical configuration)
4. Start

### Docker - Environment:

* Gitlab Configuration
|Variable|Description|Example|
|:---------|:----------|:----------|
|COLL_GITLAB_PROT|Protocol|http or https|
|COLL_GITLAB_IP|URL or IP address|http://... or https://...|
|COLL_GITLAB_PORT|Port|80 or 443 or other|
|COLL_GITLAB_USER|User (admin permission)|root or other|
|COLL_GITLAB_PASS|Password|user_password_test|
|COLL_GITLAB_VERIFY_SSL|Verify ssl certificate|0 or 1|

### Harvesters - Usage:

Before deployment, you need to deploy first SCM improvements.

1. Execute ```docker-compose up -d glcollector```
2. See logs ```docker-compose logs glcollector```
3. Wait to finish and exit docker-compose logs

To deploy other containers without to remove collected information.

```docker-compose up -d --no-recreate```
