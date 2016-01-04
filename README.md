# Mongo PHP Adapter

The Mongo PHP Adapter is a userland library designed to act as an adapter 
between applications relying on ext-mongo and the new driver (ext-mongodb).

It provides the API of ext-mongo built on top of mongo-php-library, thus being
compatible with PHP7.

# Stability

This library is not yet stable enough to be used in production. Use at your own
risk.

# Installation

This library requires you to have the mongodb extension installed and conflicts
with the legacy mongo extension.

The preferred method of installing this library is with
[Composer](https://getcomposer.org/) by running the following from your project
root:

    $ composer require "alcaeus/mongo-php-adapter=dev-master"

# Known issues

## [Mongo](https://secure.php.net/manual/en/class.mongo.php)

 - The Mongo class is deprecated and was not implemented in this library. If you
 are still using it please update your code to use the new classes.

## MongoClient

 - The [MongoClient::connect](https://php.net/manual/de/mongoclient.connect.php)
 and [MongoClient::close](https://secure.php.net/manual/de/mongoclient.close.php)
 methods are not implemented because the underlying driver connects lazily and
 does not offer methods for connecting disconnecting.
 - The [MongoClient::getConnections](https://secure.php.net/manual/de/mongoclient.getconnections.php)
 method is not implemented because the underlying driver does not offer a method
 to retrieve this data.
 - The [MongoClient::killCursor](https://php.net/manual/de/mongoclient.killcursor.php)
 method is not yet implemented.

## MongoDB
 - The `includeSystemCollections` parameter used in the [MongoDB::getCollectionInfo](https://php.net/manual/de/mongodb.getcollectioninfo.php]),
 [MongoDB::getCollectionNames](https://php.net/manual/de/mongodb.getcollectionnames.php]),
 and [MongoDB::listCollections](https://php.net/manual/de/mongodb.listcollections.php)
 methods is ignored. These methods do not return information about system
 collections.
 - The [MongoDB::repair](https://secure.php.net/manual/de/mongodb.repair.php)
 method is not yet implemented.
 - The [MongoDB::authenticate](https://secure.php.net/manual/de/mongodb.authenticate.php)
 method is not yet implemented.

## MongoCollection

 - The [MongoCollection::createIndex](https://secure.php.net/manual/de/mongocollection.createindex.php)
 method does not yet return the same result as the original method. Instead, it
 always returns the name of the index created.

## Types

 - Return values containing objects of the [MongoDB\BSON\Javascript](https://secure.php.net/manual/de/class.mongodb-bson-javascript.php)
 class cannot be converted to full [MongoCode](https://secure.php.net/manual/de/class.mongocode.php)
 objects because there are no accessors for the code and scope properties.
