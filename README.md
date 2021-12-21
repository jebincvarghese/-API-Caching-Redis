# API-Caching-Redis-Python

## Create network

```
# docker network create myapp
```

## Creating container for caching using redis image

```
# docker container run --name cache -d --network myapp --restart always redis:latest

```

## Creating containers with flask applications

Here I am creating 3 containers with the same application to get the geoIP location of the input IP address and to map local systems ports 8081, 8082 and 8083 to the container port number 8080.

Your IPSTACK_KEY is your unique authentication key used to gain access to the ipstack API, https://ipstack.com/. 

```
#docker container run -d --name ipstackapp1 --network myapp --restart always -p 8081:8080 -e CACHING_SERVER=cache -e IPSTACK_KEY=a0fb9d2cff312331bab08baf8486502c jebincvarghese/ipstack:v1
   
#docker container run -d --name ipstackapp2 --network myapp --restart always -p 8082:8080 -e CACHING_SERVER=cache -e IPSTACK_KEY=a0fb9d2cff312331bab08baf8486502c jebincvarghese/ipstack:v1

#docker container run -d --name ipstackapp3 --network myapp --restart always -p 8083:8080 -e CACHING_SERVER=cache -e IPSTACK_KEY=a0fb9d2cff312331bab08baf8486502c jebincvarghese/ipstack:v1

```

Now your applicaton will be availble on IPv4 Public IP:8081, IPv4 Public IP:8082, and IPv4 Public IP:8083

## Load balancing containers with ALB

Create a target group and register the targets as shown below,

I am registering the same instance as different targets on port 8081, 8082 and 8083.


Create ALB using this target group


Instead of setting up a container for caching (Redis) you can use ``ElastiCache``, then replace ``CACHING_SERVER=redis`` with ElastiCache primary end point.






