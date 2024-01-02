# Pairs Library Documentation

The Pairs library is a PHP tool designed to efficiently store and retrieve key-value pairs in a database. It provides a simple and flexible interface for managing data in a relational database. Below is a comprehensive guide on how to use the library.

# Dedication

This library was initially a part of [User Synthetics](https://github.com/ucscode/user-synthetics) project but was extracted to become a standalone project. 

## Table of Contents

- [Introduction](#introduction)
- [Features](#features)
- [Requirements](#requirements)
- [Installation](#installation)
- [Usage](#usage)
  - [Initialization](#initialization)
  - [Set a Key-Value Pair](#set-a-key-value-pair)
  - [Retrieve a Value](#retrieve-a-value)
  - [Remove a Key-Value Pair](#remove-a-key-value-pair)
  - [Get All Pairs](#get-all-pairs)
  - [Get Pairs by Reference](#get-pairs-by-reference)
  - [Get Pairs by Key Pattern](#get-pairs-by-key-pattern)
  - [Foreign Constraints](#foreign-constraints)
- [Contributing](#contributing)
- [License](#license)

## Introduction

The Pairs class allows you to create a meta table that consists of key-value pairs. Each row in the table represents a unique combination of key and reference ID, allowing you to store and retrieve data in a flexible and efficient manner. The class also supports linking the meta table to a parent table using foreign keys for data integrity and consistency.

## Features

- Create a meta table with key-value pairs
- Link the meta table to a parent table using foreign keys
- Add or update reference data based on key and reference ID
- Retrieve reference data based on key and reference ID
- Remove reference data based on key and reference ID
- Retrieve all data associated with a specific reference ID or matching a given pattern
- Utilizes the sQuery library for efficient SQL query generation.

## Requirements

- PHP 8.1 or higher
- MySQLi extension
- [sQuery](https://github.com/ucscode/squery) library (required for efficient query generation)

## Installation

```bash
composer require ucscode/pairs
```

## Usage

### Initialization

```php
use Ucscode\Pairs\Pairs;

// Include the necessary files and create a mysqli connection
$mysqli = new mysqli("host", "username", "password", "database");

// Initialize the Pairs class
$pairs = new Pairs($mysqli, 'tablename');
```

### Set a Key-Value Pair

```php
$pairs->set('car', 'toyota', 2);
```

This sets the key "car" with the value "toyota" for the reference (owner) 2.

### Retrieve a Value

```php
$value = $pairs->get('car', 2);
```

This retrieves the value for the key "car" and reference 2.

### Remove a Key-Value Pair

```php
$pairs->remove('car', 2);
```

This removes the key-value pair for the key "car" and reference 2.

### Get All Pairs

```php
$allPairs = $pairs->getSequence();
```

This retrieves all available data grouped by reference.

### Get Pairs by Reference

```php
$pairsByReference = $pairs->getSequence(2);
```

This retrieves all data for reference 2.

### Get Pairs by Key Pattern

```php
$pairsByKeyPattern = $pairs->getSequence(2, 'user-%');
```

This retrieves all data for reference 2 whose key matches words starting from "user-"

### Foreign Constraints

```php
$foreignConstraint = new ForeignConstraint('parentTableName');
$foreignConstraint->describePrimaryKeyUnsigned(true);
$foreignConstraint->describePrimaryKeyNullable(false);
$foreignConstraint->describePrimaryKeyColumnName('id');
$pairs->setForeignConstraint($foreignConstraint);
```

This sets up a `foreign constraint` where "`parentTableName`" becomes the parent table, and the pairs table becomes the child.

## Contributing

Contributions are welcome! If you find any issues or have suggestions for improvements, please open an [issue](https://github.com/ucscode/Pairs/issues) or submit a [pull request](https://github.com/ucscode/Pairs/pulls) on the GitHub repository.

## License

This project is licensed under the MIT License. See the [LICENSE](https://opensource.org/license/mit/) file for more information.