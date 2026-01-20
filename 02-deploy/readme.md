### General information

image-name: simple-api
install version: v1.0.0
location: registry.class.syscallx86.com

### Deploy application on cluster


- create namespace simple-api
- switch into that namespace
- pull the repository github.com/veldrane/kubernetes-app
- read the readme file and locate deployment manifest
- find the path on registry.class.syscallx86.com
- customize manifest, setup right image-path and apply against tour cluster
- monitor starting simple-api pod
- look at logs of the simple-api-pod