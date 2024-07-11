The error message indicates that the `mysql-server` package is not available in the default Debian repositories you have configured. This can happen if the MySQL package has been removed or replaced in the Debian repositories.

To install MySQL on Debian, you can use the MySQL APT repository provided by Oracle. Here's how to do it:

### Step-by-Step Installation

1. **Download the MySQL APT Repository Configuration Package**:
   ```sh
   wget https://dev.mysql.com/get/mysql-apt-config_0.8.22-1_all.deb
   ```

2. **Install the MySQL APT Repository Configuration Package**:
   ```sh
   sudo dpkg -i mysql-apt-config_0.8.22-1_all.deb
   ```
   During the installation, you will be prompted to select the MySQL version. Make sure to select the appropriate version of MySQL Server (usually the latest GA version).

3. **Update the package index**:
   ```sh
   sudo apt update
   ```

4. **Install MySQL Server**:
   ```sh
   sudo apt install mysql-server
   ```

5. **Secure MySQL Installation** (Optional but recommended):
   ```sh
   sudo mysql_secure_installation
   ```
   This script will guide you through securing your MySQL installation by setting the root password, removing anonymous users, disallowing root login remotely, and removing test databases.

6. **Verify MySQL Installation**:
   ```sh
   sudo systemctl status mysql
   ```
   This command will show the status of the MySQL service, indicating whether it is running.

### Detailed Commands

1. **Download MySQL APT Configuration Package**:
   ```sh
   wget https://dev.mysql.com/get/mysql-apt-config_0.8.22-1_all.deb
   ```

2. **Install the downloaded package**:
   ```sh
   sudo dpkg -i mysql-apt-config_0.8.22-1_all.deb
   ```

3. **Update the package index**:
   ```sh
   sudo apt update
   ```

4. **Install MySQL Server**:
   ```sh
   sudo apt install mysql-server
   ```

5. **Secure MySQL Installation**:
   ```sh
   sudo mysql_secure_installation
   ```

By following these steps, you should be able to install MySQL on your Debian system without encountering the package availability issue.