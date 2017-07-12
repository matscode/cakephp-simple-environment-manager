## CakePHP Simple Environment Manager
Basically Loads and/or overrides configuration file depending on your environment file. Its basically the conventional cakePHP `bootstrap.php` file that was extended
<br>
Environment options supported are;
- development
- local (for if you are developing locally on your machine)
- production (This is recommended for your live configuration overrides)
theres an additional directory created in `config/` that has these environment names. you can create em if it does not exist.

### Usage
Replace your current `bootstrap.php` with the one in this repo.

#### - Step 1
Set your environment on line `91`
``` php
define( 'ENVIRONMENT', 'local' );
```

#### - Step 2
Open the `bootstrap.php` file - `line 96` , add your configurations file names.
<br>
Configuration file names should be without path or `.php` ext
``` php
$configFiles =
        [
            'defaults'  => // this are your original configurations files
                [
                    'app'
                ],
            'overrides' => // this are your environment based configuration to override specific values from the original configuration file
                [
                    // 'app' // you might need to create this first in the desired environment dir
                ]
        ];
```
##### Example Override

Creates a file named `app.php` inside `config/local/` with the following content

``` php
// config/local/app.php
// value to override in default cake app.php file
return
[
    'debug'          => filter_var( env( 'DEBUG', true ), FILTER_VALIDATE_BOOLEAN ), // the debug can be set to false in your defaul app.php file
    'defaultsdfdsf'  => [
				'className'        => 'Cake\Database\Connection',
				'driver'           => 'Cake\Database\Driver\Mysql',
				'persistent'       => false,
				'host'             => 'localhost',
				//'port' => 'non_standard_port_number',
				'username'         => 'root',
				'password'         => '',
				'database'         => 'local_test_db',
				'encoding'         => 'utf8',
				'timezone'         => 'UTC',
				'cacheMetadata'    => true,
				'quoteIdentifiers' => false,
				'log'              => false,
				//'init' => ['SET GLOBAL innodb_stats_on_metadata = 0'],
				'url'              => env( 'DATABASE_TEST_URL', null ),
			]
]
```
Add the file to `$configFiles['overrides']` array.
<br>
**PS**: You can override any of your default configurations with your overrides. [Read more](https://book.cakephp.org/3.0/en/development/configuration.html#Cake\Core\Configure) on cake configurations.
``` php
$configFiles =
        [
            'defaults'  =>
                [
                    'app'
                ],
            'overrides' => 
                [
                    'app'
                ]
        ];
```

### - Step 3
LOL, Just kidding, thats all that neccesary. Neither do I like stressful implementation. Have a wonderful time coding

### Reccomentation
I would advice you add the content of the `.gitignore` file to your. So whenever you push (probably continous deployment), you are sure as h*ll not gonna push your unwanted overrides in production with. That way, atleast you get an error message saying one of your override file can not be loaded.

#### License
- GNU GPLV3