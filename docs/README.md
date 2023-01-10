# Headline

> An awesome project.

## Getting Started 

Ensure you are in the doc directory

### Build docker image

Run `docker build -f Dockerfile -t docsify/demo .`

### Run docker image

Run `docker run -itp 3000:3000 --name=docsify -v $(pwd):/docs docsify/demo`
