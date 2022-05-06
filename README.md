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
1. Generate Privat key and Public Key
    * LOCAL
        * Create KEY
                                                        
                achmad@achmad-Latitude-7480:~$ ssh-keygen
2. Check Privat key and Public Key
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
1. Create Pipline
    * BITBUCKET
        * Create .yml Manual by Default
                                                        
                Choose your repository -> Click Deployment -> Click Commit File
                
            ![image](https://user-images.githubusercontent.com/77251566/167135052-d7968e2a-dabf-4e23-8085-6d705a732bf7.png)

2. Create variable for secret value, example for user, password, host and than anything
    * BITBUCKET
        * Create secret variable
                                                        
                Choose your repository -> Click Repository Settings -> Click Repository Variable
                
            * SAMPLE: BITBUCKET WITHOUT CREATE PIPLINE SO YOU CAN'T CREATE VARIBALE IN YOUR REPOSITORY 
            ![image](https://user-images.githubusercontent.com/77251566/167136349-cefd65ad-2bf2-4f1e-8dae-f305c918b369.png)
            * SAMPLE: BITBUCKET WITH CREATE PIPLINE SO YOU CAN CREATE VARIBALE IN YOUR REPOSITORY 
            ![image](https://user-images.githubusercontent.com/77251566/167137998-e1f1599f-95fb-488d-be28-a3ca64dc55aa.png)

                      Fill varibale with you want, check Secured if you feel it's a secret then star will appear

3. Create SSH KEY
    * BITBUCKET
        * Generate SSH KEY
                                                        
                Choose your repository -> Click Repository Settings -> Click SSH Keys -> Click Generate Keys or Click Use myown Keys

            ![image](https://user-images.githubusercontent.com/77251566/167141409-e4e14f0d-483e-4777-9c89-4140afda92e7.png)

            * If you choose Generate Keys
                  
                  Copy your keys -> add on the SERVER in ~/.ssh/authorized_keys
            
            * If you choose Use my own keys
                  
                  Copy your keys public and privat at LOCAL -> paste add on the Bitbucket -> Click Save Key Pair
                  
            ![image](https://user-images.githubusercontent.com/77251566/167139850-852d3386-75d3-44db-9a04-118e8fa20b47.png)
                  
4. Code file .yml
    * BITBUCKET
        * Code file .yml for update automate

                script:
                  - echo "Your deployment script goes here..."
                  - apt-get update -y
                  - apt-get install -y ssh
                  - echo $VARIABLE-SSH_PK_DEV > ~/.ssh/id_rsa
                  - chmod 600 ~/.ssh/id_rsa
                  - cat ~/.ssh/id_rsa
                  - apt-get install ssh-askpass -y
                  - ssh -o StrictHostKeyChecking=no ${VARIABLE-SSH_USER_DEV}@${VARIABLE-SSH_HOST_DEV} "cd /var/www/html/achmad/testing/ && git pull https://[USERNAME-BITBUCKET]:[PASSWORD-BITBUCKET]@bitbucket.org/[USERNAME-BITBUCKET]/[REPONAME-BITBUCKET].git  "


