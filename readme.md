<p align="center">
    <a href="https://www.awes.io/?utm_source=github&utm_medium=repository" target="_blank" rel="noopener noreferrer">
        <img width="100" src="https://static.awes.io/promo/Logo_sign_color.svg" alt="Awes.io logo">
    </a>
</p>

<h1 align="center">Localization Helper</h1>

<p align="center">Package for convenient work with Laravel's localization features and fast language files generation.</p>

<p align="center">
    <a href="https://www.awes.io/?utm_source=github&amp;utm_medium=shields">
        <img src="https://repo.pkgkit.com/4GBWO/awes-io/localization-helper/badges/master/coverage.svg" alt="Coverage report" >
    </a>
    <a href="https://www.awes.io/?utm_source=github&amp;utm_medium=shields">
        <img src="https://www.pkgkit.com/4GBWO/awes-io/localization-helper/version.svg" alt="Last version" >
    </a>
    <a href="https://www.awes.io/?utm_source=github&amp;utm_medium=shields">
        <img src="https://repo.pkgkit.com/4GBWO/awes-io/localization-helper/badges/master/build.svg" alt="Build status" >
    </a>
    <a href="https://www.awes.io/?utm_source=github&amp;utm_medium=shields">
        <img src="https://www.pkgkit.com/4GBWO/awes-io/localization-helper/downloads.svg" alt="Downloads" >
    </a>
    <a href="https://www.awes.io/?utm_source=github&amp;utm_medium=shields">
        <img src="https://img.shields.io/github/license/awes-io/localization-helper.svg" alt="License" />
    </a>
    <a href="https://www.awes.io/?utm_source=github&amp;utm_medium=shields">
        <img src="https://www.pkgkit.com/4GBWO/awes-io/localization-helper/status.svg" alt="CDN Ready" /> 
    </a>
    <a href="https://www.awes.io/?utm_source=github&amp;utm_medium=shields" target="_blank">
        <img src="https://static.pkgkit.com/badges/laravel.svg" alt="laravel" />
    </a>
    <a href="https://www.awes.io/?utm_source=github&amp;utm_medium=shields">
        <img src="https://img.shields.io/github/last-commit/awes-io/localization-helper.svg" alt="Last commit" />
    </a>
    <a href="https://github.com/awes-io/awes-io">
        <img src="https://ga-beacon.appspot.com/UA-134431636-1/awes-io/repository" alt="Analytics" />
    </a>
    <a href="https://www.pkgkit.com/?utm_source=github&amp;utm_medium=shields">
        <img src="https://www.pkgkit.com/badges/hosted.svg" alt="Hosted by Package Kit" />
    </a>
    <a href="https://www.patreon.com/join/awesdotio">
        <img src="https://static.pkgkit.com/badges/patreon.svg" alt="Patreon" />
    </a>
</p>

##
<p align="center">
    <img src="https://static.awes.io/github/localization-helper.gif" alt="Localization Helper" />
</p>

## Installation

Via Composer

``` bash
$ composer require awes-io/localization-helper
```

In Laravel 5.5+, service provider and facade will be automatically registered. For older versions, follow the steps below:

Register service provider in `config/app.php`:

```php
'providers' => [
// [...]
        AwesIO\LocalizationHelper\LocalizationHelperServiceProvider::class,
],
```

You may also register `LaravelLocalization` facade:

```php
'aliases' => [
// [...]
        'LocalizationHelper' => AwesIO\LocalizationHelper\Facades\LocalizationHelper::class,
],
```

## Config

### Config Files

In order to edit default configuration you may execute:

```
php artisan vendor:publish --provider="AwesIO\LocalizationHelper\LocalizationHelperServiceProvider"
```

After that, `config/localizationhelper.php` will be created.

## Usage

<p align="center">
    <img src="https://static.awes.io/github/localization-helper.png" alt="Localization Helper" />
</p>

Package registers global helper function `_p($file_key, $default, $placeholders)`:

```php
_p('auth.login', 'Login'); // "Login"
```

It will create new localization file `auth.php` (if it doesn't exist) and write second parameter as language string under `login` key:

```php
return [
    "login" => "Login"
];
```

On second call with same file/key `_p('auth.login')`, localization string will be returned, file will remain untouched.

Placeholders are also supported:

```php
_p(
    'mail.invitation', 
    'You’re invited to join :company company workspace', 
    ['company' => 'Awesio']
);
```

If key is returned, it means that string already exists in localization file and you are trying to add new one using its value as an array.

```php
// in localization file.php
return [
    "test" => "Test string"
];

_p('file.test.new', 'Test string'); // will return "file.test.new"

_p('file.test_2.new', 'Test string'); // will return "Test string"

// and modify localization file:
return [
    "test" => "Test string",
    "test_2" => [
        "new" => "Test string"
    ]
];
```

## Change log

Please see the [changelog](changelog.md) for more information on what has changed recently.


## Testing

The coverage of the package is <a href="https://www.awes.io/?utm_source=github&amp;utm_medium=shields"><img src="https://repo.pkgkit.com/4GBWO/awes-io/localization-helper/badges/master/coverage.svg" alt="Coverage report"></a>.
                                   
You can run the tests with:

```bash
composer test
```

## Contributing

Please see [contributing.md](contributing.md) for details and a todolist.

## Credits

- [Galymzhan Begimov](https://github.com/begimov)
- [All Contributors](contributing.md)

## License

[MIT](http://opensource.org/licenses/MIT)