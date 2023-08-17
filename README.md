**devops_assignment2_part1**

**Step 1**

**Command:** docker network create my_network

**Output:** c08d4d8c8856070e1d04e2bda3a1e4653f1ed515e53a20333f7f6150470f8608

**Command:** docker network ls

**Output:** 
NETWORK ID     NAME         DRIVER    SCOPE
c9a9a1f084cd   bridge       bridge    local
23d66ce47f46   host         host      local
c08d4d8c8856   my_network   bridge    local
422afa7575fa   none         null      local

**Step 2**

**Command:** docker run --name nginx_container -d --network my_network -p 80:80 nginx

**Output:** 27c78a27d9698f0ad7b183090310159b50b6c1e652999e781faca5fbc1c53597

**Step 3**

**Command:** http://localhost:80

**Output:** accesible

**Step 4**

**Command:** docker run --name httpd_container -d --network my_network -p 8081:80 httpd

**Output:** b08578e08fea137226a6bb35bc70ed991e88c8f10cdcef343a067ff6bedb8464

**Step 5**

**Command:** http://localhost:8081

**Output:** accesible

**Step 6**

**Command:** docker network inspect my_network

**Output:**
[
    {
        "Name": "my_network",
        "Id": "376cacd66de9adb5b8c02abfe26b0e2179779142a5b8cbf1e163ef959b26a917",
        "Created": "2023-08-16T19:09:26.197574899Z",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": {},
            "Config": [
                {
                    "Subnet": "172.19.0.0/16",
                    "Gateway": "172.19.0.1"
                }
            ]
        },
        "Internal": false,
        "Attachable": false,
        "Ingress": false,
        "ConfigFrom": {
            "Network": ""
        },
        "ConfigOnly": false,
        "Containers": {
            "112691fd68cfd6549105b344520bcbb4f67c1d33255ab33a61a47e5d957957ec": {
                "Name": "httpd_container",
                "EndpointID": "3373c4630c99fc8f195b31d125dcd467d3138dfbb33a25e7d71655851528c994",
                "MacAddress": "02:42:ac:13:00:03",
                "IPv4Address": "172.19.0.3/16",
                "IPv6Address": ""
            },
            "27c78a27d9698f0ad7b183090310159b50b6c1e652999e781faca5fbc1c53597": {
                "Name": "nginx_container",
                "EndpointID": "7593b0d0f8f0623538805fe1f82533ef52fa2a16b68f38556ca46d4a54ccbb47",
                "MacAddress": "02:42:ac:13:00:02",
                "IPv4Address": "172.19.0.2/16",
                "IPv6Address": ""
            }
        },
        "Options": {},
        "Labels": {}
    }
]

**Step 7**

**Command:** 

docker stop nginx_container

docker rm nginx_container

**Step 8**

**Command:** docker run --name nginx_container_2 -d --network my_network -p 8082:80 nginx

**Output:** 5247289f26995b1e6f7190cdd255326a3a2f1ad674a30f2c61463c541639be92


**Step 9**

**Command:** http://localhost:8082

**Output:** accesible

**Step 10**

**Command:** docker container ls

**Output:** 

CONTAINER ID   IMAGE                   COMMAND                  CREATED              STATUS              PORTS
                                                                                               NAMES
003f24b15fd1   httpd                   "httpd-foreground"       About a minute ago   Up About a minute   0.0.0.0:8081->80/tcp                                                                                          httpd_container
5247289f2699   nginx                   "/docker-entrypoint.…"   4 minutes ago        Up 4 minutes        0.0.0.0:8082->80/tcp                                                                                          nginx_container_2
27c78a27d969   nginx                   "/docker-entrypoint.…"   19 minutes ago       Up 19 minutes       0.0.0.0:80->80/tcp                                                                                            nginx_container
ca0d149f1880   rabbitmq:3-management   "docker-entrypoint.s…"   7 days ago           Up 2 hours          4369/tcp, 5671/tcp, 0.0.0.0:5672->5672/tcp, 15671/tcp, 15691-15692/tcp, 25672/tcp, 0.0.0.0:15672->15672/tcp   rabbit-server


**Step 11**

**Command:** 

docker stop httpd_container
docker rm httpd_container
docker stop nginx_container_2
docker rm nginx_container_2
docker stop nginx_container
docker rm nginx_container

**Output:** 

Ok