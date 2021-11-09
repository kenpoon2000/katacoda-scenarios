Docker-Compose can define and run multi-container by using a YAML file to configure the containers. 

First of all, we need to make a YAML file `docker-compose.yml`

You can get this file by execute this command
`wget https://raw.githubusercontent.com/kenpoon2000/katacoda-scenarios/main/test/docker-compose.yml`{{execute}}

After download the yml file, you can start up the applications by execute command:
`docker-compose up`{{execute}}


<pre class="file" data-target="clipboard">
version: '3.2' 
 
services: 
    mysql-server: 
        container_name: mysql           #Specify the name
        ports: 
            - "13306:3306"              #Specify the port for this application
        environment: 
            MYSQL_ROOT_PASSWORD: secret #Password for root user in MySQL
            MYSQL_DATABASE: wordpress   #Create a database for Wordpress 
            MYSQL_USER: wordpress_user  #Create a Wordpress user in MySQL
            MYSQL_PASSWORD: secret      #Password for wordpress_user            
        image: mysql/mysql-server       

    wordpress: 
        image: wordpress:latest 
        container_name: wordpress 
        ports: 
            - "20080:80" 
        environment: 
            WORDPRESS_DB_HOST: mysql-server:3306   #
            WORDPRESS_DB_USER: wordpress_user      #
            WORDPRESS_DB_PASSWORD: secret          #
        depends_on: 
            - mysql-server   #                     
</pre>