# Setting Up Prometheus and cAdvisor in Docker

This guide provides a step-by-step process for setting up Prometheus in Docker along with cAdvisor to monitor container-level metrics.

## Prerequisites
- Installed Docker and Docker Compose
- Basic knowledge of Docker commands

---

## Step 1: Check Running Docker Containers
To see how many Docker containers are currently running, execute:
```bash
docker ps
```

---

## Step 2: Enable Docker Metrics Exporter
By default, Docker does not export any metrics. To enable it:

### 1. Edit the Docker Daemon Configuration File
```bash
sudo vi /etc/docker/daemon.json
```

### 2. Add the Following Configuration
```json
{
  "metrics-addr": "127.0.0.1:9323",
  "experimental": true
}
```

### 3. Restart Docker Service
```bash
sudo systemctl restart docker
```

### 4. Verify if Docker is Exporting Metrics
```bash
curl localhost:9323/metrics
```

To further configure Docker’s networking and optimize container management, you can update `/etc/docker/daemon.json` as follows:

```json
{
  "exec-opts": [
    "native.cgroupdriver=cgroupfs"
  ],
  "bip": "172.12.0.1/24",
  "registry-mirrors": [
    "http://docker-registry-mirror.kodekloud.com"
  ],
  "metrics-addr": "127.0.0.1:9323",
  "experimental": true
}
```

Restart Docker again:
```bash
sudo systemctl restart docker
```

---

## Step 3: Configure Prometheus to Monitor Docker
### 1. Edit the Prometheus Configuration File
```bash
sudo vi /etc/prometheus/prometheus.yml
```

### 2. Add the Following Job Configuration Under `scrape_configs`:
```yaml
  - job_name: "docker"
    static_configs:
      - targets: ["localhost:9323"]
```

### 3. Restart Prometheus Service
```bash
sudo systemctl restart prometheus
```

### 4. Verify Metrics in Prometheus
Use the expression search box in Prometheus UI (`http://localhost:9090`) to check:
```
engine_daemon_container_states_containers
```
This will display container statuses.

---

## Step 4: Configure Prometheus to Monitor cAdvisor
### 1. Edit the Prometheus Configuration File Again
```bash
sudo vi /etc/prometheus/prometheus.yml
```

### 2. Add the Following Job Configuration:
```yaml
  - job_name: "cadvisor"
    static_configs:
      - targets: ["localhost:8070"]
```

### 3. Restart Prometheus Service
```bash
sudo systemctl restart prometheus
```

---

## Step 5: Deploy cAdvisor to Collect Container-Level Metrics
cAdvisor collects and exposes metrics about running containers.

### 1. Create a Docker Compose File
```bash
sudo vi /root/docker-compose.yml
```

### 2. Add the Following Configuration:
```yaml
version: '3.4'
services:
  cadvisor:
    image: gcr.io/cadvisor/cadvisor
    container_name: cadvisor
    privileged: true
    devices:
      - "/dev/kmsg:/dev/kmsg"
    volumes:
      - /:/rootfs:ro
      - /var/run:/var/run:ro
      - /sys:/sys:ro
      - /var/lib/docker/:/var/lib/docker:ro
      - /dev/disk/:/dev/disk:ro
    ports:
      - 8070:8080
```

### 3. Deploy the cAdvisor Container
```bash
cd /root/
docker compose up -d
```

### 4. Verify if cAdvisor is Running
```bash
curl localhost:8070/metrics
```

### 5. Add cAdvisor as a Prometheus Job
Edit `/etc/prometheus/prometheus.yml` again:
```yaml
  - job_name: "cadvisor"
    static_configs:
      - targets: ["localhost:8070"]
```

### 6. Restart Prometheus Service
```bash
sudo systemctl restart prometheus
```

---

## Step 6: Access Prometheus and Monitor Metrics
Once all configurations are set up, access Prometheus UI at:
```
http://localhost:9090
```
You can monitor metrics from both Docker and cAdvisor.

To check container status, search for:
```
engine_daemon_container_states_containers
```

To check per-container resource utilization, search for:
```
cadvisor_container_cpu_usage_seconds_total
```

---

## Conclusion
By following this setup, you:
- Enabled Docker metrics export on port 9323
- Integrated Prometheus to collect Docker metrics
- Deployed cAdvisor for per-container monitoring
- Configured Prometheus to collect cAdvisor metrics

This setup ensures Prometheus efficiently monitors your Docker containers and provides valuable insights into their performance and health.

