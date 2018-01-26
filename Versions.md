Notable StepMania Versions
=======

Manias have been stepped all throughout the ages and here is a sampling of some of the versions used to do so:

Official
--------
* [StepMania 3.0](versions/stepmania-3-0)
* [StepMania 3.9](versions/stepmania-3-9)
* [StepMania 4.0 alpha](versions/stepmania-4-0-alpha)
* [StepMania 4.0 beta](versions/stepmania-4-0-beta)
* [StepMania 5.0](versions/stepmania-5-0)

## Stable
### StepMania 5.0
**StepMania 5.0.x** is the current stable release of StepMania. Based on the 4.0 alpha fork sm-ssc, it provides a number of new and improved features over 3.9, including a new default theme, a Lua backend, support for different screen aspect ratios, new features for charts (such as rolls, warps, fake arrows, and lifts), the new game mode `kb7` (inspired by games such as DJMax and o2Jam), improvements to the `pump` game mode, and other internal improvements.

## Unstable branch
### StepMania 5.1
**StepMania 5.1** (also known as [5_1-new](https://github.com/stepmania/stepmania/tree/5_1-new)) is an upcoming refresh release of the 5.0.x series, which focuses on incremental improvements and maintaining compatibility with 5.0.x content such as themes. It features a new high-definition default theme, support for loading songs out of user profiles on USB drives, and new internal features of interest to content creators, such as an expanded suite of song modifier effects and a new image caching system.

Its first public beta was officially released on January 25, 2018.

## Experimental branch
### StepMania 5.2
StepMania's master branch (also known as **StepMania 5.2**) contains bleeding edge changes to multiple core components of the game, such as a rewritten notefield and associated modifier system, a new noteskin system (which allows a single noteskin to support multiple game types), a new preferences framework, and a new Lua-based menu system with support for mouse input. Changes from 5.1, such as the new default theme, USB custom songs, and the new modifiers (implemented through a compatibility layer), are also present in this branch.

More specific details on the changes can be found in the [documentation](https://github.com/stepmania/stepmania/tree/master/Docs/Themerdocs/5.1_incompatibilities). Themes designed for 5.0 and 5.1 must be modified in order to operate correctly on these builds; in other words, it's not 100% backwards compatible.

Unofficial
----------
As StepMania is an open source project, there have been specific forks designed to serve specific niches and communities.

* StepMania AMX: A fork based on a fork of 3.9, with a particular focus on Pump it Up-related enhancements.
* Etterna: A fork based on the 5.0.x series meant to appeal to keyboard players. It focuses on advanced user interface features and in-game statistics, performance improvements, and integration with an online score tracking website. It also trims out a number of features deemed unnecessary to its target audience.
* OpenITG: A fork based on a snapshot of StepMania's CVS tree (also known as "3.95") that was used as the basis of the arcade game _In the Groove 2_. It is designed to emulate the behavior of the game, whilst adding features and enhancements of interest to arcade environments. OpenITG was intended primarily to serve as a "drop-in" replacement for the stock binary on an _In the Groove 2_ cabinet.
  * NotITG: A branch of OpenITG that adds additional modifiers and other features of interest for the creation of simfiles with scripted effects. It is distributed as an alternate binary for existing OpenITG installations.
* sm-ssc: A fork of the StepMania 4 alpha source code, created after StepMania 4 itself was shelved (and replaced by a new iteration of StepMania 4 that had more in common with 3.9 than the "StepMania 4 CVS" builds released before it). sm-ssc would later be merged into the main StepMania source tree, serving as the basis of the current StepMania 5.0.x series.
* StepF2: Another Pump it Up-focused fork, except based on StepMania 5.
* 3.9 Plus: A fork created as an alternative to StepMania 4 during its development, which focused on adding new features (including those backported from "3.95" and the StepMania 4 alphas) to the existing StepMania 3.9 version.