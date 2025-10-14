### . Add non root user to Docker group
`USER 1000:1000` 
in the Dockerfile or
`sudo usermod -aG docker $USER
`newgrp docker`
This is used to run the containers without root privileges

### . Remove unnecessary packages
After setting up all containers, remove packages that are not necessary for the containers to work properly.
For example: curl