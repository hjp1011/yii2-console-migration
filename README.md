
Yii2 uses Migration to back up and restore the database, adding other extended usage methods.

Notice：If you are using PHP7.2, then yII must use v2.0.15.1 or higher, because the yii2 core class Object conflicts with the PHP7.2 reserved class Object.

[![Latest Stable Version](http://poser.pugx.org/hjp1011/yii2-console-migration/v)](https://packagist.org/packages/hjp1011/yii2-console-migration) [![Total Downloads](http://poser.pugx.org/hjp1011/yii2-console-migration/downloads)](https://packagist.org/packages/hjp1011/yii2-console-migration) [![Latest Unstable Version](http://poser.pugx.org/hjp1011/yii2-console-migration/v/unstable)](https://packagist.org/packages/hjp1011/yii2-console-migration) [![License](http://poser.pugx.org/hjp1011/yii2-console-migration/license)](https://packagist.org/packages/hjp1011/yii2-console-migration) [![PHP Version Require](http://poser.pugx.org/hjp1011/yii2-console-migration/require/php)](https://packagist.org/packages/hjp1011/yii2-console-migration)

```php
use yii\base\Object // PHP7.1 and previous versions
use yii\base\BaseObject // PHP7.2
```

Yii2 uses Migration to back up and restore the database
===========================
Yii2 uses Migration to back up and restore databases. Initially, yii2 wanted to do a backup function on the command line, but later reorganized the classes to add other extended uses.
安装 Installation
------------

The preferred way to install this extension is through [composer] (http://getcomposer.org/download/).

Run

```
composer require hjp1011/yii2-console-migration "@dev"
```

Or add

```
"hjp1011/yii2-console-migration": "*"
```

To the corresponding location of the 'composer. Json' file.


Backup table in command line:
-----

in```console\config\main.php``` add  :

```php
'controllerMap' => [
    'migrate' => [
        'class' => 'yiiframe\migration\ConsoleController',
    ],
],
```

Use on the command line:
```
php ./yii migrate/backup all #Backup all tables
php ./yii migrate/backup table1,table2,table3... #Backup multiple tables
php ./yii migrate/backup table1 #Back up a table

php ./yii migrate/up #Restore all tables
```

Back up tables in the background:
-----
Add the following code to a background controller, such as PublicController:
```php
public function actions()
{
    return [
        'backup' => [
            'class' => 'yiiframe\migration\WebAction',
            'returnFormat' => 'json',
            'migrationPath' => '@console/migrations'
        ]
    ];
}
```
Send an Ajax request to```/admin/public/backup?tables=yii2_ad,yii2_admin```。

Other usage:
-----

For friends who want to do more extensions, you can inherit directly
```yiiframe\migration\components\MigrateCreate```

Or use the following code:
```php
$migrate = Yii::createObject([
        'class' => 'yiiframe\migration\components\MigrateCreate',
        'migrationPath' => $this->migrationPath
]);
$migrate->create($table);
```
