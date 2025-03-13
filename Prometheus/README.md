# Setting Up Prometheus as a Systemd Service

This guide provides a step-by-step process for installing, configuring, and running Prometheus as a background service using systemd.

## Installation and Setup

### 1. Download and Extract Prometheus
1. Use `wget` to download Prometheus:
   ```bash
   wget <prometheus_download_link>
   ```
2. Extract the downloaded tarball:
   ```bash
   tar xvf <prometheus_tarball>
   ```
3. Move into the extracted directory:
   ```bash
   cd prometheus-
   ```
   *(Ensure the directory name matches your downloaded version.)*

### 2. Creating a Dedicated User and Group for Prometheus
1. Create a new user and group named `promet`:
   ```bash
   sudo useradd --no-create-home --shell /bin/false promet

   Note: Remember, for simplicity i consider User and Group as "promet" (throught the page)
   ex:
      uid=1007(promet) gid=1008(promet) groups=1008(promet)
   ```

### 3. Move Prometheus Files to Appropriate Directories &  Set Permissions for Prometheus Directories and Files
1. Create necessary directories:
   ```bash
   sudo mkdir -p /etc/prometheus /var/lib/prometheus
   sudo chown promet:promet /etc/prometheus/
   sudo chown promet:promet /var/lib/prometheus/
   ```
2. Copy Prometheus binaries to `/usr/local/bin/`:
   ```bash
   sudo cp prometheus /usr/local/bin/
   sudo cp promtool /usr/local/bin/
   sudo chown promet:promet /usr/local/bin/prometheus
   sudo chown promet:promet /usr/local/bin/promtool
   ```
3. Copy configuration files:
   ```bash
   sudo cp -r consoles /etc/prometheus/
   sudo chown -R promet:promet /etc/prometheus/consoles/
   sudo cp -r console_libraries /etc/prometheus/
   sudo chown -R promet:promet /etc/prometheus/console_libraries/
   sudo cp prometheus.yml /etc/prometheus/
   sudo chown promet:promet /etc/prometheus/prometheus.yml
   ```

## Configuring Prometheus as a Systemd Service

### 5. Create a Systemd Service File
1. Open a new systemd service file:
   ```bash
   sudo vi /etc/systemd/system/prometheus.service
   ```
2. Add the following configuration:
   ```ini
   [Unit]
   Description=Prometheus
   Wants=network-online.target
   After=network-online.target

   [Service]
   User=promet
   Group=promet
   Type=simple
   ExecStart=/usr/local/bin/prometheus --config.file=/etc/prometheus/prometheus.yml --storage.tsdb.path=/var/lib/prometheus/

   [Install]
   WantedBy=multi-user.target
   ```

### 6. Reload Systemd and Start Prometheus Service
1. Reload systemd configuration:
   ```bash
   sudo systemctl daemon-reload
   ```
2. Enable Prometheus to start on boot:
   ```bash
   sudo systemctl enable prometheus
   ```
3. Start Prometheus service:
   ```bash
   sudo systemctl start prometheus
   ```
4. Check the status of Prometheus:
   ```bash
   sudo systemctl status prometheus
   ```

## Verifying the Installation
Once Prometheus is running as a background service, you can access the web interface at:
```
http://localhost:9090
```

This confirms that Prometheus is successfully set up and running as a systemd service.

---

We ensure that Prometheus is properly installed, configured, and runs in the background even after a system reboot. This setup is ideal for production environments where continuous monitoring is required.
## =======================================================================================================================
# Setting Up Node Exporter as a Systemd Service

This guide provides a step-by-step process for installing, configuring, and running Node Exporter as a background service using systemd.

## Installation and Setup

### 1. Download and Extract Node Exporter
1. Use `wget` to download Node Exporter:
   ```bash
   wget <node_exporter_download_link>
   ```
2. Extract the downloaded tarball:
   ```bash
   tar xvf <node_exporter_tarball>
   ```
3. Move into the extracted directory:
   ```bash
   cd node_exporter-
   ```
   *(Ensure the directory name matches your downloaded version.)*

### 2. Move Node Exporter Binary to `/usr/local/bin/`
1. Copy the Node Exporter binary to the appropriate directory:
   ```bash
   sudo cp node_exporter /usr/local/bin/
   ```

### 3. Create a Dedicated User and Group for Node Exporter
1. Create a new user and group named `node_exporter`:
   ```bash
   sudo useradd --no-create-home --shell /bin/false node_exporter
   ```
2. Set ownership for the binary file:
   ```bash
   sudo chown node_exporter:node_exporter /usr/local/bin/node_exporter
   ```

## Configuring Node Exporter as a Systemd Service

### 4. Create a Systemd Service File
1. Open a new systemd service file:
   ```bash
   sudo vi /etc/systemd/system/node_exporter.service
   ```
2. Add the following configuration:
   ```ini
   [Unit]
   Description=Node Exporter
   Wants=network-online.target
   After=network-online.target

   [Service]
   User=node_exporter
   Group=node_exporter
   Type=simple
   ExecStart=/usr/local/bin/node_exporter

   [Install]
   WantedBy=multi-user.target
   ```

### 5. Reload Systemd and Start Node Exporter Service
1. Reload systemd configuration:
   ```bash
   sudo systemctl daemon-reload
   ```
2. Enable Node Exporter to start on boot:
   ```bash
   sudo systemctl enable node_exporter
   ```
3. Start Node Exporter service:
   ```bash
   sudo systemctl start node_exporter
   ```
4. Check the status of Node Exporter:
   ```bash
   sudo systemctl status node_exporter
   ```

## Verifying the Installation
Once Node Exporter is running as a background service, you can access its metrics at:
```
http://localhost:9100/metrics
```

This confirms that Node Exporter is successfully set up and running as a systemd service.

---
We ensure that Node Exporter is properly installed, configured, and runs in the background even after a system reboot. This setup is ideal for monitoring system metrics efficiently.


