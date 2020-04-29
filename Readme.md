# Entorno desarrollo drupal con docker

## Iniciar 

`./run`

o

`docker-composer up`

Abrir http://localhost:8010

## Entrar en contenedor.

`docker exec -it drupal-cercle bash`

Una vez dentro del contenedor instalaremos drupal-console y drush.

### Instalar drupal console.

```
composer require drupal/console:~1.0 --prefer-dist --optimize-autoloader
curl https://drupalconsole.com/installer -L -o drupal.phar
mv drupal.phar /usr/local/bin/drupal
chmod +x /usr/local/bin/drupal
```

### Instalar drush.

```
composer require drush/drush
ln -s /var/www/html/vendor/drush/drush/drush /usr/local/bin/
```

## Ejemplo de comandos que nos ayudarán en el desarrollo.

### Console commands

```
./vendor/drupal/console/bin/drupal cache:rebuild
```
### Composer.

```
composer require drupal/devel
```

### Instalar módulos:

```
COMPOSER_MEMORY_LIMIT=-1 composer require drupal/devel
```

Añadimos COMPOSER_MEMORY_LIMIT para evitar problemas de memoria.

### Activar módulo

```
./vendor/drupal/console/bin/drupal module:install devel
```

### Actualizar drupal

```
COMPOSER_MEMORY_LIMIT=-1 composer update
drush updatedb
drush cache:rebuild
```

### Crear contenido de prueba.

```
./vendor/drupal/console/bin/drupal create:terms
./vendor/drupal/console/bin/drupal create:nodes
```

### Instalar y activar tema.

```
./vendor/drupal/console/bin/drupal theme:download bootstrap_barrio
drush theme:enable bootstrap_barrio
```

## Instalar tema basado en material design

`COMPOSER_MEMORY_LIMIT=-1 composer require drupal/material_base`

### Dependencias

`COMPOSER_MEMORY_LIMIT=-1 composer require drupal/block_class`

## Referencias

- https://github.com/geerlingguy/drupal-container
