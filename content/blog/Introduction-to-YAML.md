---
title: "Introduction to YAML"
date: 2022-01-12T15:51:50+05:30
draft: false
---

# What is YAML?

[YAML](https://yaml.org/) is a very popular data serialization language like [JSON](https://www.json.org/json-en.html) or [XML](https://www.xml.com/) for writing configuration files. YAML is used with many DevOps tools and applications such as [Docker](https://www.docker.com/), [Kubernetes](https://kubernetes.io/) etc.

YAML stands for **YAML Ain't Markup Language** and YAML files have either `.yaml` or `.yml` as their extension.

### What does serialization languages do?

Serialization languages facilitate different applications written in a variety of technologies and programming langauges to transfer data using a common, agreed on and standard format such as YAML.

[YAML](https://yaml.org/), [JSON](https://www.json.org/json-en.html) and [XML](https://www.xml.com/) are the most popular serialization languages

## Why learn YAML? How does it compare to JSON and XML?

YAML is the most human readable and intuitive format when compared to alternatives and hence, is a great fit for writing configurations of almost all the mordern DevOps tools such as [Docker compose](https://docs.docker.com/compose/) files, [Ansible](https://www.ansible.com/), [Prometheus](https://prometheus.io/), [Kubernetes](https://kubernetes.io/) and many more.

Let us look at the differences between YAML, JSON and XML:

### YAML

A simple config in YAML would look something like this:
```YAML
microservices:
  - app: user-authentication
    port: 8000
    version: 1.0
```
- Note that there are no special characters to define data structures.
- YAML uses line seperation and space identation for defining the structure of data.

### XML

The same configuration in XML would look like this:
```XML
<microservices>
  <microservices>
    <app>user-authentication</app>
    <port>8000</port>
    <version>1.0</version>
  </microservices>
</microservices>
```
Note that here we are using tags (`<> </>`) to define data structure.

### JSON

The same configuration in JSOn would look like this:
```JSON
{
  microservices: [
    {
      app: "user-authentication"
      port: 8000
      version: "1.0"
    }
  ]
}
```
Note that here, we are using curly braces (`{}`) to define data structure.

**NOTE: YAML is a superset of JSON i.e any valid JSON file is also a valid YAML file.**

<br>

# YAML Syntax

YAML consists of a number of components such as key-value pairs, objects, lists etc. which helps us structure the data as needed. 

Let's go through them one by one:

## Key-value pairs

```YAML
app: user-authentication
port: 8000
version: 1.7
```
- In the above example `app: user-authentication` or `port: 8000` are called key-value pairs.
- **Note** that `user-authentication` in the above example is a String, we don't need to to include Strings in `"` unless we're using special characters such as a newline in which case we'll have to write this key-value pair as `app: "user-authentication \n"`

<hr>

## Comments

```YAML
# This is a comment
app: user-authentication
port: 8000
# This is an another comment
version: 1.7
```
- We can write comments in YAML using `#`
- Adding comments is always considered a good practice to make the config more easily readable and human understandable.

<hr>

## Objects

```YAML
microservice:
  app: user-authentication
  port: 8000
  version: 1.7
```
- We can group multiple key-value pairs inside of an object.
- In the above example we have the object `microservice`

**NOTE:<br>Always take care of the spaces and identation while writing YAML. There are many code editor extensions and websites which can help with YAML validation.**

<hr>

## Lists

```YAML
microservice:
  - app: user-authentication
    port: 8000
    version: 1.7
  - app: user-data
    port: 9000
    version: 2.0
  - app: user-name
    port: 7000
    version: ["1.0", 2.0, 3.0, "latest"]    
    
microservices:
  - user-authentication
  - user-data
  - user-name
```
- As shown above, we can create lists using `-`
- Lists helps us organize data when we have multiple key-value pairs under one object or multiple values under one key.
- We can also create nested lists as shown in the example below:

```YAML
microservice:
  - app: user-authentication
    port: 8000
    version: 1.7
  - app: user-data
    port: 9000
    version:                # nested list
      - 1.0
      - 2.0
      - 3.0
  - app: user-name
    port: 7000
    version: 1.8
```
- Lists can also be created using this syntax:

```YAML
microservice:
  - app: user-authentication
    port: 8000
    version: [1.7, 1.8, 1.9, "version"]     # another syntax for lists
  - app: user-data
    port: 9000
    version: 2.0
```
<hr>

## Booleans

YAML accepts `true/false`, `yes/no` and `on/off` as boolean data.

```YAML
microservice:
  app: user-authentication
  port: 8000
  version: 1.7
  deployed1: true # boolean true/false
  deployed2: yes  # boolean yes/no
  deployed3: on   # boolean on/off
```

<hr>

## Multi-line Strings

```YAML
multilineString: |
  this is a multiline string
  and this is the next line
  next line
  etc
  
singlelineString: >
  this is a single line string,
  All three lines
  should be in the same line.
```

- As shown in above example, We can use `|` to display each line of string data type as a newline
- Similarly, we can use `>` if we want a single line string but don;t want to write it as a single line in our config file to make it more human readable.

<hr>

## Some things to note

### Accessing Environment Variables:

We can access environment variable in YAML using `$<env varibale>`

```YAML
command:
  - /bin/sh
  - -ec
  - >-
  mysql  -h 127.0.0.1 -u root -p$MYSQL_ROOT_PASSWORD -e 'SELECT 1'
```
In the above example, we are using the env variable `MYSQL_ROOT_PASSWORD`

### Placeholders:

- We can use placeholders in YAML using double curly braces `{{value}}`
- For eg: We need this in [Helm](https://helm.sh/) and [Ansible](https://www.ansible.com/) where placeholder value gets replaced using template generator.

### Multiple YAML Documents:

- We can separate different YAML configs using `---`
- This comes very handy in [Kubernetes](https://kubernetes.io/) where we have multiple components in one service and we want to group them in single YAML file.

```
apiVersion: v1
kind: configMap
metadata
  name: config-file
  
---

apiVersion: v1
kind: configMap
metadata
  name: config-file
```

**Note that we can write Kubernetes configuration files in both YAML and JSON format but YAML is more commonly used as it is cleaner and more readable**

<br>

# Thank you so much for reading 💖

Hope you liked this blog on YAML. If you find any mistakes or inaccuracies, please inform me on social or by [filing an issue](https://github.com/anubha-v-ardhan/anubha-v-ardhan.github.io/issues/new).
Any feedback is highly appreciated :)

If you liked my work, share it with your friends

Feel free to ping me on socials.

