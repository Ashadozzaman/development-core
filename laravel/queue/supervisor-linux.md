To run your Laravel queue workers in the background using **Supervisor**, the configuration you provided looks good. Below are the detailed steps to set this up and ensure it works smoothly in the background:

---

### **1. Install Supervisor**

If Supervisor is not installed on your system, install it:

```bash
sudo apt update
sudo apt install supervisor
```

---

### **2. Configure Supervisor**

Create a new Supervisor configuration file for your Laravel queue workers.

```bash
sudo nano /etc/supervisor/conf.d/laravel-worker.conf
```

Paste the following content, replacing `your-user` with your actual system username:

```ini
[program:laravel-worker]
process_name=%(program_name)s_%(process_num)02d
command=php /home/uysys/Developement/laravel-queue/artisan queue:work --sleep=3 --tries=3 --timeout=300
autostart=true
autorestart=true
numprocs=2 // how many worker run at a time
user=uysys
redirect_stderr=true
stdout_logfile=/home/uysys/Developement/laravel-queue/storage/logs/worker.log
```

---

### **3. Update File Permissions**

Ensure that the `stdout_logfile` path exists and is writable by Supervisor. Create the log directory and adjust permissions if necessary:

```bash
mkdir -p /home/uysys/Developement/laravel-queue/storage/logs
chmod -R 775 /home/uysys/Developement/laravel-queue/storage/logs
```

---

### **4. Start and Enable Supervisor**

Reload Supervisor to apply the new configuration:

```bash
sudo supervisorctl reread
sudo supervisorctl update
sudo supervisorctl start laravel-worker:*
```

---

### **5. Verify Worker Status**

Check the status of the Laravel workers managed by Supervisor:

```bash
sudo supervisorctl status
```

You should see something like this:

```
laravel-worker:laravel-worker_00   RUNNING   pid 12345, uptime 0:00:30
laravel-worker:laravel-worker_01   RUNNING   pid 12346, uptime 0:00:30
```

---

### **6. Logs and Monitoring**

- The workers will now run in the background, and logs will be written to `/home/uysys/Developement/laravel-queue/storage/logs/worker.log`.
- To view logs in real-time:

```bash
sudo tail -f /var/log/supervisor/supervisord.log

tail -f /home/uysys/Developement/laravel-queue/storage/logs/worker.log
```

---

### **7. Manage Workers**

You can use these commands to manage the workers:

- **Restart all workers**:

  ```bash
  sudo supervisorctl restart laravel-worker:*
  ```

- **Stop all workers**:

  ```bash
  sudo supervisorctl stop laravel-worker:*
  ```

- **Start all workers**:
  ```bash
  sudo supervisorctl start laravel-worker:*
  ```

---

### **8. Ensure Supervisor Starts on Boot**

Enable Supervisor to start automatically on system boot:

```bash
sudo systemctl enable supervisor
```

---

This setup will ensure your Laravel queue workers run as a background service managed by Supervisor.
