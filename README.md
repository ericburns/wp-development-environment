# WordPress Theme Development Environment

## Installation

### Install VirtualBox

1) Download [VirtualBox](https://www.virtualbox.org/wiki/Downloads).
2) Install it.

You can check that the install worked by opening a terminal and typing `VBoxManage --version`.

_Example output_:

```
5.2.14r123301
```

### Install Vagrant

1) Download [Vagrant](https://www.vagrantup.com/downloads.html).
2) Install it.

You can check that the install worked by opening a terminal and typing `vagrant --version`.

_Example output_:

```
Vagrant 2.1.2
```

## Setup

### Configure database & domain

In `ansible/playbook.yml`, you can modify the following:

```ansible
database_name: db_name
database_user: db_user
database_password: db_pass
wp_domain: dev.example.com
```

### Create & Provision the VM

From the root directory, open a terminal and run:

```bash
vagrant up
```

This will take a while. Vagrant has to download a copy of the OS, install required packages, move files around, etc.

### Testing that it works

Go to `192.168.33.20` in a browser, to access the development site.

You can change this IP by modifying the `private_network` IP in `Vagrantfile`:

```
config.vm.network "private_network", ip: "192.168.33.20"
```

Optionally, you may also modify your hosts file. In OSX, add the following to `/etc/hosts`:

```
192.168.33.20   dev.example.com
```

_If you changed the IP or the domain, make sure it is reflected here._

You may have to refresh your hosts file:

```bash
sudo dscacheutil -flushcache; sudo killall -HUP mDNSResponder
```

## Development

`src/plugins` and `src/themes` map to `/var/www/wordpress/wp-content/plugins` and `/var/www/wordpress/wp-content/themes`, respectively.

Changes here are reflected in the VM.