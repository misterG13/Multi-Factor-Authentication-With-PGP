# Installing GnuPG for PHP

GnuPG (GNU Privacy Guard) is required for the `php-gnupg` extension, which this project uses for PGP encryption and key management.

## Requirements

- GnuPG 2.x installed on the system
- [GPGME](https://www.gnupg.org/related_software/gpgme/) library (`libgpgme`), required by the extension
- PHP 8.0+ with the `php-gnupg` extension

The `php-gnupg` extension is distributed through [PECL](https://pecl.php.net/package/gnupg). On most distributions the extension is also available as a distro package, which is the recommended quick path. See the [official installation manual](https://www.php.net/manual/en/gnupg.installation.php) for reference.

## Debian / Ubuntu

GnuPG and the PHP extension are available from the default repositories.

```bash
sudo apt-get update
sudo apt-get install -y php-gnupg gnupg2
```

To install for a specific PHP version (e.g., 8.3):

```bash
sudo apt-get install -y php8.3-gnupg gnupg2
```

After installing a distro PHP extension, restart the web server/PHP-FPM for the extension to be enabled.

### Alternative: Install via PECL

PECL compiles the extension against your exact PHP build and version:

```bash
# Required build dependencies
sudo apt-get update
sudo apt-get install -y gnupg2 libgpgme-dev php-dev php-pear

# Build and install the extension
sudo pecl install gnupg
```

Enable the extension whether it was installed via distro or PECL:

```bash
echo "extension=gnupg.so" | sudo tee /etc/php/8.3/mods-available/gnupg.ini
sudo phpenmod gnupg
```

Then restart your PHP service (e.g., `sudo systemctl restart php8.3-fpm`).

## Fedora / RHEL

```bash
sudo dnf install php-gnupg gnupg2
```

On older systems using `yum`:

```bash
sudo yum install php-gnupg gnupg2
```

Restart the web server/PHP-FPM after installation.

### Alternative: Install via PECL

```bash
sudo dnf install gnupg2 gpgme-devel php-devel php-pear

sudo pecl install gnupg
```

Enable the extension:

```bash
echo "extension=gnupg.so" | sudo tee /etc/php.d/gnupg.ini
```

Then restart your PHP service (e.g., `sudo systemctl restart php-fpm`).

## macOS

Install via Homebrew:

```bash
brew install gnupg
```

The PHP extension is installed via PECL (the manual's recommended method), which requires the GPGME library:

```bash
brew install gpgme

pecl install gnupg
```

Then add to your `php.ini`:

```ini
extension=gnupg.so
```

Restart your PHP service (e.g., `brew services restart php`).

## Verify Installation

**CLI method (recommended):**

```bash
php -m | grep gnupg
```

If `gnupg` appears in the output, the extension is loaded.

**Web method:**

Create a temporary file in your web root:

```bash
echo '<?php phpinfo();' | sudo tee phpinfo.php
```

Open `phpinfo.php` in a browser and search for `gnupg`. If the section exists, the extension is active.

Delete the file immediately after verification:

```bash
sudo rm -f phpinfo.php
```

> Never leave `phpinfo()` exposed in a production or public environment.

## Windows

Install [Gpg4win](https://gpg4win.org/download.html), which bundles GnuPG and required components for Windows.

For the PHP extension on Windows, see the [php-gnupg PECL page](https://pecl.php.net/package/gnupg).

## Resources

- [GnuPG Downloads](https://gnupg.org/download/)
- [php-gnupg Manual](https://www.php.net/manual/en/book.gnupg.php)
- [GnuPG Setup](https://www.php.net/manual/en/gnupg.setup.php)
- [php-gnupg Installation (official)](https://www.php.net/manual/en/gnupg.installation.php)
- [GnuPG Documentation](https://gnupg.org/documentation/)
- [Project Installation Guide](../README.md)