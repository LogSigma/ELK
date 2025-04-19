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
Elasticsearch 설치시 공개 서명키가 필요하며, 아래와 같이 공개 서명키(public signing key) 를 설치해줍니다.

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
인증서 오류발생 할 경우 아래와 같은 값 추가
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

#### 5-1. Elasticsearch.yml 파일 수정
```sh
vi /etc/elasticsearch/elasticsearch.yml
```
```
cluster.name: log-hub
node.name: log-node-1

network.host: 10.250.111.58
transport.tcp.port: 9100
transport.tcp.compress: true

http.port: 9200

discovery.seed_host: ["10.250.111.58:9100"]
cluster.initial_master_nodes: ["log-node-1"]
```
#### 5-2. elasticsearch jvm.options heap 메모리 사이즈 조절
```sh
vi /etc/elasticsearch/jvm.option
```
```sh
-Xms4g
-Xmx4g
```
#### 5-3. logstash.yml 파일 수정
```sh
vi /etc/logstash/logstash.yml
```
```sh
```
#### 5-4. logstash jvm 옵션 heap 메모리 조절 ( 1G => 4G )
```sh
vi /etc/logstash/jvm.option
```
```sh
-Xms4g
-Xmx4g
```
#### 5-5. kibana.yml 환경 설정
```sh
vi /etc/kibana/kibana.yml
```
```sh
server.port: 5501
server.host: 0.0.0.0
elasticsearch.hosts: "http://localhost:9200"
```


물론입니다. 요청하신 대로 정합성(accuracy) 수치 제거하고, 여전히 성능 향상과 수율 기여의 핵심 메시지를 유지한 포멀하지만 쉬운 영어 문체의 Introduction 문단은 아래와 같습니다:

⸻

(Introduction)
Measuring critical dimensions (CD) in semiconductor manufacturing is a key step to ensure that wafer patterns are produced correctly. This is typically done using scanning electron microscope (SEM) images. Traditional CD measurement methods are rule-based and depend on predefined image processing rules. However, these methods often struggle with complex patterns, such as those found in on-cell overlay (OCO) images, and may produce inaccurate results or even fail to detect some CD values. These issues can lead to incorrect feedback for process control, delays in development, and a reduction in overall manufacturing yield.

To overcome these limitations, we propose a deep learning-based measurement approach using a foundation model trained on a wide range of real SEM images from different semiconductor processes. This method provides more stable and consistent CD measurements, even under challenging conditions like pattern variation, misalignment, or poor image quality. It performs well across various product types, including DRAM and V-NAND, without requiring product-specific tuning or adjustments.

By improving measurement reliability and reducing errors, this approach supports better control of upstream processes such as lithography and etching. Ultimately, it can help accelerate product development and contribute to improving yield in semiconductor fabrication.

⸻

더 기술적으로 정리된 버전이나 세부 구성(예: 연구 기여 항목 정리)도 원하시면 도와드릴게요.
