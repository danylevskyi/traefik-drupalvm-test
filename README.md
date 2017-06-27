# Traefik proxy for Drupal VM test

This repository aims to show a simple example for usage Traefik as a proxy for 2 Drupal VM containers.

## Requirements

  - docker (Mac users should use Docker Edge for better performance)
  - docker-compose
  - composer

## How to install

### 1. Clone the repository to your local directory

### 2. Edit your `hosts` file

```
127.0.0.1       drupal1.dev
127.0.0.1       drupal2.dev
```

### 3. Download Drupal source code

```
cd drupal1 && composer create-project drupal-composer/drupal-project:8.x-dev drupal --stability dev --no-interaction
cd drupal2 && composer create-project drupal-composer/drupal-project:8.x-dev drupal --stability dev --no-interaction
```

### 4. Start the containers

```
cd traefik && docker-compose up -d
cd drupal1 && docker-compose up -d
cd drupal2 && docker-compose up -d
```

### 5. Install Drupal

```
docker exec drupal1 bash -c "drush site-install standard -y --db-url=mysql://drupal:drupal@localhost/drupal --root=/var/www/drupalvm/drupal/web --account-name=admin --account-pass=admin --site-name=Drupal1"
docker exec drupal2 bash -c "drush site-install standard -y --db-url=mysql://drupal:drupal@localhost/drupal --root=/var/www/drupalvm/drupal/web --account-name=admin --account-pass=admin --site-name=Drupal2"
```

### 6. Test it

Visit `http://drupal1.dev` and `http://drupal1.dev`. You should see working Drupal installations.
