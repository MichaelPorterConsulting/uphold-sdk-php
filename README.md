# Bitreserve SDK for PHP
[![Latest Version](https://img.shields.io/packagist/v/seegno/bitreserve-sdk-php.svg)](https://packagist.org/packages/seegno/bitreserve-sdk-php)
[![Build Status](https://travis-ci.org/seegno/bitreserve-sdk-php.svg?branch=master)](https://travis-ci.org/seegno/bitreserve-sdk-php)
[![Code Climate](https://codeclimate.com/github/seegno/bitreserve-sdk-php/badges/gpa.svg)](https://codeclimate.com/github/seegno/bitreserve-sdk-php)
[![Test Coverage](https://codeclimate.com/github/seegno/bitreserve-sdk-php/badges/coverage.svg)](https://codeclimate.com/github/seegno/bitreserve-sdk-php)
[![License](https://img.shields.io/packagist/l/seegno/bitreserve-sdk-php.svg)](https://packagist.org/packages/seegno/bitreserve-sdk-php)

Bitreserve is a next generation money service business that shields you from bitcoin volatility by enabling you to hold bitcoin as the money you use every day.

The Bitreserve SDK for PHP provides an easy way for developers to integrate PHP applications with the [Bitreserve API](https://developers.bitreserve.org).

## Requirements

* PHP >= 5.4.4 with the [cURL](http://php.net/manual/en/book.curl.php) extension.
* [Guzzle](https://github.com/guzzle/guzzle) library.

## Installation

### Standalone

Grab the latest version of the library:

    $ git clone https://github.com/seegno/bitreserve-sdk-php.git

Install composer:

    $ curl -s https://getcomposer.org/installer | php

Install the library dependencies:

    $ php composer.phar install

Require the autoloader file generated by composer:

```php
require 'vendor/autoload.php';
```

### Integrating with another project using composer

Require the library package as a dependency:
```json
{
    "require": {
        "seegno/bitreserve-sdk-php": "1.1.*"
    }
}
```

## Basic usage

In order to learn more about the Bitreserve API, please check out the [developer website](https://developer.bitreserve.org/api/v0/#authentication).

First, create a Personal Access Token (PAT) using the command described below.

### Create a Personal Access Token

    $ php lib/Bitreserve/console.php tokens:create

Then, create a new instance of the `Client` class with token. Take a look at the following examples and explore more on the [examples](https://github.com/bitreserve/bitreserve-sdk-php/tree/master/examples) directory.

### Get authenticated user
```php
require_once 'vendor/autoload.php';

use \Bitreserve\BitreserveClient as Client;

// Initialize the client.
$client = new Client('AUTHORIZATION_TOKEN');

// Get the current user.
$user = $client->getUser();
```

### Create and commit a new transaction
```php
require_once 'vendor/autoload.php';

use \Bitreserve\BitreserveClient as Client;

// Initialize the client.
$client = new Client('AUTHORIZATION_TOKEN');

// Get the current user.
$user = $client->getUser();

// Get a specific card by id.
$card = $user->getCardsById('ade869d8-7913-4f67-bb4d-72719f0a2be0');

// Create a new transaction.
$transaction = $card->createTransaction('foo@bar.com', '2.0', 'BTC');

// Commit the transaction.
$transaction->commit();
```

### Get all public transactions
```php
require_once 'vendor/autoload.php';

use \Bitreserve\BitreserveClient as Client;

// Initialize the client. In this case, we don't need an
// AUTHORIZATION_TOKEN because the Ticker endpoint is public.
$client = new Client();

// Get all public transactions.
$transactions = $client->getReserve()->getTransactions();
```

Or you could get a specific public transaction:

```php
// Get one public transaction.
$transaction = $client->getReserve()->getTransactionById('a97bb994-6e24-4a89-b653-e0a6d0bcf634');
```

### Get reserve status
```php
require_once 'vendor/autoload.php';

use \Bitreserve\BitreserveClient as Client;

// Initialize the client. In this case, we don't need an
// AUTHORIZATION_TOKEN because the Ticker endpoint is public.
$client = new Client();

// Get the reserve summary of all the obligations and assets within it.
$statistics = $client->getReserve()->getStatistics();
```

## Contributing & Development

#### Contributing

Found a bug or want to suggest something? Take a look first on the current and closed [issues](https://github.com/seegno/bitreserve-sdk-php/issues). If it is something new, please [submit an issue](https://github.com/seegno/bitreserve-sdk-php/issues/new).

#### Develop

It will be awesome if you can help us evolve `bitreserve-sdk-php`. Want to help?

1. [Fork it](https://github.com/seegno/bitreserve-sdk-php).
2. `php composer.phar install`.
3. Hack away.
4. Run the tests: `phpunit`.
5. Create a [Pull Request](https://github.com/seegno/bitreserve-sdk-php/compare).
