To install the Redis PHP extension for PHP 8.2, you can follow these steps:

1. **Update Package Repositories:**
   It's a good practice to update your package repositories to ensure you get the latest available packages. Run the following command:

   ```bash
   sudo apt update
   ```

2. **Install Redis Server:**
   If you haven't already installed Redis server, you can do so by running:

   ```bash
   sudo apt install redis-server
   ```

3. **Install Redis PHP Extension:**
   Install the Redis PHP extension for PHP 8.2:

   ```bash
   sudo apt install php8.2-redis
   ```

   This command will install the Redis PHP extension for PHP 8.2.

4. **Restart PHP-FPM Service:**
   After installing the Redis PHP extension, restart your PHP-FPM service to apply the changes:

   ```bash
   sudo systemctl restart php8.2-fpm
   ```

   This command may vary depending on your PHP-FPM service name.

5. **Verify Installation:**
   You can verify that the Redis PHP extension is installed and enabled by creating a PHP file (e.g., `info.php`) in your web server's document root with the following content:

   ```php
   <?php
   phpinfo();
   ```

   Then, access this file from your browser (`http://your_server_ip/info.php`) and search for "redis" to see if the extension is listed and enabled.

Once you have completed these steps, the Redis PHP extension should be installed and ready to use with PHP 8.2. You can now proceed with your application, and the `Redis` class should be available for use.