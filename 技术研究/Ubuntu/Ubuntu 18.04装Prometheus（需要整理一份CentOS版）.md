## 操作步骤

1. 下载二进制文件

~~~ shell

mdkir -p ~/software/prometheus && cd ~/software/prometheus
wget https://github.com/prometheus/prometheus/releases/ (网速慢，可以在window机器上搭vpn下载，用rz传递)

~~~

2. 解压二进制文件并复制可执行文件

~~~ shell

tar -zxvf prometheus-2.3.2.linux-amd64.tar.gz
sudo cp prometheus-2.3.2.linux-adm64/prometheus /usr/local/bin/
sudo cp prometheus-2.3.2.linux-adm64/promtool /usr/local/bin/

~~~

3. 编写配置文件/etc/prometheus/prometheus.yml

~~~ yml

global:
  scrape_interval:     15s
  evaluation_interval: 15s

alerting:
  alertmanagers:
  - static_configs:
    - targets:
      # - alertmanager:9093

rule_files:
  - "rules/node_rules.yml"
  # - "second_rules.yml"

scrape_configs:
  - job_name: 'prometheus'
    static_configs:
    - targets: ['localhost:9090']
  - job_name: 'node'
    file_sd_configs:
      - files:
        - targets/nodes/*.json
        refresh_interval: 5m
  - job_name: docker
    file_sd_configs:
      - files:
        - targets/docker/*.json
        refresh_interval: 5m

~~~

4. 启动Prometheus

~~~

nohup sudo prometheus --config.file "/etc/prometheus/prometheus.yml" &

~~~