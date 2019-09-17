# Core SMMART Schema

Core SMMART Schema is a set of [JSON Schema][ref-json-schema] that validates
several core JSON structures used by SMMART.

[ref-json-schema]: https://json-schema.org/

## Synopsis

The Core SMMART Schema consists of three schemata:

  - Schema for Mod Entry ("Entry Schema")
  - Schema for Mod Catalog ("Catalog Schema")
  - Schema for Mod Artifact ("Artifact Schema")

## Details

### Schema for Mod Entry

The following fields are REQUIRED:

  - `protocol` The SMMART version that applies to this metadata file.
    - MUST be a JSON String.

  - `id` The identifier that MUST uniquely distinguish a mod within the database.
    - MUST be a JSON String.
  - `name` The original, unabridged name of this mod.
    - MUST be a JSON String.

The following fields are OPTIONAL:

  - `summary` The short summary that describes the functionality of the mod.
    - MUST be a JSON String.
  - `maintainer`
    - MUST be a JSON Array consists with zero or more JSON Strings.

## Schema for Mod Catalog

The following fields are REQUIRED:

  - `protocol` The SMMART version that applies to this metadata file.
    - MUST be a JSON String.

  - `id` The identifier that MUST match a single entry of mod metadata.
    - MUST be a JSON String.
  - `versions` The list of original, unabridged version strings whose
    corresponding artifact does exist.
    - MUST be a JSON Array of JSON String.

## Schema for Mod Artifact

The following fields are REQUIRED:

  - `protocol` The SMMART version that applies to this metadata file.
    - MUST be a JSON String.

  - `id` The identifier that MUST uniquely distinguish a mod within the database.
    - MUST be a JSON String.
  - `version` The original, unabridged version string of this artifact.
    - MUST be a JSON String.

  - `license` The license that applies to this artifact.
    - MUST be a JSON String whose contents MUST comply with SPDX Specification,
      Version 2.1.

  - `checksum` The checksum of target artifact for verification purpose.
    - MUST be a JSON Object.
    - This field MUST contain a field, `sha256`, whose value MUST be the SHA-256
      checksum of target artifact in string form.
    - This field MAY contain a field, `sha1`, whose value MUST be the SHA-1
      checksum of target artifact in string form.
    - This field MAY contain a field, `md5`, whose value MUST be the MD5
      checksum of target artifact in string form.

  - `minecraft` The version of Minecraft that this artifact is targeting.
    - MUST be a JSON String.

  - `framework` The modding framework that this artifact relies on.
    - MUST be either:
      * a JSON String, that uniquely identifies a framework, or
      * a JSON `null` literal, that MUST be interpreted as "this artifacts is
        a jar mod, i.e. whose contents are expected to be included into the
        Minecraft binary executable."

  - `dependencies` The list of other artifacts that this artifact expected to
    be present in order to be functional.
    - MUST be a JSON Array of JSON String.

  - `downloads` The list of possible sources that can retrieve this artifact,
    whose checksums MUST comply with the listed checksums in this metadata file.
    - MUST be a JSON Array of JSON Objects, whose contents MUST include:
      * `url` The location that the artifact locates at.
    - Optionally, each JSON Object in that JSON Array may contain the following
      fields:
      * `type` The descriptor of `url` as described above.
