# Wazuh + Elastic Stack Setup Guide

This guide walks through the installation of a small but practical SOC lab using Wazuh + Elastic Stack on Ubuntu. It is designed to be used immediately in a home lab or classroom environment.

## Overview

This setup creates a single-node SIEM environment:

- Wazuh manager for collection and alerting
- Elasticsearch for indexing and search
- Kibana for SOC dashboards and investigations
- Wazuh agents installed on Windows and Linux endpoints

## Lab topology

- 10.0.0.10 — Wazuh Manager / Elasticsearch / Kibana
- 10.0.0.20 — Windows endpoint with Sysmon and Wazuh agent
- 10.0.0.30 — Linux server with SSH and auth logs
- 10.0.0.40 — Attacker VM (Kali or similar)

## Requirements

- Ubuntu 22.04 LTS server for the SIEM host
- 8 GB RAM minimum, 16 GB recommended
- 4 vCPU or more recommended
- Disk: at least 50 GB free
- Static IP or predictable DHCP
- root or sudo access
- network connectivity between manager and endpoints

## Step 1: Prepare the OS

Update packages and install required dependencies.

```bash
sudo apt-get update
sudo apt-get install -y curl apt-transport-https unzip wget libcap2-bin gnupg
```

Set time synchronization.

```bash
sudo timedatectl set-ntp true
```

## Step 2: Install Elasticsearch

Add the Elastic repository.

```bash
curl -fsSL https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo gpg --dearmor -o /usr/share/keyrings/elasticsearch.gpg
sudo tee /etc/apt/sources.list.d/elastic-8.x.list > /dev/null <<'EOF'
deb [signed-by=/usr/share/keyrings/elasticsearch.gpg] https://artifacts.elastic.co/packages/8.x/apt stable main
EOF
```

Install Elasticsearch.

```bash
sudo apt-get update
sudo apt-get install -y elasticsearch
```

Configure Elasticsearch for a single-node lab environment.

```bash
sudo nano /etc/elasticsearch/elasticsearch.yml
```

Use the following minimum settings:

```yaml
cluster.name: soc-lab-cluster
node.name: soc-lab-node-1
network.host: 0.0.0.0
http.port: 9200
discovery.type: single-node
xpack.security.enabled: true
```

Enable and start Elasticsearch.

```bash
sudo systemctl daemon-reload
sudo systemctl enable elasticsearch
sudo systemctl start elasticsearch
```

Check the cluster status.

```bash
curl -k -u elastic:changeme https://localhost:9200
```

If the default password is not yet set or you are not using the generated password, generate an Elastic password as needed and record it.

## Step 3: Install Kibana

Install Kibana.

```bash
sudo apt-get install -y kibana
```

Configure Kibana.

```bash
sudo nano /etc/kibana/kibana.yml
```

Set server settings:

```yaml
server.host: "0.0.0.0"
server.port: 5601
elasticsearch.hosts: ["https://localhost:9200"]
elasticsearch.username: "kibana_system"
elasticsearch.password: "<KIBANA_PASSWORD>"
```

Start Kibana.

```bash
sudo systemctl enable kibana
sudo systemctl start kibana
```

Check Kibana is serving traffic.

```bash
curl -I http://localhost:5601
```

Open the Kibana UI in a browser:

- http://10.0.0.10:5601

## Step 4: Install Wazuh Manager

Add the Wazuh repository.

```bash
curl -s https://packages.wazuh.com/key/GPG-KEY-WAZUH | sudo gpg --dearmor -o /usr/share/keyrings/wazuh.gpg
sudo tee /etc/apt/sources.list.d/wazuh.list > /dev/null <<'EOF'
deb [signed-by=/usr/share/keyrings/wazuh.gpg] https://packages.wazuh.com/4.x/apt/ stable main
EOF
```

Install the Wazuh manager package.

```bash
sudo apt-get update
sudo apt-get install -y wazuh-manager
```

Start and enable the manager.

```bash
sudo systemctl daemon-reload
sudo systemctl enable wazuh-manager
sudo systemctl start wazuh-manager
```

Check service state.

```bash
sudo systemctl status wazuh-manager
```

## Step 5: Configure Wazuh Manager to use Elasticsearch

Edit the Wazuh manager configuration file.

```bash
sudo nano /var/ossec/etc/ossec.conf
```

Ensure the manager is set to connect to the correct indexes and that the Elasticsearch connection is enabled. In a basic lab install with the default Wazuh manager package, the generated configuration is usually enough for a single-node environment.

Validate the config:

```bash
sudo /var/ossec/bin/wazuh-control status
```

## Step 6: Install Wazuh Dashboard

For local lab use, Wazuh Dashboard is a convenient UI that sits on top of the Wazuh API. It is often easier than using raw Kibana for immediate analyst work.

Install the Wazuh dashboard package.

```bash
sudo apt-get install -y wazuh-dashboard
```

Configure the dashboard.

```bash
sudo nano /etc/wazuh-dashboard/opensearch_dashboards.yml
```

Set the host and Elasticsearch URL.

```yaml
server.host: "0.0.0.0"
server.port: 5601
opensearch.hosts: ["https://localhost:9200"]
opensearch.ssl.verificationMode: none
opensearch.username: "kibana_system"
opensearch.password: "<PASSWORD>"
```

Start the dashboard.

```bash
sudo systemctl enable wazuh-dashboard
sudo systemctl start wazuh-dashboard
```

Open the dashboard in a browser:

- http://10.0.0.10:5601

## Step 7: Verify the environment

Once services are running, verify the manager can communicate with Elasticsearch and that the Wazuh UI loads.

Useful checks:

```bash
curl -k https://localhost:9200
curl -s http://localhost:55000
```

The Wazuh API is usually available on port 55000 in the default lab setup.

## Step 8: Register agents

Proceed to the agent onboarding guide in `docs/agent-onboarding.md`.

## Common troubleshooting

### Elasticsearch does not start

Check the log file:

```bash
sudo journalctl -u elasticsearch -n 100 --no-pager
```

Common issues:

- insufficient memory
- invalid YAML syntax
- permissions problems
- single-node discovery not enabled

### Wazuh manager not starting

```bash
sudo journalctl -u wazuh-manager -n 100 --no-pager
```

### Kibana cannot connect to Elasticsearch

Check the Elasticsearch certificate and credentials.

```bash
sudo grep -n "elasticsearch" /etc/kibana/kibana.yml
sudo journalctl -u kibana -n 100 --no-pager
```

## Recommended next steps

- install the Windows agent
- configure Sysmon on the endpoint
- install the Linux agent on the server
- run the lab exercises from `labs/`
- create detections from `detections/sigma/`

## Lab success criteria

Your lab is ready when:

- the manager is running
- Elasticsearch responds on 9200
- Kibana or Wazuh dashboard loads
- at least one Windows and one Linux agent are active
- telemetry is visible in the dashboard

## Notes

The exact package versions and command syntax may vary slightly depending on the date and distribution. The general lab flow remains the same: install Elasticsearch, install Kibana, install Wazuh Manager, register agents, and validate the data flow.
