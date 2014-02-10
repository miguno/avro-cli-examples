# avro-cli-examples

Examples on how to use the command line tools in Avro Tools to read and write Avro files.

See my original article
[Reading and Writing Avro Files From the Command Line](http://www.michael-noll.com/blog/2013/03/17/reading-and-writing-avro-files-from-the-command-line/#json-to-binary-avro)
from April 2013 for more information about using Avro Tools.


# Getting Avro Tools

You can get a copy of the latest stable Avro Tools jar file from the
[Avro Releases](http://avro.apache.org/releases.html#Download) page.  The actual file is in the `java` subdirectory
of a given Avro release version.

Here is a direct link to [avro-tools-1.7.6.jar](http://www.us.apache.org/dist/avro/avro-1.7.6/java/avro-tools-1.7.6.jar)
(12 MB) on the US Apache mirror site.


# File overview

* [twitter.avro](https://github.com/miguno/avro-cli-examples/blob/master/twitter.avro)
  -- data records in uncompressed binary Avro format
* [twitter.snappy.avro](https://github.com/miguno/avro-cli-examples/blob/master/twitter.snappy.avro)
  -- data records in Snappy-compressed binary Avro format
* [twitter.avsc](https://github.com/miguno/avro-cli-examples/blob/master/twitter.avsc)
  -- Avro schema of the example data
* [twitter.json](https://github.com/miguno/avro-cli-examples/blob/master/twitter.json)
  -- data records in plain-text JSON format
* [twitter.pretty.json](https://github.com/miguno/avro-cli-examples/blob/master/twitter.pretty.json)
  -- data records in pretty-printed JSON format


# JSON to binary Avro

Without compression:

    $ java -jar ~/avro-tools-1.7.6.jar fromjson --schema-file twitter.avsc twitter.json > twitter.avro

With Snappy compression:

    $ java -jar ~/avro-tools-1.7.6.jar fromjson --codec snappy --schema-file twitter.avsc twitter.json


# Binary Avro to JSON

The same command will work on both uncompressed and compressed data.

    $ java -jar ~/avro-tools-1.7.6.jar tojson twitter.avro > twitter.json
    $ java -jar ~/avro-tools-1.7.6.jar tojson twitter.snappy.avro > twitter.json

Output:

```json
{"username":"miguno","tweet":"Rock: Nerf paper, scissors is fine.","timestamp": 1366150681 }
{"username":"BlizzardCS","tweet":"Works as intended.  Terran is IMBA.","timestamp": 1366154481 }
```

You can also pretty-print the JSON output with the  `-pretty` parameter:

    $ java -jar ~/avro-tools-1.7.6.jar tojson -pretty twitter.avro > twitter.pretty.json
    $ java -jar ~/avro-tools-1.7.6.jar tojson -pretty twitter.snappy.avro > twitter.pretty.json

Output:

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


# Retrieve Avro schema from binary Avro

The same command will work on both uncompressed and compressed data.

    $ java -jar ~/avro-tools-1.7.6.jar getschema twitter.avro > twitter.avsc
    $ java -jar ~/avro-tools-1.7.6.jar getschema twitter.snappy.avro > twitter.avsc

[![githalytics.com alpha](https://cruel-carlota.pagodabox.com/d1bb6d38b2ac73e2f46a6fc29a3a249e "githalytics.com")](http://githalytics.com/miguno/avro-cli-examples)
