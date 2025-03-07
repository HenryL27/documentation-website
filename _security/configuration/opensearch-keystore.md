---
layout: default
title: OpenSearch keystore
parent: Configuration
nav_order: 50
---

# OpenSearch keystore

`opensearch-keystore` is a utility script used to manage an OpenSearch keystore. An OpenSearch keystore provides a secure method of storing sensitive information, such as passwords and keys, used in an OpenSearch cluster. The script allows you to securely create, list, add, and remove settings. It is included in the OpenSearch distribution. 

## Usage

In order to use the `opensearch-keystore` script, you must have access to the file system containing the OpenSearch installation and the ability to execute OpenSearch scripts.

To use `opensearch-keystore`, open a terminal and use the following command syntax:

```
opensearch-keystore [command] [options]
```
{% include copy.html %}

## Commands

The `opensearch-keystore` script supports the following the commands: 

- `create`: Initializes a new keystore. If a keystore already exists, this command will overwrite the existing keystore.
- `list`: Lists all settings in the keystore.
- `add <setting-name>`: Adds a new setting to the current keystore. When a new setting is added, the script prompts you for the value of that setting. After adding the setting and value, both are securely stored in the keystore.
- `add-file <file-name>`: Adds a new file to the keystore.
- `remove <setting-name>`: Removes an existing setting from the keystore.
- `upgrade <setting-name>`: Upgrades an existing setting in the keystore.
- `passwd`: Sets a password for the keystore.
- `has-passwd`: Prints whether the keystore is password protected.
- `help`: Displays help information about all `opensearch-keystore` commands.

## Options

You can append each command with the following options:

- `-h, --help`: Displays help information about the script and its options.
- `-s, --silent`: Provides minimal output when the script responds to a command.
- `-v, --verbose`: Provides a verbose output for debugging purposes.

## Examples

The following examples provide the basic syntax for common `opensearch-keystore` commands:

### Creating a new keystore

**Command**

```bash
./bin/opensearch-keystore create
```
{% include copy.html %}

If a keystore already exists, the script will ask whether you would like to overwrite the existing keystore.
   
**Response**

The script responds with a confirmation that the keystore was created:
   
```bash
Created opensearch keystore in $OPENSEARCH_HOME/config/opensearch.keystore
```

### Listing settings in the keystore

**Command**
   
```bash
./bin/opensearch-keystore list
```
{% include copy.html %}

**Response**

The script responds with a list of settings in the keystore:

```bash
keystore.seed
plugins.security.ssl.http.pemkey_password_secure
```

### Adding a new setting

```bash
./bin/opensearch-keystore add plugins.security.ssl.http.pemkey_password_secure
```
{% include copy.html %}

**Response**

After this command, you will be prompted to enter the secret key securely.

### Removing a setting

**Command**

```bash
./bin/opensearch-keystore remove plugins.security.ssl.http.pemkey_password_secure
```
{% include copy.html %}

**Response**

No response exists for this command. To confirm that the setting was deleted, use `opensearch-keystore list`.

## Referring to keystore entries

After a setting has been added to a keystore, you can refer back to that setting in your OpenSearch configuration. To refer back to the setting, add the keystore setting name as a placeholder in the `opensearch.yml` configuration file, as shown in the following example:

```bash
plugins.security.ssl.http.pemkey_password_secure: ${plugins.security.ssl.http.pemkey_password_secure}
```
