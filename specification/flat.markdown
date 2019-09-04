# Flat-File SMMART Data Representation

Flat-File SMMART Data Representation is a way to structure a SMMART-compliant
database in a plain, static file system, useful for serving data on a static
website or storing data on disk.

## Directory Structure

A Flat-File SMMART Data Representation has the following directory structure:

 - `./index/`
   - `./index/mod_a/`
     - `./index/mod_a/info.json`
     - `./index/mod_a/versions.json`
     - `./index/mod_a/versions/`
       - `./index/mod_a/versions/1.0.json`
       - `./index/mod_a/versions/1.2.json`
       - ...
   - `./index/mod_b/`
     - `./index/mod_b/info.json`
     - `./index/mod_b/versions.json`
     - `./index/mod_b/versions/`
       - `./index/mod_b/versions/0.1.0.json`
       - `./index/mod_b/versions/0.1.1.json`
       - ...
   - ...

## Encoding

All files MUST be encoded in UTF-8.
