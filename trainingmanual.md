*Installation*

Afte login into instance through ssh take a clone using below commands.

    cd ~
    sudo git clone https://ami_bajwala:EJG7CDrxYTmeMXEjSBXY@bitbucket.org/ami_bajwala/driver_new_tech.git

![step1](images/Installation_step1.png)

Run production.sh from driver_new_tech which will take the clone of backend as well as front-end
repositories and install all teh required prerequisites.

    cd driver_new_tech
    sudo bash production_host.sh

![production.sh](images/Installation_step2_1.png)

![production.sh](images/Installation_step2_2.png)

You must define the constant values in the .env file. A template .env.sample is provided which contains the keys and
values required to run DRIVER2.0.

Create .env file in the project directory refer template .env.sample follow steps below:

    cd /var/www/driver_new_tech/
    sudo nano .env
    save and close the file

![Environment](images/InstallationEnvironment.png)

In the project directory(/var/www/driver_new_tech/) as a superuser, execute steps below:

    sudo docker-compose up -d

![docker-compose](images/Installation_DockerCompose_1.png)
![docker-compose](images/Installation_DockerCompose_2.png)

Review the containers using below command

    sudo docker ps

![docker ps](images/Installation_Dockerps.png)


Execute the configure.sh file using below commands.

    cd /var/www/driver_new_tech/
    ./configure.sh

![configure.sh](images/Installation_Configure1.png)

Enter username and password for superuser


Create Incident and Intervention schema using below commands.

    sudo docker exec "driver-new-tech" python ./scripts/load_incident_schema.py --authz 'Token 0af6fba5c87d6335c61c5981007ed385e094bd39' --api-url 'http://{{ip_addr/domain_name}}/api'
    
    sudo docker exec "driver-new-tech" python ./scripts/load_intervention_schema.py --authz 'Token 36df3ade778ca4fcf66ba998506bdefa54fdff1c' --api-url 'http://{{ip_addr/domain_name}}/api'

Add English language for both Admin&User panel using below command.

    python ./scripts/load_default_languages.py --authz 'Token 36df3ade778ca4fcf66ba998506bdefa54fdff1c' --api-url 'http://{{ip_addr/domain_name}}/api'

![schema and language](images/Installation_Schema_Language.png)

Admin Panel

    sudo nano /var/www/wb-driver-admin-front-end-angular/dist/web-driver-admin/index.html
    change <app-root hostname = "http://{{ip_addr/domain_name}}/"> to running ip ip_addr/domain_name

![Index.html](images/Installation_Index_Admin.png)

User Panel

    sudo nano /var/www/wb-driver-userpanel_front-end/dist/WB-Driver/index.html
    change <app-root hostname = "http://{{ip_addr/domain_name}}/" windshaftUrl = "http://{{ip_addr/domain_name}}"></app-root> to running ip_addr/domain_name

![Index.html](images/Installation_IndexAdmin.png)