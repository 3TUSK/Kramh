# Schema for Minecraft Mod Artifact Resource Tracking (SMMART)

A metadata schema designed for tracking Modded Minecraft related resources,
mostly mod artifacts.

Objectives of this project are:
  - Creating a easy-to-use, intuitive format for describing mod
  - Tracking version history of mod release
  - Making large-scale mod catalog possible
  - Providing an independent model of describing a modpack

On the contrary, these are not objectives of this project:
  - Becoming a mirror on itself, or being a CurseForge replacement
  - Making yet another Minecraft launcher for Modded Minecraft players
  - Providing hosting services

### Somethings to pay attention to...

1. [RFC 2119](https://tools.ietf.org/html/rfc2119) applies here.
2. [ECMA 404](http://www.ecma-international.org/publications/files/ECMA-ST/ECMA-404.pdf) applies here.
3. [JSON Schema Draft-7](http://json-schema.org/draft-07/schema) applies on all spec files here, unless otherwise noted.

### Acknowledgements

The motivation of this project is inspired by:
  - CKAN (Comprehensive Kerbal Archiving Network) (https://github.com/KSP-CKAN/CKAN)
  - MCArchive project (https://github.com/MCArchive/metarepo)

The creation format itself is influenced by:
  - Apache Maven POM format
  - LuaRock rockspec (https://github.com/luarocks/luarocks)

Special thanks to those tools:
  - JSON Schema Tool (https://www.jsonschema.net/)
