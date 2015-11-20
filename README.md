# Openpay Server PHP - Laravel

Implementación de los servicios de Openpay 

##Instalación

Ejecutar el siguiente comando

```console
composer require gozozo/openpay-server
```
Después agregar la siguiente línea  en **`provider`** en el archivo que se encuentra en **`config/app.php`** del proyecto

```php
Gozozo\OpenpayServer\OpenpayServerServiceProvider::class,
```

y luego ejecutamos los siguintes dos comandos en la terminal
```console
php artisan vendor:publish --provider="Gozozo\OpenpayServer\OpenpayServerServiceProvider"
php artisan migrate
```

##Configuración de .env
Es necesario agregar las siguientes configuraciones en el archivo **.env** del proyecto de **Laravel**

###Configurar middleware 

Permite una autenticación antes de acceder a las rutas de openpay
```
OPENPAY_MIDDLEWARE=<Nombre_middleware>
```
###Llaves del API de Openpay

Configuración de las llaves 
```txt
OPENPAY_ID = <Id_de_pruebas>
OPENPAY_SK = <Llave_privada_pruebas>
OPENPAY_ID_PRODUCTION = <Id_producción>
OPENPAY_SK_PRODUCTION = <Llave_privada_producción>
```

###Tabla de referencia

Relación de la tabla de referencia openpay con tu tabla de usuarios. Dejar sin datos si no se desea relación
```txt
OPENPAY_TABLE = <Tabla_usuario>
OPENPAY_REFERENCE = <Id_tabla_usuario>
```

##Activar modo producción 

Es necesario asignar a la variable de `APP_ENV`  que se encuentra en nuestro archivo **.env** a **production**
```txt
APP_ENV = production
```

