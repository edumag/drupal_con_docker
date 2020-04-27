# Drupal8 con docker

## Entrar en contenedor.

`docker exec -it drupal8 bash`

## Drush

```
cd web
../vendor/drush/drush/drush cr
```

## Console commands

```
cd web
../vendor/drupal/console/bin/drupal cache:rebuild
```
## Composer.

```
composer require drupal/devel
```

## Crear proyecto

```
COMPOSER_MEMORY_LIMIT=-1 composer create-project drupal/recommended-project [PROYECTO]
```

## Instalar módulos:

```
COMPOSER_MEMORY_LIMIT=-1 composer require drupal/devel
```

Añadimos COMPOSER_MEMORY_LIMIT para evitar problemas de memoria.

## Activar módulo

```
cd web/
../vendor/drupal/console/bin/drupal module:install devel
```

## Actualizar drupal

```
COMPOSER_MEMORY_LIMIT=-1 composer update
../vendor/drush/drush/drush updatedb
../vendor/drush/drush/drush cache:rebuild
```

## Crear contenido de prueba.

```
../vendor/drupal/console/bin/drupal create:terms
../vendor/drupal/console/bin/drupal create:nodes
```

## Instalar y activar tema.

```
../vendor/drupal/console/bin/drupal theme:download bootstrap_barrio
../vendor/drush/drush/drush theme:enable bootstrap_barrio
```

## Referencias

- https://hub.docker.com/r/feikede/drupal8-docker/
