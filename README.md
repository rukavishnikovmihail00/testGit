# Delivery-tool

The tool provides artifacts delivery to your local Artifactory storage
_______________________________________________________________________________________________________________________

There are 3 functions of the Delivery tool:
- __pack__   - read a packing config, download files and docker images using skopeo, create an archive with some structure
- __upload__ - unpack the archive, parse an uploading config and the archive structure and upload files to Artifactory instance
- __show__   - show space by a repository
_______________________________________________________________________________________________________________________

## Requirements
There are the things that have to be pre-installed on your system

- Python 3.8     :white_check_mark:
- Docker 20.10.7 :white_check_mark:
- Docker-compose 1.29.2 :white_check_mark:
- Skopeo 1.4.0 :white_check_mark:
- Ansible 2.11.1 :white_check_mark:
________________________________________________________________________________________________________________________

## User guide
There is an information about Delivery tool usage

- __Setup the tool__
	
    Run `build.sh` bash script. Delivery tool package will be installed

- __Navigate to the delivery_tool directory__

    usage: **cd delivery_tool**
________________________________________________________________________________________________________________________

Now you can use Delivery tool functions:

- __pack__

    usage: **python3 delivery-tool-rukavishnikov.pyz pack -f config.yaml**

- __upload__

    usage: **python3 delivery-tool-rukavishnikov.pyz upload -f artifactory.yaml -a ArchContent.zip**

    *ArchContent.zip is just an archive that is created in the pack option of Delivery tool.*
- __show__

    usage: **python3 delivery-tool-rukavishnikov.pyz show -f artifactory.yaml**
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
   home_dir: /home/mikhail/.jfrog
```

This configuration file needs to contain the Artifactory URL specified if `url` section.
In `repositories` section there should be a Generic repository name in `files` and Docker repository name in `docker`.
Besides, please, specify the Docker images in `images` section and your Artifactory home directory in `home_dir`.
_________________________________________________________________________________________________________________________





   

