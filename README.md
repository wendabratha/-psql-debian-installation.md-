# -psql-debian-installation.md-

# Postgres

1. Create the file /etc/apt/sources.list.d/pgdg.list, and add a line for the repository:
`deb http://apt.postgresql.org/pub/repos/apt/ YOUR_DEBIAN_VERSION_HERE-pgdg main`

2. Import the repository signing key, and update the package lists.
```bash
wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | \
  sudo apt-key add -
sudo apt-get update 
```

3. Install from the package manager.
`apt-get install postgresql-9.5` (or whatever)

Here's [the documentation](http://www.postgresql.org/download/linux/debian/).

1. apt.postgresql.org has the PostGIS packages too, so...
`sudo apt-get install postgresql-9.5-postgis-2.2 pgadmin3 postgresql-contrib-9.5`

2. For routing:
`sudo apt-get install postgresql-9.5-pgrouting`

3. Enable Adminpack:
```bash
# Log in to the psql console as postgres user:
sudo -u postgres psql
```

```sql
CREATE EXTENSION adminpack;
-- Never install PostGIS in the postgres database, create a user database.
-- You can also enable the PostGIS extension here (or with the GUI as described below):
CREATE DATABASE gisdb;
\connect gisdb;

CREATE EXTENSION postgis;
SELECT postgis_full_version();

-- Install pgRouting
CREATE  EXTENSION pgrouting;
SELECT * FROM pgr_version();

\q
```

See http://postgis.net/install/ and http://trac.osgeo.org/postgis/wiki/UsersWikiPostGIS22UbuntuPGSQL95Apt
