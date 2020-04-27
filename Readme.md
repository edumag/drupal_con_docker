# Drupal8 con docker

## Iniciar 

```
docker-composer up
```

Abrir http://localhost:8010

Hacer la instalción manualmente.

## Entrar en contenedor.

`docker exec -it drupal8 bash`

## Instalar drupal console.

```
composer require drupal/console:~1.0 --prefer-dist --optimize-autoloader
curl https://drupalconsole.com/installer -L -o drupal.phar
mv drupal.phar /usr/local/bin/drupal
chmod +x /usr/local/bin/drupal
```

## Instalar drush.

```
composer require drush/drush
ln -s /var/www/html/vendor/drush/drush/drush /usr/local/bin/
```

## Console commands

```
cd web
drupal cache:rebuild
```
## Composer.

```
composer require drupal/devel
```

## Instalar módulos:

```
COMPOSER_MEMORY_LIMIT=-1 composer require drupal/devel
```

Añadimos COMPOSER_MEMORY_LIMIT para evitar problemas de memoria.

## Activar módulo

```
cd web/
drupal module:install devel
```

## Actualizar drupal

```
COMPOSER_MEMORY_LIMIT=-1 composer update
drush updatedb
drush cache:rebuild
```

## Crear contenido de prueba.

```
drupal create:terms
drupal create:nodes
```

## Instalar y activar tema.

```
drupal theme:download bootstrap_barrio
drush theme:enable bootstrap_barrio
```

## Referencias

- https://github.com/geerlingguy/drupal-container
