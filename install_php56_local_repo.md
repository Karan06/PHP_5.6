
# 🐘 Install PHP 5.6 from Local Repository on Ubuntu 20.04

This guide sets up PHP 5.6 using a local repository containing `.deb` files.

## 📁 Step 1: Organize Your `.deb` Files

Ensure all required `.deb` packages for PHP 5.6 are stored in:

```
/opt/php56-localrepo/
```

## 🛠️ Step 2: Create APT Package Index

Run the following commands:

```bash
cd /opt/php56-localrepo

# Generate the Packages index
dpkg-scanpackages . /dev/null | gzip -9c > Packages.gz
dpkg-scanpackages . /dev/null > Packages

# Set correct permissions
chmod -R a+r /opt/php56-localrepo
```

## 📦 Step 3: Add Local Repository to APT

Create a new source list file:

```bash
echo "deb [trusted=yes] file:/opt/php56-localrepo ./" | sudo tee /etc/apt/sources.list.d/php56-localrepo.list
```

Then update the package cache:

```bash
sudo apt update
```

## ✅ Step 4: Install PHP 5.6 and Extensions

```bash
sudo apt install php5.6 php5.6-cli php5.6-common php5.6-mbstring php5.6-xml \
php5.6-mysql php5.6-curl php5.6-zip php5.6-gd php5.6-mcrypt php5.6-readline \
php5.6-opcache php5.6-imap php5.6-ldap libapache2-mod-php5.6 -y
```

## 🔍 Step 5: Verify Installation

```bash
php -v
```

Expected output should include:

```
PHP 5.6.40 (cli) ...
```

---

💡 **Tip**: To serve PHP using Apache or Nginx, make sure the appropriate modules like `libapache2-mod-php5.6` or `php5.6-fpm` are installed and configured.

