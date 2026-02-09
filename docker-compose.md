Here’s a list of **commonly used `docker-compose` commands**, along with brief descriptions:

---

### 🛠️ Basic Commands

| Command                  | Description                                                          |
| ------------------------ | -------------------------------------------------------------------- |
| `docker-compose up`      | Starts all services defined in `docker-compose.yml`.                 |
| `docker-compose up -d`   | Starts all services in **detached** mode (runs in background).       |
| `docker-compose down`    | Stops and removes containers, networks, and volumes created by `up`. |
| `docker-compose build`   | Builds images for services defined in the `docker-compose.yml`.      |
| `docker-compose restart` | Restarts all services.                                               |
| `docker-compose stop`    | Stops all running services.                                          |
| `docker-compose start`   | Starts existing containers for services.                             |
| `docker-compose ps`      | Lists running containers managed by the current compose file.        |

---

### 📦 Service Specific

| Command                               | Description                                      |
| ------------------------------------- | ------------------------------------------------ |
| `docker-compose up service_name`      | Starts only the specified service.               |
| `docker-compose build service_name`   | Builds the image only for the specified service. |
| `docker-compose restart service_name` | Restarts a specific service.                     |

---

### 🐚 Executing Commands Inside Containers

| Command                                    | Description                                          |
| ------------------------------------------ | ---------------------------------------------------- |
| `docker-compose exec service_name bash`    | Opens a Bash shell inside the container.             |
| `docker-compose exec service_name sh`      | Opens a `sh` shell (useful if Bash isn't installed). |
| `docker-compose exec service_name COMMAND` | Runs a specific command inside the container.        |

---

### 🧹 Cleanup & Maintenance

| Command                                | Description                                                              |
| -------------------------------------- | ------------------------------------------------------------------------ |
| `docker-compose down -v`               | Also removes named volumes declared in `volumes`.                        |
| `docker-compose down --rmi all`        | Removes all images used by any service.                                  |
| `docker-compose down --remove-orphans` | Removes containers for services not defined in the current compose file. |
| `docker-compose rm`                    | Removes stopped service containers.                                      |

---

### 🔍 Logs and Monitoring

| Command                            | Description                                   |
| ---------------------------------- | --------------------------------------------- |
| `docker-compose logs`              | Shows logs for all services.                  |
| `docker-compose logs -f`           | Tails logs (like `tail -f`) for all services. |
| `docker-compose logs service_name` | Shows logs for a specific service.            |

---

### 🧪 Testing and Debugging

| Command                                   | Description                                                             |
| ----------------------------------------- | ----------------------------------------------------------------------- |
| `docker-compose run service_name COMMAND` | Runs a one-time command against a service (e.g., `artisan` in Laravel). |
| `docker-compose config`                   | Validates and shows the final config from your `docker-compose.yml`.    |

---

Let me know if you want examples or aliases for frequent usage!
