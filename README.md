# Delivery-tool

The tool provides artifacts delivery to your local Artifactory storage
_______________________________________________________________________________________________________________________

There are 3 functions of the Delivery tool:
- __pack__   - downloads all the files, copies the images specified in your configuration file and makes an arhive
- __upload__ - extracts the archive made in 'pack' function and uploads all the files and images to the Artifactory storage
- __show__   - shows you an information about size used in your Generic and Docker repositories
_______________________________________________________________________________________________________________________

## Requirements
There are the things that have to be pre-installed on your system

- Python         :white_check_mark:
- Docker         :white_check_mark:
- Docker-compose :white_check_mark:
- Skopeo         :white_check_mark:
- Ansible        :white_check_mark:
________________________________________________________________________________________________________________________

## User guide
There is an information about Delivery tool usage

- __pack__

    usage: **-f config.yaml pack**

- __upload__

    usage: **-f artifactory.yaml -a ArchContent.zip upload**

    *ArchContent.zip is just an archive that is created in the pack option of Delivery tool.*
- __show__

    usage: **-f artifactory.yaml show**
________________________________________________________________________________________________________________________

### The example of config.yaml

```
   files:
   - https://docker.bintray.io/artifactory/bintray-tools/com/jfrog/bintray/client/api/0.2/api-0.2.jar
   - https://docker.bintray.io/artifactory/jfrog-cli/v1/1.0.0/jfrog-cli-linux-386/jfrog
   - https://repo.jfrog.org/artifactory/jcenter-cache/1.0/com/minimalviking/deviceinfo/com.minimalviking.deviceinfo/maven-metadata.xml
   images:
   - docker.bintray.io/jfrog/artifactory-pro:7.19.8
   - docker.bintray.io/postgres:13.2-alpine
   - docker.bintray.io/jfrog/nginx-artifactory-pro:7.19.8
```

You need to specify file URLs in `files` section and Docker images in `images` section according to the example above
_________________________________________________________________________________________________________________________
### The example of artifactory.yaml

```
   url: http://10.0.2.15:8082/artifactory
   repositories:
     files: delivery_tool.files
     docker: delivery-tool.docker
  images:
  - docker.bintray.io/jfrog/artifactory-pro:7.19.8
  - docker.bintray.io/postgres:13.2-alpine
  - docker.bintray.io/jfrog/nginx-artifactory-pro:7.19.8
```

This configuration file needs to contain the Artifactory URL specified if `url` section.
In `repositories` section there should be a Generic repository name in `files` and Docker repository name in `docker`.
Besides, please, specify the Docker images in `images` section.
_________________________________________________________________________________________________________________________





   

