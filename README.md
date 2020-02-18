![Docker Image CI](https://github.com/oksana-c/docker-tika-jaxrs-server/workflows/Docker%20Image%20CI/badge.svg?branch=master)

# docker-tika-jaxrs-server

Dockerfile to create a docker image that contains the latest Ubuntu running the Apache Tika 1.23 Server on Port 9998 using Java 11.

Out-of-the-box the container also includes dependencies for the GDAL and Tesseract OCR parsers. The following language packs are currently installed:
* English
* Spanish

To install more languages simply update the apt-get command to include the package containing the language you require, or include your own custom packs using an ADD command.

## Usage

First you need to pull down the build from Dockerhub, which can be done by invoking:

    docker pull oksanac/docker-tika-jaxrs-server

Then to run the container, execute the following command:

    docker run -d -p 9998:9998 oksanac/docker-tika-jaxrs-server

### Use with Docker Compose file

```yml
version: '3.7'
services:
  tika:
    image: oksanac/docker-tika-jaxrs-server
    ports:
      - 9998:9998
```

## Add custom tika-config.xml

Modify configuration in `conf/tika-config.xml` and rebuild the image.

## Building

To build the image from scratch, simply invoke:

    docker build -t 'docker-tika-jaxrs-server' github.com/oksana-c/docker-tika-jaxrs-server
   
You can then use the following command (using the name you allocated in the build command as part of -t option):

    docker run -d -p 9998:9998 docker-tika-jaxrs-server
    
## Testing

To test PDF parser:

`curl -X PUT --data-binary @<path-to-pdf-file.pdf> http://tika.gao.test:9998/tika --header "Content-type: application/pdf"`
    
## More

For more info on Apache Tika Server, visit [Apache Tika Server documentation](http://wiki.apache.org/tika/TikaJAXRS).

## Author

  * Oksana Cyrwus (<connect@oksanac.com>)

  Credits to [David Meikle](https://github.com/LogicalSpark/docker-tikaserver) for the original image.

## Licence

Copyright 2019 Oksana Cyrwus

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.