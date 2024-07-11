### Prerequisites
- A running Kong installation
- Nodejs >= 8, <= 12.x (12.16 LTS is recommended)
- Npm
### Installation
Install npm and node.js. Instructions can be found [here](https://sailsjs.com/#/getStarted?q=what-os-do-i-need).

Install bower, ad gulp packages.
```
$ git clone https://github.com/pantsel/konga.git
$ cd konga
$ npm i
```
### Configuration
You can configure your application to use your environment specified settings.
There is an example configuration file on the root folder.
```
sudo cp .env_example .env
```
Just copy this to `.env` and make necessary changes to it. Note that this `.env` file is in .gitignore so it won't go to VCS at any point.
### Databases Integration
Konga is bundled with It's own persistence mechanism for storing users and configuration.

A local persistent object store is used by default, which works great as a bundled, starter database (with the strict caveat that it is for non-production use only).

The application also supports some of the most popular databases out of the box:

- MySQL
- MongoDB
- PostgresSQL
In order to use them, set the appropriate env vars in your `.env` file.
### Running Konga
## Development
```
$ npm start
```
Konga GUI will be available at http://localhost:1337

## Production

### Database Setup:
Install MySQL: If MySQL is not already installed on your system, install it first.
```
sudo apt update
sudo apt install mysql-server
```
Create a Database: Start the MySQL service and create a database and user for Konga:
```
sudo mysql
```
In the MySQL console, create a database and user, and grant the necessary permissions:
```
CREATE DATABASE konga;
CREATE USER 'konga_user'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON konga.* TO 'konga_user'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```
### Configure Konga:
**Set DB Adapter and URI:** In the .env file of Konga, modify the DB_ADAPTER and DB_URI variables:
```
DB_ADAPTER=mysql
DB_URI=mysql://konga_user:password@localhost:3306/konga
```

```
DB_ADAPTER=postgres
DB_URI=postgresql://kong:Start@123@localhost:5432/konga
```
Replace `password` with the password you set for the MySQL user `konga_user`.

### Install Dependencies:
Navigate to your `Konga` directory and `run npm install` to install the required dependencies:
```
cd ~/konga
npm install
```
### Start Konga:
Once the dependencies are installed and the `.env` file is configured, start Konga using the `npm start` command:
```
npm start
```
### Access Konga:
Open a web browser and navigate to `http://localhost:1337` (or the port you specified in the `.env` file). You should be able to access Konga's web interface.

### Debugging
I need Change the user's authentication method
```
ALTER USER 'konga_user'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
FLUSH PRIVILEGES;
```
Update the `sails-mysql` package:
```
npm update sails-mysql
```
#### Some time need to create manualy database and table.
In case of MySQL or PostgresSQL adapters, Konga will not perform db migrations when running in production mode.

You can manually perform the migrations by calling `$ node ./bin/konga.js ` prepare , passing the args needed for the database connectivity.

For example for:

```
$ node ./bin/konga.js  prepare --adapter postgres --uri postgresql://localhost:5432/konga

node ./bin/konga.js prepare --adapter mysql --uri mysql://konga_user:Start@123@localhost:3306/konga
```
The process will exit after all migrations are completed.
##### Finally:

```
npm run production
```
Run in background
```
nohup npm run production &
```

Konga GUI will be available at http://localhost:1337

## Reference URL [Here](https://github.com/pantsel/konga?tab=readme-ov-file#installation)
