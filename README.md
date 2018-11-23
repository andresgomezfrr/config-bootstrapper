[![CircleCI](https://circleci.com/gh/wizzie-io/config-bootstrapper/tree/master.svg?style=svg)](https://circleci.com/gh/wizzie-io/config-bootstrapper/tree/master)
[![Maintainability](https://api.codeclimate.com/v1/badges/5b66393cb45c21f4ad0b/maintainability)](https://codeclimate.com/github/wizzie-io/config-bootstrapper/maintainability)
[![GitHub release](https://img.shields.io/github/release/wizzie-io/config-bootstrapper.svg)](https://github.com/wizzie-io/config-bootstrapper/releases/latest)
[![Maven Central](https://maven-badges.herokuapp.com/maven-central/io.wizzie/config-bootstrapper/badge.svg)](https://maven-badges.herokuapp.com/maven-central/io.wizzie/config-bootstrapper)
[![wizzie-io](https://img.shields.io/badge/powered%20by-wizzie.io-F68D2E.svg)](https://github.com/wizzie-io/)

# Config Bootstrapper Library

The config bootstrapper is a library that allows us to load configuration from different sources: kafka, filesystem or other datastore. Depends on the source the library can load the last configuration and offer it to the user application or also it can load the new configuration, for example via Kafka.

Currently, the library has two bootstrapper:

### DummyBootstrapper

`io.wizzie.bootstrapper.bootstrappers.impl.DummyBootstrapper`

The DummyBootstrapper does nothing. It is only used to load base config file, but it doesn't load bootstrapping config.

### FileBootstrapper

`io.wizzie.bootstrapper.bootstrappers.impl.FileBootstrapper`

The FileBootstrapper loads a configuration from file into the filesystem. This boostrapper only loads the configuration one time at the startup.

| Property     | Description     | 
| :------------- | :-------------  | 
| `file.bootstrapper.path`      | Stream config file path      |


### KafkaBootstrapper 

`io.wizzie.bootstrapper.bootstrappers.impl.KafkaBootstrapper`

The KafkaBootstrapper loads a configuration from kafka topic. This bootstrapper can subscribe to kafka topic to load new configuration at runtime, it identifies the configuration using the `application.id`, this property must be equal to the kafka key into the message, and the kafka value is the configuration.

| Property     | Description     | 
| :------------- | :-------------  | 
| `bootstrap.kafka.topics`      | Topics that are used to read the bootstrapper configuration      |
| `application.id`      | The app id to identify the client configuration      |
| `bootstrap.servers`      | The kafka broker to read the bootstrapper configuration      |

### KafkaNoFilterBootstrapper 

`io.wizzie.bootstrapper.bootstrappers.impl.KafkaNoFilterBootstrapper`

The KafkaNoFilterBootstrapper loads a configuration from kafka topic. This bootstrapper can subscribe to kafka topic to load new configuration at runtime. It loads all configurations inside bootstrapper topics. It passes the source topic, source key, and source value with configuration.

| Property     | Description     | 
| :------------- | :-------------  | 
| `bootstrap.kafka.topics`      | Topics that are used to read the bootstrapper configuration      |
| `bootstrap.servers`      | The kafka broker to read the bootstrapper configuration      |
