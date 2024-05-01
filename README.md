# avro-cli-examples

Examples on how to use the command line tools in [Avro Tools](http://avro.apache.org/) to read and write Avro files.

See my original article
[Reading and Writing Avro Files From the Command Line](http://www.michael-noll.com/blog/2013/03/17/reading-and-writing-avro-files-from-the-command-line/#json-to-binary-avro)
for more information on using Avro Tools.

---

Table of Contents

- <a href="#prerequisites">Getting Avro Tools</a>
- <a href="#json-to-avro">JSON to binary Avro</a>
- <a href="#avro-to-json">Binary Avro to JSON</a>
- <a href="#retrieve-avro-schema">Retrieve Avro schema from binary Avro</a>
- <a href="#related-tools">Related tools</a>

---

<a name="prerequisites"></a>

# Getting Avro Tools

You can get a copy of the latest stable Avro Tools jar file from the
[Avro Releases](https://avro.apache.org/project/download/) page.
The actual `avro-tools-*.jar` file is in the `java/` subdirectory of a given
Avro release version.

Here is a direct link to
[avro-tools-1.11.3.jar](https://dlcdn.apache.org/avro/avro-1.11.3/java/avro-tools-1.11.3.jar)
(53 MB).

```shell
# Download the Avro Tools jar to the current local directory.
# The examples below assume the jar is in the current directory.
$ curl -O -J https://dlcdn.apache.org/avro/avro-1.11.3/java/avro-tools-1.11.3.jar
```

# File overview

- [twitter.avro](twitter.avro)
  — data records in uncompressed binary Avro format
- [twitter.snappy.avro](twitter.snappy.avro)
  — data records in Snappy-compressed binary Avro format
- [twitter.avsc](twitter.avsc)
  — Avro schema of the example data
- [twitter.json](twitter.json)
  — data records in plain-text JSON format
- [twitter.pretty.json](twitter.pretty.json)
  — data records in pretty-printed JSON format

<a name="json-to-avro"></a>

# JSON to binary Avro

Without compression:

```shell
$ java -jar avro-tools-1.11.3.jar fromjson --schema-file twitter.avsc twitter.json > twitter.avro
```

With Snappy compression:

```shell
$ java -jar avro-tools-1.11.3.jar fromjson --codec snappy --schema-file twitter.avsc twitter.json > twitter.snappy.avro
```

<a name="avro-to-json"></a>

# Binary Avro to JSON

The same command works on both uncompressed and compressed data.

```shell
$ java -jar avro-tools-1.11.3.jar tojson twitter.avro > twitter.json
$ java -jar avro-tools-1.11.3.jar tojson twitter.snappy.avro > twitter.json
```

Example:

```shell
$ java -jar avro-tools-1.11.3.jar tojson twitter.avro
```

returns

```json
{"username":"miguno","tweet":"Rock: Nerf paper, scissors is fine.","timestamp": 1366150681 }
{"username":"BlizzardCS","tweet":"Works as intended.  Terran is IMBA.","timestamp": 1366154481 }
```

You can also pretty-print the JSON output with the `-pretty` parameter:

    $ java -jar avro-tools-1.11.3.jar tojson -pretty twitter.avro > twitter.pretty.json
    $ java -jar avro-tools-1.11.3.jar tojson -pretty twitter.snappy.avro > twitter.pretty.json

Example:

```shell
$ java -jar avro-tools-1.11.3.jar tojson -pretty twitter.avro
```

returns

```json
{
  "username" : "miguno",
  "tweet" : "Rock: Nerf paper, scissors is fine.",
  "timestamp" : 1366150681
}
{
  "username" : "BlizzardCS",
  "tweet" : "Works as intended.  Terran is IMBA.",
  "timestamp" : 1366154481
}
```

<a name="retrieve-avro-schema"></a>

# Retrieve Avro schema from binary Avro

The same command works on both uncompressed and compressed data.

```shell
$ java -jar avro-tools-1.11.3.jar getschema twitter.avro > twitter.avsc
$ java -jar avro-tools-1.11.3.jar getschema twitter.snappy.avro > twitter.avsc
```

Example:

```shell
$ java -jar avro-tools-1.11.3.jar getschema twitter.avro
{
  "type" : "record",
  "name" : "twitter_schema",
  "namespace" : "com.miguno.avro",
  "fields" : [ {
    "name" : "username",
    "type" : "string",
    "doc" : "Name of the user account on Twitter.com"
  }, {
    "name" : "tweet",
    "type" : "string",
    "doc" : "The content of the user's Twitter message"
  }, {
    "name" : "timestamp",
    "type" : "long",
    "doc" : "Unix epoch time in seconds"
  } ],
  "doc:" : "A basic schema for storing Twitter messages"
}
```

<a name="related-tools"></a>

# Related tools

You can also take a look at the CLI tools
[avrocat](https://github.com/apache/avro/blob/trunk/lang/c/src/avrocat.c),
[avromod](https://github.com/apache/avro/blob/trunk/lang/c/src/avromod.c), and
[avropipe](https://github.com/apache/avro/blob/trunk/lang/c/src/avropipe.c) that are part of the Avro suite.
You must build these tools yourself by following their respective
[INSTALL](https://github.com/apache/avro/blob/trunk/lang/c/INSTALL) instructions.
