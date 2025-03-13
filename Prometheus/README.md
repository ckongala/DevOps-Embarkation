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
   ```

### 3. Move Prometheus Files to Appropriate Directories
1. Create necessary directories:
   ```bash
   sudo mkdir -p /etc/prometheus /var/lib/prometheus
   ```
2. Copy Prometheus binaries to `/usr/local/bin/`:
   ```bash
   sudo cp prometheus /usr/local/bin/
   sudo cp promtool /usr/local/bin/
   ```
3. Copy configuration files:
   ```bash
   sudo cp -r consoles /etc/prometheus/
   sudo cp -r console_libraries /etc/prometheus/
   sudo cp prometheus.yml /etc/prometheus/
   ```

### 4. Set Permissions for Prometheus Directories and Files
1. Change ownership to the `promet` user and group:
   ```bash
   sudo chown -R promet:promet /etc/prometheus
   sudo chown -R promet:promet /var/lib/prometheus
   ```
2. Adjust permissions:
   ```bash
   sudo chmod 644 /etc/prometheus/prometheus.yml
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

By following these steps, you ensure that Prometheus is properly installed, configured, and runs in the background even after a system reboot. This setup is ideal for production environments where continuous monitoring is required.

