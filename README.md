# projCert
This is a simple php website including Jenkinsfile. It contains a Dockerfile to build a docker container on remote host.
And an Ansbile .yml files to install docker if it doesn't exists.
Make sure your master vm/server has java, jenkins, Ansible & GIT installed.
In the inventory file for Ansible in master vm/server, make sure to add the IP address of your test worker node where you want to deploy your application for testing.
Make sure file /var/run/docker.sock has enough privilesges for Jenkins user to run a job else you will get a permission denied error.
The app will be deployed using a deployContainer.yml file. In case if its already running, the app will be auto-deleted and a new container will be deployed again.
Once the container is running you can access it in your browser by accessing "http://IP:32768/website", where IP is the ip address of your docker running container node.
