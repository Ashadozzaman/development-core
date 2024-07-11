To run an `npm run production` command in the background by creating a service, you can use a system service manager like `systemd` on Linux. Below are the steps to create a systemd service for your npm script:

1. **Create a service file**:
   
   Create a new service file in the `/etc/systemd/system` directory. You will need superuser privileges to do this. For example, you can create a file named `npm-production.service`:

   ```bash
   sudo nano /etc/systemd/system/npm-production.service
   ```

2. **Edit the service file**:

   Add the following content to the file. Modify the paths and user as needed for your environment:

   ```ini
        [Unit]
        Description=Node.js Production Service For Konga
        After=network.target

        [Service]
        ExecStart=/root/.nvm/versions/node/v12.22.12/bin/npm run production
        WorkingDirectory=/root/konga
        StandardOutput=journal
        StandardError=journal
        SyslogIdentifier=npm-production
        User=user-name
        Restart=always
        Environment=NODE_ENV=production
        Environment=PATH=/root/.nvm/versions/node/v12.22.12/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

        [Install]
        WantedBy=multi-user.target

   ```

   **Note:** Must be find the correct path using the `which` command for axctul path `ExecStart`&`Environment=PATH`:
   ```
   which npm
   ```

   - `ExecStart`: ExecStart=/root/.nvm/versions/node/v12.22.12/bin/npm run production: This specifies the command that starts the service. It uses the npm executable located in the specified path to run the production script.
   - `WorkingDirectory`: Path to your project directory.
   - `User`: The user under which the service should run. Replace `your-username` with the appropriate username.
   - `Restart`: Configures the service to restart automatically if it crashes.
   - `Environment`: Sets the environment variables, such as `NODE_ENV`.

3. **Reload the systemd manager configuration**:

   After creating or modifying the service file, reload the systemd manager configuration to make the system aware of the new service:

   ```bash
   sudo systemctl daemon-reload
   ```

4. **Enable the service**:

   Enable the service to start at boot:

   ```bash
   sudo systemctl enable npm-production
   ```

5. **Start the service**:

   Start the service immediately:

   ```bash
   sudo systemctl start npm-production
   ```

6. **Check the status of the service**:

   You can check the status of your service to ensure it is running correctly:

   ```bash
   sudo systemctl status npm-production
   ```

This setup will run your `npm run production` command in the background as a service, and it will restart automatically if it crashes.