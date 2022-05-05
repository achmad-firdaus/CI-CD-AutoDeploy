# CI-CD-AutoDeploy <img src="https://raw.githubusercontent.com/MartinHeinz/MartinHeinz/master/wave.gif" width="30px">
All Abound CI-CD AutoDeploy

#### LIST
- [Help 👻](#introduction-)
- [SSH With PrivatKey 👻](#ssh-with-privatkey-)
- [Configuration CI CD 👻](#configuration-ci-cd-)

#### INTRODUCTION 👻

    First, what you have to make sure:
    1. You can SSH with privat key in your server, this have 2 condition:
        1. You can:
           if you are in this phase, you only need configuration from git to the server, you don't need a lot of configuration on the server
        2. You can't:
           if you are in this phase, you have to follow from the beginning the configuration on local computer and on the server
    Onether step:
    2. Configuration generate key and register key:
        1. Local Computer,
        2. Server Ubuntu
    3. Testing ssh in your local with privat key,
    4. Configuration git:
        1. Add some variable ,
        2. Create and Configuration file .yml for make pipline in git,
        3. Create public key and register to the server

#### SSH-WITH-PRIVATKEY 👻

    sudo docker run --name=[name container] -p [local port]:[docker port] [option] [image]
    sudo docker run --name=MySql -p 33061:3306 -e MYSQL_ROOT_PASSWORD=1  mysql
    
    sudo docker exec -it MySql2 mysql -uroot -p // enter in mysql

#### CONFIGURATION CI CD 👻

    sudo docker exec -it [container name] bash




