# SMMART Specification

This document describes the entire SMMART Specification. It has three parts:

  - Core SMMART Schema, which defines a set of JSON Schemata used by other parts
    of SMMART Specification.
  - SMMART API Definition, which defines a set of HTTP endpoints that a
    SMMART-compliant service provider MUST implement.
  - Flat-File SMMART Data Representation, which defines a way to store SMMART-
    compliant data in a plain, static file system structure.

All occurrences of keywords "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT",
"SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this
specification are to be interpreted as described in [RFC 2119][rfc-2119].

## Introduction

Modded Minecraft has a rough history with the same length as that of
Minecraft itself. In the past years of community development, countless
developers have poured a substantial amount of effort into it, resulting in
a grand repository of "mods", scattered over the entire Internet.

There are still people who use terms like "The Dark Age" to refer a time period
when mod developers (often called "modders") host their mod files on various
cloud storage services such as Dropbox and MediaFire and use link-shortener
services such as adf.ly to bring them a tiny bit of income. However, the
launch of CurseForge changed the entire game: they offer mod file hosting
services for no charges, recompense modders for their work, and provide a one-
site modpack publishing service. Since then, the community started to shift
over everything to CurseForge, pushing Curse Inc. (later Twitch who acquired
Curse Inc.) to the position of a de facto standard of Modded Minecraft community.

Undeniably, CurseForge is now an indispensable part of the Modded Minecraft.
Nevertheless, CurseForge is not the entire scene of this thriving community.
There are mods that are not hosted on CurseForge, so CurseForge still has a
list of non-CurseForge mods that are allowed to be included in a CurseForge
modpack, alongside with an application mechanism for it. Mod reposting is still
relevant; while we have taken steps to confront it, verifying whether a mod jar
comes from the authentic source is still a burden, especially for an absolute
novice. Further, Modded Minecraft faces the global audience, even though English is
the conventional lingua franca in this community, users who are not proficient
in English would still be annoying.

Inspired by various package manager used by different Linux Distributions as
well as the CKAN Project from Kerbel Space Program community, the Schema for
Minecraft Mod Artifact Resource Tracking (SMMART) intends to set up a uniformed
and platform-agnostic standard to record and exchange information about the mod
files ("artifacts").

[rfc-2119]: https://tools.ietf.org/html/rfc2119
