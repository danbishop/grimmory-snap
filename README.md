# grimmory-snap

[![Get it from the Snap Store](https://snapcraft.io/en/dark/install.svg)](https://snapcraft.io/grimmory)

Grimmory is a self-hosted library management system for ebooks, comics, and audiobooks. Your books and data stay on your server, with no subscription fees or cloud dependency.

**This is an unofficial snap.** After installing, and waiting for the the various
services to start, your instance will be accessible at http://localhost:6060

You'll probably want to connect the snap as follows to grant access to your books
which should be in `/mnt/somewhere` or `/media/somewhere` so that the snap can see them:

```bash
sudo snap connect grimmory:removable-media
sudo snap connect grimmory:mount-observe
```

There are two services, backend (the Grimmory server),
and mariadb (the database server). The database files and logs are stored in the snap's
data directory, which is preserved across snap updates.

**Ports**

You can change the port that each service uses with the following commands:

For the port that MariaDB listens on (default 41936):

```bash
sudo snap set grimmory database-port=<desired-port>
```

For the port that grimmory-api listens on (default 6060):

```bash
sudo snap set grimmory api-port=<desired-port>
```

After changing the ports, you will need to restart the snap for the changes to take effect:

```bash
sudo snap restart grimmory
```

**Database**

If you need to connect to the MariaDB database from outside the snap, the username is `grimmory`
and you can use the following command to get the password:

```bash
snap get grimmory database-password
```

You can also connect with the following command as root:

```bash
sudo mariadb --socket=/var/snap/grimmory/common/run/mysql/mysqld.sock -u root --skip-ssl
```
