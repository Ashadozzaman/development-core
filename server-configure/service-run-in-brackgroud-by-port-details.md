## 1. **Check for a Service Running in the Background (By Port)**
   To check if a service is running on a specific port, you can use `netstat`, `ss`, or `lsof`.

   **Using `netstat`:**
   ```bash
   sudo netstat -tuln | grep :<port_number>
   ```
   **Using `ss`:**
   ```bash
   sudo ss -tuln | grep :<port_number>
   ```
   **Using `lsof`:**
   ```bash
   sudo lsof -i :<port_number>
   ```

   Replace `<port_number>` with the actual port number (e.g., 3000).

   **Example:**
   ```bash
   sudo netstat -tuln | grep :3000
   ```

## 2. **Forcefully Kill a Process by Port**
   If a process is using a specific port and needs to be stopped:

   **Using `fuser`:**
   ```bash
   sudo fuser -k <port_number>/tcp
   ```

   **Example:**
   ```bash
   sudo fuser -k 3000/tcp
   ```

   **Using `kill` with PID:**
   After identifying the PID of the process using the port (from `netstat`, `ss`, or `lsof` output):
   ```bash
   sudo kill -9 <PID>
   ```
   Replace `<PID>` with the actual Process ID.

### 3. **List All Running Services**
   To list all services and their statuses:
   ```bash
   sudo systemctl list-units --type=service --all
   ```

### 4. **Disable/Enable a Service at Boot**
   - **Disable a Service from Starting at Boot:**
     ```bash
     sudo systemctl disable <service_name>
     ```
   - **Enable a Service to Start at Boot:**
     ```bash
     sudo systemctl enable <service_name>
     ```

### 5. **Forcefully Stop a Stubborn Service**
   If a service isn't responding to `stop` commands:
   ```bash
   sudo systemctl stop <service_name> --force
   ```

   Alternatively, kill the service's process directly:
   ```bash
   sudo pkill -9 -f <service_name>
   ```
   Replace `<service_name>` with the command or process name associated with the service.

### 6. **Check Logs for a Service**
   To view logs for a specific service:
   ```bash
   sudo journalctl -u <service_name>
   ```

   **Example:**
   ```bash
   sudo journalctl -u nginx
   ```

These commands should help you effectively manage, check, and troubleshoot services on your server.