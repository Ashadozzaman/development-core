To install Composer on a Debian system, follow these steps:

### Step 1: Update the package manager
```bash
sudo apt update
```

### Step 2: Install required dependencies
```bash
sudo apt install curl php-cli php-mbstring git unzip
```

### Step 3: Download the Composer installer
```bash
curl -sS https://getcomposer.org/installer -o composer-setup.php
```

### Step 4: Verify the installer signature (optional but recommended)
First, get the latest Composer signature hash from the [Composer Public Keys page](https://composer.github.io/pubkeys.html) or run the following command:
```bash
HASH=$(curl -sS https://composer.github.io/installer.sig)
```

Then, verify the downloaded installer:
```bash
php -r "if (hash_file('sha384', 'composer-setup.php') === '$HASH') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
```

### Step 5: Install Composer globally
```bash
sudo php composer-setup.php --install-dir=/usr/local/bin --filename=composer
```

### Step 6: Remove the installer script
```bash
rm composer-setup.php
```

### Step 7: Verify the installation
```bash
composer --version
```

This will display the installed Composer version, confirming that it has been installed successfully on your Debian system.