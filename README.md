# ELK(Elasticsearch+Logstash+Kibana)

## 1. Java 설치
Elasticsearch 는 Java8 이상이 필요합니다. 만약 java가 설치되어 있지 않으면 jdk 1.8.0-openjdk 파일을 설치합니다.

```sh
[root@localhost ~]# java -version
openjdk version "1.8.0_232"
OpenJDK Runtime Environment (build 1.8.0_232-b09)
OpenJDK 64-Bit Server VM (build 25.232-b09, mixed mode)
```

## 2. lasticsearch PGP 키 가져오기

```sh
rpm --import https://artifacts.elastic.co/GPG-KEY-elasticsearch
```

## 3. Elastic repository 설정

```sh
vi /etc/yum.repos.d/Elastic.repo
```
```sh
[Elastic-7.x]
name=Elastic repository for 7.x packages
baseurl=https://artifacts.elastic.co/packages/7.x/yum
gpgcheck=1
gpgkey=https://artifacts.elastic.co/GPG-KEY-elasticsearch
enabled=1
autorefresh=1
type=rpm-md
```
인증서 오류날시 아래 값 추가
```sh
sslverify=0
```
## 4. Elasticsearch/ Logstash / Kibana  설치

```sh
yum -y install elasticsearch

yum -y install logstash

yum -y install kibana
```

## 5. 환경설정
