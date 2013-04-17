# avro-cli-examples

Examples on how to use the command line tools in Avro Tools to read and write Avro files.

See my original article
[Reading and Writing Avro Files From the Command Line](http://www.michael-noll.com/blog/2013/03/17/reading-and-writing-avro-files-from-the-command-line/#json-to-binary-avro)
from April 2013 for more information about using Avro Tools.

# File overview

* [twitter.avro](https://github.com/miguno/avro-cli-examples/blob/master/twitter.avro) -- data records in uncompressed
  binary Avro format
* [twitter.snappy.avro](https://github.com/miguno/avro-cli-examples/blob/master/twitter.snappy.avro) -- data records in
  Snappy-compressed binary Avro format
* [twitter.avsc](https://github.com/miguno/avro-cli-examples/blob/master/twitter.avsc) -- Avro schema (in JSON
  representation) of the data records in ``twitter.avro``, ``twitter.snappy.avro`` and ``twitter.json``.
* [twitter.json](https://github.com/miguno/avro-cli-examples/blob/master/twitter.avro) -- data records in plain-text
  JSON format


# JSON to binary Avro

Without compression:

    $ java -jar ~/avro-tools-1.7.4.jar fromjson --schema-file twitter.avsc twitter.json > twitter.avro

With Snappy compression:

    $ java -jar ~/avro-tools-1.7.4.jar fromjson --codec snappy --schema-file twitter.avsc twitter.json

If you run into ``SnappyError: [FAILED_TO_LOAD_NATIVE_LIBRARY]`` when trying to compress the data with Snappy make sure
you use JDK 6 and not JDK 7.


# Binary Avro to JSON

The same command will work on both uncompressed and compressed data.

    $ java -jar ~/avro-tools-1.7.4.jar tojson twitter.avro > twitter.json
    $ java -jar ~/avro-tools-1.7.4.jar tojson twitter.snappy.avro > twitter.json

If you run into ``SnappyError: [FAILED_TO_LOAD_NATIVE_LIBRARY]`` when trying to decompress the data with Snappy make
sure you use JDK 6 and not JDK 7.


# Retrieve Avro schema from binary Avro

The same command will work on both uncompressed and compressed data.

    $ java -jar ~/avro-tools-1.7.4.jar getschema twitter.avro > twitter.avsc
    $ java -jar ~/avro-tools-1.7.4.jar getschema twitter.snappy.avro > twitter.avsc

