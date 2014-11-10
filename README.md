mini_projet_vagrant-docker
==========================
In this repository you will find an example of using vagrant virtual machine to add a spatial database using a postgres server hosted in a container in your virtual machine; and to be able to visualise you layer in geoserver.

To do that all you have to do is to follow the steps bellow. LET'S GO !!!
==
What you will need ?:
- Vagrant
- A vagrant virtual box
- Boot2docker

First of all you have to set the proxy environement to be able to download the vagrant-proxyconf for that all you have 
to do is :
- Open the script env.bat and replace the proxy value with your proxy
- Execute the script in your console
That is being done. Now:
- Launch your virtual machine « vagrant up »
- Download « vagrant plugin install  vagrant-proxyconf »
- Launch Boot2docker « vagrant ssh »
- Execute the script "run.sh" « /bin/bash run.sh »: that script pull two images (postgres and geoserver) and create 
        two containers for each image. It also create a database in the "postgres" container based on the script "dab.sql".

Now you have two containers , one hosting postgres+postgis server and the other geoserver. Also ,in the script "run.sh" we published the containers ports (5432,8080) to the host.

In the vagrantfile the two lines that begin with "config.vm.network" redirect your windows machine's port to your virtual machine's ports
Which allow "geoserver" to access the spatial dababase in your container.

OKey, now all you have to do is to open geoserver sign in, add a new store choose the option "Postgis data base" and in the connexion parameters:
- Replace local host by the ip address of your container 
- Replace port by the port used in you posgres container 
- User, password:postgres,postgres (or the user name and the password you choosed while instaling posgreserver)
- Click on save 


How to get the ip address of a container
====
- Type "docker ps" To display all you running containers
- Type "docker inspect name of container" you can fin the ip adress you are looking for under the name "IPAddress"
ps : you can just type the first two letters of the container's name .

Now you have to publish your layer and you can visualise it !!!
