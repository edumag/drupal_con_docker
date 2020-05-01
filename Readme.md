# Entorno desarrollo drupal con docker

## Iniciar 

`./run`

o

`docker-composer up`

Abrir http://localhost:8010

### Entrar en contenedor.

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

### Instalación del proyecto

`drush site:install`

### Referencias

- https://github.com/geerlingguy/drupal-container

## Ejemplo de comandos que nos ayudarán en el desarrollo.

### Estado de las actualizaciones

`./vendor/drush/drush/drush updatedb:status`

### Borrar cache

```
./vendor/drupal/console/bin/drupal cache:rebuild
```

### Instalar módulo devel

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
./vendor/drush/drush/drush updatedb
./vendor/drush/drush/drush cache:rebuild
```

### Crear contenido de prueba.

```
./vendor/drupal/console/bin/drupal create:terms
./vendor/drupal/console/bin/drupal create:nodes
```

### Instalar y activar tema con drupal console.

```
./vendor/drupal/console/bin/drupal theme:download bootstrap_barrio
./vendor/drush/drush/drush theme:enable bootstrap_barrio
```

### Instalar tema con composer

`COMPOSER_MEMORY_LIMIT=-1 composer require drupal/material_base`



## Crear tema hijo basado en el tema Barrio

```bash
./vendor/drupal/console/bin/drupal theme:download bootstrap_barrio
./vendor/drush/drush/drush theme:enable bootstrap_barrio
mkdir themes/custom
cp -R themes/contrib/bootstrap_barrio/subtheme/ themes/custom/
cd themes/custom
mv subtheme $TEMA_PROPIO
cd $TEMA_PROPIO
# Renombrar ficheros
rename 's/bootstrap_barrio_subtheme/$TEMA_PROPIO/g' * */* */*/*
# Renombrar referencias del código.
sed -i -e 's/bootstrap_barrio_subtheme/$TEMA_PROPIO/g' * */* */*/*
# Nombre del tema.
sed -i -e 's/Bootstrap Barrio Subtheme/Temapropio/g' *.info.yml
```



### Referencias

- https://github.com/geerlingguy/drupal-container
- [Crear y configurar tema hijo del tema Barrio](https://www.youtube.com/watch?v=D5A_aFdlWEs)

