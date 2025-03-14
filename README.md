# GPU Monitoring Client (gpu-mon-cli)

## Overview

The **GPU Monitoring Client (gpu-mon-cli)** is designed to efficiently manage and collect real-time GPU performance data across multi-cloud and multi-site environments at scale. It transmits collected data to Splunk for visualization and analysis.

## Download

You can download the latest version of **gpu-mon-cli** from [here](#).

### Included Files

- `config_cli`
- `run`

## System Requirements

### Software Pre-requisites

- OS: Linux/Ubuntu
- Python: 3.8 or above

### Hardware Architecture

- x86\_64

## Configuration

Before running **gpu-mon-cli**, you need to configure it.

### Steps to Configure gpu-mon-cli

1. Open a terminal on your Linux system.
2. Execute the following command:
   ```sh
   sudo ./config_cli
   ```
3. Provide the required details as prompted:
   - **Enable Debugging**: Set to `True` to enable debug messages (default: `False`).
   - **Enable CSV Dump**: Set to `True` to store captured data in CSV format (default: `False`).
   - **Enable Logs**: Set to `True` to generate logs for troubleshooting (default: `False`).
   - **Sampling Interval Seconds**: Defines the time interval for data capture (default: `60` seconds).
   - **Splunk HTTPS Enabled**: Set to `True` if Splunk is using HTTPS.
   - **Splunk Host Address**: Provide the Splunk IP address or hostname (default: `127.0.0.1`).
   - **Splunk Collector Port**: Provide Splunk HTTP Event Collector port (default: `8088`).
   - **Splunk Management Port**: Provide Splunk Management Port (default: `8089`).
   - **Splunk Host App Owner**: Define the application owner (default: `nobody`).
   - **Splunk Host App Name**: Define the application name (default: `onstak_gpu_pmd`).
   - **Splunk Host App Metrics Source Type**: Define the source type (default: `onstak_gpu_pmd`).
   - **Splunk Metrics Token**: Provide the token (no default value, must be provided).
   - **Splunk Host App Username**: Provide the admin username.
   - **Splunk Host App Password**: Provide the admin password.

### Notes:

- All sensitive information is stored in an encrypted format.
- The configuration will only be saved if all inputs pass validation.

## Running gpu-mon-cli

### Running the Application

1. Open a terminal on your GPU-enabled machine.
2. Navigate to the directory where `gpu-mon-cli` is located.
3. Execute the following command:
   ```sh
   sudo ./run
   ```
4. Upon successful execution, real-time GPU performance metrics will be collected and sent to Splunk.

### Running as a Background Process

To ensure uninterrupted execution, it is recommended to run `gpu-mon-cli` as a background process using **systemd**.

### Setting up systemd Service for gpu-mon-cli

1. Create a new service file:
   ```sh
   sudo nano /etc/systemd/system/gpu-mon.service
   ```
2. Add the following content:
   ```ini
   [Unit]
   Description=GPU Monitoring Client Service
   After=network.target

   [Service]
   Type=simple
   WorkingDirectory=/path/to/gpu-mon-cli
   ExecStart=/usr/bin/sudo ./run
   Restart=always
   RestartSec=60
   User=root

   [Install]
   WantedBy=multi-user.target
   ```
3. Reload **systemd**, enable, and start the service:
   ```sh
   sudo systemctl daemon-reload
   sudo systemctl enable gpu-mon
   sudo systemctl start gpu-mon
   ```

This setup ensures that **gpu-mon-cli** runs continuously and automatically restarts if it stops or if the system reboots.

## Support

For further assistance, please contact our support team.

---

**Note:** This document provides installation and configuration instructions for `gpu-mon-cli`. Ensure all necessary permissions and dependencies are met before running the application.

