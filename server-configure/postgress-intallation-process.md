To create a PostgreSQL database named `konga` and a user named `konga_user` on a Debian machine, follow these steps:

### 1. Install PostgreSQL

First, ensure PostgreSQL is installed on your Debian machine. You can install it using the following command if it's not already installed:

```bash
sudo apt update
sudo apt install postgresql postgresql-contrib
```

### 2. Access PostgreSQL Shell

After installation, PostgreSQL should be running as a service. By default, it creates a `postgres` user and also sets up authentication. You can access the PostgreSQL command-line interface (CLI) as the `postgres` user:

```bash
sudo -u postgres psql
```

### 3. Create Database

Once inside the PostgreSQL shell (`psql`), you can create a database named `konga`:

```sql
CREATE DATABASE konga;
```

### 4. Create User

Next, create a user named `konga_user` with a password. Replace `'password'` with a strong password of your choice:

```sql
CREATE USER konga_user WITH PASSWORD 'password';
```

### 5. Grant Privileges

Grant all privileges on the `konga` database to the `konga_user`:

```sql
GRANT ALL PRIVILEGES ON DATABASE konga TO konga_user;
```

### 6. Modify Authentication Method (Optional)

By default, PostgreSQL on Debian uses "peer" authentication for local connections, meaning it expects Unix domain socket connections to use the same username as the system user. If you want to connect using the `konga_user` from other users or applications, you might need to modify the `pg_hba.conf` file. Here's how you can do it:

- Open the `pg_hba.conf` file:
  ```bash
  sudo nano /etc/postgresql/{version}/main/pg_hba.conf
  ```
  Replace `{version}` with your PostgreSQL version number (e.g., `12`).

- Add the following line at the bottom of the file to allow `konga_user` to connect from all hosts using password authentication:
  ```
  # TYPE  DATABASE        USER            ADDRESS                 METHOD
  host    konga           konga_user      all                     md5
  ```

- Save and close the file. Then restart PostgreSQL for changes to take effect:
  ```bash
  sudo systemctl restart postgresql
  ```

### 7. Verify Setup

Exit the PostgreSQL shell by typing `\q`.

You can now verify that the `konga` database and `konga_user` have been created successfully:

- Connect to PostgreSQL using the `konga_user`:
  ```bash
  psql -U konga_user -d konga -h localhost
  ```
  You will be prompted to enter the password you set for `konga_user`.

- Once connected, you can start using the `konga` database and perform any necessary operations.

This completes the process of creating a PostgreSQL database named `konga` and a user `konga_user` on a Debian machine. Adjust any details such as passwords and privileges according to your specific requirements and security policies.