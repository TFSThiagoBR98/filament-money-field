# Filament Money Field
Money field powered by [Money PHP ](https://www.moneyphp.org/en/stable/).

This package gives much better localization support for money fields in Filament than most other packages. For example when it comes to currency symbols and decimal and thousand separators. Especially for more obscure currencies.

Example of a money field with Swedish localization. 
This package would give "1234.56 kr", while most other solutions probably would give you something like "SEK 1234.56" which is not the correct format for Sweden.

## Requirements

- PHP 8.2 or higher
- Filament 3.0 or higher
- [PHP Internationalization extension (intl) ](https://www.php.net/manual/en/intro.intl.php)
- The database column should be a integers with minor units (i.e. cents) and not a float (Floats should never be used for storing money).

## Installation

```bash
composer require pelmered/filament-money-field
```

**Optional: Set the default options for currency and locale so that you don't have to set them for every field.**

**Option 1 (Recommended): Put the default options in your .env file.**

```php
MONEY_DEFAULT_LOCALE=sv_SE
MONEY_DEFAULT_CURRENCY=SEK
```
**Option 2: Publish the config file and set the default options there.**
```bash
php artisan vendor:publish --provider="Pelmered\FilamentMoneyField\FilamentMoneyFieldServiceProvider" --tag="config"
```

## Usage

### InfoList

```php
use Pelmered\FilamentMoneyField\Infolists\Components\MoneyEntry;

MoneyEntry::make('price'); // Defaults to USD and the current Laravel locale

// The default can be set in the Infolist class with:
public static string $defaultCurrency = 'SEK';

MoneyEntry::make('price')
    ->currency('USD')
    ->locale('en_US');

MoneyEntry::make('price')
    ->currency('SEK')
    ->locale('sv_SE');
```

### Form

```php
use Filament\Forms\Components\MoneyField;

MoneyField::make('price'); // Defaults to USD and the current Laravel locale

MoneyField::make('price')
    ->currency('USD')
    ->locale('en_US');

MoneyField::make('price')
    ->currency('SEK')
    ->locale('sv_SE');
```

### Table column

```php
use Pelmered\FilamentMoneyField\Tables\Columns\MoneyColumn;

MoneyColumn::make('price'); // Defaults to USD and the current Laravel locale

MoneyColumn::make('price')
    ->currency('USD')
    ->locale('en_US');

MoneyColumn::make('price')
    ->currency('SEK')
    ->locale('sv_SE');
```
