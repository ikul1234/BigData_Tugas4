## Bigdata 2020

# Tugas 4 Big DATA

- [Tugas 4 Big DATA](#tugas-4-big-data)
- [Tools](#tools)
- [Kafka Docker](#kafka-docker)
- [Running](#running)
- [Testing](#testing)

# Tools
Tools yang diperlukan dalam tugas ini:
1. Docker Desktop
2. Conductor
3. zookeeper
4. kafka


# Kafka Docker
* Docker sudah terinstall <br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_4/picture/docker.jpg "docker")<br/>
* Membangun infrastruktur kafka dengan docker (2 broker dan 1 zookeeper sebagai cluster) (docker-compose.yml)

```
version: '2'

networks:
  kafka-net:
    driver: bridge

services:
  zookeeper-server:
    image: 'bitnami/zookeeper:latest'
    networks:
      - kafka-net
    ports:
      - '2181:2181'
    environment:
      - ALLOW_ANONYMOUS_LOGIN=yes
      
  kafka-server1:
    image: 'bitnami/kafka:latest'
    networks:
      - kafka-net    
    ports:
      - '9092:9092'
    environment:
      - KAFKA_CFG_ZOOKEEPER_CONNECT=zookeeper-server:2181
      - KAFKA_CFG_ADVERTISED_LISTENERS=PLAINTEXT://localhost:9092
      - ALLOW_PLAINTEXT_LISTENER=yes
    depends_on:
      - zookeeper-server
      
  kafka-server2:
    image: 'bitnami/kafka:latest'
    networks:
      - kafka-net    
    ports:
      - '9093:9092'
    environment:
      - KAFKA_CFG_ZOOKEEPER_CONNECT=zookeeper-server:2181
      - KAFKA_CFG_ADVERTISED_LISTENERS=PLAINTEXT://localhost:9093
      - ALLOW_PLAINTEXT_LISTENER=yes
    depends_on:
      - zookeeper-server
```

# Running

* Pertama jalankan command ``` compose up -d ``` di folder yang sudah ada docker-compose.yml<br/>
  ![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_4/picture/compose.PNG "docker")<br/>
* Pastikan berhasil seperti gambar di bawah <br/>
  ![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_4/picture/success_compose.PNG "docker")<br/>
* Cek di Docker apakah sudah berhasil
  ![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_4/picture/docker_compose.PNG "docker")<br/>

# Testing

* Test pada Conduktor dengan setting sama seperti di script<br/>
  ![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_4/picture/conductor_install.PNG "docker")<br/>

* Cek apakah kafka sudah terbuat<br/>
  ![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_4/picture/result.PNG "docker")<br/>
