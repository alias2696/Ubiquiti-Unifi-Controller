# Ubiquiti-Unifi-Controller

Docker folder:
- contains the Docker file needed to build the image
- builds version 5.4.1.16 of the controller, if you need this changed you can change it inside the Dockerfile

docker build  -t unifi-5.4.16-v024 .

Kubernetes folder:
- contains the files needed to build a kubernetes deployment 
- mongodb and unifi storages are stored on PV
- the initial build was done on an inhouse k8s deployment with storage on Glusterfs; if you are deploying outside Glusterfs please replace the PV yaml files with corect statements
- unifi service is been exposed via local ip feel free to replace the 10.20.0.11 with whatever makes sense in your deployment
