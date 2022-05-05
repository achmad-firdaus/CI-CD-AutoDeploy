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
1. Generate Privat key and Public Key:
    * LOCAL
        * Create KEY
                                                        
                achmad@achmad-Latitude-7480:~$ ssh-keygen
2. Check Privat key and Public Key:
    * LOCAL
        * Check Private KEY
        
                achmad@achmad-Latitude-7480:~$ cat .ssh/id_rsa
        * Check Public KEY
        
                achmad@achmad-Latitude-7480:~$ cat .ssh/id_rsa.pub
3. Create "authorized_keys" on your SERVER
    * LOCAL
        * Add "authorized_keys" on server
        
                Sample: 
                ssh-copy-id -i ~/.ssh/id_rsa.pub [USER_NAME]@[HOST_NAME]
                
                achmad@achmad-Latitude-7480:~$ ssh-copy-id -i ~/.ssh/id_rsa.pub root@199.192.36.59
                /usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/home/achmad/.ssh/id_rsa.pub"
                /usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
                /usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
                root@139.162.36.59's password: 

                Number of key(s) added: 1

                Now try logging into the machine, with:   "ssh 'root@139.162.36.59'"
                and check to make sure that only the key(s) you wanted were added.
3. TEST 1, SSH Server With KEY
    * LOCAL
        * Like simple ssh to linux server
        
                Sample: 
                ssh [USER_NAME]@[HOST_NAME]
                
                achmad@achmad-Latitude-7480:~$ ssh root@199.192.36.59
                
                NOTE:
                If you login still using password then it dosen't work !
                Floow Below.
                
### If you are asked to enter password when ssh ###
* Following this:
    * SERVER
        * Login with ssh to the server with password:
        
                Sample: 
                ssh [USER_NAME]@[HOST_NAME]
                
                achmad@achmad-Latitude-7480:~$ ssh root@199.192.36.59
                
        * Add varibale to authorized_keys for check file is exist:
        
                achmad@achmad-Latitude-Server:~$ echo public_key_string >> ~/.ssh/authorized_keys
                
        * Check authorized_keys:

                achmad@achmad-Latitude-Server:~$ cat ~/.ssh/authorized_keys
                
        * Set Permission All file in .ssh :

                achmad@achmad-Latitude-Server:~$ chmod -R go= ~/.ssh

        * Set OWN User & Group Folder & File All file in .ssh :
                
                I user root user
                achmad@achmad-Latitude-Server:~$ chown -R root:root ~/.ssh
                
        BACK TO STEP 4.
    

#### CONFIGURATION CI CD 👻

    sudo docker exec -it [container name] bash




