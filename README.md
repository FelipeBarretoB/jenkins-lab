# Jenkins Lab

## Ejecutar Docker Compose

Para ejecutar Docker Compose, asegúrate de que tengas Docker Compose instalado en tu sistema. Luego, sigue estos pasos:

1. Navega a la ubicación donde se encuentra tu archivo `docker-compose.yml`.

2. Ejecuta el siguiente comando en tu terminal para iniciar los contenedores definidos en el archivo `docker-compose.yml`:

```bash
docker-compose up -d
```

3. Extraer passwords

```bash
docker logs id_container
```

```bash
docker exec id_container cat /var/jenkins_home/secrets/initialAdminPassword
```


## Lab 

In this lab we'll configure a Jenkins pipeline to build a simple Node.js application.

First we enter the jenkins dashboard using the port configured in the docker-compose file, in this case it is 8080.

We then download the suggested plugins and create a new user

We then need to add the NodeJS plugin to Jenkins. To do this, go to Manage Jenkins > Manage Plugins > Available and search for NodeJS. Install the plugin and restart Jenkins.

With this, in tools add the NodeJS installation and configure it with the name "node" and the version 10.15.2

We then create a new pipeline and configure it with the repository of the application to be built.

We add our git repository and configure the pipeline to use the Jenkinsfile in the root of the repository.

![node](../images/Screenshot%202025-03-12%20at%208.41.23 PM.png)

We then give node it's bin path and the npm path

![path](../images/Screenshot%202025-03-12%20at%208.42.36 PM.png)

Finally, we tell the pipeline to use shell, and run the following commands:

```bash
npm install
npm run build
npm start app.js &
```

We use the '&' so that the process runs in the background and the pipeline can continue.

We then save the pipeline and run it.

![pipeline](../images/Screenshot%202025-03-15%20at%206.23.02 PM.png)

The pipeline will run and the application will be built and started.

![pipeline_run](../images/Screenshot%202025-03-15%20at%207.47.46 PM.png)


The output of the job in jenkins should look like this:

![complete](../images/Screenshot%202025-03-12%20at%208.41.23 PM.png)