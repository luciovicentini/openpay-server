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

# Rutas

### Clientes

|   Tipo   |  Ruta  |     Descripción     |  Observaciones  |  Ejemplo  |
|  :----:  |  :---- |  :--------------:   |      :----:     |  :----:   |
|   POST   | openpay/customer | Crea un nuevo cliente | **Parameters** lleva el json de información del cliente:  ```[parameters] = <``` [Json nuevo cliente Openpay]  ```>``` | **url :** ` http://ejemplo.com/openpay/customer/` **datos :** `"{"external_id" : "","name" : "customer name","last_name" : "","email" : "customer_email@me.com","requires_account" : false,"phone_number" : "44209087654","address" : {"line1" : "Calle 10","line2" : "col. san pablo","line3" : "entre la calle 1 y la 2","state" : "Queretaro","city" : "Queretaro","postal_code" : "76000","country_code" : "MX"}}"` |
|  DELETE  | openpay/customer/{id_user} | Elimina al cliente | - | **url :** ` http://ejemplo.com/openpay/customer/1 ` |

### Tarjetas de un cliente

|  Tipo  |  Ruta  |     Descripción     |  Observaciones  |   Ejemplo   |
| :----: |  :---- |  :--------------:   |      :----:     |   :----:    |
|  POST  | openpay/customer/{id_user}/card | Guarda una nueve tarjeta al cliente | **Parameters** lleva el json de información del tarjeta:  ```[parameters] = <``` [Json nueva tarjeta]  ```>``` | **url :** ` http://ejemplo.com/openpay/customer/1/card `  **datos :** `"{"card_number":"4111111111111111","holder_name":"Juan Perez Ramirez","expiration_year":"20","expiration_month":"12","cvv2":"110"}"` |
|   GET  | openpay/customer/{id_user}/card | Regresa todas las tarjetas de un cliente  | - | **url :** ` http://ejemplo.com/openpay/customer/1/card ` |
| DELETE | openpay/customer/{id_user}/card/{id_card} | Elimina tarjeta del cliente | - |  **url :** ` http://ejemplo.com/openpay/customer/1/card/aarwcowd2iuaxfsv5c70 ` |

### Cargo con id tarjeta de un cliente

|  Tipo  |  Ruta  |     Descripción     |  Observaciones  |  Ejemplo  |
| :----: |  :---- |  :--------------:   |     :----:      |  :----:   |
|  POST  | openpay/customer/{id_user}/card/{id_card}/charge | Crea un cargo a tarjeta ya guardada | **Parameters** lleva el json de información del cargo:  ```[parameters] = <``` [Json nuevo cargo]  ```>``` | **url :** ` http://ejemplo.com/openpay/customer/1/card/kqgykn96i7bcs1wwhvgw/charge `  **datos :** `"{"source_id" : "kqgykn96i7bcs1wwhvgw","method" : "card","amount" : 100,"currency" : "MXN","description" : "Cargo inicial a mi cuenta","order_id" : "oid-00051","device_session_id" : "kR1MiQhz2otdIuUlQkbEyitIqVMiI16f"}"` |

[Json nuevo cliente Openpay]:<http://www.openpay.mx/docs/api/?php#crear-un-nuevo-cliente>
[Json nueva tarjeta]:<http://www.openpay.mx/docs/api/?php#crear-una-tarjeta>
[Json nuevo cargo]:<http://www.openpay.mx/docs/api/?php#con-id-de-tarjeta-o-token>