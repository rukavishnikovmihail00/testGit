# Delivery-tool

The tool provides artifacts delivery to your local Artifactory storage

![](https://raw.githubusercontent.com/rukavishnikovmihail00/testGit/newbranch/delivery_tool.png "Delivery tool")
_______________________________________________________________________________________________________________________

There are 4 functions of the Delivery tool:
- __install__ - read an installation config and install Artifactory to the instance using ansible.
- __pack__   - read a packing config, download files and docker images using skopeo, create an archive with some structure.
- __upload__ - unpack the archive, parse an uploading config and the archive structure and upload files to Artifactory instance. Show full and delta size of
repositories.
- __show__   - show space by a repository.
_______________________________________________________________________________________________________________________

## Prerequisites
There are the things that have to be pre-installed on your system

- Python 3.8     :white_check_mark:
- Docker 20.10.7 :white_check_mark:
- Docker-compose 1.29.2 :white_check_mark:
- Skopeo 1.4.0 :white_check_mark:
- Ansible 2.11.1 :white_check_mark:
________________________________________________________________________________________________________________________

## User guide
There is an information about Delivery tool usage

- __Set your configurations__

    Change `config.yaml` and `artifactory.yaml` according to the example below.

- __Setup the tool__
	
    Run `build.sh` bash script. Delivery tool package will be installed.

- __Navigate to the delivery_tool directory__

    usage: **cd delivery_tool**

- __Specify your credentials for Artifactory instance__

    Note, that credentials must be `admin:password` for the first Artifactory launch.
________________________________________________________________________________________________________________________

Now you can use Delivery tool functions:

- __install__ 

    usage: **python3 delivery-tool-rukavishnikov.pyz install -f create.yaml -a artifactory.yaml [repo]**
	
    `repo` is optional, so you can include it if you need to create Generic repository automatically.

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
   docker_registry: 10.0.2.15:17001
   repositories:
     files: delivery_tool.files
     docker: delivery-tool.docker
   home_dir: /home/mikhail/.jfrog
   lic_path: /home/mikhail/artifactory.lic
```

This configuration file needs to contain the Artifactory URL specified in `url` section and docker registry.
In `repositories` section there should be a Generic repository name in `files` and Docker repository name in `docker`.
`lic_path` is a path to your artifactory.lic file, that contains Artifactory license key.
Besides, please, specify the Docker images in `images` section and your Artifactory home directory in `home_dir`.
_________________________________________________________________________________________________________________________





   

