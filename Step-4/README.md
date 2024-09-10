## Install Prometheus and Grafana On the another EC2 Server 

1) Login to Promethues-Grafana EC2 instance, add Promethues user and intall prometheus using below commands

```sh
sudo useradd \
    --system \
    --no-create-home \
    --shell /bin/false prometheus

wget https://github.com/prometheus/prometheus/releases/download/v2.47.1/prometheus-2.47.1.linux-amd64.tar.gz
```
![image](https://github.com/user-attachments/assets/0454574f-ed34-4b5a-b5ed-29af38423944)
