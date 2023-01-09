# The Landing Pad Dockerized Wordpress website

## Getting started

You can use Docker to run a local instance of the site after restoring it from
a backup.

1. Restore a backup of the website
    1. Run `docker compose up`
        * Starts the Docker containers
    1. Visit http://localhost:8080/wp-admin/install.php
        * Setup Wordpress with any settings, these will be overridden later
    1. Log in to http://localhost:8080/wp-admin/
    1. Install the [All-in-One WP Migration plugin][1] ([developer website][2])
    1. Use the All-in-One WP Migration plugin to import a `*.wpress` backup
1. Use phpMyAdmin to gain access to the website
    1. Visit http://localhost:8081
    1. Log in using the username and password specified in the `docker/db/.env`
      file
    1. Set a new password for the `admin` user in the `wrd_users` table
        * Hash the password plaintext using the MD5 function
1. Log in to the restored website
    1. Visit http://localhost:8080/wp-admin
    1. Log in with the credentials set in the previous step

## Exporting a static site

The static version of the website is stored in the `docs` directory and hosted
on [GitHub Pages][5].

1. Use the [Simply Static plugin][3] ([developer website][4]) to generate a
static version of the website
    * Ensure the "Destination URLs" option under the "General" tab is set to
      "Save for offline use"
    * Ensure the "Force URL replacements" option under the "Advanced" tab is
      selected
1. Remove all files in the `docs` directory
    * This ensures deleted files aren't preserved when importing the new files
1. Download and unzip the exported files
1. Copy the exported files into the `docs` directory
1. Commit changes and push to GitHub

## phpMyAdmin

phpMyAdmin is available at http://localhost:8081 after starting up the Docker
containers. The database user and password are in the `docker/db/.env` file

## Miscellaneous

### Accessing the Wordpress container (`web`)

```
docker exec -it landing-pad-wp-web-1 bash
```

### Accessing the database

```
docker exec -it landing-pad-wp-db-1 mysql thelanf1_wor1 -u thelanf1_wor1 -p
```

### Deleting the Docker Compose project

This may be helpful to start fresh, e.g. reset the database

```
docker compose -p landing-pad rm -fv
```

[1]: https://wordpress.org/plugins/all-in-one-wp-migration/
[2]: https://servmask.com/
[3]: https://wordpress.org/plugins/simply-static/
[4]: https://patrickposner.dev/
[5]: https://pages.github.com/
