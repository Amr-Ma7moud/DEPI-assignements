**Docker**
a) 1.  
 a docker container is an isolated process that run the application/s in an isolated environment using the host OS's kernel
diff:
docker container: a light weight process that share the host OS's resources that is faster to start and deploy as it doesn't need to spin up a machine to start but it needs a docker deamon to start and work (in-case of using docker as podman doesn't have a deamon) and it achieve isolation using native Linux kernel's namespaces and CGroups
VM: is a virtual machine that has its own OS, vCPU, vRAM, vROM and so on as it use those resources from the host's resources and it is heavier to run but it give more boundaries for the system and it needs a hypervisor to run on and manage the virtualization process so it can act as its own machine 2.
Docker file is a file that contain docker specific code/instructions to tell docker how to build and construct an image 1. `FROM` : selects the image that the container will use for that step 2. `COPY`: copies files from the directory/repo that contain the project code and files into the images 3. `RUN`: runs a command in the shell wile building the image (build time) as `RUN pacman -Syu` 4. `CMD`: an overridable run time command that can start a container and can be combined with `ENTRYPOINT` command to produce overridable default parameters

---

    B)
    1. .
    	docker image layer: is produced by each instruction in the Dockerfile, and those layers are read-only that can be cached to be reused whenever those step didn't change, which enhance build time significantly if implemented  and it optimize disk space usage as those layers can be shared between images which can skip re-downloads
    2. .
    	volumes: is a way to store data permanently in disk seperatly from the container and its life cycle which help make the data persistent and availble even if the container removed, recreated or replaced which can be used in an other container later on, a DB volume is a good example as we need the data to be always available even if the container is removed, recreated or replaced

---

    C)
    1.
    	docker handle networking by using the kernel network namespaces which allow docker to make containers communicate with each others in the intended way while isolating them in the intended way by choosing the network
    	1. bridge: a virtual network managed by docker and can be user defined, provides a network level isolation for the containers running in it as those containers can talk with each others freely while outsiders can't talk to them unless a port is published and it is the default choice for every container unless it is specified otherwise
    	2. host: No network isolation at all as it work as any normal process working on the host's **network** and it may produce port conflicts
    	3. none: Disables all external and internal networking for the container except for a local localhost interface
    2.  first by making a network using `docker network create` command then attach each container to it with the `--network [networkName]` option then each container can reach other containers by using its name that was assigned to it while creating the container
    example:
    	create the network: `docker network create --driver bridge web-app`
    	create the first container: `docker run --name front-end -p 80 --network web-app nginx`
    	create the second continer: `docker run --name db --network web-app postgres`
    	now the front-end can reach the DB by simply using `db:<postgresPort>` as the domain to each it

---

Practical question
C)
`docker run -d --name docker-task --memory=512m --cpus=1 -p 8080:8080 docker-task`
Resource limits reduce the risk that one container consumes all host resources that may affect the performance of the other containers
