# PHP - OneSignal
Classe facilitar o uso do OneSignal para Push Notifications com PHP

## Baixando o projeto

```
    "repositories": [
        {
            "type":"package",
            "package": {
              "name": "webtouchbr/php-onesignal",
              "version":"master",
              "source": {
                  "url": "https://github.com/webtouchbr/php-onesignal.git",
                  "type": "git",
                  "reference":"master"
                }
            }
        }
    ],
    
    "require": {
        "webtouchbr/php-onesignal": "master",
        ...
    }
```

## Exemplos

Abaixo segue alguns exemplos de como usar a classe


### Cadastrando um Dispositivo
``` php
<?php
require_once(dirname(__FILE__).'/vendor/autoload.php');

use CWG\OneSignal\OneSignal;
use CWG\OneSignal\Device;

$appID = '92b9c6bb-89d2-4cbc-8862-a80e4e81a251';
$authorizationRestApiKey = 'MWRjMTg2MjEtNTBmYS00ODA4LWE1M2EtM2YyZjU5ZmRkNGQ5';

$api = new OneSignal($appID, $authorizationRestApiKey);

//Criando o Dispositivo
$retorno = $api->device->setLanguage('pt')
                ->setIdentifier('12312312313')
                ->setDevice(Device::ANDROID)
                ->addTag('matricula', '11111111')
                ->addTag('curso', '12312312')
                ->addTag('turma', '1111')
                ->create();


print_r($retorno);
``` 

### Alterando Dispositivo

``` php
<?php
require_once(dirname(__FILE__).'/vendor/autoload.php');

use CWG\OneSignal\OneSignal;
use CWG\OneSignal\Device;

$appID = '92b9c6bb-89d2-4cbc-8862-a80e4e81a251';
$authorizationRestApiKey = 'MWRjMTg2MjEtNTBmYS00ODA4LWE1M2EtM2YyZjU5ZmRkNGQ5';
$deviceID = '69aeecc1-7b58-44d1-8000-7767de437adf';

$api = new OneSignal($appID, $authorizationRestApiKey);

//Novas informações do Dispositivo
$retorno = $api->device->setLanguage('pt')
                ->setIdentifier('12312312313')
                ->setDevice(Device::ANDROID)
                ->addTag('matricula', '11')
                ->update($deviceID);


print_r($retorno);
```

### Enviando notificação para todos dispositivos

``` php
<?php
require_once(dirname(__FILE__).'/vendor/autoload.php');
use CWG\OneSignal\OneSignal;

$appID = '92b9c6bb-89d2-4cbc-8862-a80e4e81a251';
$authorizationRestApiKey = 'MWRjMTg2MjEtNTBmYS00ODA4LWE1M2EtM2YyZjU5ZmRkNGQ5';

$api = new OneSignal($appID, $authorizationRestApiKey);


//Enviando notificação para todo mundo
$retorno = $api->notification->setBody('Ola')
                            ->setTitle('Titulo')
                            ->send();
print_r($retorno);
```

### Enviando notificação baseado em tags

``` php
<?php
require_once(dirname(__FILE__).'/vendor/autoload.php');
use CWG\OneSignal\OneSignal;

$appID = '92b9c6bb-89d2-4cbc-8862-a80e4e81a251';
$authorizationRestApiKey = 'MWRjMTg2MjEtNTBmYS00ODA4LWE1M2EtM2YyZjU5ZmRkNGQ5';

$api = new OneSignal($appID, $authorizationRestApiKey);


//Enviando notificação para quem usa tag categorias esporte ou natação
$retorno = $api->notification->setBody('Ola')
                            ->setTitle('Titulo')
                            ->addTag('categoria', 'esporte')
                            ->addTag('categoria', 'natacao')
                            ->send();
print_r($retorno);
```

### Enviando notificação baseado no dispositivo
``` php
<?php
require_once(dirname(__FILE__).'/vendor/autoload.php');
use CWG\OneSignal\OneSignal;

$appID = '92b9c6bb-89d2-4cbc-8862-a80e4e81a251';
$authorizationRestApiKey = 'MWRjMTg2MjEtNTBmYS00ODA4LWE1M2EtM2YyZjU5ZmRkNGQ5';
$deviceID = '69aeecc1-7b58-44d1-8000-7767de437adf';
$api = new OneSignal($appID, $authorizationRestApiKey);


//Enviando notificação para um dispositivo
$retorno = $api->notification->setBody('Ola')
                            ->setTitle('Titulo')
                            ->addDevice($deviceID)
                            ->send();
``` 

---
**Autor:**  Carlos W. Gama *(carloswgama@gmail.com)*
**Licença:** MIT

Livre para usar, modificar como desejar e destribuir como quiser
