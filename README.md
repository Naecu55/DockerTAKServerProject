# DockerTAKServerProject

Docker Ubuntu TAK Server Project

apt-get -u upgrade

# Creates a new volume that containers can consume and store data in.

docker volume create takserver-db

# docker network create is a Docker command used to create a new Docker network.

# This command allows you to define the network's characteristics, such as the driver to use (e.g., bridge, overlay) # and other optional settings. 

# User-defined networks enable containers to communicate with each other, and with the external world, based on the network configuration

docker network create takserver

sudo docker network create takserver
05fdda8acfc290a0ba5e5a384814a510e1c5b5c1fee91b1e17c1acd836a92f49

openssl rand -base64 12 | tr -dc 'a-zA-Z0-9' (ignore)

sed -i 's/password=""/password="{PASSWORD}"/g' tak/CoreConfig.example.xml

sudo docker build -t takserver-db -f docker/Dockerfile.takserver-db .

< WARNING: apt does not have a stable CLI interface. Use with caution in scripts.>

sudo docker run --mount source=takserver-db,destination=/var/lib/postgresql -v $(pwd)/tak:/opt/tak:z -it -p 5432:5432 --network takserver --network-alias tak-database --name takserver-db -d takserver-db

sudo docker build -t takserver -f docker/Dockerfile.takserver .

sudo docker run -v $(pwd)/tak:/opt/tak:z -it -p 8089:8089 -p 8443:8443 -p 8446:8446 -p 9001:9001 --network takserver --name takserver -d takserver

vi tak/certs/cert-metadata.sh

sudo docker exec -it takserver bash -c "cd /opt/tak/certs && ./makeRootCa.sh --ca-name TAK-ROOT-CA-01"

sudo docker exec -it takserver bash -c "cd /opt/tak/certs && echo y |./makeCert.sh ca TAK-ID-CA-01"

sudo docker exec -it takserver bash -c "cd /opt/tak/certs && ./makeCert.sh server takserver"

sudo sed -i "s/truststore-root/truststore-TAK-ID-CA-01/g" tak/CoreConfig.xml

sudo docker restart takserver && tail -f tak/logs/takserver-messaging.log

sudo docker exec -it takserver bash -c "cd /opt/tak/certs && ./makeCert.sh client webadmin"

sudo docker exec -it takserver bash -c "java -jar /opt/tak/utils/UserManager.jar certmod -A /opt/tak/certs/files/webadmin.pem"

sudo docker exec -it takserver bash -c "java -jar /opt/tak/utils/UserManager.jar usermod -A -p '{PASSWORD}' webadmin"

--

sudo docker exec -it takserver bash -c "java -jar /opt/tak/utils/UserManager.jar usermod -A -p '{PASSWORD}' webadmin"
Password complexity check failed. 


Password must be a minimum of 15 characters including 1 uppercase, 1 lowercase, 1 number, and 1 special character from this list [-_!@#$%^&*(){}[]+=~`|:;<>,./?].

:~/takserver-docker-5.4-RELEASE-19$ sudo docker exec -it takserver bash -c "java -jar /opt/tak/utils/UserManager.jar usermod -A -p '{PASSWORD}' webadmin"
Password complexity check failed. Password must be a minimum of 15 characters including 1 uppercase, 1 lowercase, 1 number, and 1 special character from this list 

------------

[-_!@#$%^&*(){}[]+=~`|:;<>,./?].

----------

sudo docker exec -it takserver bash -c "java -jar /opt/tak/utils/UserManager.jar usermod -A -p 'PASSSSSSSS' webadmin"
User Updated:
        Username:      'webadmin'
        Role:          ROLE_ADMIN
        Fingerprint:   DA:5A:D7:2D:20:ED:A7:15:1F:4B:87:CC:07:8B:A3:FD:05:6C:CA:6E:BC:A6:D7:67:95:D3:A8:2D:D0:74:44:1C
        Groups (read and write permission):
                __ANON__

sudo chmod -R 777 webadmin.p12

-rwxrwxrwx 1 root root 4582 Jun 17 16:54 webadmin.p12
-rw-r--r-- 1 root root 5564 Jun 17 16:54 webadmin-trusted.pem
-rw-r--r-- 1 root root 5020 Jun 17 16:55 webadmin.jks


Copy from from WSL to C:\Ubuntu-WSL\webadmin.p.12

Goto chrome://settings/security click on Manage certificates and run through the process accordingly.
![image](https://github.com/user-attachments/assets/fadb0cd6-9ce5-4ddb-9992-81475868a829)

