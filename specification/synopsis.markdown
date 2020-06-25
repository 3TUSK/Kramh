# SMMART Specification

This document describes the entire SMMART Specification. It has three parts:

  - Core SMMART Schema, which defines a set of JSON Schemata used by other parts
    of SMMART Specification.
  - SMMART API Definition, which defines a set of HTTP endpoints that a 
    SMMART-compliant service provider MUST implement.
  - Flat-File SMMART Data Representation, which defines a way to store 
    SMMART-compliant data in a plain, static file system structure, for example 
    hard disk or object storage services.

All occurrences of keywords "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT",
"SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this
specification are to be interpreted as described in [RFC 2119][rfc-2119].

## Introduction

Modded Minecraft has a history with roughly the same length as that of
Minecraft itself. In the past decade of community development, countless
developers have poured a substantial amount of effort into it, resulting in
a grand repository of "mods", scattered over the entire Internet.

There are still people who use terms like "The Dark Age" to refer a time period
when mod developers (often called "modders") host their mod files on various
cloud storage services such as Dropbox and MediaFire and use link-shortener
services such as adf.ly to bring them a tiny bit of income. However, the
launch of CurseForge changed the entire game: they offer mod file hosting
services for no charges, recompense modders for their work, and provide a 
centralized modpack publishing service. Since then, the community started to 
shift over everything to CurseForge, pushing Curse Inc. (later Twitch who acquired
Curse Inc.) to the position of the de facto standard of Modded Minecraft community.

Undeniably, CurseForge is now an indispensable part of the Modded Minecraft.
Nevertheless, CurseForge is not the entire scene of this thriving community. There 
are issues that CurseForge did not or could not address:

  - There are mods that are not hosted on CurseForge, so CurseForge still has a
    list of non-CurseForge mods that are allowed to be included in a CurseForge
    modpack, alongside with an application mechanism for it. 
    As such, tracking mods that are not on CurseForge becomes a burden: they can 
    be everywhere, and it is entirely possible that one of websites we rely on 
    will be no more tomorrow. 
  - Mod reposting is still relevant. While we have taken steps to confront it, 
    verifying whether a mod jar comes from authentic sources is still a burden, 
    especially for an absolute novice.  
    Moreover, for a mod licensed under a FLOSS license, redistribution of their 
    binary executables is typically allowed, so extra data for verification purpose 
    are necessary.
  - Modded Minecraft faces global audiences. Even though conventionally English is 
    the lingua franca in this community, users who are not proficient in English 
    would still suffer from language barriers and potentially misinformation. 
    A carefully curated guide, backed by a language-agnostic catalog, would be 
    helpful to this situation.
  - Further, the sudden rising of Fabric ecosystem reminds us again that there *can* 
    be more than one modding framework in the world of modded Minecraft. Apparently, 
    CurseForge was not designed with this extreme case in mind. 
    With the fact that there are multiple mod and "plugin" frameworks co-existed, 
    we need a way to properly sort out all the mods and "plugins" we may get. 
  - Last but not least, the most recent leadership change from Twitch to Overwolf 
    set off a new wave of community unrest. We can hope the best result, but we are 
    not prophets and cannot predicate future. 
    A centralized repository has been proven as beneficial to the community, but it 
    would be a diaster when such a repository is abandoned. Decentralized repositories 
    are resilient to external changes, but it is not as convenient as a centralized one. 
    We need a repository that falls between these two approaches. 

All of these problems are pointing to a single answer:

A mod catalog and curation system within a scale-free network.

Inspired by various package manager used by different Linux Distributions as well as the 
CKAN Project from Kerbel Space Program community, the Schema for Minecraft Mod Artifact 
Resource Tracking (SMMART) intends to set up a uniformed and platform-agnostic standard 
to record and exchange information about mod files (collectively called "artifacts" 
through the entire specification), with the capability of being decentralized.

<!-- 
TODO: Maybe we can drop "Minecraft" and name this spec "Schema for Mod Artifact 
Resource Tracking", abbr. SMART. This would require decoupling from Minecraft.
-->

[rfc-2119]: https://tools.ietf.org/html/rfc2119
